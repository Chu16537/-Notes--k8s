# HorizontalPodAutoscaler

- 支持 Colddown / Delay 
    - up 3分 / down 5分


kubectl create -f ./helloworld-depolyment.yaml

kubectl expose deploy helloworld-deployment --name helloworld-service --type=ClusterIP

kubectl create -f ./helloworld-hpa.yaml

while true; do curl http://10.96.229.58:3000;curl http://10.96.229.58:3000;curl http://10.96.229.58:3000;curl http://10.96.229.58:3000;curl http://10.96.229.58:3000; done