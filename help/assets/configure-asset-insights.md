---
title: アセットインサイトを設定して分析を取得します。
description: ' [!DNL Adobe Experience Manager Assets]でアセットインサイトを設定します。'
contentOwner: AG
role: Architect, Admin
feature: アセットインサイト、アセットレポート
exl-id: 67be0ae6-5939-40fe-bf8a-b8a2c2f68f15
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 35%

---

# アセットインサイトの設定 {#configure-asset-insights}

[!DNL Adobe Experience Manager Assets] では、サードパーティ Web サイトで使用されているデジタルアセットの使用状況データを [!DNL Adobe Analytics] から取得します。アセットインサイトでこのデータを取得してインサイトを生成できるようにするには、まず[!DNL Adobe Analytics]と統合するように機能を設定します。 この機能をオンプレミスインストールで使用するには、[!DNL Adobe Analytics]ライセンスを別途購入してください。 [!DNL Managed Services]をご利用のお客様は、[!DNL Experience Manager]にバンドルされている[!DNL Analytics]ライセンスを受け取ります。 [Managed Services製品の説明](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html)を参照してください。

>[!NOTE]
>
>インサイトのサポートおよび提供がおこなわれるのは、画像に対してのみです。

1. [!DNL Experience Manager] で&#x200B;**[!UICONTROL ツール]**／**[!UICONTROL アセット]**&#x200B;をクリックします。

   ![chlimage_1-72](assets/chlimage_1-210.png)

1. 「**[!UICONTROL インサイト設定]**」カードをクリックします。
1. ウィザードで、データセンターを選択し、会社名、ユーザー名、共有暗号鍵などの資格情報を指定します。

   ![Experience Managerのアセットインサイト用Adobe Analyticsの設定](assets/insights_config2.png)

   *図：のアセッ [!DNL Adobe Analytics] トインサイト用にを設定し [!DNL Experience Manager]ます。*

1. 「**[!UICONTROL 認証]**」をクリックします。
1. [!DNL Experience Manager]が資格情報を認証した後、**[!UICONTROL レポートスイート]**&#x200B;リストから、アセットインサイトでデータを取得する[!DNL Adobe Analytics]レポートスイートを選択します。 「**[!UICONTROL 追加]**」をクリックします。
1. [!DNL Experience Manager] でレポートスイートが設定されたら、「**[!UICONTROL 完了]**」をタップします。

## ページトラッカー {#page-tracker}

[!DNL Adobe Analytics]アカウントを設定すると、ページトラッカーコードが生成されます。 アセットインサイトでサードパーティWebサイトで使用される[!DNL Experience Manager]アセットを追跡できるようにするには、Webサイトコードにページトラッカーコードを含めます。 [!DNL Experience Manager Assets]の[!UICONTROL ページトラッカー]ユーティリティを使用して、ページトラッカーコードを生成します。 サードパーティのWebページにページトラッカーコードを含める方法について詳しくは、[Webページでのページトラッカーと埋め込みコードの使用](/help/assets/use-page-tracker.md)を参照してください。

1. [!DNL Experience Manager] で&#x200B;**[!UICONTROL ツール]**／**[!UICONTROL アセット]**&#x200B;をクリックします。

   ![chlimage_1-73](assets/chlimage_1-214.png)

1. **[!UICONTROL ナビゲーション]**&#x200B;ページで、「**[!UICONTROL インサイトページトラッカー]**」カードをクリックします。
1. 「**[!UICONTROL ダウンロード]**」をクリックして、ページトラッカーコードをダウンロードします。
