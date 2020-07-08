---
title: を使用して、サポートされる様々なファイル形式を処理するためのベストプラクティス [!DNL Adobe Experience Manager Assets]。
description: を使用して、サポートされる様々なファイルタイプを処理するためのベストプラクティス [!DNL Experience Manager Assets]。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 678e91699523c22a7048bd7b344fa539b849ae8b
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 46%

---


# Assets のファイル形式に関するベストプラクティス {#assets-file-format-best-practices}

[!DNL Adobe Experience Manager Assets] はユーザーの様々なファイルサポート要件に対応するために、アドビ製およびサードパーティ製の数多くのファイル形式ライブラリをサポートしています。The supported Adobe libraries include, [!DNL Adobe Camera Raw], Gibson, Adobe PDF Rasterizer, and [!DNL Adobe InDesign Server]. また、は、、などのサードパーティライブラリを [!DNL Experience Manager Assets] サポートし [!DNL ImageMagick]て [!DNL TwelveMonkeys]います。

サポートされるファイル形式については、[アセットでサポートされるファイル形式](/help/assets/assets-formats.md)を参照してください。

>[!TIP]
>
>If you are using [!DNL Experience Manager] on Adobe Managed Services (AMS), reach out to Adobe Customer Care if you plan to process lots of large PSD or PSB files. AMSデプロイメントに関するこれらのベストプラクティスを実装し、アドビ独自の形式に関する最良のツールとモデルを選択するには、アドビカスタマーケアの担当者にご相談ください。 [!DNL Experience Manager] は、30000 x 23000ピクセルを超える高解像度PSBファイルを処理できない場合があります。

## [!DNL Adobe Camera Raw] ライブラリ {#adobe-camera-raw-library}

最適なパフォーマンスを得るために、RAWファイルとDNGファイルには [!DNL Adobe Camera Raw] ライブラリを使用することをお勧めします。

[!DNL Adobe Camera Raw] ライブラリは、入力としてCMYKカラープロファイルをサポートしています。 ただし、出力は RGB カラースペースで生成され、JPEG 形式の出力のみがサポートされます。サムネールにはソースファイルのカラースペース（CMYK など）は保持されません。

詳しくは、 [Camera Rawのサポートを参照してください](/help/assets/camera-raw.md)。

## Adobe PDF Rasterizer ライブラリ {#adobe-pdf-rasterizer-library}

最適な結果を得るために、次のファイルで Adobe PDF Rasterizer ライブラリを使用することをお勧めします。

* サイズが大きくコンテンツが多い PDF ファイル
* 追加設定なしでは生成されないサムネールがある AI ファイル
* SPOT（PMS）カラーの AI ファイル

PDF Rasterizer を使用して生成されたサムネールやプレビューの画質は、既製のラスター出力と比較して優れています。Adobe PDF Rasterizerライブラリは、カラースペースの変換をサポートしていません。 ソースPDFファイルのカラースペースに関係なく、Adobe PDF RasterizerはRGB出力のみを生成します。

## [!DNL Adobe InDesign Server] {#adobe-indesign-server}

Adobe recommends that you use [!DNL Adobe InDesign Server] to extract [!DNL Adobe InDesign]-specific renditions, such as IDML and HTML. For more information, see [Adding Experience Manager assets as references in Adobe InDesign](/help/assets/managing-linked-subassets.md#refai).

## [!DNL Dynamic Media] {#dynamic-media}

[!DNL Dynamic Media] は、パフォーマンスが最適化されスケーラビリティに優れたグローバルネットワーク経由で、様々なバリエーションのリッチコンテンツをリアルタイムで生成および配信します。インタラクティブな表示エクスペリエンスを提供し、デジタルキャンペーンの管理プロセスを促進します。For details around enabling [!DNL Dynamic Media], see [Configuring Dynamic Media](/help/assets/config-dynamic.md).

Currently, [!DNL Dynamic Media] can support videos up to 15 GB of content per file.

## ImageMagick ライブラリ {#imagemagick-library}

次のシナリオについては、ImageMagick ライブラリの使用をお勧めします。

* EPS ファイルのサムネールのレンディションを生成するとき。
* イメージプロファイル情報を保持するとき.
* 透明性を保持するとき.
* PSD および PSB ファイルを処理するとき.

To know how to set up the [!DNL ImageMagick] library in [!DNL Experience Manager], see [Using ImageMagick](/help/assets/media-handlers.md#an-example-using-imagemagick). 最適な使用方法については、[ImageMagick の設定のベストプラクティス](/help/assets/best-practices-for-imagemagick.md)を参照してください。

## 画像トランスコーディングライブラリ {#image-transcoding-library}

Adobe Imaging Transcoding Libraryは、画像のエンコーディング、トランスコード、再サンプリング、サイズ変更など、主要な画像処理機能を実行する画像処理ソリューションです。

画像トランスコーディングライブラリは、以下の MIME タイプをサポートします。

* JPG／JPEG
* PNG（8 ビットおよび 16 ビット）
* GIF
* BMP
* TIFF／圧縮 TIFF（32 ビット TIFF、PTIFF 以外）。
* ICO
* ICN

For details, see [Imaging Transcoding Library](/help/assets/imaging-transcoding-library.md).
