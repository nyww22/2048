# モバイルWiFiルータセットアップ

### OpenWrtインストール

{% embed url="https://qiita.com/YujiroTakahashi/items/b1ad93c9f5538e4f71e5" %}

```text
# imgファイルを取得
wget https://downloads.openwrt.org/snapshots/targets/bcm27xx/bcm2711/openwrt-bcm27xx-bcm2711-rpi-4-ext4-factory.img.gz

# gzipファイルを展開
gunzip openwrt-bcm27xx-bcm2711-rpi-4-ext4-factory.img.gz

# デバイスファイルパスを確認
sudo fdisk -l
* ディスク /dev/sda: 29.74 GiB, 31914983424 バイト, 62333952 セクタ
* Disk model: SD/MMC/MS PRO   
* 単位: セクタ (1 * 512 = 512 バイト)
* セクタサイズ (論理 / 物理): 512 バイト / 512 バイト
* I/O サイズ (最小 / 推奨): 512 バイト / 512 バイト
* ディスクラベルのタイプ: dos
* ディスク識別子: 0x5452574f
*
* デバイス   起動 開始位置 最後から   セクタ サイズ Id タイプ
* /dev/sda1  *        8192   139263   131072    64M 83 Linux
* /dev/sda2         139264 62333951 62194688  29.7G 83 Linux

# SDカードへ更新
sudo dd if=~/openwrt-bcm27xx-bcm2711-rpi-4-ext4-factory.img of=/dev/sda bs=2M conv=fsync

```

{% embed url="https://qiita.com/somainit/items/4de7187f41406d7ee1f1" %}

```text

sudo fdisk /dev/sda

* fdisk (util-linux 2.34) へようこそ。
* ここで設定した内容は、書き込みコマンドを実行するまでメモリのみに保持されます。
* 書き込みコマンドを使用する際は、注意して実行してください。
* 
* 
* コマンド (m でヘルプ): p
* ディスク /dev/sda: 29.74 GiB, 31914983424 バイト, 62333952 セクタ
* Disk model: SD/MMC/MS PRO   
* 単位: セクタ (1 * 512 = 512 バイト)
* セクタサイズ (論理 / 物理): 512 バイト / 512 バイト
* I/O サイズ (最小 / 推奨): 512 バイト / 512 バイト
* ディスクラベルのタイプ: dos
* ディスク識別子: 0x5452574f
* 
* デバイス   起動 開始位置 最後から セクタ サイズ Id タイプ
* /dev/sda1  *        8192   139263 131072    64M  c W95 FAT32 (LBA)
* /dev/sda2         147456   360447 212992   104M 83 Linux
* 
* コマンド (m でヘルプ): d
* パーティション番号 (1,2, 既定値 2): 2
* 
* パーティション 2 を削除しました。
* 
* コマンド (m でヘルプ): n
* パーティションタイプ
*    p   基本パーティション (1 プライマリ, 0 拡張, 3 空き)
*    e   拡張領域 (論理パーティションが入ります)
* 選択 (既定値 p): p
* パーティション番号 (2-4, 既定値 2): 2
* 最初のセクタ (2048-62333951, 既定値 2048): 147456
* Last sector, +/-sectors or +/-size{K,M,G,T,P} (147456-62333951, 既定値 62333951): 62333951
* 
* 新しいパーティション 2 をタイプ Linux、サイズ 29.7 GiB で作成しました。
* パーティション #2 には ext4 署名が書き込まれています。
* 
* 署名を削除しますか？ [Y]es/[N]o: N
* 
* コマンド (m でヘルプ): w
* 
* パーティション情報が変更されました。
* ディスクを同期しています。

sudo fdisk /dev/sda
* fdisk (util-linux 2.34) へようこそ。
* ここで設定した内容は、書き込みコマンドを実行するまでメモリのみに保持されます。
* 書き込みコマンドを使用する際は、注意して実行してください。
* 
* 
* コマンド (m でヘルプ): n
* パーティションタイプ
*    p   基本パーティション (1 プライマリ, 0 拡張, 3 空き)
*    e   拡張領域 (論理パーティションが入ります)
* 選択 (既定値 p): p
* パーティション番号 (2-4, 既定値 2): 2
* 最初のセクタ (2048-62333951, 既定値 2048): 139264
* Last sector, +/-sectors or +/-size{K,M,G,T,P} (139264-62333951, 既定値 62333951): 
* 
* 新しいパーティション 2 をタイプ Linux、サイズ 29.7 GiB で作成しました。
* 
* コマンド (m でヘルプ): w
* パーティション情報が変更されました。
* ioctl() を呼び出してパーティション情報を再読み込みします。
* ディスクを同期しています。

umount /dev/sda1
umount /dev/sda2

sudo e2fsck -f /dev/sda2
* e2fsck 1.45.5 (07-Jan-2020)
* Pass 1: Checking iノードs, blocks, and sizes
* Pass 2: Checking ディレクトリ structure
* Pass 3: Checking ディレクトリ connectivity
* Pass 4: Checking reference counts
* Pass 5: Checking グループ summary information
* Padding at end of iノード ビットマップ is not set. 修正<y>? yes
* 
* rootfs: ***** ファイルシステムは変更されました *****
* rootfs: 1176/6656 files (0.0% non-contiguous), 4728/26624 blocks

sudo resize2fs /dev/sda2
* resize2fs 1.45.5 (07-Jan-2020)
* Resizing the filesystem on /dev/sda2 to 7773312 (4k) blocks.
* The filesystem on /dev/sda2 is now 7773312 (4k) blocks long.

```

{% embed url="https://qiita.com/somainit/items/fc7e4b3c01e6450927b8" %}

イーサネットポート（Eth0）とLANケーブル、Hostマシン（Ubuntu20.04）を接続する。

{% embed url="https://ichi.pro/ho-muru-ta-toshite-no-raspberrypi-91925125961076" %}



```text
@ ssh-keygen -f "/home/takuto/.ssh/known_hosts" -R "192.168.1.1"

@ ssh root@192.168.1.1

The authenticity of host '192.168.1.1 (192.168.1.1)' can't be established.
ED25519 key fingerprint is SHA256:b+7FeRhjYnwgif+vtfpOGK+VDXV0YGFUQlD45L5pABA.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '192.168.1.1' (ED25519) to the list of known hosts.


BusyBox v1.31.1 () built-in shell (ash)

  _______                     ________        __
 |       |.-----.-----.-----.|  |  |  |.----.|  |_
 |   -   ||  _  |  -__|     ||  |  |  ||   _||   _|
 |_______||   __|_____|__|__||________||__|  |____|
          |__| W I R E L E S S   F R E E D O M
 -----------------------------------------------------
 OpenWrt SNAPSHOT, r15477-c578fdfc29
 -----------------------------------------------------
=== WARNING! =====================================
There is no root password defined on this device!
Use the "passwd" command to set up a new password
in order to prevent unauthorized SSH logins.
--------------------------------------------------
root@OpenWrt:~# 

# rootユーザのパスワード変更
root@OpenWrt:~# passwd root
Changing password for root
New password: 
Retype password: 
passwd: password for root changed by root

# Raspberry Pi4 Eth0ポートの設定変更
uci set network.lan.proto=dhcp
uci commit
service network restart


```

モデムにRaspberry Pie4をLANケーブルで接続する。

接続後にRaspberry Pie4に割り当てられた動的IPアドレスを確認する。

```text
ifconfig

br-lan    Link encap:Ethernet  HWaddr DC:A6:32:9C:15:A6  
          inet addr:192.168.0.18  Bcast:192.168.0.255  Mask:255.255.255.0
          inet6 addr: fd7d:eaaa:b058::1/60 Scope:Global
          inet6 addr: fe80::dea6:32ff:fe9c:15a6/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:5063 errors:0 dropped:0 overruns:0 frame:0
          TX packets:2743 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:3266822 (3.1 MiB)  TX bytes:249965 (244.1 KiB)

eth0      Link encap:Ethernet  HWaddr DC:A6:32:9C:15:A6  
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:8497 errors:0 dropped:0 overruns:0 frame:0
          TX packets:3570 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:4037410 (3.8 MiB)  TX bytes:319866 (312.3 KiB)

lo        Link encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:984 errors:0 dropped:0 overruns:0 frame:0
          TX packets:984 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:96453 (94.1 KiB)  TX bytes:96453 (94.1 KiB)


```

ホストPCから接続する

```text
ssh root@192.168.0.18

```

LuCIのインストールを実施する

```text
opkg update
opkg install luci
opkg install \
    luci-i18n-base-ja \
    luci-i18n-firewall-ja \
    luci-i18n-opkg-ja
    
service uhttpd restart

```

![](.gitbook/assets/image%20%287%29.png)

編集ボタンを押下する。

![](.gitbook/assets/image%20%286%29.png)

\[インターフェース設定\]-\[無線セキュリティ\]を変更する

![](.gitbook/assets/image%20%284%29.png)

![](.gitbook/assets/image%20%289%29.png)

![](.gitbook/assets/image%20%285%29.png)

\[有効\]で設定する。

![](.gitbook/assets/image%20%288%29.png)

\[再起動\]を行う。

接続先のパスフレーズ：405BD8BA50EB



### その他

{% embed url="https://qiita.com/somainit/items/fc7e4b3c01e6450927b8" %}











