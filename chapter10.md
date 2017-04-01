# モニタリング
## 10-1 概要

モニタリングシステムの組み込みは重要

- メトリクスの収集
- メトリクスの結果のデータを利用するぶぶん

## 10-2 Hadoopのメトリクス

さまざまなメトリクスが組み込まれている

### metrics1

- jvm
- dfs
- mapred
- rpc
    - リモートプロシージャコールのメトリクス
- jmxサーブレットの利用

### metrics2

- SNMP
   - サービスやデバイスからメトリクスを取り出すための標準規格

## 10-3 健全性のモニタリング

- メトリクスの取捨選択
    - それぞれのサービスの健全性を最も的確に表しているのがどのメトリクスであるのか
    - アラートの状態にあることを示す閾値の設定も重要
    - 闇雲にすべてのメトリクスを監視しても意味がない
- 基本的なルール
    - すべての閾値は流動的なもの
    - 新しいクラスタでは、まずは安全な値を閾値にし、利用状況を測定し、時間の経過とともに制度を高める
    - アラートのノイズ比率を低くすること

### ホストのレベルでのチェック

- dfs.name.dir
- HADOOP_LOG_DIR
- dfs.data.dir
- mapred.local.dir
- スワップアウトされた毎秒のページ数
- CPUのメトリクス パフォーマンスは計測するがアラートを出してはいけない
- ネットワークのレイテンシー
- **プロセスの存在チェックはしあいで、デーモン及びサービスレベルのメトリクスのチェックに任せる**

### Hadoopのプロセスのチェック

- ネームノード/ジョブトラッカー/セカンダリネームノードのプロセスに対してヒープのモニタリング
- ネームノードとジョブトラッカーについて、ガベージコレクションの実行にかかった平均時間のモニタリング

### HDFSのチェック

-
- HDFSの空き容量の絶対値(Free)が妥当な閾値以上か
- メタデータのパスの絶対数がdfs.name.dirで指定されているパスの数と一致すること
- MissingBlocksとCorruptBlocksが妥当な閾値より低い
- BlockCapacityの確認
- LastCheckpointTimeが3日以内

### MapReduceのチェック

- 稼働数ノードの総数がサービスレベルアグリーメントを満たすようにジョブを実行できる値になっていること
- ブラックリスト入りしているタスクトラッカー数がクラスタ内のタスクトラッカー数に対して一定のパーセンテージ以下になっていること