---
title: '[!DNL Adobe Camera Raw] サポート。'
description: ' [!DNL Adobe Experience Manager Assets]で [!DNL Adobe Camera Raw] サポートを有効にする方法を説明します。'
contentOwner: AG
role: Administrator
feature: 開発者ツール
exl-id: 7159a908-4c36-42b4-bbb4-d7fb1be4ee1b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 35%

---

# Camera Rawの{#camera-raw-support}を使用して画像を処理する

[!DNL Adobe Camera Raw]サポートを有効にして、CR2、NEF、RAFなどの生のファイル形式を処理し、画像をJPEG形式でレンダリングできます。 この機能は、ソフトウェア配布から入手可能な[Camera Rawパッケージ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg)を使用して[!DNL Adobe Experience Manager Assets]でサポートされます。

>[!NOTE]
>
>この機能は JPEG レンディションのみをサポートします。Windows 64ビット、Mac OS、およびRHEL 7.xでサポートされています。

[!DNL Experience Manager Assets]で[!DNL Camera Raw]サポートを有効にするには、次の手順に従います。

1. ソフトウェア配布から[Camera Rawパッケージ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg)をダウンロードします。
1. `https://[aem_server]:[port]/workflow` にアクセスします。**[!UICONTROL DAMアセットの更新]**&#x200B;ワークフローを開きます。
1. **[!UICONTROL サムネールを処理]**&#x200B;の手順を開きます。
1. 「**[!UICONTROL サムネール]**」タブで次の設定を指定します。

   * **[!UICONTROL サムネール]**:  `140:100:false, 48:48:false, 319:319:false`
   * **[!UICONTROL スキップ MIME タイプ]**: `skip:image/dng, skip:image/x-raw-(.*)`

   ![chlimage_1-128](assets/chlimage_1-334.png)

1. 「**[!UICONTROL Webに対応した画像]**」タブの「**[!UICONTROL リストをスキップ]**」フィールドで、`audio/mpeg, video/(.*), image/dng, image/x-raw-(.*)`と指定します。

   ![chlimage_1-129](assets/chlimage_1-335.png)

1. サイドパネルから、**[!UICONTROL Camera Raw/DNGハンドラー]**&#x200B;ステップを&#x200B;**[!UICONTROL サムネールの作成]**&#x200B;ステップの下に追加します。
1. **[!UICONTROL Camera Raw/DNGハンドラー]**&#x200B;の手順で、**[!UICONTROL 「引数]**」タブに次の設定を追加します。

   * **[!UICONTROL MIMEタイプ]**: `image/dng` および  `image/x-raw-(.*)`
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

これで、Camera Raw ファイルを Assets に読み込むことができます。Camera Rawパッケージをインストールし、必要なワークフローを設定すると、サイドパネルのリストに「**[!UICONTROL 画像調整]**」オプションが表示されます。

![chlimage_1-131](assets/chlimage_1-337.png)

*図：サイドペインのオプション。*

![chlimage_1-132](assets/chlimage_1-338.png)

*図：「 」オプションを使用して、画像に軽量な編集を行います。*

[!DNL Camera Raw]画像に編集内容を保存した後、その画像に対して新しいレンディション`AdjustedPreview.jpg`が生成されます。 [!DNL Camera Raw]を除く他の画像タイプの場合、変更はすべてのレンディションに反映されます。

## ベストプラクティス、既知の問題、および制限 {#best-practices}

この機能には次の制限があります。

* この機能は JPEG レンディションのみをサポートします。これは、Windows 64 ビット、Mac OS および RHEL 7.x でサポートされます。
* メタデータの書き戻しは、RAW および DNG 形式ではサポートされていません。
* [!DNL Camera Raw]ライブラリには、一度に処理できる合計ピクセル数に関する制限があります。 現在、ファイルの長辺に最大65000ピクセル、または最初に検出された条件に応じて512 MPで処理できます。
