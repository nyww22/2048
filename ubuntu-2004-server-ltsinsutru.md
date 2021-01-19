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
sudo apt -y install net-tools

# WiFiアダプタ情報の確認
sudo lshw -class network -short
/1      wlan0   network    Wireless interface
/2      eth0    network    Ethernet interface


sudo vim /etc/netplan/99_config.yaml

ー＞以下の編集を行う
network:
  ethernets:
     eth0:
          dhcp4: true
          optional: true
  wifis:
     wlan0:
          dhcp4: true
          #dhcp6: false
          #addresses: [192.168.0.70/24]
          #gateway4: 192.168.0.1
          #nameservers:
          #    addresses: [192.168.0.1, 8.8.8.8, 8.8.4.4]
          access-points:
              "BCW710J-83382-A":
                      password: "3585744d7553c"
  version: 2
  renderer: NetworkManager

sudo netplan apply
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



### DNSサーバの設定確認

```text
$ sudo systemd-resolve --status

Global
       LLMNR setting: no                  
MulticastDNS setting: no                  
  DNSOverTLS setting: no                  
      DNSSEC setting: no                  
    DNSSEC supported: no                  
          DNSSEC NTA: 10.in-addr.arpa     
                      16.172.in-addr.arpa 
                      168.192.in-addr.arpa
                      17.172.in-addr.arpa 
                      18.172.in-addr.arpa 
                      19.172.in-addr.arpa 
                      20.172.in-addr.arpa 
                      21.172.in-addr.arpa 
                      22.172.in-addr.arpa 
                      23.172.in-addr.arpa 
                      24.172.in-addr.arpa 
                      25.172.in-addr.arpa 
                      26.172.in-addr.arpa 
                      27.172.in-addr.arpa 
                      28.172.in-addr.arpa 
                      29.172.in-addr.arpa 
                      30.172.in-addr.arpa 
                      31.172.in-addr.arpa 
                      corp                
                      d.f.ip6.arpa        
                      home                
                      internal            
                      intranet            
                      lan                 
                      local               
                      private             
                      test                

Link 3 (wlan0)
      Current Scopes: DNS        
DefaultRoute setting: yes        
       LLMNR setting: yes        
MulticastDNS setting: no         
  DNSOverTLS setting: no         
      DNSSEC setting: no         
    DNSSEC supported: no         
  Current DNS Server: 8.8.4.4    
         DNS Servers: 192.168.0.1
                      8.8.8.8    
                      8.8.4.4    
          DNS Domain: ~.         

Link 2 (eth0)
      Current Scopes: DNS                 
DefaultRoute setting: yes                 
       LLMNR setting: yes                 
MulticastDNS setting: no                  
  DNSOverTLS setting: no                  
      DNSSEC setting: no                  
    DNSSEC supported: no                  
  Current DNS Server: 218.219.82.240      
         DNS Servers: 218.219.82.240      
                      220.208.109.240     
          DNS Domain: ~.                  
                      hachi1.kt.home.ne.jp
lines 43-61/61 (END)

```

{% embed url="https://qiita.com/atomyah/items/1989138730f3385844dd" %}



### mDNS（multicast DNS）の導入

```text
# 接続先サーバオペレーション
#

# Avahiパッケージのインストール
$ sudo apt-get install avahi-daemon

# ホスト名の変更
$ vim /etc/hostname

（変更前）
ubuntu

（変更後）
NEW_HOSTNAME

:wq!

```

```text
#　ホスト端末先オペレーション
#

$ ping NEW_HOSTNAME.local

```

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



