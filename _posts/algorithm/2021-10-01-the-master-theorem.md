---
title:  "[Algorithm] The Master Theorem(Divide and conquer) "

categories:
  - algorithm
tags: 
  - [masterTheorem,master,algorithm]

toc: true
toc_sticky: true


---

***
이 **포스트**는 한양대학교 김태형 교수님의 **알고리즘 설계와 분석** 과목의 **강의** 와 **강의자료**를 참고하였습니다.
이 포스트에서 사용하는 **divide-and-conquer** 에 대한 설명은 [포스트](https://chanhyukpark-tech.github.io/algorithm/Divide-and-conquer/) 를 참고해주세요.

***

## The Master Theorem
일반적인 형태로 나타난 점화식을 쉽게 풀 수 있는 방법이있다.
물론 이 방법이 적용되지 않는 문제가 있고, 그러한 문제들은 점화식을 수학적으로 풀어야하는 방법 뿐이다.
일반형이 a와 b 를 변수로 하는 꼴로 나타내져있다.

![image](https://user-images.githubusercontent.com/69495129/135611508-6ad83e21-4923-432c-9332-9b40512ae3b1.png)
세 가지의 Condition 이 존재한다. 

f(n) 의 order 와 n^(logba) 의 order 를 비교하는 과정은 공통적이다.  

아래 여러가지 예시가 있다. 기초 수학이 필요하다.

![image](https://user-images.githubusercontent.com/69495129/135614725-7675ee33-02bd-4f22-b772-45bf5921068e.png)
![image](https://user-images.githubusercontent.com/69495129/135614753-5799937a-6208-48bf-aeec-c1a69c799280.png)
![image](https://user-images.githubusercontent.com/69495129/135614768-f6d9b873-4a6c-4111-a735-45fb5c9f7796.png)
![image](https://user-images.githubusercontent.com/69495129/135614791-c93cb3ba-2642-49f9-a5e8-db4f9fa72143.png)
![image](https://user-images.githubusercontent.com/69495129/135614818-56c95b50-72d8-4fe2-bbff-df38d957c27b.png)


## Summary
- Master Theorem 적용불가능한 문제의 Check를 잘해야한다.

*** 
<br>

    🌜 주관적인 견해가 담긴 정리입니다. 다양한 의견이 있으실 경우
    언제든지 댓글 혹은 메일로 지적해주시면 감사하겠습니다! 😄

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}
