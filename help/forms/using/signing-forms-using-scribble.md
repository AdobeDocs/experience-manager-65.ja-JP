---
title: 手書き署名を使用したフォームへの電子署名の適用
seo-title: Apply electronic signatures to a form using scribble signatures
description: 手書きでのフォームへの署名
seo-description: Signing forms using scribble
uuid: ffeba886-9b24-4ed1-95c0-e19356ff2f23
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 76d178d1-8e40-41b3-80d4-66b2f8d04211
docset: aem65
feature: Adaptive Forms
exl-id: 096f61b0-59f4-4699-9093-8fb1ed81fded
source-git-commit: 9ee8e79777b89fbf4d6e5b5fd1dbb1ef3bc9ad5d
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 73%

---

# 手書き署名を使用したフォームへの電子署名の適用{#apply-electronic-signatures-to-a-form-using-deprecated-scribble-signatures}

**手書き署名**&#x200B;コンポーネントや&#x200B;**署名ステップ**&#x200B;コンポーネントを使用すると、アダプティブフォームに手書きで署名することができます。署名ステップコンポーネントでは、アダプティブフォームの PDF バージョンが表示されます。署名ステップコンポーネントを使用するには、レコードのドキュメントオプションが有効になっているか、フォームテンプレートに基づくアダプティブフォームが必要です。

![手書き署名ダイアログ](/help/forms/using/assets/scribble-signature.png)

## 署名ウィンドウで使用できる様々なオプション

* **回答：** 次をクリック： **ペイントブラシ** アイコンをクリックして、キャンバスに署名を描画します。
* **B:** 次をクリック： **クリア** アイコンを使用して、キャンバス上の署名をクリアします。
* **C:** 次をクリック： **位置情報** アイコン：署名と共に位置情報を追加します。
* **D:** 次をクリック： **キーボード** アイコンをクリックして、キャンバスに名前を入力します。

完了![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 手書き署名ウィンドウのアイコンを使用すると、署名を編集できません。 署名を編集する場合は、現在の署名を無視し、上記の [ ブラシ/キーボードをペイント ] オプションを使用して再署名する必要があります。

次をタップします。 **設定** ![設定](assets/configure.png) アイコンをクリックして、手書き署名キャンバスの縦横比を設定します。
* 手書き署名キャンバスの縦横比が 1 未満の場合、位置情報は手書き署名キャンバスの下部に追加されます。

* 手書き署名キャンバスの縦横比が 1 を超える場合、位置情報は手書き署名キャンバスの右側に追加されます。

![手書き署名 — 下](/help/forms/using/assets/scribble-signature-aspectratio.PNG)


>[!NOTE]
>
>署名は常に PNG 形式で保存されます。

## アダプティブフォームでの手書き署名使用の設定 {#configure-an-adaptive-form-to-use-scribble-signature}

1. レコードのドキュメントオプションが有効になっているか、フォームテンプレートに基づくアダプティブフォームを作成します。詳しい手順については、「[アダプティブフォームの作成](../../forms/using/creating-adaptive-form.md)」を参照してください。
1. **手書き署名**&#x200B;コンポーネントを、コンポーネントブラウザーからアダプティブフォームにドラッグ＆ドロップします。
1. **設定**（![設定](assets/configure.png)）アイコンをタップします。この操作により、手書き署名コンポーネントのプロパティを表示するプロパティブラウザーが開きます。手書き署名コンポーネントのプロパティを設定します。
1. 署名ステップコンポーネントを、コンポーネントブラウザーからアダプティブフォームにドラッグ＆ドロップします。

   >[!NOTE]
   >
   >署名ステップコンポーネントは、フォームの幅いっぱいに表示されます。そのため、署名ステップコンポーネントが含まれているセクションに他のコンポーネントを配置しないようにすることをお勧めします。

1. コンテンツブラウザーで「**フォームコンテナ**」をタップし、**設定**（![](/help/forms/using/assets/configure.png)）アイコンをタップします。この操作により、アダプティブフォームのコンテナプロパティを表示するプロパティブラウザーが開きます。**アダプティブフォームコンテナ**／**電子署名**&#x200B;に移動して、「**Adobe Sign を有効にする**」オプションを選択解除します。完了（![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)）アイコンをタップして、変更を保存します。

   >[!NOTE]
   >
   >署名ステップコンポーネントをアダプティブフォームに追加すると、「Adobe Sign を有効にする」オプションが自動的に選択されます。

1. **設定**（![設定](assets/configure.png)）アイコンをタップします。この操作により、署名ステップのプロパティを表示するプロパティブラウザーが開きます。以下のプロパティを設定します。

   * **要素名**：コンポーネントの名前を指定します。

   * **タイトル：**&#x200B;コンポーネントの一意のタイトルを指定します。
   * **テンプレートメッセージ：**&#x200B;署名 PDF の読み込み中に表示するメッセージを指定します。Adobe Sign サービスによる署名 PDF の準備と読み込みには、ある程度の時間がかかります。
   * **署名サービス：**「**手書き署名**」オプションを選択します。

   * **CSS クラス**：クライアントライブラリの CSS クラスを指定します（存在する場合）。CSS クラスの代わりに[テーマ](../../forms/using/themes.md)や[インラインスタイル](../../forms/using/inline-style-adaptive-forms.md)を使用することをお勧めします。

   完了（![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)）アイコンをタップして、変更を保存します。署名が正常に設定されます。

   これで、フォームを記入する際に、PDF バージョンのアダプティブフォームが表示され、PDF ドキュメントの署名オプションが提供されます。詳しくは、「[手書き署名を使用したアダプティブフォームの署名](../../forms/using/signing-forms-using-scribble.md#sign-an-adaptive-form-using-scribble-signature)」を参照してください。

## 手書き署名を使用したアダプティブフォームの署名 {#sign-an-adaptive-form-using-scribble-signature}

1. フォームへの記入を完了して署名ステップページに到達すると、署名画面が表示されます。

   ![手書き署名ダイアログ](/help/forms/using/assets/esignscribblesign.jpg)

1. 「**[!UICONTROL 署名]**」をクリックします。手書き署名ダイアログが表示されます。フォームに署名し、完了（![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)）アイコンをクリックして、変更内容を保存します。

   ![手書き署名ダイアログ](/help/forms/using/assets/scribblewidget.png)

1. 「完了」をクリックして署名プロセスを完了します。

   ![署名プロセスの完了](/help/forms/using/assets/scribblecomplete.jpg)

署名がフォームに追加され、フォームコントロールが次のパネルに移動します。
