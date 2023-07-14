---
title: ランディングページ用のデザインインポーターの拡張と設定
description: ランディングページ用のデザインインポーターの設定方法を説明します。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
docset: aem65
exl-id: 1b8c6075-13c6-4277-b726-8dea7991efec
source-git-commit: 260f71acd330167572d817fdf145a018b09cbc65
workflow-type: tm+mt
source-wordcount: '3502'
ht-degree: 34%

---

# ランディングページ用のデザインインポーターの拡張と設定{#extending-and-configuring-the-design-importer-for-landing-pages}

ここでは、ランディングページのデザインインポーターを設定し、必要に応じて拡張する方法について説明します。 読み込み後のランディングページの使用については、 [ランディングページ。](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md)

**デザインインポーターにカスタムコンポーネントを抽出させる**

次に、デザインインポーターがカスタムコンポーネントを認識するための論理的な手順を示します

1. TagHandler の作成

   * タグハンドラーは、特定の種類の HTML タグを処理する POJO です。TagHandler が処理できるHTMLタグの「種類」は、TagHandlerFactory の OSGi プロパティ「tagpattern.name」を介して定義されます。 この OSGi プロパティは基本的に、処理する入力 html タグに一致する正規表現です。 ネストされたタグはすべて、処理のためにタグハンドラーにスローされます。 例えば、ネストされた &lt;p> タグ、 &lt;p> タグが TagHandler にもスローされます。このタグの扱い方は、ユーザーが自由に設定できます。
   * タグハンドラーインターフェイスは、SAX コンテンツハンドラーインターフェイスに似ています。 各 html タグの SAX イベントを受け取ります。 タグハンドラープロバイダーは、デザインインポーターフレームワークによって自動的に呼び出される特定のライフサイクルメソッドを実装する必要があります。

1. 対応する TagHandlerFactory を作成します。

   * タグハンドラーファクトリは、タグハンドラーのインスタンスの生成を担当する OSGi コンポーネント (singleton) です。
   * タグハンドラーファクトリは、「tagpattern.name」と呼ばれる OSGi プロパティを公開する必要があります。このプロパティの値は、入力された HTML タグと一致させます。
   * 入力された HTML タグと一致するタグハンドラーが複数ある場合は、順位の高いタグハンドラーが選択されます。この順位は OSGi プロパティ **service.ranking** として公開されています。
   * TagHandlerFactory は OSGi コンポーネントです。 TagHandler に提供する参照は、すべてこのファクトリを介して存在する必要があります。

1. デフォルトの順位を変更する場合は、必ず TagHandlerFactory でより望ましい順位を設定します。

>[!CAUTION]
>
>ランディングページの読み込みに使用するデザインインポーター [はAEM 6.5 で非推奨（廃止予定）になりました。](/help/release-notes/deprecated-removed-features.md#deprecated-features).

## 読み込むHTMLの準備 {#preparing-the-html-for-import}

インポーターページを作成したら、完全なHTMLランディングページを読み込むことができます。 HTMLのランディングページを読み込むには、まずその内容をデザインパッケージに zip 形式で圧縮する必要があります。 デザインパッケージには、HTMLのランディングページと参照元のアセット（画像、CSS、アイコン、スクリプトなど）が含まれています。

次の参照シートは、読み込み用のHTMLの準備方法の例です。

ランディングページ参照シート

[ファイルを入手](assets/cheatsheet.zip)

### Zip ファイルのレイアウトと要件 {#zip-file-layout-and-requirements}

>[!NOTE]
>
>この時点で、ZIP ファイルには、1 つのHTMLページまたは 1 つのページの一部のみ含めることができます。

zip のサンプルレイアウトを次に示します。

* /index.html -> ランディングページHTMLファイル
* /css -> を CSS clientlib に追加する
* /img -> すべての画像とアセット
* /js -> を JS clientlib に追加する場合

このレイアウトは、HTML5 Boilerplate のレイアウトのベストプラクティスに基づいています。詳しくは、[https://html5boilerplate.com/](https://html5boilerplate.com/) を参照してください。

>[!NOTE]
>
>少なくとも、デザインパッケージ **必須** 含む **index.html** ファイルをルートレベルに配置します。 読み込むランディングページにモバイルバージョンも含まれている場合、zip ファイルには **mobile.index.html** と一緒に **index.html** をルートレベルに設定します。

### ランディングページの準備HTML {#preparing-the-landing-page-html}

HTMLを読み込むには、ランディングページHTMLにキャンバス div を追加する必要があります。

canvas div は `id="cqcanvas"` を含む HTML **div** です。この div を HTML の `<body>` タグ内に挿入し、変換対象のコンテンツを囲む必要があります。

キャンバス div を追加した後のランディングページHTMLのサンプルスニペットを次に示します。

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

### 編集可能なAEMコンポーネントを含めるHTMLの準備 {#preparing-the-html-to-include-editable-aem-components}

ランディングページを読み込む場合、ページをそのまま読み込むこともできます。つまり、ランディングページを読み込んだ後は、読み込んだ項目をAEMで編集することはできません ( ページにAEMコンポーネントを追加できます )。

ランディングページを読み込む前に、ランディングページの一部のパーツを編集可能な AEM コンポーネントに変換することができます。これにより、ランディングページデザインを読み込んだ後も、ランディングページの一部をすばやく編集することができます。

パーツを変換するには、読み込む HTML ファイル内の適切なコンポーネントに `data-cq-component` を追加します。

次の節では、ランディングページの特定の部分を様々な編集可能なAEMコンポーネントに変換できるようにHTMLファイルを編集する方法について説明します。 コンポーネントについて詳しくは、 [ランディングページコンポーネント](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md).

>[!NOTE]
>
>ランディングページの一部をAEMコンポーネントに変換するHTMLマークアップは、長い形式と短縮形のタグ宣言の両方を持ちます。 それぞれのコンポーネントについて説明します。

### 制限事項 {#limitations}

読み込む前に、次の制限事項に注意してください。

### タグに適用された class や id などの属性は &amp;lt;body> タグは保持されません {#any-attribute-like-class-or-id-applied-on-the-amp-lt-body-tag-is-not-preserved}

id や class などの属性が body タグに適用されている場合（例：`<body id="container">`）、この属性は読み込み後に保持されません。したがって、読み込むデザインは、`<body>` タグに適用されている属性に依存しないようにしてください。

### zip ファイルのドラッグ＆ドロップ {#drag-and-drop-zip}

ドラッグ＆ドロップによる zip ファイルのアップロードは、Internet Explorer および Firefox バージョン 3.6 以前ではサポートされていません。これらのブラウザーを使用してデザインをアップロードするには、ファイルのドロップゾーンをクリックしてファイルのアップロードダイアログボックスを開き、そのダイアログを使用してデザインをアップロードします。

デザイン zip の「ドラッグ&amp;ドロップ」をサポートするブラウザーは、Chrome、Safari5.x、Firefox 4 以降です。

### Modernizr はサポートされない {#modernizr-is-not-supported}

`Modernizr.js` は、ブラウザーのネイティブ機能を検出し、html5 要素に適しているかどうかを検出する JavaScript ベースのツールです。 様々なブラウザーの古いバージョンのサポートを強化するために Modernizr が使用されているデザインを読み込むと、ランディングページソリューションで問題が発生する場合があります。`Modernizr.js` スクリプトは、デザインインポーターではサポートされていません。

### デザインパッケージの読み込み時に、ページのプロパティが保持されない {#page-properties-are-not-preserved-at-the-time-of-importing-design-package}

デザインパッケージを読み込む前にページ用に設定されたページプロパティ（カスタムドメイン、HTTPS の適用など）は、デザインが読み込まれると失われます。 したがって、デザインパッケージを読み込んだ後でページのプロパティを設定することをお勧めします。

### HTMLのみのマークアップを想定 {#html-only-markup-assumed}

読み込み時には、セキュリティ上の理由から、マークアップが不要になり、無効なマークアップの読み込みと公開を避けるために、不要なマークアップが削除されます。 この場合、HTMLのみのマークアップと、インラインSVGや Web コンポーネントなどの他の形式の要素がすべて除外されると想定します。

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

**リストを含むテキスト**

リストを含むテキストを追加するには：

* 1st
* 2nd

RTE エディターで編集できる

```xml
<div data-cq-component="text"><p>This is text with a list:</p><ul><li>1st</li><li>2nd</li></ul><p>It can be edited with the RTE editor</p></div>
```

**色付きテキスト**

RTE エディターで編集できる色（ピンク）のテキストを追加するには：

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

タイトルコンポーネントは、次の 7 つのタイプをサポートします。 `h1, h2, h3, h4, h5, h6` および `default`.

**短縮形のコンポーネントタグ宣言**：

```xml
<h1 data-cq-component="title">Title component shorthand</h1>
```

### 画像 {#image}

HTMLコンポーネント (foundation/components/image) をデザインパッケージ内のHTMLに挿入するための画像マークアップを次に示します。

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

#### 絶対 URL img src は、画像コンポーネント Div 内でサポートされていません {#absolute-url-img-src-not-supported-within-image-component-div}

コンポーネントを変換するために、絶対 URL の src を持つ`<img>`タグを設定すると、対応する **UnsupportedTagContentException** が発生します。例えば、次のような記述はサポートされません。

`<div data-cq-component="image">`

`<img src="https://cdn.printfriendly.com/pf-button.gif" alt="Print Friendly and PDF"/>`

`</div>`

ただし、それ以外の場合は、画像コンポーネント div に含まれていない img タグで、絶対 URL 画像がサポートされます。

### コールトゥアクションコンポーネント {#call-to-action-components}

ランディングページの一部を「編集可能なコールトゥアクションコンポーネント」として読み込むようにマークできます。読み込まれたコールトゥアクションコンポーネントは、ランディングページの読み込み後に編集できます。 AEMには、次の CTA コンポーネントが含まれています。

* クリックスルーリンク — クリックすると訪問者がターゲット URL に移動するテキストリンクを追加できます。
* グラフィカルリンク — クリックすると訪問者がターゲット URL に移動する画像を追加できます。

#### クリックスルーリンク {#click-through-link}

この CTA コンポーネントを使用して、ランディングページにテキストリンクを追加できます。

サポートされるプロパティ

* ラベル（太字、斜体、下線オプション付き）
* Target URL。サードパーティおよびAEMの URL をサポート
* ページレンダリングオプション（同じウィンドウ、新しいウィンドウなど）

HTMLタグを使用して、読み込んだ zip ファイルにクリックスルーコンポーネントを含めます。 ここで、href はターゲット URL に、「製品の詳細を表示」はラベルにマッピングされます。

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

このコンポーネントは、任意のスタンドアロンアプリケーションで使用することも、zip から読み込むこともできます。

**短縮形のコンポーネントタグ宣言**：

```xml
<a href="/somelink.html" data-cq-component="clickThroughLink">Click Through Link shorthand</a>
```

#### グラフィックリンク {#graphical-link}

この CTA コンポーネントを使用して、ランディングページにリンクを含む任意のグラフィカル画像を追加できます。 画像は、単純なボタンでも、背景としての任意のグラフィカル画像でもかまいません。 画像をクリックすると、コンポーネントプロパティで指定されたターゲット URL に移動します。 これは「コールトゥアクション」グループの一部です。

サポートされるプロパティ

* 画像の切り抜き、回転
* カーソルを合わせたときのテキスト、説明、サイズ（ピクセル）
* Target URL。サードパーティおよびAEMの URL をサポート
* ページレンダリングオプション（同じウィンドウ、新しいウィンドウなど）

HTML タグを使用して、読み込まれた zip ファイルにグラフィックリンクコンポーネントを含めます。ここでは、href がターゲット URL にマッピングされ、img src がレンダリング画像で、「title」がホバーテキストとして取られます。

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
>CSS を使用して画像をアンカータグに関連付けるその他の方法はサポートされていません。 例えば、次のマークアップは機能しません。
>
>`<div data-cq-component="clickthroughgraphicallink">`
>
>`<a class="hasBackground" href="https://myURLhere/"></a>`
>
>`</div>`
>
>関連する `css .hasbackground { background-image: pathtoimage }` とともに
>

### リードフォーム {#lead-form}

リードフォームとは、訪問者/リードのプロファイル情報を収集するために使用されるフォームです。 この情報を保存し、後でその情報に基づいて効果的なマーケティングを行うことができます。 この情報には、通常、タイトル、名前、E メール、生年月日、住所、興味などが含まれます。 このコンポーネントは「CTA リードフォーム」グループに含まれています。

**サポートされている機能**

* 事前定義されたリードフィールド - 名、姓、住所、生年月日、性別、詳細情報、ユーザー ID、メール ID、送信ボタンがサイドキックで使用できます。必要なコンポーネントをリードフォームにドラッグ＆ドロップするだけで使用できます。
* これらのコンポーネントを使用して、作成者がスタンドアロンのリードフォームをデザインできます。これらのフィールドはリードフォームフィールドに対応しています。スタンドアロンまたは読み込まれた zip アプリケーションでは、cq:form または cta リードフォームのフィールド、名前、および要件に従って設計を使用して、追加のフィールドを追加できます。
* 特定の事前定義された CTA リードフォーム名を使用してフォームフィールドをマッピングします。例えば、firstName をリードフォームの名にマッピングしたりします。
* リードフォームが cq:form コンポーネントにマッピングされないフィールド — テキスト、ラジオ、チェックボックス、ドロップダウン、非表示、パスワード。
* ユーザーは「ラベル」タグを使用してタイトルを設定し、スタイル属性「クラス」を使用してスタイルを設定することができます（CTA リードフォームコンポーネントでのみ使用可能）。
* 「ありがとうございます」ページや購読リストをフォームの非表示パラメーターとして設定（index.htm 内）するか、「リードフォームの最初」の編集バーから追加または編集することができます。

  &lt;input type=&quot;hidden&quot; name=&quot;redirectUrl&quot; value=&quot;/content/we-retail/en/user/register/thank_you&quot;/>

  &lt;input type=&quot;hidden&quot; name=&quot;groupName&quot; value=&quot;leadForm&quot;/>

* required（必須）などの制約を、各コンポーネントの編集設定から指定することができます。

HTML タグを使用して、読み込まれた zip ファイルにグラフィックリンクコンポーネントを含めます。ここでは、「firstName」がリードフォームの firstName にマッピングされます。チェックボックスを除き、これら 2 つのチェックボックスは cq:form ドロップダウンコンポーネントにマッピングされます。

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

### Parsys {#parsys}

AEM parsys コンポーネントは、他のAEMコンポーネントを含むことができるコンテナコンポーネントです。 読み込んだHTMLに parsys コンポーネントを追加できます。 これにより、ユーザーは、読み込んだ後でも、編集可能なAEMコンポーネントをランディングページに追加/削除できます。

段落システムを使用すると、ユーザーはサイドキックを使用してコンポーネントを追加できます。

parsys コンポーネント（`foundation/components/parsys`）をデザインパッケージ内の HTML に挿入するための HTML マークアップを次に示します。

```xml
<div data-cq-component="parsys">
   <div data-cq-component="title"><h2>ULTIMATE PROTECTION</h2></div>
        <div data-cq-component="title"><h3>ON SALE</h3></div>
</div>
```

上記のマークアップをHTMLに含めると、次の処理がおこなわれます。

* デザインパッケージの読み込み後に作成されたランディングページにAEM parsys コンポーネント (foundation/components/parsys) を挿入します。
* サイドキックをデフォルトのコンポーネントで初期化します。 新しいコンポーネントは、サイドキックから parsys コンポーネントにコンポーネントをドラッグすることで、ランディングページに追加できます。
* 2 つのタイトルコンポーネントも parsys の一部です。

### ターゲット {#target}

ターゲットコンポーネントは、ページ上のエクスペリエンスのコンテンツを表示します。 1 つのキャンペーンで多数のエクスペリエンスを作成でき、ターゲットコンポーネントで、異なるエクスペリエンスのコンテンツを、ページを訪問する様々なユーザーに動的に表示できます。

ターゲットコンポーネントを挿入し、キャンペーン内に様々なエクスペリエンスを作成するための HTML マークアップ：

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

## その他のインポートオプション {#additional-importing-options}

読み込まれたコンポーネントを編集可能なAEMコンポーネントにするかどうかを指定する以外に、デザインパッケージを読み込む前に次の設定を行うこともできます。

* 読み込まれたページで定義されたメタデータを抽出してページのプロパティをHTMLします。
* HTMLで文字セットエンコーディングを指定する。
* インポーターページテンプレートのオーバーレイ

### 読み込まれたHTMLで定義されたメタデータを抽出してページプロパティを設定する {#setting-page-properties-by-extracting-metadata-defined-in-imported-html}

読み込まれたHTMLの先頭で宣言された次のメタデータは、デザインインポーターによってプロパティ「jcr:description」として抽出され、保持されます。

* &lt;meta name=&quot;description&quot; content=&quot;&quot;>

HTMLタグに設定された Lang 属性は、デザインインポーターによってプロパティ「jcr:language」として抽出され、保持されます。

* &lt;html lang=&quot;en&quot;>

### html での文字セットエンコーディングの指定 {#specifying-the-charset-encoding-in-the-html}

デザインインポーターは、読み込まれたHTMLで指定されたエンコーディングを読み取ります。 エンコーディングは次のように指定できます。

`<meta charset="UTF-8">`

*または*

`<meta http-equiv="content-type" content="text/html;charset=utf-8">`

読み込んだHTMLでエンコーディングが指定されていない場合、デザインインポーターによって設定されたデフォルトのエンコーディングは UTF-8 になります。

### テンプレートのオーバーレイ {#overlaying-template}

空白のランディングページテンプレートをオーバーレイするには、`/apps/<appName>/designimporter/templates/<templateName>` でオーバーレイを新規作成します。

AEM のテンプレートを新規作成する手順については、[こちら](/help/sites-developing/templates.md)を参照してください。

### ランディングページからのコンポーネントの参照 {#referring-a-component-from-landing-page}

data-cq-component 属性を使用してHTMLで参照するコンポーネントがあり、デザインインポーターがこの場所にコンポーネントをレンダリングするとします。 例えば、テーブルコンポーネント ( `resourceType = /libs/foundation/components/table`) をクリックします。 この場合、HTML に次の行を追加する必要があります。

`<div data-cq-component="/libs/foundation/components/table">foundation table</div>`

data-cq-component 内のパスは、コンポーネントの resourceType にする必要があります。

### ベストプラクティス {#best-practices}

読み込み時のコンポーネント変換用にマークされた要素では、次の CSS セレクターと同様の CSS セレクターを使用することはお勧めしません。

| E > F | E 要素の F 要素の子 | [子結合子](https://www.w3.org/TR/css3-selectors/#child-combinators) |
|---|---|---|
| E + F | F 要素の直前に E 要素が付く | [隣接兄弟結合子](https://www.w3.org/TR/css3-selectors/#adjacent-sibling-combinators) |
| E ～ F | F 要素の前に E 要素が付く | [一般兄弟結合子](https://www.w3.org/TR/css3-selectors/#general-sibling-combinators) |
| E:root | E 要素、ドキュメントのルート | [構造擬似クラス](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-child(n) | E 要素（親の n 番目の子） | [構造擬似クラス](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-last-child(n) | E 要素（親の n 番目の子）で、最後の要素から数えています | [構造擬似クラス](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-of-type(n) | E 要素（その型の n 番目の兄弟） | [構造擬似クラス](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-last-of-type(n) | E 要素は、その型の n 番目の兄弟で、最後の要素から数えています | [構造擬似クラス](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |

これは、 &lt;div> タグは、インポート後に生成された Html に追加されます。

* 上記と同様の構造に依存するスクリプトは、AEMコンポーネントへの変換用にマークされた要素で使用することはお勧めしません。
* &lt;div data-cq-component=&quot;&amp;ast;&quot;> などコンポーネントの変換用のマークアップタグに、スタイルを使用することは推奨されません。
* デザインレイアウトは、HTML5 Boilerplate のベストプラクティスに従って作成する必要があります。詳しくは、[https://html5boilerplate.com/](https://html5boilerplate.com/) を参照してください。

## OSGi モジュールの設定 {#configuring-osgi-modules}

OSGi コンソールから設定可能なプロパティを公開するコンポーネントを次に示します。

* ランディングページデザインインポーター
* ランディングページビルダー
* モバイルランディングページビルダー
* ランディングページエントリプリプロセッサ

次の表で、プロパティについて簡単に説明します。

<table>
 <tbody>
  <tr>
   <td><strong>コンポーネント</strong></td>
   <td><strong>プロパティ名</strong></td>
   <td><strong>プロパティの説明 </strong></td>
  </tr>
  <tr>
   <td>ランディングページデザインインポーター</td>
   <td>フィルターを抽出</td>
   <td>抽出したファイルのフィルター時に使用する正規表現のリスト。<br />指定したいずれかのパターンに一致する zip エントリは、抽出から除外されます。</td>
  </tr>
  <tr>
   <td>ランディングページビルダー</td>
   <td>ファイルパターン</td>
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
   <td>サポートするデバイスグループのリスト。</td>
  </tr>
  <tr>
   <td>ランディングページエントリプリプロセッサ</td>
   <td>Search Pattern </td>
   <td>アーカイブエントリコンテンツ内で検索するパターン。この正規表現とエントリコンテンツは、行ごとに照合されます。一致した場合、一致したテキストは指定の置換パターンに置き換えられます。<br /><br />ランディングページエントリプリプロセッサーの現在の制限事項については、下記のメモを参照してください。</td>
  </tr>
  <tr>
   <td> </td>
   <td>パターンを置換</td>
   <td>見つかった一致を置き換えるパターン。 $1、$2 など、正規表現のグループ参照を使用できます。また、このパターンでは、 {designPath} インポート時に実際の値で解決される</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>**ランディングページエントリプリプロセッサの現在の制限：**
>検索パターンを変更する必要がある場合は、felix プロパティエディターを開く際に、バックスラッシュ文字を手動で追加して正規表現のメタ文字をエスケープする必要があります。 バックスラッシュを手動で追加しない場合、正規表現は無効と見なされ、古い文字は置き換えられません。
>
>例えば、デフォルトの設定が
>
>>`/\* *CQ_DESIGN_PATH *\*/ *(['"])`
>
>また、検索パターン内で`CQ_DESIGN_PATH`を `VIPURL` と置換する必要がある場合、検索パターンは次のようになります。
>
>`/\* *VIPURL *\*/ *(['"])`

## トラブルシューティング {#troubleshooting}

デザインパッケージを読み込む際に、この節で説明する複数のエラーが発生する場合があります。

### ランディングページ関連コンポーネントを使用したサイドキックの初期化 {#initialization-of-sidekick-with-landing-page-relevant-components}

デザインパッケージに parsys コンポーネントマークアップが含まれている場合、読み込み後にサイドキックにランディングページ関連のコンポーネントが表示され始めます。 新しいコンポーネントは、ランディングページ内の parsys コンポーネントにドラッグ&amp;ドロップできます。 デザインモードに移動して、新しいコンポーネントをサイドキックに追加することもできます。

### 読み込み時に表示されるエラーメッセージ {#error-messages-displayed-during-import}

エラーが発生した場合（例えば、読み込まれたパッケージが有効な zip ではない場合など）、デザインの読み込みではパッケージは読み込まれません。 代わりに、ページ上部のドラッグ&amp;ドロップボックスのすぐ上にエラーメッセージが表示されます。 エラーシナリオの例をここに示します。 エラーを修正した後、更新した zip を同じ空白のランディングページに再読み込みできます。 エラーがスローされる様々なシナリオを次に示します。

* 読み込まれたデザインパッケージは有効な zip アーカイブではありません。
* 読み込まれたデザインパッケージの最上位レベルに index.html が含まれていない。

### 読み込み後に表示される警告 {#warnings-displayed-after-import}

警告がある場合 ( 例えば、HTMLがパッケージ内に存在しない画像を参照する場合など ) は、その zip を読み込むと同時に結果ウィンドウに問題/警告の一覧を表示します。 次のような様々なシナリオで警告が発生し、デザインインポーターによって表示されます。

* HTML が参照する画像がパッケージ内に存在しません。
* HTML が参照するスクリプトがパッケージ内に存在しません。
* HTML が参照するスタイルがパッケージ内に存在しません。

### ZIP ファイルのファイルはAEMのどこに保存されていますか？ {#where-are-the-files-of-the-zip-file-being-stored-in-aem}

ランディングページが読み込まれると、デザインパッケージ内のファイル（画像、CSS、JS など）はAEMの次の場所に保存されます。

`/etc/designs/default/canvas/content/campaigns/<name of brand>/<name of campaign>/<name of landing page>`

ランディングページが We.Retail キャンペーンの下に作成され、ランディングページの名前が **myBlankLandingPage** Zip ファイルが保存されていた場所は次のようになります。

`/etc/designs/default/canvas/content/campaigns/geometrixx/myBlankLandingPage`

### 書式が保持されません {#formatting-not-preserved}

CSS を作成する際は、次の制限事項に注意してください。

テキストおよび（編集可能な）画像が次のような場合：

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

次に、 `box img` がデザインインポーターで使用されると、生成されるランディングページの形式が保持されていないように見えます。 この問題を回避するために、AEMは CSS に div タグを追加し、それに応じてコードを書き換えます。 そうしないと、一部の CSS ルールが無効になります。

```xml
.box img

{ float:right; margin: 0 0 5px 5px; border: 1px #343434 solid; }
```

>[!NOTE]
>
>また、デザイナーはデザインインポーターが **id=cqcanvas** タグ内のコードのみを認識することに注意してください。これを怠ると、デザインが保持されなくなります。
