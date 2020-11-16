---
title: リソースマッピング
seo-title: リソースマッピング
description: リソースマッピングを使用してリダイレクト、バニティー URL および AEM 用の仮想ホストを定義する方法について説明します。
seo-description: リソースマッピングを使用してリダイレクト、バニティー URL および AEM 用の仮想ホストを定義する方法について説明します。
uuid: 2ca2d0e4-6f90-4ecc-82db-26991f08c66f
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 3582a4d8-a47b-467a-9e25-cb45f969ec93
docset: aem65
translation-type: tm+mt
source-git-commit: 44eb94b917fe88b7c90c29ec7da553e15be391db
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 66%

---


# リソースマッピング{#resource-mapping}

リソースマッピングは、リダイレクト、バニティー URL および AEM 用の仮想ホストを定義するために使用します。

例えば、これらのマッピングを使用すると次のことが可能です。

* Prefix all requests with `/content` so that the internal structure is hidden from the visitors to your website.
* Define a redirect so that all requests to the `/content/en/gateway` page of your website are redirected to `https://gbiv.com/`.

One possible HTTP mapping prefixes all requests to `localhost:4503` with `/content`. このようなマッピングを使用すると、Web サイトの訪問者に対して内部構造を非表示にすることができます。例えば、次のページにアクセスできます。

`localhost:4503/content/we-retail/en/products.html`

マッピング前のページは次のとおりです。

`localhost:4503/we-retail/en/products.html`

as the mapping will automatically add the prefix `/content` to `/we-retail/en/products.html`.

>[!CAUTION]
>
>バニティー URL は regex パターンをサポートしません。

>[!NOTE]
>
>詳しくは、Sling のドキュメントと「[Mappings for Resource Resolution](https://sling.apache.org/site/resources.html)」と「[Resources](https://sling.apache.org/site/mappings-for-resource-resolution.html)」を参照してください。

## マッピング定義の確認 {#viewing-mapping-definitions}

マッピングでは 2 つのリストが作成されます。JCR Resource Resolver は、これらのリストを（トップダウン）評価して一致項目を探します。

These lists can be viewed (together with configuration information) under the **JCR ResourceResolver** option of the Felix console; for example, `https://<*host*>:<*port*>/system/console/jcrresolver`:

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

**代替機能** `/libs/cq/core/content/welcome.html`.

これにより、次の要求がリダイレクトされます。

`https://localhost:4503/welcome` ``

リダイレクト先は次のとおりです。

`https://localhost:4503/libs/cq/core/content/welcome.html`

新しいマッピング定義がリポジトリ内に作成されます。

>[!NOTE]
>
>There are many resources available that help explain how to define regular expressions; for example [https://www.regular-expressions.info/](https://www.regular-expressions.info/).

### AEM でのマッピング定義の作成 {#creating-mapping-definitions-in-aem}

AEM の標準インストールには、次のフォルダーがあります。

`/etc/map/http`

これは、HTTP プロトコル用のマッピングを定義する場合に使用する構造です。Other folders ( `sling:Folder`) can be created under `/etc/map` for any other protocols that you want to map.

#### /content への内部リダイレクトの設定{#configuring-an-internal-redirect-to-content}

To create the mapping that prefixes any request to https://localhost:4503/ with `/content`:

1. Using CRXDE navigate to `/etc/map/http`.

1. 新しいノードを作成します。

   * **タイプ**：`sling:Mapping`
これは目的のマッピング用のノードタイプですが、必須ではありません。

   * **名前** `localhost_any`

1. 「**すべて保存**」をクリックします。
1. このノードに次のプロパティを&#x200B;**追加**&#x200B;します。

   * **名前** `sling:match`

      * **型** `String`

      * **値** `localhost.4503/`
   * **名前** `sling:internalRedirect`

      * **型** `String`

      * **値** `/content/`


1. 「**すべて保存**」をクリックします。

This will handle a request such as:
`localhost:4503/geometrixx/en/products.html`
as if:
`localhost:4503/content/geometrixx/en/products.html`
had been requested.

>[!NOTE]
>
>使用可能な sling のプロパティとその設定方法について詳しくは、Sling のドキュメントの「[Resources](https://sling.apache.org/site/mappings-for-resource-resolution.html)」を参照してください。

>[!NOTE]
>
>を使用して、発行環境 `/etc/map.publish` の設定を保持できます。 次に、これらを複製し、パブリッシュ環境の `/etc/map.publish`Apache Sling Resource Resolver **の** Mapping Location [](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver) ()に対して設定する必要があります。

