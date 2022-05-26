## 前置作業

1. 設定 yaml 檔案

### 指令

| 說明              | 指令                           |
| ----------------- | ------------------------------ |
| 查看所有 pod      | kubectl get pods               |
| 查看指定 pod 資訊 | kubectl describe pods $podName |

## 創建 yaml 檔案

1. kubectl create
    ```
    kubectl create -f $yamlName.yaml
    ---
    kubectl create -f my-first-pod.yaml
    ```

## 與 pod 互動

#### 1. 使用 port-forward

1. kubectl port-forward
    ```
    kubectl port-forward $podName $port:$port
    ---
    kubectl port-forward my-pod-d05 8000:3000
    ```

#### 2. 創建 service

1. 創 service

    ```
    kubectl expose pod $podName --type=NodePort --name=$serviceName
    ---
    kubectl expose pod my-pod --type=NodePort --name=my-pod-service  --port=$port
    ```

1. 取得網址
    ```
    minikube service $serviceName --url
    ---
    minikube service my-pod-service --url
    ```

## 使用 alpine 來 debug

1. 開啟 alpine
    ```
    kubectl run -i --tty alpine --image=alpine --restart=Never -- sh
    ---
    kubectl run -i --tty alpine --image=alpine --restart=Never -- sh
    ```
1. 安裝 curl
    ```
    apk add --no-cache curl
    ```

1. curl pod
    ```
    curl $podIp:port
    ---
    curl http://172.17.0.4:3000
    ```
