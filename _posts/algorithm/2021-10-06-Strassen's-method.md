---
title:  "[Algorithm] Strassen's method "

categories:
  - algorithm
tags: 
  - [Strassen,matrix,multiplication]

toc: true
toc_sticky: true


---

***
이 **포스트**는 한양대학교 김태형 교수님의 **알고리즘 설계와 분석** 과목의 **강의** 와 **강의자료**를 참고하였습니다.
이 포스트에서 사용하는 **divide-and-conquer** 에 대한 설명은 [divide and conquer 에 대한 설명](https://chanhyukpark-tech.github.io/algorithm/Divide-and-conquer/) 를 참고해주세요.

**

Standary matrix multiplication 을 사용하면 다음과 같은 Pseudocode 를 작성할 수 있고 시간 복잡도는 cubic 이므로 배우 비싼 알고리즘이다.
![image](https://user-images.githubusercontent.com/69495129/136182308-c33f44bf-646d-44d3-bc6e-7b00d1d5c8ab.png)

이러한 비싼 행렬곱의 알고리즘 문제를 해결하기 위해서 Strassen's Method가 나왔다.

![image](https://user-images.githubusercontent.com/69495129/136182405-5230bd9b-98ab-41ec-8791-d6e4e30370db.png)
![image](https://user-images.githubusercontent.com/69495129/136182421-1d2ab396-f388-482d-a8fc-17e891e69ea5.png)

위 그림과 같이 m1~m7을 정의함으로써 그를 활용(이용) 하여 두 NxN 의 행렬곱을 수행 할 수 있다.
위 그림은 원소를 곱하는것을 나타낸 그림이다. 우리는 divide and conquer방식을 사용할것이므로 하나의 행렬을 더 작은행렬로 나누면서 strassen's method 를 사용할것이다.
위는 원소를 곱하는 연산이였다면 아래는 행렬을 곱하는 연산이다.

![image](https://user-images.githubusercontent.com/69495129/136182580-134dee32-9402-48b2-bbef-32f1cc538e0a.png)

## Strassen's Algorithm
- Problem : Determine the product of two n x n matrices where n is a power of 2
- Inputs : An integer n that is a power of 2, and two n x n matrices A and B.
- Outputs : the product C of A and B
![image](https://user-images.githubusercontent.com/69495129/136182858-24f822c2-b94a-4e61-a7ba-960d13b9b366.png)

위 그림에서 주석처리된 strassen을 재귀적으로 호출한 부분은 그림에서는 m1 만 표현을 하였지만 아랫부분에 m2,m3,m4,m5,m6,m7 이 생략되어있다고 보면된다.
strassen's method 는 한개의 행렬을 four submatrices 로 나눈다.
특정 threshold 아래에서는 우리가 알고있는 cubic time complexity 를 갖는 standary matrix multiplication algorithm 을 사용하는 것이 더 효율적이다.

![image](https://user-images.githubusercontent.com/69495129/136183169-750511b1-d0b8-447e-be6f-68ef0b933d2f.png)
![image](https://user-images.githubusercontent.com/69495129/136183196-13c33a43-9470-4ea0-9822-09d8820b546a.png)

하나의 원소끼리의 곱은 7번 합/차는 18번 일어난다.
![image](https://user-images.githubusercontent.com/69495129/136183502-1b48afb5-d804-4d26-8959-6e3248e00dcb.png)

분홍색이 합/차 초록색이 곱을 나타낸다.
즉 우리는 n의 지수를 살펴보면 일반적인 행렬곱에서의 지수승 3 에서 2.81로 감소시켰기 때문에 발전시켰다고 할 수 있다.


## Summary
- 현재 Coppersmith and Winograd (1987) 이라는 사람이 지수승을 2.38까지 감소시켰다
- However, the constant is so large that Strassen’s algorithm is usually more efficient unless the size of n is excessively large.- 
- No 세타(n2) algorithm has been designed.
- Nobody proved that it’s impossible!
*** 
<br>

    🌜 주관적인 견해가 담긴 정리입니다. 다양한 의견이 있으실 경우
    언제든지 댓글 혹은 메일로 지적해주시면 감사하겠습니다! 😄

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}
