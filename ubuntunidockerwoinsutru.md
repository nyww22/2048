# Ubuntu20.04にDockerをインストール

{% embed url="https://docs.docker.com/engine/install/ubuntu/" %}

```text
# 古いバージョンのDockerを削除する
$ sudo apt-get remove docker docker-engine docker.io containerd runc


$ sudo apt-get update

$ sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

sudo apt-key fingerprint 0EBFCD88

sudo add-apt-repository \
   "deb [arch=arm64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"

# Docker CEをインストールする
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
sudo apt-get install docker-compose

# dockerグループへユーザを追加
sudo usermod -aG docker $USER

# グループへの変更をアクティブ化
newgrp docker 

```





update\(2021.6.13\)

docker-composeのインストール方法を更新

```text
$ sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

$ sudo chmod +x /usr/local/bin/docker-compose

```

{% embed url="https://docs.docker.com/compose/install/" %}



### AUFS StorageDriverを用いる場合

{% embed url="https://docs.docker.com/storage/storagedriver/aufs-driver/" %}

```text
＃カーネルがAUFSドライバをサポートしているか確認する。
sudo grep aufs /proc/filesystems

```



