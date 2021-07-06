# 分散システムデザインパターン

#### 

#### アンバサダーパターン

シャーディングされたredisの実装

```text
# Statefulsetで実装されたWorkloadsAPI
$ kubectl create -f redis-shards.yaml

# Services API 
$ kubectl create -f redis-service.yaml

# twemproxy用の設定ファイルを登録
$ kubectl create configmap twem-config --from-file=./nutcracker.yaml

# twemproxyとアプリケーションコンテナをデプロイ
$ kubectl create -f twemproxy-ambassador-pod.yaml

# アプリケーションコンテナでbash起動する
$ kubectl exec -it ambassador-example --container nginx bash
apt update
apt install -y redis-tools

redis-cli
127.0.0.1:6379> set hoge 1
127.0.0.1:6379> set fuga 2

127.0.0.1:6379> get hoge
1

127.0.0.1:6379> get fuga
2






```









