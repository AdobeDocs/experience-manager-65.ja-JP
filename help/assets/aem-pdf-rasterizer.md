---
title: PDFラスタライザーを使用したレンディションの生成
description: Adobe PDF Rasterizerライブラリを使用して、高品質のサムネールとレンディションを生成します。
contentOwner: AG
role: Developer, Administrator
feature: 開発者ツール，レンディション
exl-id: 6f365d6b-3972-4885-8766-5889e24289f1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 43%

---

# PDF Rasterizer {#using-pdf-rasterizer}を使用

コンテンツを多用する大きなPDFまたはAIファイルを[!DNL Adobe Experience Manager Assets]にアップロードすると、デフォルトのライブラリで正確な出力が生成されない場合があります。 AdobeのPDF Rasterizerライブラリを使用すると、デフォルトライブラリの出力と比較して、より信頼性が高く正確な出力を生成できます。 Adobeは、次のシナリオでPDF Rasterizerライブラリを使用することをお勧めします。

次のようなファイルで PDF Rasterizer ライブラリを使用することをお勧めします。

* 大量のコンテンツを集中的に消費するAIファイルまたはPDFファイル。
* AIファイルおよびデフォルトで生成されないサムネール付きPDFファイル。
* Pantone Matching System（PMS）カラーを使用した AI ファイル.

PDF Rasterizer を使用して生成されたサムネールおよびプレビューは、何もしなくてもすぐに使用できる出力に比べて高品質です。そのため、デバイス全体で一貫した表示エクスペリエンスを得ることができます。Adobe PDF Rasterizer ライブラリはカラースペース変換をサポートしません。ソースファイルのカラースペースに関わらず、RGB として出力されます。

1. [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/product/assets/aem-assets-pdf-rasterizer-pkg)から、[!DNL Adobe Experience Manager]デプロイメントにPDF Rasterizerパッケージをインストールします。

   >[!NOTE]
   >
   >PDF Rasterizer ライブラリは、Windows と Linux のみで使用できます。

1. `https://[aem_server]:[port]/workflow`の[!DNL Assets]ワークフローコンソールにアクセスします。 [!UICONTROL DAMアセットの更新]ワークフローを開きます。

1. デフォルトの方法を使用してPDFファイルおよびAIファイルのサムネールおよびWebレンディションが生成されないようにするには、次の手順に従います。

   * **[!UICONTROL サムネールを処理]**&#x200B;の手順を開き、必要に応じて「**[!UICONTROL サムネール]**」タブの「**[!UICONTROL MIMEタイプをスキップ]**」フィールドに`application/pdf`または`application/postscript`を追加します。

   ![skip_mime_types-2](assets/skip_mime_types-2.png)

   * 「**[!UICONTROL Webに対応した画像]**」タブで、必要に応じて「**[!UICONTROL リストをスキップ]**」に`application/pdf`または`application/postscript`を追加します。

   ![画像形式のサムネール処理をスキップする設定](assets/web_enabled_imageskiplist.png)

1. **[!UICONTROL PDF/AI画像プレビューレンディションをラスタライズ]**&#x200B;ステップを開き、プレビュー画像レンディションのデフォルト生成をスキップするMIMEタイプを削除します。 例えば、MIMEタイプ`application/pdf`、`application/postscript`、または`application/illustrator`を&#x200B;**[!UICONTROL MIMEタイプ]**&#x200B;リストから削除します。

   ![process_arguments](assets/process_arguments.png)

1. 「**[!UICONTROL PDF Rasterizer Handler]**」ステップをサイドパネルから「**[!UICONTROL サムネールを処理]**」ステップの下にドラッグします。
1. **[!UICONTROL PDF Rasterizer Handler]**&#x200B;ステップに対して、次の引数を設定します。

   * MIMEタイプ：`application/pdf`または`application/postscript`
   * コマンド: `PDFRasterizer -d -s 1280 -t PNG -i ${file}`
   * 追加するサムネールのサイズ：319:319、140:100、48:48。必要に応じて、サムネールのカスタム設定を追加します。

   `PDFRasterizer` コマンドのコマンドライン引数には、以下のものがあります。

   * `-d`:テキスト、ベクトルアートワークおよび画像のスムーズなレンダリングを有効にするフラグ。高い画質の画像が作成されます。ただし、このパラメーターを指定すると、コマンドの実行速度が遅くなり、画像サイズも増大します。

   * `-s`:画像の最大サイズ（高さまたは幅）。これは各ページで DPI に変換されます。異なるサイズのページが混在している場合、ページごとに異なる比率で拡大縮小される場合があります。デフォルトは実際のページサイズです。

   * `-t`:出力画像のタイプ。有効なタイプは JPEG、PNG、GIF および BMP です。デフォルト値は JPEG です。

   * `-i`:入力PDFのパス。必須パラメーターです。

   * `-h`: ヘルプ


1. 中間レンディションを削除するには、「**[!UICONTROL 生成されたレンディションを削除]**」を選択します。
1. PDF RasterizerでWebレンディションを生成するには、「**[!UICONTROL Webレンディションを生成]**」を選択します。

   ![generate_web_renditions1](assets/generate_web_renditions1.png)

1. 「**[!UICONTROL Webに対応した画像]**」タブで設定を指定します。

   ![web_enabled_image1](assets/web_enabled_image1.png)

1. ワークフローを保存します。
1. PDF RasterizerでPDFライブラリを使用してPDFページを処理できるようにするには、[!UICONTROL ワークフロー]コンソールから&#x200B;**[!UICONTROL DAMプロセスのサブアセット]**&#x200B;モデルを開きます。
1. サイドパネルから、「**[!UICONTROL Web対応の画像レンディションを作成]**」ステップの下にある「PDF Rasterizer Handler」ステップをドラッグします。
1. **[!UICONTROL PDF Rasterizer Handler]**&#x200B;ステップに対して、次の引数を設定します。

   * MIMEタイプ：`application/pdf`または`application/postscript`
   * コマンド: `PDFRasterizer -d -s 1280 -t PNG -i ${file}`
   * サムネールサイズを追加：`319:319`、`140:100`、`48:48`。 必要に応じて、カスタムサムネール設定を追加します。

   `PDFRasterizer` コマンドのコマンドライン引数には、以下のものがあります。

   * `-d`:テキスト、ベクトルアートワークおよび画像のスムーズなレンダリングを有効にするフラグ。高い画質の画像が作成されます。ただし、このパラメーターを指定すると、コマンドの実行速度が遅くなり、画像サイズも増大します。

   * `-s`:画像の最大サイズ（高さまたは幅）。これは各ページで DPI に変換されます。異なるサイズのページが混在している場合、ページごとに異なる比率で拡大縮小される場合があります。デフォルトは実際のページサイズです。

   * `-t`:出力画像のタイプ。有効なタイプは JPEG、PNG、GIF および BMP です。デフォルト値は JPEG です。

   * `-i`:入力PDFのパス。必須パラメーターです。

   * `-h`: ヘルプ


1. 中間レンディションを削除するには、「**[!UICONTROL 生成されたレンディションを削除]**」を選択します。
1. PDF RasterizerでWebレンディションを生成するには、「**[!UICONTROL Webレンディションを生成]**」を選択します。

   ![generate_web_renditions](assets/generate_web_renditions.png)

1. 「**[!UICONTROL Webに対応した画像]**」タブで設定を指定します。

   ![web_enabled_image-1](assets/web_enabled_image-1.png)

1. ワークフローを保存します。
1. [!DNL Experience Manager Assets]にPDFファイルまたはAIファイルをアップロードします。 PDF Rasterizer により、ファイルのサムネールと Web レンディションが生成されます。
