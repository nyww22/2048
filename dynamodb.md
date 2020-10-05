# DynamoDB

![](.gitbook/assets/image%20%2810%29.png)

![](.gitbook/assets/image%20%2811%29.png)

![](.gitbook/assets/image%20%2813%29.png)

![](.gitbook/assets/image%20%287%29.png)

![](.gitbook/assets/image%20%286%29.png)

![](.gitbook/assets/image%20%288%29.png)

![](.gitbook/assets/image%20%289%29.png)

#### 

#### Design Pattern

![](.gitbook/assets/image%20%2812%29.png)

Relational DB   
正規化が重要。データは柔軟にクエリができる。  
ただし、クエリはコストが高くとらふっぃくが多い状況ではスケールがうまくいかないケースがある。実装の詳細やパフォーマンスを気にせず柔軟に設計は可能。クエリの最適化には、スキーマ設計に影響はないが、正規化が重要となる。

DynamoDB   
具体的にスキーマ設計を行っていく。  
データは限られた範囲で、検索は可能。フィルタをかけるや、全件検索するのは高コスト。もっとも一般的で重要なクエリをできるだけ早く、より低コストにするため具体的にスキーマ設計を行う。データ構造は具体的なビジネスユースケースにあわせて調整をしていく。

  
  




