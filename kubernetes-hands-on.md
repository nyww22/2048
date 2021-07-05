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

{% embed url="https://kubernetes.io/ja/docs/tasks/tools/install-kubectl/" %}

#### minikubeインストール＆設定

```text
$ curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
$ sudo install minikube-linux-amd64 /usr/local/bin/minikube
$ minikube version
minikube version: v1.21.0
commit: 76d74191d82c47883dc7e1319ef7cebd3e00ee11

$ minikube start
😄  Ubuntu 20.04 上の minikube v1.21.0
✨  dockerドライバーが自動的に選択されました。他の選択肢:  ssh, none
👍  コントロールプレーンのノード minikube を minikube 上で起動しています
🚜  イメージを Pull しています...
💾  Kubernetes v1.20.7 のダウンロードの準備をしています
    > gcr.io/k8s-minikube/kicbase...: 359.09 MiB / 359.09 MiB  100.00% 2.26 MiB
    > preloaded-images-k8s-v11-v1...: 492.20 MiB / 492.20 MiB  100.00% 2.73 MiB
🔥  docker container (CPUs=2, Memory=3900MB) を作成しています...
🐳  Docker 20.10.7 で Kubernetes v1.20.7 を準備しています...
    ▪ 証明書と鍵を作成しています...
    ▪ Control Plane を起動しています...
    ▪ RBAC のルールを設定中です...
🔎  Kubernetes コンポーネントを検証しています...
    ▪ イメージ gcr.io/k8s-minikube/storage-provisioner:v5 を使用しています
🌟  有効なアドオン: storage-provisioner, default-storageclass
🏄  完了しました！ kubectl が「"minikube"」クラスタと「"default"」ネームスペースを使用するよう構成されました

```

