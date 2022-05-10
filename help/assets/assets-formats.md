---
title: サポートしているファイル形式と MIME タイプ
description: ' [!DNL Assets]  および  [!DNL Dynamic Media]  でサポートしているファイル形式と MIME タイプおよび各形式でサポートされる機能。'
contentOwner: AG
mini-toc-levels: 1
role: User, Admin
feature: Asset Management,Renditions
exl-id: a4bcf67b-54f4-4681-9e42-fd4753acde1a
source-git-commit: fcbfd8b378282d908b68c61ab235e9b80fd6644c
workflow-type: tm+mt
source-wordcount: '1751'
ht-degree: 99%

---

# [!DNL Adobe Experience Manager Assets] でサポートされる形式 {#assets-supported-formats}

[!DNL Experience Manager Assets] は幅広いファイル形式をサポートしており、各機能は異なる MIME タイプに様々なサポートを提供しています。[!DNL Assets] を他の標準準拠のデジタルアセット管理（DAM）ソリューションおよびデスクトップソフトウェアと統合するには、アドビの [!DNL Extensible Metadata Platform]（XMP）を使用します。

凡例を使用すると、サポートレベルがわかります。

| サポートレベル | 説明 |
| :-----------: | ------------------------------ |
| ✓ | サポート対象 |
| &#42; | アドオン機能により対応 |
| − | 適用なし |

## [!DNL Experience Manager] でサポートされるラスタライズ画像形式 {#supported-raster-image-formats}

[!DNL Assets] でサポートされるラスタライズ画像形式は次の通りです。

| 形式 | ストレージ | メタデータの管理 | メタデータ抽出 | サムネールの生成 | 編集 | メタデータの書き戻し | インサイト |
| ------------ | :------: | :-----------------: | :-----------------: | :------------------: | :------: | :----------------: | :------: |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ |
| TIFF | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| BMP | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ |
| PNM | ✓ | ✓ | - | - | - | - | ✓ |
| PGM | ✓ | ✓ | - | - | - | - | ✓ |
| PBM | ✓ | ✓ | - | - | - | - | ✓ |
| PPM | ✓ | ✓ | - | - | - | - | ✓ |
| PSD ‡ | ✓ | ✓ | ✓ | ✓ | - | - | ✓ |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | - | ✓ | - |
| PICT | - | - | - | - | - | - | ✓ |
| PSB | ✓ | ✓ | ✓ | ✓ | - | - | - |

‡ 結合された画像は PSD ファイルから抽出されます。この画像は Adobe Photoshop によって生成され、PSD ファイルに含まれます。設定によって、結合された画像は実際の画像とは異なる場合があります。

上記の情報に加えて、以下を考慮してください。

* EPS ファイルのサポートは画像のラスタライズにのみ適用されます。例えば、EPS ベクター画像のサムネールの生成はデフォルトではサポートされません。サポートを追加するには、[ImageMagick を設定](best-practices-for-imagemagick.md)してください。サードパーティ製のツールを統合して追加機能を有効にするには、[コマンドラインベースのメディアハンドラー](media-handlers.md#command-line-based-media-handler)を参照してください。

* PSB ファイル形式でのメタデータの書き戻しは、`NComm` ハンドラーに追加すると機能するようになります。

* EPS ファイルの場合、メタデータの書き戻しは、PostScript Document Structuring Convention（PS-Adobe）バージョン 3.0 以降でサポートされています。

## サポートしている 3D ファイル形式 {#support-3d-formats}

サポートしている 3D 形式は、次のリストのとおりです。

[Dynamic Media での 3D アセット操作](/help/assets/assets-3d.md)も参照してください。

| 形式 | ストレージ | バージョン管理 | ワークフロー | 公開 | アクセス制御 | サムネールプレビュー | 3D プレビュー | Dynamic Media の配信 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DN | ✓ | ✓ | ✓ |  | ✓ | ✓ | - | - |
| gLB | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| gLTF | ✓ | ✓ | ✓ |  | ✓ | - | ✓ | - |
| OBJ | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| STL | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| USDz | ✓ | ✓ | ✓ | ✓ | ✓ | - | - | ✓ |

## サポートしている PDF Rasterizer ライブラリ {#supported-pdf-rasterizer-library}

Adobe PDF Rasterizer ライブラリは、サイズが大きくコンテンツが多い [!DNL Adobe Illustrator] ファイルや PDF ファイルに対して、高品質のサムネールとプレビューを生成します。次のようなファイルで PDF Rasterizer ライブラリを使用することをお勧めします。

* 処理でリソースに負担がかかる、コンテンツ集約型の AI ファイルや PDF ファイル。
* AI／PDF ファイル。デフォルトではサムネールは生成されません。
* Pantone Matching System（PMS）カラーを使用した AI ファイル.

[PDF ラスタライザーの使用](aem-pdf-rasterizer.md)を参照してください。

## サポートしている画像トランスコーディングライブラリ {#supported-image-transcoding-library}

Adobe Imaging Transcoding ライブラリは、エンコーディング、トランスコーディング、サンプリング変更、サイズ変更などの中心的な画像処理機能を実行する画像処理ソリューションです。

Imaging Transcoding ライブラリは、JPG／JPEG、PNG（8 ビットおよび 16 ビット）、GIF、BMP、TIFF／圧縮 TIFF（32 ビット TIFF ファイルおよび PTIFF ファイルを除く）、ICO、および ICN MIME タイプをサポートしています。

[画像トランスコーディングライブラリ](imaging-transcoding-library.md)を参照してください。

## サポート対象の Camera Raw {#supported-camera-raw}

 [!DNL Adobe Camera Raw] ライブラリを使用すると、[!DNL Assets] で RAW 画像を取り込むことができます。[Camera Raw サポート](camera-raw.md)を参照してください。

## サポートしている [!DNL Assets] ドキュメント形式 {#supported-document-formats}

アセット管理機能でサポートしているドキュメント形式は、次のとおりです。

| 形式 | ストレージ | [メタデータの管理](metadata.md) | フルテキスト<br> 抽出 | [メタデータ抽出](metadata.md) | サムネールの<br>生成 | [サブアセットの抽出](managing-linked-subassets.md) | [メタデータの書き戻し](xmp-writeback.md) | [接続された Assets](use-assets-across-connected-assets-instances.md) |
|---|---|---|---|---|---|---|---|---|
| [AI](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | - | ✓ | ✓ | ✓ | ✓ | - |
| DOC | ✓ | ✓ | ✓ | ✓ | - | - | - | ✓ |
| DOCX | ✓ | ✓ | ✓ | ✓ | - | - | - | ✓ |
| ODT | ✓ | ✓ | ✓ | - | - | - | - | ✓ |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| HTML | ✓ | ✓ | ✓ | - | - | - | - | ✓ |
| RTF | ✓ | ✓ | ✓ | - | - | - | - | ✓ |
| TXT | ✓ | ✓ | ✓ | - | - | - | - | ✓ |
| XLS | ✓ | ✓ | ✓ | - | - | - | - | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ | - | - | - | ✓ |
| ODS | ✓ | ✓ | ✓ | - | - | - | - | - |
| PPT | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ |
| ODP | ✓ | ✓ | ✓ | - | - | - | - | - |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | ✓ | ✓ | - | ✓ | ✓ | ✓ | ✓ | - |
| PS | ✓ | ✓ | - | - | - | - | - | - |
| QXP | ✓ | ✓ | - | - | - | - | - | - |
| EPUB | ✓ | ✓ | - | ✓ | ✓ | - | - | - |

## サポートしているマルチメディア形式 {#supported-multimedia-formats}

|  | ストレージ | メタデータの管理 | メタデータ抽出 | サムネールの生成 | FFmpeg トランスコーディング |
|:---|:---:|:---:|:---:|:---:|:---:|
| AAC | ✓ | ✓ | - | - | &#42; |
| MIDI | ✓ | ✓ | - | - | &#42; |
| 3GP | ✓ | ✓ | - | - | &#42; |
| MP3 | ✓ | ✓ | ✓ | - | &#42; |
| MPG | ✓ | ✓ | - | - | &#42; |
| OGA | ✓ | ✓ | - | - | &#42; |
| OGG | ✓ | ✓ | - | - | &#42; |
| RA | ✓ | ✓ | - | - | &#42; |
| WAV | ✓ | ✓ | - | - | &#42; |
| WMA | ✓ | ✓ | - | - | &#42; |
| DVI | ✓ | ✓ | - | &#42; | &#42; |
| FLV | ✓ | ✓ | - | &#42; | &#42; |
| M4V | ✓ | ✓ | - | &#42; | &#42; |
| MPEG | ✓ | ✓ | - | &#42; | &#42; |
| OGV | ✓ | ✓ | - | &#42; | &#42; |
| MOV | ✓ | ✓ | - | &#42; | &#42; |
| WMV | ✓ | ✓ | - | &#42; | &#42; |
| SWF | ✓ | ✓ | - | - | - |

## サポートされるアーカイブ形式 {#supported-archive-formats}

サポートされるアーカイブ形式と一般的な DAM ワークフローの適用性については、次の表で説明します。

| 形式 | ストレージ | バージョン管理 | ワークフロー | 公開 | アクセス制御 | Dynamic Media の配信 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| TGZ | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| JAR | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| RAR | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| TAR | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| ZIP | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |

## その他のサポートされる形式 {#other-supported-formats}

次に、いくつかの特定のファイル形式に対する通常の DAM 機能の適用性について説明します。

| 形式 | ストレージ | バージョン管理 | ワークフロー | 公開 | アクセス制御 | Dynamic Media の配信 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| SVG | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| CSS | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| VTT | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| XML | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| JavaScript（独自の配信ドメインで設定する場合） | - | - | - | - | - | ✓ |

>[!NOTE]
>
>JavaScript ファイルのアップロードと配布は安全な場合もあれば、安全でない場合もあります。必要に応じて、オーバーレイを使用して、ユーザーによる JS ファイルのアップロードを防ぐことができます。

## サポートされる MIME タイプ {#supported-mime-types}

デフォルトでは、[!DNL Experience Manager] は、ファイル拡張子を使用してファイルタイプを検出します。[!DNL Experience Manager] は、ファイルのコンテンツからこれを検出できます。後者の場合、[!DNL Experience Manager] web コンソールの「[!UICONTROL Day CQ DAM Mime Type Service]」で「[!UICONTROL Detect MIME from content]」オプションを選択します。

サポートされている MIME タイプのリストは、CRXDE Lite（`/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`）で入手できます。

| ファイル拡張子 | MIME タイプ／インターネットメディアタイプ | デフォルトの jobParam 値 | 許可される jobParam 値 |
|---|---|---|---|
| 画像 | image/s7asset | `usmAmount=1.75&usmRadius=0.2`<br>`&usmThreshold=2&usmMonochrome=0&` | デフォルトの jobParam は、すべての MIME タイプの画像アセットに適用されます。<ul><li>[knockoutBackgroundOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-knockout-background-options.html?lang=ja)</li><li>[manualCropOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-manual-crop-options.html?lang=ja)</li><li>[autoColorCropOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-auto-color-crop-options.html?lang=ja)</li><li>[autoTransparentCropOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-auto-transparent-crop-options.html?lang=ja)</li><li>[colorManagementOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-color-management-options.html?lang=ja)</li><li>[autoSetCreationOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-auto-set-creation-options.html?lang=ja)</li><li>[emailSetting](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/sting-constants/r-email-settings.html?lang=ja)</li><li>[xmpKeywords](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-xmp-keywords.html?lang=ja)</li><li>[unsharpMaskOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-unsharp-mask-options.html?lang=ja)</li></ul> |
| 3G2 | video/3gpp2 |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html?lang=ja) |
| 3GP | video/3gpp |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| AAC | audio/x-aac |  |  |
| AFM | application/x-font-type1 |  |  |
| AI | application/postscript | `aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-post-script-options.html?lang=ja)</li><li> [illustratorOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-illustrator-options.html?lang=ja)</li></ul> |
| AIFF | audio/x-aiff |  |  |
| AVI | video/x-msvideo |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| BMP | image/bmp |  |  |
| CSS | text/css |  |  |
| DOC | application/msword |  |  |
| EPS | <ul><li>application/postscript</li><li>application/eps</li><li>application/x-eps</li><li>image/eps</li><li>image/x-eps</li></ul> |  |  |
| F4V | video/x-f4v |  | ExcludeMasterVideoFromAVS |
| FLA | application/x-shockwave-flash |  |  |
| FLV | video/x-flv |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| FPX | image/vnd.fpx |  |  |
| GIF | image/gif |  |  |
| ICC | application/vnd.iccprofile |  |  |
| ICM | application/vnd.iccprofile |  |  |
| INDD | application/x-indesign |  |  |
| JPEG | image/jpeg |  |  |
| JPG | image/jpeg |  |  |
| M2V | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| M4V | video/x-m4v |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MOV | video/quicktime |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MP3 | audio/mpeg |  |  |
| MP4 | video/mp4 |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MPEG | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MPG | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MTS | model/vnd.mts |  |  |
| OGV | video/ogg |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| OTF | application/x-font-otf |  |  |
| PDF | application/pdf | `pdfprocess=Rasterize&resolution=150`<br>`&colorspace=Auto&pdfbrochure=false`<br>`&keywords=false&links=false` | [pdfOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-pdf-options.html?lang=ja) |
| PFB | application/x-font-type1 |  |  |
| PFM | application/x-font-type1 |  |  |
| PICT | image/x-pict |  |  |
| PNG | image/png |  |  |
| PPT | application/vnd.ms-powerpoint |  |  |
| PS | application/postscript | `psprocess=Rasterize&psresolution=150`<br>`&pscolorspace=Auto&psalpha=false`<br>`&psextractsearchwords=false`<br>`&aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-post-script-options.html)</li><li>[illustratorOptions]（https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-illustrator-options.html?lang=ja）</li></ul> |
| PSD | image/vnd.adobe.photoshop | `process=None&layerNaming=Layername`<br>`&anchor=Center&createTemplate=false`<br>`&extractText=false&extendLayers=false` | <ul><li>[photoshopOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-photoshop-options.html?lang=ja)</li><li>[photoshopLayerOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-photoshop-layer-options.html?lang=ja)</li></ul> |
| RTF | application/rtf |  |  |
| SVG | image/svg+xml |  |  |
| SWF | application/x-shockwave-flash |  |  |
| TAR | application/x-tar |  |  |
| TIF／TIFF | image/tiff |  |  |
| TTC | application/x-font-ttf |  |  |
| TTF | application/x-font-ttf |  |  |
| VOB | video/dvd |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| VTT | text/vtt |  |  |
| WAV | audio/x-wav |  |  |
| WEBM | video/webm |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| WMA | audio/x-ms-wma |  |  |
| WMV | video/x-ms-wmv |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| XLS | application/vnd.ms-excel |  |  |
| ZIP | application/zip |  |  |

## Dynamic Media - トランスコードでサポートされる入力ビデオ形式 {#supported-input-video-formats-for-dynamic-media-transcoding}

| ビデオファイル拡張子 | コンテナ | 推奨されるビデオコーデック | サポートされないビデオコーデック |
|---|---|---|---|
| AVI | A/V Interleave | XVID、DIVX、HDV、MiniDV（DV25）、Techsmith Camtasia、Huffyuv、Fraps、Panasonic DVCPro | Indeo3（IV30）、MJPEG、Microsoft® Video 1（MS-CRAM） |
| FLV、F4V | Adobe Flash | H264/AVC、Flix VP6、H263、Sorenson | SWF（ベクターアニメーションファイル） |
| M4V | Apple iTunes | H264/AVC | - |
| MKV | Matroska | H264/AVC | - |
| MOV、QT | Apple QuickTime | H264/AVC、Apple ProRes422 &amp; HQ、Sony XDCAM、Sony DVCAM、HDV、Panasonic DVCPro、Apple DV（DV25）、Apple PhotoJPEG、Sorenson、Avid DNxHD、Avid AVR | Apple Intermediate、Apple Animation |
| MP4 | MPEG-4 | H264/AVC（すべてのプロファイル） | - |
| MPG、VOB、M2V、MP2 | MPEG-2 | MPEG-2 | - |
| MXF ‡ | MXF | Sony XDCAM、MPEG-2、MPEG-4、Panasonic DVCPro | - |
| OGV、OGG | Ogg | Theora、VP3、Dirac | - |
| WebM | WebM | Google VP8 | - |
| WMV | Windows Media 9 | WMV3（v9）、WMV2（v8）、WMV1（v7）、GoToMeeting（G2M2、G2M3、G2M4） | Microsoft® Screen（MSS2）、Microsoft® Photo Story（WVP2） |

‡このビデオ形式は、Dynamic Media のインタラクティブビデオでの使用や、Experience Manager Assets の注釈での使用には、まだサポートされていません。

## Dynamic Media - サポートされるドキュメント形式 {#supported-document-formats-dynamic-media}

| 形式 | アップロード<br>（入力形式） | 画像<br>プリセット<br>の作成<br>（出力形式） | 動的<br>レンディション<br>のプレビュー | 動的<br>レンディション<br>の配信 | 動的<br>レンディション<br>のダウンロード |
|---|:---:|:---:|:---:|:---:|:---:|
| [AI](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | - | - | - | - |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | ✓ | - | - | - | - |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) （下記の注意を参照） | ✓ | ✓ | ✓ | ✓ | ✓ |

>[!NOTE]
>
>安全なPDFの場合、アップロードのみがサポートされます。

上記の機能に加えて、次を考慮する必要があります。

* PDF ファイルの動的レンディションの生成に Dynamic Media を使用するには、[Adobe Illustrator（AI）、Postscript（EPS）および PDF ファイル形式](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)を参照してください。

* AI ファイルの動的レンディションのプレビューと生成に Dynamic Media を使用するには、[Adobe Illustrator（AI）、Postscript（EPS）および PDF ファイル形式](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)を参照してください。

* INDD ファイルの動的レンディションの生成に Dynamic Media を使用するには、[InDesign（INDD）ファイル形式](../assets/managing-image-presets.md#indesign-indd-file-format)を参照してください。

## Dynamic Media - サポートしているラスターイメージ形式 {#supported-raster-image-formats-dynamic-media}

| 形式 | アップロード<br>（入力形式） | 画像<br>プリセット<br>の作成<br>（出力形式） | 動的<br>レンディション<br>のプレビュー | 動的<br>レンディション<br>の配信 | 動的<br>レンディション<br>のダウンロード | この形式をサポートするタイプを設定 |
|---|:---:|:---:|:---:|:---:|:---:| --- |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ | [画像](/help/assets/image-sets.md)、[混在メディア](/help/assets/mixed-media-sets.md)および [スピン](/help/assets/spin-sets.md) |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ | [画像](/help/assets/image-sets.md)、[混在メディア](/help/assets/mixed-media-sets.md)および [スピン](/help/assets/spin-sets.md) |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ | [画像](/help/assets/image-sets.md)、[混在メディア](/help/assets/mixed-media-sets.md)および [スピン](/help/assets/spin-sets.md) |
| BMP | ✓ | - | - | - | - | [画像](/help/assets/image-sets.md), [混在メディア](/help/assets/mixed-media-sets.md)および [スピン](/help/assets/spin-sets.md) |
| PSD‡ | ✓ | - | - | - | - | - |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| PICT | ✓ | - | - | - | - | - |

‡ 結合された画像は PSD ファイルから抽出されます。この画像は Adobe Photoshop によって生成され、PSD ファイルに含まれます。設定によって、結合された画像は実際の画像である場合とそうでない場合があります。

* EPS ファイルのサポートは画像のラスタライズにのみ適用されます。例えば、EPS ベクター画像のサムネールの生成はデフォルトではサポートされません。サポートを追加するには、[ImageMagick を設定](best-practices-for-imagemagick.md)してください。サードパーティツールを統合して追加機能を有効にするには、「[コマンドラインベースのメディアハンドラー](media-handlers.md#command-line-based-media-handler)」を参照してください。

* [!DNL Dynamic Media] を使用して EPS ファイルのプレビューと動的レンダリングを生成するには、[Adobe Illustrator（AI）、Postscript（EPS）および PDF ファイル形式を参照してください。](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* EPS ファイルの場合、メタデータの書き戻しは、PostScript Document Structuring Convention（PS-Adobe）バージョン 3.0 以降でサポートされています。

## Dynamic Media — サポートされていないラスタライズ画像形式 {#unsupported-image-formats-dynamic-media}

以下のリストは、Dynamic Media でサポートされて&#x200B;*いない*&#x200B;ラスタライズ画像ファイル形式のサブタイプに関する説明です。

ナレッジベース記事「[Dynamic Mediaでサポートされていないファイル形式を検出する](https://helpx.adobe.com/jp/experience-manager/kb/detect-unsupported-assets-for-dynamic-media.html)」も参照してください。

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
| JPEG  | Files where the initial three bytes is incorrect. | To identify a JPEG file, its initial three bytes must be `ff d8 ff`. If they are anything else, then it is not classified as a JPEG.<br>&bull; There is no software tool that can help with this issue.<br>&bull; A small C++/java program which reads the initial three bytes of a file should be able to detect these types of files.<br>&bull; It may be better to track the source of such files and look at the tool generating the file. |
| PNG |  Files that have an IDAT chunk size greater than 100 MB. | You can detect this issue using [libpng](http://www.libpng.org/pub/png/libpng.html) in C++. |
| PSB |  | Use exiftool if the file type is PSB.<br>Example in an ExifTool log:<br>1. File type: `PSB` |
| PSD | Files with a color space other than CMYK, RGB, Grayscale, or Bitmap are not supported.<br>DuoTone, Lab, and Indexed color spaces are not supported. | Use ExifTool if Color mode is Duotone.<br>Example in an ExifTool log:<br>1. Color mode: `Duotone` |
|  | Files with abrupt endings. | Adobe is unable to detect this condition. Also, such files cannot be opened with Adobe PhotoShop. Adobe suggests you examine the tool that was used to create such a file and troubleshoot at the source. |
|  | Files that have a bit depth greater than 16. | Use ExifTool if the bit depth is greater than 16.<br>Example in an ExifTool log:<br>1. Bit depth: `32` |
|  | File that have Lab color space. | Use exiftool if the color mode is Lab.<br>Example in an ExifTool log:<br>1. Color mode: `Lab` |
| TIFF | Files that have floating point data. That is, a TIFF file with 32-bit depth is not supported. | Use ExifTool if the MIME type is `image/tiff` and the SampleFormat has `Float` in its value. Example in an ExifTool log:<br>1. MIME type: `image/tiff`<br>Sample format: `Float #`<br>2. MIME type: `image/tiff`<br>Sample format: `Float; Float; Float; Float` |
|  | Files that have Lab color space. | Use ExifTool if the color mode is Lab.<br>Example in an ExifTool log:<br>1. Color mode: `Lab` |
-->

## Dynamic Media — サポートされる 3D 形式 {#supported-three-d-file-formats-in-dm}

Dynamic Media は、次の 3D ファイル形式をサポートしています。

[Dynamic Media での 3D アセット操作](/help/assets/assets-3d.md) も参照してください。

| 3D ファイル拡張子 | ファイル形式 | MIME タイプ | 備考 |
|---|---|---|---|
| GLB | バイナリ GL 伝送 | model/gltf-binary | マテリアルとテクスチャを単一のアセットとして含めます。 |
| OBJ | WaveFront 3D オブジェクトファイル | application/x-tgif |  |
| STL | ステレオリソグラフィ | application/vnd.ms-pki.stl |  |
| USDZ | 汎用シーン記述 Zip アーカイブ | model/vnd.usdz+zip | *取り込みのみサポート。表示やインタラクションは利用不可。* USDZ は独自の 3D 形式ですが、Safari や iOS でネイティブに表示できます。 |

>[!MORELIKETHIS]
>
>* [Assets と Dynamic Media Classic でMIME タイプベースの アップロードジョブパラメーターのサポートを有効化します](/help/sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support)。
>* [アップロードジョブパラメーターサポートの MIME タイプベースの設定](config-dynamic.md)を参照してください。

