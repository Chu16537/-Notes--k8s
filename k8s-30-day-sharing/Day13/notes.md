## 前置作業

| 說明 | 指令 |
| ---- | ---- |
|      |      |


kb create -f wordpress-secret.yaml
kb create -f my-wordpress-deploy.yaml
kb create -f wordpress-service.yaml 

minikube service wordpress-service-d13 --url

kb delete  deployments.apps wordpress-app 
kb delete secrets wordpress-secret-d13 
kb delete svc wordpress-service-d13 