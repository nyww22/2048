# Kubernetes Hands-On

#### ARM64（Raspberry Pi4）へのインストール方法

```text
# kubectlインストール
# URL: https://kubernetes.io/ja/docs/tasks/tools/install-kubectl/

$ curl -LO "https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/arm64/kubectl"
$ chmod +x ./kubectl
$ sudo mv ./kubectl /usr/local/bin/kubectl
$ kubectl version --client

# minikubeインストール
$ curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-arm64
$ chmod +x minikube
$ sudo mkdir -p /usr/local/bin/
$ sudo install minikube /usr/local/bin/
$ minikube version

$ sudo apt-get install conntrack

$ minikube start --vm-driver=none 

```

{% embed url="https://kubernetes.io/ja/docs/tasks/tools/install-kubectl/" %}



```text
boot時の設定を変更してcgroupfsのmemoryを有効にする。

/boot/firmware/cmdline.txtにcgroup_enable=cpuset cgroup_memory=1 cgroup_enable=memoryを追記して再起動する。追記が終わったあとのファイルは以下の通り。

$ cat /boot/firmware/cmdline.txt 
net.ifnames=0 dwc_otg.lpm_enable=0 console=ttyAMA0,115200 console=tty1 root=/dev/mmcblk0p2 rootfstype=ext4 elevator=deadline rootwait cgroup_enable=cpuset cgroup_memory=1 cgroup_enable=memory

# reboot

```



#### Ubuntu20.04へのインストール方法

```text
 $ curl -LO "https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl"
 $ chmod +x ./kubectl 
 $ sudo mv ./kubectl /usr/local/bin/kubectl
 $ kubectl version --client
 
```

