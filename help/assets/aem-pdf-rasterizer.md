---
title: PDFラスタライザを使用したレンディションの生成
description: この記事では、Adobe PDF Rasterizer ライブラリを使用して、高品質のサムネールとレンディションを生成する方法について説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: abc4821ec3720969bf1c2fb068744c07477aca46

---


# PDFラスタライザを使用 {#using-pdf-rasterizer}

サイズが大きくコンテンツが多い PDF や AI ファイルを Adobe Experience Manager（AEM）Assets にアップロードすると、デフォルトのライブラリで正確な出力が生成されない場合があります。そのような場合、Adobe PDF Rasterizer ライブラリでは、デフォルトライブラリの出力よりも信頼性が高く正確な出力を生成できます。

次のようなファイルで PDF Rasterizer ライブラリを使用することをお勧めします。

* サイズが大きくコンテンツが多い AI／PDF ファイル.
* サムネールがあらかじめ生成されていないAIファイルおよびPDFファイル。
* Pantone Matching System（PMS）カラーを使用した AI ファイル.

PDF Rasterizer を使用して生成されたサムネールおよびプレビューは、何もしなくてもすぐに使用できる出力に比べて高品質です。そのため、デバイス全体で一貫した表示エクスペリエンスを得ることができます。Adobe PDF Rasterizer ライブラリはカラースペース変換をサポートしません。ソースファイルのカラースペースに関わらず、RGB として出力されます。

1. Install the PDF Rasterizer package on your AEM deployment from [Package Share](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/product/assets/aem-assets-pdf-rasterizer-pkg).

   >[!NOTE]
   >
   >PDF Rasterizer ライブラリは、Windows と Linux のみで使用できます。

1. Access the AEM Assets workflow console at `https://[server]:[port]/workflow`. Open the [!UICONTROL DAM Update Asset] workflow page.

1. デフォルトの方法を使用して PDF および AI ファイルのサムネールおよび Web レンディションが生成されないようにするには、次の手順に従います。

   * Open the **[!UICONTROL Process Thumbnails]** step, and add `application/pdf` or `application/postscript` in the **[!UICONTROL Skip Mime Types]** field under the **[!UICONTROL Thumbnails]** tab as necessary.
   ![skip_mime_types-2](assets/skip_mime_types-2.png)

   * In the **[!UICONTROL Web Enabled Image]** tab, add `application/pdf` or `application/postscript` under **[!UICONTROL Skip List]** depending upon your requirements.
   ![画像形式のサムネール処理をスキップする設定](assets/web_enabled_imageskiplist.png)

1. Open the **[!UICONTROL Rasterize PDF/AI Image Preview Rendition]** step, and remove the MIME type for which you want to skip the default generation of preview image renditions. For example, remove the MIME type `application/pdf`, `application/postscript`, or `application/illustrator` from the **[!UICONTROL MIME Types]** list.

   ![process_arguments](assets/process_arguments.png)

1. 「**[!UICONTROL PDF Rasterizer Handler]**」ステップをサイドパネルから「**[!UICONTROL サムネールを処理]**」ステップの下にドラッグします。
1. **[!UICONTROL PDFラスタライザハンドラ手順に対して次の引数を設定します]** 。

   * MIMEタイプ：または `application/pdf``application/postscript`

   * コマンド: `PDFRasterizer -d -p 1 -s 1280 -t PNG -i ${file}`
   * 追加するサムネールのサイズ：319:319、140:100、48:48。必要に応じて、サムネールのカスタム設定を追加します。
   `PDFRasterizer` コマンドのコマンドライン引数には、以下のものがあります。

   * `-d`:テキスト、ベクトルアートワークおよび画像のスムーズなレンダリングを有効にするフラグ。 高い画質の画像が作成されます。ただし、このパラメーターを指定すると、コマンドの実行速度が遅くなり、画像サイズも増大します。

   * `-p`:ページ番号。 デフォルト値は、すべてのページです。「*」は、すべてのページを示します。

   * `-s`:画像の最大寸法（高さまたは幅）。 これは各ページで DPI に変換されます。異なるサイズのページが混在している場合、ページごとに異なる比率で拡大縮小される場合があります。デフォルトは実際のページサイズです。

   * `-t`:出力画像のタイプ。 有効なタイプは JPEG、PNG、GIF および BMP です。デフォルト値は JPEG です。

   * `-i`:入力PDFのパス。 必須パラメーターです。

   * `-h`: ヘルプ


1. 中間レンディションを削除するには、「**[!UICONTROL 生成されたレンディションを削除]**」を選択します。
1. PDF Rasterize で Web レンディションを生成するには、「**[!UICONTROL Web レンディションを生成]**」を選択します。

   ![generate_web_renditions1](assets/generate_web_renditions1.png)

1. Specify the settings in the **[!UICONTROL Web Enabled Image]** tab.

   ![web_enabled_image1](assets/web_enabled_image1.png)

1. ワークフローを保存します。
1. To enable PDF Rasterizer to process PDF pages with PDF libraries, open the **[!UICONTROL DAM Process Subasset]** model from the Workflow console.
1. From the side panel, drag the PDF Rasterizer Handler step under the **[!UICONTROL Create Web-Enabled Image Rendition]** step.
1. **[!UICONTROL PDFラスタライザハンドラ手順に対して次の引数を設定します]** 。

   * MIME Types:または `application/pdf``application/postscript`

   * コマンド: `PDFRasterizer -d -p 1 -s 1280 -t PNG -i ${file}`
   * 追加するサムネールのサイズ：319:319、140:100、48:48。必要に応じて、サムネールのカスタム設定を追加します。
   PDFRasterizer コマンドのコマンドライン引数には、以下のものがあります。

   * `-d`:テキスト、ベクトルアートワークおよび画像のスムーズなレンダリングを有効にするフラグ。 高い画質の画像が作成されます。ただし、このパラメーターを指定すると、コマンドの実行速度が遅くなり、画像サイズも増大します。

   * `-p`:ページ番号。 デフォルト値は、すべてのページです。`*` はすべてのページを表します。

   * `-s`:画像の最大寸法（高さまたは幅）。 これは各ページで DPI に変換されます。異なるサイズのページが混在している場合、ページごとに異なる比率で拡大縮小される場合があります。デフォルトは実際のページサイズです。

   * `-t`:出力画像のタイプ。 有効なタイプは JPEG、PNG、GIF および BMP です。デフォルト値は JPEG です。

   * `-i`:入力PDFのパス。 必須パラメーターです。

   * `-h`: ヘルプ


1. 中間レンディションを削除するには、「**[!UICONTROL 生成されたレンディションを削除]**」を選択します。
1. PDF Rasterize で Web レンディションを生成するには、「**[!UICONTROL Web レンディションを生成]**」を選択します。

   ![generate_web_renditions](assets/generate_web_renditions.png)

1. Specify the settings in the **[!UICONTROL Web Enabled Image]** tab.

   ![web_enabled_image-1](assets/web_enabled_image-1.png)

1. ワークフローを保存します。
1. PDFまたはAIファイルをAEM Assetsにアップロードします。 PDF Rasterizer により、ファイルのサムネールと Web レンディションが生成されます。
