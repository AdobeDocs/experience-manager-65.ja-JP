---
title: Adobe Target との統合の前提条件
seo-title: Prerequisites for Integrating with Adobe Target
description: Adobe Target との統合の前提条件について説明します。
seo-description: Find out about the prerequisites for integrating with Adobe Target.
uuid: 55d87a96-5fe7-4f7e-93c1-fdf7fbb7c971
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: ae4a6e97-c0d7-472d-a25f-b89b1abf4df3
docset: aem65
exl-id: 30813c44-51ac-4e6e-8ee6-4e8baacb1ff9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '557'
ht-degree: 100%

---

# Adobe Target との統合の前提条件{#prerequisites-for-integrating-with-adobe-target}

[AEM と Adobe Target の統合](/help/sites-administering/target.md)の一環として、Adobe Target を登録し、レプリケーションエージェントを設定して、パブリッシュノードでアクティビティ設定を保護する必要があります。

## Adobe Target の登録 {#registering-with-adobe-target}

AEM と Adobe Target を統合するには、有効な Adobe Target アカウントが必要です。このアカウントには、**承認者**&#x200B;レベル以上の権限が必要です。Adobe Target に登録すると、クライアントコードを受け取ります。AEM を Adobe Target に接続するには、クライアントコードおよび Adobe Target のログイン名とパスワードが必要です。

クライアントコードは、Adobe Target サーバーを呼び出すときに Adobe Target の顧客アカウントを識別します。

>[!NOTE]
>
>統合を使用するには、Target チームによってご自身のアカウントも有効にされている必要があります。
>
>そうでない場合は、[Adobe カスタマーケア](https://docs.adobe.com/content/help/ja/target/using/cmp-resources-and-contact-information.html)にご連絡ください。

## Target レプリケーションエージェントの有効化 {#enabling-the-target-replication-agent}

Test &amp; Target [レプリケーションエージェント](/help/sites-deploying/replication.md)を作成者インスタンス上で有効にする必要があります。AEM のインストールに [nosamplecontent](/help/sites-deploying/configure-runmodes.md#using-samplecontent-and-nosamplecontent) 実行モードを使用した場合、このレプリケーションエージェントはデフォルトでは有効になっていません。実稼動環境の保護に関する情報については、[セキュリティチェックリスト](/help/sites-administering/security-checklist.md)を参照してください。

1. AEM のホームページで、**ツール**／**導入**／**レプリケーション**&#x200B;をクリックまたはタップします。
1. 「**作成者のエージェント**」をクリックまたはタップします。
1. **Test &amp; Target**&#x200B;レプリケーションエージェントをクリックまたはタップして、「**編集**」をクリックまたはタップします。
1. 「有効」オプションをオンにして、「**OK**」をクリックまたはタップします。

   >[!NOTE]
   >
   >Test &amp; Target レプリケーションエージェントを設定する場合、URI は、「**トランスポート**」タブでデフォルトで **tnt:///** に設定されています。この URI を **https://admin.testandtarget.omniture.com** に置換しないでください。
   >
   >**tnt:///** を使用して接続をテストしようとすると、エラーが発生することに注意してください。これは想定されている動作です。この URI は内部でのみ使用されるべきものであり、**接続をテスト**&#x200B;では使用すべきではありません。

## アクティビティ設定ノードの保護 {#securing-the-activity-settings-node}

権限のないユーザーがアクセスできないように、パブリッシュインスタンスでアクティビティ設定ノード **cq:ActivitySettings** を保護する必要があります。アクティビティ設定ノードには、Adobe Target へのアクティビティの同期を処理するサービスのみがアクセスできるようにしてください。

**cq:ActivitySettings** ノードは、*アクティビティ jcr:content ノードの下*&#x200B;の `/content/campaigns/*nameofbrand*`* の下の CRXDE Lite で利用できます（例：`/content/campaign/we-retail/master/myactivity/jcr:content/cq:ActivitySettings`）。このノードは、コンポーネントのターゲティング後にのみ作成されます。

アクティビティの jcr:content の下にある **cq:ActivitySettings** ノードは、次の ACL によって保護されています。

* すべて拒否（全員）
* &quot;target-activity-authors&quot; に jcr:read,rep:write を許可（デフォルトで作成者はこのグループのメンバー）
* &quot;targetservice&quot; に jcr:read,rep:write を許可

これらの設定により、権限を持たないユーザーがノードプロパティにアクセスできなくなります。オーサーインスタンスとパブリッシュインスタンスの両方で同じ ACL を使用します。詳しくは、[ユーザー管理とセキュリティ](/help/sites-administering/security.md)を参照してください。

## AEM Link Externalizer の設定 {#configuring-the-aem-link-externalizer}

Adobe Target でアクティビティを編集する場合、AEM オーサーノードで URL を変更していなければ、URL は **localhost** を指しています。書き出すコンテンツを特定の&#x200B;*Publish*&#x200B;ドメインに指定する場合は、AEM Link Externalizer を設定できます。

>[!NOTE]
>
>[クラウド設定を追加](/help/sites-administering/experience-fragments-target.md#add-the-cloud-configuration)も参照してください。

AEM Externalizer を設定するには：

>[!NOTE]
>
>詳しくは、[URL の外部化](/help/sites-developing/externalizer.md)を参照してください。

1. **https://&lt;server>:&lt;port>/system/console/configMgr** の OSGi Web コンソールに移動します。
1. **Day CQ Link Externalizer** を探し、オーサーノードのドメインを入力します。

   ![chlimage_1-120](assets/aem-externalizer-01.png)
