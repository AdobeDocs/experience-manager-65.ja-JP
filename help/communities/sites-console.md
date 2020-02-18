---
title: コミュニティサイトコンソール
seo-title: コミュニティサイトコンソール
description: コミュニティサイトコンソールにアクセスする方法
seo-description: コミュニティサイトコンソールにアクセスする方法
uuid: 74134281-244c-40da-a941-7f2f3e706d4b
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 4130f952-5bb5-4e32-91d6-47b2885b30a4
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# コミュニティサイトコンソール{#communities-sites-console}

コミュニティサイトコンソールでは、以下の操作ができます。

* サイト作成
* サイト編集
* サイト管理
* [ネストされたグループの作成と編集](/help/communities/groups.md)（サブコミュニティ）

オーサー環境で素早くコミュニティサイトを作成する方法や、オーサー環境とパブリッシュ環境からコミュニティグループを作成する方法については、[AEM Communities 使用の手引き](/help/communities/getting-started.md)を参照してください。

>[!NOTE]
>
>The main Communities menus for the creation of [community sites](/help/communities/sites-console.md), [community site templates](/help/communities/sites.md), [community group templates](/help/communities/tools-groups.md) and [community functions](/help/communities/functions.md) are for use only in the author environment.

## 前提条件 {#prerequisites}

コミュニティサイトを作成する前に、以下の手順をおこなう必要があります。**

* 1 つ以上のパブリッシュインスタンスが実行されているようにします。
* enable the [tunnel service](/help/communities/deploy-communities.md#tunnel-service-on-author) to manage members and member groups
* [プライマリパブリッシャー](/help/communities/deploy-communities.md#primary-publisher)を指定します。
* プライマリパブリッシャーのポートがデフォルト（4503）以外の場合は、[レプリケーションを設定します](/help/communities/deploy-communities.md#replication-agents-on-author)。

サイトで様々な機能がサポートされるよう確実に準備するために、次の手順を実行することをお勧めします。

* [最新の機能パック](/help/communities/deploy-communities.md#latestfeaturepack)をインストールします。
* AEM Communities で [Adobe Analytics](/help/communities/analytics.md) を有効にします。
* [電子メール](/help/communities/email.md)を設定します。
* [コミュニティ管理者](/help/communities/users.md#creating-community-members)を指定します。
* ソーシャルログインの [OAuth ハンドラーを有効にします](/help/communities/social-login.md#adobe-granite-oauth-authentication-handler)。

## コミュニティサイトコンソールへのアクセス {#accessing-communities-sites-console}

オーサー環境でコミュニティサイトコンソールに移動するには、

* グローバルナビゲーションから：**コミュニティ、サイト**

コミュニティサイトコンソールには、既存のコミュニティサイトが表示されます。このコンソールから、コミュニティサイトを作成、編集、管理、削除できます。

新しいコミュニティサイトを作成するには、「**作成**」アイコンを選択します。

ネストされたグループのオーサリング、変更、公開、書き出しまたは追加をおこなうために既存のコミュニティサイトにアクセスするには、サイトのフォルダーアイコンを選択します。

For example, the following image shows the main Communities Sites console displaying the folders for two community sites : [enable](/help/communities/getting-started-enablement.md) and [engage](/help/communities/getting-started.md) :

![chlimage_1-154](assets/chlimage_1-154.png)

## サイト作成 {#site-creation}

サイト作成コンソールでは、選択した[コミュニティサイトテンプレート](/help/communities/sites.md)と設定に基づき、サイトの機能を段階的に組み立てることができます。

作成されるサイトには、いずれもログイン機能が含まれます。これは、サイト訪問者がコンテンツの投稿、メッセージの送信またはグループへの参加をおこなう前に、サインインする必要があるからです。その他の機能には、ユーザープロファイル、メッセージング、通知、サイトメニュー、検索、テーマ設定、ブランドなどがあります。

The process is launched by selecting the `Create` button located at the top of the Communities Sites console.

作成プロセスでは、一連の手順がパネル形式で表示されます。パネルには、設定する機能セット（サブパネルとして表示）が含まれています。最後の手順でサイトをコミットする前に、**次の**手順または**戻る**前の手順に進むことができます。

### Step 1 : Site Template {#step-site-template}

![newsitetemplate](assets/newsitetemplate.png)

サイトテンプレートパネルでは、タイトル、説明、サイトのルート、ベース言語、名前およびサイトテンプレートを指定します。

* **コミュニティサイトのタイトル**:サイトの表示タイトル。タイトルは、公開済みのサイトとサイト管理UIに表示されます。

* **コミュニティサイトの説明**:サイトの説明。説明は公開済みサイトに表示されません。

* **コミュニティサイトのルート**:サイトのルートパス。
The default root is `/content/sites`, but the root may be moved to any location within the web site.

* **コミュニティサイトの基本言語** :(単一言語の場合は手を付けないでください。英語)プルダウンメニューを使用して ** 、使用可能な言語(ドイツ語、イタリア語、フランス語、日本語、スペイン語、ポルトガル語（ブラジル）、中国語（繁体字）、中国語（簡体字）)から1つ以上のベース言語を選択します。 One community site will be created for each language added, and will exist within the same site folder following the best practice described in [Translating Content for Multilingual Sites](/help/sites-administering/translation.md). 各サイトのルートページには、選択したいずれかの言語の言語コード（例えば、英語では「en」、フランス語では「fr」）で名付けられた子ページが含まれます。

* **コミュニティサイト名**:urlに表示されるサイトのルートページの名前

   * 名前はサイトの作成後には容易に変更できないので、再確認してください
   * ベースURL ( `https://*server:port/site root/site name*)` は `Community Site Name`

   * 有効な URL に、ベース言語コード + 「.html」を追加します。
      *例えば*、 `https://localhost:4502/content/sites/mysight/en.html`

* **コミュニティサイトテンプレート** メニュー：プルダウンメニューを使用して、利用可能なコミュニティサ [イトテンプレートを選択しま](/help/communities/tools.md)す。

「**次へ**」を選択します。

### 手順 2：デザイン {#step-design}

デザインパネルには、テーマとブランドバナーを選択するための、以下の 2 つのサブパネルが含まれています。

#### コミュニティサイトテーマ {#community-site-theme}

![sitetheme](assets/sitetheme.png)

このフレームワークでは、レスポンシブで柔軟なサイトデザインを実現できるよう、[Twitter Bootstrap](https://twitterbootstrap.org/) を使用しています。プリロードされた多数のブートストラップテーマの1つを選択して、選択したコミュニティサイトテンプレートのスタイルを設定したり、ブートストラップテーマをアップロードしたりできます。

選択すると、テーマの上に不透明な青色のチェックマークのオーバーレイが表示されます。

コミュニティサイトの公開後は、[プロパティを編集](#modifying-site-properties)し、別のテーマを選択できます。

#### コミュニティサイトブランディング {#community-site-branding}

![chlimage_1-155](assets/chlimage_1-155.png)

コミュニティサイトブランディングとは、各ページ上部にヘッダーとして表示される画像のことです。

画像の幅は、予想されるブラウザー内でのページの表示に合わせます。画像の高さは 120 ピクセルにします。

画像を選択するときは、次の点に注意してください。

* 画像の上端から測定して 120 ピクセルの高さとなるように画像を切り抜きます。
* 画像はブラウザーウィンドウの左端に固定されます。
* 画像はリサイズされず、以下のように調整されます。

   * 画像の幅がブラウザーの幅より短いときは、画像が水平方向に繰り返し表示されます。
   * ブラウザーの幅よりも大きい場合、画像は切り抜かれたように見えます

「**次へ**」を選択します。

### 手順 3：設定 {#step-settings}

設定パネルには複数のサブパネルが含まれています。各サブパネルに表示される機能を設定した後に、サイト作成の最後の手順に進みます。

* [ユーザー管理](#user-management)
* [タグ付け](#tagging)
* [役割](#roles)
* [モデレート](#moderation)
* [Analytics](#analytics)
* [翻訳](#translation)
* [イネーブルメント](#enablement)

>[!NOTE]
>
>**トンネルサービスの有効化**
>
>いくつかの設定サブパネルでは、信頼されているメンバーを、UGC のモデレーター、グループの管理者またはパブリッシュ環境でのイネーブルメントリソースの連絡先に割り当てることができます。
>
>The convention is for publish-side [users and user groups](/help/communities/users.md) (members and member groups) to not be duplicated in the author environment.
>
>したがって、オーサー環境でコミュニティサイトを作成し、信頼されているメンバーを様々な役割に割り当てる場合は、パブリッシュ環境からメンバーのデータを取得する必要があります。
>
>これは、作成者環境でを有効にす ` [AEM Communities Publish Tunnel Service](/help/communities/deploy-communities.md#tunnel-service-on-author)`ることで達成されます。

#### ユーザー管理 {#user-management}

![createsitesettings](assets/createsitesettings.png)

>[!NOTE]
>
>It is recommended that [enablement community sites](/help/communities/overview.md#enablement-community) be private (contact your account representative for more information).
>
>コミュニティサイトを非公開にするとは、匿名のサイト訪問者に対してアクセスを拒否し、自己登録やソーシャルログインを使用禁止にすることです。

* **ユーザー登録を許可**&#x200B;オンにすると、サイト訪問者は自己登録をしてコミュニティメンバーになることができます。If unchecked, the community site is *restricted* and site visitors must be assigned to the community site&#39;s members group, make a request or be sent an invitation by email. 選択しない場合、匿名アクセスは許可されません。
*private *コミュニティサイトのチェックを外します。 初期設定はオンです。

* **匿名アクセスを許可する**このチェックボックスをオンにすると、コミュニティサイトは*open *開かれ、サイトの訪問者はすべてこのサイトにアクセスできます。
オフにすると、サインイン済みのメンバーのみがサイトにアクセスできます。*private *コミュニティサイトのチェックを外します。 初期設定はオンです。

* **メッセージを許可**&#x200B;オンにすると、メンバーはコミュニティサイト内の別のメンバーおよびグループにメッセージを送信できます。オフにすると、コミュニティのメッセージング機能は設定されません。初期設定はオフです。

* **ソーシャルログインを許可：Facebook**オンの場合、サイト訪問者はFacebookアカウントの資格情報を使用してサインインできます。 The selected [Facebook cloud configuration](/help/communities/social-login.md#create-a-facebook-connect-cloud-service) should be configured to add users to the community site&#39;s members group once the community site is created.
オフにすると、Facebook ログインは表示されません。非公開のコミュニティサイトの場合はオフのままにします。**&#x200B;初期設定はオフです。

* **ソーシャルログインを許可：Twitter**&#x200B;オンにすると、サイト訪問者は Twitter のアカウント資格情報でサインインできます。The selected [Twitter cloud configuration](/help/communities/social-login.md#create-a-twitter-connect-cloud-service) should be configured to add users to the community site&#39;s members group once the community site is created.
オフにすると、Twitter ログインは表示されません。非公開のコミュニティサイトの場合はオフのままにします。**&#x200B;初期設定はオフです。

>[!NOTE]
>
>**ソーシャルログインの許可**
>
>Facebook と Twitter のサンプル設定が存在し、選択可能な場合がありますが、[実稼動環境](/help/sites-administering/production-ready.md)では、カスタム Facebook アプリケーションとカスタム Twitter アプリケーションを作成する必要があります。[Facebook と Twitter を使用したソーシャルログイン](/help/communities/social-login.md)を参照してください。

#### タグ付け {#tagging}

![chlimage_1-156](assets/chlimage_1-156.png)

コミュニティコンテンツに適用できるタグを制御するには、以前に[タグ付けコンソール](/help/sites-administering/tags.md#tagging-console)で定義したタグ名前空間を選択します。

また、コミュニティサイトに対してタグ名前空間を選択すると、カタログとリソースを定義するときに表示される選択肢が制限されます。See [Tagging Enablement Resources](/help/communities/tag-resources.md) for important information.

* テキスト検索ボックス：入力を開始すると、サイト上での使用が許可されているタグが表示されます。

#### 役割 {#roles}

![コミュニティの役割](assets/site-admin-2.png)

[コミュニティメンバーの役割](/help/communities/users.md)は、これらの設定で割り当てます。

コミュニティメンバーは先行入力検索で簡単に検索できます。

* **コミュニティマネー**&#x200B;ジャーの入力を開始し、コミュニティメンバーやメンバーグループを管理できる1つ以上のコミュニティメンバーまたはメンバーグループを選択します。

* **コミュニティモデレーター**&#x200B;テキストを入力し、ユーザー生成コンテンツの信頼されたモデレーターとなる、1 人以上のコミュニティメンバーまたは 1 つ以上のメンバーグループを選択します。

* **コミュニティ特権メンバ**&#x200B;ーの入力を開始し、コミュニティ機能に対して選択された場合に新しいコンテンツを作成する機能を与える1つ以上のコミュニティメンバー `Allow Privileged Member` またはメンバーグループを [選択します](/help/communities/functions.md)。

* **コミュニティ管理**&#x200B;者他のサイト管理者やデフォルトのコミュニティ管理者とは独立したサイト構造を処理できる1人または複数のサイト管理者を入力して選択します。 階層の任意のレベルでグループを作成し、ネストされたグループのデフォルトの管理者になることができます（ただし、後でネストされたグループの管理者の役割から削除することもできます）。

#### モデレート {#moderation}

![chlimage_1-157](assets/chlimage_1-157.png)

ユーザー生成コンテンツ（UGC）のモデレートのグローバル設定は、ここで制御します。個々のコンポーネントには、モデレートを制御するための追加設定があります。

* **コンテンツを事前にモデレート**&#x200B;オンにすると、投稿されたコミュニティコンテンツは、モデレーターが承認するまで表示されません。初期設定はオフです。For more information, see [Moderating Community Content](/help/communities/moderate-ugc.md#premoderation).

* **コンテンツが非表示になるまでのフラグ設定しきい値** 0 より大きい値を指定した場合は、その回数だけフラグが設定されると、トピックまたは投稿が非公開になります。-1に設定した場合、フラグ付けされたトピックまたは投稿は公開ビューで非表示になりません。 初期設定は 5 です。

#### Analytics {#analytics}

![chlimage_1-158](assets/chlimage_1-158.png)

* **Analytics を有効にする** Adobe Analytics が Communities 機能向けに[設定されている](/help/communities/analytics.md)場合にのみ使用できます。初期設定はオフです。オンにすると、以下の追加選択メニューが表示されます。

![chlimage_1-159](assets/chlimage_1-159.png)

* **クラウド設定フレームワークの参照**プルダウンメニューから、このコミュニティサイト用に設定した Analytics クラウドサービスフレームワークを選択します。
   `Communities`は、 [Analytics Configuration for Communities Featuresドキュメントのフレームワークの例です](/help/communities/analytics.md#aem-analytics-framework-configuration) 。

#### TRANSLATION {#translation}

![chlimage_1-160](assets/chlimage_1-160.png)

* **機械翻訳を許可**&#x200B;オンにすると（初期設定はオフ）、このサイト内の UGC に対する機械翻訳が有効になります。これは、サイトが多言語サイトとして設定されている場合でも、ページコンテンツなどの他のコンテンツには影響しません。 See [Translating User Generated Content](/help/communities/translate-ugc.md) for information on configuring a licensed translation service for AEM Communities. See [Translating Content for Multilingual Sites](/help/sites-administering/translation.md) for a complete overview.

![chlimage_1-161](assets/chlimage_1-161.png)

* **選択した言語の機械翻訳を有効にする**&#x200B;機械翻訳に対して有効になっている言語は、翻訳統合設定で指定されたシステム設定に [デフォルトで設定されま](/help/communities/translate-ugc.md#translation-integration-configuration)す。 これらのデフォルト設定は、デフォルトを削除したり、プルダウンメニューから他の言語を選択したりすることで、このサイトで上書きされる場合があります。

* **翻訳プロバイダーの選択**&#x200B;デフォルトでは、サービスプロバイダーはデモ用にのみを使用する体験版サ `microsoft`ービスです。 If no translation service provider is licensed, **Allow Machine Translation** should be unchecked.

* **グローバル共有ストアを選択**&#x200B;複数の言語コピーがある Web サイトでは、グローバル共有ストアを使用して、各言語コピーから単一スレッドの会話を閲覧できるようにできます。これを実現するには、言語コピーとして含まれているいずれかの言語を選択します。Default is *No Global Shared Store*.

* **変換プロバイダー設定を選択**&#x200B;ライセンスがある翻訳プロバイダー用に作成された[翻訳統合フレームワーク](/help/sites-administering/tc-tic.md)を選択します。

* **コミュニティサイトの翻訳オプションを選択**

   * **ページ全体を翻訳**&#x200B;選択すると、ページ上のすべての UGC がそのページの基本言語に翻訳されます。初期設定では選択されていません。**

   * **選択項目のみ翻訳**&#x200B;選択すると、それぞれの投稿の横に翻訳オプションが表示され、個々の投稿をページの基本言語に翻訳することを許可できます。初期設定では選択されています。**

* **保持オプションを選択**

   * **ユーザーのリクエストにより貢献度を翻訳し、その後保持する**&#x200B;選択すると、リクエストがあるまでコンテンツは翻訳されません。翻訳後、翻訳はリポジトリに保存されます。初期設定では選択されていません。**

   * **翻訳を保持しない**&#x200B;選択すると、翻訳はリポジトリに保存されません。選択されていないと、翻訳は保持されます。初期設定では選択されていません。**

* **スマートレンダリング**&#x200B;次のいずれかを選択します。

   * `Always show contributions in the original language` (デフォルト値)
   * `Always show contributions in user preferred language`
   * `Show contributions in user preferred language for only logged-in users`

#### イネーブルメント {#enablement}

![chlimage_1-162](assets/chlimage_1-162.png)

The `ENABLEMENT`settings are applicable when the chosen community site template includes the [assignments function](/help/communities/functions.md#assignments-function), which is available when the enablement features are licensed and [configured](/help/communities/enablement.md). 割り当て機能を含むリファレンスサイトテンプレートは、 `Reference Structured Learning Site Template.`

* **イネーブルメントマネージャ**（必須）このイネーブルメントコミュニティを管理す `Community Enablementmanagers` るには、グループのメンバーのみを選択できます。 実施可能マネージャは、リソースにメンバを割り当てる責任を負います。 See also [Managing Users and User Groups](/help/communities/users.md).

* **Marketing Cloud 組織 ID**（オプション）[Video Heartbeat Analytics](/help/communities/analytics.md#video-heartbeat-analytics) のライセンスの ID です。

「**次へ**」を選択します。

### 手順 4：コミュニティサイトの作成 {#step-create-communities-site}

調整が必要な場合は、「**戻る**」ボタンを使用して調整を行います。

Once **Create** is selected and started, the process of creating the site cannot be interrupted.

サイト作成後は、以下のようになります。

* URL（ノード名）の変更はサポートされていません。
* コミュニティサイトテンプレートに後から変更を加えても、作成済みのコミュニティサイトに影響が及ぶことはありません。
* コミュニティサイトテンプレートを無効にしても、作成済みのコミュニティサイトに影響が及ぶことはありません。
* コミュニティサイトのプロパティを変更することで、サイトの[構造](#modify-structure)を編集できます。

![chlimage_1-163](assets/chlimage_1-163.png)

プロセスが完了すると、新しいサイトのフォルダーがコミュニティサイトコンソールに表示されます。このコンソールで、作成者がページコンテンツを追加したり、管理者がサイトのプロパティを変更したりできます。

![chlimage_1-164](assets/chlimage_1-164.png)

コミュニティサイトを変更するには、そのプロジェクトフォルダーを選択して開きます。

![siteactions-1](assets/siteactions-1.png)

When hovering over a site with a mouse, or touching a site card, icons appear which allow for [editing the site in author mode](#authoring-site-content), [opening the site properties for modification](#modifying-site-properties), [publishing the site](#publishing-the-site), [exporting the site](#exporting-the-site), and [deleting the site](#deleting-the-site).

## サイトコンテンツのオーサリング {#authoring-site-content}

![chlimage_1-165](assets/chlimage_1-165.png)

サイトのコンテンツは、他の AEM Web サイトと同じツールを使用してオーサリングできます。To open the site for authoring, select the `Open Site` iconm that appears on hovering the site with mouse. サイトが新しいタブで開き、Communitiesのサイトコンソールにアクセスできるようになります。

![chlimage_1-166](assets/chlimage_1-166.png)

>[!NOTE]
>
>AEM に馴染みがない場合は、[基本操作](/help/sites-authoring/basic-handling.md)に関するドキュメントおよび[ページのオーサリングのクイックガイド](/help/sites-authoring/qg-page-authoring.md)を参照してください。

## サイトプロパティの変更 {#modifying-site-properties}

![chlimage_1-167](assets/chlimage_1-167.png)

The properties of an exisitng site, specified during the site creation process, can be modified by selecting the `Edit Site`icon that appears on hovering the site with mouse.

`Details of the following properties match the descriptions provided in the` 「サイ [トの作成](#site-creation) 」セクション。

![chlimage_1-168](assets/chlimage_1-168.png)

### 基本事項の変更 {#modify-basic}

基本パネルでは、次のものを変更できます。

* コミュニティサイトのタイトル
* コミュニティサイトの説明

コミュニティサイト名は変更できません。

別のコミュニティサイトテンプレートを選択しても、テンプレートとサイトの間に関係は残っていないので、既存のコミュニティサイトに影響が及ぶことはありません。

その一方で、コミュニティサイトの[構造](#modify-structure)は変更できます。

### 構造の変更 {#modify-structure}

構造パネルでは、最初にコミュニティサイトテンプレートから作成された構造を変更できます。パネルから、

* 追加の[コミュニティ機能](/help/communities/functions.md)をサイト構造にドラッグ＆ドロップできます。
* サイト構造内の各コミュニティ機能の上に次のアイコンが表示されます。

   * **`gear icon`**
表示タイトル、URL名*、権限を持つメンバー・グループなどの設 [定の編集](/help/communities/users.md#privilegedmembersgroups)

   * **`trashcan icon`**
サイト構造から関数を削除（削除）

   * **`grid icon`**
サイトのトップレベルナビゲーションバーに表示される関数の順序を変更する

>[!NOTE]
>
>トップにある機能を除き、サイト構造のすべての機能の順序を変更できます。したがって、コミュニティサイトのホームページは変更できません。

>[!CAUTION]
>
>* 表示タイトルを変更しても副次的な影響はありませんが、コミュニティサイトに属するコミュニティ機能の URL 名を編集することは推奨されません。
例えば、URL の名前を変更しても、既存の UGC は移動されません。そのため、UGC が「失われる」ことになります。

>[!CAUTION]
The groups function must *not *be the *first nor the only* function in the site structure.
他の機能（[ページ機能](/help/communities/functions.md#page-function)など）を含め、その機能を 1 番目にリストする必要があります。

#### 例：コミュニティのサイト構造へのカタログ機能の追加 {#example-adding-a-catalog-function-to-a-community-site-structure}

![chlimage_1-169](assets/chlimage_1-169.png)

### デザインの変更 {#modify-design}

デザインパネルでは、適用する新しいテーマを選択できます。

* [コミュニティサイトテーマ](#community-site-theme)
* [コミュニティサイトブランディング](#community-site-branding)

   * ブランド画像を変更するには、パネルの一番下までスクロールします。

### 設定の変更 {#modify-settings}

設定パネルでは、コミュニティサイト作成の手順 3 のサブパネルにあるほとんどの設定にアクセスできます。

* [ユーザー管理](#user-management)
* [タグ](#tagging)
* [モデレート](#moderation)
* [メンバーの役割](#roles)
* [Analytics](#analytics)
* [翻訳](#translation)

### サムネイルの変更 {#modify-thumbnail}

サムネイルパネルでは、コミュニティサイトコンソールでサイトを表現する画像をアップロードできます。

### イネーブルメントの変更 {#modify-enablement}

イネーブルメントパネルでは、コミュニティサイトの作成中に表示された設定にアクセスできます。

See the [ENABLEMENT](#enablement) description.

## サイトの公開 {#publishing-the-site}

After a community site has been newly created or modified, it is possible to publish (activate) the site by selecting the `Publish Site` icon, that appears on mouse hover over the site.

![chlimage_1-170](assets/chlimage_1-170.png)

サイトが正常に公開されると、次のようなメッセージが表示されます。

![chlimage_1-171](assets/chlimage_1-171.png)

### ネストされたグループでの公開 {#publishing-with-nested-groups}

コミュニティサイトを公開した後、[グループコンソール](/help/communities/groups.md)を使用して作成された各サブコミュニティ（ネストされたグループ）を個別に公開する必要があります。

## サイトの書き出し {#exporting-the-site}

![chlimage_1-172](assets/chlimage_1-172.png)

サイトにマウスポインターを置くと表示される書き出しアイコンを選択して、コミュニティサイトのパッケージを作成します。このパッケージは、[パッケージマネージャー](/help/sites-administering/package-manager.md)に格納され、ダウンロード可能になります。UGC はサイトパッケージに含まれていません。

## サイトの削除 {#deleting-the-site}

![deleteicon](assets/deleteicon.png)

コミュニティサイトを削除するには、サイトを削除アイコンを選択します。このアイコンは、コミュニティサイトコンソール内でサイトにマウスポインターを置くと表示されます。サイトを削除すると、UGC やユーザーグループ、アセット、データベースレコードなど、そのサイトに関連付けられているアイテムがすべて削除されます。

## 作成されたコミュニティユーザーグループ {#created-community-user-groups}

新しいコミュニティサイトが公開されると、新しいメンバーグループが作成されます（ユーザーグループはパブリッシュ環境で作成されます）。各グループには、様々な管理の役割およびメンバーの役割に応じて適切な権限が設定されます。

The name created for the member groups includes the *site-name* given the site in [Step 1](#step13asitetemplate) (the name which appears in the URL) as well as an unique ID to avoid conflicts with community sites and groups having the same site-name for different community site roots.

例えば、「Getting Started Tutorial」というタイトルを持つサイトのサイト名が「engage」の場合、モデレーターのユーザーグループは次のようになります。

* タイトル：コミュニティ Engage モデレーター
* 名前：community-*engage-uid*-moderators

サイト作成中にモデレーターまたはグループ管理者の役割を割り当てられたメンバーは、適切なグループとメンバーグループに割り当てられます。これらのグループとメンバーの割り当ては、新しいサイトが公開されるときに、公開時に作成されます。

For details, see [Managing Users and User Groups](/help/communities/users.md).

>[!NOTE]
[ソーシャルログインを許可：Facebook](#user-management) が有効な場合は、以下に示すユーザーグループが作成された後に、
* community-*&lt;site-name>*-*&lt;uid>*-members

is created, the applied [Facebook cloud service](/help/communities/social-login.md#createafacebookcloudservice) should be configured to add users to this group.

## 認証エラーの設定 {#configure-for-authentication-error}

ユーザーが誤った資格情報を入力してログインに失敗した場合、コミュニティサイトはデフォルトでサンプルのログインページにリダイレクトします。This sample login will not be present on a [production server](/help/sites-administering/production-ready.md).

正しくリダイレクトするには、サイトを設定してパブリッシュ環境にプッシュした後、以下の手順を実行し、認証失敗時にコミュニティサイトにリダイレクトされるようにします。

* それぞれの AEM パブリッシュインスタンスに移動します。
* 最初に管理者権限でサインインします。
* [Web コンソール](/help/sites-deploying/configuring-osgi.md)にアクセスします。

   * for example, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

* locate `Adobe Granite Login Selector Authentication Handler`
* select the `pencil`icon to open the configuration for edit
* enter a** Login Page Mappings** as follows :
/content/sites/*&lt;site-name>*/path/to/login/page**:**/content/sites/*&lt;site-name>*
for example:
/content/sites/*engage*/en/signin:/content/sites/*engage*/en

* 「**Save**」を選択します。

![chlimage_1-173](assets/chlimage_1-173.png)

### 認証リダイレクトのテスト {#test-authentication-redirection}

ログインページマッピングをコミュニティサイト用に設定した前述の AEM パブリッシュインスタンス上で、次の操作をおこないます。

* コミュニティサイトのホームページを参照します。

   * for example, [https://localhost:4503/content/sites/engage/en.html](https://localhost:4503/content/sites/engage/en.html)

* 「ログアウト」を選択します。
* 「ログイン」を選択します。
* ユーザー名「x」やパスワード「x」など、明らかに誤っている資格情報を入力します。
* ログインページに「無効なログイン」エラーが表示されます。

![chlimage_1-174](assets/chlimage_1-174.png)

## 主なサイトのコンソールからコミュニティサイトへのアクセス {#accessing-community-sites-from-main-sites-console}

From the global navigation Sites console, community sites are located in the `Community Sites` folder.

コミュニティサイトにはこの方法でアクセスできますが、管理タスクをおこなう場合は、コミュニティサイトコンソールからコミュニティサイトにアクセスする必要があります。

![chlimage_1-175](assets/chlimage_1-175.png)

