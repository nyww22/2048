# マイクロサービスアーキテクチャ

### サービス間通信の信頼性を高める防御的実装-Reliability

1. 呼び出し先サービスの位置は一定ではない
   1. サービスディスカバリ
2. 一時的な呼び出しの失敗
   1. リトライ（w/ Exponential back-off）
3. 継続した呼び出しの失敗
   1. サーキットブレーカー
4. 呼び出し先サービスのパフォーマンス悪化
   1. タイムアウト
5. 呼び出し元システムの不具合
   1. スロットリング



### サービス間通信の可観測性-Obserability


