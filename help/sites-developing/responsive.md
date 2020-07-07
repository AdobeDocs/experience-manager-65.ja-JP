---
title: Webページ用レスポンシブデザイン
seo-title: Webページ用レスポンシブデザイン
description: レスポンシブデザインを使用すると、同じページを複数のデバイスで、複数の向きで効果的に表示できます
seo-description: レスポンシブデザインを使用すると、同じページを複数のデバイスで、複数の向きで効果的に表示できます
uuid: 3d324557-e7ff-4c82-920f-9b5a906925e8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
discoiquuid: 532544b0-1932-419a-b6bd-ecf57a926fef
legacypath: /content/docs/en/aem/6-0/develop/mobile/responsive
translation-type: tm+mt
source-git-commit: ebf3f34af7da6b1a659ac8d8843152b97f30b652
workflow-type: tm+mt
source-wordcount: '5339'
ht-degree: 63%

---


# Web ページのレスポンシブデザイン{#responsive-design-for-web-pages}

>[!NOTE]
>
>Adobe recommends using the SPA Editor for projects that require single page application framework-based client-side rendering (such as _React_). [詳細情報](/help/sites-developing/spa-overview.md)を参照してください。


Web ページが表示されるクライアントの表示域に適応するように Web ページをデザインします。レスポンシブデザインを使用すると、同じページを複数のデバイスで、縦、横の両方の向きで効果的に表示できます。次の画像の例は、表示域サイズの変更に対してページがどのように応答するかを示しています。

* レイアウト：表示域が小さい場合は 1 列レイアウトを使用し、表示域が大きい場合は複数列レイアウトを使用します。
* テキストサイズ：表示域が大きい場合は、（見出しなどの適切な箇所で）大きいテキストサイズを使用します。
* コンテンツ：小型デバイスに表示する場合は、重要なコンテンツのみを表示します。
* ナビゲーション：他のページにアクセスするためのデバイス専用のツールを提供します。
* 画像：ウィンドウのサイズに応じて、クライアントの表示域に適した画像レンディションを配信します。

![chlimage_1-4](assets/chlimage_1-4a.png)

複数のウィンドウサイズと向きに適応可能な HTML5 ページを生成する Adobe Experience Manager（AEM）アプリケーションを開発します。例えば、次のような表示域の幅の範囲が、様々なデバイスタイプと向きに対応します。

* 幅 480 ピクセル以下（携帯電話、縦置き）
* 幅 767 ピクセル以下（携帯電話、横置き）
* 幅 768 ～ 979 ピクセル（タブレット、縦置き）
* 幅 980 ～ 1,199 ピクセル（タブレット、横置き）
* 幅 1,200 ピクセル以上（デスクトップ）

レスポンシブデザインの動作の実装について詳しくは、次のトピックを参照してください。

* [メディアクエリ](/help/sites-developing/responsive.md#using-media-queries)
* [可変グリッド](/help/sites-developing/responsive.md#developing-a-fluid-grid)
* [アダプティブ画像](/help/sites-developing/responsive.md#using-adaptive-images)

As you design, use **[!UICONTROL Sidekick]** to preview your pages for various screen sizes.

## Before you develop {#before-you-develop}

Web ページをサポートする AEM アプリケーションを開発する前に、デザインについていくつかの決定をおこなう必要があります。例えば、次の情報が必要になります。

* ターゲットとするデバイス
* ターゲットの表示域サイズ
* ターゲットの表示域サイズごとのページレイアウト

### Application structure {#application-structure}

次のような一般的な AEM アプリケーション構造により、すべてのレスポンシブデザイン実装をサポートできます。

* ページコンポーネント：/apps/*application_name*/components 以下に存在
* テンプレート：/apps/*application_name*/templates 以下に存在
* デザイン：/etc/designs 以下に存在

## Using media queries {#using-media-queries}

メディアクエリによって、ページレンダリング用の CSS スタイルを選択的に使用できます。AEM 開発ツールおよび機能を使用すれば、アプリケーションでメディアクエリを効果的かつ効率的に実装できます。

The W3C group provides the [Media Queries](https://www.w3.org/TR/css3-mediaqueries/) recommendation that describes this CSS3 feature and the syntax.

### Creating the CSS file {#creating-the-css-file}

CSS ファイルでは、ターゲットとしているデバイスのプロパティに基づいてメディアクエリを定義します。次の実装方法は、各メディアクエリのスタイルを管理するのに効果的です。

* ClientLibraryFolder を使用して、ページのレンダリング時に組み立てられる CSS を定義します。
* 各メディアクエリおよび関連するスタイルを、それぞれ個別の CSS ファイルで定義します。メディアクエリのデバイスの特徴を表したファイル名を使用すると便利です。
* すべてのデバイスに共通するスタイルを、個別の 1 つの CSS ファイルで定義します。
* ClientLibraryFolder の css.txt ファイルで、組み立てられた CSS ファイル内で必要とされる順に CSS ファイルを並べます。

We.Retail Media サンプルではこの実装方法を使用して、サイトデザインのスタイルを定義しています。The CSS file used by We.Retail is located at `*/apps/weretail/clientlibs/clientlib-site/less/grid.less`.

次の表に、css 子フォルダー内のファイルを示します。

<table>
 <tbody>
  <tr>
   <th>ファイル名</th>
   <th>説明</th>
   <th>メディアクエリー</th>
  </tr>
  <tr>
   <td>style.css</td>
   <td>共通のスタイル。</td>
   <td>該当なし</td>
  </tr>
  <tr>
   <td>bootstrap.css</td>
   <td>共通のスタイル（Twitter Bootstrap による定義）。</td>
   <td>該当なし</td>
  </tr>
  <tr>
   <td>responsive-1200px.css</td>
   <td>幅 1,200 ピクセル以上のすべてのメディア用のスタイル。</td>
   <td><p>@media (min-width: 1200px) {<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-980px-1199px.css</td>
   <td>幅 980 ～ 1,199 ピクセルのメディア用のスタイル。</td>
   <td><p>@media (min-width: 980px) and (max-width: 1199px) {<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-768px-979px.css</td>
   <td>幅 768 ～ 979 ピクセルのメディア用のスタイル。 </td>
   <td><p>@media (min-width: 768px) and (max-width: 979px) {<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-767px-max.css</td>
   <td>幅 768 ピクセル未満のすべてのメディア用のスタイル。</td>
   <td><p>@media (max-width: 767px) {<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-480px.css</td>
   <td>幅 481 ピクセル未満のすべてのメディア用のスタイル。</td>
   <td>@media (max-width: 480) {<br /> ...<br /> }</td>
  </tr>
 </tbody>
</table>

The css.txt file in the `/etc/designs/weretail/clientlibs` folder lists the CSS files that the client library folder includes. ファイルの記載順序により、スタイルの優先順位が実装されます。スタイルは、デバイスのサイズが小さくなるほど特化されます。

`#base=css`

```
style.css
 bootstrap.css
```

```
responsive-1200px.css
 responsive-980px-1199px.css
 responsive-768px-979px.css
 responsive-767px-max.css
 responsive-480px.css
```

**ヒント**: 説明的なファイル名を使用すると、対象となるビューポートサイズを簡単に識別できます。

### AEM ページでのメディアクエリの使用 {#using-media-queries-with-aem-pages}

ページコンポーネントの JSP スクリプトにクライアントライブラリフォルダーを含めることで、メディアクエリを含む CSS ファイルを生成し、そのファイルを参照できます。

```xml
<ui:includeClientLib categories="apps.weretail.all"/>
```

>[!NOTE]
>
>The `apps.weretail.all` client library folder embeds the clientlibs library.

この JSP スクリプトにより、スタイルシートを参照する次の HTML コードが生成されます。

```xml
<link rel="stylesheet" href="/etc/designs/weretail/clientlibs-all.css" type="text/css">
<link href="/etc/designs/weretail.css" rel="stylesheet" type="text/css">
```

## Previewing for specific devices {#previewing-for-specific-devices}

異なる表示域サイズでページのプレビューを参照して、レスポンシブデザインの動作をテストします。**[!UICONTROL プレビューモードでは、]** サイドキックに **[!UICONTROL 「デバイス]****** 」ドロップダウンメニューが含まれ、デバイスを選択できます。 デバイスを選択すると、その表示域サイズに合わせてページが変更されます。

![chlimage_1-5](assets/chlimage_1-5a.png)

To enable the device preview in **[!UICONTROL Sidekick]**, you must configure the page and the **[!UICONTROL MobileEmulatorProvider]** service. Another page configuration controls the list of devices that appears in the **[!UICONTROL Devices]** list.

### 「デバイス」リストの追加{#adding-the-devices-list}

「 **[!UICONTROL Devices]** 」 **[!UICONTROL リストは、]** Devices **** リストをレンダリングするJSPスクリプトがページに含まれている場合、サイドキックに表示されます。 サイドキックに **[!UICONTROL デバイス]** リストを追加するには **[!UICONTROL 、ページの]**`/libs/wcm/mobile/components/simulator/simulator.jsp``head` セクションにスクリプトを含めます。

この `head` セクションを定義している JSP で次のコードをインクルードします。

`<cq:include script="/libs/wcm/mobile/components/simulator/simulator.jsp"/>`

To see an example, open the `/apps/weretail/components/page/head.jsp` file in CRXDE Lite.

### Registering Page components for simulation {#registering-page-components-for-simulation}

デバイスシミュレーターを有効にしてページで使用できるようにするには、MobileEmulatorProvider ファクトリサービスによってページコンポーネントを登録して `mobile.resourceTypes` プロパティを定義します。

AEM と連携する場合は、いくつかの方法でこのようなサービスの設定を管理できます。詳しくは、[OSGi の設定](/help/sites-deploying/configuring-osgi.md)を参照してください。

例えば、アプリケーションで ` [sling:OsgiConfig](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository)` ノードを作成するには、次のように設定します。

* Parent folder: `/apps/application_name/config`
* 名前：`com.day.cq.wcm.mobile.core.impl.MobileEmulatorProvider-*alias*`

   The - `*alias*` suffix is required because the MobileEmulatorProvider service is a factory service. このファクトリで一意となる任意のエイリアスを使用します。

* jcr:primaryType: `sling:OsgiConfig`

次のノードプロパティを追加します。

* 名前：`mobile.resourceTypes`
* 型：`String[]`
* 値： Webページをレンダリングするページコンポーネントへのパス。 例えば、geometrixx-mediaアプリでは次の値が使用されます。

   ```
   geometrixx-media/components/page
    geometrixx-unlimited/components/pages/page
    geometrixx-unlimited/components/pages/coverpage
    geometrixx-unlimited/components/pages/issue
   ```

### Specifying the device groups {#specifying-the-device-groups}

デバイスリストーに表示されるデバイスグループを指定するには、サイトのルートページの `cq:deviceGroups``jcr:content` ノードにプロパティを追加します。 プロパティの値は、デバイスグループノードへのパスの配列です。

Device group nodes are located in the `/etc/mobile/groups` folder.

For example, the root page of the Geometrixx Media site is `/content/geometrixx-media`. The `/content/geometrixx-media/jcr:content` node includes the following property:

* 名前：`cq:deviceGroups`
* 型：`String[]`
* 値：`/etc/mobile/groups/responsive`

[デバイスグループを作成および編集する](/help/sites-developing/groupfilters.md)には、ツールコンソールを使用します。

>[!NOTE]
>
>レスポンシブデザインに使用するデバイスグループについては、「一般」タブでデバイスグループを編集して、「エミュレーターを無効にする」を選択します。このオプションによって、レスポンシブデザインに関係のないエミュレーターカルーセルが表示されなくなります。


## Using adaptive images {#using-adaptive-images}

メディアクエリを使用して、ページに表示する画像リソースを選択できます。ただし、使用条件の設定にメディアクエリを使用しているすべてのリソースがクライアントにダウンロードされます。メディアクエリは、ダウンロードされたリソースが表示されるかどうかを決定するものに過ぎません。

画像などの大きいリソースの場合、すべてのリソースをダウンロードするとなると、クライアントのデータパイプラインを効率的に使用しているとは言えません。リソースを選択的にダウンロードするには、JavaScript を使用してリソース要求を開始してから、メディアクエリでリソースの選択を実行するようにします。

次の方法では、メディアクエリを使用して選択されたリソースが 1 つだけ読み込まれます。

1. リソースの各バージョンに対して DIV 要素を追加します。リソースの URI を属性値として追加します。ブラウザーには、この属性がリソースとして解釈されません。
1. リソースとして該当する各 DIV 要素にメディアクエリを追加します。
1. ドキュメントの読み込み時またはウィンドウのサイズ変更時に、JavaScript コードによって各 DIV 要素のメディアクエリが評価されます。
1. クエリの結果に基づいて、追加するリソースが決定されます。
1. そのリソースを参照する HTML 要素が DOM に挿入されます。

### Evaluating media queries using Javascript {#evaluating-media-queries-using-javascript}

Implementations of the [MediaQueryList interface](https://dev.w3.org/csswg/cssom-view/#the-mediaquerylist-interface) that the W3C defines enable you to evaluate media queries using javascript. You can apply logic to the media query results and execute scripts that are targeted for the current window:

* この関数は、MediaQueryListインターフェイスを実装するブラウザでサポートされ `window.matchMedia()` ます。 この関数は、指定した文字列に対してメディアクエリをテストします。 この関数は、クエリ結果へのアクセスを提供する `MediaQueryList` オブジェクトを返します。

* For browsers that do not implement the interface, you can use a `matchMedia()` polyfill, such as [matchMedia.js](https://github.com/paulirish/matchMedia.js), a freely-available javascript library.

#### Selecting media-specific resources {#selecting-media-specific-resources}

W3C で提言されている [picture 要素](https://picture.responsiveimages.org/)では、メディアクエリーを使用して画像要素用のソースを決定します。picture 要素では、要素の属性を使用してメディアクエリーを画像パスに関連付けます。

自由に利用できる [picturefill.jsライブラリ](https://github.com/scottjehl/picturefill) は、提案された `picture` 要素と同じ機能を提供し、同じ方法を使用します。 一連の `window.matchMedia``div` 要素に定義されたメディアクエリを評価するためのpicturefill.jsライブラリ呼び出し。 各 `div` 要素は画像ソースも指定します。 このソースは、 `div` 要素のメディアクエリが返すときに使用され `true`ます。

The `picturefill.js` library requires HTML code that is similar to the following example:

```xml
<div data-picture>
    <div data-src='path to default image'></div>
    <div data-src='path to small image'    data-media="(media query for phone)"></div>
    <div data-src='path to medium image'   data-media="(media query for tablet)"></div>
    <div data-src='path to large image'     data-media="(media query for monitor)"></div>
</div>
```

When the page is rendered, picturefull.js inserts an `img` element as the last child of the `<div data-picture>` element:

```xml
<div data-picture>
    <div data-src='path to default image'></div>
    <div data-src='path to small image'    data-media="(media query for phone)"></div>
    <div data-src='path to medium image'   data-media="(media query for tablet)"></div>
    <div data-src='path to large image'     data-media="(media query for monitor)"></div>
    <img src="path to medium image">
</div>
```

AEM ページでは、`data-src` 属性の値は、リポジトリ内のリソースへのパスを表します。

### Implementing adaptive images in AEM {#implementing-adaptive-images-in-aem}

AEM アプリケーションでアダプティブ画像を実装するには、必要な JavaScript ライブラリを追加し、ページに必要な HTML マークアップを含める必要があります。

**ライブラリ**

次の JavaScript ライブラリを取得し、クライアントライブラリフォルダーに格納します。

* [matchMedia.js](https://github.com/paulirish/matchMedia.js) （MediaQueryListインターフェイスを実装していないブラウザ用）
* [picturefill.js](https://github.com/scottjehl/picturefill)
* jquery.js( `/etc/clientlibs/granite/jquery` クライアントライブラリフォルダー(カテゴリ= jquery)を介して使用可能)
* [jquery.debouncedresize.js](https://github.com/louisremi/jquery-smartresize)（ウィンドウのサイズ変更後に一度発生する jquery イベント）

**ヒント：** 埋め込むことで、複数のクライアントライブラリフォルダーを自動的に連結でき [ます](/help/sites-developing/clientlibs.md#embedding-code-from-other-libraries)。

**HTML**

picturefill.jsコードで必要となるdiv要素を生成するコンポーネントを作成します。 AEMページでは、data-src属性の値は、リポジトリ内のリソースへのパスです。 例えば、ページコンポーネントは、メディアクエリと、DAM内の画像レンディションに関連付けられたパスをハードコード化できます。 または、作成者が画像レンディションを選択したり、ランタイムレンダリングオプションを指定したりできるカスタム画像コンポーネントを作成します。

次の HTML の例では、同じ画像の 2 つの DAM レンディションから選択されます。

```xml
<div data-picture>
    <div data-src='/content/dam/geometrixx-media/articles/meridien.png'></div>
    <div data-src='/content/dam/geometrixx-media/articles/meridien.png/jcr:content/renditions/cq5dam.thumbnail.319.319.png'    data-media="(min-width: 769px)"></div>
    <div data-src='/content/dam/geometrixx-media/articles/meridien.png/jcr:content/renditions/cq5dam.thumbnail.140.100.png'   data-media="(min-width: 481px)"></div>
</div>
```

>[!NOTE]
>
>アダプティブ画像基盤コンポーネントは、次の場所でアダプティブ画像を実装します。
>
>* クライアントライブラリフォルダー: `/libs/foundation/components/adaptiveimage/clientlibs`
>* HTMLを生成するスクリプト： `/libs/foundation/components/adaptiveimage/adaptiveimage.jsp`
>
>
以降では、このコンポーネントの詳細について説明します。


### Understanding image rendering in AEM {#understanding-image-rendering-in-aem}

画像レンダリングをカスタマイズするには、静的画像レンダリングの AEM デフォルト実装を理解する必要があります。AEM は画像コンポーネントと画像レンダリングサーブレットを提供しており、これらが連携して Web ページ用の画像をレンダリングします。イベントコンポーネントがページの段落システムに含まれると、次の一連の画像が発生します。

1. オーサリング：作成者は画像コンポーネントを編集し、HTML ページに含める画像ファイルを指定します。このファイルパスが、その画像コンポーネントノードのプロパティ値として格納されます。
1. ページの要求：ページコンポーネントの JSP により HTML コードが生成されます。画像コンポーネントの JSP により img 要素が生成され、この要素がページに追加されます。
1. 画像の要求：Web ブラウザーがページを読み込み、img 要素の src 属性に従って画像を要求します。
1. 画像レンダリング：画像レンダリングサーブレットが Web ブラウザーに画像を返します。

![chlimage_1-6](assets/chlimage_1-6a.png)

例えば、画像コンポーネントの JSP により、次のような HTML 要素が生成されます。

`<img title="My Image" alt="My Image" class="cq-dd-image" src="/content/mywebsite/en/_jcr_content/par/image_0.img.jpg/1358372073597.jpg">`

ブラウザーがページを読み込むときに、src 属性の値を URL として使用して画像を要求します。Sling によりこの URL が次のように分解されます。

* リソース: `/content/mywebsite/en/_jcr_content/par/image_0`
* File name extension: `.jpg`
* セレクター: `img`
* Suffix: `1358372073597.jpg`

ノード `image_0` の `jcr:resourceType` 値は、 `foundation/components/image`の値、はの `sling:resourceSuperType` 値です `foundation/components/parbase`。 このパーベスコンポーネントには、セレクターと要求URLのファイル名拡張子に一致するimg.GET.javaスクリプトが含まれています。 CQは、このスクリプト（サーブレット）を使用してイメージをレンダリングします。

To see the source code of the script, use CRXDE Lite to open the `/libs/foundation/components/parbase/img.GET.java`
file.

## Scaling images for the current viewport size {#scaling-images-for-the-current-viewport-size}

クライアントの表示域の特性に合わせて画像を実行時に拡大縮小し、レスポンシブデザインの原則に従った画像を配信します。静的画像レンダリングと同じ、サーブレットとオーサリングコンポーネントによるデザインパターンを使用します。

コンポーネントは次のタスクを実行する必要があります。

* 画像リソースのパスと必要なサイズをプロパティ値として保存します。
* メディアセレクターと画像レンダリング用のサービス呼び出しを含む `div` 要素を生成します。

>[!NOTE]
>
>Webクライアントは、matchMediaおよびPicturefillのJavaScriptライブラリ（または類似のライブラリ）を使用して、メディアセレクターを評価します。


画像要求を処理するサーブレットは、次のタスクを実行する必要があります。

* コンポーネントのプロパティから画像のパスとサイズを取得します。
* プロパティに従って画像の拡大縮小をおこない、画像を返します。

**利用可能なソリューション**

AEM により、ユーザーが利用または拡張できる次の実装がインストールされます。

* メディアクエリを生成するアダプティブ画像基盤コンポーネント、および画像の拡大縮小をおこなう Adaptive Image Component Servlet への HTTP 要求
* Geometrixx Commons パッケージによりインストールされる、画像の解像度を変更するための Image Reference Modification Servlet サンプルサーブレット

### Understanding the Adaptive Image component {#understanding-the-adaptive-image-component}

アダプティブイメージコンポーネントは、デバイス画面に従ってサイズ設定されたイメージをレンダリングするためのAdaptive Image Componentサーブレットへの呼び出しを生成します。 このコンポーネントには次のリソースが含まれています。

* JSP：メディアクエリと Adaptive Image Component Servlet への呼び出しを関連付ける div 要素を追加します。
* Client libraries: The clientlibs folder is a `cq:ClientLibraryFolder` that assembles the matchMedia polyfill javascript library and a modified Picturefill javascript library.
* Edit dialog box: The `cq:editConfig` node overrides the CQ foundation image component so that the drop target creates an adaptive-image component rather than a foundation image component.

#### Adding the DIV elements {#adding-the-div-elements}

adaptive-image.jsp スクリプトには div 要素とメディアクエリを生成する次のコードが含まれています。

```
<div data-picture data-alt='<%= alt %>'>
    <div data-src='<%= path + ".img.320.low." + extension + suffix %>'       data-media="(min-width: 1px)"></div>                                        <%-- Small mobile --%>
    <div data-src='<%= path + ".img.320.medium." + extension + suffix %>'    data-media="(min-width: 320px)"></div>  <%-- Portrait mobile --%>
    <div data-src='<%= path + ".img.480.medium." + extension + suffix %>'    data-media="(min-width: 321px)"></div>  <%-- Landscape mobile --%>
    <div data-src='<%= path + ".img.476.high." + extension + suffix %>'      data-media="(min-width: 481px)"></div>   <%-- Portrait iPad --%>
    <div data-src='<%= path + ".img.620.high." + extension + suffix %>'      data-media="(min-width: 769px)"></div>  <%-- Landscape iPad --%>
    <div data-src='<%= path + ".img.full.high." + extension + suffix %>'     data-media="(min-width: 1025px)"></div> <%-- Desktop --%>

    <%-- Fallback content for non-JS browsers. Same img src as the initial, unqualified source element. --%>
    <noscript>
        <img src='<%= path + ".img.320.low." + extension + suffix %>' alt='<%= alt %>'>
    </noscript>
</div>
```

`path` 変数には、現在のリソース（adaptive-image コンポーネントノード）のパスが格納されます。このコードにより、次の構造を持つ一連の `div` 要素が生成されます。

`<div data-scr = "*path-to-parent-node*.adaptive-image.adapt.*width*.*quality*.jpg" data-media="*media query*"></div>`

属性の値は、Slingが画像をレンダリングするアダプティブ画像コンポーネントサーブレットに解決されるURLです。 `data-scr` data-media属性には、クライアントのプロパティに対して評価されるメディアクエリが含まれます。

次の HTML コードは、JSP によって生成される `div` 要素の例です。

```xml
<div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.320.low.jpg'></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.320.medium.jpg'    data-media="(min-width: 320px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.480.medium.jpg'    data-media="(min-width: 321px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.476.high.jpg'     data-media="(min-width: 481px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.620.high.jpg'     data-media="(min-width: 769px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.full.high.jpg'     data-media="(min-width: 1025px)"></div>
```

#### Changing the image size selectors {#changing-the-image-size-selectors}

アダプティブ画像コンポーネントをカスタマイズし、幅セレクターを変更する場合は、その幅をサポートするように Adaptive Image Component Servlet を設定する必要もあります。

### Adaptive Image Component Servlet について {#understanding-the-adaptive-image-component-servlet}

Adaptive Component Servlet は、指定された幅に応じて JPEG 画像のサイズを変更し、JPEG 画質を設定します。

#### The interface of the Adaptive Image Component Servlet {#the-interface-of-the-adaptive-image-component-servlet}

Adaptive Image Component Servlet は、デフォルトの Sling サーブレットにバインドされ、.jpg、.jpeg、.gif および .png ファイル拡張子をサポートします。このサーブレットのセレクターは img です。

>[!CAUTION]
>
>アダプティブレンディション用のアニメーション .gif ファイルは AEM でサポートされていません。

そのため、Sling は次の形式の HTTP 要求 URL をこのサーブレットへと解決します。

`*path-to-node*.img.*extension*`

For example, Sling forwards HTTP requests with the URL `http://localhost:4502/content/geometrixx/adaptiveImage.img.jpg` to Adaptive Image Component Servlet.

2 つの追加セレクターにより、要求される画像の幅と JPEG 画質を指定します。次の例では、幅 480 ピクセルで中程度の画質の画像を要求します。

`http://localhost:4502/content/geometrixx/adaptiveImage.adapt.480.MEDIUM.jpg`

**サポートされている画像プロパティ**

このサーブレットは、有限個の画像の幅と画質を受け入れます。次の幅はデフォルトでサポートされています（ピクセル単位）。

* full
* 320
* 480
* 476
* 620

full 値は、拡大縮小しないことを示します。

JPEG 画質については、次の値がサポートされています。

* LOW
* MEDIUM
* HIGH

対応する数値はそれぞれ、0.4、0.82、1.0 です。

**サポートされるデフォルトの幅の変更**

Web コンソール（[http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)）または sling:OsgiConfig ノードを使用して、Adobe CQ Adaptive Image Component Servlet でサポートされる幅を設定します。

AEM サービスの設定方法について詳しくは、[OSGi の設定](/help/sites-deploying/configuring-osgi.md)を参照してください。

<table>
 <tbody>
  <tr>
   <th> </th>
   <th>Webコンソール</th>
   <th>sling:OsgiConfig</th>
  </tr>
  <tr>
   <th>サービス名またはノード名</th>
   <td>「設定」タブのサービス名：Adobe CQ Adaptive Image Component Servlet</td>
   <td>com.day.cq.wcm.foundation.impl. AdaptiveImageComponentServlet</td>
  </tr>
  <tr>
   <th>プロパティ</th>
   <td><p>サポートされる幅</p>
    <ul>
     <li>サポートされる幅を追加するには、+ ボタンをクリックし、正の整数を入力します。</li>
     <li>サポートされる幅を削除するには、該当する項目の「-」ボタンをクリックします。</li>
     <li>サポートされる幅を変更するには、フィールド値を編集します。</li>
    </ul> </td>
   <td><p>adapt.supported.widths</p>
    <ul>
     <li>このプロパティは複数値の String です。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

#### 実装の詳細 {#implementation-details}

この `com.day.cq.wcm.foundation.impl.AdaptiveImageComponentServlet` クラスは、AbstractImageServlet [](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.html) クラスを拡張します。 AdaptiveImageComponentServletソースコードは、 `/libs/foundation/src/impl/src/com/day/cq/wcm/foundation/impl` フォルダー内にあります。

このクラスは、Felix SCR アノテーションを使用して、サーブレットが関連付けられるリソースタイプとファイル拡張子および 1 つ目のセレクターの名前を設定します。

```java
@Component(metatype = true, label = "Adobe CQ Adaptive Image Component Servlet",
        description = "Render adaptive images in a variety of qualities")
@Service
@Properties(value = {
    @Property(name = "sling.servlet.resourceTypes", value = "foundation/components/adaptiveimage", propertyPrivate = true),
    @Property(name = "sling.servlet.selectors", value = "img", propertyPrivate = true),
    @Property(name = "sling.servlet.extensions", value ={
            "jpg",
            "jpeg",
            "png",
            "gif"
    }, propertyPrivate = true)
})
```

このサーブレットは Property SCR アノテーションを使用して、サポートされるデフォルトの画質と画像サイズを設定します。

```java
@Property(value = {
            "320", // iPhone portrait
            "480", // iPhone landscape
            "476", // iPad portrait
            "620" // iPad landscape
    },
            label = "Supported Widths",
            description = "List of widths this component is permitted to generate.")
```

The `AbstractImageServlet` class provides the `doGet` method that processes the HTTP request. This method determines the resource that is associated with the request, retrieves resource properties from the repository, and returns them in an [ImageContext](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.ImageContext.html) object.

>[!NOTE]
>
>The [com.day.cq.commons.DownloadResource](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/DownloadResource.html) class provides the `getFileReference method`, which retrieves the value of the resource&#39;s `fileReference` property.

この `AdaptiveImageComponentServlet` クラスは、 `createLayer` メソッドを上書きします。 この方法は、オブジェクトからイメージリソースのパスと要求されたイメージ幅を取得する `ImageContext` 。 次に、 `info.geometrixx.commons.impl.AdaptiveImageHelper` クラスのメソッドを呼び出し、実際の画像の拡大/縮小を実行します。

また、AdaptiveImageComponentServletクラスは、writeLayerメソッドをオーバーライドします。 この方法では、画像にJPEG画質を適用します。

### Image Reference Modification Servlet (Geometrixx Common) {#image-reference-modification-servlet-geometrixx-common}

サンプルの Image Reference Modification Servlet は、Web ページ上の画像の拡大縮小をおこなうために、img 要素のサイズ関連属性を生成します。

#### サーブレットの呼び出し {#calling-the-servlet}

このサーブレットは `cq:page` リソースにバインドされ、.jpg ファイル拡張子をサポートしています。The servlet selector is `image`. そのため、Sling は次の形式の HTTP 要求 URL をこのサーブレットへと解決します。

`path-to-page-node.image.jpg`

For example, Sling forwards HTTP requests with the URL `http://localhost:4502/content/geometrixx/en.image.jpg` to Image Reference Modification Servlet.

3 つの追加セレクターにより、要求される画像の幅、高さおよび画質（オプション）を指定します。次の例では、幅 770 ピクセル、高さ 360 ピクセルで中程度の画質の画像を要求します。

`http://localhost:4502/content/geometrixx/en.image.770.360.MEDIUM.jpg`

**サポートされている画像プロパティ**

このサーブレットは、有限個の画像サイズと画質の値を受け入れます。

次の値はデフォルトでサポートされています（幅 x 高さ）。

* 256 x 192
* 370 x 150
* 480 x 200
* 127 x 127
* 770 x 360
* 620 x 290
* 480 x 225
* 320 x 150
* 375 x 175
* 303 x 142
* 1170 x 400
* 940 x 340
* 770 x 300
* 480 x 190

画質については、次の値がサポートされています。

* LOW
* MEDIUM
* HIGH

AEM と連携する場合は、いくつかの方法でこのようなサービスの設定を管理できます。詳しくは、[OSGi の設定](/help/sites-deploying/configuring-osgi.md)を参照してください。

#### 画像リソースの指定 {#specifying-the-image-resource}

画像のパス、サイズおよび画質の値は、リポジトリ内のノードのプロパティとして格納する必要があります。

* The node name is `image`.
* The parent node is the `jcr:content` node of a `cq:page` resource.

* 画像のパスは、`fileReference` というプロパティの値として格納します。

When authoring a page, use **Sidekick** to specify the image and add the `image` node to the page properties:

1. In **Sidekick**, click the **Page** tab, and then click **Page Properties**.
1. Click the **Image** tab and specify the image.
1. 「**OK**」をクリックします。

#### 実装の詳細 {#implementation-details-1}

info.geometrixx.commons.impl.servlets.ImageReferenceModificationServletクラスは、AbstractImageServlet [](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.html) クラスを拡張します。 cq-geometrixx-commons-pkgパッケージをインストールしている場合、ImageReferenceModificationServletソースコードは `/apps/geometrixx-commons/src/core/src/main/java/info/geometrixx/commons/impl/servlets` フォルダー内にあります。

このクラスは、Felix SCR アノテーションを使用して、サーブレットが関連付けられるリソースタイプとファイル拡張子および 1 つ目のセレクターの名前を設定します。

```java
@Component(metatype = true, label = "Adobe CQ Image Reference Modification Servlet",
        description = "Render the image associated with a page in a variety of dimensions and qualities")
@Service
@Properties(value = {
    @Property(name = "sling.servlet.resourceTypes", value = NameConstants.NT_PAGE, propertyPrivate = true),
    @Property(name = "sling.servlet.selectors", value = "image", propertyPrivate = true),
    @Property(name = "sling.servlet.extensions", value = "jpg", propertyPrivate = true)
})
```

このサーブレットは Property SCR アノテーションを使用して、サポートされるデフォルトの画質と画像サイズを設定します。

```java
@Property(label = "Image Quality",
            description = "Quality must be a double between 0.0 and 1.0", value = "0.82")
@Property(value = {
                "256x192", // Category page article list images
                "370x150", // "Most popular" desktop & iPad & carousel min-width: 1px
                "480x200", // "Most popular" phone
                "127x127", // article summary phone square images
                "770x360", // article summary, desktop
                "620x290", // article summary, tablet
                "480x225", // article summary, phone (landscape)
                "320x150", // article summary, phone (portrait) and fallback
                "375x175", // 2-column article summary, desktop
                "303x142", // 2-column article summary, tablet
                "1170x400", // carousel, full
                "940x340",  // carousel min-width: 980px
                "770x300",  // carousel min-width: 768px
                "480x190"   // carousel min-width: 480px
            },
            label = "Supported Resolutions",
            description = "List of resolutions this component is permitted to generate.")
```

The `AbstractImageServlet` class provides the `doGet` method that processes the HTTP request. This method determines the resource that is associated with the call, retrieves resource properties from the repository, and saves them in an [ImageContext](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.ImageContext.html) object.

この `ImageReferenceModificationServlet` クラスは、 `createLayer` メソッドを上書きし、レンダリングするイメージリソースを決定するロジックを実装します。 このメソッドは、ページのノード名の子ノードを取得し `jcr:content``image`ます。 このノードから [Image](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/foundation/Image.html) オブジェクトが作成され、 `image` メソッドは画像ノードの `getFileReference``fileReference` プロパティから画像ファイルへのパスを返します。

>[!NOTE]
>The [com.day.cq.commons.DownloadResource](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/DownloadResource.html) class provides the getFileReferencemethod.


## Developing a fluid grid {#developing-a-fluid-grid}

AEM enables you to efficiently and effectively implement fluid grids. This page explains how you can integrate your fluid grid or an existing grid implementation (such as [Bootstrap](https://twitter.github.com/bootstrap/)) into your AEM application.

可変グリッドについて詳しくない場合は、このページの下部にある[可変グリッドの概要](/help/sites-developing/responsive.md#developing-a-fluid-grid)を参照してください。この概要では、可変グリッドの概要を説明し、その設計方法についてアドバイスしています。

### Defining the grid using a Page component {#defining-the-grid-using-a-page-component}

ページコンポーネントを使用して、ページのコンテンツブロックを定義する HTML 要素を生成します。ページが参照する ClientLibraryFolder には、コンテンツブロックのレイアウトを制御する CSS が含まれています。

* ページコンポーネント：一連のコンテンツブロックを表す div 要素を追加します。コンテンツブロックを表す div 要素には、作成者がコンテンツを追加できる parsys コンポーネントなどがあります。
* クライアントライブラリフォルダー：div 要素用のメディアクエリとスタイルが含まれる CSS ファイルが格納されます。

例えば、サンプルのgeometrixx-mediaアプリケーションにはmedia-homeコンポーネントが含まれています。 このページ・コンポーネントは、2つのスクリプトを挿入します。このスクリプトは、クラスの2つの `div` 要素を生成し `row-fluid`ます。

* 最初の行には、クラスの `div` 要素が含まれ `span12` ます（コンテンツは12列に及びます）。 この `div` 要素にはparsysコンポーネントが含まれます。

* The second row contains two `div` elements, one of class `span8` and the other of class `span4`. それぞれの `div` 要素には parsys コンポーネントが含まれます。

```xml
<div class="page-content">
    <div class="row-fluid">
        <div class="span12">
            <cq:include path="grid-12-par" resourceType="foundation/components/parsys" />
        </div>
    </div>
    <div class="row-fluid">
        <div class="span8">
            <cq:include path="grid-8-par" resourceType="foundation/components/parsys" />
        </div>
        <div class="span4">
            <cq:include path="grid-4-par" resourceType="foundation/components/parsys" />
        </div>
    </div>
</div>
```

>[!NOTE]
>
>When a component includes multiple `cq:include` elements that reference the parsys component, each `path` attribute must have a different value.


#### Scaling the Page component grid {#scaling-the-page-component-grid}

geometrixx-mediaページコンポーネント(`/etc/designs/geometrixx-media`)に関連付けられているデザインには、ClientLibraryFolderが含まれ `clientlibs` ます。 このClientLibraryFolderは、クラスの子である `row-fluid` クラス、 `span*` クラス、クラス `span*` のCSSスタイルを定義し `row-fluid` ます。 メディアクエリを使用すると、ビューポートサイズごとにスタイルを再定義できます。

次の例のCSSは、これらのスタイルのサブセットです。 このサブセットでは、 `span12`、、 `span8``span4` 、およびクラスと、2つのビューポートサイズ用のメディアクエリについて説明します。 CSSの次の特性に注意してください。

* The `.span` styles define element widths using absolute numbers.
* The `.row-fluid .span*` styles define element widths as percenteages of the parent. パーセンテージは、幅の絶対数から計算します。
* 大きい表示域のメディアクエリでは、大きい幅の絶対数が割り当てられます。

>[!NOTE]
>
>Geometrixx Media サンプルでは、[Bootstrap](https://twitter.github.com/bootstrap/javascript.html) JavaScript フレームワークを、その可変グリッド実装に統合しています。Bootstrap フレームワークは bootstrap.css ファイルを提供します。

```xml
/* default styles (no media queries) */
 .span12 { width: 940px }
 .span8 { width: 620px }
 .span4 { width: 300px }
 .row-fluid .span12 { width: 100% }
 .row-fluid .span8 { width: 65.95744680851064% }
 .row-fluid .span4 { width: 31.914893617021278% }

@media (min-width: 768px) and (max-width: 979px) {
 .span12 { width: 724px; }
 .span8 {     width: 476px; }
 .span4 {     width: 228px; }
 .row-fluid .span12 {     width: 100%;}
 .row-fluid .span8 {     width: 65.74585635359117%; }
 .row-fluid .span4 {     width: 31.491712707182323%; }
}

@media (min-width: 1200px) {
 .span12 { width: 1170px }
 .span8 { width: 770px }
 .span4 { width: 370px }
 .row-fluid .span12 { width: 100% }
 .row-fluid .span8 { width: 65.81196581196582% }
 .row-fluid .span4 { width: 31.623931623931625% }
}
```

#### Repositioning content in the Page component grid {#repositioning-content-in-the-page-component-grid}

Geometrixx Media サンプルアプリケーションのページでは、幅の広い表示域の場合に、コンテンツブロックの行が水平方向に広げられます。小さい表示域では、同じブロックが垂直方向に広げられます。次の CSS の例は、media-home ページコンポーネントが生成する HTML コードに対してこの動作を実装するスタイルを示しています。

* The default CSS for the media-welcome page assigns the `float:left` style for `span*` classes that are inside `row-fluid` classes.

* 小さい表示域用のメディアクエリーでは、同じクラスに対して `float:none` スタイルを割り当てます。

```xml
/* default styles (no media queries) */
    .row-fluid [class*="span"] {
        width: 100%;
        float: left;
}

@media (max-width: 767px) {
    [class*="span"], .row-fluid [class*="span"] {
        float: none;
        width: 100%;
    }
}
```

#### Modularize your Page components {#tip-modularize-your-page-components}

コンポーネントをモジュール化すると、コードを効率的に使用できます。サイトでは、ようこそページ、記事ページ、製品ページなどの様々なタイプのページを使用します。それぞれのタイプのページには、様々なタイプのコンテンツが含まれ、おそらく様々なレイアウトが使用されます。ただし、各レイアウトの特定の要素が複数のページで共通している場合、そのレイアウト部を実装するコードを再利用できます。

**ページコンポーネントのオーバーレイの使用**

Create a main page component that provides scripts for generating the various parts of a page, such as `head` and `body` sections, and `header`, `content`, and `footer` sections within the body.

そのメインページコンポーネントを `cq:resourceSuperType` として使用する他のページコンポーネントを作成します。これらのコンポーネントには、必要に応じてメインページのスクリプトをオーバーライドするスクリプトが含まれます。

例えば、goemetrixx-media アプリケーションにはページコンポーネントが含まれています（`sling:resourceSuperType` は基盤ページコンポーネントです）。複数の子コンポーネント（article、category および media-home）はこのページコンポーネントを`sling:resourceSuperType`   として使用します。それぞれの子コンポーネントには、ページコンポーネントの content.jsp ファイルをオーバーライドする content.jsp ファイルが含まれます。

**スクリプトの再利用**

複数のページコンポーネントに共通する行と列の組み合わせを生成する、複数の JSP スクリプトを作成します。For example, the `content.jsp` script of the article and media-home components both reference the `8x4col.jsp` script.

**ターゲットの表示域サイズによる CSS スタイルの整理**

異なる表示域サイズ用の CSS スタイルとメディアクエリを、それぞれ別のファイルに追加します。クライアントライブラリフォルダーを使用してこれらのファイルを連結します。

### Inserting components into the page grid {#inserting-components-into-the-page-grid}

コンポーネントが 1 つのコンテンツブロックを生成する場合、一般に、そのページコンポーネントが構築するグリッドがコンテンツの配置を制御します。

作成者は、コンテンツブロックが様々なサイズや相対位置でレンダリングされる可能性があることを意識する必要があります。コンテンツのテキストでは、他のコンテンツブロックを指すために相対方向を使用しないようにしてください。

必要であれば、コンポーネントで、生成する HTML コード用に必要となる CSS または JavaScript ライブラリを提供してください。コンポーネント内のクライアントライブラリフォルダーを使用して、CSS および JS ファイルを生成します。ファイルにアクセスできるようにするには、/etc フォルダー内の別のクライアントライブラリフォルダー内で[依存関係を作成するかライブラリを組み込みます](/help/sites-developing/clientlibs.md#creating-client-library-folders)。

**サブグリッド**

コンポーネントに複数のコンテンツブロックが含まれている場合は、コンテンツブロックを行の内部に追加して、ページ上にサブグリッドを構築します。

* div 要素を行およびコンテンツブロックとして表現するには、周囲のページコンポーネントと同じクラス名を使用します。
* ページデザインの CSS で実装している動作をオーバーライドするには、行の div 要素に対して 2 つ目のクラス名を使用し、クライアントライブラリフォルダー内に関連する CSS を格納します。

For example, the `/apps/geometrixx-media/components/2-col-article-summary` component generates two columns of content. このコンポーネントが生成する HTML の構造は次のとおりです。

```xml
<div class="row-fluid mutli-col-article-summary">
    <div class="span6">
        <article>
            <div class="article-summary-image">...</div>
            <div class="social-header">...</div>
            <div class="article-summary-description">...</div>
            <div class="social">...</div>
        </article>
    </div>
</div>
```

The `.row-fluid .span6` selectors of the page&#39;s CSS applies to the `div` elements of the same class and structure in this HTML. ただし、このコンポーネントには/apps/geometrixx-media/components/2-col-article-summary/clientlibsクライアントライブラリフォルダーも含まれます。

* CSS ではページコンポーネントと同じメディアクエリを使用して、レイアウトの変更を、同じ離散したページ幅により確立します。
* セレクターでは、行の `multi-col-article-summary` 要素の `div` クラスを使用して、ページの `row-fluid` クラスの動作をオーバーライドします。

For example, the following styles are included in the `/apps/geometrixx-media/components/2-col-article-summary/clientlibs/css/responsive-480px.css` file:

```xml
@media (max-width: 480px) {
    .mutli-col-article-summary .article-summary-image {
        float: left;
        width: 127px;
    }
    .mutli-col-article-summary .article-summary-description {
        width: auto;
        margin-left: 127px;
    }
    .mutli-col-article-summary .article-summary-description h4 {
        padding-left: 10px;
    }
    .mutli-col-article-summary .article-summary-text {
        margin-left: 127px;
        min-height: 122px;
        top: 0;
    }
}
```

## Introduction to fluid grids {#introduction-to-fluid-grids}

可変グリッドでは、ページレイアウトをクライアントの表示域サイズに合わせて変更できます。グリッドは、ページ上のコンテンツブロックを配置する論理的な列と行で構成されます。

* 列はコンテンツブロックの水平方向の位置と幅を決定します。
* 行はコンテンツブロックの垂直方向の相対位置を決定します。

HTML5 テクノロジーを使用すれば、グリッドを実装して、ページレイアウトを異なる表示域サイズに合わせて変更するようにグリッドを操作できます。

* HTML `div` elements contain blocks of content that span a certain number of columns.
* これらのdiv要素の1つ以上が、共通の親divelementを共有する場合に行を構成します。

### Using discrete widths {#using-discrete-widths}

ターゲットにしている表示域の幅の各範囲について、静的なページ幅と、一定の幅を持つコンテンツブロックを使用します。ブラウザーウィンドウのサイズを手動で変更すると、離散したウィンドウ幅のそれぞれでコンテンツサイズが変更されます（これらの離散した幅はブレークポイントとも呼ばれます）。そのため、ページデザインはより安定し、ユーザーエクスペリエンスが最大化されます。

#### Scaling the grid {#scaling-the-grid}

グリッドを使用してコンテンツブロックを異なる表示域サイズに合わせて拡大縮小します。コンテンツブロックは特定の列数にまたがります。列の幅が異なる表示域サイズに合うように拡大縮小し、それに合わせてコンテンツブロックの幅も拡大縮小します。拡大縮小では、コンテンツブロックを隣り合わせで配置できる十分な幅を持つ大規模から中規模の表示域がサポートされます。

![](do-not-localize/chlimage_1-1a.png)

#### Repositioning content in the grid {#repositioning-content-in-the-grid}

コンテンツブロックのサイズは、幅の最小値による制約を受けます。その幅未満になると、拡大縮小は実行されません。小さい表示域の場合、コンテンツブロックを水平方向ではなく垂直方向に広げるためにグリッドを使用できます。

![](do-not-localize/chlimage_1-2a.png)

### Designing the grid {#designing-the-grid}

ページ上にコンテンツのブロックを配置する必要がある列と行を決定します。 ページレイアウトによって、グリッドにまたがる列数と行数が決まります。

**列数**

すべての表示域サイズのすべてのレイアウトで、コンテンツブロックを水平方向に配置できる十分な列を用意します。将来のページデザインに対応するために、現在必要な列数よりも多い数を使用してください。

**行のコンテンツ**

行を使用して、コンテンツブロックの垂直方向の位置を制御します。同じ行を共有するコンテンツブロックを次のように決定します。

* すべてのレイアウトで、水平方向に隣り合うコンテンツブロックは同じ行内に位置します。
* 水平方向（幅の広い表示域の場合）および垂直方向（小さい表示域の場合）で隣り合うコンテンツブロックは同じ行内に位置します。

### Grid implementations {#grid-implementations}

ページ上のコンテンツブロックのレイアウトを制御するには、CSS クラスおよびスタイルを作成します。ページデザインは多くの場合、表示域内のコンテンツブロックの相対的なサイズと位置に基づいています。表示域によってコンテンツブロックの実際のサイズが決定します。CSS では、相対サイズと絶対サイズを指定する必要があります。次の 3 つのタイプの CSS クラスを使用して可変グリッドを実装できます。

* すべての行のコンテナである `div` 要素のクラス。 このクラスは、グリッドの絶対幅を設定します。
* A class for `div` elements that represent a row. このクラスでは、格納するコンテンツブロックの水平方向または垂直方向の位置を制御します。
* 異なる幅のコンテンツブロックを表す `div` 要素用のクラス。幅は親（行）のパーセンテージとして表します。

ターゲットとなる表示域の幅（およびその関連するメディアクエリ）が、ページレイアウトに使用される離散した幅を定めます。

#### Widths of content blocks {#widths-of-content-blocks}

一般に、コンテンツブロッククラスの `width` スタイルは、ページおよびグリッドの次の特徴に基づいています。

* ターゲットとなるそれぞれの表示域サイズで使用しているページの幅の絶対値。これらは既知の値です。
* それぞれのページの幅に対応するグリッドの列の幅の絶対値。これらの値はユーザーが指定します。
* ページ全体の幅のパーセンテージとして指定した、各列の幅の相対値。これらの値はユーザーが計算して指定します。

CSS には、次の構造を使用した一連のメディアクエリが含まれます。

```xml
@media(query_for_targeted_viewport){

  .class_for_container{ width:absolute_page_width }
  .class_for_row { width:100%}

  /* several selectors for content blocks   */
  .class_for_content_block1 { width:absolute_block_width1 }
  .class_for_content_block2 { width:absolute_block_width2 }
  ...

  /* several selectors for content blocks inside rows */
  .class_for_row .class_for_content_block1 { width:relative_block_width1 }
  .class_for_row .class_for_content_block2 { width:relative_block_width2 }
  ...
}
```

ページ用の要素のクラスと CSS スタイルを開発するための出発点として、次のアルゴリズムを使用します。

1. すべての行を含む div 要素のクラス名を定義します（例：`content.`）。
1. Define a CSS class for div elements that represent rows, such as `row-fluid`.
1. コンテンツブロック要素のクラス名を定義します。 可能なすべての幅に対して、列の範囲に関してクラスが必要です。 例えば、3列にまたがる `span3` 要素に対してはクラスを使用し、4列にまたがる `div``span4` クラスを使用します。 グリッド内の列数に応じてクラスを定義します。

1. ターゲットとする表示域サイズごとに、対応するメディアクエリを CSS ファイルに追加します。各メディアクエリに次の項目を追加します。

   * A selector for the `content` class, for example `.content{}`.
   * Selectors for each span class, for example `.span3{ }`.
   * A selector for the `row-fluid` class, for example `.row-fluid{ }`
   * Selectors for span classes that are inside row-fluid classes, for example `.row-fluid span3 { }`.

1. 各セレクターに幅のスタイルを追加します。

   1. `content` セレクターの幅を、ページの絶対サイズに設定します（例：`width:480px`）。
   1. すべての row-fluid セレクターの幅を 100％に設定します。
   1. Set the width of all span selectors to the absolute width of the content block. A trivial grid uses evenly-distributed columns of the same width: `(absolute width of page)/(number of columns)`.
   1. Set the width of the `.row-fluid .span` selectors as a percentage of the total width. 数式を使用してこの幅を計算し `(absolute span width)/(absolute page width)*100` ます。

#### 行内のコンテンツブロックの配置 {#positioning-content-blocks-in-rows}

Use the float style of the `.row-fluid` class to control whether the content blocks in a row are arranged horizontally or vertically.

* `float:left` または `float:right` スタイルを使用すると、子要素（コンテンツブロック）が水平方向に分布します。

* The `float:none` style causes vertical distribution of child elements.

各メディアクエリ追加内の `.row-fluid` セレクターのスタイル。 そのメディアクエリに使用するページレイアウトに従って値を設定します。 例えば、次の図は、幅の広いビューポートではコンテンツを水平に、幅の狭いビューポートでは垂直に分配する行を示しています。

![](do-not-localize/chlimage_1-3a.png)

次の CSS によりこの動作を実装できます。

```xml
@media (min-width: 768px) and (max-width: 979px) {
   .row-fluid {
       width:100%;
       float:left
   }
}

@media (max-width:480px){
    .row-fluid {
       width:100%;
       float:none
   }
}
```

#### Assigning classes to content blocks {#assigning-classes-to-content-blocks}

ターゲットとしているそれぞれの表示域サイズのページレイアウトに対して、各コンテンツブロックがまたがる列数を決定します。次に、それぞれのコンテンツブロックの div 要素で使用するクラスを決定します。

このような div クラスを確立したら、AEM アプリケーションを使用してグリッドを実装できます。
