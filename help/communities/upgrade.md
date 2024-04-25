---
title: AEM 6.5 Communities へのアップグレード
description: 以前のバージョンからAEM 6.5 Communities にアップグレードする方法
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
docset: aem65
exl-id: ea41d35c-967c-4606-b4ec-377e817902e4
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 2%

---

# AEM 6.5 Communities へのアップグレード {#upgrading-to-aem-communities}

各サイトのトポロジと機能によっては、AEM Communities 6.5 にアップグレードする場合や最新の機能パックをインストールする場合に、次の操作が必要になることがあります。

この節は、コミュニティに固有で、に提供される情報を補完します。 [AEM 6.5 へのアップグレード](/help/sites-deploying/upgrade.md) （プラットフォーム）。

## AEM 6.1 以降からのアップグレード {#upgrading-from-aem-or-later}

### Solr の再インデックス {#reindex-solr}

MSRP が設定されたデプロイメントに新しい Communities 機能パックをインストールする場合は、次の操作が必要になります。

1. のインストール [最新の機能パック](/help/communities/deploy-communities.md#latestfeaturepack).
1. のインストール [最新の Solr 設定ファイル](/help/communities/msrp.md#upgrading).
1. MSRP の再インデックス：セクションを参照 [MSRP インデックス再作成ツール](/help/communities/msrp.md#msrp-reindex-tool).

## AEM 6.0 からのアップグレード {#upgrading-from-aem}

既存の UGC を保持する必要がある場合、保持する方法は、デプロイメントに UGC が保存されているかどうかによって異なります [オンプレミス](#on-premise-storage) または [Adobe雲](#adobe-cloud-storage).

### Adobeクラウドストレージ {#adobe-cloud-storage}

アップグレードされたサイトがAdobeクラウドストレージを使用するように設定されていた場合、SRP メソッドが古い場所にある既存の UGC を見つけることができず、すべての UGC が失われたように見える場合があります（誤って）。

したがって、ASRP に使用を指示する機能があります `AEM 6.0 compatability-mode` UGC にアクセスします。

すべてのAEM 6.3 オーサーインスタンスおよびパブリッシュインスタンスに対して：

* 管理者権限でログインします。
* 設定 [ASRP](/help/communities/asrp.md).
* 次の手順に従って、既存の UGC を表示します。

   * Web コンソールを参照します。

      * 例： [https://&lt;host>:&lt;port>/system/console/configMgr](https://localhost:4502/system/console/configMgr)

      * を見つける **AEM Communities ユーティリティ** 設定。
      * 設定パネルを展開する場合に選択します。

         * *Uncheck* `Cloud Storage`

         * 「**保存**」を選択します

     ![ユーティリティ](assets/utilities.png)

### オンプレミスストレージ {#on-premise-storage}

アップグレードされたサイトでクラウドストレージを使用しなかった場合は、既存の UGC を、共通ストアをサポートするAEM 6.1 Communities で導入された新しい構造に準拠するように変換する必要があります。

この目的のために、GitHub でオープンソース移行ツールを利用できます。
[AEM Communities UGC Migration Tool](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

### Java API {#java-apis}

AEM 6.0 Social Communities からAEM 6.3 Communities にアップグレードする際に、多くの API が異なるパッケージに再編成されました。 Communities の機能をカスタマイズするために IDE を使用する場合、ほとんどの問題を簡単に解決できます。

非推奨（廃止予定）の SocialUtils パッケージについて詳しくは、以下を参照してください。 [SocialUtils のリファクタリング](/help/communities/socialutils.md).

関連トピック [コミュニティでの Maven の使用](/help/communities/maven.md).

### JSP コンポーネントテンプレートがありません {#no-jsp-component-templates}

この [ソーシャルコンポーネントフレームワーク](/help/communities/scf.md) （SCF）は、 [HandlebarsJS](https://handlebarsjs.com/) AEM 6.0 以前で使用されていた Java Server Pages （JSP）の代わりに使用される（HBS）テンプレート言語です。

AEM 6.0 では、JSP コンポーネントは、新しい HBS フレームワークコンポーネントと同じ場所に配置され、HBS コンポーネントは通常、「hbs」という名前のサブフォルダーに格納されていました。

AEM 6.1 では、JSP コンポーネントは完全に削除されました。 Communities の場合は、JSP コンポーネントをすべて SCF コンポーネントに置き換えることをお勧めします。

## AEM Communities UGC Migration Tool {#aem-communities-ugc-migration-tool}

この [AEM Communities UGC Migration Tool](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration) はオープンソースの移行ツールで、GitHub で利用可能です。以前のバージョンのAEM ソーシャルコミュニティから UGC を書き出し、AEM Communities 6.1 以降に読み込むようにカスタマイズできます。

以前のバージョンから UGC を移動するだけでなく、ツールを使用して UGC を 1 つから移動することもできます [SRP](/help/communities/working-with-srp.md) 別の宛先（MSRP から DSRP など）

## AEM 5.6.1 以前からのアップグレード {#upgrading-from-aem-or-earlier}

概念的には、コミュニティ コンポーネントには次の 3 世代があります。

**第 1 世代**:CQ 5.4 ～ AEM 5.6.0 の概算で、次のようになります **collab** プラットフォーム間で UGC を同期する手段としてレプリケーションを使用してローカルリポジトリに UGC を格納するコンポーネント。 その他の違いは、Java サーバーページ（JSP）を使用した実装と、オーサー環境でのみオーサリングで構成されるブログ機能です。

**第 2 世代**:AEM 5.6.1 からAEM 6.1 までは、次の要素が混在しています **collab** および **ソーシャル** コンポーネント。 AEM 6.0 では、新しい [ソーシャルコンポーネントフレームワーク](/help/communities/scf.md) （SCF）とAEM 6.2 では、 [共通 UGC ストア](/help/communities/working-with-srp.md) UGC にアクセスするには [ストレージリソースプロバイダー](/help/communities/srp.md) （SRP）。

**第 3 世代**:AEM 6.2 以降では、次のみ **ソーシャル** コンポーネント：UGC 用の SRP の選択を必要とするハンドルバー（HBS）コンポーネントとして SCF に実装される
