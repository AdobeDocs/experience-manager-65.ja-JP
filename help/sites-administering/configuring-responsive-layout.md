---
title: レイアウトコンテナおよびレイアウトモードの設定
description: レイアウトコンテナおよびレイアウトモードの設定方法について学びます。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
legacypath: /content/docs/en/aem/6-2/administer/operations/page-authoring/configuring-responsive-layouting
exl-id: 61152b2d-4c0b-4cfd-9669-cf03d32cb7c7
solution: Experience Manager, Experience Manager Sites
feature: Operations
role: Admin
source-git-commit: 17c4084d9ee93e5fe6652d63438eaf34cbc83c12
workflow-type: ht
source-wordcount: '1479'
ht-degree: 100%

---


# レイアウトコンテナおよびレイアウトモードの設定{#configuring-layout-container-and-layout-mode}

レイアウトコンテナおよびレイアウトモードの設定方法について学びます。

>[!TIP]
>
>このドキュメントでは、サイト管理者および開発者向けのレスポンシブデザインの概要と、AEMでの機能の実現方法について説明します。
>
>コンテンツ作成者の場合、コンテンツページでレスポンシブデザイン機能の使用方法について詳しくは、[コンテンツページのレスポンシブレイアウト](/help/sites-authoring/responsive-layout.md)ドキュメントを参照してください。

## 概要 {#overview}

[レスポンシブレイアウト](/help/sites-authoring/responsive-layout.md)は、[レスポンシブ web デザイン](https://en.wikipedia.org/wiki/Responsive_web_design)を実現するためのメカニズムです。レスポンシブレイアウトを使用すると、ユーザーが使用するデバイスのレイアウトとサイズに応じて web ページを作成できます。

AEM は、次のメカニズムを組み合わせて使用することにより、ページのレスポンシブレイアウトを実現します。

* [**レイアウトコンテナ**](/help/sites-authoring/responsive-layout.md#adding-a-layout-container-and-its-content-edit-mode)&#x200B;コンポーネント

  このコンポーネントが提供するグリッド段落システムを使用すると、レスポンシブグリッド内にコンポーネントを追加および配置できるようになります。ページのデフォルトの parsys として使用したり、コンポーネントブラウザーで作成者が使用できるようにしたりできます。

   * デフォルトの&#x200B;**レイアウトコンテナ**&#x200B;コンポーネントは以下の場所で定義します。

     `/libs/wcm/foundation/components/responsivegrid`

   * レイアウトコンテナは次のように定義できます。

      * ユーザーがページに追加できるコンポーネントとして。
      * ページのデフォルトの parsys として。
      * 両方として。

        レイアウトコンテナをページの標準とし、この中でユーザーがレイアウトコンテナをさらに追加できるようにすることができます。例えば、列を制御する場合などです。

* **[レイアウトモード](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode)**
レイアウトコンテナをページに配置したら、**レイアウト**&#x200B;モードを使用して、レスポンシブグリッド内にコンテンツを配置できます。

* [**エミュレーター**](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate)
これにより、コンポーネントのサイズをインタラクティブに変更することで、デバイスやウィンドウのサイズに従ってレイアウトを並べ替えるレスポンシブ web サイトを作成および編集できます。その後、ユーザーはエミュレーターを使用してコンテンツがどのようにレンダリングされるかを確認できます。

これらのレスポンシブグリッドのメカニズムを使用すると、次のことができます。

* ブレークポイント（デバイスのグループ化を示す）を使用して、デバイスのレイアウトに基づいて様々なコンテンツの動作を定義します。
* デバイスグループに基づいてコンポーネントを非表示にします（コンポーネントを非表示にするブレークポイントを定義します）。
* 水平にグリッドにスナップを使用します（グリッドにコンポーネントを配置し、必要に応じてサイズ変更し、横並びまたは上下に並べて折たたみやリフローのタイミングを定義）。
* 列の制御を実現します。

>[!TIP]
>
>アドビはフロントエンド開発者用に参照用としてレスポンシブレイアウトの [GitHub ドキュメント](https://adobe-marketing-cloud.github.io/aem-responsivegrid/)を提供しています。フロントエンド開発者は AEM の外部で AEM グリッドを使用できます（例えば、今後の AEM サイト向けに静的 HTML モックアップを作成する場合）。

>[!NOTE]
>
>標準のインストールでは、レスポンシブレイアウトは [We.Retail 参照サイト](/help/sites-developing/we-retail.md)に対して設定されています。他のページの[レイアウトコンテナコンポーネントをアクティベート](#enable-the-layout-container-component-for-page)します。

>[!CAUTION]
>
>**レイアウトコンテナ**&#x200B;コンポーネントはクラシック UI で使用できますが、完全な機能はタッチ操作対応 UI でのみ使用できます。

## レスポンシブエミュレーターの設定 {#configuring-the-responsive-emulator}

このタスクを行うと、自分のサイトにレスポンシブ&#x200B;**エミュレーター**&#x200B;を表示できます。

### エミュレーション用のページコンポーネントの登録 {#register-your-page-components-for-emulation}

エミュレーターがページをサポートできるようにするには、ページコンポーネントを登録する必要があります。詳しくは、[シミュレーション用のページコンポーネントの登録](/help/sites-developing/responsive.md#registering-page-components-for-simulation)を参照してください。

### デバイスグループの指定 {#specify-the-device-groups}

エミュレーターのデバイスリストに表示されるデバイスグループを指定するには、[デバイスグループの指定](/help/sites-developing/responsive.md#specifying-the-device-groups)を参照してください。

### 指定したデバイスグループにサイトをリンクする {#link-your-site-to-the-specified-device-groups}

エミュレーターを含めるには、サイトをデバイスグループにリンクします。詳しくは、[デバイスリストの追加](/help/sites-developing/responsive.md#adding-the-devices-list)（クラシック UI とタッチ操作向け UI の両方）を参照してください。

## サイトのレイアウトモードのアクティベート {#activate-layout-mode-for-your-site}

この手順は、サイトで&#x200B;**レイアウト**&#x200B;モードを有効にするために使用します。

### ブレークポイントの設定 {#configure-the-breakpoints}

[ブレークポイント](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate)には次の特徴があります。

* レスポンシブデザインで使用されます。
* 次の項目を定義できます。

   * ページテンプレートでは、設定は該当するテンプレートで作成されたすべてのページにコピーされます。
   * ページノードでは、設定は子ページに継承されます。

* 次のようにタイトルおよび幅を定義します。

   * タイトルは、必要に応じて向きと共に、一般的なデバイスのグループ化を表します。例えば、phone、tablet、tabletlandscape などです。
   * 幅は、一般的なデバイスのグループ化の最大幅をピクセル単位で定義します。例えば、電話のブレークポイントの幅が 768 である場合、これが電話デバイスに使用されるレイアウトの最大幅になります。

* エミュレーターの使用中に、ページエディターの上部にマーカーとして表示されます。
* 親ノード階層から継承され、自由に上書きできます。
* 最後に設定されたブレークポイントより上のすべてに対応するデフォルト（標準）のブレークポイントがあります&#x200B;*。*

CRXDE Lite または XML を使用して定義できます。

>[!NOTE]
>
>新しいプロジェクトを設定する場合：
>
>* テンプレートにブレークポイントを追加します。
>
>既存のプロジェクト（既存のコンテンツを含む）を移行する場合は、次の操作を行います。
>
>* テンプレートにブレークポイントを追加する
>* 既存のページに同じブレークポイントを追加する
>
>  継承は操作中なので、これをコンテンツのルートページに制限できます。

#### CRXDE Lite を使用したブレークポイントの設定 {#configuring-breakpoints-using-crxde-lite}

1. CRXDE Lite（または同等のツール）を使用して、次のいずれかに移動します。

   * テンプレート定義。
   * ページの `jcr:content` ノード。

1. `jcr:content` の下に、以下のノードを作成します。

   * 名前：`cq:responsive`
   * 型：`nt:unstructured`

1. この下に、次のノードを作成します。

   * 名前：`breakpoints`
   * 型：`nt:unstructured`

1. breakpoints ノードの下に、任意の数のブレークポイントを作成できます。それぞれ、以下のプロパティを持つ単一のノードとして定義してください。

   * 名前：`<descriptive name>`
   * 型：`nt:unstructured`
   * タイトル：`String` * `<descriptive title seen in Emulator>`*
   * 幅：`Decimal` * `<value of breakpoint>`*

#### XML を使用したブレークポイントの設定 {#configuring-breakpoints-using-xml}

ブレークポイントは、該当するテンプレート（またはコンテンツ）フォルダーの下で `.context.html` の `<jcr:content>` セクション内に配置されます。

定義の例は次のとおりです。

```html
<cq:responsive jcr:primaryType="nt:unstructured">
  <breakpoints jcr:primaryType="nt:unstructured">
    <phone jcr:primaryType="nt:unstructured" title="{String}Phone" width="{Decimal}768"/>
    <tablet jcr:primaryType="nt:unstructured" title="{String}Tablet" width="{Decimal}1200"/>
  </breakpoints>
</cq:responsive>
```

### レスポンシブ情報プロバイダーの追加 {#add-a-responsive-information-provider}

>[!NOTE]
>
>これは、ページコンポーネントが基盤ページコンポーネントに基づいていない場合にのみ必要です。

以下の `cq:infoProviders` ノード構造を、親ページコンポーネントにコピーします。

`/libs/foundation/components/page/cq:infoProviders/responsive`

## ページのコンポーネントサイズ変更の有効化 {#enable-component-resizing-for-the-page}

この手順は、**レイアウト**&#x200B;モードでコンポーネントのサイズ変更を可能にするために必要です。

### レイアウトコンテナをメインの parsys として設定する {#set-layout-container-as-main-parsys}

ページのメインの parsys をレイアウトコンテナとして設定するには、parsys を次のように定義します。

`wcm/foundation/components/responsivegrid`

次のいずれかで定義します。

* ページコンポーネント
* ページテンプレート（今後の使用のため）

以下に、定義を説明する 2 つの例を示します。

* **HTL：**

  ```html
  <sly data-sly-resource="${'par' @ resourceType='wcm/foundation/components/responsivegrid'}/>
  ```

* **JSP：**

  ```html
  <cq:include path="par" resourceType="wcm/foundation/components/responsivegrid" />
  ```

### レスポンシブ CSS を含める {#include-the-responsive-css}

#### LESS を使用した CSS のブレークポイント {#css-for-breakpoints-using-less}

AEM では、必要な CSS の一部の生成に LESS を使用するため、これらをプロジェクトに含める必要があります。

また、追加の設定と関数呼び出しを提供するために、[クライアントライブラリ](https://experienceleague.adobe.com/docs/?lang=ja)も作成する必要があります。次の LESS エクストラクトは、プロジェクトに追加する必要がある最小限の例です。

```css
@import (once) "/libs/wcm/foundation/clientlibs/grid/grid_base.less";

/* maximum amount of grid cells to be provided */
@max_col: 12;

/* default breakpoint */
.aem-Grid {
  .generate-grid(default, @max_col);
}

/* phone breakpoint */
@media (max-width: 768px) {
  .aem-Grid {
    .generate-grid(phone, @max_col);
  }
}

/* tablet breakpoint */
@media (min-width: 769px) and (max-width: 1200px) {
  .aem-Grid {
    .generate-grid(tablet, @max_col);
  }
}
```

基本のグリッドの定義は、次の場所にあります。

`/libs/wcm/foundation/clientlibs/grid/grid_base.less`

#### スタイル設定に関する考慮事項 {#styling-considerations}

レスポンシブコンテナ内に保持されるコンポーネントは、レスポンシブグリッドのサイズに従って（それぞれの HTML DOM 要素と共に）サイズ変更されます。したがって、このような状況では、（含まれている）固定幅の DOM 要素の定義を回避（または更新）することをお勧めします。

次に例を示します。

* 前：

   * `width=100px`

* 後：

   * `max-width=100px`

#### サイズ変更とアダプティブ画像の整合性 {#resizing-and-adaptive-image-compliance}

グリッド内でコンポーネントのサイズを変更すると、次のリスナーが適宜トリガーされます。

* `beforeedit`
* `beforechildedit`
* `afteredit`

* `afterchildedit`

レスポンシブグリッドに含まれているアダプティブ画像のコンテンツを適切にサイズ変更および更新するには、`REFRESH_PAGE` リスナーに設定されている `afterEdit` を、含まれているすべてのコンポーネントの `EditConfig` ファイルに追加する必要があります。

次に例を示します。

`<cq:listeners jcr:primaryType="cq:EditListenersConfig" afteredit="REFRESH_PAGE" />`

アダプティブ画像のメカニズムは、現在のウィンドウサイズに適した画像の選択を制御するスクリプトを介して使用可能になります。DOM の準備が整った後、または専用のイベントを受信するとアクティベートされます。現時点のところ、ユーザーのアクションの結果を適切に反映するには、ページを更新する必要があります。

>[!CAUTION]
>
>カスタムスタイルシートの clientlibs を作成時と公開時に適切に機能させるには、これをヘッダーの一部として読み込む必要があります。

## ページ用のレイアウトコンテナコンポーネントの有効化 {#enable-the-layout-container-component-for-page}

これらのタスクにより、作成者は&#x200B;**レイアウトコンテナ**&#x200B;コンポーネントのインスタンスをページにドラッグできます。

### ページ編集用のレイアウトコンテナコンポーネントの有効化 {#enable-the-layout-container-component-for-page-editing}

作成者がさらに多くのレスポンシブグリッドをコンテンツページに追加できるようにするには、ページのレイアウトコンテナコンポーネントを有効にする必要があります。これは、次のいずれかを使用して行います。

* **オーサー環境**

  [デザインモード](/help/sites-authoring/default-components-designmode.md)を使用して、ページの&#x200B;**レイヤーコンテナ**&#x200B;コンポーネントをアクティベートします。

* **コンポーネント定義**

  コンポーネントを定義するときに、`allowedComponent` または静的インクルードを使用します。

### レイアウトコンテナのグリッドの設定 {#configure-the-grid-of-the-layout-container}

レイアウトコンテナの特定のインスタンスごとに、使用可能な列の数を設定できます。

1. **オーサー環境**

   レイアウトコンテナの特定のインスタンスごとに、使用可能な列の数を設定できます。

   これを行うには、[デザインモード](/help/sites-authoring/default-components-designmode.md)を使用して、必要なコンテナのデザインダイアログを開きます。ここで、配置やサイズ設定に使用できる列の数を指定できます。デフォルトは 12 です。

1. **XML**

   レスポンシブグリッドの定義は、次の場所で指定します。

   `etc/design/<*your-project-name*>/.content.xml`

   以下のパラメーターを定義できます。

   * 使用可能な列の数：

      * `columns="{String}8"`

   * 現在のコンポーネントに追加できるコンポーネント：

      * `components="[/libs/wcm/foundation/components/responsivegrid, ...`

## ネストされたレスポンシブグリッド {#nested-responsive-grids}

プロジェクトのニーズをサポートするために、レスポンシブグリッドのネストが必要になる場合があります。ただし、アドビが推奨するベストプラクティスは、構造をできるだけフラットに保つことであることに注意してください。

ネストされたレスポンシブグリッドの使用を回避できない場合は、次の点を確認してください。

* すべてのコンテナ（コンテナ、タブ、アコーディオンなど）に `layout = responsiveGrid` プロパティがある。
* コンテナ階層でプロパティ `layout = simple` が混在していない。

これには、ページテンプレートのすべての構造コンテナが含まれます。

内側のコンテナの列番号は、外側のコンテナの列番号より大きくしないでください。次の例では、この条件を満たしています。デフォルト（デスクトップ）画面では外側のコンテナの列番号は 8 ですが、内側のコンテナの列番号は 4 です。

>[!BEGINTABS]

>[!TAB ノード構造の例]

```text
container
  @layout = responsiveGrid
  cq:responsive
    default
      @offset = 0
      @width = 8
  container
  @layout = responsiveGrid
    cq:responsive
      default
        @offset = 0
        @width = 4
    text
      @text =" Text Column 1"
```

>[!TAB 結果として得られる HTML の例]

```html
<div class="container responsivegrid aem-GridColumn--default--none aem-GridColumn aem-GridColumn--default--8 aem-GridColumn--offset--default--0">
  <div id="container-c9955c233c" class="cmp-container">
    <div class="aem-Grid aem-Grid--8 aem-Grid--default--8 ">
      <div class="container responsivegrid aem-GridColumn--default--none aem-GridColumn aem-GridColumn--offset--default--0 aem-GridColumn--default--4">
        <div id="container-8414e95866" class="cmp-container">
          <div class="aem-Grid aem-Grid--4 aem-Grid--default--4 ">
            <div class="text aem-GridColumn aem-GridColumn--default--4">
              <div data-cmp-data-layer="..." id="text-1234567890" class="cmp-text">
                <p>Text Column 1</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>
```

>[!ENDTABS]
