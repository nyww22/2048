# Kubernetes Hands-On



```text
# kubectlインストール
$ curl -LO https://dl.k8s.io/v1.21.0/kubernetes-client-linux-arm.tar.gz
$ tar xvfz kubernetes-client-linux-arm.tar.gz
$ sudo cp kubernetes/client/bin/kubectl /usr/local/bin/
$ kubectl version


# minikubeインストール
$ curl -LO https://github.com/kubernetes/minikube/releases/download/v1.20.0/minikube-linux-arm
$ chmod +x minikube-linux-arm
$ sudo cp minikube-linux-arm /usr/local/bin/minikube
$ minikube version]

$ sudo apt-get install conntrack

$ minikube start --vm-driver=none 

```



```text
boot時の設定を変更してcgroupfsのmemoryを有効にする。

/boot/firmware/cmdline.txtにcgroup_enable=cpuset cgroup_memory=1 cgroup_enable=memoryを追記して再起動する。追記が終わったあとのファイルは以下の通り。

$ cat /boot/firmware/cmdline.txt 
net.ifnames=0 dwc_otg.lpm_enable=0 console=ttyAMA0,115200 console=tty1 root=/dev/mmcblk0p2 rootfstype=ext4 elevator=deadline rootwait cgroup_enable=cpuset cgroup_memory=1 cgroup_enable=memory

# reboot

```



