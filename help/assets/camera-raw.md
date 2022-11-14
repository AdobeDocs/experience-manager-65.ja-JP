---
title: "[!DNL Adobe Camera Raw] のデジタルアセット処理サポート"
description: ' [!DNL Adobe Experience Manager Assets] で  [!DNL Adobe Camera Raw]  のサポートを有効にする方法を説明します'
contentOwner: AG
role: Admin
feature: Developer Tools
exl-id: 7159a908-4c36-42b4-bbb4-d7fb1be4ee1b
source-git-commit: e24316cb9495a552960ae0620e4198f10a08b691
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 100%

---

# [!DNL Adobe Camera Raw] を使用して画像を処理する {#camera-raw-support}

[!DNL Adobe Camera Raw] サポートを有効にすると、CR2、NEF、RAF などの RAW ファイル形式を処理し、画像を JPEG 形式でレンダリングできます。この機能は、ソフトウェア配布から入手できる [Camera Raw パッケージ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg)を使用して [!DNL Adobe Experience Manager Assets] でサポートされています。

>[!NOTE]
>
>この機能は JPEG レンディションのみをサポートします。これは、Windows 64 ビット、Mac OS および RHEL 7.x でサポートされます。

[!DNL Experience Manager Assets] で [!DNL Camera Raw] サポートを有効にするには、次の手順に従います。

1. [[!DNL Camera Raw]  パッケージ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/aem-assets-cameraraw-pkg-1.4.8.zip)を [!DNL Software Distribution] からダウンロードします。
1. `https://[aem_server]:[port]/workflow` にアクセスします。**[!UICONTROL DAM アセットの更新]**&#x200B;ワークフローを開きます。
1. **[!UICONTROL サムネールを処理]**&#x200B;手順を編集します。
1. 「**[!UICONTROL サムネール]**」タブで次の設定を入力します。

   * **[!UICONTROL サムネール]**：`140:100:false, 48:48:false, 319:319:false`
   * **[!UICONTROL スキップ MIME タイプ]**：`skip:image/dng, skip:image/x-raw-(.*)`

   ![chlimage_1-128](assets/chlimage_1-334.png)

1. 「**[!UICONTROL Web に対応した画像]**」タブの&#x200B;**[!UICONTROL リストをスキップ]**&#x200B;フィールドで、`audio/mpeg, video/(.*), image/dng, image/x-raw-(.*)` を指定します。

   ![chlimage_1-129](assets/chlimage_1-335.png)

1. サイドパネルから、**[!UICONTROL サムネールを処理]**&#x200B;ステップの下に **[!UICONTROL Camera Raw/DNG ハンドラー]**&#x200B;手順を追加します。
1. 「**[!UICONTROL Camera Raw/DNG ハンドラー]**」ステップの「**[!UICONTROL 引数]**」タブで、次の設定を入力します。

   * **[!UICONTROL MIME タイプ]**：`image/dng` および `image/x-raw-(.*)`
   * **[!UICONTROL コマンド]**：

      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.web.1280.1280.jpeg 1280 1280`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.319.319.jpeg 319 319`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.140.100.jpeg 140 100`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.48.48.jpeg 48 48`

   ![chlimage_1-130](assets/chlimage_1-336.png)

1. 「**[!UICONTROL 保存]**」をクリックします。

>[!NOTE]
>
>上記の設定が **[!UICONTROL Camera RAW および DNG 処理ステップによるサンプルの DAM 更新アセット]**&#x200B;設定と同じであることを確認してください。

これで、Camera Raw ファイルを Assets にインポートすることができます。Camera RAW パッケージをインストールして必要なワークフローを設定した後、パネルのリストに「**[!UICONTROL 画像調整]**」オプションが表示されます。

![chlimage_1-131](assets/chlimage_1-337.png)

*図：サイドペインのオプション。*

![chlimage_1-132](assets/chlimage_1-338.png)

*図：オプションを使用して、画像に軽量の編集をおこないます。*

[!DNL Camera Raw] 画像に対する編集を保存すると、その画像に対して、新しいレンディション「`AdjustedPreview.jpg`」が生成されます。[!DNL Camera Raw] 以外の画像タイプの場合は、変更内容がすべてのレンディションに反映されます。

## ベストプラクティス、既知の問題、および制限 {#best-practices}

この機能には次の制限があります。

* この機能は JPEG レンディションのみをサポートします。これは、Windows 64 ビット、Mac OS および RHEL 7.x でサポートされます。
* メタデータの書き戻しは、RAW および DNG 形式ではサポートされていません。
* [!DNL Camera Raw] ライブラリには、一度に処理できる合計ピクセルに関する制限があります。現在、最初に検出された条件に応じて、ファイルの長辺で最大 65000 ピクセルまたは 512 MP を処理できます。
