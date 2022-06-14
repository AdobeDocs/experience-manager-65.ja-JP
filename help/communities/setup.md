---
title: 初期セットアップ
seo-title: Initial Setup
description: Communities の設定
seo-description: Setting up Communities
uuid: c53d280c-c5ae-47cf-8038-f0dea68e15ff
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 0d462ad1-5619-4bb6-9609-bc8987c40a0c
exl-id: 6bda0f09-7ae5-4540-b035-9dd249ac3186
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 45%

---

# 初期セットアップ {#initial-setup}

## オーサーインスタンスおよびパブリッシュインスタンスの開始 {#start-author-and-publish-instances}

開発およびデモの目的では、1 つのオーサーインスタンスと 1 つのパブリッシュインスタンスを実行する必要があります。

これをおこなうには、基本的なAEM [はじめに](../../help/sites-deploying/deploy.md#getting-started) 手順は次のようになります。

* でのオーサー環境 [localhost:4502](http://localhost:4502/)
* でのパブリッシュ環境 [localhost:4503](http://localhost:4503/)

AEM Communities では、各環境を次の目的で使用します。

* オーサー環境は次の場合に使用します。

   * サイト、テンプレートおよびコンポーネントの開発。
   * 管理タスクと設定タスク

* パブリッシュ環境は、次のもの用です。

   * コンテンツを投稿およびモデレートするコミュニティエクスペリエンス。
   * コミュニティグループ、メンバー、メンバーグループを作成する。

>[!NOTE]
>
>AEM に馴染みがない場合は、[基本操作](../../help/sites-authoring/basic-handling.md)に関するドキュメントおよび[ページのオーサリングのクイックガイド](../../help/sites-authoring/qg-page-authoring.md)を参照してください。

## Communities の最新リリースのインストール {#install-latest-communities-release}

このチュートリアルでは、 [エンゲージメントコミュニティサイト](overview.md#engagement-community) とは、AEM Communities 6.2 機能パックバージョン 1.10 に基づいています。

最新の機能パックがインストールされていることを確認するには、次のページにアクセスします。

* [最新リリース](deploy-communities.md#latest-releases)

[イネーブルメントコミュニティサイト](overview.md#enablement-community)の作成に関するチュートリアルについては、[イネーブルメントのための AEM Communities 使用の手引き](getting-started-enablement.md)を参照してください。

## Analytics の設定 {#configure-analytics}

[コミュニティサイトで Adobe Analytics が設定されている](analytics.md)場合、コミュニティアクティビティに関する情報が利用できます。これにより、コミュニティメンバーのエクスペリエンスが向上するほか、サイトの管理者はフィードバックを得られます。

Adobe Analyticsとの統合はオプションです。

## 電子メール通知の設定 {#configure-email-for-notifications}

通知機能。デフォルトでは、 `Communities Sites` コンソール。通知用の e メールチャネルを提供します。

これを使用するには、電子メールをサイト用に適切に設定する必要があります。

[電子メールの設定](email.md)を参照してください。

## トンネルサービスの有効化 {#enable-the-tunnel-service}

オーサー環境でコミュニティサイトを作成するときに、トンネルサービスを使用すると、パブリッシュ環境に登録されている信頼済みのコミュニティメンバーに対して役割を割り当てることができます。また、トンネルサービスでは、 [メンバーコンソールとグループコンソール](members.md) （オーサー環境で）

この規則は、パブリッシュ環境で作成されたメンバーとメンバーグループに対して次のように適用されます。 *not* は、オーサー環境で再作成されます。 詳しくは、[ユーザーとユーザーグループの管理](users.md)を参照してください。

でトンネルサービスを有効にする簡単な手順 **作成者** インスタンスについては、 [トンネルサービス](deploy-communities.md#tunnel-service-on-author).

## コミュニティ管理者の役割 {#community-administrator-role}

コミュニティ管理者グループのメンバーは、コミュニティサイトの作成、サイトの管理、メンバーの管理（コミュニティの利用を禁止可能）およびコンテンツのモデレートを実行できます。

### ユーザーを作成 {#create-user}

でのユーザーの作成 *作成者*&#x200B;コミュニティ管理者の役割が割り当てられているユーザー：

* オーサーインスタンス上

   * 例： [http://localhost:4502/](http://localhost:4503/)

* 管理者権限でログイン

   * 例えば、ユーザー名「admin」/パスワード「admin」です。

* メインコンソールから、に移動します。 **[!UICONTROL ツール]** > **[!UICONTROL 運用]** > **[!UICONTROL セキュリティ]** > **[!UICONTROL ユーザー]**.
* 次の **編集** メニュー、選択 **[!UICONTROL ユーザーを追加]**

* 内 `Create New User` ダイアログの入力：

   * **[!UICONTROL ID]**:シリウス
   * **[!UICONTROL 電子メールアドレス]**：sirius.nilson@mailinator.com
   * **[!UICONTROL パスワード]**：password
   * **[!UICONTROL パスワードの確認 (&amp;A);]**:パスワード
   * **[!UICONTROL 名]**：Sirius
   * **[!UICONTROL 姓]**:ニルソン

### コミュニティ管理者グループに対する Sirius の割り当て {#assign-sirius-to-community-administrators-group}

下にスクロールして `Add User to Groups`:

* 「C」と入力して検索

   * 選択 `Community Administrators`
   * 選択 `Community Enablement Managers`

* 「**[!UICONTROL 保存]**」を選択します。

![create-user](assets/create-user.png)

## ソーシャルログインの有効化 {#enable-social-login}

Facebook および Twitter でデモバージョンのソーシャルログインを使用するには、先に以下をおこなう必要があります。

1. 修正パックまたは [最新の機能パック](deploy-communities.md#latestfeaturepack) (2017 年 3 月のFacebook API の変更に対応 )。
1. [OAuth プロバイダーを有効にする](social-login.md#adobe-granite-oauth-authentication-handler) （パブリッシュ環境で）

実稼動サーバーでは、ソーシャルログインの提供に必要なクラウドサービスを作成する必要があります。

[Facebook と Twitter を使用したソーシャルログイン](social-login.md)を参照してください。

## チュートリアルタグの作成 {#create-tutorial-tags}

`Tutorial` のタグ名前空間を使用して、エンゲージメントチュートリアルとイネーブルメントチュートリアルに使用するタグを作成します。

以下を使用： [タグ付けコンソール](../../help/sites-administering/tags.md#tagging-console) 次のタグを作成するには：

* `Tutorial: Sports / Baseball`
* `Tutorial: Sports / Gymnastics`
* `Tutorial: Sports / Skiing`
* `Tutorial: Arts / Visual`
* `Tutorial: Arts / Auditory`
* `Tutorial: Arts / History`

![tutorial-tags](assets/tutorial-tags.png)

手順に従って、次の操作を実行します。

1. [タグ権限の設定](../../help/sites-administering/tags.md#setting-tag-permissions).
1. [タグを公開](../../help/sites-administering/tags.md#publishing-tags).

AEM Communities 入門チュートリアル用に作成したタグのサンプルパッケージ

[ファイルを入手](assets/tutorial_tags-v63.zip)

## UGC 共通ストア用の MongoDB {#mongodb-for-ugc-common-store}

を設定することをお勧めしますが、オプションです。 [MSRP](msrp.md) (MongoDB) [共通店](working-with-srp.md) を使用すると、パブリッシュ環境またはオーサー環境からすべての UGC を柔軟にモデレートできます。

手順については、 [デモ用に MongoDB を設定する方法](demo-mongo.md).

デフォルトでは、AEM のオーサーインスタンスおよびパブリッシュインスタンスをインストールすると、ユーザー生成コンテンツ（UGC）は、[JSRP](jsrp.md)を使用してアクセスする [JCR Tar ストレージ](../../help/sites-deploying/platform.md)に格納されます。JSRP は共通のストアではありません。つまり、UGC は、UGC が入力されたインスタンス上でのみ表示されます。 通常、UGC はパブリッシュインスタンスで入力され、オーサー環境では表示されないので、モデレートタスクはすべてパブリッシュインスタンスを使用する必要があります。
