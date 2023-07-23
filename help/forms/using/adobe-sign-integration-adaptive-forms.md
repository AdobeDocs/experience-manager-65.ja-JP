---
title: Adobe Sign の AEM Forms への統合
seo-title: Integrate Adobe Sign with AEM Forms
description: Adobe Sign for AEM Formsの設定方法を説明します
seo-description: Learn how to configure Adobe Sign for AEM Forms
uuid: e5049775-fb6c-4228-9823-e6a2811460da
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 1f28b257-5419-4a21-a54a-b20bf35530ac
docset: aem65
feature: Adaptive Forms, Acrobat Sign
exl-id: 52146038-1582-41b8-aee0-215d04bb91d7
source-git-commit: e7a3558ae04cd6816ed73589c67b0297f05adce2
workflow-type: tm+mt
source-wordcount: '2055'
ht-degree: 59%

---

# [!DNL Adobe Sign] の AEM [!DNL Forms] との統合{#integrate-adobe-sign-with-aem-forms}

<span class="preview"> Adobeでは、最新の拡張可能なデータキャプチャを使用することをお勧めします [コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja) 対象 [新しいアダプティブFormsの作成](/help/forms/using/create-an-adaptive-form-core-components.md) または [AEM SitesページへのアダプティブFormsの追加](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). これらのコンポーネントは、アダプティブFormsの作成における大幅な進歩を表し、印象的なユーザーエクスペリエンスを実現します。 この記事では、基盤コンポーネントを使用してアダプティブFormsを作成する古い方法について説明します。 </span>

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/services/adobe-sign-integration-adaptive-forms.html?lang=en#adobe-acrobat-sign-for-government) |
| AEM 6.5 | この記事 |

[!DNL Adobe Sign] により、アダプティブフォームの電子サインワークフローを有効にできます。電子サインを使用すると、法務、販売、給与、人事管理など、様々な分野におけるドキュメント処理ワークフローが改善されます。

[!DNL Adobe Acrobat Sign] とアダプティブフォームの一般的なシナリオでは、ユーザーがアダプティブフォームに入力してサービスを申し込みます。例えば、クレジットカードの申込フォームや住民サービスフォームなどです。ユーザーが申込フォームに入力、送信、署名すると、フォームがサービスプロバイダーに送信され、さらにアクションが実行されます。 サービスプロバイダーは受信した申込フォームを確認し、[!DNL Adobe Acrobat Sign] を使用して申請を承認します。AEM Formsは、Adobe Acrobat SignとAdobe Acrobat Sign Solutionsの両方の政府機関をサポートしています。 ライセンスと要件に応じて、次のいずれかのソリューションとAEM Formsを統合または接続できます。

* [AEM FormsとAdobe Acrobat Signの接続](#adobe-sign)
* [AEM FormsをAdobe Acrobat Sign Solutionsと連携して政府機関向け](#adobe-acrobat-sign-for-government)

## AEM FormsとAdobe Acrobat Signの接続 {#adobe-sign}

接続するには **[!DNL AEM Forms]** と **[!DNL Adobe Acrobat Sign]**&#x200B;を設定し、前提条件の節に示すソフトウェアとアカウントを設定して、Adobe SignをすべてのAEM Formsオーサーインスタンスとパブリッシュインスタンスに接続します。

## 前提条件 {#prerequisites}

[!DNL Adobe Sign] を AEM [!DNL Forms] に統合するには、以下のものが必要になります。

* 有効な [Adobe Sign 開発者アカウント](https://acrobat.adobe.com/jp/ja/why-adobe/developer-form.html)
* [SSL が有効になっている](/help/sites-administering/ssl-by-default.md) AEM サーバー[!DNL Forms]
* [Adobe Sign API アプリケーション](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md)。
* [!DNL Adobe Sign] API アプリケーションの資格情報（クライアント ID およびクライアントの秘密鍵）。
* 再構成時に、作成インスタンスと公開インスタンスの両方から既存の [!DNL Adobe Sign] 構成を削除します。
* オーサーインスタンスとパブリッシュインスタンスには、[同一の暗号キー](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed)を使用します。

## AEM [!DNL Forms] を使用して [!DNL Adobe Sign] を設定する {#configure-adobe-sign-with-aem-forms}

上記の前提条件の準備が完了したら、以下の手順により、オーサーインスタンス上の AEM [!DNL Forms] を使用して [!DNL Adobe Sign] を設定します。

1. AEM [!DNL Forms] のオーサーインスタンスで、**ツール** ![ハンマー](assets/hammer.png)／**[!UICONTROL 一般]**／**[!UICONTROL 設定ブラウザー]**&#x200B;に移動します。
1. **[!UICONTROL 設定ブラウザー]**&#x200B;ページで「**[!UICONTROL 作成]**」をタップします。
   * 詳しくは、[設定ブラウザー](/help/sites-administering/configurations.md)のドキュメントを参照してください。
1. **[!UICONTROL 設定を作成]**&#x200B;ダイアログで、設定の&#x200B;**[!UICONTROL タイトル]**&#x200B;を指定し、「**[!UICONTROL クラウド設定]**」を有効にして「**[!UICONTROL 作成]**」をタップします。設定コンテナが作成されます。
1. **ツール** ![ハンマー](assets/hammer.png)／**[!UICONTROL Cloud Services]**／**[!UICONTROL Adobe Sign]** に移動し、上記の手順で作成した設定コンテナを選択します。

   >[!NOTE]
   >
   >手順1〜4を実行して、新しい構成コンテナを作成し、コンテナで [!DNL Adobe Sign] 構成を作成するか、**ツール** ![ハンマー](assets/hammer.png)／**[!UICONTROL Cloud Services]**／**[!UICONTROL Adobe Sign]**&#x200B;で既存の `global` フォルダーを使用できます。新しい設定コンテナで設定を作成する場合、必ず&#x200B;**[!UICONTROL 設定コンテナ]**&#x200B;フィールドに値を入力する必要があります。

   >[!NOTE]
   >
   設定ページの URL がで始まっていることをCloud Services設定ページで確認します。 **HTTPS**. 「HTTPS」で始まっていない場合は、AEM [!DNL Forms] サーバーで [SSL を有効](/help/sites-administering/ssl-by-default.md)にしてください。

1. 設定ページで「**[!UICONTROL 作成]**」をタップして、AEM [!DNL Forms] 内に [!DNL Adobe Sign] の設定を作成します。
1. **[!UICONTROL Adobe Sign 設定を作成]**&#x200B;ページの「**[!UICONTROL 一般]**」タブで、設定の&#x200B;**[!UICONTROL 名前]**&#x200B;を指定して「**[!UICONTROL 次へ]**」をタップします。必要に応じてタイトルを指定し、設定のサムネールを参照して選択することもできます。

1. 現在のブラウザーウィンドウの URL をメモ帳にコピーします。この URL は、AEM [!DNL Forms] で [!DNL Adobe Sign] アプリケーションを設定する際に必要になります。

1. 「**[!UICONTROL 設定]**」タブで、「**[!UICONTROL OAuth URL]**」フィールドにはデフォルトの URL が入力されています。URL の形式は次の通りです。

   `https://<shard>/public/oAuth/v2`

   次に例を示します。
   `https://secure.na1.echosign.com/public/oauth/v2`

   各パラメーターの意味は次のとおりです。

   **na1** は、デフォルトのデータベースシャードを参照します。データベースシャードの値を更新することができます。[!DNL  Adobe Sign] クラウド設定で、[正しいシャード](https://helpx.adobe.com/jp/sign/using/identify-account-shard.html)をポイントしていることを確認します。

   別の [!DNL Adobe Sign] 設定を Adobe Experience Manager の機能またはコンポーネント用に作成する場合は、すべての [!DNL Adobe Sign] クラウド設定が同じシャードをポイントしていることを確認してください。

   >[!NOTE]
   >
   **Adobe Sign 設定を作成**&#x200B;ページを開いたままにします。 閉じないでください。 **クライアント ID** および&#x200B;**クライアント秘密鍵**&#x200B;は、以降の手順で説明するように、[!DNL Adobe Sign] アプリケーションの OAuth 設定を行った後に取得できます。


1. 以下の手順に従って、[!DNL Adobe Sign] アプリケーションの OAuth 設定を指定します。

   1. ブラウザーウィンドウを開き、[!DNL Adobe Sign] 開発者アカウントにサインインします。
   1. AEM [!DNL Forms] 用に設定されているアプリケーションを選択し、「**[!UICONTROL アプリケーションの OAuth を設定]**」をタップします。
   1. **[!UICONTROL クライアント ID]** および&#x200B;**[!UICONTROL クライアント秘密鍵]**&#x200B;をメモ帳に追加します。
   1. 上記の手順でコピーした HTTPS URL を「**[!UICONTROL リダイレクト URL]**」ボックスに追加します。
   1. [!DNL Adobe Sign] アプリケーションに対して以下の OAuth 設定を有効にして、「**[!UICONTROL 保存]**」をクリックします。

   * agreement_read
   * agreement_write
   * agreement_send
   * widget_write
   * workflow_read

   [!DNL Adobe Sign] アプリケーション用に OAuth 設定を構成してキーを取得するための詳しい手順については、開発者用ドキュメントの[アプリケーション用に OAuth 設定を構成する](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md)を参照してください。

   ![OAuth 設定](assets/oauthconfig_new.png)

1. **[!UICONTROL Adobe Sign 設定を作成]**&#x200B;ページに戻ります。「**[!UICONTROL 設定]**」タブで、「**[!UICONTROL OAuth URL]**」フィールドに以下のデフォルトの URL が表示されます。URL の形式は次の通りです。

   `https://<shard>/public/oAuth/v2`

   次に例を示します。
   `https://secure.na1.echosign.com/public/oauth/v2`

   各パラメーターの意味は次のとおりです。

   **na1** は、デフォルトのデータベースシャードを参照します。

   データベースシャードの値を更新することができます。データベースシャードの新しい値を使用できるように、サーバーを再起動します。

   >[!NOTE]
   >
   オーサーインスタンスとパブリッシュインスタンスの設定が同じシャードを指していることを確認します。1 つの組織に対して複数の Adobe Sign 設定を作成する場合は、すべての設定で同じシャードが使用されていることを確認します。

1. **[!UICONTROL Adobe Sign 設定を作成]**&#x200B;ページに戻ります。「**[!UICONTROL 設定]**」タブで、「**クライアント ID**」（アプリケーション ID とも言われます）と「**クライアント秘密鍵**」の値を指定します。AEM Forms 用に作成した [Adobe Sign アプリケーションのクライアント ID とクライアント秘密鍵](https://opensource.adobe.com/acrobat-sign/developer_guide/helloworld.html#get-the-app-id-and-secret)を使用します。

1. 「**[!UICONTROL 添付ファイルにも Adobe Sign を有効にする]**」オプションを選択すると、アダプティブフォームに添付されているファイルが、署名用に送信された対応する [!DNL Adobe Sign] ドキュメントに添付されます。

1. 「**[!UICONTROL Adobe Sign に接続]**」をタップします。資格情報の入力画面が表示されたら、[!DNL Adobe Sign] アプリケーションの作成時に使用したユーザー名とパスワードを入力します。

1. 「**[!UICONTROL 作成]**」をタップして、[!DNL Adobe Sign] 設定を作成します。

1. AEM web コンソールを開きます。URL は `https://'[server]:[port]'/system/console/configMgr` です。
1. **[!UICONTROL Forms 共通設定サービス]を開きます。**
1. 「**[!UICONTROL 許可]**」フィールドで、「すべてのユーザー - すべてのユーザーに（匿名かログインしているかによらず）添付ファイルのプレビューとフォームの検証と署名を許可」を&#x200B;**選択**&#x200B;して「**[!UICONTROL 保存]」をクリックします。**&#x200B;オーサーインスタンスが [!DNL Adobe Sign] を使用するように設定されます。
1. 設定を公開します。
1. [レプリケーション](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/replication.html?lang=ja)を使用して、対応する公開インスタンスに同一の構成を作成します。

これで [!DNL Adobe Sign] が AEM [!DNL Forms] に統合され、アダプティブフォームで使用できるようになりました。[アダプティブフォームで Adobe Sign サービスを使用する](../../forms/using/working-with-adobe-sign.md#configure-adobe-sign-for-an-adaptive-form)には、上記のとおりアダプティブフォームのプロパティで作成した設定コンテナを指定します。

## AEM FormsをAdobe Acrobat Sign Solutionsと連携して政府機関向け {#adobe-acrobat-sign-for-government}

AEM FormsとAdobe Acrobat Sign Solutions for Government の接続は、複数の手順で構成されます。 以下が含まれます。

* AEMインスタンスのリダイレクト URL の作成
* リダイレクト URL とスコープをAdobe Sign Solutions for Government チームと共有する
* Adobe Signチームからの資格情報の受信
* 受け取った資格情報を使用してAEM FormsをAdobe Acrobat Sign Solutions for Government に接続します

![adobe-acrobat-sign-govt-workflow](/help/forms/using/assets/adobe-acrobat-sign-govt-workflow.png)

### 事前準備 {#prerequisites-for-adobe-sign-for-acrobat-sign-for-government}

AEM FormsとAdobe Acrobat Sign Solution の接続を開始する前に、

* 次を確認します。 [Adobe Acrobat Sign Solutions for Government](https://opensource.adobe.com/acrobat-sign/signgov/gstarted.html#account-provisioning) アカウントがプロビジョニングされました。
* AEM [!DNL Forms] サーバは [SSL が有効](/help/sites-administering/ssl-by-default.md) .
* AEM [!DNL Forms] サーバーが使用しています [同一の暗号鍵](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed) オーサーインスタンスとパブリッシュインスタンスの場合。

### AEM FormsをAdobe Acrobat Sign Solutionsに接続して政府機関向け {#connect-adobe-acrobat-sign-for-government}

#### AEMインスタンスのリダイレクト URL の作成

1. AEM Formsインスタンスで、に移動します。 **[!UICONTROL ツール]** ![ハンマー](assets/hammer.png) > **[!UICONTROL 一般]** > **[!UICONTROL 設定ブラウザー]**.
1. **[!UICONTROL 設定ブラウザー]**&#x200B;ページで「**[!UICONTROL 作成]**」をタップします。
1. **[!UICONTROL 設定を作成]**&#x200B;ダイアログで、設定の&#x200B;**[!UICONTROL タイトル]**&#x200B;を指定し、「**[!UICONTROL クラウド設定]**」を有効にして「**[!UICONTROL 作成]**」をタップします。設定コンテナが作成されます。 コンテナ名またはフォルダー名にスペースが含まれていないことを確認します。

1. に移動します。 **[!UICONTROL ツール]** ![ハンマー](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Acrobat Sign]** 前の手順で作成した設定コンテナを開きます。 アダプティブフォームを作成する際に、**[!UICONTROL 設定コンテナ]**&#x200B;フィールドにコンテナ名を指定します。
1. 設定ページで「**[!UICONTROL 作成]**」をタップして、AEM Forms 内に [!DNL Adobe Acrobat Sign] の設定を作成します。
1. 現在のブラウザーウィンドウの URL を、URL からメモ帳にコピーします。 この URL は `re-direct URL`. 次の節では、 `re-direct URL` および `Scopes` Adobe Signチームとリクエスト資格情報（クライアント ID とクライアント秘密鍵）を使用します。

>[!NOTE]
>
>
* A `re-direct URL` には、 [トップレベル](https://en.wikipedia.org/wiki/Top-level_domain) ドメイン。 例：`https://adobe.com/libs/adobesign/cloudservices/adobesign/createcloudconfigwizard/cloudservices.html/conf/global`
* ローカル URL を `re-direct URL`. 例：`https://localhost:4502/libs/adobesign/cloudservices/adobesign/createcloudconfigwizard/cloudservices.html/conf/global`


#### リダイレクト URL とスコープをAdobe Signチームと共有し、資格情報を受け取る

Adobe Acrobat Sign for Government Solutions チームには、 `re-direct URL` Adobe Acrobat Signアプリケーション（以下に示す）でAEM Formsと政府機関向けのAdobe Acrobat Sign Solutionsとの接続を可能にする資格情報（クライアント ID とクライアント秘密鍵）を生成するために有効にするスコープ。

共有する `scopes` （以下に示す）および `re-direct URL` Adobe Acrobat Sign for Government Solution 担当者と共に前の節の最後の手順を作成し、メモしました。 [Adobe Professional Servicesチームメンバー](https://opensource.adobe.com/acrobat-sign/signgov/gstarted.html#password).

**_スコープ_**

* [!DNL agreement_read]
* [!DNL agreement_write]
* [!DNL agreement_send]
* [!DNL widget_read]
* [!DNL widget_write]
* [!DNL workflow_read]
* [!DNL offline_access]

担当者が資格情報を生成し、共有します。 次の節では、資格情報（クライアント ID とクライアントの秘密鍵）を使用して、AEM FormsをAdobe Acrobat Sign Solutionsと政府機関向けに接続します。

#### 受け取った資格情報を使用してAEM FormsをAdobe Acrobat Sign Solutions for Government に接続します

1. を開きます。 `re-direct URL` ブラウザーに表示されます。 を作成し、 `re-direct URL` の最後の段階で [AEMインスタンスでのリダイレクト URL の作成](#create-redirect-url) 」セクションに入力します。

1. **[!UICONTROL Adobe Sign 設定を作成]**&#x200B;ページの「**[!UICONTROL 一般]**」タブで、設定の&#x200B;**[!UICONTROL 名前]**&#x200B;を指定して「**[!UICONTROL 次へ]**」をタップします。必要に応じて&#x200B;**[!UICONTROL タイトル]**&#x200B;を指定し、設定の&#x200B;**[!UICONTROL サムネ―ル]**&#x200B;を参照して選択することもできます。「**[!UICONTROL 次へ]**」をクリックします。

1. 内 **[!UICONTROL 設定]** タブ **[!UICONTROL Adobe Sign設定を作成]** ページ、 **[!UICONTROL ソリューションを選択]** オプション、選択 [!DNL Adobe Acrobat Sign Solutions for Government].

   ![Adobe Acrobat Sign Solutions for Government](/help/forms/using/assets/adobe-sign-for-govt.png)

1. 内 **[!UICONTROL 電子メール]** 「 」フィールドで、Adobe Acrobat Sign Solutions for Government アカウントに関連付けられた電子メールアドレスを指定します。

1. この **[!UICONTROL OAuth URL]** フィールドは、Adobe Signデータベースシャードを指定します。 「 」フィールドにはデフォルトの URL が入力されます。 URL は変更しないでください。

1. Adobe Acrobat Signが政府機関向けのソリューション担当者 ([Adobe Professional Servicesチームメンバー]) を [**[!UICONTROL クライアント ID]** および **[!UICONTROL クライアント秘密鍵]**].

1. を選択します。 **[!UICONTROL 添付ファイルに対してAdobe Acrobat Signを有効にする]** アダプティブフォームに添付されたファイルを、対応する [!DNL Adobe Acrobat Sign] ドキュメントが署名用に送信されました。

1. 「**[!UICONTROL Adobe Sign に接続]**」をタップします。資格情報の入力画面が表示されたら、[!DNL Adobe Acrobat Sign] アプリケーションの作成時に使用したユーザー名とパスワードを入力します。次のアクセスを確認するメッセージが表示されたとき `Adobe Acrobat Sign for Government Solutions` 「 」、「 」、「 」の順にクリックします。 **[!UICONTROL アクセスを許可]**. 資格情報が正しく、[!DNL AEM Forms] が [!DNL Adobe Acrobat Sign] 開発者アカウントにアクセスできるようにした場合は、次のような成功メッセージが表示されます。

   ![Adobe Acrobat Sign Cloud 設定成功](/help/forms/using/assets/adobe-sign-cloud-configuration-success.png)

   資格情報の入力画面が表示されたら、[!DNL Adobe Acrobat Sign] アプリケーションの作成時に使用したユーザー名とパスワードを入力します。次のアクセスを確認するメッセージが表示されたとき `your account`をクリックし、 **[!UICONTROL アクセスを許可]**.

1. 「**[!UICONTROL 作成]**」をタップして、 設定を作成します。
1. AEM web コンソールを開きます。URL は `https://'[server]:[port]'/system/console/configMgr` です。
1. **[!UICONTROL Forms 共通設定サービス]を開きます。**
1. 「**[!UICONTROL 許可]**」フィールドで、「すべてのユーザー - すべてのユーザーに（匿名かログインしているかによらず）添付ファイルのプレビューとフォームの検証と署名を許可」を&#x200B;**選択**&#x200B;して「**[!UICONTROL 保存]」をクリックします。**&#x200B;オーサーインスタンスが [!DNL Adobe Sign] を使用するように設定されます。

1. 設定を公開します。
1. [レプリケーション](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/replication.html?lang=ja)を使用して、対応する公開インスタンスに同一の構成を作成します。

次に、以下を実行できます。 [アダプティブフォームでのAdobe Acrobat Signフィールドの追加を使用します。](working-with-adobe-sign.md) または [AEM Workflow](/help/forms/using/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step). Cloud Service設定に使用する設定コンテナを、有効になっているすべてのアダプティブFormsに追加してください。 [!DNL Adobe Acrobat Sign]. 設定コンテナは、アダプティブフォームのプロパティから指定できます。


## [!DNL Adobe Sign] スケジューラーを設定して署名ステータスを同期する {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

[!DNL Adobe Sign] が有効になっているアダプティブフォームは、すべての署名者がフォームに署名するまで送信されません。[!DNL Adobe Sign] Scheduler サービスは、デフォルトで、署名者からの応答を 24 時間ごとにチェック（ポーリング）するように設定されています。このデフォルトの間隔は、ご利用の環境に合わせて変更できます。デフォルトの間隔を変更するには、次の手順を実行します。

1. 管理者の資格情報を使用して AEM [!DNL Forms] サーバーにログインし、**ツール**／**[!UICONTROL 操作]**／**[!UICONTROL Web コンソール]**&#x200B;に移動します。

   ブラウザーウィンドウで、以下の URL に移動することもできます。
   `https://[localhost]:'port'/system/console/configMgr`

1. を探して開きます。 **[!UICONTROL Adobe Sign Configuration Service]** オプション。 を指定します。 [cron 式](https://en.wikipedia.org/wiki/Cron#CRON_expression) 内 **[!UICONTROL ステータス更新スケジューラの式]** フィールドとクリック **[!UICONTROL 保存]**. 例えば、毎日午前 0 時に設定サービスを実行するには、**[!UICONTROL ステータス更新スケジューラー式]**&#x200B;フィールドに `0 0 0 1/1 * ? *` を指定します。

これで、[!DNL Adobe Sign] のステータスを同期するデフォルトの間隔が変更されました。

## 関連記事 {#related-articles}

* [アダプティブフォームで Adobe Sign を使用する](../../forms/using/working-with-adobe-sign.md)
* [Form 中心のワークフローを備えたAdobe Sign](/help/forms/using/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step)
* [AEM Forms で Adobe Sign を使用（ビデオ）](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/forms-and-sign/introduction.html?lang=ja)
