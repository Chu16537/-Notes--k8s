# Ingress

![架構](./describe-ingress.png)

-   可作負載平衡
-   只需開放一個對外的 port number，Ingress 可以在設定檔中設置不同的路徑，決定要將使用者的請求傳送到哪個 Service 物件
-   Ingress 本身並沒有提供負載平衡的功能，還需要透過 Ingress Controller 來實現

-   minikube 啟動 ingress

    ```
    minikube addons enable ingress
    ```

