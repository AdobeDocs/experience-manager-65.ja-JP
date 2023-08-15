---
title: SAP Commerce Cloud を使用した開発
description: SAP Commerce Cloud 統合フレームワークには、API を備えた統合レイヤーが含まれています。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
exl-id: b3de1a4a-f334-44bd-addc-463433204c99
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '2296'
ht-degree: 35%

---

# SAP Commerce Cloud を使用した開発 {#developing-with-sap-commerce-cloud}

>[!NOTE]
>
>e コマースフレームワークは、任意の e コマースソリューションで使用できます。ここで扱う特定および例は、 [hybris](https://www.sap.com/products/crm.html) 解決策。

統合フレームワークには、API を備えた統合レイヤーが含まれています。次の操作が可能です。

* e コマースシステムをプラグインして、製品データを AEM に取り込む

* 特定の e コマースエンジンに依存しないコマース機能を提供する AEM コンポーネントを作成する

![chlimage_1-11](/help/sites-developing/assets/chlimage_1-11a.png)

>[!NOTE]
>
>[API に関するドキュメント](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation)もお読みください。

統合レイヤーを使用するための、標準搭載のAEMコンポーネントがいくつか用意されています。 現在、次のものがあります。

* 製品表示コンポーネント
* 買い物かご
* チェックアウト

検索の場合、AEM検索、e コマースシステムの検索、サードパーティ検索またはその組み合わせを使用できる統合フックが提供されます。

## e コマースエンジンの選択 {#ecommerce-engine-selection}

e コマースフレームワークは、任意の e コマースソリューションと共に使用できます。使用するエンジンは、AEMによって識別可能である必要があります。

* e コマースエンジンは、`CommerceService` インターフェイスをサポートする OSGi サービスです。

   * エンジンは、`commerceProvider` サービスプロパティによって区別できます。

* AEM では、`CommerceService` と `Product` に対して `Resource.adaptTo()` をサポートしています。

   * `adaptTo` 実装は、リソースの階層内で `cq:commerceProvider` プロパティを探します。

      * 見つかった場合、値は、コマースサービス参照のフィルターに使用されます。

      * 見つからない場合は、最上位のコマースサービスが使用されます。

   * A `cq:Commerce` mixin が使用され、 `cq:commerceProvider` は、厳密に型指定されたリソースに追加できます。

* 適切なコマースファクトリ定義を参照するために、`cq:commerceProvider` プロパティも使用されます。

   * 例えば、 `cq:commerceProvider` プロパティに値を指定 `hybris` は、の OSGi 設定と相関関係にあります。 **Day CQ Commerce Factory for Hybris** (com.adobe.cq.commerce.hybris.impl.HybrisServiceFactory) — パラメーター `commerceProvider` には値もあります `hybris`.

   * ここで、**カタログバージョン**&#x200B;など、さらに別のプロパティを設定できます（適切かつ使用可能な場合）。

以下の例を参照してください。

| `cq:commerceProvider = geometrixx` | 標準のAEMインストールでは、特定の実装が必要です。例えば、汎用 API への最小限の拡張を含むGeometrixx例の場合、 |
|--- |--- |
| `cq:commerceProvider = hybris` | hybris 実装 |

### 例 {#example}

```shell
/content/store
+ cq:commerceProvider = hybris
  + mens
    + polo-shirt-1
    + polo-shirt-2
    + employee
+ cq:commerceProvider = jcr
  + adobe-logo-shirt
    + cq:commerceType = product
    + price = 12.50
  + adobe-logo-shirt_S
    + cq:commerceType = variant
    + size = S
  + adobe-logo-shirt_XL
    + cq:commerceType = variant
    + size = XL
    + price = 14.50
```

>[!NOTE]
>
>CRXDE Liteを使用すると、hybris 実装の製品コンポーネントでの処理方法を確認できます。
>
>`/apps/geometrixx-outdoors/components/hybris/product/product.jsp`

### hybris 4 向けの開発 {#developing-for-hybris}

e コマース統合フレームワークの Hybris 拡張が更新されて、Hybris 4 との下位互換性を保ちながら、Hybris 5 がサポートされるようになりました。

コード内のデフォルト設定は、Hybris 5 向けに調整されています。

Hybris 4 向けの開発には、以下が必要です。

* Maven を呼び出す場合は、次のコマンドライン引数をコマンドに追加します。

  `-P hybris4`

  事前設定済みの Hybris 4 ディストリビューションをダウンロードして、バンドル `cq-commerce-hybris-server` に組み込みます。

* OSGi 設定マネージャーで、

   * Default Response Parser サービスの Hybris 5 サポートを無効にします。

   * Hybris Basic Authentication Handler サービスのサービスランクが Hybris OAuth Handler サービスよりも低いことを確認します。

### セッション処理 {#session-handling}

hybris は、ユーザーセッションを使用して、顧客の買い物かごなどの情報を保存します。 セッション ID は、hybris から `JSESSIONID` hybris への以降のリクエスト時に送信する必要がある cookie。 セッション ID をリポジトリに保存しないように、セッション ID は買い物客のブラウザーに保存される別の cookie にエンコードされます。 次の手順を実行します。

* 最初のリクエストでは、買い物客のリクエストに Cookie が設定されていないので、セッションを作成するリクエストが hybris インスタンスに送信されます。

* その応答からセッション cookie が抽出され、新しい cookie 内でエンコードされ（例えば `hybris-session-rest`）、買い物客への応答に設定されます。元の cookie は特定のパスに対してのみ有効で、それ以外の場合は後続のリクエストでブラウザーから返送されないので、新しい cookie でのエンコードが必要です。 また、パス情報を Cookie の値に追加する必要があります。

* 以降のリクエストでは、これらの Cookie が `hybris-session-<*xxx*>` Cookie からデコードされ、hybris のデータを要求するための HTTP クライアントに設定されます。

>[!NOTE]
>
>元のセッションが無効になったときに、新しい匿名セッションが作成されます。

#### CommerceSession {#commercesession}

* このセッションは、 **買い物かご**&#x200B;を「所有」しています

   * 追加や削除などを実行します。

   * 買い物かごについての様々な計算を実行します。

     `commerceSession.getProductPrice(Product product)`

* *注文*&#x200B;データの保存場所を管理します&#x200B;**。**

  `CommerceSession.getUserContext()`

* また、 **支払い** 処理接続

* また、 **達成** 接続

### 製品の同期と公開 {#product-synchronization-and-publishing}

hybris で管理される製品データは、AEMで使用できる必要があります。 次のメカニズムが実装されました。

* ID の最初の読み込みは、hybris によってフィードとして提供されます。 このフィードは更新される可能性があります。
* hybris は、(AEMがポーリングする ) フィードを介して更新情報を提供します。
* AEMが製品データを使用している場合、現在のデータのリクエストを hybris に返します（最終変更日を使用した条件付き取得リクエスト）。
* Hybris 上では、宣言的な方法でフィードコンテンツを指定できます。
* フィード構造とAEMコンテンツモデルのマッピングは、AEM側のフィードアダプターでおこなわれます。

![chlimage_1-12](/help/sites-developing/assets/chlimage_1-12a.png)

* インポーター (b) は、カタログ用のAEMのページツリー構造の初期設定に使用されます。
* hybris でのカタログの変更は、フィードを介してAEMに示され、その後AEMに反映されます (b)

   * カタログバージョンに関する製品の追加/削除/変更。

   * 製品が承認されました。

* hybris 拡張機能は、ポーリングインポーター（「hybris」スキーム）を提供します。このインポーターは、指定した間隔（例えば、24 時間ごとに間隔が秒単位で指定される）でAEMに変更をインポートするように設定できます。

  ```JavaScript
      http://localhost:4502/content/geometrixx-outdoors/en_US/jcr:content.json
       {
       * "jcr:mixinTypes": ["cq:PollConfig"],
       * "enabled": true,
       * "source": "hybris:outdoors",
       * "jcr:primaryType": "cq:PageContent",
       * "interval": 86400
       }
  ```

* AEM のカタログ構成は、**ステージング済み**&#x200B;カタログバージョンと&#x200B;**オンライン**&#x200B;カタログバージョンを認識します。

* カタログバージョン間で製品を同期するには、対応するAEMページ (a、c) のアクティベートまたはアクティベート解除が必要です

   * 製品の **オンライン** カタログバージョンでは、製品のページをアクティベートする必要があります。

   * 製品を削除するには、アクティベートを解除する必要があります。

* AEMでページをアクティベートする場合 (c) にはチェック (b) が必要で、次の場合にのみ可能です。

   * 製品が、製品ページの&#x200B;**オンライン**&#x200B;カタログバージョン内にある

   * 参照元の製品は、 **オンライン** 他のページ（キャンペーンページなど）のカタログバージョン。

* アクティベートされた製品ページは、製品データにアクセスする必要があります **オンライン** バージョン (d)。

* AEMパブリッシュインスタンスは、製品とパーソナライズされたデータ (d) を取得するために、hybris へのアクセス権が必要です。

### アーキテクチャ {#architecture}

#### 製品とバリアントのアーキテクチャ {#architecture-of-product-and-variants}

1 つの製品に複数のバリエーションを含めることができます。例えば、色やサイズによって異なる場合があります。 製品は、バリエーションを駆動するプロパティを定義する必要があります。Adobe用語は次のとおりです。 *バリアント軸*.

ただし、すべてのプロパティがバリアント軸であるわけではありません。 バリエーションは他のプロパティにも影響を与えます。例えば、価格はサイズに依存する場合があります。 買い物客はこれらのプロパティを選択できないので、バリアント軸とは見なされません。

各製品やバリアントはリソースで表されるので、1:1 がリポジトリノードにマッピングされます。 特定の製品やバリアントをそのパスで一意に識別できるのも当然です。

製品/バリアントリソースには、必ずしも実際の製品データが含まれるとは限りません。 これは、別のシステム（hybris など）で保持されているデータの表現の場合があります。 例えば、製品の説明や価格などは、AEMには格納されず、e コマースエンジンからリアルタイムで取得されます。

すべての製品リソースは、`Product API` で表現できます。製品 API のほとんどの呼び出しはバリエーション固有です（バリエーションは親から共有値を継承する場合がありますが）が、バリエーションのセットをリストする呼び出しもあります ( `getVariantAxes()`, `getVariants()`など )。

>[!NOTE]
>
>実際には、バリアント軸は、 `Product.getVariantAxes()` 戻り値：
>* hybris は hybris 実装用に定義します。
>
>（一般的に）製品には多数のバリアント軸を持たせることができますが、デフォルトの製品コンポーネントでは次の 2 つのバリアント軸のみが処理されます。
>
>1. `size`
>
>1. さらにもう 1 つ
>
>この追加バリアントは、製品リファレンスの `variationAxis` プロパティ（Geometrixx Outdoors の場合、通常は `color`）を使用して選択されます。

#### 製品の参照と製品データ {#product-references-and-product-data}

一般に、製品データは、 `/etc`、および製品の参照は、 `/content`.

製品バリエーションと製品データノードの間には 1 対 1 のマッピングが必要です。

製品リファレンスには、各バリエーションを表すノードも必要ですが、すべてのバリエーションを表す必要はありません。例えば、製品に S、M、L のバリエーションがある場合、製品データは次のようになります。

```shell
etc
|──commerce
|  |──products
|     |──shirt
|       |──shirt-s
|       |──shirt-m
|       |──shirt-l
```

「Big and Tall」カタログには次のバリエーションだけが含まれます。

```shell
content
|──big-and-tall
|  |──shirt
|     |──shirt-l
```

最後に、製品データを使用するための要件はありません。すべての製品データをカタログ内のリファレンスの配下に配置できますが、実際には、すべての製品データを複製せずに複数のカタログを用意することはできません。

**API**

#### com.adobe.cq.commerce.api.Product インターフェイス {#com-adobe-cq-commerce-api-product-interface}

```java
public interface Product extends Adaptable {

    public String getPath();            // path to specific variation
    public String getPagePath();        // path to presentation page for all variations
    public String getSKU();             // unique ID of specific variation

    public String getTitle();           // shortcut to getProperty(TITLE)
    public String getDescription();     // shortcut to getProperty(DESCRIPTION)
    public String getImageUrl();        // shortcut to getProperty(IMAGE_URL)
    public String getThumbnailUrl();    // shortcut to getProperty(THUMBNAIL_URL)

    public <T> T getProperty(String name, Class<T> type);

    public Iterator<String> getVariantAxes();
    public boolean axisIsVariant(String axis);
    public Iterator<Product> getVariants(VariantFilter filter) throws CommerceException;
}
```

#### com.adobe.cq.commerce.api.VariantFilter  {#com-adobe-cq-commerce-api-variantfilter}

```java
/**
 * Interface for filtering variants and AxisFilter provided as common implementation
 *
 * The <code>VariantFilter</code> is used to filter variants,
 * for example, when using {@link Product#getVariants(VariantFilter filter)}.
 */
public interface VariantFilter {
    public boolean includes(Product product);
}

/**
 * A {@link VariantFilter} for filtering variants by the given
 * axis and value. The following example returns a list of
 * variant products that have a value of <i>blue</i> on the
 * <i>color</i> axis.
 *
 * <p>
 * <code>product.getVariants(new AxisFilter("color", "blue"));</code>
 */
public class AxisFilter implements VariantFilter {

    private String axis;
    private String value;

    public AxisFilter(String axis, String value) {
        this.axis = axis;
        this.value = value;
    }

    /**
     * {@inheritDoc}
     */
    public boolean includes(Product product) {
        ValueMap values = product.adaptTo(ValueMap.class);

        if(values != null) {
            String v = values.get(axis, String.class);

            return v != null && v == value;
        }

        return false;
    }
}
```

* **一般的なストレージメカニズム**

   * 製品ノードは `nt:unstructured` です。

   * 製品ノードは、次のいずれかになります。

      * 参照。製品データは別の場所に保存されます。

         * 製品リファレンスには、`productData` プロパティが含まれます。このプロパティは、製品データ（一般的には `/etc/commerce/products` の下にあります）を指します。

         * 製品データは階層的です。製品属性は、製品データノードの上位ノードから継承されます。

         * また、製品の参照には、ローカルのプロパティを含めることもできます。このプロパティは、製品データで指定されたプロパティを上書きします。

      * 製品自体：

         * `productData` プロパティはありません。

         * すべてのプロパティをローカルに格納する product ノード（productData プロパティを含まない）は、独自の上位ノードから製品属性を直接継承します。

* **AEM-generic プロダクト構造**

   * 各バリアントには、独自のリーフノードが必要です。

   * 製品インターフェイスは製品とバリアントの両方を表しますが、関連するリポジトリノードは、それがどれであるかに固有です。

   * product ノードは、製品の属性とバリアント軸を表します。

#### 例 {#example-1}

```shell
+ banyan_shirt
    - cq:commerceType = product
    - cq:productAttributes = [jcr:title, jcr:description, size, price, color]
    - cq:productVariantAxes = [color, size]
    - jcr:title = Banyan Shirt
    - jcr:description = Flowery, all-cotton shirt.
    - price = 14.00
    + banyan_shirt_s
        - cq:commerceType = variant
        - size = S
        + banyan_shirt_s_red
            - cq:commerceType = variant
            - color = red
        + banyan_shirt_s_blue
            - cq:commerceType = variant
            - color = blue
    + banyan_shirt_m
        - cq:commerceType = variant
        - size = M
        + banyan_shirt_m_red
            - cq:commerceType = variant
            - color = red
        + banyan_shirt_m_blue
            - cq:commerceType = variant
            - color = blue
    + banyan_shirt_l
        - cq:commerceType = variant
        - size = L
        + banyan_shirt_l_red
            - cq:commerceType = variant
            - color = red
        + banyan_shirt_l_blue
            - cq:commerceType = variant
            - color = blue
    + banyan_shirt_xl
        - cq:commerceType = variant
        - size = XL
        - price = 18.00
```

#### 買い物かごのアーキテクチャ {#architecture-of-the-shopping-cart}

**コンポーネント**

* 買い物かごは、`CommerceSession:` によって管理されます。

   * `CommerceSession` は、追加や削除などを実行します。
   * `CommerceSession` は、買い物かごに対する様々な計算も実行します。

* 買い物かごに直接関連はしませんが、`CommerceSession` はカタログの価格情報も提供する必要があります（価格を管理しているので）。

   * 価格には、次の複数の修飾子があります。

      * 数量割引。
      * 様々な通貨。
      * VAT 対応および VAT 対応です。

   * 修飾子は、次のインターフェイスを使用してオープンエンドになります。

      * `int CommerceSession.getQuantityBreakpoints(Product product)`
      * `String CommerceSession.getProductPrice(Product product)`

**ストレージ**

* ストレージ

   * hybris の場合、hybris サーバーが買い物かごを所有します。
   * AEM汎用の場合、買い物かごは、 [ClientContext](/help/sites-administering/client-context.md).

**パーソナライズ機能**

* 常に [ClientContext](/help/sites-administering/client-context.md).
* 買い物かごの ClientContext `/version/` は、すべてのケースで作成されます。

   * 製品は、`CommerceSession.addCartEntry()` メソッドを使用して追加する必要があります。

* 次の図は、ClientContext に格納される買い物かご情報の例を示しています。

![chlimage_1-13](/help/sites-developing/assets/chlimage_1-13a.png)

#### チェックアウトのアーキテクチャ {#architecture-of-checkout}

**買い物かごと注文データ**

`CommerceSession` は、次の 3 つの要素を管理します。

1. 買い物かごの内容
1. 価格
1. 注文の詳細

1. **買い物かごの内容**

   買い物かごのコンテンツスキーマは、次の API で固定されます。

   ```java
   public void addCartEntry(Product product, int quantity);
   public void modifyCartEntry(int entryNumber, int quantity);
   public void deleteCartEntry(int entryNumber);
   ```

1. **価格**

   価格のスキーマも、API によって決められています。

   ```java
   public String getCartPreTaxPrice();
   public String getCartTax();
   public String getCartTotalPrice();
   public String getOrderShipping();
   public String getOrderTotalTax();
   public String getOrderTotalPrice();
   ```

1. **注文の詳細**

   しかし、注文の詳細は API によって決められていません&#x200B;*。*

   ```java
   public void updateOrderDetails(Map<String, String> orderDetails);
   public Map<String, String> getOrderDetails();
   public void submitOrder();
   ```

**送料計算**

* 多くの場合、注文フォームには複数の配送オプション（および価格）が含まれている必要があります。
* 価格は、品目や注文の詳細（重み付けや配送先住所など）に基づく場合があります。
* `CommerceSession` はすべての依存関係にアクセスするので、製品価格と同じ方法で扱うことができます。

   * `CommerceSession` は送料を管理します。
   * `updateOrder(Map<String, Object> delta)` を使用して、配送の詳細情報を取得または更新できます。

>[!NOTE]
>
>以下のような発送セレクターを実装することもできます。
>
> `yourProject/commerce/components/shippingpicker` の下）で、次の手順をおこないます。
>
>* これは基本的に `foundation/components/form/radio` のコピーですが、以下を行うための `CommerceSession` へのコールバックを備えています。
>
>* メソッドが使用可能かどうかの確認
>* 価格情報の追加
>* 関連する `CommerceSession` 情報の公開に関する制御権を持ちつつ、買い物客が AEM 内の注文ページ（発送方法のスーパーセットとその説明テキストを含む）を更新できるようにする

**支払い処理**

* `CommerceSession` は、支払い処理の接続も管理します。

* `CommerceSession` 実装には、選択された支払い処理サービスへの具体的な呼び出しを追加する必要があります。

**注文のフルフィルメント**

* `CommerceSession` は、フルフィルメントの接続も管理します。
* `CommerceSession` 実装には、選択された支払い処理サービスへの具体的な呼び出しを追加する必要があります。

### 検索定義 {#search-definition}

標準のサービス API モデルに従って、e コマースプロジェクトは、個々のコマースエンジンで実装できる検索関連の API のセットを提供します。

>[!NOTE]
>
>現在、標準で Search API を実装しているのは hybris エンジンだけです。
>
>ただし、検索 API は汎用的で、各 CommerceService で個別に実装できます。

e コマースプロジェクトには、次の場所にあるデフォルトの検索コンポーネントが含まれています。

`/libs/commerce/components/search`

![chlimage_1-14](/help/sites-developing/assets/chlimage_1-14a.png)

これにより、検索 API を使用して、選択したコマースエンジンに対するクエリを実行できます ( [e コマースエンジンの選択](#ecommerce-engine-selection)):

#### 検索 API {#search-api}

コアプロジェクトには、次のような汎用/ヘルパークラスが用意されています。

1. `CommerceQuery`

   検索クエリを記述するために使用されます（クエリテキスト、現在のページ、ページサイズ、並べ替え、選択されたファセットに関する情報が含まれます）。 検索 API を実装するすべての e コマースサービスは、検索を実行するためにこのクラスのインスタンスを受け取ります。 `CommerceQuery` は、リクエストオブジェクト（`HttpServletRequest`）からインスタンス化できます。

1. `FacetParamHelper`

    1 つの静的メソッド（`toParams`）を提供するユーティリティクラス。このメソッドを使用して、ファセットのリストと 1 つのトグル値から `GET` パラメーター文字列を生成します。これは、UI 側で役立ちます。各ファセットの値ごとにハイパーリンクを表示する必要があります。ユーザーがハイパーリンクをクリックすると、それぞれの値が切り替えられます（つまり、選択した場合はクエリから削除され、それ以外の場合は追加されます）。 これは、複数値または単一値のファセットの処理、値の上書きなどのすべてのロジックを処理します。

検索 API のエントリポイントは、`CommerceService#search` オブジェクトを返す `CommerceResult` メソッドです。詳しくは、 [API ドキュメント](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation) を参照してください。

### ユーザーの統合 {#user-integration}

AEMと様々な e コマースシステム間で統合が提供されます。 これには、AEM固有のコードがAEMと反対にについてのみ知る必要があるように、様々なシステム間で買い物客を同期する方法が必要です。

* 認証

  AEM は&#x200B;*唯一*&#x200B;の Web フロントエンドと見なされるので、*すべて*&#x200B;の認証は AEM が実行します。

* Hybris のアカウント

  AEM は、買い物客ごとに対応する（セカンダリ）アカウントを Hybris に作成します。 このアカウントのユーザー名は、AEM ユーザー名と同じです。暗号的にランダムなパスワードは、AEMで自動生成され（暗号化され）保存されます。

#### 既存のユーザー {#pre-existing-users}

AEMのフロントエンドは、既存の hybris 実装の前に配置できます。 また、hybris エンジンを既存のAEMインストールに追加できます。 これを行うには、システムは、次のいずれかのシステムで既存のユーザーを適切に処理できる必要があります。

* AEM -> hybris

   * hybris にログインする際に、AEMユーザーが存在しない場合は、次の手順を実行します。

      * 暗号化されたランダムパスワードを使用して新規 hybris ユーザーを作成します。
      * この hybris ユーザー名を AEM ユーザーのユーザーディレクトリに保存します。

   * 参照先: `com.adobe.cq.commerce.hybris.impl.HybrisSessionImpl#login()`

* hybris -> AEM の場合

   * AEM へのログイン時に、システムがユーザーを認識していない場合は、

      * 提供されたユーザー名/pwd を使用して hybris にログインしようとします。
      * 成功した場合は、AEMで同じパスワードを使用して新しいユーザーを作成します (AEM固有の salt はAEM固有のハッシュになります )。

   * 上記のアルゴリズムは Sling の `AuthenticationInfoPostProcessor` で実装されます。

      * 参照先: `com.adobe.cq.commerce.hybris.impl.user.LazyUserImporter.java`

### 読み込みプロセスのカスタマイズ {#customizing-the-import-process}

既存の機能を基にカスタムインポートハンドラーを構築するには：

* `ImportHandler` インターフェイスを実装する必要があります。

* `DefaultImportHandler` を拡張できます。

```java
/**
 * Services implementing the <code>ImportHandler</code> interface are
 * called by the {@link HybrisImporter} to create actual commerce entities
 * such as products.
 */
public interface ImportHandler {

  /**
  * Not used.
  */
  public void createTaxonomie(ImporterContext ctx);

  /**
  * Creates a catalog with the given name.
  * @param ctx   The importer context
  * @param name  The catalog's name
  * @return Path of created catalog
  */
  public String createCatalog(ImporterContext ctx, String name) throws Exception;

  /**
  * Creates a product from the given values.
  * @param ctx                The importer context
  * @param values             The product's properties
  * @param parentCategoryPath The containing category's path
  * @return Path of created product
  */
  public String createProduct(ImporterContext ctx, ValueMap values, String parentCategoryPath) throws Exception;

  /**
  * Creates a variant product from the given values.
  * @param ctx             The importer context
  * @param values          The product's properties
  * @param baseProductPath The base product's path
  * @return Path of created product
  */
  public String createVariantProduct(ImporterContext ctx, ValueMap values, String baseProductPath) throws Exception;

  /**
  * Creates an asset for a product. This is usually a product
  * image.
  * @param ctx             The importer context
  * @param values          The product's properties
  * @param baseProductPath The product's path
  * @return Path of created asset
  */
  public String createAsset(ImporterContext ctx, ValueMap values, String productPath) throws Exception;

  /**
  * Creates a category from the given values.
  * @param ctx           The importer context
  * @param values        The category's properties
  * @param parentPath    Path of parent category or base path of import in case of root category
  * @return Path of created category
  */
  public String createCategory(ImporterContext ctx, ValueMap values, String parentCategoryPath) throws Exception;
}
```

カスタムハンドラーをインポーターが認識するには、次を指定する必要があります。 `service.ranking`プロパティの値が 0 より大きい（例：0）。

```java
@Component
@Service
@Property(name = "service.ranking", value = 100)
public class MyImportHandler extends DefaultImportHandler
{
...
}
```
