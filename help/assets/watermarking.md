---
title: デジタルアセットへの透かしの追加.
description: 透かし処理機能を使用して、アセットにデジタル透かしを追加する方法について説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: c7d0bcbf39adfc7dfd01742651589efb72959603

---


# デジタルアセットの透かし {#watermarking}

Adobe Experience Manager (AEM)Assetsを使用すると、アセットに電子透かしを追加して、アセットの信頼性と著作権の所有権を確認できます。 AEM Assets では、PNG および JPEG ファイル上の透かしとしてテキストを使用できます。

To be able to apply watermark on assets, add the watermarking step in the [!UICONTROL DAM Update Asset] workflow.

1. AEMユーザーインターフェイスにアクセスし、ツール/ワ **[!UICONTROL ークフロ]** ー **[!UICONTROL /モデルに移]** 動します ****。
1. From the **[!UICONTROL Workflow Models]** page, select the **[!UICONTROL DAM Update Asset]** workflow and click **[!UICONTROL Edit]**.

1. From the side panel, drag the **[!UICONTROL Add Watermark]** step to the [!UICONTROL DAM Update Asset] workflow.

   ![透かしステ [!UICONTROL 追加ップをドラッグし] 、 [!UICONTROL DAM更新アセットのワークフロー]](assets/add_watermark_step_aem_assets.png)2に追加します。
   *図：透かしステッ[!UICONTROL 追加プをドラッグし]、[!UICONTROL DAM更新アセットのワークフローに追加しま]す*

   >[!NOTE]
   >
   >Place the [!UICONTROL Add Watermark] step anywhere before the [!UICONTROL Process Thumbnail] step.

1. 「**[!UICONTROL 透かしを追加]**」ステップを開いて、プロパティを表示します。
1. 「**[!UICONTROL 引数]**」タブで、各種フィールド（テキスト、フォントタイプ、サイズ、カラー、位置、向きなど）に有効な値を指定します。変更を確定するために、完了アイコンをタップまたはクリックします。

   ![Assets における「透かしを追加」ステップの引数の指定](assets/arguments_add_watermark_aem_assets.png)

   *図：アセットの透かしの追加手順の引数を指定します。*

1. Save the **[!UICONTROL DAM Update Asset]** workflow with the watermark step.
1. Assets ユーザーインターフェイスから、サンプルアセットをアップロードします。透かしがフォントサイズやカラーなどと共に、上記手順で設定した位置に表示されます。
