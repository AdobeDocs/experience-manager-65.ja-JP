---
title: Adobe Sign の AEM Forms への統合
seo-title: Integrate Adobe Sign with AEM Adaptive Forms
description: AEM Adaptive Forms用のAdobe Signの設定について説明します。 Adobe Signは、法務、販売、給与、人事管理など、様々な分野に関するドキュメントのワークフローと処理を改善します。
uuid: e5049775-fb6c-4228-9823-e6a2811460da
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 1f28b257-5419-4a21-a54a-b20bf35530ac
docset: aem65
feature: Adaptive Forms, Acrobat Sign
exl-id: 52146038-1582-41b8-aee0-215d04bb91d7
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '1981'
ht-degree: 87%

---

# [!DNL Adobe Sign] の AEM [!DNL Forms] との統合{#integrate-adobe-sign-with-aem-forms}

<span class="preview"> Adobeでは、最新の拡張可能なデータキャプチャを使用することをお勧めします [コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja) 対象： [新しいアダプティブFormsの作成](/help/forms/using/create-an-adaptive-form-core-components.md) または [AEM SitesページへのアダプティブFormsの追加](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). これらのコンポーネントは、アダプティブフォームの作成における大幅な進歩を示すものであり、優れたユーザーエクスペリエンスを実現します。この記事では、基盤コンポーネントを使用してアダプティブフォームを作成するより従来的な方法について説明します。</span>

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/services/adobe-sign-integration-adaptive-forms.html?lang=en#adobe-acrobat-sign-for-government) |
| AEM 6.5 | この記事 |

[!DNL Adobe Sign] により、アダプティブフォームの電子サインワークフローを有効にできます。電子サインを使用すると、法務、販売、給与、人事管理など、様々な分野におけるドキュメント処理ワークフローが改善されます。

[!DNL Adobe Acrobat Sign] とアダプティブフォームの一般的なシナリオでは、ユーザーがアダプティブフォームに入力してサービスを申し込みます。例えば、クレジットカードの申込フォームや住民サービスフォームなどです。ユーザーが申込フォームの入力、送信、署名を行うと、追加のアクションのためにサービスプロバイダーにそのフォームが送信されます。サービスプロバイダーは受信した申込フォームを確認し、[!DNL Adobe Acrobat Sign] を使用して申請を承認します。AEM Forms は、Adobe Acrobat Sign および Adobe Acrobat Sign Solutions for Government の両方をサポートしています。ライセンスと要件に応じて、次のいずれかのソリューションと AEM Forms を統合または接続できます。

* [AEM Forms と Adobe Acrobat Sign の接続](#adobe-sign)
* [AEM Forms と Adobe Acrobat Sign Solutions for Government を接続](#adobe-acrobat-sign-for-government)

## AEM Forms と Adobe Acrobat Sign の接続 {#adobe-sign}

**[!DNL AEM Forms]** と **[!DNL Adobe Acrobat Sign]** を接続するには、前提条件の節に一覧表示されているソフトウェアとアカウントを設定し、Adobe Sign をすべての AEM Forms オーサーインスタンスとパブリッシュインスタンスに接続します。

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
1. 次の日： **[!UICONTROL 設定ブラウザー]** ページ、選択 **[!UICONTROL 作成]**.
   * 詳しくは、[設定ブラウザー](/help/sites-administering/configurations.md)のドキュメントを参照してください。
1. Adobe Analytics の **[!UICONTROL 設定を作成]** ダイアログ、指定する **[!UICONTROL タイトル]** 設定の場合は、を有効にします。 **[!UICONTROL クラウド設定]**&#x200B;をクリックし、次を選択します。 **[!UICONTROL 作成]**. 設定コンテナが作成されます。
1. **ツール** ![ハンマー](assets/hammer.png)／**[!UICONTROL Cloud Services]**／**[!UICONTROL Adobe Sign]** に移動し、上記の手順で作成した設定コンテナを選択します。

   >[!NOTE]
   >
   >手順 1～4 を実行して、設定コンテナを作成し、 [!DNL Adobe Sign] コンテナ内の設定、または既存の `global` フォルダー内 **ツール** ![ハンマー](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL Adobe Sign]**. 新しい設定コンテナで設定を作成する場合、必ず&#x200B;**[!UICONTROL 設定コンテナ]**&#x200B;フィールドに値を入力する必要があります。

   >[!NOTE]
   >
   Cloud Services 設定ページの URL が **HTTPS** で始まっていることを確認してください。「HTTPS」で始まっていない場合は、AEM [!DNL Forms] サーバーで [SSL を有効](/help/sites-administering/ssl-by-default.md)にしてください。

1. 設定ページで、「 」を選択します。 **[!UICONTROL 作成]** を作成します。 [!DNL Adobe Sign] AEMでの設定 [!DNL Forms].
1. Adobe Analytics の **[!UICONTROL 一般]** タブ **[!UICONTROL Adobe Sign設定を作成]** ページで、 **[!UICONTROL 名前]** を選択します。 **[!UICONTROL 次へ]**. 必要に応じてタイトルを指定し、設定のサムネールを参照して選択することもできます。

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
   1. AEM用に設定されたアプリケーションを選択します。 [!DNL Forms]をクリックし、次を選択します。 **[!UICONTROL アプリケーションの OAuth を設定]**.
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

   データベースシャードの値を更新することができます。サーバーを再起動すると、データベースシャードの新しい値を使用できます。

   >[!NOTE]
   >
   オーサーインスタンスとパブリッシュインスタンスの設定が同じシャードを指していることを確認します。1 つの組織に対して複数の Adobe Sign 設定を作成する場合は、すべての設定で同じシャードが使用されていることを確認します。

1. **[!UICONTROL Adobe Sign 設定を作成]**&#x200B;ページに戻ります。「**[!UICONTROL 設定]**」タブで、「**クライアント ID**」（アプリケーション ID とも言われます）と「**クライアント秘密鍵**」の値を指定します。AEM Forms 用に作成した [Adobe Sign アプリケーションのクライアント ID とクライアント秘密鍵](https://opensource.adobe.com/acrobat-sign/developer_guide/helloworld.html#get-the-app-id-and-secret)を使用します。

1. 「**[!UICONTROL 添付ファイルにも Adobe Sign を有効にする]**」オプションを選択すると、アダプティブフォームに添付されているファイルが、署名用に送信された対応する [!DNL Adobe Sign] ドキュメントに添付されます。

1. 選択 **[!UICONTROL Adobe Signに接続]**. 資格情報の入力画面が表示されたら、[!DNL Adobe Sign] アプリケーションの作成時に使用したユーザー名とパスワードを入力します。

1. 選択 **[!UICONTROL 作成]** を作成します。 [!DNL Adobe Sign] 設定。

1. AEM web コンソールを開きます。URL は `https://'[server]:[port]'/system/console/configMgr` です。
1. **[!UICONTROL Forms 共通設定サービス]を開きます。**
1. 「**[!UICONTROL 許可]**」フィールドで、「すべてのユーザー - すべてのユーザーに（匿名かログインしているかによらず）添付ファイルのプレビューとフォームの検証と署名を許可」を&#x200B;**選択**&#x200B;して「**[!UICONTROL 保存]」をクリックします。**&#x200B;オーサーインスタンスが [!DNL Adobe Sign] を使用するように設定されます。
1. 設定を公開します。
1. [レプリケーション](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/replication.html?lang=ja)を使用して、対応する公開インスタンスに同一の構成を作成します。

これで [!DNL Adobe Sign] が AEM [!DNL Forms] に統合され、アダプティブフォームで使用できるようになりました。[アダプティブフォームで Adobe Sign サービスを使用する](../../forms/using/working-with-adobe-sign.md#configure-adobe-sign-for-an-adaptive-form)には、上記のとおりアダプティブフォームのプロパティで作成した設定コンテナを指定します。

## AEM forms と Adobe Acrobat Sign Solutions for Government の接続 {#adobe-acrobat-sign-for-government}

AEM Forms と Adobe Acrobat Sign Solutions for Government の接続は、複数の手順で構成されます。以下が含まれます。

* AEM インスタンスのリダイレクト URL の作成
* リダイレクト URL とスコープを Adobe Sign Solutions for Government チームと共有
* Adobe Sign チームからの資格情報の受信
* 受け取った資格情報を使用して AEM Forms を Adobe Acrobat Sign Solutions for Government と接続

![adobe-acrobat-sign-govt-workflow](/help/forms/using/assets/adobe-acrobat-sign-govt-workflow.png)

### 事前準備 {#prerequisites-for-adobe-sign-for-acrobat-sign-for-government}

AEM Forms と Adobe Acrobat Sign Solutions の接続を開始する前に、

* [Adobe Acrobat Sign Solutions for Government](https://opensource.adobe.com/acrobat-sign/signgov/gstarted.html#account-provisioning) アカウントがプロビジョニングされていることを確認します。
* AEM [!DNL Forms] サーバーが [SSL 有効](/help/sites-administering/ssl-by-default.md)になっていること。
* AEM [!DNL Forms] サーバーが、オーサーインスタンスとパブリッシュインスタンスに[同一の暗号キー](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed)を使用していること。

### AEM forms と Adobe Acrobat Sign Solutions for Government の接続 {#connect-adobe-acrobat-sign-for-government}

#### AEM インスタンスのリダイレクト URL の作成

1. AEM Forms のインスタンスで、**[!UICONTROL ツール]** ![ハンマー](assets/hammer.png)／**[!UICONTROL 一般]**／**[!UICONTROL 設定ブラウザー]**&#x200B;に移動します。
1. 次の日： **[!UICONTROL 設定ブラウザー]** ページ、選択 **[!UICONTROL 作成]**.
1. Adobe Analytics の **[!UICONTROL 設定を作成]** ダイアログ、指定する **[!UICONTROL タイトル]** 設定の場合は、を有効にします。 **[!UICONTROL クラウド設定]**&#x200B;をクリックし、次を選択します。 **[!UICONTROL 作成]**. これにより、設定コンテナが作成されます。コンテナ／フォルダー名にスペースが含まれていないことを確認します。

1. **[!UICONTROL ツール]** ![ハンマー](assets/hammer.png)／**[!UICONTROL クラウドサービス]**／**[!UICONTROL Adobe Acrobat Sign]** に移動し、上記の手順で作成した設定コンテナを開きます。アダプティブフォームを作成する際に、**[!UICONTROL 設定コンテナ]**&#x200B;フィールドにコンテナ名を指定します。
1. 設定ページで、「 」を選択します。 **[!UICONTROL 作成]** を作成します。 [!DNL Adobe Acrobat Sign] AEM Formsでの設定
1. 現在のブラウザーウィンドウの URL を、URL からメモ帳にコピーします。この URL は、`re-direct URL` と呼ばれます。次の節では、`re-direct URL` と `Scopes` を Adobe Sign チームと共有し、資格情報（クライアント ID とクライアント秘密鍵）をリクエストします。

>[!NOTE]
>
>
* `re-direct URL` には、[トップレベル](https://en.wikipedia.org/wiki/Top-level_domain)ドメインを含める必要があります。例：`https://adobe.com/libs/adobesign/cloudservices/adobesign/createcloudconfigwizard/cloudservices.html/conf/global`
* ローカル URL を `re-direct URL` として使用しないでください。例：`https://localhost:4502/libs/adobesign/cloudservices/adobesign/createcloudconfigwizard/cloudservices.html/conf/global`


#### Adobe Sign チームとのリダイレクト URL とスコープの共有および資格情報の受信

Adobe Acrobat Sign for Government Solutions チームには、 `re-direct URL` Adobe Acrobat Signアプリケーション（以下に示す）でAEM Formsと政府機関との接続に使用する資格情報（クライアント ID とクライアント秘密鍵）を生成するために有効にするスコープ。

前の節の最後の手順で作成してメモした `scopes`（下記）と `re-direct URL` を、Adobe Acrobat Sign Solutions for Government の担当者である [Adobe Professional Services チームメンバー](https://opensource.adobe.com/acrobat-sign/signgov/gstarted.html#password)と共有します。

**_スコープ_**

* [!DNL agreement_read]
* [!DNL agreement_write]
* [!DNL agreement_send]
* [!DNL widget_read]
* [!DNL widget_write]
* [!DNL workflow_read]
* [!DNL offline_access]

担当者が資格情報を生成し、共有します。次の節では、資格情報（クライアント ID とクライアントの秘密鍵）を使用して、AEM Forms を Adobe Acrobat Sign Solutions for Government に接続します。

#### 受け取った資格情報を使用して、AEM Forms を Adobe Acrobat Sign Solutions for Government に接続する

1. ブラウザーで `re-direct URL` を開きます。「[AEM インスタンスにリダイレクト URL を作成](#create-redirect-url)」セクションの最後の手順で `re-direct URL` を作成し、書き留めました。

1. Adobe Analytics の **[!UICONTROL 一般]** タブ **[!UICONTROL Adobe Sign設定を作成]** ページで、 **[!UICONTROL 名前]** を選択します。 **[!UICONTROL 次へ]**. 必要に応じて&#x200B;**[!UICONTROL タイトル]**&#x200B;を指定し、設定の&#x200B;**[!UICONTROL サムネ―ル]**&#x200B;を参照して選択することもできます。「**[!UICONTROL 次へ]**」をクリックします。

1. **[!UICONTROL Adobe Sign 設定を作成]**&#x200B;ページの「**[!UICONTROL 設定]**」タブの、「**[!UICONTROL ソリューションを選択]**」オプションで、[!DNL Adobe Acrobat Sign Solutions for Government] を選択します。

   ![政府向け Adobe Acrobat Sign ソリューション](/help/forms/using/assets/adobe-sign-for-govt.png)

1. 「**[!UICONTROL メール]**」フィールドで、Adobe Acrobat Sign Solutions for Government アカウントに関連付けられたメールアドレスを指定します。

1. 「**[!UICONTROL OAuth URL]**」フィールドは、Adobe Sign データベースシャードを指定します。このフィールドにはデフォルトの URL が含まれています。URL を変更しないでください。

1. 前の節で、Adobe Acrobat Sign for Government Solution 担当者（[Adobe Professional Services チームメンバー]）が共有した資格情報を [**[!UICONTROL クライアント ID]** と&#x200B;**[!UICONTROL クライアントの秘密鍵]**] として使用します。

1. 「**[!UICONTROL 添付ファイルの Adobe Acrobat Sign を有効にする]**」オプションを選択すると、アダプティブフォームに添付されているファイルが、署名用に送信された対応する [!DNL Adobe Acrobat Sign] ドキュメントに添付されます。

1. 選択 **[!UICONTROL Adobe Signに接続]**. 資格情報の入力画面が表示されたら、[!DNL Adobe Acrobat Sign] アプリケーションの作成時に使用したユーザー名とパスワードを入力します。`Adobe Acrobat Sign for Government Solutions` へのアクセスを確認するメッセージが表示されたら、「**[!UICONTROL アクセスを許可]**」をクリックします。資格情報が正しく、[!DNL AEM Forms] が [!DNL Adobe Acrobat Sign] 開発者アカウントにアクセスできるようにした場合は、次のような成功メッセージが表示されます。

   ![Adobe Acrobat Sign クラウド設定成功](/help/forms/using/assets/adobe-sign-cloud-configuration-success.png)

   資格情報の入力画面が表示されたら、[!DNL Adobe Acrobat Sign] アプリケーションの作成時に使用したユーザー名とパスワードを入力します。`your account` へのアクセスを確認するメッセージが表示されたら、「**[!UICONTROL アクセスを許可]**」をクリックします。

1. 選択 **[!UICONTROL 作成]** をクリックして設定を作成します。
1. AEM web コンソールを開きます。URL は `https://'[server]:[port]'/system/console/configMgr` です。
1. **[!UICONTROL Forms 共通設定サービス]を開きます。**
1. 「**[!UICONTROL 許可]**」フィールドで、「すべてのユーザー - すべてのユーザーに（匿名かログインしているかによらず）添付ファイルのプレビューとフォームの検証と署名を許可」を&#x200B;**選択**&#x200B;して「**[!UICONTROL 保存]」をクリックします。**&#x200B;オーサーインスタンスが [!DNL Adobe Sign] を使用するように設定されます。

1. 設定を公開します。
1. [レプリケーション](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/replication.html?lang=ja)を使用して、対応する公開インスタンスに同一の構成を作成します。

これで、[アダプティブフォーム](working-with-adobe-sign.md)または [AEM ワークフローで Adobe Acrobat Sign のフィールドの追加を使用](/help/forms/using/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step)できます。[!DNL Adobe Acrobat Sign] 用に有効化するすべてのアダプティブフォームに、Cloud Service の設定に使用する設定コンテナを追加してください。設定コンテナは、アダプティブフォームのプロパティから指定できます。


## [!DNL Adobe Sign] スケジューラーを設定して署名ステータスを同期する {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

[!DNL Adobe Sign] が有効になっているアダプティブフォームは、すべての署名者がフォームに署名するまで送信されません。[!DNL Adobe Sign] Scheduler サービスは、デフォルトで、署名者からの応答を 24 時間ごとにチェック（ポーリング）するように設定されています。このデフォルトの間隔は、ご利用の環境に合わせて変更できます。デフォルトの間隔を変更するには、次の手順を実行します。

1. 管理者の資格情報を使用して AEM [!DNL Forms] サーバーにログインし、**ツール**／**[!UICONTROL 操作]**／**[!UICONTROL Web コンソール]**&#x200B;に移動します。

   ブラウザーウィンドウで、以下の URL に移動することもできます。
   `https://[localhost]:'port'/system/console/configMgr`

1. 「**[!UICONTROL Adobe Sign 設定サービス]**」オプションを探して選択します。「**[!UICONTROL ステータス更新スケジューラーの式]**」フィールドで [Cron 式](https://en.wikipedia.org/wiki/Cron#CRON_expression)を指定して「**[!UICONTROL 保存]**」をクリックします。例えば、毎日午前 0 時に設定サービスを実行するには、**[!UICONTROL ステータス更新スケジューラー式]**&#x200B;フィールドに `0 0 0 1/1 * ? *` を指定します。

これで、[!DNL Adobe Sign] のステータスを同期するデフォルトの間隔が変更されました。

## 関連記事 {#related-articles}

* [アダプティブフォームで Adobe Sign を使用する](../../forms/using/working-with-adobe-sign.md)
* [Adobe Sign と Forms 中心のワークフロー](/help/forms/using/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step)
* [AEM Forms で Adobe Sign を使用（ビデオ）](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/forms-and-sign/introduction.html?lang=ja)
