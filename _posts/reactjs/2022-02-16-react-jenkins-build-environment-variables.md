---
title:  "[react] 젠킨스로 CD 구축하여 ec2 배포시 .env file 위치"

categories:
  - reactjs 
tags:
  - [react,jenkins,CI/CD,build]

toc: true
toc_sticky: true

date: 2022-02-16

---

### 문제상황

react 로 프로젝트를 진행한 후 Jenkins 를 통해 CD 를 구축하였다. 
Jenkins 에서 하는일은 git 을 clone 하여 빌드를 한 뒤, 빌드한 결과물을 ec2 에 nginx 가 바라보는 폴더안에 복제시켜주는것이다.

이미지업로드 기능을 구현하기 전에는 몰랐었지만, 이미지업로드를 S3 를 통해 구현하면서 S3 에 관한 ACCESS_KEY 들을 .env 를 통해서 관리해야할 필요가 생겨났다.
보안정보이므로 레포지토리에 .env 자체를 올릴수는 없었다. 로컬에서는 client 폴더 안에 .env file 을 위치시켰지만, 배포하면 어디에 위치시켜야할지 고민을 하게 되었다.



***
<br>

    🌜 주관적인 견해가 담긴 글입니다. 다양한 의견이 있으실 경우
    언제든지 댓글 혹은 메일로 지적해주시면 감사하겠습니다! 😄

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}

