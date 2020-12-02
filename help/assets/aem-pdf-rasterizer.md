---
title: PDFラスタライザーを使用したレンディションの生成
description: ' [!DNL Adobe Experience Manager]のAdobe PDFラスタライザライブラリを使用して、高品質のサムネールとレンディションを生成します。'
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5069c2cd26e84866d72a61d36de085dadd556cdd
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 43%

---


# PDFラスタライザを使用{#using-pdf-rasterizer}

コンテンツを大量に消費する大きなPDFファイルまたはAIファイルを[!DNL Adobe Experience Manager Assets]にアップロードする場合、デフォルトの変換では正確な出力が生成されない場合があります。 AdobeのPDFラスタライザライブラリでは、初期設定のライブラリの出力と比較して、より信頼性の高い正確な出力を生成できます。 Adobeでは、次の場合にPDF Rasterizerライブラリを使用することをお勧めします。

* 大量のコンテンツが必要なAIファイルまたはPDFファイル。
* デフォルトでは生成されないサムネール付きのAIファイルおよびPDFファイル。
* Pantone Matching System（PMS）カラーを使用した AI ファイル.

PDF Rasterizer を使用して生成されたサムネールおよびプレビューは、何もしなくてもすぐに使用できる出力に比べて高品質です。そのため、デバイス全体で一貫した表示エクスペリエンスを得ることができます。Adobe PDF Rasterizer ライブラリはカラースペース変換をサポートしません。ソースファイルのカラースペースに関わらず、RGB として出力されます。

1. [ソフトウェアの配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/product/assets/aem-assets-pdf-rasterizer-pkg)から、[!DNL Adobe Experience Manager]デプロイメントにPDF Rasterizerパッケージをインストールします。

   >[!NOTE]
   >
   >PDF Rasterizer ライブラリは、Windows と Linux のみで使用できます。

1. `https://[aem_server]:[port]/workflow`の[!DNL Assets]ワークフローコンソールにアクセスします。 [!UICONTROL DAM Update Asset]ワークフローを開きます。

1. デフォルトの方法でPDFファイルおよびAIファイルのサムネールとWebレンディションが生成されないようにするには、次の手順に従います。

   * **[!UICONTROL サムネールを処理]**&#x200B;の手順を開き、必要に応じて、**[!UICONTROL サムネール]**&#x200B;タブの下の&#x200B;**[!UICONTROL Skip Mime Types]**&#x200B;フィールドに`application/pdf`または`application/postscript`を追加します。

   ![skip_mime_types-2](assets/skip_mime_types-2.png)

   * 「**[!UICONTROL Web対応リスト]**」タブで、必要に応じて「画像&#x200B;]**をスキップ」の下に`application/pdf`または`application/postscript`を追加します。**[!UICONTROL 

   ![画像形式のサムネール処理をスキップする設定](assets/web_enabled_imageskiplist.png)

1. **[!UICONTROL PDF/AI画像プレビューレンディションをラスタライズ]**&#x200B;の手順を開き、プレビュー画像レンディションのデフォルトの生成をスキップするMIMEタイプを削除します。 例えば、MIMEタイプ`application/pdf`、`application/postscript`、または`application/illustrator`を&#x200B;**[!UICONTROL MIMEタイプ]**&#x200B;リストから削除します。

   ![process_arguments](assets/process_arguments.png)

1. 「**[!UICONTROL PDF Rasterizer Handler]**」ステップをサイドパネルから「**[!UICONTROL サムネールを処理]**」ステップの下にドラッグします。
1. **[!UICONTROL PDFラスタライザーハンドラー]**&#x200B;の手順に対して次の引数を設定します。

   * MIME types:`application/pdf`または`application/postscript`
   * コマンド: `PDFRasterizer -d -p 1 -s 1280 -t PNG -i ${file}`
   * 追加するサムネールのサイズ：319:319、140:100、48:48。必要に応じて、サムネールのカスタム設定を追加します。

   `PDFRasterizer` コマンドのコマンドライン引数には、以下のものがあります。

   * `-d`:テキスト、ベクトルアートワークおよび画像のスムーズなレンダリングを有効にするフラグ。高い画質の画像が作成されます。ただし、このパラメーターを指定すると、コマンドの実行速度が遅くなり、画像サイズも増大します。

   * `-p`:ページ番号。デフォルト値は、すべてのページです。すべてのページを示すには、`*`を使用します。

   * `-s`:画像の最大寸法（高さまたは幅）これは各ページで DPI に変換されます。異なるサイズのページが混在している場合、ページごとに異なる比率で拡大縮小される場合があります。デフォルトは実際のページサイズです。

   * `-t`:出力画像の種類。有効なタイプは JPEG、PNG、GIF および BMP です。デフォルト値は JPEG です。

   * `-i`:入力PDFのパス。必須パラメーターです。

   * `-h`: ヘルプ


1. 中間レンディションを削除するには、「**[!UICONTROL 生成されたレンディションを削除]**」を選択します。

1. PDFラスタライザーでWebレンディションを生成するには、「**[!UICONTROL Webレンディションを生成]**」を選択します。

   ![generate_web_renditions1](assets/generate_web_renditions1.png)

1. 「**[!UICONTROL Web対応の画像]**」タブで設定を指定します。

   ![web_enabled_image1](assets/web_enabled_image1.png)

1. ワークフローを保存します。

1. PDFラスタライザーでPDFライブラリを使用してPDFページを処理できるようにするには、[!UICONTROL ワークフロー]コンソールから&#x200B;**[!UICONTROL DAM Process Subasset]**&#x200B;モデルを開きます。

1. サイドパネルから、**[!UICONTROL Web対応の画像レンディションを作成]**&#x200B;の手順の下にあるPDFラスタライザハンドラの手順をドラッグします。

1. **[!UICONTROL PDFラスタライザーハンドラー]**&#x200B;の手順に対して次の引数を設定します。

   * MIME types:`application/pdf`または`application/postscript`

   * コマンド: `PDFRasterizer -d -p 1 -s 1280 -t PNG -i ${file}`
   * 追加サムネールのサイズ：`319:319`、`140:100`、`48:48`。 必要に応じて、追加カスタムサムネールの設定を指定します。

   `PDFRasterizer` コマンドのコマンドライン引数には、以下のものがあります。

   * `-d`:テキスト、ベクトルアートワークおよび画像のスムーズなレンダリングを有効にするフラグ。高い画質の画像が作成されます。ただし、このパラメーターを指定すると、コマンドの実行速度が遅くなり、画像サイズも増大します。

   * `-p`:ページ番号。デフォルト値は、すべてのページです。`*` はすべてのページを表します。

   * `-s`:画像の最大寸法（高さまたは幅）これは各ページで DPI に変換されます。異なるサイズのページが混在している場合、ページごとに異なる比率で拡大縮小される場合があります。デフォルトは実際のページサイズです。

   * `-t`:出力画像の種類。有効なタイプは JPEG、PNG、GIF および BMP です。デフォルト値は JPEG です。

   * `-i`:入力PDFのパス。必須パラメーターです。

   * `-h`: ヘルプ


1. 中間レンディションを削除するには、「**[!UICONTROL 生成されたレンディションを削除]**」を選択します。
1. PDFラスタライザーでWebレンディションを生成するには、「**[!UICONTROL Webレンディションを生成]**」を選択します。

   ![generate_web_renditions](assets/generate_web_renditions.png)

1. 「**[!UICONTROL Web対応の画像]**」タブで設定を指定します。

   ![web_enabled_image-1](assets/web_enabled_image-1.png)

1. ワークフローを保存します。
1. PDFまたはAIファイルを[!DNL Experience Manager Assets]にアップロードします。 PDF Rasterizer により、ファイルのサムネールと Web レンディションが生成されます。
