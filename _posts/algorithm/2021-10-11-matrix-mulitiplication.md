---
title:  "[Algorithm] 동적계획법 (DP)_연쇄행렬곱셈 "

categories:
  - algorithm
tags: 
  - [dynamic programming,matrix,algorithm]

toc: true
toc_sticky: true


---

***

# Problem Description
행렬의 연산은 앞의 행렬이 pxq 행렬 뒤의 행렬이 qxr 인 행렬일때 O(pqr) 번의 기본연산을 수행해서 곱셈을한다. 이때 이번문제에서는 어떻게 해서 행렬의 곱셈을 하는데 기본연산을 적게할 것인가가 아닌
어떻게 하면 행렬의 곱셈에 필요한 기본연산을 적게 할 수 있을까에 대한 문제이다.
즉 행렬은 교환 법칙이 성립하지 않고, 기본연산의 총횟수가 최소가 되는 곱셈 순서(괄호 치기) 를 찾는 문제이다.

# Approach
![image](https://user-images.githubusercontent.com/69495129/137114027-8842266b-17af-4ab1-ae9d-41cfa089d0c1.png)



# Solution

![image](https://user-images.githubusercontent.com/69495129/137114052-8b0199cd-941c-4be9-9a21-ac45a5f7dbc2.png)

# Time Complexity

총 DP Table 의 칸의 개수는 n^2 개이다. 한개의 칸을 채울때 필요한 연산의 개수를 세워보자. 최악의 경우 즉 우리가 찾는 DP[1][6] 의 경우가 가장 많은 연산을 요구할것이다. 그때는 k가 1에서부터 j 가지 
모든 경우를 계산한 후 그것에 minimum 값을 찾아야한다. 
즉 우리는 n^2 칸이 있고 , 한개의 칸을 채울때 최악의 경우 n 번의 연산을 해야하므로 O(n^3) 의 Time Complexity 를 갖는다고 할 수 있다.

## Summary
- 행렬의 곱셈을 연산할때 최소를 찾는것이 아닌, 주어진 행렬들의 곱을 최소의 연산으로 수행하는 최소횟수를 구하는 알고리즘이다.
*** 
<br>

    🌜 주관적인 견해가 담긴 정리입니다. 다양한 의견이 있으실 경우
    언제든지 댓글 혹은 메일로 지적해주시면 감사하겠습니다! 😄

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}
