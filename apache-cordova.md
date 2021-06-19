# Apache Cordova



{% embed url="https://cordova.apache.org/docs/en/6.x/guide/platforms/ubuntu/index.html" %}

```text
$ cat Dockerfile

FROM ubuntu:16.04
RUN apt-get update -y; \
apt-get install -y nodejs npm
#node -v; \
#npm -v
RUN apt-get install -y software-properties-common; \
add-apt-repository ppa:cordova-ubuntu/ppa; \
apt-get update -y; \
apt-get install -y cordova-cli
RUN add-apt-repository ppa:ubuntu-sdk-team/ppa; \
apt-get update -y; \
apt-get dist-upgrade; \
apt-get install -y click-dev phablet-tools ubuntu-sdk-ide

RUN click chroot -a armhf -f ubuntu-sdk-15.04 install cmake libicu-dev:armhf pkg-config qtbase5-dev:armhf qtchooser qtdeclarative5-dev:armhf qtfeedback5-dev:armhf qtlocation5-dev:armhf qtmultimedia5-dev:armhf qtpim5-dev:armhf libqt5sensors5-dev:armhf qtsystems5-dev:armhf

```





Android Emulator on Docker

Docker上で動作させてWebブラウザでエミュレータ画面を表示させる方法

{% embed url="https://github.com/google/android-emulator-container-scripts" %}

```text
# 事前準備
# python3仮想環境をインストールする
$ sudo apt-get install python3-venv

# Android Command Line Tools(sdk-manager)をインストールする
$ wget -O cmdlinetools.zip https://dl.google.com/android/repository/commandlinetools-linux-7302050_latest.zip?hl=ja
$ unzip cmdlinetools.zip

# Android Platform Tools(adb)をインストールする
$ wget -O andorid-platform-tools.zip https://dl.google.com/android/repository/platform-tools-latest-linux.zip?hl=ja
$ unzip android-platform-tools.zip
$ sudo mv android-platform-tools /usr/local/

# 使用するコマンドのみシンボリックリンクを設定する
$ sudo ln -s /usr/local/android-platform-tools/adb /usr/local/bin/adb
$ cd /usr/local/bin
$ ls -la
drwxr-xr-x  2 root        root            4096  6月 19 09:03 .
drwxr-xr-x 13 root        root            4096  6月 19 08:10 ..
lrwxrwxrwx  1 root        root              37  6月 19 09:03 adb -> /usr/local/android-platform-tools/adb


# 上記サイトからソースコード一式をダウンロードする
$ git clone https://github.com/google/android-emulator-container-scripts.git

$ cd android-emulator-container-scripts/


$ . ./configure.sh && emu-docker create stable "P android x86_64"

# homeディレクトリに.androidフォルダを作成する
# adbkey生成時に該当フォルダへ出力するため
$ mkdir ~/.android

$ ./create_web_container.sh -p user,pw



```



