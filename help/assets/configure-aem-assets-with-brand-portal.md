---
title: AEM Assets と Brand Portal の連携の設定
description: アセットおよびコレクションを Brand Portal に公開するために AEM Assets を Brand Portal と統合する方法について説明します。
topic-tags: brand-portal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
docset: aem65
feature: Brand Portal
role: Admin
exl-id: ae33181c-9eec-421c-be55-4bd019de40b8
hide: true
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '2130'
ht-degree: 61%

---


# AEM Assets と Brand Portal の連携の設定 {#configure-integration-65}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/configure-aem-assets-with-brand-portal.html?lang=ja) |
| AEM 6.5 | この記事 |

Adobe Experience Manager Assets Brand Portalを使用すると、承認済みのブランドアセットをAdobe Experience Manager Assets からBrand Portalに公開し、Brand Portalユーザーに配布できます。

AEM Assets と Brand Portal の連携は、Adobe 開発者コンソールを通じて設定されます。このコンソールでは、Brand Portal テナントの認証に使用する Adobe Identity Management サービス（IMS）アカウントトークンを調達します。

>[!NOTE]
>
>Adobe 開発者コンソールを使用した AEM Assets と Brand Portal の連携の設定は、AEM 6.5.4.0 以降でサポートされています。
>
>これまで、Brand Portal は、旧来の OAuth ゲートウェイを通じてクラシックインターフェイスで設定されていました。このゲートウェイは、JSON Web トークン（JWT）交換を使用して認証用の IMS トークンを取得します。
>
>旧来の OAuth を使用した設定は、2020年4月6日（PT）以降はサポートされなくなり、Adobe 開発者コンソールを使用した設定に変更されました。

>[!TIP]
>
>***既存のお客様のみ***
>
>Adobeでは、既存のレガシー OAuth Gateway 設定を引き続き使用することをお勧めします。 旧来の OAuth Gateway 設定で問題が発生した場合は、既存の設定を削除し、Adobe Developerコンソールを使用して設定を作成します。

このヘルプでは、次の 2 つのユースケースについて説明します。

* [新しい設定](#configure-new-integration-65)：新しいBrand Portalユーザーで、Brand Portalを使用してAEM Assetsオーサーインスタンスを設定する場合は、Adobe Developerコンソールを使用して設定を作成できます。
* [設定をアップグレード](#upgrade-integration-65)：旧来の OAuth Gateway を使用した設定を既におこなっているBrand Portalユーザーの場合は、既存の設定を削除し、Adobe Developerコンソールを使用して設定を作成します。

具体的には、以下の操作に関する十分な知識があるユーザーを対象としています。

* Adobe Experience Manager パッケージと AEM パッケージのインストール、設定、管理

* Linux®およびMicrosoft® Windows オペレーティングシステムの使用。

## 前提条件 {#prerequisites}

AEM Assets と Brand Portal の連携を設定するには以下が必要です。

* 最新のサービスパックが付属したAEM Assetsオーサーインスタンスの起動および実行
* Brand Portal テナント URL
* Brand Portal テナントの IMS 組織に対するシステム管理者権限を持つユーザー

[AEM 6.5 のダウンロードとインストール](#aemquickstart)

[最新のAEM Service Pack をダウンロードしてインストールする](#servicepack)

### AEM 6.5 のダウンロードとインストール {#aemquickstart}

AEMオーサーインスタンスを設定するには、AEM 6.5 を使用することをお勧めします。 AEM が稼働していない場合は、以下の場所から AEM をダウンロードしてください。

* 既にAEMを使用している場合は、 [Adobeライセンス Web サイト](https://licensing.adobe.com).

* ユーザーがAdobeパートナーの場合、 [Adobeパートナートレーニングプログラム](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=82357Q) AEM 6.5 をリクエストするには、以下を実行します。

AEMをダウンロードしたら、AEMオーサーインスタンスの設定手順については、 [デプロイと保守](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html?lang=ja#default-local-install).

### 最新の AEM サービスパックをダウンロードしてインストールする {#servicepack}

詳しい手順については、現在の [AEM 6.5 Service Pack リリースノート](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=ja).

**Adobeカスタマーサポートに連絡** 最新のAEMパッケージまたは Service Pack が見つからない場合。

## 設定の作成 {#configure-new-integration-65}

Brand Portalと連携するAEM Assetsの設定をおこなうには、AEM AssetsオーサーインスタンスとAdobe Developerコンソールの両方で設定が必要です。

1. AEM Assets クラウドインスタンスで、IMS アカウントを作成し、公開証明書（公開鍵）を生成します。
1. Adobe 開発者コンソールで、Brand Portal テナント（組織）用のプロジェクトを作成します。
1. そのプロジェクトで、公開鍵で API を設定して、サービスアカウント（JWT）接続を作成します。
1. サービスアカウント資格情報と JWT ペイロード情報を取得します。
1. AEM Assets で、サービスアカウント資格情報と JWT ペイロードを使用して IMS アカウントを設定します。
1. AEM Assets で、IMS アカウントと Brand Portal エンドポイント（組織 URL）を使用して Brand Portal Cloud Service を設定します。
1. AEM Assets から Brand Portal にアセットを公開して、設定をテストします。

>[!NOTE]
>
>AEM Assetsオーサーインスタンスは、1 つのBrand Portalテナントでのみ設定できます。

AEM Assets と Brand Portal を初めて設定する場合は、以下の手順を上記の順序で実行します。

1. [公開証明書の取得](#public-certificate)
1. [サービスアカウント（JWT）接続の作成](#createnewintegration)
1. [IMS アカウントの設定](#create-ims-account-configuration)
1. [Cloud Service の設定](#configure-the-cloud-service)
1. [設定のテスト](#test-integration)

### IMS 設定の作成 {#create-ims-configuration}

IMS 設定は、AEM AssetsテナントでBrand Portalオーサーインスタンスを認証します。

IMS 設定には、次の 2 つの手順が含まれます。

* [公開証明書の取得](#public-certificate)
* [IMS アカウントの設定](#create-ims-account-configuration)

### 公開証明書の取得 {#public-certificate}

公開鍵（証明書）は、Adobe 開発者コンソールでプロファイルを認証します。

1. AEM Assetsオーサーインスタンスにログインします。 デフォルトの URL は `http://localhost:4502/aem/start.html` です。

1. **ツール**![ツール](assets/do-not-localize/tools.png)パネルで、**[!UICONTROL セキュリティ]**／**[!UICONTROL Adobe IMS 設定]**&#x200B;に移動します。

1. Adobe IMS設定ページで、 **[!UICONTROL 作成]**. リダイレクト先： **[!UICONTROL Adobe IMSテクニカルアカウント設定]** ページに貼り付けます。 デフォルトでは、「**証明書**」タブが開きます。

1. 「**[!UICONTROL クラウドソリューション]**」ドロップダウンリストで「**[!UICONTROL Adobe Brand Portal]**」を選択します。

1. 「**[!UICONTROL 新しい証明書を作成]**」チェックボックスをオンにして、公開鍵の **エイリアス** を指定します。このエイリアスが、公開鍵の名前になります。

1. 「**[!UICONTROL 証明書を作成]**」をクリックします。「**[!UICONTROL OK]**」をクリックして公開証明書を生成します。

   ![証明書を作成](assets/ims-config2.png)

1. **[!UICONTROL 公開鍵をダウンロード]**&#x200B;アイコンをクリックして、公開鍵（.crt）ファイルをローカルマシンに保存します。

   この公開鍵を後で使用して、Brand Portalテナントの API を設定し、Adobe Developerコンソールでサービスアカウント資格情報を生成します。

   ![証明書をダウンロード](assets/ims-config3.png)

1. 「**[!UICONTROL 次へ]**」をクリックします。

   Adobe Analytics の **アカウント** 「 」タブに「 」Adobe IMSを入力すると、Adobe Developer Console で生成されるサービスアカウント資格情報が必要なアカウントが作成されます。 このページは開いたままにしておきます。

   新しいタブを開き、 [Adobe Developerコンソールでのサービスアカウント (JWT) 接続の作成](#createnewintegration) IMS アカウントを設定するための資格情報と JWT ペイロードを取得できます。

### サービスアカウント (JWT) 接続の作成 {#createnewintegration}

Adobe Developer Console で、プロジェクトと API をBrand Portalテナント（組織）レベルで設定します。 API を設定すると、サービスアカウント（JWT）接続が作成されます。API を設定するには、キーペア（秘密鍵と公開鍵）を生成する方法と、公開鍵をアップロードする方法の 2 つがあります。 AEM Assets と Brand Portal の統合を設定するには、AEM Assets で公開鍵（証明書）を生成し、その公開鍵をアップロードして Adobe 開発者コンソールで資格情報を作成する必要があります。これらの資格情報は、AEM Assets で IMS アカウントを設定するために必要です。IMS アカウントを設定したら、AEM Assets に Brand Portal Cloud Service を設定できます。

サービスアカウント資格情報と JWT ペイロードを作成するには、以下の手順を実行します。

1. IMS 組織（Brand Portal テナント）のシステム管理者権限で Adobe 開発者コンソールにログインします。デフォルトの URL は [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui) です。


   >[!NOTE]
   >
   >右上隅のドロップダウン（組織）リストで正しい IMS 組織 (Brand Portalテナント ) が選択されていることを確認します。

1. 「**[!UICONTROL 新規プロジェクトを作成]**」をクリックします。システムで生成された名前を持つ空のプロジェクトが組織に対して作成されます。

   クリック **[!UICONTROL プロジェクトを編集]** そのため、 **[!UICONTROL プロジェクトタイトル]** および **[!UICONTROL 説明]**&#x200B;をクリックし、 **[!UICONTROL 保存]**.

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

1. API が設定されると、API の概要ページにリダイレクトされます。左側のナビゲーションから、 **[!UICONTROL 資格情報]**&#x200B;をクリックし、 **[!UICONTROL サービスアカウント (JWT)]** オプション。

   >[!NOTE]
   >
   >資格情報を表示し、JWT トークンの生成、資格情報の詳細のコピー、クライアントの秘密鍵の取得などのアクションを実行できます。

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

   The API Key, Client Secret key, and JWT payload information that is used to create IMS account configuration.
-->

### IMS アカウントの設定 {#create-ims-account-configuration}

次の手順が既に実行されていることを確認します。

* [公開証明書の取得](#public-certificate)
* [サービスアカウント（JWT）接続の作成](#createnewintegration)

IMS アカウントを設定するには：

1. IMS 設定を開き、「**[!UICONTROL アカウント]**」タブに移動します。[公開証明書の取得](#public-certificate)中も、ページは開いたままになっています。

1. IMS アカウントの&#x200B;**[!UICONTROL タイトル]**&#x200B;を指定します。

   「**[!UICONTROL 認証サーバー]**」フィールドで、URL「 [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)」を指定します。。

   **[!UICONTROL API キー]**&#x200B;にクライアント ID を指定し、[サービスアカウント（JWT）接続の作成](#createnewintegration)時にコピーした&#x200B;**[!UICONTROL クライアントの秘密鍵]**&#x200B;と&#x200B;**[!UICONTROL ペイロード]**（JWT ペイロード）を貼り付けます。

   「**[!UICONTROL 作成]**」をクリックします。

   IMS アカウントが設定されます。

   ![IMS アカウントの設定](assets/create-new-integration6.png)

1. その IMS アカウント設定を選択し、「**[!UICONTROL 正常性をチェック]**」をクリックします。

   ダイアログボックスの「**[!UICONTROL チェック]**」をクリックします。正常に設定されると、*トークンが正常に取得されました*&#x200B;というメッセージが表示されます。

   ![正常な設定の確認ダイアログ](assets/create-new-integration5.png)

>[!CAUTION]
>
>IMS 設定は 1 つだけにする必要があります。
>
>IMS 設定がヘルスチェックに合格していることを確認します。設定がヘルスチェックに合格しない場合は無効です。削除して、別の有効な設定を作成します。

### Brand Portal Cloud Service の設定 {#configure-the-cloud-service}

1. AEM Assetsオーサーインスタンスにログインします。

1. **ツール**&#x200B;の![ツール](assets/do-not-localize/tools.png)パネルで、**[!UICONTROL Cloud Services]**／**[!UICONTROL AEM Brand Portal]** に移動します。

1. Brand Portal の設定ページで、「**[!UICONTROL 作成]**」をクリックします。

1. 設定の&#x200B;**[!UICONTROL タイトル]**&#x200B;を入力します。

   [IMS アカウントの設定](#create-ims-account-configuration)時に作成した IMS 設定を選択します。

   「**[!UICONTROL サービス URL]**」に、Brand Portal テナント（組織）URL を入力します。

   ![Brand Portal Configuration ウィンドウ](assets/create-cloud-service.png)

1. 「**[!UICONTROL 保存して閉じる]**」をクリックします。クラウド設定が作成されます。

   これで、AEM AssetsオーサーインスタンスがBrand Portalテナントで設定されました。

### 設定のテストと検証 {#test-integration}

1. AEM Assets クラウドインスタンスにログインします。

1. **ツール**&#x200B;の![ツール](assets/do-not-localize/tools.png)パネルで、**[!UICONTROL デプロイメント]**／**[!UICONTROL レプリケーション]**&#x200B;に移動します。

   ![ツールパネル](assets/test-integration1.png)

1. レプリケーションページで、 **[!UICONTROL 作成者のエージェント]**.

   ![レプリケーションページ](assets/test-integration2.png)

   Brand Portal テナントのために作成された 4 つのレプリケーションエージェントを表示できます。

   Brand Portalテナントのレプリケーションエージェントを探し、レプリケーションエージェント URL をクリックします。

   ![Assets レプリケーション設定](assets/test-integration3.png)

   >[!NOTE]
   >
   >レプリケーションエージェントは並行して動作し、ジョブの配布を均等に共有するので、公開速度が元の速度の 4 倍に向上します。 Cloud Service を設定した後、レプリケーションエージェントを有効にするために追加の設定は必要ありません。レプリケーションエージェントはデフォルトでアクティベートされ、複数のアセットを並行して公開できるようになります。

1. AEM AssetsとBrand Portalの間の接続を確認するには、 **[!UICONTROL 接続をテスト]** アイコン。

   ![アセットレプリケーション設定の確認](assets/test-integration4.png)

   *テストパッケージが正常に配信された*&#x200B;ことを示すメッセージが表示されます。

   ![テスト確認出力](assets/test-integration5.png)

1. 4 つのレプリケーションエージェントすべてでテスト結果を確認します。


   >[!NOTE]
   >
   >どのレプリケーションエージェントも無効にしないでください。一部のアセットのレプリケーション（キューで実行中）が失敗する可能性があります。
   >
   >タイムアウトエラーを避けるために、4 つのレプリケーションエージェントすべてが設定されていることを確認します。[Brand Portal への並列公開における問題のトラブルシューティング](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/troubleshoot-parallel-publishing.html?lang=ja#connection-timeout)を参照してください。
   >
   >自動生成された設定は変更しないでください。

次の操作が可能になっています。

* [AEM Assets から Brand Portal へのアセットの公開](../assets/brand-portal-publish-assets.md)
* [Brand Portal から AEM Assets への公開](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html?lang=ja) - Brand Portal でのアセットのソーシング
* [AEM Assets から Brand Portal へのフォルダーの公開](../assets/brand-portal-publish-folder.md)
* [AEM Assets から Brand Portal へのコレクションの公開](../assets/brand-portal-publish-collection.md)
* [Brand Portal へのプリセット、スキーマ、ファセットの公開](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html?lang=ja)
* [Brand Portal へのタグの公開](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html?lang=ja)

詳しくは、 [Brand Portalドキュメント](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html?lang=ja) を参照してください。


## 設定のアップグレード {#upgrade-integration-65}

既存の設定をAdobe Developer Console にアップグレードするには、一覧に表示された順序で次の手順を実行します。

1. [実行中のジョブの検証](#verify-jobs)
1. [既存の設定を削除](#delete-existing-configuration)
1. [設定の作成](#configure-new-integration-65)

### 実行中のジョブの検証 {#verify-jobs}

編集をおこなう前に、公開ジョブがAEM Assetsオーサーインスタンスで実行されていないことを確認してください。 そのため、4 つのレプリケーションエージェントすべてでアクティブジョブのステータスを確認し、キューがアイドル状態であることを確認できます。

1. AEM Assetsオーサーインスタンスにログインします。

1. **ツール**&#x200B;の![ツール](assets/do-not-localize/tools.png)パネルで、**[!UICONTROL デプロイメント]**／**[!UICONTROL デプロイメントレプリケーション]**&#x200B;に移動します。

1. レプリケーションページで、 **[!UICONTROL 作成者のエージェント]**.

   ![アセットのレプリケーションエージェント](assets/test-integration2.png)

1. Brand Portal テナントのレプリケーションエージェントを見つけます。

   次の点を確認します。 **キューは待機中です** すべてのレプリケーションエージェントに対して実行され、アクティブな公開ジョブはありません。

   ![レプリケーションキューの設定](assets/test-integration3.png)

### 既存の設定を削除 {#delete-existing-configuration}

既存の設定の削除時に、次のチェックリストを実行します。

* 4 つのレプリケーションエージェントをすべて削除
* Brand Portal Cloud Service の削除
* Macユーザーを削除

1. AEM Assetsオーサーインスタンスにログインし、CRX Lite を管理者として開きます。 デフォルトの URL は `http://localhost:4502/crx/de/index.jsp` です。

1. `/etc/replications/agents.author` に移動して、Brand Portal テナントの 4 つのレプリケーションエージェントをすべて削除します。

   ![CRXDE のレプリケーションエージェント](assets/delete-replication-agent.png)

1. `/etc/cloudservices/mediaportal` に移動して、Brand Portal クラウドサービス設定を削除します。

   ![CRXDE でのレプリケーションエージェントの詳細](assets/delete-cloud-service.png)

1. に移動します。 `/home/users/mac` をクリックし、 **Macユーザー** Brand Portalテナントの

   ![CRXDE でのレプリケーションエージェントの詳細](assets/delete-mac-user.png)


次の操作を実行できます。 [設定の作成](#configure-new-integration-65) AEM 6.5 オーサーインスタンス上のAdobe Developerコンソールを介して



<!--
   Comment Type: draft

   <li> </li>
   -->

<!--
   Comment Type: draft

   <li>Step text</li>
   -->
