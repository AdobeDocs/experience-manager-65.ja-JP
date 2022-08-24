---
title: 「チュートリアル：インタラクティブ通信の作成 」
seo-title: Create an Interactive Communication for Print and Web
description: すべての構築ブロックを使ってインタラクティブ通信を作成する
seo-description: Create an Interactive Communication using all building blocks
uuid: 5ffaa86f-87c7-4673-8b41-63ec61421be2
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ac5d8d4f-fc13-4e8d-819c-c5db07fa6870
docset: aem65
feature: Interactive Communication
exl-id: aaacee66-6bbe-498b-91b1-3a9545ff1aeb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2004'
ht-degree: 100%

---

# チュートリアル：インタラクティブ通信の作成 {#tutorial-create-interactive-communication}

![09-style-your-adaptive-form-small](assets/09-style-your-adaptive-form-small.png)

これは、「[最初のインタラクティブ通信の作成](/help/forms/using/create-your-first-interactive-communication.md)」シリーズを構成するチュートリアルです。チュートリアル内のユースケースを理解して実際に操作できるように、このシリーズのチュートリアルを最初から順に学習することをお勧めします。

フォームデータモデル、ドキュメントフラグメント、テンプレート、Web 版用のテーマなどのすべての構築ブロックの作成が終わったら、インタラクティブ通信の作成を開始できます。

インタラクティブ通信は、印刷チャネルと Web チャネルという 2 つのチャネルを使用して配信することができます。また、印刷チャネルをマスターとしてインタラクティブ通信を作成することも可能です。印刷チャネルを Web チャネルのマスターとして使用すると、Web チャネルに連結されたコンテンツ、継承設定、データが印刷チャネルから取得されます。また、印刷チャネルで加えられた変更が Web チャネルでも同期されるようにします。ただし、インタラクティブ通信の作成者は、Web チャネル内の特定のコンポーネントの継承設定を解除することができます。

本チュートリアルは、印刷版および Web 版のインタラクティブ通信の作成方法を順を追って説明します。このチュートリアルを完了すると、次の操作を実行できるようになります。

* 印刷チャネル用のインタラクティブ通信の作成
* Web チャネル用のインタラクティブ通信の作成
* 印刷をマスターとする印刷版および Web 版インタラクティブ通信の作成

## 同期なしでの印刷版および Web 版のインタラクティブ通信の作成 {#create-interactive-communications-for-print-and-web-with-no-synchronization}

### 印刷チャネル用のインタラクティブ通信の作成 {#create-interactive-communication-for-print-channel}

以下は、本チュートリアル内で既に作成済みで、印刷チャネル用のインタラクティブ通信を作成する際に必要になるリソース一覧です。

**印刷テンプレート：** [create_first_ic_print_template](../../forms/using/create-templates-print-web.md)

**フォームデータモデル：**[FDM_Create_First_IC](../../forms/using/create-form-data-model0.md)

**ドキュメントフラグメント：** [bill_details_first_ic、customer_details_first_ic、bill_summary_first_ic、summary_charges_first_ic](../../forms/using/create-document-fragments.md)

**レイアウトフラグメント：** [table_lf](../../forms/using/create-templates-print-web.md)

**画像：** PayNow および ValueAddedServices

1. AEM オーサーインスタンスにログインし、**[!UICONTROL Adobe Experience Manager]**／**[!UICONTROL フォーム]**／**[!UICONTROL フォームとドキュメント]**&#x200B;に移動します。
1. 「**作成**」をタップし、「**インタラクティブ通信**」を選択します。**インタラクティブ通信の作成**&#x200B;ウィザードが表示されます。
1. 「**タイトル**」と「**名前**」フィールドに **create_first_ic** と入力します。**FDM_Create_First_IC** をフォームデータモデルとして選択し、「**次へ**」をタップします。
1. **チャンネル**&#x200B;ウィザードで以下を実行します。

   1. **create_first_ic_print_template** を印刷テンプレートとして指定し、「**選択**」をタップします。「**Web チャンネルのマスターとして印刷を使用**」のチェックボックスが選択されていないことを確認してください。

   1. **Create_First_IC_templates** フォルダー／**Create_First_IC_Web_Template** を Web テンプレートとして指定し、「**選択**」をタップします。

   1. 「**作成**」をタップします。

   インタラクティブ通信が正常に作成されたことを通知する確認メッセージが表示されます。

1. 「**編集**」をタップし、右側のペインでインタラクティブ通信を開きます。
1. 「**アセット**」タブに移動してフィルターを適用し、左側のペインのドキュメントフラグメントだけを表示します。
1. 以下のドキュメントフラグメントをインタラクティブ通信のターゲット領域にドラッグアンドドロップします。

   | ドキュメントフラグメント | ターゲット領域 |
   |---|---|
   | bill_details_first_ic | BillDetails |
   | customer_details_first_ic | CustomerDetails |
   | bill_summary_first_ic | BillSummary |
   | summary_charges_first_interactive_communication | 料金 |

   ![インタラクティブ通信用のドキュメントフラグメント](assets/create_first_ic_doc_fragments_new.png)

1. **グラフ**&#x200B;のターゲット領域をタップし、**+** をタップして&#x200B;**グラフ**&#x200B;のコンポーネントを追加します。
1. グラフのコンポーネントをタップし、![configure_icon](assets/configure_icon.png)（設定）を選択します。グラフのプロパティが左側のペインに表示されます：

   1. グラフ名を指定します。
   1. 「**グラフのタイプ**」ドロップダウンリストから「**円グラフ**」を選択します。
   1. **X 軸**&#x200B;セクションの&#x200B;**通話**&#x200B;データモデルオブジェクトタイプから **Calltype** プロパティを選択します。![done_icon](assets/done_icon.png) をタップします。
   1. 「**関数**」ドロップダウンリストから「**頻度**」を選択します。
   1. **Y 軸**&#x200B;セクションの&#x200B;**通話**&#x200B;データモデルオブジェクトタイプから **Calltype** プロパティを選択します。![done_icon](assets/done_icon.png) をタップします。
   1. ![done_icon](assets/done_icon.png) をタップして、グラフのプロパティを保存します。

1. 「**アセット**」タブに移動してフィルターを適用し、左側のペインのレイアウトフラグメントだけを表示します。**table_lf** レイアウトフラグメントを&#x200B;**通話明細**&#x200B;のターゲット領域にドラッグアンドドロップします。
1. 「**日付**」列のテキストフィールドを選択し、![configure_icon](assets/configure_icon.png)（設定）をタップします。
1. 「**連結タイプ**」ドロップダウンリストから「**データモデルオブジェクト**」を選択し、**calls**／**calldate** の順に選択します。![done_icon](assets/done_icon.png) をタップしてプロパティを保存します。

   同様に、**時刻**、**番号**、**時間**、および&#x200B;**料金**&#x200B;のテキストフィールドについて、それぞれ **calltime**、**callnumber**、**callduration**、および **callcharges** との連結を作成します。

1. **PayNow** のターゲット領域をタップし、**+** をタップして&#x200B;**画像**&#x200B;のコンポーネントを追加します。
1. 画像のコンポーネントをタップし、![configure_icon](assets/configure_icon.png)（設定）を選択します。画像のプロパティが左側のペインに表示されます：

   1. 「**名前**」フィールドで、**PayNow** を画像の名前として指定します。
   1. 「**アップロード**」をタップし、ローカルのファイルシステムに保存された   の画像を選択して「**開く**」をタップします。
   1. ![done_icon](assets/done_icon.png) をタップして、画像のプロパティを保存します。

1. 手順 13～14 を繰り返し、**ValueAddedServices** の画像を **ValueAddedServices** のターゲット領域に追加します。

### Web チャネル用インタラクティブ通信の作成 {#create-interactive-communication-for-web-channel}

以下は、本チュートリアル内で既に作成済みで、Web チャネル用のインタラクティブ通信を作成する際に必要になるリソース一覧です。

**Web テンプレート：** [Create_First_IC_Web_Template](../../forms/using/create-templates-print-web.md)

**フォームデータモデル：** [FDM_Create_First_IC](../../forms/using/create-form-data-model0.md)

**ドキュメントフラグメント：** [bill_details_first_ic、customer_details_first_ic、bill_summary_first_ic、summary_charges_first_ic](../../forms/using/create-document-fragments.md)

**画像：** PayNowWeb および ValueAddedServicesWeb

1. AEM オーサーインスタンスにログインし、**[!UICONTROL Adobe Experience Manager]**／**[!UICONTROL フォーム]**／**[!UICONTROL フォームとドキュメント]**&#x200B;に移動します。
1. 「**作成**」をタップし、「**インタラクティブ通信**」を選択します。**インタラクティブ通信の作成**&#x200B;ウィザードが表示されます。
1. 「**タイトル**」と「**名前**」フィールドに **create_first_ic** と入力します。**FDM_Create_First_IC** をフォームデータモデルとして選択し、「**次へ**」をタップします。
1. **チャンネル**&#x200B;ウィザードで以下を実行します。

   1. **create_first_ic_print_template** を印刷テンプレートとして指定し、「**選択**」をタップします。「**Web チャンネルのマスターとして印刷を使用**」のチェックボックスが選択されていないことを確認してください。

   1. **Create_First_IC_templates** フォルダー／**Create_First_IC_Web_Template** を Web テンプレートとして指定し、「**選択**」をタップします。

   1. 「**作成**」をタップします。

   インタラクティブ通信が正常に作成されたことを通知する確認メッセージが表示されます。

1. 「**編集**」をタップし、右側のペインでインタラクティブ通信を開きます。
1. 左側のペインから「**チャンネル**」タブをタップし、「**Web**」をタップします。
1. 「**アセット**」タブに移動してフィルターを適用し、左側のペインのドキュメントフラグメントだけを表示します。
1. 以下のドキュメントフラグメントをインタラクティブ通信のターゲット領域にドラッグアンドドロップします。

   | ドキュメントフラグメント | ターゲット領域 |
   |---|---|
   | bill_details_first_ic | BillDetails |
   | customer_details_first_ic | CustomerDetails |
   | bill_summary_first_ic | BillSummary |
   | summary_charges_first_interactive_communication | 料金 |

1. **請求概要**&#x200B;のターゲット領域をタップし、**+** をタップして&#x200B;**グラフ**&#x200B;のコンポーネントを追加します。
1. グラフのコンポーネントをタップし、![configure_icon](assets/configure_icon.png)（設定）を選択します。グラフのプロパティが左側のペインに表示されます：

   1. グラフ名を指定します。
   1. 「**グラフのタイプ**」ドロップダウンリストから「**円グラフ**」を選択します。

   1. **X 軸**&#x200B;セクションの&#x200B;**通話**&#x200B;データモデルオブジェクトタイプから **Calltype** プロパティを選択します。![done_icon](assets/done_icon.png) をタップします。

   1. 「**関数**」ドロップダウンリストから「**頻度**」を選択します。

   1. **Y 軸**&#x200B;セクションの&#x200B;**通話**&#x200B;データモデルオブジェクトタイプから **Calltype** プロパティを選択します。![done_icon](assets/done_icon.png) をタップします。

   1. ![done_icon](assets/done_icon.png) をタップして、グラフのプロパティを保存します。

1. 左側のペインから「**データソース**」タブを選択し、**通話**&#x200B;データモデルオブジェクトを&#x200B;**通話明細**&#x200B;のターゲット領域にドラッグアンドドロップします。**通話**&#x200B;データモデルオブジェクトに含まれるすべてのプロパティが、右側のペインの&#x200B;**通話明細**&#x200B;のターゲット領域にテーブル列として表示されます。

   ユースケースに基づいて、テーブルには、通話日、通話時刻、通話番号、通話時間、そして通話料金の列が必要です。

   ![インタラクティブ通信用テーブル](assets/table_ic_web_new.png)

1. **Mobilenum** テーブルの列見出しを選択し、**追加のオプション**／**列の削除**&#x200B;の順に選択します。同様に、**Calltype** の列を削除します。
1. **Calldate** テーブル列見出しを選択し、「![編集](assets/edit.png)」をタップしてテキストの名前を「**通話日**」に変更します。同様に、テーブル内の他の列見出しの名前を変更します。
1. ユースケースに基づき、「**Pay Now**」（今すぐ支払う）ボタンをインタラクティブ通信に挿入し、ユーザーがボタンをクリックして支払いを行えるようにします。ボタンを挿入するには、次の手順を実行します。

   1. **Pay Now** のターゲット領域をタップし、**+** をタップして&#x200B;**テキスト**&#x200B;のコンポーネントを追加します。

   1. テキストコンポーネントをタップし、「![編集](assets/edit.png)」をタップします。
   1. テキストの名前を **Pay Now** に変更します。
   1. テキストを選択し、ハイパーリンクアイコンをタップします。
   1. **パス**&#x200B;フィールドで支払い URL を指定します。
   1. 「**ターゲット**」ドロップダウンリストから「**新規タブ**」を選択します。

   1. ![done_icon](assets/done_icon.png) をタップして、ハイパーリンクのプロパティを保存します。

1. 「**プレビュー**」オプションの隣にあるドロップダウンリストから「**スタイル**」を選択します。

   ![インタラクティブ通信のスタイルモードを選択](assets/select_style_ic_web_new.png)

1. ハイパーリンクテキストのスタイルを設定し、インタラクティブ通信でボタンとして表示するには次の手順を実行します。

   1. テキストコンポーネントをタップし、「![編集](assets/edit.png)」を選択します。
   1. 「**境界線**」セクションで、**境界線の幅**&#x200B;を **1.5px** に指定します。**境界線のスタイル**&#x200B;として&#x200B;**実線**&#x200B;を選択し、**境界線の半径**&#x200B;を **46px** に指定します。

   1. 「**背景**」セクションから、ボタンの背景色に赤を選択します。
   1. 「**寸法と位置**」セクションの「**余白**」フィールドで、「**同時に編集**」アイコンをタップして、**右**&#x200B;の余白を **450px** に設定します。上、下、左のフィールドは空白に設定されます。

   ![インタラクティブ通信にハイパーリンクを挿入](assets/ic_web_hyperlink_new.png)

1. **Pay Now** のターゲット領域をタップし、**+** をタップして&#x200B;**画像**&#x200B;のコンポーネントを追加します。
1. 画像のコンポーネントをタップし、![configure_icon](assets/configure_icon.png)（設定）を選択します。画像のプロパティが左側のペインに表示されます：

   1. 「**名前**」フィールドで、**PayNow** を画像の名前として指定します。

   1. 「**アップロード**」をタップし、ローカルのファイルシステムに保存された **PayNowWeb** の画像を選択して「**開く**」をタップします。

   1. ![done_icon](assets/done_icon.png) をタップして、画像のプロパティを保存します。

1. ユースケースに基づき、「**登録**」ボタンをインタラクティブ通信に挿入し、ユーザーがボタンをクリックして付加価値サービスを追加できるようにします。

   手順 13～17 を繰り返し、**付加価値サービス** ターゲット領域に「**登録**」ボタンを追加し、**ValueAddedServicesWeb**&#x200B;画像を追加します。

## 自動同期での印刷版および Web 版のインタラクティブ通信の作成 {#create-interactive-communications-for-print-and-web-with-auto-synchronization}

インタラクティブ通信は、印刷チャネルと Web チャネル間の自動同期を有効化することでも作成できます。自動同期を有効化するには、インタラクティブ通信を作成する際に印刷をマスターオプションとして選択します。印刷チャネルをマスターとして選択すると、Web チャネルに連結されたコンテンツ、継承設定、データが印刷チャネルから取得されます。また、印刷チャネルで加えられた変更が Web チャネルにも反映されるようにします。

印刷チャネルを使って Web チャネルのコンテンツを派生するには、次の手順を実行します。

1. AEM オーサーインスタンスにログインし、**[!UICONTROL Adobe Experience Manager]**／**[!UICONTROL フォーム]**／**[!UICONTROL フォームとドキュメント]**&#x200B;に移動します。
1. 「**作成**」をタップし、「**インタラクティブ通信**」を選択します。**インタラクティブ通信の作成**&#x200B;ウィザードが表示されます。
1. 「**タイトル**」と「**名前**」フィールドに **create_first_ic** と入力します。**FDM_Create_First_IC** をフォームデータモデルとして選択し、「**次へ**」をタップします。
1. **チャネル**&#x200B;ウィザードで以下を実行します。

   1. **create_first_ic_print_template** を印刷テンプレートとして指定し、「**選択**」をタップします。

   1. 「**Web チャネルのマスターとして印刷を使用**」チェックボックスを選択します。
   1. **Create_First_IC_templates** フォルダー／**Create_First_IC_Web_Template** を Web テンプレートとして指定し、「**選択**」をタップします。

   1. 「**作成**」をタップします。

   インタラクティブ通信が正常に作成されたことを通知する確認メッセージが表示されます。

1. 「**編集**」をタップし、右側のペインでインタラクティブ通信を開きます。
1. 「[印刷チャネル用のインタラクティブ通信の作成](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-print-channel)」セクションの手順 6 ～ 15 を実行します。
1. 左側のペインのタブから「**チャネル**」をタップし、「**Web**」をタップし、印刷チャネルから Web チャネル用にコンテンツを自動生成します。
1. 手順 4 で「**Web チャネルのマスターとして印刷を使用**」のチェックボックスを選択したので、コンテンツと連結は印刷チャネルから Web チャネル用に自動生成されます。

   印刷チャネルのコンテンツは Web チャネルのテンプレートコンテンツの下に挿入されます。印刷チャネルから自動生成された Web チャネルのコンテンツを変更するには、どのターゲット領域の継承もキャンセルできます。

   Web チャネル内の関連するターゲット領域にカーソルを置いて ![cancelinheritance](assets/cancelinheritance.png)（継承キャンセル）を選択し、**継承をキャンセル**&#x200B;ダイアログで「**はい**」をタップします。

   ![継承のキャンセル](assets/cancel_inheritance_web_channel_new.png)

   コンポーネントの継承をキャンセルした場合は、その継承を再度有効にすることができます。継承をもう一度有効にするには、目的のコンポーネントが含まれているターゲット領域の境界線にカーソルを置いて ![reenableinheritance](assets/reenableinheritance.png) をタップします。

1. 左側のペインで、「**コンテンツ**」タブを選択します。
1. 自動生成された Web チャネルコンテンツを、コンテンツツリーを使用して Web テンプレートの既存のパネルにドラッグアンドドロップします。以下は配置を調節する必要があるコンポーネントの一覧です。

   * 請求明細コンポーネントを請求明細パネルに
   * 顧客情報コンポーネントを顧客情報パネルに
   * 請求内容コンポーネントを請求内容パネルに
   * 請求概要コンポーネントを請求概要パネルに
   * レイアウトフラグメント（テーブル）を通話明細パネルに

   ![Web コンテンツツリー](assets/ic_web_content_tree_new.png)

1. 「[Web チャネル用インタラクティブ通信の作成](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-web-channel)」の手順 13 ～ 18 を繰り返し、「**Pay Now**」（今すぐ支払う）および「**登録**」ハイパーリンクをインタラクティブ通信の Web チャネルに挿入します。
