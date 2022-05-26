## 前置作業

| 說明 | 指令 |
| ---- | ---- |
|      |      |


kubectl get all --all-namespaces

kubectl run -i --tty alpine --image=alpine --restart=Never -- sh


kubectl create -f ./mysql-secret.yaml
kubectl create -f ./mysql-server-pod.yaml
kubectl create -f ./mysql-server-service.yaml

kubectl create -f wordpress-pod.yaml
kubectl create -f wordpress-service.yaml