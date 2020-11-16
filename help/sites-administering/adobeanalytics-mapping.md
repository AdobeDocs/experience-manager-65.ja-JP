---
title: コンポーネントデータと Adobe Analytics プロパティとのマッピング
seo-title: コンポーネントデータと Adobe Analytics プロパティとのマッピング
description: コンポーネントデータと SiteCatalyst プロパティをマッピングする方法について説明します。
seo-description: コンポーネントデータと SiteCatalyst プロパティをマッピングする方法について説明します。
uuid: b08ab37f-ad58-4c04-978f-8e21a3823ae8
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 6c1f8869-62d9-4fac-aa0d-b99bb0e86d6b
docset: aem65
translation-type: tm+mt
source-git-commit: 6f49e01aa3e9841c7b2917870593452b778667d2
workflow-type: tm+mt
source-wordcount: '1470'
ht-degree: 53%

---


# コンポーネントデータと Adobe Analytics プロパティとのマッピング{#mapping-component-data-with-adobe-analytics-properties}

Adobe Analytics に送信するデータを収集するフレームワークにコンポーネントを追加します。分析データを収集するために設計されたコンポーネントは、適切な **CQ 変数**&#x200B;にデータを保存します。When you add such a component to a framework, the framework displays the list of CQ variables so that you can each to the appropriate **Analytics variable**.

![aa-11](assets/aa-11.png)

When the **AEM view** is open the Analytics variables appear in the content finder.

![aa-12](assets/aa-12.png)

You can map multiple Analytics variables with the same **CQ variable**.

![chlimage_1-68](assets/chlimage_1-68.png)

ページが読み込まれ、次の条件が満たされると、マップされたデータがAdobe Analyticsに送信されます。

* ページがフレームワークに関連付けられている。
* ページが、フレームワークに追加されたコンポーネントを使用する。

CQコンポーネント変数をAdobe Analyticsレポートプロパティにマッピングするには、次の手順を実行します。

1. In the **AEM view**, drag a tracking component from sidekick onto the framework. For example, drag the **Page** component component from the **General** category.

   ![aa-13](assets/aa-13.png)

   デフォルトのコンポーネントグループには、「**一般**」、「**コマース**」、「**コミュニティ**」、「**Search&amp;Promote**」および「**その他**」があります。AEM インスタンスは、異なるグループおよびコンポーネントを表示するように設定されていることがあります。

1. To map Adobe Analytics variables with variables that are defined in the component, drag an **Analytics variable** from the content finder onto a field on the tracking component. 例えば、にドラッグ `Page Name (pageName)` し `pagedata.title`ます。

   ![aa-14](assets/aa-14.png)

   >[!NOTE]
   >
   >フレームワーク用に選択されたレポートスイートID(RSID)によって、コンテンツファインダーに表示されるAdobe Analytics変数が決まります。

1. 他のコンポーネントおよび変数について、前述の 2 つの手順を繰り返します。

   >[!NOTE]
   >
   >You can map multiple Analytics variables (e.g. `props`, `eVars`, `events`) to the same CQ variable (e.g. `pagedata.title`)

   >[!CAUTION]
   >
   >次の状態が強く推奨されます。
   >    
   >    * `eVars` の値 `props``pagedata.X` は、または `eventdata.X`
      >    
      >    
   * それに対して、イベントは`eventdata.events.X` で始まる変数にマッピングされる必要があること


1. To make the framework available on the publish instance of your site, open the **Page** tab of sidekick, and click **Activate Framework.**

## 製品関連変数のマッピング {#mapping-product-related-variables}

AEMでは、製品関連の変数およびAdobe Analytics製品関連のプロパティにマップするイベントに命名規則を使用します。

| CQ 変数 | Analytics 変数 | 説明 |
|---|---|---|
| `product.category` | `product.category` （コンバージョン変数） | 製品カテゴリです。 |
| `product.sku` | `product.sku` （コンバージョン変数） | 製品 SKU です。 |
| `product.quantity` | `product.quantity` （コンバージョン変数） | 購入される製品の数です。 |
| `product.price` | `product.price` （コンバージョン変数） | 製品価格です。 |
| `product.events.<eventName>` | レポートで製品に関連付けるための成功イベントです。 | `product.events` は、*eventName* という名前のイベントのプレフィックスです。 |
| `product.evars.<eVarName>` | 製品に関連付けるためのコンバージョン変数（`eVar`）です。 | `product.evars` は、*eVarName* という名前の eVar 変数のプレフィックスです。 |

いくつかの AEM Commerce コンポーネントは、これらの変数名を使用します。

>[!NOTE]
>
>Adobe Analytics製品プロパティをCQ変数にマップしないでください。 この表で説明している製品関連マッピングの設定は、Products 変数へのマッピングと実質的に同じです。

### Adobe Analytics のレポートのチェック {#checking-reports-on-adobe-analytics}

1. AEMに提供されたのと同じ資格情報を使用して、Adobe AnalyticsのWebサイトにログインします。
1. 選択した RSID が、前の手順で使用したものであることを確認します。
1. （ページの左側の）**レポート**&#x200B;で、**カスタムコンバージョン**／**カスタムコンバージョン 1～10** を選択して、`eVar7` に対応する変数を選択します。

1. 使用しているAdobe Analyticsのバージョンに応じて、レポートが使用した検索語句で更新されるまで、平均45分待つ必要があります。例：茄子

## Adobe Analytics フレームワークでの Content Finder（cf#）の使用 {#using-the-content-finder-cf-with-adobe-analytics-frameworks}

最初は、Adobe Analyticsのフレームワークを開くと、コンテンツファインダーに事前定義されたAnalytics変数が含まれます。これは次の場所です。

* トラフィック
* コンバージョン
* イベント

RSID が選択されている場合、その RSID に属するすべての変数がリストに追加されます。\
The `cf#` is needed in order to map Analytics variables to the CQ variables present on the different tracking components. 基本トラッキングのためのフレームワークのセットアップを参照してください。

フレームワーク用に選択した表示に応じて、コンテンツファインダーは、Analytics変数(AEM表示内)またはCQ変数(Analytics表示内)によって入力されます。

リストは、次の方法で操作できます。

1. **AEM ビュー**&#x200B;では、リストは、3 つのフィルターボタンを使用してどの変数の型が選択されているかに応じて、フィルターできます。

   * どのボタンも選択されて&#x200B;*いない*&#x200B;場合、完全なリストが表示されます。
   * If the **Traffic** button is selected, the list will only show the variables belonging to the Traffic section.
   * If the **Conversion** button is selected, the list will only show the variables belonging to the Conversion section.
   * 「**イベント**」ボタンが選択されている場合、リストには、「イベント」セクションに属する変数のみが表示されます。

   >[!NOTE]
   >
   >一度に 1 つのフィルターのみアクティブにできます。

   >[!NOTE]
   >
   >Search&amp;Promote変数は、「コンバージョン」セクションにも属します。

   1. また、リストには検索機能があり、検索フィールドに入力されたテキストに従って要素をフィルタリングします。
   1. リストの要素の検索中にフィルターオプションを有効にした場合、表示される結果も、アクティブなボタンに従ってフィルタリングされます。
   1. リストは、渦巻き矢印ボタンを使用して、いつでもリロードできます。
   1. 複数の RSID がフレームワークで選択されている場合、リストのすべての変数は、選択した RSID 内で使用されたすべてのラベルを使用して表示されます。


1. Adobe Analytics表示では、コンテンツファインダーにCQ表示内にドラッグされたトラッキングコンポーネントに属するすべてのCQ変数が表示されます。

   * e.g. in case the **Download component** is the *only one dragged* in CQ view (which has two mappable variables *eventdata.downloadLink* and *eventdata.events.startDownload*), the Content Finder wil look like this when switching to Adobe Analytics view:

   ![aa-22](assets/aa-22.png)

   * The variables can be dragged&amp;dropped onto any Adobe Analytics variable belonging to either one of the 3 variable sections (**Traffic**, **Conversion** and **Events**).

   * 新しいトラッキングコンポーネントをCQ表示のフレームワークにドラッグすると、そのコンポーネントに属するCQ変数が自動的にAdobe Analytics表示のコンテンツファインダー(cf#)に追加されます。
   >[!NOTE]
   >
   >一度に1つのCQ変数のみをAdobe Analytics変数にマップできます

## AEM ビューと Analytics ビューの使用 {#using-aem-view-and-analytics-view}

いつでも、フレームワークページ上でのAdobe Analyticsのマッピングを表示する2つの方法を切り替えることができます。 2 つのビューは、2 つの異なる見方からのフレームワーク内のマッピングの概要をわかりやすく提供します。

### AEM ビュー {#aem-view}

![aa-23](assets/aa-23.png)

上記の図を例に挙げると、**AEM ビュー**&#x200B;には次のプロパティがあります。

1. これはフレームワークが開いたときのデフォルトの表示です。
1. 左側：コンテンツファインダー(cf#)は、選択されたRSIDに基づいて、Adobe Analytics変数によって入力されます。
1. タブヘッダー（**AEM ビュー**&#x200B;と **Analytics ビュー**）：2 つのビューを切り替えるのに使用します。

1. **AEM ビュー**:

   1. フレームワークにその親から継承されるコンポーネントがある場合、コンポーネントにマッピングされた変数と共に、ここにリストが表示されます。

      1. 継承されたコンポーネントはロックされています。
      1. 継承されたコンポーネントのロックを解除するには、コンポーネントの名前の横にある鍵アイコンをダブルクリックします。
      1. 継承を元に戻すには、ロックされていないコンポーネントを削除する必要があります。その後、コンポーネントはロックされた状態に戻されます。
   1. **分析フレームワークにコンポーネントを追加するには、ここにコンポーネントをドラッグします**：コンポーネントはサイドキックからドラッグアンドドロップすることができます。
   1. 現在分析フレームワークに含まれるすべてのコンポーネントを検索できます。

      1. コンポーネントを追加するには、サイドキックの「コンポーネント」タブからドラッグします。
      1. コンポーネントとそのすべてのマッピングを削除するには、コンポーネントのコンテキストメニューから「削除」を選択し、確認ダイアログで削除を受け入れます。
      1. コンポーネントは、作成したフレームワークからのみ削除でき、従来のように子フレームワークからは削除できません（上書きのみ可能です）。


### Analytics ビュー {#analytics-view}

![aa-24](assets/aa-24.png)

1. This view can be accessed by switching to the **Analytics view** tab on the framework.
1. 左側：コンテンツファインダー（cf#）は、CQ ビューのフレームワークにドラッグしたコンポーネントに基づく CQ 変数によって入力されます。
1. タブヘッダー（**AEM ビュー**&#x200B;と **Analytics ビュー**）：2 つのビューを切り替えるのに使用します。

1. 3つのテーブル(トラフィック、コンバージョン、イベント)リストは、すべてのAdobe Analytics変数で使用できます。 一覧表示されています。ここに示されるマッピングは、AEM ビューのものと同じです。

   * **トラフィック**：

      * Traffic variable ( `prop1`) mapped to a CQ variable ( `eventdata.downloadLink`)

      * コンポーネントの隣に鍵アイコンがある場合、これは、親フレームワークからの継承であり、そのため編集できないことを意味します。
   * **コンバージョン**:

      * Conversion variable ( `eVar1`) mapped to a CQ variable ( `pagedata.title`)

      * CQ 変数フィールドをダブルクリックしてコードを手動で入力することにより、JavaScript 式にマッピングされたコンバージョン変数（`eVar3`）をインラインで追加しました。
   * **イベント**:

      * Event variable ( `event1`) mapped to a CQ event ( `eventdata.events.pageView`)



>[!NOTE]
>
>すべての表の CQ 変数列は、フィールドをダブルクリックしてテキストを追加することで、インラインで入力することもできます。これらのフィールドは、JavaScript を入力として受け取ります。
>
>* 例：次の列 `prop3` に
>* `'`* `Adobe:'+pagedata.title+':'+pagedata.sitesection`\
   >  を使用して、ページの *タイトル* と *sitesectionを連結して送信するには**:* （コロン）で始まり、 *Adobe* : `prop3`

>



>[!CAUTION]
>
>Adobe Analytics変数にマップできるCQ変数は、いつでも1つだけです。

