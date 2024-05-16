---
title: CRX2Oak 移行ツールの使用
description: Adobe Experience Manager での CRX2Oak 移行ツールの使用方法について説明します。このツールは、異なるリポジトリ間でデータを移行する際に役立つように設計されています。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
feature: Upgrading
exl-id: ef3895b9-8d35-4881-8188-c864ae3f0b4c
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: ht
source-wordcount: '1175'
ht-degree: 100%

---

# CRX2Oak 移行ツールの使用{#using-the-crx-oak-migration-tool}

## はじめに {#introduction}

CRX2Oak は、異なるリポジトリ間でデータを移行するために設計されたツールです。

このツールを使用すると、Apache Jackrabbit 2 をベースとする以前の CQ バージョンから Oak にデータを移行したり、Oak リポジトリ間でデータをコピーしたりできます。

最新バージョンの crx2oak は、次の場所で公開されているアドビのリポジトリからダウンロードできます。[https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/](https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/)

>[!NOTE]
>
>Apache Oak と Adobe Experience Manager（AEM）の永続性の主要な概念について詳しくは、[AEM プラットフォームの紹介](/help/sites-deploying/platform.md)を参照してください。

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

より詳細なカスタマイズが必要な場合は、個別に実行することもできます。ただし、このモードでは、変更がリポジトリに対してのみ行われるので、その他の AEM の再設定は手動で実行する必要があります。これはスタンドアロンモードと呼ばれます。

また、スタンドアロンモードのデフォルト設定では、ノードストアのみが移行され、新しいリポジトリでは古いバイナリストレージが再使用されることにも注意してください。

### 自動クイックスタートモード {#automated-quickstart-mode}

AEM 6.3 以降では、CRX2Oak でユーザー定義の移行プロファイルを処理できます。また、このプロファイルには、既に使用可能なすべての移行オプションを設定することができます。これにより、柔軟性が向上するだけでなく、AEM の設定を自動化できるようになります。このような機能は、スタンドアロンモードでツールを使用している場合には使用できません。

CRX2Oak をクイックスタートモードに切り替えるには、次のオペレーティングシステム環境変数を使用して、AEM インストールディレクトリの crx-quickstart フォルダーへのパスを定義します。

**UNIX ベースのシステムおよび macOS の場合：**

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

`CommitHooks` を使用して、カスタム Java™ ロジックを実装できます。カスタム `RepositoryInitializer` クラスを実装して、カスタム値でリポジトリを初期化できます。

#### メモリマップ操作のサポート {#support-for-memory-mapped-operations}

CRX2Oak はデフォルトで、メモリマップ操作もサポートしています。メモリマップ操作はパフォーマンスを大幅に向上させるので、可能な限り常に使用する必要があります。

>[!CAUTION]
>
>ただし、Windows プラットフォームでは、メモリマップ操作はサポートされていません。そのため、Windows で移行を実行するときには、**--disable-mmap** パラメーターを追加することが推奨されます。

#### コンテンツの選択的移行 {#selective-migration-of-content}

デフォルトでは、このツールは`"/"`パスの下にあるリポジトリ全体を移行します。しかし、どのコンテンツを移行するかは完全に制御できます。

新しいインスタンスに不要な部分がコンテンツにある場合は、 `--exclude-path` パラメーターを使用してそのコンテンツを除外し、アップグレード手順を最適化できます。

#### パスの結合 {#path-merging}

2 つのリポジトリ間でデータをコピーする必要があり、両方のインスタンス上でコンテンツパスが異なる場合は、`--merge-path` パラメーターでコンテンツパスを定義できます。定義すると、CRX2Oak は新しいノードのみをコピー先リポジトリにコピーし、古いノードは元の場所に保持します。

![chlimage_1-152](assets/chlimage_1-152.png)

#### バージョンのサポート {#version-support}

デフォルトでは、AEM は変更された各ノードまたは各ページのバージョンを作成し、リポジトリ内に保存します。これらのバージョンを使用して、ページを以前の状態に復元することができます。

ただし、元のページが削除されても、これらのバージョンはパージされません。長時間使用されているリポジトリを扱う場合は、孤立したバージョンによって生じた冗長なデータを移行で再処理することがあります。

このような状況に役立つ機能は、`--copy-versions` パラメーターを付加することです。このパラメーターを使用すると、リポジトリの移行またはコピー中に、バージョンノードをスキップできます。

`--copy-orphaned-versions=true` を付加して、孤立したバージョンをコピーするかどうかを選択することもできます。

特定の日付までのバージョンをコピーする場合、どちらのパラメーターも日付形式 `YYYY-MM-DD` をサポートしています。

![chlimage_1-153](assets/chlimage_1-153.png)

#### オープンソース版 {#open-source-version}

オープンソース版の CRX2Oak は、oak-upgrade の形で提供されています。このツールは、次の機能を除くすべての機能をサポートしています。

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
* `--ldap`：LDAP ユーザーを CQ 5.x インスタンスから Oak ベースのインスタンスに移行します。この機能を有効にするには、Oak 設定内の ID プロバイダーを ldap という名前にする必要があります。詳細情報は、[LDAP に関するドキュメント](/help/sites-administering/ldap-config.md)を参照してください。

* `--ldap-config:`：認証に複数の サーバーを使用していた CQ 5.x リポジトリに対しては、このパラメーターと `--ldap` パラメーターを併用します。このパラメーターを使用して、CQ 5.x の `ldap_login.conf` または `jaas.conf` 設定ファイルを指すことができます。形式は、`--ldapconfig=path/to/ldap_login.conf` です。

### バージョンストアオプション {#version-store-options}

* `--copy-orphaned-versions`：孤立したバージョンのコピーをスキップします。サポートされているパラメーターは、`true`、`false`、`yyyy-mm-dd` です。デフォルトは `true` です。

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

処理中に発生する可能性があるすべての問題をトラブルシューティングするために、移行プロセス用のデバッグ情報を有効にすることもできます。有効にする方法は、ツールを実行するモードによって異なります。

<table>
 <tbody>
  <tr>
   <td><strong>CRX2Oak モード</strong></td>
   <td><strong>アクション</strong></td>
  </tr>
  <tr>
   <td>クイックスタートモード</td>
   <td>CRX2Oak を実行するときに、コマンドラインに「<strong>--log-level TRACE</strong>」オプションまたは「<strong>--log-level DEBUG </strong>」オプションを追加できます。このモードでは、ログは自動的に <strong>upgrade.log ファイル</strong>にリダイレクトされます。</td>
  </tr>
  <tr>
   <td>スタンドアロンモード</td>
   <td><p>「<strong>--trace</strong>」オプションを CRX2Oak コマンドラインに追加して、標準出力に TRACE イベントを表示できるようにします（後で検査するには、リダイレクト文字：「&gt;」または「tee」コマンドを使用してログを自分でリダイレクトする必要があります）。</p> </td>
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
