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


### 생각

- 처음에는 ec2 ubuntu 내의 다른곳에 .env file 을 생성하고 그것을 참조하려고 했다. 하지만 react code 인 process.env 로 어느 파일을 참조해야할지 정확한 답을 찾을 수 없는 상황이였다.

- 젠킨스를 통해서 빌드하는 과정 어디선가 환경변수를 주입해주는 방법을 찾으면 될 것 같았다. (깃에는 안올라가있으니깐 주입을해줘야한다)

- netlify 나 vercel heroku 는 항상 매개변수를 대시보드에서 주입해준것이 떠올랐다.


### 해결방법

프론트엔드 개발자신 [김민수](https://github.com/minsoo-web) 님에게 이런상황애 .env file 을 어디서 관리하는지 여쭤봤는데 정확한 해결법을 주셨다....

![image](https://user-images.githubusercontent.com/69495129/154199265-70d92669-59c0-4893-87fe-36cbb02d179e.png)

젠킨스에서 매개변수를 설정할 수 있다고 하셨다. 당연히 빌드를 하는 곳이니 매개변수를 설정할 수 있는게 맞다...

젠킨스의 파이프라인 => 구성을 들어가면 이름과 값을 설정할 수 있다.

![image](https://user-images.githubusercontent.com/69495129/154199423-3f517e71-259c-4391-8496-bedf14572961.png)


그 후 빌드하는 과정에서 이 매개변수를 





***
<br>

    🌜 주관적인 견해가 담긴 글입니다. 다양한 의견이 있으실 경우
    언제든지 댓글 혹은 메일로 지적해주시면 감사하겠습니다! 😄

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}

