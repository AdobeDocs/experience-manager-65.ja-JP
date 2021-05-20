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
exl-id: ed494922-3e15-4778-84c1-35c8846ce980
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '866'
ht-degree: 52%

---

# イネーブルメントのための初期設定   {#initial-setup-for-enablement}

## オーサーインスタンスおよびパブリッシュインスタンスの開始 {#start-author-and-publish-instances}

開発用およびデモ用の場合、1 つのオーサーインスタンスと 1 つのパブリッシュインスタンスを実行する必要があります。

基本的なAEMの「[はじめに](../../help/sites-deploying/deploy.md#getting-started)」の手順に従います。

* [localhost:4502](http://localhost:4502/)のオーサー環境
* [localhost:4503](http://localhost:4503/)のパブリッシュ環境

AEM Communities では、各環境を次の目的で使用します。

* オーサー環境は次の用途です。

   * サイト、テンプレート、コンポーネント、イネーブルメントリソース、学習パスの開発。
   * イネーブルメントリソースと学習パスへのメンバーとメンバーのグループの割り当て。
   * 割り当て、表示および投稿に関するレポートの生成
   * 管理タスクと設定タスク

* パブリッシュ環境は、次の用途です。

   * イネーブルメントマネージャーが管理するトピックに基づく学習/トレーニング。
   * イネーブルメントリソースと学習パスにコメントを付け、評価します。
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

コミュニティサイト](analytics.md)に[Adobe Analyticsを設定すると、コミュニティメンバー（学習者）に割り当てられたイネーブルメントリソースと学習パスに関して生成される[レポート](reports.md)に、より多くの情報が表示されます。

## 電子メール通知の設定 {#configure-email-for-notifications}

`Communities Sites`コンソールを使用して作成されるすべてのサイトでデフォルトで使用できる通知機能は、通知用のEメールチャネルを提供します。

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

その後、次の手順に従います。

1. [タグ権限の設定](../../help/sites-administering/tags.md#setting-tag-permissions)
1. [タグを公開する](../../help/sites-administering/tags.md#publishing-tags)

AEM Communities 入門チュートリアル用に作成したタグのサンプルパッケージ

[ファイルを入手](assets/communities_tutorialtags-10.zip)

## イネーブルメントメンバーおよびグループの作成 {#create-enablement-members-and-groups}

イネーブルメントコミュニティサイトの場合、サイト訪問者は自己登録やソーシャルログイン](sites-console.md#user-management)の使用を行えません。[

代わりに、[トンネルサービス](#enable-the-tunnel-service)を有効にすると、[メンバーコンソール](members.md)を使用して、パブリッシュ環境に新しいメンバーを登録します。

このチュートリアルでは、パブリッシュ環境で 3 人のメンバーを作成します。2人のメンバーは学習パスに割り当てられたユーザーグループのメンバーになり、3人目のメンバーはイネーブルメントリソースの連絡先になります。

さらに、4 人目のメンバーをオーサー環境で作成し、コミュニティ管理者およびコミュニティイネーブルメントマネージャーの役割を割り当てます。

>[!NOTE]
>
>これらのメンバーは、*イネーブルメントチュートリアル*&#x200B;コミュニティサイトを作成する前に作成されています。
>
>後で作成する場合は、イネーブルメントチュートリアルメンバーグループのメンバーを作成するときに、これらのメンバーをメンバーグループに追加できます。**
>
>または、これらのメンバーを後から[メンバーグループに割り当て](enablement-create-site.md#assignuserstocommunityenablemembersgroup)ます。

### Riley Taylor - 登録者  {#riley-taylor-enrollee}

Community Ski Class という名前の学習者グループに追加される[メンバーを作成](members.md#create-new-member)します。

* **ID**:ライリー
* **電子メール**：riley.taylor@mailinator.com
* **パスワード**：password
* **パスワードの確認**:パスワード
* **名**：Riley
* **姓**:テイラー

### Sidney Croft - 登録者 {#sidney-croft-enrollee}

「Community Ski Class」グループに追加される [2 人目のメンバーを作成](members.md#create-new-member)します。

* **ID**:シドニー
* **電子メール**：sidney.croft@mailinator.com
* **パスワード**：password
* **パスワードの確認**:パスワード
* **名**：Sidney
* **姓**:クロフト

### Quinn Harper - イネーブルメントリソースの連絡先およびモデレーター {#quinn-harper-enablement-resource-contact-and-moderator}

[サイトの](members.md#create-new-member) 作成後にコミュニティサイトのメンバーグループに追加されるメンバーを作成します。このメンバーシップにより、サイトのイネーブルメントリソースが作成される際に、メンバーをイネーブルメント[リソース連絡先](resources.md#settings)として割り当てることができます。

* **ID**:クイン
* **電子メール**：quinn.harper@mailinator.com
* **パスワード**：password
* **パスワードの確認**:パスワード
* **名**：Quinn
* **姓**:ハーパー

### ユーザーグループを追加 - Community Ski Class {#add-a-user-group-community-ski-class}

Community Ski Class という名前の[新しいグループを追加](members.md#create-new-group)します。

* **ID**:community-ski-class
* **名前**：Community Ski Class
* **説明**:イネーブルメントリソースを割り当てるためのサンプルグループ
* **グループにメンバーを追加** &#39;add&#39;:

   * riley
   * sidney

* 「**[!UICONTROL 保存]**」を選択します。

### Community Ski Class のプロパティ {#community-ski-class-properties}

![ski-class-properties](assets/ski-class-properties.png)

>[!NOTE]
>
>コミュニティサイトの作成中に、既存のメンバーおよびグループをコミュニティサイトのメンバーグループに追加できます。

## コミュニティ管理者の役割 {#community-administrator-role}

コミュニティ管理者グループのメンバーは、コミュニティサイトの作成、サイトの管理、メンバーの管理（コミュニティの利用を禁止可能）およびコンテンツのモデレートを実行できます。

### ユーザーを作成 {#create-user}

*author*&#x200B;にコミュニティ管理者の役割を割り当てるユーザーを作成します。

* オーサーインスタンス上

   * 例： [http://localhost:4502/](http://localhost:4503/)

* 管理者権限でログイン

   * 例：ユーザー名「admin」/パスワード「admin」

* メインコンソールで、**[!UICONTROL ツール]** / **[!UICONTROL 操作]** / **[!UICONTROL セキュリティ]** / **[!UICONTROL ユーザー]**&#x200B;に移動します。
* **[!UICONTROL 編集]**&#x200B;メニューから、「**[!UICONTROL ユーザーを追加]**」を選択します。

* `Create New User`ダイアログで、次のように入力します。

   * **ID&amp;ast;**:シリウス
   * **電子メールアドレス**：sirius.nilson@mailinator.com
   * **パスワード(&amp;A);**:パスワード
   * **パスワードの確認(&amp;A);**:パスワード
   * **名**：Sirius
   * **姓(&amp;A);**:ニルソン

### コミュニティ管理者グループに対する Sirius の割り当て {#assign-sirius-to-community-administrators-group}

`Add User to Groups`まで下にスクロールします。

* 検索するには&#39;C&#39;と入力します

   *  `Community Administrators`
   *  `Community Enablement Managers`

* 「**[!UICONTROL 保存]**」を選択します。

![admin-role](assets/admin-role.png)
