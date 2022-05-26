# Deployment

-   可使升降版本
-   服務升級過程中做到無停機服務遷移(zero downtime deployment)
-   strategy 可以設定 rollout 時的動作

| 說明                                                                                                     | 指令                                            |
| -------------------------------------------------------------------------------------------------------- | ----------------------------------------------- |
| kubectl get deployments                                                                                  | 取得目前 Kubernetes 中的 deployments 的資訊     |
| kubectl get rs                                                                                           | 取得目前 Kubernetes 中的 Replication Set 的資訊 |
| kubectl describe deploy $deployment-name                                                                 | 取得特定 deployment 的詳細資料                  |
| kubectl set image deploy/ $deployment-name $pod-name: $image-path: $version                              | 將 deployment 管理的 pod 升級到特定 image 版本  |
| kubectl edit deploy $deployment-name                                                                     | 編輯特定 deployment 物件                        |
| kubectl rollout status deploy $deployment-name                                                           | 查詢目前某 deployment 升級狀況                  |
| kubectl rollout history deploy $deployment-name                                                          | 查詢目前某 deployment 升級的歷史紀錄            |
| kubectl rollout undo deploy $deployment-name                                                             | 回滾 Pod 到先前一個版本                         |
| kubectl rollout undo deploy $deployment-name --to-revision=<n>(n 是 kubectl rollout history 的 REVISION) | 回滾 Pod 到某個特定版本                         |

-   讓 deployment 綁定一個 Service

    -   name : 名稱
    -   serviceName : service 名稱

    ```
    kubectl expose deploy $name --type=NodePort --name=$serviceName

    取得 serviceName url
    minikube service $serviceName --url
    ```

-   讓 deployment 綁定一個 Service
    -   deployment-name : 要升級的 deployment 名稱
    -   pod-name : 要升級的 pod 名稱
    -   docker-images: docker image REPOSITORY
    -   tag : docker images TAG
    ```
    kubectl set image deploy/$deployment-name $pod-name=$docker-images:tag
    ```
-   查看版本變動歷史

    -   deployment-name : 要升級的 deployment 名稱

    ```
    kubectl rollout history deployment $deployment-name
    ```

-   回到特定版本

    -   deployment-name : 要升級的 deployment 名稱
    -   revision : 編本編號 需要先 查看版本變動歷史

    ```
    kubectl rollout undo deploy $deployment-name --to-revision=$revision

    // 拿 revision 版本編號
    kubectl rollout history deployment $deployment-name
    ```
