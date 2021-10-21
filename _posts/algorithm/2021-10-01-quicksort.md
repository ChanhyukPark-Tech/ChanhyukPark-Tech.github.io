---
title:  "[Algorithm] Quicksort(Divide and conquer) "

categories:
  - algorithm
tags:
  - [Quicksort,algorithm,partition]

toc: true
toc_sticky: true


---

***
이 **포스트**는 한양대학교 김태형 교수님의 **알고리즘 설계와 분석** 과목의 **강의** 와 **강의자료**를 참고하였습니다.
이 포스트에서 사용하는 **divide-and-conquer** 에 대한 설명은 [포스트](https://chanhyukpark-tech.github.io/algorithm/Divide-and-conquer/) 를 참고해주세요.

***

## Quicksort

- C.A.R Hoare(1962) 가 개발한 정렬 알고리즘
- quick sort 는 instable sorting algorithm 이다.
- divide-and-conquer algorithm 의 하나이다 
- **평균**적으로 매우 빠른 수행속도를 갖는다.


```pseudocode
void quicksort(index low, index high)
{
  index pivotpoint;
  if (high > low) 
    {
      partition(low,high,pivotpoint);
      quicksort(low,pivotpoint-1);
      quicksort(pivotpoint+1,high);
    }
}
```


## Image
merge sort 는 combine 하면서 정렬이 되는 반면 quicksort 는 나눠지면서 정렬이 되는것을 볼 수 있다(피벗을 중심으로 왼쪽 오른쪽). 
즉 merge sort 는 combine 이 중요한 algorithm 이고 quicksort 는 divide 가 중요한 algorithm 이다.

![image](https://user-images.githubusercontent.com/69495129/135615815-6182a937-eeb6-4113-b777-3802f676561a.png)

## Partitioning Algorithm

```pseudocode
void partition (index low, index high, index& pivotpoint) {
	index i, j; 
    keytype pivotitem;pivotitem = S[low];// Choose first item for pivotitem
    j = low;
    for(i = low + 1; i <= high; i++)
    	if (S[i] < pivotitem) {
    	j++;exchange S[i] and S[j];
    	}
    	pivotpoint = j;
    	exchange S[low] and S[pivotpoint];    // Put pivotitem at pivotpoint
    }
```
| i    | j    | S[1] | S[2] | S[3] | S[4] | S[5] | S[6] | S[7] | S[8] |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| -    | -    | 15   | 22   | 13   | 27   | 12   | 10   | 20   | 25   |
| 2    | 1    | 15   | 22   | 13   | 27   | 12   | 10   | 20   | 25   |
| 3    | 2    | 15   | 22   | 13   | 27   | 12   | 10   | 20   | 25   |
| 4    | 2    | 15   | *13* | *22* | 27   | 12   | 10   | 20   | 25   |
| 5    | 3    | 15   | 13   | 22   | 27   | 22   | 10   | 20   | 25   |
| 6    | 4    | 15   | 13   | *12* | 10   | *22* | 27   | 20   | 25   |
| 7    | 4    | 15   | 13   | 12   | *10* | 22   | *27* | 20   | 25   |
| -    | 4    | *10* | 13   | 12   | *15* | 22   | 27   | 20   | 25   |


### Every-Case Time Complexity (Partition)
- Basic operation : the comparision of S[i] with pivotItem.
- 모든 원소들과 피봇은 한번씩 모두 비교한다.
- Input size : n = high - low + 1 , the number of items in the array S.
  - Because every item except the first is compared. (when pivot is the element of the first of array)
  - T(n) = n - 1.



## Worst-Case Time Complexity (QuickSort)
- Basic operation: the comparison of S[i]with pivotitemin partition
- Input size: n, the number of items in the array S.
  - The worst case occurs if the array is already sorted in nondecreasing order. (unbalance)
  - No items are less than the first item, if it is sorted. (unbalance)
  - Therefore, the array is repeatedly partitioned into an empty subarray on the left and a subarray with one less item on the right.
  - T(n) = T(0) + T(n -1)+ n -1.  (unbalance 한쪽은 0개 한쪽은 n에서 pivot 을 제외한 n-1)
  - Since T(0) = 0, T(n) = T(n-1) + n–1. (n-1은 각원소와 pivot 을 비교하는 연산)
Solving the recurrence relation,T(n) = T(n-1) + n-1T(n -1) = T(n-2) + n–2T(n -2) = T(n-3) + n–3...T(2) = T(1) + 1T(1) = T(0) + 0T(0) = 0  
`T(n) = n(n-1)/2` `O(n^2)`

> 증명 과정은 사진으로 대체하겠습니다. 수학적 귀납법을 사용합니다.
![image](https://user-images.githubusercontent.com/69495129/135617936-40c077f4-3a43-4670-be3c-2668f504f5fd.png)
![image](https://user-images.githubusercontent.com/69495129/135617953-32513678-9a96-40b3-a17d-804dd4148d9d.png)

<br>
O(n^2) 의 Time complexity 를 갖는다면 , selection insertion bubble 과 같은 시간 복잡도를 갖는 엄청 좋지 않은 sorting algorithm 인데 왜 사람들은 quicksort 를 빠르다고 하고 
심지어 자주사용하는것일까?

> Quick Sort 의 Worst case 는 pivot이 잘못 잡혀서 양쪽 배열이 너무나 unbalance 하게 분배되는 경우이다. 이런 경우는 사실 실제 상황에서 흔치않다. pivot 을 어떻게 설정하는지에 따라 다르겠지만,
> 꽤 균등하게 양쪽의 배열의 숫자가 맞춰진다. 이를 이용하여 Average-Case Time Complexity 를 구해본다. 일반적으로 Quick Sort 의 time complexity 가 O(nlogn) 이라고하는것은 다른 Algorithm 과는 다르게
> Average-Case 일 경우의 이야기이다.

![image](https://user-images.githubusercontent.com/69495129/135618301-6464bcca-0451-4f1b-85ab-162a332089a7.png)
![image](https://user-images.githubusercontent.com/69495129/135618370-ff10cdb5-fa47-4685-8c08-0b67942c8eac.png)
![image](https://user-images.githubusercontent.com/69495129/135618413-e44e3d1a-b193-400c-b5a9-291fa1aeddc5.png)


## Summary
- Quicksort 의 worstcase time complexity 는 O(n^2) 이다.
*** 
<br>

    🌜 주관적인 견해가 담긴 정리입니다. 다양한 의견이 있으실 경우
    언제든지 댓글 혹은 메일로 지적해주시면 감사하겠습니다! 😄

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}
