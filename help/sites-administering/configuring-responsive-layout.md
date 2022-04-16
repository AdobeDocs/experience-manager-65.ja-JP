---
title: レイアウトコンテナおよびレイアウトモードの設定
seo-title: Configuring Layout Container and Layout Mode
description: レイアウトコンテナおよびレイアウトモードの設定方法について学びます。
seo-description: Learn how to configure Layout Container and Layout Mode.
uuid: 952b7c86-76ab-4699-8530-8638e46bb50f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 10940000-808a-48ae-8e46-61eccef71eab
legacypath: /content/docs/en/aem/6-2/administer/operations/page-authoring/configuring-responsive-layouting
exl-id: 61152b2d-4c0b-4cfd-9669-cf03d32cb7c7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '1309'
ht-degree: 100%

---

# レイアウトコンテナおよびレイアウトモードの設定{#configuring-layout-container-and-layout-mode}

[レスポンシブレイアウト](/help/sites-authoring/responsive-layout.md)は、[レスポンシブ web デザイン](https://ja.wikipedia.org/wiki/%E3%83%AC%E3%82%B9%E3%83%9D%E3%83%B3%E3%82%B7%E3%83%96%E3%82%A6%E3%82%A7%E3%83%96%E3%83%87%E3%82%B6%E3%82%A4%E3%83%B3)を実現するためのメカニズムです。レスポンシブレイアウトを使用すると、ユーザーが使用するデバイスのレイアウトとサイズに応じて web ページを作成できます。

>[!NOTE]
>
>これは、アダプティブ web デザイン（主にクラシック UI 用）を使用する[モバイル web](/help/sites-developing/mobile-web.md) メカニズムと比較できます。

AEM は、次のメカニズムを組み合わせて使用することにより、ページのレスポンシブレイアウトを実現します。

* [**レイアウトコンテナ**](/help/sites-authoring/responsive-layout.md#adding-a-layout-container-and-its-content-edit-mode)&#x200B;コンポーネント

   このコンポーネントは、レスポンシブグリッド内にコンポーネントを追加および配置できるグリッド段落システムを提供します。ページのデフォルトの parsys として使用したり、コンポーネントブラウザーで作成者が使用できるようにしたりできます。

   * デフォルトの&#x200B;**レイアウトコンテナ**&#x200B;コンポーネントは以下の場所で定義します。

      /libs/wcm/foundation/components/responsivegrid

   * レイアウトコンテナは次のように定義できます。

      * ユーザーがページに追加できるコンポーネントとして。
      * ページのデフォルトの parsys として。
      * 両方として。

         レイアウトコンテナをページの標準とし、この中でユーザーがレイアウトコンテナをさらに追加できるようにすることができます。例えば、列を制御する場合などです。

* **[レイアウトモード](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode)**
レイアウトコンテナをページに配置したら、 
**レイアウト**&#x200B;モードを使用してレスポンシブグリッド内にコンテンツを配置することができます。

* [**エミュレーター**](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate)
コンポーネントをインタラクティブにサイズ変更することによって、デバイスやウィンドウのサイズに従ってレイアウトを再編成する、レスポンシブ web サイトを作成および編集できます。その後、エミュレーターを使用して、コンテンツのレンダリング方法を確認できます。

>[!CAUTION]
>
>**レイアウトコンテナ**&#x200B;コンポーネントはクラシック UI でも使用できますが、完全な機能を利用できるのはタッチ対応 UI のみです。

これらのレスポンシブグリッドメカニズムを使用すると、次のことが可能になります。

* ブレークポイント（デバイスのグループ分けを指示）を使用して、デバイスレイアウトに基づいて様々なコンテンツ動作を定義する。
* デバイスグループに基づいてコンポーネントを非表示にする（どのブレークポイントでコンポーネントを非表示にするかを定義する）。
* グリッドに対して水平方向のスナップを使用（グリッドにコンポーネントを配置し、必要に応じてサイズ変更し、横方向や上限方向への折たたみやリフローのタイミングを定義）する。
* 列の制御を実現します。

>[!NOTE]
>
>標準インストールでは、レスポンシブレイアウトは [We.Retail リファレンスサイト](/help/sites-developing/we-retail.md)用に設定されています。他のページの[レイアウトコンテナコンポーネントをアクティベート](#enable-the-layout-container-component-for-page)する必要があります。

## レスポンシブエミュレーターの設定 {#configuring-the-responsive-emulator}

このタスクをおこなうと、自分のサイトにレスポンシブ&#x200B;**エミュレーター**&#x200B;を表示できます。

### エミュレーション用のページコンポーネントの登録 {#register-your-page-components-for-emulation}

エミュレーターでページをサポートできるようにするには、ページコンポーネントを登録する必要があります。[シミュレーション用のページコンポーネントの登録](/help/sites-developing/responsive.md#registering-page-components-for-simulation)を参照してください。

### デバイスグループの指定 {#specify-the-device-groups}

エミュレーターの「デバイス」リストに表示されるデバイスグループを指定するには、[デバイスグループの指定](/help/sites-developing/responsive.md#specifying-the-device-groups)を参照してください。

### 指定したデバイスグループにサイトをリンク {#link-your-site-to-the-specified-device-groups}

エミュレーターを含めるには、サイトをデバイスグループにリンクする必要があります。[「デバイス」リストの追加](/help/sites-developing/responsive.md#adding-the-devices-list)（クラシック UI とタッチ操作向け UI の両方）を参照してください。

## サイトのレイアウトモードのアクティベート {#activate-layout-mode-for-your-site}

この手順は、サイトで&#x200B;**レイアウト**&#x200B;モードを有効にするために使用します。

### ブレークポイントの設定 {#configure-the-breakpoints}

[ブレークポイント](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate)には次の特徴があります。

* レスポンシブデザインで使用します。
* 定義可能です。

   * ページテンプレート上で定義した場合、設定は該当するテンプレートで作成されたすべてのページにコピーされます。
   * ページノード上で定義した場合、設定はすべての子ページに継承されます。

* タイトルと幅を定義します。

   * タイトルは、汎用デバイスグループを、必要に応じて向きを含めて説明します。例えば、phone、tablet、tabletlandscape などです。
   * 幅は、該当する汎用デバイスグループの最大幅をピクセル単位で定義します。例えば、ブレークポイント phone の幅が 768 である場合、これが電話デバイスに使用されるレイアウトの最大幅です。

* エミュレーターを使用しているときに、ページエディターの上部にマーカーとして表示されます。
* 親ノード階層から継承され、任意に上書きできます。
* 最後に設定されたブレークポイントより上のすべてに対応するデフォルト（標準）のブレークポイントがあります&#x200B;*。*

CRXDE Lite または XML を使用して定義できます。

>[!NOTE]
>
>新しいプロジェクトを設定する場合：
>
>* テンプレートにブレークポイントを追加する必要があります。
>
>既存のプロジェクト（既存のコンテンツを含む）を移行する場合：
>
>* テンプレートにブレークポイントを追加する必要があります。
>* 既存のページに同じブレークポイントを追加する
>
>  継承は操作中なので、これをコンテンツのルートページに制限できます。

#### CRXDE Lite を使用したブレークポイントの設定 {#configuring-breakpoints-using-crxde-lite}

1. CRXDE Lite（または同等のツール）を使用して、以下のいずれかに移動します。

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

定義の例は以下のとおりです。

```xml
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

### レイアウトコンテナをメイン parsys として設定 {#set-layout-container-as-main-parsys}

ページのメイン parsys をレイアウトコンテナになるように設定するには、parsys を次のように定義する必要があります。

`wcm/foundation/components/responsivegrid`

以下の場所で定義します。

* ページコンポーネント
* ページテンプレート（今後使用するため）

以下に、定義を説明する 2 つの例を示します。

* **HTL：**

   ```xml
   <sly data-sly-resource="${'par' @ resourceType='wcm/foundation/components/responsivegrid'}/>
   ```

* **JSP：**

   ```
   <cq:include path="par" resourceType="wcm/foundation/components/responsivegrid" />
   ```

### レスポンシブ CSS を含める {#include-the-responsive-css}

#### LESS を使用したブレークポイントの CSS {#css-for-breakpoints-using-less}

AEM では、LESS を使用して、必要な CSS の一部を生成します。これらをプロジェクトに含める必要があります。

さらに、[クライアントライブラリ](https://docs.adobe.com/content/docs/ja/aem/6-0/develop/the-basics/clientlibs.html)を使用して、設定および関数呼び出しを追加する必要があります。以下の LESS の抜粋は、プロジェクトに最低限追加する必要のあるものの例です。

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

基本のグリッド定義は以下の場所にあります。

`/libs/wcm/foundation/clientlibs/grid/grid_base.less`

#### スタイル設定の考慮事項 {#styling-considerations}

レスポンシブコンテナ内に格納されているコンポーネントは、レスポンシブグリッドサイズに従って（それぞれの HTML DOM 要素と共に）サイズ変更されます。したがって、このような状況では、固定幅の（制限された）DOM 要素の定義を回避（または更新）することをお勧めします。

次に例を示します。

* 前：

   * `width=100px`

* 後：

   * `max-width=100px`

#### サイズ変更とアダプティブ画像の整合性 {#resizing-and-adaptive-image-compliance}

グリッド内でコンポーネントをサイズ変更すると、以下のリスナーが適宜トリガーされます。

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

## ページ用にレイアウトコンテナコンポーネントを有効化 {#enable-the-layout-container-component-for-page}

このタスクにより、作成者は、**レイアウトコンテナ**&#x200B;コンポーネントのインスタンスをページにドラッグできます。

### ページ編集用にレイアウトコンテナコンポーネントを有効化 {#enable-the-layout-container-component-for-page-editing}

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

   レスポンシブグリッドの定義は次の場所で指定します。

   `etc/design/<*your-project-name*>/.content.xml`

   以下のパラメーターを定義できます。

   * 使用可能な列の数：

      * `columns="{String}8"`
   * 現在のコンポーネントに追加できるコンポーネント：

      * `components="[/libs/wcm/foundation/components/responsivegrid, ...`
