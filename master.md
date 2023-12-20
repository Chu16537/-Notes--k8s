啟動
```
成功
kubeadm join 192.168.64.8:6443 --token gbqiav.txgstynabh0tmam3 \
	--discovery-token-ca-cert-hash sha256:c42848a6f94b3de3e1abb60e8adabc246653aa2a397b9d9542c2a79e8ad3cb2a
```
錯誤
[init] Using Kubernetes version: v1.28.3
[preflight] Running pre-flight checks
error execution phase preflight: [preflight] Some fatal errors occurred:
	[ERROR FileContent--proc-sys-net-bridge-bridge-nf-call-iptables]: /proc/sys/net/bridge/bridge-nf-call-iptables does not exist
[preflight] If you know what you are doing, you can make a check non-fatal with `--ignore-preflight-errors=...`
To see the stack trace of this error execute with --v=5 or higher

請使用 
    modprobe br_netfilter
    echo '1' > /proc/sys/net/ipv4/ip_forward
```

```
退出 root 

  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config

執行完上面後 就可以使用

kubectl get nodes


  export KUBECONFIG=/etc/kubernetes/admin.conf
  ```