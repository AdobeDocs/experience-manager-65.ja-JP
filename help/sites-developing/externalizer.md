---
title: URL の外部化
seo-title: URL の外部化
description: Externalizer は、プログラムによってリソースパスを外部 URL および絶対 URL に変換できる OSGi サービスです
seo-description: Externalizer は、プログラムによってリソースパスを外部 URL および絶対 URL に変換できる OSGi サービスです
uuid: 65bcc352-fc8c-4aa0-82fb-1321a035602d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 938469ad-f466-42f4-8b6f-bfc060ae2785
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 31%

---


# URL の外部化{#externalizing-urls}

In AEM, the **Externalizer** is an OSGI service that allows you to programmatically transform a resource path (e.g. `/path/to/my/page`) into an external and absolute URL (for example, `https://www.mycompany.com/path/to/my/page`) by prefixing the path with a pre-configured DNS.

インスタンスがWebレイヤーの背後で実行されている場合は、その外部に表示されるURLを知ることはできないので、要求範囲外でリンクを作成する必要がある場合があるので、このサービスを使用して、これらの外部URLを設定して構築することができます。

このページでは、**Externalizer** サービスの設定方法と使用方法について説明します。詳しくは、関連する [Javadoc](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html) を参照してください。

## Externalizer サービスの設定 {#configuring-the-externalizer-service}

The **Externalizer** service allows you to centrally define multiple domains that can be used to programmatically prefix resource paths. Each domain is identified by a unique name that is used to programmatically reference the domain.

**Externalizer** サービスのドメインマッピングを定義するには：

1. Navigate to the configuration manager via **Tools**, then **Web Console**, or enter:

   `https://<host>:<port>/system/console/configMgr`

1. Click **Day CQ Link Externalizer** to open the configuration dialog box.

   >[!NOTE]
   >
   >The direct link to the configuration is `https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl`

   ![aem-externalizer-01](assets/aem-externalizer-01.png)

1. Define a **Domains** mapping: a mapping consists of a unique name that can be used in the code to reference the domain, a space and the domain:

   `<unique-name> [scheme://]server[:port][/contextpath]`

   ここで、

   * **scheme** は通常、httpまたはhttpsですが、ftpなどを指定することもできます。

      * 必要に応じてhttpsを使用し、httpsリンクを強制する
      * URLの外部化を要求する際に、クライアントコードがスキームを上書きしない場合に使用されます。
   * **server** はホスト名です（ドメイン名またはipアドレスを指定できます）。
   * **port** （オプション）はポート番号です。
   * **contextpath** （オプション）は、AEMがwebアプリとして別のコンテキストパスの下にインストールされている場合にのみ設定されます。

   例：`production https://my.production.instance`

   次のマッピング名は事前に定義されており、AEMがそれらに依存しているため、常に設定する必要があります。

   * `local`  — ローカルインスタンス
   * `author`  — オーサリングシステムのDNS
   * `publish` - 公開 Web サイトの DNS

   >[!NOTE]
   >
   >カスタム設定を使用すると、新しいカテゴリ（など）を追加でき `production`ます。また、 `staging` などの外部のAEM以外のシステムも追加でき `my-internal-webservice`ます。 プロジェクトのコードベース内の異なる場所にまたがるこのようなURLのハードコーディングを避けると便利です。

1. 「**保存**」をクリックして変更を保存します。

>[!NOTE]
>
>Adobe recommends that you [add the configuration to the repository](/help/sites-deploying/configuring.md#addinganewconfigurationtotherepository).

### Externalizer サービスの使用 {#using-the-externalizer-service}

This section shows a few examples of how the **Externalizer** service can be used:

1. **JSP で Externalizer サービスを取得する：**

   ```java
   Externalizer externalizer = resourceResolver.adaptTo(Externalizer.class);
   ```

1. **「publish」ドメインを付与してパスを外部化する：**

   ```java
   String myExternalizedUrl = externalizer.publishLink(resolver, "/my/page") + ".html";
   ```

   ドメインマッピングの前提：

   * `publish https://www.website.com`

   `myExternalizedUrl` は次の値で終わります。

   * `https://www.website.com/contextpath/my/page.html`


1. **「author」ドメインを付与してパスを外部化するには：**

   ```java
   String myExternalizedUrl = externalizer.authorLink(resolver, "/my/page") + ".html";
   ```

   ドメインマッピングの前提：

   * `author https://author.website.com`

   `myExternalizedUrl` は次の値で終わります。

   * `https://author.website.com/contextpath/my/page.html`


1. **「local」ドメインを付与してパスを外部化するには：**

   ```java
   String myExternalizedUrl = externalizer.externalLink(resolver, Externalizer.LOCAL, "/my/page") + ".html";
   ```

   ドメインマッピングの前提：

   * `local https://publish-3.internal`

   `myExternalizedUrl` は次の値で終わります。

   * `https://publish-3.internal/contextpath/my/page.html`


1. 他の例については、関連する [Javadoc](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html) を参照してください。
