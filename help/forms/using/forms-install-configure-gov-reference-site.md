---
title: We.Gov および We.Finance リファレンスサイトのセットアップと設定
seo-title: Set up and configure We.Gov reference site
description: AEM Forms デモパッケージをインストール、設定、カスタマイズします。
seo-description: Install, configure, and customize an AEM Forms demo package.
uuid: 0a6ad8f9-0d38-40c3-ad8d-e705edef55f8
contentOwner: anujkapo
discoiquuid: fe5da0aa-d3a8-4b77-a447-9e429fdc2816
docset: aem65
exl-id: 1fee474e-7da5-4ab2-881a-34b8e055aa29
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '4703'
ht-degree: 89%

---

# We.Gov および We.Finance リファレンスサイトのセットアップと設定 {#set-up-and-configure-we-gov-reference-site}

## デモパッケージの詳細 {#demo-package-details}

### インストールの前提条件 {#installation-prerequisites}

このパッケージは、**AEM Forms 6.4 OSGI オーサー**&#x200B;のために作成され、テスト済みで、次のプラットフォームバージョンでサポートされています。

| AEM のバージョン | AEM FORMS パッケージバージョン | ステータス |
|---|---|---|
| 6.4 | 5.0.86 | **サポート対象** |
| 6.5 | 6.0.80 | **サポート対象** |
| 6.5.3 | 6.0.122 | **サポート対象** |

このパッケージには、次のプラットフォームバージョンをサポートするクラウド設定が含まれています。

| クラウドプロバイダー | サービスバージョン | ステータス |
|---|---|---|
| Adobe Sign | v5 API | **サポート対象** |
| Microsoft Dynamics 365 | 1710（9.1.0.3020） | **サポート対象** |
| Adobe Analytics | v1.4 Rest API | **サポート対象** |
**パッケージのインストールに関する考慮事項：**

* このパッケージは、他のデモパッケージや古いデモパッケージバージョンがないクリーンなサーバーにインストールする必要があります
* パッケージは、オーサーモードで実行されている OSGi サーバーにインストールする必要があります。

### このパッケージに含まれる機能 {#what-does-this-package-include}

[AEM Forms We.Gov デモパッケージ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/we-gov-forms.pkg.all-2.0.2.zip)（**we-gov-forms.pkg.all-&lt;version>.zip**）は、他の複数のサブパッケージおよびサービスを含むパッケージとして提供されます。パッケージには次のモジュールが含まれています。

* **we-gov-forms.pkg.all-&lt;version>.zip** - *完全なデモパッケージ*

   * **we-gov-forms.ui.apps-&lt;version>.zip** *- すべてのコンポーネント、クライアントライブラリ、サンプルユーザー、ワークフローモデルなどが含まれます。*

      * **we-gov-forms.core-&lt;version>.jar** - *すべての OSGi サービス、カスタムワークフローステップ実装などが含まれます。*

      * **we-gov-forms.derby&lt;version>.jar** - *すべての OSGi サービス、データベーススキーマなどが含まれます。*

      * **core.wcm.components.all-2.0.4.zip** - *サンプル WCM コンポーネントのコレクション*

      * **grid-aem.ui.apps-1.0-SNAPSHOT.zip** - *Sites ページ列コントロール用の AEM Sites グリッドレイアウトパッケージ*
   * **we-gov-forms.ui.content-&lt;version>.zip** - *すべてのコンテンツ、ページ、画像、フォーム、インタラクティブ通信アセットなどが含まれます。*

   * **we-gov-forms.ui.analytics-&lt;version>.zip** - *リポジトリ内に保存するすべての We.Gov Forms Analytics データが含まれます。*

   * **we-gov-forms.config.public-&lt;version>.zip** - *フォームのデータモデルやサービスの連結の問題を回避するために役立つ、プレースホルダークラウド設定を含むすべてのデフォルト設定ノードが含まれます。*


このパッケージのアセットには、次のものが含まれます。

* 編集可能なテンプレートを使用したAEM Site Pages
* AEM Forms Adaptive Forms
* AEM Forms Interactive Communications（印刷と web チャンネル）
* AEM Forms XDP Document of Record
* AEM Forms MS Dynamics Forms データモデル
* Adobe Sign との統合
* AEM ワークフローモデル
* AEM Assets サンプル画像
* サンプル（メモリ内）Apache Derby データベース
* Apache Derby データソース（フォームデータモデルで使用）

## デモパッケージのインストール {#demo-package-installation}

この節では、デモパッケージのインストールについて説明します。

### ソフトウェア配布から {#from-software-distribution}

1. [ソフトウェア配布](https://experience.adobe.com/jp/downloads)を開きます。ソフトウェア配布にログインするには、Adobe ID が必要です。
1. ヘッダーメニューで「**[!UICONTROL Adobe Experience Manager]**」をタップします。
1. 「**[!UICONTROL フィルター]**」セクションで、
   1. 「**[!UICONTROL ソリューション]**」ドロップダウンリストから「**[!UICONTROL Forms]**」を選択します。
   2. パッケージのバージョンとタイプを選択します。また、「**[!UICONTROL ダウンロードを検索]**」オプションを使用して結果をフィルターすることもできます。
1. **we-gov-forms.pkg.all-&lt;version>.zip** パッケージ名をタップし、「**[!UICONTROL EULA 条項に同意]**」を選択して、「**[!UICONTROL ダウンロード]**」をタップします。
1. [パッケージマネージャー](https://docs.adobe.com/content/help/jp/experience-manager-65/administering/contentmanagement/package-manager.html)を開き「**[!UICONTROL パッケージをアップロード]**」をクリックしてパッケージをアップロードします。
1. パッケージを選択して、「**[!UICONTROL インストール]**」をクリックします。

   ![we gov forms パッケージ](assets/wegov_forms_package.jpg)

1. インストールプロセスを完了させます。
1. *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html?wcmmode=disabled* に移動して、インストールが正常に完了したことを確認します。

### ローカル ZIP ファイルから {#from-a-local-zip-file}

1. **we-gov-forms.pkg.all-&lt;version>.zip** ファイルをダウンロードして見つけます。
1. *https://&lt;aemserver>:&lt;port>/crx/packmgr/index.jsp* に移動します。
1. 「パッケージをアップロード」オプションを選択します。

   ![パッケージをアップロードオプション](assets/upload_package.jpg)

1. ファイルブラウザーを使用して、ダウンロードした ZIP ファイルに移動して選択します。
1. 「開く」をクリックしてアップロードします。
1. アップロードが完了したら、「インストール」オプションを選択してパッケージをインストールします。

   ![WeGov Formsパッケージのインストール](assets/wegov_forms_package-1.jpg)

1. インストールプロセスを完了させます。
1. *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html?wcmmode=disabled* に移動して、インストールが正常に完了したことを確認します。

### 新しいパッケージバージョンのインストール {#installing-new-package-versions}

新しいパッケージバージョンをインストールするには、4.1 と 4.2 で定義されている手順に従います。別の古いパッケージがすでにインストールされていても新しいパッケージバージョンをインストールできますが、最初に古いパッケージバージョンをアンインストールすることをお勧めします。古いパッケージバージョンをアンインストールするには、次の手順に従います。

1. *https://&lt;aemserver>:&lt;port>/crx/packmgr/index.jsp* に移動します。
1. 古い **we-gov-forms.pkg.all-&lt;version>.zip** ファイルを見つけます。
1. 「その他」オプションを選択します。
1. ドロップダウンから「アンインストール」オプションを選択します。

   ![WeGov パッケージをアンインストール](assets/uninstall_wegov_forms_package.jpg)

1. 確認後、「アンインストール」を再度選択し、アンインストール処理を完了させます。

## デモパッケージの設定 {#demo-package-configuration}

この節では、プレゼンテーション前のデモパッケージのデプロイ後の設定の詳細と手順について説明します。

### 架空のユーザー設定 {#fictional-user-configuration}

1. *https://&lt;aemserver>:&lt;port>/libs/granite/security/content/groupadmin.html* に移動します。
1. 以下のタスクを実行するには、管理者としてログインします。
1. ページの末尾まで下にスクロールし、すべてのユーザーグループを読み込みます。
1. 「**ワークフロー**&quot;.
1. 「**workflow-users**&quot;グループ化し、&quot;プロパティ&quot;をクリックします。
1. 「メンバー」タブに移動します。
1. 入力 **wegov** 「ユーザーまたはグループを選択」フィールドで、
1. ドロップダウンから「 」を選択します。**We.Gov Forms Users**&quot;.

   ![ワークフローユーザーのグループ設定の編集](assets/edit_group_settings.jpg)

1. メニューバーの「保存して閉じる」をクリックします。
1. 手順 2～7 を繰り返し、「**分析**」をクリックし、「**Analytics 管理者**&quot;グループを作成し、&quot;**We.Gov Forms Users**&quot;グループをメンバーとして使用します。
1. 手順 2～7 を繰り返し、「**フォームユーザー**」をクリックし、「**forms-power-users**&quot;グループを作成し、&quot;**We.Gov Forms Users**&quot;グループをメンバーとして使用します。
1. 手順 2～7 を繰り返し、「**forms-users**」をクリックし、「**forms-users**&quot;グループに追加し、今回は&quot;**We.Gov ユーザー**&quot;グループをメンバーとして使用します。

### メールサーバーの設定 {#email-server-configuration}

1. 設定ドキュメントの確認 [メール通知の設定](/help/sites-administering/notification.md)
1. このタスクを実行するには、管理者としてログインします。
1. *https://&lt;aemserver>:&lt;port>/system/console/configMgr* に移動します。
1. **Day CQ Mail Service** サービスを探して、設定します。

   ![Day CQ メールサービスの設定](assets/day_cq_mail_service.jpg)

1. 任意の SMTP サーバーに接続するようにサービスを設定します。

   1. **SMTP サーバーのホスト名**：例（smtp.gmail.com）
   1. **サーバーポート**：SSL を使用した gmail の例：465
   1. **SMTP ユーザー：** demo@ &lt;companyname> .com
   1. **「差出人」のアドレス**:aemformsdemo@adobe.com

   ![SMTP を設定](assets/configure_smtp.jpg)

1. 「保存」をクリックして設定を保存します。

### （オプション）AEM SSL 設定 {#aemsslconfig}

この節では、AEM インスタンスで SSL を設定して、Adobe Sign クラウドを設定できるようにする方法について詳しく説明します。

**参照：**

1. [デフォルトの SSL](/help/sites-administering/ssl-by-default.md)

**メモ：**

1. https://&lt;aemserver>:&lt;port>/aem/inbox に移動すると、上記の参照ドキュメントリンクで説明されているプロセスを完了できます。
1. `we-gov-forms.pkg.all-[version].zip` パッケージには、パッケージの一部である `we-gov-forms.pkg.all-[version].zip/ssl` フォルダーを抽出することでアクセスできるサンプル SS キーと証明書が含まれています。

1. SSL 証明書およびキーの詳細：

   1. 「CN=localhost」に対して発行された
   1. 10 年の有効性
   1. 「password」のパスワード値
1. 秘密鍵は *localhostprivate.der*。
1. 証明書は *localhost.crt*。
1. 「次へ」をクリックします。
1. HTTPS Hostname は *localhost* に設定する必要があります。
1. ポートは、システムが公開しているポートに設定する必要があります。

### （オプション）Adobe Sign クラウド設定 {#adobe-sign-cloud-configuration}

この節では、Adobe Sign クラウド設定の詳細と手順について説明します。

**参照：**

1. [Adobe Sign の AEM Forms への統合](adobe-sign-integration-adaptive-forms.md)

#### クラウド設定 {#cloud-configuration}

1. 前提条件を確認します。必要な SSL 設定について詳しくは、[AEM SSL 設定](../../forms/using/forms-install-configure-gov-reference-site.md#aemsslconfig)を参照してください。
1. 次の URL に移動します。

   *https://&lt;aemserver>:&lt;port>/libs/adobesign/cloudservices/adobesign.html/conf/we-gov*

   >[!NOTE]
   >
   >設定の問題を回避するために、AEM サーバーにアクセスするために使用する URL は、Adobe Sign OAuth リダイレクト URI で設定された URL と一致する必要があります（例： *https://&lt;aemserver>:&lt;port>/mnt/overlay/adobesign/cloudservices/adobesign/properties.html*）。

1. 「We.gov Adobe Sign」設定を選択します。
1. 「プロパティ」をクリックします。
1. 「設定」タブに移動します。
1. OAuth URL を入力します（例： [https://secure.na1.echosign.com/public/oauth](https://secure.na1.echosign.com/public/oauth)）。
1. 設定した Adobe Sign インスタンスから、設定したクライアント ID とクライアント秘密鍵を指定します。
1. 「Adobe Signに接続」をクリックします。
1. 接続に成功したら、「保存して閉じる」をクリックして統合を完了します。

### （オプション） MS Dynamics クラウド設定 {#ms-dynamics-cloud-configuration}

この節では、MS Dynamics クラウド設定の詳細と手順について説明します。

**参照：**

1. [Microsoft Dynamics OData の設定](https://docs.adobe.com/content/help/jp/experience-manager-64/forms/form-data-model/ms-dynamics-odata-configuration.html)
1. [AEM Forms用Microsoft Dynamics の設定](https://helpx.adobe.com/experience-manager/kt/forms/using/config-dynamics-for-aem-forms.html)

#### MS Dynamics OData クラウドサービス {#ms-dynamics-odata-cloud-service}

1. 次の URL に移動します。

   https://&lt;aemserver>:&lt;port>/libs/fd/fdm/gui/components/admin/fdmcloudservice/fdm.html/conf/we-gov

   1. MS Dynamics アプリケーションの登録で設定したリダイレクト URL と同じ URL を使用してサーバーにアクセスしていることを確認してください。

1. 「Microsoft Dynamics ODataCloud Service」設定を選択します。
1. 「プロパティ」をクリックします。

   ![Microsoft OData クラウドサービスのプロパティ](assets/properties_odata_cloud_service.jpg)

1. 「認証設定」タブに移動します。
1. 以下の詳細を入力します。

   1. **サービスルート：**&#x200B;例`https://msdynamicsserver.api.crm3.dynamics.com/api/data/v9.1/`
   1. **認証タイプ：** OAuth 2.0
   1. **認証設定**（この情報を収集するには[MS Dynamics クラウド設定](../../forms/using/forms-install-configure-gov-reference-site.md#dynamicsconfig)を参照してください）。

      1. クライアント ID - アプリケーション ID とも呼ばれます
      1. クライアントの秘密鍵
      1. OAuth URL - 例： [https://login.windows.net/common/oauth2/authorize](https://login.windows.net/common/oauth2/authorize)
      1. 更新トークン URL - 例： [https://login.windows.net/common/oauth2/token](https://login.windows.net/common/oauth2/token)
      1. アクセストークン URL - 例：[https://login.windows.net/common/oauth2/token](https://login.windows.net/common/oauth2/token)
      1. 認証範囲 - **openid**
      1. 認証ヘッダー - **認証ベアラ**
      1. リソース - 例：`https://msdynamicsserver.api.crm3.dynamics.com`
   1. 「OAuth に接続」をクリックします。


1. 認証が成功したら、「保存して閉じる」をクリックして統合を完了します。

#### MS Dynamics クラウド設定 {#dynamicsconfig}

この節で説明する手順は、MS Dynamics Cloud インスタンスからクライアント ID、クライアント秘密鍵、詳細を見つけるのに役立ちます。

1. [https://portal.azure.com/](https://portal.azure.com/) に移動し、ログインします。
1. 左側のメニューから「すべてのサービス」を選択します。
1. 検索するか、「アプリ登録」に移動します。
1. 既存のアプリケーション登録を作成するか、選択します。
1. **アプリケーション ID** を AEM クラウド設定の OAuth として使用される&#x200B;**クライアント ID** にコピーします。
1. 「設定」または「マニフェスト」をクリックして、 **返信 URL。**

   1. この URL は、OData サービスの設定時に AEM サーバーにアクセスするために使用される URL と一致させる必要があります。

1. 設定ビューで、「キー」をクリックして、新しいキーの作成を表示します ( これはAEMのクライアント秘密鍵として使用されます )。

   1. 後で Azure や AEM で表示できないため、キーのコピーを保持してください。

1. リソース URL/サービスルート URL を探すには、MS Dynamics インスタンスダッシュボードに移動します。
1. 上部のナビゲーションバーで、「Sales」または独自のインスタンスタイプをクリックし、「設定を選択」をクリックします。
1. 右下の「カスタマイズ」と「開発者向けリソース」をクリックします。
1. 次のサービスルート URL があります。例：

   *`https://msdynamicsserver.api.crm3.dynamics.com/api/data/v9.1/`

1. 更新およびアクセストークン URL の詳細は、次の場所で確認できます。

   *[https://docs.microsoft.com/en-us/rest/api/datacatalog/authenticate-a-client-app](https://docs.microsoft.com/ja-jp/rest/api/datacatalog/authenticate-a-client-app)*

#### フォームデータモデル（Dynamics）のテスト {#testing-the-form-data-model}

クラウド設定が完了したら、フォームデータモデルをテストする必要があります。

1. 次に移動します。

   *https://&lt;aemserver>:&lt;port>/aem/forms.html/content/dam/formsanddocuments-fdm/we-gov*

1. 「We.gov Microsoft Dynamics CRM FDM」を選択し、「プロパティ」を選択します。

   ![Dynamics CRM FDM のプロパティ](assets/properties_dynamics_crm.jpg)

1. 「ソースを更新」タブに移動します。
1. 「Context-Aware Configuration」が「/conf/we-gov」に設定され、設定済みのデータソースが「ms-dynamics-odata-cloud-service」になっていることを確認します。

   ![設定済みのデータソース](assets/configured_data_source.jpg)

1. フォームデータモデルを編集します。

1. サービスをテストし、設定済みのデータソースに正常に接続できることを確認します。

   >[!NOTE]
   サービスをテストしたら、**キャンセル**&#x200B;をクリックし、不本意の変更がフォームデータモデルに反映されないようにします。

   >[!NOTE]
   データソースが FDM に正常にバインドされるには、AEM サーバーの再起動が必要であることが報告されています。

#### フォームデータモデル（Derby）のテスト {#test-fdm-derby}

クラウド設定が完了したら、フォームデータモデルをテストする必要があります。

1. *https://&lt;aemserver>:&lt;port>/aem/forms.html/content/dam/formsanddocuments-fdm/we-gov* に移動します。

1. **We.gov 登録 FDM** を選択し、**プロパティ**&#x200B;を選択します。

   ![Dynamics CRM FDM のプロパティ](assets/aftia-enrollment-fdm.jpg)

1. 「**ソースを更新**」タブに移動します。

1. **コンテキスト対応の設定**&#x200B;が `/conf/we-gov` に設定されていること、および設定済みのデータソースが **We.Gov Derby DS** であることを確認します。

   ![Dynamics CRM FDM のプロパティ](assets/aftia-update-data-source.jpg)

1. 「**保存して閉じる**」をクリックします。

1. [サービスのテスト](work-with-form-data-model.md#test-data-model-objects-and-services)を行い、設定したデータソースに正常に接続できることを確認します。

   * 接続をテストするには、**HOMEMORTGAGEACCOUNT** を選択し、get サービスを実行します。サービスおよびシステム管理者をテストすると、取得されたデータを確認できます。

### Adobe Analytics 設定（オプション） {#adobe-analytics-configuration}

この節では、Adobe Analytics Cloud 設定の詳細と手順について説明します。

**参照：**

* [Adobe Analytics との統合](../../sites-administering/adobeanalytics.md)

* [Adobe Analytics への接続とフレームワークの作成](../../sites-administering/adobeanalytics-connect.md)

* [ページ分析データの表示](../../sites-authoring/pa-using.md)

* [分析とレポートの設定](configure-analytics-forms-documents.md)

* [AEM Forms の分析レポートの確認方法と詳細](view-understand-aem-forms-analytics-reports.md)

### Adobe Analytics クラウドサービス設定 {#adobe-analytics-cloud-service-configuration}

このパッケージは、Adobe Analytics に接続するように事前設定されています。この設定を更新するには、次の手順を実行します。

1. *https://&lt;aemserver>:&lt;port>/libs/cq/core/content/tools/cloudservices.html* に移動します。
1. Adobe Analyticsセクションを探し、「設定を表示」リンクを選択します。
1. 「We.Gov Adobe Analytics (Analytics Configuration)」設定を選択します。

   ![Analytics クラウドサービス設定](assets/analytics_config.jpg)

1. 「編集」ボタンをクリックして、Adobe Analytics設定を更新します（共有暗号鍵を指定する必要があります）。 「Analytics に接続」をクリックして接続し、「OK」をクリックして完了します。

   ![We.Gov Adobe Analytics](assets/wegov_adobe_analytics.jpg)

1. フレームワーク設定を更新する場合は、同じページで、「We.Gov Adobe Analytics Framework (Analytics Framework)」をクリックします ( [AEMオーサリングの有効化](../../forms/using/forms-install-configure-gov-reference-site.md#enableauthoring) （オーサリングを有効にする）。

#### Adobe Analytics ユーザー資格情報の検索 {#analytics-locating-user-credentials}

Adobe Analytics アカウントのユーザー資格情報を見つけるには、アカウント管理者が次のタスクを実行する必要があります。

1. Adobe Experience Cloud ポータルに移動します。
   * 管理者の資格情報を使用してログインします。
1. メインダッシュボードで「Adobe Analytics」アイコンを選択します。
   ![迅速なアクセス](assets/aftia-quick-access.jpg)
1. 「管理者」タブに移動し、「User Management」の既存項目を選択します。
   ![レポート](assets/aftia-reports.jpg)
1. 「**ユーザー**」タブを選択します。
   ![User Management](assets/aftia-user-management.jpg)
1. ユーザーのリストから目的のユーザーを選択します。
1. ページの下部までスクロールすると、ページの下部にユーザー認証情報が表示されます。
   ![アクセスを管理](assets/aftia-admin-user-access.jpg)
1. ユーザー名と共有暗号鍵の情報が、権限ボックスの右側に表示されます。
1. ユーザー名の名前の中にコロンが含まれていることに注意してください。コロンの左側にあるすべての情報はユーザー名で、コロンの右側にあるすべての情報は会社名です。
   * 次に例を示します。*ユーザー名：会社名*

#### Adobe Analytics でのユーザー認証の設定 {#setup-user-authentication}

管理者は次の操作を実行して、ユーザーに AEM Analytics の権限を付与できます。

1. Adobe Admin Console に移動します。

1. Admin Console に公開されている Analytics インスタンスをクリックします。

   * これは、管理ページのメインページにあります。

1. 「 Analytics 管理者の完全なアクセス」を選択します。

1. ユーザーをプロファイルに追加します。

   ![Analytics 管理者の完全なアクセス](assets/aftia-full-admin-access.jpg)

1. ユーザー ID がプロファイルにマッピングされたら、「権限」タブをクリックします。

1. すべての権限がプロファイルにマッピングされていることを確認します。

   ![権限を編集](assets/aftia-admin-access-edit.jpg)

1. ユーザーのログイン機能に関して権限がマッピングされると、数時間かかる場合があります。

### Adobe Analytics レポート {#adobe-analytics-reporting}

#### Adobe Analytics Sites レポートを表示 {#view-adobe-analytics-sites-reporting}

>[!NOTE]
`we-gov-forms.ui.analytics-<version>.zip` パッケージがインストールされている場合、AEM Forms Analytics データはオフラインでも、Adobe Analytics クラウド設定なしでも利用できますが、AEM Sites データにはアクティブなクラウド設定が必要です。

1. *https://&lt;aemserver>:&lt;port>/sites.html/content* に移動します。 
1. 「AEM Forms We.Gov Site」を選択して、サイトのページを表示します。
1. サイトページの 1 つ（例：ホーム）を選択し、「Analytics &amp; Recommendations」を選択します。

   ![分析と推奨表示](assets/analytics_recommendations.jpg)

1. このページには、AEM Sites ページに関連する、Adobe Analytics から取得した情報が表示されます（注意：設計により、この情報は Adobe Analytics から定期的に更新され、リアルタイムには表示されません）。

   ![AEM Sites 分析](assets/sites_analysis.jpg)

1. ページビューページに戻る（手順 3.でアクセス）と、「リスト表示」の項目を表示する表示設定を変更することで、ページビュー情報を表示することもできます。
1. 「表示」ドロップダウンメニューを探し、「リスト表示」を選択します。

   ![リスト表示](assets/list_view.jpg)

1. 同じメニューから「設定を表示」を選択し、「Analytics」セクションから表示する列を選択します。

   ![列を構成](assets/configure_columns.jpg)

1. 「更新」をクリックして、新しい列を使用可能にします。

   ![新しい列の表示](assets/new_columns_display.jpg)

#### Adobe Analytics Forms レポートを表示 {#view-adobe-analytics-forms-reporting}

>[!NOTE]
`we-gov-forms.ui.analytics-<version>.zip` パッケージがインストールされている場合、AEM Forms Analytics データはオフラインでも、Adobe Analytics クラウド設定なしでも利用できますが、AEM Sites データにはアクティブなクラウド設定が必要です。

1. 次に移動します。

   *https:///&lt;aemserver>:&lt;port>/aem/forms.html/content/dam/formsanddocuments/adobe-gov-forms*

1. 「Enrollment Application For Health Benefits」アダプティブフォームを選択し、「Analytics レポート」オプションを選択します。

   ![分析レポート](assets/analytics_report.jpg)

1. ページが読み込まれるのを待ち、分析レポートデータを表示します。

   ![分析レポートデータの表示](assets/analytics_report_data.jpg)

### Adobe Automated Forms 設定イネーブルメント {#automated-forms-enablement}

AEM Forms を Adobe Forms と共にインストールして設定するには、変換ツールのユーザーが以下を所有している必要があります。

1. Adobe I/O へのアクセス。

1. Adobe Forms コンバージョンサービスとの統合をする権限。

1. オーサーとして実行される Adobe AEM 6.5 最新のサービスパック。

詳細な手順を読む前に、次の点を確認してください。

* [フォームの自動コンバージョンサービスの設定](https://docs.adobe.com/content/help/jp//aem-forms-automated-conversion-service/using/configure-service.html)

#### IMS 設定の作成パート 1 {#creating-ims-config}

Forms 変換ツールと正しく通信するようにサービスを設定するには、ユーザーは Adobe I/O に登録できるように Identity Management System（IMS）サービスを設定する必要があります。

1. https://&lt;aemserver>:&lt;port> > に移動します。Adobe Experience 
Manager の左上の ／>ツール／>セキュリティ／ >Adobe IMS設定をクリックします。

1. 「作成」をクリックします。

1. 以下の画像のアクションを実行します。

   ![IMS テクニカルアカウント設定](assets/aftia-technical-account-configuration.jpg)

1. 必ず証明書をダウンロードしてください。

1. 設定の残りの部分を続行しないでください。 [Adobe I/O での統合の作成](#create-integration-adobeio)節を確認してください。

>[!NOTE]
この節で作成された証明書は、Adobe I/Oで統合サービスを作成するために使用されます。統合サービスで作成すると、Adobe I/O からのその情報を使用して設定を完了することができます。

#### Adobe I/O での統合の作成 {#create-integration-adobeio}

アドビメイン内で統合を作成するためにシステム管理者に連絡しない場合は、ご自身に作成する能力があることを確認してください。

1. [Adobe I/O コンソール](https://console.adobe.io/)に移動します。

1. 統合を作成をクリックします。

1.  API にアクセスを選択します。

1. 正しいグループ（右上のドロップダウンリスト）に属していることを確認します。

1. Experience Cloud セクションで、 Forms コンバージョンツールを選択します。

1. 「続行」をクリックします。

1. 統合の名前と説明を入力します。

1. 2.1 節の公開鍵を使用して、鍵の統合内に配置します。

1. 自動 Forms コンバージョン用のプロファイルを選択します。

   ![新しい統合の作成](assets/aftia-create-new-integration.jpg)

#### IMS 設定の作成パート 2 {#create-ims-config-part-next}

これで統合を作成したので、IMS 設定のインストールを完了します。

1. 接続の詳細を表示するには、Adobe I/O 内の統合をクリックします。

1. AEM（ツール/セキュリティ/IMS）内で IMS 設定に移動します。

1. IMS 設定画面で「次へ」をクリックします。

1. 認証サーバー（スクリーンショットに表示されている値）を入力します。

1. API キーを入力します。

1. クライアントの秘密鍵を入力します（統合を表示するには、Adobe I/O で公開をクリックする必要があります）。

1. Adobe I/O の「JWT」タブをクリックして、JWT ペイロードを取得し、IMS 設定のペイロードに貼り付けます。

   ![ペイロード IMS 設定](assets/aftia-payload-ims-config.jpg)

1. 作成したら、IMS 設定をクリックし、ヘルスチェックを選択すると、次の結果が表示されます。

   ![正常性の確認](assets/aftia-health-confirmation.jpg)

#### クラウド設定（We.Gov AFC 実稼動） {#configure-cloud-configuration}

IMS の設定が完了したら、AEM でクラウド設定を確認することができます。設定が存在しない場合は、次の手順を使用して AEM でクラウド設定を作成します。

1. ブラウザーを開き、システム URL https://&lt;domain_name>:&lt;system_port> に移動します。

1. ／ツール／Cloud Services／自動フォームコンバージョン設定画面の左上隅にある Adobe Experience Manager をクリックします。

1. 設定を配置する設定フォルダーを選択します。

1. 作成をクリックします。

1. 以下のスクリーンショットに情報を入力します。

   ![AFC 実稼動](assets/aftia-afc-production.jpg)

1. 設定にタイトルと名前を入力します。

1. システムのサービス URL は、https://aemformsconversion.adobe.io/ に設定されます。

1. テンプレート URL */conf/we-gov/settings/wcm/templates/we-gov-flamingo-template*。

1. テーマ URL：*/content/dam/formsanddocuments-themes/adobe-gov-forms-themes/we-gov-theme*

1. 次へをクリックします。

1. この設定では、2 つのチェックボックス値を空のままにしておきます。

   * これらのオプションについて詳しくは、[クラウドサービスを設定](https://docs.adobe.com/content/help/jp/aem-forms-automated-conversion-service/using/configure-service.html#configure-the-cloud-service)を参照してください。

#### クラウド設定（We.Finance AFC 実稼動） {#configure-cloud-configuration-wefinance}

IMS 設定が完了したら、AEM でクラウド設定を作成する手順に進むことができます。

1. ブラウザーを開き、システム URL https://&lt;domain_name>:&lt;system_port> に移動します。

1. ／ツール／Cloud Services／自動フォームコンバージョン設定画面の左上隅にある Adobe Experience Manager をクリックします。

1. 設定を配置する設定フォルダーを選択します。

1. 作成をクリックします。

1. 以下のスクリーンショットに情報を入力します。

   ![We.Finance AFC 実稼働](assets/aftia-wefinance-afc-prod.jpg)

1. 設定にタイトルと名前を入力します。

1. システムのサービス URL は https://aemformsconversion.adobe.io/ に設定されます

1. テンプレート URL：*/conf/we-finance/settings/wcm/templates/we-finance-adaptive-form*

1. テーマ URL：*/content/dam/formsanddocuments-themes/adobe-finance-forms-themes/we-finance-theme*

1. 次へをクリックします。

1. この設定では、2 つのチェックボックス値を空のままにしておきます。

   * これらのオプションについて詳しくは、[クラウドサービスを設定](https://docs.adobe.com/content/help/en/aem-forms-automated-conversion-service/using/configure-service.html#configure-the-cloud-service)を参照してください。

#### フォーム変換のテスト（We.Gov 登録アプリケーション） {#test-forms-conversion}

設定が完了したら、PDF ドキュメントをアップロードしてテストできます。

1. AEM システム https://&lt;domain_name>:&lt;system_port> に移動します

1. フォーム／フォームとドキュメント／AEM Forms We.gov Forms／AFC をクリックします。

1. We.Gov 登録アプリケーション PDF を選択します。

1. 右上隅の「**自動変換処理の開始** 」ボタンをクリックします。

1. ユーザーは、次に示すようにこのオプションを表示できます。

   ![変換後のアダプティブフォーム](assets/aftia-converted-adaptive-form.jpg)

1. ボタンを選択すると、次のオプションが表示されます

   * ユーザーが *We.Gov AFC 実稼働* 設定を選択していることを確認してください

   ![変換設定](assets/aftia-conversion-settings.jpg)

   ![詳細な変換設定](assets/aftia-conversion-settings-2.jpg)

1. 使用するすべてのオプションを設定したら、変換を開始を選択します。

1. 変換処理が始まると、次の画面が表示されます。

   ![変換設定](assets/aftia-conversion-in-progress.jpg)

1. 変換が完了すると、次の画面が表示されます。

   ![変換されたアダプティブフォーム](assets/aftia-converted-adaptive-form-2.jpg)

   **出力**&#x200B;フォルダーをクリックして、生成されたアダプティブフォームを表示します。

#### 既知の問題とメモ {#known-issues-notes}

フォーム自動変換サービスには、[ベストプラクティス、既知の複雑なパターン](https://docs.adobe.com/content/help/jp/aem-forms-automated-conversion-service/using/styles-and-pattern-considerations-and-best-practices.html)、および [既知の問題](https://docs.adobe.com/content/help/jp/aem-forms-automated-conversion-service/using/introduction.html)が含まれています。AEM Forms のフォーム自動変換サービスを使用する前に、これらを確認してください。

1. 変換後にフォームを FDM にバインドする場合は、「データをバインドせずにアダプティブフォームを生成」を有効にしてフォームを生成します。

1. テンプレートフォルダーで、すべてのユーザーに対して jcr:read 権限が有効になっていることを確認してください。有効になっていないと、サービスユーザーがリポジトリーからテンプレートを読み取れず、変換が失敗します。

## デモパッケージのカスタマイズ {#demo-package-customizations}

このセクションでは、デモのカスタマイズ手順を説明します。

### テンプレートのカスタマイズ {#templates-customization}

編集可能テンプレートは、次の場所にあります。

*https://&lt;aemserver>:&lt;port>/libs/wcm/core/content/sites/templates.html/conf/we-gov*

これらのテンプレートには、次の場所にあるコンポーネントを使用して作成および構成された、AEM サイト、アダプティブフォーム、インタラクティブ通信の各テンプレートが含まれます。

*https://&lt;aemserver>:&lt;port>/crx/de/index.jsp#/apps/we-gov/components*

#### スタイルシステム {#customizetemplates}

このサイトではクライアントライブラリも取り上げており、その 1 つが Bootstrap 4（[https://getbootstrap.com/](https://getbootstrap.com/)）を読み込みます。このクライアントライブラリは、次の場所から利用できます。

*https://&lt;aemserver>:&lt;port>/crx/de/index.jsp#/apps/we-gov/clientlibs/clientlib-base/css/bootstrap*

このパッケージに含まれる編集可能なテンプレートには、ページネーションやスタイル設定などに Bootstrap 4 の CSS クラスを使用するテンプレートポリシーやページポリシーも事前に設定されています。テンプレートポリシーにすべてのクラスが追加されているわけではありませんが、Bootstrap 4 でサポートされるクラスはすべてポリシーに追加できます。使用可能なクラスの一覧については、はじめにページを参照してください。

[https://getbootstrap.com/docs/4.1/getting-started/introduction/](https://getbootstrap.com/docs/4.1/getting-started/introduction/)

このパッケージに含まれるテンプレートは、スタイルシステムもサポートしています。

[スタイルシステム](../../sites-authoring/style-system.md)

#### テンプレートロゴ {#template-logos}

プロジェクト DAM アセットには、We.Gov のロゴや画像も含まれています。これらのアセットは、次の場所から利用できます。

*https://&lt;aemserver>:&lt;port>/assets.html/content/dam/we-gov*

ページテンプレートとフォームテンプレートの編集時に、ナビゲーションコンポーネントとフッターコンポーネントを編集することで、ブランドロゴを更新することができます。これらのコンポーネントには、ロゴの更新に使用でき、ブランドとロゴを設定可能なダイアログが用意されています。

![テンプレートロゴ](assets/template_logos.jpg)

詳しくは、ページコンテンツの編集を参照してください。

[ページコンテンツの編集](../../sites-authoring/editing-content.md)

### サイトページのカスタマイズ {#sites-pages-customization}

すべてのサイトページは、*https://&lt;aemserver>:&lt;port>/sites.html/content/we-gov* から利用できます。

また、これらのサイトページでは、AEM Grid パッケージを使用して一部のコンポーネントのレイアウトを制御しています。

#### スタイルシステム {#style-system}

このパッケージに含まれているページは、スタイルシステムもサポートしています。

[スタイルシステム](../../sites-authoring/style-system.md)

また、サポート対象のスタイルに関するドキュメントとしては、[テンプレートをカスタマイズするためのスタイルシステム](../../forms/using/forms-install-configure-gov-reference-site.md#customizetemplates)を参照してください。

### アダプティブフォームのカスタマイズ {#adaptive-forms-customization}

すべてのアダプティブフォームが次の場所から利用できます。

*https://&lt;aemserver>:&lt;port>/aem/forms.html/content/dam/formsanddocuments/adobe-gov-forms*

これらのフォームは、特定の使用例に合わせてカスタマイズできます。フォームの正常な機能を維持するために、特定のフィールドと送信ロジックを変更しないでください。変更してはいけないものの一例は、次のとおりです。

**健康増進のための登録申請：**

* contact_id - 送信時に MS Dynamics の連絡先 ID を受け取るために使用される非表示フィールド
* 送信 - コールバックをサポートするために、送信ボタンのロジックにカスタマイズが必要でした。カスタマイズについてはドキュメントにまとめられていますが、Forms データモデルを使用して MS Dynamics に対して POST 操作と GET 操作の両方を実行しながらフォームを送信するには、大規模なスクリプトが必要でした。
* ルートパネル - AEM インボックスの Granite UI コンポーネントはどれも変更できないので、Initialize イベントを使用して可能な限り控えめな方法で AEM インボックスに MS Dynamics ボタンを追加します。

#### アダプティブフォームのスタイル設定 {#adaptive-form-styling}

アダプティブフォームもスタイル設定することができ、それにはスタイルエディターまたはテーマエディターを使用します。

* [アダプティブフォームコンポーネントのインラインスタイリング](inline-style-adaptive-forms.md)
* [テーマの作成および使用](themes.md)

### ワークフローのカスタマイズ {#workflow-customization}

登録アダプティブフォームは、OSGI ワークフローに送信されて処理されます。このワークフローは、*https://&lt;aemserver>:&lt;port>/conf/we-gov/settings/models/we-gov-process.html* にあります。

一部の制限があるため、このワークフローには、複数のスクリプトとカスタム OSGi ワークフロープロセスステップが含まれています。 これらのワークフローステップは汎用ステップとして作成され、設定ダイアログを使用して作成されたものではありません。現時点では、ワークフローステップの設定はプロセス引数に応じて異なります。

すべてのワークフローステップの Java コードは、**we-gov-forms.core-&lt;version>.jar** バンドルに含まれています。

## デモに関する考慮事項と既知の問題 {#demo-considerations-and-known-issues}

このセクションでは、デモ機能についての説明と、デモプロセスの設計において特に検討が必要になる可能性のある項目について説明します。

### デモに関する考慮事項 {#demo-considerations}

* AGRS-159 に従い、登録アダプティブフォームで使用する連絡先の名前（名、ミドルネーム、姓）は固有にします。
* 登録アダプティブフォームは、フォームのメールフィールドに指定されたメールアドレスに Adobe Sign メールを送信します。このメールアドレスには、Adobe Sign クラウド設定で使用したのと同じメールアドレスを指定することはできません。

### 既知の問題 {#known-issues}

* （AGRS-120）サイトナビゲーションコンポーネントは現時点で、2 レベル以上の深さのネストされた子ページをサポートしていません。
* （AGRS-159）現時点では MS Dynamics FDM は操作を 2 回実行する必要があり、まず、登録アダプティブフォームのデータを Dynamics に POST し、次に連絡先 ID を取得するためにユーザーレコードを取り込みます。現在の状態では、同じ名前のユーザーが Dynamics に複数存在すると連絡先 ID の取得が失敗し、登録アダプティブフォームを送信できません。

## アクセシビリティテストの設定 {#configure-accessibility-testing}

### アクセシビリティテスト用の Chrome アドオンの有効化 {#enable-chrome-add-on}

アクセシビリティテストを実行するには、まず[ここ](https://chrome.google.com/webstore/detail/accessibility-developer-t/fpkknkljclfencbdbgkenhalefipecmb?hl=ja)から Chrome プラグインをインストールする必要があります。

インストールが完了したら、テストするページを Chrome ブラウザーで読み込みます（注：タブを複数開いているとスコアに影響する場合があります。タブは 1 つだけ開くことを推奨します）。ページを読み込んだら、
そのページで**右クリック**&#x200B;し、「**Audits**」タブを選択します。その画面で開発者は、アクセシビリティプラグインで実行する検証のタイプを選択できます。必要なオプションをすべて選択したら、「レポートを生成」ボタンを選択します。これにより、アクセシビリティの総合評価や、その評価を向上するための提案が記載された PDF ドキュメントが生成されます。

レポートの生成を実行すると、次の情報が表示されます。

![アクセシビリティレポート](assets/aftia-accessibility.jpg)

ユーザーに表示される数値は、アクセシビリティの総合評価の判定です。スコアに続いて、計算方法に関する説明もあります。

これを書き出す場合は、画面の右側の 3 つのボタンをクリックし、プラグインに表示される該当オプションをさらに選択します。

![アクセシビリティレポート](assets/aftia-accessibility-report.jpg)

### Ultramarine テーマ {#ultramarine-theme}

アドビがサポートし一般公開されている Ultramarine テーマは、
インストール可能な ZIP ファイルである `we-gov-forms.pkg.all-<version>.zip` に組み込まれています。CRX パッケージマネージャーを使用してこのパッケージをインストールしたら、

AEM Forms で **Forms**／**テーマ**／**リファレンステーマ**／**Ultramarine** の順にクリックして Ultramarine テーマにアクセスできます。

![Ultramarine テーマ](assets/aftia-ultramarine-theme.jpg)

## 設定オプション {#configuration-options}

ユーザーは、次のような様々なワークフローサービスオプションを設定できます。

1. Microsoft Dynamics エントリ
1. Adobe Sign
1. AEM 顧客コミュニケーション管理
1. Adobe Analytics

これらをワークフロー内で有効になるように設定するには、次のタスクを実行する必要があります。

1. https://&#39;[server]:[port]&#39;/system/console/configMgr に移動します。

1. *WeGov Configurations* を見つけます。

1. サービス定義を開き、選択したサービスをワークフロー内で呼び出せるようにしてください。

   >[!NOTE]
   ユーザーが Configuration Manager ページ内でサービスを有効にしているのと同じ理由で、要求された外部サービスと通信するために、ユーザーは引き続きサービス設定を行う必要があります。

   ![we gov forms パッケージ](assets/aftia-configuration-options.jpg)

1. 設定が完了したら、「保存」ボタンをクリックして設定を保存します。

## 次の手順 {#next-steps}

これで、We.Gov リファレンスサイトを利用するための設定がすべて完了しました。We.Gov リファレンスサイトのワークフローと手順について詳しくは、[We.Gov リファレンスサイトのチュートリアル](../../forms/using/forms-gov-reference-site-user-demo.md)を参照してください。
