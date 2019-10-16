---
title:  "k8s"
search: false
categories: 
  - kubenetes
last_modified_at: 2019-10-14T14:00:00+09:00
---


# kubernetes - 2


## 세팅한 노드 상태 확인
- 아무 pod도 떠있지 않은 노드는 어떤상황일까?


## 용어 정리

### Node
  = 물리서버

* 쿠버네티스 pod들이 실행되는 공간
  

<실습> Node 상태 확인하기

`kubectl get nodes`

`kubectl decribe nodes`

##### Pod
* n개의 컨테이너가 묶여있는 k8s의 기본 실행 단위   
* 쿠버네티스 객체 모델중 만들고 배포할 수 있는 가장 작은 단위이다.
* 각각의 파드는 유일한 IP주소를 할당 받는다. 즉 파드 내부의 모든 컨테이너는 네트워크 네임스페이스, IP주소, 포트 공유
* pod 는 self-care 불가
##### Controller
* 여러 파드들을 생성하고 관리해준다. 클러스터 범위내에서의 레플리케이션 핸들링, 롤아웃, 셀프힐링 기능 제공 
##### ReplicaSet
* 지정된 수의 파드 레플리카가 항상 실행 되도록 보장한다.
* 하지만 직접 정의하는 경우는 없고 `Deployment`가 레플리카셋을 관리하며 다른 유용한 기능과 함께 파드에 대한 선언적 업데이트를 제공하는 상위 개념이기 때문에 Deployment로써 관리하는것이 좋다.
##### Deployment

##### DaemonSet

##### Cronjob

##### Service

##### Ingress

##### NameSpace

##### ConfigMap

##### Secret

##### RBAC
    - AWS의 IAM과 같은 기능을 하는 권한 관리 방식


## 도구에 대한 간단 설명

### kubeadm
    - 새로운 클러스터 구축에 사용되는 툴
    - 마스터 노드 init, worker node 추가 등
### kubectl
    - 구축된 클러스터에 명령을 내리도록 돕는 툴
    - 새로운 deployment, cronjob등을 정의 하거나 현재 pod, service등 현재 클러스터의 상황 파악등이 가능함

## 간단한 pod 배포
- namespace 구성 + namespace 사용하는이유


## 