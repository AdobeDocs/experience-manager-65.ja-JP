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
feature: Brand Portal
role: Business Practitioner
exl-id: 92a156f0-ce2a-4c83-bd57-0c29efbf784f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 67%

---

# Brand Portal へのフォルダーの公開{#publish-folders-to-brand-portal}

Adobe Experience Manager（AEM）Assets の管理者は、アセットやフォルダーを組織の AEM Assets Brand Portal インスタンスに公開（または公開ワークフローを未来の日時で設定）できます。ただし、最初に AEM Assets を Brand Portal と統合する必要があります。詳しくは [AEM Assets と Brand Portal の連携の設定](/help/assets/configure-aem-assets-with-brand-portal.md)を参照してください。

アセットまたはフォルダーを公開すると、Brand Portalのユーザーがそのアセットまたはフォルダーを使用できるようになります。

その後、AEM Assetsで元のアセットまたはフォルダーに変更を加えても、そのアセットまたはフォルダーを再公開するまで、変更はBrand Portalに反映されません。 このため、作業中の変更が Brand Portal に提供されることがありません。管理者が公開した承認済みの変更のみが Brand Portal で提供されます。

## Brand Portal へのフォルダーの公開 {#publish-folders-to-brand-portal-1}

1. AEM Assetsインターフェイスで、目的のフォルダーの上にマウスポインターを置き、クイックアクションから「**公開**」オプションを選択します。

   あるいは、目的のフォルダーを選択して後述の手順に従います。

   ![publish2bp](assets/publish2bp.png)

1. **フォルダーを今すぐ公開**

   選択したフォルダーを Brand Portal に公開するには、次のいずれかを実行します。

   * ツールバーで「**クイック公開**」を選択します。次に、メニューから「**Brand Portalに公開**」を選択します。

   * ツールバーで「**公開を管理**」を選択します。
   1. **アクション**&#x200B;から「**Brand Portalに公開**」を選択し、**スケジュール**&#x200B;から「**今すぐ**」を選択して、「**次へ**」をクリックします。
   1. 「**範囲**」の選択を確認し、「**Brand Portal に公開**」をクリックします。

   フォルダーが Brand Portal への公開用のキューに入れられたことを示すメッセージが表示されます。Brand Portal のインターフェイスにログインして、公開されたフォルダーを確認します。

   **フォルダーを後で公開**

   アセットフォルダーのBrand Portalへの公開ワークフローを後の日時にスケジュールするには：

   1. 公開するアセット/フォルダーを選択したら、上部のツールバーから「**公開を管理**」を選択します。
   1. **アクション**&#x200B;から「**Brand Portalに公開**」を選択し、**スケジュール**&#x200B;から「**後で**」を選択します。

      ![publishlaterbp](assets/publishlaterbp.png)

   1. 「**アクティベート日**」を選択して時刻を指定します。「**次へ**」をクリックします。
   1. 「**範囲**」で選択内容を確認します。「**次へ**」をクリックします。
   1. 「**ワークフロー**」でワークフロータイトルを指定します。「**後で公開する**」をクリックします。

      ![manageschedulepub](assets/manageschedulepub.png)



## Brand Portal へのフォルダーの非公開 {#unpublish-folders-from-brand-portal}

AEM オーサーインスタンスからアセットインスタンスの公開を取り消すことで、Brand Portal に公開されているアセットフォルダーを削除できます。元のフォルダーを非公開にすると、Brand Portal ユーザーはそのコピーを使用できなくなります。

Brand Portal へのフォルダーの公開をすぐに取り消すことも、取り消しのスケジュールを未来の日時で設定することもできます。Brand Portal へのアセットフォルダーを非公開にするには、次の手順を実行します。

1. AEM オーサーインスタンス内の AEM Assets インターフェイスで、公開を取り消すフォルダーを選択します。

   ![publish2bp-1](assets/publish2bp.png)

1. ツールバーの「**公開を管理**」をクリックします。

1. **Brand Portal への公開を今すぐ取り消し**

   Brand Portal へのフォルダーの公開をすぐに取り消すには、次のようにします。

   1. ツールバーで「**公開を管理**」を選択します。
   1. **アクション**&#x200B;から「**Brand Portalから非公開**」を選択し、**スケジュール**&#x200B;から「**今すぐ**」を選択して、「**次へ**」をクリックします。
   1. 「**範囲**」の選択を確認し、「**Brand Portal から非公開**」をクリックします。

   ![confirm-unpublish](assets/confirm-unpublish.png)

   **後でBrand Portalから非公開にする**

   Brand Portal へのフォルダーの公開を停止するスケジュールを未来の日時で設定するには、次のようにします。

   1. ツールバーで「**公開を管理**」を選択します。
   1. **アクション**&#x200B;から「**Brand Portalから非公開**」を選択し、「**スケジュール**」から「**後で**」を選択します。
   1. 「**アクティベート日**」を選択して時刻を指定します。「**次へ**」をクリックします。
   1. 「**範囲**」で選択内容を確認し、「**次へ**」をクリックします。
   1. 「**ワークフロー**」で&#x200B;**ワークフロータイトル**&#x200B;を指定します。**後で非公開にするをクリックします。**

      ![unpublishworkflows](assets/unpublishworkflows.png)


>[!NOTE]
>
>Brand Portalに対してアセットを公開/非公開にする手順は、フォルダーに対する対応する手順と似ています。
