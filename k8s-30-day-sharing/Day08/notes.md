## 前置作業

| 說明                                                                                                      | 指令                                            |
| --------------------------------------------------------------------------------------------------------- | ----------------------------------------------- |
| kubectl get deployments                                                                                   | 取得目前 Kubernetes 中的 deployments 的資訊     |
| kubectl get rs                                                                                            | 取得目前 Kubernetes 中的 Replication Set 的資訊 |
| kubectl describe deploy <deployment-name>                                                                 | 取得特定 deployment 的詳細資料                  |
| kubectl set image deploy/ <deployment-name> <pod-name>: <image-path>: <version>                           | 將 deployment 管理的 pod 升級到特定 image 版本  |
| kubectl edit deploy <deployment-name>                                                                     | 編輯特定 deployment 物件                        |
| kubectl rollout status deploy <deployment-name>                                                           | 查詢目前某 deployment 升級狀況                  |
| kubectl rollout history deploy <deployment-name>                                                          | 查詢目前某 deployment 升級的歷史紀錄            |
| kubectl rollout undo deploy <deployment-name>                                                             | 回滾 Pod 到先前一個版本                         |
| kubectl rollout undo deploy <deployment-name> --to-revision=<n>(n 是 kubectl rollout history 的 REVISION) | 回滾 Pod 到某個特定版本                         |
