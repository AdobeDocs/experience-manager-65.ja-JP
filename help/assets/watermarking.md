---
title: デジタルアセットへの透かしの追加.
description: 透かし処理機能を使用して、アセットにデジタル透かしを追加する方法について説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5035d3457187f4d5fe5c2af255a1a886df7291b4
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 35%

---


# デジタルアセットの透かしの設定 {#watermarking}

[!DNL Adobe Experience Manager Assets] アセットに電子透かしを追加できます。これにより、ユーザーはアセットの信頼性と著作権の所有権を検証できます。 [!DNL Experience Manager Assets] では、PNG および JPEG ファイル上の透かしとしてテキストを使用できます。

To be able to apply watermark on assets, add the watermarking step in the [!UICONTROL DAM Update Asset] workflow.

1. ユーザーインターフェイスにアクセスし、 [!DNL Experience Manager] ツール **[!UICONTROL /]** ワークフロー **[!UICONTROL /]** モデルに移動します ****。
1. From the **[!UICONTROL Workflow Models]** page, select the **[!UICONTROL DAM Update Asset]** workflow and click **[!UICONTROL Edit]**.

1. From the side panel, drag the **[!UICONTROL Add Watermark]** step to the [!UICONTROL DAM Update Asset] workflow.

   ![[!UICONTROL 透かし] 手順をドラッグし、 [!UICONTROL DAM Update Asset] ワークフロー](assets/add_watermark_step_aem_assets.png)2に追加します。
   *図： 「[!UICONTROL 追加Watermark]」ステップをドラッグし、「[!UICONTROL DAM Update Asset]」ワークフローに追加します。*

   >[!NOTE]
   >
   >Place the [!UICONTROL Add Watermark] step anywhere before the [!UICONTROL Process Thumbnail] step.

1. 「**[!UICONTROL 透かしを追加]**」ステップを開いて、プロパティを表示します。
1. 「**[!UICONTROL 引数]**」タブで、各種フィールド（テキスト、フォントタイプ、サイズ、カラー、位置、向きなど）に有効な値を指定します。変更を確認するには、「 **[!UICONTROL 完了]**」をクリックします。

   ![Assets における「透かしを追加」ステップの引数の指定](assets/arguments_add_watermark_aem_assets.png)

   *図： の透かしの追加手順で引数を指定し[!DNL Assets]ます。*

1. Save the **[!UICONTROL DAM Update Asset]** workflow with the watermark step.
1. From the [!DNL Assets] user interface, upload a sample asset. 透かしがフォントサイズやカラーなどと共に、上記手順で設定した位置に表示されます。

プログラムによって、または動的なドキュメントを使用してPDFの透かしを埋め込むには、 [AEMドキュメントサービス](/help/forms/using/overview-aem-document-services.md) の機能を使用することを検討します。
