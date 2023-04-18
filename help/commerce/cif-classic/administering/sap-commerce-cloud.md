---
title: AEM with SAPCommerce Cloud
description: AEMと SAPCommerce Cloudの使用方法を説明します。
uuid: cee1a781-fcba-461e-a0a4-c561a1dbcbf3
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
exl-id: c342f789-2ff7-4802-99c7-c3699218fe47
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '1717'
ht-degree: 67%

---

# SAP Commerce Cloud {#sap-commerce-cloud}

インストール後、インスタンスを設定できます。

1. [ファセット検索のGeometrixx Outdoors](#configure-the-facetted-search-for-geometrixx-outdoors).
1. [カタログバージョンを設定します](#configure-the-catalog-version)。
1. [インポート構造の設定](#configure-the-import-structure).
1. [読み込む製品属性の設定](#configure-the-product-attributes-to-load).
1. [製品データのインポート](#importing-the-product-data).
1. [カタログインポーターを設定します](#configure-the-catalog-importer)。
1. 以下を使用： [インポーターを使用してカタログを読み込みます](#catalog-import) をAEMの特定の場所に追加します。

## ファセット検索のGeometrixx Outdoors {#configure-the-facetted-search-for-geometrixx-outdoors}

>[!NOTE]
>
>hybris 5.3.0.1 以降では、この設定は必要ありません。

1. ブラウザーで次の URL にアクセスし、**Hybris 管理コンソール**&#x200B;に移動します。

   [http://localhost:9001/hmc/hybris](http://localhost:9001/hmc/hybris)

1. サイドバーで、 **システム**&#x200B;を、 **ファセット検索**&#x200B;を、 **ファセット検索設定**.
1. **Sample Solr Configuration for clothescatalog** 用に&#x200B;**エディターを開きます**。

1. 「**Catalog versions**」の下の「**Add Catalog version**」を使用して、リストに `outdoors-Staged` と `outdoors-Online` を追加します。
1. **設定を保存します。**
1. 「**SOLR Item types**」を開き、次の **SOLR Sort** を `ClothesVariantProduct` に追加します。

   * relevance (&quot;Relevance&quot;, score)
   * name-asc (&quot;Name (ascending)&quot;, name)
   * name-desc (&quot;Name (descending)&quot;, name)
   * price-asc (&quot;Price (ascending)&quot;, priceValue)
   * price-desc (&quot;Price (descending)&quot;, priceValue)

   >[!NOTE]
   >
   >コンテキストメニュー（通常は右ボタンをクリック）を使用して、「`Create Solr sort`」を選択します。
   >
   >Hybris 5.0.0 の場合は、「`Indexed Types`」タブを開き、「`ClothesVariantProduct`」をダブルクリックして「`SOLR Sort`」タブを開きます。

   ![chlimage_1-36](/help/sites-administering/assets/chlimage_1-36a.png)

1. 「**Indexed Types**」タブで、「**Composed Type**」を次のように設定します。

   `Product - Product`

1. 「**Indexed Types**」タブで、「`full`」の「**Indexer queries**」を次のように変更します。

   ```shell
   SELECT {pk} FROM {Product} WHERE {pk} NOT IN ({{SELECT {baseProductpk} FROM {variantproduct}}})
   ```

1. 「**Indexed Types**」タブで、「`incremental`」の「**Indexer queries**」を次のように変更します。

   ```shell
   SELECT {pk} FROM {Product} WHERE {pk} NOT IN ({{SELECT {baseProductpk} FROM {variantproduct}}}) AND {modifiedtime} <= ?lastIndexTime
   ```

1. 「**Indexed Types**」タブで、`category` ファセットを変更します。カテゴリリストの最後のエントリをダブルクリックすると、「**Indexed property**」タブが表示されます。

   >[!NOTE]
   >
   >hybris 5.2 の場合は、「Properties」テーブルの `Facet` 属性が以下のスクリーンショットに従って選択されていることを確認します。

   ![chlimage_1-37](/help/sites-administering/assets/chlimage_1-37a.png) ![chlimage_1-38](/help/sites-administering/assets/chlimage_1-38a.png)

1. 「**Facet Settings**」タブを開き、フィールドの値を変更します。

   ![chlimage_1-39](/help/sites-administering/assets/chlimage_1-39a.png)

1. 変更内容を&#x200B;**保存**&#x200B;します。
1. 再び「**SOLR Item types**」から、以下のスクリーンショットに従って、`price` ファセットを変更します。`category` と同様に、`price` をダブルクリックすると、「**Indexed property**」タブが表示されます。

   ![chlimage_1-40](/help/sites-administering/assets/chlimage_1-40a.png)

1. 「**Facet Settings**」タブを開き、フィールドの値を変更します。

   ![chlimage_1-41](/help/sites-administering/assets/chlimage_1-41a.png)

1. 変更内容を&#x200B;**保存**&#x200B;します。
1. 開く **システム**, **ファセット検索**&#x200B;を、 **インデクサー操作ウィザード**. cron ジョブを開始します。

   * **インデクサー操作**：`full` 
   * **Solr 設定**：`Sample Solr Config for Clothes`

## カタログバージョンの設定 {#configure-the-catalog-version}

読み込まれた&#x200B;**カタログバージョン**（`hybris.catalog.version`）を OSGi サービス用に設定できます。

**Day CQ Commerce Hybris 設定**
（`com.adobe.cq.commerce.hybris.common.DefaultHybrisConfigurationService`）

通常、**カタログバージョン**&#x200B;は、`Online` または `Staged`（デフォルト）に設定されます。 

>[!NOTE]
>
>AEM と連携する場合は、いくつかの方法でこのようなサービスの設定を管理できます。詳しくは、[OSGi の設定](/help/sites-deploying/configuring-osgi.md)を参照してください。設定可能なパラメーターとそのデフォルト値の詳細については、コンソールも参照してください。

ログ出力は、作成したページやコンポーネントに関するフィードバックを提供し、潜在的なエラーを報告します。

## インポート構造の設定 {#configure-the-import-structure}

次のリストは、デフォルトで作成される（アセット、ページ、コンポーネントの）サンプル構造を示しています。

```shell
+ /content/dam/path/to/images
  + 12345.jpg (dam:Asset)
    + ...
  + ...
+ /content/site/en
  - cq:commerceProvider = "hybris"
  - cq:hybrisBaseStore = "basestore"
  - cq:hybrisCatalogId = "catalog"
  + category1 (cq:Page)
    + jcr:content (cq:PageContent)
      - jcr:title = "Category 1"
    + category11 (cq:Page)
      + jcr:content (cq:PageContent)
        - jcr:title = "Category 1.1"
      + 12345 (cq:Page)
        + jcr:content (cq:PageContent)
          + par
            + product (nt:unstructured)
              - cq:hybrisProductId = "12345"
              - sling:resourceType = "commerce/components/product"
              + image (nt:unstructured)
                - sling:resourceType = "commerce/components/product/image"
                - fileReference = "/content/dam/path/to/images/12345.jpg"
              + 12345.1-S (nt:unstructured)
                - cq:hybrisProductId = "12345.1-S"
                - sling:resourceType = "commerce/components/product"
                + image (nt:unstructured)
                  - sling:resourceType = "commerce/components/product/image"
                  - fileReference = "/content/dam/path/to/images/12345.1-S.jpg"
              + ...
```

`DefaultImportHandler` インターフェイスを実装する OSGi サービス `ImportHandler` によって、このような構造が作成されます。商品、商品バリエーション、カテゴリ、アセットなどを作成するために、実際のインポーターによって読み込みハンドラーが呼び出されます。

>[!NOTE]
>
>以下が可能です。 [独自の読み込みハンドラを実装して、このプロセスをカスタマイズします。](#configure-the-import-structure).

インポート時に生成される構造は、次の目的で設定できます。

``**Day CQ Commerce Hybris デフォルトインポートハンドラー**
`(com.adobe.cq.commerce.hybris.importer.DefaultImportHandler`)

AEM と連携する場合は、いくつかの方法でこのようなサービスの設定を管理できます。詳しくは、[OSGi の設定](/help/sites-deploying/configuring-osgi.md)を参照してください。設定可能なパラメーターとそのデフォルト値の詳細については、コンソールも参照してください。

## 読み込む製品属性の設定 {#configure-the-product-attributes-to-load}

応答パーサーは、（バリアント）製品に対して読み込むプロパティと属性を定義するように設定できます。

1. OSGi バンドルを設定します。

   **Day CQ Commerce Hybris デフォルト応答パーサー**
（`com.adobe.cq.commerce.hybris.impl.importer.DefaultResponseParser`）

   ここで、読み込みとマップに必要な、様々なオプションと属性を定義できます。

   >[!NOTE]
   >
   >AEM と連携する場合は、いくつかの方法でこのようなサービスの設定を管理できます。詳しくは、[OSGi の設定](/help/sites-deploying/configuring-osgi.md)を参照してください。設定可能なパラメーターとそのデフォルト値の詳細については、コンソールも参照してください。

## 製品データのインポート {#importing-the-product-data}

製品データを読み込むには、様々な方法があります。 製品データは、環境の初期設定時に、または hybris データに変更が加えられた後に、読み込むことができます。

* [完全読み込み](#full-import)
* [増分読み込み](#incremental-import)
* [高速更新](#express-update)

hybris から読み込まれた実際の商品情報は、次の場所にあるリポジトリに保持されます。

`/etc/commerce/products`

次のプロパティは、hybris とのリンクを示します。

* `commerceProvider`
* `cq:hybrisCatalogId`
* `cq:hybrisProductID`

>[!NOTE]
>
>hybris 実装（`geometrixx-outdoors/en_US`）は、商品 ID と他の基本的な情報のみを `/etc/commerce` の配下に保存します。
>
>hybris サーバーは、製品に関する情報が要求されるたびに参照されます。

### 完全読み込み {#full-import}

1. 必要に応じて、既存の製品データをすべて削除します (CRXDE Lite)。

   1. 商品データを保持するサブツリーに移動します。

      `/etc/commerce/products`

      次に例を示します。

      [`http://localhost:4502/crx/de/index.jsp#/etc/commerce/products`](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

   1. 商品データを保持しているノード（例：`outdoors`）を削除します。
   1. 「**すべて保存**」をクリックして、変更内容を保存します。

1. AEM で hybris インポーターを開きます。

   `/etc/importers/hybris.html`

   次に例を示します。

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. 必要なパラメーターを設定します。例：

   ![chlimage_1-42](/help/sites-administering/assets/chlimage_1-42a.png)

1. 「**Import Catalog**」をクリックして読み込みを開始します。

   完了したら、次の URL で読み込んだデータを検証できます。

   ```
       /etc/commerce/products/outdoors
   ```

   これは CRXDE Lite で開くことができます。次に例を示します。      

   `[http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)`

### 増分読み込み {#incremental-import}

1. AEMで保持されている関連製品の情報を、次の場所にある適切なサブツリーで確認します。

   `/etc/commerce/products`

   これは CRXDE Lite で開くことができます。次に例を示します。      

   [http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

1. hybris で、関連商品に関して保持している情報を更新します。

1. AEM で hybris インポーターを開きます。

   `/etc/importers/hybris.html`

   次に例を示します。

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. 「**増分読み込み**」チェックボックスを選択します。
1. 「**カタログをインポート**」をクリックして読み込みを開始します。

   完了したら、AEM で更新されたデータを次の場所で確認できます。

   ```
       /etc/commerce/products
   ```


### 高速更新 {#express-update}

読み込み処理には長い時間がかかることがあるので、商品同期の拡張として、カタログの特定の領域を選択して手動で呼び出される高速更新を実行できます。書き出しフィードと標準属性設定を使用します。

1. AEMで保持されている関連製品の情報を、次の場所にある適切なサブツリーで確認します。

   `/etc/commerce/products`

   これは CRXDE Lite で開くことができます。次に例を示します。      

   [http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

1. hybris で、関連商品に関して保持している情報を更新します。

1. hybris で、商品を Express Queue に追加します。次に例を示します。

   ![chlimage_1-43](/help/sites-administering/assets/chlimage_1-43a.png)

1. AEM で hybris インポーターを開きます。

   `/etc/importers/hybris.html`

   次に例を示します。

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. クリックボックスを選択 **高速更新**.
1. 「**カタログをインポート**」をクリックして読み込みを開始します。

   完了したら、AEM で更新されたデータを次の場所で確認できます。

   ```
       /etc/commerce/products
   ```

## カタログインポーターの設定 {#configure-the-catalog-importer}

hybris カタログは、hybris カタログ、カテゴリおよび商品用のバッチインポーターを使用して AEM に読み込むことができます。

インポーターが使用するパラメーターは、以下に合わせて設定できます。

**Day CQ Commerce Hybris カタログインポーター**
（`com.adobe.cq.commerce.hybris.impl.importer.DefaultHybrisImporter`）

AEM と連携する場合は、いくつかの方法でこのようなサービスの設定を管理できます。詳しくは、[OSGi の設定](/help/sites-deploying/configuring-osgi.md)を参照してください。設定可能なパラメーターとそのデフォルト値の詳細については、コンソールも参照してください。

## カタログの読み込み {#catalog-import}

hybris パッケージには、初期ページ構造を設定するためのカタログインポーターが付属しています。

次の場所から利用できます。

`http://localhost:4502/etc/importers/hybris.html`

![ecommerceimportconsole](/help/sites-administering/assets/ecommerceimportconsole.png)

以下の情報を指定する必要があります。

* **基本ストア** hybris で設定された基本ストアの識別子。

* **カタログ** 読み込むカタログの識別子。

* **ルートパス** カタログを読み込むパス。

## カタログからの商品の削除 {#removing-a-product-from-the-catalog}

カタログから 1 つ以上の製品を削除するには：

1. [OSGi サービス用にを設定する](/help/sites-deploying/configuring-osgi.md) **Day CQ Commerce Hybris カタログインポーター**;関連項目 [カタログインポーターの設定](#configure-the-catalog-importer).

   次のプロパティをアクティブにします。

   * **製品の削除を有効にする**
   * **製品アセットの削除を有効にする**

   >[!NOTE]
   >
   >AEM と連携する場合は、いくつかの方法でこのようなサービスの設定を管理できます。詳しくは、[OSGi の設定](/help/sites-deploying/configuring-osgi.md)を参照してください。設定可能なパラメーターとそのデフォルト値の詳細については、コンソールも参照してください。

1. 増分更新を 2 回実行して、インポーターを初期化します（[カタログの読み込み](#catalog-import)を参照）。

   * 1 回目の実行では、変更された商品セットがログリストに表示されます。
   * 2 回目は、製品を更新する必要はありません。

   >[!NOTE]
   >
   >1 つ目のインポートは、製品情報を初期化することです。 2 つ目のインポートでは、すべてが正常に動作し、製品セットが準備できていることを確認します。

1. 削除する製品を含むカテゴリページを確認します。 製品の詳細が表示されます。

   例えば、次のカテゴリは Cajamara 製品の詳細を表示します。

   [http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html](http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html)

1. hybris コンソールで製品を削除します。 「**Change approval status**」オプションを使用して、ステータスを「`unapproved`」に設定します。製品がライブフィードから削除されます。

   次に例を示します。

   * [http://localhost:9001/productcockpit](http://localhost:9001/productcockpit) ページを開きます。
   * カタログ `Outdoors Staged` を選択します
   * `Cajamara` を検索します
   * この商品を選択し、承認ステータスを「`unapproved`」に変更します。

1. 別の増分更新を実行します ( [カタログの読み込み](#catalog-import)) をクリックします。 ログには、削除された製品のリストが表示されます。
1. [ロールアウト](/help/commerce/cif-classic/administering/generic.md#rolling-out-a-catalog) 適切なカタログ 製品ページと製品ページは、AEM内から削除されます。

   次に例を示します。

   * 次を開きます：:

      [http://localhost:4502/aem/catalogs.html/content/catalogs/geometrixx-outdoors-hybris](http://localhost:4502/aem/catalogs.html/content/catalogs/geometrixx-outdoors-hybris)

   * `Hybris Base` カタログをロールアウトします
   * 次を開きます：:

      [http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html](http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html)

   * `Cajamara` 商品が `Bike` カテゴリから削除されました

1. 商品を元に戻すには：

   1. hybris で、承認ステータスを「**approved**」に戻します。
   1. AEM内：

      1. 増分更新を実行する
      1. 該当するカタログを再度ロールアウトします。
      1. 適切なカテゴリページを更新します

## ClientContext への注文履歴特性の追加 {#add-order-history-trait-to-the-client-context}

注文履歴を [ClientContext](/help/sites-developing/client-context.md) に追加するには：

1. 次のどちらかの方法で、[ClientContext のデザインページ](/help/sites-administering/client-context.md)を開きます。

   * 編集するページを開いてから、**Ctrl + Alt + C** キー（Windows）または **control + option + C** キー（Mac）を使用してクライアントコンテキストを開きます。ClientContext の左上隅にある鉛筆アイコンを使用して、**ClientContext のデザインページを開きます**。
   * [http://localhost:4502/etc/clientcontext/default/content.html](http://localhost:4502/etc/clientcontext/default/content.html) に直接移動します。

1. [を **注文履歴** コンポーネント](/help/sites-administering/client-context.md#adding-a-property-component) から **買い物かご** ClientContext の t コンポーネント。
1. ClientContext に注文履歴の詳細が表示されていることを確認できます。 次に例を示します。

   1. を開きます。 [クライアントコンテキスト](/help/sites-administering/client-context.md).
   1. 買い物かごに項目を追加します。
   1. チェックアウトを完了します。
   1. ClientContext を確認します。
   1. 別の項目を買い物かごに追加します。
   1. チェックアウトページに移動します。

      * ClientContext に注文履歴の概要が表示されます。
      * 「以前買い物されたお客様です」というメッセージが表示されます。

   >[!NOTE]
   >
   >このメッセージは、次の方法で実現されています。
   >
   >* [http://localhost:4502/content/campaigns/geometrixx-outdoors/hybris-returning-customer.html](http://localhost:4502/content/campaigns/geometrixx-outdoors/hybris-returning-customer.html) に移動します。
   >
   >  キャンペーンは 1 つのエクスペリエンスで構成されます。
   >
   >* セグメント（[http://localhost:4502/etc/segmentation/geometrixx-outdoors/returning-customer.html](http://localhost:4502/etc/segmentation/geometrixx-outdoors/returning-customer.html)）をクリックします。
   >
   >* **注文履歴プロパティ**&#x200B;特性を使用してセグメントが作成されます。

