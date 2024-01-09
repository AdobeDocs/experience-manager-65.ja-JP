---
title: アダプティブフォームの作成方法
description: ' [!DNL Experience Manager Forms] を使用したアダプティブフォームの作成方法を説明します。アダプティブフォームは、情報の収集および処理を合理化するレスポンシブ HTML5 フォームです。フォームデータモデルと XML または JSON スキーマに基づいてアダプティブフォームを作成する方法について詳しく調べます。'
Keywords: create adaptive form core component, create core component based adaptive form, creare adaptive form
products: SG_EXPERIENCEMANAGER/6.5/FORMS
contentOwner: Khushwant Singh
topic-tags: Adaptive Forms
docset: aem65
role: Admin, Developer
feature: Adaptive Forms, Core Components
exl-id: ee596672-b0b5-42e9-a139-72f90287bf3b
source-git-commit: 4a8155f754d1f71354717f5eb22511baab110916
workflow-type: tm+mt
source-wordcount: '1731'
ht-degree: 98%

---

# コアコンポーネントベースのアダプティブフォームを作成 {#creating-an-adaptive-form-core-components}


<span class="preview">アドビでは、コアコンポーネントを使用して、[AEM Sites ページへのアダプティブフォームの追加](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)や[スタンドアロンのアダプティブフォームの作成](/help/forms/using/create-an-adaptive-form-core-components.md)を行うことをお勧めします。</span>

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form-core-components.html?lang=ja) |
| AEM 6.5 | この記事 |

<!--**Applies to:** ✅ Adaptive Form Core Components ❎ [Adaptive Form Foundation Components](/help/forms/using/create-adaptive-form.md).-->

アダプティブフォームを使用すると、魅力的でレスポンシブ、かつ動的でアダプティブなフォームを作成できます。AEM Forms は、アダプティブフォームをすばやく作成するための、ビジネスユーザーにとってわかりやすい UI を提供します。UI はクイックタブナビゲーションを備えており、アダプティブフォームを作成するための事前設定済みのテンプレート、スタイル設定、フィールド、送信オプションを簡単に選択することができます。

開始する前に、使用可能な Forms コンポーネントのタイプについて学習します。

* [アダプティブフォームコアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja)：標準化されたデータキャプチャコンポーネントです。これらのコンポーネントは、デジタル登録エクスペリエンスのカスタマイズ機能を提供し、開発時間を短縮し、メンテナンスコストを削減します。開発者は、これらのコンポーネントを簡単にカスタマイズし、スタイルを設定できます。これらの最新かつ拡張性の高いコンポーネントを活用してアダプティブフォームを開発することをお勧めします。

* [アダプティブフォーム基盤コンポーネント](creating-adaptive-form.md)：従来の（古い）データキャプチャコンポーネントです。引き続きこれらを使用して、既存の基盤コンポーネントベースのアダプティブフォームを編集できます。 フォームを作成する場合は、[アダプティブフォームコアコンポーネント](/help/forms/using/create-adaptive-form.md)を使用してアダプティブフォームを作成することをお勧めします。

## 前提条件

アダプティブフォームを作成するには、以下が必要です。

* **環境でのアダプティブフォームコアコンポーネントの有効化**：AEM アーキタイププロジェクトバージョン 41 以降は、[使用する環境でコアコンポーネントを有効にする](/help/forms/using/enable-adaptive-forms-core-components.md)ことが必要です。使用する環境でコアコンポーネントを有効にすると、**アダプティブフォーム（コアコンポーネント）**&#x200B;のテンプレートとカンバステーマが環境に追加されます。

* **アダプティブフォームテンプレート**：テンプレートは基本構造を提供し、アダプティブフォームのアピアランス（レイアウトとスタイル）を定義します。これには、特定のプロパティやコンテンツ構造を有するフォーマット済みのコンポーネントが含まれます。また、テーマと送信アクションを定義するオプションも提供されます。 テーマは、ルックアンドフィールと送信アクションを定義し、アダプティブフォームの送信時に実行するアクションを定義します。 また、[サンプルテンプレート](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html?lang=ja)を環境にデプロイできます。フォームの作成を迅速に開始することができます。

  >[!NOTE]
  >
  > ご利用の環境に&#x200B;**アダプティブフォーム（コアコンポーネント）**&#x200B;テンプレートがない場合は、[ご利用の環境のアダプティブフォームコアコンポーネントを有効にします](/help/forms/using/enable-adaptive-forms-core-components.md)。ご利用の環境でコアコンポーネントを有効にすると、**アダプティブフォーム（コアコンポーネント）**&#x200B;テンプレートが環境に追加されます。

* **アダプティブフォームのテーマ**：テーマには、コンポーネントとパネル向けのスタイル設定の詳細が含まれます。 スタイルには、背景カラー、ステートカラー、透明度、配置、サイズなどのプロパティが含まれます。テーマを適用すると、指定したスタイルが対応するコンポーネントに反映されます。使用する環境でコアコンポーネントを有効にすると、`Canvas` テーマがデフォルトで追加されます。[標準のテーマをダウンロードしてカスタマイズする](create-or-customize-themes-for-adaptive-forms-core-components.md)ことができます。**標準提供の**&#x200B;テーマとして、[サンプルテーマ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html?lang=ja)を環境にデプロイできます。これにより、フォームのスタイル設定を開始でき、ビジネス要件に応じてテーマを作成またはカスタマイズするための基本構造が提供されます。

* **権限**：[!DNL forms-users] グループにユーザーを追加します。[!DNL forms-users] グループのメンバーには、アダプティブフォームを作成する権限があります。フォーム専用のユーザーグループの詳細なリストについて詳しくは、[グループと権限](forms-groups-privileges-tasks.md)を参照してください。

<!--
>[!NOTE]
>
>
> In addition to the given themes and templates when you enable Core Components, you can also deploy the latest out-of-the box [sample themes and templates](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html) to your AEM environment for use in Core Components based Adaptive Forms.
-->

## アダプティブフォームを作成 {#create-an-adaptive-form}

1. ローカルの [AEM オーサーインスタンス](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html?lang=ja#author-and-publish-installs)にログインします。

1. Experience Manager のログインページに資格情報を入力します。ログイン後、左上隅の「 」を選択します。 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms &amp; Documents]**.

1. 選択 **[!UICONTROL 作成]**  > **[!UICONTROL アダプティブFormsの作成]**.

1. アダプティブフォームコアコンポーネントテンプレートを選択し、「**[!UICONTROL 次へ]**」をクリックします。

1. **[!UICONTROL プロパティを追加]**&#x200B;が表示されます。以下のプロパティフィールドの値を指定します。「タイトル」フィールドと「ドキュメント名」フィールドは必須です。

   * **[!UICONTROL タイトル：]**&#x200B;フォームの表示名を指定します。タイトルを指定すると、[!DNL Experience Manager Forms] ユーザーインターフェイス内のフォームを特定しやすくなります。
   * **[!UICONTROL 名前：]**&#x200B;フォームの名前を指定します。指定された名前のノードがリポジトリーに作成されます。タイトルを入力し始めると、名前フィールドの値が自動的に生成されます。候補として入力された値は変更可能です。名前フィールドには、英数字、ハイフン、アンダースコアのみを使用できます。
   * **[!UICONTROL 説明：]**&#x200B;フォームに関する詳細情報を入力します。
   * **[!UICONTROL テーマクライアントライブラリ]：**&#x200B;アダプティブフォームのテーマを指定します。デフォルトでは、`adaptiveform.theme.canvas3` のテーマが選択されています。また、**[!UICONTROL テーマクライアントライブラリ]**&#x200B;ドロップダウンメニューから別のテーマを選択できます。
   * **[!UICONTROL 設定コンテナ：]**&#x200B;アダプティブフォームの設定ファイルを保存する場所を定義します。これらの設定ファイルには、アダプティブフォームの動作と表示方法に関連する設定およびプロパティが含まれています。
   * **[!UICONTROL タグ：]**&#x200B;アダプティブフォームを一意に識別するためのタグを指定します。タグを指定すると、フォームを検索しやすくなります。タグを作成するには、「**[!UICONTROL タグ]**」ボックスに新しいタグ名を入力します。
1. 「**[!UICONTROL 作成]**」を選択します。アダプティブフォームが作成され、フォームを編集用に開くためのダイアログが表示されます。


1. 選択 **[!UICONTROL 編集]** をクリックして、新しく作成されたフォームを新しいタブで開きます。 フォームが編集用に開かれ、テンプレート内の利用可能なコンテンツが表示されます。また、新規作成されたフォームをカスタマイズするサイドバーも表示されます。


## アダプティブフォームのコアコンポーネントを使用してフォームを作成

フォームを編集用に開いた後、使用可能なアダプティブフォームのコアコンポーネントを使用して、フォームフィールドをフォームに追加できます。ドラッグ＆ドロップするか、「+ [コンポーネントを挿入]」オプションを使用して、これらのコンポーネントをフォームに追加できます。使用可能な[アダプティブフォームのコアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja#components)について詳しくは、AEM コアコンポーネントのドキュメントを参照してください。また、[https://aemcomponents.dev/](https://aemcomponents.dev/) では、使用可能なコアコンポーネントの動作を確認できます。

## アダプティブフォームの送信アクションを設定 {#configure-submit-action-for-form}

送信アクションを使用すると、アダプティブフォーム経由で取り込んだデータの送信先を選択できます。送信アクションは、ユーザーがアダプティブフォームの「送信」ボタンをクリックするとトリガーされます。アダプティブフォームには、すぐに使用できる送信アクションがいくつか含まれています。デフォルトの送信アクションを拡張して、独自のカスタム送信アクションを作成することもできます。フォームの送信アクションを設定するには、次の手順を実行します。

1. コンテンツブラウザーを開き、アダプティブフォームの&#x200B;**[!UICONTROL ガイドコンテナ]**&#x200B;コンポーネントを選択します。
1. ガイドコンテナプロパティ ![ガイドプロパティ](/help/forms/using/assets/configure-icon.svg) アイコンをクリックします。アダプティブフォームコンテナダイアログボックスが開きます。

1. 「**[!UICONTROL 送信]**」タブをクリックします。

   ![レンチアイコンをクリックしてアダプティブフォームコンテナダイアログボックスを開き、送信アクションを設定します](/help/forms/using/assets/adaptive-forms-submit-message.png)

1. 必要に応じて、**[!UICONTROL 送信アクション]**&#x200B;を選択して設定します。送信アクションについて詳しくは、[アダプティブフォームの送信アクション](/help/forms/using/configuring-submit-actions.md)を参照してください。

<!--
    
    ![Click the Wrench icon to open Adaptive Form Container dialog box to configure Data Models for the Adaptive Form Container component](/help/forms/assets/adaptive-forms-container.png)

-->

## ユーザーをページにリダイレクトするか、フォーム送信時にお礼のメッセージを表示

フォームの送信時に、ユーザーを別の web ページまたはメッセージにリダイレクトできます。ユーザーをリダイレクトするか、お礼のメッセージを設定するには、次の手順を実行します。

1. コンテンツブラウザーを開き、アダプティブフォームの&#x200B;**[!UICONTROL ガイドコンテナ]**&#x200B;コンポーネントを選択します。
1. ガイドコンテナプロパティ ![ガイドプロパティ](/help/forms/using/assets/configure-icon.svg) アイコンをクリックします。アダプティブフォームコンテナダイアログボックスが開きます。
1. 「**[!UICONTROL 送信]**」タブを開きます。

   ![レンチアイコンをクリックしてアダプティブフォームコンテナダイアログボックスを開き、リダイレクトページまたはお礼のメッセージを設定](/help/forms/using/assets/adaptive-forms-submit-message.png)

   * リダイレクト URL を設定するには、「送信」オプションで、「**[!UICONTROL URL にリダイレクト]**」オプションを選択し、AEM Sites ページを参照して選択するか、外部ページの URL を指定します。

   * カスタムメッセージまたはお礼のメッセージを設定するには、「送信」オプションで「**[!UICONTROL メッセージを表示]**」オプションを選択し、**[!UICONTROL メッセージコンテンツ]**&#x200B;ボックスにメッセージを入力します。これはリッチテキストボックスで、全画面表示オプションを使用して、使用可能なすべてのリッチテキスト項目を表示できます。

## アダプティブフォームのスキーマまたはフォームデータモデルを設定 {#configure-schema-or-data-model-for-form}

フォームデータモデルを使用してフォームをデータソースに接続し、ユーザーのアクションに基づいてデータを送受信することができます。また、フォームを JSON スキーマに接続して、送信されたデータを事前定義済みの形式で受信することもできます。必要に応じて、フォームを JSON スキーマまたはフォームデータモデルに接続します。

* [JSON スキーマを作成して環境にアップロード](/help/forms/using/adaptive-form-json-schema-form-model.md)
* [フォームデータモデルを作成](/help/forms/using/create-form-data-models.md)

### フォームの JSON スキーマまたはフォームデータモデルを設定

フォームの JSON スキーマまたはフォームデータモデルを設定するには：

1. コンテンツブラウザーを開き、アダプティブフォームの&#x200B;**[!UICONTROL ガイドコンテナ]**&#x200B;コンポーネントを選択します。
1. ガイドコンテナプロパティ ![ガイドプロパティ](/help/forms/using/assets/configure-icon.svg) アイコンをクリックします。アダプティブフォームコンテナダイアログボックスが開きます。
1. 「**[!UICONTROL データモデル]**」タブを開きます。

   ![レンチアイコンをクリックしてアダプティブフォームコンテナダイアログボックスを開き、JSON スキーマまたはフォームデータモデルを設定](/help/forms/using/assets/adaptive-forms-select-form-data-model-or-json-schema.png)

1. 要件に応じて、JSON スキーマまたはフォームデータモデルを選択し、設定します。

   * 「**[!UICONTROL フォームモデル]**」オプションを選択する場合は、「**[!UICONTROL フォームデータモデルを選択]**」オプションを使用して、事前設定済みのフォームデータモデルを選択します。
   * 「**[!UICONTROL スキーマ]**」オプションを選択する場合は、「**[!UICONTROL スキーマ]**」オプションを使用して、フォームの JSON スキーマを選択します。

1. 「**[!UICONTROL 完了]**」をクリックします。

>[!NOTE]
>
> ガイドコンテナプロパティを使用して、アダプティブフォームの JSON スキーマやフォームデータモデルを編集できます。

## 事前入力サービスを設定  {#configure-prefill-service-for-form}

事前入力サービスを使用すると、既存のデータを使用してアダプティブフォームのフィールドに自動入力できます。ユーザーがフォームを開くと、これらのフィールドの値は事前入力されています。以下の操作を実行できます。

* [カスタム事前入力サービスを作成](/help/forms/using/prepopulate-adaptive-form-fields.md)
* [フォームデータモデルの事前入力サービスを使用](#fdm-prefill-service)

### フォームデータモデルの事前入力サービスを使用して、アダプティブフォームのフィールドに事前入力 {#fdm-prefill-service}

フォームデータモデルの事前入力サービスでは、フォームデータモデル事前入力サービス、またはカスタムの事前入力サービスを使用して、アダプティブフォームのフィールドに事前入力できます。フォームデータモデルの事前入力サービスでは、[設定済みのフォームデータモデルのサービスを取得](work-with-form-data-model.md#add-data-model-objects-and-services-add-data-model-objects-and-services)を使用して、データを取得します。アダプティブフォームでフォームデータモデルの事前入力サービスを使用するには、次の手順を実行します。

1. コンテンツブラウザーを開き、アダプティブフォームの&#x200B;**[!UICONTROL ガイドコンテナ]**&#x200B;コンポーネントを選択します。
1. ガイドコンテナプロパティ ![ガイドプロパティ](/help/forms/using/assets/configure-icon.svg) アイコンをクリックします。アダプティブフォームコンテナダイアログボックスが開きます。
1. アダプティブフォームコンテナプロパティ（![アダプティブフォームコンテナプロパティ](/help/forms/using/assets/configure-icon.svg)アイコン）をクリックします。データモデルを設定するためのアダプティブフォームコンテナダイアログボックスが開きます。
   ![レンチアイコンをクリックしてアダプティブフォームコンテナダイアログボックスを開き、リダイレクトページまたはお礼のメッセージを設定](/help/forms/using/assets/adaptive-forms-container-prefill-service.png)
1. フォームデータモデルを選択. 「**[!UICONTROL 基本]**」タブを開きます。事前入力サービスで、「**[!UICONTROL フォームデータモデルの事前入力サービス]**」を選択します。
1. 「**[!UICONTROL 完了]**」をクリックします。これで、アダプティブフォームがフォームデータモデルの事前入力を使用するように設定されました。[ルールエディター](rule-editor.md)を使用して、フォームのフィールドに事前入力するルールを作成できるようになりました。

<!--
## Edit Form Model properties of an Adaptive Form {#edit-form-model}

1. Select the Adaptive Form and select ![Page information](/help/forms/using/assets/configure-icon.svg) > **[!UICONTROL Open Properties]**. The Form Properties page opens. 

1. Go to the **[!UICONTROL Form Model]** tab and choose a form model. If the Adaptive Form is without a form model, you have the freedom to choose either a JSON schema or a form data model. On the other hand, if the Adaptive Form is already based on a form model, you have the option to switch to another form model of the same type. For instance, if the form is using a JSON schema, you can easily switch to another JSON schema, and similarly if the form is using a Form Data Model, you can switch to another Form Data Model. 

1. Select **[!UICONTROL Save]** to save the properties.
-->

## 次の手順

* [ルールエディターを使用してフォームに動的な動作を追加](rule-editor.md)
* [コアコンポーネントベースのアダプティブフォームのテーマを作成またはカスタマイズ](create-or-customize-themes-for-adaptive-forms-core-components.md)


## 関連トピック

* [コアコンポーネントベースのアダプティブフォームを作成](create-an-adaptive-form-core-components.md)
* [AEM Sites ページまたはエクスペリエンスフラグメントにアダプティブフォームを作成または追加](create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [サンプルのテーマテンプレートおよびフォームデータモデル](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html?lang=ja)
