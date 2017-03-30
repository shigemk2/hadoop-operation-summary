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


