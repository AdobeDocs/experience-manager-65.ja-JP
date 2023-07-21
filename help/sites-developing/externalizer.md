---
title: URL の外部化
description: Externalizer は、プログラムによってリソースパスを外部および絶対 URL に変換できる OSGi サービスです
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
docset: aem65
exl-id: 971d6c25-1fbe-4c07-944e-be6b97a59922
source-git-commit: a56d5121a6ce11b42a6c30dae9e479564d16af27
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 58%

---

# URL の外部化{#externalizing-urls}

Adobe Experience Manager(AEM) では、 **Externalizer** は、リソースパス ( 例えば、 `/path/to/my/page`) を外部 URL や絶対 URL( 例えば、 `https://www.mycompany.com/path/to/my/page`) を追加する必要があります。

インスタンスが Web レイヤーの背後で実行されている場合、自身の外部向け URL がわかりません。また、リンクをリクエストスコープの範囲外で作成する必要がある場合があります。これらの理由で、このサービスは、そのような外部 URL を設定して組み立てるための一元化された場所を提供します。

このページでは、 **Externalizer** サービスとその使用方法について説明します。 詳しくは、 [Javadocs](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/Externalizer.html).

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

1. を定義 **ドメイン** マッピング：マッピングは、ドメイン、スペースおよびドメインを参照するためにコード内で使用できる一意の名前で構成されます。

   `<unique-name> [scheme://]server[:port][/contextpath]`

   ここで、

   * **スキーム** は http または https ですが、ftp などでもかまいません。

      * 必要に応じて、https を使用して https リンクを強制します。
      * URL の外部化を要求する際に、クライアントコードがスキームを上書きしない場合に使用されます。

   * **server** はホスト名です（ドメイン名または IP アドレス）。
   * **port**（オプション）はポート番号です。
   * **contextpath**（オプション）は、AEM が異なるコンテキストパスの下の Web アプリケーションとしてインストールされている場合に限り設定します。

   例：`production https://my.production.instance`

   AEMでは次のマッピング名が使用されるので、事前に定義されており、設定する必要があります。

   * `local` - ローカルインスタンス
   * `author` - オーサリングシステムの DNS
   * `publish` - 公開 Web サイトの DNS

   >[!NOTE]
   >
   >カスタム設定を使用すると、次のようなカテゴリを追加できます。 `production`, `staging`または外部の非AEMシステム ( `my-internal-webservice`. このような URL をプロジェクトのコードベースの様々な場所にハードコーディングするのを防ぐのに役立ちます。

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

1. 他の例については、関連する [Javadoc](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/Externalizer.html) を参照してください。
