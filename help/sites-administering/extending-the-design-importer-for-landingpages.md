---
title: ランディングページ用のデザインインポーターの拡張と設定
seo-title: Extending and Configuring the Design Importer for Landing Pages
description: ランディングページ用のデザインインポーターの設定方法について説明します。
seo-description: Learn how to configure the Design Importer for landing pages.
uuid: a2dd0c30-03e4-4e52-ba01-6b0b306c90fc
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: e02f5484-fbc2-40dc-8d06-ddb53fd9afc2
docset: aem65
exl-id: 1b8c6075-13c6-4277-b726-8dea7991efec
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '3503'
ht-degree: 100%

---

# ランディングページ用のデザインインポーターの拡張と設定{#extending-and-configuring-the-design-importer-for-landing-pages}

ここでは、ランディングページ用にデザインインポーターを設定し、必要に応じて拡張する方法について説明します。読み込み後のランディングページの使用については、[ランディングページ](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md)を参照してください。

**デザインインポーターでカスタムコンポーネントを抽出する**

デザインインポーターにカスタムコンポーネントを認識させる論理的な手順を説明します。

1. TagHandler の作成

   * タグハンドラーは、特定の種類の HTML タグを処理する POJO です。TagHandler が処理できる HTML タグの「種類」は、TagHandlerFactory の OSGi プロパティ「tagpattern.name」によって定義されます。この OSGi プロパティは本来、処理対象として入力された HTML タグと一致する正規表現です。ネストされたタグはすべて、タグハンドラーにスローされ処理されます。例えば、ネストされた &lt;p> タグを含む div を登録した場合、&lt;p> タグも TagHandler にスローされ、必要に応じて処理することができます。
   * タグハンドラーのインターフェイスは、SAX コンテンツファインダーのインターフェイスに似ています。SAX コンテンツファインダーは HTML タグごとに SAX イベントを受け取ります。タグハンドラーを提供する場合、特定のライフサイクルメソッドを実装する必要があります。このメソッドは、デザインインポーターのフレームワークによって自動的に呼び出されます。

1. 対応する TagHandlerFactory を作成します。

   * タグハンドラーファクトリは、タグハンドラーのインスタンスの生成を管理する OSGi コンポーネント（シングルトン）です。
   * タグハンドラーファクトリは、「tagpattern.name」と呼ばれる OSGi プロパティを公開する必要があります。このプロパティの値は、入力された HTML タグと一致します。
   * 入力された HTML タグと一致するタグハンドラーが複数ある場合は、順位の高いタグハンドラーが選択されます。この順位は OSGi プロパティ **service.ranking** として公開されています。
   * TagHandlerFactory は OSGi コンポーネントです。TagHandler に参照を提供する場合、その参照はこのファクトリを経由する必要があります。

1. デフォルトの順位を変更する場合は、必ず TagHandlerFactory でより望ましい順位を設定します。

>[!CAUTION]
>
>ランディングページの読み込みに使用されていたデザインインポーターは、[AEM 6.5 で廃止されました。](/help/release-notes/deprecated-removed-features.md#deprecated-features)

## 読み込み用の HTML の準備 {#preparing-the-html-for-import}

インポーターページを作成したら、HTML ランディングページ全体を読み込むことができます。HTML ランディングページを読み込むには、最初にこのページのコンテンツを zip ファイルにしてデザインパッケージを作成する必要があります。デザインパッケージには、HTML ランディングページと、参照するアセット（画像、CSS、アイコン、スクリプトなど）が含まれます。

次のチートシートには、読み込み用に HTML を準備する方法の一例が示されています。

ランディングページのチートシート

[ファイルを入手](assets/cheatsheet.zip)

### zip ファイルのレイアウトと要件 {#zip-file-layout-and-requirements}

>[!NOTE]
>
>この時点では、zip ファイルに 1 つの HTML ページ、またはページの一部分のみを含めることができます。

zip ファイルのレイアウトの例を以下に示します。

* /index.html -> ランディングページの HTML ファイル
* /css -> CSS clientlib への追加用
* /img -> すべての画像とアセット
* /js -> JS clientlib への追加用

このレイアウトは、HTML5 Boilerplate のレイアウトのベストプラクティスに基づいています。詳しくは、[https://html5boilerplate.com/](https://html5boilerplate.com/) を参照してください。

>[!NOTE]
>
>少なくとも、デザインパッケージのルートレベルに **index.html** ファイルを&#x200B;**含める必要があります**。読み込むランディングページにモバイルバージョンがある場合は、この zip ファイルのルートレベルに **mobile.index.html** と **index.html** を含める必要があります。

### ランディングページの HTML の準備 {#preparing-the-landing-page-html}

HTML を読み込むには、キャンバス div をランディングページ HTML に追加する必要があります。

canvas div は `id="cqcanvas"` を含む HTML **div** です。この div を HTML の `<body>` タグ内に挿入し、変換対象のコンテンツを囲む必要があります。

キャンバス div を追加した後のランディングページ HTML のスニペットの例を次に示します。

```xml
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title></title>
  <meta name="description" content="">
</head>
<body>
 <div id="cqcanvas">
  <!-- HTML content intended for conversion -->
 </div>
</body>
</html>
```

### HTML に編集可能な AEM コンポーネントを含める準備 {#preparing-the-html-to-include-editable-aem-components}

ランディングページを読み込むとき、ページを現状維持で読み込むことができます。この場合、ランディングページの読み込み後、読み込まれたいずれの項目も AEM では編集できません（AEM コンポーネントをページに追加することは引き続き可能です）。

ランディングページを読み込む前に、ランディングページの一部のパーツを編集可能な AEM コンポーネントに変換することができます。これにより、ランディングページデザインを読み込んだ後も、ランディングページの一部をすばやく編集することができます。

パーツを変換するには、読み込む HTML ファイル内の適切なコンポーネントに `data-cq-component` を追加します。

次の節では、HTML ファイルを編集し、ランディングページの特定のパーツをそれぞれ編集可能な AEM コンポーネントに変換する方法について説明します。[ランディングページコンポーネント](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md)で、コンポーネントについて詳しく説明します。

>[!NOTE]
>
>ランディングページのパーツを AEM コンポーネントに変換するための HTML マークアップには、長い形式と短縮形のタグ宣言の両方の形式があります。各コンポーネントで、両方の形式について説明しています。

### 制限事項 {#limitations}

読み込みをおこなう前に、次の制限事項に注意してください。

### タグに適用された class や id などの属性は保持されない {#any-attribute-like-class-or-id-applied-on-the-amp-lt-body-tag-is-not-preserved}

id や class などの属性が body タグに適用されている場合（例：`<body id="container">`）、この属性は読み込み後に保持されません。したがって、読み込むデザインは、`<body>` タグに適用されている属性に依存しないようにしてください。

### zip ファイルのドラッグ＆ドロップ {#drag-and-drop-zip}

ドラッグ＆ドロップによる zip ファイルのアップロードは、Internet Explorer および Firefox バージョン 3.6 以前ではサポートされていません。これらのブラウザーの使用時にデザインをアップロードする場合は、ファイルのドロップ領域をクリックしてファイルのアップロードダイアログボックスを開き、そのダイアログを使用してデザインをアップロードします。

デザイン zip ファイルの「ドラッグ＆ドロップ」をサポートするブラウザーは、Chrome、Safari 5.x、Firefox 4 以降です。

### Modernizr はサポートされない {#modernizr-is-not-supported}

`Modernizr.js` は Javascript ベースのツールで、ブラウザーのネイティブ機能を検出し、この機能が HTML5 要素として適切かどうかを判断します。様々なブラウザーの古いバージョンのサポートを強化するために Modernizr が使用されているデザインを読み込むと、ランディングページソリューションで問題が発生する場合があります。`Modernizr.js` スクリプトは、デザインインポーターではサポートされていません。

### ページプロパティはデザインパッケージの読み込み時に保持されない {#page-properties-are-not-preserved-at-the-time-of-importing-design-package}

デザインパッケージを読み込む前に、ページプロパティ（カスタムドメイン、強制 HTTPS など）を（空白のランディングページテンプレートを使用する）ページに設定した場合、このプロパティはデザインが読み込まれた後に失われます。したがって、デザインパッケージを読み込んだ後でページプロパティを設定することをお勧めします。

### HTML のみのマークアップを想定 {#html-only-markup-assumed}

読み込み時に、セキュリティ上の理由から、また、無効なマークアップが読み込まれて公開されないように、マークアップがサニタイズ削除されます。この場合、HTML のみのマークアップと、その他のあらゆる形式の要素（インライン SVG や Web コンポーネントなど）が除外されることを前提としています。

### テキスト {#text}

テキストコンポーネント（`foundation/components/text`）をデザインパッケージ内の HTML に挿入するための HTML マークアップを次に示します。

```xml
<div data-cq-component="text"> <p>This is some editable text</p> </div>
```

上記のマークアップを HTML 内に含めると、次の操作がおこなわれます。

* デザインパッケージの読み込み後に作成されたランディングページ内に、編集可能な AEM テキストコンポーネント（`sling:resourceType=foundation/components/text`）を作成します。
* 作成されたテキストコンポーネントの `text` プロパティに、`div` で囲まれた HTML を設定します。

**短縮形のコンポーネントタグ宣言**：

```xml
<p data-cq-component="text">Text component shorthand</p>
```

**リスト付きテキスト**

次のリストを含むテキストを追加します。

* 1 行目
* 2 行目

これを RTE エディターで編集可能にします。

```xml
<div data-cq-component="text"><p>This is text with a list:</p><ul><li>1st</li><li>2nd</li></ul><p>It can be edited with the RTE editor</p></div>
```

**色付きのテキスト**

テキストを色（ピンク）付きで追加し、RTE エディターで編集できるようにします。

```xml
<div class="pink" data-cq-component="text"><p>This is pink text.</p><p>It can be edited with the RTE editor</p></div>
```

### タイトル {#title}

タイトルコンポーネント（`wcm/landingpage/components/title`）をデザインパッケージ内の HTML に挿入するための HTML マークアップを次に示します。

```xml
<div data-cq-component="title"> <h1>This is some editable title text</h1> </div>
```

上記のマークアップを HTML 内に含めると、次の操作がおこなわれます。

* デザインパッケージの読み込み後に作成されたランディングページ内に、編集可能な AEM タイトルコンポーネント（`sling:resourceType=wcm/landingpage/components/title`）を作成します。
* 作成されたタイトルコンポーネントの `jcr:title` プロパティに、div で囲まれた見出しタグ内のテキストを設定します。
* `type` プロパティに見出しタグ（この場合は `h1`）を設定します。

タイトルコンポーネントは、7 つのタイプ（`h1, h2, h3, h4, h5, h6` および `default`）をサポートします。

**短縮形のコンポーネントタグ宣言**：

```xml
<h1 data-cq-component="title">Title component shorthand</h1>
```

### 画像 {#image}

画像コンポーネント（foundation/components/image）をデザインパッケージ内の HTML に挿入するための HTML マークアップを次に示します。

```xml
<div data-cq-component="image">
<img src="img/video1.png" alt="Video about Polar Brake Goggles in action" title="Polar Brake Goggles" width="300" height="200" />
</div>
```

上記のマークアップを HTML 内に含めると、次の操作がおこなわれます。

* デザインパッケージの読み込み後に作成されたランディングページ内に、編集可能な AEM 画像コンポーネント（`sling:resourceType=foundation/components/image`）を作成します。
* 作成された画像コンポーネントの `fileReference` プロパティに、src 属性で指定された画像の読み込み先のパスを設定します。
* `alt` プロパティに、img タグ内の alt 属性の値を設定します。
* `title` プロパティに、img タグ内の title 属性の値を設定します。
* `width` プロパティに、img タグ内の width 属性の値を設定します。
* `height` プロパティに、img タグ内の height 属性の値を設定します。

**短縮形のコンポーネントタグ宣言：**

```xml
<img data-cq-component="image" src="test.png" alt="Image component shorthand"/>
```

#### 画像コンポーネントの div 内で絶対 URL の img src はサポートされない {#absolute-url-img-src-not-supported-within-image-component-div}

コンポーネントを変換するために、絶対 URL の src を持つ`<img>`タグを設定すると、対応する **UnsupportedTagContentException** が発生します。例えば、次のような記述はサポートされません。

`<div data-cq-component="image">`

`<img src="https://cdn.printfriendly.com/pf-button.gif" alt="Print Friendly and PDF"/>`

`</div>`

これ以外の、画像コンポーネントの div に含まれていない img タグの場合は、絶対 URL の画像がサポートされます。

### コールトゥアクションコンポーネント {#call-to-action-components}

ランディングページの一部を「編集可能なコールトゥアクションコンポーネント」として読み込むためにマークすることができます。これにより読み込まれたコールトゥアクションコンポーネントは、ランディングページの読み込み後に編集できます。AEM には次のようなコールトゥアクション（CTA）コンポーネントが含まれています。

* クリックスルーリンク：訪問者がクリックするとターゲット URL に移動するテキストリンクを追加できます。
* グラフィックリンク：訪問者がクリックするとターゲット URL に移動する画像を追加できます。

#### クリックスルーリンク {#click-through-link}

この CTA コンポーネントを使用して、ランディングページにテキストリンクを追加できます。

サポートされるプロパティ

* ラベル（太字、イタリック、下線のオプションを含む）
* ターゲット URL（サードパーティおよび AEM の URL をサポート）
* ページレンダリングオプション（同一のウィンドウ、新規のウィンドウなど）

HTML タグを使用して、読み込まれた zip ファイルにクリックスルーコンポーネントを含めます。ここで、href がターゲット URL にマッピングされたり、「製品の詳細を表示」がラベルにマッピングされたりします。

```xml
<div id="cqcanvas">
.
.
                <div data-cq-component="clickThroughLink">
        <a href="/content/we-retail/us/en/products/equipment/snow-sports/flying-snowboard.html">View Product Details  ></a>
  </div>
.
.
</div>
```

このコンポーネントは任意のスタンドアロンのアプリケーションで使用したり、zip ファイルから読み込むことができます。

**短縮形のコンポーネントタグ宣言**：

```xml
<a href="/somelink.html" data-cq-component="clickThroughLink">Click Through Link shorthand</a>
```

#### グラフィックリンク {#graphical-link}

この CTA コンポーネントを使用して、リンク付きのグラフィック画像をランディングページに追加できます。単純なボタンの画像や、背景としてのグラフィック画像を使用できます。画像をクリックすると、ユーザーはコンポーネントのプロパティで指定されたターゲット URL に誘導されます。このコンポーネントは「コールトゥアクショングループ」に含まれています。

サポートされるプロパティ

* 画像のトリミング、回転
* マウスポインターを置いたときのテキスト、説明、ピクセル単位のサイズ
* ターゲット URL（サードパーティおよび AEM の URL をサポート）
* ページレンダリングオプション（同一のウィンドウ、新規のウィンドウなど）

HTML タグを使用して、読み込まれた zip ファイルにグラフィックリンクコンポーネントを含めます。ここでは、href がターゲット URL にマッピングされ、img src がレンダリング画像になり、マウスを置いたときのテキストとして「title」が使用されます。

```xml
<div id="cqcanvas">
  <div data-cq-component="clickThroughGraphicalLink"><a href="https://www.adobe.com/go/wem"><img src="img/call-to-action-button.png" title="Click Here to Learn More" /></a></div>
</div>
```

**短縮形のコンポーネントタグ宣言**：

```xml
<a href="/somelink.html" data-cq-component="clickThroughGraphicalLink"><img src="linkimage.png" alt="Click Through Graphical Link shorthand"/></a>
```

>[!NOTE]
>
>クリックスルーグラフィックリンクを作成するには、アンカータグと画像タグを div の中に `data-cq-component="clickthroughgraphicallink"` 属性で囲む必要があります。
>
>例：`<div data-cq-component="clickthroughlink"> <a href="https://myURLhere/"><img src="image source here"></a> </div>`
>
>CSS を使用して画像とアンカータグを関連付けるその他の方法はサポートされていません。例えば、次のようなマークアップは無効です。
>
>`<div data-cq-component="clickthroughgraphicallink">`
>
>`<a class="hasBackground" href="https://myURLhere/"></a>`
>
>`</div>`
>
>関連する `css .hasbackground { background-image: pathtoimage }` とともに

### リードフォーム {#lead-form}

リードフォームは、訪問者（リード）のプロファイル情報を収集するために使用するフォームです。この情報を保存して後で使用し、この情報に基づき効果的なマーケティングをおこなうことができます。この情報には通常、タイトル、名前、電子メール、生年月日、住所、興味などがあります。このコンポーネントは「CTA リードフォーム」グループに含まれています。

**サポートされている機能**

* 事前定義されたリードフィールド - 名、姓、住所、生年月日、性別、詳細情報、ユーザー ID、メール ID、送信ボタンがサイドキックで使用できます。必要なコンポーネントをリードフォームにドラッグ＆ドロップするだけで使用できます。
* これらのコンポーネントを使用して、作成者がスタンドアロンのリードフォームをデザインできます。これらのフィールドはリードフォームフィールドに対応しています。スタンドアロンのアプリケーション、または読み込んだ zip アプリケーションで、ユーザーが cq:form または cta リードフォームフィールドを使用して別のフィールドを追加し、要件に応じてデザインすることができます。
* 特定の事前定義された CTA リードフォーム名を使用してフォームフィールドをマッピングします。例えば、firstName をリードフォームの名にマッピングしたりします。
* リードフォームにマッピングされないフィールドは、cq:form コンポーネント（テキスト、ラジオボタン、チェックボックス、ドロップダウン、非表示、パスワード）にマッピングされます。
* ユーザーは &quot;label&quot; タグを使用してタイトルを設定したり、スタイル属性 &quot;class&quot; を使用してスタイルを設定することができます（CTA リードフォームコンポーネントでのみ有効）。
* ありがとうページや購読リストをフォームの hidden パラメーターとして設定（index.htm 内）したり、「リードフォームの最初」の編集バーから追加または編集することができます。

   &lt;input type=&quot;hidden&quot; name=&quot;redirectUrl&quot; value=&quot;/content/we-retail/en/user/register/thank_you&quot;/>

   &lt;input type=&quot;hidden&quot; name=&quot;groupName&quot; value=&quot;leadForm&quot;/>

* required（必須）などの制約を、各コンポーネントの編集設定から指定することができます。

HTML タグを使用して、読み込まれた zip ファイルにグラフィックリンクコンポーネントを含めます。ここでは、「firstName」がリードフォームの firstName にマッピングされたりしています。チェックボックスはこれらとは異なり、2 つのチェックボックスが cq:form ドロップダウンコンポーネントにマッピングされています。

```xml
<div id="cqcanvas">
   <div id="form_wrapper">
    <h2>NEWSLETTER SIGN UP</h2>
       <div data-cq-component="leadFormGeneration">
       <form method="post" action="#" onsubmit="return popupBox()">
       <label for="firstName" class="checkText">
        FIRST NAME
       </label><br />
       <input name="firstName" class="text pink" type="text" /><br />
       <label for="lastName" class="checkText">
        LAST NAME
       </label><br />
       <input name="lastName" class="text pink" type="text" /><br />
       <label for="emailId" class="checkText">
        EMAIL ADDRESS
       </label><br />
       <input name="emailId" class="text pink" type="text" /><br />

       <div class="checkboxes">
       <input type="checkbox" class="check" name="send_news" /> <label for="send_news" class="checkText">Send me the latest We.Retail news and announcements.</label><br />
       <input type="checkbox" class="check" name="send_offers" /> <label for="send_offers" class="checkText">Send me We.Retail deals and special offers.</label><br />
       </div>
       <input type="submit" name="submit" class="submit pink" value="Sign Up >" />
       </form>
     </div>
   </div>
```

### 段落システム（parsys） {#parsys}

AEM parsys コンポーネントは、他の AEM コンポーネントを含むことができるコンテナコンポーネントです。読み込んだ HTML に parsys コンポーネントを追加することができます。これにより、ランディングページが読み込まれた後も、ユーザーはこのページに対して編集可能な AEM コンポーネントの追加や削除をおこなうことができます。

段落システムでは、ユーザーがサイドキックを使用してコンポーネントを追加することができます。

parsys コンポーネント（`foundation/components/parsys`）をデザインパッケージ内の HTML に挿入するための HTML マークアップを次に示します。

```xml
<div data-cq-component="parsys">
   <div data-cq-component="title"><h2>ULTIMATE PROTECTION</h2></div>
        <div data-cq-component="title"><h3>ON SALE</h3></div>
</div>
```

上記のマークアップを HTML に含めるには、以下をおこないます。

* デザインパッケージの読み込み後に作成されたランディングページに、AEM parsys コンポーネント（foundation/components/parsys）を挿入します。
* サイドキックをデフォルトコンポーネントで初期化します。新しいコンポーネントをランディングページに追加するには、コンポーネントをサイドキックから parsys コンポーネントにドラッグします。
* 2 つのタイトルコンポーネントも parsys に含まれます。

### ターゲット {#target}

ターゲットコンポーネントには、ページ上のエクスペリエンスのコンテンツが表示されます。キャンペーン内にエクスペリエンスを多数作成することができ、ターゲットコンポーネントには、ページを訪問する多様なユーザーに対して様々なエクスペリエンスからのコンテンツを動的に表示することができます。

ターゲットコンポーネントを挿入し、またキャンペーン内に様々なエクスペリエンスを作成するための HTML マークアップを次に示します。

```xml
<div data-cq-component="target">
 <section data-cq-component="experience" data-cq-experience="default">
  <p data-cq-component="text">Default content. Select this campaign in client context to view other experiences</p>
 </section>

 <section data-cq-component="experience" data-cq-segment="over-30">
  <p data-cq-component="text">Content for Over 30</p>
 </section>

 <section data-cq-component="experience" data-cq-segment="under-30">
  <p data-cq-component="text">Content for Under 30</p>
 </section>
</div>
```

## その他の読み込みオプション {#additional-importing-options}

デザインパッケージを読み込む前には、読み込まれるコンポーネントを編集可能な AEM コンポーネントにするかどうかだけではなく、次のような設定もおこなえます。

* 読み込まれた HTML で定義されているメタデータを抽出し、ページプロパティを設定する。
* HTML での文字セットのエンコーディングを指定する。
* インポーターページテンプレートをオーバーレイする。

### 読み込まれた HTML で定義されているメタデータを抽出し、ページプロパティを設定 {#setting-page-properties-by-extracting-metadata-defined-in-imported-html}

読み込まれた HTML の冒頭で宣言されている次のメタデータは、デザインインポーターによって「jcr:description」プロパティとして抽出され保持されます。

* &lt;meta name=&quot;description&quot; content=&quot;&quot;>

HTML タグに設定されている lang 属性セットは、デザインインポーターによって「jcr:language」プロパティとして抽出され保持されます。

* &lt;html lang=&quot;en&quot;>

### HTML での文字セットのエンコーディングの指定 {#specifying-the-charset-encoding-in-the-html}

デザインインポーターは、読み込まれた HTML で指定されているエンコーディングを読み取ります。エンコーディングは次のように指定できます。

`<meta charset="UTF-8">`

*または*

`<meta http-equiv="content-type" content="text/html;charset=utf-8">`

読み込まれた HTML でエンコーディングが指定されていない場合、デザインインポーターによって設定されるデフォルトのエンコーディングセットは UTF-8 です。

### テンプレートのオーバーレイ {#overlaying-template}

空白のランディングページテンプレートをオーバーレイするには、`/apps/<appName>/designimporter/templates/<templateName>` でオーバーレイを新規作成します。

AEM のテンプレートを新規作成する手順については、[こちら](/help/sites-developing/templates.md)を参照してください。

### ランディングページにあるコンポーネントの参照 {#referring-a-component-from-landing-page}

data-cq-component 属性を使用して HTML で参照したいコンポーネントがあり、デザインインポーターによってコンポーネントにこの参照の場所が含まれるようにするとします。例えば、表コンポーネント（`resourceType = /libs/foundation/components/table`）を参照するとします。この場合、HTML に次の行を追加する必要があります。

`<div data-cq-component="/libs/foundation/components/table">foundation table</div>`

data-cq-component 内のパスは、コンポーネントの resourceType で指定されたパスにする必要があります。

### ベストプラクティス {#best-practices}

次に示すような CSS セレクターを、読み込み時のコンポーネントの変換用にマークする要素と共に使用することは推奨されません。

| E > F | F 要素は E 要素の子 | [子結合子](https://www.w3.org/TR/css3-selectors/#child-combinators) |
|---|---|---|
| E + F | F 要素の直前に E 要素 | [隣接兄弟結合子](https://www.w3.org/TR/css3-selectors/#adjacent-sibling-combinators) |
| E ～ F | F 要素の前に E 要素 | [一般兄弟結合子](https://www.w3.org/TR/css3-selectors/#general-sibling-combinators) |
| E:root | E 要素はドキュメントのルート | [構造擬似クラス](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-child(n) | E 要素は親の n 番目の子 | [構造擬似クラス](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-last-child(n) | E 要素は親の最後から n 番目の子 | [構造擬似クラス](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-of-type(n) | E 要素はこのタイプの n 番目の兄弟 | [構造擬似クラス](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-last-of-type(n) | E 要素はこのタイプの最後から n 番目の兄弟 | [構造擬似クラス](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |

読み込み後に生成された HTML には &lt;div> タグなどその他の HTML 要素も追加されるので、推奨されません。

* 上記と同じような構造に依存するスクリプトを、AEM コンポーネントへの変換用にマークする要素と共に使用することも推奨されません。
* &lt;div data-cq-component=”&amp;ast;”> などコンポーネントの変換用のマークアップタグに、スタイルを使用することは推奨されません。
* デザインレイアウトは、HTML5 Boilerplate のベストプラクティスに従って作成する必要があります。詳しくは、[https://html5boilerplate.com/](https://html5boilerplate.com/) を参照してください。

## OSGi モジュールの設定 {#configuring-osgi-modules}

OSGi コンソールから設定可能なプロパティを公開するコンポーネントを次に示します。

* ランディングページデザインインポーター
* ランディングページビルダー
* モバイルランディングページビルダー
* ランディングページエントリプリプロセッサー

プロパティについて、以下の表で簡単に説明します。

<table>
 <tbody>
  <tr>
   <td><strong>コンポーネント</strong></td>
   <td><strong>プロパティ名</strong></td>
   <td><strong>プロパティの説明 </strong></td>
  </tr>
  <tr>
   <td>ランディングページデザインインポーター</td>
   <td>Extract Filter</td>
   <td>抽出したファイルのフィルター時に使用する正規表現のリスト。<br />指定したいずれかのパターンに一致する zip エントリは、抽出から除外されます。</td>
  </tr>
  <tr>
   <td>ランディングページビルダー</td>
   <td>File Pattern</td>
   <td>File Pattern で定義した正規表現に一致する HTML ファイルを処理するよう、ランディングページビルダーを設定できます。</td>
  </tr>
  <tr>
   <td>モバイルランディングページビルダー</td>
   <td>ファイルパターン</td>
   <td>File Pattern で定義した正規表現に一致する HTML ファイルを処理するよう、ランディングページビルダーを設定できます。</td>
  </tr>
  <tr>
   <td> </td>
   <td>Device Groups</td>
   <td>サポートされるデバイスグループのリスト。</td>
  </tr>
  <tr>
   <td>ランディングページエントリプリプロセッサー</td>
   <td>Search Pattern </td>
   <td>アーカイブエントリコンテンツ内で検索するパターン。この正規表現とエントリコンテンツは、行ごとに照合されます。一致した場合、一致したテキストは指定の置換パターンに置き換えられます。<br /><br />ランディングページエントリプリプロセッサーの現在の制限事項については、下記のメモを参照してください。</td>
  </tr>
  <tr>
   <td> </td>
   <td>Replace Pattern</td>
   <td>一致が見つかったときに置換するパターン。$1、$2 など、正規表現のグループ参照を使用できます。また、このパターンでは {designPath} など、読み込み時に実際の値で解決されるキーワードがサポートされます。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>**ランディングページエントリプリプロセッサーの現在の制限事項**
>検索パターンに変更を加える必要がある場合、Felix プロパティエディターを開いたとき、バックスラッシュ文字を手動で追加し正規表現のメタ文字をエスケープ処理する必要があります。バックスラッシュ文字を手動で追加しない場合、正規表現が無効と見なされ、検索前のものが置き換えられません。
>
>例えば、デフォルト設定が
>`/\* *CQ_DESIGN_PATH *\*/ *(['"])`
>
>また、検索パターン内で >`CQ_DESIGN_PATH` を `VIPURL` と置換する必要がある場合、検索パターンは次のようになります。
`/\* *VIPURL *\*/ *(['"])`

## トラブルシューティング {#troubleshooting}

デザインパッケージの読み込み時に発生する可能性のあるいくつかのエラーについて説明します。

### ランディングページに関連するコンポーネントによるサイドキックの初期化 {#initialization-of-sidekick-with-landing-page-relevant-components}

デザインパッケージに parsys コンポーネントのマークアップが含まれる場合、読み込み後のサイドキックには最初、ランディングページに関連するコンポーネントが表示されます。新しいコンポーネントを、ランディングページ内の parsys コンポーネントにドラッグ＆ドロップすることができます。また、デザインモードに移動して、新しいコンポーネントをサイドキックに追加することもできます。

### 読み込み時に表示されるエラーメッセージ {#error-messages-displayed-during-import}

読み込まれたパッケージが有効な zip ファイルではない、などのエラーが発生した場合、デザインインポーターではパッケージの読み込みが行われず、ページの上部（ドラッグ＆ドロップボックスのすぐ上）にエラーメッセージが表示されます。エラーが発生するシナリオの例を以下に示します。エラーを修正したら、更新した zip ファイルを同じ空白のランディングページに再読み込みすることができます。次のような様々なシナリオでエラーがスローされます。

* 読み込まれたデザインパッケージが有効な zip アーカイブではない。
* 読み込まれたデザインパッケージの最上位レベルに index.html が含まれていない。

### 読み込み後に表示される警告 {#warnings-displayed-after-import}

HTML が参照する画像がパッケージ内に存在しない、などの警告が発生した場合、デザインインポーターでは zip ファイルの読み込みが行われますが、同時に問題や警告のリストが結果ウィンドウに表示されます。問題のリンクをクリックすると、デザインパッケージ内の問題を示す警告のリストが表示されます。次のような様々なシナリオで警告が発生し、デザインインポーターによって表示されます。

* HTML が参照する画像がパッケージ内に存在しません。
* HTML が参照するスクリプトがパッケージ内に存在しません。
* HTML が参照するスタイルがパッケージ内に存在しません。

### AEM で zip ファイルの各ファイルが格納されている場所 {#where-are-the-files-of-the-zip-file-being-stored-in-aem}

ランディングページが読み込まれた後、デザインパッケージ内のファイル（画像、CSS、js など）はAEM の次の場所に格納されます。

`/etc/designs/default/canvas/content/campaigns/<name of brand>/<name of campaign>/<name of landing page>`

ランディングページが We.Retail キャンペーンに作成され、このランディングページの名前が **myBlankLandingPage** である場合、zip ファイルが格納される場所は次のとおりです。

`/etc/designs/default/canvas/content/campaigns/geometrixx/myBlankLandingPage`

### 保持されない書式 {#formatting-not-preserved}

CSS を作成するときには、次の制限事項に注意してください。

テキストと（編集可能な）画像が次のような場合：

```xml
<div class="box">
<p><div data-cq-component="image"><img src="assets/image.jpg" width="115"
height="116" /></div>Some Text </p>
</div>
```

さらに、CSS が次のように `box` クラスに適用されている場合：

```xml
.box

{ width: 450px; padding:10px; border: 1px #C5DBE7 solid; margin: 0px auto 0 auto; background-image:url(assets/box.gif); background-repeat:repeat-x,y; font-family:Verdana, Arial, Helvetica, sans-serif; font-size:12px; color:#6D6D6D; }
```

`box img` がデザインインポーターで使用され、読み込んだ後のランディングページは書式が保持されていないように見えます。この問題の回避策として、AEM では CSS に div タグが追加され、その結果コードが書き換えられるということに注意してください。これを怠ると、CSS ルールが無効になる場合があります。

```xml
.box img

{ float:right; margin: 0 0 5px 5px; border: 1px #343434 solid; }
```

>[!NOTE]
また、デザイナーはデザインインポーターが **id=cqcanvas** タグ内のコードのみを認識することに注意してください。これを怠ると、デザインが保持されなくなります。
