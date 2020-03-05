---
title: Brand Portal へのフォルダーの公開
seo-title: Brand Portal へのフォルダーの公開
description: Brand Portal へのフォルダーの公開および非公開の方法を説明します。
seo-description: Brand Portal へのフォルダーの公開および非公開の方法を説明します。
uuid: 350beb85-c0fb-4a1c-8597-c03592c02d3d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: brand-portal
content-type: reference
discoiquuid: 39b8cf9b-afec-4c9a-8a5d-7fc87e643f26
docset: aem65
translation-type: tm+mt
source-git-commit: 9f923782d3d0a7bdf45b18e8025bd2d083acf77c

---


# Brand Portal へのフォルダーの公開{#publish-folders-to-brand-portal}

Adobe Experience Manager（AEM）Assets の管理者は、アセットやフォルダーを組織の AEM Assets Brand Portal インスタンスに公開（または公開ワークフローを未来の日時で設定）できます。ただし、最初に AEM Assets を Brand Portal と統合する必要があります。For details, see [Configure AEM Assets with Brand Portal](/help/assets/configure-aem-assets-with-brand-portal.md).

アセットまたはフォルダを公開すると、Brand Portalでそのアセットまたはフォルダをユーザが使用できるようになります。

AEM Assetsの元のアセットまたはフォルダーに対して後で変更を行った場合、その変更は、アセットまたはフォルダーを再公開するまでBrand Portalに反映されません。 この機能を使用すると、作業中の変更がBrand Portalで使用できなくなります。 Brand Portalでは、管理者が発行した承認済みの変更のみを利用できます。

## Brand Portal へのフォルダーの公開 {#publish-folders-to-brand-portal-1}

1. From the AEM Assets interface, hover over the desired folder and select **Publish** option from the quick actions.

   あるいは、目的のフォルダーを選択して後述の手順に従います。

   ![publish2bp](assets/publish2bp.png)

1. **フォルダーを今すぐ公開**

   選択したフォルダーを Brand Portal に公開するには、次のいずれかを実行します。

   * From the toolbar, select **Quick Publish**. Then from the menu, select **Publish to Brand Portal**.

   * From the toolbar, select **Manage Publication**.
   1. 「アクシ **ョン** 」から「Publish to Portal **」を選択し、「Scheduling** Now **Brand********Now」を選択し、「Click Next」を選択します。**
   1. 「スコープ」での選択を確 **認し** 、「ブランドポ **ータルに投稿」をクリックします**。
   フォルダーが Brand Portal への公開用のキューに入れられたことを示すメッセージが表示されます。Brand Portal のインターフェイスにログインして、公開されたフォルダーを確認します。

   **フォルダーを後で公開**

   アセットフォルダのBrand Portalへの投稿ワークフローを後日にスケジュールするには：

   1. Once you have selected assets/ folders to publish, select **Manage Publication** from the tool bar at the top.
   1. 「アクシ **ョン** 」から「Publish to Brand **Portal**」を選択し、「Scheduling ******** Later」から「Brand Portal」を選択します。

      ![publishlatebp](assets/publishlaterbp.png)

   1. Select an **Activation date** and specify time. 「**次へ**」をクリックします。
   1. Confirm your selection in **Scope**. 「**次へ**」をクリックします。
   1. Specify a Workflow title under **Workflows**. Click **Publish Later**.

      ![manageschedulepub](assets/manageschedulepub.png)



## Brand Portal へのフォルダーの公開の取り消し {#unpublish-folders-from-brand-portal}

AEM オーサーインスタンスからアセットインスタンスの公開を取り消すことで、Brand Portal に公開されているアセットフォルダーを削除できます。元のフォルダーの公開を取り消すと、そのコピーはBrand Portalユーザーは使用できなくなります。

Brand Portal へのフォルダーの公開をすぐに取り消すことも、取り消しのスケジュールを未来の日時で設定することもできます。Brand Portal へのアセットフォルダーの公開を取り消すには、次のようにします。

1. AEM オーサーインスタンス内の AEM Assets インターフェイスで、公開を取り消すフォルダーを選択します。

   ![publish2bp-1](assets/publish2bp.png)

1. From the toolbar, Click **Manage Publication**.

1. **Brand Portal への公開を今すぐ取り消し**

   Brand Portal へのフォルダーの公開をすぐに取り消すには、次のようにします。

   1. From the toolbar, select **Manage Publication**.
   1. 「アクシ **ョン** 」から「Brand Portalから非公開」を選択し、 **Scheduling** Now **Click Now********Click Next」を選択します。**
   1. 「スコープ」での選択を確 **認し** 、「Brand Portalか **ら非公開」をクリックします**。
   ![非公開の確認](assets/confirm-unpublish.png)

   **後でBrand Portalから非公開にする**

   Brand Portal へのフォルダーの公開を停止するスケジュールを未来の日時で設定するには、次のようにします。

   1. From the toolbar, select **Manage Publication**.
   1. From **Action** select **Unpublish from Brand Portal**, and from **Scheduling** select **Later**.
   1. Select an **Activation date** and specify the time. 「**次へ**」をクリックします。
   1. 「スコープ」での選択を確 **認し** 、「次へ」をクリ **ックします**。
   1. Specify a **Workflow title** in **Workflows**. Click **Unpublish Later.**

      ![unpublishworkflows](assets/unpublishworkflows.png)


>[!NOTE]
>
>Brand Portalに対してアセットを公開/非公開する手順は、フォルダの対応する手順と似ています。

