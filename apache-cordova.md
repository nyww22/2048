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

{% embed url="https://qiita.com/ntsk/items/7e068812db4cd654d914" %}



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

# docker起動（Web接続＋adb接続可能）
$ docker-compose -f js/docker/docker-compose-build.yaml -f js/docker/development.yaml up

# docker起動（Web接続のみ）
$ docker-compose -f js/docker/docker-compose-build.yaml up

```



Androidビルド環境構築

{% embed url="https://qiita.com/kaihei777/items/1a94a8a329c8fb67d421" %}

```text
$ cat Dockerfile

# ----------
FROM node-base as android-cordova-builder

ARG GRADLE_VERSION="6.5"

ENV BUILD_TOOLS_VERSION=28.0.3
ENV PLATFORMS_VERSION=android-28

#RUN apt update -y; \
#apt install -y openjdk-11-jdk

# openjdk8
RUN wget --quiet https://github.com/AdoptOpenJDK/openjdk8-binaries/releases/download/jdk8u292-b10/OpenJDK8U-jdk_x64_linux_hotspot_8u292b10.tar.gz; \
tar xzf OpenJDK8U-jdk_x64_linux_hotspot_8u292b10.tar.gz; \
rm -rf OpenJDK8U-jdk_x64_linux_hotspot_8u292b10.tar.gz; \
mv ./jdk8u292-b10 /opt/

# command-line-toolsをダウンロードして解凍します。
RUN wget --quiet -O android-sdk.zip https://dl.google.com/android/repository/commandlinetools-linux-7302050_latest.zip?hl=ja; \
unzip -q -d android-sdk-linux android-sdk.zip; \
rm -rf android-sdk.zip; \
mv android-sdk-linux /usr/local/; \
ln -s /usr/local/android-sdk-linux/cmdline-tools/bin/sdkmanager /usr/local/bin/sdkmanager

# gradleをダウンローして解凍します。
RUN wget --quiet --output-document=gradle-bin.zip https://services.gradle.org/distributions/gradle-${GRADLE_VERSION}-bin.zip; \
unzip -q -d gradle gradle-bin.zip; \
rm -rf gradle-bin.zip; \
mv ./gradle /usr/local


# 環境変数
ENV JAVA_HOME /opt/jdk8u292-b10
ENV ANDROID_SDK_ROOT /usr/local/android-sdk-linux
ENV GRADLE_HOME /usr/local/gradle/gradle-${GRADLE_VERSION}
ENV PATH $PATH:$ANDROID_SDK_ROOT/cmdline-tools/bin:$GRADLE_HOME/bin:$JAVA_HOME/bin:$ANDROID_SDK_ROOT/platform-tools:$ANDROID_SDK_ROOT/tools

# sdk-toolsのlicensesに同意します。
RUN mkdir ~/.android && \
    touch ~/.android/repositories.cfg
RUN yes | sdkmanager --sdk_root=${ANDROID_SDK_ROOT} --licenses >/dev/null

# install android tools and more
RUN sdkmanager --sdk_root=${ANDROID_SDK_ROOT} "tools" "build-tools;${BUILD_TOOLS_VERSION}" "platforms;${PLATFORMS_VERSION}" "platform-tools" "extras;android;m2repository"

RUN npm install -g cordova

# native-client build
#RUN cd native-client; \
#cordova platform add android; \
#cordova cordova prepare; \
#cordova build

## ----------
FROM android-cordova-builder as apk-builder

WORKDIR /home/node/oauth-work/native-client
RUN cordova platform add android
RUN cordova plugin add cordova-plugin-inappbrowser
RUN cordova plugin add cordova-plugin-customurlscheme --variable URL_SCHEME=com.oauthinaction.mynativeapp
RUN cordova build

```



