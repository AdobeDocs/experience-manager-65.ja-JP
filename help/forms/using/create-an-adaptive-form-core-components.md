---
title: アダプティブフォームの作成方法
seo-title: Learn how to create a Core Components based Adaptive Form on AEM 6.5 Forms.
description: ' [!DNL Experience Manager Forms] を使用したアダプティブフォームの作成方法を説明します。アダプティブフォームは、情報の収集および処理を合理化するレスポンシブ HTML5 フォームです。フォームデータモデルと XML または JSON スキーマに基づいてアダプティブフォームを作成する方法について詳しく調べます。 '
seo-description: Learn how to create an Adaptive Form using [!DNL Experience Manager Forms]. Adaptive Forms are responsive HTML5 forms that streamline information gathering and processing. Dig deeper on how to create an Adaptive Form based on a Form Data Model and XML or JSON schema.
Keywords: create adaptive form core component, create core component based adaptive form, creare adaptive form
products: SG_EXPERIENCEMANAGER/6.5/FORMS
contentOwner: Khushwant Singh
topic-tags: Adaptive Forms
docset: aem65
role: Admin, Developer
source-git-commit: 3bc61e56d2fcd9f32c37a7ea04b0ffc6728bfc56
workflow-type: tm+mt
source-wordcount: '1725'
ht-degree: 33%

---


# コアコンポーネントベースのアダプティブFormsを作成する {#creating-an-adaptive-form-core-components}


<span class="preview"> Adobeでは、コアコンポーネントを次のように使用することをお勧めします。 [AEM SitesページへのアダプティブFormsの追加](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md) または [スタンドアロンのアダプティブFormsを作成する](/help/forms/using/create-an-adaptive-form-core-components.md). </span>

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form-core-components.html?lang=ja) |
| AEM 6.5 | この記事 |

**適用先：** ✅アダプティブフォームのコアコンポーネント❎ [アダプティブフォームの基盤コンポーネント](/help/forms/using/create-adaptive-form.md).

アダプティブフォームを使用すると、魅力的でレスポンシブ、かつ動的でアダプティブなフォームを作成できます。AEM Formsは、ビジネスに適した UI を提供し、アダプティブFormsをすばやく作成します。 UI は、事前設定済みのテンプレート、スタイル設定、フィールド、送信オプションを簡単に選択して、アダプティブフォームを作成するためのクイックタブナビゲーションを提供します。

開始する前に、使用可能な Forms コンポーネントのタイプについて学習します。

* [アダプティブフォームコアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja)：標準化されたデータキャプチャコンポーネントです。これらのコンポーネントは、デジタル登録エクスペリエンスのカスタマイズ機能を提供し、開発時間を短縮し、メンテナンスコストを削減します。開発者は、これらのコンポーネントを簡単にカスタマイズし、スタイルを設定できます。これらの最新かつ拡張性の高いコンポーネントを活用してアダプティブフォームを開発することをお勧めします。

* [アダプティブフォーム基盤コンポーネント](creating-adaptive-form.md)：従来の（古い）データキャプチャコンポーネントです。引き続きこれらを使用して、既存の基盤コンポーネントベースのアダプティブフォームを編集できます。 フォームを作成する場合、Adobeでは  [アダプティブFormsコアコンポーネント](/help/forms/using/create-adaptive-form.md) アダプティブFormsを作成する

## 前提条件

アダプティブフォームを作成するには、以下が必要です。

* **環境でのアダプティブFormsコアコンポーネントの有効化**:AEMアーキタイププロジェクトバージョン 41 以降は、 [お使いの環境に合わせたコアコンポーネントの有効化](/help/forms/using/enable-adaptive-forms-core-components.md). お使いの環境に対してコアコンポーネントを有効にすると、 **アダプティブForms（コアコンポーネント）** テンプレートとキャンバステーマが環境に追加されます。

* **アダプティブフォームテンプレート**：テンプレートは基本構造を提供し、アダプティブフォームのアピアランス（レイアウトとスタイル）を定義します。これには、特定のプロパティやコンテンツ構造を有するフォーマット済みのコンポーネントが含まれます。また、テーマと送信アクションを定義するオプションも提供されます。 テーマは、ルックアンドフィールと送信アクションを定義し、アダプティブフォームの送信時に実行するアクションを定義します。 

  >[!NOTE]
  >
  > ご利用の環境に&#x200B;**アダプティブフォーム（コアコンポーネント）**&#x200B;テンプレートがない場合は、[ご利用の環境のアダプティブフォームコアコンポーネントを有効にします](/help/forms/using/enable-adaptive-forms-core-components.md)。ご利用の環境でコアコンポーネントを有効にすると、**アダプティブフォーム（コアコンポーネント）**&#x200B;テンプレートが環境に追加されます。

* **アダプティブフォームのテーマ**：テーマには、コンポーネントとパネル向けのスタイル設定の詳細が含まれます。 スタイルには、背景カラー、ステートカラー、透明度、配置、サイズなどのプロパティが含まれます。テーマを適用すると、指定したスタイルが対応するコンポーネントに反映されます。The `Canvas` コアコンポーネントを環境に対して有効にすると、テーマがデフォルトで追加されます。 また、 [標準のテーマをダウンロードしてカスタマイズする](create-or-customize-themes-for-adaptive-forms-core-components.md).

* **権限**：[!DNL forms-users] グループにユーザーを追加します。[!DNL forms-users] グループのメンバーには、アダプティブフォームを作成する権限があります。フォーム固有のユーザーグループの詳細なリストについては、 [グループと権限](forms-groups-privileges-tasks.md).

## アダプティブフォームの作成 {#create-an-adaptive-form}

1. ローカルにログイン [AEMオーサーインスタンス](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html?lang=en#author-and-publish-installs).

1. Experience Manager のログインページに資格情報を入力します。ログイン後、左上隅の **[!UICONTROL Adobe Experience Manager]**／**[!UICONTROL Forms]**／**[!UICONTROL フォームとドキュメント]**&#x200B;をタップします。

1. タップ **[!UICONTROL 作成]**  > **[!UICONTROL アダプティブFormsの作成]**.

1. アダプティブFormsコアコンポーネントテンプレートを選択し、 **[!UICONTROL 次へ]**.

1. The **[!UICONTROL プロパティを追加]** が表示されます。 以下のプロパティフィールドの値を指定します。「タイトル」フィールドと「ドキュメント名」フィールドは必須です。

   * **[!UICONTROL タイトル：]**&#x200B;フォームの表示名を指定します。タイトルを指定すると、[!DNL Experience Manager Forms] ユーザーインターフェイス内のフォームを特定しやすくなります。
   * **[!UICONTROL 名前：]**&#x200B;フォームの名前を指定します。指定された名前のノードがリポジトリーに作成されます。タイトルを入力し始めると、名前フィールドの値が自動的に生成されます。候補として入力された値は変更可能です。「ドキュメント名」フィールドには、英数字、ハイフン、アンダースコアのみを使用できます。
   * **[!UICONTROL 説明：]**&#x200B;フォームに関する詳細情報を指定します。
   * **[!UICONTROL テーマクライアントライブラリ]:** アダプティブフォームのテーマを指定します。 デフォルトでは、 `adaptiveform.theme.canvas3` テーマが選択されている。 また、 **[!UICONTROL テーマクライアントライブラリ]** ドロップダウンメニュー。
   * **[!UICONTROL 設定コンテナ：]**  アダプティブFormsの設定ファイルを保存する場所を定義します。 これらの設定ファイルには、アダプティブFormsの動作と外観に関連する設定とプロパティが含まれています。
   * **[!UICONTROL タグ：]**&#x200B;アダプティブフォームを一意に識別するためのタグを指定します。タグを指定すると、フォームを検索しやすくなります。タグを作成するには、「**[!UICONTROL タグ]**」ボックスに新しいタグ名を入力します。
1. 「**[!UICONTROL 作成]**」をタップします。アダプティブフォームが作成され、フォームを編集用に開くためのダイアログが表示されます。


1. タップ **[!UICONTROL 編集]** をクリックして、新しく作成されたフォームを新しいタブで開きます。 フォームが編集用に開かれ、テンプレート内の利用可能なコンテンツが表示されます。また、新しく作成されたフォームをカスタマイズするサイドバーも表示されます。


## アダプティブFormsコアコンポーネントを使用したフォームの作成

フォームを編集用に開いた後、使用可能なアダプティブFormsコアコンポーネントを使用して、フォームフィールドをフォームに追加できます。 ドラッグ&amp;ドロップするか、「+」を使用します [コンポーネントを挿入] オプションを使用して、これらのコンポーネントをフォームに追加できます。 利用可能な情報については、 AEMコアコンポーネントのドキュメントを参照してください [アダプティブFormsコアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=en#components). また、[https://aemcomponents.dev/](https://aemcomponents.dev/) では、使用可能なコアコンポーネントの動作を確認できます。

## アダプティブフォームの送信アクションの設定 {#configure-submit-action-for-form}

送信アクションを使用すると、アダプティブフォームから取り込んだデータの送信先を選択できます。 これは、ユーザーがアダプティブフォーム上の「送信」ボタンをクリックするとトリガーされます。 アダプティブフォームには、すぐに使用できる送信アクションがいくつか含まれています。 デフォルトの送信アクションを拡張して、独自のカスタム送信アクションを作成することもできます。 フォームの送信アクションを設定するには、次の手順を実行します。

1. コンテンツブラウザーを開き、「 **[!UICONTROL ガイドコンテナ]** アダプティブフォームのコンポーネント
1. ガイドコンテナのプロパティをクリックします。 ![ガイドのプロパティ](/help/forms/using/assets/configure-icon.svg) アイコン。 アダプティブフォームコンテナダイアログボックスが開きます。

1. 次をクリック：  **[!UICONTROL 送信]** タブをクリックします。

   ![レンチアイコンをクリックしてアダプティブフォームコンテナダイアログボックスを開き、送信アクションを設定します](/help/forms/using/assets/adaptive-forms-submit-message.png)

1. を選択して設定します。 **[!UICONTROL 送信アクション]**、要件に応じて。 送信アクションについて詳しくは、 [アダプティブフォーム送信アクション](/help/forms/using/configuring-submit-actions.md)

<!--
    
    ![Click the Wrench icon to open Adaptive Form Container dialog box to configure Data Models for the Adaptive Form Container component](/help/forms/assets/adaptive-forms-container.png)

-->

## ユーザーをページにリダイレクトしたり、フォーム送信時に「ありがとうございます」メッセージを表示したりします

フォームの送信時に、別の Web ページまたはメッセージにユーザーをリダイレクトできます。 ユーザーをリダイレクトするか、「ありがとうございます」メッセージを設定するには、次の手順を実行します。

1. コンテンツブラウザーを開き、「 **[!UICONTROL ガイドコンテナ]** アダプティブフォームのコンポーネント
1. ガイドコンテナのプロパティをクリックします。 ![ガイドのプロパティ](/help/forms/using/assets/configure-icon.svg) アイコン。 アダプティブフォームコンテナダイアログボックスが開きます。
1. を開きます。 **[!UICONTROL 送信]** タブをクリックします。

   ![レンチアイコンをクリックしてアダプティブフォームコンテナダイアログボックスを開き、リダイレクトページまたは「ありがとうございます」メッセージを設定します。](/help/forms/using/assets/adaptive-forms-submit-message.png)

   * リダイレクト URL を設定するには、「送信時」オプションで、 **[!UICONTROL URL にリダイレクト]** 」オプションを選択し、AEM Sitesページを参照して選択するか、外部ページの URL を指定します。

   * カスタムメッセージまたは「ありがとうございます」メッセージを設定するには、「送信」オプションで、 **[!UICONTROL メッセージを表示]** オプションを選択し、 **[!UICONTROL メッセージの内容]** ボックス。 これはリッチテキストボックスで、全画面表示オプションを使用して、使用可能なすべてのリッチテキスト項目を表示できます。

## アダプティブフォームのスキーマまたはフォームデータモデルの設定 {#configure-schema-or-data-model-for-form}

フォームデータモデルを使用して、フォームをデータソースに接続し、ユーザーの操作に基づいてデータを送受信することができます。 また、フォームを JSON スキーマに接続して、送信済みデータを事前定義済みの形式で受け取ることもできます。 必要に応じて、フォームを JSON スキーマまたはフォームデータモデルに接続します。

* [JSON スキーマを作成し、環境にアップロードする](/help/forms/using/adaptive-form-json-schema-form-model.md)
* [フォームデータモデルを作成する](/help/forms/using/create-form-data-models.md)

### フォームの JSON スキーマまたはフォームデータモデルを設定する

フォームの JSON スキーマまたはフォームデータモデルを設定するには、次の手順を実行します。

1. コンテンツブラウザーを開き、「 **[!UICONTROL ガイドコンテナ]** アダプティブフォームのコンポーネント
1. ガイドコンテナのプロパティをクリックします。 ![ガイドのプロパティ](/help/forms/using/assets/configure-icon.svg) アイコン。 アダプティブフォームコンテナダイアログボックスが開きます。
1. を開きます。 **[!UICONTROL データモデル]** タブをクリックします。

   ![レンチアイコンをクリックしてアダプティブフォームコンテナダイアログボックスを開き、JSON スキーマまたはフォームデータモデルを設定します](/help/forms/using/assets/adaptive-forms-select-form-data-model-or-json-schema.png)

1. 必要に応じて、JSON スキーマまたはフォームデータモデルを選択し、設定します。

   * 次の項目を選択した場合： **[!UICONTROL フォームモデル]** オプションを選択する場合は、 **[!UICONTROL フォームデータモデルを選択]** 」オプションを使用して事前設定済みのフォームデータモデルを選択します。
   * 次の項目を選択した場合： **[!UICONTROL スキーマ]** オプションを選択する場合は、 **[!UICONTROL スキーマ]** オプションを使用して、フォームの JSON スキーマを選択します。

1. 「**[!UICONTROL 完了]**」をクリックします。

>[!NOTE]
>
> Guide Container プロパティを使用して、アダプティブフォームの JSON スキーマまたはフォームデータモデルを編集できます。

## 事前入力サービスの設定  {#configure-prefill-service-for-form}

事前入力サービスを使用すると、既存のデータを使用してアダプティブフォームのフィールドに自動入力することができます。 ユーザーがフォームを開くと、これらのフィールドの値は事前入力されています。以下の操作を実行できます。

* [カスタム事前入力サービスの作成](/help/forms/using/prepopulate-adaptive-form-fields.md)
* [フォームデータモデルの事前入力サービスを使用する](#fdm-prefill-service)

### フォームデータモデルの事前入力サービスを使用して、アダプティブフォームのフィールドに事前入力する {#fdm-prefill-service}

フォームデータモデルの事前入力サービスを使用すると、フォームデータモデルまたはカスタム事前入力サービスを使用して、アダプティブフォームのフィールドに事前入力することができます。 フォームデータモデルの事前入力サービスでは、 [設定済みのフォームデータモデルのサービスを取得する](work-with-form-data-model.md#add-data-model-objects-and-services-add-data-model-objects-and-services) データを取得します。 アダプティブフォームでフォームデータモデルの事前入力サービスを使用するには、次の手順を実行します。

1. コンテンツブラウザーを開き、「 **[!UICONTROL ガイドコンテナ]** アダプティブフォームのコンポーネント
1. ガイドコンテナのプロパティをクリックします。 ![ガイドのプロパティ](/help/forms/using/assets/configure-icon.svg) アイコン。 アダプティブフォームコンテナダイアログボックスが開きます。
1. アダプティブフォームコンテナのプロパティをクリックします。 ![アダプティブフォームコンテナのプロパティ](/help/forms/using/assets/configure-icon.svg) アイコン。 データモデルを設定するためのアダプティブフォームコンテナダイアログボックスが開きます。
   ![レンチアイコンをクリックしてアダプティブフォームコンテナダイアログボックスを開き、リダイレクトページまたは「ありがとうございます」メッセージを設定します。](/help/forms/using/assets/adaptive-forms-container-prefill-service.png)
1. フォームデータモデルを選択. を開きます。 **[!UICONTROL 基本]** タブをクリックします。 事前入力サービスで、「 」を選択します。 **[!UICONTROL フォームデータモデルの事前入力サービス]**.
1. 「**[!UICONTROL 完了]**」をクリックします。これで、アダプティブフォームがフォームデータモデルの事前入力を使用するように設定されました。 これで、 [ルールエディター](rule-editor.md) ：フォームのフィールドに事前入力するルールを作成します。

<!--
## Edit Form Model properties of an Adaptive Form {#edit-form-model}

1. Select the Adaptive Form and tap ![Page information](/help/forms/using/assets/configure-icon.svg) > **[!UICONTROL Open Properties]**. The Form Properties page opens. 

1. Go to the **[!UICONTROL Form Model]** tab and choose a form model. If the Adaptive Form is without a form model, you have the freedom to choose either a JSON schema or a form data model. On the other hand, if the Adaptive Form is already based on a form model, you have the option to switch to another form model of the same type. For instance, if the form is using a JSON schema, you can easily switch to another JSON schema, and similarly if the form is using a Form Data Model, you can switch to another Form Data Model. 

1. Tap **[!UICONTROL Save]** to save the properties.
-->

## 次の手順

* [ルールエディターを使用して、フォームに動的な動作を追加します。](rule-editor.md)
* [コアコンポーネントベースのアダプティブFormsのテーマを作成またはカスタマイズする](create-or-customize-themes-for-adaptive-forms-core-components.md)
* コアコンポーネントベースのアダプティブFormsのテンプレートを作成する

## 関連トピック

* [コアコンポーネントベースのアダプティブフォームの作成](create-an-adaptive-form-core-components.md)
* [アダプティブフォームを作成するか、AEM Sitesページまたはエクスペリエンスフラグメントに追加する](create-or-add-an-adaptive-form-to-aem-sites-page.md)

