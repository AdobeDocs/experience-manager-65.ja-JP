---
title: AEM Assets と Brand Portal の連携の設定
seo-title: AEM Assets と Brand Portal の連携の設定
description: Brand Portalにアセットやコレクションを公開するためのBrand Portalを使用したAEM Assetsの設定方法について説明します。
seo-description: Brand Portalにアセットやコレクションを公開するためのBrand Portalを使用したAEM Assetsの設定方法について説明します。
uuid: b95c046e-9988-444c-b50e-ff5ec8cafe14
topic-tags: brand-portal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: dca5a2ac-1fc8-4251-b073-730fd6f49b1c
docset: aem65
translation-type: tm+mt
source-git-commit: 7c03ba5e2ec7954cca8b129f453919d151956df5
workflow-type: tm+mt
source-wordcount: '2084'
ht-degree: 33%

---


# AEM Assets と Brand Portal の連携の設定 {#configure-integration-65}

Adobe Experience Managerアセットブランドポータルを使用すると、承認されたブランドアセットをAdobe Experience ManagerアセットからBrand Portalに公開し、Brand Portalユーザに配信できます。

AEM Assetsは、Adobe開発者コンソールを介してBrand Portalで設定されます。このコンソールは、Brand Portalテナントの認証用にAdobeIdentity Managementサービス(IMS)アカウントトークンを調達します。

>[!NOTE]
>
>Adobe開発者コンソールを使用したBrand PortalでのAEM Assetsの設定は、AEM 6.5.4.0以降でサポートされています。
>
>以前は、Brand Portalは従来のOAuth Gatewayを介して設定されていました。従来のOAuth Gatewayは、JSON Web Token(JWT)交換を使用して、認証用のIMSアクセストークンを取得します。
>
>従来のOAuth Gatewayを使用した設定は、2020年4月6日からサポートされなくなり、Adobe開発者コンソールに変更されました。


>[!TIP]
>
>***既存のお客様のみ***
>
>既存のレガシーOAuth Gateway構成を引き続き使用することをお勧めします。 レガシーOAuth Gateway設定で問題が発生した場合は、既存の設定を削除し、Adobe開発者コンソールを使用して新しい設定を作成します。



このヘルプでは、次の2つの使用例について説明します。
* [新しい設定](#configure-new-integration-65):新しいBrand Portalユーザーで、Brand PortalでAEM Assetsの作成者インスタンスを設定する場合は、Adobe開発者コンソールで設定を作成できます。
* [アップグレード設定](#upgrade-integration-65):既存のBrand Portalユーザーが従来のOAuth Gatewayに対して設定を行っている場合は、既存の設定を削除し、Adobe開発者コンソールを使用して新しい設定を作成します。

具体的には、以下の操作に関する十分な知識があるユーザーを対象としています。

* Adobe Experience ManagerおよびAEMパッケージのインストール、設定、管理。

* LinuxおよびMicrosoft Windowsオペレーティングシステムの使用

## 前提条件 {#prerequisites}

AEM Assets と Brand Portal の連携を設定するには以下が必要です。

* 最新のService Packを含むAEM Assets作成者インスタンスを起動および実行する
* Brand PortalテナントURL
* Brand PortalテナントのIMS組織に対するシステム管理者権限を持つユーザー


[AEM 6.5のダウンロードとインストール](#aemquickstart)

[最新の AEM サービスパックをダウンロードしてインストールする](#servicepack)

### Download and install AEM 6.5 {#aemquickstart}

AEMオーサーインスタンスを設定するには、AEM 6.5を使用することをお勧めします。 AEM が稼働していない場合は、以下の場所から AEM をダウンロードしてください。

* If you are an existing AEM customer, download AEM 6.5 from [Adobe Licensing website](http://licensing.adobe.com).

* If you are an Adobe partner, use [Adobe Partner Training Program](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=82357Q) to request AEM 6.5.

AEM をダウンロードしたら、「[デプロイメントと保守](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/deploying/deploy.html#default-local-install)」の説明に従い、AEM オーサーインスタンスの設定を行ってください。

### 最新の AEM サービスパックをダウンロードしてインストールする{#servicepack}

詳細な手順については、

* [AEM 6.5 Service Pack リリースノート](https://docs.adobe.com/content/help/en/experience-manager-65/release-notes/service-pack/sp-release-notes.html)

**最新のAEMパッケージまたはService Packが見つからない場合は、サポート** にお問い合わせください。

## 設定の作成 {#configure-new-integration-65}

Brand PortalでAEM Assetsを設定するには、AEM Assets作成者インスタンスとAdobe開発者コンソールの両方の設定が必要です。

1. AEM Assetsで、IMSアカウントを作成し、公開証明書（公開鍵）を生成します。
1. Adobe 開発者コンソールで、Brand Portal テナント（組織）用のプロジェクトを作成します。
1. そのプロジェクトで、公開鍵で API を設定して、サービスアカウント（JWT）接続を作成します。
1. サービスアカウント資格情報と JWT ペイロード情報を取得します。
1. AEM Assetsで、サービスアカウント資格情報とJWTペイロードを使用してIMSアカウントを設定します。
1. AEM Assetsで、IMSアカウントとBrand Portalエンドポイント（組織URL）を使用してBrand Portalクラウドサービスを設定します。
1. AEM AssetsからBrand Portalにアセットを公開して、設定をテストします。


>[!NOTE]
>
>AEM Assetsの作成者インスタンスは、1つのBrand Portalテナントでのみ構成できます。



ブランドポータルを使用してAEM Assetsを初めて設定する場合は、一覧に示した順序で次の手順を実行します。
1. [公開証明書の取得](#public-certificate)
1. [サービスアカウント（JWT）接続の作成](#createnewintegration)
1. [IMS アカウントの設定](#create-ims-account-configuration)
1. [Cloud Service の設定](#configure-the-cloud-service)
1. [設定のテスト](#test-integration)

### IMS 設定の作成 {#create-ims-configuration}

IMS設定は、Brand PortalテナントでAEM Assets作成者インスタンスを認証します。

IMS 設定には、次の 2 つの手順が含まれます。

* [公開証明書の取得](#public-certificate)
* [IMS アカウントの設定](#create-ims-account-configuration)

### 公開証明書の取得 {#public-certificate}

公開鍵（証明書）は、Adobeデベロッパーコンソールでプロファイルを認証します。

1. AEM Assets オーサーインスタンスにログインします。デフォルトの URL は `http://localhost:4502/aem/start.html` です。

1. **ツール**![ツール](assets/do-not-localize/tools.png)パネルで、**[!UICONTROL セキュリティ]**／**[!UICONTROL Adobe IMS 設定]**&#x200B;に移動します。

1. Adobe IMS 設定ページで、「**[!UICONTROL 作成]**」をクリックします。It will redirect to the **[!UICONTROL Adobe IMS Technical Account Configuration]** page. デフォルトでは、「**証明書**」タブが開きます。

1. 「 **[!UICONTROL Cloud Solution]** 」ドロップダウンリストで「 **[!UICONTROL Adobeブランドポータル]** 」を選択します。

1. 「 **[!UICONTROL 新しい証明書を]** 作成 **」チェックボックスをオンにして、公開鍵の** エイリアスを指定します。 エイリアスは、公開鍵の名前として機能します。

1. 「**[!UICONTROL 証明書を作成]**」をクリックします。Then, click **[!UICONTROL OK]** to generate the public key.

   ![証明書を作成](assets/ims-config2.png)

1. Click the **[!UICONTROL Download Public Key]** icon and save the public key (.crt) file on your machine.

   公開鍵は、後でBrand PortalテナントのAPIを設定し、Adobeデベロッパーコンソールでサービスアカウントの資格情報を生成するために使用されます。

   ![証明書をダウンロード](assets/ims-config3.png)

1. 「**[!UICONTROL 次へ]**」をクリックします。

   「 **アカウント** 」タブで、AdobeIMSアカウントが作成されます。このアカウントには、Adobe開発者コンソールで生成されるサービスアカウント資格情報が必要です。 このページは開いたままにしておきます。

   新しいタブを開き、[Adobe 開発者コンソールでサービスアカウント（JWT）接続を作成](#createnewintegration)して、IMS アカウントを設定するための資格情報と JWT ペイロードを取得します。

### サービスアカウント（JWT）接続の作成 {#createnewintegration}

Adobeデベロッパーコンソールでは、プロジェクトとAPIはBrand Portalテナント（組織）レベルで設定されます。 APIを設定すると、サービスアカウント(JWT)接続が作成されます。 API を設定するには、キーペア（秘密鍵と公開鍵）を生成する方法と、公開鍵をアップロードする方法の 2 とおりがあります。Brand PortalでAEM Assetsを設定するには、AEM Assetsで公開鍵（証明書）を生成し、Adobeデベロッパーコンソールで公開鍵をアップロードして秘密鍵証明書を作成する必要があります。 これらの資格情報は、AEM AssetsでIMSアカウントを設定するために必要です。 IMSアカウントを設定すると、AEM AssetsでBrand Portalクラウドサービスを設定できます。

サービスアカウント資格情報と JWT ペイロードを生成するには、次の手順を実行します。

1. IMS 組織（Brand Portal テナント）のシステム管理者権限で Adobe 開発者コンソールにログインします。デフォルトの URL は次のとおりです。 [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui).


   >[!NOTE]
   >
   >右上隅にあるドロップダウン（組織）リストから正しいIMS組織（Brand Portalテナント）が選択されていることを確認します。

1. 「**[!UICONTROL 新規プロジェクトを作成]**」をクリックします。システムで生成された名前を持つ空のプロジェクトが組織に対して作成されます。

   「**[!UICONTROL プロジェクトを編集]**」をクリックして、「**[!UICONTROL プロジェクトタイトル]**」と「**[!UICONTROL 説明]**」を更新し、「**[!UICONTROL 保存]**」をクリックします。

1. In the **[!UICONTROL Project overview]** tab, click **[!UICONTROL Add API]**.

1. In the **[!UICONTROL Add an API window]**, select **[!UICONTROL AEM Brand Portal]** and click **[!UICONTROL Next]**.

   AEM Brand Portal サービスにアクセスできることを確認します。

1. In the **[!UICONTROL Configure API]** window, click **[!UICONTROL Upload your public key]**. Then, click **[!UICONTROL Select a File]** and upload the public key (.crt file) that you have downloaded in the [obtain public certificate](#public-certificate) section.

   「**[!UICONTROL 次へ]**」をクリックします。

   ![「公開鍵をアップロード」](assets/service-account3.png)

1. Verify the public key and click **[!UICONTROL Next]**.

1. デフォルトの製品プロファイルとして **[!UICONTROL 「Assets Brand Portal]** 」を選択し、「設定済みAPIを **[!UICONTROL 保存]**」をクリックします。

   <!-- 
   In Brand Portal, a default profile is created for each organization. The Product Profiles are created in admin console for assigning users to groups (based on the roles and permissions). For configuration with Brand Portal, the OAuth token is created at organization level. Therefore, you must configure the default Product Profile for your organization. 
   -->

   ![製品プロファイルを選択](assets/service-account4.png)

1. APIが設定されると、APIの概要ページにリダイレクトされます。 From the left navigation under **[!UICONTROL Credentials]**, click on the **[!UICONTROL Service Account (JWT)]** option.

   >[!NOTE]
   >
   >秘密鍵証明書を表示し、JWTトークンの生成、秘密鍵証明書の詳細のコピー、クライアントシークレットの取得などの操作を実行できます。

1. 「**[!UICONTROL クライアント資格情報]**」タブから、**[!UICONTROL クライアント ID]** をコピーします。

   「**[!UICONTROL クライアント秘密鍵を取得]**」をクリックし、**[!UICONTROL クライアントの秘密鍵]**&#x200B;をコピーします。

   ![サービスアカウント資格情報](assets/service-account5.png)

1. Navigate to the **[!UICONTROL Generate JWT]** tab and copy the **[!UICONTROL JWT Payload]** information.

You can now use the client ID (API key), client secret, and JWT payload to [configure the IMS account](#create-ims-account-configuration) in AEM Assets.

<!--
### Create Adobe I/O integration {#createnewintegration}

Adobe I/O integration generates API Key, Client Secret, and Payload (JWT) which is required in setting up the IMS Account configurations.

1. Login to Adobe I/O Console with system administrator privileges on the IMS organization of the Brand Portal tenant.

   Default URL: [https://console.adobe.io/](https://console.adobe.io/) 

1. Click **[!UICONTROL Create Integration]**.

1. Select **[!UICONTROL Access an API]**, and click **[!UICONTROL Continue]**.

   ![Create New Integration](assets/create-new-integration1.png)

1. Create a new integration page opens. 
   
   Select your organization from the drop-down list.

   In **[!UICONTROL Experience Cloud]**, Select **[!UICONTROL AEM Brand Portal]** and click **[!UICONTROL Continue]**. 

   If the Brand Portal option is disabled for you, ensure that you have selected correct organization from the drop-down box above the **[!UICONTROL Adobe Services]** option. If you do not know your organization, contact your administrator.

   ![Create Integration](assets/create-new-integration2.png)

1. Specify a name and description for the integration. Click **[!UICONTROL Select a File from your computer]** and upload the `AEM-Adobe-IMS.crt` file downloaded in the [obtain public certificates](#public-certificate) section.

1. Select the profile of your organization. 

   Or, select the default profile **[!UICONTROL Assets Brand Portal]** and click **[!UICONTROL Create Integration]**. The integration is created.

1. Click **[!UICONTROL Continue to integration details]** to view the integration information. 

   Copy the **[!UICONTROL API Key]** 
   
   Click **[!UICONTROL Retrieve Client Secret]** and copy the Client Secret key.

   ![API Key, Client Secret, and payload information of an integration](assets/create-new-integration3.png)

1. Navigate to **[!UICONTROL JWT]** tab, and copy the **[!UICONTROL JWT payload]**.

   The API Key, Client Secret key, and JWT payload information will be used to create IMS account configuration.
-->

### IMS アカウントの設定 {#create-ims-account-configuration}

次の手順を実行したことを確認します。

* [公開証明書の取得](#public-certificate)
* [サービスアカウント（JWT）接続の作成](#createnewintegration)

次の手順を実行してIMSアカウントを設定します。

1. Open the IMS Configuration and navigate to the **[!UICONTROL Account]** tab. You kept the page open while [obtaining the public certificate](#public-certificate).

1. IMS アカウントの&#x200B;**[!UICONTROL タイトル]**&#x200B;を指定します。

   In the **[!UICONTROL Authorization Server]** field, specify the URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/).

   Specify client ID in the **[!UICONTROL API key]** field, **[!UICONTROL Client Secret]**, and **[!UICONTROL Payload]** (JWT payload) that you have copied while [creating the service account (JWT) connection](#createnewintegration).

   「**[!UICONTROL 作成]**」をクリックします。

   IMS アカウントが設定されます。

   ![IMS アカウントの設定](assets/create-new-integration6.png)


1. その IMS アカウント設定を選択し、「**[!UICONTROL ヘルスチェック]**」をクリックします。

   ダイアログボックスの「**[!UICONTROL チェック]**」をクリックします。正常に設定されると、*トークンが正常に取得されました*&#x200B;というメッセージが表示されます。

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>IMS 設定は 1 つだけにする必要があります。
>
>IMS 設定がヘルスチェックに合格していることを確認します。設定がヘルスチェックに合格しない場合は無効です。削除して、新しい有効な設定を作成する必要があります。



### Cloud Service の設定{#configure-the-cloud-service}

Brand Portal Cloud Service を設定するには、次の手順を実行します。

1. AEM Assets オーサーインスタンスにログインします。

1. **ツール**&#x200B;の![ツール](assets/do-not-localize/tools.png)パネルで、**[!UICONTROL Cloud Services]**／**[!UICONTROL AEM Brand Portal]** に移動します。

1. Brand Portal の設定ページで、「**[!UICONTROL 作成]**」をクリックします。

1. 設定の&#x200B;**[!UICONTROL タイトル]**&#x200B;を入力します。

   [IMS アカウントの設定](#create-ims-account-configuration)時に作成した IMS 設定を選択します。

   In the **[!UICONTROL Service URL]** field, specify your Brand Portal tenant (organization) URL.

   ![](assets/create-cloud-service.png)

1. 「**[!UICONTROL 保存して閉じる]**」をクリックします。クラウド設定が作成されます。

   これで、AEM Assets作成者インスタンスがBrand Portalテナントと共に設定されました。

### 設定のテスト{#test-integration}

設定を検証するには、次の手順を実行します。

1. AEM Assets クラウドインスタンスにログインします。

1. From the **Tools** ![Tools](assets/do-not-localize/tools.png) panel, navigate to **[!UICONTROL Deployment]** > **[!UICONTROL Replication]**.

   ![](assets/test-integration1.png)

1. レプリケーションページで、「**[!UICONTROL 作成者のエージェント]**」をクリックします。

   ![](assets/test-integration2.png)

   Brand Portalテナント用に作成された4つのレプリケーションエージェントが表示されます。

   Brand Portalテナントのレプリケーションエージェントを探し、レプリケーションエージェントURLをクリックします。

   ![](assets/test-integration3.png)


   >[!NOTE]
   >
   >レプリケーションエージェントは並行して動作し、ジョブの分散を均等に共有するので、パブリッシング速度を元の速度の4倍に増やします。 クラウドサービスの設定後、複数のアセットの並列発行を有効にするために、デフォルトでアクティブ化される複製エージェントを有効にするために、追加の設定は必要ありません。


1. To verify the connection between AEM Assets and Brand Portal, click on the **[!UICONTROL Test Connection]** icon.

   ![](assets/test-integration4.png)

   テ *ストパッケージが正常に配信されたことを示すメッセージが表示されます*。

   ![](assets/test-integration5.png)

1. 4つのレプリケーションエージェントすべてでテスト結果を確認します。


   >[!NOTE]
   >
   >アセットの複製（実行中のキュー）が失敗する原因となる可能性があるので、複製エージェントを無効にしないでください。
   >
   >タイムアウトエラーを回避するために、4つのレプリケーションエージェントがすべて構成されていることを確認します。 See [troubleshoot issues in parallel publishing to Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/troubleshoot-parallel-publishing.html#connection-timeout).

次の操作が可能になりました。

* [AEM Assets から Brand Portal へのアセットの公開](../assets/brand-portal-publish-assets.md)
* [Brand PortalからAEM Assets](https://docs.adobe.com/content/help/ja-JP/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html) - Brand Portalでアセットを発行
* [AEM Assets から Brand Portal へのフォルダーの公開](../assets/brand-portal-publish-folder.md)
* [AEM Assets から Brand Portal へのコレクションの公開](../assets/brand-portal-publish-collection.md)
* [Brand Portal へのプリセット、スキーマ、ファセットの公開](https://docs.adobe.com/content/help/ja-JP/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [Brand Portal へのタグの公開](https://docs.adobe.com/content/help/ja-JP/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)

See [Brand Portal documentation](https://docs.adobe.com/content/help/ja-JP/experience-manager-brand-portal/using/home.html) for more information.


## 設定のアップグレード {#upgrade-integration-65}

既存の設定をAdobe開発者コンソールにアップグレードするには、一覧に示した手順に従って次の手順を実行します。
1. [実行中のジョブの確認](#verify-jobs)
1. [既存の設定の削除](#delete-existing-configuration)
1. [設定の作成](#configure-new-integration-65)

### 実行中のジョブの確認 {#verify-jobs}

変更を行う前に、AEM Assetsの作成者インスタンスで発行ジョブが実行されていないことを確認してください。 その場合は、4つのレプリケーションエージェントすべてでアクティブなジョブの状態を確認し、キューがアイドル状態であることを確認できます。

1. AEM Assets オーサーインスタンスにログインします。

1. From the **Tools** ![Tools](assets/do-not-localize/tools.png) panel, navigate to **[!UICONTROL Deployment]** > **[!UICONTROL Deployment Replication]**.

1. レプリケーションページで、「**[!UICONTROL 作成者のエージェント]**」をクリックします。

   ![](assets/test-integration2.png)

1. Brand Portalテナントのレプリケーションエージェントを見つけます。

   すべてのレプリケーションエージェントで **キューがアイドル状態であることを確認します** 。公開ジョブがアクティブでないことを確認します。

   ![](assets/test-integration3.png)

### 既存の設定の削除 {#delete-existing-configuration}

既存の設定の削除時に、次のチェックリストを実行する必要があります。
* 4つのレプリケーションエージェントをすべて削除する
* Brand Portalクラウドサービスの削除
* MACユーザーの削除

1. AEM Assets作成者インスタンスにログインし、管理者としてCRX Liteを開きます。 デフォルトの URL は `http://localhost:4502/crx/de/index.jsp` です。

1. Brand Portalテナントの4つのレプリケーションエージェントすべてに移動 `/etc/replications/agents.author` して削除します。

   ![](assets/delete-replication-agent.png)

1. Brand Portalクラウドサービスの設定に移動 `/etc/cloudservices/mediaportal` して削除します。

   ![](assets/delete-cloud-service.png)

1. Brand Portalテナントの `/home/users/mac` MACユーザ **** に移動して削除します。

   ![](assets/delete-mac-user.png)


AEM 6.5作成者インスタンスのAdobe開発者コンソールを使用して [、設定を](#configure-new-integration-65) 作成できるようになりました。



<!--
   Comment Type: draft

   <li> </li>
   -->

<!--
   Comment Type: draft

   <li>Step text</li>
   -->


