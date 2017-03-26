# Hadoopクラスタの計画
## Hadoopディストリビューションとバージョンの選択

- ディストリビューションとバージョンの選択は計画を立てるうえで非常に重要
- Cloudera Distribution Including Apache Hadoop(CDH)

- 実用品質
- HDFSのアペンド
- Kerberosのセキュリティ
- HDFSのシンボリックリンク
- YARN
- MRv1のデーモン
- ネームノードフェデレーション
- 高可用性ネームノード

- バージョン
- マスターのハードウェア
- ワーカーのハードウェア
- クラスタのサイジング
- ブレード/SAN/仮想化

## オペレーティングシステムの選択と準備

稼働例

- RHEL
- Ubuntu
- SuSE
- Debian

### ディレクトリ群

- ホームディレクトリ
- データノード用データディレクトリ
- ネームノード用ディレクトリ
- MapReduce用ローカルディレクトリ
- ログディレクトリ
- pidディレクトリ
- tempディレクトリ

### ソフトウェア

- cron
- ntp
- ssh
- postfix/sendmail
- rsync

### ホスト名/DNS/識別

- この扱いはきわめて気難しい

### ユーザー/グループ/権限

- hdfs
- mapred

など

## カーネルのチューイング

注意しておかないといけないパラメーター

- vm.swappiness
- vm.overcommit_memory

## ディスクの構成

- ext3
- ext4
- xfs

## ネットワークの設計

- HDFS
- MapReduce
- ネットワークトポロジー
- スパインファブリック

