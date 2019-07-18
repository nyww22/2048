# Security

### SSL証明書・サーバ証明書

SSL証明書とルート証明書の関係

{% file src=".gitbook/assets/wp-sslandroot-certificate.pdf" %}



[認証\(Authentication, Authn\)と承認\(認可, Authorization, Authz\)の違い](http://d.hatena.ne.jp/end0tknr/20110104/1294112345)

{% hint style="info" %}
認証（Authn）と認可（Authz）

認証：個人の身元の確認  
認可：誰かに許可を与えること
{% endhint %}



![Authz&#xFF08;&#x8A8D;&#x53EF;&#xFF09;&#x3068;AWS Lambda&#x306E;&#x7D44;&#x307F;&#x5408;&#x308F;&#x305B;](.gitbook/assets/image%20%284%29.png)

![OpenID&#x3068;AWS Lambda&#x306E;&#x7D44;&#x307F;&#x5408;&#x308F;&#x305B;](.gitbook/assets/image%20%281%29.png)

![Amazon Cognito&#x306B;&#x3088;&#x308B;Authz&#x306E;&#x4ED5;&#x7D44;&#x307F;](.gitbook/assets/image%20%283%29.png)



識別・認証・認可の３フェーズによるアクセス制御

{% embed url="https://enterprisezine.jp/article/detail/8049" %}



### Refresh Tokenの仕組み

{% embed url="https://auth0.com/blog/jp-refresh-tokens-what-are-they-and-when-to-use-them/" %}



### 認証（ID連携）

{% embed url="https://techblog.yahoo.co.jp/web/auth/id\_federation\_impl\_patterns/" %}



### OAuth認証とは

OAuthは認可の仕組みであるが、OAuthを使って『誰が？』にあたる部分のユーザ識別を行う仕組みです。

{% embed url="https://qiita.com/TakahikoKawasaki/items/f2a0d25a4f05790b3baa" %}



### IDトークンとアクセストークンの使い道の違い

{% embed url="https://qiita.com/wadahiro/items/ad36c7932c6627149873" %}



### OAuth認証の脆弱性について

{% embed url="https://www.sakimura.org/2012/02/1487/" %}

{% embed url="https://ritou.hatenablog.com/entry/2018/11/12/110613" %}

{% embed url="https://www.atmarkit.co.jp/ait/articles/1710/24/news011.html" %}



### シングルサインオンについて

{% embed url="https://www.ogis-ri.co.jp/pickup/themistruct/note/note\_sso01.html" %}



