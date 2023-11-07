---
title: ImageMagick をインストールして設定する
description: ImageMagick ソフトウェアの概要と、インストール方法、コマンドラインプロセスのステップの設定方法、ImageMagick を使用して画像の編集、組み立て、サムネール生成を行う方法を学習します。
contentOwner: AG
role: Admin
feature: Renditions,Developer Tools
exl-id: 6c149d31-1e64-4d29-a32a-58bd69e9fa98
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 64%

---

# [!DNL Experience Manager Assets] と連携するための ImageMagick のインストールと設定 {#install-and-configure-imagemagick-to-work-with-aem-assets}

ImageMagick はビットマップ画像を作成、編集、組み立てまたは変換するためのソフトウェアプラグインです。PNG、JPEG、JPEG-2000、GIF、TIFF、DPX、EXR、WebP、Postscript、PDF、SVG など、200 種類以上の多様な形式の画像を読み書きできます。ImageMagick を使用して、画像のサイズ変更、反転、ミラー、回転、変形、シアーおよび変換を行います。 また、ImageMagick を使用して、画像の色を調整したり、各種特殊効果を適用したり、テキスト、線、ポリゴン、楕円、曲線を描画したりすることもできます。

ImageMagick で画像を処理するには、コマンドラインから [!DNL Adobe Experience Manager] メディアハンドラーを使用します。ImageMagick を使用して様々なファイル形式を操作するには、 [Assets ファイル形式のベストプラクティス](/help/assets/assets-file-format-best-practices.md). サポートされるすべてのファイル形式については、 [Assets でサポートされる形式](/help/assets/assets-formats.md).

ImageMagick を使用して大きなファイルを処理するには、通常よりも大きなメモリ要件、IM ポリシーに必要な潜在的な変更、パフォーマンスへの全体的な影響を検討します。 メモリ要件は、解像度、ビット深度、カラープロファイル、ファイル形式など、様々な要因によって異なります。 ImageMagick を使用して非常に大きなファイルを処理する場合は、[!DNL Experience Manager] サーバーのベンチマークを適切に実行してください。いくつかの有用なリソースを最後に紹介します。

>[!NOTE]
>
>[!DNL Adobe Managed Services] で [!DNL Experience Manager]（AMS）を使用していて高解像度の PSD または PSB ファイルを多数処理する予定がある場合は、アドビカスタマーサポートに連絡してください。[!DNL Experience Manager] では、30000 x 23000ピクセルを超える高解像度の PSB ファイルを処理できない場合があります。

## ImageMagick のインストール {#installing-imagemagick}

様々なオペレーティングシステムで、複数のバージョンの ImageMagic インストールファイルを利用できます。 ご使用のオペレーティングシステムに適したバージョンを使用してください。

1. オペレーティングシステムに適した [ImageMagick インストールファイル](https://www.imagemagick.org/script/download.php)をダウンロードします。
1. [!DNL Experience Manager] サーバーをホスティングしているディスクに ImageMagick をインストールするには、インストールファイルを起動します。

1. path 環境変数を ImageMagick のインストールディレクトリに設定します。
1. インストールが成功したかどうかを確認するには、`identify -version` コマンドを実行します。

## コマンドラインの処理手順の設定 {#set-up-the-command-line-process-step}

特定の使用例に応じてコマンドラインプロセスのステップを設定できます。以下のステップを実行すると、JPEG 画像ファイルを [!DNL Experience Manager] の `/content/dam` に追加するたびに、反転画像とサムネール（140 x 100、48 x 48、319 x 319 および 1280 x 1280）が生成されます。

1. [!DNL Experience Manager] サーバーで、ワークフローコンソール（`https://[aem_server]:[port]/workflow`）に移動し、「**[!UICONTROL DAM アセットの更新]**」ワークフローモデルを開きます。
1. 「**[!UICONTROL DAM アセットの更新]**」ワークフローモデルから、「**[!UICONTROL EPS のサムネール （ImageMagick を使用）]**」ステップを開きます。
1. 「**[!UICONTROL 引数]**」タブで、「**[!UICONTROL MIME タイプ]**」リストに `image/jpeg` を追加します。

   ![mime_types_jpeg](assets/mime_types_jpeg.png)

1. 「**[!UICONTROL コマンド]**」ボックスに、次のコマンドを入力します。

   `convert ./${filename} -flip ./${basename}.flipped.jpg`

1. 「**[!UICONTROL 生成されたレンディションを削除]**」フラグと「**[!UICONTROL Web レンディションを生成]**」フラグを選択します。

   ![select_flags](assets/select_flags.png)

1. 「**[!UICONTROL Web に対応した画像]**」タブで、1280 x 1280 ピクセルというサイズでレンディションの詳細を指定します。さらに、**[!UICONTROL MIME タイプ]** ボックスで `image/jpeg` を指定します。

   ![Web に対応した画像](assets/web_enabled_image.png)

1. 「**[!UICONTROL OK]**」をクリックして、変更を保存します。

   >[!NOTE]
   >
   >The `convert` 特定の Windows バージョン（Windows SE など）では、コマンドを実行できない場合があります。これは、ネイティブの Windows SE と競合するためです `convert` Windows インストールに含まれるユーティリティ。 この場合は、ImageMagick ユーティリティの完全パスを指定します。 例えば、次のように指定します。
   >
   >
   >`"C:\Program Files\ImageMagick-6.8.9-Q16\convert.exe" -define jpeg:size=319x319 ./${filename} -thumbnail 319x319 cq5dam.thumbnail.319.319.png`

1. 「**[!UICONTROL サムネールを処理]**」ステップを開き、「**[!UICONTROL MIME タイプをスキップ]**」に MIME タイプ `image/jpeg` を追加します。

   ![skip_mime_types](assets/skip_mime_types.png)

1. 「**[!UICONTROL Web に対応した画像]**」タブで、「**[!UICONTROL リストをスキップ]**」に MIME タイプ `image/jpeg` を追加します。「**[!UICONTROL OK]**」をクリックして、変更を保存します。

   ![web_enabled](assets/web_enabled.png)

1. ワークフローを保存します。

1. 処理が適切であることを確認するには、[!DNL Assets] に JPG 画像をアップロードします。処理が完了したら、反転画像とレンディションが生成されているかどうかを確認します。

## セキュリティの脆弱性の軽減 {#mitigating-security-vulnerabilities}

ImageMagick を使用した画像の処理には、複数のセキュリティ脆弱性が関連しています。 例えば、ユーザーが送信した画像を処理すると、リモートコードが実行 (RCE) されるリスクが発生します。

さらに、様々な画像処理プラグインは、PHP の imagick、Ruby の rmagick と paperclip、nodejs の imagemagick など、ImageMagick ライブラリに依存します。

ImageMagick または影響を受けるライブラリを使用する場合、Adobeでは、次のタスクの少なくとも 1 つ（できれば両方）を実行して、既知の脆弱性を軽減することを推奨します。

1. 処理のために ImageMagick に送信する前に、すべての画像ファイルがサポートしている画像ファイルタイプに対応する、想定される[「マジックバイト」](https://en.wikipedia.org/wiki/List_of_file_signatures)で始まっていることを確認します。
1. ポリシーファイルを使用して、脆弱な ImageMagick コーダーを無効にします。ImageMagick のグルーバルポリシーは `/etc/ImageMagick` にあります。
