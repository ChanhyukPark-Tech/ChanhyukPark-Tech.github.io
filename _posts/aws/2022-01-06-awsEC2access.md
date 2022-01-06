---
title:  "[aws] aws EC2 에 접근하는 4가지방법"

categories:
  - aws
tags:
  - [aws,ec2,ssh,IAM]

toc: true
toc_sticky: true

---


```
`인턴` 을 하면서 aws china region 에 접근해야할 일이 생겼다.
china region 은 다른 국가와 달리 aws 에 제약이 많다고 한다. 
그래서 일반적인 ssh 접근으로는 접근이 불가능하였고, 다른 방법으로 인스턴스에 접근할 수 밖에 없었다.
```

일반적으로 AWS EC2 에 접근하는 방법은 총 4가지 방법이 있다. (SSH,EC2 INSTANCE,Session Manager, EC2 직렬 콘솔)
이 방법들의 차이는 글의 후반부에서 설명하도록 하고, 중국 리전에서는 SSH연결과 Session Manager 로 접근밖에 되지 않는다.
key의 문제로 인해 SSH연결이 불가능하였고, Session Manager를 이용하였다. 

Session Manager는 인증수단이 키페어가 아닌 IAM 이라고 한다. 

```
AWS Identity and Access Management(IAM)는 모든 AWS에 대해 세분화된 액세스 제어를 제공합니다. 
IAM을 사용하면 서비스 및 리소스에 액세스할 수 있는 사용자와 액세스할 수 있는 조건을 지정할 수 있습니다.
IAM 정책으로 인력 및 시스템에 대한 권한을 관리하여 최소 권한을 보장할 수 있습니다.
```


## Session Manager 로 인스턴스에 접근하는 방법


AWS 에서 IAM 을 검색한다

![image](https://user-images.githubusercontent.com/69495129/148335400-395c2a65-1bc7-4554-b7c4-2ec1d2fb77e0.png)


좌측의 Roles 혹은 역할을 클릭해준다

![image](https://user-images.githubusercontent.com/69495129/148335469-6c1a9f7e-fdf3-43b1-999d-324fb7504cbb.png)

Create role 클릭

![image](https://user-images.githubusercontent.com/69495129/148335525-86a11481-e682-422d-abe2-ba7e011049e9.png)

EC2 선택

![image](https://user-images.githubusercontent.com/69495129/148335570-3f5f7c74-1aa6-4b12-9c57-c19c8b4d99e2.png)

`AmazonEC2RoleforSSM` 선택
 
다음 하다가 Role name 은 원하는거 지정 저는 `MyEC2RoleForSSM` 로 이름을 지정해주겠습니다.

이제 인스턴스에 이 역할(role)을 등록시켜줍니다 

instance(ec2) 탭에 갑니다.

![image](https://user-images.githubusercontent.com/69495129/148335756-8493dd21-89b6-49a3-96a1-76cfd2938269.png)

session manager 로 접근하고자 하는 인스턴스의 우클릭 및 instance settings => attatch/Replace IAM Role ! 하고 아까 자신이 지정해줬던 역할이름 선택및 저장

다음 aws 에서 `systems manager` 검색

![image](https://user-images.githubusercontent.com/69495129/148335689-74c02f4c-c111-4b5d-9274-7042c1e0572c.png)

좌측에서 session manager 클릭

조금기다리면 (5분정도) 자신이 지정한 인스턴스가 목록에 나올것입니다 등장하면 `Start session`  버튼을 클릭하면 ec2 에 접근이 바로 가능합니다.



## EC2 에 접근하는 4가지 방법 비교

![image](https://user-images.githubusercontent.com/69495129/148335912-5207c9fc-5aba-4479-a8a8-e1aef4f7d38d.png)


그림 출처는 유튜버 `AWS 강의실` 님입니다.


## Summary 

지금까지는 EC2에 접근할때 항상 터미널에서 ssh 나 putty 로 접근하는 방법밖에 없는 줄 알았는데, 다른방법으로도 접근이 가능하다는것을 처음 알았다.. 하루종일 방법만 찾아본 결과였다.
그리고 aws china region 은 같은 aws 는 아닌거같다 너무나 많은 제약상황이 있어서 나중에 중국에서 비즈니스를 할 떄는 알리바바 클라우드도 고려해봐야겠다.






🌜 주관적인 견해가 담긴 글입니다. 다양한 의견이 있으실 경우
언제든지 댓글 혹은 메일로 지적해주시면 감사하겠습니다! 😄

