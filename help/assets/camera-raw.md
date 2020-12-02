---
title: '[!DNL Adobe Camera Raw] サポート'
description: ' [!DNL Adobe Experience Manager Assets]で [!DNL Adobe Camera Raw] サポートを有効にする方法を学びます。'
contentOwner: AG
translation-type: tm+mt
source-git-commit: bccc937c1e1a349ab292a748c3c7b9d0c68b6199
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 35%

---


# &lt;a0Camera Raw/>を使用して画像を処理{#camera-raw-support}

[!DNL Adobe Camera Raw]サポートを有効にして、CR2、NEF、RAFなどの生のファイル形式を処理し、画像をJPEG形式でレンダリングできます。 この機能は、[!DNL Adobe Experience Manager Assets]で、Software Distributionの[Camera Rawパッケージ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg)を使用してサポートされます。

>[!NOTE]
>
>この機能は JPEG レンディションのみをサポートします。Windows 64ビット、Mac OS、およびRHEL 7.xでサポートされています。

[!DNL Experience Manager Assets]で[!DNL Camera Raw]サポートを有効にするには、次の手順に従います。

1. [パッケージCamera Raw](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg)をSoftware Distributionからダウンロードします。
1. `https://[aem_server]:[port]/workflow` にアクセスします。**[!UICONTROL DAM Update Asset]**&#x200B;ワークフローを開きます。
1. **[!UICONTROL サムネールを処理]**&#x200B;の手順を開きます。
1. 「**[!UICONTROL サムネール]**」タブで次の設定を指定します。

   * **[!UICONTROL サムネール]**:  `140:100:false, 48:48:false, 319:319:false`
   * **[!UICONTROL スキップ MIME タイプ]**: `skip:image/dng, skip:image/x-raw-(.*)`

   ![chlimage_1-128](assets/chlimage_1-334.png)

1. 「**[!UICONTROL Web対応のリスト]**」タブの「**[!UICONTROL 画像をスキップ]**」フィールドで、`audio/mpeg, video/(.*), image/dng, image/x-raw-(.*)`を指定します。

   ![chlimage_1-129](assets/chlimage_1-335.png)

1. サイドパネルから、**[!UICONTROL サムネールCamera Rawの作成]**&#x200B;の手順の下に&#x200B;**[!UICONTROL /DNGハンドラー]**&#x200B;の手順を追加します。
1. **[!UICONTROL Camera Raw/DNGハンドラー]**&#x200B;の手順で、**[!UICONTROL 「引数]**」タブに次の設定を追加します。

   * **[!UICONTROL MIMEタイプ]**: `image/dng` と  `image/x-raw-(.*)`
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

これで、Camera Raw ファイルを Assets に読み込むことができます。パッケージをインストールしCamera Rawて必要なワークフローを設定すると、サイドパネルのリストに「**[!UICONTROL 画像の調整]**」オプションが表示されます。

![chlimage_1-131](assets/chlimage_1-337.png)

*図：サイドペインのオプション。*

![chlimage_1-132](assets/chlimage_1-338.png)

*図：このオプションを使用して、画像に対して軽量な編集を行います。*

編集内容を[!DNL Camera Raw]画像に保存すると、その画像に対して新しいレンディション`AdjustedPreview.jpg`が生成されます。 [!DNL Camera Raw]以外の他の画像タイプでは、変更はすべてのレンディションに反映されます。

## ベストプラクティス、既知の問題、および制限 {#best-practices}

この機能には次の制限があります。

* この機能は JPEG レンディションのみをサポートします。これは、Windows 64 ビット、Mac OS および RHEL 7.x でサポートされます。
* メタデータの書き戻しは、RAW および DNG 形式ではサポートされていません。
* [!DNL Camera Raw]ライブラリには、一度に処理できる合計ピクセル数に関する制限があります。 現在、ファイルの長辺で最大65,000ピクセル、または最初に検出される条件に合わせて512 MPで処理できます。
