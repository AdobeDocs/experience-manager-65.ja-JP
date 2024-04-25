---
title: 初期セットアップ
description: Adobe Experience Manager Communities の最初の設定方法について説明します。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
exl-id: 6bda0f09-7ae5-4540-b035-9dd249ac3186
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 2%

---

# 初期セットアップ {#initial-setup}

## オーサーインスタンスとパブリッシュインスタンスの開始 {#start-author-and-publish-instances}

開発とデモンストレーションの目的では、1 つのオーサーインスタンスと 1 つのパブリッシュインスタンスを実行する必要があります。

これを行うには、基本的なAdobe Experience Manager（AEM）の手順に従います [はじめに](../../help/sites-deploying/deploy.md#getting-started) 次のような指示が表示されます。

* オーサー環境： [localhost:4502](http://localhost:4502/)
* パブリッシュ環境： [localhost:4503](http://localhost:4503/)

AEM Communitiesについては、

* オーサー環境の対象：

   * サイト、テンプレート、コンポーネントの開発。
   * 管理タスクと設定タスク

* パブリッシュ環境は次の目的で使用されます。

   * コンテンツを投稿およびモデレートするコミュニティエクスペリエンス。
   * コミュニティグループ、メンバーおよびメンバーグループの作成。

>[!NOTE]
>
>AEMに詳しくない場合は、次のドキュメントを参照してください [基本操作](../../help/sites-authoring/basic-handling.md) および [ページのオーサリングのクイックガイド](../../help/sites-authoring/qg-page-authoring.md).

## 最新の Communities リリースのインストール {#install-latest-communities-release}

このチュートリアルでは、 [エンゲージメントコミュニティサイト](overview.md#engagement-community) また、AEM Communities 6.2 機能パック バージョン 1.10 に基づいています。

最新の機能パックがインストールされていることを確認するには、次の URL にアクセスしてください。

* [最新リリース](deploy-communities.md#latest-releases)

## Analytics を設定 {#configure-analytics}

条件 [Adobe Analyticsがコミュニティサイト用に設定されています](analytics.md)を参照すると、コミュニティメンバーのエクスペリエンスを向上させ、サイトの管理者にフィードバックを提供する、コミュニティアクティビティに関する情報を利用できます。

Adobe Analyticsとの統合はオプションです。

## 通知用のメールの設定 {#configure-email-for-notifications}

通知機能（を使用して作成されたすべてのサイトについてデフォルトで使用可能） `Communities Sites` コンソール：通知用のメールチャネルを提供します。

メールをサイト用に適切に設定することが必要です。

参照： [メールの設定](email.md).

## トンネル サービスを有効にする {#enable-the-tunnel-service}

オーサー環境でコミュニティサイトを作成する場合、トンネルサービスを使用すると、パブリッシュ環境で登録された信頼できるコミュニティメンバーに役割を割り当てることができます。 また、トンネルサービスでは、からコミュニティメンバーにアクセスすることもできます。 [メンバーコンソールとグループコンソール](members.md) オーサー環境で実行します。

パブリッシュ環境で作成されたメンバーおよびメンバーグループの規則は、次のとおりです。 *ではない* オーサー環境で再作成します。 詳しくは、を参照してください [ユーザーとユーザーグループの管理](users.md).

上でトンネル サービスを有効にするための簡単な手順 **作成者** インスタンスについては、を参照 [トンネルサービス](deploy-communities.md#tunnel-service-on-author).

## コミュニティ管理者役割 {#community-administrator-role}

コミュニティ管理者グループのメンバーは、コミュニティサイトの作成、サイトの管理、メンバーの管理（メンバーのコミュニティへの参加を禁止できます）、コンテンツの管理を行うことができます。

### ユーザーを作成 {#create-user}

でユーザーを作成 *作成者*、コミュニティ管理者の役割が割り当てられているユーザー：

* オーサーインスタンス上

   * 例： [http://localhost:4502/](http://localhost:4503/)

* 管理者権限でログイン

   * 例：ユーザー名「admin」/パスワード「admin」

* メインコンソールから、に移動します。 **[!UICONTROL ツール]** > **[!UICONTROL 運用]** > **[!UICONTROL セキュリティ]** > **[!UICONTROL ユーザー]**.
* から **編集** メニュー、選択 **[!UICONTROL ユーザーを追加]**

* が含まれる `Create New User` ダイアログで次の情報を入力：

   * **[!UICONTROL ID]**: sirius
   * **[!UICONTROL メールアドレス]**: sirius.nilson@mailinator.com
   * **[!UICONTROL パスワード]**：password
   * **[!UICONTROL パスワードの確認（&amp;Ast）]**：パスワード
   * **[!UICONTROL 名前（名）]**: Sirius
   * **[!UICONTROL 名前（姓）]**：ニルソン

### Sirius のコミュニティ管理者グループへの割り当て {#assign-sirius-to-community-administrators-group}

Scroll down to `Add User to Groups`:

* 検索するには「C」を入力

   * `Community Administrators` を選択します。
   * `Community Enablement Managers` を選択します。

* 「**[!UICONTROL 保存]**」を選択します。

![create-user](assets/create-user.png)

## ソーシャルログインを有効にする {#enable-social-login}

facebookとTwitterによるソーシャルログインのデモバージョンを使用する前に、次の操作が必要です。

1. 修正パックをインストールする [最新の機能パック](deploy-communities.md#latestfeaturepack) （2017 年 3 月のFacebook API の変更用）。
1. [OAuth プロバイダーの有効化](social-login.md#adobe-granite-oauth-authentication-handler) パブリッシュ環境で以下を行います。

実稼動サーバーの場合は、ソーシャルログインを提供するために必要なクラウドサービスを作成する必要があります。

参照： [facebookとTwitterを使用したソーシャルログイン](social-login.md).

## チュートリアルタグの作成 {#create-tutorial-tags}

のタグ名前空間を使用してタグを作成し、engage チュートリアルに使用できるようにします `Tutorial`.

の使用 [タグ付けコンソール](../../help/sites-administering/tags.md#tagging-console) 次のタグを作成します。

* `Tutorial: Sports / Baseball`
* `Tutorial: Sports / Gymnastics`
* `Tutorial: Sports / Skiing`
* `Tutorial: Arts / Visual`
* `Tutorial: Arts / Auditory`
* `Tutorial: Arts / History`

![tutorial-tags](assets/tutorial-tags.png)

その後、次の手順に従います。

1. [タグの権限の設定](../../help/sites-administering/tags.md#setting-tag-permissions).
1. [タグを公開する](../../help/sites-administering/tags.md#publishing-tags).

AEM Communitiesの「はじめに」Tutorials用に作成されたタグのサンプルパッケージ

[ファイルを入手](assets/tutorial_tags-v63.zip)

## MongoDB for UGC の共通ストア {#mongodb-for-ugc-common-store}

を設定することをお勧めしますが、オプションです [MSRP](msrp.md) （MongoDB）を [共通店舗](working-with-srp.md) を使用して、パブリッシュ環境またはオーサー環境から、すべての UGC を柔軟にモデレートできます。

手順については、を参照してください。 [MongoDB をデモ用に設定する方法](demo-mongo.md).

デフォルトでは、オーサーインスタンスとパブリッシュ AEM インスタンスをインストールすると、ユーザー生成コンテンツ（UGC）がに保存されます。 [JCR Tar ストレージ](../../help/sites-deploying/platform.md) （を使用してアクセスされる） [JSRP](jsrp.md). JSRP は共通ストアではありません。つまり、UGC は、入力されたインスタンスでのみ表示されます。 通常、UGC はパブリッシュインスタンスに入力され、オーサー環境では表示されないので、すべてのモデレーションタスクでパブリッシュインスタンスを使用する必要があります。
