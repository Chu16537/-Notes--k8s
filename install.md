## 安裝流程

1. 禁止 mem swap 虛擬內存- k8s 啟動會去確認你有沒有開啟,會把容器放入裡面使用,會減少執行效能
    ```
    sudo sed -i '/swap.img/ s/^\(.*\)$/#\1/g' /etc/fstab

    swapoff -a

    查看
    free -m
    ```
1. 先設定 k8s server上網路
    ```
    cat <<EOF | sudo tee /etc/sysctl.d/k8s.conf
    net.bridge.bridge-nf-call-ip6tables = 1
    net.bridge.bridge-nf-call-iptables = 1
    EOF
    
    sudo sysctl --system
    ```
3. 安裝 kubeadm, kubelet, kubectl
    ```
    sudo apt-get update && sudo apt-get install -y apt-transport-https curl

    curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -

    cat <<EOF | sudo tee /etc/apt/sources.list.d/kubernetes.list
    deb https://apt.kubernetes.io/ kubernetes-xenial main
    EOF

    sudo apt-get update
    sudo apt-get install -y kubelet kubeadm kubectl
    
    # 防止他們更新
    sudo apt-mark hold kubelet kubeadm kubectl
    ```
1. 設定 linux kernel
    ```
    cat > /etc/modules-load.d/containerd.conf <<EOF
    overlay
    br_netfilter
    EOF

    modprobe overlay
    modprobe br_netfilter
    ```


1. 設定網路給 CRI-O(https://linux.cn/article-15687-1.html)
    ```
    cat > /etc/sysctl.d/kubernetes-cri.conf <<EOF
    net.bridge.bridge-nf-call-iptables  = 1
    net.ipv4.ip_forward                 = 1
    net.bridge.bridge-nf-call-ip6tables = 1
    EOF

    sysctl --system


    sudo apt install apt-transport-https ca-certificates curl gnupg2 software-properties-common -y

    # 看版本
    lsb_release -a
    // 改為自己的版本
    export OS=xUbuntu_22.04
    export CRIO_VERSION=1.24

    echo "deb https://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/$OS/ /"| sudo tee /etc/apt/sources.list.d/devel:kubic:libcontainers:stable.list

    echo "deb http://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable:/cri-o:/$CRIO_VERSION/$OS/ /"|sudo tee /etc/apt/sources.list.d/devel:kubic:libcontainers:stable:cri-o:$CRIO_VERSION.list

    curl -L https://download.opensuse.org/repositories/devel:kubic:libcontainers:stable:cri-o:$CRIO_VERSION/$OS/Release.key | sudo apt-key add -

    curl -L https://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/$OS/Release.key | sudo apt-key add -

    sudo apt update
    apt-get install -y cri-o cri-o-runc

    #啟動
    systemctl daemon-reload && sudo systemctl enable crio && systemctl start crio

    systemctl status crio
    ```

2. K8s Master Node 啟動 
    ```
    看log journalctl -f -u kubelet
    本步驟全部以 Root 身份執行

    kubeadm init

    狀況1 — 機器上 Docker 同時存在，導致 kubeadm 分不清楚是要用 docker 還是 cri-0
    錯誤訊息如下 :
    Found multiple CRI sockets, please use --cri-socket to select one: /var/run/dockershim.sock, /var/run/crio/crio.sock
    To see the stack trace of this error execute with --v=5 or higher

    解決辦法: 指定我們使用 crio 來執行
    kubeadm init --cri-socket=/var/run/crio/crio.sock

    錯誤訊息如下 :
    W1030 01:50:57.860385    5225 initconfiguration.go:120] Usage of CRI endpoints without URL scheme is deprecated and can cause kubelet errors in the future. Automatically prepending scheme "unix" to the "criSocket" with value "/var/run/crio/crio.sock". Please update your configuration!
    [init] Using Kubernetes version: v1.28.3
    [preflight] Running pre-flight checks
    error execution phase preflight: [preflight] Some fatal errors occurred:
	[ERROR FileContent--proc-sys-net-bridge-bridge-nf-call-iptables]: /proc/sys/net/bridge/bridge-nf-call-iptables does not exist
    [preflight] If you know what you are doing, you can make a check non-fatal with `--ignore-preflight-errors=...`
    To see the stack trace of this error execute with --v=5 or higher

    解決辦法:回到上面 >> 設定 linux kernel

    Timeout
    其實這是因為網路設定不正確導致 kubeadm 與 kubelet 無法驗證
    錯誤訊息主要類似 Unfortunately, an error has occurred: timed out waiting for the condition :

    解決辦法:
    先看一下 crio-bridge 的網路設定
    cat /etc/cni/net.d/100-crio-bridge.conf
    應該會類似如下
    {
        "cniVersion": "0.3.1",
        "name": "crio",
        "type": "bridge",
        "bridge": "cni0",
        "isGateway": true,
        "ipMasq": true,
        "hairpinMode": true,
        "ipam": {
          "type": "host-local",
          "routes": [
            { "dst": "0.0.0.0/0" },
            { "dst": "1100:200::1/24" }
          ],
          "ranges": [
            [{ "subnet": "10.85.0.0/16" }],
            [{ "subnet": "1100:200::/24" }]
          ]
    }

    注意上面粗斜體的部分，這邊是 crio 的網路位置，一般來說大家應該都是 10.85.0.0/16 ，如果不一樣的話請自行修改以下指令
    用以下指令啟動
    export CIDR=10.85.0.0/16
    kubeadm init --pod-network-cidr=$CIDR --cri-socket=/var/run/crio/crio.sock


    已經存在
    錯誤訊息類似 : ERROR FileAvailable — etc-kubernetes-manifests-kube-apiserver.yaml /etc/kubernetes/manifests/kube-apiserver.yaml already exists

    解決辦法 :輸入指令清除
    kubeadm reset --cri-socket=/var/run/crio/crio.sock


    等待初始化完成
    ```