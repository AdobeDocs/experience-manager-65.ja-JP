---
title: '"チュートリアルを公開しない：アダプティブフォームフィールドへのルールの適用」'
seo-title: アダプティブフォームのフィールドにルールを適用する
description: このチュートリアルでは、ルールを作成して、インタラクティブ機能、ビジネスロジック、スマート検証機能をアダプティブフォームに追加する方法について説明します。
seo-description: このチュートリアルでは、ルールを作成して、インタラクティブ機能、ビジネスロジック、スマート検証機能をアダプティブフォームに追加する方法について説明します。
page-status-flag: de-activated
uuid: 60f142aa-81ca-4333-8614-85a01e23e917
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 982eddba-2350-40e7-8a42-db02d28cf133
translation-type: tm+mt
source-git-commit: e3ecf724cdfcd20ef4c089605e644ad10ef1221b
workflow-type: tm+mt
source-wordcount: '1148'
ht-degree: 64%

---


# チュートリアル：アダプティブフォームのフィールドにルールを適用する {#tutorial-apply-rules-to-adaptive-form-fields}

![06-apply-rules-to-adaptive-form_main](assets/06-apply-rules-to-adaptive-form_main.png)

これは、[最初のアダプティブフォームを作成する](/help/forms/using/create-your-first-adaptive-form.md)シリーズを構成するチュートリアルです。チュートリアル内のユースケースを理解して実際に操作できるように、このシリーズのチュートリアルを最初から順に学習することをお勧めします。

## このチュートリアルについて {#about-the-tutorial}

ルールを作成して、インタラクティブ機能、ビジネスロジック、スマート検証機能をアダプティブフォームに追加することができます。アダプティブフォームには、ルールエディターが組み込まれています。ルールエディターには、ガイドツアー機能に類似したドラッグアンドドロップ機能が用意されています。このドラッグアンドドロップ機能は、ルールを作成するための最も効率的で簡単な方法です。ルールエディターには、自分のコーディング技術を試してみたいユーザーや、より複雑なコードを作成したいと考えているユーザーのために、コードウィンドウが用意されています。

ルールエディターの詳細については、[アダプティブフォームのルールエディタ－](/help/forms/using/rule-editor.md)を参照してください。

このチュートリアルを終了すると、ルールを作成して以下の操作を実行できるようになります。

* フォームデータモデルサービスを呼び出して、データベースからデータを取得する
* フォームデータモデルサービスを呼び出して、データベースにデータを追加する
* 検証チェック処理を実行して、エラーメッセージを表示する

このチュートリアルの各セクションの最後にあるインタラクティブな GIF 画像で、作成するフォームの機能をその場で確認することができます。

## 手順 1：データベースから顧客レコードを取得する {#retrieve-customer-record}

[フォームデータモデルの作成](/help/forms/using/create-form-data-model.md)チュートリアルでフォームデータモデルを作成しましたが、ここでは、ルールエディターを使用してそのフォームデータモデルサービスを呼び出し、データを取得してデータベースに情報を追加します。

すべての顧客に一意の顧客 ID 番号が割り当てられているため、特定の顧客に関連する顧客データをデータベース内で特定することができます。以下の手順では、顧客 ID を使用して、データベースから情報を取得します。

1. アダプティブフォームを編集用に開きます。

   [http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html](http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html)

1. 「**[!UICONTROL 顧客 ID]**」フィールドをタップし、「**[!UICONTROL ルールを編集]**」アイコンをタップします。ルールエディターウィンドウが表示されます。
1. 「**[!UICONTROL + 作成]**」アイコンをタップしてルールを追加します。ビジュアルエディターが表示されます。

   In the Visual Editor, the **[!UICONTROL WHEN]** statement is selected by default. Also, the form object (in this case, **[!UICONTROL Customer ID]**) from where you launched the rule editor is specified in the **[!UICONTROL WHEN]** statement.

1. Tap the **[!UICONTROL Select State]** drop-down and select **[!UICONTROL is changed]**.

   ![customeridischanged](assets/whencustomeridischanged.png)

1. 「**[!UICONTROL THEN]**」ステートメントの「**[!UICONTROL アクションの選択]**」ドロップダウンで「**[!UICONTROL サービスの呼び出し]**」を選択します。
1. 「**[!UICONTROL 選択]**」ドロップダウンで「**[!UICONTROL 発送先住所を取得]**」サービスを選択します。
1. Drag-and-drop the **[!UICONTROL Customer ID]** field from the Form Objects tab to the **[!UICONTROL Drop object or select here]** field in the **[!UICONTROL INPUT]** box.

   ![dropobjectstoinputfield-retrievedata](assets/dropobjectstoinputfield-retrievedata.png)

1. Drag-and-drop the **[!UICONTROL Customer ID, Name, Shipping Address, State, and Zip Code]** field from the Form Objects tab to the **[!UICONTROL Drop object or select here]** field in the **[!UICONTROL OUTPUT]** box.

   ![dropobjectstooutputfield-retrievedata](assets/dropobjectstooutputfield-retrievedata.png)

   「**[!UICONTROL 完了]**」をタップして、ルールを保存します。On the rule editor window, tap **[!UICONTROL Close]**.

1. アダプティブフォームのプレビューを表示します。「**[!UICONTROL 顧客 ID]**」フィールドに ID を入力します。これで、データベース内の顧客情報をフォームに取り込むことができます。

   ![retrieve-information](assets/retrieve-information.gif)

## 手順 2：更新後の顧客住所をデータベースに追加する {#updated-customer-address}

データタベースから顧客情報を取得したら、出荷先住所、都道府県、郵便番号を変更します。ここでは、フォームデータモデルサービスを呼び出し、顧客情報を変更してデータベースに保存する手順について説明します。

1. 「**[!UICONTROL 送信]**」フィールドを選択して「**[!UICONTROL ルールを編集]**」アイコンをタップします。ルールエディターウィンドウが表示されます。
1. Select the **[!UICONTROL Submit - Click]** rule and tap the **[!UICONTROL Edit]** icon. 送信ルールを編集するためのオプションが表示されます。

   ![送信規則](assets/submit-rule.png)

   In the WHEN option, the **[!UICONTROL Submit]** and **[!UICONTROL is clicked]** options are already selected.

   ![submit-is-clicked](assets/submit-is-clicked.png)

1. 「**[!UICONTROL THEN]**」オプションで「**[!UICONTROL + ステートメントを追加]**」オプションをタップします。「**[!UICONTROL アクションの選択]**」ドロップダウンで「**[!UICONTROL サービスの呼び出し]**」を選択します。
1. 「**[!UICONTROL 選択]**」ドロップダウンで「**[!UICONTROL 出荷先住所の更新]**」を選択します。

   ![update-shipping-address](assets/update-shipping-address.png)

   ![dropobjectstoinputfield-updatedata](assets/dropobjectstoinputfield-updatedata.png)

1. 「 **[!UICONTROL フォームオブジェクト]** 」タブから、「 [!UICONTROL 配送先住所、州、郵便番号] 」フィールドを、Dropオブジェクトの対応するtablenameプロパティ（例えば、customerdetails.shippingAddress）にドラッグ&amp;ドロップするか、「INPUT」ボックスの「 **[!UICONTROL ここ」フィールドを選択し]****** ます。 tablenameが先頭に付くすべてのフィールド（この使用例ではcustomerdetailsなど）は、アップデートサービスの入力データとして機能します。 これらのフィールドで指定された値は、すべてデータソース内で更新されます。

   >[!NOTE]
   >
   >Do not drag-and-drop the **[!UICONTROL Name]** and **[!UICONTROL Customer ID]** fields to the corresponding tablename.property (for example, customerdetails.name). 間違って顧客の名前やIDを更新するのを防ぐのに役立ちます。

1. 「フォームオブジェクト」タブの「**[!UICONTROL 顧客 ID]**」フィールドをドラッグし、「**[!UICONTROL 入力]**」ボックスの「id」フィールドにドロップします。先頭にtablenameが付いていないフィールド（この使用例ではcustomerdetailsなど）は、アップデートサービスの検索パラメーターとして機能します。 The **[!UICONTROL id]** field in this use case uniquely identifies a record in the  **customerdetails**  table.
1. 「**[!UICONTROL 完了]**」をタップして、ルールを保存します。On the rule editor window, tap **[!UICONTROL Close]**.
1. アダプティブフォームのプレビューを表示します。顧客の詳細情報を取得し、発送先住所を変更してフォームを送信します。同じ顧客の詳細情報をもう一度取得すると、更新された発送先住所が表示されます。

## 手順 3：（オプション）コードエディターを使用して検証処理を実行し、エラーメッセージを表示する {#step-bonus-section-use-the-code-editor-to-run-validations-and-display-error-messages}

フォームにデータが正しく入力されているかどうかを確認するには、そのフォーム上で検証処理を実行する必要があります。データが正しく入力されていない場合は、エラーメッセージが表示されます。例えば、存在しない顧客 ID がフォームに入力されている場合は、エラーメッセージが表示されます。

アダプティブフォームには、検証機能が組み込まれたコンポーネントがいくつか用意されています（共通のユースケースで使用できる電子メールや数値フィールドなど）。高度なユースケース（データベースからレコードが 1 件も返されなかった場合にエラーメッセージを表示するなど）の場合は、ルールエディターを使用します。

次の手順は、フォームに入力された顧客IDがデータベースに存在しない場合にエラーメッセージを表示するルールを作成する方法を示しています。 The rule also brings the focus to and resets the **[!UICONTROL Customer ID]** field. The rule uses [the dataIntegrationUtils API of the form data model service](/help/forms/using/invoke-form-data-model-services.md) to check if the Customer ID exists in the database.

1. Tap the **[!UICONTROL Customer ID]** field and tap the `Edit Rules` icon. The [!UICONTROL Rule Editor] window opens.
1. 「**[!UICONTROL + 作成]**」アイコンをタップしてルールを追加します。ビジュアルエディターが表示されます。

   In the Visual Editor, the **[!UICONTROL WHEN]** statement is selected by default. Also, the form object (in this case, **[!UICONTROL Customer ID]**) from where you launched the rule editor is specified in the **[!UICONTROL WHEN]** statement.

1. Tap the **[!UICONTROL Select State]** drop-down and select **[!UICONTROL is changed]**.

   ![customeridischanged](assets/whencustomeridischanged.png)

   「**[!UICONTROL THEN]**」ステートメントの「**[!UICONTROL アクションの選択]**」ドロップダウンで「**[!UICONTROL サービスの呼び出し]**」を選択します。

1. **[!UICONTROL ビジュアルエディター]**&#x200B;から&#x200B;**[!UICONTROL コードエディター]**&#x200B;に切り替えます。切り替え用コントロールは、ウィンドウの右側にあります。コードエディターが開き、以下のようなコードが表示されます。

   ![コードエディター](assets/code-editor.png)

1. 「input」変数セクションのコードを以下のように変更します。

   ```javascript
   var inputs = {
       "id" : this
   };
   ```

1. Replace the `guidelib.dataIntegrationUtils.executeOperation (operationInfo, inputs, outputs)` section with the following code:

   ```javascript
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, function (result) {
     if (result) {
         result = JSON.parse(result);
       customer_Name.value = result.name;
       customer_Shipping_Address = result.shippingAddress;
     } else {
       if(window.confirm("Invalid Customer ID. Provide a valid customer ID")) {
             customer_Name.value = " ";
            guideBridge.setFocus(customer_ID);
       }
     }
   });
   ```

1. アダプティブフォームのプレビューを表示します。正しくない顧客 ID を入力して、エラーメッセージが表示されることを確認します。

   ![display-validation-error](assets/display-validation-error.gif)

