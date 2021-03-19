---
title: デジタルアセットへの透かしの追加
description: 透かし処理機能を使用して、アセットにデジタル透かしを追加する方法について説明します。
contentOwner: AG
role: 営業者、管理者
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 31%

---


# デジタルアセットの透かし{#watermarking}

[!DNL Adobe Experience Manager Assets] アセットに電子透かしを追加できます。これにより、ユーザーはアセットの信頼性と著作権の所有権を検証できます。[!DNL Experience Manager Assets] では、PNG および JPEG ファイル上の透かしとしてテキストを使用できます。

アセットに透かしを適用するには、[!UICONTROL DAM Update Asset]ワークフローで透かしを追加します。

1. [!DNL Experience Manager]ユーザーインターフェイスにアクセスし、**[!UICONTROL ツール]**/**[!UICONTROL ワークフロー]**/**[!UICONTROL モデル]**&#x200B;に移動します。
1. **[!UICONTROL ワークフローモデル]**&#x200B;ページから、**[!UICONTROL DAM更新アセット]**&#x200B;ワークフローを選択し、**[!UICONTROL 編集]**&#x200B;をクリックします。

1. サイドパネルから、追加&#x200B;**[!UICONTROL 透かし]**&#x200B;ステップを[!UICONTROL DAM Update Asset]ワークフローにドラッグします。

   ![Watermarkstepをドラッグし、 [!UICONTROL 追加] DAM Update   Assetworkflowに追加します。](assets/add_watermark_step_aem_assets.png)

   *図： [!UICONTROL Watermarkstepをドラッグし、「] DAM Update  [!UICONTROL Assetworkflow」に追加し] ます。*

   >[!NOTE]
   >
   >[!UICONTROL 透かし追加]ステップを[!UICONTROL サムネールを処理]ステップの前の任意の場所に配置します。

1. 「**[!UICONTROL 透かしを追加]**」ステップを開いて、プロパティを表示します。
1. 「**[!UICONTROL 引数]**」タブで、各種フィールド（テキスト、フォントタイプ、サイズ、カラー、位置、向きなど）に有効な値を指定します。変更を確認するには、「**[!UICONTROL 完了]**」をクリックします。

   ![ における「透かしを追加」ステップの引数の指定[!DNL Assets]](assets/arguments_add_watermark_aem_assets.png)

   *図：の透かしの追加手順で引数を指定し [!DNL Assets]ます。*

1. **[!UICONTROL DAM Update Asset]**&#x200B;ワークフローを透かしの手順と共に保存します。
1. [!DNL Assets]ユーザーインターフェイスから、サンプルアセットをアップロードします。 透かしがフォントサイズやカラーなどと共に、上記手順で設定した位置に表示されます。

プログラム的に、または動的な情報を使用してPDFドキュメントに透かしを付けるには、[Experience Managerドキュメントサービス](/help/forms/using/overview-aem-document-services.md)オファーを使用することを検討してください。

## ヒントと制限事項 {#tips-limitations}

* テキストベースの透かしのみがサポートされます。 [!UICONTROL 透かしプロセス]の作成時に画像をアップロードできる場合でも、画像は透かしとして追加使用されません。
* 透かしの設定は、PNGファイルとJPEGファイルのみサポートされています。 その他のアセット形式は、透かしが埋め込まれていません。
