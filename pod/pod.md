# POD

-   在同一個 Pod 裡面的 containers，可以用 local port numbers 來互相溝通
-   一個 Pod 裡面可以包含一個或多個 Docker Container
-   同一個 Pod 中的 containers，可以透過 Pod 內部的網路直接溝通
    由於每個 Pod 中有自己的網路。所以同一個 Pod 中的 containers 之間可以透過**<localhost:port_num>**互相溝通。而這樣無需透過外網的性質，讓我們可以將性質相近的服務放在同一個 Pod 裡，好比一個後端 API service，與一個後端認證 service，可以放在同一個 pod 裡互相溝通。

---

-   能將 pod 中的某個 port number，與本機端的 port 做 mapping

    -   並使用 externalPort
    -   externalPort 對外使用的 port

    ```
    kubectl port-forward $podName $externalPort:$podPort
    ```

-   讓 Pod 綁定一個 Service
    -   name : 名稱
    -   serviceName : service 名稱

    ```
    kubectl expose pod $podName --type=NodePort --name=$serviceName

    取得 serviceName url
    minikube service $serviceName --url
    ```

-   對 Pod 下指令

    ```
    kubectl exec $podName -- <command>
    ```

-   強迫 pod 立即結束

    -   num : 數量

    ```
    kubectl delete pods $podName --grace-period=0 --force
    ```

-   動態更新 pod lables 
   -   name : 名稱
    ```
   kubectl label pods $name env=production
    ```
