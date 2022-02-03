---
title:  "[react] 리액트 웹소켓 Websocket - sockjs - InvalidStateError: The connection has not been established yet "

categories:
  - reactjs 
tags:
  - [react, webSocket,sockjs]

toc: true
toc_sticky: true

date: 2022-02-03

---

프로젝트로 리액트에서 웹소켓을 이용할 일이 있었다. 백엔드는 스프링으로 구현되어있기 떄문에 스프링에 최적화된 stomp 를 사용했다.
잘 연결됐다 싶었는데 메세지를 보낼때마다 아래와 같은 오류가 계속 발생했다.

```
Websocket - sockjs - InvalidStateError: The connection has not been established yet
```

메시지를 보내는 부분의 코드는 다음과 같다.

```typescript
const sendMessage =  () => {
        // Todo : axios

            stompClient.send("/pub/messages", {}, JSON.stringify({
                "message": message,
                "senderId": 7,
                "receiverId": 14,
                "roomId": 5,
            }));
        }
        setMessage("");
    };
```

위 처럼 코드를 작성하니 메세지를 보내는 trigger 를 발생시킬때마다 위와같은 오류가 나왔다.

async await 도 사용해보고 여러가지 찾아본결과 임의로 시간을 지연시키는 등 편법을 써봤지만 
오류해결에는 도움이 안되었다. 

위 에러문구를 잘 해석해보면 아직 웹소켓이 준비가 되지않았는데, 계속 trigger 를 시키니깐 오류가 난것이였다.
여러가지 찾아본 결과 Stomp.Client 안에는 ws.readyState 라는 integer 값이 있으며, 연결되었을 경우에(준비가된 경우) 1을 반환한다고 한다.
그 사실을 이용해서 새로운 함수를 만들어줬다! 이 함수를 이용해서 기존의 send 를 감싸줄 것이다! 코드는 직관적이다.

```typescript
// 웹소켓이 연결될 때 까지 실행하는 함수
    function waitForConnection(stompClient:Stomp.Client, callback :any) {
        setTimeout(
            function () {
                // 연결되었을 때 콜백함수 실행
                if (stompClient.ws.readyState === 1) {
                    callback();
                    // 연결이 안 되었으면 재호출
                } else {
                    waitForConnection(stompClient, callback);
                }
            },
            1 // 밀리초 간격으로 실행
        );
    }
```


아까 send 만 있던 함수를 새롭게 정의한 waitForConnection 함수로 감싸주자


```typescript
const sendMessage =  () => {
        // Todo : axios

        waitForConnection(stompClient,function() {
            stompClient.send("/pub/messages", {}, JSON.stringify({
                "message": message,
                "senderId": 7,
                "receiverId": 14,
                "roomId": 5,
            }));
        })
        setMessage("");
    };
```

위처럼하면 몇번이고 메세지를 보내도 아까와 같은 오류가 뜨지 않는것을 확인했다!

프로젝트가 끝나면 전체 웹소켓에 대한 글을 작성하겠습니다.


***
<br>

    🌜 주관적인 견해가 담긴 글입니다. 다양한 의견이 있으실 경우
    언제든지 댓글 혹은 메일로 지적해주시면 감사하겠습니다! 😄

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}

