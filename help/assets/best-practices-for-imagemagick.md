---
title: AEM Assets と連携するための ImageMagick のインストールと設定
description: ImageMagick ソフトウェアの概要と、インストール方法、コマンドラインプロセスのステップの設定方法、ImageMagick を使用して画像の編集、組み立て、サムネール生成をおこなう方法を学習します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 31234518537ca4a0b7ff36e8d52a3b7b1b8fe4f7

---


# AEM Assets と連携するための ImageMagick のインストールと設定{#install-and-configure-imagemagick-to-work-with-aem-assets}

ImageMagickは、ビットマップ画像の作成、編集、構成または変換を行うソフトウェアプラグインです。 PNG、JPEG、JPEG-2000、GIF、TIFF、DPX、EXR、WebP、Postscript、PDF、SVGなど、様々な形式（200以上）の画像の読み取りと書き込みが可能です。 ImageMagick は、画像のサイズ変更、反転、ミラー、回転、変形、剪断および変換をおこなう場合に使用します。ImageMagick を使用して、画像の色を調整したり、各種特殊効果を適用したりすることもできます。また、テキスト、直線、多角形、楕円および曲線を描画することもできます。

ImageMagick で画像を処理するには、コマンドラインから Adobe Experience Manager（AEM）メディアハンドラーを使用します。ImageMagick を使用して様々なファイル形式を取り扱うには、[Assets のファイル形式に関するベストプラクティス](/help/assets/assets-file-format-best-practices.md)を参照してください。すべてのサポートされるファイル形式については、[Assets でサポートされるファイル形式](/help/assets/assets-formats.md)を参照してください。

ImageMagick を使用して大きなファイルを処理する場合は、必要なメモリが通常より多くなること、IM ポリシーの変更が必要になる可能性があること、パフォーマンスへの全体的な影響を考慮してください。メモリ要件は、解像度、ビット深度、カラープロファイル、ファイル形式などの様々な要因によって異なります。ImageMagick を使用して非常に大きなファイルを処理する場合は、AEM サーバーのベンチマークを適切に実行してください。いくつかの有用なリソースを最後に紹介します。

>[!NOTE]
>
>AEM on Adobe Managed Services(AMS)を使用している場合は、高解像度のPSDまたはPSBファイルを多数処理する予定の場合は、アドビカスタマーケアにお問い合わせください。 3000 x 23000ピクセルを超える高解像度のPSBファイルは、Experience Managerでは処理されない場合があります。

## ImageMagick のインストール {#installing-imagemagick}

各種オペレーティングシステム向けに、様々なバージョンの ImageMagick インストールファイルが用意されています。オペレーティングシステムに適したバージョンを使用してください。

1. Download the appropriate [ImageMagick installation files](https://www.imagemagick.org/script/download.php) for your operating system.
1. AEM サーバーをホスティングしているディスクに ImageMagick をインストールするには、インストールファイルを起動します。

1. path 環境変数を ImageMagick のインストールディレクトリに設定します。
1. インストールが成功したかどうかを確認するには、`identify -version` コマンドを実行します。

## コマンドラインプロセスのステップの設定 {#set-up-the-command-line-process-step}

特定の使用例に応じてコマンドラインプロセスのステップを設定できます。Perform these steps to generate a flipped image and thumbnails (140x100, 48x48, 319x319, and 1280x1280) each time you add a JPEG image file to `/content/dam` on the AEM server:

1. On the AEM server, go to the Workflow console (`https://[aem_server]:[port]/workflow`) and open the **[!UICONTROL DAM Update Asset]** workflow model.
1. **[!UICONTROL DAM Update Assetワークフローモデルから]** 、 **[!UICONTROL EPSサムネール(]** powered by ImageMagick)の手順を開きます。
1. In the **[!UICONTROL Arguments tab]**, add `image/jpeg` to the **[!UICONTROL Mime Types]** list.

   ![mime_types_jpeg](assets/mime_types_jpeg.png)

1. 「**[!UICONTROL コマンド]**」ボックスに、次のコマンドを入力します。

   `convert ./${filename} -flip ./${basename}.flipped.jpg`

1. Select the **[!UICONTROL Delete Generated Rendition]** and **[!UICONTROL Generate Web Rendition]** flags.

   ![select_flags](assets/select_flags.png)

1. 「**[!UICONTROL Web に対応した画像]**」タブで、1280 x 1280 ピクセルというサイズでレンディションの詳細を指定します。さらに、「Mimetype」ボッ `image/jpeg` クスでを **[!UICONTROL 指定し]** ます。

   ![web_enabled_image](assets/web_enabled_image.png)

1. 「**[!UICONTROL OK]**」をクリックして、変更を保存します。

   >[!NOTE]
   >
   >The `convert` command may not run with certain Windows versions (for example Windows SE), because it conflicts with the native `convert` utility that is part of Windows installation. このような場合は、ImageMagick ユーティリティの完全パスを指定します。例えば、以下のように指定します。
   >
   >
   >`"C:\Program Files\ImageMagick-6.8.9-Q16\convert.exe" -define jpeg:size=319x319 ./${filename} -thumbnail 319x319 cq5dam.thumbnail.319.319.png`

1. Open the **[!UICONTROL Process Thumbnails]** step, and add the MIME type `image/jpeg` under **[!UICONTROL Skip Mime Types]**.

   ![skip_mime_types](assets/skip_mime_types.png)

1. In the **[!UICONTROL Web Enabled Image]** tab, add the MIME type `image/jpeg` under the **[!UICONTROL Skip List]**. 「**[!UICONTROL OK]**」をクリックして、変更を保存します。

   ![web_enabled](assets/web_enabled.png)

1. ワークフローを保存します。
1. ImageMagick が画像を正しく処理できるかどうかを確認するには、JPG 画像を AEM Assets にアップロードします。その画像の反転画像とレンディションが生成されるかどうかを確認します。

## セキュリティの脆弱性の緩和 {#mitigating-security-vulnerabilities}

ImageMagick を使用した画像の処理に関連して、セキュリティの脆弱性が複数存在します。例えば、ユーザーが送信した画像の処理は、リモートコード実行（RCE）のリスクを伴います。

さらに、PHP の imagick、Ruby の rmagick と paperclip、nodejs の imagemagick など様々な画像処理プラグインが、ImageMagick ライブラリに依存しています。

ImageMagick または影響を受けるライブラリを使用する場合は、以下のタスクのどちらか（できれば両方）を実行して、既知の脆弱性を緩和することをお勧めします。

1. Verify that all image files begin with the expected [&quot;magic bytes&quot;](https://en.wikipedia.org/wiki/List_of_file_signatures) corresponding to the image file types you support before sending them to ImageMagick for processing.
1. ポリシーファイルを使用して、脆弱なImageMagickコーダーを無効にします。 The global policy for ImageMagick is found at `/etc/ImageMagick`.
