---
title: 公開したサイトを使ってみる
seo-title: Experience the Published Site
description: 公開したサイトの参照
seo-description: Browse to a published site
uuid: 44594e9e-27ad-475d-953d-3611b04f0df8
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: dd0cbc05-a361-46bc-b9f1-d045f8f23890
docset: aem65
exl-id: ebc4e1e7-34f0-4f4e-9f00-178dfda23ce4
source-git-commit: 840ea373537799af995c3b8ce0c8bf575752775b
workflow-type: tm+mt
source-wordcount: '1193'
ht-degree: 32%

---

# 公開したサイトを使ってみる {#experience-the-published-site}

## パブリッシュサーバー上の新しいサイトの参照 {#browse-to-new-site-on-publish}

新しく作成したコミュニティサイトが公開されたので、サイトの作成時に表示される URL を参照します。ただし、次に例を示します。

* 作成者 URL = https://localhost:4502/content/sites/engage/en.html
* 公開 URL = https://localhost:4503/content/sites/engage/en.html

どのメンバーがオーサーインスタンスにサインインし、どのメンバーがパブリッシュインスタンスにサインインしているかを混乱なく把握するために、インスタンスごとに異なるブラウザーを使用することを推奨します。

公開済みサイトに初めてアクセスするときは、通常、そのサイト訪問者はまだサインインしておらず、匿名です。

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

様々なリンクを選択すると、読み取り専用モードになります。

### JCR での匿名アクセスの防止 {#prevent-anonymous-access-on-jcr}

ただし、既知の制限により、コミュニティサイトコンテンツは jcr コンテンツと json を通じて匿名の訪問者に公開されます。 **匿名アクセスを許可** はサイトのコンテンツに対して無効です。 ただし、この動作は、Sling の制限を回避策として使用して制御できます。

jcr コンテンツと json を介した匿名ユーザーによるアクセスからコミュニティサイトのコンテンツを保護するには、次の手順に従います。

1. AEM オーサーインスタンスで、 https:// hostname:port/editor.html/content/site/sitename.htmlに移動します。

   >[!NOTE]
   >
   >ローカライズされたサイトに移動しないでください。

1. に移動します。 **ページプロパティ**.

   ![page-properties](assets/page-properties.png)

1. 「**詳細**」タブに移動します。

1. 有効にする **認証要件**.

   ![site-authentication](assets/site-authentication.png)

1. ログインページのパスを追加します。 例： **/content/......./GetStarted**.
1. ページを公開します。

## 信頼されているコミュニティメンバー {#trusted-community-member}

この操作は、次を前提としています。 [Aaron McDonald](/help/communities/tutorials.md#demo-users) は次の役割を割り当てられました： [コミュニティマネージャーとモデレーター](/help/communities/create-site.md#roles). そうでない場合は、オーサー環境に戻ります。 [サイト設定の変更](/help/communities/sites-console.md#modifying-site-properties) コミュニティマネージャーとモデレーターの両方として Aaron McDonald を選択します。

右上隅で、「 `Log in`をクリックし、ユーザー名 (aaron.mcdonald@mailinator.com) とパスワード (password) を使用して署名します。 twitterまたはFacebookの資格情報を使用してログインする機能に注目してください。

![ログイン](assets/login.png)

登録済みのコミュニティメンバーとしてサインインしたら、次のメニュー項目に注目して、コミュニティサイトをクリックして参照してください。

* **プロファイル** オプションを使用すると、プロファイルを表示および編集できます。
* [メッセージ](/help/communities/configure-messaging.md) 「 」オプションを使用すると、ダイレクトメッセージの節に移動し、次の操作をおこなうことができます。

   1. 受信したダイレクトメッセージ（インボックス）、送信したダイレクトメッセージ（送信済みアイテム）、削除した（ごみ箱）を表示します。
   1. 個人およびグループに送信する新しいダイレクトメッセージを作成します。

* [通知](/help/communities/notifications.md) オプションを選択すると、通知セクションに移動します。このセクションでは、関心のあるイベントを表示したり、通知設定を編集したりできます。
* [管理](/help/communities/published-site.md#moderationlink) モデレート権限を持っている場合は、AEM Communitiesのモデレートページに移動します。

![adminscreen](assets/adminscreen.png)

カレンダーページがホームページになっていますが、これは、選択した参照サイトテンプレートの最初に含まれているのがカレンダー機能で、その後にアクティビティストリーム機能、フォーラム機能などが続いているからです。この構造は、 [サイトテンプレート](/help/communities/sites.md#edit-site-template) コンソールまたはオーサー環境でサイトプロパティを変更する場合：

![sitetemplate](assets/sitetemplate.png)

>[!NOTE]
>
>コミュニティのコンポーネントと機能について詳しくは、次を参照してください。
>
>* [コミュニティコンポーネント](/help/communities/author-communities.md)（作成者向け）
>* [コンポーネントおよび機能の基本事項](/help/communities/essentials.md)（開発者向け）


### フォーラムリンク {#forum-link}

フォーラムリンクを選択すると、基本的なフォーラム機能が表示されます。

メンバーは、新しいトピックを投稿したり、トピックをフォローしたりできます。

サイト訪問者は、様々な方法で投稿を表示したり、並べ替えたりできます。

![formlink](assets/forumlink.png)

### グループリンク {#groups-link}

Aaron はグループ管理者なので、グループリンクを選択すると、新しいグループを作成するための画面が表示されます。ここで、グループテンプレートや画像を選択したり、グループをオープンにするかシークレットにするかを設定したり、メンバーを招待したりできます。

パブリッシュ環境でグループを作成する例を次に示します。

グループは、オーサー環境で作成し、オーサー環境のコミュニティサイト内で管理することもできます ([コミュニティグループコンソール](/help/communities/groups.md)) をクリックします。 の経験 [オーサー環境でのグループの作成](/help/communities/nested-groups.md) は、このチュートリアルの次の段階です。

![grouplink](assets/grouplink.png)

参照グループの作成：

1. 選択 **新しいグループ**
1. **「設定」タブ**

   * Group Name : `Sports`
   * 説明 : `A parent group for various sporting groups`.
   * グループ URL 名 : `sports`
   * 選択 `Open Group` （コミュニティメンバーが参加することを許可）

1. **「テンプレート」タブ**

   * 選択 `Reference Group` （構造内にグループ機能を含み、ネストされたグループを許可します）

1. 選択 **グループを作成**

   ![creategroup](assets/creategroup.png)

新しいグループが作成されたら、その中に（ネストされる）2 つのグループを作成するために&#x200B;**新しい Sports グループを選択**&#x200B;します。サイト構造は、グループ機能で始めることができないので、Sports グループを開いた後、「グループ」リンクを選択する必要があります。

![grouplink1](assets/grouplink1.png)

2 番目のリンクセット ( `Blog`( 現在選択されているグループに属し、 `Sports` グループ化します。 「スポーツ」 `Groups` リンクを使用すると、Sports グループ内に 2 つのグループをネストできます。

例えば、 `new groups`.

* 次の名前の 1 つ： `Baseball`

   * 設定を `Open Group` （必須のメンバーシップ）。
   * 「テンプレート」タブで、「 `Conversational Group`.

* 次の名前の 1 つ： `Gymnastics`

   * 設定をに変更します。 `Member Only Group` （メンバーシップの制限）。
   * 「テンプレート」タブで、「 `Conversational Group`.

**注意**：

* 両方のグループが表示される前に、ページの更新が必要になる場合があります。
* このテンプレートでは、 *not* にグループ機能を含めるので、これ以上グループをネストすることはできません。
* 作成者の場合、 [グループコンソール](/help/communities/groups.md) は 3 つ目の選択肢を提供します。 `Public Group` （オプションのメンバーシップ）。

両方のグループが作成されたら、Baseball グループ（オープングループ）を選択し、そのリンクに注目します。

`Discussions` `What's New` `Members`

このグループのリンクは、メインサイトのリンクの下に表示され、結果として、次のように表示されます。

![grouplink2](assets/grouplink2.png)

オーサー環境で、管理者権限を持つユーザーが [コミュニティグループコンソール](/help/communities/members.md) をクリックし、Weston McCall を `Community Engage Gymnastics <uid> Members` グループ化します。

引き続きパブリッシュ環境で、Aaron McDonald としてログアウトし、次のように匿名のサイト訪問者として Sports グループ内のグループを表示します。

* ホームページから
* 選択 `Groups` リンク
* 選択 `Sports` リンク
* スポーツを選択&#39; `Groups` リンク

Baseball グループのみが表示されます。

Weston McCall（weston.mccall@dodgit.com／password）としてログインし、同じ場所に移動します。Weston が `Join` 開場 `Baseball` グループ化し、次のいずれかを選択します。 `enter or Leave` 私人 `Gymnastics` グループ化します。

![grouplink3](assets/grouplink3.png)

### Web ページリンク {#web-page-link}

Web ページリンクを選択すると、サイトに含まれる基本的な Web ページが表示されます。標準のAEMオーサリングツールを使用して、オーサー環境でこのページにコンテンツを追加できます。

例えば、次に移動します。 **作成者** インスタンス、 `engage` フォルダーを [コミュニティサイトコンソール](/help/communities/sites-console.md)を選択し、 **サイトを開く** アイコンをクリックしてオーサリング編集モードに入ります。 次に、プレビューモードを選択して、 `Web Page` リンクをクリックし、「編集モード」を選択して、タイトルコンポーネントとテキストコンポーネントを追加します。 最後に、ページのみ、またはサイト全体を再公開します。

![webpagelink](assets/webpagelink.png)

### モデレートリンク {#moderationlink}

コミュニティメンバーがモデレート権限を持っている場合は、モデレートリンクが表示され、選択すると、投稿されたコミュニティコンテンツが表示され、コミュニティのコンテンツを使用できるようになります [モデレート済み](/help/communities/moderate-ugc.md) ～に似た方法で [モデレートコンソール](/help/communities/moderation.md) （オーサー環境で）

ブラウザーの戻るボタンを使用して、公開したサイトに戻ります。ほとんどのコンソールは、パブリッシュ環境のグローバルナビゲーションからはアクセスできません。

![moderationlink](assets/moderationlink.png)

## 自己登録 {#self-registration}

ログアウトした後に、新しいユーザー登録を作成できます。

* 選択 `Log In`
* 選択 `Sign up for a new account`

![登録](assets/registration.png)

![登録](assets/signup.png)

デフォルトでは、電子メールアドレスがログイン ID になります。オフにすると、訪問者は独自のログイン ID（ユーザー名）を入力できます。 ユーザー名は、パブリッシュ環境で一意である必要があります。

ユーザーの名前、電子メールおよびパスワードを指定した後、「 」を選択します。 `Sign Up` ユーザーを作成し、署名を有効にします。

サインインすると、最初に表示されるページが `Profile` ページに貼り付けることができます。

![プロファイル](assets/profile.png)

メンバーが自分のログイン ID を忘れた場合は、電子メールアドレスを使用して回復することができます。

![forgotusername](assets/forgotusername.png)
