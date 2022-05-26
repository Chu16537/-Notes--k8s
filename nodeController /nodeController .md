# NodeController 

- 定期監控每個 Node 的狀態，若是有 Node 呈現 unhealthy 的狀態時，就會將該 Node 從清單中移除，而在該 Node 上的 Pod 就會被重新分配到其他 Node 上
- 當 Node 的狀態狀態變回 healthy 時，Node Controller 則會把該 Node 加回可用的清單中


-   移除 node

    ```
    node_name: node名稱
    
    kubectl drain $node_name
    ```

---


-   恢復 node

    ```
    node_name: node名稱
    
    kubectl uncordon $node_name
    ```

---