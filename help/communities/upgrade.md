---
title: AEM 6.5 Communities へのアップグレード
seo-title: AEM 6.5 Communities へのアップグレード
description: 以前のバージョンから AEM 6.5 Communities へアップグレードする方法
seo-description: 以前のバージョンから AEM 6.5 Communities へアップグレードする方法
uuid: 929c3892-1b3b-46a7-8e70-fa6864125911
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: abe5a998-bbe3-4a2b-bcf7-b490a8275219
docset: aem65
exl-id: ea41d35c-967c-4606-b4ec-377e817902e4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 58%

---

# AEM 6.5 Communities へのアップグレード {#upgrading-to-aem-communities}

各サイトのトポロジや機能に応じて、AEM Communities 6.5 へのアップグレード時または最新の機能パックのインストール時に次のアクションが必要になる場合があります。

このセクションの内容は Communities に特化しており、[AEM 6.5 へのアップグレード](/help/sites-deploying/upgrade.md)（プラットフォーム）の説明を補足するものです。

## AEM 6.1 以降のバージョンからのアップグレード {#upgrading-from-aem-or-later}

### Solr のインデックス再作成 {#reindex-solr}

MSRPを使用して設定されたデプロイメントに新しいCommunities機能パックをインストールする場合は、次の操作が必要です。

1. [最新の機能パック](/help/communities/deploy-communities.md#latestfeaturepack)をインストールします。
1. [最新のSolr設定ファイル](/help/communities/msrp.md#upgrading)をインストールします。
1. MSRPの再インデックス
[MSRPインデックス再作成ツール](/help/communities/msrp.md#msrp-reindex-tool)の節を参照してください。

### Enablement 2.0 {#enablement}

AEM 6.3 以降、イネーブルメント機能では、MySQL の中にレポート情報が保存されなくなりました。MySQL の依存関係は、SCORM コンテンツの追跡用のみに存在します。

Enablement 1.0 からのコンテンツの移行のサポートについては、[カスタマーケア](https://helpx.adobe.com/jp/marketing-cloud/contact-support.html)にお問い合わせください。

## AEM 6.0 からのアップグレード  {#upgrading-from-aem}

既存のUGCを保持する必要がある場合は、デプロイメントがUGC [オンプレミス](#on-premise-storage)と[Adobeクラウド](#adobe-cloud-storage)のどちらに保存したかによって、保存方法が異なります。

### アドビクラウドストレージ {#adobe-cloud-storage}

アップグレードされたサイトがアドビクラウドストレージを使用するように設定された場合、SRP のメソッドは古い場所にある既存の UGC を見つけることができなくなるので、すべての UGC が失われたかのように（誤って）表示される可能性があります。

したがって、ASRPに`AEM 6.0 compatability-mode`を使用してUGCにアクセスするよう指示する機能があります。

AEM 6.3 のすべてのオーサーインスタンスとパブリッシュインスタンスについて:

* 管理者権限でサインインします。
* [ASRP](/help/communities/asrp.md)を設定します。
* 既存のUGCを表示するには、次の手順に従います。

   * Webコンソールを参照します。

      * 例： [https://&lt;host>:&lt;port>/system/console/configMgr](https://localhost:4502/system/console/configMgr)

      * **AEM Communities Utilities**&#x200B;設定を見つけます。
      * 選択して設定パネルを展開します。

         * *オフ* `Cloud Storage`

         * 「**保存**」を選択します。

      ![utilities](assets/utilities.png)


### オンプレミスストレージ {#on-premise-storage}

アップグレードされたサイトでクラウドストレージを使用しなかった場合、既存の UGC は、共通ストアをサポートするために AEM 6.1 Communities で導入された新しい構造に合わせて変換する必要があります。

この目的で、GitHub でオープンソース移行ツールを使用できます。[AEM Communities UGC Migration Tool](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

### Java API {#java-apis}

AEM 6.0 Social Communities から AEM 6.3 Communities にアップグレードするときは、多くの API が異なるパッケージに再編成されていることに注意してください。Communities機能のカスタマイズにIDEを使用する場合は、ほとんどの問題を簡単に解決できます。

廃止された SocialUtils パッケージについて詳しくは、[SocialUtils のリファクタリング](/help/communities/socialutils.md)を参照してください。

また、[コミュニティでの Maven の使用](/help/communities/maven.md)も参照してください。

### JSP コンポーネントテンプレートの廃止  {#no-jsp-component-templates}

[ソーシャルコンポーネントフレームワーク](/help/communities/scf.md)(SCF)は、AEM 6.0より前に使用されていたJava Server Pages(JSP)の代わりに、[HandlebarsJS](https://www.handlebarsjs.com/)(HBS)テンプレート言語を使用します。

AEM 6.0 では、JSP コンポーネントは新しい HBS フレームワークコンポーネントと同じ場所に残っています（HBS コンポーネントは通常、「hbs」という名前のサブフォルダーに存在します）。

AEM 6.1 以降では JSP コンポーネントは完全に削除されています。コミュニティの場合は、JSPコンポーネントの使用をすべてSCFコンポーネントで置き換えることをお勧めします。

## AEM Communities UGC Migration Tool {#aem-communities-ugc-migration-tool}

[AEM Communities UGC Migration Tool ](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)は、GitHub で使用できるオープンソース移行ツールで、以前のバージョンの AEM Social Communities から UGC を書き出して AEM Communities 6.1 以降に読み込むようにカスタマイズできます。

以前のバージョンから UGC を移行するだけでなく、MSRP から DSRP のように [SRP](/help/communities/working-with-srp.md) 間で UGC を移行する際にもこのツールを使用できます。

## AEM 5.6.1 以前のバージョンからのアップグレード  {#upgrading-from-aem-or-earlier}

概念的に、コミュニティコンポーネントには 3 つの世代があります。

**第1世代**:CQ 5.4からAEM 5.6.0までが、UGCを複数のプラットフォーム間で同期する手段としてレプリケーションを使用してローカルリポジトリに格納するコラブコンポーネントで **** す。その他の違いは、Java Server Pages(JSP)を使用した実装と、オーサー環境でのみオーサリングで構成されるブログ機能です。

**第2世代**:AEM 5.6.1からAEM 6.1まで、これはカラーバンドのソーシャルコンポーネン **** トの組み **** 合わせです。AEM 6.0では新しい[ソーシャルコンポーネントフレームワーク](/help/communities/scf.md)(SCF)が導入され、AEM 6.2では[共通のUGCストア](/help/communities/working-with-srp.md)が導入されました。このストアでは、[ストレージリソースプロバイダー](/help/communities/srp.md)(SRP)を使用してUGCにアクセスします。

**第3世代**:AEM 6.2以降では、SCFにHandlebars(HBS)コンポーネントとして実装さ **** れ、UGC用のSRPの選択が必要なソーシャルコンポーネントのみが存在します。
