---
title: 「チュートリアル：インタラクティブ通信の作成 」
description: すべての構築ブロックを使ってインタラクティブ通信を作成する
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Interactive Communication
exl-id: aaacee66-6bbe-498b-91b1-3a9545ff1aeb
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1884'
ht-degree: 100%

---

# チュートリアル：インタラクティブ通信の作成 {#tutorial-create-interactive-communication}

![09-style-your-adaptive-form-small](assets/09-style-your-adaptive-form-small.png)

これは、「[最初のインタラクティブ通信の作成](/help/forms/using/create-your-first-interactive-communication.md)」シリーズを構成するチュートリアルです。チュートリアルの使用例全体を理解、実行、デモするために、シリーズを時系列に沿って実施することをお勧めします。

フォームデータモデル、ドキュメントフラグメント、テンプレート、web 版用のテーマなどのすべての構築ブロックの作成が終わったら、インタラクティブ通信の作成を開始できます。

インタラクティブ通信は、印刷チャネルと web チャネルという 2 つのチャネルを使用して配信することができます。また、印刷チャネルをメインとしてインタラクティブ通信を作成することも可能です。印刷チャネルを web チャネルのメインとして使用すると、web チャネルに連結されたコンテンツ、継承設定、データが印刷チャネルから取得されます。また、印刷チャネルで加えられた変更が web チャネルでも同期されるようにします。ただし、インタラクティブ通信の作成者は、web チャネル内の特定のコンポーネントの継承設定を解除することができます。

このチュートリアルは、印刷版および web 版のインタラクティブ通信の作成方法を順を追って説明します。このチュートリアルを完了すると、次の操作を実行できるようになります。

* 印刷チャネル用のインタラクティブ通信を作成
* Web チャネル用のインタラクティブ通信を作成
* 印刷をメインとする印刷版および web 版インタラクティブ通信を作成

## 同期なしでの印刷版および web 版のインタラクティブ通信を作成 {#create-interactive-communications-for-print-and-web-with-no-synchronization}

### 印刷チャネル用のインタラクティブ通信を作成 {#create-interactive-communication-for-print-channel}

以下は、このチュートリアル内で既に作成済みで、印刷チャネル用のインタラクティブ通信を作成する際に必要になるリソース一覧です。

**印刷テンプレート：** [create_first_ic_print_template](../../forms/using/create-templates-print-web.md)

**フォームデータモデル：**[FDM_Create_First_IC](../../forms/using/create-form-data-model0.md)

**ドキュメントフラグメント：** [bill_details_first_ic、customer_details_first_ic、bill_summary_first_ic、summary_charges_first_ic](../../forms/using/create-document-fragments.md)

**レイアウトフラグメント：**[table_lf](../../forms/using/create-templates-print-web.md)

**画像：** PayNow および ValueAddedServices

1. AEM オーサーインスタンスにログインし、**[!UICONTROL Adobe Experience Manager]**／**[!UICONTROL フォーム]**／**[!UICONTROL フォームとドキュメント]**&#x200B;に移動します。
1. 「**作成**」を選択し、「**インタラクティブ通信**」を選択します。**インタラクティブ通信の作成**&#x200B;ウィザードが表示されます。
1. 「**タイトル**」と「**名前**」フィールドに **create_first_ic** と入力します。**FDM_Create_First_IC** をフォームデータモデルとして選択し、「**次へ**」を選択します。
1. **チャンネル**&#x200B;ウィザードで以下を実行します。

   1. **create_first_ic_print_template** を印刷テンプレートとして指定し、「**選択**」を選択します。「**Web チャンネルのメインとして印刷を使用**」のチェックボックスが選択されていないことを確認してください。

   1. **Create_First_IC_templates** フォルダー／**Create_First_IC_Web_Template** を web テンプレートとして指定し、「**選択**」を選択します。

   1. 「**作成**」を選択します。

   インタラクティブ通信が正常に作成されたことを通知する確認メッセージが表示されます。

1. 「**編集**」を選択し、右側のパネルでインタラクティブ通信を開きます。
1. 「**アセット**」タブに移動してフィルターを適用し、左側のペインのドキュメントフラグメントだけを表示します。
1. 以下のドキュメントフラグメントをインタラクティブ通信のターゲット領域にドラッグ＆ドロップします。

   | ドキュメントフラグメント | ターゲット領域 |
   |---|---|
   | bill_details_first_ic | BillDetails |
   | customer_details_first_ic | CustomerDetails |
   | bill_summary_first_ic | BillSummary |
   | summary_charges_first_interactive_communication | 料金 |

   ![インタラクティブ通信用のドキュメントフラグメント](assets/create_first_ic_doc_fragments_new.png)

1. **グラフ**&#x200B;のターゲット領域を選択し、「**+**」を選択して&#x200B;**グラフ**&#x200B;のコンポーネントを追加します。
1. グラフのコンポーネントを選択し、![configure_icon](assets/configure_icon.png)（設定）を選択します。グラフのプロパティが左側のパネルに表示されます。

   1. グラフ名を指定します。
   1. 「**グラフのタイプ**」ドロップダウンリストから「**円グラフ**」を選択します。
   1. **X 軸**&#x200B;セクションの&#x200B;**通話**&#x200B;データモデルオブジェクトタイプから **Calltype** プロパティを選択します。![done_icon](assets/done_icon.png) を選択します。
   1. 「**関数**」ドロップダウンリストから「**頻度**」を選択します。
   1. **Y 軸**&#x200B;セクションの&#x200B;**通話**&#x200B;データモデルオブジェクトタイプから **Calltype** プロパティを選択します。![done_icon](assets/done_icon.png) を選択します。
   1. ![done_icon](assets/done_icon.png) を選択して、グラフのプロパティを保存します。

1. 「**アセット**」タブに移動してフィルターを適用し、左側のペインのレイアウトフラグメントだけを表示します。**table_lf** レイアウトフラグメントを&#x200B;**通話明細**&#x200B;のターゲット領域にドラッグアンドドロップします。
1. 「**日付**」列のテキストフィールドを選択し、![configure_icon](assets/configure_icon.png)（設定）を選択します。
1. 「**連結タイプ**」ドロップダウンリストから「**データモデルオブジェクト**」を選択し、**calls**／**calldate** の順に選択します。![done_icon](assets/done_icon.png) を選択してプロパティを保存します。

   同様に、**時刻**、**番号**、**時間**、および&#x200B;**料金**&#x200B;のテキストフィールドについて、それぞれ **calltime**、**callnumber**、**callduration**、および **callcharges** との連結を作成します。

1. **Pay Now** のターゲット領域を選択し、「**+**」を選択して&#x200B;**画像**&#x200B;のコンポーネントを追加します。
1. 画像のコンポーネントを選択し、![configure_icon](assets/configure_icon.png)（設定）を選択します。画像のプロパティが左側のパネルに表示されます。

   1. 「**名前**」フィールドで、**PayNow** を画像の名前として指定します。
   1. 「**アップロード**」を選択し、ローカルのファイルシステムに保存された画像を選択して「**開く**」を選択します。
   1. ![done_icon](assets/done_icon.png) を選択して、画像のプロパティを保存します。

1. 手順 13～14 を繰り返し、**ValueAddedServices** の画像を **ValueAddedServices** のターゲット領域に追加します。

### Web チャネル用インタラクティブ通信を作成 {#create-interactive-communication-for-web-channel}

以下は、このチュートリアル内で既に作成済みで、web チャネル用のインタラクティブ通信を作成する際に必要になるリソース一覧です。

**Web テンプレート：** [Create_First_IC_Web_Template](../../forms/using/create-templates-print-web.md)

**フォームデータモデル：** [FDM_Create_First_IC](../../forms/using/create-form-data-model0.md)

**ドキュメントフラグメント：** [bill_details_first_ic、customer_details_first_ic、bill_summary_first_ic、summary_charges_first_ic](../../forms/using/create-document-fragments.md)

**画像：** PayNowWeb および ValueAddedServicesWeb

1. AEM オーサーインスタンスにログインし、**[!UICONTROL Adobe Experience Manager]**／**[!UICONTROL フォーム]**／**[!UICONTROL フォームとドキュメント]**&#x200B;に移動します。
1. 「**作成**」を選択し、「**インタラクティブ通信**」を選択します。**インタラクティブ通信の作成**&#x200B;ウィザードが表示されます。
1. 「**タイトル**」と「**名前**」フィールドに **create_first_ic** と入力します。**FDM_Create_First_IC** をフォームデータモデルとして選択し、「**次へ**」を選択します。
1. **チャンネル**&#x200B;ウィザードで以下を実行します。

   1. **create_first_ic_print_template** を印刷テンプレートとして指定し、「**選択**」を選択します。「**Web チャンネルのメインとして印刷を使用**」のチェックボックスが選択されていないことを確認してください。

   1. **Create_First_IC_templates** フォルダー／**Create_First_IC_Web_Template** を web テンプレートとして指定し、「**選択**」を選択します。

   1. 「**作成**」を選択します。

   インタラクティブ通信が正常に作成されたことを通知する確認メッセージが表示されます。

1. 「**編集**」を選択し、右側のパネルでインタラクティブ通信を開きます。
1. 左側のパネルから「**チャネル**」タブを選択し、「**Web**」を選択します。
1. 「**アセット**」タブに移動してフィルターを適用し、左側のペインのドキュメントフラグメントだけを表示します。
1. 以下のドキュメントフラグメントをインタラクティブ通信のターゲット領域にドラッグ＆ドロップします。

   | ドキュメントフラグメント | ターゲット領域 |
   |---|---|
   | bill_details_first_ic | BillDetails |
   | customer_details_first_ic | CustomerDetails |
   | bill_summary_first_ic | BillSummary |
   | summary_charges_first_interactive_communication | 料金 |

1. **請求概要**&#x200B;のターゲット領域を選択し、**+** を選択して&#x200B;**グラフ**&#x200B;のコンポーネントを追加します。
1. グラフのコンポーネントを選択し、![configure_icon](assets/configure_icon.png)（設定）を選択します。グラフのプロパティが左側のパネルに表示されます。

   1. グラフ名を指定します。
   1. 「**グラフのタイプ**」ドロップダウンリストから「**円グラフ**」を選択します。

   1. **X 軸**&#x200B;セクションの&#x200B;**通話**&#x200B;データモデルオブジェクトタイプから **Calltype** プロパティを選択します。![done_icon](assets/done_icon.png) を選択します。

   1. 「**関数**」ドロップダウンリストから「**頻度**」を選択します。

   1. **Y 軸**&#x200B;セクションの&#x200B;**通話**&#x200B;データモデルオブジェクトタイプから **Calltype** プロパティを選択します。![done_icon](assets/done_icon.png) を選択します。

   1. ![done_icon](assets/done_icon.png) を選択して、グラフのプロパティを保存します。

1. 左側のペインから「**データソース**」タブを選択し、**通話**&#x200B;データモデルオブジェクトを&#x200B;**通話明細**&#x200B;のターゲット領域にドラッグアンドドロップします。**通話**&#x200B;データモデルオブジェクトに含まれるすべてのプロパティが、右側のペインの&#x200B;**通話明細**&#x200B;のターゲット領域にテーブル列として表示されます。

   ユースケースに基づいて、テーブルには、通話日、通話時刻、通話番号、通話時間、そして通話料金の列が必要です。

   ![インタラクティブ通信用テーブル](assets/table_ic_web_new.png)

1. **Mobilenum** テーブルの列見出しを選択し、**追加のオプション**／**列の削除**&#x200B;の順に選択します。同様に、**Calltype** の列を削除します。
1. **Calldate** テーブル列見出しを選択し、「![編集](assets/edit.png)」を選択してテキストの名前を「**通話日**」に変更します。同様に、テーブル内の他の列見出しの名前を変更します。
1. ユースケースに基づき、「**今すぐ支払う**」ボタンをインタラクティブ通信に挿入し、ユーザーがボタンをクリックして支払いを行えるようにします。ボタンを挿入するには、次の手順を実行します。

   1. **今すぐ支払う**&#x200B;のターゲット領域を選択し、**+** を選択して&#x200B;**テキスト**&#x200B;コンポーネントを追加します。

   1. テキストコンポーネントを選択し、「![編集](assets/edit.png)」を選択します。
   1. テキストの名前を「**今すぐ支払う**」に変更します。
   1. テキストを選択し、ハイパーリンクアイコンを選択します。
   1. 「**パス**」フィールドで支払い URL を指定します。
   1. **ターゲット**&#x200B;ドロップダウンリストから「**新規タブ**」を選択します。

   1. ![done_icon](assets/done_icon.png) を選択して、ハイパーリンクのプロパティを保存します。

1. 「**プレビュー**」オプションの隣にあるドロップダウンリストから「**スタイル**」を選択します。

   ![インタラクティブ通信のスタイルモードを選択](assets/select_style_ic_web_new.png)

1. ハイパーリンクテキストのスタイルを設定し、インタラクティブ通信でボタンとして表示するには次の手順を実行します。

   1. テキストコンポーネントを選択し、「![編集](assets/edit.png)」を選択します。
   1. 「**境界線**」セクションで、**境界線の幅**&#x200B;を **1.5px** に指定します。**境界線のスタイル**&#x200B;として&#x200B;**実線**&#x200B;を選択し、**境界線の半径**&#x200B;を **46px** に指定します。

   1. 「**背景**」セクションから、ボタンの背景色に赤を選択します。
   1. 「**寸法と位置**」セクションの「**余白**」フィールドで、「**同時に編集**」アイコンを選択して、**右**&#x200B;の余白を **450px** に設定します。上、下、左のフィールドは空白に設定されます。

   ![インタラクティブ通信にハイパーリンクを挿入](assets/ic_web_hyperlink_new.png)

1. **今すぐ支払う**&#x200B;のターゲット領域を選択し、**+** を選択して&#x200B;**画像**&#x200B;コンポーネントを追加します。
1. 画像コンポーネントを選択し、![configure_icon](assets/configure_icon.png)（設定）を選択します。画像のプロパティが左側のパネルに表示されます。

   1. 「**名前**」フィールドで、「**PayNow**」を画像の名前として指定します。

   1. 「**アップロード**」を選択し、ローカルのファイルシステムに保存された **PayNowWeb** の画像を選択して「**開く**」を選択します。

   1. ![done_icon](assets/done_icon.png) を選択して、画像のプロパティを保存します。

1. ユースケースに基づき、「**登録**」ボタンをインタラクティブ通信に挿入し、ユーザーがボタンをクリックして付加価値サービスを追加できるようにします。

   手順 13～17 を繰り返し、**付加価値サービス** ターゲット領域に「**登録**」ボタンを追加し、**ValueAddedServicesWeb**&#x200B;画像を追加します。

## 自動同期での印刷版および web 版のインタラクティブ通信の作成 {#create-interactive-communications-for-print-and-web-with-auto-synchronization}

インタラクティブ通信は、印刷チャネルと web チャネル間の自動同期を有効化することでも作成できます。自動同期を有効にするには、インタラクティブ通信の作成時に印刷チャネルをマスターとして選択します。印刷チャネルをマスターとして選択すると、web チャネルに連結されたコンテンツ、継承設定、データが印刷チャネルから取得されます。また、印刷チャネルに対する変更内容が web チャネルに反映されます。

印刷チャネルを使って web チャネルのコンテンツを取得するには、次の手順に従います。

1. AEM オーサーインスタンスにログインし、**[!UICONTROL Adobe Experience Manager]**／**[!UICONTROL フォーム]**／**[!UICONTROL フォームとドキュメント]**&#x200B;に移動します。
1. 「**作成**」を選択し、「**インタラクティブ通信**」を選択します。**インタラクティブ通信の作成**&#x200B;ウィザードが表示されます。
1. 「**タイトル**」と「**名前**」フィールドに **create_first_ic** と入力します。**FDM_Create_First_IC** をフォームデータモデルとして選択し、「**次へ**」を選択します。
1. **チャネル**&#x200B;ウィザードで以下を実行します。

   1. **create_first_ic_print_template** を印刷テンプレートとして指定し、「**選択**」を選択します。

   1. 「**Web チャネルのマスターとして印刷を使用**」チェックボックスを選択します。
   1. **Create_First_IC_templates** フォルダー／**Create_First_IC_Web_Template** を web テンプレートとして指定し、「**選択**」を選択します。

   1. 「**作成**」を選択します。

   インタラクティブ通信が正常に作成されたことを通知する確認メッセージが表示されます。

1. 「**編集**」を選択し、右側のパネルでインタラクティブ通信を開きます。
1. 「[印刷チャネル用のインタラクティブ通信の作成](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-print-channel)」セクションの手順 6～15 を実行します。
1. 左側のパネルから「**チャネル**」タブを選択し、「**Web**」を選択し、印刷チャネルから web チャネル用にコンテンツを自動生成します。
1. 手順 4 で「**Web チャネルのマスターとして印刷を使用**」のチェックボックスを選択したので、コンテンツと連結は印刷チャネルから Web チャネル用に自動生成されます。

   印刷チャネルのコンテンツは web チャネルのテンプレートコンテンツの下に挿入されます。印刷チャネルから自動生成された web チャネルのコンテンツを変更するには、どのターゲット領域の継承もキャンセルできます。

   Web チャネル内の関連するターゲット領域にポインタを合わせて、![cancelinheritance](assets/cancelinheritance.png)（継承をキャンセル）を選択し、**継承をキャンセル**&#x200B;ダイアログで「**はい**」を選択します。

   ![継承のキャンセル](assets/cancel_inheritance_web_channel_new.png)

   コンポーネントの継承をキャンセルした場合は、その継承を再度有効にすることができます。継承をもう一度有効にするには、目的のコンポーネントが含まれているターゲット領域の境界線にポインタを合わせて ![reenableinheritance](assets/reenableinheritance.png) を選択します。

1. 左側のパネルで「**コンテンツ**」タブを選択します。
1. 自動生成された web チャネルコンテンツを、コンテンツツリーを使用して web テンプレートの既存のパネルにドラッグ＆ドロップします。以下は配置を調節する必要があるコンポーネントの一覧です。

   * 請求明細コンポーネントを請求明細パネルに
   * 顧客情報コンポーネントを顧客情報パネルに
   * 請求概要コンポーネントを請求概要パネルに
   * 請求概要コンポーネントを請求概要パネルに
   * レイアウトフラグメント（テーブル）を通話明細パネルに

   ![Web コンテンツツリー](assets/ic_web_content_tree_new.png)

1. 「[Web チャネル用インタラクティブ通信の作成](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-web-channel)」の手順 13 ～ 18 を繰り返し、「**Pay Now**」（今すぐ支払う）および「**登録**」ハイパーリンクをインタラクティブ通信の Web チャネルに挿入します。
