---
title: コンテキスト内モデレート
seo-title: In-Context Moderation
description: モデレートアクションを実行する方法
seo-description: How to perform moderator actions
uuid: 282a8bea-2822-4e5c-b9f4-4d9a5380d895
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ee104f6f-123b-4a6e-9031-849fc1318cc5
role: Admin
exl-id: 47b3c19c-5228-4b72-b78c-7ed71b308921
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '789'
ht-degree: 44%

---

# コンテキスト内モデレート {#in-context-moderation}

AEM Communities では、管理者と信頼されているコミュニティメンバーが、コミュニティコンテンツをそのコンテンツが投稿された公開済みのページ上で直接モデレートできます。

を使用する場合 [モデレートコンソール](moderation.md)コンテンツに対して表示される情報には、コンテキスト内でモデレートする際に使用できる追加のモデレートアクションにアクセスできるように、公開済みページへのリンクが含まれます。

## モデレートアクション {#moderation-actions}

モデレートの概要で [モデレートアクション](moderate-ugc.md#moderation-actions).

## モデレート UI {#moderation-ui}

パブリッシュインスタンスで使用できるモデレーター用の UI は、ユーザー生成コンテンツ（UGC）を投稿および管理するためのダイアログ内にあります。UI の要素は、サイト訪問者のステータス ( 訪問者が

1. コンテンツを投稿したメンバー。
1. 信頼できるメンバーモデレーター。
1. 管理者。
1. サインインしていますが、管理者、モデレーター、コンテンツの作成者ではありません。
1. サインインしていません。

## 例 {#example}

以下に示すように、[AEM Communities 使用の手引き](getting-started.md)で作成した [Geometrixx Engage](http://localhost:4503/content/sites/engage/en.html) サイトを使用して、フォーラムのスレッドを素早くセットアップし、パブリッシュ環境で様々なモデレートアクティビティを体験することができます。

Aaron McDonald（aaron.mcdonald@mailinator.com）は、サイト作成時に community-engage-moderators グループに追加された、信頼されているコミュニティメンバーです。

[メンバーコンソール](members.md)を使用して、Rebekah Larsen（rebekah.larsen@trashymail.com）を community-engage-members グループのメンバーとして追加できます。

コミュニティユーザーグループについて詳しくは、[ユーザーとユーザーグループの管理](users.md)を参照してください。

### フォーラム投稿の作成 {#create-the-forum-posts}

* Rebekah Larsen（rebekah.larsen@trashymail.com）としてログインします。

   * フォーラムを選択
   * 新しい投稿を選択
   * 件名を入力

      ハミングバードフィーダーでネクターを変更するタイミング

   * 本文を入力

      毎年ハチドリの餌を吊り上げる時はあまり成功していませんでした Seems they come a day or two then that is it.I change it once a week is that too long? Do I need to change it sooner?

   * 投稿を選択
   * ログアウトを選択

* Aaron McDonald（aaron.mcdonald@mailinator.com）としてログインします。

   * フォーラムを選択
   * Hummingbird のトピックで、「詳細を表示」を選択します。
   * 返信を投稿のコメントを入力

      私は週に 1 回私のを変更し、5 月から 10 月までそれらを得る。

   * 返信を選択
   * ログアウトを選択

* Andrew Schaeffer（andrew.schaeffer@trashymail.com）としてログインします。

   * フォーラムを選択
   * Hummingbird のトピックで、「詳細を表示」を選択します。
   * 返信を投稿のコメントを入力

      私は蜜と飼料を販売しています — https://my.viral.url/にアクセスしてください

   * 返信を選択
   * ログアウトを選択

### 匿名のサイト訪問者（#5） {#anonymous-site-visitor}

以下は、サインインしていないサイト訪問者が閲覧したフォーラムのビューです (5)。

匿名のサイト訪問者にできることは、フォーラムを表示することだけです。コンテンツを投稿することも、モデレートアクションを実行することもできません。

![community-forum-visitor](assets/community-forum-visitor.png)

### 新しいメンバー（#4） {#new-member}

オーサー環境で、管理者としてログインし、Boyd Larsen(boyd.larsen@dodgit.com) を community-engage-members グループの新しいメンバーとして追加します。その際、 [メンバーコンソール](members.md)、次にログアウトします。

公開時に、Boyd Larsen としてログインし、を選択してスレッドにアクセスします。 `Forum`、 `Read more` 蜂雀の巣箱のために

注意:

* Boyd はフォーラムに参加していません。
* Boyd は何も削除できません。
* Boyd はサインインし、返信またはフラグコンテンツを実行できます。

Boyd としてログインした状態で「フラグ」を選択し、Andrew が投稿したコンテンツにフラグを設定します。

ログアウトします。

![community-forum-member](assets/community-forum-member.png)

### 管理者（#3） {#administrator}

管理者 (admin) としてログインし、「フォーラム」を選択してスレッドにアクセスし、投稿の「詳細を表示」を選択します。

注意:

* 管理者は、フラグ設定、削除、編集、拒否、切り取り、閉じる、ピン、機能を実行できます。
* 管理者は「管理」を選択してモデレートコンソールにアクセスできます。

![community-admin-forum](assets/community-admin-forum.png)

[モデレートコンソール](moderation.md)にアクセスするには、パブリッシュ環境で「管理」メニュー項目を選択します。

管理者には、Geometrixx Engage コミュニティサイトのコンテンツだけでなく、すべてのモデレート可能なコンテンツが表示されます。

サイドパネルには検索フィルターがあり、開閉を切り替えることができます。

ログアウトします。

![moderation-console-publish](assets/moderation-console-publish.png)

### コミュニティモデレーター（#2） {#community-moderator}

コミュニティモデレーターの Aaron McDonald(aaron.mcdonal@mailinator.com) としてログインし、「フォーラム」を選択してスレッドにアクセスし、Hummingbird の投稿の「詳細を表示」を選択します。

注意:

* Aaron は、自分の投稿の返信、削除、編集または拒否を実行できます。
* Aaron では、他のコンテンツにフラグ/許可、返信、削除、編集、拒否を設定することもできます。
* Aaron は、フォーラムトピックを「切り取り」して、そのトピックをモデレート対象の別のフォーラムに移動できます。
* Aaron は、「管理」を選択してモデレートコンソールにアクセスできます。

![community-forum-moderator](assets/community-forum-moderator.png)

[モデレートコンソール](moderation.md)にアクセスするには、パブリッシュ環境で「管理」メニュー項目を選択します。

コミュニティモデレーターには、Geometrixx Engage コミュニティサイトのモデレート可能なコンテンツだけが表示されます。

コミュニティモデレーターは、管理者と同じオプションを使用できます（画像では検索サイドバーは閉じています）が、他の AEM コンソールにはアクセスできません。

ログアウトします。

![moderator-access](assets/moderator-access.png)

### コンテンツ作成者（#1） {#content-author}

スレッドを開始したコミュニティメンバーである Rebekah Larsen(rebekah.larsen@mailinator.com) としてログインし、「フォーラム」を選択してスレッドにアクセスし、Hummingbird の投稿の「続きを読む」を選択します。

注意:

* Rebekah は、自分の投稿を削除または編集できます。
* Rebekah は、他のコンテンツに返信したり、他のコンテンツにフラグを設定したりすることもできます。
* Rebekah はモデレートコンソールにアクセスできません。

![community-forum-author](assets/community-forum-author.png)
