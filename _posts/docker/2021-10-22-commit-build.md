---
title:  "[Docker🐳] Commit & Build "

categories:
  - docker
tags:
  - [docker,commit,build]

toc: true
toc_sticky: true


---

# Docker Commit & Build
개인적으로 공부하면서 참조하려고 만든 포스트입니다.
유튜브 생활코딩 님의 강의를 참고하였습니다.

![image](https://user-images.githubusercontent.com/69495129/138320009-3e65c84c-f64a-44af-884a-70b381a372e1.png)


>개인적으로 도커 공부를하면서 image 를 만들기 위해서 commit 을 사용할 경우도 있고 build를 사용할 
>경우도 있어서 이 둘의 차이점은 image를 만드는데 어떤것인가에 대해서 의문점을 갖게 되었다.

## commit
우리가 사용하고있는 container 에서 commit 명령어를 사용하면 명령어에 의해서 container 가 image가 된다

## Build
`Dockerfile` 을 작성한다.  그 후 build 명령을 내리면 docker 는 dockerfile 을 바탕으로 새로운 image를 만들게된다.


## 차이점
둘다 결과적으로는 image 를 만든다
`commit` 은 이미 사용중인 container 가 있을때 그것을 image로 바꾸는 backup 의 느낌
`build` 는 구체적으로 시간의 순서에 따라 기록해서 만드는 image를 생성하는 느낌

>하지만 결과적으로는 image 가 만들어진다



## Summary
- 결과적으로는 둘다 image를 생성하는 방법이다.
- commit 은 backup build 는 create 라고 기억하면 좋을 것 같다.
- 이해하면 당연하게 여겨진다.

***
<br>

    🌜 주관적인 견해가 담긴 글입니다. 다양한 의견이 있으실 경우
    언제든지 댓글 혹은 메일로 지적해주시면 감사하겠습니다! 😄

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}

