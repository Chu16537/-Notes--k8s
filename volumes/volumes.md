# Volumes

-   Pod 物件中的 container 儲存的資料會隨著 container 的生命週期消失而消失，而無法被保存下來
-   讓 Pod 中的 container 即便因為某些因素而 crash ，資料仍可完整的被保存下來，讓新產生的 container 能延續使用
-   以透過掛載(mounting)的方式，供許多個 Pods 同時存取

## emptyDir

-   建立一個新的 Pod 物件時 Kubernetes 自動建立,當 Pod 從 Node 中被移除時，emptyDir 也會隨之消失
-   該 Pod 中所有的 container 都可以讀寫
-   暫時性儲存空間 & 共用儲存空間

## hostPath

-   hostPath 的生命週期與 Node 相同

    ```
    kubectl create -f ./volumes/hostPath.yaml 

    // 新增檔案在 apiservice 裡面
    kubectl exec -it apiserver -- /bin/bash
    ls /tmp
    echo "aaa" >> /tmp/test.txt
    cat /tmp/test.txt
    exit 

    // 在外面也可以讀取到
    minikube ssh
    cat /tmp/test.txt 
    ```

## Cloud Storage

## NFS (Network FileSystem)
