---
title: リソースマッピング
seo-title: Resource Mapping
description: リソースマッピングを使用してリダイレクト、バニティー URL および AEM 用の仮想ホストを定義する方法について説明します。
seo-description: Learn how to define redirects, vanity URLs and virtual hosts for AEM by using resource mapping.
uuid: 2ca2d0e4-6f90-4ecc-82db-26991f08c66f
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 3582a4d8-a47b-467a-9e25-cb45f969ec93
docset: aem65
feature: Configuring
exl-id: 3eebdd38-da5b-4c38-868a-22c3c7a97b66
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 100%

---

# リソースマッピング{#resource-mapping}

リソースマッピングは、リダイレクト、バニティー URL および AEM 用の仮想ホストを定義するために使用します。

例えば、これらのマッピングを使用すると次のことが可能です。

* すべてのリクエストに `/content` というプレフィックスを付けて、web サイトの訪問者に内部構造が表示されないようにする。
* Web サイトの `/content/en/gateway` ページへのリクエストがすべて `https://gbiv.com/` にリダイレクトされるように、リダイレクトを定義する。

HTTP マッピングの一例として、`localhost:4503` に対するすべてのリクエストに `/content` というプレフィックスを指定します。このようなマッピングを使用すると、Web サイトの訪問者に対して内部構造を非表示にすることができます。例えば、次のページの場合は、

`localhost:4503/content/we-retail/en/products.html`

次の URL を使用してアクセスできます。

`localhost:4503/we-retail/en/products.html`

マッピングによって、`/content` というプレフィックスが `/we-retail/en/products.html` に自動的に追加されるからです。

>[!CAUTION]
>
>バニティー URL は regex パターンをサポートしません。

>[!NOTE]
>
>詳しくは、Sling のドキュメントと「[Mappings for Resource Resolution](https://sling.apache.org/site/resources.html)」と「[Resources](https://sling.apache.org/site/mappings-for-resource-resolution.html)」を参照してください。

## マッピング定義の確認 {#viewing-mapping-definitions}

マッピングでは 2 つのリストが作成されます。JCR Resource Resolver は、これらのリストを（トップダウン）評価して一致項目を探します。

これらのリストは、Felix コンソールの **JCR ResourceResolver** オプション（例：`https://<*host*>:<*port*>/system/console/jcrresolver`）で（設定情報と一緒に）確認できます。

* Configuration
（[Apache Sling Resource Resolver](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver) 用に定義された）現在の設定を表示します。

* Configuration Test
URL またはリソースパスを入力できます。「**Resolve**」または「**Map**」をクリックして、システムによるエントリの変換方法を確認します。

* **Resolver Map Entries**
URL をリソースにマップするために ResourceResolver.resolve メソッドが使用するエントリのリストです。

* **Mapping Map Entries**
リソースパスを URL にマップするために ResourceResolver.map メソッドが使用するエントリのリストです。

2 つのリストには、アプリケーションでデフォルトとして定義されたエントリを含む様々なエントリが表示されます。これらのエントリの目的は、多くの場合、ユーザーのために URL を簡略化することです。

リストでは、**パターン**（要求に適合する正規表現）と&#x200B;**リプレースメント**（適用するリダイレクトを定義します）がペアになっています。

例えば、次のパターンがあるとします。

**パターン** `^[^/]+/[^/]+/welcome$`

このパターンは次のリプレースメントを呼び出します。

**リプレースメント** `/libs/cq/core/content/welcome.html`.

これにより、次のリクエストがリダイレクトされます。

`https://localhost:4503/welcome` ``

リダイレクト先は次のとおりです。

`https://localhost:4503/libs/cq/core/content/welcome.html`

新しいマッピング定義がリポジトリ内に作成されます。

>[!NOTE]
>
>正規表現の定義方法について説明したリソースは多数あります（例：[https://www.regular-expressions.info/](https://www.regular-expressions.info/)）。

### AEM でのマッピング定義の作成 {#creating-mapping-definitions-in-aem}

AEM の標準インストールには、次のフォルダーがあります。

`/etc/map/http`

これは、HTTP プロトコル用のマッピングを定義する場合に使用する構造です。マッピングするその他のプロトコル用に別のフォルダー（`sling:Folder`）を `/etc/map` の下に作成できます。

#### /content への内部リダイレクトの設定 {#configuring-an-internal-redirect-to-content}

https://localhost:4503/ に対するリクエストに `/content` というプレフィックスを指定するマッピングを作成するには：

1. CRXDE を使用して `/etc/map/http` に移動します。

1. 新しいノードを作成します。

   * **タイプ**：`sling:Mapping`
これは目的のマッピング用のノードタイプですが、必須ではありません。

   * **名前** `localhost_any`

1. 「**すべて保存**」をクリックします。
1. **このノードに次のプロパティを追加します。**

   * **名前** `sling:match`

      * **型** `String`

      * **値** `localhost.4503/`
   * **名前** `sling:internalRedirect`

      * **型** `String`

      * **値** `/content/`


1. 「**すべて保存**」をクリックします。

これにより、例えば `localhost:4503/geometrixx/en/products.html` というリクエストは、`localhost:4503/content/geometrixx/en/products.html` がリクエストされたものとして処理されます。

>[!NOTE]
>
>使用可能な Sling のプロパティとその設定方法について詳しくは、Sling のドキュメントの [Resources](https://sling.apache.org/site/mappings-for-resource-resolution.html) を参照してください。

>[!NOTE]
>
>`/etc/map.publish` を使用して、パブリッシュ環境の設定を保持する。 これらの設定をレプリケートして、パブリッシュ環境の [Apache Sling Resource Resolver](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver) の「**Mapping Location**」用に新しい場所（`/etc/map.publish`）を設定する必要があります。
