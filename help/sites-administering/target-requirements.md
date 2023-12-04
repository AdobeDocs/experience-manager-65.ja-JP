---
title: Adobe Target との統合の前提条件
description: Adobe Targetとの統合の前提条件について説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: 30813c44-51ac-4e6e-8ee6-4e8baacb1ff9
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 46%

---

# Adobe Target との統合の前提条件{#prerequisites-for-integrating-with-adobe-target}

の一部として [AEMとAdobe Targetの統合](/help/sites-administering/target.md)を使用する場合は、Adobe Targetに登録し、レプリケーションエージェントを設定し、パブリッシュノードでアクティビティのセキュリティを保護する必要があります。

## Adobe Targetへの登録 {#registering-with-adobe-target}

AEMをAdobe Targetと統合するには、有効なAdobe Targetアカウントが必要です。 このアカウントには、**承認者**&#x200B;レベル以上の権限が必要です。Adobe Target に登録すると、クライアントコードを受け取ります。AEMをAdobe Targetに接続するには、クライアントコードとAdobe Targetのログイン名およびパスワードが必要です。

クライアントコードは、Adobe Targetサーバーを呼び出す際にAdobe Targetの顧客アカウントを識別します。

>[!NOTE]
>
>統合を使用するには、Target チームがアカウントを有効にする必要もあります。
>
>該当しない場合は、 [Adobeカスタマーケア](https://experienceleague.adobe.com/docs/target/using/cmp-resources-and-contact-information.html?lang=ja).

## Target レプリケーションエージェントの有効化 {#enabling-the-target-replication-agent}

Test &amp; Target [レプリケーションエージェント](/help/sites-deploying/replication.md)を作成者インスタンス上で有効にする必要があります。AEM のインストールに [nosamplecontent](/help/sites-deploying/configure-runmodes.md#using-samplecontent-and-nosamplecontent) 実行モードを使用した場合、このレプリケーションエージェントはデフォルトでは有効になっていません。実稼動環境の保護について詳しくは、 [セキュリティチェックリスト](/help/sites-administering/security-checklist.md).

1. AEMホームページで、 **ツール** > **導入** > **レプリケーション**.
1. クリック **作成者のエージェント**.
1. 次をクリック： **Test と Target（test と Target）** レプリケーションエージェントを選択し、「 **編集**.
1. 「有効」オプションを選択し、「 **OK**.

   >[!NOTE]
   >
   >Test と Target のレプリケーションエージェントを設定する際に、 **輸送** 」タブに設定されている場合、URI はデフォルトで「 **tnt:///**. この URI を **https://admin.testandtarget.omniture.com** に置換しないでください。
   >
   >接続をテストしようとする場合 **tnt:///**&#x200B;を呼び出すと、エラーがスローされます。 この URI は内部でのみ使用されるので、これは期待された動作です。では使用しないでください。 **接続をテスト**.

## アクティビティ設定ノードの保護 {#securing-the-activity-settings-node}

パブリッシュインスタンスでアクティビティ設定ノード **cq:ActivitySettings** を保護し、通常のユーザーがアクセスできないようにします。アクティビティ設定ノードには、Adobe Target へのアクティビティの同期を処理するサービスのみがアクセスできるようにしてください。

The **cq:ActivitySettings** ノードは、CRXDE lite の下の `/content/campaigns/*nameofbrand*`* *activitys jcr:content ノードの下で、* *例： `/content/campaign/we-retail/master/myactivity/jcr:content/cq:ActivitySettings`. このノードは、コンポーネントのターゲティング後にのみ作成されます。

アクティビティの jcr:content の下にある **cq:ActivitySettings** ノードは、次の ACL によって保護されています。

* 全員に対してすべて拒否
* 「target-activity-authors」に対して jcr:read,rep:write を許可します (author はこのグループのメンバーです。
* 「targetservice」の jcr:read,rep:write を許可

これらの設定により、通常のユーザーはノードプロパティにアクセスできなくなります。 オーサーとパブリッシュで同じ ACL を使用します。 詳しくは、[ユーザー管理とセキュリティ](/help/sites-administering/security.md)を参照してください。

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

   ![Day CQ Link Externalizer](assets/aem-externalizer-01.png)
