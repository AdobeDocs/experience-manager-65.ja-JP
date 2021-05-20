---
title: アダプティブフォームの作成方法
description: ' [!DNL Experience Manager Forms]を使用してアダプティブフォームを作成する方法を説明します。 アダプティブフォームとは、情報の処理・収集を効率化するレスポンシブな HTML5 フォームのことです。フォームデータモデル、XFAフォームテンプレート、XMLまたはJSONスキーマに基づくアダプティブフォームの作成方法を詳しく説明します。 '
feature: アダプティブフォーム
role: Business Practitioner, Developer
level: Beginner
exl-id: 2c25a8b7-73f7-40fb-a303-9446a708c8eb
source-git-commit: ad67634278088f8f953fde61a3543acdd70537dd
workflow-type: tm+mt
source-wordcount: '1858'
ht-degree: 86%

---

# アダプティブフォームの作成 {#creating-an-adaptive-form}

## <strong>アダプティブフォームの作成</strong> {#strong-create-an-adaptive-form-strong}

次の手順を実行して、アダプティブフォームを作成します。

1. `https://'[server]:[port]'/<custom-context-if-any>.`で[!DNL Experience Manager Forms]オーサーインスタンスにアクセスする

1. Experience Manager のログインページに資格情報を入力します。

   ログイン後、左上隅の **[!UICONTROL Adobe Experience Manager]**／**[!UICONTROL フォーム]**／**[!UICONTROL フォームとドキュメント]**&#x200B;をタップします。

   >[!NOTE]
   >
   >デフォルトのインストールでは、ログインは `admin`、パスワードは `admin` に設定されています。

1. 「**[!UICONTROL 作成]**」をタップして、「**[!UICONTROL アダプティブフォーム]**」を選択します。
1. テンプレートを選択するためのオプションが表示されます。テンプレートについて詳しくは、「[アダプティブフォームテンプレート](creating-adaptive-form.md#p-adaptive-form-templates-p)」を参照してください。 テンプレートをタップして選択し、「次へ」をタップします。
1. 「プロパティの追加」オプションが表示されます。以下のプロパティフィールドの値を指定します。「タイトル」フィールドと「ドキュメント名」フィールドは必須です。

   * **[!UICONTROL タイトル：]**&#x200B;フォームの表示名を指定します。タイトルを指定すると、[!DNL Experience Manager Forms] ユーザーインターフェイス内のフォームを特定しやすくなります。
   * **[!UICONTROL 名前：]**&#x200B;フォームの名前を指定します。指定された名前を持つノードがリポジトリに作成されます。タイトルを入力し始めると、名前フィールドの値が自動的に生成されます。候補として入力された値は変更可能です。「ドキュメント名」フィールドには、英数字、ハイフン、アンダースコアのみを使用できます。無効な入力は、すべてハイフンに置き換えられます。
   * **[!UICONTROL 説明：]**&#x200B;フォームに関する詳細情報を指定します。
   * **[!UICONTROL タグ：]**&#x200B;アダプティブフォームを識別するための固有タグを指定します。タグを指定すると、フォームを検索しやすくなります。タグを作成するには、「**[!UICONTROL タグ]**」ボックスに新しいタグ名を入力します。

1. 次のフォームモデルの 1 つを基にアダプティブフォームを作成することができます。

   * [フォームデータモデル](#fdm)
   * [XFA フォームテンプレート](#create-an-adaptive-form-based-on-an-xfa-form-template)
   * [XML または JSON スキーマ](#create-an-adaptive-form-based-on-xml-or-json-schema)
   * なし、またはフォームモデルを使用しない

   これらは、**[!UICONTROL プロパティを追加]**&#x200B;ページの「**[!UICONTROL フォームモデル]**」タブから設定できます。デフォルトで選択されているフォームモデルは、「**[!UICONTROL なし]**」です。

1. 「**[!UICONTROL 作成]**」をタップします。アダプティブフォームが作成され、フォームを編集用に開くためのダイアログが表示されます。

   すべてのプロパティの指定が完了したら、「**[!UICONTROL 作成]**」をクリックします。 アダプティブフォームが作成され、フォームを編集用に開くためのダイアログが表示されます。

   すべてのプロパティの指定が完了したら、「**[!UICONTROL 作成]**」をクリックします。 アダプティブフォームが作成され、フォームを編集用に開くためのダイアログが表示されます。

1. 「**[!UICONTROL 開く]**」をタップし、新しく作成されたフォームを新しいタブで開きます。フォームが編集用に開かれ、テンプレート内の利用可能なコンテンツが表示されます。新しく作成されたフォームを必要に応じてカスタマイズするためのサイドバーも表示されます。

   アダプティブフォームのタイプにより、関連付けられた XFA フォームテンプレート、XML スキーマまたは JSON スキーマに存在するフォーム要素が、サイドバーにある&#x200B;**[!UICONTROL コンテンツブラウザー]**&#x200B;の「**[!UICONTROL データモデルオブジェクト]**」タブに表示されます。これらの要素もアダプティブフォームにドラッグアンドドロップすることができます。

   アダプティブフォームのオーサリングインターフェースと使用可能なコンポーネントについて詳しくは、「[アダプティブフォームの作成について](introduction-forms-authoring.md)」を参照してください。

   >[!NOTE]
   >
   >新しく作成されたフォームを新しいタブで開くには、ブラウザでポップアップを許可してください。

## フォームデータモデルに基づくアダプティブフォームの作成 {#fdm}

[[!DNL Experience Manager Forms]  のデータ統合機能](data-integration.md)では、複数のデータソースを統合し、エンティティとサービスをまとめてフォームデータモデルを作成します。これは、JSON スキーマの拡張機能です。フォームデータモデルを使用してアダプティブフォームを作成することができます。フォームデータモデル内で設定されたエンティティまたはデータモデルオブジェクトは、フォームのオーサリングのデータモデルオブジェクトとして使用できます。これらは各データソースに結合され、フォームの事前入力や送信済みデータの各データソースへの書き戻しに使用されます。アダプティブフォームのルールを使用して、フォームデータモデル内に設定されたサービスを呼び出すこともできます。

フォームデータモデルを使用してアダプティブフォームを作成するには：

1. プロパティを追加画面の「フォームモデル」タブで、**[!UICONTROL 次から選択]**&#x200B;ドロップダウンリストから「**[!UICONTROL フォームデータモデル]**」を選択します。

   ![create-af-1-1](assets/create-af-1-1.png)

1. 「**[!UICONTROL フォームデータモデルを選択]**」をタップして展開します。すべての有効なフォームデータモデルが一覧表示されます。

   任意のフォームデータモデルを選択します。

   ![create-af-2-1](assets/create-af-2-1.png)

>[!NOTE]
>
>アダプティブフォームのフォームデータモデルを変更することもできます。詳しい手順については、「[アダプティブフォームのフォームモデルのプロパティを編集する](#edit-form-model)」を参照してください。

## XFA フォームテンプレートに基づくアダプティブフォームの作成 {#create-an-adaptive-form-based-on-an-xfa-form-template}

アダプティブフォームを作成する際に、XFA フォームテンプレートを再利用することができます。再利用するには、XFA フォームテンプレートをアップロードし、アダプティブフォームに関連付けます。フォームテンプレート（XFA フォーム）の要素が、アダプティブフォームの作成時にコンテンツファインダーで利用できるようになります。フォームテンプレート要素は、コンテンツファインダーからフォームへとドラッグ＆ドロップすることができます。

<!-- >>[!NOTE]
>
>[Upload the XFA Form Template](get-xdp-pdf-documents-aem.md) to AEM Forms before you start creating an adaptive form based on the form template.

Do the following to use an XFA form template as form model for your adaptive form:

1. On the **[!UICONTROL Add Properties]** page, open the **[!UICONTROL Form Model]** tab.
1. In the Form Model tab, from the drop-down list, select **[!UICONTROL Form Templates]**. All the form templates that are uploaded to the repository via AEM Forms UI are listed for selection. Select a template from the list.

   ![Associate XFA Form Template with an Adaptive Form](assets/form_model_xfa_associate.png)
**Figure:** *Selecting a form template*

   >[!NOTE]
   >
   >You can also change the form template for an adaptive form. For detailed steps, see [Edit Form Model properties of an adaptive form](#edit-form-model). -->

## XML スキーマまたは JSON スキーマに基づくアダプティブフォームの作成 {#create-an-adaptive-form-based-on-xml-or-json-schema}

XML スキーマおよび JSON スキーマは、組織内のバックエンドシステムによってデータが作成または使用される構造を表します。スキーマをアダプティブフォームに関連付け、その要素を使用して、アダプティブフォームに動的なコンテンツを追加することができます。 スキーマの要素は、アダプティブフォームのオーサリング用に、コンテンツブラウザーの「データモデルオブジェクト」タブで使用できます。 スキーマ要素をドラッグ＆ドロップしてフォームを作成できます。

アダプティブフォームのオーサリングのための XML または JSON スキーマの設計方法について理解するには、次のドキュメントを参照してください。

* [XMLスキーマを使ったアダプティブフォームの作成](adaptive-form-xml-schema-form-model.md)
* [JSON スキーマを使用したアダプティブフォームの作成](adaptive-form-json-schema-form-model.md)

アダプティブフォームのフォームモデルとして XML または JSON スキーマを使用するには、次のことを行ってください。

1. アダプティブフォーム作成ページの&#x200B;**[!UICONTROL プロパティの追加]**&#x200B;手順で、「**[!UICONTROL フォームモデル]**」タブをタップします。
1. 「フォームモデル」のタブで、**[!UICONTROL 次から選択]**&#x200B;ドロップダウンから「**[!UICONTROL スキーマ]**」を選択します。

1. 「**[!UICONTROL スキーマを選択]**」をタップして、以下のいずれかの操作を行います。

   * **[!UICONTROL ディスクからアップロード]** - このオプションを選択して、「スキーマ定義をアップロード」をタップし、ファイルシステムから XML スキーマまたは JSON スキーマを参照してアップロードします。アップロードされたスキーマファイルはフォームとともに保存されますが、他のアダプティブフォームからアクセスすることはできません。
   * **[!UICONTROL リポジトリを検索]** - このオプションを選択して、リポジトリで使用できるスキーマ定義ファイルのリストから選択します。XML または JSON スキーマファイルをフォームモデルとして選択します。選択したスキーマは参照によってフォームに関連付けられ、他のアダプティブフォームで使用するためにアクセスできます。

   >[!CAUTION]
   >
   >JSON スキーマファイル名が **.schema.json** で終わることを確認してください。例：mySchema.schema.json

   ![XML または JSON スキーマの選択](assets/upload-schema.png)
   **図：***XML または JSON スキーマの選択*

1. （XML スキーマのみ）XML スキーマを選択またはアップロードした後、選択した XSD ファイルのルートエレメントを指定してアダプティブフォームにマッピングします。

   ![XSD ルート要素の選択](assets/xsd-root-element.png)
   **図：***XSD ルート要素の選択*

>[!NOTE]
>
>アダプティブフォームのスキーマを変更することもできます。詳しい手順については、「[アダプティブフォームのフォームモデルのプロパティを編集する](#edit-form-model)」を参照してください。

## アダプティブフォームテンプレート {#adaptive-form-templates}

テンプレートでは基本的がい造を提供しており、アダプティブフォームの外観（レイアウトやスタイル）を定義します。これには、特定のプロパティやコンテンツ構造を有するフォーマット済みのコンポーネントが含まれます。<!-- Out of the box, AEM Forms provides some adaptive form templates. To get the complete template package including advanced templates, you need to install the AEM Forms add-on package. For more information, see [Installing AEM Forms add-on package](installing-configuring-aem-forms-osgi.md).-->

さらに、テンプレートエディターを使用して独自のテンプレートを作成できます。テンプレートの操作について詳しくは、「[アダプティブフォームテンプレート](template-editor.md)」を参照してください。

>[!NOTE]
>
>拡張テンプレートを使用してアダプティブフォームを作成し、そのフォームを編集用として開くと、エラーメッセージが表示されます。拡張テンプレートには署名ステップコンポーネントがあり、デフォルトで Adobe Sign が有効になっています。このエラーを修正するには、[Adobe Sign のクラウド設定](adobe-sign-integration-adaptive-forms.md)を作成して選択し、[署名者を設定](working-with-adobe-sign.md#addsignerstoanadaptiveform)してください。

## アダプティブフォームのフォームモデルプロパティの編集  {#edit-form-model}

アダプティブフォームはフォームモデルを使用せずに（フォームモデルの「なし」オプションを使用して）作成することも、フォームモデル（フォームテンプレート、XML スキーマ、JSON スキーマなど）を使用して作成することもできます。アダプティブフォームのフォームデータモデルを「なし」から別のフォームモデルに変更することもできます。フォームモデルをベースとするアダプティブフォームでは、同じフォームモデルに別のフォームテンプレート、XML スキーマ、JSON スキーマ、フォームデータモデルを選択することもできます。ただし、フォームモデルを別のフォームモデルに変更することはできません。

1. アダプティブフォームを選択し、「**プロパティ**」アイコンをタップします。
1. 「**[!UICONTROL フォームモデル]**」タブを開き、以下のいずれかを実行します。

   * アダプティブフォームにフォームモデルが無い場合、別のフォームモデルを選択し、それに従いフォームテンプレート、XML スキーマ、JSON スキーマ、フォームデータモデルを選択することもできます。
   * アダプティブフォームがフォームモデルをベースとしている場合は、同じフォームモデルに別のフォームテンプレート、XML スキーマ、JSON スキーマ、フォームデータモデルを選択することもできます。

1. 「**[!UICONTROL 保存]**」をタップして、プロパティを保存します。

## アダプティブフォームの自動保存 {#auto-save-an-adaptive-form}

デフォルトでは、アダプティブフォームのコンテンツは、保存ボタンを押したときなど、ユーザーアクション時に保存されます。アダプティブフォームを設定して、イベントまたは時間間隔に基づいてコンテンツの自動保存を開始することができます。自動保存オプションは次のようなときに便利です。

* 匿名ユーザーおよびログインユーザーに対してコンテンツを自動保存する
* ユーザーの介在をほとんどあるいはまったく必要としないでフォームのコンテンツを保存する
* ユーザーのイベントに基づいてフォームのコンテンツの保存を開始する
* 特定の時間間隔が経過したらフォームのコンテンツを繰り返し保存する

### アダプティブフォームの自動保存の有効化  {#enable-auto-save-for-an-adaptive-form}

デフォルトでは、この自動保存オプションは無効になっています。自動保存オプションの有効化は、アダプティブフォームの「自動保存」タブで行うことができます。「自動保存」タブには、その他の設定オプションがいくつか用意されています。次の手順を実行して、アダプティブフォームの自動実行オプションを有効にし設定します。

1. プロパティの「自動保存」セクションにアクセスするには、コンポーネントを選択し、![フィールドレベル](assets/field-level.png) / **[!UICONTROL アダプティブフォームコンテナ]**&#x200B;をタップしてから、![cmppr](assets/cmppr.png)をタップします。
1. 「**[!UICONTROL 自動保存]**」セクションで、自動保存オプションを&#x200B;**[!UICONTROL 有効]**&#x200B;にします。
1. 「**[!UICONTROL アダプティブフォームイベント]**」ボックスで、1 または TRUE を指定して、フォームがブラウザーに読み込まれたときに自動保存を開始します。トリガーされると true を返してフォームのコンテンツの保存を開始する条件式をイベントに指定することもできます。
1. トリガーを指定します。設定に従い、自動保存がトリガーされます。以下のオプションがあります。

   * **[!UICONTROL 時刻に基づいた自動保存]**：特定の時間間隔に基づいてコンテンツの保存を開始するには、このオプションを選択します。
   * **[!UICONTROL イベントに基づいた自動保存]**：イベントがトリガーされたときにコンテンツの保存を開始するには、このオプションを選択します。

   トリガーを選択すると、方法の設定ボックスが有効になります。方法の設定ボックスでは、次のことができます。

   * **[!UICONTROL 時刻に基づいた自動保存]**&#x200B;トリガーを選択した場合は、時間間隔を指定します。
   * 「**[!UICONTROL イベントに基づく]**」トリガーを選択した場合は、イベント名を指定します。

   <!-- You can also create and add your own custom strategy to the list. For details, see [Implement a custom strategy to autosave the forms](auto-save-an-adaptive-form.md#p-implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms-p). -->

1. （時間ベースの自動保存のみ）次の手順を実行して、時間ベースの自動保存のオプションを設定します。

   1. 「**[!UICONTROL この間隔で自動保存]**」ボックスで、時間間隔を秒数で指定します。「間隔」ボックスに指定されている秒数が経過するたびに、フォームは繰り返し保存されます。

1. （イベントベースの自動保存のみ）次の手順を実行して、イベントベースの自動保存のためのオプションを設定します。

   1. 「**[!UICONTROL このイベントで自動保存]**」ボックスで、[GuideBridge](https://helpx.adobe.com/jp/aem-forms/6/javascript-api/GuideBridge.html) イベントを指定します。式が TRUE に評価されるたびに、フォームが保存されます。

1. （オプション）匿名ユーザーに対するコンテンツを自動保存するには、「**[!UICONTROL 匿名のユーザーの自動保存を有効にする]**」オプションを選択し、「**[!UICONTROL OK]**」をクリックします。

   >[!NOTE]
   >
   >自動保存オプションが匿名ユーザーに対して機能するには、すべてのユーザーにフォームのプレビュー、確認および署名を許可するように Forms Common Configuration Service が設定されていることを確認します。
   >
   >サービスを設定するには、`https://'[server]:[port]'system/console/configMgr`にあるAdobe Experience Manager Webコンソール設定に移動し、**[!UICONTROL Forms Common Configuration Service]**&#x200B;を編集して、**[!UICONTROL Allow]**&#x200B;フィールドの「**[!UICONTROL All Users]**」オプションを選択し、設定を保存します。
