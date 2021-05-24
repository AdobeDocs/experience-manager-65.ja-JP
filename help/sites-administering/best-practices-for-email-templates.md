---
title: 電子メールテンプレートのベストプラクティス
seo-title: 電子メールテンプレートのベストプラクティス
description: AEM での電子メールテンプレートの作成に関するベストプラクティスについて学習します。
seo-description: AEM での電子メールテンプレートの作成に関するベストプラクティスについて学習します。
uuid: 07417a63-7ca6-484c-b55d-57b319428329
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration, best-practices
content-type: reference
discoiquuid: 2418777e-4eb2-4d82-aa9e-8d1b0bf740f3
docset: aem65
exl-id: 6666eddc-dc17-4bd4-9d55-e6522f40a680
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1130'
ht-degree: 63%

---

# 電子メールテンプレートのベストプラクティス {#best-practices-for-email-templates}

>[!CAUTION]
>
>AEM Eメールコンポーネントは非推奨（廃止予定）となりました。 コンテンツとスタイルを結合するEメールの性質上、AEMで標準で提供されるEメールコンポーネントは、プロジェクトに必要なあらゆるコンポーネントにカスタムスタイルを実装する必要があるので、再利用が制限されます。
>
>電子メールコンポーネントはプロジェクトレベルで実装でき、非推奨（廃止予定）のAEM電子メールコンポーネントではその方法が示されています。 ただし、これらの非推奨コンポーネントはプロジェクトでは使用しないでください。

このドキュメントでは、適切な電子メールキャンペーンテンプレートを作成するための、電子メールデザインに関するいくつかのベストプラクティスについて説明します。

AEM で利用可能なデモキャンペーンは、これらすべてのベストプラクティスに従っています。デモキャンペーンでのベストプラクティスの実装方法は、各ベストプラクティスで説明しています。

独自のニュースレターを作成する際に、これらのベストプラクティスを利用してください。

>[!NOTE]
>
>すべてのキャンペーンコンテンツは、タイプ`cq/personalization/components/ambitpage`の`master`ページの下に作成する必要があります。
>
>例えば、計画されているキャンペーン構造が
>
>`/content/campaigns/teasers/en/campaign-promotion-global`
>
>`master`ページの下に配置されていることを確認する必要があります
>
>`/content/campaigns/teasers/master/en/campaign-promotion-global`

>[!NOTE]
>
>Adobe Campaignのメールテンプレートを作成する場合、テンプレートの&#x200B;**jcr:content**&#x200B;ノードに&#x200B;**mapRecipient**&#x200B;の値を持つ&#x200B;**acMapping**&#x200B;プロパティを含める必要があります。含めないと、AEMの&#x200B;**Page Properties**&#x200B;でAdobe Campaignテンプレートを選択できません。

## テンプレート／ページコンポーネント {#template-page-component}

***/libs/mcm/campaign/components/campaign_newsletterpage***

<table>
 <tbody>
  <tr>
   <td><strong>ベストプラクティス</strong></td>
   <td><strong>実装</strong></td>
  </tr>
  <tr>
   <td><p>ドキュメントタイプを指定して、一貫したレンダリングを確実におこなうようにします。</p> <p>先頭に DOCTYPE を追加します（HTML または XHTML）。</p> </td>
   <td><p><i>cq:doctype</i>プロパティを<i>"/etc/designs/default/jcr:content/campaign_newsletterpage"</i>で変更することで、デザインで設定できます。</p> <p>デフォルトは、"XHTML" です。</p> <p>&lt;!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "https://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd"&gt;</p> <p>"HTML_5" に変更できます。</p> <p>&lt;!DOCTYPE HTML&gt;</p> </td>
  </tr>
  <tr>
   <td><p>文字定義を指定して、特殊文字の正しいレンダリングを確実におこなうようにします。</p> <p>&lt;head&gt;にCHARSET宣言（例：iso-8859-15、UTF-8）を追加します。</p> </td>
   <td><p>UTF-8 に設定します。</p> <p>&lt;meta http-equiv="content-type" content="text/html; charset=UTF-8"&gt;</p> </td>
  </tr>
  <tr>
   <td><p>&lt;table&gt;要素を使用してすべての構造をコード化します。 より複雑なレイアウトの場合、テーブルをネストして複雑な構造を構築します。</p> <p>電子メールは、css がなくても見やすくする必要があります。</p> </td>
   <td><p>テーブルは、コンテンツ構築でテンプレート全体にわたって使用されます。現在のところ、最大で 4 つのネストされたテーブルを使用しています（1 つの基本テーブル + 最大 3 つのネストレベル）。</p> <p>&lt;div&gt; タグは、コンポーネントの適切な編集を確実におこなうために、オーサリングモードでのみ使用します。</p> </td>
  </tr>
  <tr>
   <td>要素の属性（cellpadding、valign、width など）を使用してテーブルの寸法を設定します。これは、ボックスモデル構造を強制します。</td>
   <td><p>すべてのテーブルに、<i>border</i>、<i>cellpadding</i>、<i>cellspacing</i>、<i>width</i>など、必要な属性が含まれます。</p> <p>テーブル内の要素の位置を調整するために、すべてのテーブルセルに<i>valign="top"</i>属性が設定されています。</p> </td>
  </tr>
  <tr>
   <td><p>可能であれば、モバイルでの使いやすさを考慮します。メディアクエリーを使用して、小さい画面でのテキストサイズを大きくして、リンク用に親指サイズのヒット領域を提供します。</p> <p>設計で可能であれば、電子メールをレスポンシブにします。</p> </td>
   <td>CSS スタイルがデモデザインの説明で使用されている限り、メディアクエリーを使用してモバイルフレンドリーなバージョンを提供します。</td>
  </tr>
  <tr>
   <td>すべての CSS を最初に配置するよりも、インライン CSS が優れています。</td>
   <td><p>基盤となる HTML 構造をより効果的に実演し、ニュースレターの構造を容易にカスタマイズできるようにするには、一部の CSS 定義のみをインラインにします。</p> <p>ベーススタイルとテンプレートのバリエーションは、ページの&lt;head&gt;内のスタイルブロックに抽出されました。 ニュースレターの最終版では、これらの CSS 定義は、HTML にインラインになっている必要があります。自動インライン化メカニズムが計画されていますが、現在は利用できません。</p> </td>
  </tr>
  <tr>
   <td>CSS をシンプルに保ちます。複合スタイル宣言、短縮形コード、CSS レイアウトプロパティ、複雑なセレクターおよび疑似要素を避けます。</td>
   <td>CSS スタイルがデモデザインの説明で使用されている限り、推奨される CSS は次のようになります。</td>
  </tr>
  <tr>
   <td>電子メールの幅は、最大 600 ～ 800 pixel にする必要があります。これは、多くのクライアントで提供されるプレビューパネルのサイズ内での動作を優れたものにします。</td>
   <td>デモデザインでは、コンテンツテーブルの<i>幅</i>は600pxに制限されています。</td>
  </tr>
 </tbody>
</table>

### 画像 {#images}

/libs/mcm/campaign/components/image

| **ベストプラクティス** | **実装** |
|---|---|
| 画像に&#x200B;*alt*&#x200B;属性を追加します。 | *alt*&#x200B;属性は、画像コンポーネントに必須として定義されています。 |
| 画像には、*png*&#x200B;形式ではなく&#x200B;*jpg*&#x200B;形式を使用します | 画像は、画像コンポーネントでは、常に、 JPG として提供されます。 |
| テーブルでは、背景画像の代わりに`<img>`要素を使用します。 | テンプレートでは、背景画像データは使用されていません。 |
| 写真に style=&quot;display block&quot; 属性を追加します。Gmail での表示を向上できます。 | すべての画像には、デフォルトで&#x200B;*style=&quot;display block&quot;*&#x200B;属性が含まれます。 |

### テキストとリンク {#text-and-links}

/libs/mcm/campaign/components/heading, /libs/mcm/campaign/components/textimage

<table>
 <tbody>
  <tr>
   <td><strong>ベストプラクティス</strong></td>
   <td><strong>実装</strong></td>
  </tr>
  <tr>
   <td>CSS(font-family)では、スタイルの代わりにhtml &lt;font&gt;を使用します。</td>
   <td>RichTextEditor（例：textimage コンポーネントに含まれるもの）は、選択したテキストへのフォントファミリーおよびフォントサイズの選択および適用をサポートするようになりました。これらは&lt;font&gt;タグとしてレンダリングされます。</td>
  </tr>
  <tr>
   <td><i>Arial、Verdana、Georgia</i>、<i>Times New Roman</i>など、基本的なクロスプラットフォームフォントを使用します。</td>
   <td><p>ニュースレターのデザインによって異なります。</p> <p>デモデザインでは、Helvetica フォントが使用されますが、存在しない場合は一般的なサンセリフフォントに戻ります。</p> </td>
  </tr>
 </tbody>
</table>

### 汎用 {#generic}

| **ベストプラクティス** | **実装** |
|---|---|
| W3C バリデーターを使用して、HTML コードを修正します。すべての開始タグが適切に閉じられるようにします。 | コードは検証されました。XHTMLトランジショナルDoctypeの場合、`<html>`要素の欠落しているxmlns属性のみが欠落します。 |
| JavaScriptやFlashを気にしないでください。これらのテクノロジーは、主にEメールクライアントでサポートされていません。 | JavaScript も Flash も、ニュースレターテンプレートでは使用していません。 |
| マルチパート送信では、プレーンテキストバージョンを追加します。 | 新しいウィジェットは、ページプロパティに組み込まれ、ページコンテンツからプレーンテキストを簡単に抽出できます。これは、最終的なプレーンテキストバージョンの開始点として使用できます。 |

## キャンペーンニュースレターのテンプレートと例  {#campaign-newsletter-templates-and-examples}

AEM には、キャンペーンニュースレターを作成するためのいくつかのテンプレートおよびコンポーネントが標準で付属しています。これらのテンプレートおよびコンポーネントを使用して、カスタムのニュースレターを作成できます。

### テンプレート {#templates}

基盤を提供し、様々なコンテンツの流れを可能にするために、3 つの少しずつ違ったテンプレートのタイプが標準で用意されています。これらを簡単に使用して、カスタムニュースレターを作成できます。

すべてに&#x200B;**ヘッダー**、**フッター**、**本文**&#x200B;セクションがあります。 bodyセクションの下の各テンプレートは、**列のデザイン**（1列、2列または3列）で異なります。

![](assets/chlimage_1-69.png)

### コンポーネント {#components}

現在、[キャンペーンテンプレート内で使用可能なコンポーネントが 7 つ](/help/sites-authoring/adobe-campaign-components.md)あります。これらのコンポーネントは、すべてアドビのマークアップ言語である **HTL** に基づいています。

| **コンポーネント名** | **コンポーネントパス** |
|---|---|
| 見出し | /libs/mcm/campaign/components/heading |
| 画像 | /libs/mcm/campaign/components/image |
| テキストおよびパーソナライゼーション | /libs/mcm/campaign/components/personalization |
| Textimage | /libs/mcm/campaign/components/textimage |
| リンク | /libs/mcm/campaign/components/reference |
| Dynamic Media Classic(旧称Scene7)画像テンプレート | /libs/mcm/campaign/s7image |
| ターゲット参照 | /libs/mcm/campaign/components/reference |

>[!NOTE]
>
>これらのコンポーネントは、メールコンテンツに最適化されています。つまり、このドキュメントで説明したベストプラクティスを厳密に順守します。その他の標準提供コンポーネントを使用すると、通常、これらのルールに違反します。

これらのコンポーネントについて詳しくは、[Adobe Campaign コンポーネント](/help/sites-authoring/adobe-campaign-components.md)を参照してください。
