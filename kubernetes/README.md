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
