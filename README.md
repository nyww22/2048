# サーバレスアーキテクチャ

{% embed url="https://aws.amazon.com/jp/blogs/news/aws-serverless-application-model-sam-command-line-interface-build-test-and-debug-serverless-apps-locally/" %}



### AWSにおける サーバーレス構成 <a id="p02"></a>

> AWSにおいてのサーバーレス構成は、「Amazon S3、DynamoDB、Lambda これらの活用によって、EC2などの仮想化インスタンスサーバーを使わずにWEBサービスを開発する論理的構造\(アーキテクチャ\)」となります。
>
> 「サーバーレス」というのは、Amazon S3、Lambda 等のサービスが、サーバーを使用していない…ということではありません。これらのサービスももちろんAWSサーバー上で動いています。しかし、システム運用の為に、EC2使用時の様に、固定スケールのサーバー領域の常時稼働を必要としている訳ではありません。「サーバーレス」の定義としては、ユーザーがサーバー領域を意識せず、直接利用出来るサービスを活用した構成、と言えるでしょう。

###  AWS の「EC2」と「Lambda」の違い <a id="p03"></a>

> EC2インスタンスを利用する場合、起動直後はOSがインストールされただけの状態となり、システムを稼働させるには、アカウントの初期設定を始め、各種ミドルウェアをインストールするなどの、環境構築が必要となります。しかし、Lambdaを利用した場合、AWSの提供した実行環境の中で起動する為、プログラムさえ用意すれば、すぐに使用が可能となります。
>
> また、料金も、システムの実行時間のみの課金になりますので、コストの削減が期待出来ます。
>
> #### EC2 インスタンス
>
> ![&#x30B5;&#x30FC;&#x30D0;&#x30FC;&#x30EC;&#x30B9;&#x6BD4;&#x8F03;](https://www.skyarch.net/iot/asset/serverless_icon01.png?v=20190416)
>
> * 汎用的なサーバー
> * 起動直後はOSインストールのみの状態
> * 初期設定、環境設定が必要
> * システムの運用、保守、監視が必要
> * 利用出来るのは契約したサーバーの容量
> * 一定料金。仮想サーバー稼働時間内の代金
>
> #### Lambda
>
> ![Lambda](https://www.skyarch.net/iot/asset/serverless_icon02.png?v=20190416)
>
> * インフラ環境の整備、必要無し
> * 実行環境は、AWSが提供
> * ミドルウェア等の脆弱性対応不要
> * トリガを選択し、プログラムをアップロードすれば直ちに動作
> * 自動スケーリング対応
> * システムを実行時間（100ミリ秒単位）で課金
> * 利用されなければ無課金



### 「Lambda」とAWSサービス <a id="p04"></a>

> 「Lambda」は、AWS環境にすでに用意されている多種多様なサービスと連携して利用する事が出来ます。基本的なWEBサービスの土台はそろっていますので、最小限のプログラミングでシステムを構築する事ができ、運用を始める事が出来ます。
>
> #### 「Lambda」に組み合わせて使用出来る代表的なAWSサービス
>
> ![AWS Lambda](https://www.skyarch.net/iot/asset/serverless_lambda01.png?v=20190416)



### 「Lambda」の特性 <a id="p05"></a>

> 「Lambda」は設定されているプログラムを起動させる実行環境となります。起動条件が整った際に、プログラムをLambda環境に呼び出し、実行されます。この為、Lambdaでは、実行した時間とその回数のみの課金となります。ですから、待機時間の長いシステムや、CPUの負荷が時間帯によって差のあるシステムなどに導入すれば、大幅なコストの削減が期待できます。
>
> しかし、ゲームアプリや配信系サービスなど、常にシステムの動いている必要のあるサービスや、高負荷な状態が長時間続くシステムなどでは、Lambda、すなわちサーバーレス構成は不向きなものと言えます。



### サーバーレス構造・実績 <a id="p06"></a>

> #### 大量のアクセスを捌くアーキテクチャ
>
> 下記はある企業のサイトで実装した、サーバーレスの導入例です。ネットでの注文のデータを今後に活かす為、データベースに蓄積するシステムになります。これをオンプレミス\(自社運用\)で賄おうとすると膨大なサーバーが必要となります。そこでAWSを利用した実装を考察しましたが、システムの常時起動、AutoScaleによる負荷の対応、RDSの同時接続数などの課題が上りました。
>
> ![&#x30B5;&#x30FC;&#x30D0;&#x30FC;&#x30EC;&#x30B9;](https://www.skyarch.net/iot/asset/serverless_lambda02.png?v=20190416)
>
> 上記を踏まえ、サーバーレス構成での実装です。API Gatewayでリクエストを受けた際にLambdaを起動。処理したデータをAWS環境のSQSにてキューとして一旦保存。このキューをもう一つのLambdaの定期実行によりチェックして、データべースに保存する、という構成です。リクエストと定期時実行によるLambdaの起動で、運用コストの削減が期待でき、キューイングによる保存処理によって、データベースへの負荷を軽減します。![&#x30B5;&#x30FC;&#x30D0;&#x30FC;&#x30EC;&#x30B9;](https://www.skyarch.net/iot/asset/serverless_lambda03.png?v=20190416)
>
> このように部分部分でシステムを分割し、疎結合なアーキテクチャを採用する事で、下記のようなメリットを享受する事ができます。
>
> * 大量のアクセスを捌くことが可能となる
> * 並行開発が可能となる
> * メンテナンスを容易に実施出来る
>
> #### サーバレスアーキテクチャの動作確認
>
> リクエスト結果をS3へファイル保存を行うサーバレス構成を元にサーバレス構成の監視方法をご説明します。
>
> ![&#x30B5;&#x30FC;&#x30D0;&#x30FC;&#x30EC;&#x30B9;](https://www.skyarch.net/iot/asset/serverless_lambda04.png?v=20190416)
>
> Lambdaより、定期実行でサンプルリクエストをして、正しい流れでS3へのデータ保存が出来ているかを監視します。異常が検知された際には、管理者へアラートメールが送られます。



### Useful Frameworks for Serverless Web Apps

#### Java - HttpServlet, Spring, Spark and Jersey

{% embed url="https://github.com/awslabs/aws-serverless-java-container" %}



### 参考サイト

{% embed url="https://dev.classmethod.jp/cloud/aws/aws-reinvent-arc401/" %}

{% embed url="https://www.skyarch.net/iot/serverless.html" %}



