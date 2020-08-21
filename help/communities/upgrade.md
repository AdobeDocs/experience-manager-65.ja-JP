---
title: AEM 6.5 Communities へのアップグレード
seo-title: AEM 6.5 Communities へのアップグレード
description: 以前のバージョンから AEM 6.4 Communities へアップグレードする方法
seo-description: 以前のバージョンから AEM 6.4 Communities へアップグレードする方法
uuid: 929c3892-1b3b-46a7-8e70-fa6864125911
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: abe5a998-bbe3-4a2b-bcf7-b490a8275219
docset: aem65
translation-type: tm+mt
source-git-commit: c190d5f223c85f6c49fea1391d8a3d2baff20192
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 58%

---


# AEM 6.5 Communities へのアップグレード {#upgrading-to-aem-communities}

各サイトのトポロジや機能に応じて、AEM Communities 6.5 へのアップグレード時または最新の機能パックのインストール時に次のアクションが必要になる場合があります。

このセクションの内容は Communities に特化しており、[AEM 6.5 へのアップグレード](/help/sites-deploying/upgrade.md)（プラットフォーム）の説明を補足するものです。

## AEM 6.1 以降のバージョンからのアップグレード {#upgrading-from-aem-or-later}

### Solr のインデックス再作成 {#reindex-solr}

MSRPで設定された配置に新しいCommunities機能パックをインストールする場合、次の操作が必要になります。

1. Install the [latest feature pack](/help/communities/deploy-communities.md#latestfeaturepack).
1. Install the [latest Solr config files](/help/communities/msrp.md#upgrading).
1. Reindex MSRP
see section [MSRP Reindex Tool](/help/communities/msrp.md#msrp-reindex-tool).

### Enablement 2.0 {#enablement}

AEM 6.3 以降、イネーブルメント機能では、MySQL の中にレポート情報が保存されなくなりました。MySQL の依存関係は、SCORM コンテンツの追跡用のみに存在します。

Enablement 1.0 からのコンテンツの移行のサポートについては、[カスタマーケア](https://helpx.adobe.com/jp/marketing-cloud/contact-support.html)にお問い合わせください。

## AEM 6.0 からのアップグレード {#upgrading-from-aem}

If pre-existing UGC needs to be retained, then the means to do so depends on whether the deployment stored UGC [on-premise](#on-premise-storage) or in the [Adobe cloud](#adobe-cloud-storage).

### アドビクラウドストレージ {#adobe-cloud-storage}

アップグレードされたサイトがアドビクラウドストレージを使用するように設定された場合、SRP のメソッドは古い場所にある既存の UGC を見つけることができなくなるので、すべての UGC が失われたかのように（誤って）表示される可能性があります。

Thus, there is the ability to instruct ASRP to use `AEM 6.0 compatability-mode` to access UGC.

AEM 6.3 のすべてのオーサーインスタンスとパブリッシュインスタンスについて:

* 管理者権限でサインインします。
* Configure [ASRP](/help/communities/asrp.md).
* 既存のUGCを表示するには、次の手順に従います。

   * Webコンソールを参照します。

      * For example, [https://&lt;host>:&lt;port>/system/console/configMgr](https://localhost:4502/system/console/configMgr)

      * Locate **AEM Communities Utilities** configuration.
      * 選択して設定パネルを展開します。

         * *オフ* `Cloud Storage`

         * Select **Save**

      ![utilities](assets/utilities.png)


### オンプレミスストレージ {#on-premise-storage}

アップグレードされたサイトでクラウドストレージを使用しなかった場合、既存の UGC は、共通ストアをサポートするために AEM 6.1 Communities で導入された新しい構造に合わせて変換する必要があります。

この目的で、GitHub でオープンソース移行ツールを使用できます。[AEM Communities UGC Migration Tool](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

### Java API {#java-apis}

AEM 6.0 Social Communities から AEM 6.3 Communities にアップグレードするときは、多くの API が異なるパッケージに再編成されていることに注意してください。IDEを使用してCommunities機能をカスタマイズする場合、ほとんどの問題を簡単に解決できます。

廃止された SocialUtils パッケージについて詳しくは、[SocialUtils のリファクタリング](/help/communities/socialutils.md)を参照してください。

また、[コミュニティでの Maven の使用](/help/communities/maven.md)も参照してください。

### JSP コンポーネントテンプレートの廃止 {#no-jsp-component-templates}

[ソーシャルコンポーネントフレームワーク](/help/communities/scf.md) (SCF)は、AEM 6.0より前のバージョンで使用されていたJava Server Pages(JSP)の代わりに、 [HandlebarsJS](https://www.handlebarsjs.com/) (HBS)テンプレート言語を使用します。

AEM 6.0 では、JSP コンポーネントは新しい HBS フレームワークコンポーネントと同じ場所に残っています（HBS コンポーネントは通常、「hbs」という名前のサブフォルダーに存在します）。

AEM 6.1 以降では JSP コンポーネントは完全に削除されています。Communitiesの場合、JSPコンポーネントの使用をすべてSCFコンポーネントで置き換えることをお勧めします。

## AEM Communities UGC Migration Tool {#aem-communities-ugc-migration-tool}

[AEM Communities UGC Migration Tool ](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)は、GitHub で使用できるオープンソース移行ツールで、以前のバージョンの AEM Social Communities から UGC を書き出して AEM Communities 6.1 以降に読み込むようにカスタマイズできます。

以前のバージョンから UGC を移行するだけでなく、MSRP から DSRP のように [SRP](/help/communities/working-with-srp.md) 間で UGC を移行する際にもこのツールを使用できます。

## AEM 5.6.1 以前のバージョンからのアップグレード {#upgrading-from-aem-or-earlier}

概念的に、コミュニティコンポーネントには 3 つの世代があります。

**第1世代**:CQ 5.4 ～ AEM 5.6.0の概要です。これらは、複数のプラットフォーム間でUGCを同期する手段としてレプリケーションを使用し、ローカルリポジトリにUGCを格納する **collab** コンポーネントです。 その他の違いとしては、Java Server Pages(JSP)を使用した実装と、作成者環境でのみ作成されるブログ機能があります。

**第2世代**:AEM 5.6.1からAEM 6.1まで、これは **collab** と **social** のコンポーネントの組み合わせです。 AEM 6.0 introduced the new [social component framework](/help/communities/scf.md) (SCF) and AEM 6.2 introduced a [common UGC store](/help/communities/working-with-srp.md) where UGC is accessed using a [storage resource provider](/help/communities/srp.md) (SRP).

**第3世代**:AEM 6.2以降では、SCFにHandlebars(HBS)コンポーネントとして実装される **ソーシャル** コンポーネントのみが存在し、UGC用のSRPを選択する必要があります。
