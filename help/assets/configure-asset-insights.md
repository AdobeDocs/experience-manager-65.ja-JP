---
title: アセットインサイトを設定して分析を取得します。
description: ' [!DNL Adobe Experience Manager Assets] でアセットインサイトを設定します。'
contentOwner: AG
role: Architect, Admin
feature: Asset Insights,Asset Reports
exl-id: 67be0ae6-5939-40fe-bf8a-b8a2c2f68f15
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: ht
source-wordcount: '253'
ht-degree: 100%

---

# アセットインサイトの設定 {#configure-asset-insights}

[!DNL Adobe Experience Manager Assets] では、サードパーティ Web サイトで使用されているデジタルアセットの使用状況データを [!DNL Adobe Analytics] から取得します。アセットインサイトでこのようなデータを取得してインサイトを得るためには、まず、[!DNL Adobe Analytics] と統合するようにこの機能を設定します。オンプレミスのインストールでこの機能を使用するには、別途 [!DNL Adobe Analytics] ライセンスを購入します。[!DNL Managed Services] のお客様は、[!DNL Experience Manager] にバンドルされている [!DNL Analytics] ライセンスを受け取ります。詳しくは、[Managed Services 製品説明](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-experience-manager-managed-services.html)を参照してください。

>[!NOTE]
>
>インサイトのサポートおよび提供が行われるのは、画像に対してのみです。

1. [!DNL Experience Manager] で&#x200B;**[!UICONTROL ツール]**／**[!UICONTROL アセット]**&#x200B;をクリックします。

   ![chlimage_1-72](assets/chlimage_1-210.png)

1. 「**[!UICONTROL インサイト設定]**」カードをクリックします。
1. ウィザードで、データセンターを選択し、会社名、ユーザー名、共有暗号鍵などの資格情報を指定します。

   ![Experience Manager で Adobe Analytics をアセットインサイト用に設定](assets/insights_config2.png)

   *図：[!DNL Experience Manager] で [!DNL Adobe Analytics] をアセットインサイト用に設定*

1. 「**[!UICONTROL 認証]**」をクリックします。
1. [!DNL Experience Manager] によって認証情報が認証されたら、**[!UICONTROL レポートスイート]**&#x200B;リストから、アセットインサイトでデータをフェッチする [!DNL Adobe Analytics] レポートスイートを選択します。「**[!UICONTROL 追加]**」をクリックします。
1. [!DNL Experience Manager] でレポートスイートが設定されたら、「**[!UICONTROL 完了]**」をタップします。

## ページトラッカー {#page-tracker}

[!DNL Adobe Analytics] アカウントを設定すると、ページトラッカーコードが生成されます。サードパーティの web サイトで使用される [!DNL Experience Manager] アセットをアセットインサイトで追跡できるようにするには、web サイトコードにページトラッカーコードを組み込みます。[!DNL Experience Manager Assets] の[!UICONTROL ページトラッカー]ユーティリティを使用して、ページトラッカーコードを生成します。サードパーティの web ページにページトラッカーコードを組み込む方法について詳しくは、[Web ページでのページトラッカーと埋め込みコードの使用](/help/assets/use-page-tracker.md)を参照してください。

1. [!DNL Experience Manager] で&#x200B;**[!UICONTROL ツール]**／**[!UICONTROL アセット]**&#x200B;をクリックします。

   ![chlimage_1-73](assets/chlimage_1-214.png)

1. **[!UICONTROL ナビゲーション]**&#x200B;ページで、「**[!UICONTROL インサイトページトラッカー]**」カードをクリックします。
1. 「**[!UICONTROL ダウンロード]**」をクリックして、ページトラッカーコードをダウンロードします。
