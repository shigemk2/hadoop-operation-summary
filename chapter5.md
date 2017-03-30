# インストールと設定

- 前準備
    - バージョン
    - ディストリビューション
    - デーモン
    - 場所
- taballは柔軟だけど曖昧かつ複雑
- RPMかDebパッケージから

- インストールの選択肢
    - Apache Hadoop
    - CDH

## 設定の概要

- 設定の柔軟性がすごく高い
- 開発者が知っておくべきパラメータ 10 vs 管理者が知っておくべきパラメータ 150

- hadoop-env.sh
- core-site.xml
- hdfs-site.xml
- mapred-site.xml
- log4j.properties
- masters
- slaves
- fair-scheduler.xml
- capacity-scheduler.xml
- dfs.include
- dfs.exclude
- hadoop-policy.xml
- mapred-queue-acls.xml
- taskcontroller.cfg

## 環境変数とシェルスクリプト

- 多くの環境変数を使う
- hadoop-env.sh

## ログの設定

- ほとんどあらゆる部分でlog4jが使われている
    - 設定ファイルはlog4j.properties
    - 設定は結構複雑

## HDFS

- プロパティ群はほとんどhdfs-site.xmlで設定されている
    - fs.default.name
    - dfs.name.dir
    - dfs.data.dir
    - fs.checkpoint.dir
    - dfs.permissions.supergroup
    - io.file.buffer.size
    - dfs.balance.bandwidthPerSec
    - dfs.block.size
    - dfs.datanode.du.reserved
    - dfs.namenode.handler.count
    - dfs.datanode.failed.volumes.tolerated
    - dfs.hosts
    - dfs.host.exclude
    - fs.trash.interval

## 高可用性ネームノード

ネームノードサービスに中断が生じるとHDFSのサービスが中断する。Hadoop2.0.0/CDH4で高可用性ネームノードが使えるようになった

- NFSファイラー

## ネームノードフェデレーション

- Hadoop 2.0 / CDH4

- HA: 単一の名前空間を2台のネームノードのどちらかが提供
- ネームノードフェデレーション: 大規模な名前空間の別々の断片を複数のネームノードが提供

- hdfs-site.xmlのdfs.nameservices
- ViewFS

## MapReduce

特に指定していない場合mapred-site.xmlに設定

- mapred.job.tracker
- mapred.local.dir

チューニング

- mapred.child.java.opts
- mapred.child.ulimit
- mapred.tasktracker.map.tasks.maximum
- mapred.tasktracker.reduce.tasks.maximum
- io.sort.mb
- mapred.compress.map.output
- mapred.map.output.compression.codec
- mapred.output.compression.type
- mapred.job.tracker.handler.count
- mapred.jobtracker.taskScheduler
- mapred.reduce.parallel.copies
- mapred.reduce.tasks
- tasktracker.http.threads
- mapred.reduce.slowstart.completed.maps

## ラックのトポロジー

マシン群がデータセンターのラックにどのような物理的配置で置かれているかを定義するもの

