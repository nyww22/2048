# Python3+Docker+VSCode\(Remote Developer\)

Docker Install

{% embed url="https://docs.docker.com/engine/install/ubuntu/" %}

{% embed url="https://qiita.com/reflet/items/4b3f91661a54ec70a7dc" %}

{% embed url="https://docs.docker.com/engine/install/linux-postinstall/" %}

```text
# Install Docker Engine
   
    $ sudo apt-get remove docker docker-engine docker.io containerd runc
   
   $ sudo apt-get update
   
   $ sudo apt-get install     apt-transport-https     ca-certificates     curl     gnupg-agent     software-properties-common
   
   $ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
   
   $ sudo apt-key fingerprint 0EBFCD88
   
   $ sudo add-apt-repository    "deb [arch=arm64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
   
   $ sudo apt-get update
   
   $ sudo apt-get install docker-ce docker-ce-cli containerd.io
```

Visual Stadio Code + Remote Developer

{% embed url="https://qiita.com/quailDegu/items/63114ba1e14416df8040" %}



VSCode Remote Development

{% embed url="https://code.visualstudio.com/docs/remote/containers" %}

{% embed url="https://code.visualstudio.com/docs/containers/ssh" %}

{% embed url="https://aadojo.alterbooth.com/entry/2020/08/20/102600" %}





Remote-Containders

{% embed url="https://qiita.com/sgmryk/items/e8178fbf246b2c7aad81" %}

{% embed url="https://qiita.com/tnk4on/items/7ccb1921907bdb99002a" %}

sudoコマンドでの実行でなくても良い形でgroupへユーザを登録する必要がある。

{% embed url="https://www.virment.com/how-to-fix-couldnt-connect-to-docker-daemon/" %}

{% embed url="https://qiita.com/kanosawa/items/07e26edb19c86091fa48" %}

{% embed url="https://dev.classmethod.jp/articles/vs-code-remote-development-ec2/" %}



{% embed url="https://code.visualstudio.com/docs/remote/containers-advanced\#\_developing-inside-a-container-on-a-remote-docker-host" %}

{% embed url="https://qiita.com/kanosawa/items/07e26edb19c86091fa48" %}

[https://tech.actindi.net/2019/06/18/085723](https://tech.actindi.net/2019/06/18/085723)  




TroubleShooting

{% embed url="https://github.com/microsoft/vscode-docker/wiki/Troubleshooting" %}



雑談

{% embed url="https://tech.tanaka733.net/entry/visual-studio-code-extension-1" %}



