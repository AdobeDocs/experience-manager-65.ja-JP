---
title: 公開したサイトを使ってみる
description: サイトの作成時に、パブリッシュサーバー上で表示される URL を参照する方法について説明します。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: ebc4e1e7-34f0-4f4e-9f00-178dfda23ce4
source-git-commit: f03d0ab9d0f491441378e16e1590d33651f064b5
workflow-type: tm+mt
source-wordcount: '1205'
ht-degree: 2%

---

# 公開したサイトを使ってみる {#experience-the-published-site}

## 公開で新しいサイトを参照 {#browse-to-new-site-on-publish}

新しく作成したコミュニティサイトが公開されたので、サイトの作成時に表示される URL を参照します。ただし、次に例を示します。

* 作成者 URL = https://localhost:4502/content/sites/engage/en.html
* 公開 URL = https://localhost:4503/content/sites/engage/en.html

オーサーとパブリッシュでどのメンバーがサインインしているかに関する混乱を最小限に抑えるために、インスタンスごとに異なるブラウザーを使用することをお勧めします。

公開されたサイトに初めてアクセスした場合、通常、サイト訪問者は既にサインインしておらず、匿名になります。

`https://localhost:4503/content/sites/engage/en.html {#http-localhost-content-sites-engage-en-html}`

![authorpublished](assets/authorpublished.png)

## 匿名のサイト訪問者 {#anonymous-site-visitor}

匿名のサイト訪問者の UI には、次の情報が表示されます。

* サイトのタイトル（入門チュートリアル）
* プロファイルリンクなし
* メッセージリンクがありません
* 通知リンクがありません
* 検索フィールド
* ログインリンク
* ブランドバナー
* 参照サイトテンプレートに含まれるコンポーネントのメニューリンク。

様々なリンクを選択した場合は、読み取り専用モードになっています。

### JCR での匿名アクセスの防止 {#prevent-anonymous-access-on-jcr}

ただし、既知の制限により、コミュニティサイトコンテンツは jcr コンテンツと json を通じて匿名の訪問者に公開されます。 **匿名アクセスを許可** はサイトのコンテンツに対して無効です。 ただし、この動作は、Sling の制限を回避策として使用して制御できます。

jcr コンテンツと json を介した匿名ユーザーによるアクセスからコミュニティサイトのコンテンツを保護するには、次の手順に従います。

1. AEMオーサーインスタンスで、 https:// hostname:port/editor.html/content/site/sitename.htmlに移動します。

   >[!NOTE]
   >
   >ローカライズされたサイトに移動しないでください。

1. に移動します。 **ページのプロパティ**.

   ![page-properties](assets/page-properties.png)

1. 「**詳細**」タブに移動します。

1. 有効にする **認証要件**.

   ![site-authentication](assets/site-authentication.png)

1. ログインページのパスを追加します。 例： **/content/......./GetStarted**.
1. ページを公開します。

## 信頼できるコミュニティメンバー {#trusted-community-member}

この操作は、次を前提としています。 [Aaron McDonald](/help/communities/tutorials.md#demo-users) は次の役割を割り当てられました： [コミュニティマネージャーとモデレーター](/help/communities/create-site.md#roles). そうでない場合は、次の場所にオーサー環境に戻ります。 [サイト設定を変更する](/help/communities/sites-console.md#modifying-site-properties) コミュニティマネージャーとモデレーターの両方として Aaron McDonald を選択します。

右上隅で、「 `Log in`をクリックし、ユーザー名 (aaron.mcdonald@mailinator.com) とパスワード (password) を使用して署名します。 twitterまたはFacebookの資格情報を使用してログインする機能に注目してください。

![ログイン](assets/login.png)

登録済みのコミュニティメンバーとしてサインインしたら、次のメニュー項目に注目して、コミュニティサイトをクリックして参照してください。

* **プロファイル** 「 」オプションを使用すると、プロファイルを表示および編集できます。
* [メッセージ](/help/communities/configure-messaging.md) 「 」オプションを選択すると、ダイレクトメッセージのセクションに移動します。このセクションでは、次の操作を実行できます。

   1. 受信したダイレクトメッセージ（インボックス）、送信したダイレクトメッセージ（送信済みアイテム）および削除した（ごみ箱）を表示します。
   1. 新しいダイレクトメッセージを作成して、個人やグループに送信できるようにします。

* [通知](/help/communities/notifications.md) オプションを選択すると、通知セクションに移動します。このセクションでは、関心のあるイベントを表示したり、通知設定を編集したりできます。
* [管理](/help/communities/published-site.md#moderationlink) モデレート権限を持っている場合は、AEM Communitiesのモデレートページに移動します。

![adminscreen](assets/adminscreen.png)

選択したリファレンスサイトテンプレートには、最初にカレンダー機能が含まれ、次にアクティビティストリーム機能、フォーラム機能などが含まれていたので、カレンダーページはホームページになっています。 この構造は、 [サイトテンプレート](/help/communities/sites.md#edit-site-template) コンソールまたはオーサー環境でサイトプロパティを変更する場合：

![sitetemplate](assets/sitetemplate.png)

>[!NOTE]
>
>コミュニティのコンポーネントと機能について詳しくは、次を参照してください。
>
>* [コミュニティコンポーネント](/help/communities/author-communities.md) （作成者向け）
>* [コンポーネント、機能、機能の基本事項](/help/communities/essentials.md) （開発者向け）

### フォーラムリンク {#forum-link}

「フォーラム」リンクを選択して、基本的なフォーラム機能を表示します。

メンバーは、新しいトピックを投稿したり、トピックをフォローしたりできます。

サイトの訪問者は、投稿を表示し、様々な方法で並べ替えることができます。

![forumlink](assets/forumlink.png)

### グループリンク {#groups-link}

Aaron はグループ管理者なので、「グループ」リンクを選択すると、グループテンプレート、画像、グループが開いているか秘密鍵であるかを選択し、メンバーを招待することで、コミュニティグループを作成できます。

これは、パブリッシュ環境でグループを作成する例です。

グループは、オーサー環境で作成し、オーサー環境のコミュニティサイト内で管理することもできます ([コミュニティグループコンソール](/help/communities/groups.md)) をクリックします。 の経験 [オーサー環境でのグループの作成](/help/communities/nested-groups.md) は、このチュートリアルの次の段階です。

![grouplink](assets/grouplink.png)

参照グループを作成します。

1. 選択 **新しいグループ**
1. **「設定」タブ**

   * グループ名 : `Sports`
   * 説明 : `A parent group for various sporting groups`.
   * グループ URL 名 : `sports`
   * 選択 `Open Group` （コミュニティメンバーが参加することを許可）

1. **「テンプレート」タブ**

   * 選択 `Reference Group` （構造内にグループ機能を含み、ネストされたグループを許可します）。

1. 選択 **グループを作成**

   ![creategroup](assets/creategroup.png)

新しいグループが作成された後、 **新しいスポーツグループを選択します。** を使用して、2 つのグループ（ネスト）を作成します。 サイト構造はグループ機能で始めることができないので、 Sports グループを開いた後、「グループ」リンクを選択する必要があります。

![grouplink1](assets/grouplink1.png)

2 番目のリンクセット ( `Blog`( 現在選択されているグループに属し、 `Sports` グループ化します。 「スポーツ」 `Groups` リンクを使用すると、Sports グループ内に 2 つのグループをネストできます。

例えば、 `new groups`.

* 次の名前の 1 つ： `Baseball`

   * 設定を「 `Open Group` （必須のメンバーシップ）。
   * 「テンプレート」タブで、「 `Conversational Group`.

* 次の名前の 1 つ： `Gymnastics`

   * 設定をに変更します。 `Member Only Group` （メンバーシップの制限）。
   * 「テンプレート」タブで、「 `Conversational Group`.

**注意**:

* 両方のグループが表示される前に、ページの更新が必要になる場合があります。
* このテンプレートでは、 *not* にグループ機能を含めるので、グループをこれ以上ネストすることはできません。
* 作成者の場合、 [グループコンソール](/help/communities/groups.md) は 3 つ目の選択肢を提供します。a `Public Group` （オプションのメンバーシップ）。

両方のグループを作成したら、Baseball グループ（開いているグループ）を選択し、リンクに注目します。

`Discussions` `What's New` `Members`

グループのリンクはメインサイトのリンクの下に表示され、結果として次のように表示されます。

![grouplink2](assets/grouplink2.png)

オーサー環境で、管理者権限を持つユーザーが [コミュニティグループコンソール](/help/communities/members.md) をクリックし、Weston McCall を `Community Engage Gymnastics <uid> Members` グループ化します。

公開後、Aaron McDonald としてログアウトし、Sports Group 内のグループを匿名のサイト訪問者として表示します。

* ホームページから
* 選択 `Groups` リンク
* 選択 `Sports` リンク
* スポーツを選択&#39; `Groups` リンク

Baseball グループのみが表示されます。

Weston McCall(weston.mccall@dodgit.com / password) としてログインし、同じ場所に移動します。 Weston が `Join` 開場所 `Baseball` グループ化し、次のいずれかを選択します。 `enter or Leave` 私人 `Gymnastics` グループ化します。

![grouplink3](assets/grouplink3.png)

### Web ページリンク {#web-page-link}

「Web ページ」リンクを選択して、サイトに含まれる基本 Web ページを表示します。 標準のAEMオーサリングツールを使用して、オーサー環境でこのページにコンテンツを追加できます。

例えば、次に移動します。 **作成者** インスタンス、 `engage` フォルダーを [コミュニティサイトコンソール](/help/communities/sites-console.md)を選択し、 **サイトを開く** アイコンをクリックしてオーサリング編集モードに入ります。 次に、プレビューモードを選択して、 `Web Page` リンクをクリックし、「編集モード」を選択して、タイトルコンポーネントとテキストコンポーネントを追加します。 最後に、ページのみ、またはサイト全体を再公開します。

![webpagelink](assets/webpagelink.png)

### モデレートリンク {#moderationlink}

コミュニティメンバーにモデレート権限がある場合は、「モデレート」リンクが表示されます。 リンクを選択すると、投稿されたコミュニティのコンテンツが表示され、コンテンツを [モデレート済み](/help/communities/moderate-ugc.md) ～に似た方法で [モデレートコンソール](/help/communities/moderation.md) （オーサー環境で）。

ブラウザーの「戻る」ボタンを使用して、公開済みのサイトに戻ります。 ほとんどのコンソールは、パブリッシュ環境のグローバルナビゲーションからはアクセスできません。

![moderationlink](assets/moderationlink.png)

## 自己登録 {#self-registration}

ログアウト後に、ユーザー登録を作成できます。

* `Log In` を選択します。
* `Sign up for a new account` を選択します。

![登録](assets/registration.png)

![登録](assets/signup.png)

デフォルトでは、電子メールアドレスはログイン ID です。 オフにすると、訪問者は独自のログイン ID（ユーザー名）を入力できます。 ユーザー名は、パブリッシュ環境で一意である必要があります。

ユーザーの名前、電子メールおよびパスワードを指定した後、「 」を選択します。 `Sign Up` はユーザーを作成し、署名を有効にします。

ログイン後、最初に表示されるページは、 `Profile` ページに貼り付けることができます。

![プロファイル](assets/profile.png)

メンバーがログイン ID を忘れた場合は、そのメールアドレスを使用して復元できます。

![forgotusername](assets/forgotusername.png)
