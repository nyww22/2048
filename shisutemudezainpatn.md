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


# ローカルマシンに戻り、下記の各コマンドで各Redisの登録されたキーを確認する
$ kubectl exec -it sharded-redis-0 --container redis redis-cli
127.0.0.1:6379> keys *

$ kubectl exec -it sharded-redis-1 --container redis redis-cli
127.0.0.1:6379> keys *
hoge

$ kubectl exec -it sharded-redis-2 --container redis redis-cli
127.0.0.1:6379> keys *
fuga



# 各種デプロイ資材を破棄する
$ kubectl delete -f twemproxy-ambassador-pod.yaml 
pod "ambassador-example" deleted

$ kubectl delete -f redis-service.yaml
service "redis" deleted

$ kubectl delete -f redis-shards.yaml
statefulset.apps "sharded-redis" deleted

$ kubectl delete configmap twemconfig
configmap "twem-config" deleted

# 資材削除されているかの確認
$ kubectl get all



```



サービスブローカーとしての利用













