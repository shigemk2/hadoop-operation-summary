# アイデンティティ、認証、認可

- マルチテナンシー
    - 1つの大規模なシステム中で、多くの独立したエンティティをサポートする
    - それぞれのエンティティに対して同じシステムを個別に立ち上げるコストが高い or 運用が複雑なときに有効
    - 例: 複数のデータベースを1つのデータベースサーバー内に立ち上げる機能
    - Hadoopの例: 1時間毎の実働のMapReduceジョブを実行させるために大規模なクラスタを構築したなら、概してそれらのジョブの間には空きリソースがあることにある
    - リソース状況の空きはグループにとっての損失なので、小さなクラスタ群を1つの大きなクラスタにまとめるほうが理にかなっている

### ユーザーがHadoopで何かを行う際の疑問

- ユーザーは自分を誰だと主張しているか
- そのユーザーは主張通りの存在であると証明できるか
- ユーザーが行おうとしていることはそのユーザーに対して許可されているか

- シンプルモード(デフォルト)
- セキュアモード(Kerberos経由で強力な認証をサポート)

Kerberosプロトコルを使ってユーザーやデーモン自身を認証すること

## アイデンティティ

- ユーザーがホストのオペレーションシステム上の誰であるかということ
- HDFSやMapReduceにおいて誰であるのかということ

読んでもわけのわからない認証エラー

`Exception encounterd while connectiong to the server`

## KerberosとHadoop

- Kerberosプロトコルを通して強力な認証をサポート
- サーバーが検証できる有効なKerberosのチケットを提示
- Kerberosには多くの実装と多くのプロトコル
- プリンシパル ユーザー

- KDC(Key Distribution Center)
    - 認証サーバー
    - チケット発行チケット

- Kerberosに関連する認証
    - クラスタ内のノードがお互いを認証すること
    - 人間とシステムの両方を含むユーザーがサービスとやりとりするためにクラスタにアクセスすること

- セキュリティを有効にするプロセスの概要
    + すべてのサービスを監査し、セキュリティの有効化によって問題が起こらないことを確認
    + セキュリティが有効化されていないHadoopクラスタを設定し、動作させる
    + Kerberosの環境を設定、動作させる
    + ホスト名の名前解決が正常にできていることを確認する
    + Hadoop用のKerberosプリンシパル群を作成する
    + プリンシパルのキーをキータブにエクスポートし、それらをクラスタ内の適切なノードに配布
    + Hadoopの設定ファイルを更新
    + 全サービスを再起動
    + テスト

- Kerberosの暗号化アルゴリズム
    - AES128
    - AES256
        - JCE

- core-site.xml
    - hadoop.security.authentication
    - hadoop.security.authorization

- hdfs-site.xml
    - dfs.block.access.token
    - dfs.namenode.keytab.file
    - dfs.namenode.kerberos.principal
    - dfs.namenode.kerberos.https.principal
    - dfs.https.address
    - dfs.https.port
    - dfs.datanode.keytab.file
    - dfs.datanode.kerberos.principal
    - dfs.datanode.kerberos.https.principal
    - dfs.datanode.address
    - dfs.datanode.http.address
    - dfs.datanode.data.dir.perm

- mapred-site.xml
    - mapreduce.jobtracker.kerberos.principal
    - mapreduce.jobtracker.https.principal
    - mapreduce.jobtracker.keytab.file
    - mapreduce.tasktracker.kerberos.principal
    - mapreduce.tasktracker.kerberos.https.principal
    - mapreduce.tasktracker.keytab.file
    - mapreduce.task.traker.task-controller
    - mapreduce.tasktracker.group

- taskcontroller.org
    - mapred.local.dir
    - hadoop.log.dir
    - mapred.tasktracker.group
    - min.user.id

## 認可

ある操作をユーザーが行うことが認可されているかどうかを評価する処理

### HDFS

- HDFSのパーミッション
    - 読み込み
    - 書き込み
    - 実行

### MapReduce

MapReduceのユーザー

- クラスタの所有者
- クラスタの管理者
- キューの管理者
- ジョブの所有者

- ACLの定義と有効化
    + mapred-site.xml
    + mapred-queue-acls.xml

- その他のツールとシステム
    - Apache Hive
    - Apache HBase
    - Apache Oozie
    - Hue
    - Apache Sqoop
    - Apache Flume
    - Apache ZooKeeper
    - ApackePig/Cascading/Crunch

## システムの構築

設計方針

- セキュアにするかしないか
- すべてのノード上のすべてのユーザーとグループ
- ローカルKerberosKDCの実行
- アクセスを反映したHDFSの階層の確率
- アクセス連携のためのゲートウエイサービスの使用

- セキュアにするか
