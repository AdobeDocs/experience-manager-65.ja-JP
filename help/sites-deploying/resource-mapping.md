---
title: リソースマッピング
description: リソースマッピングを使用して、Adobe Experience Manager のリダイレクト、バニティー URL、仮想ホストを定義する方法について説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
docset: aem65
feature: Configuring
exl-id: 3eebdd38-da5b-4c38-868a-22c3c7a97b66
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 100%

---

# リソースマッピング{#resource-mapping}

リソースマッピングを使用して、Adobe Experience Manager（AEM）のリダイレクト、バニティー URL、仮想ホストを定義します。

例えば、これらのマッピングを使用すると次のことが可能です。

* すべてのリクエストに `/content` というプレフィックスを付けて、web サイトの訪問者に内部構造が表示されないようにする。
* Web サイトの `/content/en/gateway` ページへのリクエストがすべて `https://gbiv.com/` にリダイレクトされるように、リダイレクトを定義する。

HTTP マッピングの一例として、`localhost:4503` に対するすべてのリクエストに `/content` というプレフィックスを指定します。このようなマッピングを使用すると、Web サイトの訪問者に対して内部構造を非表示にすることができます。例えば、次のページの場合は、

`localhost:4503/content/we-retail/en/products.html`

以下を使用してアクセスします。

`localhost:4503/we-retail/en/products.html`

マッピングによって、`/we-retail/en/products.html` に `/content` という接頭辞が自動的に追加されます。

>[!CAUTION]
>
>バニティー URL は regex パターンをサポートしません。

>[!NOTE]
>
>詳しくは、Sling のドキュメントと「[Mappings for Resource Resolution](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)」と「[Resources](https://sling.apache.org/documentation/the-sling-engine/resources.html)」を参照してください。

## マッピングの定義の表示 {#viewing-mapping-definitions}

このマッピングは 2 つのリストを形成し、JCR リソースリゾルバーは一致を見つけるために（トップダウンで）評価します。

これらのリストは、Felix コンソールの **JCR ResourceResolver** オプション（例：`https://<*host*>:<*port*>/system/console/jcrresolver`）で（設定情報と一緒に）確認できます。

* Configuration
（[Apache Sling Resource Resolver](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver) 用に定義された）現在の設定を表示します。

* 設定テスト
URL またはリソースパスを入力できます。「**解決**」または「**マップ**」をクリックして、システムがエントリの変換する方法を確認します。

* **Resolver Map Entries**
URL をリソースにマップするために ResourceResolver.resolve メソッドが使用するエントリのリストです。

* **Mapping Map Entries**
リソースパスを URL にマップするために ResourceResolver.map メソッドが使用するエントリのリストです。

2 つのリストには、アプリケーションでデフォルトとして定義されたエントリを含む、様々なエントリが表示されます。多くの場合、ユーザーの URL を簡素化することを目的としています。

リストでは、リクエストに一致する正規表現である&#x200B;**パターン**&#x200B;と、適用するリダイレクトを定義する&#x200B;**リプレースメント**&#x200B;を対にします。

例えば、次のパターン

**パターン** `^[^/]+/[^/]+/welcome$`

は、次のリプレースメントをトリガーします。

**Replacement** `/libs/cq/core/content/welcome.html`.

次のリクエストをリダイレクトするには、

`https://localhost:4503/welcome` ``

次に対して

`https://localhost:4503/libs/cq/core/content/welcome.html`

新しいマッピング定義がリポジトリ内に作成されます。

>[!NOTE]
>
>正規表現の定義方法について説明したリソースが多数あります。例えば、[https://www.regular-expressions.info/](https://www.regular-expressions.info/) です。

### AEM でのマッピング定義の作成 {#creating-mapping-definitions-in-aem}

AEM の標準インストールでは、次のフォルダーを検索できます。

`/etc/map/http`

これは、HTTP プロトコル用のマッピングを定義する場合に使用する構造です。マッピングするその他のプロトコル用に別のフォルダー（`sling:Folder`）を `/etc/map` の下に作成できます。

#### /content への内部リダイレクトの設定 {#configuring-an-internal-redirect-to-content}

https://localhost:4503/ に対するリクエストに `/content` というプレフィックスを指定するマッピングを作成するには：

1. CRXDE を使用して `/etc/map/http` に移動します。

1. ノードの作成：

   * **タイプ**：`sling:Mapping`
これは目的のマッピング用のノードタイプですが、必須ではありません。

   * **名前** `localhost_any`

1. 「**すべて保存**」をクリックします。
1. **このノードに次のプロパティを追加します。**

   * **名前** `sling:match`

      * **型** `String`

      * **値** `localhost.4503/`

   * **名前** `sling:internalRedirect`

      * **型** `String[]`

      * **値** `/content/`

1. 「**すべて保存**」をクリックします。

これにより、次のようなリクエストは
`localhost:4503/geometrixx/en/products.html`
は、次のリクエスト
`localhost:4503/content/geometrixx/en/products.html`
であるかのように処理されます。

>[!NOTE]
>
>使用可能な Sling のプロパティとその設定方法について詳しくは、Sling のドキュメントの [Resources](https://sling.apache.org/documentation/the-sling-engine/resources.html) を参照してください。

>[!NOTE]
>
>`/etc/map.publish` を使用して、パブリッシュ環境の設定を保持する。これらを複製し、パブリッシュ環境の [Apache Sling Resource Resolver](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver) の&#x200B;**マッピングロケーション**&#x200B;用に新しい場所（`/etc/map.publish`）を設定する必要があります。
