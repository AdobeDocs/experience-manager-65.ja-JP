---
title: Facebook と Twitter を使用したソーシャルログイン
seo-title: Social Login with Facebook and Twitter
description: ソーシャルログインを使用すると、サイト訪問者はFacebookまたはTwitterアカウントでログインできます。
seo-description: Social login lets site visitors to sign in with their Facebook or Twitter account.
uuid: f70e346e-0d8c-41a0-a100-206a420088dc
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: c0a71870-8f95-40c8-9ffd-b7af49723288
role: Admin
exl-id: aed9247c-eb81-470c-9fa4-a98c3df2dcaa
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '2783'
ht-degree: 38%

---

# Facebook と Twitter を使用したソーシャルログイン {#social-login-with-facebook-and-twitter}

ソーシャルログインは、サイト訪問者にFacebookまたはTwitterアカウントでログインするオプションを提示する機能です。 したがって、許可されたFacebookまたはTwitterのデータがAEMメンバープロファイルに含まれます。

![socialloginweretail](assets/socialloginweretail.png)

## ソーシャルログインの概要 {#social-login-overview}

ソーシャルログイン機能を含めるには、カスタムの Facebook アプリケーションや Twitter アプリケーションを作成する必要があります。**

we-retail のサンプルは、FacebookおよびTwitterのサンプルアプリとクラウドサービスを提供していますが、 [実稼働用 web サイト](../../help/sites-administering/production-ready.md).

必要な手順は以下のとおりです。

1. すべての AEM パブリッシュインスタンスで [OAuth 認証を有効](#adobe-granite-oauth-authentication-handler)にします。

   OAuth を有効にしない場合、はログインに失敗します。

1. **作成** ソーシャルアプリとクラウドサービス。

   * facebookでのログインをサポートするには：

      * の作成 [Facebookアプリ](#create-a-facebook-app).
      * の作成と公開 [Facebook Connect Cloud Service](#create-a-facebook-connect-cloud-service).
   * twitterでのログインをサポートするには：

      * の作成 [Twitterアプリ](#create-a-twitter-app).
      * の作成と公開 [Twitter Connect Cloud Service](#create-a-twitter-connect-cloud-service).


1. コミュニティサイトに対して&#x200B;[**ソーシャルログインを有効**](#enable-social-login)にします。

以下に示す 2 つの基本的な概念があります。

1. **範囲** （権限）は、アプリがリクエストできるデータを指定します。

   * facebookとTwitter [AdobeGranite OAuth Application and Provider](#adobe-granite-oauth-application-and-provider) インスタンスの場合は、デフォルトで、アプリの基本的な権限がその範囲に含まれます。

1. **フィールド** (params) は、URL パラメーターを使用してリクエストされた実際のデータを指定します。

   * これらのフィールドは、 [AEM Communities Facebook OAuth Provider](#aem-communities-facebook-oauth-provider) および [AEM Communities Twitter OAuth Provider](#aem-communities-twitter-oauth-provider).
   * ほとんどの使用例ではデフォルトのフィールドで十分ですが、変更できます。

## Facebook ログイン {#facebook-login}

### Facebook API バージョン {#facebook-api-version}

ソーシャルログインと we-retail の Facebook アプリのサンプルは、Facebook Graph API 1.0 バージョンで開発されたものです。
AEM 6.4 GA およびAEM 6.3 SP1 のソーシャルログインが更新され、新しいFacebook Graph API 2.5 バージョンと連携するようになりました。

>[!NOTE]
>
>古いAEMバージョンの場合、ログで例外が発生する場合 **ここからトークンを抽出できません**、をそのAEMリリースの最新 CFP にアップグレードします。

facebook Graph API のバージョン情報については、 [Facebook API 変更ログ](https://developers.facebook.com/docs/apps/changelog).

### Facebook アプリの作成 {#create-a-facebook-app}

facebookソーシャルログインを有効にするには、適切に設定されたFacebookアプリケーションが必要です。

facebookアプリケーションを作成するには、Facebookの手順 ( [https://developers.facebook.com/apps/](https://developers.facebook.com/apps/). 手順の変更は、次の情報には反映されません。

一般的な手順（Facebook API v2.7 の時点）：

* 新しい Facebook アプリを追加します。**
   * の場合 *Platform*、Web サイトを選択します。
      * の場合 *サイトの URL*&#x200B;を入力して、 `  https://<server>:<port>.`
      * の場合 *表示名*」で、「 Facebook Connect サービスのタイトル」として使用するタイトルを入力します。
      * の場合 *カテゴリ*，推奨選択 *ページのアプリ*&#x200B;ですが、何でもかまいません。
      * 「製品を追加」で、「Facebook ログイン」を選択します。**
      * の場合 *有効な OAuth リダイレクト URI*&#x200B;を入力して、 `  https://<server>:<port>.`

>[!NOTE]
>
>開発の場合、http://localhost:4503が機能します。

アプリケーションが作成されたら、 **[!UICONTROL アプリ ID]** および **[!UICONTROL App Secret]** 設定。 この情報は、 [Facebook cloud service](#createafacebookcloudservice).

### Facebook Connect クラウドサービス {#create-a-facebook-connect-cloud-service}

クラウドサービス設定を作成することで、[Adobe Granite OAuth Application and Provider](#adobe-granite-oauth-application-and-provider) インスタンスが作成されます。このインスタンスが、Facebook アプリケーションと新しいユーザーの追加先のメンバーグループを識別します。

1. AEM オーサーインスタンスで、管理者権限でサインインします。
1. グローバルナビゲーションから、 **[!UICONTROL ツール]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Facebook Social ログイン設定]**.
1. **[!UICONTROL コンテキストパス]**&#x200B;設定を選択します。

   **[!UICONTROL コンテキストパス]** は、コミュニティサイトの作成/編集時に選択したクラウド設定パスと同じである必要があります。

1. コンテキストパスの下にクラウドサービスを作成できる設定になっているかを確認します。
1. に移動します。 **[!UICONTROL ツール]** > **[!UICONTROL 一般]** > **[!UICONTROL 設定ブラウザー]**. コンテキストを選択し、プロパティを編集します。 まだ有効になっていなければ、クラウド設定を有効にします。

   ![config-propertiespng](assets/config-propertiespng.png)

   * 詳しくは、[設定ブラウザー](/help/sites-administering/configurations.md)のドキュメントを参照してください。

1. **Facebook クラウドサービス設定を作成または編集します。**

   ![fbsocialloginconfigpng](assets/fbsocialloginconfigpng.png)

   * **[!UICONTROL タイトル]** (*必須*) Facebook App を識別する表示タイトルを入力します。 同じ名前を *表示名* facebookアプリ用。
   * **[!UICONTROL アプリ ID/API キー]** (*必須*) ***アプリ ID*** (Facebook App 用 ) これは、 [AdobeGranite OAuth Application and Provider](https://helpx.adobe.com/jp/experience-manager/6-3/communities/using/social-login.html#AdobeGraniteOAuthApplicationandProvider) ダイアログから作成されたインスタンス。
   * **[!UICONTROL App Secret]** (*必須*) ***App Secret*** (Facebook App 用 )
   * **[!UICONTROL ユーザーを作成]**&#x200B;オンにすると、Facebook アカウントでログインしたときに AEM ユーザーエントリが作成され、選択されたユーザーグループのメンバーとして追加されます。デフォルトはオンです（強く推奨）。
   * **[!UICONTROL ユーザー ID をマスク]**:選択を解除したままにします。
   * **[!UICONTROL スコープメール]**:ユーザーの電子メール id は、Facebookから取得する必要があります。
   * **[!UICONTROL ユーザーグループに追加]** 「ユーザーグループの追加」を選択して、1 つ以上の [メンバーグループ](https://helpx.adobe.com/jp/experience-manager/6-3/communities/using/users.html) ユーザーを追加するコミュニティサイト用に作成されます。

   >[!NOTE]
   >
   >グループはいつでも追加または削除できます。しかし、既存ユーザーのメンバーシップに影響はありません。自動メンバーシップは、このフィールド更新後に作成された新規ユーザーにのみ適用されます。匿名ユーザーが無効になっているサイトの場合は、そのクローズドコミュニティサイト専用の対応するコミュニティメンバーグループにユーザーを追加します。

   * 選択 **[!UICONTROL 保存]**.
   * **[!UICONTROL 公開]**.


結果は [AdobeGranite OAuth Application and Provider](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#adobe-granite-oauth-application-and-provider) 追加の範囲（権限）を追加しない限り、追加の変更を必要としないインスタンス。 デフォルトの範囲は、Facebookログインの標準の権限です。 追加のスコープが必要な場合は、OSGi 設定を直接編集する必要があります。 システムまたはコンソールから直接変更がおこなわれている場合は、上書きしないよう、タッチ UI からクラウドサービス設定を編集しないでください。

### AEM Communities Facebook OAuth Provider {#aem-communities-facebook-oauth-provider}

AEM Communitiesプロバイダーは、 [AdobeGranite OAuth Application and Provider](#adobe-granite-oauth-application-and-provider) インスタンス。

以下をおこなうには、このプロバイダーを編集する必要があります。

* ユーザーの更新を許可
* フィールドを追加 [範囲内](#adobe-granite-oauth-application-and-provider)

   * デフォルトで許可されているすべてのフィールドがデフォルトで含まれるわけではありません。

編集が必要な場合は、それぞれの AEM パブリッシュインスタンスで次の設定をします。

1. 管理者権限でサインインします。
1. 次に移動： [Web コンソール](../../help/sites-deploying/configuring-osgi.md). 例：http://localhost:4503/system/console/configMgr
1. AEM Communities Facebook OAuth Provider を見つけます。
1. 鉛筆アイコンを選択して編集用に開きます。

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

      リポジトリ内のユーザーデータが格納される場所。 コミュニティサイトでは、メンバーがお互いのプロファイルを閲覧できる権限を確保するために、パスをデフォルトの */home/users/community* にする必要があります。

   * **[!UICONTROL フィールドを有効にする]**

      オンにすると、その下にリストされているフィールドが、ユーザー認証およびユーザー情報を求める Facebook へのリクエストに指定されます。デフォルト値はオフです。

   * **[!UICONTROL フィールド]**

      「Enable fields」をオンにした場合は、Facebook Graph API の呼び出し時に以下のフィールドが含まれます。これらのフィールドは、クラウドサービス設定で定義された範囲内で許可されている必要があります。追加のフィールドを使用するには、Facebook の承認が必要な場合があります。Facebook ドキュメントの Facebook ログイン権限の節を参照してください。パラメーターとして追加されるデフォルトのフィールドは次のとおりです。

      * id
      * name
      * first_name
      * last_name
      * link
      * locale
      * picture
      * timezone
      * updated_time
      * verified
      * email

   いずれかのフィールドを追加または変更した場合は、対応する Default Sync ハンドラー設定を更新してマッピングを修正してください。

   * **[!UICONTROL ユーザーを更新]**

      オンにすると、ログインするたびにリポジトリ内のユーザーデータが更新され、プロファイルの変更やリクエストされた追加データが反映されます。デフォルト値はオフです。


#### 次の手順 {#next-steps}

続いて以下の手順をおこないますが、この手順は Facebook でも Twitter でも共通です。

* [クラウドサービス設定を公開する](#publishcloudservices)
* [コミュニティサイトに対して有効にする](#enable-social-login)

## Twitter ログイン {#twitter-login}

### Twitter アプリの作成 {#create-a-twitter-app}

Twitter ソーシャルログインを有効にするには、設定された Twitter アプリが必要です。

最新の手順に従って、で新しいTwitterアプリケーションを作成します。 [https://apps.twitter.com](https://apps.twitter.com/).

一般的な手順は次のとおりです。

1. を入力します。 *名前* これにより、web サイトのユーザーに対するTwitterアプリケーションが識別されます。
1. 「*説明*」を入力します。
1. の場合 *web サイト*  — 入力 `https://<server>`.
1. の場合 *コールバック URL*  — 入力 `https://server`.

   >[!NOTE]
   >
   >ポートを指定する必要はありません。
   >
   >開発の場合、https://127.0.0.1/が機能します。

1. アプリケーションが作成されたら、 **[!UICONTROL 消費者 (API) キー]** および **[!UICONTROL 消費者 (API) 秘密鍵]**. この情報は、 [Twitter cloud service](#createatwittercloudservice).

#### 権限 {#permissions}

Twitter アプリケーション管理の権限のセクションで、次の設定をします。

* **[!UICONTROL アクセス]**:選択 `Read only`.

   * その他のオプションはサポートされません。

* **[!UICONTROL 追加の権限]**:オプションで選択 `Request email addresses from users`.

   * 選択しなかった場合は、ユーザーの AEM のプロファイルに電子メールアドレスが含まれなくなります。
   * Twitter の説明に、追加でおこなう手順が示されています。

ソーシャルログインに対しておこなわれる唯一の REST リクエストは、次のとおりです。 *[GETアカウント/認証情報の確認](https://dev.twitter.com/rest/reference/get/account/verify_credentials)*.

### Twitter Connect クラウドサービスの作成 {#create-a-twitter-connect-cloud-service}

クラウドサービス設定を作成することで、[Adobe Granite OAuth Application and Provider](#adobe-granite-oauth-application-and-provider) インスタンスが作成されます。このインスタンスが、Twitter アプリケーションと新しいユーザーの追加先のメンバーグループを識別します。

1. オーサーインスタンスで、管理者権限でサインインします。
1. グローバルナビゲーションから、 **[!UICONTROL ツール]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Twitter Social ログイン設定]**.
1. を選択します。 **[!UICONTROL コンテキストパス]** 設定。

   コンテキストパスは、コミュニティサイトの作成または編集時に選択したクラウド設定パスと同じでなければなりません。

1. コンテキストパスの下にクラウドサービスを作成できる設定になっているかを確認します。
1. に移動します。 **[!UICONTROL ツール]** > **[!UICONTROL 一般]** > **[!UICONTROL 設定ブラウザー]**. コンテキストを選択し、プロパティを編集します。 まだ有効になっていなければ、クラウド設定を有効にします。

   ![twitterconfigpropng](assets/twitterconfigproppng.png)

   * 詳しくは、[設定ブラウザー](/help/sites-administering/configurations.md)のドキュメントを参照してください。

1. Twitter クラウドサービス設定を作成または編集します。

   ![twittersocialloginpng](assets/twittersocialloginpng.png)

   * **[!UICONTROL タイトル]**

      (*必須*) Twitter App を識別する表示タイトルを入力します。 同じ名前を *表示名* twitterアプリ用。

   * **[!UICONTROL 消費者キー]**

      (*必須*) **消費者 (API) キー** twitterアプリ用。 これは、 [AdobeGranite OAuth Application and Provider](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#AdobeGraniteOAuthApplicationandProvider) ダイアログから作成されたインスタンス。

   * **[!UICONTROL 消費者の秘密鍵]**

      (*必須*) ***消費者 (API) シークレット*** (Twitter App 用 )

   * **[!UICONTROL ユーザーを作成]**

      オンにすると、TwitterアカウントでログインしたときにAEMユーザーエントリが作成され、選択したユーザーグループにメンバーとして追加されます。 デフォルトはオンです（強く推奨）。

   * **[!UICONTROL ユーザー ID をマスク]**

      選択を解除したままにします。

   * **[!UICONTROL ユーザーグループに追加]**

      「ユーザーグループを追加」を選択して、1 つ以上の [メンバーグループ](https://helpx.adobe.com/experience-manager/6-3/communities/using/users.html) ユーザーを追加するコミュニティサイト用に作成されます。
   >[!NOTE]
   >
   >グループはいつでも追加または削除できます。ただし、既存のユーザーのメンバーシップは影響を受けません。 自動メンバーシップは、このフィールド更新後に作成された新規ユーザーにのみ適用されます。匿名ユーザーが無効になっているサイトの場合は、その非公開のコミュニティサイト向けの対応する community-members グループにユーザーを追加します。

1. 選択 **[!UICONTROL 保存]** および **[!UICONTROL 公開]**.

結果は [AdobeGranite OAuth Application and Provider](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#adobe-granite-oauth-application-and-provider) これ以上変更する必要のないインスタンス。 デフォルトの範囲には、Twitter にログインするための標準的な権限が含まれています。

### AEM Communities Twitter OAuth Provider {#aem-communities-twitter-oauth-provider}

AEM Communities設定は、 [AdobeGranite OAuth Application and Provider](#adobe-granite-oauth-application-and-provider) インスタンス。 ユーザー更新を許可するには、このプロバイダーを編集する必要があります。

編集が必要な場合は、それぞれの AEM パブリッシュインスタンスで次の設定をします。

1. 管理者権限でサインインします。
1. 次に移動： [Web コンソール](../../help/sites-deploying/configuring-osgi.md).

   例：http://localhost:4503/system/console/configMgr

1. AEM Communities Twitter OAuth Provider を見つけます。
1. 鉛筆アイコンを選択して編集用に開きます。

   ![twitteroauth_png](assets/twitteroauth_png.png)

   * **[!UICONTROL OAuth Provider ID]**

   (*必須*) デフォルト値は *soco -twitter*. 編集しないでください。

   * **[!UICONTROL Cloud Service設定]**

      デフォルト値は *conf.*&#x200B;編集しないでください。

   * **[!UICONTROL OAuth Provider Service Config]**

      デフォルト値は `/apps/social/twitterprovider/config/` です。編集しないでください。

   * **[!UICONTROL ユーザーパス]**

      リポジトリ内のユーザーデータが格納される場所。 コミュニティサイトでは、メンバーが互いのプロファイルを表示する権限を確保するために、パスをデフォルトにする必要があります `/home/users/community`.

   * **[!UICONTROL Enable Params]** 編集しない
   * **[!UICONTROL URL パラメーター]** 編集しない
   * **[!UICONTROL ユーザーを更新]**

      オンにすると、ログインするたびにリポジトリ内のユーザーデータが更新され、プロファイルの変更やリクエストされた追加データが反映されます。デフォルト値はオフです。


#### 次の手順 {#next-steps-1}

続いて以下の手順をおこないますが、この手順は Facebook でも Twitter でも共通です。

* [クラウドサービス設定を公開する](#publishcloudservices)
* [コミュニティサイトに対して有効にする](#enable-social-login)

## ソーシャルログインの有効化 {#enable-social-login}

### AEM Communities サイトコンソール {#aem-communities-sites-console}

クラウドサービスを設定すると、 [ユーザー管理](https://helpx.adobe.com/jp/experience-manager/6-3/communities/using/sites-console.html#USERMANAGEMENT) コミュニティサイト中のサブパネルの設定 [作成](https://helpx.adobe.com/jp/experience-manager/6-3/communities/using/sites-console.html#SiteCreation) または [管理](https://helpx.adobe.com/jp/experience-manager/6-3/communities/using/sites-console.html#ModifyingSiteProperties).

1. ソーシャルログイン設定を保存したサイト設定コンテキストを選択します。

1. 「一般」タブで、クラウド設定をおこないます。

   ![managesites_png](assets/managesites_png.png)

1. 「設定」タブで、「**[!UICONTROL ソーシャルログイン]**」を有効にして「保存」を選択します。

   ![usermgmt_png](assets/usermgmt_png.png)

## ソーシャルログインのテスト {#test-social-login}

* 確認 [AdobeGranite OAuth Authentication Handler](#adobe-granite-oauth-authentication-handler) は、すべてのパブリッシュインスタンスで有効になっています。
* クラウドサービスが公開されていることを確認します。
* コミュニティサイトが公開されていることを確認します。
* ブラウザーで公開済みサイトを起動します。例： http://localhost:4503/content/sites/engage/en.html
* 選択 **[!UICONTROL ログイン]**.
* 次のいずれかを選択 **[!UICONTROL facebookでログイン]** または **[!UICONTROL twitterでログイン]**.
* facebookまたはTwitterにまだログインしていない場合は、適切な資格情報を使用してログインします。
* facebookまたはTwitterアプリで表示されるダイアログに応じて、権限を付与する必要が生じる場合があります。
* ページ上部のツールバーが更新され、ログインが成功したことが反映されています。
* 選択 **[!UICONTROL プロファイル]**:プロファイルページには、ユーザーのアバター画像、名、姓が表示されます。 また、許可されたフィールドやパラメーターに従って、FacebookまたはTwitterプロファイルからの情報も表示されます。

## AEM プラットフォーム OAuth 設定 {#aem-platform-oauth-configurations}

### Adobe Granite OAuth Authentication Handler {#adobe-granite-oauth-authentication-handler}

この `Adobe Granite OAuth Authentication Handler` はデフォルトでは有効ではなく、 ***すべてのAEMパブリッシュインスタンスで有効にする必要があります。***

パブリッシュインスタンスで認証ハンドラーを有効にするには、以下のように OSGi 設定を開いて保存するだけです。

* 管理者権限でサインインします。
* 次に移動： [Web コンソール](../../help/sites-deploying/configuring-osgi.md).
例： http://localhost:4503/system/console/configMgr
* 場所 `Adobe Granite OAuth Authentication Handler`.
* 「 」を選択して、設定を編集用に開きます。
* 「**[!UICONTROL 保存]**」を選択します。

![graniteauth](assets/graniteoauth.png)

>[!CAUTION]
>
>認証ハンドラーをのFacebookまたはTwitterインスタンスと混同しないように注意してください。 *AdobeGranite OAuth Application and Provider*.

![graniteoauth1](assets/graniteoauth1.png)

### Adobe Granite OAuth Application and Provider {#adobe-granite-oauth-application-and-provider}

facebookまたはTwitterのクラウドサービスを作成すると、 `Adobe Granite OAuth Authentication Handler` が作成されました。

Facebook または Twitter アプリ用に作成されたインスタンスを見つけるには、以下のようにします。

1. 管理者権限でサインインします。
1. 次に移動： [Web コンソール](../../help/sites-deploying/configuring-osgi.md).

   例：http://localhost:4503/system/console/configMgr

1. AdobeGranite OAuth Application and Provider を見つけます。

   * 次の場所にあるインスタンスを見つけます。 **[!UICONTROL クライアント ID]** が **[!UICONTROL アプリ ID]**.

      ![graniteauth2](assets/graniteoauth2.png)

      次のプロパティを除き、設定の他のプロパティは変更しないでください。

   * **[!UICONTROL 設定 ID]**

      (*必須*) OAuth 設定 ID は一意である必要があります。 クラウドサービスの作成時に自動生成されます。

   * **[!UICONTROL クライアント ID]**

      (*必須*) クラウドサービスの作成時に提供されたアプリケーション ID。

   * **[!UICONTROL クライアントの秘密鍵]**

      (*必須*) クラウドサービスの作成時に提供されたアプリケーション秘密鍵。

   * **[!UICONTROL 範囲]**

      (*オプション*) 許可される内容の追加範囲は、プロバイダーから求めることができます。 デフォルトで、ソーシャル認証とプロファイルデータの提供に必要な権限が範囲に含まれています。

   * **[!UICONTROL プロバイダー ID]**

      (*必須*) AEM Communitiesのプロバイダー ID は、クラウドサービスの作成時に設定されます。 編集しないでください。facebook Connect の場合、値は *soco -facebook*. twitter Connect の場合、値は *soco -twitter*.

   * **[!UICONTROL グループ]**

      (*推奨*) 作成したユーザーを追加する 1 つ以上のメンバーグループ。 AEM Communitiesの場合は、コミュニティサイトのメンバーグループをリストすることをお勧めします。

   * **[!UICONTROL コールバック URL]**

      (*オプション*) OAuth プロバイダーがクライアントをリダイレクトして戻すように設定した URL。 元のリクエストのホストを使用するには、相対 URL を使用します。最初にリクエストされた URL を代わりに使用するには、空のままにします。この  URL .
   >[!NOTE]
   >
   >コールバックのドメインは、プロバイダー (FacebookまたはTwitter) に登録する必要があります。

OAuth 認証ハンドラーの設定ごとに、インスタンスに 2 つの追加の設定が作成されます。

* Apache Jackrabbit Oak Default Sync Handler (org.apache.jackrabbit.oak.spi.security.authentication.external.impl.DefaultSyncHandler) — ここで編集は必要ありませんが、Facebookフィールドが CQ ユーザープロファイルノードにマッピングされる方法をユーザーフィールドマッピングで確認できます。 また、「Sync Handler Name」は、OAuth プロバイダー設定の設定 ID と一致します。
* Apache Jackrabbit Oak External Login Module (org.apache.jackrabbit.oak.spi.security.authentication.external.impl.ExternalLoginModuleFactory) — 編集は必要ありませんが、「ID プロバイダー名」と「同期ハンドラー名」は、それぞれ対応する OAuth 設定と同期ハンドラー設定を指しています。

詳しくは、 [Apache Oak 外部ログインモジュールを使用した認証](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html).

## OAuth ユーザーのトラバーサルパフォーマンス {#oauth-user-traversal-performance}

数十万人ものユーザーがFacebookまたはTwitterログインを使用して登録したコミュニティサイトの場合、サイト訪問者がソーシャルログインを使用した際に実行されるクエリのトラバーサルパフォーマンスを、次の Oak インデックスを追加することで改善できます。

ログにトラバーサル警告が記録されている場合は、このインデックスを追加することを推奨します。

オーサーインスタンスで、管理者権限でサインインします。

1. グローバルナビゲーションから：選択 **ツール、 [CRX/DE Lite](../../help/sites-developing/developing-with-crxde-lite.md).**
1. ntBaseLucene のコピーから ntBaseLucene-oauth という名前のインデックスを作成します。

   * ノードの下 `/oak:index`
   * ノードを選択 `ntBaseLucene`
   * 選択 **[!UICONTROL コピー]**
   * 選択 `/oak:index`
   * 選択 **[!UICONTROL 貼り付け]**
   * ntBaseLucene のコピーをに名前変更 `ntBaseLucene-oauth`

1. ntBaseLucene-oauth ノードのプロパティを変更します。

   * **[!UICONTROL indexPath]**: `/oak:index/ntBaseLucene-oauth`
   * **[!UICONTROL 名前]**: `oauthid-123****`
   * **[!UICONTROL 再インデックス]**: `true`
   * **[!UICONTROL reindexCount]**：`1`

1. ノード/oak:index/ntBaseLucene-oauth/indexRules/nt:base/properties の下で、次の手順を実行します。

   * cqTags を除くすべての子ノードを削除します。
   * cqTags の名前をに変更します。 `oauthid-123****`
   * ノードのプロパティを変更する `oauthid-123****`

      * **[!UICONTROL 名前]**: `oauthid-123****`
   * **[!UICONTROL すべて保存]** を選択します。


* の **名前** `oauthid-123`，置換 *123* facebook ***アプリ ID*** またはTwitter ***消費者 (API) キー*** これは、 **クライアント ID** 内 [AdobeGranite OAuth Application and Provider](social-login.md#adobe-granite-oauth-application-and-provider) 設定。

   ![graniteoauth-crxde](assets/graniteoauth-crxde.png)

詳しくは、 [Oak クエリとインデックス作成](../../help/sites-deploying/queries-and-indexing.md).

## Dispatcher 設定 {#dispatcher-configuration}

[コミュニティのための Dispatcher の設定](dispatcher.md)を参照してください。
