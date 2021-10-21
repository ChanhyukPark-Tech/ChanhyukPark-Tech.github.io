---
title:  "[Algorithm] Mergesort(Divide and conquer) "

categories:
  - algorithm
tags:
  - [divide,conquer,mergesort]

toc: true
toc_sticky: true


---

***
이 **포스트**는 한양대학교 김태형 교수님의 **알고리즘 설계와 분석** 과목의 **강의** 와 **강의자료**를 참고하였습니다.
이 포스트에서 사용하는 **divide-and-conquer** 에 대한 설명은 [포스트](https://chanhyukpark-tech.github.io/algorithm/Divide-and-conquer/) 를 참고해주세요.

***

## Mergesort

- Problem
  - Sort n keys in nondecreasing order.
- Inputs(parameters)
  - Positive integer n, array of keys S indexed from 1 to n.
- Outputs
  - The array S containing the keys in nondecreasing order.
- Design Strategy
  - **Divide** the array into two subarrays each with n/2 items.
  - **Conquer** (solve) each subarray by sorting it. Unless the array is sufficiently small, use recursion to do this.
  - **Combine** the solutions to the subarrays by merging them into a single sorted array.

> Array 의 length가 1인경우 즉 원소의 개수가 1인 배열인 형태일 때 Conquer 되었다고 한다.




```pseudocode
void mergesort(int n, keytype S[])

{
  if (n>1){
    const int h = celing(n/2) , m = n - h;
    keytype U[1..h], V[1..m];
    copy S[1] through S[h] to U[1] through U[h];
    copy S[h+1] through S[n] to V[1] through V[m];
    
    mergesort(h,U);
    mergesort(m,V);
    merge(h,m,U,V,S);
  }
}
```
```pseudocode
void merge(int h, int m, const keytype U[], const keytype V[], const keytype S[])
{
  index i=1,j=1,j=1;
  while( i <=h && j <= m ){
    if(U[i] < V[j]) {
      S[k] = U[i];
      i++;
    }else{
      S[k] = V[j];
      j++;
    }
  }
  if( i > h )
    copy V[j] through V[m] to S[k] through S[h+m];
  else  
    copy U[i] through U[h] to S[k] through S[h+m];
}

```

### Image

![image](https://user-images.githubusercontent.com/69495129/135615074-95eddfed-77a8-4f74-8a31-73da45d7e79e.png)

### Table 


|  k   |        U        |        V        |           S (Result)            |
| ---  |  -------------  |  -------------  |  -----------------------------  |
|  1   | **10** 12 20 27 | **13** 15 22 25 |               10                |
|  2   | 10 **12** 20 27 | **13** 15 22 25 |              10 12              |
|  3   | 10 12 **20** 27 | **13** 15 22 25 |            10 12 13             |
|  4   | 10 12 **20** 27 | 13 **15** 22 25 |           10 12 13 15           |
|  5   | 10 12 **20** 27 | 13 15 **22** 25 |         10 12 13 15 20          |
|  6   | 10 12 20 **27** | 13 15 **22** 25 |        10 12 13 15 20 22        |
|  7   | 10 12 20 **27** | 13 15 22 **25** |      10 12 13 15 20 22 25       |
|  -   | 10 12 20 **27** |   13 15 22 25   | 10 12 13 15 20 22 25 27 < Final |




## Time Complexity : Merge
- Basic operation : the comparision of U[i] and V[j].
- Input size: h, and m , the number of items in each of the two input arrays.
- Analysis:
  - Worst case : when i = h, and j = m - 1.
  - W(h,m) = h + m - 1.
  - 양쪽 배열의 크기가 각각 h 개 m 개 있고 한개한개씩 끝까지 비교한다고 하면(최악의 상황) 총 h+m 개수이므로 h+m-1 번의 연산이 필요하다.

## Worst-Case Time Complexity:
- Basic operation : the comparison that takes place in merge.
- Input size: n. the number of items in the array S.
- Analysis:
  - W(h,m) = W(h) + W(m) + h + m - 1 .
    - W(h) is the time to sort U.
    - W(m) is the time to sort V.
    - h + m - 1 is the time to merge.
  - W(n) = 2W(n/2) + n - 1
  - W(1) = 0
  - W(n) = θ(nlogn)

## Space Complexity Analysis
- in-place sort
  - A sorting algorithm that does not use any extra space beyond that needed to store the input.
  - Mergesort() is not an in-place sorting algorithm.
  - New arrays U and V will be created when mergesort is called.
  - The total number of extra array items created is 2n
  - In other words,the space complexity is θ(n)
  - We may reduce the extra space to n (쥐어짜기)
  - But it is not possible to make mergesort algorithm to be an in-place sort.

### why 2n?
The total number of extra array items created is 2n
길이가 n 인배열을 merge sort 하기 위해 길이가 n/2 인 배열 2개로 나눠야하고 
길이가 n/2 인 배열을 merge sort하기 위해 길이가 n/4 인 배열 2개로 나눠야한다..
이 모든걸 합치면 n+n/2+n/4 .... = 2n 이 된다. 
즉 상수부분이 2이고 이것을 더 좋게하면 상수를 1로 만들어서 n 으로 만들 수 있다. 하지만 Big-O 표기상으론 같은 Order라는 사실을 잊지말자
즉 in-place sort 가 아니라는 사실은 여전하다.


```pseudocode
void mergsort2 (index low, index high){
  index mid;
  if(low < high){
    mid = ( low + high ) / 2;
    mergesort2(low,mid);
    mergesort2(mid+1,high);
    merge2(low,mid,high);
  }
} 
```
```pseudocode
void merge2(index low, index mid, index high) 
   {
     index i=low, j=mid+1, k=low;  
     keytype U[low..highwhile (i <= mid && j <= high)
   {
     if (S[i] < S[j]) { U[k] = S[i]; i++; |else { U[k] = S[j]; j++;  }k++;
   }
     if (i > mid)
       copy S[j] through S[high] to U[k] through U[high];
     else
       copy S[i] through S[mid] to U[k] through U[high];
       copy U[low] through U[high] to S[low] through S[high];
   }

```
*** 
<br>

    🌜 주관적인 견해가 담긴 정리입니다. 다양한 의견이 있으실 경우
    언제든지 댓글 혹은 메일로 지적해주시면 감사하겠습니다! 😄

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}
