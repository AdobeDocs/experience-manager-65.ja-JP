---
title: 手書き署名を使用したフォームへの電子署名の適用
seo-title: Apply electronic signatures to a form using scribble signatures
description: 手書きを使用したフォームへの署名
seo-description: Signing forms using scribble
uuid: ffeba886-9b24-4ed1-95c0-e19356ff2f23
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 76d178d1-8e40-41b3-80d4-66b2f8d04211
docset: aem65
feature: Adaptive Forms
exl-id: 096f61b0-59f4-4699-9093-8fb1ed81fded
source-git-commit: e7a3558ae04cd6816ed73589c67b0297f05adce2
workflow-type: tm+mt
source-wordcount: '719'
ht-degree: 71%

---

# 手書き署名を使用したフォームへの電子署名の適用{#apply-electronic-signatures-to-a-form-using-deprecated-scribble-signatures}

<span class="preview"> Adobeでは、最新の拡張可能なデータキャプチャを使用することをお勧めします [コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja) 対象 [新しいアダプティブFormsの作成](/help/forms/using/create-an-adaptive-form-core-components.md) または [AEM SitesページへのアダプティブFormsの追加](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). これらのコンポーネントは、アダプティブFormsの作成における大幅な進歩を表し、印象的なユーザーエクスペリエンスを実現します。 この記事では、基盤コンポーネントを使用してアダプティブFormsを作成する古い方法について説明します。 </span>


| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-components-to-an-adaptive-form/signing-forms-using-scribble.html) |
| AEM 6.5 | この記事 |


**手書き署名**&#x200B;コンポーネントや&#x200B;**署名ステップ**&#x200B;コンポーネントを使用すると、アダプティブフォームに手書きで署名することができます。署名ステップコンポーネントでは、アダプティブフォームの PDF バージョンが表示されます。署名ステップコンポーネントを使用するには、レコードのドキュメントオプションが有効になっているか、フォームテンプレートに基づくアダプティブフォームが必要です。

![手書き署名ダイアログ](/help/forms/using/assets/scribble-signature.png)

## 署名ウィンドウで使用できる様々なオプション

* **A：** **ペイントブラシ**&#x200B;アイコンをクリックして、キャンバスに署名を描きます。
* **B：** **消去**&#x200B;アイコンをクリックして、キャンバス上の署名を消去します。
* **C：** **位置情報**&#x200B;アイコンをクリックして、署名とともに位置情報を追加します。
* **D：** **キーボード**&#x200B;アイコンをクリックして、キャンバスに名前を入力します。

手書き署名ウィンドウで完了アイコン![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) をタップすると、署名を編集できなくなります。署名を編集する場合は、現在の署名を無視して、上記のペイントブラシ／キーボードオプションを使用して再署名する必要があります。

**設定**&#x200B;アイコン ![configure](assets/configure.png) をクリックして、手書き署名キャンバスのアスペクト比を設定できます。
* 手書き署名キャンバスのアスペクト比が 1 未満の場合、位置情報は手書き署名キャンバスの下部に追加されます。

* 手書き署名キャンバスのアスペクト比が 1 を超える場合、位置情報は手書き署名キャンバスの右側に追加されます。

![手書き署名 -下部](/help/forms/using/assets/scribble-signature-aspectratio.PNG)


>[!NOTE]
>
>署名は常に PNG 形式で保存されます。
>

## アダプティブフォームでの手書き署名使用の設定 {#configure-an-adaptive-form-to-use-scribble-signature}

1. レコードのドキュメントオプションが有効になっているか、フォームテンプレートに基づくアダプティブフォームを作成します。詳しい手順については、「[アダプティブフォームの作成](../../forms/using/creating-adaptive-form.md)」を参照してください。
1. **手書き署名**&#x200B;コンポーネントを、コンポーネントブラウザーからアダプティブフォームにドラッグ＆ドロップします。
1. **設定**（![設定](assets/configure.png)）アイコンをタップします。この操作により、手書き署名コンポーネントのプロパティを表示するプロパティブラウザーが開きます。手書き署名コンポーネントのプロパティを設定します。
1. 署名ステップコンポーネントを、コンポーネントブラウザーからアダプティブフォームにドラッグ＆ドロップします。

   >[!NOTE]
   >
   >署名ステップコンポーネントは、フォームで使用できる全幅を取ります。 署名ステップコンポーネントを含むセクションには、他のコンポーネントを含めないことをお勧めします。
   >

1. コンテンツブラウザーで「**フォームコンテナ**」をタップし、**設定**&#x200B;アイコン（![設定](/help/forms/using/assets/configure.png)）をタップします。この操作により、アダプティブフォームのコンテナプロパティを表示するプロパティブラウザーが開きます。に移動します。 **アダプティブフォームコンテナ** > **電子署名** を選択し、選択を解除します。 **Adobe Signを有効にする** オプション。 完了（![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)）アイコンをタップして、変更を保存します。

   >[!NOTE]
   >
   >署名ステップコンポーネントをアダプティブフォームに追加すると、「Adobe Sign を有効にする」オプションが自動的に選択されます。
   >

1. **設定**（![設定](assets/configure.png)）アイコンをタップします。これにより、プロパティブラウザーが開き、署名ステップのプロパティが表示されます。 以下のプロパティを設定します。

   * **要素名**：コンポーネントの名前を指定します。

   * **タイトル：** コンポーネントの一意のタイトルを指定します。
   * **テンプレートメッセージ：** 署名メッセージの読み込み中に表示するPDFを指定します。 Adobe Signサービスでは、署名PDFの準備と読み込みに時間がかかります。
   * **署名サービス：**「**手書き署名**」オプションを選択します。

   * **CSS クラス**：クライアントライブラリの CSS クラスを指定します（存在する場合）。CSS クラスの代わりに[テーマ](../../forms/using/themes.md)や[インラインスタイル](../../forms/using/inline-style-adaptive-forms.md)を使用することをお勧めします。

   完了（![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)）アイコンをタップして、変更を保存します。署名が正常に設定されます。

   これで、フォームに入力する際に、アダプティブフォームのPDF版が表示され、PDFドキュメントに署名するためのオプションが提供されます。 詳しくは、「[手書き署名を使用したアダプティブフォームの署名](../../forms/using/signing-forms-using-scribble.md#sign-an-adaptive-form-using-scribble-signature)」を参照してください。

## 手書き署名を使用したアダプティブフォームの署名 {#sign-an-adaptive-form-using-scribble-signature}

1. アダプティブフォームに入力して署名ステップページに到達すると、署名画面が表示されます。

   ![手書き署名ダイアログ](/help/forms/using/assets/esignscribblesign.jpg)

1. クリック **[!UICONTROL 署名]**. 手書き署名ダイアログが表示されます。 フォームに署名し、完了（![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)）アイコンをクリックして、変更内容を保存します。

   ![手書き署名ダイアログ](/help/forms/using/assets/scribblewidget.png)

1. 「完了」をクリックして署名プロセスを完了します。

   ![署名プロセスの完了](/help/forms/using/assets/scribblecomplete.jpg)

署名がフォームに追加され、フォームコントロールが次のパネルに移動します。
