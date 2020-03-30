---
title: インタラクティブ通信内の条件
seo-title: インタラクティブ通信内の条件
description: ここでは、インタラクティブ通信で使用する条件フラグメントの作成方法と編集方法について説明します。インタラクティブ通信の作成では 4 種類のドキュメントフラグメントが使用されますが、条件フラグメントはそのうちの 1 つです。他の 3 つは、テキストフラグメント、リストフラグメント、レイアウトフラグメントです。
seo-description: インタラクティブ通信で使用する条件の作成と編集
uuid: c98f02d5-1769-46dd-ab35-6e8145a24939
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fe59d260-d392-4d6f-bb7e-2f2a1d701f51
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# インタラクティブ通信内の条件{#conditions-in-interactive-communications}

ここでは、インタラクティブ通信で使用する条件フラグメントの作成方法と編集方法について説明します。インタラクティブ通信の作成では 4 種類のドキュメントフラグメントが使用されますが、条件フラグメントはそのうちの 1 つです。他の 3 つは、テキストフラグメント、リストフラグメント、レイアウトフラグメントです。

## 概要 {#overview}

条件は、インタラクティブ通信に含めることができるドキュメントフラグメントです。他のドキュメントフラグメントには、[テキストフラグメント](../../forms/using/texts-interactive-communications.md)、リストフラグメント、レイアウトフラグメントがあります。条件を使用すると、提供されたデータとルールに基づいて、インタラクティブ通信に含まれる1つ以上のコンテキストアセットを定義できます。

例：

* 顧客が使用しているクレジットカードの種類に基づいて、そのクレジットカードの年会費と画像を取引明細書に表示する。
* 顧客が居住している国の税制に基づいて、保険料支払期日の通知に税額の計算結果を表示する。

条件内のアセットは、適用されるルールと、そのルールに渡される値に基づいてレンダリングされます。条件のルールでは、次のタイプのデータの値を確認できます。

* 関連するフォームデータモデルのプロパティ
* 条件で作成する変数
* 文字列
* 数値
* 数式
* 日付

## 条件の作成 {#createcondition}

1. 「**[!UICONTROL フォーム]**／**[!UICONTROL ドキュメントフラグメント]**」を選択します。
1. Select **[!UICONTROL Create]** > **[!UICONTROL Condition]**.
1. 次の情報を指定します。

   * **[!UICONTROL タイトル]**:（オプション）条件のタイトルを入力します。 タイトルは一意である必要はなく、特殊文字や英語以外の文字を含めることもできます。条件は、（利用可能な場合に）そのタイトル（サムネールやプロパティなど）によって参照されます。
   * **[!UICONTROL 名前]**:フォルダー内の条件の一意の名前。 どのような状態であっても、1 つのフォルダー内に、同じ名前を持つ 2 つのドキュメントフラグメント（テキスト、条件、リスト）を保管することはできません。「名前」フィールドでは、英数字およびハイフンのみ使用できます。「名前」フィールドは、タイトルフィールドに基づいて自動的に入力されます。「タイトル」フィールドに入力した特殊文字、スペース、数字および英数字以外の文字は、ハイフンに置き換えられます。 「タイトル」フィールドの値は「名前」フィールドに自動的にコピーされますが、値を編集することもできます。

   * **[!UICONTROL 説明]**：ドキュメントフラグメントの説明を入力します。
   * **[!UICONTROL フォームデータモデル]**：（任意）フォームデータモデルに基づいて条件を作成する場合は、「フォームデータモデル」ラジオボタンを選択します。When you select Form Data Model radio button, **[!UICONTROL Form Data Model]** field appears. フォームデータモデルを参照して選択します。インタラクティブ通信用の条件を作成する場合は、そのインタラクティブ通信で使用するものと同じデータモデルを使用する必要があります。For more information on form data model, see [Data Integration](../../forms/using/data-integration.md).

   * **[!UICONTROL タグ]**：（任意）カスタムタグを作成する場合は、テキストフィールドに値を入力して Enter キーをタップします。この条件を保存すると、新しく追加されたタグが作成されます。

1. 「**[!UICONTROL 次へ]**」をタップします。

   条件の作成ページが表示されます。

   ![createcondition](assets/createcondition.png)

1. Tap **[!UICONTROL Add Assets]**.

   アセットの選択ページが表示されます。このページには、条件内に追加できるテキスト、リスト、条件、画像が表示されます。

   >[!NOTE]
   >
   >アセットの選択ページには、新しく作成されたアセットと FDM ベースのアセット（作成する条件と同じ FDM を使用して作成されたアセット）だけが表示されます。

1. 条件に含めるアセットをタップして選択し、「**[!UICONTROL 完了]**」をタップします。

   条件の作成ページが表示されます。このページには、作成されたアセットが一覧表示されます。

   ![createconditionassetsadd](assets/createconditionassetsadd.png)

   以下のオプションを使用して、条件内のアセットを管理することができます。

   ![createconditionscreenassetsaddedannotated](assets/createconditionscreenassetsaddedannotated.png)

   **[拒否の変更]。**このアイコンをタップすると、アセットと条件のルールに対して行った変更が拒否されます。   **[B]Accept Change。**このアイコンをタップして、条件のアセットおよびルールに加えた変更を受け入れます。   **[C]重複資産&#x200B;**適用対象のルール（存在する場合）と共に条件内のアセットのコピーを作成する場合は、このアイコンをタップします。その後、複製されたアセットで、ルールとアセットの編集を行うことができます。特定のコンテキストに基づいて代替のアセットを表示するための類似のルールを作成する場合は、アセットを複製すると便利です。   **[D表示]プレビュー&#x200B;**このアイコンをタップすると、プレビューの作成/条件の編集ページにアセットのアイコンが表示されます。   **&#39;server&#39;順序を変更します。** このアイコンを長押しして、アセットをドラッグ&amp;ドロップし、条件内で並べ替えます。

   条件の実行時の動作を指定するには、次のオプションを選択します。

   * **複数の結果評価を無効化 / 複数の結果評価を有効化**：「複数の結果評価を有効化」オプションを選択すると、すべての条件が評価され、その結果として、すべての true ルールの要約が表示されます。「複数の結果評価を無効化」オプションを選択すると、true と判断された最初のルールだけが評価され、そのルールが条件の出力になります。

   * **改ページ**:条件のアセット間に改 ![ページを追加するには](assets/break.png)、このオプション（改ページ）を選択します。 When this option is not selected ( ![nobreak](assets/nobreak.png)), if a condition is overflowing to the next page in the print output, the whole condition is shifted to the next page instead of breaking in the page between the assets in the condition.

1. 「**[!UICONTROL ルールを作成]**」をタップして、アセットの表示と非表示を切り替えるためのルールを必要に応じて追加します。ルール内で変数を使用する方法については、「[変数の作成](#variables)」を参照してください。For more information, see [Adding rules to condition](#ruleeditor).

   作成されたルールが、条件作成画面の「ルール」列に表示されます。

   ![createconditionscreenrulesadded](assets/createconditionscreenrulesadded.png)

   >[!NOTE]
   >
   >既にルールが設定されている条件（または繰り返しが適用されている条件）にアセットを挿入することができます。

1. 「**[!UICONTROL 保存]**」をタップします。

   これで、条件が作成されました。この条件を使用して、インタラクティブ通信を作成することができます。

   >[!NOTE]
   >
   >新しい条件や編集後の条件を保存するには、条件内に追加する各アセットについて、1 つ以上のルールを設定する必要があります。

## 条件の編集 {#edit-a-condition}

以下の手順により、条件を編集することができます。ポップアップメニューで「フラグメントを編集」を選択して、インタラクティブ通信内で条件を編集することもできます。

1. 「**[!UICONTROL フォーム]**／**[!UICONTROL ドキュメントフラグメント]**」を選択します。
1. 目的の条件に移動して、その条件を選択します。
1. 「**[!UICONTROL 編集]**」をタップします。
1. 条件内で、必要な変更を行います。For more details on the information you can change in a condition, see [Create condition](#createcondition).
1. Tap **[!UICONTROL Save]** and then tap **[!UICONTROL Close]**.

## 条件内でルールを作成する {#ruleeditor}

条件内でルールエディターを使用して、**事前に定義された条件**&#x200B;に基づいてアセットの表示と非表示を切り替えるためのルールを作成することができます。事前に定義された条件は、以下のデータに基づいて設定することができます。

* 文字列
* 数値
* 数式
* 日付
* 関連するフォームデータモデルのプロパティ
* 作成済みの任意の[変数](#variables)

### 条件内でルールを作成する {#create-rule-in-condition}

1. While creating or editing a condition, tap ![ruleeditoricon](assets/ruleeditoricon.png) (Rule Editor) icon for the relevant asset.

   ルール作成ダイアログが表示されます。文字列、数値、数式、日付のほかに、以下のデータをルールエディターで使用して、ルールのステートメントを作成することができます。

   * 関連するフォームデータモデルのプロパティ
   * 作成済みの任意の[変数](#variables)
   ![createruledialog](assets/createruledialog.png)

   評価するオプションを選択します。

   >[!NOTE]
   >
   >Collection プロパティを使用して、アセットを表示するためのルールを作成することはできません。

1. 「次の値と等しい」、「次の値を含む」、「次の値で始まる」など、ルールを評価するための適切な演算子を選択します。
1. 評価式、文字列、データモデルプロパティ、変数、または日付を挿入します。

   ![ポリシータイプが「標準」の場合にアセットを表示するためのルール](assets/ruleincondition.png)

   ポリシータイプが「標準」の場合にアセットを表示するためのルール

   * While creating or editing a rule, you can also tap ![icon_resize](assets/icon_resize.png) (Resize) to expand the Create Rule/Edit Rule dialog. ダイアログを拡張して全画面表示にすると、ルールを構成する[変数](#variables)を作成できるようになります。「サイズ変更」を再度タップして、通常のルールの作成ダイアログに戻ります。

   * 1 つのルールで複数の条件を作成することもできます。

1. 「**[!UICONTROL Done]**」をタップします。

   これで、ルールがアセットに適用されます。

## 条件内で変数を作成して使用する {#variables}

While creating or editing a rule in a condition, you can tap ![icon_resize](assets/icon_resize.png) (Resize) to expand the Create Rule\Edit Rule dialog. ダイアログを拡張して全画面表示にすると、以下の操作を実行できるようになります。

* ルール内で変数を作成して使用する
* ルール内でのフォームデータモデルのプロパティと変数のドラッグ&amp;ドロップ

サイズ変更アイコンをもう一度タップすると、通常のサイズのダイアログに戻ります。

### 変数の作成 {#create-variables}

1. While creating or editing a rule in a condition, you can tap ![icon_resize](assets/icon_resize.png) (Resize) to expand the Create Rule\Edit Rule dialog.

   拡張されたダイアログが全画面モードで表示されます。

   ![expandeditruledialog](assets/expandededitruledialog.png)

1. In the left pane, tap **[!UICONTROL Variables]**.

   変数ペインが表示されます。

   ![expandeditrulevariables](assets/expandededitrulevariables.png)

1. 「**[!UICONTROL 作成]**」をタップします。

   変数作成ペインが表示されます。

1. Enter the following information and tap **[!UICONTROL Create]**:

   * **[!UICONTROL 名前]**:変数の名前。
   * **[!UICONTROL 説明]**:必要に応じて、変数の説明を入力します。
   * **[!UICONTROL タイプ]**:変数のタイプを選択します。文字列、数値、ブール値または日付。
   * **[!UICONTROL 特定の値のみ許可]**：文字列タイプまたは数値タイプの変数の場合、このオプションを選択すると、エージェント UI のプレースホルダーの特定の値セットから、エージェントによって値が選択されます。To specify the set of values, select this option and then specify comma-separated values that are allowed in the **[!UICONTROL Values]** field.

1. 「**[!UICONTROL 作成]**」をタップします。

   作成された変数が変数ペインに表示されます。

1. ルール内に変数を挿入するには、ルール内の任意のオプションのプレースホルダーにその変数をドラッグアンドドロップします。
1. After you have constructed a valid rule, tap **[!UICONTROL Done]**.

   必要に応じて、条件内でさらに変更を行い、その変更内容を保存します。

