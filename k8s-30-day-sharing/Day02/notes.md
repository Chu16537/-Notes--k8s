## 安裝

1. Minikube
1. kubectl

-   補充
    在 ~/.bashrc 加入以下

```
source <(kubectl completion bash)
alias kb=kubectl
complete -F __start_kubectl k

alias mk=minikube
```

## 啟動 minikube

1. 正常啟動
    ```
    minikube start
    ```
1. 啟動時 使用 minikube 的 docker

    ```
    minikube start --driver=docker

    ----
    minikube start
    eval $(minikube -p minikube docker-env)
    ```

1. 查看 minikube 內部 docker
    ```
    minikube docker-env
    ```

### 指令

| 說明              | 指令               |
| ----------------- | ------------------ |
| 狀態              | minikube status    |
| 版本              | minikube version   |
| config            | cat ~/.kube/config |
| 查看所有 k8c 服務 | kubectl get all    |

### 練習步驟

-   補充 1.變數前面有"$" 代表需要帶入參數

1. run service (開啟一個 server ＆ pod )

    ```
    kubectl run $name --image=$imageREPOSITORY:imageTag --port=$port
    ---
    kubectl run hello-minikube --image=gcr.io/google_containers/echoserver:1.8 --port=8080
    ```

1. 讓指定名稱的 pod 可以給外部連接

    ```
    kubectl expose pod $podName --type NodePort --port $port
    ---
    kubectl expose pod hello-minikube --type NodePort --port 8080
    ```

1. 取得指定的 pod url

    ```
    minikube service $podName --url
    ---
    minikube service hello-minikube --url
    ```
