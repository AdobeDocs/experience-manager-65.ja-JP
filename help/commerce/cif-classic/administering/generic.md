---
title: 汎用 e コマースの管理
seo-title: Administering generic eCommerce
description: AEMの汎用ソリューションは、リポジトリ内に保持されているコマース情報を管理する方法を提供します。
seo-description: The AEM generic solution provides methods of managing the commerce information held within the repository.
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
docset: aem65
exl-id: c29f6213-1df6-45af-91c8-14b255276d82
source-git-commit: 6ebcc7bd5c72c01672244fdfba353a8949f6e331
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 汎用 e コマースの管理 {#administering-generic-ecommerce}

AEMの汎用ソリューションは、（外部 e コマースエンジンを使用するのとは異なり）リポジトリ内に保持されるコマース情報を管理する方法を提供します。 これには以下が含まれます。

* [製品](/help/commerce/cif-classic/administering/concepts.md#products)
* [製品バリアント](/help/commerce/cif-classic/administering/concepts.md#product-variants)
* [カタログ](/help/commerce/cif-classic/administering/concepts.md#catalogs)
* [プロモーション](/help/commerce/cif-classic/administering/concepts.md#promotions)
* [割引券](/help/commerce/cif-classic/administering/concepts.md#vouchers)
* [注文](/help/commerce/cif-classic/administering/concepts.md#shopping-cart-and-orders)
* [プロキシページ](/help/commerce/cif-classic/administering/concepts.md#proxy-pages)

>[!NOTE]
>
>標準のAEMインストールには、汎用AEM(JCR)e コマース実装が含まれます。
>
>これは、現在、デモ目的、または要件に応じたカスタム実装の基本的な基盤としての役割を果たすためのものです。

## 製品と製品のバリエーション {#products-and-product-variations}

>[!NOTE]
>
>以下の手順は、製品と製品バリエーションの両方に適用されます。

製品を作成する前に、 [足場](/help/sites-authoring/scaffolding.md). 製品の定義に必要なフィールドと、その編集方法を指定します。

基礎モードは、個々の製品タイプごとに必要です。 適切な基礎モードは、次のいずれかの方法で製品に関連付けられます。

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
>追加の設定を行わずに、任意の場所で新しい製品定義を作成できます。

### 製品の読み込み {#importing-products}

#### 製品の読み込み — タッチ操作向け UI {#importing-products-touch-optimized-ui}

1. **Commerce** から&#x200B;**製品**&#x200B;コンソールに移動します。
1. の使用 **製品** コンソールは必要な場所に移動します。
1. 以下を使用： **製品を読み込み** アイコンをクリックしてウィザードを開きます。

   ![製品を読み込みアイコン](/help/sites-administering/do-not-localize/chlimage_1-13.png)

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

1. 選択 **次へ** 製品をインポートするために、実行されたアクションのログが表示されます。

   >[!NOTE]
   >
   >製品は現在の場所に、または現在の場所を基準に読み込まれます。

   >[!NOTE]
   >
   >繰り返し **次へ** および **戻る** は製品定義を繰り返し読み込みます。 ただし、SKU が同じ場合は、リポジトリ内に存在する情報が上書きされるだけです。

1. 選択 **完了** をクリックしてウィザードを閉じます。

#### 製品の読み込み — クラシック UI {#importing-products-classic-ui}

1. の使用 **ツール** コンソールを開く **コマース** フォルダー。
1. ダブルクリックして、 **製品インポーター**:

   ![製品インポーターコンソール](/help/sites-administering/assets/chlimage_1-22.jpeg)

1. 以下を指定します。

   * **ストア名**

     製品は以下にインポートされます。

     `/etc/commerce/products/<*store name*>/`

   * **コマースプロバイダー**

     [コマースプロバイダー](/help/commerce/cif-classic/administering/concepts.md#commerce-providers)のインポーター（デフォルトでは Geometrixx）。

   * **ソースファイル**

     インポートするファイルのリポジトリ内の場所。

   * **増分読み込み**

     （完全インポートではなく）増分インポートかどうかを示します。

1. クリック **製品を読み込み**.

### 製品情報の作成 {#creating-product-information}

>[!NOTE]
>
>標準の商品管理は必要最小限です。Geometrixx-Outdoors の商品セットは、基本的なものだからです。複雑さは製品の[基礎モード](/help/sites-authoring/scaffolding.md)によるので、独自の製品基礎モードを使用すれば、より高度な編集が可能になります。

#### 製品情報の作成 — タッチ操作向け UI {#creating-product-information-touch-optimized-ui}

1. の使用 **製品** コンソール ( **コマース**) 必要な場所に移動します。
1. 以下を使用： **作成** アイコンをクリックして、次のいずれかを選択します（構造と場所に応じて異なります）。

   * **製品を作成**
   * **製品バリエーションを作成**

   ![プラス形の作成アイコン](/help/sites-administering/do-not-localize/chlimage_1-14.png)

1. ウィザードが表示されます。以下を使用： **基本** および **製品タブ** をクリックします。 [製品属性](/help/commerce/cif-classic/administering/concepts.md#product-attributes) 新しい製品または製品バリアントの場合。

   >[!NOTE]
   >
   >**タイトル** および **SKU** は、プロダクトまたはバリアントを作成するのに最低限必要な情報です。

1. 選択 **作成** をクリックして情報を保存します。

>[!NOTE]
>
>多くの製品は、様々な色やサイズで提供されています。 基本製品と関連製品バリアントに関する情報は、 **製品** コンソール。
>
>プロダクトとそのバリアントはツリー構造として保存され、プロダクト情報が上部に表示され、バリアントがその下に表示されます（この構造は UI によって適用されます）。

### 製品情報の編集 {#editing-product-information}

>[!NOTE]
>
>geometrixx-outdoors の製品画像は、次の場所から提供されます。
>
>`/etc/commerce/products/...`
>
>つまり、デフォルトでは、これらは [dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=ja)必要に応じてを設定します。

#### 製品情報の編集 — タッチ操作向け UI {#editing-product-information-touch-optimized-ui}

1. の使用 **製品** コンソール ( **コマース**) 製品情報に移動します。
1. 次のいずれかを使用します。

   * [クイックアクション](/help/sites-authoring/basic-handling.md#quick-actions)
   * [選択モード](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   **製品データを表示**&#x200B;アイコンを選択します。

   ![製品データを表示アイコン — 情報アイコン](/help/sites-administering/do-not-localize/chlimage_1-15.png)

1. [製品属性](/help/commerce/cif-classic/administering/concepts.md#product-attributes)が表示されます。「**編集**」と「**完了**」を使用して、変更があれば実行します。

### 製品参照の表示 {#showing-product-references}

#### 製品リファレンスの表示 — タッチ操作向け UI {#showing-product-references-touch-optimized-ui}

1. の使用 **製品** コンソール ( **コマース**) 製品情報に移動します。
1. 次のアイコンを使用して、参照のセカンダリレールを開きます。

   ![二重矢印アイコン](/help/sites-administering/do-not-localize/chlimage_1-16.png)

1. 必要な商品を選択します。セカンダリレールが更新され、使用可能な参照タイプが表示されます。

   ![参照を開いた状態の製品コンソール](/help/sites-administering/assets/chlimage_1-88.png)

1. 参照タイプ（「製品ページ」など）をクリックまたはタップして、リストを展開します。
1. 特定の参照を選択して、オプションを表示します。

   * 製品ページに移動
   * 製品ページを編集

   ![製品コンソールのリファレンスパネル](/help/sites-administering/assets/chlimage_1-89.png)

### 商品の検索 {#search-for-products}

1. **コマース**&#x200B;から&#x200B;**製品**&#x200B;コンソールに移動します。
1. 次のアイコンを使用して、検索のセカンダリレールを開きます。

   ![虫眼鏡アイコン](/help/sites-administering/do-not-localize/chlimage_1-17.png)

1. 製品の検索には、複数のファセットを使用できます。 1 回の検索に使用できるファセットは 1 つまたは複数のみです。 見つかった製品は次のように表示されます。

   ![製品コンソールの製品データ](/help/sites-administering/assets/chlimage_1-90.png)

1. 製品をクリックまたはタップすると、その製品が開きます。 また、公開したり、製品データを表示したりすることもできます。

#### 検索の拡張 {#extending-search}

CRXDE Lite:

1. 次の URL に移動します。

   `http://localhost:4502/crx/de/index.jsp#/libs/commerce/gui/content/products/aside/items/search/items/searchpanel/facets`

1. 例えば、商品の検索ページに表示するサイズを変更できます。`sizegroup` ノードをクリックします。
1. `items` ノードをクリックしてから、`propertypredicate` ノードをクリックします。
1. `propertyValues` を変更できます。例えば、XS または XXL を追加したり、サイズを削除したりできます。
1. 「**すべて保存**」をクリックして、商品の検索ページに移動します。変更が表示されます。

### 複数のアセット {#multiple-assets}

製品コンポーネントに複数のアセットを追加してから、製品ページに表示されるアセットを指定できます。

>[!NOTE]
>
>複数のアセットに関連する操作はすべて、タッチ操作向け UI を使用して実行されます。

#### 複数のアセットの追加 {#adding-multiple-assets}

1. **コマース**&#x200B;から&#x200B;**製品**&#x200B;コンソールに移動します。
1. **製品**&#x200B;コンソールを使用して、必要な商品に移動します。

   >[!NOTE]
   >
   >バリアントレベルではなく商品レベルに移動する必要があります。

1. 選択モードまたはクイックアクションを使用して、**製品データを表示**&#x200B;アイコンをタップまたはクリックします。
1. 「編集」アイコンをタップまたはクリックします。
1. スクロールして **追加**.

   ![製品データのスクリーンショットの追加](/help/sites-administering/assets/chlimage_1-91.png)

1. 「**追加**」をタップまたはクリックします。新しいアセットプレースホルダーが表示されます。
1. 「**変更**」をタップまたはクリックすると、アセットを選択できるダイアログが表示されます。
1. 追加するアセットを選択します。

   >[!NOTE]
   >
   >選択できるアセットは次の中から選択します。 [Assets](/help/assets/assets.md).

1. 「完了」アイコンをタップまたはクリックします。

これで、2 つのアセットが製品コンポーネントに保存されました。 製品ページに表示するものを設定できます。 これはカテゴリシステムで機能します。 最初に、個々のアセットにカテゴリを追加する必要があります。

1. 「**商品データを表示**」をタップまたはクリックします。
1. アセットの下の「**アセットカテゴリ**」に入力します（例：`cat1` および `cat2`）。

   >[!NOTE]
   >
   >カテゴリにはタグも使用できます。

1. 「完了」アイコンをタップまたはクリックします。 次は、 [ロールアウト](#rolling-out-a-catalog) 変更内容。

これで、製品コンポーネント内のアセットにカテゴリが追加されました。 次の 3 つの異なるレベルで表示するカテゴリを設定できます。

* [製品ページ](#product-page)
* [カタログ](#catalog)
* [製品コンソール](#products-console)

>[!NOTE]
>
>カテゴリを設定しない場合、最初のアセットが製品ページに表示されます。

表示する画像を選択するメカニズムを次に示します。

1. 製品ページのカテゴリが設定されているかどうかを確認します。
1. カタログがない場合は、カテゴリがカタログに設定されているかどうかを確認します。
1. 設定されていない場合、製品コンソール用にカテゴリが設定されているかどうかを確認します。

>[!NOTE]
>
>カタログレベルと製品コンソールレベルの両方で、変更を適用し、製品ページで違いを確認するには、変更をロールアウトする必要があります。

#### 製品ページ {#product-page}

1. 製品ページに移動します。
1. **編集** 製品コンポーネント。
1. 選択した&#x200B;**画像カテゴリ**&#x200B;を入力します（例：`cat1`）。
1. 「**完了**」をタップまたはクリックします。ページが更新され、正しいアセットが表示されます。

#### カタログ  {#catalog}

1. カタログに移動します。
1. タップまたはクリック **プロパティを表示**.
1. 「**編集**」をタップまたはクリックします。
1. 「**アセット**」タブをタップまたはクリックします。
1. 必要なを入力します **製品アセットカテゴリ**.
1. 「**完了**」をタップまたはクリックします。
1. [ロールアウト](#rolling-out-a-catalog) 変更内容。

#### 製品コンソール {#products-console}

1. **製品**&#x200B;コンソールを使用して、必要な商品に移動します。
1. 「**製品データを表示**」をタップまたはクリックします。
1. 「**編集**」をタップまたはクリックします。
1. タイプ a **デフォルトのアセットカテゴリ**.
1. 「**完了**」をタップまたはクリックします。
1. [ロールアウト](#rolling-out-a-catalog) 変更内容。

### 製品情報の公開/非公開 {#publishing-unpublishing-product-information}

#### 製品情報の公開/非公開 — タッチ操作向け UI {#publishing-unpublishing-product-information-touch-optimized-ui}

>[!NOTE]
>
>多くの場合、製品情報は、それを参照するページを通じて公開されます。 例えば、商品 Y を参照するページ X を公開する際に、AEMは、商品 Y も公開するかどうかを尋ねます。
>
>特殊なケースでは、AEM は、商品データからの直接の公開もサポートしています。

1. の使用 **製品** コンソール ( **コマース**) 製品情報に移動します。
1. 次のいずれかを使用します。

   * [クイックアクション](/help/sites-authoring/basic-handling.md#quick-actions)
   * [選択モード](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   必要に応じて&#x200B;**公開**&#x200B;アイコンまたは&#x200B;**非公開**&#x200B;アイコンを選択します。

   ![ワールドアイコン](/help/sites-administering/do-not-localize/chlimage_1-18.png) ![バツ印の付いたワールドアイコン — 記号なし](/help/sites-administering/do-not-localize/chlimage_1-19.png)

   それぞれに応じて商品情報が公開または非公開になります。

<!-- Search&Promote is end of life as of September 1, 2022 ### Product Feed {#product-feed} -->

<!-- Search&Promote is end of life as of September 1, 2022 The Search&Promote integration allows you to: -->

<!-- Search&Promote is end of life as of September 1, 2022 * use the eCommerce API, independently of the underlying repository structure and commerce platform. -->
<!-- Search&Promote is end of life as of September 1, 2022 * leverage the Index Connector feature of Search&Promote to provide a product feed in XML format. -->
<!-- Search&Promote is end of life as of September 1, 2022 * leverage the Remote Control feature of Search&Promote to perform on-demand or scheduled requests of the product feed -->
<!-- Search&Promote is end of life as of September 1, 2022 * feed generation for different Search&Promote accounts, configured as cloud services configurations. -->

<!-- Search&Promote is end of life as of September 1, 2022 For more information, read [Product Feed](/help/sites-administering/product-feed.md). -->

### 製品アップデートのイベントハンドラー {#event-handler-for-product-updates}

製品の追加、変更または削除時、および製品ページの追加、変更または削除時にイベントを記録するイベントハンドラーがあります。 次の OSGi イベントがあります。

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

買い物かごに追加リンクを含む画像コンポーネントを使用すると、画像上の商品にリンクされたホットスポットを作成することで、商品を買い物かごにすばやく追加できます。

ホットスポットをクリックすると、製品のサイズと数量を選択するためのダイアログが開きます。

1. コンポーネントを追加するページに移動します。
1. ページにコンポーネントをドラッグ&amp;ドロップします。
1. コンポーネント内の画像を [アセットブラウザー](/help/sites-authoring/author-environment-tools.md#assets-browser).
1. 次のいずれかを実行できます。

   * コンポーネントをクリックしたあと、編集アイコンをクリックする
   * ゆっくりダブルクリックする

1. 全画面表示アイコンをクリックします。

   ![全画面表示アイコン](/help/sites-administering/assets/chlimage_1-92.png)

1. ローンチマップアイコンをクリックします。

   ![マップを起動アイコン](/help/sites-administering/assets/chlimage_1-93.png)

1. 形状アイコンのいずれかをクリックします。

   ![シェイプアイコン](/help/sites-administering/do-not-localize/chlimage_1-21.png)

1. 必要に応じて形状を修正し、移動します。
1. 図形をクリックします。
1. 参照アイコンをクリックすると、 [アセットピッカー](/help/assets/search-assets.md#assetpicker).

   >[!NOTE]
   >
   >または、バリアントレベルではなく、製品レベルで使用する必要がある製品パスを直接入力できます。

   ![タイプパス](/help/sites-administering/assets/chlimage_1-94.png)

1. 確認アイコンを 2 回クリックし、「全画面を終了」をクリックします。
1. ページ上のコンポーネントの横の任意の場所をクリックします。 ページが更新され、画像に次の記号が表示されます。

   ![プラス記号](/help/sites-administering/do-not-localize/chlimage_1-22.png)

1. 切り替え先 [プレビュー](/help/sites-authoring/editing-content.md#previewingpagestouchoptimizedui) モード。
1. 「 + 」ホットスポットをクリックします。 「**パス**」に入力した商品のサイズと数量を選択できるダイアログが表示されます。

   ![製品の例：本調](/help/sites-administering/assets/chlimage_1-95.png)

1. サイズと数量を入力します。
1. 「カートに追加」ボタンをクリックします。 ダイアログが閉じます。
1. 買い物かごに移動します。 商品はここにあるはずです。

#### 設定オプション {#configuration-options}

ホットスポットをクリックしたときのダイアログの表示を設定できます。

1. コンポーネントをクリックし、設定アイコンをクリックします。

   ![設定アイコン](/help/sites-administering/assets/chlimage_1-96.png)

1. 下にスクロール. ここに **買い物かごに追加** タブをクリックします。

   ![「買い物かご」タブに追加](/help/sites-administering/assets/chlimage_1-97.png)

1. クリック **買い物かごに追加**. 3 つの設定オプションを使用できます。

   ![設定オプション](/help/sites-administering/assets/chlimage_1-98.png)

1. 「完了」アイコンをクリックします。

## カタログ {#catalogs}

### カタログの生成 {#generating-a-catalog}

#### カタログの生成 — タッチ操作向け UI {#generating-a-catalog-touch-optimized-ui}

>[!NOTE]
>
>カタログは、商品データを参照します。

カタログを生成するには：

1. サイトコンソール ( 例： [http://localhost:4502/sites.html/content](http://localhost:4502/sites.html/content)) をクリックします。
1. 新しいページを作成する場所に移動します。
1. オプションリストを開くには、**作成**&#x200B;アイコンを使用します。

   ![create-icon](/help/sites-administering/do-not-localize/chlimage_1-23.png)

1. リストから「**カタログを作成**」を選択すると、カタログを作成ウィザードが表示されます。

   ![カタログ作成ウィザード](/help/sites-administering/assets/chlimage_1-99.png)

1. 必要なカタログブループリントに移動します。
1. タップまたはクリック **選択** ボタンをクリックし、必要なカタログブループリントをタップまたはクリックします。
1. 「**次へ**」をタップまたはクリックします。

   ![カタログのプロパティウィザード](/help/sites-administering/assets/chlimage_1-100.png)

1. 「**タイトル**」と「**名前**」を入力します。
1. 次をタップまたはクリックします。 **作成** 」ボタンをクリックします。 カタログが作成され、ダイアログが開きます。

   ![カタログ作成ダイアログ](/help/sites-administering/assets/chlimage_1-101.png)

1. 「**完了**」ボタンをタップまたはクリックすると、サイトコンソールに戻り、カタログを表示することができます。

   「**カタログを開く**」ボタンをタップまたはクリックすると、カタログ（例：`http://localhost:4502/editor.html/content/test-catalog.html`）が開きます。

#### カタログの生成 - クラシック UI {#generating-a-catalog-classic-ui}

>[!NOTE]
>
>カタログは、 [製品データ](#products-and-product-variants).

1. の使用 **Web サイト** コンソールで、 **カタログブループリント**、「基本カタログ」の順に選択します。

   次に例を示します。

   `http://localhost:4502/siteadmin#/content/catalogs/geometrixx-outdoors/base-catalog`

1. **セクションのブループリント**&#x200B;テンプレートを使用して新規ページを作成します。

   （例：`Swimwear`）。

1. 新しい `Swimwear` ページを開いて「**ブループリントを編集**」をクリックすると、**プロパティ**&#x200B;ダイアログが表示されるので、**製品**&#x200B;の選択をセットアップできます。

   例えば、 **タグ/キーワード** フィールドで「アクティビティ」を選択し、「Geometrixx — アウトドア」セクションから「スイミング」を選択します。

1. クリック **OK** プロパティを保存するには、以下を実行します。製品の例は、 **製品選択条件** をブループリントページに追加します。
1. クリック **ロールアウトの変更…**&#x200B;を選択します。 **ページとすべてのサブページをロールアウト**&#x200B;を選択し、「 **次へ** その後 **ロールアウト**. ロールアウトが正常に完了すると、**ステータス**&#x200B;インジケーターが緑色で表示されます。
1. 「**閉じる**」をクリックして、次の場所およびその下にある新しいカタログセクションを確認します。

   `http://localhost:4502/cf#/content/geometrixx-outdoors/en/swimwear.html`

1. ブループリントページで再び「**ブループリントを編集**」をクリックし、**プロパティ**&#x200B;ダイアログで「**生成されたページ**」タブを開きます。バナーリストフィールドで、表示する画像を選択します（例：`summer.jpg`）。
1. クリック **OK** プロパティを保存するには、以下を実行します。バナー情報は、 **製品選択条件** をブループリントページに追加します。
1. これらの新しい変更をロールアウトします。

### カタログのロールアウト {#rolling-out-a-catalog}

#### カタログのロールアウト — タッチ操作向け UI {#rolling-out-a-catalog-touch-optimized-ui}

カタログをロールアウトするには：

1. **Commerce** を介して&#x200B;**カタログ**&#x200B;コンソールに移動します。
1. ロールアウトするカタログに移動します。
1. 次のいずれかを使用します。

   * [クイックアクション](/help/sites-authoring/basic-handling.md#quick-actions)
   * [選択モード](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   **ロールアウトの変更**&#x200B;アイコンを選択します。

   ![ロールアウト](/help/sites-administering/do-not-localize/chlimage_1-24.png)

1. ウィザードで、必要に応じてロールアウトを設定してから、「**ロールアウトの変更**」をタップまたはクリックします。
1. ダイアログが表示されます。処理が終了したら、「**完了**」をタップまたはクリックします。

#### カタログのロールアウト — クラシック UI {#rolling-out-a-catalog-classic-ui}

カタログをロールアウトするには：

1. ロールアウトするカタログに移動します。次に例を示します。

   `http://localhost:4502/cf#/content/catalogs/geometrixx-outdoors/base-catalog.html`

1. クリック **ロールアウトの変更…**
1. 必要に応じてロールアウトを設定します。
1. 「**ロールアウト**」をクリックします。

### ブループリントインポーター {#blueprint-importer}

#### ブループリントインポーター — タッチ操作向け UI {#blueprint-importer-touch-optimized-ui}

1. **Commerce** を介して&#x200B;**カタログ**&#x200B;コンソールに移動します。
1. カタログのブループリントを読み込む場所に移動します。
1. 次をタップまたはクリックします。 **ブループリントを読み込み** アイコン

   ![ブループリントを読み込みアイコン](/help/sites-administering/do-not-localize/chlimage_1-13.png)

1. ウィザードで、必要に応じて「ソース」を選択し、をタップまたはクリックします。 **次へ**.

   ![ブループリントウィザード](/help/sites-administering/assets/chlimage_1-102.png)

1. タップまたはクリック **完了** インポートが完了したら、

#### ブループリントインポーター — クラシック UI {#blueprint-importer-classic-ui}

1. **ツール**&#x200B;コンソールを使用して、**Commerce** に移動します。

   次に例を示します。

   `http://localhost:4502/miscadmin#/etc/commerce`

1. を開きます。 **カタログブルプリントインポータ**.
1. 必要に応じてインポートを設定します。
1. クリック **カタログブループリントを読み込み**.

## プロモーション {#promotions}

### プロモーションの作成 {#creating-a-promotion}

#### プロモーションの作成 — クラシック UI {#creating-a-promotion-classic-ui}

>[!NOTE]
>
>次の例では、 [campaign](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md)、割引券に使用されます。
>
>プロモーションは、 [エクスペリエンス](/help/sites-authoring/personalization.md) キャンペーン内で
>
>詳しくは、 [プロモーションと割引券](#promotions-and-vouchers).

1. を開きます。 **Web サイト** オーサーインスタンスのコンソール。
1. 左側のパネルで、必要なを選択します **Campaign**.
1. クリック **新規**&#x200B;を選択し、 **Promotion** テンプレートを作成して、 **タイトル** ( および **名前** 必要に応じて ) 新しい割引券に対して使用します。
1. 「**作成**」をクリックします。新しいプロモーションページが右側のパネルに表示されます。

1. 次のどちらかの方法で、**プロパティ**&#x200B;を編集します。

   * このページを開き、「編集」ボタンをクリックしてプロパティダイアログを表示する
   * Web サイトコンソールでページを選択し、コンテキストメニュー（通常はマウスの右ボタン）を使用して **プロパティ…** プロパティダイアログを開きます。

   次を指定： **プロモーションタイプ**, **割引タイプ**, **割引値** および必要に応じてその他のフィールド

1. 「**OK**」をクリックして保存します。

1. これで、プロモーションをアクティベートでき、買い物客がパブリッシュインスタンスでプロモーションを表示できるようになります。

## 割引券 {#vouchers}

### 割引券の作成 {#creating-a-voucher}

#### 割引券の作成 — クラシック UI {#creating-a-voucher-classic-ui}

1. を開きます。 **Web サイト** オーサーインスタンスのコンソール。
1. 左側のパネルで、必要なを選択します **Campaign**.
1. クリック **新規**&#x200B;を選択し、 **割引券** テンプレートを作成して、 **タイトル** ( および **名前** 必要に応じて ) 新しい割引券に対して使用します。
1. 「**作成**」をクリックします。新しい割引券ページが右側のパネルに表示されます。

1. ダブルクリックして新しい割引券ページを開き、「**編集**」をクリックして、必要に応じて情報を設定します。
1. 「**OK**」をクリックして保存します。

1. これで割引券をアクティブ化でき、買い物客がパブリッシュインスタンス上の買い物かごで利用できるようになりました。

### 割引券の削除 {#removing-vouchers}

#### 割引券の削除 — クラシック UI {#removing-vouchers-classic-ui}

割引券を顧客が利用できないようにするには、次のいずれかを実行します。

* 割引券を非アクティブ化します。オーサー環境で使用できる状態になるので、後で再度アクティブ化できます。
* 完全に削除します。

両方のアクションは、 **Web サイト** コンソール。

### 割引券の変更 {#modifying-vouchers}

#### 割引券の変更 — クラシック UI {#modifying-vouchers-classic-ui}

割引券またはプロモーションのプロパティを変更するには、 **Web サイト** コンソールとクリック **編集**. 保存後、変更がパブリッシュインスタンスにプッシュされるように、アクティブ化する必要があります。

### 買い物かごへの割引券の追加 {#adding-vouchers-to-a-cart}

ユーザーが買い物かごに割引券を追加できるようにするには、組み込みの **割引券** コンポーネント（コマースカテゴリ）。 買い物かごが表示されるページと同じページにこのを追加する必要があります（ただし必須ではありません）。 割引券コンポーネントは、ユーザーが割引券コードを入力できる単なる形式です。適用された割引券のリストとその割引を実際に表示する買い物かごコンポーネントです。

デモサイト (Geometrixx Outdoors — 英語 ) では、買い物かごページの実際の買い物かごの下に割引券フォームが表示されます。

## 注文 {#orders}

>[!NOTE]
>
>標準の AEM には、商品の返送、注文ステータスの更新、受け渡しの実行、納品書の生成など、注文に関連する標準機能に必要なアクションがないことを思い出してください。主な目的は技術のプレビューです。
>
>AEM の汎用の注文管理は基本的なものにとどまっています。ウィザードで使用可能なフィールドは、次の基礎モードによって異なります。
>`/etc/scaffolding/geometrixx-outdoors/order/jcr:content/cq:dialog`
>
>カスタマイズした基礎モードを作成する場合は、さらに注文情報を保存できます。

>[!NOTE]
>
>注文コンソールには、決して公開されないベンダーの注文情報が表示されます。
>
> 顧客の注文情報はそのホームディレクトリに保持され、顧客のアカウントの注文履歴で公開されます。この情報は、ホームディレクトリの他の部分と共に公開されます。

### 注文情報の作成 {#creating-order-information}

#### 注文情報の作成 — タッチ操作向け UI {#creating-order-information-touch-optimized-ui}

1. の使用 **注文** コンソールは必要な場所に移動します。
1. 以下を使用： **作成** 選択するアイコン **注文を作成**.

   ![プラス形の作成アイコン](/help/sites-administering/do-not-localize/chlimage_1-14.png)

1. ウィザードが表示されます。「**基本**」、「**コンテンツ**」、「**支払い**」および「**受け渡し**」タブを使用して、[新しい注文に関する情報](/help/commerce/cif-classic/administering/concepts.md#order-information)を入力します。

1. 選択 **作成** をクリックして情報を保存します。

### 注文情報の編集 {#editing-order-information}

#### 注文情報の編集 — タッチ操作向け UI {#editing-order-information-touch-optimized-ui}

1. の使用 **注文** コンソールで順序に移動します。
1. 次のいずれかを使用します。

   * [クイックアクション](/help/sites-authoring/basic-handling.md#quick-actions)
   * [選択モード](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   **注文データを表示**&#x200B;アイコンを選択します。

   ![情報アイコン](/help/sites-administering/do-not-localize/chlimage_1-15.png)

1. [注文情報](/help/commerce/cif-classic/administering/concepts.md#order-information)が表示されます。「**編集**」と「**完了**」を使用して、変更があれば実行します。

