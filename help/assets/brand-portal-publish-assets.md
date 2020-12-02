---
title: Brand Portal へのアセットの公開
seo-title: Brand Portal へのアセットの公開
description: Brand Portalにアセットを公開および非公開する方法を説明します。
seo-description: Brand Portalにアセットを公開および非公開する方法を説明します。
uuid: 350beb85-c0fb-4a1c-8597-c03592c02d3d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: brand-portal
content-type: reference
discoiquuid: 39b8cf9b-afec-4c9a-8a5d-7fc87e643f26
docset: aem65
translation-type: tm+mt
source-git-commit: 4c00385984a0ac315a60c768cb517832ab4289b4
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 61%

---


# Brand Portal へのアセットの公開 {#publish-assets-to-brand-portal}

Adobe Experience Manager（AEM）Assets の管理者は、アセットやフォルダーを組織の AEM Assets Brand Portal インスタンスに公開（または公開ワークフローを未来の日時で設定）できます。ただし、最初に AEM Assets を Brand Portal と連携するように設定する必要があります。詳しくは [AEM Assets と Brand Portal の連携の設定](/help/assets/configure-aem-assets-with-brand-portal.md)を参照してください。

レプリケーションが正常に終了したら、アセット、フォルダー、コレクションを Brand Portal に公開することができます。アセットを Brand Portal に公開するには、次の手順を実行します。

>[!NOTE]
>
>AEM オーサーが過剰なリソースを占有しないように、できればピーク時を避け、時間をずらして公開することをお勧めします。

1. アセットコンソールから、公開するアセットまたはフォルダーを選択し、ツールバーの「**[!UICONTROL クイック公開]**」オプションをクリックします。

   または、Brand Portal に公開するアセットを選択します。

   ![publish2bp-2](assets/publish2bp.png)

1. アセットをBrand Portalに公開するには、次の2つのオプションを使用できます。
   * [アセットを直ちに公開](#publish-to-bp-now)
   * [アセットを後で公開](#publish-to-bp-now)

## アセットを今すぐ公開 {#publish-to-bp-now}

選択したアセットを Brand Portal に公開するには、次のいずれかを実行します。

* ツールバーで「**[!UICONTROL クイック公開]**」を選択します。次に、メニューから「**[!UICONTROL ブランドポータルに公開]**」を選択します。

* ツールバーで「**[!UICONTROL 公開を管理]**」を選択します。

   1. 次に、**[!UICONTROL アクション]**&#x200B;で「**[!UICONTROL ブランドポータルに公開]**」を選択し、**[!UICONTROL スケジュール]**&#x200B;で「**[!UICONTROL 今すぐ]**」を選択します。 「**[!UICONTROL 次へ]**」をクリックします。

   2. **[!UICONTROL スコープ]**&#x200B;内で、選択を確認し、「**[!UICONTROL ブランドポータルに発行]**」をクリックします。

アセットが Brand Portal への公開用のキューに入れられたことを示すメッセージが表示されます。Brand Portal のインターフェイスにログインして、公開されたアセットを確認します。

## アセットを後で公開 {#publish-to-bp-later}

アセットを Brand Portal に公開するスケジュールを後の日時に設定するには、次の手順を実行します。

1. 発行するアセット/フォルダを選択したら、上部のツールバーから「**[!UICONTROL パブリケーションを管理]**」を選択します。

1. **[!UICONTROL パブリケーションの管理]**&#x200B;ページで、**[!UICONTROL アクション]**&#x200B;から「**[!UICONTROL ブランドポータルに公開]**」を選択し、**[!UICONTROL スケジュール]**&#x200B;から「**[!UICONTROL 後で]**」を選択します。

   ![publishlaterbp-1](assets/publishlaterbp-1.png)

1. 「**[!UICONTROL アクティベート日]**」を選択して時刻を指定します。「**[!UICONTROL 次へ]**」をクリックします。

1. 「**アクティベート日**」を選択して時刻を指定します。「**次へ**」をクリックします。

1. 「**[!UICONTROL ワークフロー]**」で&#x200B;**[!UICONTROL ワークフロータイトル]**&#x200B;を指定します。「**[!UICONTROL 後で公開する]**」をクリックします。

   ![publishworkflow](assets/publishworkflow.png)

次に、Brand Portalにログインして、公開されたアセットがBrand Portalインターフェイスで使用できるかどうかを確認します。

![bp_landing_page](assets/bp_landing_page.png)

