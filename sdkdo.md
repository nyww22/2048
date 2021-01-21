# SDカード移行



### SDカードからPCへバックアップ

```text
$ sudo fdisk -l

ディスク /dev/sda: 29.74 GiB, 31914983424 バイト, 62333952 セクタ
Disk model: SD/MMC/MS PRO   
単位: セクタ (1 * 512 = 512 バイト)
セクタサイズ (論理 / 物理): 512 バイト / 512 バイト
I/O サイズ (最小 / 推奨): 512 バイト / 512 バイト
ディスクラベルのタイプ: dos
ディスク識別子: 0xab86aefd

デバイス   起動 開始位置 最後から   セクタ サイズ Id タイプ
/dev/sda1  *        2048   526335   524288   256M  c W95 FAT32 (LBA)
/dev/sda2         526336 62333918 61807583  29.5G 83 Linux


$ sudo dd if=/dev/sda of=/home/takuto/sdcardimg.dd


```



### バックアップファイルからSDカードへリストア

```text
$ sudo dd if=/home/takuto/sdcardimg.dd of=/dev/sdc


```

