---
title: サポートされるファイル形式を処理するためのベストプラクティス
description: ' [!DNL Experience Manager Assets]を使用して、サポートされる様々なファイルタイプを処理するためのベストプラクティス。'
contentOwner: AG
role: Administrator
feature: アセット管理、開発者ツール
exl-id: da080f12-4cf7-4c26-901b-cd40d9c00bcb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 46%

---

# Assets のファイル形式に関するベストプラクティス {#assets-file-format-best-practices}

[!DNL Adobe Experience Manager Assets] はユーザーの様々なファイルサポート要件に対応するために、アドビ製およびサードパーティ製の数多くのファイル形式ライブラリをサポートしています。サポートされるAdobeライブラリは、[!DNL Adobe Camera Raw]、Gibson、Adobe PDF Rasterizer、[!DNL Adobe InDesign Server]です。 さらに、[!DNL Experience Manager Assets]は、[!DNL ImageMagick]、[!DNL TwelveMonkeys]などのサードパーティライブラリをサポートします。

サポートされるファイル形式については、[アセットでサポートされるファイル形式](/help/assets/assets-formats.md)を参照してください。

>[!TIP]
>
>Adobe Managed Services(AMS)で[!DNL Experience Manager]を使用している場合、大量のPSDまたはPSBファイルを処理する予定がある場合は、Adobeカスタマーケアにお問い合わせください。 Adobeカスタマーケア担当者と協力して、AMSデプロイメントに対してこれらのベストプラクティスを実装し、Adobe独自の形式に対して可能な限り最適なツールとモデルを選択します。 [!DNL Experience Manager] は、30000 x 23000ピクセルを超える高解像度のPSBファイルを処理しない場合があります。

## [!DNL Adobe Camera Raw] ライブラリ  {#adobe-camera-raw-library}

最適なパフォーマンスを得るために、AdobeではRAWファイルとDNGファイルに[!DNL Adobe Camera Raw]ライブラリを使用することをお勧めします。

[!DNL Adobe Camera Raw] ライブラリは、CMYKカラープロファイルを入力としてサポートします。ただし、出力は RGB カラースペースで生成され、JPEG 形式の出力のみがサポートされます。サムネールにはソースファイルのカラースペース（CMYK など）は保持されません。

詳しくは、[Camera Raw的なサポート](/help/assets/camera-raw.md)を参照してください。

## Adobe PDF Rasterizer ライブラリ {#adobe-pdf-rasterizer-library}

最適な結果を得るために、次のファイルで Adobe PDF Rasterizer ライブラリを使用することをお勧めします。

* サイズが大きくコンテンツが多い PDF ファイル
* 追加設定なしでは生成されないサムネールがある AI ファイル
* SPOT（PMS）カラーの AI ファイル

PDF Rasterizer を使用して生成されたサムネールやプレビューの画質は、既製のラスター出力と比較して優れています。Adobe PDF Rasterizerライブラリは、カラースペースの変換をサポートしていません。 ソースPDFファイルのカラースペースに関係なく、Adobe PDF RasterizerはRGB出力のみを生成します。

## [!DNL Adobe InDesign Server] {#adobe-indesign-server}

Adobeでは、[!DNL Adobe InDesign Server]を使用して、IDMLやHTMLなど、[!DNL Adobe InDesign]固有のレンディションを抽出することをお勧めします。 詳しくは、Adobe InDesign](/help/assets/managing-linked-subassets.md#refai)で[Experience Managerアセットを参照として追加を参照してください。

## [!DNL Dynamic Media] {#dynamic-media}

[!DNL Dynamic Media] は、パフォーマンスが最適化されスケーラビリティに優れたグローバルネットワーク経由で、様々なバリエーションのリッチコンテンツをリアルタイムで生成および配信します。インタラクティブな表示エクスペリエンスを提供し、デジタルキャンペーンの管理プロセスを促進します。[!DNL Dynamic Media]の有効化について詳しくは、[Dynamic Media](/help/assets/config-dynamic.md)の設定を参照してください。

現在、[!DNL Dynamic Media]は、1ファイルあたり最大15 GBのコンテンツのビデオをサポートしています。

## ImageMagick ライブラリ {#imagemagick-library}

次のシナリオについては、ImageMagick ライブラリの使用をお勧めします。

* EPS ファイルのサムネールのレンディションを生成するとき。
* イメージプロファイル情報を保持するとき.
* 透明性を保持するとき.
* PSD および PSB ファイルを処理するとき.

[!DNL Experience Manager]で[!DNL ImageMagick]ライブラリを設定する方法については、[ImageMagick](/help/assets/media-handlers.md#an-example-using-imagemagick)の使用を参照してください。 最適な使用方法については、[ImageMagick の設定のベストプラクティス](/help/assets/best-practices-for-imagemagick.md)を参照してください。

## 画像トランスコーディングライブラリ  {#image-transcoding-library}

Adobe画像トランスコーディングライブラリは、画像のエンコーディング、トランスコーディング、再サンプリング、サイズ変更など、主要な画像処理機能を実行する画像処理ソリューションです。

画像トランスコーディングライブラリは、以下の MIME タイプをサポートします。

* JPG／JPEG
* PNG（8 ビットおよび 16 ビット）
* GIF
* BMP
* TIFF／圧縮 TIFF（32 ビット TIFF、PTIFF 以外）。
* ICO
* ICN

詳しくは、[画像トランスコーディングライブラリ](/help/assets/imaging-transcoding-library.md)を参照してください。
