---
title: AEM 6.5 Communities へのアップグレード
seo-title: Upgrading to AEM 6.5 Communities
description: 以前のバージョンから AEM 6.5 Communities へアップグレードする方法
seo-description: How to upgrade from an earlier version to AEM 6.5 Communities
uuid: 929c3892-1b3b-46a7-8e70-fa6864125911
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: abe5a998-bbe3-4a2b-bcf7-b490a8275219
docset: aem65
exl-id: ea41d35c-967c-4606-b4ec-377e817902e4
source-git-commit: 07f8a9f629122102d30676926b225d57e542147d
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 58%

---

# AEM 6.5 Communities へのアップグレード {#upgrading-to-aem-communities}

各サイトのトポロジや機能に応じて、AEM Communities 6.5 へのアップグレード時または最新の機能パックのインストール時に次のアクションが必要になる場合があります。

このセクションの内容は Communities に特化しており、[AEM 6.5 へのアップグレード](/help/sites-deploying/upgrade.md)（プラットフォーム）の説明を補足するものです。

## AEM 6.1 以降のバージョンからのアップグレード {#upgrading-from-aem-or-later}

### Solr のインデックス再作成 {#reindex-solr}

MSRP で設定されたデプロイメントに新しい Communities 機能パックをインストールする場合は、次の操作が必要になります。

1. のインストール [最新の機能パック](/help/communities/deploy-communities.md#latestfeaturepack).
1. のインストール [最新の Solr 設定ファイル](/help/communities/msrp.md#upgrading).
1. MSRP のインデックス再作成の節を参照 [MSRP インデックス再作成ツール](/help/communities/msrp.md#msrp-reindex-tool).

### Enablement 2.0 {#enablement}

AEM 6.3 以降、イネーブルメント機能では、MySQL の中にレポート情報が保存されなくなりました。MySQL の依存関係は、SCORM コンテンツの追跡用のみに存在します。

Enablement 1.0 からのコンテンツの移行のサポートについては、[カスタマーケア](https://helpx.adobe.com/jp/marketing-cloud/contact-support.html)にお問い合わせください。

## AEM 6.0 からのアップグレード {#upgrading-from-aem}

既存の UGC を保持する必要がある場合は、その方法は、デプロイメントが UGC を保存したかどうかによって異なります [オンプレミス](#on-premise-storage) または [Adobe雲](#adobe-cloud-storage).

### アドビクラウドストレージ {#adobe-cloud-storage}

アップグレードされたサイトがアドビクラウドストレージを使用するように設定された場合、SRP のメソッドは古い場所にある既存の UGC を見つけることができなくなるので、すべての UGC が失われたかのように（誤って）表示される可能性があります。

したがって、ASRP に対して、 `AEM 6.0 compatability-mode` をクリックして UGC にアクセスします。

AEM 6.3 のすべてのオーサーインスタンスとパブリッシュインスタンスについて:

* 管理者権限でサインインします。
* 設定 [ASRP](/help/communities/asrp.md).
* 既存の UGC を表示するには、次の手順に従います。

   * Web コンソールを参照します。

      * 例： [https://&lt;host>:&lt;port>/system/console/configMgr](https://localhost:4502/system/console/configMgr)

      * 場所 **AEM Communities Utilities** 設定。
      * 選択して設定パネルを展開します。

         * *オフ* `Cloud Storage`

         * 選択 **保存**

      ![utilities](assets/utilities.png)


### オンプレミスストレージ {#on-premise-storage}

アップグレードされたサイトでクラウドストレージを使用しなかった場合、既存の UGC は、共通ストアをサポートするために AEM 6.1 Communities で導入された新しい構造に合わせて変換する必要があります。

この目的で、GitHub でオープンソース移行ツールを使用できます。[AEM Communities UGC Migration Tool](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

### Java API {#java-apis}

AEM 6.0 Social Communities から AEM 6.3 Communities にアップグレードするときは、多くの API が異なるパッケージに再編成されていることに注意してください。コミュニティ機能のカスタマイズに IDE を使用する場合は、ほとんどを簡単に解決できます。

廃止された SocialUtils パッケージについて詳しくは、[SocialUtils のリファクタリング](/help/communities/socialutils.md)を参照してください。

また、[コミュニティでの Maven の使用](/help/communities/maven.md)も参照してください。

### JSP コンポーネントテンプレートの廃止 {#no-jsp-component-templates}

この [ソーシャルコンポーネントフレームワーク](/help/communities/scf.md) (SCF) は、 [HandlebarsJS](https://handlebarsjs.com/) AEM 6.0 より前の Java Server Pages(JSP) の代わりに (HBS) テンプレート言語を使用します。

AEM 6.0 では、JSP コンポーネントは新しい HBS フレームワークコンポーネントと同じ場所に残っています（HBS コンポーネントは通常、「hbs」という名前のサブフォルダーに存在します）。

AEM 6.1 以降では JSP コンポーネントは完全に削除されています。コミュニティの場合は、JSP コンポーネントのすべての使用を SCF コンポーネントに置き換えることをお勧めします。

## AEM Communities UGC Migration Tool {#aem-communities-ugc-migration-tool}

[AEM Communities UGC Migration Tool ](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)は、GitHub で使用できるオープンソース移行ツールで、以前のバージョンの AEM Social Communities から UGC を書き出して AEM Communities 6.1 以降に読み込むようにカスタマイズできます。

以前のバージョンから UGC を移行するだけでなく、MSRP から DSRP のように [SRP](/help/communities/working-with-srp.md) 間で UGC を移行する際にもこのツールを使用できます。

## AEM 5.6.1 以前のバージョンからのアップグレード {#upgrading-from-aem-or-earlier}

概念的に、コミュニティコンポーネントには 3 つの世代があります。

**第 1 世代**:CQ 5.4 からAEM 5.6.0 まで、これらは以下の通りです。 **collab** プラットフォーム間で UGC を同期する手段としてレプリケーションを使用して、ローカルリポジトリに UGC を保存したコンポーネント。 その他の違いとしては、Java Server Pages(JSP) を使用した実装と、オーサー環境でのみオーサリングで構成されるブログ機能があります。

**第 2 世代**:AEM 5.6.1 からAEM 6.1 まで、これは次の 2 種類の **collab** および **social** コンポーネント。 AEM 6.0 では新しい [ソーシャルコンポーネントフレームワーク](/help/communities/scf.md) (SCF) およびAEM 6.2 では、 [共通 UGC ストア](/help/communities/working-with-srp.md) UGC には、 [ストレージリソースプロバイダー](/help/communities/srp.md) (SRP)。

**第 3 世代**:AEM 6.2 以降では、 **social** SCF で Handlebars(HBS) コンポーネントとして実装され、UGC 用の SRP の選択が必要なコンポーネント。
