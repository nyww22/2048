# DynamoDB

![](.gitbook/assets/image%20%2836%29.png)

![](.gitbook/assets/image%20%2855%29.png)

![](.gitbook/assets/image%20%2858%29.png)

![](.gitbook/assets/image%20%2810%29.png)

![](.gitbook/assets/image%20%286%29.png)

![](.gitbook/assets/image%20%2819%29.png)

![](.gitbook/assets/image%20%2831%29.png)

#### 

#### Design Pattern

![](.gitbook/assets/image%20%2856%29.png)

Relational DB   
正規化が重要。データは柔軟にクエリができる。  
ただし、クエリはコストが高くとらふっぃくが多い状況ではスケールがうまくいかないケースがある。実装の詳細やパフォーマンスを気にせず柔軟に設計は可能。クエリの最適化には、スキーマ設計に影響はないが、正規化が重要となる。

DynamoDB   
具体的にスキーマ設計を行っていく。  
データは限られた範囲で、検索は可能。フィルタをかけるや、全件検索するのは高コスト。もっとも一般的で重要なクエリをできるだけ早く、より低コストにするため具体的にスキーマ設計を行う。データ構造は具体的なビジネスユースケースにあわせて調整をしていく。

  
  


![](.gitbook/assets/image%20%2833%29.png)

![](.gitbook/assets/image%20%2811%29.png)

![](.gitbook/assets/image%20%2860%29.png)

![](.gitbook/assets/image%20%2832%29.png)

![](.gitbook/assets/image%20%2817%29.png)

FILTERはあくまでも全部取得して、抜き出すので、非常にコストがかかる。  
  


![](.gitbook/assets/image%20%2813%29.png)

![](.gitbook/assets/image%20%2825%29.png)

![](.gitbook/assets/image%20%2854%29.png)

FILTERより圧倒的にコストが安くなる方法。



![](.gitbook/assets/image%20%2837%29.png)

![](.gitbook/assets/image%20%2857%29.png)

![](.gitbook/assets/image%20%2820%29.png)

![](.gitbook/assets/image%20%2835%29.png)

![](.gitbook/assets/image%20%2824%29.png)

![](.gitbook/assets/image%20%2839%29.png)

![](.gitbook/assets/image%20%2838%29.png)

![](.gitbook/assets/image%20%2853%29.png)



![](.gitbook/assets/image%20%2851%29.png)

![](.gitbook/assets/image%20%2827%29.png)

![](.gitbook/assets/image%20%2844%29.png)

![](.gitbook/assets/image%20%2822%29.png)

![](.gitbook/assets/image%20%2845%29.png)

![](.gitbook/assets/image%20%2829%29.png)

データサイズが大きいものということで、S3と連携させる方法もある。



![](.gitbook/assets/image%20%2823%29.png)

![](.gitbook/assets/image%20%2840%29.png)

![](.gitbook/assets/image%20%2821%29.png)

![](.gitbook/assets/image%20%2816%29.png)

![](.gitbook/assets/image%20%287%29.png)

![](.gitbook/assets/image%20%2826%29.png)

![](.gitbook/assets/image%20%2848%29.png)

![](.gitbook/assets/image%20%2812%29.png)

![](.gitbook/assets/image%20%2818%29.png)

![](.gitbook/assets/image%20%2846%29.png)

![](.gitbook/assets/image%20%289%29.png)

![](.gitbook/assets/image%20%2863%29.png)

![](.gitbook/assets/image%20%2830%29.png)

![](.gitbook/assets/image%20%2815%29.png)

![](.gitbook/assets/image%20%2828%29.png)

![](.gitbook/assets/image%20%2842%29.png)

![](.gitbook/assets/image%20%2849%29.png)

![](.gitbook/assets/image%20%288%29.png)



![](.gitbook/assets/image%20%2861%29.png)

![](.gitbook/assets/image%20%2814%29.png)

![](.gitbook/assets/image%20%2841%29.png)

![](.gitbook/assets/image%20%2847%29.png)

![](.gitbook/assets/image%20%2843%29.png)

![](.gitbook/assets/image%20%2862%29.png)

![](.gitbook/assets/image%20%2850%29.png)

![](.gitbook/assets/image%20%2834%29.png)

{% embed url="https://aws.amazon.com/jp/blogs/news/how-to-use-dynamodb-global-secondary-indexes-to-improve-query-performance-and-reduce-costs/" %}





