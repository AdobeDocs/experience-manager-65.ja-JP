---
title: アセットインサイトの設定
description: AEM Assetsでのアセットインサイトの設定を参照してください。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 44daaa61f7328e79fd4e11a503b0eef3ff9ffb56

---


# アセットインサイトの設定 {#configure-asset-insights}

Adobe Experience Manager（AEM）Assets は、サードパーティの Web サイトで使用される AEM アセットに関する使用状況データを Adobe Analytics からフェッチします。アセットインサイトでこのようなデータを取得して洞察を得るためには、最初に Adobe Analytics と統合するようにこの機能を設定します。

>[!NOTE]
>
>インサイトは画像に対してのみサポートおよび提供されます。

1. AEM で&#x200B;**[!UICONTROL ツール]**／**[!UICONTROL アセット]**&#x200B;をクリックします。

   ![chlimage_1-72](assets/chlimage_1-210.png)

1. 「**[!UICONTROL インサイト設定]**」カードをクリックします。
1. ウィザードで、データセンターを選択し、会社名、ユーザー名、共有暗号鍵などの資格情報を指定します。

   ![AEM のアセットインサイト用に Adobe Analytics を設定する](assets/insights_config2.png)

   *図：AEMでのアセットインサイト用のAdobe Analyticsの設定*

1. 「**[!UICONTROL 認証]**」をクリックまたはタップします。
1. AEM によって資格情報が認証されたら、**[!UICONTROL レポートスイート]**&#x200B;リストから、アセットインサイトでデータをフェッチする Adobe Analytics レポートスイートを選択します。「**[!UICONTROL 追加]**」をクリックします。
1. After AEM sets up your report suite, click/tap **[!UICONTROL Done]**.

## Page tracker {#page-tracker}

Adobe Analyticsアカウントを設定すると、ページトラッカーコードが生成されます。 サードパーティの Web サイトで使用される AEM アセットをアセットインサイトで追跡できるようにするには、Web サイトコードにトラッカーコードを組み込みます。AEM Assets のページトラッカーユーティリティを使用してページトラッカーコードを生成してください。For more information on how to include your Page Tracker code in third-party web pages, see [Use page tracker and embed code in web pages](/help/assets/touch-ui-using-page-tracker.md).

1. AEM で&#x200B;**[!UICONTROL ツール]**／**[!UICONTROL アセット]**&#x200B;をクリックします。

   ![chlimage_1-73](assets/chlimage_1-214.png)

1. **[!UICONTROL ナビゲーション]**&#x200B;ページで、「**[!UICONTROL インサイトページトラッカー]**」カードをクリックします。
1. Click **[!UICONTROL Download]** to download the page tracker code.
