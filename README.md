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

> 주의 : mysql-database 컨테이너 문제로 한글 입력은 오류가 납니다 :)
