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

