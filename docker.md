# Docker

-   docker build
    -t 可設置名稱
    name 會影響上傳 所以名稱要相同(dockerhub 帳號/dockerhub 的 Repository 名稱)
    tag 可設置版本,記得： ,預設 latest(docker push 預設上傳 latest)

    ```
    docker build . -t $name:$tag
    ```
