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
exl-id: 971d6c25-1fbe-4c07-944e-be6b97a59922
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 31%

---

# URL の外部化{#externalizing-urls}

AEMの&#x200B;**Externalizer**&#x200B;は、リソースパス(例えば、`/path/to/my/page`)を外部URLと絶対URL（例えば、`https://www.mycompany.com/path/to/my/page`）に埋め込みます。

インスタンスがWebレイヤーの背後で実行されている場合、外部で表示されるURLを認識できないので、リクエスト範囲外でリンクを作成する必要が生じる場合があるので、このサービスを使用して、外部URLを設定して作成できます。

このページでは、**Externalizer** サービスの設定方法と使用方法について説明します。詳しくは、関連する [Javadoc](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html) を参照してください。

## Externalizer サービスの設定  {#configuring-the-externalizer-service}

**Externalizer**&#x200B;サービスを使用すると、リソースパスにプログラム的にプレフィックスを付けるために使用できる複数のドメインを一元的に定義できます。各ドメインは、プログラムでドメインを参照する際に使用される一意の名前で識別されます。

**Externalizer** サービスのドメインマッピングを定義するには：

1. **ツール**&#x200B;から設定マネージャーに移動し、**Webコンソール**&#x200B;を開くか、次のように入力します。

   `https://<host>:<port>/system/console/configMgr`

1. **Day CQ Link Externalizer**&#x200B;をクリックして、設定ダイアログボックスを開きます。

   >[!NOTE]
   >
   >設定への直接リンクは`https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl`です。

   ![aem-externalizer-01](assets/aem-externalizer-01.png)

1. **ドメイン**&#x200B;マッピングを定義します。マッピングは、ドメイン、スペースおよびドメインを参照するコードで使用できる一意の名前で構成されます。

   `<unique-name> [scheme://]server[:port][/contextpath]`

   ここで、

   * **** スキーマは通常、httpまたはhttpsですが、ftpなどの場合もあります。

      * 必要に応じて、httpsを使用してhttpsリンクを強制します。
      * URLの外部化を要求する際にクライアントコードがスキームを上書きしない場合に使用されます。
   * **** serverはホスト名です（ドメイン名またはipアドレスを使用できます）。
   * **port** （オプション）はポート番号です。
   * **contextpath** （オプション）は、AEMが別のコンテキストパスの下にwebアプリとしてインストールされている場合にのみ設定されます。

   例：`production https://my.production.instance`

   次のマッピング名は事前に定義されており、AEMがこれらを利用するため常に設定する必要があります。

   * `local`  — ローカルインスタンス
   * `author`  — オーサリングシステムのDNS
   * `publish` - 公開 Web サイトの DNS

   >[!NOTE]
   >
   >カスタム設定を使用すると、`production`、`staging`などの新しいカテゴリや、`my-internal-webservice`などの外部のAEM以外のシステムを追加できます。 このようなURLを、プロジェクトのコードベースの異なる場所にハードコーディングするのを防ぐのに役立ちます。

1. 「**保存**」をクリックして変更を保存します。

>[!NOTE]
>
>Adobeでは、リポジトリに[設定を追加することをお勧めします。](/help/sites-deploying/configuring.md#addinganewconfigurationtotherepository)

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

   ドメインマッピングが次のような場合：

   * `publish https://www.website.com`

   `myExternalizedUrl` 値で終わる

   * `https://www.website.com/contextpath/my/page.html`


1. **「author」ドメインを付与してパスを外部化するには：**

   ```java
   String myExternalizedUrl = externalizer.authorLink(resolver, "/my/page") + ".html";
   ```

   ドメインマッピングが次のような場合：

   * `author https://author.website.com`

   `myExternalizedUrl` 値で終わる

   * `https://author.website.com/contextpath/my/page.html`


1. **「local」ドメインを付与してパスを外部化するには：**

   ```java
   String myExternalizedUrl = externalizer.externalLink(resolver, Externalizer.LOCAL, "/my/page") + ".html";
   ```

   ドメインマッピングが次のような場合：

   * `local https://publish-3.internal`

   `myExternalizedUrl` 値で終わる

   * `https://publish-3.internal/contextpath/my/page.html`


1. 他の例については、関連する [Javadoc](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html) を参照してください。
