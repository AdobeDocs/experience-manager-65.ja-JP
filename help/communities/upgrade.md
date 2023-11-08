---
title: AEM 6.5 Communities へのアップグレード
seo-title: Upgrading to AEM 6.5 Communities
description: 以前のバージョンからAEM 6.5 Communities にアップグレードする方法
seo-description: How to upgrade from an earlier version to AEM 6.5 Communities
uuid: 929c3892-1b3b-46a7-8e70-fa6864125911
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: abe5a998-bbe3-4a2b-bcf7-b490a8275219
docset: aem65
exl-id: ea41d35c-967c-4606-b4ec-377e817902e4
source-git-commit: e2a3470784beb04c2179958ac6cb98861acfaa71
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 2%

---

# AEM 6.5 Communities へのアップグレード {#upgrading-to-aem-communities}

各サイトのトポロジと機能に応じて、AEM Communities 6.5 にアップグレードする場合、または最新の機能パックをインストールする場合に、次の操作が必要になる場合があります。

この節は、コミュニティに固有で、 [AEM 6.5 へのアップグレード](/help/sites-deploying/upgrade.md) （プラットフォーム）を使用します。

## AEM 6.1 以降からのアップグレード {#upgrading-from-aem-or-later}

### Solr のインデックス再作成 {#reindex-solr}

MSRP で設定されたデプロイメントに新しい Communities 機能パックをインストールする場合は、次の操作が必要になります。

1. をインストールします。 [最新の機能パック](/help/communities/deploy-communities.md#latestfeaturepack).
1. をインストールします。 [最新の Solr 設定ファイル](/help/communities/msrp.md#upgrading).
1. MSRP のインデックス再作成の節を参照 [MSRP インデックス再作成ツール](/help/communities/msrp.md#msrp-reindex-tool).

## AEM 6.0 からのアップグレード {#upgrading-from-aem}

既存の UGC を保持する必要がある場合は、その方法は、デプロイメントが UGC を保存したかどうかによって異なります [オンプレミス](#on-premise-storage) または [Adobe雲](#adobe-cloud-storage).

### Adobeクラウドストレージ {#adobe-cloud-storage}

アップグレードされたサイトがAdobeクラウドストレージを使用するように設定されている場合は、SRP メソッドが既存の UGC を古い場所で見つけられないので、すべての UGC が失われたかのように（間違って）表示されることがあります。

したがって、ASRP に対して、 `AEM 6.0 compatability-mode` をクリックして UGC にアクセスします。

すべてのAEM 6.3 オーサーインスタンスとパブリッシュインスタンスの場合：

* 管理者権限でログインします。
* 設定 [ASRP](/help/communities/asrp.md).
* 既存の UGC を表示するには、次の手順に従います。

   * Web コンソールを参照します。

      * 例： [https://&lt;host>:&lt;port>/system/console/configMgr](https://localhost:4502/system/console/configMgr)

      * 場所 **AEM Communities Utilities** 設定。
      * 選択して設定パネルを展開します。

         * *オフ* `Cloud Storage`

         * 「**保存**」を選択します

     ![utilities](assets/utilities.png)

### オンプレミスストレージ {#on-premise-storage}

アップグレードしたサイトがクラウドストレージを使用しなかった場合は、共通ストアをサポートするために、既存の UGC をAEM 6.1 Communities で導入された新しい構造に合わせて変換する必要があります。

そのために、GitHub でオープンソース移行ツールを利用できます。
[AEM Communities UGC 移行ツール](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

### Java API {#java-apis}

AEM 6.0 ソーシャルコミュニティからAEM 6.3 Communities にアップグレードする際に、多くの API が異なるパッケージに再編成されました。 コミュニティ機能のカスタマイズに IDE を使用する場合は、ほとんどを簡単に解決できます。

非推奨（廃止予定）の SocialUtils パッケージについて詳しくは、 [SocialUtils のリファクタリング](/help/communities/socialutils.md).

関連トピック [コミュニティでの Maven の使用](/help/communities/maven.md).

### JSP コンポーネントテンプレートなし {#no-jsp-component-templates}

The [ソーシャルコンポーネントフレームワーク](/help/communities/scf.md) (SCF) は、 [HandlebarsJS](https://handlebarsjs.com/) AEM 6.0 より前の Java Server Pages(JSP) の代わりに (HBS) テンプレート言語を使用します。

AEM 6.0 では、JSP コンポーネントは、新しい HBS フレームワークコンポーネントと同じ場所に同じ場所に残り、HBS コンポーネントは通常、「hbs」という名前のサブフォルダーにあります。

AEM 6.1 以降では、JSP コンポーネントは完全に削除されました。 コミュニティの場合は、JSP コンポーネントのすべての使用を SCF コンポーネントに置き換えることをお勧めします。

## AEM Communities UGC 移行ツール {#aem-communities-ugc-migration-tool}

The [AEM Communities UGC 移行ツール](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration) は、GitHub で利用可能なオープンソース移行ツールで、AEM social communities の以前のバージョンから UGC を書き出してAEM Communities 6.1 以降に読み込むようにカスタマイズできます。

以前のバージョンから UGC を移動する以外に、このツールを使用して UGC を 1 つから移動することもできます [SRP](/help/communities/working-with-srp.md) を別のもの（MSRP から DSRP へなど）に変更する場合に使用します。

## AEM 5.6.1 以前からのアップグレード {#upgrading-from-aem-or-earlier}

概念上、次の 3 世代のコミュニティコンポーネントが存在します。

**第 1 世代**：約 CQ 5.4 ～ AEM 5.6.0 です。これらは、 **collab** プラットフォーム間で UGC を同期する手段としてレプリケーションを使用して、ローカルリポジトリに UGC を保存したコンポーネント。 その他の違いとしては、Java Server Pages(JSP) を使用した実装と、オーサー環境でのみオーサリングで構成されるブログ機能があります。

**第 2 世代**:AEM 5.6.1 からAEM 6.1 まで、これは次の 2 種類の **collab** および **social** コンポーネント。 AEM 6.0 では新しい [ソーシャルコンポーネントフレームワーク](/help/communities/scf.md) (SCF) およびAEM 6.2 では、 [共通 UGC ストア](/help/communities/working-with-srp.md) UGC には、 [ストレージリソースプロバイダー](/help/communities/srp.md) (SRP)。

**第 3 世代**:AEM 6.2 以降では、 **social** SCF で Handlebars(HBS) コンポーネントとして実装され、UGC 用の SRP の選択が必要なコンポーネント。
