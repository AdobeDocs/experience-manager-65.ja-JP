---
title: We.GovおよびWe.Financeリファレンスサイトの設定と設定
seo-title: Web.Govリファレンスサイトのセットアップと設定
description: AEM Formsデモパッケージをインストール、設定、カスタマイズします。
seo-description: AEM Formsデモパッケージをインストール、設定、カスタマイズします。
uuid: 0a6ad8f9-0d38-40c3-ad8d-e705edef55f8
contentOwner: anujkapo
discoiquuid: fe5da0aa-d3a8-4b77-a447-9e429fdc2816
docset: aem65
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '4742'
ht-degree: 4%

---


# We.GovおよびWe.Financeリファレンスサイトのセットアップと設定{#set-up-and-configure-we-gov-reference-site}

## デモパッケージの詳細{#demo-package-details}

### インストールの前提条件{#installation-prerequisites}

このパッケージは&#x200B;**AEM Forms6.4 OSGI Author**&#x200B;向けに作成され、テスト済みなので、次のプラットフォームバージョンでサポートされています。

| AEMバージョン | AEM FORMSパッケージ版 | ステータス |
|---|---|---|
| 6.4 | 5.0.86 | **サポート対象** |
| 6.5 | 6.0.80 | **サポート対象** |
| 6.5.3 | 6.0.122 | **サポート対象** |

このパッケージには、次のプラットフォームバージョンをサポートするクラウド設定が含まれています。

| クラウドプロバイダー | サービスのバージョン | ステータス |
|---|---|---|
| Adobe Sign | v5 API | **サポート対象** |
| Microsoft Dynamics 365 | 1710 (9.1.0.3020) | **サポート対象** |
| Adobe Analytics | v1.4 Rest API | **サポート対象** |
**パッケージのインストールに関する考慮事項：**

* パッケージは、クリーンサーバーにインストールされ、他のデモパッケージや古いデモパッケージバージョンが含まれていないことが想定されます。
* パッケージはOSGIサーバーにインストールされ、作成者モードで実行されている必要があります

### このパッケージに含まれる内容{#what-does-this-package-include}

[AEM FormsWe.Govデモパッケージ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/we-gov-forms.pkg.all-2.0.2.zip) (**we-gov-forms.pkg.all-&lt;version>.zip**)は、他の複数のサブパッケージやサービスを含むパッケージとして提供されます。 パッケージには、次のモジュールが含まれます。

* **we-gov-forms.pkg.all-&lt;version>.zip** - *完全なデモパッケージ*

   * **we-gov-forms.ui.apps-&lt;version>.zip** *— すべてのコンポーネント、クライアントライブラリ、サンプルユーザー、ワークフローモデルなどが含まれます。*

      * **we-gov-forms.core-&lt;version>.jar**  — すべてのOSGIサービス、カスタムワークフロー手順の実装などを *含みます。*

      * **we-gov-forms.derby&lt;version>.jar**  — すべてのOSGIサービス、データベーススキーマなどを *含みます。*

      * **core.wcm.components.all-2.0.4.zip**  — サンプルWCMコンポーネントの *収集*

      * **grid-aem.ui.apps-1.0-SNAPSHOT.zip** - *AEM Sitesグリッドレイアウトパッケージ（サイトページ列管理用）*
   * **we-gov-forms.ui.content-&lt;version>.zip** - *コンテンツ、ページ、画像、フォーム、インタラクティブな通信アセットなどをすべて含みます。*

   * **we-gov-forms.ui.analytics-&lt;version>.zip**  — リポジトリに格納されるすべてのWeb.GovForms分析データが *含まれます。*

   * **we-gov-forms.config.public-&lt;version>.zip**  — フォームデータモデルやサービスバインディングの問題を回避するために、プレースホルダークラウド設定を含むすべてのデフォルト設定ノードを *含みます。*


このパッケージに含まれるアセットは次のとおりです。

* 編集可能なテンプレートを含むAEMサイトページ
* AEM Forms適応Forms
* AEM Forms・インタラクティブ・コミュニケーション(印刷およびWebチャネル)
* AEM FormsXDPレコードドキュメント
* AEM FormsMSダイナミクスFormsデータモデル
* Adobe Sign統合
* AEMワークフローモデル
* AEM Assetsサンプル画像
* Apache Derbyデータベースのサンプル（メモリ内）
* Apache Derbyデータソース（フォームデータモデルで使用）

## デモパッケージのインストール{#demo-package-installation}

この節では、デモパッケージのインストールについて説明します。

### ソフトウェア配布{#from-software-distribution}から

1. [ソフトウェア配布](https://experience.adobe.com/downloads)を開きます。 ソフトウェアディストリビューションにログインするには、Adobe ID が必要です。
1. ヘッダーメニューにある&#x200B;**[!UICONTROL Adobe Experience Manager]**&#x200B;をタップします。
1. 「**[!UICONTROL フィルター]**」セクションで、
   1. 「**[!UICONTROL ソリューション]**」ドロップダウンリストから「**[!UICONTROL Forms]**」を選択します。
   2. パッケージのバージョンとタイプを選択します。 また、「**[!UICONTROL ダウンロードを検索]**」オプションを使用して、結果をフィルターすることもできます。
1. **we-gov-forms.pkg.all-&lt;version>.zip**&#x200B;パッケージ名をタップし、「**[!UICONTROL EULA条件に同意する]**」を選択して、「**[!UICONTROL ダウンロード]**」をタップします。
1. [Package Manager](https://docs.adobe.com/content/help/ja-JP/experience-manager-65/administering/contentmanagement/package-manager.html)を開き、「**[!UICONTROL パッケージをアップロード]**」をクリックして、パッケージをアップロードします。
1. パッケージを選択し、「**[!UICONTROL インストール]**」をクリックします。

   ![govフォームパッケージ](assets/wegov_forms_package.jpg)

1. インストールプロセスを完了できるようにします。
1. *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html?wcmmode=disabled*&#x200B;に移動し、インストールが正常に完了したことを確認します。

### ローカルZIPファイル{#from-a-local-zip-file}から

1. **we-gov-forms.pkg.all-&lt;version>.zip**&#x200B;ファイルをダウンロードして探します。
1. *https://&lt;aemserver>:&lt;port>/crx/packmgr/index.jsp*&#x200B;に移動します。
1. 「パッケージをアップロード」オプションを選択します。

   ![パッケージのアップロードオプション](assets/upload_package.jpg)

1. ファイルブラウザーを使用して、ダウンロードしたZIPファイルに移動し、選択します。
1. 「開く」をクリックしてアップロードします。
1. アップロードが完了したら、「インストール」オプションを選択してパッケージをインストールします。

   ![WeGovFormsパッケージのインストール](assets/wegov_forms_package-1.jpg)

1. インストールプロセスを完了できるようにします。
1. *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html?wcmmode=disabled*&#x200B;に移動し、インストールが正常に完了したことを確認します。

### 新しいパッケージバージョン{#installing-new-package-versions}のインストール

新しいパッケージバージョンをインストールするには、4.1および4.2で定義されている手順に従います。新しいパッケージバージョンをインストールし、別の古いパッケージを既にインストールすることは可能ですが、最初に古いパッケージバージョンをアンインストールすることをお勧めします。 これを行うには、次の手順に従います。

1. *https://&lt;aemserver>:&lt;port>/crx/packmgr/index.jsp*&#x200B;に移動します。
1. 古い&#x200B;**we-gov-forms.pkg.all-&lt;version>.zip**&#x200B;ファイルを探します。
1. 「詳細」オプションを選択します。
1. ドロップダウンで[アンインストール]オプションを選択します。

   ![WeGovパッケージのアンインストール](assets/uninstall_wegov_forms_package.jpg)

1. 確認の上で、もう一度「Uninstall」（アンインストール）を選択し、アンインストールプロセスを完了させます。

## デモパッケージ構成{#demo-package-configuration}

この節では、プレゼンテーション前のデモパッケージのデプロイメント完了後の設定の詳細と手順について説明します。

### 架空のユーザー設定{#fictional-user-configuration}

1. *https://&lt;aemserver>:&lt;port>/libs/granite/security/content/groupadmin.html*&#x200B;に移動します。
1. 以下のタスクを実行するには、管理者としてログインします。
1. ページの最後まで下にスクロールすると、すべてのユーザーグループが読み込まれます。
1. 「**workflow**」を検索します。
1. 「**workflow-users**」グループを選択し、「Properties」をクリックします。
1. 「メンバー」タブに移動します。
1. 「ユーザーまたはグループを選択」フィールドに&#x200B;**wegov**&#x200B;と入力します。
1. 「**We.GovFormsユーザー**」のドロップダウンから選択します。

   ![ワークフローユーザーのグループ設定の編集](assets/edit_group_settings.jpg)

1. メニューバーの「保存して閉じる」をクリックします。
1. 手順2 ～ 7を繰り返して、「**analytics**」を検索し、「**Analytics管理者**」グループを選択して、「**We.GovFormsユーザー**」グループをメンバーとして追加します。
1. 手順2 ～ 7を繰り返して、「**forms users**」を検索し、「**forms-power-users**」グループを選択して、「**We.GovFormsユーザー**」グループをメンバーとして追加します。
1. 手順2 ～ 7を繰り返して、「**forms-users**」を検索し、「**forms-users**」グループを選択して、次に「**We.Gov Users**」グループをメンバーとして追加します。

### 電子メールサーバーの設定{#email-server-configuration}

1. セットアップドキュメント[電子メール通知の設定](/help/sites-administering/notification.md)を確認
1. このタスクを実行するには、管理者としてログインします。
1. *https://&lt;aemserver>:&lt;port>/system/console/configMgr*&#x200B;に移動します。
1. 設定する&#x200B;**Day CQ Mail Service**&#x200B;サービスを探してクリックします。

   ![Day CQ 電子メールサービスの設定](assets/day_cq_mail_service.jpg)

1. 任意のSMTPサーバーに接続するようにサービスを設定します。

   1. **SMTP Server hostname**:例：(smtp.gmail.com)
   1. **サーバーポート**:例：SSLを使用したgmailの場合は(465)
   1. **SMTP User:** demo@  &lt;companyname> .com
   1. **&quot;送信者&quot;アドレス**:aemformsdemo@adobe.com

   ![SMTPの設定](assets/configure_smtp.jpg)

1. 「保存」をクリックして設定を保存します。

### （オプション）AEM SSL設定{#aemsslconfig}

この節では、Adobe Signクラウドの設定を行うためのAEMインスタンスでのSSLの設定について詳しく説明します。

**参照:**

1. [デフォルトの SSL](/help/sites-administering/ssl-by-default.md)

**備考:**

1. https://&lt;aemserver>:&lt;port>/aem/inboxに移動します。ここで、前述の「ドキュメントの参照」リンクで説明されているプロセスを完了できます。
1. `we-gov-forms.pkg.all-[version].zip`パッケージには、サンプルのSSLキーと証明書が含まれており、この証明書はパッケージの一部である`we-gov-forms.pkg.all-[version].zip/ssl`フォルダーを展開するとアクセスできます。

1. SSL証明書とキーの詳細：

   1. &quot;CN=localhost&quot;に発行される
   1. 10年間の有効性
   1. password「password」のパスワード値
1. 秘密鍵は&#x200B;*localhostprivate.der*&#x200B;です。
1. 証明書は&#x200B;*localhost.crt*&#x200B;です。
1. 「次へ」をクリックします。
1. HTTPSホスト名は、*localhost*&#x200B;に設定する必要があります。
1. ポートは、システムが公開したポートに設定する必要があります。

### （オプション）Adobe Signクラウドの設定{#adobe-sign-cloud-configuration}

この節では、Adobe Signクラウドの設定の詳細と手順について説明します。

**参照:**

1. [Adobe Sign を AEM Forms に統合する](adobe-sign-integration-adaptive-forms.md)

#### クラウド設定{#cloud-configuration}

1. 前提条件を確認します。 必要なSSL設定については、[AEM SSL設定](../../forms/using/forms-install-configure-gov-reference-site.md#aemsslconfig)を参照してください。
1. 次の URL に移動します。

   *https://&lt;aemserver>:&lt;port>/libs/adobesign/cloudservices/adobesign.html/conf/we-gov*

   >[!NOTE]
   >
   >AEMサーバーへのアクセスに使用するURLは、Adobe SignのOAuthリダイレクトURIで設定されたURLと一致し、設定の問題(例：*https://&lt;aemserver>:&lt;port>/mnt/overlay/adobesign/cloudservices/adobesign/properties.html*)

1. 「We.govAdobe Sign」設定を選択します。
1. 「プロパティ」をクリックします。
1. 「設定」タブに移動します。
1. 認証URLを入力します。例：[https://secure.na1.echosign.com/public/oauth](https://secure.na1.echosign.com/public/oauth)
1. 設定済みのAdobe Signインスタンスから、設定済みのクライアントIDとクライアントシークレットを指定します。
1. [Adobe Signに接続]をクリックします。
1. 接続が完了したら、「保存して閉じる」をクリックして統合を完了します。

### （オプション） MS Dynamicsクラウド構成{#ms-dynamics-cloud-configuration}

この節では、MS Dynamics Cloudの構成の詳細と手順を説明します。

**参照:**

1. [Microsoft Dynamics OData の設定](https://docs.adobe.com/content/help/en/experience-manager-64/forms/form-data-model/ms-dynamics-odata-configuration.html)
1. [Microsoft Dynamics forAEM Formsの構成](https://helpx.adobe.com/experience-manager/kt/forms/using/config-dynamics-for-aem-forms.html)

#### MS Dynamics ODataクラウドサービス{#ms-dynamics-odata-cloud-service}

1. 次の URL に移動します。

   https://&lt;aemserver>:&lt;port>/libs/fd/fdm/gui/components/admin/fdmcloudservice/fdm.html/conf/we-gov

   1. MS Dynamicsアプリケーション登録で構成されたのと同じリダイレクトURLを使用してサーバーにアクセスしていることを確認してください。

1. &quot;Microsoft Dynamics ODataCloud Service&quot;構成を選択します。
1. 「プロパティ」をクリックします。

   ![Microsoft ODataCloud Serviceのプロパティ](assets/properties_odata_cloud_service.jpg)

1. 「認証の設定」タブに移動します。
1. 次の詳細を入力します。

   1. **サービスルート：** 例：https://msdynamicsserver.api.crm3.dynamics.com/api/data/v9.1/
   1. **認証の種類：** OAuth 2.0
   1. **認証の設定** (この情報を収集するには、 [MS Dynamicsクラウド構成](../../forms/using/forms-install-configure-gov-reference-site.md#dynamicsconfig) 設定を参照してください):

      1. クライアントID -アプリケーション IDとも呼ばれる
      1. クライアントの秘密鍵
      1. OAuth URL — 例：[https://login.windows.net/common/oauth2/authorize](https://login.windows.net/common/oauth2/authorize)
      1. 更新トークンURL — 例：[https://login.windows.net/common/oauth2/token](https://login.windows.net/common/oauth2/token)
      1. アクセストークンURL — 例：[https://login.windows.net/common/oauth2/token](https://login.windows.net/common/oauth2/token)
      1. 認証スコープ — **openid**
      1. 認証ヘッダー — **承認ベアラー**
      1. リソース — 例：[https://msdynamicsserver.api.crm3.dynamics.com](https://msdynamicsserver.api.crm3.dynamics.com)
   1. 「OAuthに接続」をクリックします。


1. 認証が成功したら、「保存して閉じる」をクリックして統合を完了します。

#### MS Dynamicsクラウド構成設定{#dynamicsconfig}

この節で説明する手順は、MS Dynamics CloudインスタンスからクライアントID、クライアントシークレット、および詳細を見つけるのに役立ちます。

1. [https://portal.azure.com/](https://portal.azure.com/)に移動し、ログインします。
1. 左側のメニューから「All Services」を選択します。
1. 「アプリの登録」を検索または移動します。
1. 既存の申込み登録を作成または選択します。
1. AEMクラウド設定のOAuth **クライアントID**&#x200B;として使用する&#x200B;**アプリケーション ID**&#x200B;をコピーします
1. 「設定」または「マニフェスト」をクリックして、**返信URLを設定します。**

   1. このURLは、ODataサービスを設定する際に、AEMサーバーへのアクセスに使用されるURLと一致する必要があります。

1. 設定表示で、「キー」をクリックして表示で新しいキーを作成します(これは、AEMのクライアントシークレットとして使用されます)。

   1. 後でAzureまたはAEMで表示できないので、キーのコピーを保存してください。

1. リソースURL/サービスルートURLを見つけるには、MS Dynamicsインスタンスダッシュボードに移動します。
1. 上部ナビゲーションバーで、「Sales」をクリックするか、独自のインスタンスタイプをクリックし、「Select Settings」をクリックします。
1. 右下の「カスタマイズ」と「開発者向けリソース」をクリックします。
1. サービスルートURLは次のとおりです。例：

   *[https://msdynamicsserver.api.crm3.dynamics.com/api/data/v9.1/](https://msdynamicsserver.api.crm3.dynamics.com/api/data/v9.1/)*

1. 更新とアクセストークンURLの詳細は、次を参照してください。

   *[https://docs.microsoft.com/en-us/rest/api/datacatalog/authenticate-a-client-app](https://docs.microsoft.com/en-us/rest/api/datacatalog/authenticate-a-client-app)*

#### Formsデータモデル（ダイナミクス）のテスト{#testing-the-form-data-model}

クラウドの設定が完了したら、フォームデータモデルをテストする必要があります。

1.  に移動します。

   *https://&lt;aemserver>:&lt;port>/aem/forms.html/content/dam/formsanddocuments-fdm/we-gov*

1. 「Web.gov Microsoft Dynamics CRM FDM」を選択し、「プロパティ」を選択します。

   ![Dynamics CRM FDMのプロパティ](assets/properties_dynamics_crm.jpg)

1. 「ソースを更新」タブに移動します。
1. 「Context-Aware Configuration」が「/conf/we-gov」に設定され、設定済みのデータソースが「ms-dynamics-odata-cloud-service」であることを確認します。

   ![設定済みのデータソース](assets/configured_data_source.jpg)

1. フォームデータモデルを編集します。

1. サービスをテストし、設定済みのデータソースに正常に接続できることを確認します。

   >[!NOTE]
   サービスをテストした後、「**キャンセル**」をクリックして、意図しない変更がフォームデータモデルに反映されないことを確認します。

   >[!NOTE]
   データ・ソースがFDMに正常にバインドするには、AEMサーバーの再起動が必要であったと報告されています。

#### Formsデータモデル(Derby)のテスト{#test-fdm-derby}

クラウドの設定が完了したら、formsデータモデルをテストすることができます。

1. *https://&lt;aemserver>:&lt;port>/aem/forms.html/content/dam/formsanddocuments-fdm/we-gov*&#x200B;に移動します。

1. **Web.gov登録FDM**&#x200B;を選択し、**プロパティ**&#x200B;を選択します。

   ![Dynamics CRM FDMのプロパティ](assets/aftia-enrollment-fdm.jpg)

1. 「**ソースを更新**」タブに移動します。

1. **Context-Aware Configuration**&#x200B;が`/conf/we-gov`に設定されていて、設定済みのデータソースが&#x200B;**We.Gov Derby DS**&#x200B;であることを確認してください。

   ![Dynamics CRM FDMのプロパティ](assets/aftia-update-data-source.jpg)

1. 「**保存して閉じる**」をクリックします。

1. [サー](work-with-form-data-model.md#test-data-model-objects-and-services) ビスをテストし、設定済みのデータソースに正常に接続できることを確認します

   * 接続をテストするには、**HOMEMORTGAGEACCOUNT**&#x200B;を選択し、getサービスを提供します。 サービスおよびシステム管理者は、取得中のデータを確認できます。

### Adobe Analytics構成（オプション） {#adobe-analytics-configuration}

この節では、Adobe Analytics Cloud設定の詳細と説明を説明します。

**参照:**

* [Adobe Analytics との統合](../../sites-administering/adobeanalytics.md)

* [Adobe Analytics への接続とフレームワークの作成](../../sites-administering/adobeanalytics-connect.md)

* [ページ分析データの表示](../../sites-authoring/pa-using.md)

* [Analytics とレポートの設定](configure-analytics-forms-documents.md)

* [AEM Forms の分析レポートの確認方法と詳細](view-understand-aem-forms-analytics-reports.md)

### Adobe Analyticsクラウドサービスの設定{#adobe-analytics-cloud-service-configuration}

このパッケージは、Adobe Analyticsに接続するように事前に設定されています。 この設定を更新するために、次の手順を実行します。

1. *https://&lt;aemserver>:&lt;port>/libs/cq/core/content/tools/cloudservices.html*&#x200B;に移動します。
1. 「Adobe Analytics」セクションを探し、「設定を表示」リンクを選択します。
1. 「We.GovAdobe Analytics（Analytics設定）」設定を選択します。

   ![Analyticsクラウドサービスの設定](assets/analytics_config.jpg)

1. 「Edit」ボタンをクリックして、Adobe Analytics設定を更新します（Shared Secretを指定する必要があります）。 「Analyticsに接続」をクリックして接続し、「OK」をクリックして完了します。

   ![ウェゴヴAdobe Analytics](assets/wegov_adobe_analytics.jpg)

1. フレームワーク設定を更新する場合は、同じページで「Web.GovAdobe Analyticsフレームワーク（Analyticsフレームワーク）」をクリックします(オーサリングを有効にするには、「[AEMオーサリングを有効にする](../../forms/using/forms-install-configure-gov-reference-site.md#enableauthoring)」を参照)。

#### Adobe Analyticsユーザー資格情報の検索{#analytics-locating-user-credentials}

Adobe Analyticsアカウントのユーザー資格情報を見つけるには、アカウント管理者が次のタスクを実行する必要があります。

1. Adobe Experience Cloudポータルに移動します。
   * 管理者の資格情報を使用してログインします
1. メインダッシュボードでAdobe Analyticsアイコンを選択します。
   ![迅速なアクセス](assets/aftia-quick-access.jpg)
1. 「管理者」タブに移動し、「ユーザー管理（レガシー）」項目を選択します
   ![レポート](assets/aftia-reports.jpg)
1. 「**ユーザー**」タブを選択します。
   ![ユーザー管理](assets/aftia-user-management.jpg)
1. ユーザーのリストから目的のユーザーを選択します。
1. ページの下部までスクロールすると、ユーザー認証情報がページの下部に表示されます。
   ![アクセスを管理](assets/aftia-admin-user-access.jpg)
1. ユーザー名と共有暗号鍵の情報は、権限ボックスの右側に表示されます。
1. ユーザ名には名前の中にコロンが含まれることに注意してください。コロンの左にある情報はすべてユーザ名で、コロンの右にある情報はすべて会社名です。
   * 次に例を示します。*ユーザー名：会社名*

#### Adobe Analytics{#setup-user-authentication}でのユーザー認証のセットアップ

管理者は、次の操作を実行して、ユーザーにAEM Analyticsの権限を与えることができます。

1. Adobe Admin Consoleに移動します。

1. 管理コンソールに表示されるAnalyticsインスタンスをクリックします。

   * これは、管理ページのメインページにあります。

1. 「Analyticsフル管理者アクセス」を選択します。

1. プロファイル追加のユーザー。

   ![Analyticsの完全な管理者アクセス](assets/aftia-full-admin-access.jpg)

1. ユーザーIDがプロファイルにマッピングされたら、「権限」タブをクリックします。

1. すべての権限がプロファイルにマップされていることを確認します。

   ![権限の編集](assets/aftia-admin-access-edit.jpg)

1. ユーザーのログイン機能に対して権限がマッピングされると、数時間かかる場合があります。

### Adobe Analyticsレポート{#adobe-analytics-reporting}

#### 表示Adobe Analyticsサイトレポート{#view-adobe-analytics-sites-reporting}

>[!NOTE]
`we-gov-forms.ui.analytics-<version>.zip`パッケージがインストールされている場合、AEM Forms解析データは、オフライン時またはAdobe Analyticsクラウド設定なしに使用できますが、AEM Sitesデータにはアクティブなクラウド設定が必要です。

1. *https://&lt;aemserver>:&lt;port>/sites.html/content*&#x200B;に移動します。
1. 「AEM FormsWe.Govサイト」を選択して、サイトページを表示します。
1. サイトページ（ホームなど）の1つを選択し、「Analytics &amp;Recommendations」を選択します。

   ![分析とRecommendations](assets/analytics_recommendations.jpg)

1. このページには、AEM Sites・ページに関連するAdobe Analyticsから取得した情報が表示されます(注意：設計上、この情報はAdobe Analyticsから定期的に更新され、リアルタイムでは表示されません)。

   ![AEM Sites分析](assets/sites_analysis.jpg)

1. ページ表示ページ（手順3.でアクセス）に戻ると、「リスト表示」の表示項目の表示設定を変更して、ページ表示情報を表示することもできます。
1. [表示]ドロップダウンメニューを見つけ、[リスト表示]を選択します。

   ![リスト表示](assets/list_view.jpg)

1. 同じメニューで「表示設定」を選択し、「Analytics」セクションから表示する列を選択します。

   ![列の設定](assets/configure_columns.jpg)

1. 「更新」をクリックして、新しい列を利用可能にします。

   ![新しい列の表示](assets/new_columns_display.jpg)

#### 表示Adobe Analyticsフォームレポート{#view-adobe-analytics-forms-reporting}

>[!NOTE]
`we-gov-forms.ui.analytics-<version>.zip`パッケージがインストールされている場合、AEM Forms解析データは、オフライン時またはAdobe Analyticsクラウド設定なしに使用できますが、AEM Sitesデータにはアクティブなクラウド設定が必要です。

1.  に移動します。

   *https://&lt;aemserver>:&lt;port>/aem/forms.html/content/dam/formsanddocuments/adobe-gov-forms*

1. 「Enrollment Application For Health Benefits」アダプティブフォームを選択し、「Analytics Report」オプションを選択します。

   ![Analyticsレポート](assets/analytics_report.jpg)

1. ページが読み込まれるのを待ち、Analyticsレポートデータを表示します。

   ![表示分析レポートデータ](assets/analytics_report_data.jpg)

### Adobe自動Forms構成有効化{#automated-forms-enablement}

AdobeFormsとの間でAEM Formsのインストールと設定を行うには、コンバージョンツールのユーザは次の作業を行う必要があります。

1. AdobeIOへのアクセス。

1. AdobeFormsコンバージョンサービスとの統合を作成する権限です。

1. AdobeAEM 6.5の最新のサービスパックは、作成者として実行されています。

詳細な手順を読む前に、次の点を確認してください。

* [自動フォーム変換サービスの設定](https://docs.adobe.com/content/help/en/aem-forms-automated-conversion-service/using/configure-service.html)

#### IMS設定パート1 {#creating-ims-config}の作成

フォーム変換ツールと正しく通信できるようにサービスを設定するには、ユーザーがIdentity Managementシステム(IMS)サービスをAdobe I/Oに登録できるように設定する必要があります。

1. https://&lt;aemserver>:&lt;port>に移動し、「Adobeエクスペリエンス」をクリックします。
左上のマネージャー/ツール/セキュリティ/AdobeIMS設定

1. 「作成」をクリックします。

1. 下の画像のアクションを実行します。

   ![IMSテクニカルアカウントの設定](assets/aftia-technical-account-configuration.jpg)

1. 証明書は必ずダウンロードしてください。

1. 残りの構成は実行しないでください。[「Adobe I/Oでの統合の作成](#create-integration-adobeio)」の節を参照してください。

>[!NOTE]
この節で作成した証明書は、Adobe I/Oでの統合サービスの作成に使用されます。統合サービスでユーザーが作成されると、ユーザーはAdobe I/Oからの情報を使用して設定を完了できます。

#### Adobe I/Oでの統合の作成{#create-integration-adobeio}

統合を作成するには、Adobe管理者に問い合わせない場合は、システムドメイン内で統合を作成できる権限があることを確認してください。

1. [Adobe I/Oコンソール](https://console.adobe.io/)に移動します。

1. 「統合を作成」をクリックします。

1. 「APIへのアクセス」を選択します。

1. 正しいグループ(右上のドロップダウンリスト)に属していることを確認します。

1. 「Experience Cloud」セクションで、「Formsコンバージョンツール」を選択します。

1. 「続行」をクリックします。

1. 統合の名前と説明を入力します。

1. セクション2.1の公開鍵を使用すると、鍵の統合内に配置されます。

1. automated forms conversionのプロファイルを選択します。

   ![新しい統合の作成](assets/aftia-create-new-integration.jpg)

#### IMS設定パート2 {#create-ims-config-part-next}の作成

これで、統合を作成したので、IMS設定のインストールを完了できます。

1. 接続の詳細を公開するには、Adobe I/O内の統合をクリックします。

1. AEM内でIMS設定に移動します（ツール/セキュリティ/IMS）。

1. IMS設定画面で「次へ」をクリックします。

1. 認証サーバー（スクリーンショットに表示されている値）を入力します。

1. APIキーを入力します。

1. クライアントシークレットを入力します(表示するには、Adobe I/Oの統合で「公開」をクリックする必要があります)。

1. Adobe I/Oの「JWT」タブをクリックして、JWTペイロードを取得し、IMS設定のペイロードに貼り付けます。

   ![ペイロードIMSの設定](assets/aftia-payload-ims-config.jpg)

1. 作成したIMS設定をクリックして「ヘルスチェック」を選択すると、次の結果が表示されます。

   ![正常性の確認](assets/aftia-health-confirmation.jpg)

#### クラウドの設定（Web.Gov AFC実稼働環境） {#configure-cloud-configuration}

IMSの設定が完了したら、AEMでクラウドの設定を確認します。 設定が存在しない場合は、次の手順を実行してAEMでクラウド設定を作成します。

1. ブラウザーを開き、システムURL https://&lt;domain_name>:&lt;system_port>に移動します。

1. 画面の左上隅にあるAdobe Experience Manager/ツール/Cloud Services/Forms会話の自動設定をクリックします。

1. 設定を配置する設定フォルダを選択します。

1. 「作成」をクリックします。

1. 下のスクリーンショットに情報を入力してください。

   ![AFC生産](assets/aftia-afc-production.jpg)

1. 設定にタイトルと名前を指定します。

1. システムのサービスURLは、https://aemformsconversion.adobe.io/に設定されます。

1. テンプレートURL */conf/we-gov/settings/wcm/templates/we-gov-flamingo-template*。

1. テーマURL:*/content/dam/formsanddocuments-themes/adobe-gov-forms-themes/we-gov-theme*

1. 「次へ」をクリックします。

1. この設定では、2つのチェックボックスの値を空のままにしました。

   * これらのオプションの詳細については、[クラウドサービスの設定](https://docs.adobe.com/content/help/en/aem-forms-automated-conversion-service/using/configure-service.html#configure-the-cloud-service)を参照してください。

#### クラウドの設定（Web.Finance AFC実稼働環境） {#configure-cloud-configuration-wefinance}

IMSの設定が完了したら、AEMでクラウド設定を作成できます。

1. ブラウザーを開き、システムURL https://&lt;domain_name>:&lt;system_port>に移動します。

1. 画面の左上隅にあるAdobe Experience Manager/ツール/Cloud Services/Forms会話の自動設定をクリックします。

1. 設定を配置する設定フォルダを選択します。

1. 「作成」をクリックします。

1. 下のスクリーンショットに情報を入力してください。

   ![We.AFC生産に融資](assets/aftia-wefinance-afc-prod.jpg)

1. 設定にタイトルと名前を指定します。

1. システムのサービスURLはhttps://aemformsconversion.adobe.io/に設定されます。

1. テンプレートURL:*/conf/we-finance/settings/wcm/templates/we-finance-adaptive-form*

1. テーマURL:*/content/dam/formsanddocuments-テーマ/adobe-finance-forms-テーマ/we-finance-theme*

1. 「次へ」をクリックします。

1. この設定では、2つのチェックボックスの値を空のままにしました。

   * これらのオプションの詳細については、[クラウドサービスの設定](https://docs.adobe.com/content/help/en/aem-forms-automated-conversion-service/using/configure-service.html#configure-the-cloud-service)を参照してください。

#### フォーム変換（Web.Gov登録申込）のテスト{#test-forms-conversion}

設定が完了すると、ユーザーはPDFドキュメントをアップロードしてテストできます。

1. AEMシステムhttps://&lt;ドメイン名>:&lt;システムポート>に移動します。

1. Forms/Forms&amp;ドキュメント/AEM FormsWe.govForms/AFCをクリックします。

1. Web.Gov Enrollment Application PDFを選択します。

1. 右上隅の「**開始自動コンバージョン**」ボタンをクリックします。

1. 次に示すように、このオプションが表示されます。

   ![変換されたアダプティブフォーム](assets/aftia-converted-adaptive-form.jpg)

1. ボタンを選択すると、次のオプションが表示されます

   * *We.Gov AFC Production*&#x200B;の構成をユーザーが選択していることを確認します。

   ![変換設定](assets/aftia-conversion-settings.jpg)

   ![詳細な変換設定](assets/aftia-conversion-settings-2.jpg)

1. 使用するすべての開始を設定したら、「オプションの変換」を選択します。

1. 変換プロセスが始まると、次の画面が表示されます。

   ![変換設定](assets/aftia-conversion-in-progress.jpg)

1. 変換が完了すると、次の画面が表示されます。

   ![変換されたアダプティブフォーム](assets/aftia-converted-adaptive-form-2.jpg)

   **Output**&#x200B;フォルダーをクリックして、生成されたアダプティブフォームを表示します。

#### 既知の問題とメモ{#known-issues-notes}

automated forms conversionサービスには、特定の[ベストプラクティス、既知の複雑なパターン](https://docs.adobe.com/content/help/en/aem-forms-automated-conversion-service/using/styles-and-pattern-considerations-and-best-practices.html)、[既知の問題](https://docs.adobe.com/content/help/en/aem-forms-automated-conversion-service/using/known-issues.html)が含まれます。 AEM FormsAutomated forms conversionサービスの使用を開始する前に、これらを確認してください。

1. 変換後にフォームをFDMに連結する場合は、データ連結を有効にせずに「アダプティブフォームを生成」を生成します。

1. テンプレートフォルダーでjcr:read for everyone権限が有効になっていることを確認してください。有効になっていない場合、サービスユーザーはリポジトリからテンプレートを読み取れなくなり、変換は失敗します。

## デモパッケージのカスタマイズ{#demo-package-customizations}

この節では、デモのカスタマイズ手順について説明します。

### テンプレートのカスタマイズ{#templates-customization}

編集可能なテンプレートは次の場所にあります。

*https://&lt;aemserver>:&lt;port>/libs/wcm/core/content/sites/templates.html/conf/we-gov*

これらのテンプレートには、AEMサイト、アダプティブフォーム、およびインタラクティブコミュニケーションの各テンプレートが含まれ、以下の場所にあるコンポーネントを使用して作成およびアセンブルされます。

*https://&lt;aemserver>:&lt;port>/crx/de/index.jsp#/apps/we-gov/components*

#### スタイルシステム{#customizetemplates}

このサイトにはクライアントライブラリも含まれ、その1つがBootstrap4 ( [https://getbootstrap.com/](https://getbootstrap.com/) )を読み込みます。 このクライアントライブラリは、

*https://&lt;aemserver>:&lt;port>/crx/de/index.jsp#/apps/we-gov/clientlibs/clientlib-base/css/bootstrap*

このパッケージに含まれる編集可能なテンプレートには、Bootstrap4のCSSクラスを使用してページネーションやスタイルなどを設定するテンプレート/ページポリシーもあらかじめ設定されています。 テンプレートポリシーに追加されていないクラスもありますが、Bootstrap4でサポートされているクラスはすべてポリシーに追加できます。 使用可能なクラスのリストについては、「はじめに」ページを参照してください。

[https://getbootstrap.com/docs/4.1/getting-started/introduction/](https://getbootstrap.com/docs/4.1/getting-started/introduction/)

このパッケージに含まれるテンプレートは、次のスタイルシステムもサポートします。

[スタイルシステム](../../sites-authoring/style-system.md)

#### テンプレートロゴ{#template-logos}

プロジェクトDAMアセットにはWe.Govロゴや画像も含まれます。 これらのアセットは、次の場所で使用できます。

*https://&lt;aemserver>:&lt;port>/assets.html/content/dam/we-gov*

ページおよびフォームテンプレートを編集する場合、ナビゲーションとフッターのコンポーネントを編集してブランドロゴを更新することを選択できます。 次のコンポーネントは、ロゴの更新に使用できる設定可能なブランドとロゴのダイアログをオファーします。

![テンプレートロゴ](assets/template_logos.jpg)

詳しくは、「ページコンテンツの編集」を参照してください。

[ページのコンテンツの編集](../../sites-authoring/editing-content.md)

### サイトページのカスタマイズ{#sites-pages-customization}

すべてのサイトページは次の場所から利用できます。*https://&lt;aemserver>:&lt;port>/sites.html/content/we-gov*

これらのサイトページでは、AEM Gridパッケージを使用して、いくつかのコンポーネントのレイアウトを制御します。

#### スタイルシステム{#style-system}

このパッケージに含まれるページは、次のスタイルシステムもサポートします。

[スタイルシステム](../../sites-authoring/style-system.md)

サポートされるスタイルに関するドキュメントについては、[テンプレートのカスタマイズスタイルシステム](../../forms/using/forms-install-configure-gov-reference-site.md#customizetemplates)を参照してください。

### アダプティブフォームのカスタマイズ{#adaptive-forms-customization}

すべてのアダプティブフォームは、次の場所から利用できます。

*https://&lt;aemserver>:&lt;port>/aem/forms.html/content/dam/formsanddocuments/adobe-gov-forms*

これらのフォームは、特定の用途に合わせてカスタマイズできます。 フォームが正しく機能し続けるように、特定のフィールドと送信ロジックを変更しないでください。 これには以下が含まれます。

**登録申請（健康保険給付）:**

* contact_id — 送信中にMS Dynamicsの連絡先IDを受け取るために使用される非表示フィールド
* 送信 — 送信ボタンのロジックに、コールバックをサポートするためのカスタマイズが必要。 カスタマイズはドキュメントに記載されていますが、Formsデータモデルを使用してMS Dynamicsに対してPOSTとGETの両方の操作を実行する際に、フォームを送信するために大きなスクリプトが必要でした。
* [ルートパネル — 初期化]イベントは、AEM Inbox Granite UIコンポーネントを変更できないため、できる限り押し付けがましい方法でAEM InboxにMS Dynamicsボタンを追加するために使用します。

#### アダプティブフォームのスタイル設定{#adaptive-form-styling}

アダプティブフォームは、スタイルエディターまたはテーマエディターを使用してスタイルを設定することもできます。

* [アダプティブフォームコンポーネントのインラインスタイリング](inline-style-adaptive-forms.md)
* [テーマを作成して使用する](themes.md)

### ワークフローのカスタマイズ{#workflow-customization}

登録アダプティブフォームは、処理のためにOSGIワークフローに送信されます。 このワークフローは、*https://&lt;aemserver>:&lt;port>/conf/we-gov/settings/models/we-gov-process.html*&#x200B;にあります。

一部の制限により、このワークフローにはいくつかのスクリプトとカスタムOSGIワークフロープロセスステップが含まれています。 これらのワークフロー手順は一般的な手順として作成されたもので、設定ダイアログでは作成されていません。 現時点では、ワークフロー手順の設定はプロセスの引数に依存します。

すべてのワークフロー手順のJavaコードは、**we-gov-forms.core-&lt;version>.jar**&#x200B;バンドルに含まれています。

## デモに関する考慮事項と既知の問題{#demo-considerations-and-known-issues}

この節では、デモ機能と、デモプロセスの過程で特別な考慮が必要となる場合がある設計上の意思決定に関する情報を説明します。

### デモに関する考慮事項{#demo-considerations}

* AGRS-159に従って、登録アダプティブフォームで使用される連絡先の名前（最初、中間、最後）が一意であることを確認します。
* 登録アダプティブフォームは、フォームの電子メールフィールドに指定された電子メールにAdobe Sign電子メールを送信します。 その電子メールアドレスは、Adobe Signクラウド設定の設定に使用した電子メールと同じ電子メールアドレスにすることはできません。

### 既知の問題 {#known-issues}

* (AGRS-120)サイトナビゲーションコンポーネントは、現在、2レベル以上の深さの入れ子ページをサポートしていません。
* (AGRS-159)現在のMS Dynamics FDMは、最初に2つの操作を実行し、登録アダプティブフォームデータをDynamicsにPOSTし、次に連絡先IDを取得するためにユーザーレコードを取得する必要があります。 現在の状態では、同じ名前を持つ2人以上のユーザーがDynamicsに存在し、登録アダプティブフォームでの送信が許可されない場合、連絡先IDの取得は失敗します。

## アクセシビリティテストの設定{#configure-accessibility-testing}

### {#enable-chrome-add-on}上でのアクセシビリティテストChrome追加の有効化

最初にアクセシビリティテストを実行するには、Chromeプラグインをインストールする必要があります。このプラグインは[ここ](https://chrome.google.com/webstore/detail/accessibility-developer-t/fpkknkljclfencbdbgkenhalefipecmb?hl=en)にあります。

インストールが完了したら、テストするページをChromeブラウザーに読み込みます(注意：複数のタブを開くとスコアに影響する場合があるので、タブを1つだけ開くことをお勧めします)。 ページが読み込まれたら、
**ページの**&#x200B;を右クリックし、「**監査**」タブを選択します。 開発者は、アクセシビリティプラグインによって実行される監査のタイプを選択できます。 必要なオプションをすべて選択すると、「レポートを生成」ボタンを選択できます。 これにより、全体的なアクセシビリティの評価と、全体的なアクセシビリティの評価を高めるために使用できる要素を示すPDFドキュメントが生成されます。

レポートの実行後は、次の項目が表示されます。

![アクセシビリティレポート](assets/aftia-accessibility.jpg)

ユーザーの前に表示される数は、獲得したアクセシビリティの評価全体です。 スコアの後でこの値がどのように計算されたかについても説明します。

これを書き出す場合は、画面の右側の3つのボタンをクリックして、プラグインのオファーを追加するオプションを選択できます。

![アクセシビリティレポート](assets/aftia-accessibility-report.jpg)

### ウルタマリンテーマ{#ultramarine-theme}

Adobeが管理する、公に提供されるUltramarineテーマは、
`we-gov-forms.pkg.all-<version>.zip`インストール可能なZIPファイル。 CRXを使用してこのパッケージをインストールします。

Package Managerを使用すると、**Forms** > **テーマ** > **リファレンステーマ** > **ウルトラマリンアクセス可能**&#x200B;に移動して、AEM Formsのウルトラマリンテーマにアクセスできます。

![Ultramarine テーマ](assets/aftia-ultramarine-theme.jpg)

## 設定オプション {#configuration-options}

ユーザーは、次のような様々なワークフローサービスオプションを設定できます。

1. Microsoft Dynamicsエントリ
1. Adobe Sign
1. AEMカスタムコミュニケーション管理
1. Adobe Analytics

ワークフローユーザーがワークフロー内で有効になるように設定するには、次のタスクを実行する必要があります。

1. https://&#39;[server]:[port]&#39;/system/console/configMgrに移動します。

1. *WeGov Configurations*&#x200B;を探します。

1. サービス定義を開き、選択したサービスをワークフロー内で呼び出せるようにします。

   >[!NOTE]
   ユーザーがConfiguration Managerページ内でサービスを有効にしたので、要求された外部サービスと通信するために、ユーザーは引き続きサービス設定を行う必要があります。

   ![govフォームパッケージ](assets/aftia-configuration-options.jpg)

1. 設定を保存するには、「保存」ボタンをクリックします。

## 次の手順 {#next-steps}

これで、Web.Govリファレンスサイトを参照する設定が完了しました。 We.Govリファレンスサイトのワークフローと手順について詳しくは、[We.Govリファレンスサイトのチュートリアル](../../forms/using/forms-gov-reference-site-user-demo.md)を参照してください。
