---
title: ログ
seo-title: ログ
description: 一元的なログサービスのグローバルパラメーターの設定、個々のサービスに特有の設定、またはデータのログ記録の要求をおこなう方法を学習します。
seo-description: 一元的なログサービスのグローバルパラメーターの設定、個々のサービスに特有の設定、またはデータのログ記録の要求をおこなう方法を学習します。
uuid: 8c9e3628-2f2c-445d-9706-5c7725b85fe2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 5aa69b10-2cd0-4d34-8104-8c3b88405926
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 83%

---


# ログ{#logging}

AEM では、次の設定が可能です。

* 中央のログサービスのグローバルパラメーター
* 要求データのログ（要求情報用の特殊なログ設定）
* 個々のサービス固有の設定;例えば、個々のログファイルやログメッセージの形式

これらはすべて、[OSGi の設定](/help/sites-deploying/configuring-osgi.md)です。

>[!NOTE]
>
>AEM のログは、Sling の原則に基づいています。詳しくは、[Sling のログ](https://sling.apache.org/site/logging.html)を参照してください。

## グローバルログ {#global-logging}

ルートロガーを設定するには、[Apache Sling Logging Configuration](/help/sites-deploying/osgi-configuration-settings.md) を使用します。これにより、AEM のログのグローバル設定が定義されます。

* ログレベル
* 主要なログファイルの場所
* 保存するバージョンの数
* バージョンのローテーション（最大サイズまたは期間）
* ログメッセージを書き込むときに使用する形式

>[!NOTE]
>
>この[ナレッジベースの記事](https://helpx.adobe.com/experience-manager/kb/HowToRotateRequestAndAccessLog.html)では、request.log ファイルと access.log ファイルのローテーション方法について説明します。

## 個々のサービス用のロガーとライター {#loggers-and-writers-for-individual-services}

グローバルログ設定に加えて、AEM では個々のサービス用に具体的な設定をおこなうことができます。

* 具体的なログレベル
* 個々のログファイルの場所
* 保存するバージョンの数
* バージョンのローテーション（最大サイズまたは期間）
* ログメッセージを書き込むときに使用する形式
* ロガー（ログメッセージを提供する OSGi サービス）

これにより、単一のサービスに関するログメッセージを別個のファイルに送ることができます。これは、開発やテストの際、例えば特定のサービスのログレベルを上げる必要がある場合などに特に便利です。

AEM では、以下の手順でログメッセージをファイルに書き込みます。

1. **OSGi サービス**（ロガー）がログメッセージを書き込みます。
1. **Logging Logger** がこのメッセージを受け取り、仕様に従って書式設定します。
1. **Logging Writer** が、これらすべてのメッセージを、定義済みの物理ファイルに書き込みます。

これらの要素は、該当する要素の次のパラメーターによってリンクされます。

* **ロガー（Logging Logger）**

   メッセージを生成するサービスを定義します。

* **ログファイル(Logging Logger)**

   ログメッセージを保存する物理ファイルを定義します。

   これは、ロギングロガーをロギングライターとリンクするために使用します。 接続を行うには、この値がLogging Writer設定の同じパラメーターと同じである必要があります。

* **ログファイル（ログライター）**

   ログメッセージの書き込み先となる物理ファイルを定義します。

   これは、Logging Writer構成の同じパラメータと同じである必要があります。同じでないと、一致しません。 一致しない場合は、暗黙的なWriterがデフォルト設定（日別ログローテーション）で作成されます。

### 標準のロガーおよびライター {#standard-loggers-and-writers}

標準の AEM インストールには、特定のロガーおよびライターが含まれています。

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

その他のペアは、標準設定に従います。

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

1. ファクトリ設定の [Apache Sling Logging Logger Configuration](/help/sites-deploying/osgi-configuration-settings.md) の新しいインスタンスを作成します。

   1. ログファイルを指定します。
   1. ロガーを指定します。
   1. 必要に応じてその他のパラメーターを設定します。

1. ファクトリ設定の [Apache Sling Logging Writer Configuration](/help/sites-deploying/osgi-configuration-settings.md) の新しいインスタンスを作成します。

   1. ログファイルを指定します。ロガーに指定したものと同じファイルを指定する必要があります。
   1. 必要に応じてその他のパラメーターを設定します。

>[!NOTE]
>
>状況によっては、[カスタムログファイル](/help/sites-deploying/monitoring-and-maintaining.md#create-a-custom-log-file)を作成する必要があります。

