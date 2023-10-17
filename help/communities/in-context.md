---
title: コンテキスト内モデレート
description: 管理者と信頼できるコミュニティメンバーがAdobe Experience Manager Communities でモデレーターアクションを実行する方法を説明します。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 47b3c19c-5228-4b72-b78c-7ed71b308921
source-git-commit: 0a4aca939c564720f63f055e9522e56942eaa128
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 1%

---

# コンテキスト内モデレート {#in-context-moderation}

AEM Communitiesの場合、管理者や信頼できるコミュニティメンバーは、コミュニティコンテンツが投稿された公開済みページで直接モデレートを実行できます。

を使用する場合、 [モデレートコンソール](moderation.md)コンテンツに対して表示される情報には、コンテキスト内でモデレートする際に使用できる追加のモデレートアクションにアクセスできるように、公開済みページへのリンクが含まれます。

## モデレートアクション {#moderation-actions}

モデレートの概要にアクセスして、 [モデレートアクション](moderate-ugc.md#moderation-actions).

## モデレート UI {#moderation-ui}

パブリッシュインスタンスのモデレーターに表示される UI は、ユーザー生成コンテンツ (UGC) の投稿と管理を行うためのダイアログ内に含まれています。 UI の要素は、サイト訪問者のステータス ( 訪問者が

1. コンテンツを投稿したメンバー。
1. 信頼できるメンバーモデレーターです。
1. 管理者。
1. サインインしていますが、管理者、モデレーター、コンテンツの作成者ではありません。
1. サインインしていません。

## 例 {#example}

の使用 [Geometrixxエンゲージ](http://localhost:4503/content/sites/engage/en.html) 次の場合に作成されたサイト [AEM Communitiesの概要](getting-started.md)を使用すると、フォーラムにスレッドを設定して、パブリッシュ環境で様々なモデレートアクティビティを体験することができます。 以下を参照してください。

Aaron McDonald (`aaron.mcdonald@mailinator.com`) は、サイトの作成時に community-engage-moderators グループに追加することで、信頼できるコミュニティメンバーとして識別されました。

Rebekah Larsen (`rebekah.larsen@trashymail.com`) は、 [メンバーコンソール](members.md).

コミュニティユーザーグループについて詳しくは、 [ユーザーとユーザーグループの管理](users.md).

### フォーラム投稿の作成 {#create-the-forum-posts}

* Rebekah Larsen(rebekah.larsen@trashymail.com) としてログインします。

   * フォーラムを選択
   * 新しい投稿を選択
   * 件名を入力

     ハミングバードフィーダーでネクターを変更するタイミング

   * 本文のテキストを入力

     毎年ハチドリの餌を吊り上げる時はあまり成功していませんでした 1 日か 2 日来るみたいですね。 1 週間に 1 回変えるのはそんなに長いの？ もっと早く変更しなければなりませんか？

   * 投稿を選択
   * ログアウトを選択

* Aaron McDonald(aaron.mcdonald@mailinator.com) としてログインします。

   * フォーラムを選択
   * Hummingbird のトピックで、「詳細を表示」を選択します。
   * 返信を投稿のコメントを入力

     私は週に 1 回私のを変更し、5 月から 10 月までそれらを得る。

   * 返信を選択
   * ログアウトを選択

* Andrew Schaeffer(andrew.schaeffer@trashymail.com) としてログインします。

   * フォーラムを選択
   * Hummingbird のトピックで、「詳細を表示」を選択します。
   * 返信を投稿のコメントを入力

     私は蜜と飼料を販売しています — https://my.viral.url/にアクセスしてください。

   * 返信を選択
   * ログアウトを選択

### 匿名のサイト訪問者 (#5) {#anonymous-site-visitor}

以下は、サインインしていないサイト訪問者が閲覧したフォーラムのビューです (5)。

匿名のサイト訪問者はフォーラムのみを表示できますが、コンテンツを投稿したり、モデレート操作を実行したりすることはできません。

![community-forum-visitor](assets/community-forum-visitor.png)

### 新規メンバー (#4) {#new-member}

オーサー環境で、管理者としてログインし、Boyd Larsen(boyd.larsen@dodgit.com) を community-engage-members グループの新しいメンバーとして追加します。その際、 [メンバーコンソール](members.md)、次にログアウトします。

公開時に、Boyd Larsen としてログインし、を選択してスレッドにアクセスします。 `Forum`を、 `Read more` 蜂雀の巣箱のために

注意:

* Boyd はフォーラムに参加していません。
* Boyd は何も削除できません。
* Boyd はサインインし、返信またはフラグコンテンツを実行できます。

Boyd が「フラグ」を選択し、Andrew が投稿したコンテンツにフラグを設定します。

ログアウト

![community-forum-member](assets/community-forum-member.png)

### 管理者 (#3) {#administrator}

管理者 (admin) としてログインし、「フォーラム」を選択してスレッドにアクセスし、投稿の「詳細を表示」を選択します。

注意:

* 管理者は、フラグ設定、削除、編集、拒否、切り取り、閉じる、ピン、機能を実行できます。
* 管理者は「管理」を選択してモデレートコンソールにアクセスできます。

![community-admin-forum](assets/community-admin-forum.png)

管理メニュー項目を選択して、 [モデレートコンソール](moderation.md) パブリッシュ環境から。

管理者の場合、GeometrixxEngage コミュニティサイトからのコンテンツだけでなく、モデレート可能なコンテンツもすべて表示されます。

検索フィルターは、開く/閉じるを切り替えるサイドパネルです。

ログアウト.

![moderation-console-publish](assets/moderation-console-publish.png)

### コミュニティモデレーター (#2) {#community-moderator}

Aaron McDonald (`aaron.mcdonal@mailinator.com`) をクリックし、コミュニティモデレーターを選択して、「フォーラム」を選択し、Hummingbird の投稿の「詳細を表示」を選択してスレッドにアクセスします。

注意:

* Aaron は、自分の投稿の返信、削除、編集または拒否を実行できます。
* Aaron では、他のコンテンツにフラグ/許可、返信、削除、編集、拒否を設定することもできます。
* Aaron は、フォーラムトピックを「切り取り」して、そのトピックをモデレート対象の別のフォーラムに移動できます。
* Aaron は、「管理」を選択してモデレートコンソールにアクセスできます。

![community-forum-moderator](assets/community-forum-moderator.png)

管理メニュー項目を選択して、 [モデレートコンソール](moderation.md) パブリッシュ環境から。

コミュニティモデレーターの場合、GeometrixxEngage コミュニティサイトからのモデレート可能なコンテンツのみが表示されます。

コミュニティモデレーターには、管理者と同じオプション（画像は検索サイドバーを閉じた状態で表示）がありますが、他のAEMコンソールにはアクセスできません。

ログアウト.

![moderator-access](assets/moderator-access.png)

### コンテンツ作成者 (#1) {#content-author}

Rebekah Larsen (`rebekah.larsen@mailinator.com`) をクリックし、スレッドを開始し、「フォーラム」を選択してスレッドにアクセスし、Hummingbird の投稿の「詳細を表示」を選択します。

注意:

* Rebekah は、自分の投稿を削除または編集できます。
* Rebekah は、他のコンテンツに返信したり、他のコンテンツにフラグを設定したりすることもできます。
* Rebekah はモデレートコンソールにアクセスできません。

![community-forum-author](assets/community-forum-author.png)
