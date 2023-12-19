---
title: ClientContext
description: ClientContext を使用して、Adobe Experience Managerの現在のページと訪問者に関する情報を確認する方法を説明します。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
docset: aem65
exl-id: 69c66c82-fbd6-406e-aefd-b85480a62109
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '1961'
ht-degree: 85%

---


# ClientContext {#client-context}

>[!NOTE]
>
>Client Context は、ContextHub に変更されました。詳しくは、[設定](/help/sites-developing/ch-configuring.md)および[デベロッパー](/help/sites-developing/contexthub.md)に関するドキュメントを参照してください。

Client Context は、現在のページと訪問者に関する特定の情報を提供するメカニズムです。**Ctrl + Alt + c キー**（Windows）または **control + option + c キー**（Mac）で開くことができます。

![ClientContext ウィンドウの例](assets/clientcontext_alisonparker.png)

パブリッシュ環境とオーサー環境の両方で、次の情報が表示されます。

* 訪問者。インスタンス固有の情報がリクエストされたものであるか派生されたものであるかによって異なります。
* ページタグ、および現在の訪問者がそれらのタグにアクセスした回数（この情報はマウスを特定のタグの上に置くと表示されます）。
* ページ情報。
* 技術的な環境に関する情報（IP アドレス、ブラウザー、画面解像度など）。
* 現在解決されているセグメント。

アイコン（オーサー環境でのみ使用可能）を使用すると、次の ClientContext の詳細を設定できます。

![ClientContext ウィンドウの編集アイコン、読み込みアイコン、リセットアイコン](do-not-localize/clientcontext_icons.png)

* **編集**
新しいページが開き、次の操作ができます。 [プロファイルプロパティを編集、追加、削除する](#editingprofiledetails).

* **読み込み** テストを実行する[プロファイルをリストから選択してプロファイルを読み込む](#loading-a-new-user-profile)ことができます。

* **リセット** プロファイルを現在のユーザーの[プロファイルにリセット](#resetting-the-profile-to-the-current-user)できます。

## 使用できる ClientContext のコンポーネント {#available-client-context-components}

ClientContext には、([「編集」を使用して選択した内容によって](#adding-a-property-component)）次のプロパティが表示されます。

**サーファー情報**&#x200B;には、次のクライアントサイド情報が表示されます。

* **IP アドレス**
* 検索エンジンのリファラルに使用される&#x200B;**キーワード**
* 使用されている&#x200B;**ブラウザー**
* 使用されている **OS**（オペレーティングシステム）
* 画面の&#x200B;**解像度**
* **マウスの X** ポジション
* **マウスの Y** ポジション

**アクティビティストリーム** AEMフォーラム、ブログ、評価など、様々なプラットフォームでのユーザーのソーシャルアクティビティに関する情報を提供します。

**キャンペーン**：作成者がキャンペーンの特定のエクスペリエンスをシミュレートできます。このコンポーネントは通常のキャンペーンの結果とエクスペリエンスの選択をオーバーライドし、各種配列のテストを有効にします。

キャンペーンの結果は通常、キャンペーンの優先度のプロパティに基づいています。エクスペリエンスは通常、分類に基づいて選択されます。

**買い物かご** 製品エントリ（タイトル、数量、priceFormatted など）、解決されたプロモーション（タイトル、メッセージなど）、割引券（コード、説明など）を含む買い物かご情報を表示します。

買い物かごセッションストアは、ClientContextCartServlet を使用して（分類の変更に基づく）解決済みのプロモーションの変更をサーバーに通知します。

**汎用ストア**：ストアのコンテンツを表示する汎用のコンポーネントです。汎用ストアのプロパティコンポーネントの下位レベルのバージョンです。

汎用ストアは、カスタマイズされた方法でデータを表示する JS レンダラーで設定する必要があります。

**汎用ストアのプロパティ**：ストアのコンテンツを表示する汎用のコンポーネントです。汎用ストアのプロパティコンポーネントの上位レベルのバージョンです。

汎用ストアのプロパティコンポーネントには、設定されたプロパティを（サムネールと共に）リストするデフォルトのレンダラーが含まれます。

**ジオロケーション**：クライアントの緯度と経度を示します。HTML5 Geolocation API を使用して現在の位置についてブラウザーでクエリを実行します。これにより訪問者にポップアップが表示され、位置を共有することに合意するかどうかをブラウザーから確認されます。

コンテキストクラウドで表示される場合、コンポーネントは Google API を使用してマップをサムネールとして表示します。コンポーネントは Google API の[使用制限](https://developers.google.com/maps/documentation/staticmaps/intro#Limits)に従います。

>[!NOTE]
>
>AEM 6.1 では、位置情報ストアはリバースジオコーディング機能を提供していません。このため、位置情報ストアは町名や国コードなどの現在の位置に関する情報を取得しません。このストアデータを使用するセグメントは正しく機能しません。位置情報ストアには位置の緯度と経度のみが含まれます。

**JSONP Store**：インストールによって異なるコンテンツが表示されるコンポーネント。

JSONP 標準は JSON を補完し、同一生成元ポリシーを回避します（Web アプリケーションが別のドメインにあるサーバーと通信できないようにします）。これは、JSON オブジェクトを `<script>` （同じオリジンポリシーに対して許可された例外）他のドメインから。

JSONP ストアは他のストアと同じですが、別のドメインからの情報を読み込むのに現在のドメインにその情報のプロキシを必要としない点が異なります。[JSONP を介して ClientContext にデータを保存](/help/sites-administering/client-context.md#storing-data-in-client-context-via-jsonp)する例を参照してください。

>[!NOTE]
>
>JSONP ストアは cookie に情報をキャッシュしませんが、ページが読み込まれるたびにそのデータを取得します。

**プロファイルデータ**：ユーザープロファイルに収集された情報を表示します。例えば、性別、年齢、E メールアドレスなどです。

**解決済みセグメント**：どのセグメントが現在解決されているかが表示されます（クライアントのコンテキストに表示される他の情報の影響を受ける場合があります）。これは、キャンペーンを設定するときに参考となります。

例えば、マウスが現在ウィンドウの左または右の部分の上にあるかどうかなどです。このセグメントは変更をすぐに確認できるので、主にテストで使用されます。

**ソーシャルグラフ**：ユーザーの友人やフォロワーのソーシャルグラフを表示します。

>[!NOTE]
>
>現時点ではこれはデモ機能で、デモユーザーのプロファイルノードに事前設定されたデータセットに依存します。例：
>
>`/home/users/geometrixx/aparker@geometrixx.info/profile` => friends プロパティ

**タグクラウド**：現在のページに設定されているタグと、サイト閲覧中に収集されたタグを表示します。タグの上にマウスを移動すると、現在のユーザーがその特定のタグを保持しているページにアクセスした回数が表示されます。

>[!NOTE]
>
訪問したページに表示される DAM アセットに設定されているタグはカウントされません。

**Technographics ストア**：このコンポーネントは、インストール環境によって異なります。

**ViewedProducts**：買い物客が閲覧した商品を追跡します。最近閲覧した製品や、買い物かごにまだ入っていない最近閲覧した製品でクエリを実行できます。

このセッションストアにデフォルトのクライアントコンテキストコンポーネントはありません。

詳しくは、[ClientContext の詳細](/help/sites-developing/client-context.md)を参照してください。

>[!NOTE]
>
ページデータは、ClientContext のデフォルトのコンポーネントではなくなりました。必要に応じて、ClientContext を編集し、**汎用ストアのプロパティ**&#x200B;コンポーネントを追加して、**ストア**&#x200B;を `pagedata` として定義するように設定することにより、ページデータを追加できます。

## クライアントコンテキストプロファイルの変更 {#changing-the-client-context-profile}

クライアントコンテキストでは、次の詳細をインタラクティブに変更できます。

* クライアントコンテキストで使用されるプロファイルを変更すると、現在のページで様々なユーザーに対して表示されるものとは異なるエクスペリエンスが表示されます。
* ユーザープロファイルのほか、プロファイルの詳細を変更して様々な状況下でページエクスペリエンスがどのように異なるかを確認できます。

### 新規ユーザープロファイルの読み込み {#loading-a-new-user-profile}

次のいずれかの方法でプロファイルを変更できます。

* [読み込みアイコンを使用](#loading-a-new-visitor-profile-with-the-load-profile-icon)
* [選択スライダーを使用](#loadinganewvisitorprofilewiththeselectionslider)

完了したら、[プロファイルをリセット](#resetting-the-profile-to-the-current-user)できます。

#### プロファイルを読み込みアイコンを使用した新しいユーザープロファイルの読み込み {#loading-a-new-visitor-profile-with-the-load-profile-icon}

1. 次のプロファイルの読み込みアイコンをクリックします。

   ![クライアントコンテキストのプロファイルを読み込みアイコン](do-not-localize/clientcontext_loadprofile.png)

1. ダイアログが開き、ここで読み込むプロファイルを選択できます。

   ![プロファイルを選択するためのドロップダウンが表示されるプロファイルローダーダイアログ](assets/clientcontext_profileloader.png)

1. 「**OK**」をクリックして読み込みます。

#### 選択スライダーを使用した新しいユーザープロファイルの読み込み {#loading-a-new-user-profile-with-the-selection-slider}

次の選択スライダーを使用してプロファイルを選択することもできます。

1. 現在のユーザーを表すアイコンをダブルクリックします。 セレクターが開きます。矢印を使用して移動し、使用可能なプロファイルを確認します。

   ![ユーザーセレクター](assets/clientcontext_profileselector.png)

1. 読み込むプロファイルをクリックします。詳細が読み込まれたら、セレクター以外の場所をクリックしてセレクターを閉じます。

#### プロファイルの現在のユーザーへのリセット {#resetting-the-profile-to-the-current-user}

1. 次のリセットアイコンを使用して ClientContext のプロファイルを現在のユーザーのものに戻します。

   ![リセットアイコン](do-not-localize/clientcontext_resetprofile.png)

### ブラウザープラットフォームの変更 {#changing-the-browser-platform}

1. ブラウザープラットフォームを表すアイコンをダブルクリックします。 セレクターが開き、矢印を使用して移動し、使用可能なプラットフォーム/ブラウザーを確認します。

   ![ブラウザープラットフォームセレクター](assets/clientcontext_browserplatform.png)

1. 読み込むブラウザープラットフォームをクリックします。詳細が読み込まれたら、セレクター以外の場所をクリックしてセレクターを閉じます。

### 位置情報の変更 {#changing-the-geolocation}

1. 位置情報アイコンをダブルクリックします。 展開されたマップが開き、マーカーを新しい位置にドラッグできます。

   ![位置情報の詳細](assets/clientcontext_geomocationrelocate.png)

1. マップ以外の場所をクリックして閉じます。

### タグ選択の変更 {#changing-the-tag-selection}

1. ClientContext の「タグクラウド」セクションをダブルクリックします。 ダイアログが開き、ここでタグを選択できます。

   ![タグクラウドダイアログ](assets/clientcontext_tagselection.png)

1. 「OK」をクリックしてクライアントコンテキストに読み込みます。

## クライアントコンテキストの編集 {#editing-the-client-context}

クライアントコンテキストの編集を使用して、特定のプロパティの値を設定（またはリセット）したり、新規プロパティの追加や不要になったプロパティを削除したりできます。

### プロパティの詳細の編集 {#editing-property-details}

ClientContext を編集して、特定のプロパティの値を設定（またはリセット）できます。これにより、特定のシナリオをテストすることができます（特に[セグメント化](/help/sites-administering/campaign-segmentation.md)や[キャンペーン](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md)で役に立ちます）。

![クライアントコンテキストの編集](assets/clientcontext_alisonparker_edit.png)

### プロパティコンポーネントの追加 {#adding-a-property-component}

を開いた後、 **ClientContextデザインページ**&#x200B;また、 **追加** 使用可能なコンポーネントを使用した完全に新しいプロパティ ( コンポーネントはサイドキックまたは **新規コンポーネントを挿入** ダブルクリックした後に開くダイアログ **コンポーネントまたはアセットをここにドラッグ** ボックス ):

![クライアントコンテキストウィンドウへのプロパティの追加](assets/clientcontext_alisonparker_new.png)

### プロパティコンポーネントの削除 {#removing-a-property-component}

**ClientContext デザインページ**&#x200B;を開いた後、不要になった場合はプロパティを「**削除**」することもできます。このようなプロパティには、初期設定のまますぐに使用できるプロパティがあります。「**リセット**」を使用すると、プロパティが削除された場合に元に戻すことができます。

## JSONP を使用したクライアントコンテキストでのデータの保存 {#storing-data-in-client-context-via-jsonp}

この例に従って JSONP ストアコンテキストストアコンポーネントを使用して、外部データをクライアントコンテキストに追加します。次に、そのデータからの情報に基づいてセグメントを作成します。この例では、WIPmania.com が提供する JSONP サービスを使用します。このサービスは、web クライアントの IP アドレスに基づいて位置情報を返します。

この例は、Geometrixx Outdoors のサンプル web サイトを使用してクライアントコンテキストにアクセスし、作成したセグメントをテストします。クライアントコンテキストが有効になっているページであれば、別の web サイトを使用できます。（[ページへのクライアントコンテキストの追加](/help/sites-developing/client-context.md#adding-client-context-to-a-page)を参照。）

### JSONP ストアコンポーネントの追加 {#add-the-jsonp-store-component}

クライアントコンテキストに JSONP ストアコンポーネントを追加すると、web クライアントの位置情報の取得と保存に使用できます。

1. AEM オーサーインスタンスの Geometrixx Outdoors サイトの英語のホームページを開きます（[https://localhost:4502/content/geometrixx-outdoors/en.html](https://localhost:4502/content/geometrixx-outdoors/en.html)）。
1. ClientContext を開くには、Ctrl + Alt + C キー（Windows）または Control + Option + C キー（Mac）を押します。
1. ClientContext の上部にある編集アイコンをクリックして、ClientContext デザイナーを開きます。

   ![リンクアイコン](do-not-localize/chlimage_1.png)

1. ClientContext に JSONP ストアコンポーネントをドラッグします。

   ![ClientContext に JSONP ストアコンポーネントをドラッグ＆ドロップする](assets/chlimage_1-4.jpeg)

1. コンポーネントをダブルクリックして、編集ダイアログを開きます。
1. 「JSONP サービスの URL」ボックスに次の URL を入力し、「ストアを取得」をクリックします。

   `https://api.wipmania.com/jsonp?callback=${callback}`

   このコンポーネントは JSONP サービスを呼び出し、返されたデータに含まれるすべてのプロパティをリストします。 リストに含まれるプロパティは、ClientContext で使用できるプロパティです。

   ![JSONP サービスのプロパティ](assets/chlimage_1-40.png)

1. 「OK」をクリックします。
1. Geometrixx Outdoors ホームページに戻り、ページを更新します。ClientContext に、JSONP ストアコンポーネントからの情報が取り込まれます。

   ![データが入力された JSONP コンポーネントの例](assets/chlimage_1-41.png)

### セグメントを作成 {#create-the-segment}

JSONP ストアコンポーネントを使用して作成したセッションストアのデータを使用します。セグメントはセッションストアの緯度と現在の日付から、クライアントの場所が冬時間であるかどうかを判断します。

1. ツールコンソールを web ブラウザーで開きます（`https://localhost:4502/miscadmin#/etc`）。
1. フォルダーツリーで、ツール／セグメンテーションフォルダーをクリックし、新規／新しいフォルダーをクリックします。次のプロパティ値を指定し、「作成」をクリックします。

   * 名前：mysegments
   * タイトル：My Segments

1. My Segments フォルダーを選択し、新規／新しいページをクリックします。

   1. タイトルに「Winter」と入力します。
   1. セグメントテンプレートを選択します。
   1. 「作成」をクリックします。

1. Winter セグメントを右クリックし、「開く」をクリックします。
1. 汎用ストアプロパティをデフォルトの AND コンテナにドラッグします。

   ![セグメントエディターへのコンポーネントの追加](assets/chlimage_1-5.jpeg)

1. コンポーネントをダブルクリックして編集ダイアログを開き、次のプロパティ値を指定して、「OK」をクリックします。

   * ストア：wipmania
   * プロパティ名：latitude
   * 演算子：is greater than
   * プロパティ値：30

1. スクリプトコンポーネントを同じ AND コンテナにドラッグし、編集ダイアログを開きます。次のスクリプトを追加し、「OK」をクリックします。

   `3 < new Date().getMonth() < 12`
