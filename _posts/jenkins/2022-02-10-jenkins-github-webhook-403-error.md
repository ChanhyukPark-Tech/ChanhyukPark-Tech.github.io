---
title:  "[jenkins] Jenkins - Github 웹훅 설정 에러(HTTP ERROR 403 No valid crumb was included in the request) "

categories:
  - jenkins
tags:
  - [jenkins,webhook,gitHub]

toc: false
toc_sticky: false


---

최근 진행하고 있는 서버통합 프로젝트에서 젠킨스를 이용한 Continuous Deployment 를 구축해야하는 상황이 있었다.
jenkinsfile 을 잘 구축하여 수동배포는 잘 되었지만, CD 의 꽃인 push를 하면 그것을 hook으로 가로채서 jenkins 가 자동으로 빌드해주지는 못하는 오류가 발생하였다.
오류 내용을 확인하기위해서 github webhook section 을 살펴봤다. (Settings => Webhooks)

![image](https://user-images.githubusercontent.com/69495129/153365916-775b8e86-0c5e-45bb-a5e5-371c87c56481.png)

이런식으로 훅을 가로채는것이 실패했다는것을 볼 수 있고 클릭하여 상세로그를 확인하였다.

![image](https://user-images.githubusercontent.com/69495129/153365995-9f166e0e-14fc-465e-bc4a-f499d9c6cf70.png)

젠킨스로 보내고 받은 Response 를 살펴보면 위 이미지와 같다.
주요 에러로그는 다음과같다.

> Error 403 No valid crumb was included in the request

위 문제를 해결하기 위해서 스택오버플로우 및 구글링을 해봤지만 다 한가지 해결법만 제시해줬다.

## 첫번째 해결법

> jenkins configure global security 수정

configure global security ->
![image](https://user-images.githubusercontent.com/69495129/153366289-744308ba-dc10-469b-9d8c-04875e2646fe.png)

위 그림과 같이 설정해준다. 저는 이 방법으로 해결 안됐습니다.


## 내가 찾은 해결법

다들 위 첫번째 해결법으로 해결이 되는것 같은데 저는 해결이 안되어서 다른 방법을 시도했습니다.
jenkins 는 수많은 plugin 을 지우너하고 그중에 Strict Crumb Issuer 라는 플러그인을 설치해서 해결합니다 
설치후 아까 위 이미지의 CSRF Protection 에 한가지 더 메뉴가 생기고 다음과 같이 세팅을 해줍니다.

![image](https://user-images.githubusercontent.com/69495129/153366479-b749a337-98f9-4f9d-9cf1-fa12cfa53a1f.png)

Check the session ID 의 체크를 풀어줍니다.!

다음 자신의 프로필을 클릭합니다(우측상단) 그 후 설정을 들어갑니다. 자신의 프로필에 대한 설정입니다

![image](https://user-images.githubusercontent.com/69495129/153366603-0fbcce05-2cf7-4181-9786-a704e19f9148.png)

API TOKEN 을 발급 받아서 안전하게 저장해둡시다. 이것을 github 에 말해줌으로써 github 와 jenkins 를 연결시켜주도록 합니다.


![image](https://user-images.githubusercontent.com/69495129/153366782-61332455-0542-48a8-9755-92d011b7a8dd.png)

위 이미지대로 입력하시면됩니다.

저는 위 방법그대로 했는데도 안되서 혹시나해서 눈 다시 뜨고 주소를 확인해보니...
http:// 저의주소/github-webhook/ 으로 해야하는데 http:// 저의주소/git-webhook/ 라고 입력되어있더라고요.. 
`http:// 저의주소/github-webhook/` 로 해야합니다.



### 참고자료

- [honeyinfo7](https://honeyinfo7.tistory.com/293)

***
<br>

    🌜 주관적인 견해가 담긴 글입니다. 다양한 의견이 있으실 경우
    언제든지 댓글 혹은 메일로 지적해주시면 감사하겠습니다! 😄

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}

