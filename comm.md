# 指令

-   啟動 minikube

    ```
    minikube start

    minikube docker-env

    讓終端機使用 minikube 的 docker
    eval $(minikube -p minikube docker-env)
    ```

---

-   啟動 minikube 時把 port 的上限改道 50000

    -   num : 數量

    ```
    minikube start --extra-config=apiserver.ServiceNodePortRange=1-50000
    ```

-   安裝 alpine

    ```
    kubectl run -i --tty alpine --image=alpine --restart=Never -- sh

    apk add --no-cache curl
    ```

---

-   創建
    ```
    kubectl create -f $yamlName.yaml
    ```
-   刪除
    -   kind : 種類(pod service ...)
    -   name : 名稱
    ```
    kubectl delete $kind $name
    ```
-   查看資訊
    -   kind : 種類(pod service ...)
    -   name : 名稱
    ```
    kubectl describe $kind $name
    ```
-   讓 Kind 綁定一個 Service

    -   kind : 種類(pod service ...)
    -   name : 名稱
    -   serviceName : service 名稱

    ```
    kubectl expose $kind $name --type=NodePort --name=$serviceName

    取得 serviceName url
    minikube service $serviceName --url
    ```
