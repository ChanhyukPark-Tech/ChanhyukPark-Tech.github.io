---
title:  "[jenkins] Cannot run program "nohup" "

categories:
  - jenkins
tags:
  - [jenkins,nohub,git-bash]

toc: false
toc_sticky: false


---

젠킨스를 Window 10 환경에서 build 하려했지만 계속 nohup 이라는 프로그램을 찾지 못하는 문제가 발생했다.

>	Cannot run program "nohup" (in directory "C:\Users\chanhyuk-tech\AppData\Local\Jenkins\.jenkins\workspace\portfolio-react-app\client"): CreateProcess error=2, 지정된 파일을 찾을 수 없습니다

나와같은 경우는 이렇게 에러가나왔고 환경변수로 Git/bin 을 추가해줘도 계속 오류가 났다. 
최종 해결방법은 link 를 시켜줘야 해결이된다.

>mklink "C:\Program Files\Git\bin\nohup.exe" "C:\Program Files\git\usr\bin\nohup.exe"

>mklink "C:\Program Files\Git\bin\msys-2.0.dll" "C:\Program Files\git\usr\bin\msys-2.0.dll"

>mklink "C:\Program Files\Git\bin\msys-iconv-2.dll" "C:\Program Files\git\usr\bin\msys-iconv-2.dll"

>mklink "C:\Program Files\Git\bin\msys-intl-8.dll" "C:\Program Files\git\usr\bin\msys-intl-8.dll"

윈도우 Cmd 를 관리자 권한으로 실행한뒤 위와같이 4번 입력해주면 link 가 형성되고 nohup 프로그램을 잘 찾아서
jenkins 를 사용할 수 있다!


***
<br>

    🌜 주관적인 견해가 담긴 글입니다. 다양한 의견이 있으실 경우
    언제든지 댓글 혹은 메일로 지적해주시면 감사하겠습니다! 😄

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}

