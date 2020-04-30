---
title: '[!DNL Adobe Experience Manager]でデジタルアセットのメタデータを管理します。'
description: メタデータのタイプと、[!DNL Adobe Experience Manager Assets]がアセットのメタデータを管理し、アセットの分類と整理を簡単にする方法について説明します。 [!DNL Experience Manager]を使用すると、メタデータに基づいてアセットを自動的に整理および処理できます。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 90f9c0b60d4b0878f56eefea838154bb7627066d

---


# デジタルアセットのメタデータの管理 {#managing-metadata-for-digital-assets}

[!DNL Adobe Experience Manager Assets] すべてのアセットのメタデータを保持します。 これにより、アセットの分類と整理が容易になり、特定のアセットを探している人が役立ちます。 With the ability to extract metadata from files uploaded to [!DNL Experience Manager Assets], metadata management integrates with the creative workflow. With the ability to keep and manage metadata with your assets, [!DNL Experience Manager Assets] makes it possible to automatically organize and process assets based on their metadata.

* [XMP メタデータ](xmp.md).
* [メタデータの編集と追加](meta-edit.md).
* [メタデータのスキーマに関する参照情報](meta-ref.md).

## メタデータが必要な理由 {#why-we-need-metadata}

メタデータとは、データに関する情報のことです。この場合、データとは、画像などのデジタルアセットを指します。 メタデータは、効率的なアセット管理のために重要です。

メタデータは、アセットで使用できるすべてのデータの集まりですが、その画像に必ずしも含まれているとは限りません。 メタデータの例を次に示します。

* アセットの名前。
* 最終変更の日時。
* リポジトリに保存されたアセットのサイズ。
* 格納先のフォルダの名前。
* 関連するアセットまたは適用されたタグ。

These are the basic metadata properties that [!DNL Experience Manager] can manage for assets, which allows users to see all assets, for example, ordered by their last modification date - useful when trying to discover what assets have recently been added to the repository.

デジタルアセットに、次のようなデータをさらに追加できます。

* アセットのタイプ(画像、ビデオ、オーディオクリップ、ドキュメント)。
* アセットの所有者。
* アセットのタイトル。
* アセットの説明。
* アセットに割り当てられたタグ。

メタデータが多いほど、アセットをより細かく分類でき、デジタル情報量が大きくなるにつれ便利です。数百個のファイルをファイル名に基づいて管理できます。 ただし、このアプローチは拡張性が低く、関与する人の数や管理する資産の数が増えるとすぐに不足します。

メタデータを追加すると、デジタルアセットの値が大きくなります。これは、アセットが

* アクセスしやすく — システムやユーザーが簡単に見つけられます。
* 管理が容易 — 同じプロパティのセットを持つアセットを簡単に検索し、変更を適用できます。
* より完全 — アセットに追加したメタデータが多いほど、より多くの情報とコンテキストが保持されます。

For these reasons, [!DNL Assets] provides you with the right means of creating, managing, and exchanging metadata for your digital assets.

## メタデータのタイプ {#types-of-metadata}

基本的な2種類のメタデータは、技術的なメタデータと説明的なメタデータです。

テクニカルメタデータは、デジタルアセットを操作しているソフトウェアアプリケーションで役に立つもので、手動で管理できません。[!DNL Experience Manager Assets] また、その他のソフトウェアは、技術的なメタデータを自動的に判定し、アセットが変更されるとメタデータが変更される場合があります。 アセットで使用可能なテクニカルメタデータは、主にアセットのファイルタイプによって決まります。技術的なメタデータの例を以下に示します。

* ファイルのサイズ。
* 画像の寸法（高さと幅）。
* オーディオまたはビデオファイルのビットレート。
* 画像の解像度（詳細レベル）。

記述メタデータは、アセットが属するビジネスなど、アプリケーションドメインに関するメタデータです。記述メタデータは自動で定義できません。手動または半自動で作成されます。 例えば、GPS対応のカメラでは、緯度と経度を自動的に追跡し、画像に地理タグを追加できます。

記述メタデータ情報の作成にかかる手動作業はコストが高いので、ソフトウェアシステムと組織との間でメタデータのやり取りを容易にするための規格が確立されています。

[!DNL Experience Manager Assets] は、メタデータ管理に関連するすべての標準をサポートしています。

メタデータは重要なもので、メタデータの作成には膨大な手動作業を必要とするので、やり取りを容易にするための規格が確立されています。

## エンコーディング規格 {#encoding-standards}

メタデータをファイルに埋め込む方法は様々です。 エンコーディング規格は、次の中から選択できます。

* XMP: used by [!DNL Assets] to store the extracted metadata within the repository.
* ID3：オーディオファイルおよびビデオファイル用の規格です。
* Exif:（画像ファイル用）。
* Other/Legacy: from [!DNL Microsoft Word], [!DNL PowerPoint], [!DNL Excel], and so on.

### XMP {#xmp}

[!DNL Extensible Metadata Platform] (XMP)は、すべてのメタデータ管理に使用されるオープン [!DNL Experience Manager Assets] な標準です。 標準オファーは、すべてのファイル形式に埋め込むことができるユニバーサルメタデータエンコーディングです。 アドビや他の会社は、リッチコンテンツモデルを提供するXMP標準をサポートしています。 XMP標準およびのユーザーは、 [!DNL Experience Manager Assets] 強力なプラットフォームを構築できます。 詳しくは、 [XMPを参照してください](https://www.adobe.com/products/xmp.html)。

### ID3 {#id}

これらの ID3 タグに格納されたデータは、コンピューターまたはポータブル MP3 プレーヤー上でデジタルオーディオファイルの再生時に表示されます。

ID3 タグは、MP3 ファイルフォーマット用に設計されています。各フォーマットのその他の情報：

* ID3タグは、MP3およびmp3PROファイルで機能します。
* WAV ではタグが使用されません。
* WMAには、オープンソース実装を許可しない独自のタグがあります。
* Ogg Vorbis では、Ogg コンテナに埋め込まれた Xiph コメントを使用します。
* AAC では独自のタグフォーマットが使用されます。

### Exif {#exif}

Exif(Exchangeable image file format)は、デジタル写真で最も人気の高いメタデータ形式です。 JPEG、TIFF、RIFF、WAVなど、多くのファイル形式でメタデータプロパティの固定語彙を埋め込む方法を提供します。 Exif stores metadata as pairs of a metadata name and a metadata value. These metadata name-value-pairs are also called tags, not to be confused with the tagging in [!DNL Experience Manager]. Exifは最新のデジタルカメラで自動的に作成され、最新のグラフィックソフトウェアを通じてサポートされるので、メタデータ管理の最も低い共通要素と見なすことができます。

Exifの主な制限は、BMP、GIF、PNGなどの一般的な画像ファイル形式ではサポートされないことです。

通常、Exifで定義されるメタデータフィールドは技術的な性質を持ち、説明的なメタデータ管理には限られています。 このため、Exifプロパティの [!DNL Experience Manager Assets] オファーマッピングは、共通のメ [タデータスキーマ](metadata-schemas.md) と [XMPに対して行われます](xmp-writeback.md)。

### Other metadata {#other-metadata}

ファイルから埋め込み可能なその他のメタデータには、Microsoft Word、PowerPoint、Excel などがあります。

## Metadata schemata {#metadata-schemata}

メタデータスキーマは、様々なアプリケーションで使用できる、定義済みのメタデータプロパティ定義のセットです。 プロパティは常にアセットに関連付けられます。つまり、プロパティはリソースに関する「概要」です。

必要に応じて独自のメタデータスキーマが存在しない場合は、独自のメタデータスキーマを設計することもできます。 既存の情報を重複しない。 組織内でスキーマを分割すると、メタデータの共有が容易になります。 [!DNL Experience Manager] 最も頻繁に使用されるメタデータリストのデフォルトスキーマを提供します。 このリストを使用すると、メタデータ戦略をすばやく開始し、必要なメタデータプロパティをすばやく選択できます。

サポートされるメタデータスキーマを以下に示します。

### Standard metadata {#standard-metadata}

* dc - [!DNL Dublin Core] is the most important and widely used set of metadata.
* DICOM - Digital Imaging and Communications in Medicine.
* Iptc4xmpCore &amp; iptc4xmpExt - International Press Communications Standardには、多くのサブジェクト固有のメタデータが含まれています。
* rdf - Resource Description Framework - 汎用のセマンティック Web メタデータ用.
* xmp - [!DNL Extensible Metadata Platform].
* xmpBJ - Basic Job Ticketing.

### Application-specific metadata {#application-specific-metadata}

アプリケーション固有のメタデータは、技術的および説明的なメタデータを含む。 これらのメタデータを使用すると、他のアプリケーションでそのメタデータを使用することはできません。For example, if you have an asset with [!DNL Adobe Photoshop] metadata and another image-rendering application tries to access the metadata, it may not be able to access the metadata. アセットに多くのアプリケーション固有のメタデータが含まれている場合は、アプリケーション固有のプロパティを標準のプロパティに変更するワークフロー手順を作成できます。

* ACDSee - Metadata managed by the [!DNL ACDSee] program. www.acdsee.com/を参 [照してくださ](https://www.acdsee.com/)い。
* アルバム — [!DNL Adobe Photoshop Album].
* cq - Used by [!DNL Experience Manager Assets].
* dam - Used by [!DNL Experience Manager Assets].
* dex - Optima SC Description Explorer.
* crs - Adobe Photoshop Camera Raw.
* lr - [!DNL Adobe Lightroom].
* mediapro - iView MediaPro.
* MicrosoftPhoto、MP - Microsoft Photo.
* pdf、pdfx.
* photoshop &amp; psAux - [!DNL Adobe Photoshop].

### Digital Rights Management metadata {#digital-rights-management-metadata}

* CC - [!DNL Creative Commons].
* [!DNL XMPRights].
* plus - [Picture Licensing Universal System](https://www.useplus.com).
* prism - Publishing Requirements for Industry Standard Metadata（https://www.idealliance.org/prism-metadata）.
* PRL - PRISM Rights Language。
* PUR - PRISM Usage Rights。
* xmpPlus - PLUSとXMPの統合。

### Photography-specific metadata {#photography-specific-metadata}

* Exif - GPS位置を含む、カメラからの技術情報。
* CRS - [!DNL Camera Raw] スキーマ
* Iptc4xmpCore、iptc4xmpExt.
* TIFF — 画像メタデータ（TIFF画像のみではありません）。

### Print-specific metadata {#print-specific-metadata}

* pdf、pdfx - Adobe PDF およびサードパーティのアプリケーション.
* prism - Publishing Requirements for Industry Standard Metadata（[www.prismstandard.org](https://www.prismstandard.org)）.
* xmp.
* xmpPG — ページテキストのXMPメタデータ。

### マルチメディア固有のメタデータ {#multimedia-specific-metadata}

* xmpDM - [!DNL Dynamic Media].
* xmpMM - Media Management.

## メタデータ駆動型のワークフロー {#metadata-driven-workflows}

メタデータ主導型のワークフローを作成すると、一部のプロセスを自動化でき、効率が向上します。 メタデータ駆動型のワークフローでは、ワークフロー管理システムでワークフローが読み取られ、その結果、事前定義された動作が実行されます。例として、メタデータ駆動型のワークフローの使用方法をいくつか示します。

* ワークフローでは、画像にタイトルが付いているかどうかを確認できます。 タイトルが追加されない場合は、タイトルの追加が通知されます。
* ワークフローは、アセットの著作権表示が配布を許可しているかどうかを確認できます。 したがって、システムは、アセットを一方のサーバまたは他方のサーバに送信します。
* ワークフローでは、定義済みの必須のメタデータまたは無効なメタデータを含むアセットがないかどうかを *確認でき* ます。
