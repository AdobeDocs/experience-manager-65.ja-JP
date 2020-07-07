---
title: レイアウトコンテナおよびレイアウトモードの設定
seo-title: レイアウトコンテナおよびレイアウトモードの設定
description: レイアウトモードとレイアウトコンテナを設定する方法について説明します。
seo-description: レイアウトモードとレイアウトコンテナを設定する方法について説明します。
uuid: 952b7c86-76ab-4699-8530-8638e46bb50f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 10940000-808a-48ae-8e46-61eccef71eab
legacypath: /content/docs/en/aem/6-2/administer/operations/page-authoring/configuring-responsive-layouting
translation-type: tm+mt
source-git-commit: ebf3f34af7da6b1a659ac8d8843152b97f30b652
workflow-type: tm+mt
source-wordcount: '1324'
ht-degree: 81%

---


# レイアウトコンテナおよびレイアウトモードの設定{#configuring-layout-container-and-layout-mode}

[レスポンシブレイアウト](/help/sites-authoring/responsive-layout.md) は、レスポン [シブなWebデザインを実現するメカニズムです](https://en.wikipedia.org/wiki/Responsive_web_design)。 レスポンシブレイアウトを使用すると、ユーザーが使用するデバイスのレイアウトとサイズに応じて Web ページを作成できます。

>[!NOTE]
>
>これは、アダプティブ Web デザイン（主にクラシック UI 用）を使用する[モバイル Web](/help/sites-developing/mobile-web.md) メカニズムと比較できます。

AEM は、次のメカニズムを組み合わせて使用することにより、ページのレスポンシブレイアウトを実現します。

* [**レイアウトコンテナ&#x200B;**](/help/sites-authoring/responsive-layout.md#adding-a-layout-container-and-its-content-edit-mode)コンポーネント

   このコンポーネントは、レスポンシブグリッド内にコンポーネントを追加および配置できるグリッド段落システムを提供します。ページのデフォルトのparsysとして使用したり、コンポーネントブラウザで作成者が使用できるようにしたりできます。

   * The default **Layout Container** component is defined under:

      /libs/wcm/foundation/components/responsivegrid

   * レイアウトコンテナは次のように定義できます。

      * ユーザーがページに追加できるコンポーネントとして。
      * ページのデフォルトの parsys として。
      * 両方.

         ページの標準としてレイアウトコンテナを使用できますが、その中にレイアウトコンテナを追加することもできます。 例えば、列の制御を行う場合に使用します。

* **[レイアウトモード](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode)**レイアウトコンテナがページ上に配置されたら、****レイアウトモードを使用してレスポンシブグリッド内にコンテンツを配置できます。
[**エミュレーター&#x200B;**](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate)コンポーネントをインタラクティブにサイズ変更することによってデバイスやウィンドウのサイズに従ってレイアウトを再編成する、レスポンシブ Web サイトを作成および編集できます。その後、エミュレーターを使用して、コンテンツのレンダリング方法を確認できます。**

* [!CAUTION]**](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate)

>**レイアウトコンテナ**&#x200B;コンポーネントはクラシック UI でも使用できますが、完全な機能を利用できるのはタッチ対応 UI のみです。
>
>これらのレスポンシブグリッドメカニズムを使用すると、次のことが可能になります。****

ブレークポイント（デバイスのグループ分けを指示）を使用して、デバイスレイアウトに基づいて様々なコンテンツ動作を定義する。

* デバイスグループに基づいてコンポーネントを非表示にする（どのブレークポイントでコンポーネントを非表示にするかを定義する）。
* グリッドに対して水平方向のスナップを使用（グリッドにコンポーネントを配置し、必要に応じてサイズ変更し、横方向や上限方向への折たたみやリフローのタイミングを定義）する。
* 列の制御を実現する。
* [!NOTE]

>標準インストールでは、レスポンシブレイアウトは [We.Retail リファレンスサイト](/help/sites-developing/we-retail.md)用に設定されています。他のページの[レイアウトコンテナコンポーネントをアクティベート](#enable-the-layout-container-component-for-page)する必要があります。
>
>レスポンシブエミュレーターの設定 {#configuring-the-responsive-emulator}](/help/sites-developing/we-retail.md)[](#enable-the-layout-container-component-for-page)

## このタスクをおこなうと、自分のサイトにレスポンシブ&#x200B;**エミュレーター**&#x200B;を表示できます。

エミュレーション用のページコンポーネントの登録 {#register-your-page-components-for-emulation}**

### エミュレーターでページをサポートできるようにするには、ページコンポーネントを登録する必要があります。[シミュレーション用のページコンポーネントの登録](/help/sites-developing/responsive.md#registering-page-components-for-simulation)を参照してください。

デバイスグループの指定 {#specify-the-device-groups}](/help/sites-developing/responsive.md#registering-page-components-for-simulation)

### エミュレーターの「デバイス」リストに表示されるデバイスグループを指定するには、[デバイスグループの指定](/help/sites-developing/responsive.md#specifying-the-device-groups)を参照してください。

指定したデバイスグループにサイトをリンク {#link-your-site-to-the-specified-device-groups}](/help/sites-developing/responsive.md#specifying-the-device-groups)

### エミュレーターを含めるには、サイトをデバイスグループにリンクする必要があります。[「デバイス」リストの追加](/help/sites-developing/responsive.md#adding-the-devices-list)（クラシック UI とタッチ操作向け UI の両方）を参照してください。

サイトのレイアウトモードのアクティベート {#activate-layout-mode-for-your-site}](/help/sites-developing/responsive.md#adding-the-devices-list)

## These procedures are used to enable the **Layout** mode on your site.

ブレークポイントの設定 {#configure-the-breakpoints}**

### [ブレークポイント](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate)には次の特徴があります。

[レスポンシブデザインで使用します。](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate)

* 定義可能です。
* ページテンプレート上で定義した場合、設定は該当するテンプレートで作成されたすべてのページにコピーされます。

   * ページノード上で定義した場合、設定はすべての子ページに継承されます。
   * タイトルと幅を定義します。

* タイトルは、汎用デバイスグループを、必要に応じて向きを含めて説明します。例えば、phone、tablet、tabletlandscape などです。

   * 幅は、該当する汎用デバイスグループの最大幅をピクセル単位で定義します。例えば、ブレークポイント phone の幅が 768 である場合、これが電話デバイスに使用されるレイアウトの最大幅です。
   * エミュレーターを使用しているときに、ページエディターの上部にマーカーとして表示されます。

* 親ノード階層から継承され、任意に上書きできます。
* 最後に設定されたブレークポイントより上のすべてに対応するデフォルト（標準）のブレークポイントがあります。**
* CRXDE Lite または XML を使用して定義できます。**

[!NOTE]

>[!NOTE]新しいプロジェクトを設定する場合：
>
>テンプレートにブレークポイントを追加する必要があります。
>
>* 既存のプロジェクト（既存のコンテンツを含む）を移行する場合：
>
>
テンプレートにブレークポイントを追加する必要があります。
>
>* 既存のページに同じブレークポイントを追加する
>* 継承が動作している間は、コンテンツのルートページに制限できます。

>
>  
CRXDE Lite を使用したブレークポイントの設定 {#configuring-breakpoints-using-crxde-lite}

#### CRXDE Lite（または同等のツール）を使用して、以下のいずれかに移動します。{#configuring-breakpoints-using-crxde-lite}

1. テンプレート定義。

   * The `jcr:content` node of your page.
   * Under `jcr:content` create the node:

1. 名前：`cq:responsive`

   * 型：`nt:unstructured`
   * この下に、以下のノードを作成します。`nt:unstructured`

1. 名前：`breakpoints`

   * 型：`nt:unstructured`
   * breakpoints ノードの下に、任意の数のブレークポイントを作成できます。それぞれ、以下のプロパティを持つ単一のノードとして定義します。`nt:unstructured`

1. 名前：`<descriptive name>`

   * 型：`nt:unstructured`
   * タイトル: `String` * `<descriptive title seen in Emulator>`*
   * 幅: `Decimal` * `<value of breakpoint>`*
   * XML を使用したブレークポイントの設定 {#configuring-breakpoints-using-xml}`<value of breakpoint>`

#### Breakpoints are located inside the `<jcr:content>` section of the `.context.html` under the appropriate template (or content) folder.

定義の例は以下のとおりです。`<jcr:content>``.context.html`

レスポンシブ情報プロバイダーの追加 {#add-a-responsive-information-provider}

```xml
<cq:responsive jcr:primaryType="nt:unstructured">
  <breakpoints jcr:primaryType="nt:unstructured">
    <phone jcr:primaryType="nt:unstructured" title="{String}Phone" width="{Decimal}768"/>
    <tablet jcr:primaryType="nt:unstructured" title="{String}Tablet" width="{Decimal}1200"/>
  </breakpoints>
</cq:responsive>
```

### [!NOTE]

>[!NOTE]これは、ページコンポーネントが基盤ページコンポーネントに基づいていない場合にのみ必要です。
>
>以下の `cq:infoProviders` ノード構造を、親ページコンポーネントにコピーします。

`/libs/foundation/components/page/cq:infoProviders/responsive`

ページのコンポーネントサイズ変更の有効化 {#enable-component-resizing-for-the-page}

## These procedures are required so you can resize components in the **Layout** mode.

レイアウトコンテナをメイン parsys として設定 {#set-layout-container-as-main-parsys}**

### ページのメイン parsys をレイアウトコンテナになるように設定するには、parsys を次のように定義する必要があります。{#set-layout-container-as-main-parsys}

`wcm/foundation/components/responsivegrid`

`wcm/foundation/components/responsivegrid`以下の場所で定義します。

ページコンポーネント

* ページテンプレート（今後使用するため）
* 以下に、定義を説明する 2 つの例を示します。

**HTL:**

* **JSP:**

   ```xml
   <sly data-sly-resource="${'par' @ resourceType='wcm/foundation/components/responsivegrid'}/>
   ```

* レスポンシブ CSS を含める {#include-the-responsive-css}**

   ```
   <cq:include path="par" resourceType="wcm/foundation/components/responsivegrid" />
   ```

### LESS を使用したブレークポイントの CSS {#css-for-breakpoints-using-less}

#### AEM では、LESS を使用して、必要な CSS の一部を生成します。これらをプロジェクトに含める必要があります。{#css-for-breakpoints-using-less}

さらに、[クライアントライブラリ[#$tu99]を使用して、設定および関数呼び出しを追加する必要があります。以下の LESS の抜粋は、プロジェクトに最低限追加する必要のあるものの例です。



```java
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

`/libs/wcm/foundation/clientlibs/grid/grid_base.less`

スタイル設定の考慮事項 {#styling-considerations}

#### レスポンシブコンテナ内に格納されているコンポーネントは、レスポンシブグリッドサイズに従って（それぞれの HTML DOM 要素と共に）サイズ変更されます。したがって、このような状況では、固定幅の（制限された）DOM 要素の定義を回避（または更新）することをお勧めします。{#styling-considerations}

次に例を示します。

前:

* `width=100px`

   * `width=100px`後:

* `max-width=100px`

   * サイズ変更とアダプティブ画像の整合性 {#resizing-and-adaptive-image-compliance}

#### グリッド内でコンポーネントをサイズ変更すると、以下のリスナーが適宜トリガーされます。{#resizing-and-adaptive-image-compliance}

`beforeedit`

* `beforechildedit`
* `afteredit`
* `afterchildedit`

* To properly resize and update the content of an adaptive image included in a responsive grid, you need to add an `afterEdit` set to `REFRESH_PAGE` listener into the `EditConfig` file of every contained component.

次に例を示します。`afterEdit``REFRESH_PAGE``EditConfig`

`<cq:listeners jcr:primaryType="cq:EditListenersConfig" afteredit="REFRESH_PAGE" />`

`<cq:listeners jcr:primaryType="cq:EditListenersConfig" afteredit="REFRESH_PAGE" />`アダプティブ画像のメカニズムは、ウィンドウの現在のサイズに適した画像の選択を制御するスクリプトを介して使用可能になります。DOM の準備が整った後、または専用のイベントを受信したときにアクティベートされます。現時点のところ、ユーザーのアクションの結果を適切に反映するには、ページを更新する必要があります。

[!CAUTION]

>[!CAUTION]作成者と発行で正しく機能するには、カスタムスタイルシートclientlibをヘッダーの一部として読み込む必要があります。
>
>ページ用にレイアウトコンテナコンポーネントを有効化 {#enable-the-layout-container-component-for-page}

## このタスクにより、作成者は、**レイアウトコンテナ**&#x200B;コンポーネントのインスタンスをページにドラッグできます。

ページ編集用にレイアウトコンテナコンポーネントを有効化 {#enable-the-layout-container-component-for-page-editing}**

### 作成者がさらに多くのレスポンシブグリッドをコンテンツページに追加できるようにするには、ページのレイアウトコンテナコンポーネントを有効にする必要があります。これは、次のいずれかを使用しておこないます。{#enable-the-layout-container-component-for-page-editing}

**オーサー環境**

* [デザインモード](/help/sites-authoring/default-components-designmode.md)を使用して、ページの&#x200B;**レイヤーコンテナ**&#x200B;コンポーネントをアクティベートします。

   **コンポーネント定義******

* コンポーネントを定義するときに、`allowedComponent` または静的インクルードを使用します。**

   レイアウトコンテナのグリッドの設定 {#configure-the-grid-of-the-layout-container}

### レイアウトコンテナの特定のインスタンスごとに、使用可能な列の数を設定できます。{#configure-the-grid-of-the-layout-container}

**オーサー環境**

1. **レイアウトコンテナの特定のインスタンスごとに、使用可能な列の数を設定できます。**

   これをおこなうには、[デザインモード](/help/sites-authoring/default-components-designmode.md)を使用して、必要なコンテナのデザインダイアログを開きます。ここで、配置やサイズ設定に使用できる列の数を指定できます。デフォルトは 12 です。

   **XML**

1. **レスポンシブグリッドの定義は次の場所で指定します。**

   `etc/design/<*your-project-name*>/.content.xml`

   `etc/design/<*your-project-name*>/.content.xml`以下のパラメーターを定義できます。

   使用可能な列の数：

   * `columns="{String}8"`

      * `columns="{String}8"`現在のコンポーネントに追加できるコンポーネント：
   * `components="[/libs/wcm/foundation/components/responsivegrid, ...`

      * `components="[/libs/wcm/foundation/components/responsivegrid, ...`


