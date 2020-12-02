---
title: サポートされているファイル形式と MIME タイプ
description: ' [!DNL Assets] and [!DNL Dynamic Media] でサポートされるファイル形式とMIMEタイプ、および各形式でサポートされる機能。'
contentOwner: AG
translation-type: tm+mt
source-git-commit: eaff176bf3ffc197607b8eb39b15c1e945927f8e
workflow-type: tm+mt
source-wordcount: '1639'
ht-degree: 58%

---


# [!DNL Adobe Experience Manager Assets] {#assets-supported-formats}でサポートされている形式

[!DNL Experience Manager Assets] は幅広いファイル形式をサポートしており、各機能は異なる MIME タイプに様々なサポートを提供しています。[!DNL Assets]を他の標準準拠のデジタル資産管理(DAM)ソリューションやデスクトップソフトウェアと統合するには、Adobeの[!DNL Extensible Metadata Platform] (XMP)を使用します。

凡例を使用して、サポートレベルについて理解します。

| サポートレベル | 説明 |
| :-----------: | ------------------------------ |
| ✓ | サポート対象 |
| * | アドオン機能により対応 |
| - | 適用なし |

## [!DNL Experience Manager] {#supported-raster-image-formats}でサポートされているラスターイメージ形式

[!DNL Assets]でサポートされているラスターイメージ形式は次のとおりです。

| 形式 | ストレージ | メタデータの管理 | メタデータ抽出 | サムネールの生成 | 編集 | メタデータの書き戻し | インサイト |
| ------------ | :------: | :-----------------: | :-----------------: | :------------------: | :------: | :----------------: | :------: |
| PNG | kid | kid | kid | kid | kid | kid | kid |
| GIF | kid | kid | kid | kid | kid | - | kid |
| TIFF | kid | kid | kid | kid | - | kid | kid |
| JPEG | kid | kid | kid | kid | kid | kid | kid |
| BMP | kid | kid | kid | kid | kid | - | kid |
| PNM | kid | kid | - | - | - | - | kid |
| PGM | kid | kid | - | - | - | - | kid |
| PBM | kid | kid | - | - | - | - | kid |
| PPM | kid | kid | - | - | - | - | kid |
| PSD ‡ | kid | kid | kid | kid | - | - | kid |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | kid | kid | kid | kid | - | kid | - |
| PICT | - | - | - | - | - | - | kid |
| PSB | kid | kid | kid | kid | - | - | - |

‡ 結合された画像は PSD ファイルから抽出されます。この画像は Adobe Photoshop によって生成され、PSD ファイルに含まれます。設定によって、結合された画像は実際の画像である場合とそうでない場合があります。

[!DNL Dynamic Media]でサポートされているラスターイメージ形式は次のとおりです。

| 形式 | アップロード<br>（入力形式） | <br>画像<br>プリセット<br>を作成（出力形式） | プレビュー<br>動的<br>レンディション | <br>動的<br>レンディションを配信 | <br>動的<br>レンディションをダウンロード |
|---|:---:|:---:|:---:|:---:|:---:|
| PNG | kid | kid | kid | kid | kid |
| GIF | kid | kid | kid | kid | kid |
| TIFF | kid | kid | kid | kid | kid |
| JPEG | kid | kid | kid | kid | kid |
| BMP | kid | - | - | - | - |
| PSD ` | kid | - | - | - | - |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | kid | kid | kid | kid | kid |
| PICT | kid | - | - | - | - |

‡ 結合された画像は PSD ファイルから抽出されます。この画像は Adobe Photoshop によって生成され、PSD ファイルに含まれます。設定によって、結合された画像は実際の画像である場合とそうでない場合があります。

上記の情報に加えて、以下を考慮してください。

* EPS ファイルのサポートは画像のラスタライズにのみ適用されます。例えば、EPS ベクター画像のサムネールの生成はデフォルトではサポートされません。サポートを追加するには、[ImageMagick](best-practices-for-imagemagick.md) を設定してください。サードパーティのツールを統合して追加機能を有効にする方法については、[コマンドラインベースのメディアハンドラー](media-handlers.md#command-line-based-media-handler)を参照してください。

* メタデータの書き戻しは、PSBファイル形式が`NComm`ハンドラに追加されたときに機能します。

* [!DNL Dynamic Media]を使用してEPSファイルの動的レンディションをプレビューおよび生成するには、[Adobe Illustrator(AI)、Postscript(EPS)、PDFファイル形式を参照してください。](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* EPS ファイルの場合、メタデータの書き戻しは、PostScript Document Structuring Convention（PS-Adobe）バージョン 3.0 以降でサポートされています。

## サポートされる3D形式{#support-3d-formats}

次の 3D 形式のリストがサポートされています。

[Dynamic Media での 3D アセット操作](/help/assets/assets-3d.md)も参照してください。

| 形式 | ストレージ | バージョン管理 | ワークフロー | 公開 | アクセス制御 | サムネールプレビュー | 3D プレビュー | Dynamic Media の配信 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DN | kid | kid | kid |  | kid | kid | - | - |
| gLB | kid | kid | kid | kid | kid | - | kid | kid |
| gLTF | kid | kid | kid |  | kid | - | kid | - |
| OBJ | kid | kid | kid | kid | kid | - | kid | kid |
| STL | kid | kid | kid | kid | kid | - | kid | kid |
| USDz | kid | kid | kid | kid | kid | - | - | kid |

## ダイナミックメディア{#unsupported-image-formats-dynamic-media}でサポートされていないラスターイメージ形式

次のリストでは、ダイナミックメディアでサポートされていない&#x200B;**&#x200B;のラスターイメージファイル形式のサブタイプについて説明します。

[ダイナミックメディア用にサポートされていないファイル形式の検出](https://helpx.adobe.com/experience-manager/kb/detect-unsupported-assets-for-dynamic-media.html)も参照してください。

* 100 MB を超える IDAT チャンクサイズを持つ PNG ファイル。
* PSB ファイル。
* CMYK、RGB、グレースケール、ビットマップ以外のカラースペースを持つ PSD ファイルはサポートされません。DuoTone、Lab、インデックス化カラースペースはサポートされません。
* 16 を超えるビット深度を持つ PSD ファイル。
* 浮動小数点データを持つ TIFF ファイル。
* Lab カラースペースを持つ TIFF ファイル。

<!-- Topic commented out for now as of March 31, 2020. The topic may still need adjustment so it can be published live, or it may be moved into a KB article instead. Just waiting on feedback in CQDOC-15657. - Rick
## Unsupported raster image formats in Dynamic Media (#unsupported-image-formats-dynamic-media)

The following table describes the sub-types of raster image formats that are *not* supported in Dynamic Media. The table also describes suggested methods you can use to detect such files.

| Format | What is unsupported? | Suggested detection method |
|---|---|---|
| JPEG  | Files where the initial three bytes is incorrect. | To identify a JPEF file, its initial three bytes must be `ff d8 ff`. If they are anything else, then it is not classified as a JPEG.<br>&bull; There is no software tool that can help with this issue.<br>&bull; A small C++/java program which reads the initial three bytes of a file should be able to detect these types of files.<br>&bull; It may be better to track the source of such files and look at the tool generating the file. |
| PNG |  Files that have an IDAT chunk size greater than 100 MB. | You can detect this issue using [libpng](http://www.libpng.org/pub/png/libpng.html) in C++. |
| PSB |  | Use exiftool if the file type is PSB.<br>Example in an ExifTool log:<br>1. File type: `PSB` |
| PSD | Files with a color space other than CMYK, RGB, Grayscale, or Bitmap are not supported.<br>DuoTone, Lab, and Indexed color spaces are not supported. | Use ExifTool if Color mode is Duotone.<br>Example in an ExifTool log:<br>1. Color mode: `Duotone` |
|  | Files with abrupt endings. | Adobe is unable to detect this condition. Also, such files cannot be opened with Adobe PhotoShop. Adobe suggests you examine the tool that was used to create such a file and troubleshoot at the source. |
|  | Files that have a bit depth greater than 16. | Use ExifTool if the bit depth is greater than 16.<br>Example in an ExifTool log:<br>1. Bit depth: `32` |
|  | File that have Lab color space. | Use exiftool if the color mode is Lab.<br>Example in an ExifTool log:<br>1. Color mode: `Lab` |
| TIFF | Files that have floating point data. That is, a TIFF file with 32-bit depth is not supported. | Use ExifTool if the MIME type is `image/tiff` and the SampleFormat has `Float` in its value. Example in an ExifTool log:<br>1. MIME type: `image/tiff`<br>Sample format: `Float #`<br>2. MIME type: `image/tiff`<br>Sample format: `Float; Float; Float; Float` |
|  | Files that have Lab color space. | Use ExifTool if the color mode is Lab.<br>Example in an ExifTool log:<br>1. Color mode: `Lab` |
-->

## サポートされている PDF Rasterizer ライブラリ {#supported-pdf-rasterizer-library}

Adobe PDFラスタライザライブラリは、大量のコンテンツを大量に消費する[!DNL Adobe Illustrator]ファイルやPDFファイルに対して、高品質のサムネールとプレビューを生成します。 次のようなファイルで PDF Rasterizer ライブラリを使用することをお勧めします。

* 処理にリソースを大量に消費する、コンテンツを集中的に使用するAI/PDFファイル。
* AI／PDF ファイル。デフォルトではサムネールは生成されません。
* Pantone Matching System（PMS）カラーを使用した AI ファイル.

詳しくは、[PDFラスタライザの使用](aem-pdf-rasterizer.md)を参照してください。

## サポートされる画像トランスコードライブラリ{#supported-image-transcoding-library}

Adobeイメージングトランスコーディングライブラリは、エンコーディング、トランスコード、リサンプリング、サイズ変更など、主要な画像処理機能を実行する画像処理ソリューションです。

画像トランスコーディングライブラリは、JPG／JPEG、PNG（8 ビットおよび 16 ビット）、GIF、BMP、TIFF／圧縮 TIFF（32 ビット TIFF ファイルおよび PTIFF ファイルを除く）、ICO、および ICN MIME タイプをサポートします。

[イメージングトランスコーディングライブラリ](imaging-transcoding-library.md)を参照してください。

## サポートされるCamera Raw {#supported-camera-raw}

[!DNL Adobe Camera Raw]ライブラリは[!DNL Assets]に生の画像を取り込むことを可能にします。 [Camera Rawサポート](camera-raw.md)を参照してください。

## サポートされる[!DNL Assets]ドキュメント形式{#supported-document-formats}

アセット管理機能でサポートされるドキュメント形式は次のとおりです。

| 形式 | ストレージ | [メタデータの管理](metadata.md) | フルテキスト<br>抽出 | [メタデータ抽出](metadata.md) | サムネール<br>の生成 | [サブアセットの抽出](managing-linked-subassets.md) | [メタデータの書き戻し](xmp-writeback.md) | [Connected Assets](use-assets-across-connected-assets-instances.md) |
|---|---|---|---|---|---|---|---|---|
| [AI](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | kid | kid | - | kid | kid | kid | kid | - |
| DOC | kid | kid | kid | kid | - | - | - | kid |
| DOCX | kid | kid | kid | kid | - | - | - | kid |
| ODT | kid | kid | kid | - | - | - | - | kid |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | kid | kid | kid | kid | kid | kid | kid | kid |
| HTML | kid | kid | kid | - | - | - | - | kid |
| RTF | kid | kid | kid | - | - | - | - | kid |
| TXT | kid | kid | kid | - | - | - | - | kid |
| XLS | kid | kid | kid | - | - | - | - | kid |
| XLSX | kid | kid | kid | kid | - | - | - | kid |
| ODS | kid | kid | kid | - | - | - | - | - |
| PPT | kid | kid | kid | kid | kid | kid | - | kid |
| PPTX | kid | kid | kid | kid | kid | kid | - | kid |
| ODP | kid | kid | kid | - | - | - | - | - |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | kid | kid | - | kid | kid | kid | kid | - |
| PS | kid | kid | - | - | - | - | - | - |
| QXP | kid | kid | - | - | - | - | - | - |
| EPUB | kid | kid | - | kid | kid | - | - | - |

## ダイナミックメディアでサポートされているドキュメント形式{#supported-document-formats-dynamic-media}

| 形式 | アップロード<br>（入力形式） | <br>画像<br>プリセット<br>を作成（出力形式） | プレビュー<br>動的<br>レンディション | <br>動的<br>レンディションを配信 | <br>動的<br>レンディションをダウンロード |
|---|:---:|:---:|:---:|:---:|:---:|
| [愛](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | kid | - | - | - | - |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | kid | kid | kid | kid | kid |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | kid | - | - | - | - |

上記の機能に加えて、次のことを考慮してください。

* PDF ファイルの動的レンディションの生成に Dynamic Media を使用するには、[Adobe Illustrator（AI）、Postscript（EPS）および PDF ファイル形式](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)を参照してください。

* AI ファイルの動的レンディションのプレビューと生成に Dynamic Media を使用するには、[Adobe Illustrator（AI）、Postscript（EPS）および PDF ファイル形式](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)を参照してください。

* ダイナミックメディアを使用してINDDファイルのダイナミックレンディションを生成するには、[InDesign(INDD)ファイル形式](../assets/managing-image-presets.md#indesign-indd-file-format)を参照してください。

## サポートされるマルチメディア形式 {#supported-multimedia-formats}

|  | ストレージ | メタデータの管理 | メタデータ抽出 | サムネールの生成 | FFmpeg トランスコーディング |
|:---|:---:|:---:|:---:|:---:|:---:|
| AAC | kid | kid | - | - | * |
| MIDI | kid | kid | - | - | * |
| 3GP | kid | kid | - | - | * |
| MP3 | kid | kid | kid | - | * |
| MPG | kid | kid | - | - | * |
| OGA | kid | kid | - | - | * |
| OGG | kid | kid | - | - | * |
| RA | kid | kid | - | - | * |
| WAV | kid | kid | - | - | * |
| WMA | kid | kid | - | - | * |
| DVI | kid | kid | - | * | * |
| FLV | kid | kid | - | * | * |
| M4V | kid | kid | - | * | * |
| MPEG | kid | kid | - | * | * |
| OGV | kid | kid | - | * | * |
| MOV | kid | kid | - | * | * |
| WMV | kid | kid | - | * | * |
| SWF | kid | kid | - | - | - |

## {#supported-input-video-formats-for-dynamic-media-transcoding}のトランスコード用にダイナミックメディアでサポートされる入力ビデオ形式

| ビデオファイル拡張子 | コンテナ | 推奨されるビデオコーデック | サポートされないビデオコーデック |
|---|---|---|---|
| MP4 | MPEG-4 | H264/AVC（すべてのプロファイル） | - |
| MOV、QT | Apple QuickTime | H264/AVC、Apple ProRes422 &amp; HQ、Sony XDCAM、Sony DVCAM、HDV、Panasonic DVCPro、Apple DV（DV25）、Apple PhotoJPEG、Sorenson、Avid DNxHD、Avid AVR | Apple Intermediate、Apple Animation |
| FLV、F4V | Adobe Flash | H264/AVC、Flix VP6、H263、Sorenson | SWF（ベクターアニメーションファイル） |
| WMV | Windows Media 9 | WMV3（v9）、WMV2（v8）、WMV1（v7）、GoToMeeting（G2M2、G2M3、G2M4） | Microsoft Screen（MSS2）、Microsoft Photo Story（WVP2） |
| MPG、VOB、M2V、MP2 | MPEG-2 | MPEG-2 | - |
| M4V | Apple iTunes | H264/AVC | - |
| AVI | A/V Interleave | XVID、DIVX、HDV、MiniDV（DV25）、Techsmith Camtasia、Huffyuv、Fraps、Panasonic DVCPro | Indeo3（IV30）、MJPEG、Microsoft Video 1（MS-CRAM） |
| WebM | WebM | Google VP8 | - |
| OGV、OGG | Ogg | Theora、VP3、Dirac | - |
| MXF | MXF | Sony XDCAM、MPEG-2、MPEG-4、Panasonic DVCPro | - |
| MTS | AVCHD | H264/AVC | - |
| MKV | Matroska | H264/AVC | - |
| R3D、RM | Red Raw Video | MJPEG 2000 | - |
| RAM、RM | RealVideo | サポート対象外 | Real G2（RV20）、Real 8（RV30）、Real 10（RV40） |
| FLAC | Native Flac | Free lossless audio codec | - |
| MJ2 | Motion JPEG2000 | Motion JPEG 2000 codec | - |

## サポートされるアーカイブ形式 {#supported-archive-formats}

サポートされるアーカイブ形式と一般的な DAM ワークフローの適用性については、次の表で説明します。

| 形式 | ストレージ | バージョン管理 | ワークフロー | 公開 | アクセス制御 | Dynamic Media の配信 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| TGZ | kid | kid | kid | kid | kid | - |
| JAR | kid | kid | kid | kid | kid | - |
| RAR | kid | kid | kid | kid | kid | - |
| TAR | kid | kid | kid | kid | kid | - |
| ZIP | kid | kid | kid | kid | kid | kid |

## その他のサポートされる形式 {#other-supported-formats}

いくつかの特定のファイル形式に対する通常のDAM機能の適用について、以下に説明します。

| 形式 | ストレージ | バージョン管理 | ワークフロー | 公開 | アクセス制御 | Dynamic Media の配信 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| SVG | kid | kid | kid | kid | kid | - |
| CSS | kid | kid | kid | kid | kid | kid |
| VTT | kid | kid | kid | kid | kid | kid |
| XML | kid | kid | kid | kid | kid | kid |
| JavaScript（独自の配信ドメインで設定する場合） | - | - | - | - | - | kid |

>[!NOTE]
>
>JavaScriptファイルのアップロードと配布は、安全である場合とそうでない場合があります。 必要に応じて、オーバーレイを使用して、ユーザーがJSファイルをアップロードできないようにすることができます。

## サポートされる MIME タイプ {#supported-mime-types}

デフォルトでは、[!DNL Experience Manager]はファイル拡張子を使用してファイルの種類を検出します。 [!DNL Experience Manager] は、ファイルの内容からそれを検出できます。後者の場合は、[!DNL Experience Manager]Webコンソールの[!UICONTROL Day CQ DAM MIME Type Service]で、「コンテンツ]からMIMEを検出」オプションを選択します。[!UICONTROL 

サポートされるMIMEタイプのリストは、CRXDE Lite`/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`で入手できます。

| ファイル拡張子 | MIME タイプ／インターネットメディアタイプ | デフォルトの jobParam 値 | 許可される jobParam 値 |
|---|---|---|---|
| 画像 | image/s7asset | `usmAmount=1.75&usmRadius=0.2`<br>`&usmThreshold=2&usmMonochrome=0&` | デフォルトの jobParam は、すべての画像の MIME タイプのアセットに適用されます。<ul><li>[knockoutBackgroundOptions](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-knockout-background-options.html)</li><li>[manualCropOptions](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-manual-crop-options.html)</li><li>[autoColorCropOptions](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-auto-color-crop-options.html)</li><li>[autoTransparentCropOptions](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-auto-transparent-crop-options.html)</li><li>[colorManagementOptions](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-color-management-options.html)</li><li>[autoSetCreationOptions](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-auto-set-creation-options.html)</li><li>[emailSetting](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/sting-constants/r-email-settings.html)</li><li>[xmpKeywords](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-xmp-keywords.html)</li><li>[unsharpMaskOptions](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-unsharp-mask-options.html)</li></ul> |
| 3G2 | video/3gpp2 |  | [ExcludeMasterVideoFromAVS](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| 3GP | video/3gpp |  | [ExcludeMasterVideoFromAVS](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| AAC | audio/x-aac |  |  |
| AFM | application/x-font-type1 |  |  |
| AI | application/postscript | `aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-post-script-options.html)</li><li> [illustratorOptions](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-illustrator-options.html)</li></ul> |
| AIFF | audio/x-aiff |  |  |
| AVI | video/x-msvideo |  | [ExcludeMasterVideoFromAVS](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| BMP | image/bmp |  |  |
| CSS | text/css |  |  |
| DOC | application/msword |  |  |
| EPS | <ul><li>application/postscript</li><li>application/eps</li><li>application/x-eps</li><li>image/eps</li><li>image/x-eps</li></ul> |  |  |
| F4V | video/x-f4v |  | ExcludeMasterVideoFromAVS |
| FLA | application/x-shockwave-flash |  |  |
| FLV | video/x-flv |  | [ExcludeMasterVideoFromAVS](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| FPX | image/vnd.fpx |  |  |
| GIF | image/gif |  |  |
| ICC | application/vnd.iccprofile |  |  |
| ICM | application/vnd.iccprofile |  |  |
| INDD | application/x-indesign |  |  |
| JPEG | image/jpeg |  |  |
| JPG | image/jpeg |  |  |
| M2V | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| M4V | video/x-m4v |  | [ExcludeMasterVideoFromAVS](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MOV | video/quicktime |  | [ExcludeMasterVideoFromAVS](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MP3 | audio/mpeg |  |  |
| MP4 | video/mp4 |  | [ExcludeMasterVideoFromAVS](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MPEG | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MPG | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MTS | model/vnd.mts |  |  |
| OGV | video/ogg |  | [ExcludeMasterVideoFromAVS](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| OTF | application/x-font-otf |  |  |
| PDF | application/pdf | `pdfprocess=Rasterize&resolution=150`<br>`&colorspace=Auto&pdfbrochure=false`<br>`&keywords=false&links=false` | [pdfOptions](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-pdf-options.html) |
| PFB | application/x-font-type1 |  |  |
| PFM | application/x-font-type1 |  |  |
| PICT | image/x-pict |  |  |
| PNG | image/png |  |  |
| PPT | application/vnd.ms-powerpoint |  |  |
| PS | application/postscript | `psprocess=Rasterize&psresolution=150`<br>`&pscolorspace=Auto&psalpha=false`<br>`&psextractsearchwords=false`<br>`&aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-post-script-options.html)</li><li>[illustratorOptions](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-illustrator-options.html)</li></ul> |
| PSD | image/vnd.adobe.photoshop | `process=None&layerNaming=Layername`<br>`&anchor=Center&createTemplate=false`<br>`&extractText=false&extendLayers=false` | <ul><li>[photoshopOptions](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-photoshop-options.html)</li><li>[photoshopLayerOptions](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-photoshop-layer-options.html)</li></ul> |
| RTF | application/rtf |  |  |
| SVG | image/svg+xml |  |  |
| SWF | application/x-shockwave-flash |  |  |
| TAR | application/x-tar |  |  |
| TIF / TIFF | image/tiff |  |  |
| TTC | application/x-font-ttf |  |  |
| TTF | application/x-font-ttf |  |  |
| VOB | video/dvd |  | [ExcludeMasterVideoFromAVS](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| VTT | text/vtt |  |  |
| WAV | audio/x-wav |  |  |
| WEBM | video/webm |  | [ExcludeMasterVideoFromAVS](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| WMA | audio/x-ms-wma |  |  |
| WMV | video/x-ms-wmv |  | [ExcludeMasterVideoFromAVS](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| XLS | application/vnd.ms-excel |  |  |
| ZIP | application/zip |  |  |

>[!MORELIKETHIS]
>
>* [MIMEタイプベースのアセットおよびDynamic Media Classicアップロードジョブパラメーターのサポートを有効にします](/help/sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support)。
>* [アップロードジョブのパラメーターのサポートに対して、MIMEタイプベースの設定を行います](config-dynamic.md)。

