---
title: 公開したサイトを使ってみる
seo-title: 公開したサイトを使ってみる
description: 公開したサイトの参照
seo-description: 公開したサイトの参照
uuid: 44594e9e-27ad-475d-953d-3611b04f0df8
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: dd0cbc05-a361-46bc-b9f1-d045f8f23890
docset: aem65
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '1202'
ht-degree: 33%

---


# 公開したサイトを使ってみる {#experience-the-published-site}

## パブリッシュサーバー上の新しいサイトの参照 {#browse-to-new-site-on-publish}

新しく作成したコミュニティサイトが公開されたので、サイトの作成時に表示されたURLを参照し、公開サーバ上に表示されます。例：

* 作成者URL = https://localhost:4502/content/sites/engage/en.html
* 発行URL = https://localhost:4503/content/sites/engage/en.html

どのメンバーがオーサーインスタンスにサインインし、どのメンバーがパブリッシュインスタンスにサインインしているかを混乱なく把握するために、インスタンスごとに異なるブラウザーを使用することを推奨します。

公開済みサイトに初めてアクセスするときは、通常、そのサイト訪問者はまだサインインしておらず、匿名です。

`https://localhost:4503/content/sites/engage/en.html {#http-localhost-content-sites-engage-en-html}`

![authorpublished](assets/authorpublished.png)

## 匿名のサイト訪問者 {#anonymous-site-visitor}

匿名サイト訪問者のUIには、次の項目が表示されます。

* サイトのタイトル（はじめにのチュートリアル）
* プロファイルリンクなし
* メッセージのリンクなし
* 通知リンクなし
* 検索フィールド
* ログインリンク
* ブランドバナー
* リファレンスサイトテンプレートに含まれるコンポーネントのメニューリンク。

様々なリンクを選択すると、それらは読み取り専用モードになっています。

### JCR {#prevent-anonymous-access-on-jcr}での匿名アクセスの禁止

既知の制限により、jcrコンテンツとjsonを介してコミュニティサイトのコンテンツが匿名訪問者に公開されますが、**allow anonymous access**&#x200B;はサイトのコンテンツに対して無効になっています。 ただし、この動作は、回避策として「Sling制限」を使用して制御できます。

jcrコンテンツとjsonを介した匿名ユーザーによるアクセスからコミュニティサイトのコンテンツを保護するには、次の手順に従います。

1. AEM作成者インスタンスで、https:// hostname:port/editor.html/content/site/sitename.htmlに移動します。

   >[!NOTE]
   >
   >ローカライズされたサイトには移動しないでください。

1. **ページプロパティ**&#x200B;に移動します。

   ![page-properties](assets/page-properties.png)

1. 「**詳細**」タブに移動します。

1. **認証要件**&#x200B;を有効にします。

   ![サイト認証](assets/site-authentication.png)

1. ログ追加インページのパス。 例えば、**/content/......./GetStarted**.
1. ページを公開します。

## 信頼されているコミュニティメンバー {#trusted-community-member}

この経験では、[Aaron McDonald](/help/communities/tutorials.md#demo-users)が[コミュニティマネージャーおよびモデレーター](/help/communities/create-site.md#roles)の役割を割り当てられたと想定しています。 そうでない場合は、作成者環境に戻って[サイト設定](/help/communities/sites-console.md#modifying-site-properties)を変更し、コミュニティマネージャーとモデレーターの両方としてAaron McDonaldを選択します。

右上隅の「`Log in`」を選択し、ユーザー名(aaron.mcdonald@mailinator.com)とパスワード(password)で署名します。 TwitterまたはFacebookの資格情報を使用してサインインする機能に注目してください。

![ログイン](assets/login.png)

登録コミュニティのメンバーとしてサインインした後は、次のメニュー項目に注目して、コミュニティサイトをクリックして参照してください。

* **「** Profile」オプションを使用すると、プロファイルを表示および編集できます。
* [「](/help/communities/configure-messaging.md) メッセージ」オプションを選択すると、ダイレクトメッセージングセクションに移動し、次の操作を行うことができます。

   1. 受信したダイレクトメッセージ（受信トレイ）、送信済み（送信済みアイテム）、削除済み（ごみ箱）の表示。
   1. 個人やグループに送信する新しいダイレクトメッセージを作成します。

* [「](/help/communities/notifications.md) 通知」オプションを選択すると、通知セクションに移動します。このセクションでは、関心のあるイベントの表示や、通知の設定の編集が可能です。
* [モデレート権限を持つ場合は、](/help/communities/published-site.md#moderationlink) 管理により、AEM Communitiesのモデレートページに移動します。

![adminscreen](assets/adminscreen.png)

カレンダーページがホームページになっていますが、これは、選択した参照サイトテンプレートの最初に含まれているのがカレンダー機能で、その後にアクティビティストリーム機能、フォーラム機能などが続いているからです。この構造体は、[サイトテンプレート](/help/communities/sites.md#edit-site-template)コンソールから、または作成者環境でサイトのプロパティを変更する場合に表示されます。

![sitetemplate](assets/sitetemplate.png)

>[!NOTE]
>
>Communitiesのコンポーネントと機能の詳細については、次を参照してください。
>
>* [コミュニティコンポーネント](/help/communities/author-communities.md)（作成者向け）
>* [コンポーネントおよび機能の基本事項](/help/communities/essentials.md)（開発者向け）


### フォーラムリンク {#forum-link}

フォーラムリンクを選択すると、基本的なフォーラム機能が表示されます。

メンバーは、新しいトピックを投稿したり、トピックをフォローしたりできます。

サイト訪問者は、様々な方法で投稿を表示したり、並べ替えたりできます。

![フォームリンク](assets/forumlink.png)

### グループリンク {#groups-link}

Aaron はグループ管理者なので、グループリンクを選択すると、新しいグループを作成するための画面が表示されます。ここで、グループテンプレートや画像を選択したり、グループをオープンにするかシークレットにするかを設定したり、メンバーを招待したりできます。

パブリッシュ環境でグループを作成する例を次に示します。

また、グループは作成者環境で作成し、作成者環境のコミュニティサイト内で管理することもできます（[コミュニティグループコンソール](/help/communities/groups.md)）。 [作成者](/help/communities/nested-groups.md)でのグループ作成の経験は、このチュートリアルで次に説明します。

![grouplink](assets/grouplink.png)

参照グループの作成：

1. 「**新しいグループ**」を選択します
1. **「設定」タブ**

   * Group Name : `Sports`
   * 説明 : `A parent group for various sporting groups`.
   * グループ URL 名 : `sports`
   * `Open Group`を選択（コミュニティのメンバーが参加できるようにする）

1. **「テンプレート」タブ**

   * `Reference Group`を選択します（ネストされたグループを許可するため、構造にグループ関数を含む）

1. 「**グループを作成**」を選択します

   ![creategroup](assets/creategroup.png)

新しいグループが作成されたら、その中に（ネストされる）2 つのグループを作成するために&#x200B;**新しい Sports グループを選択**&#x200B;します。サイト構造はグループ機能では始まらないので、スポーツグループを開いた後、「グループ」リンクを選択する必要があります。

![grouplink1](assets/grouplink1.png)

`Blog`で始まる2番目のリンクセットは、現在選択されているグループ`Sports`に属しています。 「スポーツ」`Groups`リンクを選択すると、スポーツグループ内に2つのグループをネストできます。

例として、`new groups`を2つ追加します。

* `Baseball`という名前の1つ

   * `Open Group`（必須メンバーシップ）のままにします。
   * 「テンプレート」タブで、`Conversational Group`を選択します。

* `Gymnastics`という名前の1つ

   * 設定を`Member Only Group` （制限付きメンバーシップ）に変更します。
   * 「テンプレート」タブで、`Conversational Group`を選択します。

**注意**：

* 両方のグループを表示する前に、ページを更新する必要がある場合があります。
* このテンプレートには&#x200B;*グループ機能が*&#x200B;含まれていないので、グループをこれ以上ネストすることはできません。
* 作成者の場合、[グループコンソール](/help/communities/groups.md)は、3つ目の選択肢として`Public Group` （オプションのメンバーシップ）を提供します。

両方のグループが作成されたら、Baseball グループ（オープングループ）を選択し、そのリンクに注目します。

`Discussions` `What's New` `Members`

このグループのリンクは、メインサイトのリンクの下に表示され、結果として、次のように表示されます。

![grouplink2](assets/grouplink2.png)

作成者 — 管理者権限で、[Communities Groupsコンソール](/help/communities/members.md)に移動し、`Community Engage Gymnastics <uid> Members`グループにWeston McCallを追加します。

引き続きパブリッシュ環境で、Aaron McDonald としてログアウトし、次のように匿名のサイト訪問者として Sports グループ内のグループを表示します。

* ホームページから
* `Groups`リンクを選択
* `Sports`リンクを選択
* 「スポーツ」`Groups`リンクを選択

Baseball グループのみが表示されます。

Weston McCall（weston.mccall@dodgit.com／password）としてログインし、同じ場所に移動します。Westonは、開いている`Baseball`グループと`enter or Leave`プライベート`Gymnastics`グループのどちらかを`Join`できることに注意してください。

![grouplink3](assets/grouplink3.png)

### Web ページリンク {#web-page-link}

Web ページリンクを選択すると、サイトに含まれる基本的な Web ページが表示されます。標準のAEMオーサリングツールを使用して、作成者環境のこのページにコンテンツを追加できます。

例えば、**author**&#x200B;インスタンスに移動し、[Communitiesのサイトコンソール](/help/communities/sites-console.md)で`engage`フォルダーを開き、**サイトを開く**&#x200B;アイコンを選択して、作成者編集モードにします。 次に、プレビューモードを選択して`Web Page`リンクを選択し、編集モードを選択してタイトルとテキストコンポーネントを追加します。 最後に、ページのみまたはサイト全体を再公開します。

![webpagelink](assets/webpagelink.png)

### モデレートリンク{#moderationlink}

コミュニティメンバーがモデレート権限を持つ場合、モデレートリンクが表示され、リンクを選択すると、投稿されたコミュニティコンテンツが表示され、作成者環境の[モデレートコンソール](/help/communities/moderation.md)と同様の方法で[モデレート](/help/communities/moderate-ugc.md)できます。

ブラウザーの戻るボタンを使用して、公開したサイトに戻ります。ほとんどのコンソールは、公開環境のグローバルナビゲーションからはアクセスできません。[](/help/communities/moderate-ugc.md)

![moderationlink](assets/moderationlink.png)

## 自己登録 {#self-registration}

ログアウトした後に、新しいユーザー登録を作成できます。

*  `Log In`
*  `Sign up for a new account`

![登録](assets/registration.png)

![入会](assets/signup.png)

デフォルトでは、電子メールアドレスがログイン ID になります。選択しない場合、訪問者は独自のログインID（ユーザー名）を入力できます。 ユーザー名は、発行環境で一意である必要があります。

ユーザーの名前、電子メール、パスワードを指定した後、`Sign Up`を選択すると、ユーザーが作成され、ユーザーの署名が有効になります。

サインインすると、最初に表示されるページは`Profile`ページで、これをパーソナライズできます。

![プロファイル](assets/profile.png)

メンバーが自分のログイン ID を忘れた場合は、電子メールアドレスを使用して回復することができます。

![forgotusername](assets/forgotusername.png)

