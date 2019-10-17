---
title:  "k8s"
search: false
categories: 
  - kubenetes
last_modified_at: 2019-10-14T14:00:00+09:00
---


# kubernetes - 2


## 도구에 대한 간단 설명

### kubeadm
    - 새로운 클러스터 구축에 사용되는 툴
    - 마스터 노드 init, worker node 추가 등
### kubectl
    - 구축된 클러스터에 명령을 내리도록 돕는 툴
    - 새로운 deployment, cronjob등을 정의 하거나 현재 pod, service등 현재 클러스터의 상황 파악등이 가능함


## 개념 정리 및 실습

### Node
  = 물리서버

* 쿠버네티스 pod들이 실행되는 공간
  

<실습> Node 상태 확인하기

`kubectl get nodes`

`kubectl decribe node <node name>`

`kubectl describe <resource> <resouce name>`

> _Show details of a specific resource or group of resources_

> 노드의 디테일한 정보만 보여주는게 아니라 k8s의 리소스들을 상세 조회 하는 명령어


### Pod
* n개의 컨테이너가 묶여있는 k8s의 기본 실행 단위   
* 쿠버네티스 객체 모델중 만들고 배포할 수 있는 가장 작은 단위이다.
* 각각의 파드는 유일한 IP주소를 할당 받는다. 즉 파드 내부의 모든 컨테이너는 네트워크 네임스페이스, IP주소, 포트 공유
* pod 는 self-care 불가

<실습> 간단한 파드 템플릿으로 파드 실행 및 

`kubectl create -f "[해당 파일 path]"`
source 참고 -> https://raw.githubusercontent.com/khcdev/k8s_example/master/create_pod.yml


### NameSpace
* k8s는 동일 물리클러스터를 기반으로 복수의 가상 클러스터를 지원한다. 이들 가상 클러스터를 네임스페이스라고 함

> kube-system namespace 파악
### Controller
* 여러 파드들을 생성하고 관리해준다. 클러스터 범위내에서의 레플리케이션 핸들링, 롤아웃, 셀프힐링 기능 제공 

##### ReplicaSet

* 지정된 수의 파드 레플리카가 항상 실행 되도록 보장한다.
* 하지만 직접 정의하는 경우는 없고 `Deployment`가 레플리카셋을 관리하며 다른 유용한 기능과 함께 파드에 대한 선언적 업데이트를 제공하는 상위 개념이기 때문에 Deployment로써 관리하는것이 좋다.

##### Deployment

* 파드와 레플리카셋에 대한 선언적 업데이트를 제공한다.
deployment source -> https://raw.githubusercontent.com/kubernetes/website/master/content/ko/examples/controllers/nginx-deployment.yaml
<실습>

`kubectl apply -f https://raw.githubusercontent.com/kubernetes/website/master/content/ko/examples/controllers/nginx-deployment.yaml`

`kubectl get deployments`

`kubectl rollout statusdeployment.v1.apps/nginx-deployment`

`kubectl get rs`

`
> 각 파드에 배포한  nginx에 접근 할 수 있을까?
`kubectl get pods -o=wide`

* 디플로이 먼트는 업데이트 되는 동안 일정한 수의 파드만 중단되도록 보장한다.
기본적으로 적어도 의도한 파드수의 75% 이상이 동작하도록 보장한다.
의도한 파드수보다 더 많이 생성되는 파드의 수를 제한함 최대 125%

 + ) kubectl rollout

##### DaemonSet
모든(일부도 가능) 노드에 파드의 사본을 실행 시키게 할 수 있음

> 활용법?

### Service
하나의 논리적인 pod 셋과 그 파드들에 접근할 수 있도록 정책을 정의하는 추상화된 방법

> 서비스가 필요한 이유?
* 쿠버네티스 파드들은 장애, 배포등으로 언젠가는 죽게된다.(생명주기를 가지고 있다.)
* 쿠버네티스 클러스터 내 각 파드들은 유일한 IP를 가짐
* 즉 어플리케이션들이 지속적으로 기능 할 수 있도록 해야함

<실습>
https://kubernetes.io/docs/concepts/services-networking/connect-applications-service/
https://bcho.tistory.com/tag/External%20IP


##### Secret

### Ingress
api-gateway
### Cronjob
지정된 시간마다 파드를 업데이트 시킴

##### ConfigMap

##### RBAC
    - AWS의 IAM과 같은 기능을 하는 권한 관리 방식



 