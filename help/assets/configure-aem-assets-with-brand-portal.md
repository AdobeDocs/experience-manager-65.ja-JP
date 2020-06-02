---
title: AEM Assets と Brand Portal の連携の設定
seo-title: AEM Assets と Brand Portal の連携の設定
description: Brand Portalにアセットやコレクションを公開するためのAEM AssetsとBrand Portalの設定方法を説明します。
seo-description: Brand Portalにアセットやコレクションを公開するためのAEM AssetsとBrand Portalの設定方法を説明します。
uuid: b95c046e-9988-444c-b50e-ff5ec8cafe14
topic-tags: brand-portal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: dca5a2ac-1fc8-4251-b073-730fd6f49b1c
docset: aem65
translation-type: tm+mt
source-git-commit: 9a27aabef07d5b5104c08c414138fbb22e284a68
workflow-type: tm+mt
source-wordcount: '2074'
ht-degree: 23%

---


# AEM Assets と Brand Portal の連携の設定 {#configure-integration-65}

Adobe Experience Manager(AEM)Assetsは、Adobe Developer Consoleを介してBrand Portalで設定され、Brand Portalテナントの認証用にIMSトークンを取得します。

>[!NOTE]
>
>Adobe Developer Consoleを介したBrand PortalでのAEM Assetsの設定は、AEM 6.5.4.0以降でサポートされます。
>
>これまで、Brand Portal は、旧来の OAuth ゲートウェイを通じてクラシック UI で設定されていました。このゲートウェイは、JWT トークン交換を使用して認証用の IMS アクセストークンを取得します。
>
>レガシーOAuthを使用した設定は、2020年4月6日からはサポートされなくなり、Adobe Developer Consoleを使用した設定に変更されました。


>[!TIP]
>
>***既存のお客様のみ***
>
>既存のレガシー OAuth Gateway 設定を引き続き使用することをお勧めします。レガシーOAuth Gateway設定で問題が発生した場合は、既存の設定を削除し、Adobe Developer Consoleを使用して新しい設定を作成します。



このヘルプでは、次の2つの使用例について説明します。
* [新しい設定](#configure-new-integration-65): 新しいBrand Portalユーザーで、AEM Assets作成者インスタンスをBrand Portalで設定する場合は、Adobe Developer Consoleで新しい設定を作成できます。
* [アップグレード設定](#upgrade-integration-65): 既存のBrand Portalユーザーで、レガシーOAuth GatewayのBrand Portalで設定したAEM Assets作成者インスタンスを持つ場合は、既存の設定を削除し、Adobe Developer Consoleで新しい設定を作成することをお勧めします。

具体的には、以下の操作に関する十分な知識があるユーザーを対象としています。

* Adobe Experience ManagerとAEMパッケージのインストール、設定、管理

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

1. AEM Assetsオーサーインスタンスで、IMSアカウントを作成し、公開証明書（公開鍵）を生成します。

1. Adobe Developer Consoleで、Brand Portalテナント（組織）用のプロジェクトを作成します。

1. プロジェクトで、公開鍵を使用してAPIを設定し、サービスアカウント(JWT)接続を作成します。

1. サービスアカウントの資格情報とJWTペイロード情報を取得します。

1. AEM Assetsオーサーインスタンスで、サービスアカウントの資格情報とJWTペイロードを使用してIMSアカウントを設定します。

1. AEM Assets作成者インスタンスで、IMSアカウントとブランドポータルエンドポイント（組織URL）を使用してBrand Portalクラウドサービスを設定します。

1. AEM Assets作成者インスタンスからBrand Portalにアセットを公開して、設定をテストします。


>[!NOTE]
>
>Brand Portalテナントは、1つのAEM Assets作成者インスタンスでのみ設定する必要があります。
>
>複数のAEM Assets作成者インスタンスを持つBrand Portalテナントを設定しないでください。



AEM AssetsをBrand Portalと初めて設定する場合は、一覧に示された順序で次の手順を実行します。
1. [公開証明書の取得](#public-certificate)
1. [サービスアカウント(JWT)接続の作成](#createnewintegration)
1. [IMSアカウントの設定](#create-ims-account-configuration)
1. [Cloud Service の設定](#configure-the-cloud-service)
1. [設定のテスト](#test-integration)

### IMS 設定の作成 {#create-ims-configuration}

IMS 設定は、AEM Assets オーサーインスタンスを使用して Brand Portal テナントを認証します。

IMS 設定には、次の 2 つの手順が含まれます。

* [公開証明書の取得](#public-certificate)
* [IMSアカウントの設定](#create-ims-account-configuration)

### 公開証明書の取得 {#public-certificate}

公開証明書を使用すると、Adobe Developer Consoleでプロファイルを認証できます。

1. AEM Assetsオーサーインスタンスにログインします。 デフォルトのURLは
   `http:// localhost:4502/aem/start.html`
1. **ツール**![ツール](assets/tools.png) パネルで、 **[!UICONTROL セキュリティ/]****** Adobe IMS設定のに移動します。

   ![Adobe IMS アカウント設定 UI](assets/ims-config1.png)

1. Adobe IMS設定ページで、「 **[!UICONTROL 作成]**」をクリックします。

1. 「 **[!UICONTROL Adobe IMSテクニカルアカウント設定]** 」ページにリダイレクトされます。 By default, the **Certificate** tab opens.

   クラウドソリューションの **[!UICONTROL Adobe Brand Portalを選択します]**。

1. Mark the checkbox **[!UICONTROL Create new certificate]** and specify an **alias** for the certificate. ここで入力したエイリアスが、ダイアログ名として表示されます。

1. 「**[!UICONTROL 証明書を作成]**」をクリックします。次に、ダイアログボックスで **[!UICONTROL 「OK]** 」をクリックして、公開証明書を生成します。

   ![証明書を作成](assets/ims-config2.png)

1. Click **[!UICONTROL Download Public Key]** and save the certificate (.crt) file on your machine.

   この証明書ファイルは、Brand PortalテナントのAPIを設定し、Adobe Developer Consoleでサービスアカウントの資格情報を生成するための追加の手順で使用されます。

   ![証明書をダウンロード](assets/ims-config3.png)

1. 「**[!UICONTROL 次へ]**」をクリックします。

   「 **アカウント** 」タブでAdobe IMSアカウントを作成しますが、作成するにはAdobe Developer Consoleで生成されるサービスアカウント資格情報が必要です。 このページは開いたままにしておきます。

   新しいタブを開き、Adobe Developer Consoleでサービスアカウント(JWT)接続を [](#createnewintegration) 作成して、IMSアカウントを設定するための秘密鍵証明書とJWTペイロードを取得します。

### サービスアカウント(JWT)接続の作成 {#createnewintegration}

Adobe Developer Consoleでは、プロジェクトとAPIは組織（Brand Portalテナント）レベルで設定されます。 APIを設定すると、Adobe Developer Consoleでサービスアカウント(JWT)接続が作成されます。 キーペア（秘密鍵と公開鍵）を生成するか、公開鍵をアップロードして、APIを設定する方法は2つあります。 Brand PortalでAEM Assetsオーサーインスタンスを設定するには、AEM Assetsオーサーインスタンスで公開証明書（公開鍵）を生成し、公開鍵をアップロードしてAdobe Developer Consoleで秘密鍵証明書を作成する必要があります。 この公開鍵は、選択したブランドポータル組織のAPIを設定するために使用され、サービスアカウントの資格情報とJWTペイロードを生成します。 これらの資格情報は、AEM AssetsオーサーインスタンスでIMSアカウントを設定する際にさらに使用されます。 IMSアカウントが設定されると、AEM Assets作成者インスタンスでBrand Portalクラウドサービスを設定できます。

次の手順を実行して、サービスアカウント資格情報とJWTペイロードを生成します。

1. IMS組織（Brand Portalテナント）のシステム管理者権限でAdobe Developer Consoleにログインします。 デフォルトのURLは

   [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui)


   >[!NOTE]
   >
   >右上隅にあるドロップダウン(組織リスト)から正しいIMS組織（Brand Portalテナント）が選択されていることを確認します。

1. Click **[!UICONTROL Create new project]**. 組織用に空のプロジェクトが作成されます。

   「 **[!UICONTROL プロジェクトの編集]** 」をクリックして、 **[!UICONTROL プロジェクトタイトル]** と **[!UICONTROL 説明を更新し、「保存と]******&#x200B;保存」をクリックします。

   ![プロジェクトを作成](assets/service-account1.png)

1. 「プロジェクトの概要」タブで、「 **[!UICONTROL 追加API]**」をクリックします。

   ![追加API](assets/service-account2.png)

1. API追加ウィンドウで、「 **[!UICONTROL AEM Brand Portal]** 」を選択し、「 **[!UICONTROL 次へ]**」をクリックします。

   AEM Brand Portalサービスにアクセスできることを確認します。

1. APIを設定ウィンドウで、「公開鍵を **[!UICONTROL アップロード]**」をクリックします。 次に、「ファイルを **[!UICONTROL 選択]** 」をクリックし、「公開証明書を [取得](#public-certificate) 」セクションでダウンロードした公開証明書（.crtファイル）をアップロードします。

   「**[!UICONTROL 次へ]**」をクリックします。

   ![公開鍵をアップロード](assets/service-account3.png)

1. 公開証明書を確認し、「 **[!UICONTROL 次へ]**」をクリックします。

1. デフォルトの製品プロファイル「 **[!UICONTROL アセット」「ブランドポータル]** 」を選択し、「設定 **[!UICONTROL を保存]**」をクリックします。

   ![製品プロファイルの選択](assets/service-account4.png)

1. APIが設定されている場合、APIの概要にリダイレクトされます。 左側のナビゲーションの「 **[!UICONTROL 資格情報]**」で、「 **[!UICONTROL サービスアカウント(JWT)」をクリックし]**&#x200B;ます。

   >[!NOTE]
   >
   >必要に応じて、秘密鍵証明書を表示し、その他の操作（JWTトークンの生成、秘密鍵証明書の詳細のコピー、クライアントシークレットの取得など）を実行できます。

1. 「 **[!UICONTROL Client Credentials]** 」タブで、 **[!UICONTROL クライアントIDをコピーします]**。

   Click **[!UICONTROL Retrieve Client Secret]** and copy the **[!UICONTROL client secret]**.

   ![サービスアカウント資格情報](assets/service-account5.png)

1. Navigate to the **[!UICONTROL Generate JWT]** tab and copy the **[!UICONTROL JWT Payload]**.

クライアントID（APIキー）、クライアントシークレットおよびJWTペイロードを使用して、AEM AssetsクラウドインスタンスでIMSアカウント [を](#create-ims-account-configuration) 設定できるようになりました。

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
* [サービスアカウント(JWT)接続の作成](#createnewintegration)

次の手順を実行して、公開証明書を [取得して作成したIMSアカウントを設定します](#public-certificate)。

1. IMS設定を開き、「 **[!UICONTROL アカウント]** 」タブに移動します。 公開証明書の [取得中にページを開いたままにした](#public-certificate)。

1. IMS アカウントの&#x200B;**[!UICONTROL タイトル]**&#x200B;を指定します。

   「**[!UICONTROL 認証サーバー]**」に次の URL を入力します。[https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)

   サービスアカウント(JWT)接続の [作成中にコピーしたAPIキー、クライアントシークレット、およびJWTペイロードにクライアントIDを貼り付け](#createnewintegration)ます。

   「**[!UICONTROL 作成]**」をクリックします。

   IMSアカウントが設定されている。

   ![IMS アカウントの設定](assets/create-new-integration6.png)


1. 作成した IMS 設定を選択して「**[!UICONTROL ヘルスチェック]**」をクリックします。

   ダイアログボックスで **[!UICONTROL 「チェック]** 」をクリックします。 設定が成功すると、 *トークンが正常に取得されたことを示すメッセージが表示されます*。

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>IMS 設定は 1 つだけにする必要があります。複数の IMS 設定を作成しないでください。
>
>IMS 設定がヘルスチェックに合格していることを確認します。設定がヘルスチェックに合格しない場合は無効です。削除して、新しい有効な設定を作成する必要があります。



### Cloud Service の設定{#configure-the-cloud-service}

次の手順を実行して、ブランドポータルクラウドサービスを作成します。

1. AEM Assetsオーサーインスタンスにログインします。

1. From the **Tools** ![Tools](assets/tools.png) panel, navigate to **[!UICONTROL Cloud Services]** > **[!UICONTROL AEM Brand Portal]**.

1. Brand Portal Configurationsページで、「 **[!UICONTROL 作成]**」をクリックします。

1. 設定の&#x200B;**[!UICONTROL タイトル]**&#x200B;を入力します。

   IMSアカウントの [設定時に作成したIMS設定を選択します](#create-ims-account-configuration)。

   In the **[!UICONTROL Service URL]**, enter your Brand Portal tenant (organization) URL.

   ![](assets/create-cloud-service.png)

1. 「**[!UICONTROL 保存して閉じる]**」をクリックします。クラウド設定が作成されます。これで、AEM Assets作成者インスタンスがBrand Portalテナントと共に設定されました。

### 設定のテスト{#test-integration}

次の手順を実行して設定を検証します。

1. AEM Assetsクラウドインスタンスにログインします。

1. 「 **Tools** Tools ![」](assets/tools.png) パネルで、「 **[!UICONTROL Deployment]** 」>「Replication」>「Replication」の順に移動 ****&#x200B;します。

   ![](assets/test-integration1.png)

1. In the Replication page, click **[!UICONTROL Agents on author]**.

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
   >どのレプリケーションエージェントも無効にしないでください。一部のアセットのレプリケーションが失敗する可能性があります。

AEM Assets作成者インスタンスがBrand Portalで正しく設定され、次の操作が可能になりました。

* [AEM Assets から Brand Portal へのアセットの公開](../assets/brand-portal-publish-assets.md)
* [AEM Assets から Brand Portal へのフォルダーの公開](../assets/brand-portal-publish-folder.md)
* [AEM Assets から Brand Portal へのコレクションの公開](../assets/brand-portal-publish-collection.md)
* [Asset Sourcingを設定し](https://docs.adobe.com/content/help/ja-JP/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html) 、Brand PortalユーザがAEM Assetsにアセットを寄稿して公開できるようにします。

## 設定のアップグレード {#upgrade-integration-65}

既存の設定をアップグレードするには、次の手順を一覧に示す順序で実行します。
1. [実行中のジョブの確認](#verify-jobs)
1. [既存の設定の削除](#delete-existing-configuration)
1. [設定の作成](#configure-new-integration-65)

### 実行中のジョブの確認 {#verify-jobs}

変更を行う前に、AEM Assetsオーサーインスタンスで公開ジョブが実行されていないことを確認してください。 その場合は、4つのレプリケーションエージェントをすべて検証し、キューが理想的/空であることを確認できます。

1. AEM Assetsオーサーインスタンスにログインします。

1. 「 **Tools** Tools ![」パネルで、](assets/tools.png) 「Deployment **[!UICONTROL 」>「Deployment Replication」の順に移動します。]** 「Deployment Replication」の「 **** Tools」パネルから、

1. In the Replication page, click **[!UICONTROL Agents on author]**.

   ![](assets/test-integration2.png)

1. Brand Portalテナントのレプリケーションエージェントを見つけます。

   すべてのレプリケーションエージェントで **キューがアイドル状態であることを確認します** 。公開ジョブがアクティブでないことを確認します。

   ![](assets/test-integration3.png)

### 既存の設定の削除 {#delete-existing-configuration}

既存の設定の削除中に、次のチェックリストを実行する必要があります。
* 4つのレプリケーションエージェントをすべて削除する
* クラウドサービスの削除
* MACユーザーの削除

1. AEM Assetsオーサーインスタンスにログインし、管理者としてCRX Liteを開きます。 デフォルトのURLは

   `http:// localhost:4502/crx/de/index.jsp`

1. Brand Portalテナントの4つのレプリケーションエージェントすべてに移動 `/etc/replications/agents.author` して削除します。

   ![](assets/delete-replication-agent.png)

1. ク `/etc/cloudservices/mediaportal` ラウドサービスの設定に移動 **して削除します**。

   ![](assets/delete-cloud-service.png)

1. Brand Portalテナントの `/home/users/mac` MACユーザ **** に移動して削除します。

   ![](assets/delete-mac-user.png)


これで、AEM 6.5オーサーインスタンスに設定 [を](#configure-new-integration-65) 作成できます。



<!--
   Comment Type: draft

   <li> </li>
   -->

<!--
   Comment Type: draft

   <li>Step text</li>
   -->

レプリケーションが正常に終了したら、アセット、フォルダー、コレクションを Brand Portal に公開することができます。詳しくは、次を参照してください。

* [Brand Portal へのアセットの公開](/help/assets/brand-portal-publish-assets.md)
* [Brand Portal へのフォルダーの公開](/help/assets/brand-portal-publish-folder.md)
* [Brand Portal へのコレクションの公開](/help/assets/brand-portal-publish-collection.md)
