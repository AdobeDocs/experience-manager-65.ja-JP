---
title: AEM Assets と Brand Portal の連携の設定
seo-title: Configure AEM Assets with Brand Portal
description: AEM AssetsとBrand Portalを連携させて、アセットとコレクションをBrand Portalに公開する方法を説明します。
seo-description: Learn how to configure AEM Assets with Brand Portal for publishing assets and Collections to Brand Portal.
uuid: b95c046e-9988-444c-b50e-ff5ec8cafe14
topic-tags: brand-portal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: dca5a2ac-1fc8-4251-b073-730fd6f49b1c
docset: aem65
feature: Brand Portal
role: Admin
exl-id: ae33181c-9eec-421c-be55-4bd019de40b8
source-git-commit: d995173140237f34a03c8e84128ad9d657c9a026
workflow-type: tm+mt
source-wordcount: '2053'
ht-degree: 62%

---

# AEM Assets と Brand Portal の連携の設定 {#configure-integration-65}

Adobe Experience Manager Assets Brand Portalでは、承認済みブランドアセットをAdobe Experience Manager AssetsからBrand Portalに公開し、Brand Portalユーザーに配布できます。

AEM Assets  と Brand Portal の連携は、Adobe 開発者コンソールを通じて設定されます。このコンソールでは、Brand Portal テナントの認証に使用する Adobe Identity Management サービス（IMS）アカウントトークンを調達します。

>[!NOTE]
>
>Adobe開発者コンソールを使用したBrand PortalとのAEM Assetsの設定は、AEM 6.5.4.0以降でサポートされています。
>
>以前は、Brand Portalは、旧来のOAuth Gatewayを介して設定されていました。このゲートウェイは、JSON Webトークン(JWT)交換を使用して認証用のIMSアクセストークンを取得します。
>
>旧来のOAuth Gatewayを使用した設定は、2020年4月6日以降はサポートされなくなり、Adobe開発者コンソールに変更されました。

>[!TIP]
>
>***既存のお客様のみ***
>
>既存のレガシーOAuth Gateway設定を引き続き使用することをお勧めします。 レガシーOAuth Gateway設定で問題が発生した場合は、Adobe開発者コンソールで既存の設定を削除し、新しい設定を作成します。

このヘルプでは、次の2つの使用例について説明します。

* [新しい設定](#configure-new-integration-65):新しいBrand Portalユーザーで、AEM AssetsオーサーインスタンスをBrand Portalで設定する場合は、Adobe開発者コンソールで設定を作成できます。
* [設定のアップグレード](#upgrade-integration-65):既存のBrand PortalユーザーがレガシーOAuth Gatewayを使用して設定している場合は、Adobe開発者コンソールで既存の設定を削除し、新しい設定を作成します。

具体的には、以下の操作に関する十分な知識があるユーザーを対象としています。

* Adobe Experience ManagerおよびAEMパッケージのインストール、設定および管理。

* LinuxおよびMicrosoft Windowsオペレーティングシステムの使用。

## 前提条件 {#prerequisites}

AEM Assets と Brand Portal の連携を設定するには以下が必要です。

* 最新のサービスパックを備えたAEM Assetsオーサーインスタンスの起動および実行
* Brand Portal テナント URL
* Brand Portal テナントの IMS 組織に対するシステム管理者権限を持つユーザー

[AEM 6.5をダウンロードしてインストールする](#aemquickstart)

[最新の AEM サービスパックをダウンロードしてインストールする](#servicepack)

### AEM 6.5をダウンロードしてインストールする {#aemquickstart}

AEMオーサーインスタンスを設定するには、AEM 6.5を使用することをお勧めします。 AEM が稼働していない場合は、以下の場所から AEM をダウンロードしてください。

* 既にAEMをご利用の場合は、[AdobeライセンスWebサイト](http://licensing.adobe.com)からAEM 6.5をダウンロードしてください。

* Adobeパートナーの場合は、[Adobeパートナートレーニングプログラム](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=82357Q)を使用してAEM 6.5をリクエストします。

AEM をダウンロードしたら、「[デプロイメントと保守](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html#default-local-install)」の説明に従い、AEM オーサーインスタンスの設定を行ってください。

### 最新の AEM サービスパックをダウンロードしてインストールする {#servicepack}

詳しい手順については、

* [AEM 6.5 Service Pack リリースノート](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/service-pack/sp-release-notes.html?lang=ja)

**最新の** AEMパッケージまたはService Packが見つからない場合は、サポートにお問い合わせください。

## 設定の作成 {#configure-new-integration-65}

Brand PortalでAEM Assetsを設定するには、AEM AssetsオーサーインスタンスとAdobe開発者コンソールの両方の設定が必要です。

1. AEM Assetsで、IMSアカウントを作成し、公開証明書（公開鍵）を生成します。
1. Adobe 開発者コンソールで、Brand Portal テナント（組織）用のプロジェクトを作成します。
1. そのプロジェクトで、公開鍵で API を設定して、サービスアカウント（JWT）接続を作成します。
1. サービスアカウント資格情報と JWT ペイロード情報を取得します。
1. AEM Assets で、サービスアカウント資格情報と JWT ペイロードを使用して IMS アカウントを設定します。
1. AEM Assets で、IMS アカウントと Brand Portal エンドポイント（組織 URL）を使用して Brand Portal Cloud Service を設定します。
1. AEM Assets から Brand Portal にアセットを公開して、設定をテストします。

>[!NOTE]
>
>AEM Assetsオーサーインスタンスは、1つのBrand Portalテナントでのみ設定できます。

AEM AssetsとBrand Portalを初めて設定する場合は、以下の手順を順に実行します。
1. [公開証明書の取得](#public-certificate)
1. [サービスアカウント（JWT）接続の作成](#createnewintegration)
1. [IMS アカウントの設定](#create-ims-account-configuration)
1. [Cloud Service の設定](#configure-the-cloud-service)
1. [設定のテスト](#test-integration)

### IMS 設定の作成 {#create-ims-configuration}

IMS設定は、Brand PortalテナントでAEM Assetsオーサーインスタンスを認証します。

IMS 設定には、次の 2 つの手順が含まれます。

* [公開証明書の取得](#public-certificate)
* [IMS アカウントの設定](#create-ims-account-configuration)

### 公開証明書の取得 {#public-certificate}

公開鍵（証明書）は、Adobe 開発者コンソールでプロファイルを認証します。

1. AEM Assets オーサーインスタンスにログインします。デフォルトの URL は `http://localhost:4502/aem/start.html` です。

1. **ツール**![ツール](assets/do-not-localize/tools.png)パネルで、**[!UICONTROL セキュリティ]**／**[!UICONTROL Adobe IMS 設定]**&#x200B;に移動します。

1. Adobe IMS 設定ページで、「**[!UICONTROL 作成]**」をクリックします。**[!UICONTROL Adobe IMS 技術アカウント設定]**&#x200B;ページにリダイレクトされます。デフォルトでは、「**証明書**」タブが開きます。

1. 「**[!UICONTROL クラウドソリューション]**」ドロップダウンリストで「**[!UICONTROL Adobe Brand Portal]**」を選択します。

1. 「**[!UICONTROL 新しい証明書を作成]**」チェックボックスをオンにして、公開鍵の&#x200B;**エイリアス**&#x200B;を指定します。ここで入力したエイリアスが、公開鍵になります。

1. 「**[!UICONTROL 証明書を作成]**」をクリックします。「**[!UICONTROL OK]**」をクリックして公開証明書を生成します。

   ![証明書を作成](assets/ims-config2.png)

1. **[!UICONTROL 公開鍵をダウンロード]**&#x200B;アイコンをクリックして、公開鍵（.crt）ファイルをローカルマシンに保存します。

   この公開鍵を後で使用して、Brand Portal テナントの API を設定し、Adobe 開発者コンソールでサービスアカウント資格情報を生成します。

   ![証明書をダウンロード](assets/ims-config3.png)

1. 「**[!UICONTROL 次へ]**」をクリックします。

   「**アカウント**」タブで、Adobe IMS アカウントが作成されます。このアカウントには、Adobe 開発者コンソールで生成されるサービスアカウント資格情報が必要です。このページは開いたままにしておきます。

   新しいタブを開き、[Adobe 開発者コンソールでサービスアカウント（JWT）接続を作成](#createnewintegration)して、IMS アカウントを設定するための資格情報と JWT ペイロードを取得します。

### サービスアカウント（JWT）接続の作成 {#createnewintegration}

Adobe 開発者コンソールで、プロジェクトと API を Brand Portal テナント（組織）レベルで設定します。API を設定すると、サービスアカウント（JWT）接続が作成されます。API を設定するには、キーペア（秘密鍵と公開鍵）を生成する方法と、公開鍵をアップロードする方法の 2 とおりがあります。AEM Assets と Brand Portal の統合を設定するには、AEM Assets で公開鍵（証明書）を生成し、その公開鍵をアップロードして Adobe 開発者コンソールで資格情報を作成する必要があります。これらの資格情報は、AEM Assets で IMS アカウントを設定するために必要です。IMS アカウントを設定したら、AEM Assets に Brand Portal Cloud Service を設定できます。

サービスアカウント資格情報と JWT ペイロードを生成するには、次の手順を実行します。

1. IMS 組織（Brand Portal テナント）のシステム管理者権限で Adobe 開発者コンソールにログインします。デフォルトの URL は [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui) です。


   >[!NOTE]
   >
   >右上隅にあるドロップダウン（組織）リストから正しい IMS 組織（Brand Portal テナント）が選択されていることを確認します。

1. 「**[!UICONTROL 新規プロジェクトを作成]**」をクリックします。システムで生成された名前を持つ空のプロジェクトが組織に対して作成されます。

   「**[!UICONTROL プロジェクトを編集]**」をクリックして、「**[!UICONTROL プロジェクトタイトル]**」と「**[!UICONTROL 説明]**」をアップデートし、「**[!UICONTROL 保存]**」をクリックします。

1. 「**[!UICONTROL プロジェクトの概要]**」タブで、「**[!UICONTROL API を追加]**」をクリックします。

1. **[!UICONTROL API を追加]**&#x200B;ウィンドウで、「**[!UICONTROL AEM Brand Portal]**」を選択し、「**[!UICONTROL 次へ]**」をクリックします。

   AEM Brand Portal サービスにアクセスできることを確認します。

1. **[!UICONTROL API を設定]**&#x200B;ウィンドウで、「**[!UICONTROL 公開鍵をアップロード]**」をクリックします。次に、「**[!UICONTROL ファイルを選択]**」をクリックし、[公開証明書の取得](#public-certificate)のセクションでダウンロードした公開鍵（.crt ファイル）をアップロードします。

   「**[!UICONTROL 次へ]**」をクリックします。

   ![「公開鍵をアップロード」](assets/service-account3.png)

1. 公開鍵を確認し、「**[!UICONTROL 次へ]**」をクリックします。

1. デフォルトの製品プロファイルとして「**[!UICONTROL Assets Brand Portal]**」を選択し、「**[!UICONTROL 設定済み API を保存]**」をクリックします。

   <!-- 
   In Brand Portal, a default profile is created for each organization. The Product Profiles are created in admin console for assigning users to groups (based on the roles and permissions). For configuration with Brand Portal, the OAuth token is created at organization level. Therefore, you must configure the default Product Profile for your organization. 
   -->

   ![製品プロファイルを選択](assets/service-account4.png)

1. API が設定されると、API の概要ページにリダイレクトされます。左側のナビゲーションツリーで「**[!UICONTROL 資格情報]**」の下の「**[!UICONTROL サービスアカウント（JWT）]**」オプションをクリックします。

   >[!NOTE]
   >
   >資格情報を確認し、必要に応じて、JWT トークンの生成、資格情報の詳細のコピー、クライアントの秘密鍵の取得などのアクションを実行できます。

1. 「**[!UICONTROL クライアント資格情報]**」タブから、**[!UICONTROL クライアント ID]** をコピーします。

   「**[!UICONTROL クライアント秘密鍵を取得]**」をクリックし、**[!UICONTROL クライアントの秘密鍵]**&#x200B;をコピーします。

   ![サービスアカウント資格情報](assets/service-account5.png)

1. 「**[!UICONTROL JWT を生成]**」タブに移動し、**[!UICONTROL JWT ペイロード]**&#x200B;情報をコピーします。

これで、クライアント ID（API キー）、クライアントの秘密鍵、JWT ペイロードを使用して、AEM Assets に [IMS アカウントを設定](#create-ims-account-configuration)できるようになりました。

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

IMS アカウントを設定するには、次の手順を実行します。

1. IMS 設定を開き、「**[!UICONTROL アカウント]**」タブに移動します。[公開証明書の取得](#public-certificate)中も、ページは開いたままになっています。

1. IMS アカウントの&#x200B;**[!UICONTROL タイトル]**&#x200B;を指定します。

   「**[!UICONTROL 認証サーバー]**」フィールドで、URL「 [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)」を指定します。。

   **[!UICONTROL API キー]**&#x200B;にクライアント ID を指定し、[サービスアカウント（JWT）接続の作成](#createnewintegration)時にコピーした&#x200B;**[!UICONTROL クライアントの秘密鍵]**&#x200B;と&#x200B;**[!UICONTROL ペイロード]**（JWT ペイロード）を貼り付けます。

   「**[!UICONTROL 作成]**」をクリックします。

   IMS アカウントが設定されます。

   ![IMS アカウントの設定](assets/create-new-integration6.png)

1. その IMS アカウント設定を選択し、「**[!UICONTROL 正常性をチェック]**」をクリックします。

   ダイアログボックスの「**[!UICONTROL チェック]**」をクリックします。正常に設定されると、*トークンが正常に取得されました*&#x200B;というメッセージが表示されます。

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>IMS 設定は 1 つだけにする必要があります。
>
>IMS 設定がヘルスチェックに合格していることを確認します。設定がヘルスチェックに合格しない場合は無効です。削除して、新しい有効な設定を作成する必要があります。

### Cloud Service の設定 {#configure-the-cloud-service}

Brand Portal Cloud Service を設定するには、次の手順を実行します。

1. AEM Assets オーサーインスタンスにログインします。

1. **ツール**&#x200B;の![ツール](assets/do-not-localize/tools.png)パネルで、**[!UICONTROL Cloud Services]**／**[!UICONTROL AEM Brand Portal]** に移動します。

1. Brand Portal の設定ページで、「**[!UICONTROL 作成]**」をクリックします。

1. 設定の&#x200B;**[!UICONTROL タイトル]**&#x200B;を入力します。

   [IMS アカウントの設定](#create-ims-account-configuration)時に作成した IMS 設定を選択します。

   「**[!UICONTROL サービス URL]**」に、Brand Portal テナント（組織）URL を入力します。

   ![](assets/create-cloud-service.png)

1. 「**[!UICONTROL 保存して閉じる]**」をクリックします。クラウド設定が作成されます。

   これで、AEM AssetsオーサーインスタンスがBrand Portalテナントで設定されました。

### 設定のテスト {#test-integration}

設定を検証するには、次の手順を実行します。

1. AEM Assets クラウドインスタンスにログインします。

1. **ツール** ![ツール](assets/do-not-localize/tools.png)パネルから、**[!UICONTROL デプロイ]** / **[!UICONTROL レプリケーション]**&#x200B;に移動します。

   ![](assets/test-integration1.png)

1. レプリケーションページで、「**[!UICONTROL 作成者のエージェント]**」をクリックします。

   ![](assets/test-integration2.png)

   Brand Portalテナント用に4つのレプリケーションエージェントが作成されています。

   Brand Portalテナントのレプリケーションエージェントを探し、レプリケーションエージェントのURLをクリックします。

   ![](assets/test-integration3.png)

   >[!NOTE]
   >
   >レプリケーションエージェントは並行して動作し、ジョブの配布を均等に共有するので、公開速度は元の速度の4倍に増えます。 クラウドサービスを設定した後は、複数のアセットを並行して公開できるように、デフォルトで有効化されるレプリケーションエージェントを有効にするために追加の設定は必要ありません。

1. AEM Assets  と Brand Portal の間の接続を確認するには、「**[!UICONTROL 接続をテスト]**」アイコンをクリックします。

   ![](assets/test-integration4.png)

   *テストパッケージが正常に配信された*&#x200B;ことを示すメッセージが表示されます。

   ![](assets/test-integration5.png)

1. 4つのレプリケーションエージェントすべてでテスト結果を確認します。


   >[!NOTE]
   >
   >どのレプリケーションエージェントも無効にしないでください。無効にすると、（実行中のキュー内の）アセットのレプリケーションが失敗する可能性があります。
   >
   >タイムアウトエラーを回避するために、4つのレプリケーションエージェントがすべて設定されていることを確認します。 [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/troubleshoot-parallel-publishing.html#connection-timeout)への並列公開における問題のトラブルシューティングを参照してください。
   >
   >自動生成された設定は変更しないでください。

次の操作が可能になっています。

* [AEM Assets から Brand Portal へのアセットの公開](../assets/brand-portal-publish-assets.md)
* [Brand Portal から AEM Assets への公開](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html?lang=ja) - Brand Portal でのアセットのソーシング
* [AEM Assets から Brand Portal へのフォルダーの公開](../assets/brand-portal-publish-folder.md)
* [AEM Assets から Brand Portal へのコレクションの公開](../assets/brand-portal-publish-collection.md)
* [Brand Portal へのプリセット、スキーマ、ファセットの公開](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [Brand Portal へのタグの公開](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)

詳しくは、[Brand Portal ドキュメント](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html)を参照してください。


## 設定のアップグレード {#upgrade-integration-65}

既存の設定をAdobe開発者コンソールにアップグレードするには、以下の手順を上記の手順で実行します。
1. [実行中のジョブの確認](#verify-jobs)
1. [既存の設定の削除](#delete-existing-configuration)
1. [設定の作成](#configure-new-integration-65)

### 実行中のジョブの確認 {#verify-jobs}

変更を加える前に、AEM Assetsオーサーインスタンスで公開ジョブが実行されていないことを確認してください。 そのために、4つのレプリケーションエージェントすべてでアクティブジョブのステータスを確認し、キューがアイドル状態であることを確認できます。

1. AEM Assets オーサーインスタンスにログインします。

1. **ツール** ![ツール](assets/do-not-localize/tools.png)パネルから、**[!UICONTROL デプロイメント]** / **[!UICONTROL デプロイメントレプリケーション]**&#x200B;に移動します。

1. レプリケーションページで、「**[!UICONTROL 作成者のエージェント]**」をクリックします。

   ![](assets/test-integration2.png)

1. Brand Portalテナントのレプリケーションエージェントを見つけます。

   すべてのレプリケーションエージェントに対して&#x200B;**QueueがIdle**&#x200B;であることを確認します。公開ジョブがアクティブでないことを確認します。

   ![](assets/test-integration3.png)

### 既存の設定の削除 {#delete-existing-configuration}

既存の設定を削除する際は、次のチェックリストを実行する必要があります。
* 4つのレプリケーションエージェントをすべて削除する
* Brand Portal Cloud Serviceの削除
* MACユーザーの削除

1. AEM Assetsオーサーインスタンスにログインし、管理者としてCRX Liteを開きます。 デフォルトの URL は `http://localhost:4502/crx/de/index.jsp` です。

1. `/etc/replications/agents.author`に移動し、Brand Portalテナントの4つのレプリケーションエージェントをすべて削除します。

   ![](assets/delete-replication-agent.png)

1. `/etc/cloudservices/mediaportal`に移動し、 Brand Portal Cloud Service設定を削除します。

   ![](assets/delete-cloud-service.png)

1. `/home/users/mac`に移動し、Brand Portalテナントの&#x200B;**MACユーザー**&#x200B;を削除します。

   ![](assets/delete-mac-user.png)


AEM 6.5オーサーインスタンス上のAdobe開発者コンソールから[設定](#configure-new-integration-65)を作成できるようになりました。



<!--
   Comment Type: draft

   <li> </li>
   -->

<!--
   Comment Type: draft

   <li>Step text</li>
   -->
