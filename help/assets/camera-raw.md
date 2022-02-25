---
title: '"[!DNL Adobe Camera Raw] デジタルアセットの処理のサポート»'
description: 有効にする方法を説明します [!DNL Adobe Camera Raw] ～を支える [!DNL Adobe Experience Manager Assets]
contentOwner: AG
role: Admin
feature: Developer Tools
exl-id: 7159a908-4c36-42b4-bbb4-d7fb1be4ee1b
source-git-commit: e24316cb9495a552960ae0620e4198f10a08b691
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 29%

---

# 次を使用して画像を処理 [!DNL Adobe Camera Raw] {#camera-raw-support}

次の項目を有効にすると、 [!DNL Adobe Camera Raw] は、CR2、NEF、RAF などの生のファイル形式を処理し、画像をJPEG形式でレンダリングする機能をサポートします。 この機能は、 [!DNL Adobe Experience Manager Assets] の使用 [Camera Raw包装](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg) は、「ソフトウェア配布」から入手できます。

>[!NOTE]
>
>この機能は JPEG レンディションのみをサポートします。Windows 64 ビット、Mac OS、RHEL 7.x でサポートされています。

有効にするには [!DNL Camera Raw] ～を支える [!DNL Experience Manager Assets]を使用する場合は、次の手順に従います。

1. をダウンロードします。 [[!DNL Camera Raw] パッケージ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/aem-assets-cameraraw-pkg-1.4.8.zip) から [!DNL Software Distribution].
1. `https://[aem_server]:[port]/workflow` にアクセスします。を開きます。 **[!UICONTROL DAM アセットの更新]** ワークフロー。
1. を編集します。 **[!UICONTROL サムネールを処理]** 手順
1. で次の設定をおこないます。 **[!UICONTROL サムネール]** タブ：

   * **[!UICONTROL サムネール]**: `140:100:false, 48:48:false, 319:319:false`
   * **[!UICONTROL スキップ MIME タイプ]**: `skip:image/dng, skip:image/x-raw-(.*)`

   ![chlimage_1-128](assets/chlimage_1-334.png)

1. 内 **[!UICONTROL Web に対応した画像]** タブ、 **[!UICONTROL リストをスキップ]** フィールド、指定 `audio/mpeg, video/(.*), image/dng, image/x-raw-(.*)`.

   ![chlimage_1-129](assets/chlimage_1-335.png)

1. サイドパネルから、 **[!UICONTROL Camera Raw/DNG ハンドラー]** 下のステップ **[!UICONTROL サムネールを処理]** 手順
1. 内 **[!UICONTROL Camera Raw/DNG ハンドラー]** 手順を実行する場合は、 **[!UICONTROL 引数]** タブ：

   * **[!UICONTROL MIME タイプ]**: `image/dng` および `image/x-raw-(.*)`
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

これで、Camera Raw ファイルを Assets に読み込むことができます。Camera Rawパッケージをインストールし、必要なワークフローを設定した後、 **[!UICONTROL 画像調整]** オプションがサイドパネルのリストに表示されます。

![chlimage_1-131](assets/chlimage_1-337.png)

*図：サイドペインのオプション。*

![chlimage_1-132](assets/chlimage_1-338.png)

*図：「 」オプションを使用して、画像に軽量の編集を行います。*

編集内容を [!DNL Camera Raw] 画像、新しいレンディション `AdjustedPreview.jpg` が画像用に生成されます。 を除く他の画像タイプ [!DNL Camera Raw]を指定した場合、変更はすべてのレンディションに反映されます。

## ベストプラクティス、既知の問題、および制限 {#best-practices}

この機能には次の制限があります。

* この機能は JPEG レンディションのみをサポートします。これは、Windows 64 ビット、Mac OS および RHEL 7.x でサポートされます。
* メタデータの書き戻しは、RAW および DNG 形式ではサポートされていません。
* この [!DNL Camera Raw] ライブラリには、一度に処理できる合計ピクセル数に関する制限があります。 現在、ファイルの長辺で最大65000ピクセル、または最初に検出された条件に応じて 512 MP を処理できます。
