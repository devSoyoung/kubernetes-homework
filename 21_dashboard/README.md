# Kubernetes Dashboard

## Installation
```
$ kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v1.10.1/src/deploy/recommended/kubernetes-dashboard.yaml

secret/kubernetes-dashboard-certs created
serviceaccount/kubernetes-dashboard created
role.rbac.authorization.k8s.io/kubernetes-dashboard-minimal created
rolebinding.rbac.authorization.k8s.io/kubernetes-dashboard-minimal created
deployment.apps/kubernetes-dashboard created
service/kubernetes-dashboard created
```

로컬 작업환경에서 dashboard에 접근하기 위해서 쿠버네티스 클러스터에 secure 채널을 생성

```
$ kubectl proxy
Starting to serve on 127.0.0.1:8001
```

![dashboard initial](./dashboard-initial.png)

* **Kubeconfig** :
* **Token** : 

## Token으로 접속하기
해당 디렉토리의 `dashboard-admin.yaml` 파일을 만들고 아래 명령어 실행

```
$ kubectl apply -f dashboard-admin.yaml

$ kubectl -n kube-system describe secret $(kubectl -n kube-system get secret | grep admin-user | awk '{print $1}')
```

두 번째 커맨드를 실행하면 토큰을 얻을 수 있음. 이 토큰을 복사해서 위 화면의 Token 옵션을 선택하고 접속하면 됨.

***
## Reference
* [Kubernetes Dashboard 설치하기](https://medium.com/@essem_dev/kubernetes-dashboard-%EC%84%A4%EC%B9%98%ED%95%98%EA%B8%B0-c236c4c9f0c6)
* [Kubernetes 공식 문서 - 웹 UI (대시보드)](https://kubernetes.io/ko/docs/tasks/access-application-cluster/web-ui-dashboard/)
