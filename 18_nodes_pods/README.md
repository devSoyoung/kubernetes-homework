# Nodes and Pods
쿠버네티스의 기본 개념인

* Node
* Cluster
* Container
* Pod
* Deployment
* Ingress

를 정리

## Pod

***

## Minikube
> mini + kube 로 보이는 이름을 가진 minikube 는 **로컬 환경에서 최상의 쿠버네티스 환경을 제공하고자 하는 프로젝트 명이며, 프로그램 이름**이기도 하다. 보통 서버 및 클러스터 구조에서 운용되는 **쿠버네티스를 간편하게 구현 및 테스트**하기 위한 도구이다.

Kubernetes는 Master Node와 Worker Node 여러 개로 구성되어 있다.
이때, 여기서 말하는 Node들은 하나의 물리 서버 혹은 VM이다.
그렇다면 Kubernetes를 배우기 위해서는 여러 VM을 생성하고 그 위에 Kubernetes 환경을 구축해야 할까?
그렇지 않다. 단일 노드, 즉 로컬에서 Minikube를 통해 쿠버네티스를 실행할 수 있다.

=> kubernetes는 여러 개의 물리 서버나 VM으로 구성되는데, 공부를 할 때에는 이러한 환경을 만들고 공부를 시작하려고 하면 막막하다. 이럴 때, 단일 노드(=로컬 컴퓨터 한 대)에서 미니쿠베를 통해 쿠버네티스를 실행할 수 있다.

