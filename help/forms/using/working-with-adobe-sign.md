---
title: アダプティブフォームで Adobe Sign を使用する
seo-title: Using Adobe Sign in an adaptive form
description: アダプティブフォームで電子署名（Adobe Sign）ワークフローを有効にすると、署名ワークフローが自動化され、単一署名プロセスと複数署名プロセスが簡素化されるほか、モバイルデバイスでフォームを電子的に署名できるようになります。
seo-description: Enable e-signature (Adobe Sign) workflows for an adaptive form to automate signing workflows, simplify single and multi-signature processes, and to electronically sign forms from mobile devices.
uuid: cc3012ed-c318-4529-9adc-61aa5b5761a0
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: f79828d8-2230-4477-8ffa-eeb6a0413acd
docset: aem65
feature: Adaptive Forms, Adobe Sign
exl-id: a8decba9-229d-40a2-992a-3cc8ebefdd6d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '3826'
ht-degree: 100%

---

# アダプティブフォームでの [!DNL Adobe Sign] の使用{#using-adobe-sign-in-an-adaptive-form}

[!DNL Adobe Sign] を使用すると、アダプティブフォームの電子署名ワークフローを利用できます。電子署名を利用すると、法務、販売、給与、人事管理など分野でドキュメントを処理するワークフローを改善できます。

[!DNL Adobe Sign] とアダプティブフォームの一般的なシナリオでは、ユーザーがアダプティブフォームに入力してサービスを申し込みます。例えば、住宅ローンやクレジットカードの申請では、すべての借り手や共同申請者から、法的に有効な署名を取得する必要があります。これに類似したシナリオで電子署名ワークフローを有効にするには、[!DNL Adobe Sign] を AEM [!DNL Forms] に統合します。例えば、[!DNL Adobe Sign] を使用して、以下のような処理を実行できます。

* 完全に自動化された提案プロセス、見積りプロセス、契約プロセスを使用して、任意のデバイスで契約を締結する。
* 人事プロセスを短時間で完了し、従業員に対してデジタルエクスペリエンスを提供する。
* 契約のサイクルタイムを短縮し、ベンダーとの取引を早期に開始する。
* 共通するプロセスを自動化するためのデジタルワークフローを作成する。

[!DNL Adobe Sign] と AEM [!DNL Forms] を統合することにより、次の機能がサポートされます。

* 単一ユーザーと複数ユーザーの署名ワークフローを処理する機能
* 複数の署名ワークフローを並列的に順次処理する機能
* フォーム内とフォーム外での署名機能
* 匿名ユーザーまたはログインユーザーとしてフォームを署名する機能
* 署名プロセスを動的に処理する機能（AEM [!DNL Forms] のワークフローと統合）
* ナレッジベース、電話、ソーシャルプロファイルによる認証機能

[アダプティブフォームで Adobe Sign を使用するためのベストプラクティス](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684)を確認して、より良い署名体験を作成してください。

## 前提条件 {#prerequisites}

アダプティブフォームで [!DNL Adobe Sign] を使用する前に：

* [!DNL Adobe Sign] を使用するように AEM [!DNL Forms] クラウドサービスが設定されていることを確認してください。詳細については、[Adobe Sign の AEM Forms への統合](../../forms/using/adobe-sign-integration-adaptive-forms.md)を参照してください。
* 署名者のリストが準備されていること。少なくとも、各署名者の電子メールアドレスが必要になります。

## アダプティブフォームへの [!DNL Adobe Sign] の設定 {#configure-adobe-sign-for-an-adaptive-form}

アダプティブフォームに [!DNL Adobe Sign] を設定するには、以下の手順を実行します。

1. [アダプティブフォームのプロパティを Adobe Sign 用に編集する](../../forms/using/working-with-adobe-sign.md#enableadobesign)
1. [アダプティブフォームに Adobe Sign のフィールドを追加する](../../forms/using/working-with-adobe-sign.md#addadobesignfieldstoanadaptiveform)
1. [アダプティブフォームで Adobe Sign を有効にする](../../forms/using/working-with-adobe-sign.md#enableadobsignforanadaptiveform)
1. [アダプティブフォームで Adobe Sign Cloud Service を選択する](../../forms/using/working-with-adobe-sign.md#selectadobesigncloudserviceforanadaptiveform)

1. [アダプティブフォームに Adobe Sign の署名者を追加する](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform)
1. [アダプティブフォームで送信アクションを選択する](../../forms/using/working-with-adobe-sign.md#selectsubmitactionforanadaptiveform)

![署名者の詳細](assets/signer_details_new.png)

### アダプティブフォームのプロパティを [!DNL Adobe Sign] 用に編集する {#enableadobesign}

既存または新規のアダプティブフォームに対して、[!DNL Adobe Sign] 用のアダプティブフォームのプロパティを設定します。

[アダプティブフォームを Adobe Sign 用に作成する](../../forms/using/working-with-adobe-sign.md#create-an-adaptive-form-for-adobe-sign)では、基本的なアダプティブフォームを作成する手順を説明します。アダプティブフォームの作成時に使用できるその以外のオプションについては、[アダプティブフォームの作成](../../forms/using/creating-adaptive-form.md)を参照してください。

#### アダプティブフォームを [!DNL Adobe Sign] 用に作成する {#create-an-adaptive-form-for-adobe-sign}

署名が有効なアダプティブフォームを作成するには、以下の手順を実行します。

1. **[!UICONTROL Adobe Experience Manager]**／**[!UICONTROL Forms]**／**[!UICONTROL フォームとドキュメント]**&#x200B;に移動します。
1. 「**[!UICONTROL 作成]**」をタップして、「**[!UICONTROL アダプティブフォーム]**」を選択します。テンプレートのリストが表示されます。テンプレートを選択して、「**[!UICONTROL 次へ]**」をタップします。
1. 「**[!UICONTROL 基本]**」タブで次の操作を行います。

   1. アダプティブフォームの&#x200B;**[!UICONTROL 名前]**&#x200B;と&#x200B;**[!UICONTROL タイトル]**&#x200B;を指定します。

   1. [!DNL Adobe Sign] を AEM [!DNL Forms] で設定するときに作成した[設定コンテナ](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms)を選択します。

      >[!NOTE]
      >
      >**[!UICONTROL Adobe Sign Cloud Service]** ドロップダウンリストには、このフィールドで選択した設定コンテナで設定されたクラウドサービスが表示されます。**[!UICONTROL Adobe Sign Cloud Service]** ドロップダウンリストは、「**[!UICONTROL Adobe Signを有効にする]**」オプションを選択すると、アダプティブフォームプロパティの「**[!UICONTROL 電子署名]**」セクションで使用できます。

1. 「**[!UICONTROL フォームモデル]**」タブで、次のいずれかのオプションを選択します。

   * 「**[!UICONTROL フォームテンプレートをレコードのドキュメントテンプレートとして関連付ける]**」オプションを選択し、「レコードのドキュメント」テンプレートを選択します。フォームテンプレートベースのアダプティブフォームを使用する場合、署名用として送信されたドキュメントには、関連するフォームテンプレートに基づくフィールドだけが表示されます。表示されないアダプティブフォームのフィールドもあります。

   * 「**[!UICONTROL レコードのドキュメントを生成]**」オプションを選択します。「レコードのドキュメント」オプションが有効なアダプティブフォームを使用すると、署名用に送信されたドキュメントにアダプティブフォームのすべてのフィールドが表示されます。

1. 「**[!UICONTROL 作成」をタップします。]** 署名が有効なアダプティブフォームが作成され、このアダプティブフォームを使用して [!DNL Adobe Sign] フィールドを追加できます。

#### アダプティブフォームを [!DNL Adobe Sign] 用に編集する {#editafsign}

既存のアダプティブフォームで [!DNL Adobe Sign] を使用するには、次の手順を実行します。

1. **[!UICONTROL Adobe Experience Manager]**／**[!UICONTROL Forms]**／**[!UICONTROL フォームとドキュメント]**&#x200B;に移動します。
1. アダプティブフォームを選択し、**[!UICONTROL プロパティ]**&#x200B;をタップします。
1. 「**[!UICONTROL 基本]**」タブで、[!DNL Adobe Sign] を AEM [!DNL Forms] で設定するときに作成した[設定コンテナ](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms)を選択します。
1. 「**[!UICONTROL フォームモデル]**」タブで、次のいずれかのオプションを選択します。

   * 「**[!UICONTROL フォームテンプレートをレコードのドキュメントテンプレートとして関連付ける]**」オプションを選択し、「レコードのドキュメント」テンプレートを選択します。フォームテンプレートベースのアダプティブフォームを使用する場合、署名用として送信されたドキュメントには、関連するフォームテンプレートに基づくフィールドだけが表示されます。表示されないアダプティブフォームのフィールドもあります。

   * 「**[!UICONTROL レコードのドキュメントを生成]**」オプションを選択します。「レコードのドキュメント」オプションが有効なアダプティブフォームを使用すると、署名用に送信されたドキュメントにアダプティブフォームのすべてのフィールドが表示されます。

1. 「**[!UICONTROL 保存して閉じる]**」をタップします。アダプティブフォームは [!DNL Adobe Sign] に対して有効になっています。

### Adobe Sign のフィールドをアダプティブフォームに追加する {#addadobesignfieldstoanadaptiveform}

[!DNL Adobe Sign] には、アダプティブフォーム上に配置できる様々なフィールドが用意されています。これらのフィールドには、署名、イニシャル、会社名、タイトルなど、様々なタイプのデータを入力することができます。このため、署名が行われる際に署名だけでなく追加情報を収集できます。[!DNL Adobe Sign] ブロックコンポーネントを使用して、アダプティブフォームの様々な場所に [!DNL Adobe Sign] のフィールドを配置できます。

アダプティブフォームにフィールドを追加し、それらのフィールドに関する各種のオプションをカスタマイズするには、以下の手順を実行します。

1. **[!UICONTROL Adobe Sign ブロック]**&#x200B;コンポーネントを、コンポーネントブラウザーからアダプティブフォームにドラッグアンドドロップします。[!DNL Adobe Sign] ブロックコンポーネントには、サポート対象のすべての [!DNL Adobe Sign] フィールドが含まれています。デフォルトでは、**署名**&#x200B;フィールドがアダプティブフォームに追加されます。

   ![署名ブロック](assets/sign_block_new.png)

   デフォルトでは、公開済みアダプティブフォームに [!DNL Adobe Sign] ブロックは表示されません。Adobe Sign ブロックが表示されるのは、署名ドキュメントだけです。[!DNL Adobe Sign] ブロックの表示設定は、[!DNL Adobe Sign] ブロックコンポーネントのプロパティで変更できます。

   >[!NOTE]
   >
   >    * アダプティブフォームで [!DNL Adobe Sign] を使用する場合、[!DNL Adobe Sign] ブロックの使用は必須ではありません。[!DNL Adobe Sign] ブロックを使用せずに署名者用のフィールドを追加すると、署名ドキュメントの下部にデフォルトの署名フィールドが表示されます。
   >    * レコードのドキュメントが自動的に生成されるアダプティブフォームの場合のみ、[!DNL Adobe Sign] ブロックを使用してください。カスタムの XDP を使用して、レコードのドキュメントやフォームテンプレートベースのアダプティブフォームを生成する場合は、[!DNL Adobe Sign] ブロックはサポートされていません。


1. **[!UICONTROL Adobe Sign ブロック]**&#x200B;コンポーネントを選択し、「**編集** ![aem_6_3_edit](assets/aem_6_3_edit.png)」アイコンをタップします。フィールドを追加するためのオプションと、フィールドの外観を設定するためのオプションが表示されます。

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **A.** [!DNL Adobe Sign] フィールドを選択して追加。**B.** [!DNL Adobe Sign] ブロックを展開して全画面表示。

1. 「**[!UICONTROL Adobe Sign] フィールド** ![aem_6_3_adobesign](assets/aem_6_3_adobesign.png)」アイコンをタップします。[!DNL Adobe Sign] フィールドの選択オプションと追加オプションが表示されます。

   **[!UICONTROL タイプ]**&#x200B;ドロップダウンフィールドを展開して [!DNL Adobe Sign] フィールドを選択し、「完了」アイコン（![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)）をタップして、選択したフィールドを [!DNL Adobe Sign] ブロックに追加します。「**[!UICONTROL タイプ]**」ドロップダウンフィールドには、「署名」タイプ、「署名者の情報」タイプ、「データフィールド」タイプが表示されます。[!DNL Adobe Sign] が AEM に統合されている場合、[!DNL Forms] は「[!UICONTROL タイプ]」ドロップダウンボックスに表示されているフィールドのみサポートします。[!DNL Adobe Sign] フィールドについて詳しくは、[Adobe Sign のドキュメント](https://helpx.adobe.com/jp/sign/using/field-types.html)を参照してください。

   ![adobe-sign-block-fields-options](assets/adobe-sign-block-fields-options.png)

   フィールドには、必ず一意の名前を指定する必要があります。フィールドを必須フィールドとしてマークするための必須オプションを選択することもできます。[!DNL Adobe Sign] の一部のフィールドには、「**[!UICONTROL 名前]**」オプションと「**[!UICONTROL 必須]**」オプションのほかに、追加のオプションが用意されています。例えば、マスクや複数行のオプションなどです。また、フィールドが [!DNL Adobe Sign] の同じブロック内に存在するか別のブロック内に存在するかを問わず、[!DNL Adobe Sign] の各フィールドに一意の名前を指定できます。

   ドロップダウンリストから「**[!UICONTROL デジタル署名]**」を選択すると、アダプティブフォームにデジタル署名を適用できます。

   * オンラインでクラウド署名を使用し、トラストサービスプロバイダーがホストする[デジタル ID](https://helpx.adobe.com/jp/sign/kb/digital-certificate-providers.html) を使用する。
   * ローカルにドキュメントをダウンロードして、Adobe Acrobat または Adobe Acrobat Reader でスマートカード、USB トークン、ファイルベースのデジタル ID を使用する。

### アダプティブフォームでの [!DNL Adobe Sign] の有効化 {#enableadobsignforanadaptiveform}

初期状態の [!DNL Adobe Sign] は、アダプティブフォームに対して有効になっていません。Adobe Sign を有効にするには、以下の手順を実行します。

1. コンテンツブラウザーで「**[!UICONTROL フォームコンテナ]**」をタップし、**[!UICONTROL 設定]**&#x200B;アイコン（![設定](assets/configure.png)）をタップします。この操作により、アダプティブフォームのコンテナプロパティを表示するプロパティブラウザーが開きます。
1. このプロパティブラウザーで「**[!UICONTROL 電子サイン]**」アコーディオンを展開し、「**[!UICONTROL Adobe Sign を有効にする]**」オプションを選択します。この操作により、アダプティブフォームに対して [!DNL Adobe Sign] が有効になります。

### [!DNL Adobe Sign] Cloud Service と署名順序を選択する {#selectadobesigncloudserviceforanadaptiveform}

AEM [!DNL Forms] の 1 つのインスタンスに対して、複数の [!DNL Adobe Sign] サービスを設定できます。人事や財務などの部門ごとに個別のサービスセットを設定することをお勧めします。それにより、署名済みドキュメントのトラッキングとレポート処理が容易になります。例えば、銀行には複数の部署があります。これらの部署ごとに個別の設定を指定することで、ドキュメントを正しくトラッキングできるようになります。

また、1 つのドキュメントに対して複数の署名者を設定できます。例えば、複数のユーザーがクレジットカードを申し込む場合があります。銀行は、これらの申し込みの処理を開始する前に、すべての申請者の署名を取得する必要があります。このように複数の署名者を処理するシナリオの場合、各ドキュメントを順に署名することも、順不同で同時に署名することもできます。

クラウドサービスと署名順を選択するには、以下の手順を実行します。

![クラウドサービス](assets/cloud-service.png)

1. コンテンツブラウザーで「**[!UICONTROL フォームコンテナ]**」をタップし、**[!UICONTROL 設定]**&#x200B;アイコン（![設定](assets/configure.png)）をタップします。この操作により、アダプティブフォームのコンテナプロパティを表示するプロパティブラウザーが開きます。
1. このプロパティブラウザーで「**[!UICONTROL 電子サイン]**」アコーディオンを展開し、「**[!UICONTROL Adobe Sign を有効にする]**」オプションを選択します。この操作により、アダプティブフォームに対して [!DNL Adobe Sign] が有効になります。
1. 既に設定されている [!DNL Adobe Sign] Cloud Services のリストから、任意のクラウドサービスを選択します。

   **[!UICONTROL Adobe Sign Cloud Service]** のリストに何も表示されていない場合は、[AEM Forms を使用して Adobe Sign を設定する](../../forms/using/adobe-sign-integration-adaptive-forms.md)の記事に従い、サービスを設定してください。

   ドロップダウンリストには、ツール／**[!UICONTROL Cloud Services]**／**[!UICONTROL Adobe Sign]** の `global` フォルダーに存在するクラウドサービスが表示されます。また、このドロップダウンには、アダプティブフォームの作成時に「**[!UICONTROL 設定コンテナ]**」フィールドで選択したフォルダーに存在するクラウドサービスも表示されます。

1. 「**[!UICONTROL 署名者は署名できます]**」ダイアログボックスで、署名順序を選択します。[!DNL Adobe Sign] の署名者は、アダプティブフォームを&#x200B;**[!UICONTROL 連続]**&#x200B;して（署名者順に）署名することも、**[!UICONTROL 「同時」]**&#x200B;に（順不同で）署名することもできます。

   順に署名する場合は、1 人の署名者が、署名用のフォームを一度に 1 つずつ受け取ります。最初の署名者によるフォームの署名が完了すると、フォームが次の署名者に送信され、最後の署名者になるまでこの手順が繰り返されます。

   同時に署名する場合は、複数の署名者がフォームを同時に署名することができます。

1. [アダプティブフォームに署名者を追加](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform)し、「完了」アイコン（![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)）をタップして変更内容を保存します。


### アダプティブフォームに署名者を追加する {#addsignerstoanadaptiveform}

1 つのアダプティブフォームに対して、署名者を 1 人だけ設定することも、複数の署名者を設定することもできます。署名者を追加する際に、その署名者の詳細な認証情報を設定することもできます。また、フォームの入力者と署名者を同じユーザーにするかどうかを選択することもできます。署名者に関する各種の詳細情報の追加と指定を行うには、以下の手順を実行します。

1. コンテンツブラウザーで「**[!UICONTROL フォームコンテナ]**」をタップし、**[!UICONTROL 設定]** ![設定](assets/configure.png) アイコンをタップします。この操作により、アダプティブフォームのコンテナプロパティを表示するプロパティブラウザーが開きます。
1. このプロパティブラウザーで「**[!UICONTROL 電子サイン]**」アコーディオンを展開し、「**[!UICONTROL Adobe Sign を有効にする]**」オプションを選択します。この操作により、アダプティブフォームに対して [!DNL Adobe Sign] が有効になります。
1. 「**[!UICONTROL 署名者設定]**」で「**[!UICONTROL 署名者を追加]**」をタップします。アダプティブフォームに署名者が追加されます。1 つのアダプティブフォームに対して複数の [!DNL Adobe Sign] 署名者を追加できます。
   ![phone-details](assets/phone-details.png)

1. 「**編集** ![aem_6_3_edit](assets/aem_6_3_edit.png)」アイコンをクリックして、署名者に関する以下の情報を指定します。

   * **[!UICONTROL タイトル]：**&#x200B;署名者を一意に識別するためのタイトルを指定します。

   * **[!UICONTROL 署名者とフォーム記入者は同一ですか？]：**&#x200B;最初に署名する人とフォームを記入する人が同じである場合は「**はい**」を選択します。このオプションを「**いいえ**」に設定した場合は、アダプティブフォームの署名ステップコンポーネントは使用しないでください。フォームに署名ステップコンポーネントが含まれている場合は、このフィールドの値が自動的に「はい」に設定されます。

   * **[!UICONTROL 署名者の電子メールアドレス]：**&#x200B;署名者の電子メールアドレスを指定します。署名者は、ここで指定した電子メールアドレスで、署名する必要があるドキュメントやフォームを受信します。フォームフィールドで指定した電子メールアドレスを使用することも、ログインユーザーの AEM ユーザープロファイルで指定した電子メールアドレスを使用することも、電子メールアドレスを手動で入力することもできます。このステップは、必ず実行する必要があります。最初の署名者または唯一の署名者（署名者が 1 人の場合）のメールアドレスが、AEM Cloud Service の設定に使用された [!DNL Adobe Sign] アカウントと一致していないことを確認します。

   * **[!UICONTROL 署名者の認証方法]：**&#x200B;署名するフォームを開く前にユーザーを認証する方法を指定します。電話による認証、ナレッジベースによる認証、ソーシャル ID に基づく認証のいずれかを選択することができます。

   >[!NOTE]
   >
   >    * ソーシャル ID に基づく認証の場合、Facebook、Google、LinkedIn を使用した認証オプションがデフォルトで用意されています。これ以外のソーシャル認証プロバイダーを使用する場合は、[!DNL Adobe Sign] サポートまでお問い合わせください。


   * **[!DNL Adobe Sign]のフィールドに入力または署名：**&#x200B;署名者用の [!DNL Adobe Sign] フィールドを選択します。1 つのアダプティブフォームで複数の [!DNL Adobe Sign] フィールドを使用できます。署名者用に特定のフィールドを有効にできます。これらのフィールドには、使用可能なすべての [!DNL Adobe Sign] ブロックが表示されます。いずれかのブロックを選択すると、そのブロックのすべてのフィールドが選択されます。フィールドの選択を解除するには、「X」アイコンを使用します。

   ![signer-details](assets/signer-details.png)

   上の画像には、Personal-Information と Office-details という 2 つのサンプルの [!DNL Adobe Sign] ブロックが表示されています。

   「完了 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)」アイコンをタップします。署名者が追加され、設定が完了します。

### アダプティブフォームに対して送信アクションを選択する {#selectsubmitactionforanadaptiveform}

[!DNL Adobe Sign] フィールドをアダプティブフォームに追加したら、フォームコンテナで [!DNL Adobe Sign] を有効にし、[!DNL Adobe Sign] Cloud Service を選択して、[!DNL Adobe Sign] の署名者を追加します。その後、アダプティブフォームに対して、適切な送信アクションを選択します。アダプティブフォームの送信アクションについて詳しくは、[送信アクションの設定](../../forms/using/configuring-submit-actions.md)を参照してください。

また、[!DNL Adobe Sign] が有効になっているアダプティブフォームは、すべての署名者がフォームに署名するまで送信されないことに注意してください。一部の署名者しか署名していないフォームは、フォームポータルの「保留中の署名」セクションで表示されます。[!DNL Adobe Sign] 設定サービスは、[一定の間隔](../../forms/using/adobe-sign-integration-adaptive-forms.md)で [!DNL Adobe Sign] サーバーをポーリングすることにより、署名のステータスを確認します。すべての署名者がフォームの署名を完了すると、送信アクションサービスが起動してフォームが送信されます。[!DNL Adobe Sign] を使用するフォームでカスタムの送信アクションを実行する場合は、送信アクションサービスを使用するために、カスタム送信アクションを更新する必要があります。

<!-- Remove when forms portal goes live
>[!NOTE]
>
>Data of the adaptive form is stored temporarily on Forms Portal. It is recommended to use [custom storage for Forms Portal](/help/forms/using/configuring-draft-submission-storage.md). It ensures that the PII (personally identifiable information) data is not stored on AEM servers. 
-->

これで、フォームに署名するための準備が整いました。フォームのプレビューを表示して、署名の方法を確認することができます。署名者が電子メールで署名用のフォームを受信すると、公開済みフォーム上に [!DNL Adobe Sign] ブロックのフィールドが表示されます。この動作を、フォーム外署名機能といいます。最初の署名者に対して、フォーム内署名機能を設定することもできます。詳しい手順については、「[フォーム内署名機能の設定](../../forms/using/working-with-adobe-sign.md#create-in-form-signing-experience)」を参照してください。

## アダプティブフォームのクラウド署名の設定 {#configure-cloud-signatures-for-an-adaptive-form}

クラウドベースのデジタル署名（リモート署名）は、デスクトップ、モバイル、web 上で機能する新世代のデジタル署名で、署名者の認証に関する最高レベルのコンプライアンスと保証を満たします。クラウドベースのデジタル署名を使用してアダプティブフォームに署名できます。

[Adobe Sign 用にアダプティブフォームプロパティを編集](../../forms/using/working-with-adobe-sign.md#enableadobesign)した後、次の手順を実行してアダプティブフォームにクラウド署名フィールドを追加します。

1. **[!UICONTROL Adobe Sign ブロック]**&#x200B;コンポーネントを、コンポーネントブラウザーからアダプティブフォームにドラッグアンドドロップします。[!UICONTROL Adobe Sign ブロック]コンポーネントには、サポート対象のすべての [!DNL Adobe Sign] フィールドが含まれています。デフォルトでは、**[!UICONTROL 署名]**&#x200B;フィールドがアダプティブフォームに追加されます。

   ![Sign ブロック](assets/sign-block-new.png)

1. **[!UICONTROL Adobe Sign ブロック]**&#x200B;コンポーネントを選択し、「**編集** ![aem_6_3_edit](assets/aem_6_3_edit.png)」アイコンをタップします。フィールドを追加するためのオプションと、フィールドの外観を設定するためのオプションが表示されます。

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **A.** [!DNL Adobe Sign] フィールドを選択して追加。**B.** [!DNL Adobe Sign] ブロックを展開して全画面表示。

1. 「**[!UICONTROL Adobe Sign フィールド]** ![aem_6_3_adobesign](assets/aem_6_3_adobesign.png)」アイコンをタップします。 [!DNL Adobe Sign] フィールドの選択オプションと追加オプションが表示されます。

   「**[!UICONTROL タイプ]**」ドロップダウンフィールドを展開して「**[!UICONTROL 電子署名]**」を選択し、**完了**&#x200B;アイコンをタップして、選択したフィールドを [!DNL Adobe Sign] ブロックに追加します。

   ![電子署名](assets/digital_signatures_new.png)

   フィールドには、必ず一意の名前を指定する必要があります。

   次を使用して、アダプティブフォームにデジタル署名を適用します。

   * クラウド署名：トラストサービスプロバイダーがホストする[デジタル ID](https://helpx.adobe.com/jp/sign/kb/digital-certificate-providers.html) を使用して署名します。
   * Adobe Acrobat または Reader：ドキュメントをダウンロードして Adobe Acrobat または Reader で開き、スマートカード、USB トークン、ファイルベースのデジタル ID を使用して署名します。

   クラウド署名フィールドをアダプティブフォームに追加した後、次の手順を実行して設定プロセスを完了します。

   * [アダプティブフォームに対して Adobe Sign を有効にする](../../forms/using/working-with-adobe-sign.md#enableadobsignforanadaptiveform)
   * [アダプティブフォームに対して Adobe Sign クラウドサービスを選択する](../../forms/using/working-with-adobe-sign.md#selectadobesigncloudserviceforanadaptiveform)
   * [アダプティブフォームに Adobe Sign の署名者を追加する](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform)
   * [アダプティブフォームに対して送信アクションを選択する](../../forms/using/working-with-adobe-sign.md#selectsubmitactionforanadaptiveform)


## フォーム内署名機能の設定 {#create-in-form-signing-experience}

フォームの入力時に、アダプティブフォームに署名することもできます。この動作を、フォーム内署名機能といいます。フォーム内署名機能は、複数の署名者が存在する場合に、最初の署名者のみ使用することができます。アダプティブフォームに対してフォーム内署名機能を設定するには、以下の手順を実行します。

1. [署名ステップコンポーネントの追加と設定](../../forms/using/working-with-adobe-sign.md#add-and-configure-the-signature-step-component)を行います。
1. [概要ステップコンポーネントを追加](../../forms/using/working-with-adobe-sign.md#configure-the-thank-you-page-or-summary-step-component)します。

![フォーム内署名機能](assets/in_form_signing_experience_new.png)

### 署名ステップコンポーネントの追加と設定 {#add-and-configure-the-signature-step-component}

署名ステップコンポーネントを使用して、入力済みのフォームに電子的に署名するための領域を指定します。署名ステップコンポーネントが含まれているセクションをレンダリングすると、入力済みフォームの署名可能な PDF バージョンが表示されます。署名ステップコンポーネントは、フォームの幅いっぱいに表示されます。そのため、署名ステップコンポーネントが含まれているセクションに他のコンポーネントを配置しないようにすることをお勧めします。

署名ステップコンポーネントを設定するには、以下の手順を実行します。

1. **[!UICONTROL 署名ステップ]**&#x200B;コンポーネントを、コンポーネントブラウザーからフォームにドラッグアンドドロップします。
1. 新しく追加された署名ステップコンポーネントを選択し、「**設定** ![configure](assets/configure.png)」アイコンをタップします。この操作により、署名ステップのプロパティを表示するプロパティブラウザーが開きます。以下のプロパティを設定します。

   * **[!UICONTROL 名前]**：コンポーネントの名前を指定します。

   * **[!UICONTROL タイトル]：**&#x200B;コンポーネントの一意のタイトルを指定します。
   * **[!UICONTROL テンプレートメッセージ]：**&#x200B;署名 PDF の読み込み中に表示するメッセージを指定します。[!DNL Adobe Sign] サービスによる署名 PDF の準備と読み込みには、ある程度の時間がかかります。
   * **[!UICONTROL 署名サービス]：**「**[!DNL Adobe Sign]**」オプションを選択します。

   * **[!UICONTROL レガシーの E-sign コンポーネントを使用]**：[AEM Forms Workspace](../../forms/using/introduction-html-workspace.md)、AEM [!DNL Forms] アプリケーションでそれぞれのアダプティブフォームを使用している場合、またはベースとなるアダプティブフォームにレガシーの E-Sign コンポーネントが含まれている場合は、「**レガシーの E-Sign コンポーネントを使用**」オプションを選択します。

   * **[!UICONTROL 設定]**：設定を選択します（[!DNL Adobe Sign] クラウドサービス）。このドロップダウンボックスを使用できるのは、「**レガシーの E-Sign コンポーネントを使用**」オプションが有効になっている場合だけです。

   * **[!UICONTROL CSS クラス]**：コンポーネントの CSS クラスを指定します。

   完了（![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)）アイコンをタップして、変更を保存します。

   ![署名ステップ](assets/signature_step_new.png)

   >[!NOTE]
   >
   > * **[!UICONTROL 署名者ステップ]**&#x200B;コンポーネントをフォームにドラッグアンドドロップすると、「**[!UICONTROL 署名者とフォーム記入者は同一ですか？]**」オプションが自動的に「**はい**」に設定されます。フォームを正しく機能させるには、このオプションが設定されている必要があります。
   >
   > * 最適なエクスペリエンスを得るには、署名ステップコンポーネントの後に概要ステップコンポーネントを使用します。 署名ステップコンポーネントでフォームに署名する際に入力が完了すると、概要ステップが自動的に送信され、すぐにフォームが送信されます。 概要ステップを使用しない場合、自動送信は、[Adobe Sign Configuration Service](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-scheduler-to-sync-the-signing-status) を使用して設定された間隔の後にのみトリガーされます。
   > 以下に、いくつかのベストプラクティスを示します。
   > * 署名ステップを含むアダプティブフォームパネルは、常にアダプティブフォームの最後または 2 番目の最後のパネルに表示されます。 2 番目の最後のパネルは、最後のパネルに概要ステップが含まれている場合にのみ使用できます。
   > * 署名または概要ステップコンポーネントを含むパネルに他のコンポーネントを含めることはできません。
   > * 署名ステップを含むアダプティブフォームには送信ボタンを含めることはできません。
   > * 署名を含むアダプティブフォームの送信手順は、バックグラウンドサービスまたは概要ステップで処理されます。 フォームにも入力する設定済みの署名者が 1 人いる場合は、概要ステップを使用してアダプティブフォームの送信を処理する利点は、署名者がフォームに署名したかどうかを即座に評価し、送信アクションを呼び出すことです。 バックグラウンドサービスを使用すると、設定済みのすべての署名者がフォームに署名しているかどうかを評価し、アダプティブフォームの送信を遅らせる場合の時間が長くなります。
   > * 署名または概要ステップを含むパネルからユーザーが戻れないようにフォームをデザインします。



### 「ありがとうございます」ページまたは概要ステップコンポーネントの設定  {#configure-the-thank-you-page-or-summary-step-component}

**概要ステップ**&#x200B;コンポーネントにより、フォームが自動的に送信され、カスタマイズ後の概要ページに情報が取り込まれ、送信されたフォームの概要情報が表示されます。また、リターンマップ内の必須情報も取得されます。概要ステップコンポーネントは、フォームの幅いっぱいに表示されます。そのため、概要ステップコンポーネントが含まれているセクションに他のコンポーネントを配置しないようにすることをお勧めします。

これで、フォーム内署名機能を使用するための準備が整いました。フォームのプレビューを表示して、署名の方法を確認することができます。

## よくある質問  {#frequently-asked-questions}

**Q**：特定のアダプティブフォームを別のアダプティブフォームに埋め込むことができますが、埋め込まれたアダプティブフォームで [!DNL Adobe Sign] を有効にできますか？
**A**：いいえ。AEM [!DNL Forms] では、[!DNL Adobe Sign] が有効になっているアダプティブフォームが埋め込まれているアダプティブフォームを使用して署名することはできません。

**Q**：拡張テンプレートを使用してアダプティブフォームを作成し、そのフォームを編集用として開くと、「電子署名サインまたは署名者が正しく設定されていません」というエラーメッセージが表示されます。表示されます。このエラーメッセージを解決するにはどうすればよいですか？**A**：拡張テンプレートを使用して作成されたアダプティブフォームは、[!DNL Adobe Sign] を使用するように設定されています。このエラーを修正するには、[!DNL Adobe Sign] のクラウド設定を作成して選択し、アダプティブフォーム用の [!DNL Adobe Sign] 署名者を設定してください。

**Q**：アダプティブフォームの静的テキストコンポーネントで [!DNL Adobe Sign] のテキストタグを使用することはできますか？**A**：はい。テキストコンポーネントでテキストタグを使用して、[!DNL Adobe Sign] のフィールドを[レコードのドキュメント](../../forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)（「自動生成されたレコードのドキュメント」オプション）が有効になっているアダプティブフォームに追加することができます。テキストタグを作成する手順とルールについては、[Adobe Sign のドキュメント](https://helpx.adobe.com/jp/sign/using/text-tag.html)を参照してください。アダプティブフォームでは、テキストタグを使用する場合に制限があることにも注意してください。テキストタグを使用して作成できるのは、[Adobe Sign ブロック](../../forms/using/working-with-adobe-sign.md#configure-cloud-signatures-for-an-adaptive-form)がサポートされているフィールドだけです。

**Q：** AEM [!DNL Forms] には、[!UICONTROL Adobe Sign ブロック]と署名ステップコンポーネントの両方が用意されていますが、アダプティブフォームで両方を同時に使用することはできますか？
**A：**&#x200B;はい。フォーム内で両方のコンポーネントを同時に使用することができます。これらのコンポーネントを使用する場合は、以下の推奨事項を参照してください。

**Adobe Sign ブロック：** [!UICONTROL Adobe Sign ブロック]を使用すると、アダプティブフォームの任意の場所に [!UICONTROL Adobe Sign] フィールドを追加することができます。また、特定のフィールドを署名者に割り当てることもできます。アダプティブフォームのプレビュー時と公開時には、[!UICONTROL Adobe Sign] ブロックがデフォルトで非表示になります。これらのブロックは、署名ドキュメント内でのみ使用することができます。署名ドキュメント内では、署名者に割り当てられているフィールド以外は使用できません。[!UICONTROL Adobe Sign] ブロックは、最初の署名者だけでなく、後続の署名者も使用することができます。

**署名ステップコンポーネント：**&#x200B;署名ステップコンポーネントを使用すると、フォーム内署名機能を設定することができます。この機能では、最初の署名者のみ、フォームの入力時に署名を行うことができます。署名ステップコンポーネントが含まれているセクションをレンダリングすると、フォームの署名可能な PDF バージョンが表示されます。これは通常、最後のセクションか、最後から 2 番目のセクションになります。このセクションの後に、フォームの概要コンポーネントが表示されます。

## トラブルシューティング {#troubleshoot}

### [!DNL Adobe Sign] 契約エラー {#adobe-sign-agreement-failures}

**問題**
[!DNL Adobe Sign] サービスがアダプティブフォーム用に設定されている場合、サービスは基になるアダプティブフォーム用の [!DNL Adobe Sign] 契約を作成できません。

**解決方法**

* アダプティブフォームで使用されている [Adobe Sign Cloud Service の設定](../../forms/using/adobe-sign-integration-adaptive-forms.md)を確認します。
* [!DNL Adobe Sign]Cloud Service の設定に使用する[!DNL Adobe Sign]サーバー上の API アプリケーションに、必要な権限があることを確認します。
* 複数の[!DNL Adobe Sign]Cloud Services を使用している場合は、すべてのサービスの&#x200B;**[!UICONTROL OAuth URL]**&#x200B;を同じ&#x200B;**[!UICONTROL Adobe Sign シャード]**&#x200B;に指定します。

* [!DNL Adobe Sign]アカウントと、最初の署名者と単一の署名者を設定するには、別々のメールアドレスを使用します。最初の署名者または唯一の署名者（署名者が 1 人の場合）のメールアドレスを、AEM Cloud Services の設定に使用された [!DNL Adobe Sign] アカウントと同一にすることはできません。

### [!DNL Adobe Sign] により有効化されたアダプティブフォーム用の AEM [!DNL Forms] ワークフローが開始しない {#adobe-sign-aem-form-workflow-failures}

**問題**
[!DNL Adobe Sign] がアダプティブフォーム用に設定されている場合、[!DNL Forms]呼び出しワークフローオプションを使用して設定されたワークフローは開始しません。

**解決方法**

* 署名ステップなしで [!DNL Adobe Sign] を使用する場合、またはフォームに複数の人の署名が必要な場合、AEM [!DNL Forms] サーバーは、スケジューラーがすべての人がフォームに署名したことを確認するのを待ちます。スケジューラーは、すべてのユーザーが署名を完了した後にのみアダプティブフォームを送信し、ワークフローは、アダプティブフォームの送信が成功した後にのみ開始します。 [スケジューラー](adobe-sign-integration-adaptive-forms.md)がフォームの署名状況を確認する間隔を短くして、フォームの送信を高速化できます。


## 関連記事 {#related-articles}

* [Adobe Sign の AEM Forms への統合](../../forms/using/adobe-sign-integration-adaptive-forms.md)
* [アダプティブフォームでの Adobe Sign 使用に関するベストプラクティス](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684)
* [AEM フォームで Adobe Sign を使用（ビデオ）](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/forms-and-sign/introduction.html?lang=ja)
