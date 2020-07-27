---
title: '"チュートリアル：テンプレートの作成"'
seo-title: インタラクティブ通信用の印刷テンプレートと Web テンプレートの作成
description: インタラクティブ通信用の印刷テンプレートと Web テンプレートの作成
seo-description: インタラクティブ通信用の印刷テンプレートと Web テンプレートの作成
uuid: 22256a61-bcf6-4b02-9ee6-0ffb1cc20a6e
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 879ff6ca-e5f3-451d-acc2-f75142101ddd
docset: aem65
translation-type: tm+mt
source-git-commit: bd70508b361ac8b62ebc0344538a18369a075f3e
workflow-type: tm+mt
source-wordcount: '1804'
ht-degree: 66%

---


# チュートリアル：テンプレートの作成{#tutorial-create-templates}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

This tutorial is a step in the [Create your first Interactive Communication](/help/forms/using/create-your-first-interactive-communication.md) series. チュートリアル内のユースケースを理解して実際に操作できるように、このシリーズのチュートリアルを最初から順に学習することをお勧めします。

インタラクティブ通信を作成するには、AEM サーバーに用意されている印刷チャネルと Web チャネル用のテンプレートを入手する必要があります。

印刷チャネルのテンプレートは Adobe Forms Designer で作成されて、AEM サーバーにアップロードされます。これらのテンプレートはインタラクティブ通信を作成する際に使用できるようになります。

Web チャネル用のテンプレートは AEM で作成されます。テンプレートの作成者と管理者は、Web テンプレートの作成、編集、有効化を行うことができます。作成して有効化されたテンプレートは、インタラクティブ通信を作成する際に使用できるようになります。

本チュートリアルは、印刷チャネル用および Web チャネル用のテンプレートの作成方法を順を追って説明します。これにより、作成されたテンプレートは、インタラクティブ通信を作成する際に使用できるようになります。このチュートリアルを完了すると、次の操作を実行できるようになります。

* Adobe Forms Designer を使用して印刷チャネル用の XDP テンプレートを作成する
* XDP テンプレートを AEM Forms サーバーにアップロードする
* Web チャネル用のテンプレートを作成し有効化する

## 印刷チャネル用のテンプレートの作成 {#create-template-for-print-channel}

次のタスクを使用して、インタラクティブ通信の印刷チャネル用のテンプレートの作成と管理を行います。

* [Forms Designer を使用して XDP テンプレートを作成する](../../forms/using/create-templates-print-web.md#create-xdp-template-using-forms-designer)
* [AEM Forms サーバーに XDP テンプレートをアップロードする](../../forms/using/create-templates-print-web.md#upload-xdp-template-to-the-aem-forms-server)
* [レイアウトフラグメント用に XDP テンプレートを作成する](../../forms/using/create-templates-print-web.md#create-xdp-template-for-layout-fragments)

### Forms Designer を使用して XDP テンプレートを作成する {#create-xdp-template-using-forms-designer}

Based on the [use case](/help/forms/using/create-your-first-interactive-communication.md) and [anatomy](/help/forms/using/planning-interactive-communications.md), create the following subforms in the XDP template:

* 請求明細：ドキュメントフラグメントが含まれます
* 顧客の詳細： ドキュメントフラグメントを含む
* 請求書要約： ドキュメントフラグメントを含む
* サマリ： ドキュメントフラグメント（Chargesサブフォーム）とグラフ（Chartsサブフォーム）を含みます
* 呼び出しの項目別： テーブルを含む（レイアウトフラグメント）
* 今すぐ支払う： 画像を含む
* 付加価値サービス： 画像を含む

![create_print_template](assets/create_print_template.gif)

XDP ファイルを Forms サーバーにアップロード後、これらのサブフォームは印刷テンプレートのターゲット領域として表示されます。インタラクティブ通信を作成する際に、ドキュメントフラグメント、グラフ、レイアウトフラグメント、画像などのすべてのエンティティがターゲット領域に追加されます。

印刷チャネル用に XDP テンプレートを作成するには、次の手順を実行します。

1. Open the Forms Designer, select **File** > **New** > **Use a blank form,** tap **Next**, and then tap **Finish** to open the form for template creation.

   「**オブジェクトライブラリ**」および「**オブジェクト**」オプションが **Window** メニューから選択されていることを確認します。

1. **サブフォーム**&#x200B;コンポーネントを&#x200B;**オブジェクトライブラリ**&#x200B;からフォームにドラッグアンドドロップします。
1. 右側のペインの「**オブジェクト**」ウィンドウのサブフォームを表示するには、「サブフォーム」を選択します。
1. Select the **Subform** tab and select **Flowed** from the **Content** drop-down list. 長さを調整するには、サブフォームの左のエンドポイントをドラッグします。
1. 「**連結**」タブで、次の手順を実行します。

   1. Specify **BillDetails** in the **Name** field.

   1. 「**データ連結**」ドロップダウンリストから「**データ連結なし**」を選択します。

   ![Designerサブフォーム](assets/forms_designer_subform_new.png)

1. Similarly, select the root subform, select the **Subform** tab, and select **Flowed** from the **Content** drop-down list. 「**連結**」タブで、次の手順を実行します。

   1. Specify **TelecaBill** in the **Name** field.

   1. 「**データ連結**」ドロップダウンリストから「**データ連結なし**」を選択します。

   ![印刷テンプレートのサブフォーム](assets/root_subform_print_template_new.png)

1. 手順 2～5 を繰り返し、次のサブフォームを作成します。

   * BillDetails
   * CustomerDetails
   * BillSummary
   * Summary - Select the **Subform** tab and select **Positioned** from the **Content** drop-down list for this subform. 次のサブフォームを&#x200B;**概要**&#x200B;サブフォームに挿入します。

      * 料金
      * グラフ
   * ItemisedCalls
   * PayNow
   * ValueAddedServices

   時間を節約するには、既存のサブフォームをコピー＆ペーストして新しいサブフォームを作成することもできます。

   To shift the **Charts** subform to the right of the Charges subform, select the **Charts** subform from the left pane, select the **Layout** tab, and specify a value for **AnchorX** field. 指定する値は、**料金**&#x200B;サブフォームの「**幅**」フィールドの値よりも大きい値である必要があります。Select the **Charges** subform and select the **Layout** tab to view the value of the **Width** field.

1. **テキスト**&#x200B;オブジェクトを、**オブジェクトライブラリ**&#x200B;からフォームにドラッグアンドドロップし、ボックスに **Dial XXXX to subscribe** とテキストを入力します。
1. Right-click the text object in the left pane, select **Rename Object**, and enter the name of the text object as **Subscribe**.

   ![XDPテンプレート](assets/print_xdp_template_subform_new.png)

1. ローカルのファイルシステムにファイルを保存するには、「**ファイル**／**名前を付けて保存**」を選択して、次の手順を実行します。

   1. ファイルを保存する場所に移動し、**create_first_ic_print_template** と名前を指定します。
   1. 「**ファイルの種類**」ドロップダウンリストから&#x200B;**.xdp** を選択します。

   1. 「**保存**」をタップします。

### AEM Forms サーバーに XDP テンプレートをアップロードする {#upload-xdp-template-to-the-aem-forms-server}

Forms Designer を使用して XDP テンプレートの作成が終わったら、AEM Forms サーバーにアップロードする必要があります。これにより、作成されたテンプレートは、インタラクティブ通信を作成する際に使用できるようになります。

1. **[!UICONTROL フォーム]**／**[!UICONTROL フォームとドキュメント]**&#x200B;を選択します。
1. **作成**／**ファイルのアップロード**&#x200B;の順にタップします。

   Navigate and select the **create_first_ic_print_template** template (XDP) and tap **Open** to import the XDP template to the AEM Forms server.

### レイアウトフラグメント用に XDP テンプレートを作成する {#create-xdp-template-for-layout-fragments}

インタラクティブ通信の印刷チャネル用のレイアウトフラグメントを作成するには、Forms Designer を使用して XDP を作成し、AEM Forms サーバーにアップロードします。

1. Open the Forms Designer, select **File** > **New** > **Use a blank form,** tap **Next**, and then tap **Finish** to open the form for template creation.

   「**オブジェクトライブラリ**」および「**オブジェクト**」オプションが **Window** メニューから選択されていることを確認します。

1. Drag-and-drop the **Table** component from the **Object Library** to the form.
1. テーブルの挿入ダイアログで、次の手順を実行します。

   1. 列数を **5** と指定します。
   1. ボディ行数を **1** と指定します。
   1. 「**テーブルにヘッダー行を含む**」チェックボックスを選択します。
   1. 「**OK**」をタップします。

1. **テーブル** 1 の隣の左側のペインで「**+**」をタップし、**Cell1** を右クリックし、「**オブジェクト名の変更**」を「**日付**」に選択します。

   同様に、**Cell2**、**Cell3**、**Cell4**&#x200B;および&#x200B;**Cell5** の名前をそれぞれ&#x200B;**時刻**、**番号**、**時間**&#x200B;および&#x200B;**料金**&#x200B;に変更します。

1. **Designer表示の「Header」テキストフィールドをクリックし、** Time **、Number** Duration、Duration、Charges Charges **Charges********** Headerという名前に変更します。

   ![レイアウトフラグメント](assets/layout_fragment_print_new.png)

1. 左側のペインから&#x200B;**Row 1** を選択し、「**オブジェクト**／**連結**／**各データアイテムについて行を繰り返す**」を選択します。

   ![レイアウトフラグメントに対してプロパティを繰り返す](assets/layout_fragment_print_repeat_new.png)

1. Drag-and-drop the **Text Field** component from the **Object Library** to the **Designer View**.

   ![レイアウトフラグメントのテキストフィールド](assets/layout_fragment_print_text_field_new.png)

   同様に、**テキストフィールド**&#x200B;コンポーネントを&#x200B;**時刻**、**番号**、**時間**&#x200B;および&#x200B;**料金**&#x200B;行にドラッグアンドドロップします。

1. ローカルのファイルシステムにファイルを保存するには、「**ファイル**／**名前を付けて保存**」を選択して、次の手順を実行します。

   1. Navigate to the location to save the file and specify the name as **table_lf**.
   1. 「**ファイルの種類**」ドロップダウンリストから&#x200B;**.xdp** を選択します。

   1. 「**保存**」をタップします。
   Forms Designer を使用してレイアウトフラグメント用 XDP テンプレートの作成が終わったら、AEM Forms サーバーに[アップロード](../../forms/using/create-templates-print-web.md#upload-xdp-template-to-the-aem-forms-server)する必要があります。これにより、作成されたテンプレートは、レイアウトフラグメントを作成する際に使用できるようになります。

## Web チャネル用テンプレートの作成 {#create-template-for-web-channel}

次のタスクを使用して、インタラクティブ通信の Web チャネル用のテンプレートの作成と管理を行います。

* [テンプレート用フォルダーの作成](../../forms/using/create-templates-print-web.md#create-folder-for-templates)
* [テンプレートの作成](../../forms/using/create-templates-print-web.md#create-the-template)
* [テンプレートの有効化](../../forms/using/create-templates-print-web.md#enable-the-template)
* [インタラクティブ通信でボタンの有効化](../../forms/using/create-templates-print-web.md#enabling-buttons-in-interactive-communications)

### テンプレート用フォルダーの作成 {#create-folder-for-templates}

Web チャネルテンプレートを作成するには、作成したテンプレートを保存できるフォルダーを定義します。フォルダー内にテンプレートを作成したら、そのテンプレートを有効にする必要があります。これにより、フォームユーザーがそのテンプレートを使用して、インタラクティブ通信の Web チャネルを作成できるようになります。

編集可能なテンプレート用のフォルダーを作成するには、次の手順を実行します。

1. Tap **Tools** ![hammer-icon](assets/hammer-icon.svg) > **Configuration Browser**.
1. In the Configuration Browser page, tap **Create**.
1. In the **Create Configuration** dialog, specify **Create_First_IC_templates** as the title for the folder, check **Editable Templates**, and tap **Create**.

   ![Webテンプレートの設定](assets/create_first_ic_web_template_new.png)

   The **Create_First_IC_templates** folder is created and listed on the **Configuration Browser** page.

### テンプレートの作成 {#create-the-template}

Based on the [use case](/help/forms/using/create-your-first-interactive-communication.md) and [anatomy](/help/forms/using/planning-interactive-communications.md), create the following panels in the Web template:

* 請求明細：ドキュメントフラグメントが含まれます
* 顧客の詳細： ドキュメントフラグメントを含む
* 請求書要約： ドキュメントフラグメントを含む
* 料金の概要： ドキュメントフラグメントとグラフを含みます（2列レイアウト）
* 呼び出しの項目別： テーブルを含む
* Pay Now: Includes a **Pay Now** button and an image
* Value Added Services: Includes an image and a **Subscribe** button.

![create_web_template](assets/create_web_template.gif)

ドキュメントフラグメント、グラフ、テーブル、画像、ボタンなどのすべてのエンティティが、インタラクティブ通信を作成する際に追加されます。

**Create_First_IC_templates** フォルダーでWeb チャネル用のテンプレートを作成するには、次の手順を実行します。

1. Navigate to the appropriate template folder by selecting **Tools** > **Templates** > **Create_First_IC_templates** folder.
1. 「**作成**」をタップします。
1. On the **Pick a Template Type** configuration wizard, select **Interactive Communication - Web Channel** and tap **Next**.
1. On the **Template Details** configuration wizard, specify **Create_First_IC_Web_Template** as the template title. オプション内容を指定し、「**作成**」をタップします。

   A confirmation message that the **Create_First_IC_Web_Template** is displayed.

1. 「**開く**」をタップして、テンプレートエディターでテンプレートを開きます。
1. 「**プレビュー**」オプションの隣にあるドロップダウンリストから「**初期コンテンツ**」を選択します。

   ![テンプレートエディター](assets/template_editor_initial_content_new.png)

1. Tap **Root Panel** and then tap **+** to view the list of components that you can add to the template.
1. コンポーネントの一覧から、**ルートパネル**&#x200B;の上に追加する「**パネル**」を選択します。
1. 左側のペインで「**コンテンツ**」タブを選択します。手順 8 で追加された新しいパネルは、コンテンツツリーの&#x200B;**ルートパネル**&#x200B;の下に表示されます。

   ![コンテンツツリー](assets/content_tree_root_panel_new.png)

1. パネルを選択し、 ![configure_icon](assets/configure_icon.png) （設定）をタップします。
1. プロパティペインで、次の手順を実行します。

   1. 「名前」フィールドに&#x200B;**billdetails** と入力します。
   1. 「タイトル」フィールドに、**請求明細**&#x200B;と入力します。
   1. 「**列数**」ドロップダウンリストから、**1** を選択します。

   1. Tap ![](/help/forms/using/assets/done_icon.png) to save the properties.

   コンテンツツリーの&#x200B;**請求明細**&#x200B;に更新パネル名が更新されます。

1. 手順 7～11 を繰り返し、次のプロパティを含むパネルをテンプレートに追加します。

   | 名前 | タイトル | 列数 |
   |---|---|---|
   | customerdetails | 顧客情報 | 1 |
   | billsummary | 請求内容 | 1 |
   | summarycharges | 請求概要 | 2 |
   | itemisedcalls | 通話明細 | 1 |
   | paynow | Pay Now | 2 |
   | vas | 付加価値サービス | 1 |

   次の画像は、すべてのパネルがテンプレートに追加された後のコンテンツツリーを示しています。

   ![すべてのパネルのコンテンツツリー](assets/content_tree_all_panels_new.png)

### テンプレートの有効化 {#enable-the-template}

Web テンプレートの作成が終わったら、インタラクティブ通信を作成する際に、そのテンプレートを有効にする必要があります。

Web テンプレートを有効にするには、次の手順を実行します。

1. Tap **Tools** ![hammer-icon](assets/hammer-icon.svg) > **Templates**.
1. Navigate to the **Create_First_IC_Web_Template** template, select it, and tap **Enable**.
1. 再度「**有効**」をタップして確認します。

   これでテンプレートが有効になり、テンプレートのステータスとして「有効」が表示されます。このテンプレートは、Web チャネル用のインタラクティブ通信を作成する際に使用できます。

### インタラクティブ通信でボタンの有効化 {#enabling-buttons-in-interactive-communications}

ユースケースに基づき、「**Pay Now**」および「**登録**」ボタン（アダプティブフォームコンポーネント）をインタラクティブ通信に含める必要があります。インタラクティブ通信でこれらのボタンの仕様を有効にするには、次の手順を実行します。

1. Select **Structure** from the drop-down list next to the **Preview** option.
1. コンテンツツリーを使用して、**ドキュメントコンテナ**&#x200B;ルートパネルを選択し、「**ポリシー**」をタップして、インタラクティブ通信で使用が許可されているコンポーネントを選択します。

   ![ポリシーの設定](assets/structure_configure_policy_new.png)

1. 「**プロパティ**」セクションの「**許可されているコンポーネント**」タブで、**アダプティブフォーム**&#x200B;コンポーネントから「**ボタン**」を選択します。

   ![許可されたコンポーネント](assets/allowed_components_af_new.png)

1. Tap ![done_icon](assets/done_icon.png) to save the properties.