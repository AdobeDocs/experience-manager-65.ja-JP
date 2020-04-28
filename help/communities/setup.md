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
translation-type: tm+mt
source-git-commit: 6d425dcec4fab19243be9acb41c25b531a84ea74

---


# 初期設定 {#initial-setup}

## オーサーインスタンスおよびパブリッシュインスタンスの開始 {#start-author-and-publish-instances}

開発およびデモの目的で、1つの作成者と1つの発行インスタンスを実行する必要があります。

To do so, follow the basic AEM [Getting Started](../../help/sites-deploying/deploy.md#getting-started) instructions, which will result in:

* Author environment on [localhost:4502](http://localhost:4502/)
* Publish environment on [localhost:4503](http://localhost:4503/)

AEM Communities では、各環境を次の目的で使用します。

* 作成者の環境は次の場合に使用します。

   * サイト、テンプレート、およびコンポーネントの開発。
   * 管理タスクと設定

* 公開環境は次のものです。

   * コンテンツの投稿とモデレートのコミュニティエクスペリエンス。
   * コミュニティグループ、メンバーおよびメンバーグループの作成。

>[!NOTE]
>
>AEM に馴染みがない場合は、[基本操作](../../help/sites-authoring/basic-handling.md)に関するドキュメントおよび[ページのオーサリングのクイックガイド](../../help/sites-authoring/qg-page-authoring.md)を参照してください。


## Communities の最新リリースのインストール {#install-latest-communities-release}

This tutorial creates an [engagement community site](overview.md#engagement-community) and is based on AEM Communities 6.2 feature pack version 1.10.

最新の機能パックがインストールされていることを確認するには、次のページにアクセスします。

* [最新リリース](deploy-communities.md#latest-releases)

[イネーブルメントコミュニティサイト](overview.md#enablement-community)の作成に関するチュートリアルについては、[イネーブルメントのための AEM Communities 使用の手引き](getting-started-enablement.md)を参照してください。

## Analytics の設定 {#configure-analytics}

[コミュニティサイトで Adobe Analytics が設定されている](analytics.md)場合、コミュニティアクティビティに関する情報が利用できます。これにより、コミュニティメンバーのエクスペリエンスが向上するほか、サイトの管理者はフィードバックを得られます。

Adobe Analyticsとの統合はオプションです。

## 電子メール通知の設定 {#configure-email-for-notifications}

The notifications feature, available by default for all sites created using the `Communities Sites` console, provides an email channel for notifications.

これを使用するには、電子メールをサイト用に適切に設定する必要があります。

[電子メールの設定](email.md)を参照してください。

## トンネルサービスの有効化 {#enable-the-tunnel-service}

オーサー環境でコミュニティサイトを作成するときに、トンネルサービスを使用すると、パブリッシュ環境に登録されている信頼済みのコミュニティメンバーに対して役割を割り当てることができます。The tunnel service also allows access to community members from the [Members and Groups consoles](members.md) in the author environment.

The convention is for members and member groups created in the publish environment to *not* be recreated in the author environment. 詳しくは、[ユーザーとユーザーグループの管理](users.md)を参照してください。

For simple instructions to enable the tunnel service on an **author** instance, see [Tunnel Service](deploy-communities.md#tunnel-service-on-author).

## コミュニティ管理者の役割 {#community-administrator-role}

コミュニティ管理者グループのメンバーは、コミュニティサイトの作成、サイトの管理、メンバーの管理（コミュニティの利用を禁止可能）およびコンテンツのモデレートを実行できます。

### ユーザーを作成 {#create-user}

Create a user on *author*, who is assigned the role of Community Administrator:

* 作成者インスタンス

   * For example, [http://localhost:4502/](http://localhost:4503/)

* 管理者権限でサインイン

   * 例：ユーザー名「admin」/パスワード「admin」

* From the main console, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Security]** > **[!UICONTROL Users]**.
* From the **Edit **menu, select**[!UICONTROL Add User ]**

* ダイアログで、次のよ `Create New User` うに入力します。

   * **[!UICONTROL ID]**:シリア
   * **[!UICONTROL 電子メールアドレス]**：sirius.nilson@mailinator.com
   * **[!UICONTROL パスワード]**：password
   * **[!UICONTROL パスワードの確認(&amp;A);ast;]**:password
   * **[!UICONTROL 名]**：Sirius
   * **[!UICONTROL 姓]**:ニルソン

### コミュニティ管理者グループに対する Sirius の割り当て {#assign-sirius-to-community-administrators-group}

下にスクロールして次の操作を行い `Add User to Groups`ます。

* 検索するには&#39;C&#39;と入力してください

   *  `Community Administrators`
   *  `Community Enablement Managers`

* 「**[!UICONTROL 保存]**」を選択します。

![chlimage_1-301](assets/chlimage_1-301.png)

## ソーシャルログインの有効化 {#enable-social-login}

Facebook および Twitter でデモバージョンのソーシャルログインを使用するには、先に以下をおこなう必要があります。

1. Install a fix pack or [latest feature pack](deploy-communities.md#latestfeaturepack) (for March 2017 Facebook API changes).
1. [発行環境でOAuthプロバイダーを有効にします](social-login.md#adobe-granite-oauth-authentication-handler) 。

実稼動サーバーでは、ソーシャルログインの提供に必要なクラウドサービスを作成する必要があります。

[Facebook と Twitter を使用したソーシャルログイン](social-login.md)を参照してください。

## チュートリアルタグの作成 {#create-tutorial-tags}

`Tutorial` のタグ名前空間を使用して、エンゲージメントチュートリアルとイネーブルメントチュートリアルに使用するタグを作成します。

Use the [Tagging console](../../help/sites-administering/tags.md#tagging-console) to create the following tags:

* `Tutorial: Sports / Baseball`
* `Tutorial: Sports / Gymnastics`
* `Tutorial: Sports / Skiing`
* `Tutorial: Arts / Visual`
* `Tutorial: Arts / Auditory`
* `Tutorial: Arts / History`

![chlimage_1-302](assets/chlimage_1-302.png)

次の手順に従います。

1. [タグ権限を設定します](../../help/sites-administering/tags.md#setting-tag-permissions)。
1. [タグを公開します](../../help/sites-administering/tags.md#publishing-tags)。

AEM Communities 入門チュートリアル用に作成したタグのサンプルパッケージ

[ファイルを入手](assets/tutorial_tags-v63.zip)

## UGC 共通ストア用の MongoDB {#mongodb-for-ugc-common-store}

[MSRP](msrp.md) (MongoDB)を共通ストアとして設定することは推奨されますが、オプションです。これにより、発行環境または作成者 [](working-with-srp.md) （あるいはその両方）からすべてのUGCを柔軟にモデレートできます。

For instructions visit [How to Setup MongoDB for Demo](demo-mongo.md).

デフォルトでは、AEM のオーサーインスタンスおよびパブリッシュインスタンスをインストールすると、ユーザー生成コンテンツ（UGC）は、[JSRP](jsrp.md)を使用してアクセスする [JCR Tar ストレージ](../../help/sites-deploying/platform.md)に格納されます。JSRPは共通ストアではありません。つまり、UGCは、UGCが入力されたインスタンスでのみ表示されます。 通常、UGCは発行インスタンスに対して入力され、作成者環境には表示されないので、すべてのモデレートタスクが発行インスタンスを使用する必要があります。