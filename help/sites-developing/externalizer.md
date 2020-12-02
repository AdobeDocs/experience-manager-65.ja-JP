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

AEMでは、**Externalizer**&#x200B;はOSGIサービスで、リソースパス(例えば、`/path/to/my/page`)を外部URLや絶対URL（例えば`https://www.mycompany.com/path/to/my/page`）に埋め込みます。

インスタンスがWebレイヤーの背後で実行されている場合は、その外部に表示されるURLを知ることはできないので、要求範囲外でリンクを作成する必要がある場合があるので、このサービスを使用して、これらの外部URLを設定して構築することができます。

このページでは、**Externalizer** サービスの設定方法と使用方法について説明します。詳しくは、関連する [Javadoc](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html) を参照してください。

## Externalizer サービスの設定  {#configuring-the-externalizer-service}

**Externalizer**&#x200B;サービスを使用すると、プログラム的にリソースパスをプレフィックスするために使用できる複数のドメインを一元的に定義できます。各ドメインは、そのドメインをプログラムで参照する際に使用される一意の名前で識別されます。

**Externalizer** サービスのドメインマッピングを定義するには：

1. **ツール**&#x200B;から&#x200B;**Webコンソール**&#x200B;に移動するか、次のように入力します。

   `https://<host>:<port>/system/console/configMgr`

1. 「**Day CQ Link Externalizer**」をクリックして、設定ダイアログボックスを開きます。

   >[!NOTE]
   >
   >構成への直接リンクは`https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl`です

   ![aem-externalizer-01](assets/aem-externalizer-01.png)

1. **ドメイン**&#x200B;マッピングを定義します。マッピングは、ドメイン、スペース、ドメインを参照するコードで使用できる一意の名前で構成されます。

   `<unique-name> [scheme://]server[:port][/contextpath]`

   ここで、

   * **** schemeは通常、httpまたはhttpsですが、ftpなども使用できます。

      * 必要に応じてhttpsを使用し、httpsリンクを強制する
      * URLの外部化を要求する際に、クライアントコードがスキームを上書きしない場合に使用されます。
   * **** serverはホスト名です（ドメイン名またはipアドレスを指定できます）。
   * **port** （オプション）はポート番号です。
   * **contextpath** （オプション）は、AEMがwebアプリとして別のコンテキストパスの下にインストールされている場合にのみ設定されます。

   例：`production https://my.production.instance`

   次のマッピング名は事前に定義されており、AEMがそれらに依存しているため、常に設定する必要があります。

   * `local`  — ローカルインスタンス
   * `author`  — オーサリングシステムのDNS
   * `publish` - 公開 Web サイトの DNS

   >[!NOTE]
   >
   >カスタム設定を使用すると、`production`、`staging`などの新しいカテゴリや、`my-internal-webservice`などの外部のAEM以外のシステムを追加できます。 プロジェクトのコードベース内の異なる場所にまたがるこのようなURLのハードコーディングを避けると便利です。

1. 「**保存**」をクリックして変更を保存します。

>[!NOTE]
>
>Adobeでは、[リポジトリ](/help/sites-deploying/configuring.md#addinganewconfigurationtotherepository)に設定を追加することを推奨します。

### Externalizer サービスの使用 {#using-the-externalizer-service}

この節では、**Externalizer**&#x200B;サービスの使用例をいくつか示します。

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
