---
title: Facebook と Twitter を使用したソーシャルログイン
description: ソーシャルログインを使用すると、サイト訪問者はFacebookまたはTwitterアカウントでログインできます。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: aed9247c-eb81-470c-9fa4-a98c3df2dcaa
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '2672'
ht-degree: 2%

---

# Facebook と Twitter を使用したソーシャルログイン {#social-login-with-facebook-and-twitter}

ソーシャルログインでは、サイト訪問者が自分のFacebookまたはTwitterアカウントを使用してログインするオプションを提供できます。 そのため、AEM メンバープロファイルには、許可されたFacebookまたはTwitterデータを含めます。

![socialloginweretail](assets/socialloginweretail.png)

## ソーシャルログインの概要 {#social-login-overview}

ソーシャルログインを含めるには、次を行います *必須* カスタム FacebookおよびTwitterアプリケーションを作成する場合。

we-retail サンプルでは、Facebook、Twitterアプリおよびクラウドサービスのサンプルが提供されていますが、ではご利用いただけません。 [実稼動 web サイト](../../help/sites-administering/production-ready.md).

必要な手順は次のとおりです。

1. [OAuth 認証の有効化](#adobe-granite-oauth-authentication-handler) すべてのAEM パブリッシュインスタンスで。

   OAuth が有効になっていない場合、ログインの試みは失敗します。

1. **作成** ソーシャルアプリとクラウドサービス。

   * facebookへのログインをサポートするには：

      * を作成 [Facebook アプリ](#create-a-facebook-app).
      * の作成と公開 [Facebook Connect クラウドサービス](#create-a-facebook-connect-cloud-service).

   * twitterでのログインをサポートするには：

      * を作成 [Twitterアプリ](#create-a-twitter-app).
      * の作成と公開 [Cloud Service のTwitter接続](#create-a-twitter-connect-cloud-service).

1. [**Enable （有効）** ソーシャルログイン](#enable-social-login) コミュニティサイトの場合。

次の 2 つの基本概念があります。

1. **範囲** （権限）アプリがリクエストできるデータを指定します。

   * facebookとTwitter [Adobe Granite OAuth アプリケーションとプロバイダー](#adobe-granite-oauth-application-and-provider) インスタンスには、デフォルトで、スコープ内に基本アプリ権限が含まれます。

1. **フィールド** （params） URL パラメーターを使用してリクエストされた実際のデータを指定します。

   * これらのフィールドは、で指定します [AEM Communities Facebook OAuth プロバイダー](#aem-communities-facebook-oauth-provider) および [AEM Communities Twitter OAuth プロバイダー](#aem-communities-twitter-oauth-provider).
   * ほとんどのユースケースではデフォルトフィールドで十分ですが、変更可能です。

## Facebook ログイン {#facebook-login}

### Facebook API バージョン {#facebook-api-version}

ソーシャルログインと we-retail Facebook サンプルは、Facebook Graph API がバージョン 1.0 の場合に開発されました。AEM 6.4 GA およびAEM 6.3 SP1 の時点で、ソーシャルログインが更新され、新しいFacebook Graph API 2.5 バージョンで動作するようになりました。

>[!NOTE]
>
>古いバージョンのAEMでログに例外が発生した場合 **このからトークンを抽出できません**、そのAEM リリースの最新の CFP にアップグレードしてください。

facebook Graph API のバージョン情報については [Facebook API 変更ログ](https://developers.facebook.com/docs/apps/changelog).

### facebook アプリケーションの作成 {#create-a-facebook-app}

facebook ソーシャルログインを有効にするには、適切に設定されたFacebook アプリケーションが必要です。

facebook アプリケーションを作成するには、次の場所にあるFacebookの手順に従います [https://developers.facebook.com/apps/](https://developers.facebook.com/apps/). 手順の変更は、次の情報には反映されません。

一般に、Facebook API v2.7 の時点では次のようになります。

* *新しいFacebook アプリを追加*
   * の場合 *Platform*&#x200B;で、「Website」を選択します。
      * の場合 *サイト URL*、と入力します `  https://<server>:<port>.`
      * の場合 *表示名*&#x200B;に、Facebook connect サービスのタイトルとして使用するタイトルを入力します。
      * の場合 *カテゴリ*、推奨される選択 *ページ用アプリ*&#x200B;ただし、何でも構いません。
      * *Add Product: Facebook Login*
      * の場合 *有効な OAuth リダイレクト URI*、と入力します `  https://<server>:<port>.`

>[!NOTE]
>
>開発の場合、http://localhost:4503が機能します。

アプリケーションを作成したら、 **[!UICONTROL アプリ ID]** および **[!UICONTROL アプリの秘密鍵]** 設定。 この情報は、 [Facebook cloud service](#createafacebookcloudservice).

### facebook Connect Cloud Serviceの作成 {#create-a-facebook-connect-cloud-service}

この [Adobe Granite OAuth アプリケーションとプロバイダー](#adobe-granite-oauth-application-and-provider) インスタンスは、クラウドサービス設定を作成してインスタンス化され、Facebook アプリケーションと、新しいユーザーが追加されるメンバーグループを特定します。

1. AEM オーサーインスタンスで、管理者権限でログインします。
1. グローバルナビゲーションから、を選択します。 **[!UICONTROL ツール]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Facebook ソーシャルログイン設定]**.
1. 設定を選択します **[!UICONTROL コンテキストパス]**.

   **[!UICONTROL コンテキストパス]** は、コミュニティサイトの作成または編集時に選択したクラウド設定パスと同じである必要があります。

1. コンテキストパスが有効でその下にクラウドサービスを作成できるかどうかを確認します。
1. に移動 **[!UICONTROL ツール]** > **[!UICONTROL 一般]** > **[!UICONTROL 設定ブラウザー]**. コンテキストを選択してプロパティを編集します。 まだ有効になっていない場合は、クラウド設定を有効にします。

   ![config-properties](assets/config-propertiespng.png)

   * 詳しくは、[設定ブラウザー](/help/sites-administering/configurations.md)のドキュメントを参照してください。

1. **作成/編集** Facebook クラウドサービス設定。

   ![fbsocialloginconfigpng](assets/fbsocialloginconfigpng.png)

   * **[!UICONTROL タイトル]** （*必須*） Facebook アプリを識別する表示タイトルを入力します。 と同じ名前を入力します *表示名* （Facebook アプリケーション用）。
   * **[!UICONTROL アプリ ID/API キー]** （*必須*）を入力します ***アプリ ID*** （Facebook アプリケーション用）。 これは、 [Adobe Granite OAuth アプリケーションとプロバイダー](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#AdobeGraniteOAuthApplicationandProvider) インスタンスはダイアログから作成されました。
   * **[!UICONTROL アプリの秘密鍵]** （*必須*）を入力します ***アプリの秘密鍵*** （Facebook アプリケーション用）。
   * **[!UICONTROL ユーザーの作成]** オンにした場合、Facebook アカウントでログインすると、AEM ユーザーエントリが作成され、それらのエントリがメンバーとして選択したユーザーグループに追加されます。  デフォルトではオンになっています（強く推奨）。
   * **[!UICONTROL ユーザー ID をマスク]**：選択を解除したままにします。
   * **[!UICONTROL スコープメール]**:Facebookからユーザーのメール id を取得する必要があります。
   * **[!UICONTROL ユーザーグループに追加]** 「ユーザーグループを追加」を選択して、1 つ以上のユーザーグループを選択します [メンバーグループ](https://helpx.adobe.com/experience-manager/6-3/communities/using/users.html) ユーザーを追加するコミュニティサイトの場合。

   >[!NOTE]
   >
   >グループはいつでも追加または削除できます。 ただし、既存のユーザーのメンバーシップは影響を受けません。 自動メンバーシップは、このフィールドの更新後に作成される新規ユーザーにのみ適用されます。 匿名ユーザーが無効になっているサイトの場合は、閉じられたコミュニティサイト用の対応するコミュニティメンバーグループにユーザーを追加することを選択します。

   * を選択 **[!UICONTROL 保存]**.
   * **[!UICONTROL 公開]**.

結果は [Adobe Granite OAuth アプリケーションとプロバイダー](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#adobe-granite-oauth-application-and-provider) 範囲（権限）を追加しない限り、さらに変更する必要がないインスタンス。 デフォルトの範囲は、Facebookへのログインに対する標準の権限です。 範囲を追加する必要がある場合は、OSGi 設定を直接編集する必要があります。 システム/コンソールを介して直接行われた変更がある場合は、上書きを避けるために、タッチ UI からクラウドサービス設定を編集しないでください。

### AEM Communities Facebook OAuth プロバイダー {#aem-communities-facebook-oauth-provider}

AEM Communities プロバイダーは、を拡張します [Adobe Granite OAuth アプリケーションとプロバイダー](#adobe-granite-oauth-application-and-provider) インスタンス。

このプロバイダーは、次の操作を行うために編集が必要です：

* ユーザー更新の許可
* フィールドを追加 [範囲内](#adobe-granite-oauth-application-and-provider)

   * デフォルトで許可されているすべてのフィールドがデフォルトで含まれるわけではありません。

編集が必要な場合は、各AEM パブリッシュインスタンスで以下をおこないます。

1. 管理者権限でログインします。
1. に移動します。 [Web コンソール](../../help/sites-deploying/configuring-osgi.md). 例えば、http://localhost:4503/system/console/configMgrです。
1. AEM Communities Facebook OAuth プロバイダーを見つけます。
1. 編集する鉛筆アイコンを選択します。

   ![fboauthprov_png](assets/fboauthprov_png.png)

   * **[!UICONTROL OAuth プロバイダー ID]**

     （*必須*） デフォルト値は *ソコ - facebook*. 編集しないでください。

   * **[!UICONTROL Cloud Service設定]**

     デフォルト値は `/etc/  cloudservices /  facebookconnect`. 編集しないでください。

   * **[!UICONTROL OAuth プロバイダーサービス設定]**

     デフォルト値は `/apps/social/facebookprovider/config/`. 編集しないでください。

   * **[!UICONTROL タグを有効にする]**

     編集しないでください。

   * **[!UICONTROL ユーザーパス]**

     ユーザーデータが格納されるリポジトリ内の場所。 コミュニティサイトの場合、メンバーがお互いのプロファイルを表示するための権限を確保するには、パスをデフォルトにする必要があります */home/users/community*.

   * **[!UICONTROL フィールドを有効にする]**

     オンにした場合、リストされるフィールドは、Facebookへのユーザー認証および情報要求で指定されます。 デフォルトでは選択されていません。

   * **[!UICONTROL フィールド]**

     フィールドを有効にすると、Facebook Graph API を呼び出す際に次のフィールドが含まれます。 フィールドは、クラウドサービス設定で定義された範囲内で許可する必要があります。 その他のフィールドには、Facebookの承認が必要な場合があります。 facebook ドキュメントのFacebook ログイン権限の節を参照してください。 パラメーターとして追加されるデフォルトのフィールドは次のとおりです。

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

   フィールドを追加または変更した場合は、対応するデフォルトの同期ハンドラー設定を更新してマッピングを修正します。

   * **[!UICONTROL ユーザーの更新]**

     オンにすると、各ログイン時にリポジトリ内のユーザーデータが更新され、プロファイルの変更やリクエストされた追加データが反映されます。 デフォルトでは選択されていません。

#### 次の手順 {#next-steps}

次の手順は、FacebookとTwitterの両方で同じです。

* [クラウドサービス設定の公開](#publishcloudservices)
* [コミュニティサイト用にを有効にする](#enable-social-login)

## Twitterログイン {#twitter-login}

### twitterアプリの作成 {#create-a-twitter-app}

twitterソーシャルログインを有効にするには、設定済みのTwitterアプリケーションが必要です。

最新の手順に従って、次の場所でTwitterアプリケーションを作成します： [https://apps.twitter.com](https://apps.twitter.com/).

一般的には以下のようになります。

1. を入力 *名前* これにより、web サイトのユーザーに対するTwitterアプリケーションが識別されます。
1. 「*説明*」を入力します。
1. の場合 *web サイト*  – を入力 `https://<server>`.
1. の場合 *コールバック URL*  – を入力 `https://server`.

   >[!NOTE]
   >
   >ポートを指定する必要はありません。
   >
   >開発の場合、https://127.0.0.1/が機能します。

1. アプリケーションを作成したら、 **[!UICONTROL 消費者（API）キー]** および **[!UICONTROL 消費者（API）の秘密鍵]**. この情報は、 [Twitterクラウドサービス](#createatwittercloudservice).

#### 権限 {#permissions}

twitterアプリケーション管理の「権限」セクションで、次の操作を行います。

* **[!UICONTROL アクセス]**：を選択 `Read only`.

   * その他のオプションはサポートされていません

* **[!UICONTROL 追加の権限]**：任意で選択 `Request email addresses from users`.

   * 選択しない場合、AEMのユーザープロファイルには、メールアドレスが含まれません。
   * Twitterの手順：実行する追加の手順を示します。

ソーシャルログイン用に行われる REST リクエストはのみです。 *[GET アカウント/認証情報の確認](https://dev.twitter.com/rest/reference/get/account/verify_credentials)*.

### twitter接続Cloud Serviceを作成する {#create-a-twitter-connect-cloud-service}

この [Adobe Granite OAuth アプリケーションとプロバイダー](#adobe-granite-oauth-application-and-provider) インスタンスは、クラウドサービス設定を作成してインスタンス化され、新しいユーザーが追加されるTwitterアプリケーションとメンバーグループを特定します。

1. オーサーインスタンスで、管理者権限でログインします。
1. グローバルナビゲーションから、を選択します。 **[!UICONTROL ツール]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Twitterのソーシャルログイン設定]**.
1. を選択します。 **[!UICONTROL コンテキストパス]** 設定。

   コンテキストパスは、コミュニティサイトの作成または編集時に選択したクラウド設定パスと同じである必要があります。

1. コンテキストパスが有効でその下にクラウドサービスを作成できるかどうかを確認します。
1. に移動 **[!UICONTROL ツール]** > **[!UICONTROL 一般]** > **[!UICONTROL 設定ブラウザー]**. コンテキストを選択してプロパティを編集します。 まだ有効になっていない場合は、クラウド設定を有効にします。

   ![twitterconfigproppng](assets/twitterconfigproppng.png)

   * 詳しくは、[設定ブラウザー](/help/sites-administering/configurations.md)のドキュメントを参照してください。

1. twitterクラウドサービス設定を作成/編集します。

   ![twittersocialloginpng](assets/twittersocialloginpng.png)

   * **[!UICONTROL タイトル]**

     （*必須*） Twitterアプリを識別する表示タイトルを入力します。 と同じ名前を入力します *表示名* twitterアプリ用。

   * **[!UICONTROL 消費者キー]**

     （*必須*）を入力します **消費者（API）キー** twitterアプリ用。 これは、 [Adobe Granite OAuth アプリケーションとプロバイダー](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#AdobeGraniteOAuthApplicationandProvider) インスタンスはダイアログから作成されました。

   * **[!UICONTROL 消費者秘密鍵]**

     （*必須*）を入力します ***Consumer （API）秘密鍵*** twitterアプリ用。

   * **[!UICONTROL ユーザーの作成]**

     オンにした場合、Twitterアカウントでログインすると、AEM ユーザーのエントリが作成され、それらのエントリがメンバーとして選択したユーザーグループに追加されます。 デフォルトではオンになっています（強く推奨）。

   * **[!UICONTROL ユーザー ID をマスク]**

     選択を解除したままにします。

   * **[!UICONTROL ユーザーグループに追加]**

     「ユーザーグループを追加」を選択して、1 つ以上のユーザーグループを選択します [メンバーグループ](https://helpx.adobe.com/experience-manager/6-3/communities/using/users.html) ユーザーを追加するコミュニティサイトの場合。

   >[!NOTE]
   >
   >グループはいつでも追加または削除できます。 ただし、既存のユーザーのメンバーシップは影響を受けません。 自動メンバーシップは、このフィールドの更新後に作成される新規ユーザーにのみ適用されます。 匿名ユーザーが無効になっている Sites の場合、閉じられたコミュニティサイト用の、対応するコミュニティメンバーグループにユーザーを追加します。
   >

1. を選択 **[!UICONTROL 保存]** および **[!UICONTROL 公開]**.

結果は [Adobe Granite OAuth アプリケーションとプロバイダー](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#adobe-granite-oauth-application-and-provider) インスタンス （それ以上の変更は不要）。 デフォルトの範囲は、Twitterログインの標準的な権限です。

### AEM Communities Twitter OAuth プロバイダー {#aem-communities-twitter-oauth-provider}

AEM Communitiesの設定は、を拡張するものです [Adobe Granite OAuth アプリケーションとプロバイダー](#adobe-granite-oauth-application-and-provider) インスタンス。 このプロバイダーは、ユーザーの更新を許可するように編集する必要があります。

編集が必要な場合は、各AEM パブリッシュインスタンスで以下をおこないます。

1. 管理者権限でログインします。
1. に移動します。 [Web コンソール](../../help/sites-deploying/configuring-osgi.md).

   例えば、http://localhost:4503/system/console/configMgrです。

1. AEM CommunitiesTwitterOAuth プロバイダーを見つけます。
1. 編集する鉛筆アイコンを選択します。

   ![twitteroauth_png](assets/twitteroauth_png.png)

   * **[!UICONTROL OAuth プロバイダー ID]**

   （*必須*）、デフォルト値はです。 *ソコ twitter*. 編集しないでください。

   * **[!UICONTROL Cloud Service設定]**

     デフォルト値はです *conf.* 編集しないでください。

   * **[!UICONTROL OAuth プロバイダーサービス設定]**

     デフォルト値は `/apps/social/twitterprovider/config/` です。編集しないでください。

   * **[!UICONTROL ユーザーパス]**

     ユーザーデータが格納されるリポジトリ内の場所。 コミュニティサイトの場合、メンバーがお互いのプロファイルを表示するための権限を確保するには、パスをデフォルトにする必要があります `/home/users/community`.

   * **[!UICONTROL パラメーターを有効にする]**  – 編集しない
   * **[!UICONTROL URL パラメーター]**  – 編集しない
   * **[!UICONTROL ユーザーの更新]**

     オンにすると、各ログイン時にリポジトリ内のユーザーデータが更新され、プロファイルの変更やリクエストされた追加データが反映されます。 デフォルトでは選択されていません。

#### 次の手順 {#next-steps-1}

次の手順は、FacebookとTwitterの両方で同じです。

* [クラウドサービス設定の公開](#publishcloudservices)
* [コミュニティサイト用にを有効にする](#enable-social-login)

## ソーシャルログインを有効にする {#enable-social-login}

### AEM Communities Sites コンソール {#aem-communities-sites-console}

クラウドサービスを設定したら、を使用して、コミュニティサイトに関連するソーシャルログイン設定を有効にできます [ユーザー管理](https://helpx.adobe.com/experience-manager/6-3/communities/using/sites-console.html#USERMANAGEMENT) コミュニティサイト中の設定サブパネル [作成](https://helpx.adobe.com/experience-manager/6-3/communities/using/sites-console.html#SiteCreation) または [管理](https://helpx.adobe.com/experience-manager/6-3/communities/using/sites-console.html#ModifyingSiteProperties).

1. ソーシャルログイン設定を保存したサイト設定コンテキストを選択します。

1. 「一般」タブで、クラウド設定を指定します。

   ![managesites_png](assets/managesites_png.png)

1. 「設定」タブで、を有効にします **[!UICONTROL ソーシャルログイン]** を選択して保存します。

   ![usermgmt_png](assets/usermgmt_png.png)

## ソーシャルログインのテスト {#test-social-login}

* 確保する [Adobe Granite OAuth 認証ハンドラー](#adobe-granite-oauth-authentication-handler) はすべてのパブリッシュインスタンスで有効になっています。
* クラウドサービスが公開されていることを確認します。
* コミュニティサイトが公開されていることを確認します。
* 公開したサイトをブラウザーで起動します。
例：http://localhost:4503/content/sites/engage/en.html
* を選択 **[!UICONTROL ログイン イン]**.
* 次のいずれかを選択 **[!UICONTROL facebookでログイン]** または **[!UICONTROL twitterでログイン]**.
* facebookまたはTwitterにまだログインしていない場合は、適切な資格情報でログインします。
* facebookまたはTwitterアプリで表示されるダイアログに応じて、権限を付与する必要が生じる場合があります。
* ページ上部のツールバーが更新され、ログイン成功が反映されます。
* を選択 **[!UICONTROL Profile]**：プロファイルページには、ユーザーのアバター画像、名、姓が表示されます。 また、許可されたフィールドやパラメーターに従って、FacebookまたはTwitterプロファイルからの情報も表示されます。

## AEM Platform OAuth 設定 {#aem-platform-oauth-configurations}

### Adobe Granite OAuth 認証ハンドラー {#adobe-granite-oauth-authentication-handler}

この `Adobe Granite OAuth Authentication Handler` はデフォルトでは有効になっていません。 ***すべてのAEM パブリッシュインスタンスで有効にする必要があります。***

パブリッシュで認証ハンドラーを有効にするには、OSGi 設定を開いて保存するだけです。

* 管理者権限でログインします。
* に移動します。 [Web コンソール](../../help/sites-deploying/configuring-osgi.md).
例：http://localhost:4503/system/console/configMgr
* を見つける `Adobe Granite OAuth Authentication Handler`.
* 「」を選択して、編集用に設定を開きます。
* 「**[!UICONTROL 保存]**」を選択します。

![graniteoauth](assets/graniteoauth.png)

>[!CAUTION]
>
>認証ハンドラーをFacebookのまたはTwitterインスタンスと混同しないように注意してください *Adobe Granite OAuth アプリケーションとプロバイダー*.

![graniteoauth1](assets/graniteoauth1.png)

### Adobe Granite OAuth アプリケーションとプロバイダー {#adobe-granite-oauth-application-and-provider}

facebookまたはTwitter用の Cloud Service が作成されると、次のインスタンスが `Adobe Granite OAuth Authentication Handler` が作成されました。

facebookまたはTwitterアプリケーション用に作成されたインスタンスを見つけるには：

1. 管理者権限でログインします。
1. に移動します。 [Web コンソール](../../help/sites-deploying/configuring-osgi.md).

   例えば、http://localhost:4503/system/console/configMgrです。

1. 「Granite OAuth アプリケーションとプロバイダー」というAdobeを見つけます。

   * インスタンスを見つけます。 **[!UICONTROL クライアント ID]** 次に一致 **[!UICONTROL アプリ ID]**.

     ![graniteoauth2](assets/graniteoauth2.png)

     次のプロパティ以外は、設定のその他のプロパティは変更しません。

   * **[!UICONTROL 設定 ID]**

     （*必須*） OAuth 設定 ID は一意である必要があります。 Cloud Service の作成時に自動生成されます。

   * **[!UICONTROL クライアント ID]**

     （*必須*） Cloud Service の作成時に指定されたアプリケーション ID。

   * **[!UICONTROL クライアントの秘密鍵]**

     （*必須*） Cloud Service の作成時に提供されたアプリケーション秘密鍵。

   * **[!UICONTROL 範囲]**

     （*オプション*）許可される内容に関する追加の範囲は、プロバイダーから問い合わせることができます。 デフォルトの範囲は、ソーシャル認証とプロファイルデータを提供するために必要な権限をカバーしています。

   * **[!UICONTROL プロバイダー ID]**

     （*必須*） AEM Communitiesのプロバイダー ID は、Cloud Service の作成時に設定されます。 編集しないでください。 facebook Connect の場合、値はです *ソコ - facebook*. twitter接続の場合、値はです *ソコ twitter*.

   * **[!UICONTROL グループ]**

     （*推奨*）作成されたユーザーが追加される 1 つ以上のメンバーグループ。 AEM Communitiesの場合、コミュニティサイトのメンバーグループをリストすることをお勧めします。

   * **[!UICONTROL コールバック URL]**

     （*オプション*） OAuth プロバイダーで設定された、クライアントをリダイレクトして戻す URL。 元のリクエストのホストを使用するには、相対 url を使用します。 最初にリクエストした URL を代わりに使用するには、空のままにします。 この URL には、「/callback/j_security_check」というサフィックスが自動的に追加されます。

   >[!NOTE]
   >
   >コールバックのドメインは、プロバイダー（FacebookまたはTwitter）に登録する必要があります。

OAuth 認証ハンドラー設定ごとに、インスタンスに次の 2 つの追加設定が作成されます。

* Apache Jackrabbit Oak デフォルト同期ハンドラー（org.apache.jackrabbit.oak.spi.security.authentication.external.impl.DefaultSyncHandler） – 編集は必要ありませんが、ユーザーフィールドマッピングを調べると、Facebook フィールドが CQ ユーザープロファイルノードにマッピングされる方法を確認できます。 また、「Sync Handler Name」が OAuth プロバイダー設定の設定 ID と一致することにも注意してください。
* Apache Jackrabbit Oak External Login Module （org.apache.jackrabbit.oak.spi.security.authentication.external.impl.ExternalLoginModuleFactory） – 必要な編集はありませんが、「Identity Provider Name」と「Sync Handler Name」が同じで、対応する OAuth 設定と同期ハンドラー設定をそれぞれ指していることに気付くかもしれません。

詳しくは、を参照してください [Apache Oak External Login Module を使用した認証](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html).

## OAuth ユーザートラバーサルパフォーマンス {#oauth-user-traversal-performance}

facebookやTwitterのログインを使用して数十万人のユーザーが登録するコミュニティサイトの場合、次の Oak インデックスを追加することで、サイト訪問者がソーシャルログインを使用する際に実行されるクエリのトラバーサルパフォーマンスを向上させることができます。

ログにトラバーサルの警告が表示される場合は、このインデックスを追加することをお勧めします。

管理者権限でログインしたオーサーインスタンス：

1. グローバルナビゲーションから：を選択します **ツール、 [CRX/DE Lite](../../help/sites-developing/developing-with-crxde-lite.md).**
1. ntBaseLucene のコピーから ntBaseLucene-oauth という名前のインデックスを作成します。

   * ノードの下 `/oak:index`
   * ノードを選択 `ntBaseLucene`
   * を選択 **[!UICONTROL コピー]**
   * `/oak:index` を選択します。
   * を選択 **[!UICONTROL ペースト]**
   * ntBaseLucene のコピーの名前をに変更 `ntBaseLucene-oauth`

1. ノード ntBaseLucene-oauth のプロパティを変更します。

   * **[!UICONTROL indexPath]**: `/oak:index/ntBaseLucene-oauth`
   * **[!UICONTROL 名前]**: `oauthid-123****`
   * **[!UICONTROL 再インデックス]**: `true`
   * **[!UICONTROL reindexCount]**: `1`

1. /oak:index/ntBaseLucene-oauth/indexRules/nt:base/properties ノードの下：

   * cqTags を除くすべての子ノードを削除します。
   * cqTags の名前をに変更します。 `oauthid-123****`
   * ノードのプロパティの変更 `oauthid-123****`

      * **[!UICONTROL 名前]**: `oauthid-123****`

   * 「**[!UICONTROL すべて保存]**」を選択します。

* の場合 **名前** `oauthid-123`、置換 *123* （Facebookを使用） ***アプリ ID*** またはTwitter ***消費者（API）キー*** 次の値になります **クライアント ID** が含まれる [Adobe Granite OAuth アプリケーションとプロバイダー](social-login.md#adobe-granite-oauth-application-and-provider) 設定。

  ![graniteoauth-crxde](assets/graniteoauth-crxde.png)

その他の情報とツールについては、を参照してください [Oak クエリとインデックス作成](../../help/sites-deploying/queries-and-indexing.md).

## Dispatcher 設定 {#dispatcher-configuration}

参照： [Communities 用の Dispatcher の設定](dispatcher.md).
