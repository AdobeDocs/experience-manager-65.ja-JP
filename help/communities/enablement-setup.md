---
title: イネーブルメントのための初期設定
seo-title: 初期設定
description: イネーブルメントのための初期設定
seo-description: イネーブルメントのための初期設定
uuid: 873ec41d-c088-41d9-a535-de5300661de6
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: f2ac3d66-cc79-498f-83fb-dd96feb88de2
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '866'
ht-degree: 52%

---


# イネーブルメントのための初期設定   {#initial-setup-for-enablement}

## オーサーインスタンスおよびパブリッシュインスタンスの開始 {#start-author-and-publish-instances}

開発用およびデモ用の場合、1 つのオーサーインスタンスと 1 つのパブリッシュインスタンスを実行する必要があります。

基本的なAEM [はじめに](../../help/sites-deploying/deploy.md#getting-started)の指示に従い、

* [localhost:4502](http://localhost:4502/)の作成者環境
* [localhost:4503](http://localhost:4503/)の公開環境

AEM Communities では、各環境を次の目的で使用します。

* 作成者環境は次の目的で使用します。

   * サイト、テンプレート、コンポーネント、イネーブルメントリソース、ラーニングパスの開発。
   * 有効化リソースと学習パスへのメンバーとメンバーのグループの割り当て。
   * 割り当て、表示および投稿に関するレポートを生成します。
   * 管理タスクと設定環境。

* 公開環境は次の目的で使用します。

   * イネーブルメントマネージャが管理するトピックに基づく学習/トレーニング
   * コメント化と評価の有効化リソースと学習パス
   * リソースの連絡先と連絡を取る。

>[!NOTE]
>
>AEM に馴染みがない場合は、[基本操作](../../help/sites-authoring/basic-handling.md)に関するドキュメントおよび[ページのオーサリングのクイックガイド](../../help/sites-authoring/qg-page-authoring.md)を参照してください。

## Communities の最新リリースのインストール {#install-latest-communities-release}

このチュートリアルでは、[イネーブルメントコミュニティサイト](overview.md#enablement-community)を作成します。最新の機能パックがインストールされていることを確認するには、次のページにアクセスします。

* [最新リリース](deploy-communities.md#latest-releases)

[エンゲージメントコミュニティサイト](overview.md#engagement-community)の作成に関するチュートリアルについては、[AEM Communities 使用の手引き](getting-started.md)を参照してください。

## イネーブルメント機能の設定  {#configure-enablement-features}

このチュートリアルに従って操作するには、[イネーブルメントをインストールして設定](enablement.md)する必要があります。これには、MySQL や FFmpeg などのサードパーティの商品が必要です。

## Analytics の設定  {#configure-analytics}

[Adobe Analyticsがコミュニティサイト](analytics.md)に対して設定されると、コミュニティメンバー（学習者）に割り当てられたイネーブルメントリソースと学習パスに関して生成された[レポート](reports.md)で、より多くの情報が得られます。

## 電子メール通知の設定 {#configure-email-for-notifications}

通知機能は、デフォルトで`Communities Sites`コンソールを使用して作成されたすべてのサイトで使用でき、通知の電子メールチャネルを提供します。

これを使用するには、電子メールをサイト用に適切に設定する必要があります。

[電子メールの設定](email.md)を参照してください。

## トンネルサービスの有効化  {#enable-the-tunnel-service}

オーサー環境でコミュニティサイトを作成するときに、トンネルサービスを使用すると、パブリッシュ環境に登録されているユーザーおよびユーザーグループ（メンバー）の作成や管理と、信頼されているコミュニティメンバーへの役割の割り当て、学習者へのコンテンツの割り当てを実行できます。

詳しくは、[ユーザーとユーザーグループの管理](users.md)を参照してください。

トンネルサービスを有効にする簡単な手順については、[トンネルサービス](deploy-communities.md#tunnel-service-on-author)を参照してください。

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

次の手順に従います。

1. [タグ権限の設定](../../help/sites-administering/tags.md#setting-tag-permissions)
1. [タグを公開する](../../help/sites-administering/tags.md#publishing-tags)

AEM Communities 入門チュートリアル用に作成したタグのサンプルパッケージ

[ファイルを入手](assets/communities_tutorialtags-10.zip)

## イネーブルメントメンバーおよびグループの作成 {#create-enablement-members-and-groups}

有効化コミュニティサイトの場合、サイト訪問者は自己登録を行ったり、ソーシャルログイン](sites-console.md#user-management)を使用したりできません。[

代わりに、[トンネルサービス](#enable-the-tunnel-service)が有効な場合は、[メンバーコンソール](members.md)を使用して、新しいメンバーを発行環境に登録します。

このチュートリアルでは、パブリッシュ環境で 3 人のメンバーを作成します。2人のメンバーが学習パスに割り当てられたユーザーグループのメンバーになり、3人目のメンバーはイネーブルメントリソースの連絡先になります。

さらに、4 人目のメンバーをオーサー環境で作成し、コミュニティ管理者およびコミュニティイネーブルメントマネージャーの役割を割り当てます。

>[!NOTE]
>
>これらのメンバは、*有効化チュートリアル*&#x200B;コミュニティサイトの作成前に作成されています。
>
>後で作成する場合は、イネーブルメントチュートリアルメンバーグループのメンバーを作成するときに、これらのメンバーをメンバーグループに追加できます。**
>
>または、これらのメンバーを後から[メンバーグループに割り当て](enablement-create-site.md#assignuserstocommunityenablemembersgroup)ます。

### Riley Taylor - 登録者  {#riley-taylor-enrollee}

Community Ski Class という名前の学習者グループに追加される[メンバーを作成](members.md#create-new-member)します。

* **ID**:ライリー
* **電子メール**：riley.taylor@mailinator.com
* **パスワード**：password
* **パスワードの確認**:password
* **名**：Riley
* **姓**:テイラー

### Sidney Croft - 登録者 {#sidney-croft-enrollee}

「Community Ski Class」グループに追加される [2 人目のメンバーを作成](members.md#create-new-member)します。

* **ID**:シドニー
* **電子メール**：sidney.croft@mailinator.com
* **パスワード**：password
* **パスワードの確認**:password
* **名**：Sidney
* **姓**:クロフト

### Quinn Harper - イネーブルメントリソースの連絡先およびモデレーター {#quinn-harper-enablement-resource-contact-and-moderator}

[サイトの作成後にコミュニティサイトのメンバーグループに追加される](members.md#create-new-member) メンバーを作成します。このメンバーシップは、サイトの有効化リソースが作成されたときに、メンバーを有効化[リソース連絡先](resources.md#settings)として割り当てることを許可します。

* **ID**:クイン
* **電子メール**：quinn.harper@mailinator.com
* **パスワード**：password
* **パスワードの確認**:password
* **名**：Quinn
* **姓**:ハーパー

### ユーザーグループを追加 - Community Ski Class {#add-a-user-group-community-ski-class}

Community Ski Class という名前の[新しいグループを追加](members.md#create-new-group)します。

* **ID**:コミュニティスキー教室
* **名前**：Community Ski Class
* **説明**:有効化リソースを割り当てるためのサンプルグループ
* **Members To Group** &#39;add&#39;追加:

   * riley
   * sidney

* **[!UICONTROL 保存]**&#x200B;を選択

### Community Ski Class のプロパティ {#community-ski-class-properties}

![スキークラスの特性](assets/ski-class-properties.png)

>[!NOTE]
>
>コミュニティサイトの作成中に、既存のメンバーおよびグループをコミュニティサイトのメンバーグループに追加できます。

## コミュニティ管理者の役割 {#community-administrator-role}

コミュニティ管理者グループのメンバーは、コミュニティサイトの作成、サイトの管理、メンバーの管理（コミュニティの利用を禁止可能）およびコンテンツのモデレートを実行できます。

### ユーザーを作成  {#create-user}

*author*&#x200B;にユーザーを作成し、コミュニティ管理者の役割を割り当てます。

* 作成者インスタンス

   * 例：[http://localhost:4502/](http://localhost:4503/)

* 管理者権限でサインインする

   * 例：ユーザー名「admin」/パスワード「admin」

* メインコンソールから、**[!UICONTROL ツール]**/**[!UICONTROL 操作]**/**[!UICONTROL セキュリティ]**/**[!UICONTROL ユーザー]**&#x200B;に移動します。
* **[!UICONTROL 編集]**&#x200B;メニューで、「**[!UICONTROL 追加ユーザー]**」を選択します。

* `Create New User`ダイアログで、次のように入力します。

   * **IDast(&amp;A);**:シリウス
   * **電子メールアドレス**：sirius.nilson@mailinator.com
   * **パスワード(&amp;A);**:password
   * **パスワードの確認(&amp;A);**:password
   * **名**：Sirius
   * **姓(&amp;A);**:ニルソン

### コミュニティ管理者グループに対する Sirius の割り当て {#assign-sirius-to-community-administrators-group}

`Add User to Groups`まで下にスクロールします。

* &#39;C&#39;を入力して検索してください

   *  `Community Administrators`
   *  `Community Enablement Managers`

* **[!UICONTROL 保存]**&#x200B;を選択

![管理者ロール](assets/admin-role.png)

