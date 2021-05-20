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
exl-id: ebc4e1e7-34f0-4f4e-9f00-178dfda23ce4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1202'
ht-degree: 33%

---

# 公開したサイトを使ってみる {#experience-the-published-site}

## パブリッシュサーバー上の新しいサイトの参照 {#browse-to-new-site-on-publish}

新しく作成したコミュニティサイトが公開されたので、サイトの作成時に表示されるURLを参照します。ただし、次に例を示します。

* 作成者URL = https://localhost:4502/content/sites/engage/en.html
* パブリッシュURL = https://localhost:4503/content/sites/engage/en.html

どのメンバーがオーサーインスタンスにサインインし、どのメンバーがパブリッシュインスタンスにサインインしているかを混乱なく把握するために、インスタンスごとに異なるブラウザーを使用することを推奨します。

公開済みサイトに初めてアクセスするときは、通常、そのサイト訪問者はまだサインインしておらず、匿名です。

`https://localhost:4503/content/sites/engage/en.html {#http-localhost-content-sites-engage-en-html}`

![authorpublished](assets/authorpublished.png)

## 匿名のサイト訪問者 {#anonymous-site-visitor}

匿名のサイト訪問者のUIには、次の情報が表示されます。

* サイトのタイトル（はじめにのチュートリアル）
* プロファイルリンクなし
* メッセージのリンクなし
* 通知リンクなし
* 検索フィールド
* ログインリンク
* ブランドバナー
* リファレンスサイトテンプレートに含まれるコンポーネントのメニューリンク。

様々なリンクを選択すると、読み取り専用モードになります。

### JCR {#prevent-anonymous-access-on-jcr}での匿名アクセスを防ぐ

既知の制限により、jcrコンテンツとjsonを通じてコミュニティサイトのコンテンツを匿名訪問者に公開しますが、サイトのコンテンツに対して&#x200B;**匿名アクセスを許可**&#x200B;は無効になっています。 ただし、この動作は、Slingの制限を回避策として使用して制御できます。

コミュニティサイトのコンテンツを、匿名ユーザーがjcrコンテンツやjsonを介してアクセスするのを防ぐには、次の手順に従います。

1. AEMオーサーインスタンスで、 https:// hostname:port/editor.html/content/site/sitename.htmlに移動します。

   >[!NOTE]
   >
   >ローカライズされたサイトに移動しないでください。

1. **ページのプロパティ**&#x200B;に移動します。

   ![page-properties](assets/page-properties.png)

1. 「**詳細**」タブに移動します。

1. **認証要件**&#x200B;を有効にします。

   ![site-authentication](assets/site-authentication.png)

1. ログインページのパスを追加します。 例えば、**/content/......./GetStarted**&#x200B;です。
1. ページを公開します。

## 信頼されているコミュニティメンバー {#trusted-community-member}

この経験は、[Aaron McDonald](/help/communities/tutorials.md#demo-users)に[コミュニティマネージャーおよびモデレーター](/help/communities/create-site.md#roles)の役割が割り当てられたことを前提としています。 そうでない場合は、オーサー環境に戻って[サイト設定を変更](/help/communities/sites-console.md#modifying-site-properties)し、コミュニティマネージャーとモデレーターの両方としてAaron McDonaldを選択します。

右上隅で「`Log in`」を選択し、ユーザー名(aaron.mcdonald@mailinator.com)とパスワード(password)で署名します。 twitterまたはFacebookの資格情報を使用してログインする機能に注意してください。

![ログイン](assets/login.png)

登録済みコミュニティメンバーとしてサインインしたら、次のメニュー項目に注意して、コミュニティサイトをクリックし、参照してください。

* **** 「プロファイル」オプションを使用すると、プロファイルを表示および編集できます。
* [「](/help/communities/configure-messaging.md) Messages」オプションを選択すると、ダイレクトメッセージの節に移動し、次の操作を実行できます。

   1. 受信したダイレクトメッセージ（インボックス）、送信済み（送信済みアイテム）、削除済み（ごみ箱）を表示します。
   1. 個人やグループに送信する新しいダイレクトメッセージを作成します。

* [](/help/communities/notifications.md) 「通知」オプションを選択すると、通知セクションに移動し、関心のあるイベントを表示したり、通知設定を編集したりできます。
* [](/help/communities/published-site.md#moderationlink) 管理者は、モデレート権限を持っている場合、AEM Communitiesのモデレートページに移動します。

![adminscreen](assets/adminscreen.png)

カレンダーページがホームページになっていますが、これは、選択した参照サイトテンプレートの最初に含まれているのがカレンダー機能で、その後にアクティビティストリーム機能、フォーラム機能などが続いているからです。この構造は、[サイトテンプレート](/help/communities/sites.md#edit-site-template)コンソールから、またはオーサー環境でサイトのプロパティを変更する際に表示されます。

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

![forumlink](assets/forumlink.png)

### グループリンク {#groups-link}

Aaron はグループ管理者なので、グループリンクを選択すると、新しいグループを作成するための画面が表示されます。ここで、グループテンプレートや画像を選択したり、グループをオープンにするかシークレットにするかを設定したり、メンバーを招待したりできます。

パブリッシュ環境でグループを作成する例を次に示します。

グループは、オーサー環境で作成し、オーサー環境のコミュニティサイト内で管理することもできます（[コミュニティグループコンソール](/help/communities/groups.md)）。 オーサー](/help/communities/nested-groups.md)上での[グループの作成は、このチュートリアルで次に行います。

![grouplink](assets/grouplink.png)

参照グループの作成：

1. **新しいグループ**&#x200B;を選択します。
1. **「設定」タブ**

   * Group Name : `Sports`
   * 説明 : `A parent group for various sporting groups`.
   * グループ URL 名 : `sports`
   * `Open Group`を選択します（コミュニティメンバーの参加を許可）

1. **「テンプレート」タブ**

   * `Reference Group`を選択します（ネストされたグループを許可するために、構造にグループ機能を含めます）

1. 「**グループを作成**」を選択します。

   ![creategroup](assets/creategroup.png)

新しいグループが作成されたら、その中に（ネストされる）2 つのグループを作成するために&#x200B;**新しい Sports グループを選択**&#x200B;します。サイト構造はグループ機能で始まることができないので、Sportsグループを開いた後、「グループ」リンクを選択する必要があります。

![grouplink1](assets/grouplink1.png)

`Blog`から始まる2番目のリンクセットは、現在選択されているグループ`Sports`グループに属しています。 「Sports」の`Groups`リンクを選択すると、Sportsグループ内に2つのグループをネストできます。

例えば、`new groups`を2つ追加します。

* `Baseball`という名前の1つ

   * `Open Group`（必須のメンバーシップ）のままにします。
   * 「テンプレート」タブで、「`Conversational Group`」を選択します。

* `Gymnastics`という名前の1つ

   * 設定を`Member Only Group`（制限付きメンバーシップ）に変更します。
   * 「テンプレート」タブで、「`Conversational Group`」を選択します。

**注意**：

* 両方のグループを表示する前に、ページの更新が必要な場合があります。
* このテンプレートでは、グループ機能は&#x200B;*含まれていない*&#x200B;ので、グループのこれ以上のネストはできません。
* オーサー環境では、[グループコンソール](/help/communities/groups.md)に3つ目の選択肢(`Public Group`（オプションのメンバーシップ）が用意されています。

両方のグループが作成されたら、Baseball グループ（オープングループ）を選択し、そのリンクに注目します。

`Discussions` `What's New` `Members`

このグループのリンクは、メインサイトのリンクの下に表示され、結果として、次のように表示されます。

![grouplink2](assets/grouplink2.png)

オーサー環境で、管理権限を持つ[コミュニティグループコンソール](/help/communities/members.md)に移動し、`Community Engage Gymnastics <uid> Members`グループにWeston McCallを追加します。

引き続きパブリッシュ環境で、Aaron McDonald としてログアウトし、次のように匿名のサイト訪問者として Sports グループ内のグループを表示します。

* ホームページから
* `Groups`リンクを選択
* `Sports`リンクを選択
* Sportsの`Groups`リンクを選択します。

Baseball グループのみが表示されます。

Weston McCall（weston.mccall@dodgit.com／password）としてログインし、同じ場所に移動します。Westonは、開いている`Baseball`グループと`enter or Leave`プライベートの`Gymnastics`グループの`Join`を実行できます。

![grouplink3](assets/grouplink3.png)

### Web ページリンク {#web-page-link}

Web ページリンクを選択すると、サイトに含まれる基本的な Web ページが表示されます。標準のAEMオーサリングツールを使用して、オーサー環境でこのページにコンテンツを追加できます。

例えば、**author**&#x200B;インスタンスに移動し、[コミュニティサイトコンソール](/help/communities/sites-console.md)で`engage`フォルダーを開き、**サイトを開く**&#x200B;アイコンを選択してオーサー編集モードに入ります。 次に、プレビューモードを選択して`Web Page`リンクを選択し、編集モードを選択してタイトルとテキストコンポーネントを追加します。 最後に、ページのみまたはサイト全体を再公開します。

![webpagelink](assets/webpagelink.png)

### モデレートリンク {#moderationlink}

コミュニティメンバーがモデレート権限を持っている場合は、モデレートリンクが表示され、投稿されたコミュニティコンテンツが表示され、オーサー環境の[モデレートコンソール](/help/communities/moderation.md)と同様の方法で[モデレート](/help/communities/moderate-ugc.md)できます。

ブラウザーの戻るボタンを使用して、公開したサイトに戻ります。ほとんどのコンソールは、パブリッシュ環境のグローバルナビゲーションからはアクセスできません。[](/help/communities/moderate-ugc.md)

![moderationlink](assets/moderationlink.png)

## 自己登録 {#self-registration}

ログアウトした後に、新しいユーザー登録を作成できます。

*  `Log In`
*  `Sign up for a new account`

![登録](assets/registration.png)

![登録](assets/signup.png)

デフォルトでは、電子メールアドレスがログイン ID になります。オフにすると、訪問者は独自のログインID（ユーザー名）を入力できます。 ユーザー名は、パブリッシュ環境で一意である必要があります。

ユーザーの名前、電子メール、パスワードを指定した後、`Sign Up`を選択すると、ユーザーが作成され、署名できるようになります。

サインインすると、最初に表示されるページは`Profile`ページで、ページをパーソナライズできます。

![プロファイル](assets/profile.png)

メンバーが自分のログイン ID を忘れた場合は、電子メールアドレスを使用して回復することができます。

![forgotusername](assets/forgotusername.png)
