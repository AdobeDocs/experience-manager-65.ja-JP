---
title: AEM Assets と Brand Portal の連携の設定
seo-title: AEM Assets と Brand Portal の連携の設定
description: Brand PortalでAEM Assetsを設定して、アセットとコレクションをBrand Portalに公開する方法を説明します。
seo-description: Brand PortalでAEM Assetsを設定して、アセットとコレクションをBrand Portalに公開する方法を説明します。
uuid: b95c046e-9988-444c-b50e-ff5ec8cafe14
topic-tags: brand-portal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: dca5a2ac-1fc8-4251-b073-730fd6f49b1c
docset: aem65
translation-type: tm+mt
source-git-commit: 91caca39b0b6c5c0c98b58be02f518901a3d90e3
workflow-type: tm+mt
source-wordcount: '2045'
ht-degree: 60%

---


# AEM Assets と Brand Portal の連携の設定 {#configure-integration-65}

Adobe Experience Manager（AEM）Assets と Brand Portal の統合は、Adobe 開発者コンソールを通じて設定されます。開発者コンソールは Brand Portal テナントの認証用の IMS トークンを取得します。

>[!NOTE]
>
>Adobe Developer Consoleを使用したBrand PortalでのAEM Assetsの設定は、AEM 6.5.4.0以降でサポートされています。
>
>これまで、Brand Portal は、旧来の OAuth ゲートウェイを通じてクラシック UI で設定されていました。このゲートウェイは、JWT トークン交換を使用して認証用の IMS アクセストークンを取得します。
>
>旧来の OAuth を使用した設定は、2020 年 4 月 6 日以降はサポートされなくなり、Adobe 開発者コンソールを使用した設定に変更されました。


>[!TIP]
>
>***既存のお客様のみ***
>
>既存のレガシー OAuth Gateway 設定を引き続き使用することをお勧めします。レガシーOAuth Gateway設定で問題が発生した場合は、既存の設定を削除し、Adobe Developer Consoleを使用して新しい設定を作成します。



このヘルプでは、次の2つの使用例について説明します。
* [新しい設定](#configure-new-integration-65): 新しいBrand Portalユーザーで、AEM Assets作成者インスタンスをBrand Portalで設定する場合は、Adobe Developer Consoleで新しい設定を作成できます。
* [アップグレード設定](#upgrade-integration-65): 既存のBrand Portalユーザーで、既存のBrand PortalユーザーインスタンスをレガシーOAuth GatewayのBrand Portalで設定した場合は、既存の設定を削除し、Adobe Developer Consoleで新しい設定を作成することをお勧めします。

具体的には、以下の操作に関する十分な知識があるユーザーを対象としています。

* Adobe Experience ManagerおよびAEMパッケージのインストール、設定、管理を行います。

* LinuxおよびMicrosoft Windowsオペレーティングシステムの使用

## 前提条件 {#prerequisites}

AEM Assets と Brand Portal の連携を設定するには以下が必要です。

* 最新のサービスパックを適用した実行中の AEM Assets オーサーインスタンス
* Brand Portal テナント URL
* Brand Portal テナントの IMS 組織に対するシステム管理者権限を持つユーザー


[AEM 6.5のダウンロードとインストール](#aemquickstart)

[最新の AEM サービスパックをダウンロードしてインストールする](#servicepack)

### Download and install AEM 6.5 {#aemquickstart}

AEMオーサーインスタンスを設定するには、AEM 6.5を使用することをお勧めします。 AEM が稼働していない場合は、以下の場所から AEM をダウンロードしてください。

* If you are an existing AEM customer, download AEM 6.5 from [Adobe Licensing website](http://licensing.adobe.com).

* If you are an Adobe partner, use [Adobe Partner Training Program](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=82357Q) to request AEM 6.5.

AEM をダウンロードしたら、「[デプロイメントと保守](https://helpx.adobe.com/jp/experience-manager/6-5/sites/deploying/using/deploy.html#defaultlocalinstall)」の説明に従い、AEM オーサーインスタンスの設定を行ってください。

### 最新の AEM サービスパックをダウンロードしてインストールする{#servicepack}

詳細な手順については、

* [AEM 6.5 Service Pack リリースノート](https://helpx.adobe.com/jp/experience-manager/6-5/release-notes/sp-release-notes.html)

**最新のAEMパッケージまたはService Packが見つからない場合は、カスタマーケアにお問い合わせください** 。

## 設定の作成 {#configure-new-integration-65}

Brand PortalでAEM Assetsを設定するには、AEM Assets作成者インスタンスとAdobe Developer Consoleの両方の設定が必要です。

1. AEM Assets作成者インスタンスで、IMSアカウントを作成し、公開証明書（公開鍵）を生成します。

1. Adobe 開発者コンソールで、Brand Portal テナント（組織）用のプロジェクトを作成します。

1. そのプロジェクトで、公開鍵で API を設定して、サービスアカウント（JWT）接続を作成します。

1. サービスアカウント資格情報と JWT ペイロード情報を取得します。

1. AEM Assets作成者インスタンスで、サービスアカウントの資格情報とJWTペイロードを使用してIMSアカウントを設定します。

1. AEM Assets作成者インスタンスで、IMSアカウントとブランドポータルエンドポイント（組織URL）を使用してBrand Portalクラウドサービスを設定します。

1. AEM Assets作成者インスタンスからBrand Portalにアセットを発行して、設定をテストします。


>[!NOTE]
>
>Brand Portalテナントは、1つのAEM Assets作成者インスタンスでのみ構成できます。
>
>複数のAEM Assets作成者インスタンスを持つBrand Portalテナントを構成しないでください。



Brand PortalとのAEM Assetsを初めて設定する場合は、一覧に示した順序で次の手順を実行します。
1. [公開証明書の取得](#public-certificate)
1. [サービスアカウント（JWT）接続の作成](#createnewintegration)
1. [IMS アカウントの設定](#create-ims-account-configuration)
1. [Cloud Service の設定](#configure-the-cloud-service)
1. [設定のテスト](#test-integration)

### IMS 設定の作成 {#create-ims-configuration}

IMS 設定は、AEM Assets オーサーインスタンスを使用して Brand Portal テナントを認証します。

IMS 設定には、次の 2 つの手順が含まれます。

* [公開証明書の取得](#public-certificate)
* [IMS アカウントの設定](#create-ims-account-configuration)

### 公開証明書の取得 {#public-certificate}

公開証明書により、Adobe 開発者コンソールでプロファイルを認証できます。

1. AEM Assets オーサーインスタンスにログインします。デフォルトの URL は次のとおりです。
   `http:// localhost:4502/aem/start.html`
1. **ツール**![ツール](assets/do-not-localize/tools.png)パネルで、**[!UICONTROL セキュリティ]**／**[!UICONTROL Adobe IMS 設定]**&#x200B;に移動します。

   ![Adobe IMS アカウント設定 UI](assets/ims-config1.png)

1. Adobe IMS 設定ページで、「**[!UICONTROL 作成]**」をクリックします。

1. **[!UICONTROL Adobe IMS テクニカルアカウント設定]**&#x200B;ページにリダイレクトされます。デフォルトでは、「**証明書**」タブが開きます。

   **[!UICONTROL Adobe Brand Portal]** クラウドソリューションを選択します。

1. Mark the checkbox **[!UICONTROL Create new certificate]** and specify an **alias** for the certificate. ここで入力したエイリアスが、ダイアログ名として表示されます。

1. 「**[!UICONTROL 証明書を作成]**」をクリックします。次に、ダイアログボックスで「**[!UICONTROL OK]**」をクリックして、公開証明書を生成します。

   ![証明書を作成](assets/ims-config2.png)

1. 「**[!UICONTROL 公開鍵をダウンロード]**」をクリックし、証明書（.crt）ファイルをローカルマシンに保存します。

   この証明書ファイルを後の手順で使用して、Brand Portal テナントの API を設定し、Adobe 開発者コンソールでサービスアカウント資格情報を生成します。

   ![証明書をダウンロード](assets/ims-config3.png)

1. 「**[!UICONTROL 次へ]**」をクリックします。

   「**アカウント**」タブで Adobe IMS アカウントを作成しますが、そのために、Adobe 開発者コンソールで生成されるサービスアカウント資格情報が必要になります。このページは開いたままにしておきます。

   新しいタブを開き、[Adobe 開発者コンソールでサービスアカウント（JWT）接続を作成](#createnewintegration)して、IMS アカウントを設定するための資格情報と JWT ペイロードを取得します。

### サービスアカウント（JWT）接続の作成 {#createnewintegration}

Adobe 開発者コンソールで、プロジェクトと API を組織（Brand Portal テナント）レベルで設定します。Adobe 開発者コンソールで API を設定すると、サービスアカウント（JWT）接続が作成されます。API を設定するには、キーペア（秘密鍵と公開鍵）を生成する方法と、公開鍵をアップロードする方法の 2 とおりがあります。Brand PortalでAEM Assets作成者インスタンスを設定するには、AEM Assets作成者インスタンスで公開証明書（公開鍵）を生成し、Adobe Developer Consoleで公開鍵をアップロードして秘密鍵証明書を作成する必要があります。 この公開鍵は、選択した Brand Portal 組織の API を設定するために使用され、サービスアカウントの資格情報と JWT ペイロードが生成されます。これらの資格情報は、AEM Assetsの作成者インスタンスでIMSアカウントを設定するためにさらに使用されます。 IMSアカウントが設定されたら、AEM Assets作成者インスタンスでBrand Portalクラウドサービスを設定できます。

サービスアカウント資格情報と JWT ペイロードを生成するには、次の手順を実行します。

1. IMS 組織（Brand Portal テナント）のシステム管理者権限で Adobe 開発者コンソールにログインします。デフォルトの URL は次のとおりです。

   [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui)


   >[!NOTE]
   >
   >右上隅にあるドロップダウン（組織リスト）から正しい IMS 組織（Brand Portal テナント）が選択されていることを確認します。

1. 「**[!UICONTROL 新規プロジェクトを作成]**」をクリックします。組織の空のプロジェクトが作成されます。

   「**[!UICONTROL プロジェクトを編集]**」をクリックして、「**[!UICONTROL プロジェクトタイトル]**」と「**[!UICONTROL 説明]**」を更新し、「**[!UICONTROL 保存]**」をクリックします。

   ![プロジェクトを作成](assets/service-account1.png)

1. 「プロジェクトの概要」タブで、「**[!UICONTROL API を追加]**」をクリックします。

   ![API を追加](assets/service-account2.png)

1. API を追加ウィンドウで、「**[!UICONTROL AEM Brand Portal]**」を選択し、「**[!UICONTROL 次へ]**」をクリックします。

   AEM Brand Portal サービスにアクセスできることを確認します。

1. API を設定ウィンドウで、「**[!UICONTROL 公開鍵をアップロード]**」をクリックします。次に、「**[!UICONTROL ファイルを選択]**」をクリックし、[公開証明書の取得](#public-certificate)節でダウンロードした公開証明書（.crt ファイル）をアップロードします。

   「**[!UICONTROL 次へ]**」をクリックします。

   ![「公開鍵をアップロード」](assets/service-account3.png)

1. 公開証明書を確認し、「**[!UICONTROL 次へ]**」をクリックします。

1. デフォルトの製品プロファイル「**[!UICONTROL Assets Brand Portal]**」を選択し、「**[!UICONTROL 設定を保存]**」をクリックします。

   ![製品プロファイルを選択](assets/service-account4.png)

1. API が設定されている場合は、API の概要にリダイレクトされます。左側のナビゲーションツリーで「**[!UICONTROL 資格情報]**」の下の「**[!UICONTROL サービスアカウント（JWT）]**」をクリックします。

   >[!NOTE]
   >
   >資格情報を確認し、必要に応じて、その他のアクション（JWT トークンの生成、資格情報の詳細のコピー、クライアントの秘密鍵の取得など）を実行できます。

1. 「**[!UICONTROL クライアント資格情報]**」タブから、**[!UICONTROL クライアント ID]** をコピーします。

   「**[!UICONTROL クライアント秘密鍵を取得]**」をクリックし、**[!UICONTROL クライアントの秘密鍵]**&#x200B;をコピーします。

   ![サービスアカウント資格情報](assets/service-account5.png)

1. 「**[!UICONTROL JWT を生成]**」タブに移動し、**[!UICONTROL JWT ペイロード]**&#x200B;をコピーします。

これで、クライアント ID（API キー）、クライアントの秘密鍵、JWT ペイロードを使用して、AEM Assets クラウドインスタンスに [IMS アカウントを設定](#create-ims-account-configuration)できるようになりました。

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

### IMS アカウント設定の作成 {#create-ims-account-configuration}

次の手順を実行したことを確認します。

* [公開証明書の取得](#public-certificate)
* [サービスアカウント（JWT）接続の作成](#createnewintegration)

[公開証明書の取得](#public-certificate)で作成した IMS アカウントを設定するには、次の手順を実行します。

1. IMS 設定を開き、「**[!UICONTROL アカウント]**」タブに移動します。You kept the page open while [obtaining public certificate](#public-certificate).

1. IMS アカウントの&#x200B;**[!UICONTROL タイトル]**&#x200B;を指定します。

   「**[!UICONTROL 認証サーバー]**」に次の URL を入力します。[https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)

   [サービスアカウント（JWT）接続の作成](#createnewintegration)時にコピーした API キー、クライアントの秘密鍵、JWT ペイロードにクライアント ID を貼り付けます。

   「**[!UICONTROL 作成]**」をクリックします。

   IMS アカウントが設定されます。

   ![IMS アカウントの設定](assets/create-new-integration6.png)


1. 作成した IMS 設定を選択して「**[!UICONTROL ヘルスチェック]**」をクリックします。

   ダイアログボックスの「**[!UICONTROL チェック]**」をクリックします。正常に設定されると、*トークンが正常に取得されました*&#x200B;というメッセージが表示されます。

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>IMS 設定は 1 つだけにする必要があります。複数の IMS 設定を作成しないでください。
>
>IMS 設定がヘルスチェックに合格していることを確認します。設定がヘルスチェックに合格しない場合は無効です。削除して、新しい有効な設定を作成する必要があります。



### Cloud Service の設定{#configure-the-cloud-service}

次の手順を実行して、ブランドポータルクラウドサービスを作成します。

1. AEM Assets オーサーインスタンスにログインします。

1. **ツール**&#x200B;の![ツール](assets/do-not-localize/tools.png)パネルで、**[!UICONTROL Cloud Services]**／**[!UICONTROL AEM Brand Portal]** に移動します。

1. Brand Portal の設定ページで、「**[!UICONTROL 作成]**」をクリックします。

1. 設定の&#x200B;**[!UICONTROL タイトル]**&#x200B;を入力します。

   [IMS アカウントの設定](#create-ims-account-configuration)時に作成した IMS 設定を選択します。

   In the **[!UICONTROL Service URL]**, enter your Brand Portal tenant (organization) URL.

   ![](assets/create-cloud-service.png)

1. 「**[!UICONTROL 保存して閉じる]**」をクリックします。クラウド設定が作成されます。これで、AEM Assets作成者インスタンスがBrand Portalテナントと共に設定されました。

### 設定のテスト{#test-integration}

設定を検証するには、次の手順を実行します。

1. AEM Assets クラウドインスタンスにログインします。

1. From the **Tools** ![Tools](assets/do-not-localize/tools.png) panel, navigate to **[!UICONTROL Deployment]** > **[!UICONTROL Replication]**.

   ![](assets/test-integration1.png)

1. レプリケーションページで、「**[!UICONTROL 作成者のエージェント]**」をクリックします。

   ![](assets/test-integration2.png)

1. 各テナントに4つのレプリケーションエージェントが作成されます。

   Brand Portalテナントのレプリケーションエージェントを見つけます。

   複製エージェントのURLをクリックします。

   ![](assets/test-integration3.png)


   >[!NOTE]
   >
   >レプリケーションエージェントは並行して動作し、ジョブの分散を均等に共有するので、パブリッシング速度を元の速度の4倍に増やします。 クラウドサービスの設定後、複数のアセットの並列発行を有効にするために、デフォルトでアクティブ化される複製エージェントを有効にするために、追加の設定は必要ありません。


1. AEM Assets と Brand Portal の間の接続を検証するには、「**[!UICONTROL 接続をテスト]**」をクリックします。

   ![](assets/test-integration4.png)

   テストパッケージが正常に配信されたことを示すメッセージがページの下部に表示されます。

   ![](assets/test-integration5.png)

1. 4つのレプリケーションエージェントすべてに対するテスト結果を1つずつ確認します。


   >[!NOTE]
   >
   >レプリケーションエージェントを無効にしないでください。 これにより、一部のアセットの複製が失敗する場合があります。

AEM Assets作成者インスタンスがBrand Portalで正しく設定され、次の操作が可能になります。

* [AEM Assets から Brand Portal へのアセットの公開](../assets/brand-portal-publish-assets.md)
* [AEM Assets から Brand Portal へのフォルダーの公開](../assets/brand-portal-publish-folder.md)
* [AEM Assets から Brand Portal へのコレクションの公開](../assets/brand-portal-publish-collection.md)
* [Asset Sourcingを設定し](https://docs.adobe.com/content/help/ja-JP/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html) 、Brand Portalユーザがアセットを投稿してAEM Assetsに公開できるようにします。

## 設定のアップグレード {#upgrade-integration-65}

既存の設定をアップグレードするには、次の手順を一覧に示す順序で実行します。
1. [実行中のジョブの確認](#verify-jobs)
1. [既存の設定の削除](#delete-existing-configuration)
1. [設定の作成](#configure-new-integration-65)

### 実行中のジョブの確認 {#verify-jobs}

変更を行う前に、AEM Assetsの作成者インスタンスで公開ジョブが実行されていないことを確認してください。 その場合は、4つのレプリケーションエージェントをすべて検証し、キューが空であることを確認できます。

1. AEM Assets オーサーインスタンスにログインします。

1. From the **Tools** ![Tools](assets/do-not-localize/tools.png) panel, navigate to **[!UICONTROL Deployment]** > **[!UICONTROL Deployment Replication]**.

1. レプリケーションページで、「**[!UICONTROL 作成者のエージェント]**」をクリックします。

   ![](assets/test-integration2.png)

1. Brand Portalテナントのレプリケーションエージェントを見つけます。

   すべてのレプリケーションエージェントで **キューがアイドル状態であることを確認します** 。公開ジョブがアクティブでないことを確認します。

   ![](assets/test-integration3.png)

### 既存の設定の削除 {#delete-existing-configuration}

既存の設定の削除中に、次のチェックリストを実行する必要があります。
* 4つのレプリケーションエージェントをすべて削除する
* クラウドサービスの削除
* MACユーザーの削除

1. AEM Assetsの作成者インスタンスにログインし、管理者としてCRX Liteを開きます。 デフォルトの URL は次のとおりです。

   `http:// localhost:4502/crx/de/index.jsp`

1. Brand Portalテナントの4つのレプリケーションエージェントすべてに移動 `/etc/replications/agents.author` して削除します。

   ![](assets/delete-replication-agent.png)

1. `/etc/cloudservices/mediaportal` Cloud Service設定に移動し **て削除します**。

   ![](assets/delete-cloud-service.png)

1. Brand Portalテナントの `/home/users/mac` MACユーザ **** に移動して削除します。

   ![](assets/delete-mac-user.png)


AEM 6.5オーサーインスタンスのAdobe Developer [Consoleを使用して設定を](#configure-new-integration-65) 作成できるようになりました。



<!--
   Comment Type: draft

   <li> </li>
   -->

<!--
   Comment Type: draft

   <li>Step text</li>
   -->


