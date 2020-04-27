---
title: AEM Assetsを使用して、サポートされる様々なファイル形式を処理するためのベストプラクティスです。
description: AEM Assetsを使用して、サポートされる様々なファイルタイプを処理するためのベストプラクティスです。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 31234518537ca4a0b7ff36e8d52a3b7b1b8fe4f7

---


# Assets のファイル形式に関するベストプラクティス {#assets-file-format-best-practices}

AEM Assets はユーザーの様々なファイルサポート要件に対応するために、アドビ製およびサードパーティ製の数多くのファイル形式ライブラリをサポートしています。サポート対象のアドビのライブラリには、Adobe Camera Raw、Gibson、Adobe PDF Rasterizer、Adobe InDesign Server などがあります。さらに、AEM Assets は ImageMagick や TwelveMonkeys などのサードパーティのライブラリをサポートします。

サポートされるファイル形式については、[アセットでサポートされるファイル形式](/help/assets/assets-formats.md)を参照してください。

>[!TIP]
>
>Adobe Managed Services(AMS)でExperience Managerを使用している場合は、大量のPSDまたはPSBファイルを処理する予定の場合は、アドビのサポート窓口にご連絡ください。 AMS導入のためのこれらのベストプラクティスを実装し、アドビ独自の形式に最適なツールとモデルを選択するには、アドビカスタマーケアの担当者にご相談ください。 3000 x 23000ピクセルを超える高解像度のPSBファイルは、Experience Managerでは処理されない場合があります。

## Adobe Camera Raw ライブラリ {#adobe-camera-raw-library}

最適なパフォーマンスを得るために、RAWファイルとDNGファイルにはAdobe Camera Rawライブラリを使用することをお勧めします。

Adobe Camera Rawライブラリは、入力としてCMYKカラープロファイルをサポートします。 ただし、出力は RGB カラースペースで生成され、JPEG 形式の出力のみがサポートされます。サムネールにはソースファイルのカラースペース（CMYK など）は保持されません。

詳しくは、 [Camera Rawのサポートを参照してください](/help/assets/camera-raw.md)。

## Adobe PDF Rasterizer ライブラリ {#adobe-pdf-rasterizer-library}

最適な結果を得るために、次のファイルで Adobe PDF Rasterizer ライブラリを使用することをお勧めします。

* サイズが大きくコンテンツが多い PDF ファイル
* 追加設定なしでは生成されないサムネールがある AI ファイル
* SPOT（PMS）カラーの AI ファイル

PDF Rasterizer を使用して生成されたサムネールやプレビューの画質は、既製のラスター出力と比較して優れています。Adobe PDFラスタライザライブラリは、カラースペースの変換をサポートしていません。 ソースPDFファイルのカラースペースに関係なく、Adobe PDFラスタライザーはRGB出力のみを生成します。

## Adobe InDesign Server {#adobe-indesign-server}

IDML や HTML など Adobe InDesign 固有のレンディションを抽出するには、Adobe InDesign Server の使用をお勧めします。For more information, see [Adding AEM assets as references in Adobe InDesign](/help/assets/managing-linked-subassets.md#refai).

## Dynamic Media  {#dynamic-media}

Dynamic Media は、パフォーマンスが最適化されスケーラビリティに優れたグローバルネットワーク経由で、様々なバリエーションのリッチコンテンツをリアルタイムで生成および配信します。インタラクティブな表示エクスペリエンスを提供し、デジタルキャンペーンの管理プロセスを促進します。Dynamic Media の有効化について詳しくは、[Dynamic Media の設定](/help/assets/config-dynamic.md)を参照してください。

現在、Dynamic Media では、1 ファイルにつき最大 20 GB のコンテンツのビデオをサポートしています。

## ImageMagick ライブラリ {#imagemagick-library}

次のシナリオについては、ImageMagick ライブラリの使用をお勧めします。

* EPS ファイルのサムネールのレンディションを生成するとき
* イメージプロファイル情報を保持するとき
* 透明性を保持するとき
* PSD および PSB ファイルを処理するとき

To know how to set up the ImageMagic library in AEM, see [Using ImageMagick](/help/assets/media-handlers.md#an-example-using-imagemagick). 最適な使用方法については、[ImageMagick の設定のベストプラクティス](/help/assets/best-practices-for-imagemagick.md)を参照してください。

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
