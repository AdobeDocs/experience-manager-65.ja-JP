---
title: メタデータのスキーマに関する参照情報
description: 'Dublin Core、IPTC などのメタデータのスキーマを含め、アセットメタデータを記述する際の標準規則を学習します。 '
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5f3af7041029a1b4dd1cbb4c65bd488b62c7e10c
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 93%

---


# メタデータのスキーマに関する参照情報 {#metadata-schemata-reference}

次のリファレンスでは、一部のメタデータスキーマに関する情報（アルファベット順）と、プロパティおよびその定義のリストを示します。

## Dublin Core {#dublin-core}

Dublin Core メタデータは、アセットをより検索しやすい形で記述できるように、標準化された規則のセットを提供します。AEM Assets では、ビデオ、音楽、画像、ドキュメントなどのデジタルアセットが Dublin Core で記述されます。

シンプルな Dublin Core Metadata Element Set（DCMES）には、以下の表に示すように、15 個のメタデータ要素が含まれます。それぞれの Dublin Core 要素はオプションであり、繰り返し可能です。Dublin Core メタデータ情報は、メディアタイプ固有のメタデータと同様に、削除および追加が可能です。

In addition to the DCMES, there are other metadata elements created by the Dublin Core Initiative. See the [Dublin Core initiative](https://dublincore.org/) for more information.

| プロパティ | 説明 |
| ----------- | ------------------------------------------------------------------------------------------------------------------------ |
| contributor | コンテンツに貢献する責任を負う人または会社。 |
| coverage | アセットの対象となる地理的な場所または期間。 |
| creator | コンテンツを作成する責任を負う人または会社。 |
| date | アセットに関連付けられた日付または期間。 |
| description | アセットの詳細。 |
| format | アセットのファイル形式、物理的な媒体またはサイズ。AEM では、`dc:format` を使用してアセットの MIME タイプを示します。 |
| identifier | アセットの一意の参照。 |
| language | アセットの言語（英語の場合は en、など）。 |
| publisher | アセットを使用可能にする責任を負う人または会社。 |
| relation | 関連アセット。 |
| rights | このアセットに対して権限を持つ者に関する情報。 |
| source | アセットの派生元の関連アセット。 |
| subject | アセットのトピック。 |
| title | アセットの名前。 |
| type | アセットの性質またはジャンル。 |

## IPTC {#iptc}

IPTC（International Press Telecommunications Council）は各国の通信社による協会で、技術的な規格の開発および管理を目的とします。IPTC によって定義された、画像向けの一連のフォトメタデータ標準は、フォトグラファーの間で一般的に広く受け入れられています。これらメタデータ標準は、IPTC Information Interchange Model（IIM）として知られる、1990 年代に制定されたより広範な標準の一部です。

IPTC のヘッダー情報は、ほとんどが XMP に置き換わりましたが、IPTC のコアスキーマと拡張スキーマは XMP で利用可能です。画像プログラムでは、XMP と IPTC のプロパティは同期されます。
