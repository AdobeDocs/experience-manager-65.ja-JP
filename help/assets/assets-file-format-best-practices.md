---
title: サポートされるファイル形式を処理するためのベストプラクティス
description: サポートされる様々なファイルタイプを  [!DNL Experience Manager Assets] を使用して処理するためのベストプラクティス
contentOwner: AG
role: Admin
feature: Asset Management,Developer Tools
exl-id: da080f12-4cf7-4c26-901b-cd40d9c00bcb
source-git-commit: b2faf81983216bef9151548d90ae86f1c26a9f91
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 100%

---

# Assets のファイル形式に関するベストプラクティス {#assets-file-format-best-practices}

[!DNL Adobe Experience Manager Assets] はユーザーの様々なファイルサポート要件に対応するために、アドビ製およびサードパーティ製の数多くのファイル形式ライブラリをサポートしています。サポート対象のアドビのライブラリには、[!DNL Adobe Camera Raw]、Gibson、Adobe PDF Rasterizer および [!DNL Adobe InDesign Server] などがあります。さらに、[!DNL Experience Manager Assets] は、[!DNL ImageMagick] や [!DNL TwelveMonkeys] などを含むサードパーティライブラリをサポートしています。 

サポートされるファイル形式については、[アセットでサポートされるファイル形式](/help/assets/assets-formats.md)を参照してください。

>[!TIP]
>
>[!DNL Experience Manager] を Adobe Managed Services（AMS）で使用しており、大きな PSD ファイルまたは PSB ファイルを大量に処理する予定がある場合は、アドビカスタマーサポートにお問い合わせください。アドビカスタマーサポート担当者と協力して、AMS デプロイメントに関するこれらのベストプラクティスを実装し、アドビ独自の形式に対する最適なツールとモデルを選択します。[!DNL Experience Manager] では、30000 x 23000 ピクセルを超える高解像度の PSB ファイルを処理できない場合があります。

## [!DNL Adobe Camera Raw] ライブラリ {#adobe-camera-raw-library}

最適なパフォーマンスを得るには、RAW および DNG ファイル用の [!DNL Adobe Camera Raw] ライブラリを使用することをお勧めします。

[!DNL Adobe Camera Raw] ライブラリは、入力として CMYK カラープロファイルをサポートしています。 ただし、出力は RGB カラースペースで生成され、JPEG 形式の出力のみがサポートされます。サムネールにはソースファイルのカラースペース（CMYK など）は保持されません。

詳しくは、[Camera Raw サポート](/help/assets/camera-raw.md)を参照してください。

## Adobe PDF Rasterizer ライブラリ {#adobe-pdf-rasterizer-library}

最適な結果を得るために、次のファイルで Adobe PDF Rasterizer ライブラリを使用することをお勧めします。

* サイズが大きくコンテンツが多い PDF ファイル
* 追加設定なしでは生成されないサムネールがある AI ファイル
* SPOT（PMS）カラーの AI ファイル

PDF Rasterizer を使用して生成されたサムネールやプレビューの画質は、既製のラスター出力と比較して優れています。Adobe PDF Rasterizer ライブラリは、カラースペース変換をサポートしていません。ソース PDF ファイルのカラースペースに関わらず、Adobe PDF Rasterizer は RGB 出力のみを生成します。

## [!DNL Adobe InDesign Server] {#adobe-indesign-server}

IDML や HTML など [!DNL Adobe InDesign] 固有のレンディションを抽出するには、[!DNL Adobe InDesign Server] を使用することをお勧めします。詳しくは、[Adobe InDesign での参照としての Experience Manager アセットの追加](/help/assets/managing-linked-subassets.md#refai)を参照してください。

## [!DNL Dynamic Media] {#dynamic-media}

[!DNL Dynamic Media] は、パフォーマンスが最適化されスケーラビリティに優れたグローバルネットワーク経由で、様々なバリエーションのリッチコンテンツをリアルタイムで生成および配信します。インタラクティブな表示エクスペリエンスを提供し、デジタルキャンペーンの管理プロセスを促進します。[!DNL Dynamic Media] の有効化について詳しくは、[Dynamic Media の設定](/help/assets/config-dynamic.md)を参照してください。

現在、[!DNL Dynamic Media] では、1 ファイルにつき最大 15 GB のコンテンツのビデオをサポートしています。

## ImageMagick ライブラリ {#imagemagick-library}

次のシナリオについては、ImageMagick ライブラリの使用をお勧めします。

* EPS ファイルのサムネールのレンディションを生成するとき。
* イメージプロファイル情報を保持するとき.
* 透明性を保持するとき.
* PSD および PSB ファイルを処理するとき.

[!DNL Experience Manager] で [!DNL ImageMagick] ライブラリを設定する方法について詳しくは、[ImageMagick の使用](/help/assets/media-handlers.md#an-example-using-imagemagick)を参照してください。最適な使用方法については、[ImageMagick の設定のベストプラクティス](/help/assets/best-practices-for-imagemagick.md)を参照してください。

## 画像トランスコーディングライブラリ {#image-transcoding-library}

アドビの画像トランスコーディングライブラリは、画像のエンコーディング、トランスコーディング、リサンプリング、サイズ変更などの中心的な画像処理機能を実行する画像処理ソリューションです。

画像トランスコーディングライブラリは、以下の MIME タイプをサポートします。

* JPG／JPEG
* PNG（8 ビットおよび 16 ビット）
* GIF
* BMP
* TIFF／圧縮 TIFF（32 ビット TIFF、PTIFF 以外）。
* ICO
* ICN

詳しくは、[画像トランスコーディングライブラリ](/help/assets/imaging-transcoding-library.md)を参照してください。
