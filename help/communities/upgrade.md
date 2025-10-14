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

この節は Communities に固有で、[AEM 6.5 へのアップグレード &#x200B;](/help/sites-deploying/upgrade.md) （Platform）に記載されている情報を補完するものです。

## AEM 6.1 以降からのアップグレード {#upgrading-from-aem-or-later}

### Solr の再インデックス {#reindex-solr}

MSRP が設定されたデプロイメントに新しい Communities 機能パックをインストールする場合は、次の操作が必要になります。

1. [&#x200B; 最新の機能パック &#x200B;](/help/communities/deploy-communities.md#latestfeaturepack) をインストールします。
1. [&#x200B; 最新の Solr 設定ファイル &#x200B;](/help/communities/msrp.md#upgrading) をインストールします。
1. MSRP の再インデックス
[MSRP Reindex ツール &#x200B;](/help/communities/msrp.md#msrp-reindex-tool) の節を参照してください。

## AEM 6.0 からのアップグレード {#upgrading-from-aem}

既存の UGC を保持する必要がある場合、保持する方法は、デプロイメントが UGC[&#x200B; オンプレミス &#x200B;](#on-premise-storage) または [Adobeクラウド &#x200B;](#adobe-cloud-storage) に保存されているかどうかによって異なります。

### Adobeクラウドストレージ {#adobe-cloud-storage}

アップグレードされたサイトがAdobeクラウドストレージを使用するように設定されていた場合、SRP メソッドが古い場所にある既存の UGC を見つけることができず、すべての UGC が失われたように見える場合があります（誤って）。

したがって、ASRP に対して、`AEM 6.0 compatability-mode` を使用して UGC にアクセスするように指示する機能があります。

すべてのAEM 6.3 オーサーインスタンスおよびパブリッシュインスタンスに対して：

* 管理者権限でログインします。
* [ASRP](/help/communities/asrp.md) を設定します。
* 次の手順に従って、既存の UGC を表示します。

   * Web コンソールを参照します。

      * 例：[https://&lt;host>:&lt;port>/system/console/configMgr](https://localhost:4502/system/console/configMgr)

      * **AEM Communities Utilities** 設定を見つけます。
      * 設定パネルを展開する場合に選択します。

         * *オフ* `Cloud Storage`

         * 「**保存**」を選択します

     ![&#x200B; ユーティリティ &#x200B;](assets/utilities.png)

### オンプレミスストレージ {#on-premise-storage}

アップグレードされたサイトでクラウドストレージを使用しなかった場合は、既存の UGC を、共通ストアをサポートするAEM 6.1 Communities で導入された新しい構造に準拠するように変換する必要があります。

この目的のために、GitHub でオープンソース移行ツールを利用できます。
[AEM Communities UGC 移行ツール &#x200B;](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

### Java API {#java-apis}

AEM 6.0 Social Communities からAEM 6.3 Communities にアップグレードする際に、多くの API が異なるパッケージに再編成されました。 Communities の機能をカスタマイズするために IDE を使用する場合、ほとんどの問題を簡単に解決できます。

非推奨（廃止予定）の SocialUtils パッケージについて詳しくは、[SocialUtils のリファクタリング &#x200B;](/help/communities/socialutils.md) を参照してください。

[&#x200B; コミュニティでの Maven の使用 &#x200B;](/help/communities/maven.md) も参照してください。

### JSP コンポーネントテンプレートがありません {#no-jsp-component-templates}

[&#x200B; ソーシャルコンポーネントフレームワーク &#x200B;](/help/communities/scf.md) （SCF）は、AEM 6.0 以前の Java Server Pages （JSP）の代わりに [HandlebarsJS](https://handlebarsjs.com/) （HBS）テンプレート言語を使用します。

AEM 6.0 では、JSP コンポーネントは、新しい HBS フレームワークコンポーネントと同じ場所に配置され、HBS コンポーネントは通常、「hbs」という名前のサブフォルダーに格納されていました。

AEM 6.1 では、JSP コンポーネントは完全に削除されました。 Communities の場合は、JSP コンポーネントをすべて SCF コンポーネントに置き換えることをお勧めします。

## AEM Communities UGC Migration Tool {#aem-communities-ugc-migration-tool}

[AEM Communities UGC Migration Tool](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration) は、GitHub で利用可能なオープンソースの移行ツールで、以前のバージョンのAEM Social Communities から UGC を書き出したり、AEM Communities 6.1 以降に読み込んだりするようにカスタマイズできます。

以前のバージョンからの UGC の移動に加えて、ツールを使用して、UGC を [SRP](/help/communities/working-with-srp.md) 間（MSRP から DSRP など）で移動することもできます。

## AEM 5.6.1 以前からのアップグレード {#upgrading-from-aem-or-earlier}

概念的には、コミュニティ コンポーネントには次の 3 世代があります。

**Gen 1**：ほぼ CQ 5.4 からAEM 5.6.0 まで、これらはプラットフォーム間で UGC を同期する手段としてレプリケーションを使用してローカルリポジトリに UGC を保存した **collab** コンポーネントです。 その他の違いは、Java サーバーページ（JSP）を使用した実装と、オーサー環境でのみオーサリングで構成されるブログ機能です。

**Gen 2**:AEM 5.6.1 からAEM 6.1 まで、**collab** コンポーネントと **social** コンポーネントの組み合わせです。 AEM 6.0 では新しい [&#x200B; ソーシャルコンポーネントフレームワーク &#x200B;](/help/communities/scf.md) （SCF）が導入され、AEM 6.2 では [&#x200B; 共通の UGC ストア &#x200B;](/help/communities/working-with-srp.md) が導入されました。UGC は、[&#x200B; ストレージリソースプロバイダー &#x200B;](/help/communities/srp.md) （SRP）を使用してアクセスされます。

**Gen 3**:AEM 6.2 以降では、UGC 用の SRP の選択を必要とするハンドルバー（HBS）コンポーネントとして SCF に実装された **ソーシャル** コンポーネントのみが存在します。
