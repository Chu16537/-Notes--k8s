# Namespaces

- 在同一個 Kubernetes Cluster 中，每個 Namespaces 的名稱都是要獨特的
- 當一個 Namespaces 被刪除時，在該 Namespace 裡的所有物件也會被刪除
- 可以透過 Resource Quotas 限制一個 Namespaces 所可以存取的資源




-   更換 預設 namespaces

    ```
    newspaceName: 新名稱
    
    kubectl config set-context $(kubectl config current-context) --namespace=$newspaceName
    ```

---