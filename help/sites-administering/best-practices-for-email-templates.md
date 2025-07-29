---
title: メールテンプレートのベストプラクティス
description: AEM でメールテンプレートの作成に関するベストプラクティスについて学習します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration, best-practices
content-type: reference
docset: aem65
exl-id: 6666eddc-dc17-4bd4-9d55-e6522f40a680
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
index: false
source-git-commit: 389d5fa8de320a7237fc8290992a33743b15db99
workflow-type: ht
source-wordcount: '1072'
ht-degree: 100%

---


# メールテンプレートのベストプラクティス {#best-practices-for-email-templates}

>[!CAUTION]
>
>この記事は、非推奨である基盤コンポーネントベースの AEM 電子メールコンポーネントを対象としています。
>
>最新の[コアコンポーネントのメールコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/email/introduction.html?lang=ja)を使用することが推奨されています。

このドキュメントでは、適切なメールキャンペーンテンプレートを作成するための、メールデザインに関するいくつかのベストプラクティスについて説明します。

AEM で利用可能なデモキャンペーンは、これらすべてのベストプラクティスに従っています。デモキャンペーンでのベストプラクティスの実装方法は、各ベストプラクティスで説明しています。

自分のニュースレターを作成する際には、これらのベストプラクティスを使用してください。

>[!NOTE]
>
>すべてのキャンペーンコンテンツは、`master` タイプのページ `cq/personalization/components/ambitpage` の下に作成してください。
>
>例えば、予定されているキャンペーン構造が次のような場合
>
>`/content/campaigns/teasers/en/campaign-promotion-global`
>
>`master` ページの下に格納するようにします
>
>`/content/campaigns/teasers/master/en/campaign-promotion-global`

>[!NOTE]
>
>Adobe Campaign のメールテンプレートを作成する際には、テンプレートの **jcr:content** ノードでプロパティ **acMapping** と値 **mapRecipient** を指定する必要があります。 指定しない場合、Experience Manager の&#x200B;**ページのプロパティ**&#x200B;フィールドで Adobe Campaign のテンプレートを選択できなくなります（フィールドが無効化されています）。

## テンプレート／ページコンポーネント {#template-page-component}

***/libs/mcm/campaign/components/campaign_newsletterpage***

<table>
 <tbody>
  <tr>
   <td><strong>ベストプラクティス</strong></td>
   <td><strong>実装</strong></td>
  </tr>
  <tr>
   <td><p>ドキュメントタイプを指定して、レンダリングの一貫性を確保します。</p> <p>先頭に DOCTYPE を追加します（HTML または XHTML）。</p> </td>
   <td><p><i>"/etc/designs/default/jcr:content/campaign_newsletterpage"</i> にある <i>cq:doctype</i> プロパティを変更することで、デザインでの設定が可能になります。</p> <p>デフォルトは、"XHTML" です。</p> <p>&lt;!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional/EN" "https://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd"&gt;</p> <p>「HTML_5」に変更できます。</p> <p>&lt;!DOCTYPE HTML&gt;</p> </td>
  </tr>
  <tr>
   <td><p>文字定義を指定して、特殊文字の正確なレンダリングを確保します。</p> <p>CHARSET 定義（例：iso-8859-15、UTF-8）を &lt;head&gt; に追加します。</p> </td>
   <td><p>UTF-8 に設定します。</p> <p>&lt;meta http-equiv="content-type" content="text/html; charset=UTF-8"&gt;</p> </td>
  </tr>
  <tr>
   <td><p>&lt;table&gt;element を使用してすべての構造をコーディングします。より複雑なレイアウトの場合、テーブルをネストして複雑な構造を構築します。</p> <p>メールは、css なしでも見やすくする必要があります。</p> </td>
   <td><p>コンテンツを構造化するためにテンプレート全体でテーブルが使用されます。現在のところ、最大で 4 つのネストされたテーブルを使用しています（1 つの基本テーブル + 最大 3 つのネストレベル）。</p> <p>「&lt;div&gt;」タグは、適切なコンポーネント編集を確実におこなうために、オーサーモードでのみ使用されます。</p> </td>
  </tr>
  <tr>
   <td>要素の属性（cellpadding、valign、width など）を使用してテーブルの寸法を設定します。このメソッドは、ボックスモデル構造を強制します。</td>
   <td><p>すべてのテーブルには、<i>border</i>、<i>cellpadding</i>、<i>cellspacing</i>、<i>width</i> など、必要な属性が含まれています。</p> <p>テーブル内の要素の位置を調和させるために、すべてのテーブルのセルには、属性 <i>valign="top"</i> が設定されています。</p> </td>
  </tr>
  <tr>
   <td><p>可能であれば、モバイルでの使いやすさを考慮します。メディアクエリを使用して、小さい画面でのテキストサイズを大きくして、リンク用に親指サイズのヒット領域を提供します。</p> <p>デザイン面で可能であれば、メールをレスポンシブにします。</p> </td>
   <td>CSS スタイルがデモデザインの説明で使用されている限り、メディアクエリを使用してモバイルフレンドリーなバージョンを提供します。</td>
  </tr>
  <tr>
   <td>すべての CSS を最初に配置するよりも、インライン CSS が優れています。</td>
   <td><p>基盤となる HTML 構造をより効果的に表し、ニュースレターの構造をカスタマイズしやすくするには、一部の CSS 定義のみをインラインにします。</p> <p>ベーススタイルおよびテンプレートのバリエーションは、ページの &lt;head&gt; にあるスタイルブロックに抽出されています。ニュースレターの最終版では、これらの CSS 定義は、HTML にインライン化されています。自動インライン化メカニズムは予定されていますが、現在は利用できません。</p> </td>
  </tr>
  <tr>
   <td>CSS をシンプルに保ちます。複合スタイル宣言、短縮形コード、CSS レイアウトプロパティ、複雑なセレクターおよび疑似要素を避けます。</td>
   <td>CSS スタイルがデモデザインの説明で使用されている限り、CSS のレコメンデーションは次のようになります。</td>
  </tr>
  <tr>
   <td>メールの幅は、最大 600 ～ 800 pixel にする必要があります。このサイズ設定により、多くのクライアントで提供されるプレビューパネルのサイズ内で動作を向上します。</td>
   <td>デモデザインでは、コンテンツテーブルの<i>幅</i>は、600 pixel に制限されています。</td>
  </tr>
 </tbody>
</table>

### 画像 {#images}

/libs/mcm/campaign/components/image

| **ベストプラクティス** | **実装** |
|---|---|
| 画像に *alt* 属性を追加します。 | *alt* 属性は、画像コンポーネントに必須なものとして定義されています。 |
| 画像に *png* の代わりに *jpg* 形式を使用します。 | 画像は、画像コンポーネントでは、常に、JPG として提供されます。 |
| テーブルの背景画像の代わりに `<img>` 要素を使用します。 | テンプレートでは、背景画像データは使用されていません。 |
| 写真に style=&quot;display block&quot; 属性を追加します。これにより、Gmail での表示を向上できます。 | すべての画像には、デフォルトで *style=&quot;display block&quot;* 属性が含まれています。 |

### テキストとリンク {#text-and-links}

/libs/mcm/campaign/components/heading, /libs/mcm/campaign/components/textimage

<table>
 <tbody>
  <tr>
   <td><strong>ベストプラクティス</strong></td>
   <td><strong>実装</strong></td>
  </tr>
  <tr>
   <td>CSS（フォントファミリー）でのスタイルの代わりに html &lt;font&gt; を使用します</td>
   <td>RichTextEditor（例：textimage コンポーネントに含まれるもの）は、選択したテキストへのフォントファミリーおよびフォントサイズの選択および適用をサポートするようになりました。これらの設定は、&lt;font&gt; タグとしてレンダリングされます。</td>
  </tr>
  <tr>
   <td><i>Arial®、Verdana、Georgia</i> および <i>Times New Roman®</i> など、基本的な、クロスプラットフォーム対応フォントを使用します。</td>
   <td><p>ニュースレターのデザインによって異なります。</p> <p>デモデザインでは、Helvetica® フォントが使用されますが、存在しない場合は一般的なサンセリフフォントに戻ります。</p> </td>
  </tr>
 </tbody>
</table>

### 一般 {#generic}

| **ベストプラクティス** | **実装** |
|---|---|
| W3C バリデーターを使用して、HTML コードを修正します。すべての開始タグが適切に閉じられるようにします。 | コードは検証されました。XHTML transitional Doctype でのみ、`<html>` 要素で欠落する xmlns 属性が見つかりません。 |
| JavaScript や Flash を使用しないでください。これらのテクノロジーは、大部分のメールクライアントでサポートされません。 | JavaScript や Flash は、ニュースレターテンプレートでは使用していません。 |
| マルチパート送信では、プレーンテキストバージョンを追加します。 | 新しいウィジェットは、ページプロパティに組み込まれ、ページコンテンツからプレーンテキストを簡単に抽出できます。これは、最終的なプレーンテキストバージョンの開始点として使用できます。 |

## キャンペーンニュースレターのテンプレートと例 {#campaign-newsletter-templates-and-examples}

AEM には、キャンペーンニュースレターを作成するためのいくつかのテンプレートおよびコンポーネントが標準で付属しています。これらのテンプレートおよびコンポーネントを使用して、カスタムのニュースレターを作成できます。

### テンプレート {#templates}

基盤を提供し、様々なコンテンツの流れを可能にするために、3 つの少しずつ違ったテンプレートのタイプが標準で用意されています。これら 3 つのタイプを使用して、カスタムニュースレターを簡単に作成できます。

すべてに **header**、**footer** および **body** セクションがあります。次に示すのは body セクションです。各テンプレートの&#x200B;**列デザイン**&#x200B;はそれぞれ異なります（1、2 または 3 列）。

![可能なニュースレターのバリアント](assets/chlimage_1-69.png)

### コンポーネント {#components}

現在[キャンペーンテンプレート内で使用できる 7 つのコンポーネント](/help/sites-authoring/adobe-campaign-components.md)があります。これらのコンポーネントは、すべて Adobe マークアップ言語 **HTL** に基づいています。

| **コンポーネント名** | **コンポーネントのパス** |
|---|---|
| 見出し | /libs/mcm/campaign/components/heading |
| 画像 | /libs/mcm/campaign/components/image |
| テキストおよびパーソナライゼーション | /libs/mcm/campaign/components/personalization |
| Textimage | /libs/mcm/campaign/components/textimage |
| リンク | /libs/mcm/campaign/components/reference |
| Dynamic Media Classic（旧称Scene7）の画像テンプレート | /libs/mcm/campaign/s7image |
| ターゲット参照 | /libs/mcm/campaign/components/reference |

>[!NOTE]
>
>これらのコンポーネントは、メールコンテンツ用に最適化されています。つまり、このドキュメントで概要を説明しているベストプラクティスに従います。その他の標準コンポーネントを使用すると、通常、これらのルールに違反します。

これらのコンポーネントについて詳しくは、[Adobe Campaign コンポーネント](/help/sites-authoring/adobe-campaign-components.md)を参照してください。
