---
title: Camera Raw サポート
description: Adobe Experience Manager AssetsでCamera Rawサポートを有効にする方法を説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: e71b87b12d45bf12f29af917fddebeddedb18056

---


# Camera Rawを使用した画像の処理のサポート {#camera-raw-support}

Camera Rawのサポートを有効にして、CR2、NEF、RAFなどのRAWファイル形式を処理し、画像をJPEG形式でレンダリングできます。 この機能は、パッケージ共有で使用できる [Camera Rawパッケージを使用して](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg) 、Adobe Experience Manager Assetsでサポートされます。

>[!NOTE]
>
>この機能は JPEG レンディションのみをサポートします。Windows 64ビット、Mac OS、RHEL 7.xでサポートされています。

Adobe Experience Manager AssetsでCamera Rawのサポートを有効にするには、次の手順に従います。

1. Download the [Camera Raw package](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg) from the Package Share.
1. アクセス `https://[aem_server]:[port]/workflow`. Open the **[!UICONTROL DAM Update Asset]** workflow.
1. Open the **[!UICONTROL Process Thumbnails]** step.
1. Provide the following configuration in the **[!UICONTROL Thumbnails]** tab:

   * **[!UICONTROL サムネール]**: `140:100:false, 48:48:false, 319:319:false`
   * **[!UICONTROL スキップ MIME タイプ]**: `skip:image/dng, skip:image/x-raw-(.*)`
   ![chlimage_1-128](assets/chlimage_1-334.png)

1. 「 **[!UICONTROL Web対応の画像]** 」タブの「リスト **[!UICONTROL をスキップ]** 」フィールドで `audio/mpeg, video/(.*), image/dng, image/x-raw-(.*)`、

   ![chlimage_1-129](assets/chlimage_1-335.png)

1. From the side panel, add the **[!UICONTROL Camera Raw/DNG Handler]** step below the **[!UICONTROL Thumbnail creation]** step.
1. In the **[!UICONTROL Camera Raw/DNG Handler]** step, add the following configuration in the **[!UICONTROL Arguments]** tab:

   * **[!UICONTROL Mime Types]**: `image/dng` および `image/x-raw-(.*)`
   * **[!UICONTROL コマンド]**:

      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.web.1280.1280.jpeg 1280 1280`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.319.319.jpeg 319 319`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.140.100.jpeg 140 100`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.48.48.jpeg 48 48`
   ![chlimage_1-130](assets/chlimage_1-336.png)

1. 「**[!UICONTROL 保存]**」をクリックします。

>[!NOTE]
>
>上記の設定が **[!UICONTROL Camera RAW および DNG 処理ステップによるサンプルの DAM 更新アセット]**&#x200B;設定と同じであることを確認してください。

これで、Camera Raw ファイルを AEM Assets に読み込むことができます。After you install the Camera RAW package and configure the required workflow, **[!UICONTROL Image Adjust]** option appears in the list of side panes.

![chlimage_1-131](assets/chlimage_1-337.png)

*図：サイドペインのオプション*

![chlimage_1-132](assets/chlimage_1-338.png)

*図：オプションを使用して、画像に軽量な編集を行います。*

Camera Raw 画像に対する編集を保存すると、その画像に対して、新しいレンディション「`AdjustedPreview.jpg`」が生成されます。Camera Raw 以外の画像タイプの場合は、変更内容がすべてのレンディションに反映されます。

## ベストプラクティス、既知の問題、および制限 {#best-practices}

この機能には次の制限があります。

* この機能は JPEG レンディションのみをサポートします。これは、Windows 64 ビット、Mac OS および RHEL 7.x でサポートされます。
* メタデータの書き戻しは、RAW および DNG 形式ではサポートされていません。
* Camera Raw ライブラリには、一度に処理できる合計ピクセルに関する制限があります。現在、ファイルの長辺で最大65000ピクセル、または最初に検出される条件に合わせて512 MPを処理できます。
