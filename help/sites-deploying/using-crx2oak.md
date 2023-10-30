---
title: CRX2Oak 移行ツールの使用
description: CRX2Oak 移行ツールをAdobe Experience Managerと共に使用する方法を説明します。 このツールは、異なるリポジトリ間でデータを移行する際に役立つように設計されています。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
feature: Upgrading
exl-id: ef3895b9-8d35-4881-8188-c864ae3f0b4c
source-git-commit: ee1134be6ad81cc6638ee9004f7dad475a6cc67d
workflow-type: tm+mt
source-wordcount: '1208'
ht-degree: 67%

---

# CRX2Oak 移行ツールの使用{#using-the-crx-oak-migration-tool}

## はじめに {#introduction}

CRX2Oak は、異なるリポジトリ間でデータを移行するために設計されたツールです。

このツールを使用すると、Apache Jackrabbit 2 をベースとする以前の CQ バージョンから Oak にデータを移行したり、Oak リポジトリ間でデータをコピーしたりできます。

最新バージョンの crx2oak は、次の場所で公開されているアドビのリポジトリからダウンロードできます。[https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/](https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/)

>[!NOTE]
>
>Apache Oak とAdobe Experience Manager(AEM) 永続性の主要概念について詳しくは、 [AEM Platform の概要](/help/sites-deploying/platform.md).

## 移行のユースケース {#migration-use-cases}

このツールは、次の目的で使用できます。

* 以前の CQ 5 バージョンから AEM 6 への移行
* 複数の Oak リポジトリ間でのデータのコピー
* 異なる Oak MicroKernel 実装間でのデータの変換

外部の BLOB ストア（通称データストア）を使用したリポジトリの移行に関するサポートは、様々な組み合わせで提供されています。考えられる移行パスの 1 つは、外部 `FileDataStore` を使用する CRX2 リポジトリから `S3DataStore` を使用する Oak リポジトリへの移行です。

下の図に、CRX2Oak がサポートしているすべての移行の組み合わせを示します。

![chlimage_1-151](assets/chlimage_1-151.png)

## 機能 {#features}

ユーザーは、AEM のアップグレード中に CRX2Oak を呼び出し、事前定義済みの移行プロファイルを指定することで、永続化モードの再設定を自動化することができます。これはクイックスタートモードと呼ばれます。

より詳細なカスタマイズが必要な場合は、個別に実行することもできます。ただし、このモードでの変更はリポジトリに対してのみおこなわれ、AEMの追加の再構成は手動で実行する必要があります。 これはスタンドアロンモードと呼ばれます。

もう 1 つ注意すべき点は、スタンドアロンモードのデフォルト設定では、ノードストアのみが移行され、新しいリポジトリが古いバイナリストレージを再利用する点です。

### 自動クイックスタートモード {#automated-quickstart-mode}

AEM 6.3 以降、CRX2Oak は、すでに使用可能なすべての移行オプションを使用して設定できる、ユーザー定義の移行プロファイルを処理できます。 これにより、柔軟性が向上するだけでなく、AEM の設定を自動化できるようになります。このような機能は、スタンドアロンモードでツールを使用している場合には使用できません。

CRX2Oak をクイックスタートモードに切り替えるには、次のオペレーティングシステム環境変数を使用して、AEMインストールディレクトリ内の crx-quickstart フォルダーへのパスを定義します。

**UNIX ベースのシステムおよびmacOSの場合：**

```shell
export SLING_HOME="/path/to/crx-quickstart"
```

**Windows の場合：**

```shell
SET "SLING_HOME=/path/to/crx-quickstart"
```

#### サポートの再開 {#resume-support}

移行はいつでも中断でき、後で再開できます。

#### カスタマイズ可能なアップグレードロジック {#customizable-upgrade-logic}

カスタム Java™ロジックは `CommitHooks`. カスタム `RepositoryInitializer` クラスを実装して、カスタム値でリポジトリを初期化できます。

#### メモリマップ操作のサポート {#support-for-memory-mapped-operations}

CRX2Oak は、デフォルトでメモリマッピング操作もサポートします。 メモリマップ操作はパフォーマンスを大幅に向上させるので、可能な限り常に使用する必要があります。

>[!CAUTION]
>
>ただし、Windows プラットフォームでは、メモリマッピング操作はサポートされていません。 そのため、Windows で移行を実行するときには、**--disable-mmap** パラメーターを追加することが推奨されます。

#### コンテンツの選択的移行 {#selective-migration-of-content}

デフォルトでは、このツールは`"/"`パスの下にあるリポジトリ全体を移行します。しかし、どのコンテンツを移行するかは完全に制御できます。

新しいインスタンスに不要な部分がコンテンツにある場合は、 `--exclude-path` パラメーターを使用してそのコンテンツを除外し、アップグレード手順を最適化できます。

#### パスの結合 {#path-merging}

2 つのリポジトリ間でデータをコピーする必要があり、両方のインスタンスで異なるコンテンツパスを持つ場合は、 `--merge-path` パラメーター。 その場合、CRX2Oak は新しいノードのみを宛先リポジトリにコピーし、古いノードを配置したままにします。

![chlimage_1-152](assets/chlimage_1-152.png)

#### バージョンのサポート {#version-support}

デフォルトでは、AEMは、変更された各ノードまたはページのバージョンを作成し、リポジトリに保存します。 これらのバージョンを使用して、ページを以前の状態に復元することができます。

ただし、元のページが削除されても、これらのバージョンはパージされません。長時間稼働しているリポジトリを処理する場合、移行は、孤立したバージョンが原因で発生した冗長データを再処理する場合があります。

このような状況に役立つ機能は、`--copy-versions` パラメーターを付加することです。このパラメーターを使用すると、リポジトリの移行またはコピー中に、バージョンノードをスキップできます。

`--copy-orphaned-versions=true` を付加して、孤立したバージョンをコピーするかどうかを選択することもできます。

特定の日付までのバージョンをコピーする場合、どちらのパラメーターも日付形式 `YYYY-MM-DD` をサポートしています。

![chlimage_1-153](assets/chlimage_1-153.png)

#### オープンソース版 {#open-source-version}

CRX2Oak のオープンソースバージョンは、oak-upgrade の形式で利用できます。 このツールは、次の機能を除くすべての機能をサポートしています。

* CRX2 サポート
* 移行プロファイルのサポート
* 自動 AEM 再設定のサポート

詳細情報は、[Apache に関するドキュメント](https://jackrabbit.apache.org/oak/docs/migration.html)を参照してください。

## パラメーター {#parameters}

### ノードストアオプション {#node-store-options}

* `--cache`：MB 単位でのキャッシュサイズ（デフォルトは `256`）

* `--mmap`：セグメントストア用のメモリマップファイルアクセスを有効化します
* `--src-password:`：ソース RDB データベースのパスワード

* `--src-user:`：ソース RDB のユーザー

* `--user`：ターゲット RDB のユーザー

* `--password`：ターゲット RDB のパスワード

### 移行オプション {#migration-options}

* `--early-shutdown`：ノードのコピー後、コミットフックの適用前に、ソース JCR2 リポジトリをシャットダウンします
* `--fail-on-error`：ソースリポジトリからノードを読み取れない場合、強制的に移行を失敗させます。
* `--ldap`：LDAP ユーザーを CQ 5.x インスタンスから Oak ベースのインスタンスに移行します。これを機能させるには、Oak 設定の ID プロバイダーを ldap という名前にする必要があります。 詳細情報は、[LDAP に関するドキュメント](/help/sites-administering/ldap-config.md)を参照してください。

* `--ldap-config:` これを `--ldap` 複数の LDAP サーバーを認証に使用した CQ 5.x リポジトリのパラメーター。 このパラメーターを使用して、CQ 5.x の `ldap_login.conf` または `jaas.conf` 設定ファイルを指すことができます。形式は、`--ldapconfig=path/to/ldap_login.conf` です。

### バージョンストアオプション {#version-store-options}

* `--copy-orphaned-versions`：孤立したバージョンのコピーをスキップします。次のパラメーターがサポートされています。 `true`, `false`、および `yyyy-mm-dd`. デフォルトは `true` です。

* `--copy-versions:`：バージョンストレージをコピーします。サポートされているパラメーターは、`true`、`false`、`yyyy-mm-dd` です。デフォルトは `true` です。

#### パスオプション {#path-options}

* `--include-paths:`：コピー時に含めるパスのコンマ区切りのリスト
* `--merge-paths`：コピー時に結合するパスのコンマ区切りのリスト
* `--exclude-paths:`：コピー時に除外するパスのコンマ区切りのリスト

### コピー元 BLOB ストアオプション {#source-blob-store-options}

* `--src-datastore:`：ソース `FileDataStore` として使用するデータストアディレクトリ

* `--src-fileblobstore`：ソース `FileBlobStore` として使用するデータストアディレクトリ

* `--src-s3datastore`：ソース `S3DataStore` として使用するデータストアディレクトリ

* `--src-s3config`：ソース `S3DataStore` の設定ファイル

### コピー先 BlobStore オプション {#destination-blobstore-options}

* `--datastore:`：ターゲット `FileDataStore` として使用するデータストアディレクトリ

* `--fileblobstore:`：ターゲット `FileBlobStore` として使用するデータストアディレクトリ

* `--s3datastore`：ターゲット `S3DataStore` として使用するデータストアディレクトリ

* `--s3config`：ターゲット `S3DataStore` の設定ファイル

### ヘルプオプション {#help-options}

* `-?, -h, --help:`：ヘルプ情報を表示します。

## デバッグ {#debugging}

また、移行プロセスのデバッグ情報を有効にして、プロセス中に発生する可能性のある問題のトラブルシューティングをおこなうこともできます。 有効にする方法は、ツールを実行するモードによって異なります。

<table>
 <tbody>
  <tr>
   <td><strong>CRX2Oak モード</strong></td>
   <td><strong>アクション</strong></td>
  </tr>
  <tr>
   <td>クイックスタートモード</td>
   <td>CRX2Oak を実行するときに、コマンドラインに「<strong>--log-level TRACE</strong>」オプションまたは「<strong>--log-level DEBUG </strong>」オプションを追加できます。このモードでは、ログは自動的に <strong>upgrade.log ファイル</strong>.</td>
  </tr>
  <tr>
   <td>スタンドアロンモード</td>
   <td><p>次を追加： <strong>—trace</strong> CRX2Oak コマンドラインに対するオプションを使用して、標準出力にTRACEイベントを表示できます（後の検査では、リダイレクト文字「&gt;」または「tee」を使用してログを自分でリダイレクトする必要があります）。</p> </td>
  </tr>
 </tbody>
</table>

## その他の注意点 {#other-considerations}

MongoDB 複製セットに移行する場合は、Mongo データベースへのすべての接続で、`WriteConcern` パラメーターを `2` に設定します。

次のように、接続文字列の末尾に `w=2` パラメーターを付加することによって設定できます。

```xml
java -Xmx4092m -jar crx2oak.jar crx-quickstart/repository/ mongodb://localhost:27017/aem-author?replicaset=replica1&w=2
```

>[!NOTE]
>
>詳しくは、MongoDB の接続文字列に関するドキュメントで[書き込み上の懸念](https://docs.mongodb.org/manual/reference/connection-string/#write-concern-options)について参照してください。
