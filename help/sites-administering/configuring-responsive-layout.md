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
source-git-commit: 30327950779337ce869b6ca376120bc09826be21
workflow-type: tm+mt
source-wordcount: '1288'
ht-degree: 46%

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
これにより、コンポーネントのサイズをインタラクティブに変更することで、デバイスやウィンドウのサイズに従ってレイアウトを並べ替えるレスポンシブ Web サイトを作成および編集できます。 その後、エミュレーターを使用してコンテンツがどのようにレンダリングされるかを確認できます。

>[!CAUTION]
>
>ただし、 **レイアウトコンテナ** コンポーネントはクラシック UI で使用でき、完全な機能はタッチ操作対応 UI でのみ使用できます。

これらのレスポンシブグリッドメカニズムを使用すると、次のことができます。

* ブレークポイント（デバイスのグループ化を示す）を使用して、デバイスのレイアウトに基づいて異なるコンテンツの動作を定義します。
* デバイスグループに基づいてコンポーネントを非表示にします（コンポーネントを非表示にするブレークポイントを定義します）。
* グリッドに対して水平方向のスナップを使用します（グリッドにコンポーネントを配置し、必要に応じてサイズを変更し、横に並ぶか上下に並ぶように折りたたむ/折り返すタイミングを定義します）。
* 列の制御を実現します。

>[!NOTE]
>
>そのまま使用できるインストールでは、レスポンシブレイアウトが [We.Retail 参照サイト](/help/sites-developing/we-retail.md). 他のページの[レイアウトコンテナコンポーネントをアクティベート](#enable-the-layout-container-component-for-page)する必要があります。

## レスポンシブエミュレーターの設定 {#configuring-the-responsive-emulator}

このタスクをおこなうと、自分のサイトにレスポンシブ&#x200B;**エミュレーター**&#x200B;を表示できます。

### エミュレーション用のページコンポーネントの登録 {#register-your-page-components-for-emulation}

エミュレーターがページをサポートできるようにするには、ページコンポーネントを登録する必要があります。 詳しくは、 [シミュレーション用のページコンポーネントの登録](/help/sites-developing/responsive.md#registering-page-components-for-simulation).

### デバイスグループの指定 {#specify-the-device-groups}

エミュレーターの「デバイス」リストに表示されるデバイスグループを指定するには、次を参照してください。 [デバイスグループの指定](/help/sites-developing/responsive.md#specifying-the-device-groups).

### 指定したデバイスグループにサイトをリンクする {#link-your-site-to-the-specified-device-groups}

エミュレーターを含めるには、サイトをデバイスグループにリンクします。 詳しくは、 [デバイスリストの追加](/help/sites-developing/responsive.md#adding-the-devices-list) （クラシック UI とタッチ操作向け UI の両方）。

## サイトのレイアウトモードのアクティベート {#activate-layout-mode-for-your-site}

この手順は、サイトで&#x200B;**レイアウト**&#x200B;モードを有効にするために使用します。

### ブレークポイントの設定 {#configure-the-breakpoints}

[ブレークポイント](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate)には次の特徴があります。

* レスポンシブデザインで使用されます。
* 次の項目を定義できます。

   * ページテンプレート上で、設定は、そのテンプレートで作成されたすべてのページにコピーされます。
   * ページノード上の。このノードから、設定が子ページに継承されます。

* タイトルと幅を定義します。

   * タイトルは、必要に応じて向きと共に、一般的なデバイスのグループ化を表します。例えば、phone、tablet、tabletlandscape などです。
   * 幅は、その汎用デバイスのグループ化の最大幅をピクセル単位で定義します。 例えば、ブレークポイント電話の幅が 768 の場合、電話デバイスに使用されるレイアウトの最大幅になります。

* エミュレーターを使用しているときに、ページエディターの上部にマーカーとして表示されます。
* 親ノード階層から継承され、自由に上書きできます。
* 最後に設定されたブレークポイントより上のすべてに対応するデフォルト（標準）のブレークポイントがあります&#x200B;*。*

CRXDE Lite または XML を使用して定義できます。

>[!NOTE]
>
>新しいプロジェクトを設定する場合：
>
>* テンプレートにブレークポイントを追加します。
>
>既存のプロジェクト（既存のコンテンツを含む）を移行する場合は、次の操作をおこなう必要があります。
>
>* テンプレートへのブレークポイントの追加
>* 既存のページに同じブレークポイントを追加する
>
>  継承は操作中なので、これをコンテンツのルートページに制限できます。

#### CRXDE Lite {#configuring-breakpoints-using-crxde-lite}

1. CRXDE Lite（または同等のもの）を使用して、次のいずれかに移動します。

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

定義の例：

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

### レイアウトコンテナをメインの Parsys に設定 {#set-layout-container-as-main-parsys}

ページのメイン parsys をレイアウトコンテナに設定するには、parsys を次のように定義します。

`wcm/foundation/components/responsivegrid`

次のいずれかで、

* ページコンポーネント
* ページテンプレート（今後の使用のため）

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

#### LESS を使用するブレークポイントの CSS {#css-for-breakpoints-using-less}

AEMは、必要な CSS の一部を生成するために LESS を使用します。これらは、プロジェクトに含める必要があります。

また、 [クライアントライブラリ](https://experienceleague.adobe.com/docs/?lang=ja) 追加の設定および関数呼び出しを提供する。 以下の LESS の抽出は、プロジェクトに追加する必要のある最小限の例です。

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

基本グリッドの定義は、次の場所にあります。

`/libs/wcm/foundation/clientlibs/grid/grid_base.less`

#### スタイル設定に関する考慮事項 {#styling-considerations}

レスポンシブコンテナ内に保持されているコンポーネントは、レスポンシブHTMLのサイズに従って（各グリッド DOM 要素と共に）サイズ変更されます。 したがって、このような状況では、固定幅（含まれる）の DOM 要素の定義を避ける（または更新する）ことをお勧めします。

次に例を示します。

* 前：

   * `width=100px`

* 後：

   * `max-width=100px`

#### サイズ変更とアダプティブ画像の準拠 {#resizing-and-adaptive-image-compliance}

グリッド内のコンポーネントのサイズを変更すると、次のリスナーが適宜トリガーになります。

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

これらのタスクを使用すると、作成者は **レイアウトコンテナ** コンポーネントをページ上に配置します。

### ページ編集用のレイアウトコンテナコンポーネントの有効化 {#enable-the-layout-container-component-for-page-editing}

作成者がさらに多くのレスポンシブグリッドをコンテンツページに追加できるようにするには、ページのレイアウトコンテナコンポーネントを有効にする必要があります。これは、次のいずれかを使用して行います。

* **オーサー環境**

   用途 [デザインモード](/help/sites-authoring/default-components-designmode.md) 有効にするには **レイヤーコンテナ** ページのコンポーネント。

* **コンポーネント定義**

   コンポーネントを定義するときに、`allowedComponent` または静的インクルードを使用します。

### レイアウトコンテナのグリッドの設定 {#configure-the-grid-of-the-layout-container}

レイアウトコンテナの特定のインスタンスごとに使用できる列数を設定できます。

1. **オーサー環境**

   レイアウトコンテナの特定のインスタンスごとに、使用できる列数を設定できます。

   これを行うには、[デザインモード](/help/sites-authoring/default-components-designmode.md)を使用して、必要なコンテナのデザインダイアログを開きます。ここで、配置やサイズ設定に使用できる列の数を指定できます。デフォルトは 12 です。

1. **XML**

   レスポンシブグリッドの定義は、次の場所で指定します。

   `etc/design/<*your-project-name*>/.content.xml`

   次のパラメーターを定義できます。

   * 使用可能な列数：

      * `columns="{String}8"`
   * 現在のコンポーネントに追加できるコンポーネント：

      * `components="[/libs/wcm/foundation/components/responsivegrid, ...`
