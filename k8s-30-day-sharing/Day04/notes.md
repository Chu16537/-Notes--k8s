## 前置作業

1. dockerhub 創會員
1. 在 dockerhub 創 Repository
1. 本次所 docker build 的名稱 要跟 Repository 一樣

1. docker build

    ```
    docker build . -t $name:$tag

    -t  可設置名稱
    name 會影響上傳 所以名稱要相同(dockerhub帳號/dockerhub的Repository名稱)
    tag 可設置版本,記得： ,預設latest(docker push 預設上傳 latest)
    ---
    docker build . -t chu16537/docker-demo
    ```
