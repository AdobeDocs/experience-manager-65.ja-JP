---
title: CRX2Oak 移行ツールの使用
seo-title: Using the CRX2Oak Migration Tool
description: CRX2Oak 移行ツールの使用方法を説明します。
seo-description: Learn how to use the CRX2Oak migration tool.
uuid: 9b788981-4ef0-446e-81f0-c327cdd3214b
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: e938bdc7-f8f5-4da5-81f6-7f60c6b4b8e6
feature: Upgrading
exl-id: ef3895b9-8d35-4881-8188-c864ae3f0b4c
source-git-commit: c0574b50f3504a4792405d6fcd8aa3a2e8e6c686
workflow-type: tm+mt
source-wordcount: '1248'
ht-degree: 100%

---

# CRX2Oak 移行ツールの使用{#using-the-crx-oak-migration-tool}

## はじめに {#introduction}

CRX2Oak は、異なるリポジトリ間でデータを移行するために設計されたツールです。

このツールを使用して、Apache Jackrabbit 2 をベースとする以前の CQ バージョンから Oak にデータを移行したり、Oak リポジトリ間でデータをコピーしたりできます。

最新バージョンの crx2oak は、次の場所で公開されているアドビのリポジトリからダウンロードできます。[https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/](https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/)

最新バージョンの変更点と修正点の一覧は、[CRX2Oak のリリースノート](https://docs.adobe.com/content/help/ja/experience-manager-64/release-notes/crx2oak.html)にあります。

>[!NOTE]
>
>Apache Oak と AEM の永続性の主要な概念について詳しくは、[AEM プラットフォームの紹介](/help/sites-deploying/platform.md)を参照してください。

## 移行のユースケース {#migration-use-cases}

このツールでは以下のことが可能です。

* 以前の CQ 5 バージョンから AEM 6 への移行
* 複数の Oak リポジトリ間でのデータのコピー
* 異なる Oak マイクロカーネル実装間でのデータの変換

外部の BLOB ストア（一般的にはデータストアとして知られる）を使用したリポジトリ移行のサポートは、様々な組み合わせで提供されています。考えられる移行パスの 1 つは、外部 `FileDataStore` を使用する CRX2 リポジトリから `S3DataStore` を使用する Oak リポジトリへの移行です。

下の図に、CRX2Oak がサポートしているすべての移行の組み合わせを示します。

![chlimage_1-151](assets/chlimage_1-151.png)

## 機能 {#features}

CRX2Oak は AEM のアップグレード中に呼び出され、このとき、永続性モードの再設定を自動化する事前定義済みの移行プロファイルをユーザーが指定できます。これはクイックスタートモードと呼ばれます。

より詳細なカスタマイズが必要な場合は、CRX2Oak を個別に実行することもできます。ただし、このモードでは、変更はリポジトリに対してのみ加えられるので、その他の AEM の再設定は手動で実行する必要があります。これはスタンドアロンモードと呼ばれます。

また、スタンドアロンモードのデフォルト設定では、ノードストアのみが移行され、新しいリポジトリは古いバイナリストレージを再使用することにも注意してください。

### 自動クイックスタートモード {#automated-quickstart-mode}

AEM 6.3 以降、CRX2Oak はユーザー定義の移行プロファイルを処理できるようになりました。このプロファイルには、既に使用可能なすべての移行オプションを設定できます。これにより、柔軟性が向上すると同時に、AEM の設定を自動化できます。スタンドアロンモードでこのツールを使用している場合は、このような機能は使用できません。

CRX2Oak をクイックスタートモードに切り替えるには、次のオペレーティングシステム環境変数を使用して、AEM インストールディレクトリの crx-quickstart フォルダーへのパスを定義する必要があります。

**UNIX ベースのシステムおよび Mac OS の場合**

```shell
export SLING_HOME="/path/to/crx-quickstart"
```

**Windows の場合：**

```shell
SET "SLING_HOME=/path/to/crx-quickstart"
```

#### サポートの再開 {#resume-support}

移行はいつでも中断でき、後で再開することができます。

#### カスタマイズ可能なアップグレードロジック {#customizable-upgrade-logic}

`CommitHooks`を使用して、カスタム Java ロジックも実装できます。カスタム `RepositoryInitializer` クラスを実装して、カスタム値でリポジトリを初期化できます。

#### メモリマップ操作のサポート {#support-for-memory-mapped-operations}

CRX2Oak はデフォルトで、メモリマップ操作もサポートしています。メモリマップはパフォーマンスを大幅に向上させるので、可能な場合は常に使用する必要があります。

>[!CAUTION]
>
>ただし、メモリマップ操作は Windows プラットフォームではサポートされないことに注意してください。そのため、Windows で移行を実行するときには、**--disable-mmap** パラメーターを追加することが推奨されます。

#### コンテンツの選択的移行 {#selective-migration-of-content}

デフォルトでは、このツールは`"/"`パスの下にあるリポジトリ全体を移行します。しかし、どのコンテンツを移行するかは完全に制御できます。

新しいインスタンスに不要な部分がコンテンツにある場合は、 `--exclude-path` パラメーターを使用してそのコンテンツを除外し、アップグレード手順を最適化できます。

#### パスの結合 {#path-merging}

2 つのリポジトリ間でデータをコピーする必要があり、両方のインスタンス上でコンテンツパスが異なる場合は、`--merge-path` パラメーターでコンテンツパスを定義できます。定義すると、CRX2Oak は新しいノードのみをコピー先リポジトリにコピーし、古いノードは元の場所に保持します。

![chlimage_1-152](assets/chlimage_1-152.png)

#### バージョンのサポート {#version-support}

デフォルトでは、AEM は変更されたノードまたはページごとにバージョンを作成し、リポジトリ内に保存します。これらのバージョンを使用して、ページを以前の状態に復元できます。

ただし、元のページが削除されても、これらのバージョンはパージされません。長時間使用されているリポジトリを扱う場合は、孤立したバージョンによって生じた多数の冗長なデータを移行で処理しなければならないことがあります。

このような状況に役立つ機能は、`--copy-versions` パラメーターを付加することです。このパラメーターを使用すると、リポジトリの移行またはコピー中に、バージョンノードをスキップできます。

`--copy-orphaned-versions=true` を付加して、孤立したバージョンをコピーするかどうかを選択することもできます。

特定の日付までのバージョンをコピーする場合、どちらのパラメーターも日付形式 `YYYY-MM-DD` をサポートしています。

![chlimage_1-153](assets/chlimage_1-153.png)

#### オープンソース版 {#open-source-version}

オープンソース版の CRX2Oak は、oak-upgrade の形で入手できます。このツールは、次の機能を除くすべての機能をサポートしています。

* CRX2 サポート
* 移行プロファイルのサポート
* 自動 AEM 再設定のサポート

詳しくは、[Apache に関するドキュメント](https://jackrabbit.apache.org/oak/docs/migration.html)を参照してください。

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
* `--ldap`：LDAP ユーザーを CQ 5.x インスタンスから Oak ベースのインスタンスに移行します。この機能を有効にするには、Oak 設定内の ID プロバイダーを ldap という名前にする必要があります。詳しくは、[LDAP に関するドキュメント](/help/sites-administering/ldap-config.md)を参照してください。

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
   <td><p>「<strong>--trace</strong>」オプションを CRX2Oak コマンドラインに追加して、標準出力に TRACE イベントを表示します（後で検査するには、リダイレクト文字：「&gt;」または「tee」コマンドを使用してログを自分でリダイレクトする必要があります）。</p> </td>
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
