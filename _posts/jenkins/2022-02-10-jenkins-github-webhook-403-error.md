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
오류 내용을 확인하기위해서 github webhook section 을 살펴봤다.



***
<br>

    🌜 주관적인 견해가 담긴 글입니다. 다양한 의견이 있으실 경우
    언제든지 댓글 혹은 메일로 지적해주시면 감사하겠습니다! 😄

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}

