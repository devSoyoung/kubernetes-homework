# Kubernetes Object
* 쿠버네티스 오브젝트는 쿠버네티스 시스템에서 영속성을 가지는 개체
* 쿠버네티스는 클러스터의 상태를 나타내기 위해 이 개체를 이용
* 오브젝트를 생성하게 되면, 쿠버네티스 시스템은 그 오브젝트 생성을 보장하기 위해 지속적으로 작동

## 스펙(Spec)과 상태(Status)
* **spec** : 오브젝트가 가졌으면 하고 원하는 특징, 즉 의도한 상태를 기술
* **status** : 오브젝트의 실제 상태 를 기술하고, 쿠버네티스 시스템에 의해 제공되고 업데이트 됨

오브젝트를 생성할 때, 쿠버네티스에 스펙과 상태 정보를 전달하는데 `.yaml` 파일을 통해 전달하는 방식이 일반적임

> kubectl 은 API 요청이 이루어질 때, JSON 형식으로 정보를 변환시켜 준다.

```yaml
apiVersion: apps/v1 # apps/v1beta2를 사용하는 1.9.0보다 더 이전의 버전용
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  selector:
    matchLabels:
      app: nginx
  replicas: 2 # 템플릿에 매칭되는 파드 2개를 구동하는 디플로이먼트임
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.7.9
        ports:
        - containerPort: 80
```
* `apiVersion` : 스크립트를 실행하기 위한 쿠버네티스 API 버전
* `kind` : 리소스의 종류 (Pod, Service, ReplicaSet 등)
* `metadata` : 리소스의 메타 데이터 (라벨, 이름 등)
* `spec` : 컨테이너, 볼륨 등 리소스에 대한 상세한 스펙 정의

디플로이먼트를 생성하기 위해 `kubectl apply` 명령어를 실행

```
$ kubectl apply -f https://k8s.io/examples/application/deployment.yaml --record
```

