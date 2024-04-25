---
title: コンテキスト内モデレート
description: 管理者と信頼されたコミュニティメンバーがAdobe Experience Manager Communities でモデレーターアクションを実行する方法について説明します。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 47b3c19c-5228-4b72-b78c-7ed71b308921
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 0%

---

# コンテキスト内モデレート {#in-context-moderation}

AEM Communitiesの場合、コミュニティコンテンツが投稿された公開済みページで、管理者や信頼されたコミュニティメンバーが直接モデレートを行うことができます。

を使用する場合 [モデレートコンソール](moderation.md)を選択すると、コンテンツに対して表示される情報には、コンテキスト内でモデレートを行う際に使用できる追加のモデレートアクションにアクセスできるようにするための、公開済みページへのリンクが含まれます。

## モデレートアクション {#moderation-actions}

の説明については、モデレートの概要を参照してください。 [モデレートアクション](moderate-ugc.md#moderation-actions).

## モデレート UI {#moderation-ui}

パブリッシュインスタンスでモデレーターに表示される UI は、ユーザー生成コンテンツ（UGC）を投稿および管理するためのダイアログ内に格納されています。 UI の要素は、サイト訪問者のステータスによって決定されます。つまり、次のいずれかになります。

1. コンテンツを投稿したメンバー。
1. 信頼できるメンバーモデレーター。
1. 管理者。
1. ログインしたが、コンテンツの管理者、モデレーター、作成者ではない。
1. ログインしていません。

## 例 {#example}

使用， [Geometrixxエンゲージ](http://localhost:4503/content/sites/engage/en.html) 作成日時 [AEM Communitiesの概要](getting-started.md)を使用すると、パブリッシュ環境の様々なモデレーションアクティビティを体験できるフォーラムにスレッドを設定できます。 以下を参照してください。

Aaron McDonald （`aaron.mcdonald@mailinator.com`）は、サイトの作成時に community-engage-moderators グループに追加したことにより、信頼できるコミュニティメンバーとして識別されました。

レベッカ・ラルセン （`rebekah.larsen@trashymail.com`）は、 [メンバーコンソール](members.md).

コミュニティユーザーグループについて詳しくは、次を参照してください： [ユーザーとユーザーグループの管理](users.md).

### フォーラムの投稿の作成 {#create-the-forum-posts}

* Rebekah Larsen としてログインします（rebekah.larsen@trashymail.com）。

   * フォーラムを選択
   * 新しい投稿を選択
   * 件名を入力

     ハミング鳥フィーダーで蜜を変える場合

   * 本文を入力

     毎年ハチドリのフィーダーをハングアップする時はあまり成功していませんでした。 1 日か 2 日か来たそうだそうだそうだそうだそうだそうだそうだそうだそうだね。 週に 1 回は変えるの長すぎるの？ もっと早く変更しなければいけませんか。

   * 投稿を選択
   * 「ログアウト」を選択します

* Aaron McDonald （aaron.mcdonald@mailinator.com）としてログインする

   * フォーラムを選択
   * 「Hummingbird」トピックについては、「詳細を表示」を選択します
   * Post Reply のコメントを入力します

     私は週に 1 回私のものを変え、私は 5 月から 10 月まで彼らを得ます。

   * 返信を選択
   * 「ログアウト」を選択します

* Andrew Schaeffer （andrew.schaeffer@trashymail.com）としてログインします。

   * フォーラムを選択
   * 「Hummingbird」トピックについては、「詳細を表示」を選択します
   * Post Reply のコメントを入力します

     私は蜜とフィーダーを売っています – visit https://my.viral.url/

   * 返信を選択
   * 「ログアウト」を選択します

### 匿名サイト訪問者（#5） {#anonymous-site-visitor}

以下は、ログインしていないサイト訪問者が閲覧したフォーラムのビューです（5）。

匿名サイト訪問者はフォーラムの閲覧のみが可能ですが、コンテンツの投稿やモデレーションアクションは行えません。

![community-forum-visit](assets/community-forum-visitor.png)

### 新規メンバー（#4） {#new-member}

オーサー環境で管理者としてログインし、Boyd Larsen （boyd.larsen@dodgit.com）を community-engage-members グループの新しいメンバーとして追加するには、 [メンバーコンソール](members.md)ログアウトします。

公開時に Boyd Larsen としてログインし、を選択してスレッドにアクセスします。 `Forum`、次に `Read more` ハチドリのポストのために。

注意：

* ボイドはフォーラムに参加していません。
* ボイドは何も削除できません。
* ボイドはログインし、コンテンツに返信したりフラグを立てたりできます。

Boid に Andrew が投稿した内容を示すフラグを選択してもらいます。

ログアウト

![community-forum-member](assets/community-forum-member.png)

### 管理者（#3） {#administrator}

管理者（管理者）としてログインし、「フォーラム」を選択してスレッドにアクセスし、投稿で「詳細を読む」を選択します。

注意：

* 管理者は、フラグの設定、削除、編集、拒否、切り取り、閉じる、ピン留め、機能を実行できます。
* 管理者は、「管理」を選択してモデレートコンソールにアクセスできます。

![コミュニティ管理者フォーラム](assets/community-admin-forum.png)

「管理」メニュー項目を選択して、 [モデレートコンソール](moderation.md) パブリッシュ環境から変更します。

管理者には、Geometrixxエンゲージメントコミュニティサイトのコンテンツだけでなく、すべてのモデレート可能なコンテンツが表示されることに注意してください。

検索フィルターは、開く/閉じるを切り替えるサイドパネルです。

ログアウトします。

![moderation-console-publish](assets/moderation-console-publish.png)

### コミュニティ モデレーター（#2） {#community-moderator}

Aaron McDonald としてログインする（`aaron.mcdonal@mailinator.com`）を選択し、「フォーラム」を選択してスレッドにアクセスします。ハチドリの投稿の「詳細を読む」を選択します。

注意：

* Aaron は自分の投稿を返信、削除、編集または拒否できます。
* Aaron は、フラグ設定/許可、返信、削除、編集、その他のコンテンツの拒否も行うことができます。
* Aaron は、フォーラムのトピックを切り取って、モデレートする別のフォーラムに移動できます。
* Aaron は「管理」を選択してモデレートコンソールにアクセスできます。

![community-forum-moderator](assets/community-forum-moderator.png)

「管理」メニュー項目を選択して、 [モデレートコンソール](moderation.md) パブリッシュ環境から変更します。

コミュニティモデレーターの場合、Geometrixxエンゲージメント コミュニティサイトのモデレート可能なコンテンツのみが表示されます。

コミュニティモデレーターは管理者と同じオプションを持ちますが（画像は検索サイドバーを閉じるに切り替えられています）、他のAEM コンソールにはアクセスできません。

ログアウトします。

![モデレータのアクセス](assets/moderator-access.png)

### コンテンツ作成者（#1） {#content-author}

Rebekah Larsen としてログインする（`rebekah.larsen@mailinator.com`）を選択してスレッドにアクセスします。ハチドリの投稿の「詳細情報」を選択します。

注意：

* Rebekah は自分の投稿を削除または編集できます。
* Rebekah は、他のコンテンツに返信したり、フラグを立てたりすることもできます。
* Rebekah はモデレーションコンソールにアクセスできません。

![community-forum-author](assets/community-forum-author.png)
