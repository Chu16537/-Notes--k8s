## 前置作業

| 說明 | 指令 |
| ---- | ---- |
|      |      |


kubectl create -f ./hellospace.yaml

kubectl get resourcequotas -n hellospace

kb describe resourcequotas compute-quotas -n hellospace
kb describe resourcequotas object-quotas -n hellospace


// 切換 namespace 
kubectl config set-context  $(kubectl config current-context) --namespace=default