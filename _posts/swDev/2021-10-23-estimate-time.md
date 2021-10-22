---
title:  "[swDev] Project Time Management "

categories:
  - swDev
tags:
  - [plan, time,project]

toc: true
toc_sticky: true

---
> 이 포스트는 한양대학교 소프트웨어실무 Scott 교수님 수업을 참조하였습니다. 개인적으로 공부하면서 참조하려고 만든 포스트입니다.

What about `time` on your project
이전에 살펴본 [WBS](https://chanhyukpark-tech.github.io/swdev/plan-wbs/#summary) 내용에서 우리의 scope 를 업무단위로 나누는 과정을 살펴봤다. 
이 포스트에서는 그 업무하나하나에 대해서 얼마만큼의 시간이 소요될지 시간을 예측해보는 방법을 살펴보도록 할 것이다.

시간을 예측하는 방법에는 3가지 방법이 있으며 각자의 프로젝트 및 상황에 따라서 유동적으로 선택해서 사용하면 될 것 같다.

## methods

### 1. professional judgement
`expert` picks a number (out of thin air!)
- requires expert, experience, good memory
- may ignore project participants - very reliable for experts themselves

첫번째 방법은 전문가의 직감에 맡기는 방법이다. 어떻게 큰 프로젝트에 대한 예측을 직감에 의존할 수 있어? 
라고 생각하시는 분들도 계실것 같다. 하지만 현장에서 갈고 닦은 그 경험은 결코 무시하지 못한다.

### 2. history
based on tables of `past actuals` on major tasks
- interpolate : find appropriate function satisfying data & use it to calculate the value for a variable
- requires professional judgement & good history (with changes)

리드타임분포도를 활용한다.

![image](https://user-images.githubusercontent.com/69495129/138500653-804929de-1b92-40bf-8e82-69f6e3ec2ab3.png)

분포가 좁으면 좋다 ⇒ 비즈니스 예측성이 높다

왼쪽으로 쏠리면 ⇒ 일이 빨리 끝날 수 있다.
개발자가 질문 받을 수 있다.  ex) 이 기능 구현하는데 얼마나걸려요?
지금까지는 감으로 예상 남은 일수를 말해줬지만 , 리드타임 분포도를 이용한다면 어느정도 근거가 있는 대답을 할 수 있다. A) 이런 유형의 기능을 구현하는데는 95%의 확률로 ~일 정도 소요됩니다 😉
고객입장에서는 빨리끝내는것보다 정확히 끝내주는것을 더 좋아한다.

### 3. formula

이 포스트에서는 어떻게 공식을 사용하는지에대해서는 다루지 않을 것이다.

#### 3.1 variables
- determine major variable factors(task,person)
- determine formula of factors using measurement
- interview & plug into formula



#### 3.2 function point(metrics)
- determine smallest pieces(function point) of project
- establish time for each function point using measurement
- break project into function point, add up times, multiply by productivity of people(e.g. junior : x 2 , average : x 1 , senior : x 0.5)

`function point` : how difficult this function to develop

## best way to estimate

`theoretically ` : 3 formula
<br>
`realistically ` : 1 professional judgement

이론적으로는 공식을 이용하는게 맞지만, 프로젝트 진행중 너무나 많은 변수가 있기때문에 실제로는 전문가의 판단이 가장 잘 시간을 예측할 수 있는 방법인것 같다.
예를들어 하나의 업무를 하는데 한명이 투입되면 10일이 걸린다고 가정해보자, 그렇다면 같은 업무에 두명을 배정하면 5일이걸릴까? 결코 아닐것이다 
그들은 소통도해야하고, 토론도 해야한다 그러므로 정확히 10/2 이 아닌 6~7일이 걸릴것이라고 판단할 수 있다.
그래서 실무에서는 주로 전문가의 판단에 따르는 경우가 많다.


## graphical tools for scheduling :
pert chart 는 이 포스트에서 다루지 않고 gantt chart 만 다루도록 한다.

#### Gantt chart
order of building:
- work breakdown
- estimate(duration)
- dependencies
- resource use

show :
- critical path & non-critical path
- early & late start/finish (dealing with slack)

![image](https://user-images.githubusercontent.com/69495129/138501843-0e5f83ea-50c7-4d21-8553-2ecccf77afdb.png)
지라를 이용한 간트차트의 모습이다.

## Result
가장 중요한것은 이 세 방법중 어떤 것을 선택하더라도 반복해서 `Estimate` 를 해야한다는것이다. 한번만 해버리고 끝나면 무용지물이다.
예를들어 처음에 시간을 `Estimate` 했을때는 50% 의 정확도를 갖고 있다. 어느정도 시간이 흐른 뒤 다시 `Estimate` 하면 정확도는 75%
로 상승하는것은 당연하다. 그러므로 `iterative` 하게 시간을 측정하는것이 좋다.


***


🌜 주관적인 견해가 담긴 글입니다. 다양한 의견이 있으실 경우
언제든지 댓글 혹은 메일로 지적해주시면 감사하겠습니다! 😄

