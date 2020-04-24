---
title: デジタルアセットのメタデータの管理 [!DNL Adobe Experience Manager]内。
description: メタデータのタイプと、[!DNL Adobe Experience Manager Assets]がアセットのメタデータを管理し、アセットの分類と整理を簡単にする方法について説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: abc4821ec3720969bf1c2fb068744c07477aca46

---


# デジタルアセットのメタデータの管理 {#managing-metadata-for-digital-assets}

[!DNL Adobe Experience Manager Assets] すべてのアセットのメタデータを保持します。 したがって、アセットの分類および編成が容易にでき、特定のアセットを検索しやすくなります。With the ability to extract metadata from files uploaded to [!DNL Experience Manager Assets], metadata management integrates with the creative workflow. With the ability to keep and manage arbitrary metadata with your assets, [!DNL Experience Manager Assets] makes it possible to automatically organize and process assets based on their metadata.

* [XMP メタデータ](xmp.md)
* [メタデータの編集と追加](meta-edit.md)
* [メタデータのスキーマに関する参照情報](meta-ref.md)

## メタデータが必要な理由 {#why-we-need-metadata}

メタデータとは、データに関する情報のことです。この場合、データとは操作するアセット（画像など）を指します。メタデータによってアセットをより効率的に管理できるので、メタデータは重要なものです。

メタデータは、対象の画像で使用できるすべてのデータのコレクションですが、次のようなデータは、その画像に含まれているとは限りません。

* アセットの名前
* 最終変更日時
* リポジトリに格納されたときの画像のサイズ
* アセットが含まれるフォルダーの名前

These are the basic metadata properties that [!DNL Experience Manager] can manage for assets, which allows users to see all assets, for example, ordered by their last modification date - useful when trying to discover what assets have recently been added to the repository.

デジタルアセットに、次のようなデータをさらに追加できます。

* アセットのタイプ（画像、ビデオ、オーディオクリップ、ドキュメントなど）
* アセットの所有者
* アセットのタイトル
* アセットの説明
* アセットに割り当てられたタグ

メタデータが多いほど、アセットをより細かく分類でき、デジタル情報量が大きくなるにつれ便利です。1 人のユーザーが数百ファイルのリストをファイル名だけで管理することはできても、多数のユーザーが関係し、管理するアセットの数が多くなると、ファイル名だけの管理では不十分です。

メタデータをアセットに追加すると、アセットは次のような特徴を持つので、アセットの価値が高まります。

* アクセスのしやすさ - 検索が容易になります
* 管理のしやすさ - 一連の同じプロパティを持つアセットを容易に検索し、これらのアセットに変更を適用できます
* より高い複雑性 - アセットに追加するメタデータが多くなるほど、メタデータの管理がより重要になります

For these reasons, [!DNL Assets] provides you with the right means of creating, managing, and exchanging metadata for your digital assets.

## メタデータの基本 {#metadata-basics}

メタデータは、アセットの読み込み（取り込み）時に抽出されます。メタデータを追加すると、アセットをより細かく分類できます。

この節では、メタデータおよびエンコーディング規格のタイプについて説明します。

### メタデータのタイプ {#types-of-metadata}

メタデータには、次の 2 つの基本的なタイプがあります。

* テクニカルメタデータ
* 記述メタデータ

#### テクニカルメタデータ {#technical-metadata}

テクニカルメタデータは、デジタルアセットを操作しているソフトウェアアプリケーションで役に立つもので、手動で管理できません。Technical metadata can be determined automatically by [!DNL Experience Manager Assets] and other software and may change when the asset is modified. アセットで使用可能なテクニカルメタデータは、主にアセットのファイルタイプによって決まります。テクニカルメタデータの例を次に示します。

* ファイルのサイズ
* 画像のサイズ（高さと幅）
* オーディオファイルやビデオファイルのビットレート
* 画像の解像度（詳細レベル）

#### 記述メタデータ {#descriptive-metadata}

記述メタデータは、アセットが属するビジネスなど、アプリケーションドメインに関するメタデータです。記述メタデータは自動で定義できません。手動または半自動で作成する必要があります。例えば、画像が撮影された場所の緯度と経度を GPS が有効なカメラで自動的に追跡し、その情報を画像のメタデータに追加します。

記述メタデータ情報の作成にかかる手動作業はコストが高いので、ソフトウェアシステムと組織との間でメタデータのやり取りを容易にするための規格が確立されています。

[!DNL Experience Manager Assets] は、メタデータ管理に関連するすべての標準をサポートしています。

メタデータは重要なもので、メタデータの作成には膨大な手動作業を必要とするので、やり取りを容易にするための規格が確立されています。

### エンコーディング規格 {#encoding-standards}

メタデータは、様々な方法でファイルに埋め込むことができます。エンコーディング規格は、次の中から選択できます。

* XMP: used by [!DNL Assets] to store the extracted metadata within the repository.
* ID3：オーディオファイルおよびビデオファイル用の規格です。
* EXIF：画像ファイル用の規格です。
* その他、従来の規格：Microsoft Word、PowerPoint、Excel など

#### XMP {#xmp}

XMP means Extensible Metadata Platform and is the metadata standard that is used by [!DNL Experience Manager Assets] for all metadata management. Besides offering universal metadata encoding that can be embedded into all file formats, XMP provides a rich content model and is supported by Adobe and other companies, so that users of XMP in combination with [!DNL Experience Manager Assets] have a powerful platform to build upon.

#### ID3 {#id}

これらの ID3 タグに格納されたデータは、コンピューターまたはポータブル MP3 プレーヤー上でデジタルオーディオファイルの再生時に表示されます。

ID3 タグは、MP3 ファイルフォーマット用に設計されています。各フォーマットのその他の情報：

* ID3 タグは、MP3 ファイルおよび MP3pro ファイルで使用できます。
* WAV ではタグが使用されません。
* WMA では独自のタグが使用され、オープンソースの実装は許可されていません。
* Ogg Vorbis では、Ogg コンテナに埋め込まれた Xiph コメントを使用します。
* AAC では独自のタグフォーマットが使用されます。

#### EXIF {#exif}

EXIF は Exchangeable image file format のことで、デジタル写真で最も一般的に使用されるメタデータフォーマットです。JPEG、TIFF、RIFF、WAVなど、様々なファイル形式でメタデータプロパティの固定語彙を埋め込む方法を提供します。

EXIF の大きな制限は、その他の一般的な画像ファイル（BMP、GIF、PNG など）でサポートされないことです。

EXIF によって、メタデータの名前と値のペアとして、メタデータが格納されます。These metadata name-value-pairs are also called tags, not to be confused with the tagging in [!DNL Experience Manager].

EXIF は最新のデジタルカメラで自動的に作成され、最新のグラフィックソフトウェアでサポートされているので、メタデータの管理では最も下位の共通項目として表示されます。

EXIF で定義されるメタデータフィールドのほとんどは、高度な技術で作成されたもので、記述メタデータの管理では使用が制限されています。For this reason, [!DNL Assets] offers mapping of EXIF properties into [common metadata schemata](metadata-schemas.md) and into [XMP](xmp-writeback.md), the powerful metadata format [!DNL Assets] uses for metadata management.

#### その他のメタデータ {#other-metadata}

ファイルから埋め込み可能なその他のメタデータには、Microsoft Word、PowerPoint、Excel などがあります。

## メタデータスキーマ {#metadata-schemata}

メタデータスキーマは、様々なアプリケーションで使用できる、定義済みのメタデータプロパティ定義のセットです。プロパティは常にアセットに関連付けられます。つまり、プロパティはリソースに関するものです。

ニーズに合うメタデータスキーマが存在しない場合は、独自のメタデータスキーマを設計できます（ただし、既存のスキーマを複製しないようにしてください）。組織内でスキーマを分割すると、メタデータを共有しやすくなります。

[!DNL Experience Manager] では、そのままで使用できる、最も一般的なメタデータスキーマのリストが用意されています。したがってメタデータ機能をすぐに開始でき、定義済みのスキーマから必要なメタデータプロパティを選択できます。

サポートされるメタデータスキーマを以下に示します。

### 標準的なメタデータ {#standard-metadata}

* dc - Dublin Core - 最も重要で広く使用されるメタデータのセット
* DICOM - Digital Imaging and Communications in Medicine
* Iptc4xmpCore &amp; iptc4xmpExt - International Press Communications Standard — 多数のサブジェクト固有のメタデータ
* rdf - Resource Description Framework - 汎用のセマンティック Web メタデータ用
* xmp - Extensible Metadata Platform
* xmpBJ - Basic Job Ticketing

### アプリケーション固有のメタデータ {#application-specific-metadata}

>[!NOTE]
>
>アプリケーション固有のメタデータには、テクニカルメタデータも記述メタデータも存在します。これらのメタデータを使用すると、他のアプリケーションでそのメタデータを使用することはできません。例えば、アセットが Adobe Photoshop メタデータを持つ場合、他の画像レンダリングアプリケーションでこのアセットにアクセスしようとしても失敗します。
>
>アセット内にアプリケーション固有のメタデータが数多く存在する場合、アプリケーション固有のプロパティを標準プロパティに変更するワークフロー手順を作成できます。

* acdsee - ACDSee プログラムで管理されるメタデータ（[www.acdsee.com/](https://www.acdsee.com/)）
* album - Adobe Photoshop アルバム
* cq - used by [!DNL Experience Manager Assets]
* dam - used by [!DNL Experience Manager Assets]
* dex - Optima SC Description Explorer
* crs - Adobe Photoshop Camera Raw
* lr - Adobe Lightroom
* mediapro - iView MediaPro
* Microsoft PhotoおよびMP - Microsoft Photo
* pdf amd pdfx
* photoshop、psAux - Adobe Photoshop

### デジタル著作権管理メタデータ {#digital-rights-management-metadata}

* cc - クリエイティブコモンズ
* xmpRights
* plus - Picture Licensing Universal System（https://www.useplus.com/）
* prism - Publishing Requirements for Industry Standard Metadata（https://www.idealliance.org/prism-metadata）
* prl - Prism Rights Language
* pur - Prism Usage Rights
* xmpPlus - PLUS と XMP との統合

### 写真固有のメタデータ {#photography-specific-metadata}

* exif - カメラからの数多くのテクニカル情報（GPS 位置など）
* crs - Photoshop Camera Raw
* Iptc4xmpCore、iptc4xmpExt
* TIFF - 画像メタデータ（TIFF 画像に限りません）

### 印刷固有のメタデータ {#print-specific-metadata}

* pdf、pdfx - Adobe PDF およびサードパーティのアプリケーション
* prism - Publishing Requirements for Industry Standard Metadata（[www.prismstandard.org](https://www.prismstandard.org)）
* xmp
* xmpPG - ページ化されたテキスト用の xmp

### マルチメディア固有のメタデータ {#multimedia-specific-metadata}

* xmpDM - Dynamic Media
* xmpMM - Media Management

## メタデータ駆動型のワークフロー {#metadata-driven-workflows}

メタデータ駆動型のワークフローを作成することで、一部のプロセスを自動化し、効率性を高めることができます。メタデータ駆動型のワークフローでは、ワークフロー管理システムでワークフローが読み取られ、その結果、事前定義された動作が実行されます。

例として、メタデータ駆動型のワークフローの使用方法をいくつか示します。

* ワークフローで、画像にタイトルがあるかどうかをチェックできます。タイトルがない場合、タイトルを追加するよう特定のユーザーに通知されます。
* ワークフローで、アセットの著作権情報によって配布が許可されているかどうかをチェックできます。許可されている場合、アセットが 1 つのサーバーに送信されます。許可されていない場合、アセットが別のサーバーに送信されます。
