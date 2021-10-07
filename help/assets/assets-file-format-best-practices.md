---
title: サポートされるファイル形式を処理するためのベストプラクティス
description: ' [!DNL Experience Manager Assets] を使用して、サポートされる様々なファイルタイプを処理するためのベストプラクティス。'
contentOwner: AG
role: Admin
feature: Asset Management,Developer Tools
exl-id: da080f12-4cf7-4c26-901b-cd40d9c00bcb
source-git-commit: b2faf81983216bef9151548d90ae86f1c26a9f91
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 47%

---

# Assets のファイル形式に関するベストプラクティス {#assets-file-format-best-practices}

[!DNL Adobe Experience Manager Assets] はユーザーの様々なファイルサポート要件に対応するために、アドビ製およびサードパーティ製の数多くのファイル形式ライブラリをサポートしています。サポートされるAdobeライブラリは、[!DNL Adobe Camera Raw]、Gibson、Adobe PDF Rasterizer、[!DNL Adobe InDesign Server] です。 また、[!DNL Experience Manager Assets] は、[!DNL ImageMagick]、[!DNL TwelveMonkeys] などのサードパーティライブラリをサポートしています。

サポートされるファイル形式については、[アセットでサポートされるファイル形式](/help/assets/assets-formats.md)を参照してください。

>[!TIP]
>
>Adobe Managed Services(AMS) で [!DNL Experience Manager] を使用している場合、大きなPSDまたは PSB ファイルを大量に処理する予定がある場合は、Adobeカスタマーサポートにお問い合わせください。 Adobeカスタマーサポート担当者と協力して、AMS の導入に関するこれらのベストプラクティスを実装し、Adobe独自の形式に関する最適なツールとモデルを選択します。 [!DNL Experience Manager] は、30000 x 23000ピクセルを超える高解像度の PSB ファイルを処理しない場合があります。

## [!DNL Adobe Camera Raw] ライブラリ {#adobe-camera-raw-library}

最適なパフォーマンスを得るために、Adobeでは RAW ファイルと DNG ファイルに [!DNL Adobe Camera Raw] ライブラリを使用することをお勧めします。

[!DNL Adobe Camera Raw] ライブラリは、入力として CMYK カラープロファイルをサポートします。ただし、出力は RGB カラースペースで生成され、JPEG 形式の出力のみがサポートされます。サムネールにはソースファイルのカラースペース（CMYK など）は保持されません。

詳しくは、[Camera Raw的なサポート ](/help/assets/camera-raw.md) を参照してください。

## Adobe PDF Rasterizer ライブラリ {#adobe-pdf-rasterizer-library}

最適な結果を得るために、次のファイルで Adobe PDF Rasterizer ライブラリを使用することをお勧めします。

* サイズが大きくコンテンツが多い PDF ファイル
* 追加設定なしでは生成されないサムネールがある AI ファイル
* SPOT（PMS）カラーの AI ファイル

PDF Rasterizer を使用して生成されたサムネールやプレビューの画質は、既製のラスター出力と比較して優れています。Adobe PDF Rasterizer ライブラリは、カラースペースの変換をサポートしていません。 ソースPDFファイルのカラースペースに関係なく、Adobe PDF Rasterizer はRGB出力のみを生成します。

## [!DNL Adobe InDesign Server] {#adobe-indesign-server}

Adobeでは、[!DNL Adobe InDesign Server] を使用して、IDML やHTMLなど、[!DNL Adobe InDesign] 固有のレンディションを抽出することをお勧めします。 詳しくは、「[Adobe InDesign](/help/assets/managing-linked-subassets.md#refai) でExperience Managerアセットを参照として追加する」を参照してください。

## [!DNL Dynamic Media] {#dynamic-media}

[!DNL Dynamic Media] は、パフォーマンスが最適化されスケーラビリティに優れたグローバルネットワーク経由で、様々なバリエーションのリッチコンテンツをリアルタイムで生成および配信します。インタラクティブな表示エクスペリエンスを提供し、デジタルキャンペーンの管理プロセスを促進します。[!DNL Dynamic Media] の有効化について詳しくは、[Dynamic Media](/help/assets/config-dynamic.md) の設定を参照してください。

現在、[!DNL Dynamic Media] は 1 ファイルあたり最大 15 GB のコンテンツのビデオをサポートしています。

## ImageMagick ライブラリ {#imagemagick-library}

次のシナリオについては、ImageMagick ライブラリの使用をお勧めします。

* EPS ファイルのサムネールのレンディションを生成するとき。
* イメージプロファイル情報を保持するとき.
* 透明性を保持するとき.
* PSD および PSB ファイルを処理するとき.

[!DNL Experience Manager] で [!DNL ImageMagick] ライブラリを設定する方法については、[ImageMagick](/help/assets/media-handlers.md#an-example-using-imagemagick) の使用を参照してください。 最適な使用方法については、[ImageMagick の設定のベストプラクティス](/help/assets/best-practices-for-imagemagick.md)を参照してください。

## 画像トランスコーディングライブラリ {#image-transcoding-library}

Adobe画像トランスコーディングライブラリは、画像のエンコーディング、トランスコーディング、再サンプリング、サイズ変更など、主要な画像処理機能を実行する画像処理ソリューションです。

画像トランスコーディングライブラリは、以下の MIME タイプをサポートします。

* JPG／JPEG
* PNG（8 ビットおよび 16 ビット）
* GIF
* BMP
* TIFF／圧縮 TIFF（32 ビット TIFF、PTIFF 以外）。
* ICO
* ICN

詳しくは、[ 画像トランスコーディングライブラリ ](/help/assets/imaging-transcoding-library.md) を参照してください。
