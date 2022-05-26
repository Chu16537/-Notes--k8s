## 前置作業

| 說明 | 指令 |
| ---- | ---- |
|      |      |

1. 創建 Secret file
    ```
    kubectl create secret generic <name> --from-file=<file name 需要副檔名> --from-file=<file name 需要副檔名>
    ---
    kubectl create secret generic demo-secret-from-file --from-file=./username.txt --from-file=./password.txt
    ```
1. 創建 Secret yaml

    ```
    kubectl create -f <yaml檔>
    ---
    [環境變數版本](./demo-secrets/my-pod.yaml)

    spec.containers.env.secretKeyRef.name 必須跟 my-secret.yaml 的 metadata.name 相同

    ---

    [掛載在某個pod路徑下](./demo-secrets/my-pod-with-mounting-secret.yaml)

    spec.volumes.secret.secretName 必須跟 my-secret.yaml 的 metadata.name 相同

    spec.containers.volumeMounts.mountPath 可設定路徑

    ```

1. 創建 Secret 直接輸入

    ```
    kubectl create secret generic demo-secret-from-literal --from-literal=<檔案名稱>=<內容> --from-literal=<檔案名稱>=<內容>
    ---
    kubectl create secret generic demo-secret-from-literal --from-literal=username=root --from-literal=password=rootpass
    ```

1. 查看 secrets

    ```
    kubectl describe secrets <name>
    ---
    kubectl describe secrets demo-secret-from-file
    ```

1. 查看 secrets

    ```
    kubectl describe secrets <name>
    ---
    kubectl describe secrets demo-secret-from-file
    ```

1. 把 設定檔 放入 指定 pod

    ```
    kubectl exec -it <podName> -- /bin/bash
    ---
    kubectl describe secrets demo-secret-from-file
    ```

1. exec 環境變數版本

    ```
    kubectl exec -it <pod> -- /bin/bash

    echo $spec.evn.name
    ---

    kubectl exec -it my-pod-d12 -- /bin/bash

    echo $SECRET_USERNAME

    ```

1. exec 掛載在某個 pod 路徑下

    ```
    kubectl exec -it <pod> -- /bin/bash

    mountPath = spec.containers.volumeMounts.mountPath
    echo "$(cat mountPath/檔案)"
    ---

    kubectl exec -it my-pod-d12 -- /bin/bash

    echo "$(cat /etc/creds/username)"

    ```
