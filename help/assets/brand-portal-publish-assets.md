---
title: Brand Portal へのアセットの公開
seo-title: Brand Portal へのアセットの公開
description: Brand Portalへのアセットの公開と非公開の方法について説明します。
seo-description: Brand Portalへのアセットの公開と非公開の方法について説明します。
uuid: 350beb85-c0fb-4a1c-8597-c03592c02d3d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: brand-portal
content-type: reference
discoiquuid: 39b8cf9b-afec-4c9a-8a5d-7fc87e643f26
docset: aem65
feature: Brand Portal
role: Business Practitioner
exl-id: 76652a16-cad6-4e95-9e66-41efec452b03
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 62%

---

# Brand Portal へのアセットの公開 {#publish-assets-to-brand-portal}

Adobe Experience Manager（AEM）Assets の管理者は、アセットやフォルダーを組織の AEM Assets Brand Portal インスタンスに公開（または公開ワークフローを未来の日時で設定）できます。ただし、最初に AEM Assets を Brand Portal と連携するように設定する必要があります。詳しくは [AEM Assets と Brand Portal の連携の設定](/help/assets/configure-aem-assets-with-brand-portal.md)を参照してください。

レプリケーションが正常に終了したら、アセット、フォルダー、コレクションを Brand Portal に公開することができます。アセットを Brand Portal に公開するには、次の手順を実行します。

>[!NOTE]
>
>AEM オーサーが過剰なリソースを占有しないように、できればピーク時を避け、時間をずらして公開することをお勧めします。

1. アセットコンソールで、公開するアセットまたはフォルダーを選択し、ツールバーの「**[!UICONTROL クイック公開]**」オプションをクリックします。

   または、Brand Portal に公開するアセットを選択します。

   ![publish2bp-2](assets/publish2bp.png)

1. アセットをBrand Portalに公開するには、次の2つのオプションを使用できます。
   * [アセットを直ちに公開する](#publish-to-bp-now)
   * [アセットを後で公開](#publish-to-bp-now)

## アセットを今すぐ公開 {#publish-to-bp-now}

選択したアセットを Brand Portal に公開するには、次のいずれかを実行します。

* ツールバーで「**[!UICONTROL クイック公開]**」を選択します。次に、メニューから「**[!UICONTROL Brand Portalに公開]**」を選択します。

* ツールバーで「**[!UICONTROL 公開を管理]**」を選択します。

   1. 次に、「**[!UICONTROL アクション]**」から「**[!UICONTROL Brand Portalに公開]**」を選択し、「**[!UICONTROL スケジュール]**」から「**[!UICONTROL 今すぐ]**」を選択します。 「**[!UICONTROL 次へ]**」をクリックします。

   2. **[!UICONTROL 範囲]**&#x200B;内で、選択内容を確認し、「**[!UICONTROL Brand Portalに公開]**」をクリックします。

アセットが Brand Portal への公開用のキューに入れられたことを示すメッセージが表示されます。Brand Portal のインターフェイスにログインして、公開されたアセットを確認します。

## アセットを後で公開 {#publish-to-bp-later}

アセットを Brand Portal に公開するスケジュールを後の日時に設定するには、次の手順を実行します。

1. 公開するアセット/フォルダーを選択したら、上部のツールバーから「**[!UICONTROL 公開を管理]**」を選択します。

1. **[!UICONTROL 公開を管理]**&#x200B;ページで、**[!UICONTROL アクション]**&#x200B;から「**[!UICONTROL Brand Portalに公開]**」を選択し、**[!UICONTROL スケジュール]**&#x200B;から「**[!UICONTROL 後で]**」を選択します。

   ![publishlaterbp-1](assets/publishlaterbp-1.png)

1. 「**[!UICONTROL アクティベート日]**」を選択して時刻を指定します。「**[!UICONTROL 次へ]**」をクリックします。

1. 「**アクティベート日**」を選択して時刻を指定します。「**次へ**」をクリックします。

1. 「**[!UICONTROL ワークフロー]**」で&#x200B;**[!UICONTROL ワークフロータイトル]**&#x200B;を指定します。「**[!UICONTROL 後で公開する]**」をクリックします。

   ![publishworkflow](assets/publishworkflow.png)

次に、Brand Portalにログインして、公開済みのアセットがBrand Portalインターフェイスで使用可能かどうかを確認します。

![bp_landing_page](assets/bp_landing_page.png)
