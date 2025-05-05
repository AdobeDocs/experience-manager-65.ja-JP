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

## オーサーインスタンスとPublish インスタンスの開始 {#start-author-and-publish-instances}

開発とデモンストレーションの目的では、1 つのオーサーインスタンスと 1 つのパブリッシュインスタンスを実行する必要があります。

これを行うには、基本的なAdobe Experience Manager（AEM） [ はじめに ](../../help/sites-deploying/deploy.md#getting-started) の手順に従います。次のような結果になります。

* [localhost:4502](http://localhost:4502/) のオーサー環境
* [localhost:4503](http://localhost:4503/) のPublish環境

AEM Communitiesについては、

* オーサー環境の対象：

   * サイト、テンプレート、コンポーネントの開発。
   * 管理タスクと設定タスク

* Publish環境の目的：

   * コンテンツを投稿およびモデレートするコミュニティエクスペリエンス。
   * コミュニティグループ、メンバーおよびメンバーグループの作成。

>[!NOTE]
>
>AEMに詳しくない場合は、[ 基本操作 ](../../help/sites-authoring/basic-handling.md) および [ ページのオーサリングのクイックガイド ](../../help/sites-authoring/qg-page-authoring.md) に関するドキュメントを参照してください。

## 最新の Communities リリースのインストール {#install-latest-communities-release}

このチュートリアルは、AEM Communities 6.2 機能パックバージョン 1.10 に基づいた [ エンゲージメントコミュニティサイト ](overview.md#engagement-community) を作成します。

最新の機能パックがインストールされていることを確認するには、次の URL にアクセスしてください。

* [最新リリース](deploy-communities.md#latest-releases)

## Analytics を設定 {#configure-analytics}

[Adobe Analyticsがコミュニティ サイト用に構成されている場合 ](analytics.md)、コミュニティ メンバーのエクスペリエンスを向上させ、サイト管理者にフィードバックを提供するために、コミュニティ アクティビティに関する情報を利用できます。

Adobe Analyticsとの統合はオプションです。

## 通知用のメールの設定 {#configure-email-for-notifications}

通知機能は、`Communities Sites` コンソールを使用して作成されたすべてのサイトでデフォルトで使用でき、通知用のメールチャネルを提供します。

メールをサイト用に適切に設定することが必要です。

[ メールの設定 ](email.md) を参照してください。

## トンネル サービスを有効にする {#enable-the-tunnel-service}

オーサー環境でコミュニティサイトを作成する場合、トンネルサービスを使用すると、Publish環境に登録されている信頼できるコミュニティメンバーにロールを割り当てることができます。 また、トンネルサービスを使用すると、オーサー環境の [ メンバーコンソールとグループコンソール ](members.md) からコミュニティメンバーにアクセスできます。

この規則は、Publish環境で作成されたメンバーおよびメンバーグループをオーサー環境で再作成 *ない* うにするためのものです。 詳しくは、[ ユーザーとユーザーグループの管理 ](users.md) を参照してください。

**オーサー** インスタンスでトンネルサービスを有効にする簡単な手順については、[ トンネルサービス ](deploy-communities.md#tunnel-service-on-author) を参照してください。

## コミュニティ管理者役割 {#community-administrator-role}

コミュニティ管理者グループのメンバーは、コミュニティサイトの作成、サイトの管理、メンバーの管理（メンバーのコミュニティへの参加を禁止できます）、コンテンツの管理を行うことができます。

### ユーザーを作成 {#create-user}

コミュニティ管理者の役割が割り当てられている *author* 上にユーザーを作成します。

* オーサーインスタンス上

   * 例：[http://localhost:4502/](http://localhost:4503/)

* 管理者権限でログイン

   * 例：ユーザー名「admin」/パスワード「admin」

* メインコンソールから、**[!UICONTROL ツール]**/**[!UICONTROL 操作]**/**[!UICONTROL セキュリティ]**/**[!UICONTROL ユーザー]** に移動します。
* **編集** メニューから **[!UICONTROL ユーザーを追加]** を選択します

* `Create New User` ダイアログで、次のように入力します。

   * **[!UICONTROL ID]**: sirius
   * **[!UICONTROL メールアドレス]**:sirius.nilson@mailinator.com
   * **[!UICONTROL パスワード]**：password
   * **[!UICONTROL パスワードの確認&ast;]**：パスワード
   * **[!UICONTROL 名]**: Sirius
   * **[!UICONTROL 姓]**: Nilson

### Sirius のコミュニティ管理者グループへの割り当て {#assign-sirius-to-community-administrators-group}

`Add User to Groups` まで下にスクロール：

* 検索するには「C」を入力

   * `Community Administrators` を選択します。
   * `Community Enablement Managers` を選択します。

* 「**[!UICONTROL 保存]**」を選択します。

![create-user](assets/create-user.png)

## ソーシャルログインを有効にする {#enable-social-login}

facebookとTwitterによるソーシャルログインのデモバージョンを使用する前に、次の操作が必要です。

1. 修正パックまたは [ 最新の機能パック ](deploy-communities.md#latestfeaturepack) （2017 年 3 月のFacebook API の変更用）をインストールします。
1. パブリッシュ環境で [OAuth プロバイダーを有効にします ](social-login.md#adobe-granite-oauth-authentication-handler)。

実稼動サーバーの場合は、ソーシャルログインを提供するために必要なクラウドサービスを作成する必要があります。

[FacebookとTwitterを使用したソーシャルログイン ](social-login.md) を参照してください。

## チュートリアルタグの作成 {#create-tutorial-tags}

`Tutorial` のタグ名前空間を使用してタグを作成し、engage チュートリアルに使用できるようにします。

次のタグを作成するには、[ タグ付けコンソール ](../../help/sites-administering/tags.md#tagging-console) を使用します。

* `Tutorial: Sports / Baseball`
* `Tutorial: Sports / Gymnastics`
* `Tutorial: Sports / Skiing`
* `Tutorial: Arts / Visual`
* `Tutorial: Arts / Auditory`
* `Tutorial: Arts / History`

![tutorial-tags](assets/tutorial-tags.png)

その後、次の手順に従います。

1. [ タグの権限を設定します ](../../help/sites-administering/tags.md#setting-tag-permissions)。
1. [ タグをPublishします ](../../help/sites-administering/tags.md#publishing-tags)。

AEM Communitiesの「はじめに」Tutorials用に作成されたタグのサンプルパッケージ

[ファイルの取得](assets/tutorial_tags-v63.zip)

## MongoDB for UGC の共通ストア {#mongodb-for-ugc-common-store}

[MSRP](msrp.md) （MongoDB）を（共通ストア [ として設定して、パブリッシュ環境またはオーサー環境から、すべての UGC を柔軟にモデレートすることをお勧めしますが、これはオプションです ](working-with-srp.md)

手順については、[ デモ用に MongoDB を設定する方法 ](demo-mongo.md) を参照してください。

デフォルトでは、オーサーインスタンスとパブリッシュ AEM インスタンスをインストールすると、ユーザー生成コンテンツ（UGC）が [JCR Tar ストレージ ](../../help/sites-deploying/platform.md) に保存され、[JSRP](jsrp.md) を使用してアクセスできます。 JSRP は共通ストアではありません。つまり、UGC は、入力されたインスタンスでのみ表示されます。 通常、UGC はパブリッシュインスタンスに入力され、オーサー環境では表示されないので、すべてのモデレーションタスクでパブリッシュインスタンスを使用する必要があります。
