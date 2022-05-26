# Replication Controller

-   用來管理 Pod 的數量以及狀態
-   可以指定同時有多少個相同的 Pods 運行在 Kubernetes Cluster 上
-   當 Pod 終止運行時，會幫我們自動偵測，並且自動創建一個新的 Pod，確保 Pod 運行的數量與設定檔的指定的數量相同
-   當機器重新開啟時，會自動建立之前運行的 pod

---

-   更改 pod 數量

    -   num : 數量

    ```
    kubectl scale --replicas=$num -f $yaml.yaml
    ```

-   刪除 replication 讓 pod 繼續工作

    -   num : 數量

    ```
    kubectl delete rc $replicationName --cascade=false
    ```


