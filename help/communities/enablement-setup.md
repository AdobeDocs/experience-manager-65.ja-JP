---
title: イネーブルメントのための初期設定
seo-title: Initial Setup
description: イネーブルメントのための初期設定
seo-description: Initial Setup for Enablement
uuid: 873ec41d-c088-41d9-a535-de5300661de6
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: f2ac3d66-cc79-498f-83fb-dd96feb88de2
exl-id: ed494922-3e15-4778-84c1-35c8846ce980
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 52%

---

# イネーブルメントのための初期設定  {#initial-setup-for-enablement}

## オーサーインスタンスおよびパブリッシュインスタンスの開始 {#start-author-and-publish-instances}

開発用およびデモ用の場合、1 つのオーサーインスタンスと 1 つのパブリッシュインスタンスを実行する必要があります。

基本のAEM [はじめに](../../help/sites-deploying/deploy.md#getting-started) 結果として生じる指示

* でのオーサー環境 [localhost:4502](http://localhost:4502/)
* でのパブリッシュ環境 [localhost:4503](http://localhost:4503/)

AEM Communities では、各環境を次の目的で使用します。

* オーサー環境は次の場合に使用します。

   * サイト、テンプレート、コンポーネント、イネーブルメントリソース、学習パスの開発。
   * イネーブルメントリソースと学習パスに対するメンバーおよびメンバーのグループの割り当て。
   * 割り当て、表示および投稿に関するレポートの生成。
   * 管理タスクと設定タスク

* パブリッシュ環境は、次のもの用です。

   * イネーブルメントマネージャが管理するトピックに基づく学習/トレーニング。
   * イネーブルメントリソースと学習パスにコメントを付け、評価します。
   * リソースの連絡先と連絡を取る。

>[!NOTE]
>
>AEM に馴染みがない場合は、[基本操作](../../help/sites-authoring/basic-handling.md)に関するドキュメントおよび[ページのオーサリングのクイックガイド](../../help/sites-authoring/qg-page-authoring.md)を参照してください。

## Communities の最新リリースのインストール {#install-latest-communities-release}

このチュートリアルでは、[イネーブルメントコミュニティサイト](overview.md#enablement-community)を作成します。最新の機能パックがインストールされていることを確認するには、次のページにアクセスします。

* [最新リリース](deploy-communities.md#latest-releases)

[エンゲージメントコミュニティサイト](overview.md#engagement-community)の作成に関するチュートリアルについては、[AEM Communities 使用の手引き](getting-started.md)を参照してください。

## イネーブルメント機能の設定 {#configure-enablement-features}

このチュートリアルに従って操作するには、[イネーブルメントをインストールして設定](enablement.md)する必要があります。これには、MySQL や FFmpeg などのサードパーティの商品が必要です。

## Analytics の設定 {#configure-analytics}

条件 [Adobe Analyticsはコミュニティサイト用に設定されています](analytics.md)を使用する場合、詳しくは [レポート](reports.md) コミュニティメンバー（学習者）に割り当てられたイネーブルメントリソースと学習パスに基づいて生成されます。

## 電子メール通知の設定 {#configure-email-for-notifications}

通知機能。デフォルトでは、 `Communities Sites` コンソール。通知用の e メールチャネルを提供します。

これを使用するには、電子メールをサイト用に適切に設定する必要があります。

[電子メールの設定](email.md)を参照してください。

## トンネルサービスの有効化 {#enable-the-tunnel-service}

オーサー環境でコミュニティサイトを作成するときに、トンネルサービスを使用すると、パブリッシュ環境に登録されているユーザーおよびユーザーグループ（メンバー）の作成や管理と、信頼されているコミュニティメンバーへの役割の割り当て、学習者へのコンテンツの割り当てを実行できます。

詳しくは、[ユーザーとユーザーグループの管理](users.md)を参照してください。

トンネルサービスを有効にする簡単な手順については、[トンネルサービス](deploy-communities.md#tunnel-service-on-author)を参照してください。

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

1. [タグ権限の設定](../../help/sites-administering/tags.md#setting-tag-permissions)
1. [タグを公開](../../help/sites-administering/tags.md#publishing-tags)

AEM Communities 入門チュートリアル用に作成したタグのサンプルパッケージ

[ファイルを入手](assets/communities_tutorialtags-10.zip)

## イネーブルメントメンバーおよびグループの作成 {#create-enablement-members-and-groups}

イネーブルメントコミュニティサイトでは、サイト訪問者が [自己登録またはソーシャルログインを使用](sites-console.md#user-management).

代わりに、 [トンネルサービス](#enable-the-tunnel-service) 有効、 [メンバーコンソール](members.md) は、パブリッシュ環境で新しいメンバーを登録するために使用されます。

このチュートリアルでは、パブリッシュ環境で 3 人のメンバーを作成します。2 人のメンバーが学習パスに割り当てられるユーザーグループのメンバーになり、3 人目のメンバーがイネーブルメントリソースの連絡先になります。

さらに、4 人目のメンバーをオーサー環境で作成し、コミュニティ管理者およびコミュニティイネーブルメントマネージャーの役割を割り当てます。

>[!NOTE]
>
>これらのメンバーは、 *イネーブルメントチュートリアル* コミュニティサイト。
>
>後で作成する場合は、イネーブルメントチュートリアルメンバーグループのメンバーを作成するときに、これらのメンバーをメンバーグループに追加できます。**
>
>または、これらのメンバーを後から[メンバーグループに割り当て](enablement-create-site.md#assignuserstocommunityenablemembersgroup)ます。

### Riley Taylor - 登録者 {#riley-taylor-enrollee}

Community Ski Class という名前の学習者グループに追加される[メンバーを作成](members.md#create-new-member)します。

* **ID**:ライリー
* **電子メール**：riley.taylor@mailinator.com
* **パスワード**：password
* **パスワードを確認**:パスワード
* **名**：Riley
* **姓**:テイラー

### Sidney Croft - 登録者 {#sidney-croft-enrollee}

「Community Ski Class」グループに追加される [2 人目のメンバーを作成](members.md#create-new-member)します。

* **ID**:シドニー
* **電子メール**：sidney.croft@mailinator.com
* **パスワード**：password
* **パスワードを確認**:パスワード
* **名**：Sidney
* **姓**:切り抜き

### Quinn Harper - イネーブルメントリソースの連絡先およびモデレーター {#quinn-harper-enablement-resource-contact-and-moderator}

[メンバーを作成](members.md#create-new-member) サイトの作成後にコミュニティサイトのメンバーグループに追加されるユーザー。 このメンバーシップにより、メンバーをイネーブルメントとして割り当てることができます [リソース連絡先](resources.md#settings) サイトのイネーブルメントリソースが作成されたとき。

* **ID**:クイン
* **電子メール**：quinn.harper@mailinator.com
* **パスワード**：password
* **パスワードを確認**:パスワード
* **名**：Quinn
* **姓**:ハーパー

### ユーザーグループを追加 - Community Ski Class {#add-a-user-group-community-ski-class}

Community Ski Class という名前の[新しいグループを追加](members.md#create-new-group)します。

* **ID**:community-ski-class
* **名前**：Community Ski Class
* **説明**:イネーブルメントリソースを割り当てるためのサンプルグループ
* **メンバーをグループに追加** &#39;追加&#39;:

   * riley
   * sidney

* 選択 **[!UICONTROL 保存]**

### Community Ski Class のプロパティ {#community-ski-class-properties}

![ski-class-properties](assets/ski-class-properties.png)

>[!NOTE]
>
>コミュニティサイトの作成中に、既存のメンバーおよびグループをコミュニティサイトのメンバーグループに追加できます。

## コミュニティ管理者の役割 {#community-administrator-role}

コミュニティ管理者グループのメンバーは、コミュニティサイトの作成、サイトの管理、メンバーの管理（コミュニティの利用を禁止可能）およびコンテンツのモデレートを実行できます。

### ユーザーを作成 {#create-user}

でのユーザーの作成 *作成者*&#x200B;コミュニティ管理者の役割が割り当てられているユーザー：

* オーサーインスタンス上

   * 例： [http://localhost:4502/](http://localhost:4503/)

* 管理者権限でログイン

   * 例えば、ユーザー名「admin」/パスワード「admin」です。

* メインコンソールから、に移動します。 **[!UICONTROL ツール]** > **[!UICONTROL 運用]** > **[!UICONTROL セキュリティ]** > **[!UICONTROL ユーザー]**.
* 次の **[!UICONTROL 編集]** メニュー、選択 **[!UICONTROL ユーザーを追加]**.

* 内 `Create New User` ダイアログの入力：

   * **ID&amp;ast;**:シリウス
   * **電子メールアドレス**：sirius.nilson@mailinator.com
   * **パスワード (&amp;A);**:パスワード
   * **パスワードの確認 (&amp;A);**:パスワード
   * **名**：Sirius
   * **姓 (&amp;A);**:ニルソン

### コミュニティ管理者グループに対する Sirius の割り当て {#assign-sirius-to-community-administrators-group}

下にスクロールして `Add User to Groups`:

* 「C」と入力して検索

   * 選択 `Community Administrators`
   * 選択 `Community Enablement Managers`

* 選択 **[!UICONTROL 保存]**

![admin-role](assets/admin-role.png)
