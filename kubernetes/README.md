# Term Project 4

## apiVersion
* **service.yaml** : `apiVersion: v1`
* **deployment.yaml** : `apiVersion: apps/v1`

차이점을 찾아보니

|apps/v1|v1|
|--|--|
|statefulSet|Service|

* **statefulSet** : 

> https://matthewpalmer.net/kubernetes-app-developer/articles/kubernetes-apiversion-definition-guide.html

## docker swarm의 depends on
https://stackoverflow.com/questions/50385162/how-to-add-pod-dependency-in-kubernetes-as-like-depends-on-in-docker-compose-y

## kind: Deployment
stateless 앱을 배포할 때 사용하는 가장 기본적인 컨트롤러, 지금은 거의 기본적인 배포 방법으로 사용되고 있음

### 지원하는 배포 관련 기능
* 실행시켜야 하는 Pod의 갯수를 유지
* rolling update
* 배포 도중 정지 후 재배포
* 이전 버전으로 롤백

## kind: Service
일련의 Pod 엔드포인트를 단일 리소스로 그룹화
* Pod이 서비스 구성원이 되기 위해서는 셀렉터에 지정된 모든 라벨이 Pod에 포함되어야 함

### Service의 장점
* 구성원 Pod이 죽었다가 재생성되면서 IP 주소가 변경되더라도, 서비스 수명 동안 지속되는 안정적인 IP 주소를 획득
    * 외부에서는 Pod의 주소를 몰라도 되기 때문에, IP 바뀌어도 수정이 필요없음
* 부하 분산을 제공
