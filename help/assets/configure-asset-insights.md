---
title: アセットインサイトを設定して、解析を取得します。
description: ' [!DNL Adobe Experience Manager Assets]でアセットインサイトを設定します。'
contentOwner: AG
role: Architect, Administrator
feature: アセットインサイト，アセットレポート
exl-id: 67be0ae6-5939-40fe-bf8a-b8a2c2f68f15
source-git-commit: c07467feb96c25a4bac1916f88f04fdb37979ee1
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 47%

---

# アセットインサイトの設定 {#configure-asset-insights}

[!DNL Adobe Experience Manager Assets] では、サードパーティ Web サイトで使用されているデジタルアセットの使用状況データを [!DNL Adobe Analytics] から取得します。アセットインサイトでこのようなデータを取得して洞察を得るためには、まず、[!DNL Adobe Analytics] と連携するようにこの機能を設定します。この機能を使用するには、[!DNL Adobe Analytics]ライセンスを別途購入してください。 [!DNL Managed Services]のお客様は、[!DNL Experience Manager]にバンドルされている[!DNL Analytics]ライセンスを受け取ります。 [Managed Services製品の説明](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html)を参照してください。

>[!NOTE]
>
>インサイトのサポートおよび提供がおこなわれるのは、画像に対してのみです。

1. [!DNL Experience Manager] で&#x200B;**[!UICONTROL ツール]**／**[!UICONTROL アセット]**&#x200B;をクリックします。

   ![chlimage_1-72](assets/chlimage_1-210.png)

1. 「**[!UICONTROL インサイト設定]**」カードをクリックします。
1. ウィザードで、データセンターを選択し、会社名、ユーザー名、共有暗号鍵などの資格情報を指定します。

   ![Experience Managerでのアセットインサイト用にAdobe Analyticsを設定](assets/insights_config2.png)

   *図：でアセットインサイト [!DNL Adobe Analytics] を設定し [!DNL Experience Manager]ます。*

1. 「**[!UICONTROL 認証]**」をクリックします。
1. [!DNL Experience Manager] によって資格情報が認証されたら、**[!UICONTROL レポートスイート]**&#x200B;リストから、アセットインサイトでデータをフェッチする レポートスイートを選択します。[!DNL Adobe Analytics]「**[!UICONTROL 追加]**」をクリックします。
1. [!DNL Experience Manager]がレポートスイートを設定したら、**[!UICONTROL 完了]**&#x200B;をクリックします。

## ページトラッカー{#page-tracker}

[!DNL Adobe Analytics]アカウントを設定すると、ページトラッカーコードが生成されます。 サードパーティWebサイトで使用される[!DNL Experience Manager]アセットを追跡するためのアセットインサイトを有効にするには、Webサイトコードにページトラッカーコードを含めます。 [!DNL Experience Manager Assets]の[!UICONTROL ページトラッカー]ユーティリティを使用して、ページトラッカーコードを生成します。 ページトラッカーコードをサードパーティWebページに含める方法について詳しくは、[Use page tracker and embed code in web pages](/help/assets/use-page-tracker.md)を参照してください。

1. [!DNL Experience Manager] で&#x200B;**[!UICONTROL ツール]**／**[!UICONTROL アセット]**&#x200B;をクリックします。

   ![chlimage_1-73](assets/chlimage_1-214.png)

1. **[!UICONTROL ナビゲーション]**&#x200B;ページで、「**[!UICONTROL インサイトページトラッカー]**」カードをクリックします。
1. 「**[!UICONTROL ダウンロード]**」をクリックして、ページトラッカーコードをダウンロードします。
