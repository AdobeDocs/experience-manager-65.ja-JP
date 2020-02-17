---
title: AEM AssetsでのXMPメタデータのサポート
description: AEM Assets でメタデータ管理において使用される XMP（Extensible Metadata Platform）メタデータ規格について説明します。XMP で提供される標準形式によって、多様なアプリケーションに対応したメタデータの作成、処理およびやり取りができます。
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# XMP メタデータ {#xmp-metadata}

XMP（Extensible Metadata Platform）は、AEM Assets であらゆるメタデータ管理に使用されるメタデータ規格です。XMP で提供される標準形式によって、多様なアプリケーションに対応したメタデータの作成、処理およびやり取りができます。

Aside from offering universal metadata encoding that can be embedded into all file formats, XMP provides a rich [content model](xmp.md#xmp-core-concepts) and is [supported by Adobe](xmp.md#advantages-of-xmp) and other companies, so that users of XMP in combination with AEM Assets have a powerful platform to build upon.

[XMP の仕様](https://www.adobe.com/devnet/xmp.html)は、アドビから入手できます。

## What is XMP? {#what-is-xmp}

AEM Assets は、アドビ主導の XMP（Extensible Metadata Platform）をネイティブでサポートしています。XMP は、デジタルアセット内の標準化されたメタデータと独自メタデータを処理および格納するための規格です。XMP は、複数のアプリケーションでメタデータを効率的に使用するための共通規格となるよう設計されています。

例えば制作のプロフェッショナルは、アドビのアプリケーションに組み込まれた XMP サポートを使用して、複数のファイル形式に情報を渡します。AEM Assets リポジトリでは、XMP メタデータを抽出し、そのデータをコンテンツのライフサイクルの管理に使用します。自動化ワークフローを作成することもできます。

XMP が提供するデータモデル、ストレージモデルおよびスキーマを使用して、メタデータの定義、作成および処理方法を規格化できます。これらの概念は、すべてこの節で説明します。

EXIF、ID3、Microsoft Office などの従来のメタデータは、すべて自動的に XMP に解釈され、製品カタログなどの顧客固有のメタデータスキーマをサポートするよう拡張することができます。

XMP のメタデータは、一連のプロパティで構成されます。これらのプロパティは、常にリソースとして参照される特定のエンティティに関連付けられます。つまり、プロパティはリソースの「説明」です。XMP の場合、リソースとなるのは常にアセットです。

### アドビ {#adobe}

XMP 規格は、アドビが初めて Adobe Acrobat ソフトウェア製品の一部として導入しました。それ以降、XMP 規格が広く採用されてきました。

### XMP ecosystem {#xmp-ecosystem}

XMP によって定義される[メタデータ](https://en.wikipedia.org/wiki/Metadata)モデルは、任意の定義済みメタデータ項目のセットと併用できます。また、XMP によって、リソースで複数の処理手順がおこなわれる際にその履歴を記録する上で便利な基本的なプロパティに対して、特定の[スキーマ](https://en.wikipedia.org/wiki/XML_schema)も定義されます。処理手順は、撮影、[スキャン](https://en.wikipedia.org/wiki/Image_scanner)またはテキスト作成から、画像編集手順（[切り抜き](https://en.wikipedia.org/wiki/Cropping_%28image%29)やカラー調整など）を経て、最終的な画像へのアセンブリまでです。XMP の処理中に、各ソフトウェアプログラムまたはデバイスでデジタルリソースに独自の情報を付加できます。この情報は、最終的なデジタルファイルで保持されます。

XMP のシリアライズおよび格納は、通常 [W3C](https://en.wikipedia.org/wiki/World_Wide_Web_Consortium) [Resource Description Framework](https://en.wikipedia.org/wiki/Resource_Description_Framework)（RDF）のサブセットを使用して実行され、[XML](https://en.wikipedia.org/wiki/XML) で表記されます。

## XMP の利点 {#advantages-of-xmp}

XMP には、他のエンコーディング規格およびエンコーディングスキーマに比べて次の利点があります。

* XMP ベースのメタデータは利便性が高く、細かく分類されています。   
* XMP では 1 つのプロパティに複数の値を指定できます。
* XMP の規格化されたエンコーディングによって、メタデータを簡単にやり取りできます。
* XMP は拡張可能です。アセットに追加情報を追加できます。

### 拡張可能 {#extensible}

XMP 規格は拡張できるように設計されていて、カスタムタイプのメタデータを XMP データに追加できます。一方、EXIF は拡張できません。EXIF のプロパティのリストは固定されていて、拡張することはできません。

>[!NOTE]
>
>XMP では通常、バイナリデータタイプを埋め込むことはできません。To carry binary data in XMP, for example, thumbnail images, they must be encoded in an XML-friendly format such as `Base64`.

## XMP の中心概念 {#xmp-core-concepts}

次の節では、名前空間とスキーマ、プロパティと値、代替言語など、XMP の中心概念について説明します。

### 名前空間とスキーマ {#namespaces-and-schemata}

XMP スキーマは、一連のプロパティ名を共通の XML 名前空間で定義したものです。
名前空間には、データタイプや識別情報が含まれます。XMP スキーマは、そのスキーマの XML 名前空間 URI によって識別されます。名前空間を使用すると、異なるスキーマに存在する、名前が同じで意味が異なるプロパティとの競合を防ぐことができます。

例えば、別個に設計された 2 つのスキーマにある `Creator` プロパティは、アセットを作成した個人を意味する場合と、アセットの作成元アプリケーション（Adobe Photoshop など）を意味する場合があります。

### プロパティと値 {#properties-and-values}

XMP には、1 つ以上のスキーマからプロパティを選択し含めることができます。

多くのアドビアプリケーションで使用される一般的なサブセットに含まれるプロパティの例を示します。

* Dublin Core スキーマ：dc:title、dc:creator、dc:subject、dc:format、dc:rights
* XMP 基本スキーマ：xmp:CreateDate、xmp:CreatorTool、xmp:ModifyDate、xmp:metadataDate
* XMP Rights Management スキーマ：xmpRights:WebStatement、xmpRights:Marked
* XMP Media Management スキーマ：xmpMM:DocumentID

### 代替言語 {#language-alternatives}

XMP には、`xml:lang` プロパティをテキストプロパティに追加して、テキストの言語を指定する機能があります。
