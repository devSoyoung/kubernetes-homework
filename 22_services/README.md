# Kubernetes Service

1. pod을 띄우고, 서비스를 구성할 팟을 선택한 Service(simple-service.yaml) 실행
2. service manifest에 정의되어 있는 selector를 이용해서 실행중인 pod 중 해당되는 pod을 service에서 관리
3. 외부의 클라이언트는 Service 주소로 요청을 보내고, Service는 요청에 따라 적절한 Pod으로 작업을 전달

***

## 시작하기

```
$ minikube start
```

### Pod 실행: two-replicas-with-label.yaml

```
$ kubectl apply -f two-replicas-with-label.yaml
deployment.apps/eva-west created
deployment.apps/eva-east created
```

```
$ kubectl get pod -l app=eva
NAME                        READY   STATUS    RESTARTS   AGE
eva-east-7c555578c5-49t9z   2/2     Running   0          2m18s
eva-east-7c555578c5-r4wtr   2/2     Running   0          2m18s
eva-west-55bfcbc594-fcp76   2/2     Running   0          2m18s
eva-west-55bfcbc594-nrfqn   2/2     Running   0          2m18s

$ kubectl get pod -l app=eva -l release=west
NAME                        READY   STATUS    RESTARTS   AGE
eva-west-55bfcbc594-fcp76   2/2     Running   0          2m54s
eva-west-55bfcbc594-nrfqn   2/2     Running   0          2m54s

$ kubectl get pod -l app=eva -l release=east
NAME                        READY   STATUS    RESTARTS   AGE
eva-east-7c555578c5-49t9z   2/2     Running   0          2m57s
eva-east-7c555578c5-r4wtr   2/2     Running   0          2m57s

```

-l 옵션으로 특정 라벨을 가진 pod을 조회

```
$ kubectl get all                           
NAME                            READY   STATUS    RESTARTS   AGE
pod/eva-east-7c555578c5-49t9z   2/2     Running   0          3m53s
pod/eva-east-7c555578c5-r4wtr   2/2     Running   0          3m53s
pod/eva-west-55bfcbc594-fcp76   2/2     Running   0          3m53s
pod/eva-west-55bfcbc594-nrfqn   2/2     Running   0          3m53s

NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
service/kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   2d

NAME                       READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/eva-east   2/2     2            2           3m53s
deployment.apps/eva-west   2/2     2            2           3m53s

NAME                                  DESIRED   CURRENT   READY   AGE
replicaset.apps/eva-east-7c555578c5   2         2         2       3m53s
replicaset.apps/eva-west-55bfcbc594   2         2         2       3m53s
```

### Service 실행: simple-service.yaml  

```
$ kubectl apply -f simple-service.yaml         
service/eva created
```

```
$ kubectl get service eva             
NAME   TYPE       CLUSTER-IP      EXTERNAL-IP   PORT(S)        AGE
eva    NodePort   10.108.82.171   <none>        80:32193/TCP   35s
```

```
$ kubectl get all        
NAME                            READY   STATUS    RESTARTS   AGE
pod/eva-east-7c555578c5-49t9z   2/2     Running   0          6m1s
pod/eva-east-7c555578c5-r4wtr   2/2     Running   0          6m1s
pod/eva-west-55bfcbc594-fcp76   2/2     Running   0          6m1s
pod/eva-west-55bfcbc594-nrfqn   2/2     Running   0          6m1s

NAME                 TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)        AGE
service/eva          NodePort    10.108.82.171   <none>        80:32193/TCP   67s
service/kubernetes   ClusterIP   10.96.0.1       <none>        443/TCP        2d

NAME                       READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/eva-east   2/2     2            2           6m1s
deployment.apps/eva-west   2/2     2            2           6m1s

NAME                                  DESIRED   CURRENT   READY   AGE
replicaset.apps/eva-east-7c555578c5   2         2         2       6m1s
replicaset.apps/eva-west-55bfcbc594   2         2         2       6m1s
```

아까 목록에 없었던 eva 서비스가 생성된 것을 확인할 수 있음

```
$ kubectl cluster-info     
Kubernetes master is running at https://192.168.64.2:8443
KubeDNS is running at https://192.168.64.2:8443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.
```

```
# cluster-info에서 찾은 IP 주소와 NodePort의 포트번호로 요청
$ curl http://192.168.64.2:32193
# 응답이 정상적으로 날아옴
```

```
$ kubectl run -i --rm --tty debug \
--image=alpine:latest --restart=Never -- ash -il
$ apk add curl
$ curl http://eva/
```
kubectl로 alpine을 띄우고 interactive 모드로 접속해서 curl 설치 후 eva라는 이름으로 접근할 수 있음.
kubernetes에 이름을 잘 지으면 좋다..! 이름으로 접근할 수 있는게 많다. (어디까지..?)


### 컨테이너 접근 기록 확인하기

```
$ kubectl logs -f eva-west-55bfcbc594-fcp76 nginx                         
172.17.0.1 - - [28/Nov/2019:02:55:12 +0000] "GET / HTTP/1.1" 200 612 "-" "curl/7.64.1" "-"
172.17.0.8 - - [28/Nov/2019:02:58:11 +0000] "GET / HTTP/1.1" 200 612 "-" "curl/7.66.0" "-"
```

## 실행한 서비스, Pod 정리하기

```
$ kubectl delete -f simple-service.yaml
$ kubectl delete -f two-replicas-with-label.yaml
$ kubectl delete pods,services --all=true

$ minikube stop
```
