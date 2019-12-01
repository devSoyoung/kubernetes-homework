# Kubernetes Homework
## 과제 프로젝트 실행 순서
```
$ git clone https://github.com/devSoyoung/kubernetes-homework/
$ cd kubernetes-homework/kubernetes
```

```
$ kubectl apply -f my-deployment.yaml
$ kubectl apply -f my-service.yaml
```

```
$ kubectl get pods
$ kubectl cluster-info
```

`http://[cluster-ip]:[Nodeport]`로 접속
