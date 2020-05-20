---
title: Manage metadata of your digital assets in [!DNL Adobe Experience Manager].
description: メタデータのタイプについて説明します。メタデータに基づいてアセットを自動的に整理および処理できる [!DNL Adobe Experience Manager Assets] helps manage metadata for assets to allow easier categorization and organization of assets. [!DNL Experience Manager] 方法について説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 23d19d9656d61874cd00a9a2473092be0c53b8f8
workflow-type: tm+mt
source-wordcount: '1412'
ht-degree: 18%

---


# デジタルアセットのメタデータの管理 {#managing-metadata-for-digital-assets}

[!DNL Adobe Experience Manager Assets] は、すべてのアセットのメタデータを保持します。 アセットの分類と整理が容易になり、特定のアセットを探すユーザーの役に立ちます。 With the ability to extract metadata from files uploaded to [!DNL Experience Manager Assets], metadata management integrates with the creative workflow. メタデータを保持し、アセットと共に管理する機能により、メタデータに基づいてアセットを自動的に整理および処理できます。

* [XMP メタデータ](xmp.md).
* [メタデータの編集と追加](meta-edit.md).
* [メタデータのスキーマに関する参照情報](meta-ref.md).

<!--  TBD: Complete this section. Take help from Metadata IRD for DDAM. Also, look at metadata features in Forrester analysis.

## Understand metadata handling in Experience Manager {#metadata-possibilities-with-aem}

Describe the journey of an assets' metadata. What all happens to metadata when an asset is added to AEM.

## Add metadata to your digital assets {#add-metadata}

Typically, the applications that create digital assets add some metadata to the assets created. Before uploading an asset to Experience Manager, you can edit and modify metadata using either the native application used to create an asset or using some metadata editors. When you upload an asset to Experience Manager, the metadata is processed.

## Metadata of assets, folders, and collections {#metadata-of-assets-folders-collections}

## Modify metadata of an asset, folder, or collection {#modify-metadata}

## Modify metadata in bulk {#modify-metadata-in-bulk}

Adobe Enterprise Manager Assets lets you edit the metadata of multiple assets simultaneously so you can quickly propagate common metadata changes to assets in bulk. You can also edit the metadata for multiple collections in bulk.

Use the properties page to perform metadata changes on multiple assets or collections:

* Change metadata properties to a common value
* Add or modify tags

To customize the metadata properties page, including adding, modifying, deleting metadata properties, use the schema editor.

>[!NOTE]
>
>The bulk editing methods work for assets available in a folder or a collection. For the assets that are available across folders or match a common criteria, it is possible to [bulk update the metadata after searching](search-assets.md#metadataupdates).

1. In the Assets user interface, navigate to the location of the assets you want to edit.
1. Select the assets for which you want to edit common properties.
1. From the toolbar, click the **[!UICONTROL Properties]** icon to open the properties page for the selected assets.

   >[!NOTE]
   >
   >When you select multiple assets, the lowest common parent form is selected for the assets. In other words, the properties page only displays metadata fields that are common across the properties pages of all the individual assets.

1. Modify the metadata properties for selected assets under the various tabs.
1. To view the metadata editor for a specific asset, deselect the remaining assets in the list. The metadata editor fields are populated with the metadata for the particular asset.

   >[!NOTE]
   >
   >* In the properties page, you can remove assets from the asset list by deselecting them. The asset list has all the assets selected by default. The metadata for assets that you remove from the list is not updated.
   >* At the top of assets list, select the check box near **[!UICONTROL Title]** to toggle between selecting the assets and clearing the list.

1. To select a different metadata schema for the assets, click the **[!UICONTROL Settings]** icon from the toolbar, and select the desired schema.
1. Save the changes.
1. To append the new metadata with the existing metadata in fields that contain multiple values, select **[!UICONTROL Append mode]**. If you do not select this option, the new metadata replaces the existing metadata in the fields. click **[!UICONTROL Submit]**.

   >[!CAUTION]
   >
   >For single-value fields, the new metadata is not appended to the existing value in the field even if you select **[!UICONTROL Append mode]**.

## Configure limit for bulk metadata update {#limit-bulk-metadata-updates}

To prevent DOS like situation, Enterprise Manager limits the number of parameters supported in a Sling request. When updating metadata of many assets in one go, you may reach the limit and the metadata does not get updated for more assets. Enterprise Manager generates the following warning in the logs:

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

To change the limit, access **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]** and change the value of **[!UICONTROL Maximum POST Parameters]** in **[!UICONTROL Apache Sling Request Parameter Handling]** OSGi configuration.

-->

## メタデータが必要な理由 {#why-we-need-metadata}

メタデータとは、データに関する情報のことです。この点に関して、データは、例えば画像など、デジタルアセットを指します。 メタデータは、効率的なアセット管理を行うために重要です。

メタデータは、アセットに使用できるすべてのデータの集まりですが、その画像に必ずしも含まれているとは限りません。 メタデータの例を以下に示します。

* アセットの名前。
* 最終変更の日時。
* リポジトリに保存されたアセットのサイズ。
* フォルダーの名前。
* 関連するアセットまたは適用したタグ。

上記は、アセットに対して管理できる基本的なメタデータプロパティで [!DNL Experience Manager] す。これにより、ユーザーはすべてのアセットを表示できます。 例えば、最終変更日にアセットを並べ替えると、最近追加したアセットを検出する場合に便利です。

デジタルアセットに、次のようなデータをさらに追加できます。

* アセットのタイプ(画像、ビデオ、オーディオクリップまたはドキュメントか)。
* アセットの所有者。
* アセットのタイトル。
* アセットの説明。
* アセットに割り当てられたタグ。

メタデータが多いほど、アセットをより細かく分類でき、デジタル情報量が大きくなるにつれ便利です。数百個のファイルをファイル名だけに基づいて管理できます。 ただし、このアプローチは拡張性に欠けます。 関係者の数や管理対象資産の数が増えると、短くなります。

メタデータを追加すると、デジタルアセットの値が大きくなります。これは、アセットが

* アクセスしやすい — システムやユーザーは簡単に見つけることができます。
* 管理が容易 — 同じプロパティのセットを持つアセットを検索し、それらに変更を適用しやすくなります。
* 完了 — より多くの情報とコンテキストを、より多くのメタデータと共に持ちます。

For these reasons, [!DNL Assets] provides you with the right means of creating, managing, and exchanging metadata for your digital assets.

## メタデータのタイプ {#types-of-metadata}

メタデータの2つの基本的なタイプは、技術的なメタデータと説明的なメタデータです。

テクニカルメタデータは、デジタルアセットを操作しているソフトウェアアプリケーションで役に立つもので、手動で管理できません。[!DNL Experience Manager Assets] また、他のソフトウェアは、自動的に技術的なメタデータを決定し、アセットが変更されるとメタデータが変更される場合があります。 アセットで使用可能なテクニカルメタデータは、主にアセットのファイルタイプによって決まります。技術的なメタデータの例を以下に示します。

* ファイルのサイズ。
* 画像の寸法（高さと幅）。
* オーディオまたはビデオファイルのビットレート。
* 画像の解像度（詳細のレベル）。

記述メタデータは、アセットが属するビジネスなど、アプリケーションドメインに関するメタデータです。記述メタデータは自動で定義できません。手動または半自動で作成されます。 例えば、GPS対応のカメラでは、緯度と経度を自動的に追跡し、画像に地理タグを追加できます。

説明的なメタデータ情報を手動で作成する場合のコストが高くなります。 そのため、ソフトウェアシステムや組織間でのメタデータの交換を容易にするための基準が確立されています。 [!DNL Experience Manager Assets] は、メタデータ管理に関するすべての関連標準をサポートしています。

## エンコーディング規格 {#encoding-standards}

メタデータをファイルに埋め込む方法は様々です。 エンコーディング規格は、次の中から選択できます。

* XMP: used by [!DNL Assets] to store the extracted metadata within the repository.
* ID3：オーディオファイルおよびビデオファイル用の規格です。
* Exif: （画像ファイル用）
* Other/Legacy: from [!DNL Microsoft Word], [!DNL PowerPoint], [!DNL Excel], and so on.

### XMP {#xmp}

[!DNL Extensible Metadata Platform] (XMP)は、すべてのメタデータ管理で使用されるオープンな標準 [!DNL Experience Manager Assets] です。 すべてのファイル形式に埋め込むことができる標準オファーのユニバーサルメタデータエンコーディングです。 アドビやその他の会社は、リッチコンテンツモデルを提供するXMP標準をサポートしています。 XMP標準およびのユーザーは、基盤と [!DNL Experience Manager Assets] なる強力なプラットフォームを持っています。 詳しくは、「 [XMP](https://www.adobe.com/products/xmp.html)」を参照してください。

### ID3 {#id}

これらの ID3 タグに格納されたデータは、コンピューターまたはポータブル MP3 プレーヤー上でデジタルオーディオファイルの再生時に表示されます。

ID3 タグは、MP3 ファイルフォーマット用に設計されています。各フォーマットのその他の情報：

* ID3タグは、MP3およびmp3PROファイルで機能します。
* WAV ではタグが使用されません。
* WMAには、オープンソースの実装を許可しない独自のタグがあります。
* Ogg Vorbis では、Ogg コンテナに埋め込まれた Xiph コメントを使用します。
* AAC では独自のタグフォーマットが使用されます。

### Exif {#exif}

Exchangeable Image File Format(Exif)は、デジタル写真で最も使用されるメタデータ形式です。 JPEG、TIFF、RIFF、WAVなど、多くのファイル形式でメタデータプロパティの固定語彙を埋め込む方法を提供します。 Exif stores metadata as pairs of a metadata name and a metadata value. These metadata name-value-pairs are also called tags, not to be confused with the tagging in [!DNL Experience Manager]. 最新のデジタルカメラはExifメタデータを作成し、最新のグラフィックソフトウェアがそれをサポートします。 Exif形式は、特に画像に関するメタデータ管理で最も一般的な分母です。

Exifの主な制限は、BMP、GIF、PNGなどの一般的な画像ファイル形式ではサポートされないことです。

Exifで定義されるメタデータフィールドは、通常、技術的なもので、説明的なメタデータ管理では使用が制限されています。 このため、Exifプロパティの [!DNL Experience Manager Assets] オファーマッピングは、 [共通のメタデータスキーマ](metadata-schemas.md) と [XMP](xmp-writeback.md).

### Other metadata {#other-metadata}

Other metadata that can be embedded from files include [!DNL Microsoft Word], [!DNL PowerPoint], [!DNL Excel], and so on.

## Metadata schemata {#metadata-schemata}

メタデータスキーマは、様々なアプリケーションで使用できる、定義済みのメタデータプロパティ定義のセットです。 プロパティは常にアセットに関連付けられます。つまり、プロパティはリソースに関する「概要」です。

必要に応じたメタデータスキーマが存在しない場合は、独自のメタデータスキーマを設計することもできます。 既存の情報を重複しない。 組織内でスキーマを分割すると、メタデータの共有が容易になります。 [!DNL Experience Manager] 最も頻繁に使用されるメタデータスキーマのデフォルトリストを提供します。 このリストを使用すると、メタデータ方法を急速に開始し、必要なメタデータプロパティをすばやく選択できます。

サポートされるメタデータスキーマを以下に示します。

### Standard metadata {#standard-metadata}

* DC - [!DNL Dublin Core] は、重要で広く使用されているメタデータのセットです。
* DICOM - Digital Imaging and Communications in Medicine.
* `Iptc4xmpCore` および `iptc4xmpExt` - International Press Communications Standardには、多くのサブジェクト固有のメタデータが含まれています。
* RDF - Resource Description Framework — 汎用セマンティックWebメタデータ用。
* XMP - [!DNL Extensible Metadata Platform].
* `xmpBJ`  — 基本的なジョブチケット発行。

### Application-specific metadata {#application-specific-metadata}

アプリケーション固有のメタデータは、技術的および説明的なメタデータを含む。 このようなメタデータを使用すると、他のアプリケーションがそのメタデータを使用できない場合があります。 例えば、別の画像レンダリングアプリケーションが [!DNL Adobe Photoshop] メタデータにアクセスできない場合があります。 アプリケーション固有のプロパティを標準プロパティに変更するワークフロー手順を作成できます。

* ACDSee - Metadata managed by the [!DNL ACDSee] program. www.acdsee.com/ [を参照してくだ](https://www.acdsee.com/)さい。
* アルバム — [!DNL Adobe Photoshop Album].
* CQ - Used by [!DNL Experience Manager Assets].
* DAM - Used by [!DNL Experience Manager Assets].
* DEX - [Optima SC Description explorer](http://www.optimasc.com/products/dex/index.html) は、Windowsオペレーティングシステム向けのメタデータおよびファイル管理のためのツールの集まりです。
* CRS - [Adobe Photoshop Camera Raw](https://helpx.adobe.com/camera-raw/using/introduction-camera-raw.html).
* LR - [!DNL Adobe Lightroom].
* MediaPro - [iView MediaPro](https://en.wikipedia.org/wiki/Phase_One_Media_Pro).
* MicrosoftPhotoおよびMP - Microsoft Photo。
* PDFおよびPDF/X
* PhotoshopとpsAux - [!DNL Adobe Photoshop].

### Digital Rights Management metadata {#digital-rights-management-metadata}

* CC - [!DNL Creative Commons].
* [!DNL XMPRights].
* PLUS - [Picture Licensing Universal System](https://www.useplus.com).
* PRISM - [Publishing Requirements for Industry Standard Metadata](https://www.idealliance.org/prism-metadata).
* PRL - PRISM Rights Language。
* PUR - PRISM Usage Rights。
* `xmpPlus` - PLUSとXMPの統合。

### Photography-specific metadata {#photography-specific-metadata}

* Exif - GPS位置など、カメラからの技術情報。
* CRS - [!DNL Camera Raw] スキーマ。
* `iptc4xmpCore` および `iptc4xmpExt`.
* TIFF — 画像メタデータ（TIFF画像のみではありません）。

### Print-specific metadata {#print-specific-metadata}

* PDFおよびPDF/X - Adobe PDFおよびサードパーティアプリケーション。
* PRISM - [Publishing Requirements for Industry Standard Metadata](https://www.prismstandard.org).
* XMP - [!DNL Extensible Metadata Platform].
* `xmpPG`  — ページテキストのXMPメタデータ。

### マルチメディア固有のメタデータ {#multimedia-specific-metadata}

* `xmpDM` - [!DNL Dynamic Media].
* `xmpMM`  — メディア管理。

## メタデータ駆動型のワークフロー {#metadata-driven-workflows}

メタデータ主導のワークフローを作成すると、一部のプロセスを自動化できるので、効率が向上します。 メタデータ駆動型のワークフローでは、ワークフロー管理システムでワークフローが読み取られ、その結果、事前定義された動作が実行されます。例として、メタデータ駆動型のワークフローの使用方法をいくつか示します。

* ワークフローは、画像にタイトルが付いているかどうかを確認できます。 タイトルが追加されない場合は、タイトルを追加するように通知されます。
* ワークフローは、アセットの著作権表示が配布を許可しているかどうかを確認できます。 したがって、システムはアセットを1台のサーバまたは他のサーバに送信します。
* ワークフローでは、定義済みの必須のメタデータがないアセット、または *無効なメタデータを持つアセットがないアセットを確認できます* 。

>[!MORELIKETHIS]
>
>* [複数コレクションのメタデータプロパティの編集](managing-collections-touch-ui.md#editing-collection-metadata-in-bulk)
>* [XMP メタデータ](xmp.md).
>* [メタデータの編集と追加](meta-edit.md).
>* [メタデータのスキーマに関する参照情報](meta-ref.md).

