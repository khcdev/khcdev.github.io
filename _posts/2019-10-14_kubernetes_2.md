---
title:  "k8s"
search: false
categories: 
  - kubenetes
last_modified_at: 2019-10-14T14:00:00+09:00
---


# kubernetes - 2


## 세팅한 노드 상태 확인
- 노드에 관련한 명렁어들 확인
- 아무 pod도 떠있지 않은 노드는 어떤상황일까?


## 용어 정리

##### Node
    -> 물리 서버
##### Pod
    -> n개의 컨테이너가 묶여있는 k8s의 실행 단위
##### ReplicaSet
    -> 
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