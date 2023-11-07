---
title: アセットエディターページの作成と設定
description: カスタムのアセットエディターページを作成し、複数のアセットを同時に編集する方法を学習します。
contentOwner: AG
role: User, Admin
feature: Developer Tools,Asset Management
exl-id: 53e310a9-c511-447a-91bd-8c5b2760dc03
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '2110'
ht-degree: 48%

---

# アセットエディターページの作成と設定 {#creating-and-configuring-asset-editor-pages}

このドキュメントは次の内容について説明します。

* カスタマイズしたアセットエディターページを作成する理由。
* アセットエディターページ（メタデータの表示と編集、およびアセットに対するアクションの実行を可能にする WCM ページ）の作成とカスタマイズの方法です。
* 複数のアセットを同時に編集する方法。

<!-- TBD: Add UICONTROL tags. Need PM review. Flatten the structure a bit. Re-write to remove Geometrixx mentions and to adhere to 6.5 default samples. -->

>[!NOTE]
>
>アセット共有は、オープンソースの参照実装として使用できます。 詳しくは、 [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/). 正式にはサポートされていません。

## アセットエディターページを作成および設定する理由 {#why-create-and-configure-asset-editor-pages}

デジタルアセット管理は、より多くのシナリオで使用されています。 専門的に訓練されたユーザー（写真家や分類学者など）の小規模なソリューションから、ビジネスユーザー、WCM 作成者、ジャーナリストなど、より多様なユーザーグループに移行する場合、 [!DNL Adobe Experience Manager Assets] は多くの情報を提供する場合があります。 関係者は、特定のユーザーインターフェイスまたはアプリケーションに、関連性の高いデジタルアセットへのアクセスをリクエストし始めます。

そのようなアセット中心型アプリケーションの例としては、従業員が展示会の参加時の写真をアップロードできるイントラネット内のシンプルな写真ギャラリーや、公開 web サイトでのプレスセンターなどが考えられます。アセット中心型アプリケーションは、買い物かご、チェックアウト、検証プロセスを含む完全なソリューションに拡張することもできます。

アセット中心のアプリケーションを作成すると、コーディングは不要で、ユーザーグループとそのニーズと、使用するメタデータに関する知識のみを把握できる設定プロセスになります。 [!DNL Assets] で作成されたアセット中心型アプリケーションは拡張可能です。適度なコーディング作業によって、アセットの検索、表示、変更のための再利用可能なコンポーネントを作成できます。

[!DNL Experience Manager] のアセット中心型アプリケーションはアセットエディターページで構成されており、特定アセットの詳細を表示するために使用できます。アセットエディターページでは、アセットにアクセスするユーザーが必要な権限を持っていれば、メタデータの編集も可能です。

<!--
## Create and configure an Asset Share page {#creating-and-configuring-an-asset-share-page}

You customize the DAM Finder functionality and create pages that have all the functionality you require, which are called Asset Share pages. To create an Asset Share page, you add the page using the Geometrixx Asset Share template and then you customize the actions users can perform on that page, determine how viewers see the assets, and decide how users can build their queries.

Here are some use cases for creating a customized Asset Share page:

* Press Center for Journalists.
* Image Search Engine for internal business users.
* Image Database for website users.
* Media Tagging Interface for metadata editors.

### Create an Asset Share page {#creating-an-asset-share-page}

To create an Asset Share page, you can either create it when you are working on web sites or from the digital asset manager.

>[!NOTE]
>
>By default, when you create an Asset Share page from **New** in the digital asset manager, an Asset viewer and Asset editor are automatically created for you.

To create an new Asset Share page in the **Websites** console:

1. In the **Websites** tab, navigate to the place where you want to create an asset share page and click **New**.

1. Select the **Asset Share** page and click **Create**. The new page is created and the asset share page is listed in the **Websites** tab.

![dam8](assets/dam8.png)

The basic page created using the Geometrixx DAM Asset Share template looks as follows:

![screen_shot_2012-04-18at115456am](assets/screen_shot_2012-04-18at115456am.png)

To customize your Asset Share page, you use elements from the sidekick and you also edit query builder properties. The page **Geometrixx Press Center** is a customized version of a page based on this template:

![screen_shot_2012-04-19at123048pm](assets/screen_shot_2012-04-19at123048pm.png)

To create an asset share page by way of the digital asset manager:

1. In the digital asset manager, in **New**, select **New Asset Share**.
1. In the **Title**, enter the name of the asset share page. If desired, enter a name for the URL.

   ![screen_shot_2012-04-19at23626pm](assets/screen_shot_2012-04-19at23626pm.png)

1. Double-click the asset share page to open it and configure the page.

   ![screen_shot_2012-04-19at24114pm](assets/screen_shot_2012-04-19at24114pm.png)

   By default, when you create an Asset Share page from **New**, an Asset viewer and Asset editor are automatically created for you.

#### Customize actions {#customizing-actions}

You can determine what actions users can perform on selected digital assets from a selection of predefined actions.

To add actions to the Asset Share page:

1. In the Asset Share page that you want to customize, click **Actions** in the sidekick.

The following actions are available:

 | Action | Description |
 |---|---|
 | [!UICONTROL Delete Action] | Users can delete the selected assets. |
 | [!UICONTROL Download Action] | Lets users download selected assets to their computers. |
 | [!UICONTROL Lightbox Action] | Saves assets to a "lightbox"   where you can perform other actions on them. This comes in handy when working   with assets across multiple pages. The lightbox can also be used as a   shopping cart for assets. |
 | [!UICONTROL Move Action] | Users can move the asset to another   location |
 | [!UICONTROL Tags Action] | Lets users add tags to selected assets |
 | [!UICONTROL View Asset Action] | Opens the asset in the Asset editor for   user manipulation. |

1. Drag the appropriate action to the **Actions** area on the page. Doing so creates a button that is used to execute that action.

![chlimage_1-159](assets/chlimage_1-387.png)

#### Determine how search results are presented {#determining-how-search-results-are-presented}

You determine how results are displayed from a predefined list of lenses.

To change how search results are viewed:

1. In the Asset Share page that you want to customize, click Search.

![chlimage_1](assets/assetshare3.png)

1. Drag the appropriate lens to the top center of the page. In the Press Center, the lenses are already available. Users press the appropriate lens icon to display search results as desired.

The following lenses are available:

| Lens | Description |
|---|---|
| **[!UICONTROL List Lens]** |Presents the assets in a list fashion with details. |
| **[!UICONTROL Mosaic Lens]** |Presents assets in a mosaic fashion. |

#### Mosaic Lens {#mosaic-lens}

![chlimage_1-160](assets/chlimage_1-388.png)

#### List Lens {#list-lens}

![chlimage_1-161](assets/chlimage_1-389.png)

#### Customize the Query Builder {#customizing-the-query-builder}

The query builder lets you enter search terms and create content for the Asset Share page. When you edit the query builder, you also get to determine how many search results are displayed per page, which asset editor opens when you double-click an asset, the path the query searches, and customizes nodetypes.

To customize the query builder:

1. In the Asset Share page that you want to customize, click **Edit** in the Query Builder. By default, the **General** tab opens.
1. Select the number of results per page, the path of the asset editor (if you have a customized asset editor) and the Actions title.

![screen_shot_2012-04-23at15055pm](assets/screen_shot_2012-04-23at15055pm.png)

1. Click the **Paths** tab. Enter a path or multiple paths that the search will run. These paths are overwritten if the user uses the Paths predicate.

![screen_shot_2012-04-23at15150pm](assets/screen_shot_2012-04-23at15150pm.png)

1. Enter another node type, if desired.

1. In the **Query Builder URL** field, you can override or wrap the query builder and enter the new servlet URLs with the existing query builder component. In the **Feed URL** field, you can override the Feed URL as well.

![screen_shot_2012-04-23at15313pm](assets/screen_shot_2012-04-23at15313pm.png)

1. In the **Text** field, enter the text you want to appear for results and page numbers of results. Click **OK** when finished making changes.

![screen_shot_2012-04-23at15300pm](assets/screen_shot_2012-04-23at15300pm.png)

#### Add predicates {#adding-predicates}

Experience Manager Assets includes several predicates that you can add to the Asset Share page. These let your users further narrow searches. In some cases, they may override a query builder parameter (for example, the Path parameter).

To add predicates:

1. In the Asset Share page that you want to customize, click **Search**.

![assetshare3](assets/assetshare3.png)

1. Drag the appropriate predicates to the Asset Share page underneath the query builder. Doing so creates the appropriate fields.

![assetshare4](assets/assetshare4.png)

The following predicates are available:

| Predicate | Description |
|---|---|
| **[!UICONTROL Date Predicate]** |Lets users search for assets that were modified before and after certain dates. |
| **[!UICONTROL Options Predicate]** |The site owner can specify a property to search for (as in the property predicate, for example, cq:tags) and a content tree to populate the options from (for example, the tag tree). Doing so generates a list of options where the users can select the values (tags) that the selected property (tag property) should have. This predicate lets you build list controls like the list of tags, file types, image orientations, and so on. It is great for a fixed set of options. |
| **[!UICONTROL Path Predicate]** |Lets users define the path and subfolders, if desired. |
| **[!UICONTROL Property Predicate]** |The site owner specifies a property to search for, for example, tiff:ImageLength and the user can then enter a value, for example, 800. This returns all images that are 800 pixels high. Useful predicate if your property can have arbitrary values. |

For more information, see the [predicate Javadocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/package-summary.html).

1. To configure the predicate further, double-click it. For example, when you open the Path Predicate, you need to assign the root path.

![screen_shot_2012-04-23at15640pm](assets/screen_shot_2012-04-23at15640pm.png)
-->

## アセットエディターページの作成と設定 {#creating-and-configuring-an-asset-editor-page}

アセットエディターをカスタマイズして、デジタルアセットの表示と編集の方法を指定できます。 これをおこなうには、アセットエディターページを作成し、そのページでユーザーが実行できるビューとアクションをカスタマイズします。

>[!NOTE]
>
>DAM アセットエディターにカスタムフィールドを追加する場合は、新しい `cq:Widget` ノードから `/apps/dam/content/asseteditors.`

### アセットエディターページを作成する {#creating-the-asset-editor-page}

アセットエディターページを作成する場合は、アセット共有ページのすぐ下にページを作成することをお勧めします。

アセットエディターページを作成するには：

1. Adobe Analytics の **[!UICONTROL Web サイト]** 」タブで、アセットエディターページを作成する場所に移動し、 **新規**.
1. 「**Geometrixx アセットエディター**」を選択し、「**作成**」をクリックします。新しいページが作成され、ページが「**Web サイト**」タブに表示されます。

![screen_shot_2012-04-23at15858pm](assets/screen_shot_2012-04-23at15858pm.png)

Geometrixx アセットエディターテンプレートを使用して作成された基本ページは次のイメージのようになります。

![assetshare5](assets/assetshare5.png)

アセットエディターページをカスタマイズするには、サイドキックの要素を使用します。**Geometrixx プレスセンター** からアクセスするアセットエディターページは、このテンプレートに基づいたページのカスタマイズバージョンです。

![assetshare6](assets/assetshare6.png)

#### アセット共有ページから開くようにアセットエディターを設定する {#setting-which-asset-editor-opens-from-an-asset-share-page}

カスタマイズされたアセットエディターページを作成したら、作成したカスタマイズされたアセット共有のアセットをダブルクリックして、カスタマイズされたエディターページでアセットを開くようにします。

アセットエディターページを設定するには：

1. アセット共有ページで、QueryBuilder の隣にある「**編集**」をクリックします。

![screen_shot_2012-04-23at20123pm](assets/screen_shot_2012-04-23at20123pm.png)

1. 「**一般**」タブが選択されていない場合は、クリックします。

1. Adobe Analytics の **アセットエディターのパス** フィールドで、アセット共有ページでアセットを開くアセットエディターのパスを入力し、 **OK**.

![screen_shot_2012-04-23at21653pm](assets/screen_shot_2012-04-23at21653pm.png)

#### アセットエディターコンポーネントを追加する {#adding-asset-editor-components}

アセットエディターが持つ機能を決定するには、ページにコンポーネントを追加します。

アセットエディターコンポーネントを追加するには：

1. カスタマイズするアセットエディターページで、サイドキックの「**アセットエディター**」を選択します。使用可能なすべてのアセットエディターコンポーネントが表示されます。

>[!NOTE]
>
>カスタマイズできる内容は、使用可能なコンポーネントによって異なります。 コンポーネントを有効にするには、デザインモードに移動し、有効にする必要のあるコンポーネントを選択します。

1. サイドキックからアセットエディターにコンポーネントをドラッグし、コンポーネントダイアログボックスで編集を行います。 コンポーネントについては、次の表で説明し、以降の詳細な手順で説明します。

>[!NOTE]
>
>アセットエディターページをデザインする際に、読み取り専用または編集可能なコンポーネントを作成します。 鉛筆の画像がそのコンポーネントに表示されている場合、フィールドは編集できることをユーザーは把握しています。 デフォルトでは、ほとんどのコンポーネントは読み取り専用として設定されています。

| コンポーネント | 説明 |
|---|---|
| **[!UICONTROL メタデータフォーム]と[!UICONTROL メタデータテキストフィールド]** | アセットにメタデータを追加し、そのアセットに対して送信などのアクションを実行できます。 |
| **[!UICONTROL サブアセット]** | サブアセットをカスタマイズできます。 |
| **タグ** | ユーザーがタグを選択してアセットに追加できます。 |
| **[!UICONTROL サムネール]** | アセットのサムネールとファイル名が表示され、代替テキストを追加できます。 ここでもアセットエディターのアクションを追加できます。 |
| **[!UICONTROL タイトル]** | アセットのタイトルを表示します。このタイトルはカスタマイズ可能です。 |

![screen_shot_2012-04-23at22743pm](assets/screen_shot_2012-04-23at22743pm.png)

#### メタデータフォームとテキストフィールド — メタデータコンポーネントの表示の設定 {#metadata-form-and-text-field-configuring-the-view-metadata-component}

メタデータフォームは、開始アクションと終了アクションを含むフォームです。 その間に、次の値を入力します。 **テキスト** フィールド。 詳しくは、 [Forms](/help/sites-authoring/default-components-foundation.md#form-component) フォームの操作に関する詳細

1. フォームの開始領域の「**編集**」をクリックして、開始アクションを作成します。必要に応じて、ボックスのタイトルを入力できます。 デフォルトでは、ボックスのタイトルは **メタデータ**. 検証用の JavaScript クライアントコードを生成する場合は、「クライアントの検証」チェックボックスを選択します。

![screen_shot_2012-04-23at22911pm](assets/screen_shot_2012-04-23at22911pm.png)

1. フォームの終了領域の「**編集**」をクリックして、終了アクションを作成します。例えば、ユーザーがメタデータの変更内容を送信できる「**[!UICONTROL 送信]**」ボタンを作成できます。オプションとして、メタデータを元の状態にリセットできる「**リセット**」ボタンを追加できます。

![screen_shot_2012-04-23at23138pm](assets/screen_shot_2012-04-23at23138pm.png)

1. フォームの「**フォーム開始**」と「**フォーム終了**」の間に、メタデータテキストフィールドをドラッグします。ユーザーはこれらのテキストフィールドにメタデータを入力し、このメタデータを送信するか、他のアクションを実行することができます。

1. 「**タイトル**」などのフィールド名をダブルクリックし、メタデータフィールドを開いて変更を行います。Adobe Analytics の **一般** タブ **コンポーネントを編集** ウィンドウで、名前空間とフィールドのラベルおよびタイプを定義します。例： `dc:title`.

![screen_shot_2012-04-23at23305pm](assets/screen_shot_2012-04-23at23305pm.png)

メタデータフォームで使用可能な名前空間の変更について詳しくは、[Assets のカスタマイズと拡張](/help/assets/extending-assets.md)を参照してください。

1. 「**制約**」タブをクリックします。ここで、フィールドを必須にするかどうかを選択し、必要に応じて制約を追加できます。

![screen_shot_2012-04-23at23435pm](assets/screen_shot_2012-04-23at23435pm.png)

1. 「**表示**」タブをクリックします。ここで、メタデータフィールドの新しい幅と行数を入力できます。 を選択します。 **フィールドは読み取り専用です** チェックボックスをオンにして、ユーザーがメタデータを編集できるようにします。

![screen_shot_2012-04-23at23446pm](assets/screen_shot_2012-04-23at23446pm.png)

次に、様々なフィールドを持つメタデータフォームの例を示します。

![メタデータ](assets/chlimage_1-390.png)

アセットエディターページでは、ユーザーはこの後メタデータフィールドに値を入力し（フィールドが編集可能な場合）、終了アクション（変更内容の送信など）を実行することができます。

#### サブアセット {#sub-assets}

サブアセットコンポーネントでは、サブアセットの表示と選択をおこなうことができます。 どの名前が [メインアセット](/help/assets/assets.md#what-are-digital-assets) およびサブアセット。

サブアセットコンポーネントをダブルクリックして、サブアセットダイアログボックスを開き、メインアセットと任意のサブアセットのタイトルを変更できます。 デフォルト値は、対応するフィールドの下に表示されます。

![screen_shot_2012-04-23at23907pm](assets/screen_shot_2012-04-23at23907pm.png)

次に、設定済みのサブアセットコンポーネントの例を示します。

![screen_shot_2012-04-23at24442pm](assets/screen_shot_2012-04-23at24442pm.png)

例えば、あるサブアセットを選択すると、コンポーネントに適切なページが表示され、ボックスタイトルがサブアセットから兄弟アセットに変更されます。

![screen_shot_2012-04-23at24552pm](assets/screen_shot_2012-04-23at24552pm.png)

#### タグ {#tags}

タグコンポーネントは、ユーザーが既存のタグをアセットに割り当てることができるコンポーネントで、後での整理や取得に役立ちます。 このコンポーネントは読み取り専用にできるので、ユーザーはタグを追加できず、表示のみ可能です。

![screen_shot_2012-04-23at25031pm](assets/screen_shot_2012-04-23at25031pm.png)

タグコンポーネントをダブルクリックすると、タグダイアログボックスが開き、必要に応じて「タグ」からタイトルを変更したり、割り当てられた名前空間を選択したりできます。 このフィールドを編集可能にするには、「**[!UICONTROL 編集ボタンを非表示にする]**」チェックボックスをオフにします。デフォルトでは、タグは編集可能です。

![screen_shot_2012-04-23at24731pm](assets/screen_shot_2012-04-23at24731pm.png)

ユーザーがタグを編集できる場合は、鉛筆アイコンをクリックし、「Tags」ドロップダウンメニューからタグを選択して、タグを追加できます。

![screen_shot_2012-04-23at25150pm](assets/screen_shot_2012-04-23at25150pm.png)

次に、設定済みのタグコンポーネントを示します。

![screen_shot_2012-04-23at25244pm](assets/screen_shot_2012-04-23at25244pm.png)

#### サムネール {#thumbnail}

サムネールコンポーネントでは、選択したサムネールがアセットに表示されます（多くの形式では、サムネールは自動的に抽出されます）。 さらに、コンポーネントではファイル名と、[変更可能なアクション](/help/assets/assets-finder-editor.md#adding-asset-editor-actions)が表示されます。

![screen_shot_2012-04-23at25452pm](assets/screen_shot_2012-04-23at25452pm.png)

サムネールコンポーネントをダブルクリックして、サムネールダイアログを開き、代替テキストを変更できます。 デフォルトでは、サムネールの代替テキストは、「**Click to download asset**」です。

![screen_shot_2012-04-23at25604pm](assets/screen_shot_2012-04-23at25604pm.png)

次に、設定済みのサムネールコンポーネントの例を示します。

![screen_shot_2012-04-23at34815pm](assets/screen_shot_2012-04-23at34815pm.png)

#### タイトル {#title}

タイトルコンポーネントには、アセットのタイトルと説明が表示されます。

デフォルトでは、タイトルは読み取り専用であり、ユーザーは編集できません。編集可能にするには、コンポーネントをダブルクリックし、「**編集ボタンを非表示にする**」チェックボックスをオフにします。さらに、複数のアセットのタイトルを入力します。

![screen_shot_2012-04-23at35100pm](assets/screen_shot_2012-04-23at35100pm.png)

「タイトル」が編集可能な場合は、鉛筆アイコンをクリックして **アセットのプロパティ** ウィンドウ また、日時を選択して、アセットのオンとオフを切り替えることができます。

[!UICONTROL タイトル] を編集する際に、ユーザーは&#x200B;**タイトル**&#x200B;と&#x200B;**説明**&#x200B;を変更し、アセットのオンとオフを切り替える&#x200B;**オンタイム**&#x200B;と&#x200B;**オフタイム**&#x200B;を入力することができます。

![screen_shot_2012-04-23at35241pm](assets/screen_shot_2012-04-23at35241pm.png)

次に、設定済みのタイトルコンポーネントの例を示します。

![chlimage_1-164](assets/chlimage_1-392.png)

#### アセットエディターのアクションを追加 {#adding-asset-editor-actions}

選択したデジタルアセットに対してユーザーが実行できるアクションを、事前定義済みアクションの選択範囲で指定できます。

アセットエディターページにアクションを追加するには：

1. カスタマイズするアセットエディターページで、サイドキックの「**アセットエディター**」をクリックします。

![screen_shot_2012-04-23at35515pm](assets/screen_shot_2012-04-23at35515pm.png)

次のアクションが使用可能です。

| アクション | 説明 |
|---|---|
| [!UICONTROL ダウンロード] | ユーザーが選択したアセットをコンピューターにダウンロードできるようにします。 |
| [!UICONTROL エディター] | ユーザーが画像を編集できるようにします（インタラクティブ編集）。 |
| [!UICONTROL Lightbox] | アセットを「Lightbox」に保存します。Lightbox では、保存されたアセットに対して他のアクションを実行できます。これは、複数のページにまたがるアセットを操作する場合に便利です。 |
| [!UICONTROL ロック] | ユーザーがアセットをロックできるようにします。 この機能はデフォルトでは有効になっておらず、コンポーネントのリストで有効にする必要があります。 |
| [!UICONTROL 参照] | クリックすると、アセットで現在使用されているページが表示されます。 |
| [!UICONTROL バージョン管理] | アセットのバージョンの作成と復元が可能です。 |

1. ページの&#x200B;**アクション**&#x200B;領域に適切なアクションをドラッグします。ページ上にドラッグされたアクションを実行するために使用されるオプションが作成されます。

![chlimage_1-165](assets/chlimage_1-393.png)

## アセットエディターページを使用してアセットをマルチ編集する {#multi-editing-assets-with-the-asset-editor-page}

を使用 [!DNL Experience Manager Assets]を使用すると、複数のアセットを一度に変更できます。 アセットを選択した後、タグとメタデータを同時に変更できます。

アセットエディターページでアセットを複数編集するには：

1. Geometrixxを開く **中央を押す** ページ：
   `https://localhost:4502/content/geometrixx/en/company/press.html`

1. アセットを選択します。

   * Windows の場合：各アセットを `Ctrl + click` します。
   * Mac：各アセットを `Cmd + click` します。

   アセットの範囲を選択するには、最初のアセットをクリックしてから、最後のアセットを `Shift + click` します。

1. クリック **メタデータを編集** （内） **アクション** フィールド（ページの左側の部分）
1. Geometrixx **アセットエディターを中央揃えにする** ページが新しいタブで開きます。 アセットのメタデータが次のように表示されます。

   * すべてのアセットに適用されるのではなく、一部のアセットにのみ適用されるタグが斜体で表示されます。
   * すべてのアセットに適用されるタグは、通常フォントで表示されます。
   * タグ以外のメタデータ：フィールドの値は、選択されたすべてのアセットで同じ場合にのみ表示されます。

1. 「**ダウンロード**」をクリックして、アセットの元のレンディションを含む zip ファイルをダウンロードします。
1. 「**タグ**」フィールドの横にある「タグを編集」オプションをクリックします。

   * すべてのアセットに適用されるのではなく、一部のアセットにのみ適用されるタグは、グレーの背景になります。
   * すべてのアセットに適用されるタグの背景は白です。

   以下の操作を実行できます。

   * `x` をクリックして、すべてのアセットのタグを削除します。
   * `+` をクリックして、すべてのアセットにタグを追加します。
   * 次をクリック： **矢印** タグを選択して、すべてのアセットに新しいタグを追加します。

   クリック **OK** フォームに変更を書き込みます。 横の箱 **タグ** フィールドは自動的にチェックされます。

1. 「説明」フィールドを編集します。例えば、次のように設定します。

   `This is a common description`

   フィールドを編集すると、フォームの送信時に、選択したアセットの既存の値がその値によって上書きされます。

   注意：フィールドを編集すると、「 」フィールドの横にある「 」チェックボックスが自動的にオンになります。

1. クリック **メタデータを更新** をクリックしてフォームを送信し、すべてのアセットの変更を保存します。

   メモ：チェックボックスがオンのメタデータのみが変更されます。
