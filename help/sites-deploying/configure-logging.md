---
title: ログ
description: 中央のログサービスのグローバルパラメーターの設定方法、個々のサービスに固有の設定方法、またはデータログの要求方法について説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
feature: Configuring
exl-id: b32001a1-0078-43f6-89d6-781d6d2e9c94
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 50%

---

# ログ{#logging}

AEMでは、次の項目を設定できます。

* central ログサービスのグローバルパラメーター
* リクエストデータログ。リクエスト情報用の専用のログ設定です。
* 個々のサービスに固有の設定（個々のログファイルやログメッセージの形式など）

これらはすべて、[OSGi の設定](/help/sites-deploying/configuring-osgi.md)です。

>[!NOTE]
>
>AEMにログインする際の原則は、Sling 原則に基づいています。 詳しくは [Sling の Logging](https://sling.apache.org/site/logging.html) を参照してください。

## グローバルログ {#global-logging}

[Apache Sling Logging Configuration](/help/sites-deploying/osgi-configuration-settings.md) を使用してルートロガーを設定します。 これは、AEMにログインする際のグローバル設定を定義します。

* ログレベル
* 中央ログファイルの場所
* 保持するバージョンの数
* バージョンのローテーション（最大サイズまたは期間）
* ログメッセージを書き込むときに使用する形式

>[!NOTE]
>
>この[ナレッジベースの記事](https://helpx.adobe.com/jp/experience-manager/kb/HowToRotateRequestAndAccessLog.html)では、request.log ファイルと access.log ファイルのローテーション方法について説明します。

## 個々のサービス用のロガーとライター {#loggers-and-writers-for-individual-services}

グローバルログ設定に加えて、AEMでは個々のサービスに固有の設定を指定できます。

* 具体的なログレベル
* 個々のログファイルの場所
* 保持するバージョンの数
* バージョンのローテーション（最大サイズまたは期間）
* ログメッセージを書き込むときに使用する形式
* ロガー（ログメッセージを提供する OSGi サービス）

これにより、1 つのサービスに関するログメッセージを別個のファイルにチャネル送信できます。 これは、特定のサービスのログレベルを上げる必要がある場合など、開発やテストの際に特に便利です。

AEMでは、次の情報を使用してログメッセージをファイルに書き込みます。

1. An **OSGi サービス** (logger) はログメッセージを書き込みます。
1. A **Logging Logger** はこのメッセージを取り込み、仕様に従って書式設定します。
1. A **ログライター** は、定義した物理ファイルにこれらのメッセージをすべて書き込みます。

これらの要素は、該当する要素の次のパラメーターによってリンクされます。

* **ロガー（Logging Logger）**

  メッセージを生成するサービスを定義します。

* **Log File（Logging Logger）**

  ログメッセージを保存する物理ファイルを定義します。

  これは、Logging Logger を Logging Writer とリンクするために使用します。接続を確立するには、Logging Writer 設定の同じパラメーターと値が同じである必要があります。

* **Log File（Logging Writer）**

  ログメッセージの書き込み先の物理ファイルを定義します。

  これは Logging Writer 設定の同じパラメーターと同一でなければなりません。そうでない場合、照合は行われません。一致がない場合は、暗黙のライターがデフォルトの設定で作成されます（毎日のログローテーション）。

### 標準のロガーおよびライター {#standard-loggers-and-writers}

特定のロガーとライターは、標準のAEMインストールに含まれています。

1 つ目は特殊なケースで、`request.log` ファイルと `access.log` ファイルの両方を制御します。

* ロガー：

   * Apache Sling Customizable Request Data Logger

     (org.apache.sling.engine.impl.log.RequestLoggerService)

   * 要求コンテンツに関するメッセージを `request.log` に書き込みます。

* リンク先：

   * Apache Sling Request Logger

     (org.apache.sling.engine.impl.log.RequestLogger)

   * メッセージを `request.log` または `access.log` に書き込みます。

これらは必要に応じてカスタマイズできますが、ほとんどのインストールには標準設定が適しています。

他のペアは、標準設定に従います。

* ロガー：

   * Apache Sling Logging Logger Configuration

     (org.apache.sling.commons.log.LogManager.factory.config)

   * `logs/error.log` にメッセージ `Information` を書き込みます。

* リンク先のライター：

   * Apache Sling Logging Writer Configuration

     (org.apache.sling.commons.log.LogManager.factory.writer)

* ロガー：

   * Apache Sling Logging Logger Configuration（org.apache.sling.commons.log.LogManager.factory.config.649d51b7-6425-45c9-81e6-2697a03d6be7）

   * サービス `org.apache.pdfbox` のメッセージ `Warning` を `../logs/error.log` に書き込みます。

* 特定のライターにリンクしないので、デフォルト設定で暗黙のライターを作成して使用します（毎日のログローテーション）。

### 独自のロガーおよびライターの作成 {#creating-your-own-loggers-and-writers}

次の手順で、独自のロガーとライターのペアを定義できます。

1. ファクトリ設定のインスタンスを作成する [Apache Sling Logging Logger Configuration](/help/sites-deploying/osgi-configuration-settings.md).

   1. ログファイルを指定します。
   1. ロガーを指定します。
   1. 必要に応じて、その他のパラメーターを設定します。

1. ファクトリ設定のインスタンスを作成する [Apache Sling Logging Writer Configuration](/help/sites-deploying/osgi-configuration-settings.md).

   1. ログファイルを指定します。これは、ロガーに指定されたファイルと一致する必要があります。
   1. 必要に応じて、その他のパラメーターを設定します。

>[!NOTE]
>
>特定の状況で、 [カスタムログファイル](/help/sites-deploying/monitoring-and-maintaining.md#create-a-custom-log-file).
