# Ubuntu20.04にDockerをインストール

{% embed url="https://docs.docker.com/engine/install/ubuntu/" caption="" %}

```text
# 古いバージョンのDockerを削除する
$ sudo apt-get remove docker docker-engine docker.io containerd runc


$ sudo apt-get update

$ sudo apt-get install -y \
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
sudo apt-get install -y docker-ce docker-ce-cli containerd.io
sudo apt-get install -y docker-compose
```

## AUFS StorageDriverを用いる場合

{% embed url="https://docs.docker.com/storage/storagedriver/aufs-driver/" caption="" %}

```text
＃カーネルがAUFSドライバをサポートしているか確認する。
sudo grep aufs /proc/filesystems
```

