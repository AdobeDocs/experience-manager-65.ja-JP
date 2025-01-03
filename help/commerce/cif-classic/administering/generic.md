---
title: 汎用 e コマースの管理
description: AEM の汎用ソリューションは、リポジトリ内に保持されているコマース情報を管理する手段を提供します。
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
docset: aem65
exl-id: c29f6213-1df6-45af-91c8-14b255276d82
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '2907'
ht-degree: 100%

---

# 汎用 e コマースの管理 {#administering-generic-ecommerce}

Adobe Experience Manager（AEM）の汎用ソリューションは、（外部の e コマースエンジンを使用するのではなく）リポジトリ内に保持されているコマース情報を管理する手段を提供します。これには以下が含まれます。

* [製品](/help/commerce/cif-classic/administering/concepts.md#products)
* [製品バリアント](/help/commerce/cif-classic/administering/concepts.md#product-variants)
* [カタログ](/help/commerce/cif-classic/administering/concepts.md#catalogs)
* [プロモーション](/help/commerce/cif-classic/administering/concepts.md#promotions)
* [割引券](/help/commerce/cif-classic/administering/concepts.md#vouchers)
* [注文](/help/commerce/cif-classic/administering/concepts.md#shopping-cart-and-orders)
* [プロキシページ](/help/commerce/cif-classic/administering/concepts.md#proxy-pages)

>[!NOTE]
>
>標準の AEM インストールには、汎用 AEM（JCR）e コマース実装が含まれています。
>
>これは、デモンストレーション目的またはユーザーの要件に応じたカスタム実装の基盤として使用されています。

## 商品と商品バリエーション {#products-and-product-variations}

>[!NOTE]
>
>以下の手順は、商品と商品バリエーションのどちらにも適用されます。

製品を作成する前に、[基礎モード](/help/sites-authoring/scaffolding.md)を定義します。これにより、製品を定義する必要なフィールドと、その編集方法が指定されます。

基礎モードは、異なる商品タイプごとに必要です。次のどちらかの方法で、適切な基礎モードを商品に関連付けます。

* path
* 商品が基礎モードを参照できる

>[!NOTE]
>
>Geometrixx-Outdoors ストアの商品タイプは 1 つだけです（したがって基礎モードも次の場所に 1 つです）。
>
>`/etc/scaffolding/geometrixx-outdoors`
>
>Geometrixx-Outdoors の商品タイプは、次の場所でアクティブになっています。
>
>`/etc/commerce/products/geometrixx-outdoors`
>
>その下であれば、新しい製品定義を追加の設定なしで作成できます。

### 商品の読み込み {#importing-products}

#### 商品の読み込み - タッチ操作向け UI {#importing-products-touch-optimized-ui}

1. **Commerce** から&#x200B;**製品**&#x200B;コンソールに移動します。
1. **製品**&#x200B;コンソールを使用して、必要な場所に移動します。
1. 「**製品を読み込み**」アイコンを使用すると、ウィザードが表示されます。

   ![「製品を読み込み」アイコン](/help/sites-administering/do-not-localize/chlimage_1-13.png)

1. 以下を指定します。

   * **インポーター**

     特定の[コマースプロバイダー](/help/commerce/cif-classic/administering/concepts.md#commerce-providers)用のインポーター（デフォルトでは `Geometrixx`）。

   * **ソース**

     読み込むファイル（ブラウザーを使用してファイルを選択できます）。

   * **増分読み込み**

     （完全インポートではなく）増分インポートかどうかを示します。

   >[!NOTE]
   >
   >（サンプル geometrixx-outdoor インポーターの）増分読み込みは、商品レベルで動作します。
   >
   >必要に応じて、カスタマイズされたインポーターが動作するように定義できます。

1. 「**次へ**」を選択して製品を読み込みます。実行されたアクションのログが表示されます。

   >[!NOTE]
   >
   >製品は現在の場所、または現在の場所に相対的な場所に読み込まれます。

   >[!NOTE]
   >
   >「**次へ**」と「**戻る**」を繰り返し使用すると、製品定義が繰り返し読み込まれます。ただし、SKU が同じ場合は、リポジトリ内に存在する情報が上書きされます。

1. 「**完了**」を選択して、ウィザードを閉じます。

#### 商品の読み込み - クラシック UI {#importing-products-classic-ui}

1. **ツール**&#x200B;コンソールを使用して、**コマース**&#x200B;フォルダーを開きます。
1. ダブルクリックして&#x200B;**製品インポーター**&#x200B;を開きます。

   ![製品インポーターコンソール](/help/sites-administering/assets/chlimage_1-22.jpeg)

1. 以下を指定します。

   * **ストア名**

     製品の読み込み先は、次のとおりです。

     `/etc/commerce/products/<*store name*>/`

   * **コマースプロバイダー**

     [コマースプロバイダー](/help/commerce/cif-classic/administering/concepts.md#commerce-providers)のインポーター（デフォルトでは Geometrixx）。

   * **ソースファイル**

     インポートするファイルのリポジトリ内の場所。

   * **増分読み込み**

     （完全インポートではなく）増分インポートかどうかを示します。

1. 「**製品を読み込み**」をクリックします。

### 商品情報の作成 {#creating-product-information}

>[!NOTE]
>
>標準の商品管理は必要最小限です。Geometrixx-Outdoors の商品セットは、基本的なものだからです。複雑さは製品の[基礎モード](/help/sites-authoring/scaffolding.md)によるので、独自の製品基礎モードを使用すれば、より高度な編集が可能になります。

#### 商品情報の作成 - タッチ操作向け UI {#creating-product-information-touch-optimized-ui}

1. （**コマース**&#x200B;から）**製品**&#x200B;コンソールを使用して、必要な場所に移動します。
1. 「**作成**」アイコンを使用して、（構造と場所に応じて）次のどちらかを選択します。

   * **製品を作成**
   * **製品バリエーションを作成**

   ![プラス形の作成アイコン](/help/sites-administering/do-not-localize/chlimage_1-14.png)

1. ウィザードが開きます。「**基本**」タブと「**製品**」タブを使用して、新しい商品または製品バリアントの[製品属性](/help/commerce/cif-classic/administering/concepts.md#product-attributes)を入力します。

   >[!NOTE]
   >
   >商品またはバリアントを作成するには、少なくとも&#x200B;**タイトル**&#x200B;と **SKU** が必要です。

1. 「**作成**」を選択して、定義を保存します。

>[!NOTE]
>
>多くの商品は、幅広いカラーやサイズで提供されています。基本となる商品と関連する製品バリアントに関する情報は、どちらも&#x200B;**製品**&#x200B;コンソールから管理できます。
>
>商品とそのバリアントはツリー構造として保存されます。商品情報が一番上にあり、バリアントがその下にあります（この構造は UI によって強制されます）。

### 商品情報の編集 {#editing-product-information}

>[!NOTE]
>
>geometrixx-outdoors の商品画像は、次の場所から供給されます。
>
>`/etc/commerce/products/...`
>
>そのため、デフォルトでは [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=ja) によって商品画像がブロックされるので、必要に応じて設定してください。

#### 商品情報の編集 - タッチ操作向け UI {#editing-product-information-touch-optimized-ui}

1. （**コマース**&#x200B;から）**製品**&#x200B;コンソールを使用して、商品情報に移動します。
1. 次のいずれかを使用します。

   * [クイックアクション](/help/sites-authoring/basic-handling.md#quick-actions)
   * [選択モード](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   **製品データを表示**&#x200B;アイコンを選択します。

   ![製品データを表示アイコン - 情報アイコン](/help/sites-administering/do-not-localize/chlimage_1-15.png)

1. [製品属性](/help/commerce/cif-classic/administering/concepts.md#product-attributes)が表示されます。「**編集**」と「**完了**」を使用して、変更があれば実行します。

### 商品リファレンスの表示 {#showing-product-references}

#### 商品リファレンスの表示 - タッチ操作向け UI {#showing-product-references-touch-optimized-ui}

1. （**コマース**&#x200B;から）**製品**&#x200B;コンソールを使用して、商品情報に移動します。
1. 次のアイコンを使用して、参照のセカンダリレールを開きます。

   ![二重矢印アイコン](/help/sites-administering/do-not-localize/chlimage_1-16.png)

1. 必要な製品を選択すると、セカンダリレールの更新が表示され、使用可能な参照タイプが表示されます。

   ![参照を開いた状態の製品コンソール](/help/sites-administering/assets/chlimage_1-88.png)

1. 参照タイプ（製品ページなど）をクリックして、リストを展開します。
1. 特定の参照を選択すると、次のオプションを表示できます。

   * 製品ページに移動
   * 製品ページを編集

   ![製品コンソールの参照パネル](/help/sites-administering/assets/chlimage_1-89.png)

### 商品の検索 {#search-for-products}

1. **コマース**&#x200B;から&#x200B;**製品**&#x200B;コンソールに移動します。
1. 次のアイコンを使用して、検索のセカンダリパネルを開きます。

   ![虫眼鏡アイコン](/help/sites-administering/do-not-localize/chlimage_1-17.png)

1. 製品の検索には、複数のファセットを使用できます。1 回の検索に 1 つまたは複数のファセットだけを使用できます。見つかった製品は次のように表示されます。

   ![製品コンソールの製品データ](/help/sites-administering/assets/chlimage_1-90.png)

1. 製品をクリックまたはタップすると、その製品が開きます。また、公開したり、製品データを表示したりすることもできます。

#### 検索の拡張 {#extending-search}

CRXDE Lite を使用して、既存のファセットを変更したり、新しいファセットを追加することができます。

1. 次の URL に移動します。

   `http://localhost:4502/crx/de/index.jsp#/libs/commerce/gui/content/products/aside/items/search/items/searchpanel/facets`

1. 例えば、製品の検索ページで表示されるサイズを変更できます。`sizegroup` ノードをクリックします。
1. `items` ノードをクリックしてから、`propertypredicate` ノードをクリックします。
1. `propertyValues` を編集できます。例えば、XS または XXL を追加したり、サイズを削除したりできます。
1. 「**すべて保存**」をクリックして、商品の検索ページに移動します。変更が表示されます。

### 複数のアセット {#multiple-assets}

製品コンポーネントに複数のアセットを追加して、製品ページに表示されるアセットを指定できます。

>[!NOTE]
>
>複数のアセットに関連する操作はすべて、タッチ操作向け UI を使用して実行されます。

#### 複数のアセットの追加 {#adding-multiple-assets}

1. **コマース**&#x200B;から&#x200B;**製品**&#x200B;コンソールに移動します。
1. **製品**&#x200B;コンソールを使用して、必要な商品に移動します。

   >[!NOTE]
   >
   >バリアントレベルではなく商品レベルに移動する必要があります。

1. 選択モードまたはクイックアクションを使用して、**製品データを表示**&#x200B;アイコンを選択します。
1. 編集アイコンを選択します。
1. 「**追加**」までスクロールします。

   ![製品データのスクリーンショットの追加](/help/sites-administering/assets/chlimage_1-91.png)

1. 「**追加**」を選択します。新しいアセットのプレースホルダーが表示されます。
1. 「**変更**」を選択すると、アセットを選択するダイアログボックスが開きます。
1. 追加するアセットを選択します。

   >[!NOTE]
   >
   >アセットは「[アセット](/help/assets/assets.md)」から選択できます。

1. 完了アイコンを選択します。

これで、2 つのアセットが製品コンポーネントに保存されました。製品ページにどちらを表示するかを設定できます。これはカテゴリシステムで機能します。最初に、個々のアセットにカテゴリを追加する必要があります。

1. 「**製品データを表示**」を選択します。
1. アセットの下の「**アセットカテゴリ**」に入力します（例：`cat1` および `cat2`）。

   >[!NOTE]
   >
   >カテゴリにはタグも使用できます。

1. 完了アイコンを選択します。変更内容を[ロールアウト](#rolling-out-a-catalog)する必要があります。

これで、製品コンポーネント内のアセットにカテゴリが追加されました。表示するカテゴリを次の 3 種類のレベルで設定できます。

* [製品ページ](#product-page)
* [カタログ](#catalog)
* [製品コンソール](#products-console)

>[!NOTE]
>
>カテゴリを設定していない場合、最初のアセットが製品ページに表示されます。

表示する画像を選択する仕組みは次のとおりです。

1. 製品ページ用にカテゴリが設定されているかどうかを確認します。
1. 設定されていない場合、カタログ用にカテゴリが設定されているかどうかを確認します。
1. 設定されていない場合、製品コンソール用にカテゴリが設定されているかどうかを確認します。

>[!NOTE]
>
>カタログレベルと製品コンソールレベルの両方で変更内容をロールアウトして、変更を適用し、商品ページ上で違いを確認する必要があります。

#### 製品ページ {#product-page}

1. 商品ページに移動します。
1. 製品コンポーネントを&#x200B;**編集**&#x200B;します。
1. 選択した&#x200B;**画像カテゴリ**&#x200B;を入力します（例：`cat1`）。
1. 「**完了**」を選択します。ページを更新すると、正しいアセットが表示されます。

#### カタログ  {#catalog}

1. カタログに移動します。
1. 「**プロパティを表示**」を選択します。
1. 「**編集**」を選択します。
1. 「**アセット**」タブを選択します。
1. 必要な&#x200B;**製品アセットカテゴリ**&#x200B;を入力します。
1. 「**完了**」を選択します。
1. 変更内容を[ロールアウト](#rolling-out-a-catalog)します。

#### 製品コンソール {#products-console}

1. **製品**&#x200B;コンソールを使用して、必要な商品に移動します。
1. 「**製品データを表示**」を選択します。
1. 「**編集**」を選択します。
1. **デフォルトのアセットカテゴリ**&#x200B;を入力します。
1. 「**完了**」を選択します。
1. 変更内容を[ロールアウト](#rolling-out-a-catalog)します。

### 商品情報の公開／非公開 {#publishing-unpublishing-product-information}

#### 商品情報の公開／非公開 - タッチ操作向け UI {#publishing-unpublishing-product-information-touch-optimized-ui}

>[!NOTE]
>
>多くの場合、商品情報は商品を参照するページを通じて公開されます。例えば、製品 Y を参照するページ X を公開する際に、AEM は、製品 Y も公開するかどうかを尋ねます。
>
>特殊なケースでは、AEM は、商品データからの直接の公開もサポートしています。

1. （**コマース**&#x200B;から）**製品**&#x200B;コンソールを使用して、商品情報に移動します。
1. 次のいずれかを使用します。

   * [クイックアクション](/help/sites-authoring/basic-handling.md#quick-actions)
   * [選択モード](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   必要に応じて&#x200B;**公開**&#x200B;アイコンまたは&#x200B;**非公開**&#x200B;アイコンを選択します。

   ![地球アイコン](/help/sites-administering/do-not-localize/chlimage_1-18.png) ![バツマークの付いた地球アイコン - 記号なし](/help/sites-administering/do-not-localize/chlimage_1-19.png)

   それぞれに応じて製品情報が公開または非公開になります。

<!-- Search&Promote is end of life as of September 1, 2022 ### Product Feed {#product-feed} -->

<!-- Search&Promote is end of life as of September 1, 2022 The Search&Promote integration lets you: -->

<!-- Search&Promote is end of life as of September 1, 2022 * use the eCommerce API, independently of the underlying repository structure and commerce platform. -->
<!-- Search&Promote is end of life as of September 1, 2022 * use the Index Connector feature of Search&Promote to provide a product feed in XML format. -->
<!-- Search&Promote is end of life as of September 1, 2022 * use the Remote Control feature of Search&Promote to perform on-demand or scheduled requests of the product feed -->
<!-- Search&Promote is end of life as of September 1, 2022 * feed generation for different Search&Promote accounts, configured as cloud services configurations. -->

<!-- Search&Promote is end of life as of September 1, 2022 For more information, read [Product Feed](/help/sites-administering/product-feed.md). -->

### 製品アップデート用のイベントハンドラー {#event-handler-for-product-updates}

製品が追加、編集、削除された場合や、製品ページが追加、編集、削除された場合にイベントを記録するイベントハンドラーがあります。次の OSGi イベントが用意されています。

* `com/adobe/cq/commerce/pim/PRODUCT_ADDED`
* `com/adobe/cq/commerce/pim/PRODUCT_MODIFIED`
* `com/adobe/cq/commerce/pim/PRODUCT_DELETED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_ADDED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_MODIFIED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_DELETED`

`PRODUCT_*` イベントの場合、パスは `/etc/commerce/products` 内の基本商品を指します。`PRODUCT_PAGE_*` イベントの場合、パスは `cq:Page` ノードを指します。

これらは web コンソールで OSGI イベント（`/system/console/events`）に次のように表示されます。

![OSGi イベントの例](/help/sites-administering/do-not-localize/chlimage_1-20.png)

>[!NOTE]
>
>[AEM でのイベント処理](https://blogs.adobe.com/experiencedelivers/experience-management/event_handling_incq/)も参照してください。

### 買い物かごに追加リンクを含む画像 {#image-with-add-to-cart-links}

買い物かごに追加リンクを含む画像コンポーネントを使用すると、画像上の製品にリンクされているホットスポットを作成することによって、製品を買い物かごにすばやく追加できます。

ホットスポットをクリックすると、商品のサイズと数量を選択できるダイアログが表示されます。

1. コンポーネントを追加するページに移動します。
1. コンポーネントをページにドラッグ＆ドロップします。
1. [アセットブラウザー](/help/sites-authoring/author-environment-tools.md#assets-browser)からコンポーネントに画像をドラッグ＆ドロップします。
1. 次のいずれかを実行できます。

   * コンポーネントをクリックし、続いて編集アイコンをクリック
   * ゆっくりダブルクリック

1. フルスクリーンアイコンをクリックします。

   ![フルスクリーンアイコン](/help/sites-administering/assets/chlimage_1-92.png)

1. ローンチマップアイコンをクリックします。

   ![ローンチマップアイコン](/help/sites-administering/assets/chlimage_1-93.png)

1. シェイプアイコンのいずれかをクリックします。

   ![シェイプアイコン](/help/sites-administering/do-not-localize/chlimage_1-21.png)

1. 必要に応じてシェイプを変更および移動します。
1. シェイプをクリックします。
1. 参照アイコンをクリックすると、[アセットピッカー](/help/assets/search-assets.md#assetpicker)が表示されます。

   >[!NOTE]
   >
   >または、商品パスを直接入力できます。商品パスは、バリアントレベルではなく商品レベルである必要があります。

   ![タイプのパス](/help/sites-administering/assets/chlimage_1-94.png)

1. 確認アイコンを 2 回クリックしてから、「フルスクリーンを終了」をクリックします。
1. ページ上でコンポーネントの横の任意の場所をクリックします。ページが更新され、画像の上に次の記号が表示されます。

   ![プラス記号](/help/sites-administering/do-not-localize/chlimage_1-22.png)

1. [プレビュー](/help/sites-authoring/editing-content.md#previewingpagestouchoptimizedui)モードに切り替えます。
1. 「+」ホットスポットをクリックします。「**パス**」に入力した商品のサイズと数量を選択できるダイアログが表示されます。

   ![商品の例：ポンチョ](/help/sites-administering/assets/chlimage_1-95.png)

1. サイズと数量を入力します。
1. 「買い物かごに追加」ボタンをクリックします。ダイアログが閉じます。
1. 買い物かごに移動します。商品が入っています。

#### 設定オプション {#configuration-options}

ホットスポットをクリックしたときのダイアログの表示を設定できます。

1. コンポーネントをクリックして、設定アイコンをクリックします。

   ![設定アイコン](/help/sites-administering/assets/chlimage_1-96.png)

1. 下にスクロールします。「**買い物かごに追加**」タブがあります。

   ![「買い物かごに追加」タブ](/help/sites-administering/assets/chlimage_1-97.png)

1. 「**買い物かごに追加**」をクリックします。3 つの設定オプションを使用できます。

   ![設定オプション](/help/sites-administering/assets/chlimage_1-98.png)

1. 完了アイコンをクリックします。

## カタログ {#catalogs}

### カタログの生成 {#generating-a-catalog}

#### カタログの生成 - タッチ操作向け UI {#generating-a-catalog-touch-optimized-ui}

>[!NOTE]
>
>カタログは、製品データを参照します。

カタログを生成するには：

1. Sites コンソールを開きます（例：[http://localhost:4502/sites.html/content](http://localhost:4502/sites.html/content)）。
1. ページを作成する場所に移動します。
1. オプションリストを開くには、**作成**&#x200B;アイコンを使用します。

   ![create-icon](/help/sites-administering/do-not-localize/chlimage_1-23.png)

1. リストから、「**カタログを作成**」を選択します。カタログを作成ウィザードが開きます。

   ![カタログを作成ウィザード](/help/sites-administering/assets/chlimage_1-99.png)

1. 必要なカタログのブループリントに移動します。
1. 「**選択**」ボタンを選択し、必要なカタログのブループリントをクリックします。
1. 「**次へ**」を選択します。

   ![カタログのプロパティウィザード](/help/sites-administering/assets/chlimage_1-100.png)

1. 「**タイトル**」と「**名前**」を入力します。
1. 「**作成**」ボタンを選択します。カタログが作成され、ダイアログが表示されます。

   ![カタログ作成ダイアログ](/help/sites-administering/assets/chlimage_1-101.png)

1. 「**完了**」ボタンを選択すると、サイトのコンソールに戻り、カタログを表示できます。

   「**カタログを開く**」ボタンをタップまたはクリックすると、カタログ（例：`http://localhost:4502/editor.html/content/test-catalog.html`）が開きます。

#### カタログの生成 - クラシック UI {#generating-a-catalog-classic-ui}

>[!NOTE]
>
>カタログは、[製品データ](#products-and-product-variants)を参照します。

1. **Web サイト**&#x200B;コンソールを使用して、**カタログのブループリント**&#x200B;に移動し、基本カタログに移動します。

   例：

   `http://localhost:4502/siteadmin#/content/catalogs/geometrixx-outdoors/base-catalog`

1. **セクションのブループリント**&#x200B;テンプレートを使用してページを作成します。

   例：`Swimwear`

1. 新しい `Swimwear` ページを開き、「**ブループリントを編集**」をクリックします。**プロパティ**&#x200B;ダイアログボックスが開き、**製品**&#x200B;選択の設定が可能になります。

   例えば、「**タグ／キーワード**」フィールドを開いてアクティビティを選択し、Geometrixx-Outdoors セクションから「Swimming」を選択します。

1. 「**OK**」をクリックしてプロパティを保存します。サンプルの製品が、ブループリントページの「**製品の選択条件**」の下に表示されます。
1. 「**ロールアウトの変更...**」をクリックし、「**ページとすべてのサブページをロールアウト**」を選択して、「**次へ**」をクリックしてから「**ロールアウト**」をクリックします。ロールアウトが正常に完了すると、**ステータス**&#x200B;インジケーターが緑色で表示されます。
1. 「**閉じる**」をクリックして、次の場所およびその下にある新しいカタログセクションを確認します。

   `http://localhost:4502/cf#/content/geometrixx-outdoors/en/swimwear.html`

1. ブループリントページで再び「**ブループリントを編集**」をクリックし、**プロパティ**&#x200B;ダイアログで「**生成されたページ**」タブを開きます。バナーリストフィールドで、表示する画像を選択します（例：`summer.jpg`）。
1. 「**OK**」をクリックしてプロパティを保存します。バナー情報が、ブループリントページの「**製品の選択条件**」の下に表示されます。
1. これらの新しい変更をロールアウトします。

### カタログのロールアウト {#rolling-out-a-catalog}

#### カタログのロールアウト - タッチ操作向け UI {#rolling-out-a-catalog-touch-optimized-ui}

カタログをロールアウトするには：

1. **Commerce** を介して&#x200B;**カタログ**&#x200B;コンソールに移動します。
1. ロールアウトするカタログに移動します。
1. 次のいずれかを使用します。

   * [クイックアクション](/help/sites-authoring/basic-handling.md#quick-actions)
   * [選択モード](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   **ロールアウトの変更**&#x200B;アイコンを選択します。

   ![ロールアウト](/help/sites-administering/do-not-localize/chlimage_1-24.png)

1. ウィザードで、必要に応じてロールアウトを設定してから、「**ロールアウトの変更**」をクリックします。
1. ダイアログボックスが開きます。処理が終了したら、「**完了**」を選択します。

#### カタログのロールアウト - クラシック UI {#rolling-out-a-catalog-classic-ui}

カタログをロールアウトするには：

1. ロールアウトするカタログに移動します。例：

   `http://localhost:4502/cf#/content/catalogs/geometrixx-outdoors/base-catalog.html`

1. 「**ロールアウトの変更...**」をクリックします。
1. 必要に応じてロールアウトを設定します。
1. 「**ロールアウト**」をクリックします。

### ブループリントインポーター {#blueprint-importer}

#### ブループリントインポーター - タッチ操作向け UI {#blueprint-importer-touch-optimized-ui}

1. **Commerce** を介して&#x200B;**カタログ**&#x200B;コンソールに移動します。
1. カタログブループリントを読み込む場所に移動します。
1. **ブループリントを読み込み**&#x200B;アイコンを選択します。

   ![ブループリントを読み込みアイコン](/help/sites-administering/do-not-localize/chlimage_1-13.png)

1. ウィザードで、必要に応じて「ソース」を選択し、「**次へ**」をクリックします。

   ![ブループリントウィザード](/help/sites-administering/assets/chlimage_1-102.png)

1. 読み込みが終了したら、「**完了**」を選択します。

#### ブループリントインポーター - クラシック UI {#blueprint-importer-classic-ui}

1. **ツール**&#x200B;コンソールを使用して、**Commerce** に移動します。

   例：

   `http://localhost:4502/miscadmin#/etc/commerce`

1. **カタログブループリントインポーター**&#x200B;を開きます。
1. 必要に応じてインポートを設定します。
1. 「**カタログのブループリントを読み込み**」をクリックします。

## プロモーション {#promotions}

### プロモーションの作成 {#creating-a-promotion}

#### プロモーションの作成 - クラシック UI {#creating-a-promotion-classic-ui}

>[!NOTE]
>
>次の例では、[キャンペーン](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md)で直接行われるプロモーションを示します。これは割引券に使用されます。
>
>プロモーションは、キャンペーン内の[エクスペリエンス](/help/sites-authoring/personalization.md)で行うこともできます。
>
>詳しくは、[プロモーションと割引券](#promotions-and-vouchers)を参照してください。

1. オーサーインスタンスの **web サイト**&#x200B;コンソールを開きます。
1. 左側のウィンドウで、必要な&#x200B;**キャンペーン**&#x200B;を選択します。
1. 「**新規**」をクリックし、**プロモーション**&#x200B;テンプレートを選択して、新しい割引券に対し「**タイトル**」（および必要に応じて「**名前**」）を指定します。
1. 「**作成**」をクリックします。新しいプロモーションページが右側のウィンドウに表示されます。

1. 次のどちらかの方法で、**プロパティ**&#x200B;を編集します。

   * このページを開き、「編集」ボタンをクリックしてプロパティダイアログを表示する
   * Web サイトコンソールでページを選択し、コンテキストメニュー（通常はマウスの右ボタン）を使用して「**プロパティ…**」を選択し、プロパティダイアログを開きます。

   「**プロモーションタイプ**」、「**割引タイプ**」、「**割引値**」および必要に応じてその他のフィールドを指定します。

1. 「**OK**」をクリックして保存します。

1. これでプロモーションをアクティベートできるようになり、買い物客にパブリッシュインスタンスでプロモーションが表示されます。

## 割引券 {#vouchers}

### 割引券の作成 {#creating-a-voucher}

#### 割引券の作成 - クラシック UI {#creating-a-voucher-classic-ui}

1. オーサーインスタンスの **web サイト**&#x200B;コンソールを開きます。
1. 左側のウィンドウで、必要な&#x200B;**キャンペーン**&#x200B;を選択します。
1. 「**新規**」をクリックし、**割引券**&#x200B;テンプレートを選択して、新しい割引券に対し「**タイトル**」（および必要に応じて「**名前**」）を指定します。
1. 「**作成**」をクリックします。新しい割引券ページが右側のウィンドウに表示されます。

1. ダブルクリックで新しい割引券ページを開き、「**編集**」をクリックして、必要に応じて情報を設定します。
1. 「**OK**」をクリックして保存します。

1. これで割引券がアクティベートされ、買い物客がパブリッシュインスタンス上の買い物かごで利用できるようになります。

### 割引券の削除 {#removing-vouchers}

#### 割引券の削除 - クラシック UI {#removing-vouchers-classic-ui}

割引券を顧客が利用できないようにするには、次のいずれかの操作を実行します。

* 割引券を無効にする - オーサー環境には引き続きあるので、後でもう一度有効にできます。
* 完全に削除します。

いずれのアクションも、**Web サイト**&#x200B;コンソールで実行できます。

### 割引券の変更 {#modifying-vouchers}

#### 割引券の変更 - クラシック UI {#modifying-vouchers-classic-ui}

割引券またはプロモーションのプロパティを変更するには、**web サイト**&#x200B;コンソールでその割引券またはプロモーションをダブルクリックして「**編集**」をクリックします。保存後、変更がパブリッシュインスタンスにプッシュされるように、アクティベートする必要があります。

### 買い物かごへの割引券の追加 {#adding-vouchers-to-a-cart}

ユーザーが買い物かごに割引券を追加できるようにするには、組み込みの&#x200B;**割引券**&#x200B;コンポーネント（コマースカテゴリ）を使用します。このコンポーネントを、買い物かごが表示されているのと同じページに追加します（ただし必須ではありません）。ほとんどの場合、割引券コンポーネントはユーザーが割引券コードを入力できるフォームにすぎません。適用された割引券とその割引の一覧を実際に表示するのは、買い物かごコンポーネントです。

デモサイト（Geometrixx Outdoors - English）では、買い物かごページの実際の買い物かごの下に、割引券フォームが表示されます。

## 注文 {#orders}

>[!NOTE]
>
>標準の AEM には、商品の返送、注文ステータスの更新、受け渡しの実行、納品書の生成など、注文に関連する標準機能に必要なアクションがないことを思い出してください。主な目的は技術のプレビューです。
>
>AEM の汎用の Order Management は基本的なものにとどまっています。ウィザードで使用可能なフィールドは、次の基礎モードによって異なります。
>`/etc/scaffolding/geometrixx-outdoors/order/jcr:content/cq:dialog`
>
>カスタマイズされた基礎モードを作成する場合は、さらに多くの注文情報を保存できます。

>[!NOTE]
>
>注文コンソールには、公開されることのないベンダーの注文情報が表示されます。
>
> 顧客の注文情報はそのホームディレクトリに保持され、顧客のアカウントの注文履歴で公開されます。この情報は、ホームディレクトリの残りの情報と共に公開されます。

### 注文情報の作成 {#creating-order-information}

#### 注文情報の作成 - タッチ操作向け UI {#creating-order-information-touch-optimized-ui}

1. **製品**&#x200B;コンソールを使用して、必要な商品に移動します。
1. 「**作成**」アイコンを使用して、「**注文を作成**」を選択します。

   ![プラス形の作成アイコン](/help/sites-administering/do-not-localize/chlimage_1-14.png)

1. ウィザードが開きます。「**基本**」「**コンテンツ**」「**支払い**」「**受け渡し**」タブを使用して、[新しい注文に関する情報](/help/commerce/cif-classic/administering/concepts.md#order-information)を入力します。

1. 「**作成**」を選択して、定義を保存します。

### 注文情報の編集 {#editing-order-information}

#### 注文情報の編集 - タッチ操作向け UI {#editing-order-information-touch-optimized-ui}

1. **注文**&#x200B;コンソールを使用して、注文に移動します。
1. 次のいずれかを使用します。

   * [クイックアクション](/help/sites-authoring/basic-handling.md#quick-actions)
   * [選択モード](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   **注文データを表示**&#x200B;アイコンを選択します。

   ![情報アイコン](/help/sites-administering/do-not-localize/chlimage_1-15.png)

1. [注文情報](/help/commerce/cif-classic/administering/concepts.md#order-information)が表示されます。変更するには、「**編集**」と「**完了**」を使用します。

