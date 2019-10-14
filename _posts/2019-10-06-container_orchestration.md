---
title:  "Container Orchestration"
search: false
categories: 
  - kubenetes
last_modified_at: 2018-08-07T14:00:00+09:00
---


# Orchestration?

보통 `Container Orchestration`이라고 불린다. docker 환경에만 국한된 개념은 아니며 컨테이너의 배포 관리, 장애복구 등을 지원하는 도구이다.

## 지원하는 기능들, 왜 필요한지
* 컨테이너 자동 배치 및 복제
* 컨테이너 그룹에 대한 로드 밸런싱
* 컨테이너 장애 복구
* 클러스터 외부에 서비스 노출
* 컨테이너 추가 또는 제거로 확장 및 축소
* 컨테이너 서비스간의 인터페이스를 통한 연결 및 네트워크 포트 노출 제어

## 대표적인 서비스들

#### kubernetes(k8s)

![k8s_image](https://raw.githubusercontent.com/1ambda/1ambda.github.io/master/assets/images/infra-kubernetes/intro/logo.png)
* 구글이 다년간의 Container 배포 경험을 녹아낸 Orchestration Framework, 가장 대중적으로 사용중이다.
* 베어 메탈, VM환경, 퍼블릿 클라우드 등의 다양한 환경에서 작동하도록 설계되어 있음.
* 컨테이너의 롤링 업그레이드 지원 ( 파드의 업그레이드가 무중단으로 이루어 질 수 있게 함)

#### docker swarm

<img src="https://subicura.com/assets/article_images/2017-02-25-container-orchestration-with-docker-swarm/docker-swarm.png" width=240 height=240>

* 작동이 간단하고 구축하기 편리함
* Docker명령어와 Compose를 그대로 사용가능

3. apache mesos

<img src="https://mesos.apache.org/assets/img/mesos_logo_fb_preview.png" width=240 hegith=240>

* 수만 대의 물리 시스템으로 확장 가능하도록 설계 돠어있음
* Hadoop, MPI, Hypertable, Spark같은 응용프로그램을 동적클러스터 환경에서 리소스 공유와 분리를 통해 자원 최적화가 가능
* Docker 컨테이너를 적극적으로 지원함



# Kubernetes(이하 k8s)
    k`ubernete`s -> k 와 s 사이가 8자리여서 이렇게 부름

가장 유명한 Container Orchestration Service 
k8s 클러스터를 간단하게 구축하는 다양한 방법중에 `minikube`라는 툴이 있으나 마스터 노드 하나로만 동작하고 실제로 k8s의 강점을 경험하기에는 한계가 있기 때문에 `kubeadm`을 이용하여 구축 해볼 예정

# Kubernetes Architecture
* 아키텍쳐 그림으로 각 내용 전달
![k8s_architecture_diagram](https://miro.medium.com/max/3032/1*t5TbINIv1vbTYCTraPy16g.png)

![k8s_architecture_diagram2](http://www.mantech.co.kr/wp-content/uploads/2017/07/Kubernetes.png)

k8s는 두개의 주요한 컴포넌트로 구성 됩니다.
1. Master
2. Worker

## Master
### API Server
작업 상태를 정희하고 조회할 수 있는 RESTful 웹서비스 제공, k8s클러스터에서는 각 구성요소는 API 서버를 거쳐서 통신함 

### etcd 
모든 클러스터 데이터를 담는 쿠버네티스 뒷단의 저장소로 사용되는 일관성·고가용성 키-값 저장소.

쿠버네티스 클러스터에서 etcd를 뒷단의 저장소로 사용한다면, 이 데이터를 백업하는 계획은 필수이다.
API서버를 통해서만 조회 할 수 있다.

### Controller Manager
Pod, Service, DaemonSet, Job 등 다양한 오브젝트를 제어 및 상태를 체크하는 역할 

### Scheduler
노드의 정보와 알고리즘을 통해 특정 Pod를 어떤 노드에 배포할 지 결정함 조건에 따라 분류하고 우선순위를 통해 가장 최적의 노드 선정하여 배포


## Worker
### kubelet
클러스터의 각 노드에서 실행 되는 에이전트, kubelet은 파드에서 컨테이너가 확실하게 동작하도록 관리
쿠버네티스를 통해 생성되지 않은 컨테이너는 관리하지 않는다.

### kube-proxy
kube-proxy는 클러스터의 각 노드에서 실행되는 네트워크 프록시로, 쿠버네티스의 서비스 개념의 구현부이다.

kube-proxy는 노드의 네트워크 규칙을 유지 관리한다. 이 네트워크 규칙이 내부 네트워크 세션이나 클러스터 바깥에서 파드로 네트워크 통신을 할 수 있도록 해준다.

## 클러스터 구축 
https://futurecreator.github.io/2019/02/25/kubernetes-cluster-on-google-compute-engine-for-developers/

