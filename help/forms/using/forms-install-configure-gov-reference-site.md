---
title: We.GovおよびWe.Financeリファレンスサイトのセットアップと設定
seo-title: Set up and configure We.Gov reference site
description: AEM Formsデモパッケージをインストール、設定、カスタマイズします。
seo-description: Install, configure, and customize an AEM Forms demo package.
uuid: 0a6ad8f9-0d38-40c3-ad8d-e705edef55f8
contentOwner: anujkapo
discoiquuid: fe5da0aa-d3a8-4b77-a447-9e429fdc2816
docset: aem65
exl-id: 1fee474e-7da5-4ab2-881a-34b8e055aa29
source-git-commit: 1def8ff7bc90e2ab82ce8b50277a97da9709c78c
workflow-type: tm+mt
source-wordcount: '4703'
ht-degree: 4%

---

# We.GovおよびWe.Financeリファレンスサイトのセットアップと設定 {#set-up-and-configure-we-gov-reference-site}

## デモパッケージの詳細 {#demo-package-details}

### インストールの前提条件 {#installation-prerequisites}

このパッケージは&#x200B;**AEM Forms 6.4 OSGI Author**&#x200B;用に作成され、テスト済みです。そのため、次のプラットフォームバージョンでサポートされています。

| AEM VERSION | AEM Forms PACKAGE VERSION | ステータス |
|---|---|---|
| 6.4 | 5.0.86 | **サポート対象** |
| 6.5 | 6.0.80 | **サポート対象** |
| 6.5.3 | 6.0.122 | **サポート対象** |

このパッケージには、次のプラットフォームバージョンをサポートするクラウド設定が含まれています。

| クラウドプロバイダー | サービスバージョン | ステータス |
|---|---|---|
| Adobe Sign | v5 API | **サポート対象** |
| Microsoft Dynamics 365 | 1710(9.1.0.3020) | **サポート対象** |
| Adobe Analytics | v1.4 Rest API | **サポート対象** |
**パッケージのインストールに関する考慮事項：**

* パッケージは、他のデモパッケージや古いデモパッケージバージョンがないクリーンなサーバーにインストールされる予定です
* パッケージは、オーサーモードで実行されているOSGiサーバーにインストールされる必要があります

### このパッケージの内容 {#what-does-this-package-include}

[AEM Forms We.Govデモパッケージ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/we-gov-forms.pkg.all-2.0.2.zip)(**we-gov-forms.pkg.all-&lt;version>.zip**)は、他のサブパッケージおよびサービスを含むパッケージとして提供されます。 このパッケージには、次のモジュールが含まれています。

* **we-gov-forms.pkg.all-&lt;version>.zip**  — 完全なデモパッ *ケージ*

   * **we-gov-forms.ui.apps-&lt;version>.zip** *— すべてのコンポーネント、クライアントライブラリ、サンプルユーザー、ワークフローモデルなどが含まれます。*

      * **we-gov-forms.core-&lt;version>.jar**  — すべてのOSGIサービス、カスタムワークフローステップ実装などが含まれま *す。*

      * **we-gov-forms.derby&lt;version>.jar**  -  *すべてのOSGIサービス、データベーススキーマなどが含まれます。*

      * **core.wcm.components.all-2.0.4.zip**  - WCMコンポー *ネントのサンプルのコレクション*

      * **grid-aem.ui.apps-1.0-SNAPSHOT.zip**  — サイトページ列制御用の *AEM Sites Gridレイアウトパッケージ*
   * **we-gov-forms.ui.content-&lt;version>.zip**  — コンテンツ、ペー *ジ、画像、フォーム、インタラクティブ通信アセットなど、すべてが含まれます。*

   * **we-gov-forms.ui.analytics-&lt;version>.zip**  — リポジトリ内に *保存されるすべてのWe.Gov Forms Analyticsデータが含まれます。*

   * **we-gov-forms.config.public-&lt;version>.zip**  — フォームデータモデルやサービスバインディングの問題を回避するために、プレースホルダークラウド設定を含むすべてのデフォルト設定ノードが含まれま *す。*


このパッケージに含まれるアセットには、次のものが含まれます。

* 編集可能なテンプレートを使用したAEM Site Pages
* AEM Forms Adaptive Forms
* AEM Forms Interactive Communications（印刷チャネルとWebチャネル）
* AEM Forms XDP Document of Record
* AEM Forms MS Dynamics Formsデータモデル
* Adobe Sign統合
* AEM Workflow Model
* AEM Assetsサンプル画像
* サンプル（メモリ内）Apache Derbyデータベース
* Apache Derbyデータソース（フォームデータモデルで使用）

## デモパッケージのインストール {#demo-package-installation}

この節では、デモパッケージのインストールに関する情報を説明します。

### ソフトウェア配布から {#from-software-distribution}

1. [ソフトウェア配布](https://experience.adobe.com/downloads)を開きます。ソフトウェア配布にログインするには、Adobe ID が必要です。
1. ヘッダーメニューで「**[!UICONTROL Adobe Experience Manager]**」をタップします。
1. 「**[!UICONTROL フィルター]**」セクションで、
   1. 「**[!UICONTROL ソリューション]**」ドロップダウンリストから「**[!UICONTROL Forms]**」を選択します。
   2. パッケージのバージョンとタイプを選択します。 **[!UICONTROL ダウンロードの検索]**&#x200B;オプションを使用して、結果をフィルターすることもできます。
1. パッケージ名&#x200B;**we-gov-forms.pkg.all-&lt;version>.zip**&#x200B;をタップし、「**[!UICONTROL EULA利用条件]**&#x200B;に同意して、「**[!UICONTROL ダウンロード]**」をタップします。
1. [パッケージマネージャー](https://docs.adobe.com/content/help/ja/experience-manager-65/administering/contentmanagement/package-manager.html)を開き「**[!UICONTROL パッケージをアップロード]**」をクリックしてパッケージをアップロードします。
1. パッケージを選択し、「**[!UICONTROL インストール]**」をクリックします。

   ![we gov formsパッケージ](assets/wegov_forms_package.jpg)

1. インストールプロセスを完了する。
1. *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html?wcmmode=disabled*&#x200B;に移動して、インストールが成功したことを確認します。

### ローカルZIPファイルから {#from-a-local-zip-file}

1. **we-gov-forms.pkg.all-&lt;version>.zip**&#x200B;ファイルをダウンロードして見つけます。
1. *https://&lt;aemserver>:&lt;port>/crx/packmgr/index.jsp*&#x200B;に移動します。
1. 「パッケージをアップロード」オプションを選択します。

   ![パッケージのアップロードオプション](assets/upload_package.jpg)

1. ファイルブラウザーを使用して、ダウンロードしたZIPファイルに移動し、選択します。
1. 「開く」をクリックしてアップロードします。
1. アップロードが完了したら、「インストール」オプションを選択してパッケージをインストールします。

   ![WeGov Formsパッケージのインストール](assets/wegov_forms_package-1.jpg)

1. インストールプロセスを完了する。
1. *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html?wcmmode=disabled*&#x200B;に移動して、インストールが成功したことを確認します。

### 新しいパッケージバージョンのインストール {#installing-new-package-versions}

新しいパッケージバージョンをインストールするには、4.1と4.2で定義されている手順に従います。新しいパッケージバージョンをインストールすると、別の古いパッケージが既にインストールされますが、最初に古いパッケージバージョンをアンインストールすることをお勧めします。 それには、次の手順に従います。

1. *https://&lt;aemserver>:&lt;port>/crx/packmgr/index.jsp*&#x200B;に移動します。
1. 古い&#x200B;**we-gov-forms.pkg.all-&lt;version>.zip**&#x200B;ファイルを見つけます。
1. 「詳細」オプションを選択します。
1. ドロップダウンから「アンインストール」オプションを選択します。

   ![WeGovパッケージのアンインストール](assets/uninstall_wegov_forms_package.jpg)

1. 確認時に、「アンインストール」を再度選択し、アンインストールプロセスを完了させます。

## デモパッケージの設定 {#demo-package-configuration}

この節では、プレゼンテーション前のデモパッケージのデプロイ後の設定の詳細と手順について説明します。

### 架空のユーザー設定 {#fictional-user-configuration}

1. *https://&lt;aemserver>:&lt;port>/libs/granite/security/content/groupadmin.html*&#x200B;に移動します。
1. 以下のタスクを実行するには、管理者としてログインします。
1. ページの末尾まで下にスクロールし、すべてのユーザーグループを読み込みます。
1. 「**workflow**」を検索します。
1. 「**workflow-users**」グループを選択し、「プロパティ」をクリックします。
1. 「メンバー」タブに移動します。
1. 「ユーザーまたはグループを選択」フィールドに&#x200B;**wegov**&#x200B;と入力します。
1. 「**We.Gov Forms Users**」ドロップダウンから選択します。

   ![ワークフローユーザーのグループ設定の編集](assets/edit_group_settings.jpg)

1. メニューバーの「保存して閉じる」をクリックします。
1. 手順2～7を繰り返し、「**analytics**」を検索し、「**Analytics Administrators**」グループを選択して、「**We.Gov Forms Users**」グループをメンバーとして追加します。
1. 手順2～7を繰り返し、「**forms users**」を検索し、「**forms-power-users**」グループを選択して、「**We.Gov Forms Users**」グループをメンバーとして追加します。
1. 手順2～7を繰り返し、「**forms-users**」を検索し、「**forms-users**」グループを選択して、次に「**We.Gov Users**」グループをメンバーとして追加します。

### 電子メールサーバーの設定 {#email-server-configuration}

1. セットアップドキュメント[電子メール通知の設定](/help/sites-administering/notification.md)を確認します。
1. このタスクを実行するには、管理者としてログインします。
1. *https://&lt;aemserver>:&lt;port>/system/console/configMgr*&#x200B;に移動します。
1. 設定する&#x200B;**Day CQ Mail Service**&#x200B;サービスを探してクリックします。

   ![Day CQ 電子メールサービスの設定](assets/day_cq_mail_service.jpg)

1. 任意のSMTPサーバーに接続するようにサービスを設定します。

   1. **SMTPサーバーのホスト名**:例：(smtp.gmail.com)
   1. **サーバーポート**:例：SSLを使用するgmailの場合は(465)
   1. **SMTPユーザー：** demo@  &lt;companyname> .com
   1. **差出人のアドレス**:aemformsdemo@adobe.com

   ![SMTPの設定](assets/configure_smtp.jpg)

1. 「保存」をクリックして設定を保存します。

### （オプション）AEM SSL設定 {#aemsslconfig}

この節では、 AEMインスタンスでSSLを設定して、Adobe Sign Cloudを設定する方法について詳しく説明します。

**参照:**

1. [デフォルトの SSL](/help/sites-administering/ssl-by-default.md)

**備考:**

1. https://&lt;aemserver>:&lt;port>/aem/inboxに移動します。ここで、前述の参照ドキュメントリンクで説明されているプロセスを完了できます。
1. `we-gov-forms.pkg.all-[version].zip`パッケージには、サンプルのSSLキーと、パッケージの一部である`we-gov-forms.pkg.all-[version].zip/ssl`フォルダーを展開してアクセスできる証明書が含まれています。

1. SSL証明書およびキーの詳細：

   1. 「CN=localhost」に対して発行される
   1. 10年間の有効性
   1. 「password」のパスワード値
1. 秘密鍵は&#x200B;*localhostprivate.der*&#x200B;です。
1. 証明書は&#x200B;*localhost.crt*&#x200B;です。
1. 「次へ」をクリックします。
1. HTTPSホスト名は&#x200B;*localhost*&#x200B;に設定する必要があります。
1. ポートは、システムが公開しているポートに設定する必要があります。

### （オプション）Adobe Signクラウド設定 {#adobe-sign-cloud-configuration}

この節では、 Adobe Sign Cloud設定の詳細と手順について説明します。

**参照:**

1. [Adobe Sign の AEM Forms への統合](adobe-sign-integration-adaptive-forms.md)

#### クラウド設定 {#cloud-configuration}

1. 前提条件を確認します。 必要なSSL設定については、[AEM SSL設定](../../forms/using/forms-install-configure-gov-reference-site.md#aemsslconfig)を参照してください。
1. 次の URL に移動します。

   *https://&lt;aemserver>:&lt;port>/libs/adobesign/cloudservices/adobesign.html/conf/we-gov*

   >[!NOTE]
   >
   >設定の問題(例：*https://&lt;aemserver>:&lt;port>/mnt/overlay/adobesign/cloudservices/adobesign/properties.html*)

1. 「We.gov Adobe Sign」設定を選択します。
1. 「プロパティ」をクリックします。
1. 「設定」タブに移動します。
1. oAuth URLを入力します。例：[https://secure.na1.echosign.com/public/oauth](https://secure.na1.echosign.com/public/oauth)
1. 設定済みのAdobe Signインスタンスから、設定済みのクライアントIDとクライアント秘密鍵を指定します。
1. 「Adobe Signに接続」をクリックします。
1. 接続に成功したら、「保存して閉じる」をクリックして統合を完了します。

### （オプション）MS Dynamicsクラウド設定 {#ms-dynamics-cloud-configuration}

この節では、MS Dynamicsクラウド設定の詳細と手順について説明します。

**参照:**

1. [Microsoft Dynamics OData の設定](https://docs.adobe.com/content/help/en/experience-manager-64/forms/form-data-model/ms-dynamics-odata-configuration.html)
1. [AEM Forms用のMicrosoft Dynamicsの設定](https://helpx.adobe.com/experience-manager/kt/forms/using/config-dynamics-for-aem-forms.html)

#### MS Dynamics ODataクラウドサービス {#ms-dynamics-odata-cloud-service}

1. 次の URL に移動します。

   https://&lt;aemserver>:&lt;port>/libs/fd/fdm/gui/components/admin/fdmcloudservice/fdm.html/conf/we-gov

   1. MS Dynamicsアプリケーションの登録で設定したのと同じリダイレクトURLを使用してサーバーにアクセスしていることを確認してください。

1. 「Microsoft Dynamics ODataCloud Service」設定を選択します。
1. 「プロパティ」をクリックします。

   ![Microsoft ODataCloud Serviceのプロパティ](assets/properties_odata_cloud_service.jpg)

1. 「認証設定」タブに移動します。
1. 以下の詳細を入力します。

   1. **サービスルート：** 例：  `https://msdynamicsserver.api.crm3.dynamics.com/api/data/v9.1/`
   1. **認証の種類：** OAuth 2.0
   1. **認証設定** (この情報を収 [集するため](../../forms/using/forms-install-configure-gov-reference-site.md#dynamicsconfig) のMS Dynamicsクラウド設定を参照):

      1. クライアントID — アプリケーションIDとも呼ばれます
      1. クライアントの秘密鍵
      1. OAuth URL — 例：[https://login.windows.net/common/oauth2/authorize](https://login.windows.net/common/oauth2/authorize)
      1. 更新トークンURL — 例：[https://login.windows.net/common/oauth2/token](https://login.windows.net/common/oauth2/token)
      1. アクセストークンURL（例： ）[https://login.windows.net/common/oauth2/token](https://login.windows.net/common/oauth2/token)
      1. 承認スコープ — **openid**
      1. 認証ヘッダー — **Authorization Bearer**
      1. リソース — 例： `https://msdynamicsserver.api.crm3.dynamics.com`
   1. 「OAuthに接続」をクリックします。


1. 認証が正常に完了したら、「保存して閉じる」をクリックして統合を完了します。

#### MS Dynamicsクラウド設定 {#dynamicsconfig}

この節で説明する手順は、MS Dynamics CloudインスタンスからクライアントID、クライアント秘密鍵、および詳細を探すのに役立ちます。

1. [https://portal.azure.com/](https://portal.azure.com/)に移動してログインします。
1. 左側のメニューから、「All Services」を選択します。
1. 「アプリ登録」を検索または移動します。
1. 既存のアプリケーション登録を作成または選択します。
1. AEMクラウド設定のOAuth **クライアントID**&#x200B;として使用する&#x200B;**アプリケーションID**&#x200B;をコピーします
1. 「設定」または「マニフェスト」をクリックして、**応答URLを設定します。**

   1. このURLは、ODataサービスを設定する際に、AEMサーバーにアクセスするために使用されるURLと一致する必要があります。

1. 設定ビューで、「キー」をクリックして、新しいキーを作成します( AEMのクライアント秘密鍵として使用されます)。

   1. 後でAzureまたはAEMで表示できないので、キーのコピーを保持してください。

1. リソースURL/サービスルートURLを見つけるには、「 MS Dynamicsインスタンス」ダッシュボードに移動します。
1. 上部ナビゲーションバーで、「Sales」または独自のインスタンスタイプをクリックし、「設定を選択」をクリックします。
1. 右下の「カスタマイズ」と「開発者向けリソース」をクリックします。
1. 次に、サービスルートURLを示します。例：

   * など、特定の拡張子をファイル名に持つファイル。`https://msdynamicsserver.api.crm3.dynamics.com/api/data/v9.1/`

1. 更新およびアクセストークンのURLについて詳しくは、以下を参照してください。

   *[https://docs.microsoft.com/en-us/rest/api/datacatalog/authenticate-a-client-app](https://docs.microsoft.com/en-us/rest/api/datacatalog/authenticate-a-client-app)*

#### Formsデータモデル(Dynamics)のテスト {#testing-the-form-data-model}

クラウド設定が完了したら、フォームデータモデルをテストする必要が生じる場合があります。

1.  に移動します。

   *https://&lt;aemserver>:&lt;port>/aem/forms.html/content/dam/formsanddocuments-fdm/we-gov*

1. 「We.gov Microsoft Dynamics CRM FDM」を選択し、「プロパティ」を選択します。

   ![Dynamics CRM FDMのプロパティ](assets/properties_dynamics_crm.jpg)

1. 「ソースを更新」タブに移動します。
1. 「コンテキスト対応設定」が「/conf/we-gov」に設定され、設定済みのデータソースが「ms-dynamics-odata-cloud-service」であることを確認します。

   ![設定済みデータソース](assets/configured_data_source.jpg)

1. フォームデータモデルを編集します。

1. サービスをテストして、設定済みのデータソースに接続できることを確認します。

   >[!NOTE]
   サービスをテストした後、「**キャンセル**」をクリックし、不随意の変更がフォームデータモデルに反映されないようにします。

   >[!NOTE]
   データ・ソースをFDMに正常にバインドするには、AEM Serverの再起動が必要であったと報告されています。

#### Formsデータモデルのテスト(Derby) {#test-fdm-derby}

クラウドの設定が完了したら、フォームデータモデルをテストする必要が生じる場合があります。

1. *https://&lt;aemserver>:&lt;port>/aem/forms.html/content/dam/formsanddocuments-fdm/we-gov*&#x200B;に移動します。

1. **We.gov Enrollment FDM**&#x200B;を選択し、**Properties**&#x200B;を選択します。

   ![Dynamics CRM FDMのプロパティ](assets/aftia-enrollment-fdm.jpg)

1. 「**ソースを更新**」タブに移動します。

1. **コンテキスト対応設定**&#x200B;が`/conf/we-gov`に設定され、設定済みのデータソースが&#x200B;**We.Gov Derby DS**&#x200B;であることを確認します。

   ![Dynamics CRM FDMのプロパティ](assets/aftia-update-data-source.jpg)

1. 「**保存して閉じる**」をクリックします。

1. [サービスをテ](work-with-form-data-model.md#test-data-model-objects-and-services) ストし、設定済みのデータソースに正常に接続できることを確認します。

   * 接続をテストするには、**HOMEMORTGAGEACCOUNT**&#x200B;を選択し、getサービスを指定します。 サービスおよびシステム管理者が、取得中のデータを確認できるかどうかをテストします。

### Adobe Analytics設定（オプション） {#adobe-analytics-configuration}

この節では、Adobe Analytics Cloud設定の詳細と手順について説明します。

**参照:**

* [Adobe Analytics との統合](../../sites-administering/adobeanalytics.md)

* [Adobe Analytics への接続とフレームワークの作成](../../sites-administering/adobeanalytics-connect.md)

* [ページ分析データの表示](../../sites-authoring/pa-using.md)

* [Analytics とレポートの設定](configure-analytics-forms-documents.md)

* [AEM Forms の分析レポートの確認方法と詳細](view-understand-aem-forms-analytics-reports.md)

### Adobe Analyticsクラウドサービスの設定 {#adobe-analytics-cloud-service-configuration}

このパッケージは、Adobe Analyticsに接続するように事前に設定されています。 この設定を更新するために、以下の手順を実行します。

1. *https://&lt;aemserver>:&lt;port>/libs/cq/core/content/tools/cloudservices.html*&#x200B;に移動します。
1. Adobe Analyticsセクションを探し、「設定を表示」リンクを選択します。
1. 「We.Gov Adobe Analytics (Analytics Configuration)」設定を選択します。

   ![Analyticsクラウドサービスの設定](assets/analytics_config.jpg)

1. 「編集」ボタンをクリックして、Adobe Analytics設定を更新します（共有暗号鍵を指定する必要があります）。 「Analyticsに接続」をクリックして接続し、「OK」をクリックして完了します。

   ![We.GovAdobe Analytics](assets/wegov_adobe_analytics.jpg)

1. フレームワーク設定を更新する場合は、同じページで「We.Gov Adobe Analytics Framework (Analytics Framework)」をクリックします(オーサリングを有効にするには、「[AEMオーサリングを有効にする](../../forms/using/forms-install-configure-gov-reference-site.md#enableauthoring)」を参照)。

#### Adobe Analyticsユーザー資格情報の検索 {#analytics-locating-user-credentials}

Adobe Analyticsアカウントのユーザー資格情報を探すには、アカウント管理者が次のタスクを実行する必要があります。

1. Adobe Experience Cloudポータルに移動します。
   * 管理者の資格情報を使用してログインします。
1. メインダッシュボードでAdobe Analyticsアイコンを選択します。
   ![迅速なアクセス](assets/aftia-quick-access.jpg)
1. 「管理者」タブに移動し、「ユーザー管理（レガシー） 」項目を選択します
   ![レポート](assets/aftia-reports.jpg)
1. 「**ユーザー**」タブを選択します。
   ![ユーザー管理](assets/aftia-user-management.jpg)
1. ユーザーのリストから目的のユーザーを選択します。
1. ページの下部までスクロールすると、ユーザーの認証情報がページの下部に表示されます。
   ![アクセスを管理](assets/aftia-admin-user-access.jpg)
1. ユーザー名と共有暗号鍵の情報が、権限ボックスの右側に表示されます。
1. ユーザー名には、名前の中にコロンが含まれ、コロンの左側にあるすべての情報はユーザー名で、コロンの右側にある情報はすべて会社名です。
   * 次に例を示します。*ユーザー名：会社名*

#### Adobe Analyticsでのユーザー認証の設定 {#setup-user-authentication}

管理者は、次の操作を実行して、AEM Analyticsの権限をユーザーに付与できます。

1. Adobe Admin Consoleに移動します。

1. Admin Consoleに表示されるAnalyticsインスタンスをクリックします。

   * これは、管理ページのメインページにあります。

1. 「 Analyticsの完全な管理者アクセス」を選択します。

1. ユーザーをプロファイルに追加します。

   ![Analyticsの完全な管理者アクセス](assets/aftia-full-admin-access.jpg)

1. ユーザーIDがプロファイルにマッピングされたら、「権限」タブをクリックします。

1. すべての権限がプロファイルにマッピングされていることを確認します。

   ![権限の編集](assets/aftia-admin-access-edit.jpg)

1. ユーザーのログイン機能に関して権限がマッピングされると、数時間かかる場合があります。

### Adobe Analyticsレポート {#adobe-analytics-reporting}

#### Adobe Analytics Sitesレポートの表示 {#view-adobe-analytics-sites-reporting}

>[!NOTE]
AEM Forms Analyticsのデータは、オフライン時に、または`we-gov-forms.ui.analytics-<version>.zip`パッケージがインストールされている場合にAdobe Analyticsクラウド設定なしで使用できますが、AEM Sitesのデータにはアクティブなクラウド設定が必要です。

1. *https://&lt;aemserver>:&lt;port>/sites.html/content*&#x200B;に移動します。
1. 「AEM Forms We.Gov Site」を選択して、サイトのページを表示します。
1. サイトページの1つ（例：ホーム）を選択し、「Analytics &amp; Recommendations」を選択します。

   ![分析とRecommendations](assets/analytics_recommendations.jpg)

1. このページには、AEM Sitesページに関連する、Adobe Analyticsから取得した情報が表示されます(注意：デザインにより、この情報はAdobe Analyticsから定期的に更新され、リアルタイムには表示されません)。

   ![AEM Sites分析](assets/sites_analysis.jpg)

1. （手順3.でアクセスした）ページビューページに戻ると、「リスト表示」で項目を表示するように表示設定を変更して、ページビュー情報を表示することもできます。
1. 「表示」ドロップダウンメニューを探し、「リスト表示」を選択します。

   ![リスト表示](assets/list_view.jpg)

1. 同じメニューから「設定を表示」を選択し、「Analytics」セクションから表示する列を選択します。

   ![列の設定](assets/configure_columns.jpg)

1. 「更新」をクリックして、新しい列を使用可能にします。

   ![新しい列の表示](assets/new_columns_display.jpg)

#### Adobe Analytics formsレポートの表示 {#view-adobe-analytics-forms-reporting}

>[!NOTE]
AEM Forms Analyticsのデータは、オフライン時に、または`we-gov-forms.ui.analytics-<version>.zip`パッケージがインストールされている場合にAdobe Analyticsクラウド設定なしで使用できますが、AEM Sitesのデータにはアクティブなクラウド設定が必要です。

1.  に移動します。

   *https://&lt;aemserver>:&lt;port>/aem/forms.html/content/dam/formsanddocuments/adobe-gov-forms*

1. 「Enrollment Application For Health Benefits」アダプティブフォームを選択し、「Analyticsレポート」オプションを選択します。

   ![Analyticsレポート](assets/analytics_report.jpg)

1. ページが読み込まれ、Analyticsレポートデータが表示されます。

   ![Analyticsレポートデータの表示](assets/analytics_report_data.jpg)

### Adobe自動Forms設定の有効化 {#automated-forms-enablement}

FormsAdobeと共にAEM Formsをインストールして設定するには、コンバージョンツールのユーザーが以下をおこなう必要があります。

1. Adobe I/O

1. Formsコンバージョンサービスとの統合を作成するAdobe。

1. AdobeAEM 6.5の最新のサービスパックがオーサーとして実行されている。

詳しい手順を読む前に、次の点を確認してください。

* [自動フォーム変換サービスの設定](https://docs.adobe.com/content/help/en/aem-forms-automated-conversion-service/using/configure-service.html)

#### IMS設定の作成パート1 {#creating-ims-config}

フォーム変換ツールと正しく通信するようにサービスを設定するには、ユーザーがIdentity Management System(IMS)サービスをAdobe I/Oに登録できるように設定する必要があります。

1. https://&lt;aemserver>:&lt;port>に移動し、「Adobe Experience」をクリックします。
左上のマネージャー/ツール/セキュリティ/Adobe IMS設定

1. 「作成」をクリックします。

1. 以下の画像のアクションを実行します。

   ![IMSテクニカルアカウント設定](assets/aftia-technical-account-configuration.jpg)

1. 必ず証明書をダウンロードしてください。

1. 設定の残りの部分は続行しないでください — 「Adobe I/Oでの統合の作成」の節[を確認してください。](#create-integration-adobeio)

>[!NOTE]
この節で作成した証明書は、統合サービスの作成にAdobe I/Oされます。統合サービスでユーザーが作成された情報は、Adobe I/Oから使用して設定を完了できます。

#### 統合の作成Adobe I/O {#create-integration-adobeio}

Adobe管理者に問い合わせない場合は、システムドメイン内で統合を作成する権限を持っていることを確認してください。

1. [Adobe I/Oコンソール](https://console.adobe.io/)に移動します。

1. 「統合を作成」をクリックします。

1. 「 APIにアクセス」を選択します。

1. 正しいグループ（右上のドロップダウンリスト）に属していることを確認します。

1. 「Experience Cloud」セクションで、Forms変換ツールを選択します。

1. 「続行」をクリックします。

1. 統合の名前と説明を入力します。

1. セクション2.1の公開鍵を使用して、鍵の統合内に配置します。

1. automated forms conversion

   ![新しい統合の作成](assets/aftia-create-new-integration.jpg)

#### IMS設定の作成パート2 {#create-ims-config-part-next}

これで、統合が作成され、IMS設定のインストールを完了できます。

1. 接続の詳細を表示するには、Adobe I/O内の統合をクリックします。

1. AEM（ツール/セキュリティ/IMS）内でIMS設定に移動します。

1. IMS設定画面で「次へ」をクリックします。

1. 認証サーバー（スクリーンショットに表示されている値）を入力します。

1. APIキーを入力します。

1. クライアントの秘密鍵を入力します(表示するには、「統合」Adobe I/Oで「公開」をクリックする必要があります)。

1. 「 JWT 」タブをクリックして、JWTAdobe I/Oを取得し、IMS設定のペイロードに貼り付けます。

   ![ペイロードIMS設定](assets/aftia-payload-ims-config.jpg)

1. 作成したら、「IMS設定」をクリックし、「ヘルスチェック」を選択すると、次の結果が表示されます。

   ![正常性確認](assets/aftia-health-confirmation.jpg)

#### クラウド設定（We.Gov AFC実稼動）の設定 {#configure-cloud-configuration}

IMSの設定が完了したら、AEMでクラウド設定を確認する必要があります。 設定が存在しない場合は、次の手順を使用してAEMでクラウド設定を作成します。

1. ブラウザーを開き、システムURL https://&lt;domain_name>:&lt;system_port>に移動します。

1. 画面の左上隅にあるAdobe Experience Manager/ツール/Cloud Services/自動Forms会話設定をクリックします。

1. 設定を配置する設定フォルダーを選択します。

1. 「作成」をクリックします。

1. 以下のスクリーンショットに情報を入力します。

   ![AFC実稼動](assets/aftia-afc-production.jpg)

1. 「タイトル」と「名前」を設定に指定します。

1. システムのサービスURLはhttps://aemformsconversion.adobe.io/に設定されます。

1. テンプレートURL */conf/we-gov/settings/wcm/templates/we-gov-flamingo-template*。

1. テーマURL:*/content/dam/formsanddocuments-themes/adobe-gov-forms-themes/we-gov-theme*

1. 「次へ」をクリックします。

1. この設定の場合、2つのチェックボックス値は空のままにします。

   * これらのオプションについて詳しくは、[クラウドサービスの設定](https://docs.adobe.com/content/help/en/aem-forms-automated-conversion-service/using/configure-service.html#configure-the-cloud-service)を参照してください。

#### クラウド設定（We.Finance AFC実稼動）の設定 {#configure-cloud-configuration-wefinance}

IMSの設定が完了したら、AEMでクラウド設定を作成する作業に進むことができます。

1. ブラウザーを開き、システムURL https://&lt;domain_name>:&lt;system_port>に移動します。

1. 画面の左上隅にあるAdobe Experience Manager/ツール/Cloud Services/自動Forms会話設定をクリックします。

1. 設定を配置する設定フォルダーを選択します。

1. 「作成」をクリックします。

1. 以下のスクリーンショットに情報を入力します。

   ![We.Finance AFC Production](assets/aftia-wefinance-afc-prod.jpg)

1. 「タイトル」と「名前」を設定に指定します。

1. システムのサービスURLはhttps://aemformsconversion.adobe.io/に設定されます。

1. テンプレートURL:*/conf/we-finance/settings/wcm/templates/we-finance-adaptive-form*

1. テーマURL:*/content/dam/formsanddocuments-themes/adobe-finance-forms-themes/we-finance-theme*

1. 「次へ」をクリックします。

1. この設定の場合、2つのチェックボックス値は空のままにします。

   * これらのオプションについて詳しくは、[クラウドサービスの設定](https://docs.adobe.com/content/help/en/aem-forms-automated-conversion-service/using/configure-service.html#configure-the-cloud-service)を参照してください。

#### フォーム変換のテスト(We.Gov Enrollment Application) {#test-forms-conversion}

設定が完了したら、PDFドキュメントをアップロードしてテストできます。

1. AEMシステムhttps://&lt;domain_name>:&lt;system_port>に移動します。

1. Forms / Formsとドキュメント/ AEM Forms We.gov Forms / AFCをクリックします。

1. We.Gov Enrollment Application PDFを選択します。

1. 右上隅の「**自動コンバージョンを開始**」ボタンをクリックします。

1. ユーザーは、次に示すように、オプションを表示できます。

   ![変換後のアダプティブフォーム](assets/aftia-converted-adaptive-form.jpg)

1. ボタンを選択すると、次のオプションが表示されます

   * ユーザーが&#x200B;*We.Gov AFC Production*&#x200B;設定を選択していることを確認します。

   ![変換設定](assets/aftia-conversion-settings.jpg)

   ![詳細な変換設定](assets/aftia-conversion-settings-2.jpg)

1. 使用するすべてのオプションを設定したら、「変換を開始」を選択します。

1. 変換プロセスが始まると、次の画面が表示されます。

   ![変換設定](assets/aftia-conversion-in-progress.jpg)

1. 変換処理が完了すると、次の画面が表示されます。

   ![変換後のアダプティブフォーム](assets/aftia-converted-adaptive-form-2.jpg)

   **Output**&#x200B;フォルダーをクリックして、生成後のアダプティブフォームを表示します。

#### 既知の問題とメモ {#known-issues-notes}

automated forms conversionサービスには、特定の[ベストプラクティス、既知の複雑なパターン](https://docs.adobe.com/content/help/en/aem-forms-automated-conversion-service/using/styles-and-pattern-considerations-and-best-practices.html)、[既知の問題](https://docs.adobe.com/content/help/en/aem-forms-automated-conversion-service/using/known-issues.html)が含まれます。 AEM FormsAutomated forms conversionサービスの使用を開始する前に、これらを確認してください。

1. 変換後にフォームをFDMにバインドする場合は、「データバインディングが有効になっていないアダプティブフォームを生成」を選択してフォームを生成します。

1. テンプレートフォルダーですべてのユーザーの権限に対してjcr:readが有効になっていることを確認してください。そうしないと、サービスユーザーがリポジトリからテンプレートを読み取れず、変換が失敗します。

## デモパッケージのカスタマイズ {#demo-package-customizations}

この節では、デモのカスタマイズ手順について説明します。

### テンプレートのカスタマイズ {#templates-customization}

編集可能テンプレートは、次の場所にあります。

*https://&lt;aemserver>:&lt;port>/libs/wcm/core/content/sites/templates.html/conf/we-gov*

これらのテンプレートには、AEMサイト、アダプティブフォーム、インタラクティブ通信の各テンプレートが含まれ、次の場所にあるコンポーネントを使用して作成および組み立てられます。

*https://&lt;aemserver>:&lt;port>/crx/de/index.jsp#/apps/we-gov/components*

#### スタイルシステム {#customizetemplates}

このサイトには、Bootstrap4( [https://getbootstrap.com/](https://getbootstrap.com/) )を読み込むクライアントライブラリも備わっています。 このクライアントライブラリは、

*https://&lt;aemserver>:&lt;port>/crx/de/index.jsp#/apps/we-gov/clientlibs/clientlib-base/css/bootstrap*

このパッケージに含まれる編集可能なテンプレートは、ページネーションやスタイル設定などにBootstrap4のCSSクラスを使用するテンプレート/ページポリシーで事前に設定されています。 テンプレートポリシーにすべてのクラスが追加されているわけではありませんが、Bootstrap4でサポートされるクラスはポリシーに追加できます。 使用可能なクラスのリストについては、はじめにのページを参照してください。

[https://getbootstrap.com/docs/4.1/getting-started/introduction/](https://getbootstrap.com/docs/4.1/getting-started/introduction/)

このパッケージに含まれるテンプレートは、スタイルシステムもサポートしています。

[スタイルシステム](../../sites-authoring/style-system.md)

#### テンプレートロゴ {#template-logos}

プロジェクトDAM Assetsには、We.Govのロゴと画像も含まれます。 これらのアセットは、次の場所で使用できます。

*https://&lt;aemserver>:&lt;port>/assets.html/content/dam/we-gov*

ページおよびフォームテンプレートの編集時に、ナビゲーションコンポーネントとフッターコンポーネントを編集してブランドロゴを更新することもできます。 これらのコンポーネントは、ロゴの更新に使用できる、設定可能なブランドとロゴのダイアログを提供します。

![テンプレートロゴ](assets/template_logos.jpg)

詳しくは、ページのコンテンツの編集を参照してください。

[ページのコンテンツの編集](../../sites-authoring/editing-content.md)

### サイトページのカスタマイズ {#sites-pages-customization}

すべてのサイトページは、次の場所から利用できます。*https://&lt;aemserver>:&lt;port>/sites.html/content/we-gov*

これらのサイトページでは、AEM Gridパッケージを使用して、一部のコンポーネントのレイアウトを制御することもできます。

#### スタイルシステム {#style-system}

このパッケージに含まれるページは、スタイルシステムもサポートしています。

[スタイルシステム](../../sites-authoring/style-system.md)

また、サポートされるスタイルに関するドキュメントについては、「[テンプレートカスタマイズスタイルシステム](../../forms/using/forms-install-configure-gov-reference-site.md#customizetemplates)」を参照してください。

### アダプティブフォームのカスタマイズ {#adaptive-forms-customization}

すべてのアダプティブフォームは、次の場所から利用できます。

*https://&lt;aemserver>:&lt;port>/aem/forms.html/content/dam/formsanddocuments/adobe-gov-forms*

これらのフォームは、特定の使用例に合わせてカスタマイズできます。 フォームが引き続き正しく機能するように、特定のフィールドと送信ロジックを変更しないでください。 これには以下が含まれます。

**健康保険給付の登録申請：**

* contact_id — 送信中にMS Dynamicsの連絡先IDを受け取るために使用される非表示のフィールド
* 送信 — コールバックをサポートするために、送信ボタンのロジックにカスタマイズが必要でした。 カスタマイズについては説明していますが、Formsデータモデルを介してPOST操作とGET操作の両方をMS Dynamicsに対して実行する際に、フォームを送信するには大きなスクリプトが必要でした。
* ルートパネル — Initializeイベントは、すべてのAEMインボックスGranite UIコンポーネントが変更不可能なので、可能な限り控えめな方法でMS DynamicsボタンをAEMインボックスに追加するために使用します。

#### アダプティブフォームのスタイル設定 {#adaptive-form-styling}

アダプティブフォームは、スタイルエディターまたはテーマエディターを使用してスタイルを設定することもできます。

* [アダプティブフォームコンポーネントのインラインスタイリング](inline-style-adaptive-forms.md)
* [テーマの作成および使用](themes.md)

### ワークフローのカスタマイズ {#workflow-customization}

登録アダプティブフォームは、処理のためにOSGIワークフローに送信されます。 このワークフローは、*https://&lt;aemserver>:&lt;port>/conf/we-gov/settings/models/we-gov-process.html*&#x200B;にあります。

一部の制限により、このワークフローには、複数のスクリプトとカスタムOSGIワークフロープロセスステップが含まれています。 これらのワークフローステップは、一般的なステップとして作成され、設定ダイアログでは作成されていません。 現時点では、ワークフローステップの設定はプロセス引数に依存します。

すべてのワークフローステップのJavaコードは、**we-gov-forms.core-&lt;version>.jar**&#x200B;バンドルに含まれています。

## デモに関する考慮事項と既知の問題 {#demo-considerations-and-known-issues}

この節では、デモ機能と、デモプロセス中に特別な考慮が必要になる可能性のある設計上の決定に関する情報を説明します。

### デモに関する考慮事項 {#demo-considerations}

* AGRS-159に従い、登録アダプティブフォームで使用する連絡先の名前（最初、中間、最後）が一意であることを確認します。
* 登録アダプティブフォームは、フォームの「電子メール」フィールドに指定された電子メールにAdobe Signの電子メールを送信します。 その電子メールアドレスを、Adobe Signクラウド設定の設定に使用する電子メールと同じ電子メールアドレスにすることはできません。

### 既知の問題 {#known-issues}

* (AGRS-120)サイトナビゲーションコンポーネントは、現在、2レベルを超える深さのネストされた子ページをサポートしていません。
* (AGRS-159)現在のMS Dynamics FDMは、最初に2回の操作を実行し、登録アダプティブフォームのデータをDynamicsにPOSTしてから、連絡先IDを取得するためにユーザーレコードを取得する必要があります。 現在の状態では、同じ名前を持つユーザーがDynamicsに3人以上存在し、登録アダプティブフォームの送信が許可されない場合、連絡先IDの取得が失敗します。

## アクセシビリティテストの設定 {#configure-accessibility-testing}

### アクセシビリティテストChromeアドオンの有効化 {#enable-chrome-add-on}

最初にアクセシビリティテストを実行するには、Chromeプラグインをインストールする必要があります。これは[ここ](https://chrome.google.com/webstore/detail/accessibility-developer-t/fpkknkljclfencbdbgkenhalefipecmb?hl=en)にあります。

インストールが完了したら、Chromeブラウザー内でテストするページを読み込みます(注意：複数のタブを開くと、スコアに影響が及ぶ場合があります（1つのタブだけを開くことをお勧めします）。 ページが読み込まれると
**ページ上の「**」を右クリックし、「 **監査** 」タブを選択します。 開発者は、アクセシビリティプラグインで実行する監査のタイプを選択できます。 必要なオプションをすべて選択したら、「レポートを生成」ボタンを選択できます。 これにより、全体的なアクセシビリティ評価と、全体的なアクセシビリティ評価を上げるために使用できる内容を示すPDFドキュメントが生成されます。

レポートの実行後、次の情報が表示されます。

![アクセシビリティレポート](assets/aftia-accessibility.jpg)

ユーザーの前に表示される数は、取得した全体的なアクセシビリティ評価です。 スコアに続いて、この計算方法に関する説明もあります。

これを書き出す場合は、画面の右側の3つのボタンをクリックし、プラグインが提供するその他のオプションから選択できます。

![アクセシビリティレポート](assets/aftia-accessibility-report.jpg)

### Ultramarineテーマ {#ultramarine-theme}

Adobeが管理するUltramarineテーマは、
`we-gov-forms.pkg.all-<version>.zip`インストール可能なZIPファイル。 CRXを使用してこのパッケージをインストールしたら、

パッケージマネージャーを使用すると、AEM FormsのUltramarineテーマにアクセスできます。そのためには、**Forms** / **テーマ** / **参照テーマ** / **Ultramarine-Accessible**&#x200B;に移動します。

![Ultramarine テーマ](assets/aftia-ultramarine-theme.jpg)

## 設定オプション {#configuration-options}

ユーザーは、次のような様々なワークフローサービスオプションを設定できます。

1. Microsoft Dynamicsエントリ
1. Adobe Sign
1. AEM Custom Communication Management
1. Adobe Analytics

ワークフロー内で有効にするように設定するには、次のタスクを実行する必要があります。

1. https://&#39;[server]:[port]&#39;/system/console/configMgrに移動します。

1. *WeGov Configurations*&#x200B;を探します。

1. サービス定義を開き、選択したサービスをワークフロー内で呼び出せるようにします。

   >[!NOTE]
   ユーザーがConfiguration Managerページ内でサービスを有効にするので、要求された外部サービスと通信するには、ユーザーが引き続きサービス設定を行う必要があります。

   ![we gov formsパッケージ](assets/aftia-configuration-options.jpg)

1. 設定が完了したら、「保存」ボタンをクリックして設定を保存します。

## 次の手順 {#next-steps}

これで、We.Govリファレンスサイトを参照する設定が完了しました。 We.Govリファレンスサイトのワークフローと手順について詳しくは、[We.Govリファレンスサイトのチュートリアル](../../forms/using/forms-gov-reference-site-user-demo.md)を参照してください。
