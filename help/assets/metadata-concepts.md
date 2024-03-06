---
title: メタデータの概念について
description: アセットの分類と整理を容易にするメタデータの必要性とタイプについて説明します。
contentOwner: AG
role: User, Admin
feature: Metadata
exl-id: 312fff5f-39c1-48c1-aa99-40feb72c2f59
source-git-commit: abd3fbb5abb339d5b019fd2d7cf325404fb079e8
workflow-type: tm+mt
source-wordcount: '2665'
ht-degree: 81%

---

# メタデータの概念について {#why-we-need-metadata}

メタデータとは、データに関する情報のことです。この点に関して、データは、例えば画像などのデジタルアセットを指します。メタデータは、効率的なアセット管理を行うために重要です。

メタデータは、対象のアセットで使用できるすべてのデータのコレクションですが、次のようなデータはそのアセットに含まれているとは限りません。メタデータの例を以下に示します。

* アセットの名前。
* 最終変更の日時。
* リポジトリーに格納されたときのアセットのサイズ。
* アセットが含まれるフォルダーの名前。
* 関連するアセットまたは適用したタグ。

上記は、アセットに対して [!DNL Experience Manager] が管理できる基本的なメタデータプロパティです。これにより、ユーザーはすべてのアセットを表示できます。例えば、最終変更日にアセットを並べ替えると、最近追加したアセットを検出する場合に便利です。

デジタルアセットに、次のようなデータをさらに追加できます。

* アセットのタイプ（画像、ビデオ、オーディオクリップ、ドキュメントなど）。
* アセットの所有者。
* アセットのタイトル。
* アセットの説明。
* アセットに割り当てられたタグ。

メタデータが多いほど、アセットをより細かく分類でき、デジタル情報量が大きくなるにつれ便利です。数百個のファイルをファイル名だけに基づいて管理することは可能です。ただし、このアプローチは拡張性に欠けます。関係者の数や管理対象のアセット数が増えると不十分になります。

メタデータを追加すると、以下の理由からデジタルアセットの価値が大きくなります。

* アクセスが容易になる - システムやユーザーが簡単に見つけることができます。
* 管理しやすくなる - 一連の同じプロパティを持つアセットを容易に検索し、これらのアセットに変更を適用できます。
* 完全 - アセットは、より多くの情報とコンテキスト、より多くのメタデータを保持します。

したがって、[!DNL Assets] ではデジタルアセットのメタデータの作成、管理およびやり取りを行う適切な方法を提供します。

## メタデータのタイプ {#types-of-metadata}

メタデータの 2 つの基本的なタイプは、テクニカルメタデータと記述メタデータです。

テクニカルメタデータは、デジタルアセットを操作しているソフトウェアアプリケーションで役に立つもので、手動で管理できません。[!DNL Experience Manager Assets] と他のソフトウェアは、自動的にテクニカルメタデータを決定し、アセットが変更されるとメタデータが変更される場合があります。アセットで使用可能なテクニカルメタデータは、主にアセットのファイルタイプによって決まります。テクニカルメタデータの例を以下に示します。

* ファイルのサイズ。
* 画像の寸法（高さと幅）。
* オーディオまたはビデオファイルのビットレート。
* 画像の解像度（詳細レベル）。

記述メタデータは、アセットの元となるビジネスなど、アプリケーションドメインに関係するメタデータです。記述メタデータは自動的に決定できません。手動または半自動で作成されます。例えば、GPS 対応のカメラでは、緯度と経度を自動的に追跡し、画像に地理タグを追加できます。

記述メタデータ情報を手動で作成する場合のコストは高くなります。そのため、ソフトウェアシステムや組織間でのメタデータの交換を容易にするための基準が確立されています。[!DNL Experience Manager Assets] は、メタデータの管理に関連するすべての規格をサポートします。

## エンコーディング規格 {#encoding-standards}

メタデータをファイルに埋め込む方法は様々です。エンコーディング規格は、次の中から選択できます。

* XMP：[!DNL Assets] で抽出したメタデータをリポジトリーに格納するために使用されます。
* ID3：オーディオファイルおよびビデオファイル用の規格です。
* Exif：画像ファイル用の規格です。
* その他、従来の規格：[!DNL Microsoft Word]、[!DNL PowerPoint]、[!DNL Excel] など。

### XMP {#xmp}

[!DNL Extensible Metadata Platform]（XMP）は、すべてのメタデータ管理に対して [!DNL Experience Manager Assets] で使用されるオープンな標準です。XMP は、すべてのファイル形式に埋め込むことができる、ユニバーサルメタデータエンコーディングを提供します。アドビやその他の企業は、リッチコンテンツモデルを提供する XMP 標準をサポートしています。XMP 標準および [!DNL Experience Manager Assets] のユーザーは、基盤となる強力なプラットフォームを持っています。詳しくは、[XMP](https://www.adobe.com/products/xmp.html) を参照してください。

### ID3 {#id}

これらの ID3 タグに格納されたデータは、コンピューターまたはポータブル MP3 プレーヤーでデジタルオーディオファイルを再生すると表示されます。

ID3 タグは、MP3 ファイル形式用に設計されています。形式に関する追加情報：

* ID3 タグは、MP3 ファイルおよび mp3PRO ファイルで使用できます。
* WAV ではタグが使用されません。
* WMA には、オープンソースの実装を許可しない独自のタグがあります。
* Ogg Vorbis では、Ogg コンテナに埋め込まれた Xiph コメントを使用します。
* AAC では独自のタグ形式を使用します。

### Exif {#exif}

Exchangeable image file format（Exif）は、デジタル写真で最も一般的に使用されるメタデータフォーマットです。JPEG、TIFF、RIFF、WAV など、多くのファイル形式でメタデータプロパティの固定語彙を埋め込む方法を提供します。Exif によって、メタデータが、メタデータ名とメタデータ値のペアとして格納されます。 これらのメタデータの名前と値のペアはタグとも呼ばれます。タグと混同しないように、 [!DNL Experience Manager]. 最新のデジタルカメラは Exif メタデータを作成し、最新のグラフィックソフトウェアでサポートされています。Exif 形式は、特に画像に関するメタデータ管理で最も一般的な共通項です。

Exif の主な制限は、BMP、GIF、PNG などの一般的な画像ファイル形式ではサポートされないことです。

Exif で定義されるメタデータフィールドは、通常、テクニカルなもので、記述メタデータ管理では使用が制限されています。このため、[!DNL Experience Manager Assets] は Exif プロパティのマッピングを、[共通のメタデータスキーマ](metadata-schemas.md)と [XMP](xmp-writeback.md) に提供します。

### その他のメタデータ {#other-metadata}

ファイルから埋め込み可能なその他のメタデータには、[!DNL Microsoft Word]、[!DNL PowerPoint]、[!DNL Excel] などがあります。

## メタデータスキーマについて {#metadata-schemata}

メタデータスキーマは、メタデータプロパティの事前定義のセットで、様々なアプリケーションで使用できます。プロパティは常にアセットと関連付けられています。つまり、プロパティはリソースの「説明」です。

必要なメタデータスキーマが存在しない場合は、独自のメタデータスキーマを設計することもできます。既存の情報を重複しないようにします。組織内でスキーマを分割すると、メタデータを共有しやすくなります。[!DNL Experience Manager] は、最も頻繁に使用されるメタデータスキーマのデフォルトリストを提供します。このリストを使用すると、メタデータ戦略がすぐに開始でき、必要なメタデータプロパティをすばやく選択できます。

サポートされるメタデータスキーマを以下に示します。

### 標準的なメタデータ {#standard-metadata}

* DC - [!DNL Dublin Core] は、重要で広く使用されている一連のメタデータです。
* DICOM - Digital Imaging and Communications in Medicine。
* `Iptc4xmpCore` および `iptc4xmpExt` - International Press Communications Standard には、多くのサブジェクト固有のメタデータが含まれています。
* RDF - Resource Description Framework - 汎用のセマンティック Web メタデータ用。
* XMP - [!DNL Extensible Metadata Platform]。
* `xmpBJ` - Basic Job Ticketing。

### アプリケーション固有のメタデータ {#application-specific-metadata}

アプリケーション固有のメタデータには、テクニカルメタデータも記述メタデータも存在します。そのようなメタデータを使用する場合、他のアプリケーションでそのメタデータを使用することはできません。例えば、別の画像レンダリングアプリケーションが [!DNL Adobe Photoshop] メタデータにアクセスできない場合があります。アプリケーション固有のプロパティを標準プロパティに変更するワークフロー手順を作成できます。

* ACDSee - [!DNL ACDSee] プログラムで管理されるメタデータ。[www.acdsee.com/](https://www.acdsee.com/) を参照してください。
* Album - [!DNL Adobe Photoshop Album]。
* CQ - [!DNL Experience Manager Assets] で使用。
* DAM - [!DNL Experience Manager Assets] で使用。
* DEX - [!DNL Optima SC Description explorer] は、Windows オペレーティングシステム向けのメタデータおよびファイル管理向けのツールのコレクションです。
* CRS - [Adobe Photoshop Camera Raw](https://helpx.adobe.com/jp/camera-raw/using/introduction-camera-raw.html)。
* LR - [!DNL Adobe Lightroom]。
* MediaPro - [iView MediaPro](https://en.wikipedia.org/wiki/Phase_One_Media_Pro)。
* MicrosoftPhoto および MP - Microsoft Photo。
* PDF および PDF/X。
* Photoshop および psAux - [!DNL Adobe Photoshop]。

### Digital Rights Management (DRM) メタデータ {#digital-rights-management-metadata}

* CC - [!DNL Creative Commons]。
* [!DNL XMPRights]。
* PLUS - [Picture Licensing Universal System](https://www.useplus.com)。
* PRISM - [Publishing Requirements for Industry Standard Metadata](https://www.w3.org/submissions/2020/SUBM-prism-20200910/Image_Guide.pdf)。
* PRL - PRISM Rights Language。
* PUR - PRISM Usage Rights。
* `xmpPlus` - PLUS と XMP の統合。

### 写真固有のメタデータ {#photography-specific-metadata}

* Exif - GPS 位置など、カメラからのテクニカル情報。
* CRS - [!DNL Camera Raw] スキーマ。
* `iptc4xmpCore` および `iptc4xmpExt`。
* TIFF - 画像メタデータ（TIFF 画像に限らない）。

### 印刷固有のメタデータ {#print-specific-metadata}

* PDF および PDF/X - Adobe PDF およびサードパーティのアプリケーション。
* PRISM - [Publishing Requirements for Industry Standard Metadata](https://www.w3.org/submissions/2020/SUBM-prism-20200910/Image_Guide.pdf)。
* XMP - [!DNL Extensible Metadata Platform]。
* `xmpPG` - ページテキストの XMP メタデータ。

### マルチメディア固有のメタデータ {#multimedia-specific-metadata}

* `xmpDM` - [!DNL Dynamic Media]。
* `xmpMM` - メディア管理。

## メタデータのスキーマに関する参照情報 {#metadata-schemata-reference}

次のリファレンスでは、特定のメタデータスキーマに関する情報（アルファベット順）と、プロパティとその定義のリストを示します。

### Dublin Core {#dublin-core}

Dublin Core メタデータは、アセットをより検索しやすい形で記述できるように、標準化された規則のセットを提供します。[!DNL Assets] では、ビデオ、音楽、画像、ドキュメントなどのデジタルアセットが Dublin Core で記述されます。

シンプルな DCMES(Dublin Core Metadata Element Set) には、次の表に示す 15 個のメタデータ要素が含まれています。 各 Dublin Core 要素はオプションで、繰り返し使用できます。 Dublin Core メタデータ情報は、メディアタイプ固有のメタデータと同様に追加または削除できます。

DCMES に加えて、Dublin Core Initiative によって作成された他のメタデータ要素もあります。 詳しくは、 [Dublin Core イニシアティブ](https://dublincore.org/) を参照してください。

| Property | 説明 |
| ----------- | ------------------------------------------------------------------------------------------------------------------------ |
| contributor | コンテンツに貢献する責任を負う人または会社。 |
| 対象範囲 | アセットの対象となる地理的な場所または期間。 |
| 作成者 | コンテンツの作成を担当する人または会社。 |
| date | アセットに関連付けられた日付または期間。 |
| description | アセットに関する詳細情報。 |
| format | アセットのファイル形式、物理メディア、またはサイズ。 [!DNL Experience Manager] では、`dc:format` を使用してアセットの MIME タイプを示します。 |
| 識別子 | アセットへの一意の参照。 |
| language | アセットの言語（英語の場合は `en` など）。 |
| 媒体社 | アセットを使用可能にする人または会社。 |
| relation | 関連するアセット。 |
| 権限 | このアセットに対する権限を持つユーザーに関する情報。 |
| ソース | アセットの派生元となる関連アセット。 |
| subject | アセットのトピック。 |
| title | アセットの名前。 |
| type | アセットの特性またはジャンル。 |

### IPTC {#iptc}

IPTC は、世界中の通信機関のコンソーシアムで、技術基準の開発と維持を目標の 1 つとしています。 IPTC は、写真家の間でほぼ一般的に受け入れられる画像に対する一連の写真メタデータ規格を定義しました。 これらのメタデータ規格は、1990 年代に作成された IPTC Information Interchange Model(IIM) と呼ばれるより広範な規格の一部でした。

IPTC ヘッダー情報はほとんどXMPに置き換えられましたが、XMPでは IPTC コアスキーマと拡張スキーマを使用できます。 イメージプログラムでは、XMPと IPTC の両方のプロパティが同期されます。

## メタデータ駆動型のワークフロー {#metadata-driven-workflows}

メタデータ駆動型のワークフローを作成することで、一部のプロセスを自動化し、効率性を高めることができます。メタデータ駆動型のワークフローでは、ワークフロー管理システムでワークフローが読み取られ、その結果、事前定義された動作が実行されます。例として、メタデータ駆動型のワークフローの使用方法をいくつか示します。

* ワークフローで画像にタイトルがあるかチェックできます。タイトルがない場合、システムはタイトルを追加するよう通知します。
* ワークフローでアセットの著作権情報によって配布が許可されているかをチェックできます。そのため、システムはアセットを 1 台のサーバーまたは他のサーバーに送信します。
* ワークフローでは、定義済みの必須のメタデータがないアセット、または&#x200B;*無効な*&#x200B;メタデータを持つアセットがないことを確認できます。

## XMP メタデータ {#xmp-metadata}

XMP（Extensible Metadata Platform）は、[!DNL Adobe Experience Manager Assets] であらゆるメタデータ管理に使用されるメタデータ規格です。XMP で提供される標準形式によって、多様なアプリケーションに対応したメタデータの作成、処理およびやり取りができます。

XMP では、すべてのファイル形式に埋め込むことができる共通のメタデータエンコーディングのほか、リッチ[コンテンツモデル](#xmp-core-concepts)も提供され、[アドビによるサポート](#advantages-of-xmp)やその他各社のサポートがあるので、XMP を と組み合わせて使用すると強力なプラットフォームを構築できます。[!DNL Assets]

[XMP の仕様](https://www.adobe.com/devnet/xmp.html)は、アドビから入手できます。

### XMP とは {#what-is-xmp}

XMP 規格は、アドビが初めて Adobe Acrobat ソフトウェア製品の一部として導入しました。それ以降、XMP 規格が広く採用されてきました。[!DNL Assets] は、アドビ主導の XMP（Extensible Metadata Platform）をネイティブでサポートしています。XMP は、デジタルアセット内の標準化されたメタデータと独自メタデータを処理および格納するための規格です。XMP は、複数のアプリケーションでメタデータを効率的に使用するための共通規格となるよう設計されています。

例えば制作のプロフェッショナルは、アドビのアプリケーションに組み込まれた XMP サポートを使用して、複数のファイル形式に情報を渡します。[!DNL Assets] リポジトリでは、XMP メタデータを抽出し、そのデータをコンテンツのライフサイクルの管理に使用します。自動化ワークフローを作成することもできます。

XMP は、データモデル、ストレージモデル、スキーマを提供することで、メタデータの定義、作成および処理方法を標準化します。これらの概念はすべて、この節で説明します。

従来のメタデータ（EXIF、ID3、Microsoft Office など）はすべて XMP に自動変換され、製品カタログなどの顧客固有のメタデータスキーマをサポートするよう拡張できます。

XMP のメタデータは、一連のプロパティで構成されます。これらのプロパティは、常にリソースと呼ばれる特定のエンティティに関連付けられます。つまり、プロパティはリソースの「説明」です。 XMPがある場合、リソースは常にアセットです。

### XMP のエコシステム {#xmp-ecosystem}

XMP によって定義される[メタデータ](https://en.wikipedia.org/wiki/Metadata)モデルは、任意の定義済みメタデータ項目のセットと併用できます。また、XMP によって、リソースで複数の処理手順が行われる際にその履歴を記録するうえで便利な基本的なプロパティに対して、特定の[スキーマ](https://en.wikipedia.org/wiki/XML_schema)も定義されます。処理手順は、撮影、[スキャン](https://en.wikipedia.org/wiki/Image_scanner)またはテキスト作成から、画像編集手順（[切り抜き](https://en.wikipedia.org/wiki/Cropping_%28image%29)やカラー調整など）を経て、最終的な画像へのアセンブリまでです。XMP の処理中に、各ソフトウェアプログラムまたはデバイスでデジタルリソースに独自の情報を付加できます。この情報は、最終的なデジタルファイルで保持されます。

XMP のシリアライズおよび格納は、通常 [W3C](https://ja.wikipedia.org/wiki/World_Wide_Web_Consortium) [Resource Description Framework](https://ja.wikipedia.org/wiki/Resource_Description_Framework)（RDF）のサブセットを使用して実行され、[XML](https://ja.wikipedia.org/wiki/XML) で表記されます。

### XMP の利点 {#advantages-of-xmp}

XMP には、他のエンコーディング規格やスキーマと比較して次の利点があります。

* XMP ベースのメタデータは利便性が高く、細かく分類されています。
* XMP では 1 つのプロパティに複数の値を指定できます。
* XMP には標準化されたエンコーディングがあるので、メタデータを簡単に交換できます。
* XMP は拡張可能です。 アセットに詳細情報を追加できます。

XMP 標準は拡張可能に設計されており、カスタムタイプのメタデータを XMP データに追加できます。一方、EXIF のプロパティのリストは固定されていて、拡張することはできません。

>[!NOTE]
>
>XMP では通常、バイナリデータ型を埋め込むことはできません。XMP でバイナリデータ（サムネール画像など）を扱う場合、XML に対応するフォーマット（`Base64` など）でエンコーディングする必要があります。

### XMP の概念 {#xmp-core-concepts}

次の節では、名前空間とスキーマ、プロパティと値、代替言語など、XMP の中心概念について説明します。

#### 名前空間とスキーマ {#namespaces-and-schemata}

XMP スキーマは、一連のプロパティ名を共通の XML 名前空間で定義したものです。
名前空間には、データタイプや識別情報が含まれます。XMP スキーマは、そのスキーマの XML 名前空間 URI によって識別されます。名前空間を使用すると、異なるスキーマに存在する、名前が同じで意味が異なるプロパティとの競合を防ぐことができます。

例えば、別個に設計された 2 つのスキーマにある `Creator` プロパティは、アセットを作成した個人を意味する場合と、アセットの作成元アプリケーション（Adobe Photoshop など）を意味する場合があります。

#### プロパティと値 {#properties-and-values}

XMP には、1 つ以上のスキーマからプロパティを選択し含めることができます。多くのアドビアプリケーションで使用される一般的なサブセットに含まれるプロパティの例を示します。

* Dublin Core スキーマ： `dc:title`, `dc:creator`, `dc:subject`, `dc:format`, `dc:rights`.
* XMP 基本スキーマ：`xmp:CreateDate`、`xmp:CreatorTool`、`xmp:ModifyDate`、`xmp:metadataDate`
* XMP Rights Management スキーマ：`xmpRights:WebStatement`、`xmpRights:Marked`
* XMP Media Management スキーマ：`xmpMM:DocumentID`

#### 代替言語 {#language-alternatives}

XMP には、`xml:lang` プロパティをテキストプロパティに追加して、テキストの言語を指定する機能があります。

## IPTC メタデータの活用 {#support-for-iptc-metadata}

[!DNL Adobe Experience Manager Assets] が [!DNL Adobe Bridge] やその他の [!DNL Adobe Creative Cloud] アプリを通じてアセットに追加された IPTC メタデータ、クリエイティブの評価、キーワードをサポートする方法について説明します。

[!DNL Adobe Experience Manager Assets] では、アセットの記述に広く利用されている IPTC メタデータ標準をサポートしています。このように [!DNL Assets] では、フォトグラファー、クリエイティブエージェンシー、ライブラリ、ミュージアムなど、様々な関係者間で画像を受け入れる仕組みを強化しています。

アセットのデフォルトのメタデータスキーマに IPTC Core と IPTC 拡張のメタデータスキーマが組み込まれ、画像に表示される人、場所、製品に関する正確で信頼性の高いデータを追加できる、包括的なメタデータプロパティを定義できるようになりました。 また、画像の作成に関する日付、名前、識別子、および権限情報を柔軟に表す方法もサポートしています。

アセットのプロパティページに、 IPTC コアおよび IPTC 拡張メタデータを編集可能フィールドに表示するための個別のタブが含まれるようになりました。

1. [!DNL Assets] ユーザーインターフェイスで画像を選択します。
1. ツールバーの「**[!UICONTROL プロパティ]**」をクリックします。
1. **[!UICONTROL IPTC]** タブをクリックして、アセットの IPTC メタデータを表示します。
1. 必要に応じて、IPTC メタデータのプロパティを編集します。

   ![iptc_tab](assets/keywords-in-iptc-tab.png)

1. 「**[!UICONTROL IPTC 拡張]**」タブをクリックして、アセットの IPTC 拡張メタデータを表示します。
1. 必要に応じて、IPTC 拡張メタデータのプロパティを編集します。
1. 「**[!UICONTROL 保存して閉じる]**」をクリックして、変更内容を保存します。

### クリエイティブの評価のサポート {#creative-rating-support}

プロパティページには、個々のユーザーの評価と総評価が表示されるほか、Adobe Bridge およびその他のクリエイティブアプリを通じてアセットに割り当てられた評価も表示されるようになりました。

これらの評価は、「**[!UICONTROL 詳細]**」タブ内の「**[!UICONTROL クリエイティブの評価]**」セクションの下に表示されます。

この評価は読み取り専用のプロパティで、1 ～ 5 の範囲です。 検索パネルで、クリエイティブの評価に基づいてアセットを検索できます。

ただし、ユーザーが行ったカスタムの変更との競合を避けるために、現在、このプロパティのインデックスは作成されていません。

### キーワードのサポート {#keyword-support}

[!UICONTROL プロパティ]ページの「**[!UICONTROL IPTC]**」タブには、Adobe Bridge とその他の Adobe Creative Cloud アプリを通じてアセットに追加したキーワードも表示されます。これらのキーワードの編集や、キーワードの追加も「**[!UICONTROL IPTC]**」タブでおこなえます。

![keywords](assets/keywords-in-iptc-tab.png)
