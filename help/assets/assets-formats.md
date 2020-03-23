---
title: Assets でサポートされるファイル形式
description: AEM Assets でサポートされているファイル形式と、各形式でサポートされている機能のリスト。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 8431275c0e4de408e1ebafafafa94dcfae3c1127

---


# Assets でサポートされるファイル形式 {#assets-supported-formats}

AEM Assets は幅広いファイル形式をサポートしており、各機能は異なる MIME タイプに様々なサポートを提供しています。

AEM Assets を他の標準準拠のデジタルアセット管理（DAM）ソリューションおよびデスクトップソフトウェアと統合するには、アドビの Extensible Metadata Platform（XMP）を使用します。

凡例を使用して、サポートレベルについて理解します。

| サポートレベル | 説明 |
|:---:|---|
| ✓ | 対応 |
| * | アドオン機能により対応 |
| - | 適用なし |

## Supported Raster image formats {#supported-raster-image-formats}

アセット管理機能でサポートされるラスターイメージ形式は、次のとおりです。

| 形式 | ストレージ | メタデータの管理 | メタデータの抽出 | サムネールの生成 | インタラクティブ編集 | メタデータの書き戻し | インサイト |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ |  | ✓ |
| TIFF | ✓ | ✓ | ✓ | ✓ |  | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| BMP | ✓ | ✓ | ✓ | ✓ | ✓ |  | ✓ |
| PNM | ✓ | ✓ |  |  |  |  | ✓ |
| PGM | ✓ | ✓ |  |  |  |  | ✓ |
| PBM | ✓ | ✓ |  |  |  |  | ✓ |
| PPM | ✓ | ✓ |  |  |  |  | ✓ |
| PSD **¹** | ✓ | ✓ | ✓ | ✓ |  |  | ✓ |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ |  | ✓ |  |
| PICT |  |  |  |  |  |  | ✓ |
| PSB | ✓ | ✓ | ✓ | ✓ |  |  |  |

**§** PSDファイルから結合画像が抽出されます。 この画像は Adobe Photoshop によって生成され、PSD ファイルに含まれます。設定によって、結合された画像は実際の画像である場合とそうでない場合があります。

ダイナミックメディア機能でサポートされるラスターイメージ形式は、次のとおりです。

| 形式 | Upload<br> (Input format) | Create<br> image<br> preset<br> (Output format) | Preview<br> dynamic<br> rendition | Deliver<br> dynamic<br> rendition | Download<br> dynamic<br> rendition |
|---|:---:|:---:|:---:|:---:|:---:|
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ |
| BMP | ✓ |  |  |  |  |
| PSD **¹** | ✓ |  |  |  |  |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ |
| PICT | ✓ |  |  |  |  |

**§** PSDファイルから結合画像が抽出されます。 この画像は Adobe Photoshop によって生成され、PSD ファイルに含まれます。設定によって、結合された画像は実際の画像である場合とそうでない場合があります。

上記の情報に加えて、以下を考慮してください。

* EPS ファイルのサポートは画像のラスタライズにのみ適用されます。例えば、EPS ベクター画像のサムネールの生成はデフォルトではサポートされません。サポートを追加するには、[ImageMagick](best-practices-for-imagemagick.md) を設定してください。サードパーティのツールを統合して追加機能を有効にする方法については、コマンドラインベースのメ [ディアハンドラを参照してくださ](media-handlers.md#command-line-based-media-handler)い。

* Metadata writeback works for PSB file format when it is added to the `NComm` handler.

* EPS ファイルの動的レンディションのプレビューと生成に Dynamic Media を使用するには、[Adobe Illustrator（AI）、Postscript（EPS）および PDF ファイル形式](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)を参照してください。

* EPS ファイルの場合、メタデータの書き戻しは、PostScript Document Structuring Convention（PS-Adobe）バージョン 3.0 以降でサポートされています。

## サポートされている PDF Rasterizer ライブラリ {#supported-pdf-rasterizer-library}

Adobe PDF Rasterizer ライブラリは、サイズが大きくコンテンツが多い Adobe Illustrator ファイルおよび PDF ファイルの高品質のサムネールとプレビューを生成します。次のようなファイルで PDF Rasterizer ライブラリを使用することをお勧めします。

* 処理にリソースを大量に消費する、コンテンツを大量に消費するAI/PDFファイル。
* AI／PDF ファイル。デフォルトではサムネールは生成されません。
* Pantone Matching System（PMS）カラーを使用した AI ファイル.

See [Using PDF Rasterizer](aem-pdf-rasterizer.md).

## Supported Image Transcoding library {#supported-image-transcoding-library}

Adobe Imaging Transcodingライブラリは、エンコーディング、トランスコード、リサンプリング、サイズ変更など、主要な画像処理機能を実行する画像処理ソリューションです。

画像トランスコーディングライブラリは、JPG／JPEG、PNG（8 ビットおよび 16 ビット）、GIF、BMP、TIFF／圧縮 TIFF（32 ビット TIFF ファイルおよび PTIFF ファイルを除く）、ICO、および ICN MIME タイプをサポートします。

See [Imaging Transcoding Library](imaging-transcoding-library.md).

## Supported camera raw {#supported-camera-raw}

Adobe Camera Raw ライブラリを使用すると、AEM Assets が Raw 画像を取り込むことができます。See [Camera Raw support](camera-raw.md).

## サポートされるドキュメント形式 {#supported-document-formats}

アセット管理機能でサポートされるドキュメント形式は次のとおりです。

| 形式 | ストレージ | Metadata<br> management | Metadata<br> extraction | Thumbnail<br> generation | Interactive<br> editing | Metadata<br> writeback | [インサイト](touch-ui-asset-insights.md) | [Connected Assets](use-assets-across-connected-assets-instances.md) |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| [AI](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ |  | ✓ | ✓ | ✓ | ✓ |  |
| DOC | ✓ | ✓ | ✓ | ✓ |  |  |  | ✓ |
| DOCX | ✓ | ✓ | ✓ | ✓ |  |  |  | ✓ |
| ODT | ✓ | ✓ | ✓ |  |  |  |  | ✓ |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| HTML | ✓ | ✓ | ✓ |  |  |  |  | ✓ |
| RTF | ✓ | ✓ | ✓ |  |  |  |  | ✓ |
| TXT | ✓ | ✓ | ✓ |  |  |  |  | ✓ |
| XLS | ✓ | ✓ | ✓ |  |  |  |  | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ |  |  |  | ✓ |
| ODS | ✓ | ✓ | ✓ |  |  |  |  |  |
| PPT | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |  | ✓ |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |  | ✓ |
| ODP | ✓ | ✓ | ✓ |  |  |  |  |  |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | ✓ | ✓ |  | ✓ | ✓ | ✓ | ✓ |  |
| PS | ✓ | ✓ |  |  |  |  |  |  |
| QXP | ✓ | ✓ |  |  |  |  |  |  |
| EPUB | ✓ | ✓ |  | ✓ | ✓ |  |  |  |

ダイナミックメディア機能でサポートされるドキュメント形式は次のとおりです。

| 形式 | Upload<br> (Input format) | Create<br> image<br> preset<br> (Output format) | Preview<br> dynamic<br> rendition | Deliver<br> dynamic<br> rendition | Download<br> dynamic<br> rendition |
|---|:---:|:---:|:---:|:---:|:---:|
| [AI](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ |  |  |  |  |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | ✓ |  |  |  |  |

上記の機能に加えて、次のことを考慮してください。

* PDF ファイルの動的レンディションの生成に Dynamic Media を使用するには、[Adobe Illustrator（AI）、Postscript（EPS）および PDF ファイル形式](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)を参照してください。

* AI ファイルの動的レンディションのプレビューと生成に Dynamic Media を使用するには、[Adobe Illustrator（AI）、Postscript（EPS）および PDF ファイル形式](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)を参照してください。

* To use Dynamic Media to generate dynamic renditions for INDD files, see [InDesign (INDD) file format](../assets/managing-image-presets.md#indesign-indd-file-format).

## サポートされるマルチメディア形式 {#supported-multimedia-formats}

|  | ストレージ | メタデータの管理 | メタデータの抽出 | サムネールの生成 | FFMPEG トランスコーディング |
|:---|:---:|:---:|:---:|:---:|:---:|
| AAC | ✓ | ✓ |  | - | * |
| MIDI | ✓ | ✓ |  | - | * |
| 3GP | ✓ | ✓ |  | - | * |
| MP3 | ✓ | ✓ | ✓ | - | * |
| MPG | ✓ | ✓ |  | - | * |
| OGA | ✓ | ✓ |  | - | * |
| OGG | ✓ | ✓ |  | - | * |
| RA | ✓ | ✓ |  | - | * |
| WAV | ✓ | ✓ |  | - | * |
| WMA | ✓ | ✓ |  | - | * |
| DVI | ✓ | ✓ |  | * | * |
| FLV | ✓ | ✓ |  | * | * |
| M4V | ✓ | ✓ |  | * | * |
| MPEG | ✓ | ✓ |  | * | * |
| OGV | ✓ | ✓ |  | * | * |
| MOV | ✓ | ✓ |  | * | * |
| WMV | ✓ | ✓ |  | * | * |
| SWF | ✓ | ✓ |  |  |  |

## Supported input video formats for Dynamic Media Transcoding {#supported-input-video-formats-for-dynamic-media-transcoding}

| ビデオファイルの拡張子 | コンテナ | 推奨されるビデオコーデック | サポートされないビデオコーデック |
|---|---|---|---|
| MP4 | MPEG-4 | H264/AVC（すべてのプロファイル） |  |
| MOV、QT | Apple QuickTime | H264/AVC、Apple ProRes422 &amp; HQ、Sony XDCAM、Sony DVCAM、HDV、Panasonic DVCPro、Apple DV（DV25）、Apple PhotoJPEG、Sorenson、Avid DNxHD、Avid AVR | Apple Intermediate、Apple Animation |
| FLV、F4V | Adobe Flash | H264/AVC、Flix VP6、H263、Sorenson | SWF（ベクターアニメーションファイル） |
| WMV | Windows Media 9 | WMV3（v9）、WMV2（v8）、WMV1（v7）、GoToMeeting（G2M2、G2M3、G2M4） | Microsoft Screen（MSS2）、Microsoft Photo Story（WVP2） |
| MPG、VOB、M2V、MP2 | MPEG-2 | MPEG-2 |  |
| M4V | Apple iTunes | H264/AVC |  |
| AVI | A/V Interleave | XVID、DIVX、HDV、MiniDV（DV25）、Techsmith Camtasia、Huffyuv、Fraps、Panasonic DVCPro | Indeo3（IV30）、MJPEG、Microsoft Video 1（MS-CRAM） |
| WebM | WebM | Google VP8 |  |
| OGV、OGG | Ogg | Theora、VP3、Dirac |  |
| MXF | MXF | Sony XDCAM、MPEG-2、MPEG-4、Panasonic DVCPro |  |
| MTS | AVCHD | H264/AVC |  |
| MKV | Matroska | H264/AVC |  |
| R3D、RM | Red Raw Video | MJPEG 2000 |  |
| RAM、RM | RealVideo | 未サポート | Real G2（RV20）、Real 8（RV30）、Real 10（RV40） |
| FLAC | Native Flac | Free lossless audio codec |  |
| MJ2 | Motion JPEG2000 | Motion JPEG 2000 codec |  |

## サポートされるアーカイブ形式 {#supported-archive-formats}

サポートされるアーカイブ形式と一般的な DAM ワークフローの適用性については、次の表で説明します。

| 形式 | ストレージ | バージョン管理 | ワークフロー | 公開 | アクセス制御 | Dynamic Media の配信 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| TGZ | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| JAR | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| RAR | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| TAR | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| ZIP | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |

## その他のサポートされる形式 {#other-supported-formats}

他のいくつかのファイル形式に対する一般的な DAM ワークフローの適用性については、以下の表で説明します。ダイナミックメディア配信を除く通常のDAM機能は、すべてのファイルでサポートされます。

| 形式 | ストレージ | バージョン管理 | ワークフロー | 公開 | アクセス制御 | Dynamic Media の配信 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| **²** | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| SVG | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| CSS | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| VTT | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| XML | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| JavaScript（独自の配信ドメインで設定する場合） |  |  |  |  |  | ✓ |

**²その他の形式は** 、DAMでの保存、バージョン管理、ACL、ワークフロー、投稿およびメタデータ管理に対応しています。

## サポートされる MIME タイプ {#supported-mime-types}

デフォルトでは、AEMはファイル拡張子を使用してファイルの種類を検出します。 AEMは、ファイルの内容からこのファイルを検出できます。 For latter, select [!UICONTROL Detect MIME from content] option in [!UICONTROL Day CQ DAM Mime Type Service] in the AEM Web Console.

CRXDE Liteでは、サポートされているMIMEタイプのリストを次の場所で使用できま `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`す。

[アップロードジョブパラメーターサポートの MIME タイプベースの設定](config-dynamic.md)を参照してください。

See also [Enabling MIME type-based Assets/Scene7 upload job parameter support](/help/sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support).

| ファイル拡張子 | MIME タイプ／インターネットメディアタイプ | デフォルトの jobParam 値 | 許可される jobParam 値 |
|---|---|---|---|
| 画像 | image/s7asset | `usmAmount=1.75&usmRadius=0.2`<br>`&usmThreshold=2&usmMonochrome=0&` | デフォルトの jobParam は、すべての画像の MIME タイプのアセットに適用されます。<ul><li>[knockoutBackgroundOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_knockout_background_options.html)</li><li>manualCropOptions</li><li>[autoColorCropOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/index.html?f=r_auto_color_crop_options)</li><li>[autoTransparentCropOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/?f=r_auto_transparent_crop_options)</li><li>[colorManagementOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_color_management_options.html)</li><li>[autoSetCreationOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_auto_set_creation_options.html)</li><li>[emailSetting](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/string_constants/index.html?f=r_email_settings)</li><li>[xmpKeywords](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/index.html?f=r_xmp_keywords)</li><li>[unsharpMaskOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_unsharp_mask_options.html)</li></ul> |
| 3G2 | video/3gpp2 |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| 3GP | video/3gpp |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/?f=r_exclude_master_video_from_avs) |
| AAC | audio/x-aac |  |  |
| AFM | application/x-font-type1 |  |  |
| AI | application/postscript | `aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_post_script_options.html)</li><li> [illustratorOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_illustrator_options.html)</li></ul> |
| AIFF | audio/x-aiff |  |  |
| AVI | video/x-msvideo |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| BMP | image/bmp |  |  |
| CSS | text/css |  |  |
| DOC | application/msword |  |  |
| EPS | <ul><li>application/postscript</li><li>application/eps</li><li>application/x-eps</li><li>image/eps</li><li>image/x-eps</li></ul> |  |  |
| F4V | video/x-f4v |  | ExcludeMasterVideoFromAVS |
| FLA | application/x-shockwave-flash |  |  |
| FLV | video/x-flv |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| FPX | image/vnd.fpx |  |  |
| GIF | image/gif |  |  |
| ICC | application/vnd.iccprofile |  |  |
| ICM | application/vnd.iccprofile |  |  |
| INDD | application/x-indesign |  |  |
| JPEG | image/jpeg |  |  |
| JPG | image/jpeg |  |  |
| M2V | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| M4V | video/x-m4v |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| MOV | video/quicktime |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| MP3 | audio/mpeg |  |  |
| MP4 | video/mp4 |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| MPEG | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| MPG | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| MTS | model/vnd.mts |  |  |
| OGV | video/ogg |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| OTF | application/x-font-otf |  |  |
| PDF | application/pdf | `pdfprocess=Rasterize&resolution=150`<br>`&colorspace=Auto&pdfbrochure=false`<br>`&keywords=false&links=false` | [pdfOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/?f=r_pdf_options) |
| PFB | application/x-font-type1 |  |  |
| PFM | application/x-font-type1 |  |  |
| PICT | image/x-pict |  |  |
| PNG | image/png |  |  |
| PPT | application/vnd.ms-powerpoint |  |  |
| PS | application/postscript | `psprocess=Rasterize&psresolution=150`<br>`&pscolorspace=Auto&psalpha=false`<br>`&psextractsearchwords=false`<br>`&aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/index.html?f=r_post_script_options)</li><li>[illustratorOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/index.html?f=r_illustrator_options)</li></ul> |
| PSD | image/vnd.adobe.photoshop | `process=None&layerNaming=Layername`<br>`&anchor=Center&createTemplate=false`<br>`&extractText=false&extendLayers=false` | <ul><li>[photoshopOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/?f=r_photoshop_options)</li><li>[photoshopLayerOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_photoshop_layer_options.html)</li></ul> |
| RTF | application/rtf |  |  |
| SVG | image/svg+xml |  |  |
| SWF | application/x-shockwave-flash |  |  |
| TAR | application/x-tar |  |  |
| TIF / TIFF | image/tiff |  |  |
| TTC | application/x-font-ttf |  |  |
| TTF | application/x-font-ttf |  |  |
| VOB | video/dvd |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| VTT | text/vtt |  |  |
| WAV | audio/x-wav |  |  |
| WEBM | video/webm |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| WMA | audio/x-ms-wma |  |  |
| WMV | video/x-ms-wmv |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| XLS | application/vnd.ms-excel |  |  |
| ZIP | application/zip |  |  |

>[!MORELIKETHIS]
>
>* [MIME タイプベースの Assets／Scene7 アップロードジョブパラメーターサポートの有効化](../sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support).

