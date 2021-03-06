# AWS Lambda

SDKランタイムはアプリ内にパッケージングする

![](.gitbook/assets/image%20%2898%29.png)









{% hint style="info" %}
AWS LambdaとRDBMSの相性が悪いのは何故か？
{% endhint %}

{% embed url="https://www.keisuke69.net/entry/2017/06/21/121501" %}

（上記記述内容から抜粋して引用）

> #### 最大同時接続数の問題
>
> ご存知の通り各種[RDBMS](http://d.hatena.ne.jp/keyword/RDBMS)には最大同時接続数的なパラメータがあるわけですが、設定可能な値と実際に使い物になる値は別物です。DBエンジンごとの多少の違いはもちろんあるものの、使い物になる数値というのはCPU数やメモリ数と大きく関係してきます。
>
> 当然ながら同時に接続される数が多ければ多いほど必要なCPU数、メモリ数が増えていきます。つまり、アクティブな接続が同時に数千から数万になるDBを動かすにはそれなりのスペックが必要というわけです。そもそもプロセスやスレッドが数千とか数万になってくると1サーバのOSだと[コンテキストスイッチ](http://d.hatena.ne.jp/keyword/%A5%B3%A5%F3%A5%C6%A5%AD%A5%B9%A5%C8%A5%B9%A5%A4%A5%C3%A5%C1)やら何やら厳しくなってくるので、DB分割なんかも検討するかと思います。
>
> また、[RDBMS](http://d.hatena.ne.jp/keyword/RDBMS)というと、現状ではほとんどが処理量が増えた場合にスケールアウトで対応するのではなくスケールアップが必要になります。要はサーバに積むCPU、メモリなどを増やす方向です。参照系はスケールアウトできても更新系はスケールアップで対応するしかないことが多いです。
>
> さて、ポイントは先のLambdaファンクションの振る舞いとの兼ね合いです。まず、説明のとおり、リク[エス](http://d.hatena.ne.jp/keyword/%A5%A8%A5%B9)トがあるとコンテナが作られて起動されるのでこのタイミングでDBへのコネクションが張るわけですが、リク[エス](http://d.hatena.ne.jp/keyword/%A5%A8%A5%B9)トのたびに接続するのはコストがかかるので、その接続オーバーヘッドを減らすための方法として、グロー[バルス](http://d.hatena.ne.jp/keyword/%A5%D0%A5%EB%A5%B9)コープを利用することでコンテナがアクティブな間、つまりウォームスタートの場合はそれを利用するという方法があります。
>
> 一方で先ほどの説明の通り、Lambdaは同時に処理すべきリク[エス](http://d.hatena.ne.jp/keyword/%A5%A8%A5%B9)トは必要なリク[エス](http://d.hatena.ne.jp/keyword/%A5%A8%A5%B9)ト数分のコンテナで処理します。つまり、各コンテナからDBへとそれぞれコネクションが張られることになります。ということは仮にデフォルト状態であっても1000コネクションが張られる可能性があるということです。これがプロダクション環境でもう少し大きいシステムであれば数[千同](http://d.hatena.ne.jp/keyword/%C0%E9%C6%B1)時実行 ＝ 数千コネクションとかにになってきます。こうなってくると一般的にはコネクションプールを使うことが多いと思います。DBへ都度接続するコストを減らした上で、コネクションを使いまわすことで負荷を減らすわけです。
>
> ところが、Lambdaではこのコネクションプールを実現することが難しいのです。Lambdaファンクションのコンテナ間では何も共有しませんし、外部のデータストアへと永続化しない限りはできないからです。つまり、コンテナをまたいで利用するようなコネクションプールの実装は難しいと言えます。それを管理する中間層のようなものを用意して各コンテナはそれ経由でDBにアクセスするような何かを作るとかして頑張ればなんとかなるかも知れませんが、ちゃんと検討したことないのでわかりません。
>
> 話しを戻すと、このようなLambdaファンクションのプラットフォーム特性を考えるとダウンストリームとなるシステムも同様にスケールアウトするようなものでないと耐えきれないです。同時実行数が少ないうちはいいですが増えてくると耐えられなくなってきます。実はこれは[RDBMS](http://d.hatena.ne.jp/keyword/RDBMS)に限らない話しなんですけどね。スケールアウトできないシステムの場合、ある程度まではピークにあわせたスペックのサーバを用意しておくことで対応できるとは思いますが、限界は来るかと思います。また、せっかくNever pay for idleを特徴とするプラットフォームを利用するにも関わらず、ピークのために通常よりも巨大なスペックのDBサーバを維持するのももったいない話しですしね。
>
> というわけでLambdaと組み合わせて利用するデータストアとしてはDynamoDBを推奨しているわけです。DynamoDBの場合は分散型データベースであり同時接続数の増加そのものは気にする必要がなくなります。また、一貫して高速で安定したパフォーマンスを得られます。もちろん[スループット](http://d.hatena.ne.jp/keyword/%A5%B9%A5%EB%A1%BC%A5%D7%A5%C3%A5%C8)増に伴ってコストは発生しますが、そもそも対応できないという状況はなくなります。
>
> #### [VPC](http://d.hatena.ne.jp/keyword/VPC)アクセスのレイテンシコスト問題
>
> これは[RDBMS](http://d.hatena.ne.jp/keyword/RDBMS)に限らない話しなのですがLambdaファンクションが[VPC](http://d.hatena.ne.jp/keyword/VPC)内のリソースにアクセスしようとしたとき、かつコールドスタートが発生したときはその仕組み上10秒〜30秒ほどのレイテンシが上乗せされます。いくらコールドスタートの発生頻度が低いとはいえ、ゼロにすることはできないです。
>
> 一方で、[RDBMS](http://d.hatena.ne.jp/keyword/RDBMS)は[VPC](http://d.hatena.ne.jp/keyword/VPC)の中に置くことが多いと思います。そうするとこのレイテンシの考慮が必要になってきます。ここはシステムの要件次第なので一概には言えないですが、DBアクセスを伴う処理がたまにとは言え10秒を超えてくることを許容できるかどうかです。
>
> #### まとめ
>
> Lambdaと[RDBMS](http://d.hatena.ne.jp/keyword/RDBMS)の組み合わせをあまり推奨しない理由を2つ挙げました。  
> もちろんそれほど同時実行されることがないのであれば最初の問題はほとんど関係ないかも知れません。また、たまに発生する10秒を超える実行時間が問題ない場合もあるでしょう。
>
> 逆に言うとそうでない限り、Lambdaと[RDBMS](http://d.hatena.ne.jp/keyword/RDBMS)を組み合わせて利用するのは止めたほうがいいです。すべてのLambdaファンクションが[RDBMS](http://d.hatena.ne.jp/keyword/RDBMS)に接続する必要がないのであればDynamoDBも併用して[RDBMS](http://d.hatena.ne.jp/keyword/RDBMS)の利用は必要最低限にするのもありですし、処理によってはLambdaファンクションのアクセス先はあくまでもDynamoDBにしてストリームを使って非同期に[RDBMS](http://d.hatena.ne.jp/keyword/RDBMS)に反映するという方法が取れるかも知れません。



{% embed url="https://dev.classmethod.jp/cloud/aws/lambda-memory-alloc-and-coldstart/" %}

{% embed url="https://qiita.com/morimop/items/cb5af1131571ba6361e2" %}

{% embed url="https://dev.classmethod.jp/articles/lambda-idempotency/" %}

\*\*\*\*

