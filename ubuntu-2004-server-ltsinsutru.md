# Ubuntu 20.04 Server LTSインストール

### RaspberryPi4にUbuntu20.0.4 Server LTSをインストール

{% embed url="https://ubuntu.com/download/raspberry-pi" %}

![](.gitbook/assets/image%20%2810%29.png)

![](.gitbook/assets/image%20%2815%29.png)

ubuntu-20.04.1 imageファイルをダウンロードする。



Ubuntu Server ImageをmicroSDカードに書き込むため、専用の書き込みツールをダウンロードする。専用の書き込みツール（Raspberry Pi Imager）となっている。

![](.gitbook/assets/image%20%2814%29.png)

imager\_1.5\_amd64.debファイルをGUIからインストールする。

Raspberry Pi Imagerを起動する。

![](.gitbook/assets/image%20%2816%29.png)

![](.gitbook/assets/image%20%2811%29.png)

Operating SystemとSD Cardを選択してWRITEボタンを押下する。



microSDカードをRaspberry Pi4に挿入し起動する。

起動後ネットワーク環境の設定を実施する。

{% embed url="https://makandat.wordpress.com/2020/06/20/raspberry-pi4-%E3%81%A7-ubuntu-20-04lts-server-%E3%82%92%E5%8B%95%E3%81%8B%E3%81%99%E3%80%82/" %}

```text
sudo apt-get update
sudo apt-get upgrade
sudo apt -y install network-manager

# WiFiアダプタ情報の確認
sudo lshw -class network -short
/1      wlan0   network    Wireless interface
/2      eth0    network    Ethernet interface


sudo vim /etc/netplan/50-cloud-init.yaml

-->以下を追加
    wifis:
        wlan0:
            dhcp4: false
            dhcp6: false
            optional: true
            addresses: [192.168.0.190/24]
            gateway4: 192.168.0.1
            nameservers:
              addresses: [192.168.0.1]
              search: []
            access-points:
              "OpenWrt":
                 password: "************"
    version: 2
    renderer: NetworkManager

sudo netplan apply

sudo apt -y install net-tools

ifconfig

```



キーボードの設定変更を行う

```text
sudo dpkg-reconfigure keyboard-configuration

```



ユーザの追加とデフォルトユーザ・Rootユーザのロック

```text
# ユーザUSERNAMEを作成
sudo adduser USERNAME

# ユーザUSERNAMEをsudoグループへ追加
sudo adduser USERNAME sudo

sudo passwd -d ubuntu
sudo passwd -l ubuntu
sudo passwd -l root
```

{% embed url="https://qiita.com/quailDegu/items/63114ba1e14416df8040" %}

### 

### ファイアーウォールの設定変更

現状開いているポート番号の確認と必要なポートを変更する。

```text
# nmap（ポートスキャンソフト）をインストールする
sudo apt install nmap

# 開いているポート番号を確認する
sudo nmap -sTU localhost

Starting Nmap 7.80 ( https://nmap.org ) at 2021-01-15 01:20 UTC
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00047s latency).
Not shown: 1999 closed ports
PORT   STATE SERVICE
22/tcp open  ssh

Nmap done: 1 IP address (1 host up) scanned in 0.35 seconds


```



