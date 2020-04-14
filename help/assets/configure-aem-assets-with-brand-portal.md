---
title: AEM Assets と Brand Portal の連携の設定
seo-title: AEM Assets と Brand Portal の連携の設定
description: Brand PortalでAEM Assetsを設定し、アセットとコレクションをBrand Portalに公開する方法を説明します。
seo-description: Brand PortalでAEM Assetsを設定し、アセットとコレクションをBrand Portalに公開する方法を説明します。
uuid: b95c046e-9988-444c-b50e-ff5ec8cafe14
topic-tags: brand-portal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: dca5a2ac-1fc8-4251-b073-730fd6f49b1c
docset: aem65
translation-type: tm+mt
source-git-commit: 28354bd9785fa83939f9e3b051aac195d7706633

---


# AEM Assets と Brand Portal の連携の設定 {#configure-integration-65}

Adobe Experience Manager（AEM）Assets と Brand Portal の連携が、Adobe I/O を通じて設定されます。Adobe I/O は Brand Portal テナントの認証用の IMS トークンを取得します。

>[!NOTE]
>
>Adobe I/O を使用した AEM Assets と Brand Portal の連携の設定は、AEM 6.5.4.0 以降でサポートされています。
>
>これまで、Brand Portal は、旧来の OAuth ゲートウェイを通じてクラシック UI で設定されていました。このゲートウェイは、JWT トークン交換を使用して認証用の IMS アクセストークンを取得します。
>
>旧来の OAuth を使用した設定は、2020 年 4 月 6 日以降はサポートされなくなり、Adobe I/O を使用した設定に変更されます。


>[!TIP]
>
>***既存のお客様のみ***
>
>既存のレガシー OAuth Gateway 設定を引き続き使用することをお勧めします。レガシー OAuth Gateway 設定に問題が発生した場合は、既存の設定を削除し、Adobe I/O から新しい設定を作成します。



このヘルプでは、次の2つの使用例について説明します。
* [新しい設定](#configure-new-integration-65):新しいBrand Portalユーザーで、AEM Assets作成者インスタンスをBrand Portalで設定する場合は、Adobe I/Oで新しい設定を作成できます。
* [アップグレード設定](#upgrade-integration-65):既存のBrand Portalユーザーで、レガシーOAuth GatewayのBrand Portalで設定したAEM Assets作成者インスタンスを使用する場合は、既存の設定を削除し、Adobe I/Oで新しい設定を作成することをお勧めします。

具体的には、以下の操作に関する十分な知識があるユーザーを対象としています。

* Adobe Experience ManagerおよびAEMパッケージのインストール、設定、管理

* LinuxおよびMicrosoft Windowsオペレーティングシステムの使用

## 前提条件 {#prerequisites}

AEM Assets と Brand Portal の連携を設定するには以下が必要です。

* 最新のサービスパックを適用した実行中の AEM Assets オーサーインスタンス
* Brand Portal テナント URL
* Brand Portal テナントの IMS 組織に対するシステム管理者権限を持つユーザー


[AEM 6.5のダウンロードとインストール](#aemquickstart)

[最新の AEM サービスパックをダウンロードしてインストールする](#servicepack)

### Download and install AEM 6.5 {#aemquickstart}

AEM 6.5を使用してAEM作成者インスタンスを設定することをお勧めします。 AEM が稼働していない場合は、以下の場所から AEM をダウンロードしてください。

* If you are an existing AEM customer, download AEM 6.5 from [Adobe Licensing website](http://licensing.adobe.com).

* If you are an Adobe partner, use [Adobe Partner Training Program](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=82357Q) to request AEM 6.5.

AEM をダウンロードしたら、「[デプロイメントと保守](https://helpx.adobe.com/jp/experience-manager/6-5/sites/deploying/using/deploy.html#defaultlocalinstall)」の説明に従い、AEM オーサーインスタンスの設定を行ってください。

### 最新の AEM サービスパックをダウンロードしてインストールする{#servicepack}

詳細な手順については、

* [AEM 6.5 Service Pack リリースノート](https://helpx.adobe.com/jp/experience-manager/6-5/release-notes/sp-release-notes.html)

**最新のAEMパッケージ** またはService Packが見つからない場合は、サポートにお問い合わせください。

##  設定の作成{#configure-new-integration-65}

AEM AssetsをBrand Portalで初めて設定する場合は、一覧に示された手順を実行します。
1. [公開証明書の取得](#public-certificate)
1. [Adobe I/O 統合環境を作成する](#createnewintegration)
1. [IMSアカウント設定の作成](#create-ims-account-configuration)
1. [クラウドサービスの設定](#configure-the-cloud-service)
1. [テスト設定](#test-integration)

### IMS設定の作成 {#create-ims-configuration}

IMS設定は、AEM Assetsオーサーインスタンスを使用してBrand Portalテナントを認証します。

IMS設定には、次の2つの手順が含まれます。

* [公開証明書の取得](#public-certificate)
* [IMSアカウント設定の作成](#create-ims-account-configuration)

### 公開証明書の取得 {#public-certificate}

公開証明書を使用すると、Adobe I/Oでプロファイルを認証できます。

1. AEM Assets作成者インスタンスにログインします。デフォルトのURL:http:// localhost:4502/aem/start.html
1. ツー **ル** / ![Security](assets/tools.png) / **[!UICONTROL Adobe]** IMS Configurationsに移動し ****&#x200B;ます。

   ![Adobe IMSアカウント設定UI](assets/ims-config1.png)

1. Adobe IMS設定ページが開きます。

   「**[!UICONTROL 作成]**」をクリックします。

   これにより、 **[!UICONTROL Adobe IMS Technical Account Configurationページが表示されます]** 。

1. デフォルトでは、「証 **明書** 」タブが開きます。

   「 **Cloud Solution**」で「 **[!UICONTROL Adobe Brand Portal」を選択します]**。

1. 「新しい証明書を作成 **[!UICONTROL し、証明書のエイリアスを指定]** 」チェックボ **ックスを** オンにします。 ここで入力したエイリアスが、ダイアログ名として表示されます。 

1. 「**[!UICONTROL 証明書を作成]**」をクリックします。ダイアログが表示されます。「 **[!UICONTROL OK]** 」をクリックして公開証明書を生成します。

   ![証明書の作成](assets/ims-config2.png)

1. Click **[!UICONTROL Download Public Key]** and save the *AEM-Adobe-IMS.crt* certificate file on your machine. The certificate file is used to [create Adobe I/O integration](#createnewintegration).

   ![証明書のダウンロード](assets/ims-config3.png)

1. 「**[!UICONTROL 次へ]**」をクリックします。

   「アカウ **ント** 」タブで、Adobe IMSアカウントを作成しますが、統合の詳細が必要です。 このページは開いたままにしておきます。

   新しいタブを開き、Adobe I/O [統合を作成して](#createnewintegration) 、IMSアカウント設定の統合の詳細を取得します。

### Adobe I/O 統合環境を作成する{#createnewintegration}

Adobe I/O統合により、IMSアカウント設定の設定で必要なAPIキー、クライアントシークレット、ペイロード(JWT)が生成されます。

1. Brand PortalテナントのIMS組織のシステム管理者権限でAdobe I/O Consoleにログインします。

   デフォルトURL:https://console.adobe.io/ [](https://console.adobe.io/)

1. Click **[!UICONTROL Create Integration]**.

1. 「 **[!UICONTROL Access an API]**」を選択し、「 **[!UICONTROL Continue」をクリックします]**。

   ![新しい統合の作成](assets/create-new-integration1.png)

1. 新しい統合ページを作成します。

   ドロップダウンオプションから組織をリストします。

   **[!UICONTROL Experience Cloud]**、 **[!UICONTROL AEM Brand Portalを選択し、「続行]** 」をクリッ **[!UICONTROL クします]**。

   If the Brand Portal option is disabled for you, ensure that you have selected correct organization from the drop-down box above the **[!UICONTROL Adobe Services]** option. 自分がどの組織に属しているかわからない場合は、管理者に問い合わせてください。

   ![統合の作成](assets/create-new-integration2.png)

1. 統合の名前と説明を指定します。 Click **[!UICONTROL Select a File from your computer]** and upload the `AEM-Adobe-IMS.crt` file downloaded in the [obtain public certificates](#public-certificate) section.

1. 組織のプロファイルを選択します。

   または、デフォルトのプロファイル **[!UICONTROL Assets Brand Portalを選択し]** 、「統合を作成」を **[!UICONTROL クリックします]**。 統合環境が作成されます。

1. Click **[!UICONTROL Continue to integration details]** to view the integration information.

   **[!UICONTROL APIキーのコピー]**

   「 **[!UICONTROL Retrieve Client Secret]** 」をクリックし、Client Secretキーをコピーします。

   ![統合環境の API キー、クライアント秘密鍵、ペイロード情報の表示画面](assets/create-new-integration3.png)

1. 「 **[!UICONTROL JWT]** 」タブに移動し、 **[!UICONTROL JWTペイロードをコピーします]**。

   APIキー、クライアント秘密キー、JWTペイロード情報は、IMSアカウント設定の作成に使用されます。

### IMSアカウント設定の作成 {#create-ims-account-configuration}

次の手順を実行したことを確認します。

* [公開証明書の取得](#public-certificate)
* [Adobe I/O 統合環境を作成する](#createnewintegration)

**IMSアカウント設定を作成する手順：**

1. IMS設定ページの「アカウント」タ **[!UICONTROL ブを開きます]** 。 （このページは、「[公開証明書を取得する](#public-certificate)」セクションの最後で開いたままにしておいたページです）。

1. IMSアカウント **[!UICONTROL のタイトル]** を指定します。

   「認 **[!UICONTROL 証サーバー]**」にURLを入力します。https://ims-na1.adobelogin.com/ [](https://ims-na1.adobelogin.com/)

   「Adobe I/O統合の作成」の最後にコピーしたAPIキー、Client Secret、JWTペイロ [ードを貼り付けます](#createnewintegration)。

   「**[!UICONTROL 作成]**」をクリックします。

   統合が作成されます。

   ![IMSアカウントの設定](assets/create-new-integration6.png)


1. Select the IMS configuration and click **[!UICONTROL Check Health]**. ダイアログボックスが表示されます。

   [チェック **をクリック]**。 接続が成功すると、*トークンが正常に取得された*&#x200B;ことを示すメッセージが表示されます。

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>有効なIMS設定を1つだけ作成します。
>
> 構成が正常であることを確認します。 構成が正常でない場合は、構成を削除し、新しい正常な構成を作成します。


### Configure cloud service {#configure-the-cloud-service}

次の手順を実行して、Brand Portalクラウドサービスの設定を作成します。

1. AEM Assets作成者インスタンスにログインします。

   （デフォルト URL：http:// localhost:4502/aem/start.html）にログインします。
1. ツール **ツー** ル ![](assets/tools.png) ・パネルで、 **[!UICONTROL Cloud Services/AEM Brand Portalに移動します]**。

   ブランドポータル設定ページが開きます。

1. 「**[!UICONTROL 作成]**」をクリックします。

1. Specify a **[!UICONTROL Title]** for the configuration.

   手順で作成したIMS設定を選択し、IMSアカウント設 [定を作成します](#create-ims-account-configuration)。

   「サー **[!UICONTROL ビスURL]**」に、ブランドポータルテナントURLを入力します。

   ![](assets/create-cloud-service.png)

1. Click **[!UICONTROL Save and Close]**. クラウド設定が作成されます。 これで、AEM Assets作成者インスタンスがBrand Portalテナントと統合されました。

### Test configuration {#test-integration}

1. AEM Assets作成者インスタンスにログインします。

   （デフォルト URL：http:// localhost:4502/aem/start.html）にログインします。

1. ツー **ル**![/](assets/tools.png) 複製に **[!UICONTROL 移動します]**。

   ![](assets/test-integration1.png)

1. 複製ページが開きます。

   「作成者のエ **[!UICONTROL ージェント」をクリックしま]**&#x200B;す。

   ![](assets/test-integration2.png)

1. 各テナントに対して4つのレプリケーションエージェントが作成されます。

   ブランドポータルテナントのレプリケーションエージェントを探します。

   複製エージェントのURLをクリックします。

   ![](assets/test-integration3.png)


   >[!NOTE]
   >
   >レプリケーションエージェントは並行して動作し、ジョブの均等な配信を共有するので、パブリッシング速度は元の速度の4倍に増加します。 クラウドサービスの設定後は、複数のアセットの並行公開を有効にするために、デフォルトでアクティブ化される複製エージェントを有効にするために、追加の設定は必要ありません。

   >[!NOTE]
   >
   >どのレプリケーションエージェントも無効にしないでください。一部のアセットのレプリケーションが失敗する可能性があります。


1. AEM Assetsの作成者とBrand Portalとの接続を確認するには、「接続をテスト」をク **[!UICONTROL リックします]**。

   ![](assets/test-integration4.png)

1. テスト結果の一番下を見て、レプリケーションが成功したことを確認します。

   ![](assets/test-integration5.png)

   >[!NOTE]
   >
   >レプリケーションエージェントは並行して動作し、ジョブの均等な配信を共有するので、パブリッシング速度は元の速度の4倍に増加します。 クラウドサービスの設定後は、複数のアセットの並行公開を有効にするために、デフォルトでアクティブ化される複製エージェントを有効にするために、追加の設定は必要ありません。

1. 4つのレプリケーションエージェントすべてに対するテスト結果を1つずつ確認します。


   >[!NOTE]
   >
   >どのレプリケーションエージェントも無効にしないでください。一部のアセットのレプリケーションが失敗する可能性があります。

Brand Portalは、AEM Assets作成者インスタンスを使用して正常に設定されました。 次の操作が可能になりました。

* [AEM AssetsからBrand Portalへのアセットの公開](../assets/brand-portal-publish-assets.md)
* [AEM AssetsからBrand Portalへのフォルダーの公開](../assets/brand-portal-publish-folder.md)
* [AEM Assetsからブランドポータルにコレクションを公開する](../assets/brand-portal-publish-collection.md)
* [Brand Portalユーザが](https://docs.adobe.com/content/help/ja-JP/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html) 、アセットをAEM Assetsに寄稿および公開できるように、アセットソーシングを設定します。

## 設定のアップグレード {#upgrade-integration-65}

既存の設定をアップグレードするには、次の手順を一覧の手順で実行します。
1. [実行中のジョブの確認](#verify-jobs)
1. [既存の設定の削除](#delete-existing-configuration)
1. [ 設定の作成](#configure-new-integration-65)

### 実行中のジョブの確認 {#verify-jobs}

変更を行う前に、AEM Assetsオーサーインスタンスで公開ジョブが実行されていないことを確認してください。 この場合、4つのレプリケーションエージェントをすべて検証し、キューが理想的/空であることを確認できます。

1. AEM Assets作成者インスタンスにログインします。

   （デフォルト URL：http:// localhost:4502/aem/start.html）にログインします。

1. ツー **ル**![/](assets/tools.png) 複製に **[!UICONTROL 移動します]**。

1. 複製ページが開きます。

   「作成者のエ **[!UICONTROL ージェント」をクリックしま]**&#x200B;す。

   ![](assets/test-integration2.png)

1. ブランドポータルテナントのレプリケーションエージェントを探します。

   すべてのレプリケーショ **ンエージェントのキューがアイドル状態で** 、公開ジョブがアクティブでないことを確認します。

   ![](assets/test-integration3.png)

### 既存の設定の削除 {#delete-existing-configuration}

既存の設定の削除時に、次のチェックリストを実行する必要があります。
* 4つのレプリケーションエージェントをすべて削除する
* クラウドサービスの削除
* MACユーザーの削除

1. AEM Assetsオーサーインスタンスにログインし、管理者としてCRX Liteを開きます。

   デフォルトURL:http:// localhost:4502/crx/de/index.jsp

1. Brand Portalテナントの4 `/etc/replications/agents.author` つのレプリケーションエージェントに移動し、すべて削除します。

   ![](assets/delete-replication-agent.png)

1. クラウドサー `/etc/cloudservices/mediaportal` ビスの設定に移動し **て削除します**。

   ![](assets/delete-cloud-service.png)

1. Brand Portalテナン `/home/users/mac` トの **MACユーザ** ーに移動して削除します。

   ![](assets/delete-mac-user.png)


Adobe I/O上のAEM [](#configure-new-integration-65) 6.5オーサーインスタンスで設定を作成できるようになりました。



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
