---
title: 初期設定
seo-title: 初期設定
description: Communities の設定
seo-description: Communities の設定
uuid: c53d280c-c5ae-47cf-8038-f0dea68e15ff
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 0d462ad1-5619-4bb6-9609-bc8987c40a0c
exl-id: 6bda0f09-7ae5-4540-b035-9dd249ac3186
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 45%

---

# 初期設定 {#initial-setup}

## オーサーインスタンスおよびパブリッシュインスタンスの開始 {#start-author-and-publish-instances}

開発およびデモの目的で、1つのオーサーインスタンスと1つのパブリッシュインスタンスを実行する必要があります。

そのためには、基本的なAEMの[はじめに](../../help/sites-deploying/deploy.md#getting-started)の手順に従います。その結果、次のようになります。

* [localhost:4502](http://localhost:4502/)のオーサー環境
* [localhost:4503](http://localhost:4503/)のパブリッシュ環境

AEM Communities では、各環境を次の目的で使用します。

* オーサー環境は次の用途です。

   * サイト、テンプレートおよびコンポーネントの開発。
   * 管理タスクと設定タスク

* パブリッシュ環境は、次の用途です。

   * コンテンツを投稿およびモデレートするコミュニティ体験。
   * コミュニティグループ、メンバー、メンバーグループを作成します。

>[!NOTE]
>
>AEM に馴染みがない場合は、[基本操作](../../help/sites-authoring/basic-handling.md)に関するドキュメントおよび[ページのオーサリングのクイックガイド](../../help/sites-authoring/qg-page-authoring.md)を参照してください。

## Communities の最新リリースのインストール {#install-latest-communities-release}

このチュートリアルでは、[エンゲージメントコミュニティサイト](overview.md#engagement-community)を作成し、AEM Communities 6.2機能パックバージョン1.10をベースにしています。

最新の機能パックがインストールされていることを確認するには、次のページにアクセスします。

* [最新リリース](deploy-communities.md#latest-releases)

[イネーブルメントコミュニティサイト](overview.md#enablement-community)の作成に関するチュートリアルについては、[イネーブルメントのための AEM Communities 使用の手引き](getting-started-enablement.md)を参照してください。

## Analytics の設定  {#configure-analytics}

[コミュニティサイトで Adobe Analytics が設定されている](analytics.md)場合、コミュニティアクティビティに関する情報が利用できます。これにより、コミュニティメンバーのエクスペリエンスが向上するほか、サイトの管理者はフィードバックを得られます。

Adobe Analyticsとの統合はオプションです。

## 電子メール通知の設定 {#configure-email-for-notifications}

`Communities Sites`コンソールを使用して作成されるすべてのサイトでデフォルトで使用できる通知機能は、通知用のEメールチャネルを提供します。

これを使用するには、電子メールをサイト用に適切に設定する必要があります。

[電子メールの設定](email.md)を参照してください。

## トンネルサービスの有効化  {#enable-the-tunnel-service}

オーサー環境でコミュニティサイトを作成するときに、トンネルサービスを使用すると、パブリッシュ環境に登録されている信頼済みのコミュニティメンバーに対して役割を割り当てることができます。トンネルサービスでは、オーサー環境の[メンバーコンソールとグループコンソール](members.md)からコミュニティメンバーにアクセスすることもできます。

通常、パブリッシュ環境で作成されたメンバーとメンバーグループは、オーサー環境で再作成&#x200B;*されません。*&#x200B;詳しくは、[ユーザーとユーザーグループの管理](users.md)を参照してください。

**author**&#x200B;インスタンスでトンネルサービスを有効にする簡単な手順については、[トンネルサービス](deploy-communities.md#tunnel-service-on-author)を参照してください。

## コミュニティ管理者の役割 {#community-administrator-role}

コミュニティ管理者グループのメンバーは、コミュニティサイトの作成、サイトの管理、メンバーの管理（コミュニティの利用を禁止可能）およびコンテンツのモデレートを実行できます。

### ユーザーを作成 {#create-user}

*author*&#x200B;にコミュニティ管理者の役割を割り当てるユーザーを作成します。

* オーサーインスタンス上

   * 例： [http://localhost:4502/](http://localhost:4503/)

* 管理者権限でログイン

   * 例：ユーザー名「admin」/パスワード「admin」

* メインコンソールで、**[!UICONTROL ツール]** / **[!UICONTROL 操作]** / **[!UICONTROL セキュリティ]** / **[!UICONTROL ユーザー]**&#x200B;に移動します。
* **編集**&#x200B;メニューから、「**[!UICONTROL ユーザーを追加]**」を選択します。

* `Create New User`ダイアログで、次のように入力します。

   * **[!UICONTROL ID]**:シリウス
   * **[!UICONTROL 電子メールアドレス]**：sirius.nilson@mailinator.com
   * **[!UICONTROL パスワード]**：password
   * **[!UICONTROL パスワードの確認(&amp;A);]**:パスワード
   * **[!UICONTROL 名]**：Sirius
   * **[!UICONTROL 姓]**:ニルソン

### コミュニティ管理者グループに対する Sirius の割り当て {#assign-sirius-to-community-administrators-group}

`Add User to Groups`まで下にスクロールします。

* 検索するには&#39;C&#39;と入力します

   *  `Community Administrators`
   *  `Community Enablement Managers`

* 「**[!UICONTROL 保存]**」を選択します。

![create-user](assets/create-user.png)

## ソーシャルログインの有効化 {#enable-social-login}

Facebook および Twitter でデモバージョンのソーシャルログインを使用するには、先に以下をおこなう必要があります。

1. 修正パックまたは[最新の機能パック](deploy-communities.md#latestfeaturepack)をインストールします(2017年3月のFacebook APIの変更に対応)。
1. [パブリッシュ環境で](social-login.md#adobe-granite-oauth-authentication-handler) OAuthプロバイダーを有効にします。

実稼動サーバーでは、ソーシャルログインの提供に必要なクラウドサービスを作成する必要があります。

[Facebook と Twitter を使用したソーシャルログイン](social-login.md)を参照してください。

## チュートリアルタグの作成  {#create-tutorial-tags}

`Tutorial` のタグ名前空間を使用して、エンゲージメントチュートリアルとイネーブルメントチュートリアルに使用するタグを作成します。

[タグ付けコンソール](../../help/sites-administering/tags.md#tagging-console)を使用して、次のタグを作成します。

* `Tutorial: Sports / Baseball`
* `Tutorial: Sports / Gymnastics`
* `Tutorial: Sports / Skiing`
* `Tutorial: Arts / Visual`
* `Tutorial: Arts / Auditory`
* `Tutorial: Arts / History`

![tutorial-tags](assets/tutorial-tags.png)

その後、次の手順に従います。

1. [タグの権限を設定します](../../help/sites-administering/tags.md#setting-tag-permissions)。
1. [タグを公開します](../../help/sites-administering/tags.md#publishing-tags)。

AEM Communities 入門チュートリアル用に作成したタグのサンプルパッケージ

[ファイルを入手](assets/tutorial_tags-v63.zip)

## UGC 共通ストア用の MongoDB {#mongodb-for-ugc-common-store}

[MSRP](msrp.md)(MongoDB)を[共通ストア](working-with-srp.md)として設定することをお勧めします。これにより、パブリッシュ環境やオーサー環境から、すべてのUGCを柔軟にモデレートできます。

手順については、[MongoDBをデモ用に設定する方法](demo-mongo.md)を参照してください。

デフォルトでは、AEM のオーサーインスタンスおよびパブリッシュインスタンスをインストールすると、ユーザー生成コンテンツ（UGC）は、[JSRP](jsrp.md)を使用してアクセスする [JCR Tar ストレージ](../../help/sites-deploying/platform.md)に格納されます。JSRPは共通ストアではありません。つまり、UGCは、UGCが入力されたインスタンスにのみ表示されます。 通常、UGCはパブリッシュインスタンスで入力され、オーサー環境では表示されないので、モデレートタスクはすべてパブリッシュインスタンスを使用する必要があります。
