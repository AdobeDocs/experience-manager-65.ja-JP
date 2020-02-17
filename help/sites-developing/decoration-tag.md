---
title: 装飾タグ
seo-title: 装飾タグ
description: Web ページのコンポーネントがレンダリングされる際に、レンダリングしたコンポーネントをラッピングする HTML 要素を生成できます。AEM は、開発者向けに、含まれているコンポーネントをラップする装飾タグを制御する明確でシンプルなロジックを提供します。
seo-description: Web ページのコンポーネントがレンダリングされる際に、レンダリングしたコンポーネントをラッピングする HTML 要素を生成できます。AEM は、開発者向けに、含まれているコンポーネントをラップする装飾タグを制御する明確でシンプルなロジックを提供します。
uuid: db796a22-b053-48dd-a50c-354dead7e8ec
contentOwner: user
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 8cb9fd6e-5e1f-43cd-8121-b490dee8c2be
translation-type: tm+mt
source-git-commit: c13eabdf4938a47ddf64d55b00f845199591b835

---


# 装飾タグ{#decoration-tag}

>[!NOTE]
>
>この記事に記載されている装飾タグ動作およびオプションは、[AEM 6.3 CFP1](https://helpx.adobe.com/experience-manager/release-notes--aem-6-3-cumulative-fix-pack.html) に基づいています。
>
>CFP1 より前の 6.3 の装飾タグの動作は、AEM 6.2 の動作と同じです。

Web ページのコンポーネントがレンダリングされる際に、レンダリングしたコンポーネントをラッピングする HTML 要素を生成できます。これは主に2つの目的を果たします。

* コンポーネントは、HTML 要素でラップされている場合に、編集のみできます。
* ラッピング要素は、次を提供する HTML クラスを適用するために使用されます。

   * レイアウト情報
   * スタイル設定情報

AEM は、開発者向けに、含まれているコンポーネントをラップする装飾タグを制御する明確でシンプルなロジックを提供します。このページで説明する 2 つの要素の組み合わせによって、装飾タグがレンダリングされるかどうかやその方法が定義されます。

* コンポーネント自体がプロパティのセットでその装飾タグを設定できます。
* コンポーネント（HTL、JSP、ディスパッチャーなど）を含むスクリプトは、パラメーターを含めることで装飾タグの側面を定義できます。

## 推奨事項 {#recommendations}

ここでは、予期しない問題の発生を防ぐのに役立つ、ラッパー要素を含めるタイミングに関する一般的な推奨事項を示します。

* ページの CSS および JavaScripts がすべての場合で同じように機能できるように、ラッパー要素の存在が、WCM モード間（編集またはプレビューモード）、インスタンス間（オーサーまたはパブリッシュ）または環境間（ステージングまたは本番）で違わないようにする必要があります。
* ページエディターが適切に初期化および更新できるように、ラッパー要素は、編集可能なすべてのコンポーネントに追加する必要があります。
* 編集できないコンポーネントの場合、特定の機能を提供しないのであれば、ラッパー要素は回避できるので、結果として得られるマークアップは不必要に肥大化しなくなります。

## コンポーネントの制御 {#component-controls}

次のプロパティおよびノードをコンポーネントに適用して、装飾タグの動作を制御できます。

* **`cq:noDecoration {boolean}`**:このプロパティをコンポーネントに追加でき、true値を指定すると、AEMがコンポーネント上にラッパー要素を生成しなくなります。

* **`cq:htmlTag`ノード：**このノードは、コンポーネントに追加でき、次のプロパティを持つことができます。

   * **`cq:tagName {String}`**:これは、デフォルトのDIV要素の代わりにコンポーネントのラッピングに使用するカスタムHTMLタグを指定する場合に使用できます。
   * **`class {String}`**:これは、ラッパーに追加するcssクラス名を指定するために使用できます。
   * 他のプロパティ名は、提供されたのと同じ String 値の HTML 属性として追加されます。

## スクリプトの制御 {#script-controls}

The wrapper behavior does differ however depending on if [HTL](/help/sites-developing/decoration-tag.md#htl) or [JSP](/help/sites-developing/decoration-tag.md#jsp) is used to include the element.

### HTL {#htl}

通常、HTL のラッパー動作は、次のように要約できます。

* No wrapper DIV is rendered by default (when just doing `data-sly-resource="foo"`).
* すべての wcm モード（オーサーおよびパブリッシュの両方で無効、プレビュー、編集）は同じようにレンダリングされる。

また、ラッパーの動作も完全に制御できます。

* HTL スクリプトは、結果として得られるラッパータグの動作を完全に制御します。
* Component properties (like `cq:noDecoration` and `cq:tagName`) can also define the wrapper tag.

HTL スクリプトおよびその関連ロジックからラッパータグの動作を完全に制御できます。

For further information about developing in HTL see the [HTL documentation](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html).

#### デシジョンツリー {#decision-tree}

このデシジョンツリーは、ラッパータグの動作を決定するロジックの概要を示します。

![chlimage_1-75](assets/chlimage_1-75a.png)

#### ユースケース {#use-cases}

次の 3 つの使用例は、ラッパータグの処理方法の例です。また、目的のラッパータグの動作を制御するのがいかにシンプルかを説明しています。

すべての例で次のコンテンツ構造およびコンポーネントに従っていると想定しています。

```
/content/test/
  @resourceType = "test/components/one"
  child/
    @resourceType = "test/components/two"
```

```
/apps/test/components/
  one/
    one.html
  two/
    two.html
    cq:htmlTag/
      @cq:tagName = "article"
      @class = "component-two"
```

#### 使用例 1：コードの再利用のためのコンポーネントを含める {#use-case-include-a-component-for-code-reuse}

最も一般的な使用例は、コードの再利用のためにコンポーネントが他のコンポーネントを含む場合です。この場合、含まれるコンポーネントは、独自のツールバーおよびダイアログで編集できる必要はないので、ラッパーは不要で、コンポーネントの `cq:htmlTag` は無視されます。これはデフォルトの動作と見なすことができます。

`one.html: <sly data-sly-resource="child"></sly>`

`two.html: Hello World!`

出力結果 `/content/test.html`:

**`Hello World!`**

例えば、イメージを表示するコアイメージコンポーネントを含むコンポーネントを例に挙げます。通常は、そのコンポーネントが持つすべてのプロパティを表すMapオブジェクトに、仮想子コンポーネントをデータ密接に渡して渡す、合成リソースを使用します。

#### 使用例 2：編集可能なコンポーネントを含める {#use-case-include-an-editable-component}

もうひとつの一般的な使用例は、コンテナコンポーネントがレイアウトコンテナのような編集可能な子コンポーネントを含む場合です。この場合、含まれた各子は、必ずエディターが機能するためのラッパーを必要とします（`cq:noDecoration` プロパティで明示的に無効になっている場合を除く）。

含まれるコンポーネントは、この場合、独立したコンポーネントなので、エディターが機能するためにはラッパー要素が必要で、適用するレイアウトおよびスタイルを定義する必要があります。To trigger this behavior, there&#39;s the `decoration=true` option.

`one.html: <sly data-sly-resource="${'child' @ decoration=true}"></sly>`

`two.html: Hello World!`

出力結果 `/content/test.html`:

**`<article class="component-two">Hello World!</article>`**

#### 使用例 3：カスタム動作 {#use-case-custom-behavior}

複雑な使用例はいくつもありますが、明示的に次を提供する HTL を利用することで簡単に実現できます。

* **`decorationTagName='ELEMENT_NAME'`** ラッパーの要素名を定義する場合。
* **`cssClassName='CLASS_NAME'`** 設定するCSSクラス名を定義する場合。

`one.html: <sly data-sly-resource="${'child' @ decorationTagName='aside', cssClassName='child'}"></sly>`

`two.html: Hello World!`

結果の出 `/content/test.html`力：

**`<aside class="child">Hello World!</aside>`**

## JSP {#jsp}

When including a component using `cq:includ`e or `sling:include`, the default behavior in AEM is to use a DIV to wrap the element. ただし、このラッピングは 2 つの方法でカスタマイズできます。

* `cq:noDecoration` を使用してコンポーネントをラッピングしないように明示的に AEM に指定します。
* Use a custom HTML tag to wrap the component using `cq:htmlTag`/ `cq:tagName` or `decorationTagName`.

### デシジョンツリー {#decision-tree-1}

The following decision tree illustrates how `cq:noDecoration`, `cq:htmlTag`, `cq:tagName`, and `decorationTagName` affect the wrapper behavior.

![chlimage_1-3](assets/chlimage_1-3a.jpeg)

