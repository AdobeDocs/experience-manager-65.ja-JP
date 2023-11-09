---
title: Facebook と Twitter を使用したソーシャルログイン
description: ソーシャルログインを使用すると、サイト訪問者はFacebookまたはTwitterアカウントでログインできます。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: aed9247c-eb81-470c-9fa4-a98c3df2dcaa
source-git-commit: 451fb472e170a79f9854efadf9be1d4fe0628b94
workflow-type: tm+mt
source-wordcount: '2773'
ht-degree: 3%

---

# Facebook と Twitter を使用したソーシャルログイン {#social-login-with-facebook-and-twitter}

ソーシャルログインとは、サイト訪問者に対して、自分のFacebookまたはTwitterアカウントでログインするオプションを提示する機能です。 したがって、許可されたFacebookまたはTwitterデータをAEMメンバープロファイルに含めます。

![socialloginweretail](assets/socialloginweretail.png)

## ソーシャルログインの概要 {#social-login-overview}

ソーシャルログインを含めるには、 *必須* カスタムのFacebookおよびTwitterアプリケーションを作成する。

we-retail サンプルは、FacebookおよびTwitterのサンプルアプリとクラウドサービスを提供していますが、 [実稼働用 web サイト](../../help/sites-administering/production-ready.md).

必要な手順は次のとおりです。

1. [OAuth 認証を有効にする](#adobe-granite-oauth-authentication-handler) すべてのAEMパブリッシュインスタンス上。

   OAuth を有効にしない場合、はログインに失敗します。

1. **作成** ソーシャルアプリとクラウドサービス。

   * facebookでのログインをサポートするには：

      * の作成 [Facebookアプリ](#create-a-facebook-app).
      * の作成と公開 [Facebook Connect Cloud Service](#create-a-facebook-connect-cloud-service).

   * ログインをサポートするには、次のTwitterを使用します。

      * の作成 [Twitterアプリ](#create-a-twitter-app).
      * の作成と公開 [TwitterConnect Cloud Service](#create-a-twitter-connect-cloud-service).

1. [**有効にする** ソーシャルログイン](#enable-social-login) コミュニティサイト用。

次の 2 つの基本的な概念があります。

1. **範囲** （権限）は、アプリがリクエストできるデータを指定します。

   * 101.FacebookとTwitter [AdobeGranite OAuth Application and Provider](#adobe-granite-oauth-application-and-provider) インスタンスの場合は、デフォルトで、アプリの基本的な権限がその範囲に含まれます。

1. **フィールド** (params) は、URL パラメーターを使用してリクエストされた実際のデータを指定します。

   * これらのフィールドは、 [AEM Communities Facebook OAuth Provider](#aem-communities-facebook-oauth-provider) および [AEM CommunitiesTwitterOAuth Provider](#aem-communities-twitter-oauth-provider).
   * ほとんどの使用例ではデフォルトのフィールドで十分ですが、変更できます。

## Facebook Login {#facebook-login}

### Facebook API バージョン {#facebook-api-version}

facebook Graph API がバージョン 1.0 のときに、ソーシャルログインと we-retail Facebookのサンプルが開発されました。AEM 6.4 GA およびAEM 6.3 SP1 のソーシャルログインが更新され、新しいFacebook Graph API 2.5 バージョンと連携するようになりました。

>[!NOTE]
>
>古いAEMバージョンの場合、ログで例外が発生する場合 **ここからトークンを抽出できません**、をそのAEMリリースの最新 CFP にアップグレードします。

facebook Graph API のバージョン情報については、 [Facebook API 変更ログ](https://developers.facebook.com/docs/apps/changelog).

### facebookアプリの作成 {#create-a-facebook-app}

facebookソーシャルログインを有効にするには、適切に設定されたFacebookアプリケーションが必要です。

facebookアプリケーションを作成するには、Facebookの手順 ( [https://developers.facebook.com/apps/](https://developers.facebook.com/apps/). 手順の変更は、次の情報には反映されません。

一般に、Facebook API v2.7 以降：

* *新しいFacebookアプリの追加*
   * の場合 *Platform*、Web サイトを選択します。
      * の場合 *サイトの URL*，と入力します。 `  https://<server>:<port>.`
      * の場合 *表示名*」で、「 Facebook Connect サービスのタイトル」として使用するタイトルを入力します。
      * の場合 *カテゴリ*，推奨選択 *ページのアプリ*&#x200B;ですが、何でもかまいません。
      * *製品を追加： Facebook Login*
      * の場合 *有効な OAuth リダイレクト URI*，と入力します。 `  https://<server>:<port>.`

>[!NOTE]
>
>開発の場合、http://localhost:4503が機能します。

アプリケーションが作成されたら、 **[!UICONTROL アプリ ID]** および **[!UICONTROL App Secret]** 設定。 この情報は、 [Facebook cloud service](#createafacebookcloudservice).

### facebook ConnectCloud Serviceの作成 {#create-a-facebook-connect-cloud-service}

The [AdobeGranite OAuth Application and Provider](#adobe-granite-oauth-application-and-provider) クラウドサービス設定を作成することでインスタンス化されたインスタンスは、新しいユーザーが追加されるFacebookアプリケーションとメンバーグループを識別します。

1. AEMオーサーインスタンスで、管理者権限でログインします。
1. グローバルナビゲーションから、「 」を選択します。 **[!UICONTROL ツール]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Facebook Social ログイン設定]**.
1. 設定を選択 **[!UICONTROL コンテキストパス]**.

   **[!UICONTROL コンテキストパス]** は、コミュニティサイトの作成/編集時に選択したクラウド設定パスと同じである必要があります。

1. コンテキストパスの下にクラウドサービスの作成が有効になっているかどうかを確認します。
1. に移動します。 **[!UICONTROL ツール]** > **[!UICONTROL 一般]** > **[!UICONTROL 設定ブラウザー]**. コンテキストを選択し、プロパティを編集します。 まだ有効になっていない場合は、クラウド設定を有効にします。

   ![config-propertiespng](assets/config-propertiespng.png)

   * 詳しくは、[設定ブラウザー](/help/sites-administering/configurations.md)のドキュメントを参照してください。

1. **作成/編集** Facebookクラウドサービスの設定

   ![fbsocialloginconfigpng](assets/fbsocialloginconfigpng.png)

   * **[!UICONTROL タイトル]** (*必須*) Facebook App を識別する表示タイトルを入力します。 入力した名前を *表示名* facebookアプリ用。
   * **[!UICONTROL アプリ ID/API キー]** (*必須*) ***アプリ ID*** (Facebook App 用 ) これは、 [AdobeGranite OAuth Application and Provider](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#AdobeGraniteOAuthApplicationandProvider) ダイアログから作成されたインスタンス。
   * **[!UICONTROL App Secret]** (*必須*) ***App Secret*** (Facebook App 用 )
   * **[!UICONTROL ユーザーを作成]** オンにすると、FacebookアカウントでログインしたときにAEMユーザーエントリが作成され、選択したユーザーグループにメンバーとして追加されます。  デフォルトはオンです（強く推奨）。
   * **[!UICONTROL ユーザー ID をマスク]**：選択を解除したままにします。
   * **[!UICONTROL スコープメール]**：ユーザーの電子メール ID は、Facebookから取得する必要があります。
   * **[!UICONTROL ユーザーグループに追加]** 「ユーザーグループの追加」を選択して、1 つ以上の [メンバーグループ](https://helpx.adobe.com/experience-manager/6-3/communities/using/users.html) ユーザーを追加するコミュニティサイト用に作成されます。

   >[!NOTE]
   >
   >グループは、いつでも追加または削除できます。 ただし、既存のユーザーのメンバーシップには影響しません。 自動メンバーシップは、このフィールドの更新後に作成される新しいユーザーにのみ適用されます。 匿名ユーザーが無効になっているサイトの場合は、その非公開のコミュニティサイト向けに、対応するコミュニティメンバーグループにユーザーを追加するよう選択します。

   * 選択 **[!UICONTROL 保存]**.
   * **[!UICONTROL 公開]**.

結果は [AdobeGranite OAuth Application and Provider](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#adobe-granite-oauth-application-and-provider) 追加の範囲（権限）を追加しない限り、追加の変更を必要としないインスタンス。 デフォルトの範囲は、Facebookログインの標準の権限です。 追加のスコープが必要な場合は、OSGi 設定を直接編集する必要があります。 システム/コンソールを介して直接変更がおこなわれる場合は、上書きを避けるために、タッチ UI からクラウドサービス設定を編集しないでください。

### AEM Communities Facebook OAuth Provider {#aem-communities-facebook-oauth-provider}

AEM Communitiesプロバイダーは、 [AdobeGranite OAuth Application and Provider](#adobe-granite-oauth-application-and-provider) インスタンス。

このプロバイダーは次の操作を行うために編集が必要です：

* ユーザーの更新を許可
* フィールドを追加 [範囲内](#adobe-granite-oauth-application-and-provider)

   * デフォルトで許可されているすべてのフィールドがデフォルトで含まれるわけではありません。

編集が必要な場合は、各AEMパブリッシュインスタンスで次の手順を実行します。

1. 管理者権限でログインします。
1. 次に移動： [Web コンソール](../../help/sites-deploying/configuring-osgi.md). 例：http://localhost:4503/system/console/configMgr
1. AEM Communities Facebook OAuth Provider を見つけます。
1. 編集用に開く鉛筆アイコンを選択します。

   ![fboauthprov_png](assets/fboauthprov_png.png)

   * **[!UICONTROL OAuth Provider ID]**

     (*必須*) デフォルト値は *soco -facebook*. 編集しないでください。

   * **[!UICONTROL Cloud Service設定]**

     デフォルト値は `/etc/  cloudservices /  facebookconnect` です。編集しないでください。

   * **[!UICONTROL OAuth Provider Service Config]**

     デフォルト値は `/apps/social/facebookprovider/config/` です。編集しないでください。

   * **[!UICONTROL タグを有効にする]**

     編集しないでください。

   * **[!UICONTROL ユーザーパス]**

     リポジトリ内のユーザーデータが格納される場所。 コミュニティサイトでは、メンバーが互いのプロファイルを表示する権限を確保するために、パスをデフォルトにする必要があります */home/users/community*.

   * **[!UICONTROL フィールドを有効にする]**

     オンにすると、Facebookへのユーザー認証と情報のリクエストで、一覧表示されるフィールドが指定されます。 デフォルトはオフです。

   * **[!UICONTROL フィールド]**

     フィールドが有効な場合、Facebook Graph API を呼び出す際に、次のフィールドが含まれます。 フィールドは、クラウドサービス設定で定義された範囲内で許可する必要があります。 追加のフィールドには、Facebookの承認が必要な場合があります。 facebookドキュメントの「 Facebookログイン権限」の節を参照してください。 パラメーターとして追加されるデフォルトのフィールドは次のとおりです。

      * id
      * name
      * first_name
      * last_name
      * リンク
      * locale
      * 画像
      * timezone
      * updated_time
      * 検証済み
      * email

   フィールドが追加または変更された場合は、対応するデフォルト同期ハンドラー設定を更新して、マッピングを修正します。

   * **[!UICONTROL ユーザーを更新]**

     オンにすると、ログインのたびにリポジトリ内のユーザーデータが更新され、プロファイルの変更やリクエストされた追加データが反映されます。 初期設定はオフです。

#### 次の手順 {#next-steps}

次の手順は、FacebookとTwitterの両方で同じです。

* [クラウドサービス設定を公開する](#publishcloudservices)
* [コミュニティサイトに対して有効にする](#enable-social-login)

## Twitterログイン {#twitter-login}

### twitterアプリの作成 {#create-a-twitter-app}

ソーシャルログインを有効にするには、設定済みのTwitterTwitterが必要です。

最新の手順に従って、でTwitterアプリケーションを作成します。 [https://apps.twitter.com](https://apps.twitter.com/).

一般に、

1. を入力します。 *名前* これにより、web サイトのTwitterに対するユーザーアプリケーションが識別されます。
1. を入力します。 *説明*.
1. の場合 *web サイト*  — 入力 `https://<server>`.
1. の場合 *コールバック URL*  — 入力 `https://server`.

   >[!NOTE]
   >
   >ポートを指定する必要はありません。
   >
   >開発の場合、https://127.0.0.1/が機能します。

1. アプリケーションが作成されたら、 **[!UICONTROL 消費者 (API) キー]** および **[!UICONTROL 消費者 (API) 秘密鍵]**. この情報は、 [Twitterクラウドサービス](#createatwittercloudservice).

#### 権限 {#permissions}

twitter・アプリケーション管理の権限セクションで、次の手順を実行します。

* **[!UICONTROL アクセス]**：を選択します。 `Read only`.

   * その他のオプションはサポートされていません

* **[!UICONTROL 追加の権限]**：オプションで選択します。 `Request email addresses from users`.

   * 選択しない場合、AEMのユーザープロファイルには E メールアドレスが含まれません。
   * Twitterの指示に関する追加の手順を記載しています。

ソーシャルログインに対しておこなわれる唯一の REST リクエストは、次のとおりです。 *[GETアカウント/認証情報の確認](https://dev.twitter.com/rest/reference/get/account/verify_credentials)*.

### twitter接続Cloud Serviceの作成 {#create-a-twitter-connect-cloud-service}

The [AdobeGranite OAuth Application and Provider](#adobe-granite-oauth-application-and-provider) クラウドサービス設定を作成することでインスタンス化されたインスタンスは、新しいTwitterが追加されるユーザーアプリケーションとメンバーグループを識別します。

1. オーサーインスタンスで、管理者権限でログインします。
1. グローバルナビゲーションから、「 」を選択します。 **[!UICONTROL ツール]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Twitterソーシャルログイン設定]**.
1. を選択します。 **[!UICONTROL コンテキストパス]** 設定。

   コンテキストパスは、コミュニティサイトの作成/編集時に選択したクラウド設定パスと同じにする必要があります。

1. コンテキストパスの下にクラウドサービスの作成が有効になっているかどうかを確認します。
1. に移動します。 **[!UICONTROL ツール]** > **[!UICONTROL 一般]** > **[!UICONTROL 設定ブラウザー]**. コンテキストを選択し、プロパティを編集します。 まだ有効になっていない場合は、クラウド設定を有効にします。

   ![twitterconfigpropng](assets/twitterconfigproppng.png)

   * 詳しくは、[設定ブラウザー](/help/sites-administering/configurations.md)のドキュメントを参照してください。

1. twitterクラウドサービス設定を作成/編集します。

   ![twittersocialloginpng](assets/twittersocialloginpng.png)

   * **[!UICONTROL タイトル]**

     (*必須*) アプリを識別する表示タイトルを入力します。Twitterアプリを識別します。 入力した名前を *表示名* twitterアプリ用。

   * **[!UICONTROL 消費者キー]**

     (*必須*) **消費者 (API) キー** twitterアプリ用。 これは、 [AdobeGranite OAuth Application and Provider](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#AdobeGraniteOAuthApplicationandProvider) ダイアログから作成されたインスタンス。

   * **[!UICONTROL 消費者の秘密鍵]**

     (*必須*) ***消費者 (API) シークレット*** twitterアプリ。

   * **[!UICONTROL ユーザーを作成]**

     オンにすると、Twitterアカウントでログインすると、AEMユーザーエントリが作成され、選択したユーザーグループにメンバーとして追加されます。 デフォルトはオンです（強く推奨）。

   * **[!UICONTROL ユーザー ID をマスク]**

     選択を解除したままにします。

   * **[!UICONTROL ユーザーグループに追加]**

     「ユーザーグループを追加」を選択して、1 つ以上の [メンバーグループ](https://helpx.adobe.com/experience-manager/6-3/communities/using/users.html) ユーザーを追加するコミュニティサイト用に作成されます。

   >[!NOTE]
   >
   >グループは、いつでも追加または削除できます。 ただし、既存のユーザーのメンバーシップは影響を受けません。 自動メンバーシップは、このフィールドの更新後に作成される新しいユーザーにのみ適用されます。 匿名ユーザーが無効になっているサイトの場合は、その非公開のコミュニティサイト向けの対応する community-members グループにユーザーを追加します。
   >

1. 選択 **[!UICONTROL 保存]** および **[!UICONTROL 公開]**.

結果は [AdobeGranite OAuth Application and Provider](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#adobe-granite-oauth-application-and-provider) これ以上変更する必要のないインスタンス。 デフォルトの範囲は、Twitterログインの標準権限です。

### AEM CommunitiesTwitterOAuth Provider {#aem-communities-twitter-oauth-provider}

AEM Communities設定は、 [AdobeGranite OAuth Application and Provider](#adobe-granite-oauth-application-and-provider) インスタンス。 このプロバイダーは、ユーザーの更新を許可するために編集が必要です。

編集が必要な場合は、各AEMパブリッシュインスタンスで次の手順を実行します。

1. 管理者権限でログインします。
1. 次に移動： [Web コンソール](../../help/sites-deploying/configuring-osgi.md).

   例：http://localhost:4503/system/console/configMgr

1. AEM CommunitiesTwitterOAuth Provider を見つけます。
1. 編集用に開く鉛筆アイコンを選択します。

   ![twitteroauth_png](assets/twitteroauth_png.png)

   * **[!UICONTROL OAuth Provider ID]**

   (*必須*) デフォルト値は *ソコtwitter*. 編集しないでください。

   * **[!UICONTROL Cloud Service設定]**

     デフォルト値は *conf.* 編集しないでください。

   * **[!UICONTROL OAuth Provider Service Config]**

     デフォルト値は `/apps/social/twitterprovider/config/` です。編集しないでください。

   * **[!UICONTROL ユーザーパス]**

     リポジトリ内のユーザーデータが格納される場所。 コミュニティサイトでは、メンバーが互いのプロファイルを表示する権限を確保するために、パスをデフォルトにする必要があります `/home/users/community`.

   * **[!UICONTROL Enable Params]**  — 編集しない
   * **[!UICONTROL URL パラメーター]**  — 編集しない
   * **[!UICONTROL ユーザーを更新]**

     オンにすると、ログインのたびにリポジトリ内のユーザーデータが更新され、プロファイルの変更やリクエストされた追加データが反映されます。 デフォルトはオフです。

#### 次の手順 {#next-steps-1}

次の手順は、FacebookとTwitterの両方で同じです。

* [クラウドサービス設定を公開する](#publishcloudservices)
* [コミュニティサイトに対して有効にする](#enable-social-login)

## ソーシャルログインを有効にする {#enable-social-login}

### AEM Communities Sites コンソール {#aem-communities-sites-console}

クラウドサービスを設定すると、 [ユーザー管理](https://helpx.adobe.com/experience-manager/6-3/communities/using/sites-console.html#USERMANAGEMENT) コミュニティサイト中のサブパネルの設定 [作成](https://helpx.adobe.com/experience-manager/6-3/communities/using/sites-console.html#SiteCreation) または [管理](https://helpx.adobe.com/experience-manager/6-3/communities/using/sites-console.html#ModifyingSiteProperties).

1. ソーシャルログイン設定を保存したサイト設定コンテキストを選択します。

1. 「一般」タブで、クラウド設定を指定します。

   ![managesites_png](assets/managesites_png.png)

1. 「設定」タブで、 **[!UICONTROL ソーシャルログイン]** 保存します。

   ![usermgmt_png](assets/usermgmt_png.png)

## ソーシャルログインのテスト {#test-social-login}

* 確認 [AdobeGranite OAuth Authentication Handler](#adobe-granite-oauth-authentication-handler) は、すべてのパブリッシュインスタンスで有効になっています。
* クラウドサービスが公開されていることを確認します。
* コミュニティサイトが公開されていることを確認します。
* ブラウザーで公開済みサイトを起動します。
例： http://localhost:4503/content/sites/engage/en.html
* 選択 **[!UICONTROL ログイン]**.
* 次のいずれかを選択 **[!UICONTROL facebookでログイン]** または **[!UICONTROL ログインとTwitter]**.
* facebookまたはTwitterにまだログインしていない場合は、適切な資格情報を使用してログインします。
* facebookまたはTwitterアプリで表示されるダイアログに応じて、権限を付与する必要が生じる場合があります。
* ページ上部のツールバーが更新され、ログインが成功したことが反映されています。
* 選択 **[!UICONTROL プロファイル]**：プロファイルページには、ユーザーのアバター画像、名および姓が表示されます。 また、許可されたフィールドやパラメーターに応じて、FacebookまたはTwitterプロファイルからの情報も表示されます。

## AEM Platform OAuth 設定 {#aem-platform-oauth-configurations}

### AdobeGranite OAuth Authentication Handler {#adobe-granite-oauth-authentication-handler}

The `Adobe Granite OAuth Authentication Handler` はデフォルトでは有効ではなく、 ***すべてのAEMパブリッシュインスタンスで有効にする必要があります。***

パブリッシュで認証ハンドラーを有効にするには、OSGi 設定を開いて保存します。

* 管理者権限でログインします。
* 次に移動： [Web コンソール](../../help/sites-deploying/configuring-osgi.md).
例： http://localhost:4503/system/console/configMgr
* 場所 `Adobe Granite OAuth Authentication Handler`.
* 「 」を選択して、設定を編集用に開きます。
* 「**[!UICONTROL 保存]**」を選択します。

![graniteauth](assets/graniteoauth.png)

>[!CAUTION]
>
>認証ハンドラーとのFacebookまたはTwitterインスタンスを混同しないように注意してください。 *AdobeGranite OAuth Application and Provider*.

![graniteoauth1](assets/graniteoauth1.png)

### AdobeGranite OAuth Application and Provider {#adobe-granite-oauth-application-and-provider}

facebookまたはTwitter用のクラウドサービスを作成すると、 `Adobe Granite OAuth Authentication Handler` が作成されました。

facebookまたはTwitterアプリ用に作成されたインスタンスを見つけるには：

1. 管理者権限でログインします。
1. 次に移動： [Web コンソール](../../help/sites-deploying/configuring-osgi.md).

   例：http://localhost:4503/system/console/configMgr

1. AdobeGranite OAuth Application and Provider を見つけます。

   * 次の場所にあるインスタンスを見つけます。 **[!UICONTROL クライアント ID]** が **[!UICONTROL アプリ ID]**.

     ![graniteoauth2](assets/graniteoauth2.png)

     次のプロパティを除き、設定の他のプロパティは変更しないでください。

   * **[!UICONTROL 設定 ID]**

     (*必須*) OAuth 設定 ID は一意である必要があります。 クラウドサービスの作成時に自動生成されます。

   * **[!UICONTROL クライアント ID]**

     (*必須*) クラウドサービスの作成時に提供されたアプリケーション ID。

   * **[!UICONTROL クライアントの秘密鍵]**

     (*必須*) クラウドサービスの作成時に提供されたアプリケーション秘密鍵。

   * **[!UICONTROL 範囲]**

     (*オプション*) 許可される内容の追加範囲は、プロバイダーから求めることができます。 デフォルトの範囲は、ソーシャル認証とプロファイルデータの提供に必要な権限に対応しています。

   * **[!UICONTROL プロバイダー ID]**

     (*必須*) AEM Communitiesのプロバイダー ID は、クラウドサービスの作成時に設定されます。 編集しないでください。 facebook Connect の場合、値は *soco -facebook*. twitter接続の場合、値は *ソコtwitter*.

   * **[!UICONTROL グループ]**

     (*推奨*) 作成したユーザーを追加する 1 つ以上のメンバーグループ。 AEM Communitiesの場合は、コミュニティサイトのメンバーグループをリストすることをお勧めします。

   * **[!UICONTROL コールバック URL]**

     (*オプション*) OAuth プロバイダーがクライアントをリダイレクトして戻すように設定した URL。 元のリクエストのホストを使用するには、相対 URL を使用します。 最初にリクエストされた URL を代わりに使用するには、空のままにします。 サフィックス「/callback/j_security_check」がこの URL に自動的に追加されます。

   >[!NOTE]
   >
   >コールバックのドメインは、プロバイダー (FacebookまたはTwitter) に登録する必要があります。

OAuth 認証ハンドラーの設定ごとに、インスタンスに 2 つの追加の設定が作成されます。

* Apache Jackrabbit Oak Default Sync Handler (org.apache.jackrabbit.oak.spi.security.authentication.external.impl.DefaultSyncHandler) — ここで編集は必要ありませんが、Facebookフィールドが CQ ユーザープロファイルノードにマッピングされる方法をユーザーフィールドマッピングで確認できます。 また、「Sync Handler Name」は、OAuth プロバイダー設定の設定 ID と一致します。
* Apache Jackrabbit Oak External Login Module (org.apache.jackrabbit.oak.spi.security.authentication.external.impl.ExternalLoginModuleFactory) — ここで編集は必要ありませんが、「ID プロバイダー名」と「同期ハンドラー名」は、それぞれ対応する OAuth 設定と同期ハンドラー設定を指しています。

詳しくは、 [Apache Oak 外部ログインモジュールを使用した認証](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html).

## OAuth ユーザートラバーサルパフォーマンス {#oauth-user-traversal-performance}

数十万人ものユーザーがFacebookやTwitterログインを使用して登録したコミュニティサイトの場合、サイト訪問者がソーシャルログインを使用した際に実行されるクエリのトラバーサルパフォーマンスを、次の Oak インデックスを追加することで改善できます。

ログにトラバーサルの警告が表示される場合は、このインデックスを追加することをお勧めします。

オーサーインスタンスで、管理者権限を使用してサインインします。

1. グローバルナビゲーションから：を選択します。 **ツール、 [CRX/DE Lite](../../help/sites-developing/developing-with-crxde-lite.md).**
1. ntBaseLucene のコピーから ntBaseLucene-oauth という名前のインデックスを作成します。

   * ノードの下 `/oak:index`
   * ノードを選択 `ntBaseLucene`
   * 選択 **[!UICONTROL コピー]**
   * `/oak:index` を選択します。
   * 選択 **[!UICONTROL 貼り付け]**
   * ntBaseLucene のコピーをに名前変更 `ntBaseLucene-oauth`

1. ntBaseLucene-oauth ノードのプロパティを変更します。

   * **[!UICONTROL indexPath]**: `/oak:index/ntBaseLucene-oauth`
   * **[!UICONTROL 名前]**: `oauthid-123****`
   * **[!UICONTROL 再インデックス]**: `true`
   * **[!UICONTROL reindexCount]**: `1`

1. ノード/oak:index/ntBaseLucene-oauth/indexRules/nt:base/properties の下で、次の手順を実行します。

   * cqTags を除くすべての子ノードを削除します。
   * cqTags の名前をに変更します。 `oauthid-123****`
   * ノードのプロパティを変更する `oauthid-123****`

      * **[!UICONTROL 名前]**: `oauthid-123****`

   * **[!UICONTROL すべて保存]** を選択します。

* の **名前** `oauthid-123`，置換 *123* facebook ***アプリ ID*** またはTwitter ***消費者 (API) キー*** これが、 **クライアント ID** （内） [AdobeGranite OAuth Application and Provider](social-login.md#adobe-granite-oauth-application-and-provider) 設定。

  ![graniteoauth-crxde](assets/graniteoauth-crxde.png)

その他の情報およびツールについては、 [Oak クエリとインデックス作成](../../help/sites-deploying/queries-and-indexing.md).

## Dispatcher 設定 {#dispatcher-configuration}

詳しくは、 [コミュニティ用の Dispatcher の設定](dispatcher.md).
