# Kubernetes

### Docker ComposeとKubernetesとの関係性

{% embed url="https://www.creationline.com/lab/25164" %}

{% embed url="https://github.com/docker/compose-on-kubernetes" %}



### KubernetesとDocker Composeの違い

{% embed url="https://gihyo.jp/admin/serial/01/ubuntu-recipe/0469" %}

> 複数のコンテナを管理するツールに[Docker Compose](https://docs.docker.com/compose/)があります。Docker Composeは複数のコンテナの設定や関係をひとつのファイルにまとめて記述できるため，コンテナ同士が連携することでひとつのサービスを提供するようなソフトウェアにとっては非常に便利なツールです。さらに従来は`docker`コマンドにオプションとして渡していたような情報も設定ファイルとして記述できるため，マルチコンテナではない環境でも有用です。ただし複数のホストにデプロイするとなると，ひと手間必要になります。
>
> とどのつまりKubernetesは，複数のコンテナを複数のマシンに「いい感じ」に配置・管理できるツールなのです

