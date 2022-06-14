---
title: URL の外部化
seo-title: Externalizing URLs
description: Externalizer は、プログラムによってリソースパスを外部 URL および絶対 URL に変換できる OSGi サービスです
seo-description: The Externalizer is an OSGI service that allows you to programmatically transform a resource path into an external and absolute URL
uuid: 65bcc352-fc8c-4aa0-82fb-1321a035602d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 938469ad-f466-42f4-8b6f-bfc060ae2785
docset: aem65
exl-id: 971d6c25-1fbe-4c07-944e-be6b97a59922
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 100%

---

# URL の外部化{#externalizing-urls}

AEM の **Externalizer** は、プログラムによってリソースパス（例：`/path/to/my/page`）を外部の絶対 URL（例：`https://www.mycompany.com/path/to/my/page`）に変換できるようにする OSGi サービスであり、その変換はパスに事前設定済みの DNS をプレフィックスとして付けることで実現します。

インスタンスが Web レイヤーの背後で実行されている場合、自身の外部向け URL がわかりません。また、リンクをリクエストスコープの範囲外で作成する必要がある場合があります。これらの理由で、このサービスは、そのような外部 URL を設定して組み立てるための一元化された場所を提供します。

このページでは、**Externalizer** サービスの設定方法と使用方法について説明します。詳しくは、関連する [Javadoc](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html) を参照してください。

## Externalizer サービスの設定 {#configuring-the-externalizer-service}

**Externalizer** サービスでは、プログラムによってリソースパスにプレフィックスを付けるために使用可能な複数のドメインを一元的に定義できます。各ドメインは一意の名前によって識別され、その名前を使用して、プログラムからそのドメインを参照できます。

**Externalizer** サービスのドメインマッピングを定義するには：

1. **ツール**&#x200B;から設定マネージャー、**Web コンソール**&#x200B;の順に移動するか、以下を入力します。

   `https://<host>:<port>/system/console/configMgr`

1. 「**Day CQ Link Externalizer**」をクリックして設定ダイアログボックスを開きます。

   >[!NOTE]
   >
   >この設定に直接アクセスするためのリンクは `https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl` です。

   ![aem-externalizer-01](assets/aem-externalizer-01.png)

1. **ドメイン**&#x200B;マッピングを定義します。マッピングは、次のようなコード内でドメインを参照するために使用できる独自の名前、スペース、ドメインにより構成されます。

   `<unique-name> [scheme://]server[:port][/contextpath]`

   ここで、

   * **スキーム** は通常、http または https ですが、ftp などでもかまいません。

      * 必要に応じて、https を使用して https リンクを強制的に適用します。
      * URL の外部化を要求する際にクライアントコードがスキームを上書きしない場合に使用されます。
   * **server** はホスト名です（ドメイン名または IP アドレス）。
   * **port**（オプション）はポート番号です。
   * **contextpath**（オプション）は、AEM が異なるコンテキストパスの下の Web アプリケーションとしてインストールされている場合に限り設定します。

   例：`production https://my.production.instance`

   次のマッピング名は事前定義されており、AEM で使用されるので、常に設定されている必要があります。

   * `local` - ローカルインスタンス
   * `author` - オーサリングシステムの DNS
   * `publish` - 公開 Web サイトの DNS

   >[!NOTE]
   >
   >カスタム設定を使用すると、`production` や `staging` などの新しいカテゴリや、`my-internal-webservice` などの AEM 以外の外部システムを追加できます。このような URL をプロジェクトのコードベースの様々な場所にハードコーディングするのを防ぐのに役立ちます。

1. 「**保存**」をクリックして変更を保存します。

>[!NOTE]
>
>アドビでは、[この設定をリポジトリに追加する](/help/sites-deploying/configuring.md#addinganewconfigurationtotherepository)ことをお勧めします。

### Externalizer サービスの使用 {#using-the-externalizer-service}

ここでは、**Externalizer** サービスの使用方法に関するいくつかの例を紹介します。

1. **JSP で Externalizer サービスを取得する：**

   ```java
   Externalizer externalizer = resourceResolver.adaptTo(Externalizer.class);
   ```

1. **「publish」ドメインを付与してパスを外部化するには：**

   ```java
   String myExternalizedUrl = externalizer.publishLink(resolver, "/my/page") + ".html";
   ```

   ドメインマッピングが次のような場合：

   * `publish https://www.website.com`

   `myExternalizedUrl` が次の値で終わる。

   * `https://www.website.com/contextpath/my/page.html`


1. **「author」ドメインを付与してパスを外部化するには：**

   ```java
   String myExternalizedUrl = externalizer.authorLink(resolver, "/my/page") + ".html";
   ```

   ドメインマッピングが次のような場合：

   * `author https://author.website.com`

   `myExternalizedUrl` が次の値で終わる。

   * `https://author.website.com/contextpath/my/page.html`


1. **「local」ドメインを付与してパスを外部化するには：**

   ```java
   String myExternalizedUrl = externalizer.externalLink(resolver, Externalizer.LOCAL, "/my/page") + ".html";
   ```

   ドメインマッピングが次のような場合：

   * `local https://publish-3.internal`

   `myExternalizedUrl` が次の値で終わる。

   * `https://publish-3.internal/contextpath/my/page.html`


1. 他の例については、関連する [Javadoc](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html) を参照してください。
