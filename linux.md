## 改ip
```

sudo vi /etc/netplan/00-installer-config.yaml

network:
 ethernets:
  enp0s1:   #配置的网卡的名称
   addresses: [192.168.64.9/24]  #配置的静态ip地址和掩码
   dhcp4: no  #关闭DHCP，如果需要打开DHCP则写yes
   optional: true
   gateway4: 192.168.64.1  #网关地址
   nameservers:
     addresses: [192.168.64.1]  #DNS服务器地址，多个DNS服务器地址需要用英文逗号分隔开
 version: 2
 renderer: networkd  #指定后端采用systemd-networkd或者Network Manager，可不填写则默认使用systemd-workd


 sudo netplan apply
```