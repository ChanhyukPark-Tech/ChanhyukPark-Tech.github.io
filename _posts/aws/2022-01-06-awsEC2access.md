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

AWS 에서 IAM 검색 및 



🌜 주관적인 견해가 담긴 글입니다. 다양한 의견이 있으실 경우
언제든지 댓글 혹은 메일로 지적해주시면 감사하겠습니다! 😄

