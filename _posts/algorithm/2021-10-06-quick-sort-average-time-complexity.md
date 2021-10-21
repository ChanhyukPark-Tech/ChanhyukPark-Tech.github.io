---
title:  "[Algorithm] QuickSort Average TimeComplexity Proof "

categories:
  - algorithm
tags: 
  - [quicksort,timeComplexity,algorithm]

toc: true
toc_sticky: true


---

***
이 **포스트**는 한양대학교 김태형 교수님의 **알고리즘 설계와 분석** 과목의 **강의** 와 **강의자료**를 참고하였습니다.
이 포스트에서 사용하는 **divide-and-conquer** 에 대한 설명은 [divide and conquer 에 대한 설명](https://chanhyukpark-tech.github.io/algorithm/Divide-and-conquer/) 를 참고해주세요.
이 포스트에서 사용하는 **quickSort** 에 대한 설명은 [quickSort에 대한 설명](https://chanhyukpark-tech.github.io/algorithm/quicksort/) 를 참고해주세요.

***

사람들은 일반적인 정렬 알고리즘을 사용할때 quick sort를 가장 많이 사용한다고 알려져있다. 이전 포스트에서 quick sort 의 worst time complexity 가 O(n^2) 인 사실을 증명하였다. 다른 알고리즘과는 다르게
평균적인 시간복잡도를 살펴보자.


![image](https://user-images.githubusercontent.com/69495129/136181481-eea3d2d3-6c55-4444-b4b9-1d2ca4971ca5.png)
![image](https://user-images.githubusercontent.com/69495129/136181507-ab6ebc85-dba2-4f71-91ad-8a7073acd024.png)
![image](https://user-images.githubusercontent.com/69495129/136181534-88205d3d-70fd-4551-b407-b2f23954bb5f.png)
![image](https://user-images.githubusercontent.com/69495129/136181553-4a0c21c5-a428-41f0-82c1-b89d505bf5f2.png)
![image](https://user-images.githubusercontent.com/69495129/136181571-4952e939-7a33-42bb-b49e-727b33cda1f0.png)

<br>
중간중간에 몇개의 테크닉이 사용되지만 그렇게 어려운 부분이아니다. 차근차근 점화식을 풀어나가면 우리가 원하는 시간복잡도를 얻을 수 있다.


## Summary
- quick sort 는 가장 빠른 알고리즘으로 알려져있다.
- 평균적인 시간 복잡도를 고려해야 하는 경우도 있다.

*** 
<br>

    🌜 주관적인 견해가 담긴 정리입니다. 다양한 의견이 있으실 경우
    언제든지 댓글 혹은 메일로 지적해주시면 감사하겠습니다! 😄

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}
