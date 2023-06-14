---
title: メールテンプレートのベストプラクティス
description: AEMでの電子メールテンプレートの作成に関するベストプラクティスを確認します。
uuid: 07417a63-7ca6-484c-b55d-57b319428329
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration, best-practices
content-type: reference
discoiquuid: 2418777e-4eb2-4d82-aa9e-8d1b0bf740f3
docset: aem65
exl-id: 6666eddc-dc17-4bd4-9d55-e6522f40a680
source-git-commit: d673a447e9ce2377c8645c87f12be81cbad06238
workflow-type: tm+mt
source-wordcount: '1077'
ht-degree: 18%

---

# メールテンプレートのベストプラクティス {#best-practices-for-email-templates}

>[!CAUTION]
>
>この記事は、非推奨の基盤コンポーネントベースのAEM電子メールコンポーネントに適用されます。
>
>最新の [コアコンポーネントの電子メールコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/email/introduction.html)

このドキュメントでは、E メールキャンペーンテンプレートをよく開発した結果として生じる、E メールのデザインに関するベストプラクティスの一部を説明します。

AEMで利用できるデモキャンペーンは、これらすべてのベストプラクティスに従っています。 デモキャンペーンでのベストプラクティスの実装方法については、各ベストプラクティスを参照してください。

独自のニュースレターを作成する際は、次のベストプラクティスを利用してください。

>[!NOTE]
>
>すべてのキャンペーンコンテンツは、`master` タイプのページ `cq/personalization/components/ambitpage` の下に作成してください。
>
>例えば、計画されているキャンペーン構造が次のような場合
>
>`/content/campaigns/teasers/en/campaign-promotion-global`
>
>それが、 `master` ページ
>
>`/content/campaigns/teasers/master/en/campaign-promotion-global`

>[!NOTE]
>
>Adobe Campaignのメールテンプレートを作成する場合は、プロパティを含める必要があります **acMapping** 値 **mapRecipient** 内 **jcr:content** ノードを設定します。 選択しない場合、 Adobe Campaignテンプレートは **ページプロパティ** Experience Managerの（フィールドが無効）。

## テンプレート/ページコンポーネント {#template-page-component}

***/libs/mcm/campaign/components/campaign_newsletterpage***

<table>
 <tbody>
  <tr>
   <td><strong>ベストプラクティス</strong></td>
   <td><strong>実装</strong></td>
  </tr>
  <tr>
   <td><p>レンダリングの一貫性を保つために、ドキュメントタイプを指定します。</p> <p>先頭に DOCTYPE を追加する (HTMLまたは XHTML)</p> </td>
   <td><p><i>"/etc/designs/default/jcr:content/campaign_newsletterpage"</i> にある <i>cq:doctype</i> プロパティを変更することで、デザインでの設定が可能になります。</p> <p>デフォルトは、"XHTML" です。</p> <p>&lt;!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional/EN" "https://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd"&gt;</p> <p>「HTML5」に変更できます。</p> <p>&lt;!DOCTYPE HTML&gt;</p> </td>
  </tr>
  <tr>
   <td><p>特殊文字の正しいレンダリングが行われるように文字定義を指定します。</p> <p>CHARSET 宣言（例えば、iso-8859-15、UTF-8）を &lt;head&gt;</p> </td>
   <td><p>UTF-8 に設定されています。</p> <p>&lt;meta http-equiv="content-type" content="text/html; charset=UTF-8"&gt;</p> </td>
  </tr>
  <tr>
   <td><p>&lt;table&gt;element を使用してすべての構造をコーディングします。より複雑なレイアウトを作成するには、テーブルをネストして複雑な構造を作成する必要があります。</p> <p>CSS がなくても E メールが適切に表示されるはずです。</p> </td>
   <td><p>テンプレート全体で、コンテンツを構造化するためにテーブルが使用されます。 現在、最大 4 つのネストされたテーブル (1 つの基本テーブル+最大 3 ネストレベル )</p> <p>「&lt;div&gt;」タグは、適切なコンポーネント編集を確実におこなうために、オーサーモードでのみ使用されます。</p> </td>
  </tr>
  <tr>
   <td>テーブルの寸法を設定するには、要素の属性（cellpadding、valign、width など）を使用します。 このメソッドは、ボックスモデル構造を強制的に作成します。</td>
   <td><p>すべてのテーブルには、以下のような必要な属性が含まれます。 <i>ボーダー</i>, <i>cellpadding</i>, <i>cellspacing</i>、および <i>幅</i>.</p> <p>テーブル内の要素の位置を調和させるために、すべてのテーブルのセルには、属性 <i>valign="top"</i> が設定されています。</p> </td>
  </tr>
  <tr>
   <td><p>可能な場合は、モバイルに優しいを説明します。 メディアクエリを使用して、小さい画面でテキストサイズを大きくし、リンクにサムサイズのヒット領域を指定します。</p> <p>デザインで許可されている場合は、E メールをレスポンシブにします。</p> </td>
   <td>CSS スタイルを使用してデモデザインを説明している限り、モバイルに適したバージョンを提供するためにメディアクエリが使用されています。</td>
  </tr>
  <tr>
   <td>すべての CSS を先頭に配置するよりも、インライン CSS の方が効果的です。</td>
   <td><p>基になるHTML構造をより効果的にデモし、ニュースレターの構造を簡単にカスタマイズできるように、一部の CSS 定義のみがインライン化されています。</p> <p>ベーススタイルおよびテンプレートのバリエーションは、ページの &lt;head&gt; のスタイルブロックに抽出されています。ニュースレターの最終送信時に、これらの CSS 定義がHTMLにインライン化されます。 自動インライン化メカニズムが予定されていますが、現在は使用できません。</p> </td>
  </tr>
  <tr>
   <td>CSS をシンプルにします。 複合スタイル宣言、短縮形コード、CSS レイアウトプロパティ、複雑なセレクター、疑似要素は避けます。</td>
   <td>CSS スタイルを使用してデモデザインを説明している限り、CSS の推奨事項に従っています。</td>
  </tr>
  <tr>
   <td>電子メールの幅は、600 ～ 800 ピクセルにする必要があります。 このサイズ設定により、多くのクライアントが提供するプレビューパネルのサイズ内での動作が向上します。</td>
   <td>この <i>幅</i> のコンテンツテーブルは、デモデザインでは 600 ピクセルに制限されています。</td>
  </tr>
 </tbody>
</table>

### 画像 {#images}

/libs/mcm/campaign/components/image

| **ベストプラクティス** | **実装** |
|---|---|
| 画像に *alt* 属性を追加します。 | *alt* 属性は、画像コンポーネントに必須なものとして定義されています。 |
| 画像に *png* の代わりに *jpg* 形式を使用します。 | 画像は、常に画像コンポーネントでJPGとして提供されます。 |
| テーブルの背景画像の代わりに `<img>` 要素を使用します。 | テンプレートでは背景画像データは使用されません。 |
| 画像に style=&quot;display block&quot;属性を追加します。 これにより、Gmail 上で表示しやすくなります。 | すべての画像には、デフォルトで *style=&quot;display block&quot;* 属性が含まれています。 |

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
   <td>RichTextEditor （例えば、textimage コンポーネント）では、選択したテキストにフォントファミリとフォントサイズを選択して適用できるようになりました。 タグとしてレンダリングされます。</td>
  </tr>
  <tr>
   <td>次のような基本的なクロスプラットフォームフォントを使用します。 <i>Arial®, Verdana, Georgia</i>、および <i>Times New Roman®</i>.</td>
   <td><p>ニュースレターのデザインに依存します。</p> <p>デモデザインでは、フォント「Helvetica®」が使用されますが、存在しない場合は汎用の sans-serif フォントにフォールバックされます。</p> </td>
  </tr>
 </tbody>
</table>

### 一般 {#generic}

| **ベストプラクティス** | **実装** |
|---|---|
| W3C バリデーターを使用して、HTMLコードを修正します。 すべての開いているタグが正しく閉じられていることを確認します。 | コードが検証されました。 XHTML の遷移 Doctype のみの場合、 `<html>` 要素が見つかりません。 |
| JavaScript やFlashの使用は避けます。これらのテクノロジーは、多くの場合、E メールクライアントでサポートされていません。 | JavaScript またはFlashは、ニュースレターテンプレートでは使用されません。 |
| マルチパート送信用のプレーンテキストバージョンを追加します。 | 新しいウィジェットがページプロパティに組み込まれ、ページコンテンツからプレーンテキストバージョンを簡単に抽出できるようになりました。 最終的な平文バージョンの出発点として使用できます。 |

## Campaign ニュースレターのテンプレートと例 {#campaign-newsletter-templates-and-examples}

AEMには、キャンペーンニュースレターを作成するためのテンプレートとコンポーネントが標準で付属しています。 これらのテンプレートとコンポーネントを使用して、カスタムニュースレターを作成できます。

### テンプレート {#templates}

堅牢な基盤を提供し、様々なコンテンツフローの可能性を広げるために、すぐに使用できる 3 つの異なるテンプレートタイプが用意されています。 これら 3 つのタイプを簡単に使用して、カスタムニュースレターを作成できます。

すべてのユーザーが **ヘッダー**, a **フッター**、および **本文** 」セクションに入力します。 body セクションの下で、各テンプレートは **列デザイン** （1 列、2 列、3 列）。

![](assets/chlimage_1-69.png)

### コンポーネント {#components}

現在 [キャンペーンテンプレート内で使用できる 7 つのコンポーネント](/help/sites-authoring/adobe-campaign-components.md). これらのコンポーネントは、すべてAdobeマークアップ言語に基づいています **HTL**.

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
>これらのコンポーネントは、メールコンテンツ用に最適化されています。つまり、このドキュメントで概要を説明しているベストプラクティスに従います。 その他の標準コンポーネントを使用すると、通常、これらのルールに違反します。

これらのコンポーネントについて詳しくは、 [Adobe Campaignコンポーネント](/help/sites-authoring/adobe-campaign-components.md).
