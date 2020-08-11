---
title: アダプティブフォームで Adobe Sign を使用する
seo-title: アダプティブフォームで Adobe Sign を使用する
description: アダプティブフォームで電子署名（Adobe Sign）ワークフローを有効にすると、署名ワークフローが自動化され、単一署名プロセスと複数署名プロセスが簡素化されるほか、モバイルデバイスでフォームを電子的に署名できるようになります。
seo-description: アダプティブフォームで電子署名（Adobe Sign）ワークフローを有効にすると、署名ワークフローが自動化され、単一署名プロセスと複数署名プロセスが簡素化されるほか、モバイルデバイスでフォームを電子的に署名できるようになります。
uuid: cc3012ed-c318-4529-9adc-61aa5b5761a0
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: f79828d8-2230-4477-8ffa-eeb6a0413acd
docset: aem65
translation-type: tm+mt
source-git-commit: e562ffe229543a1ee93467bcbc1a7be6c12927c6
workflow-type: tm+mt
source-wordcount: '3643'
ht-degree: 60%

---


# アダプティブフォームで Adobe Sign を使用する{#using-adobe-sign-in-an-adaptive-form}

Adobe Sign を使用して、アダプティブフォームの電子署名ワークフローを実行することができます。電子署名により、法務、販売、給与、人事管理などに関するドキュメントを処理するためのワークフローが改善されます。

Adobe Sign とアダプティブフォームの一般的なシナリオでは、サービスを申し込むためのアダプティブフォームをユーザーが入力します。例えば、住宅ローンアプリケーションやクレジットカードアプリケーションを使用する場合、すべての借り手とその申し込み者から、正しい署名を取得する必要があります。これに類似したシナリオで電子署名ワークフローを有効にするには、Adobe Sign を AEM Forms に統合します。例えば、Adobe Sign を使用して、以下のような処理を実行することができます。

* 完全に自動化された提案プロセス、見積りプロセス、契約プロセスを使用して、任意のデバイスで契約を締結する。
* 人事プロセスを短時間で完了し、従業員に対してデジタルエクスペリエンスを提供する。
* 契約のサイクルタイムを短縮し、ベンダーとの取引を早期に開始する。
* 共通するプロセスを自動化するためのデジタルワークフローを作成する。

Adobe Sign と AEM Forms を統合することにより、次の機能がサポートされます。

* 単一ユーザーと複数ユーザーの署名ワークフローを処理する機能
* 順次署名と同時署名のワークフロー
* フォーム内とフォーム外での署名機能
* 匿名ユーザーまたはログインユーザーとしてフォームを署名する機能
* 動的な署名プロセスを処理する機能（AEM Forms のワークフローと統合）
* ナレッジベース、電話、ソーシャルプロファイルによる認証機能

## 前提条件 {#prerequisites}

アダプティブフォームで Adobe Sign を使用する前に、以下の点を確認してください。

* Adobe Sign を使用するように AEM Forms クラウドサービスが設定されていることを確認してください。詳細については、「[Adobe Sign を AEM Forms に統合する](../../forms/using/adobe-sign-integration-adaptive-forms.md)」を参照してください。
* 署名者のリストを準備してください。少なくとも、各署名者の電子メールアドレスが必要になります。

## アダプティブフォーム用に Adobe Sign を設定する {#configure-adobe-sign-for-an-adaptive-form}

アダプティブフォーム用に Adobe Sign を設定するには、以下の手順を実行します。

1. [Adobe署名用のアダプティブフォームプロパティの編集](../../forms/using/working-with-adobe-sign.md#enableadobesign)
1. [Adobe Sign のフィールドをアダプティブフォームに追加する](../../forms/using/working-with-adobe-sign.md#addadobesignfieldstoanadaptiveform)
1. [アダプティブフォームに対して Adobe Sign を有効にする](../../forms/using/working-with-adobe-sign.md#enableadobsignforanadaptiveform)
1. [アダプティブフォームに対して Adobe Sign クラウドサービスを選択する](../../forms/using/working-with-adobe-sign.md#selectadobesigncloudserviceforanadaptiveform)

1. [アダプティブフォームに Adobe Sign の署名者を追加する](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform)
1. [アダプティブフォームに対して送信アクションを選択する](../../forms/using/working-with-adobe-sign.md#selectsubmitactionforanadaptiveform)

![署名者の詳細](assets/signer_details_new.png)

### Adobe Signのアダプティブフォームプロパティの編集 {#enableadobesign}

既存または新規のアダプティブフォームに対して、Adobe Signのアダプティブフォームプロパティを設定します。

[「Adobe Sign向けアダプティブフォームの作成](../../forms/using/working-with-adobe-sign.md#create-an-adaptive-form-for-adobe-sign) 」では、基本的なアダプティブフォームの作成手順を説明しています。 「アダプティブフォームの [作成中に使用できるその他のオプションについては](../../forms/using/creating-adaptive-form.md) 、アダプティブフォームの作成」を参照してください。

#### Adobe Sign用アダプティブフォームの作成 {#create-an-adaptive-form-for-adobe-sign}

署名が有効なアダプティブフォームを作成するには、次の手順を実行します。

1. **[!UICONTROL Adobe Experience Manager]** / **[!UICONTROL Forms]** / **[!UICONTROL Forms&amp;ドキュメントに移動します]**。
1. 「**[!UICONTROL 作成]**」をタップして、「**[!UICONTROL アダプティブフォーム]**」を選択します。テンプレートのリストが表示されます。 Select the template and tap **[!UICONTROL Next]**.
1. In the **[!UICONTROL Basic]** tab:

   1. アダプティブフォームの **名前** と **タイトルを指定します** 。

   1. Adobe SignとAEM Formsの設定時に作成した [設定コンテナ](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) を選択します。

1. 「 **[!UICONTROL フォームモデル]** 」タブで、次のいずれかのオプションを選択します。

   * 「 **[!UICONTROL フォームテンプレートをレコードのドキュメントとして]** 関連付ける」オプションを選択し、「レコードのテンプレート」のドキュメントを選択します。 フォームテンプレートベースのアダプティブフォームを使用する場合、署名用に送信されたドキュメントには、関連付けられたフォームテンプレートに基づくフィールドのみが表示されます。 アダプティブフォームのすべてのフィールドを表示するわけではありません。

   * 「レコードの **[!UICONTROL ドキュメントを]** 生成」オプションを選択します。 「レコードのドキュメント」オプションを有効にしているアダプティブフォームを使用する場合、署名用に送信されたドキュメントには、アダプティブフォームのすべてのフィールドが表示されます。

1. 「**[!UICONTROL 作成」をタップします。]** 署名が有効なアダプティブフォームが作成され、Adobe Signフィールドを追加する際に使用できます。

#### Adobe Signのアダプティブフォームの編集 {#editafsign}

既存のアダプティブフォームでAdobe Signを使用するには、次の手順を実行します。

1. **[!UICONTROL Adobe Experience Manager]** / **[!UICONTROL Forms]** / **[!UICONTROL Forms&amp;ドキュメントに移動します]**。
1. Select the adaptive form and tap **[!UICONTROL Properties]**.
1. 「 **[!UICONTROL 基本]** 」タブで、Adobe SignとAEM Formsの設定時に作成した [設定コンテナ](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) を選択します。
1. 「 **[!UICONTROL フォームモード]** 」タブで、次のいずれかのオプションを選択します。

   * 「 **[!UICONTROL フォームテンプレートをレコードのドキュメントとして]** 関連付ける」オプションを選択し、「レコードのテンプレート」のドキュメントを選択します。 フォームテンプレートベースのアダプティブフォームを使用する場合、署名用に送信されたドキュメントには、関連付けられたフォームテンプレートに基づくフィールドのみが表示されます。 アダプティブフォームのすべてのフィールドを表示するわけではありません。

   * 「レコードの **[!UICONTROL ドキュメントを]** 生成」オプションを選択します。 「レコードのドキュメント」オプションを有効にしているアダプティブフォームを使用する場合、署名用に送信されたドキュメントには、アダプティブフォームのすべてのフィールドが表示されます。

1. 「**[!UICONTROL 保存して閉じる]**」をタップします。アダプティブフォームはAdobe Signで有効になっています。

### Adobe Sign のフィールドをアダプティブフォームに追加する {#addadobesignfieldstoanadaptiveform}

Adobe Sign には、アダプティブフォーム上に配置できるさまざまなフィールドが用意されています。これらのフィールドには、署名、イニシャル、会社名、タイトルなど、さまざまなタイプのデータを入力することができます。このため、署名が行われる際に署名だけでなく追加情報を収集できます。Adobe Sign ブロックコンポーネントを使用して、アダプティブフォームのさまざまな場所に Adobe Sign のフィールドを配置することができます。

アダプティブフォームにフィールドを追加し、それらのフィールドに関する各種のオプションをカスタマイズするには、以下の手順を実行します。

1. **Adobe Sign ブロック**&#x200B;コンポーネントを、コンポーネントブラウザーからアダプティブフォームにドラッグアンドドロップします。Adobe Sign ブロックコンポーネントには、サポート対象のすべての Adobe Sign フィールドが含まれています。By default, it adds a **Signature** field to the adaptive form.

   ![署名ブロック](assets/sign_block_new.png)

   デフォルトでは、発行済みアダプティブフォームに Adobe Sign ブロックは表示されません。Adobe Sign ブロックが表示されるのは、署名ドキュメントだけです。Adobe Sign ブロックの表示設定は、Adobe Sign ブロックコンポーネントのプロパティで変更することができます。

   >[!NOTE]
   >
   >    * アダプティブフォームで Adobe Sign を使用する場合、Adobe Sign ブロックの使用は必須ではありません。署名者にAdobe Signブロックを使用してフィールドを追加しない場合は、デフォルトの署名フィールドが署名ドキュメントの下部に表示されます。
   >    * レコードのドキュメントが自動的に生成されるアダプティブフォームの場合のみ、Adobe Sign ブロックを使用してください。カスタムの XDP を使用して、レコードのドキュメントやフォームテンプレートベースのアダプティブフォームを生成する場合は、Adobe Sign ブロックを使用する必要はありません。


1. Select the **Adobe Sign Block** component and tap the **Edit** ![aem_6_3_edit](assets/aem_6_3_edit.png) icon. フィールドを追加したり、フィールドの表示形式を設定したりするためのオプションが表示されます。

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **A.** [Adobe Sign]フィールドを選択して追加します。 **B.** [Adobe Sign]ブロックをフルスクリーン表示に展開する

1. 「 **Adobe Signフィールド** aem_6_3_adobesign ![](assets/aem_6_3_adobesign.png) 」アイコンをタップします。 Adobe Sign のフィールドの選択オプションと追加オプションが表示されます。

   Expand the **Type** drop-down field to select a Adobe Sign field and tap the Done ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) icon to add the selected field to Adobe Sign block. 「**タイプ**」ドロップダウンフィールドには、「署名」タイプ、「署名者の情報」タイプ、「データフィールド」タイプが表示されます。Adobe Sign が AEM Forms に統合されている場合、「タイプ」ドロップダウンボックスに表示されているフィールド以外のフィールドは使用できません。Adobe Sign フィールドについて詳しくは、[Adobe Sign のドキュメント](https://helpx.adobe.com/sign/help/field-types.html)を参照してください。

   ![adobe-sign-block-fields-options](assets/adobe-sign-block-fields-options.png)

   フィールドには一意の名前を付ける必要があります。 フィールドを必須フィールドとしてマークするための必須オプションを選択することもできます。Adobe Sign の一部のフィールドには、「**名前**」オプションと「**必須**」オプションのほかに、追加のオプションが用意されています。例えば、マスクオプや複数行のオプションなどです。また、フィールドが Adobe Sign の同じブロック内に存在するか別のブロック内に存在するかを問わず、Adobe Sign の各フィールドに一意の名前を指定できます。

   ドロップダウンリストから「 **デジタル署名** 」を選択すると、アダプティブフォームに電子署名を適用できます。

   * クラウド署名を使用して、信頼サービスプロバイダーが [](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) ホストするデジタルIDで署名するオンライン。
   * スマートカード、USBトークン、またはファイルベースのデジタルIDを使用して、Adobe AcrobatまたはReaderと共にドキュメントをローカルにダウンロードする。

### アダプティブフォームに対して Adobe Sign を有効にする {#enableadobsignforanadaptiveform}

初期状態の Adobe Sign は、アダプティブフォームに対して有効になっていません。Adobe Sign を有効にするには、以下の手順を実行します。

1. In the Content browser, tap **Form Container**, and tap the **Configure** ![configure](assets/configure.png) icon. この操作により、アダプティブフォームのコンテナプロパティを表示するプロパティブラウザーが開きます。
1. このプロパティブラウザーで「**電子署名**」アコーディオンを展開し、「**Adobe Sign を有効にする**」オプションを選択します。この操作により、アダプティブフォームに対して Adobe Sign が有効になります。

### Adobe Sign クラウドサービスと署名順序を選択する {#selectadobesigncloudserviceforanadaptiveform}

AEM Forms の 1 つのインスタンスに対して、複数の Adobe Sign サービスを設定することができます。人事や財務などの部門ごとに個別のサービスセットを設定することをお勧めします。こうすることにより、署名済みドキュメントの追跡とレポート処理が容易になります。例えば、銀行には複数の部署があります。これらの部署ごとに個別の設定を指定することにより、ドキュメントを正しく追跡できるようになります。

また、1 つのドキュメントに対して複数の署名者を設定することができます。例えば、複数のユーザーがクレジットカードを申し込む場合があります。銀行は、これらの申し込みの処理を開始する前に、すべての申し込み者の署名を取得する必要があります。このように複数の署名者を処理するシナリオの場合、各ドキュメントを順に署名することも、順不同で同時に署名することもできます。

クラウドサービスと署名順を選択するには、以下の手順を実行します。

![クラウドサービス](assets/cloud-service.png)

1. In the Content browser, tap **Form Container**, and tap the **Configure** ![configure](assets/configure.png) icon. この操作により、アダプティブフォームのコンテナプロパティを表示するプロパティブラウザーが開きます。
1. このプロパティブラウザーで「**電子署名**」アコーディオンを展開し、「**Adobe Sign を有効にする**」オプションを選択します。この操作により、アダプティブフォームに対して Adobe Sign が有効になります。
1. 既に設定されている Adobe Sign クラウドサービスのリストで、任意のクラウドサービスを選択します。

   If the **Adobe Sign Cloud Service** list is empty, follow the [Configure Adobe Sign with AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md) artilce to configure the service.

1. 「**署名者は署名できます**」ダイアログボックスで、署名順序を選択します。Adobe Sign の署名者は、アダプティブフォームを&#x200B;**連続**&#x200B;して（署名者順に）署名することも、**「同時」**&#x200B;に（順不同で）署名することもできます。

   順に署名する場合は、1 人の署名者が、署名用のフォームを一度に 1 つずつ受け取ります。最初の署名者によるフォームの署名が完了すると、フォームが次の署名者に送信され、最後の署名者になるまでこの手順が繰り返されます。

   同時に署名する場合は、複数の署名者がフォームを同時に署名することができます。

1. [アダプティブフォームに署名追加し、「](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform)[](assets/aem_6_3_forms_save.png) aem_6_3_forms_saveを完了」アイコンをタップして変更を保存します。


### アダプティブフォームに署名者を追加する {#addsignerstoanadaptiveform}

1 つのアダプティブフォームに対して、署名者を 1 人だけ設定することも、複数の署名者を設定することもできます。署名者を追加する際に、その署名者の詳細な認証情報を設定することもできます。また、フォームの入力者と署名者を同じユーザーにするかどうかを選択することもできます。署名者に関する各種の詳細情報の追加と指定を行うには、以下の手順を実行します。

1. In the Content browser, tap **Form Container**, and tap the **Configure** ![configure](assets/configure.png) icon. この操作により、アダプティブフォームのコンテナプロパティを表示するプロパティブラウザーが開きます。
1. このプロパティブラウザーで「**電子署名**」アコーディオンを展開し、「**Adobe Sign を有効にする**」オプションを選択します。この操作により、アダプティブフォームに対して Adobe Sign が有効になります。
1. Tap **Add Signer** under **Signer Configuration**. これにより、署名者がアダプティブフォームに追加されます。 アダプティブフォームには、複数のAdobe Sign署名者を追加できます。
1. ![電話の詳細](assets/phone-details.png)

   Click the **Edit** ![aem_6_3_edit](assets/aem_6_3_edit.png) icon to specify the following information about the signer:

   * **タイトル：** 署名者を一意に識別するタイトルを指定します。

   * **署名者とフォームの入力者は同じですか。** フォームの入力者と最初の署名者が同じ人物の場合は、 **「はい**」を選択します。 このオプションを「**いいえ**」に設定した場合は、アダプティブフォームの署名ステップコンポーネントは使用しないでください。フォームに署名ステップコンポーネントが含まれている場合は、このフィールドの値が自動的に「はい」に設定されます。

   * **署名者の電子メールアドレス：**&#x200B;署名者の電子メールアドレスを指定します。署名者は、ここで指定した電子メールアドレスで、署名する必要があるドキュメントやフォームを受信します。フォームフィールドで指定した電子メールアドレスを使用することも、ログインユーザーの AEM ユーザープロファイルで指定した電子メールアドレスを使用することも、電子メールアドレスを手動で入力することもできます。このステップは、必ず実行する必要があります。最初の署名者または唯一の署名者の電子メールアドレス（1人の署名者の場合）が、AEMクラウドサービスの設定に使用されたAdobe Signアカウントと一致していないことを確認します。

   * **署名者の認証方法：**&#x200B;署名するフォームを開く前にユーザーを認証する方法を指定します。電話による認証、ナレッジベースによる認証、ソーシャル ID に基づく認証のいずれかを選択することができます。
   >[!NOTE]
   >
   >    * ソーシャル ID に基づく認証の場合、Facebook、Google、LinkedIn を使用した認証オプションがデフォルトで用意されています。これ以外のソーシャル認証プロバイダーを使用する場合は、Adobe Sign サポートまでお問い合わせください。


   * **Adobe Sign のフィールドに入力または署名：**&#x200B;署名者用の Adobe Sign フィールドを選択します。1 つのアダプティブフォームで複数の Adobe Sign フィールドを使用することができます。署名者用に特定のフィールドを有効にすることができます。これらのフィールドには、使用可能なすべての Adobe Sign ブロックが表示されます。いずれかのブロックを選択すると、そのブロックのすべてのフィールドが選択されます。Xアイコンを使用して、フィールドの選択を解除できます。

   ![signer-details](assets/signer-details.png)

   上の画像には、Personal-Information と Office-details という 2 つのサンプルの Adobe Sign ブロックが表示されています。

   「 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 」アイコンをタップします。 署名者が追加され、設定されます。

### アダプティブフォームに対して送信アクションを選択する {#selectsubmitactionforanadaptiveform}

Adobe Sign フィールドをアダプティブフォームに追加したら、フォームコンテナで Adobe Sign を有効にし、Adobe Sign クラウドサービスを選択して、Adobe Sign の署名者を追加します。その後、アダプティブフォームに対して、適切な送信アクションを選択します。アダプティブフォームの送信アクションについて詳しくは、「[送信アクションの設定](../../forms/using/configuring-submit-actions.md)」を参照してください。

また、Adobe Sign が有効になっているアダプティブフォームは、すべての署名者がフォームに署名するまで送信されないことに注意してください。一部の署名者しか署名していないフォームは、フォームポータルの「保留中の署名」セクションで表示することができます。Adobe Sign 設定サービスは、[一定の間隔で](../../forms/using/adobe-sign-integration-adaptive-forms.md) Adobe Sign サーバーをポーリングすることにより、署名のステータスを確認します。すべての署名者がフォームの署名を完了すると、送信アクションサービスが起動してフォームが送信されます。Adobe Sign を使用するフォームでカスタムの送信アクションを実行する場合は、送信アクションサービスを使用するように、そのカスタム送信アクションを設定する必要があります。

<!-- Remove when forms portal goes live
>[!NOTE]
>
>Data of the adaptive form is stored temporarily on Forms Portal. It is recommended to use [custom storage for Forms Portal](/help/forms/using/configuring-draft-submission-storage.md). It ensures that the PII (personally identifiable information) data is not stored on AEM servers. -->

これで、フォームに署名するための準備が整いました。フォームのプレビューを表示して、署名の方法を確認することができます。署名者が電子メールで署名用のフォームを受信すると、発行済みフォーム上に Adobe Sign ブロックのフィールドが表示されます。この動作を、フォーム外署名機能といいます。最初の署名者に対して、フォーム内署名機能を設定することもできます。詳しい手順については、「[フォーム内署名機能の設定](../../forms/using/working-with-adobe-sign.md#create-in-form-signing-experience)」を参照してください。

## アダプティブフォームのクラウド署名の設定 {#configure-cloud-signatures-for-an-adaptive-form}

クラウドベースのデジタル署名またはリモート署名は、デスクトップ、モバイル、Web上で機能する新しい世代のデジタル署名で、署名者の認証に関する最高レベルのコンプライアンスと保証を満たします。 クラウドベースの電子署名を使用してアダプティブフォームに署名することができます。

アダプティブフォームのプロパティをAdobe署名用に [編集した後](../../forms/using/working-with-adobe-sign.md#enableadobesign)、次の手順を実行してアダプティブフォームにクラウド署名フィールドを追加します。

1. **Adobe Sign ブロック**&#x200B;コンポーネントを、コンポーネントブラウザーからアダプティブフォームにドラッグアンドドロップします。Adobe Sign ブロックコンポーネントには、サポート対象のすべての Adobe Sign フィールドが含まれています。By default, it adds a **Signature** field to the adaptive form.

   ![署名ブロック](assets/sign-block-new.png)

1. Select the **Adobe Sign Block** component and tap the **Edit** ![aem_6_3_edit](assets/aem_6_3_edit.png) icon. フィールドを追加したり、フィールドの表示形式を設定したりするためのオプションが表示されます。

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **A.** [Adobe Sign]フィールドを選択して追加します。 **B.** [Adobe Sign]ブロックをフルスクリーン表示に展開する

1. 「 **Adobe Signフィールド** aem_6_3_adobesign ![](assets/aem_6_3_adobesign.png) 」アイコンをタップします。 Adobe Sign のフィールドの選択オプションと追加オプションが表示されます。

   Expand the **Type** drop-down field to select **Digital Signature** and tap the Done icon to add the selected field to Adobe Sign block.

   ![デジタル署名](assets/digital_signatures_new.png)

   フィールドには一意の名前を付ける必要があります。

   次を使用して、アダプティブフォームに電子署名を適用します。

   * Cloud signatures:信頼サービスプロバイダーが [ホストするデジタルIDを使用して署名します](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) 。
   * Adobe AcrobatまたはReader:Adobe AcrobatまたはReaderでドキュメントをダウンロードして開き、スマートカード、USBトークン、またはファイルベースのデジタルIDを使用して署名します。

   クラウド署名フィールドをアダプティブフォームに追加した後、次の手順を実行して設定プロセスを完了します。

   * [アダプティブフォームに対して Adobe Sign を有効にする](../../forms/using/working-with-adobe-sign.md#enableadobsignforanadaptiveform)
   * [アダプティブフォームに対して Adobe Sign クラウドサービスを選択する](../../forms/using/working-with-adobe-sign.md#selectadobesigncloudserviceforanadaptiveform)
   * [アダプティブフォームに Adobe Sign の署名者を追加する](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform)
   * [アダプティブフォームに対して送信アクションを選択する](../../forms/using/working-with-adobe-sign.md#selectsubmitactionforanadaptiveform)


## フォーム内署名機能の設定 {#create-in-form-signing-experience}

フォームの入力時に、アダプティブフォームに署名することもできます。この動作を、フォーム内署名機能といいます。フォーム内署名機能は、複数の署名者が存在する場合に、最初の署名者のみ使用することができます。アダプティブフォームに対してフォーム内署名機能を設定するには、以下の手順を実行します。

1. [署名ステップコンポーネントの追加と設定](../../forms/using/working-with-adobe-sign.md#add-and-configure-the-signature-step-component)を行います。
1. [概要ステップコンポーネントを追加](../../forms/using/working-with-adobe-sign.md#configure-the-thank-you-page-or-summary-step-component)します。

![フォーム内署名エクスペリエンス](assets/in_form_signing_experience_new.png)

### 署名ステップコンポーネントの追加と設定 {#add-and-configure-the-signature-step-component}

署名ステップコンポーネントを使用して、入力済みのフォームに電子的に署名するための領域を指定します。署名ステップコンポーネントが含まれているセクションをレンダリングすると、入力済みフォームの署名可能な PDF バージョンが表示されます。署名ステップコンポーネントは、フォームの幅いっぱいに表示されます。そのため、署名ステップコンポーネントが含まれているセクションに他のコンポーネントを配置しないようにすることをお勧めします。

署名ステップコンポーネントを設定するには、以下の手順を実行します。

1. **署名ステップ**&#x200B;コンポーネントを、コンポーネントブラウザーからフォームにドラッグアンドドロップします。
1. Select the newly added Signature step component and tap the **Configure** ![configure](assets/configure.png) icon. この操作により、署名ステップのプロパティを表示するプロパティブラウザーが開きます。以下のプロパティを設定します。

   * **要素名：**&#x200B;コンポーネントの名前を指定します。

   * **タイトル：**&#x200B;コンポーネントの一意のタイトルを指定します。
   * **テンプレートメッセージ：** 署名 PDF の読み込み中に表示するメッセージを指定します。Adobe Sign サービスによる署名 PDF の準備と読み込みには、ある程度の時間がかかります。
   * **署名サービス：** 「**Adobe Sign**」オプションを選択します。

   * **レガシーの E-Sign コンポーネントを使用**：[AEM Forms Workspace](../../forms/using/introduction-html-workspace.md) または AEM Forms アプリケーションで個別のアダプティブフォームを使用する場合や、ベースとなるアダプティブフォームにレガシーの E-Sign コンポーネントが含まれている場合は、「**レガシーの E-Sign コンポーネントを使用**」オプションを選択します。

   * **設定**：設定を選択します（Adobe Sign クラウドサービス）。The drop-down box is available only if the **Use legacy E-sign component** option is enabled.

   「 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 」アイコンをタップして、変更を保存します。

   ![署名手順](assets/signature_step_new.png)

   >[!NOTE]
   >
   > * **[!UICONTROL 署名者ステップ]**&#x200B;コンポーネントをフォームにドラッグアンドドロップすると、「**[!UICONTROL 署名者とフォーム記入者は同一ですか？]**」オプションが自動的に「**はい**」に設定されます。フォームの動作を維持する必要があります。
      >
      > 
   * 最適なエクスペリエンスを得るには、署名手順コンポーネントの後に概要手順コンポーネントを使用します。 概要手順では、署名手順コンポーネントでフォームの署名を完了した後、自動的に直ちにフォームが送信されます。 要約手順を使用しない場合、 [Adobe Sign設定サービスを使用して設定された間隔の後にのみ、自動送信がトリガーされます](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-scheduler-to-sync-the-signing-status)。
   > * いくつかのベストプラクティスを次に示します。
   > * 署名手順を含むアダプティブフォームパネルは、常にアダプティブフォームの最後または2番目の最後のパネルにあります。 最後のパネルの2番目に最後のパネルになるのは、最後のパネルに概要手順が含まれている場合のみです。
   > * 署名または概要ステップのコンポーネントを含むパネルに、他のコンポーネントを含めることはできません。
   > * 署名手順を含むアダプティブフォームには、送信ボタンを含めることはできません。 送信は、バックグラウンドサービスまたは概要手順で処理されます。
   > * 署名または概要の手順を含むパネルから戻れないようにフォームをデザインします。



### 「ありがとうございます」ページまたは概要ステップコンポーネントの設定{#configure-the-thank-you-page-or-summary-step-component}

**概要ステップ**&#x200B;コンポーネントにより、フォームが自動的に送信され、カスタマイズ後の概要ページに情報が取り込まれ、送信されたフォームの概要情報が表示されます。また、リターンマップ内の必須情報も取得されます。概要ステップコンポーネントは、フォームで使用可能な全幅を占めます。 「概要手順」コンポーネントを含むセクションには、他のコンポーネントを含めないことをお勧めします。

これで、フォーム内署名機能を使用するための準備が整いました。フォームのプレビューを表示して、署名の方法を確認することができます。

## よくある質問 {#frequently-asked-questions}

**A:** いいえ。AEM Forms では、Adobe Sign が有効になっているアダプティブフォームが埋め込まれているアダプティブフォームを使用して署名することはできません。

**A:**&#x200B;拡張テンプレートを使用して作成されたアダプティブフォームは、Adobe Sign を使用するように設定されています。このエラーを修正するには、Adobe Sign のクラウド設定を作成して選択し、アダプティブフォーム用の Adobe Sign 署名者を設定してください。

**A:** はい。テキストコンポーネントでテキストタグを使用して、Adobe Sign のフィールドを[レコードのドキュメント](../../forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)（「自動生成されたレコードのドキュメント」オプション）が有効になっているアダプティブフォームに追加することができます。テキストタグを作成する手順とルールについては、[Adobe Sign のドキュメント](https://helpx.adobe.com/jp/sign/using/text-tag.html)を参照してください。アダプティブフォームでは、テキストタグを使用する場合に制限があることにも注意してください。テキストタグを使用して作成できるのは、[Adobe Sign ブロック](../../forms/using/working-with-adobe-sign.md#configure-cloud-signatures-for-an-adaptive-form)がサポートされているフィールドだけです。

**A:**&#x200B;はい。フォーム内で両方のコンポーネントを同時に使用することができます。これらのコンポーネントを使用する場合は、以下の推奨事項を参照してください。

**Adobe Signブロック：** Adobe Signブロックを使用すると、アダプティブフォームの任意の場所にAdobe Signフィールドを追加できます。 また、特定のフィールドを署名者に割り当てることもできます。アダプティブフォームのプレビュー時と発行時には、Adobe Sign ブロックがデフォルトで非表示になります。これらのブロックは、署名ドキュメント内でのみ使用することができます。署名ドキュメント内では、署名者に割り当てられているフィールド以外は使用できません。Adobe Sign ブロックは、最初の署名者だけでなく、後続の署名者も使用することができます。

**署名ステップコンポーネント：**&#x200B;署名ステップコンポーネントを使用すると、フォーム内署名機能を設定することができます。この機能では、最初の署名者のみ、フォームの入力時に署名を行うことができます。署名ステップコンポーネントが含まれているセクションをレンダリングすると、フォームの署名可能な PDF バージョンが表示されます。通常、フォームの最後または最後のセクションに続き、フォームの概要コンポーネントが表示されます。

## トラブルシューティング {#troubleshoot}

### Adobe Sign合意の失敗 {#adobe-sign-agreement-failures}

**問題**:Adobe Signサービスがアダプティブフォーム用に設定されている場合、そのサービスは基になるアダプティブフォーム用のAdobe Sign契約の作成に失敗します。

**解像度**

* アダプティブフォームで使用されているAdobe Signクラウドサービス [の](../../forms/using/adobe-sign-integration-adaptive-forms.md) 設定を確認します。
* Adobe Signクラウドサービスの設定に使用したAdobe Signサーバー上のAPIアプリケーションに、必要な権限があることを確認します。
* 複数のAdobe Signクラウドサービスを使用している場合は、すべてのサービスの **[!UICONTROL 認証URL]** を同じ **[!UICONTROL Adobe Signシャードに指定します]**。

* 別々の電子メールアドレスを使用して、Adobe Signアカウントと、最初の署名者および単一の署名者用の設定を行います。 最初の署名者の電子メールアドレスまたは唯一の署名者（単一の署名者の場合）は、AEMクラウドサービスの設定に使用されたAdobe Signアカウントと同一にできません。

## 関連記事 {#related-articles}

* [Adobe Sign を AEM Forms に統合する](../../forms/using/adobe-sign-integration-adaptive-forms.md)
* [アダプティブフォームで Adobe Sign を使用する](../../forms/using/working-with-adobe-sign.md)

* [Adobe SignとAEM Formsの併用（ビデオ）
   ](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
