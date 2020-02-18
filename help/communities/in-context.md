---
title: コンテキスト内モデレート
seo-title: コンテキスト内モデレート
description: モデレートアクションを実行する方法
seo-description: モデレートアクションを実行する方法
uuid: 282a8bea-2822-4e5c-b9f4-4d9a5380d895
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ee104f6f-123b-4a6e-9031-849fc1318cc5
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# コンテキスト内モデレート {#in-context-moderation}

AEM Communities では、管理者と信頼されているコミュニティメンバーが、コミュニティコンテンツをそのコンテンツが投稿された公開済みのページ上で直接モデレートできます。

When using a [moderation console](moderation.md), the information displayed for the content includes a link to the published page to allow access to additional moderation actions available when moderating in-context.

## モデレートアクション {#moderation-actions}

Visit the moderation overview for a description of [moderation actions](moderate-ugc.md#moderation-actions).

## モデレート UI {#moderation-ui}

パブリッシュインスタンスで使用できるモデレーター用の UI は、ユーザー生成コンテンツ（UGC）を投稿および管理するためのダイアログ内にあります。UIの要素は、サイト訪問者のステータス(訪問者が

1. コンテンツを投稿したメンバー
1. 信頼できるメンバーのモデレーター
1. 管理者
1. サインイン済みですが、管理者、モデレーター、コンテンツの作成者はいません
1. サインインしていません

## 例 {#example}

以下に示すように、[AEM Communities 使用の手引き](getting-started.md)で作成した [Geometrixx Engage](http://localhost:4503/content/sites/engage/en.html) サイトを使用して、フォーラムのスレッドを素早くセットアップし、パブリッシュ環境で様々なモデレートアクティビティを体験することができます。

Aaron McDonald（aaron.mcdonald@mailinator.com）は、サイト作成時に community-engage-moderators グループに追加された、信頼されているコミュニティメンバーです。

[メンバーコンソール](members.md)を使用して、Rebekah Larsen（rebekah.larsen@trashymail.com）を community-engage-members グループのメンバーとして追加できます。

コミュニティユーザーグループについて詳しくは、[ユーザーとユーザーグループの管理](users.md)を参照してください。

### フォーラム投稿の作成 {#create-the-forum-posts}

* Rebekah Larsen（rebekah.larsen@trashymail.com）としてログインします。

   * フォーラムの選択
   * 新しい投稿の選択
   * 件名を入力

      ハミングバードフィーダーで花蜜を交換するタイミング

   * 本文を入力

      毎年ハチドリの餌をつるす時はあまり成功していません Seems they come a day or two then that is it.I change it once a week is that too long? Do I need to change it sooner?
   * 投稿の選択
   * ログアウトの選択

* Aaron McDonald（aaron.mcdonald@mailinator.com）としてログインします。

   * フォーラムの選択
   * 「Hummingbird」のトピックで、「詳細情報を読む」を選択します。
   * 「返信を投稿」に対するコメントを入力します

      私は週に1回変更し、5月から10月までそれを受け取ります。

   * 返信の選択
   * ログアウトの選択

* Andrew Schaeffer（andrew.schaeffer@trashymail.com）としてログインします。

   * フォーラムの選択
   * 「Hummingbird」のトピックで、「詳細情報を読む」を選択します。
   * 「返信を投稿」に対するコメントを入力します

      私は花蜜と飼料を販売しています。https://my.viral.url/をご覧ください。

   * 返信の選択
   * ログアウトの選択

### Anonymous Site Visitor (#5) {#anonymous-site-visitor}

以下は、サインインしていないサイト訪問者が閲覧したフォーラムのビューです(5)。

匿名のサイト訪問者にできることは、フォーラムを表示することだけです。コンテンツを投稿することも、モデレートアクションを実行することもできません。

![chlimage_1](assets/chlimage_1.png)

### New Member (#4) {#new-member}

On author, log in as admin and add Boyd Larsen (boyd.larsen@dodgit.com) as a new member of community-engage-members group using the [Members console](members.md), then Log Out.

On publish, log in as Boyd Larsen and access the thread by selecting `Forum`, and then `Read more` for the hummingbird post.

注意

* Boyd はフォーラムに参加していません。
* Boyd は何も削除することができません。
* Boyd はログインしており、返信またはコンテンツにフラグを設定できます。

Boyd としてログインした状態で「フラグ」を選択し、Andrew が投稿したコンテンツにフラグを設定します。

ログアウトします。

![chlimage_1-1](assets/chlimage_1-1.png)

### Administrator (#3) {#administrator}

管理者（管理者）としてログインし、「フォーラム」を選択してスレッドにアクセスし、投稿に関しては「詳細を読む」を選択します。

注意

* 管理者はフラグ付け、削除、編集、拒否、切り取り、閉じる、ピン、機能を実行できます
* 管理者は「管理」を選択してモデレートコンソールにアクセスできます。

![communityadmin-forum](assets/communityadmin-forum.png)

[モデレートコンソール](moderation.md)にアクセスするには、パブリッシュ環境で「管理」メニュー項目を選択します。

管理者には、Geometrixx Engage コミュニティサイトのコンテンツだけでなく、すべてのモデレート可能なコンテンツが表示されます。

サイドパネルには検索フィルターがあり、開閉を切り替えることができます。

ログアウトします。

![moderationconsole-publish](assets/moderationconsole-publish.png)

### Community Moderator (#2) {#community-moderator}

コミュニティのモデレーターであるAaron mcDonald(aaron.mcdonal@mailinator.com)としてログインし、「フォーラム」を選択してスレッドにアクセスし、Hummingbirdの投稿の「詳細情報を表示」をクリックします。

注意

* Aaron は自分の投稿の返信、削除、編集または拒否を実行できます。
* また Aaron はそれ以外のコンテンツのフラグ設定／許可、返信、削除、編集、拒否を実行できます。
* Aaron はフォーラムトピックを切り取り、自分がモデレートしている別のフォーラムに移動できます。
* Aaron は「管理」を選択してモデレートコンソールにアクセスできます。

![chlimage_1-2](assets/chlimage_1-2.png)

[モデレートコンソール](moderation.md)にアクセスするには、パブリッシュ環境で「管理」メニュー項目を選択します。

コミュニティモデレーターには、Geometrixx Engage コミュニティサイトのモデレート可能なコンテンツだけが表示されます。

コミュニティモデレーターは、管理者と同じオプションを使用できます（画像では検索サイドバーは閉じています）が、他の AEM コンソールにはアクセスできません。

ログアウトします。

![moderatoraccess](assets/moderatoraccess.png)

### Content Author (#1) {#content-author}

スレッドを開始したコミュニティメンバーRebeh Larsen (rebekah.larsen@mailinator.com)としてログインし、「フォーラム」を選択してスレッドにアクセスし、Hummingbirdの投稿の詳細を参照してください。

注意

* Rebekah は自分の投稿を削除または編集できます。
* また Rebekah はそれ以外のコンテンツに返信またはフラグを設定できます。
* Rebekah はモデレートコンソールにアクセスできません。

![chlimage_1-3](assets/chlimage_1-3.png)

