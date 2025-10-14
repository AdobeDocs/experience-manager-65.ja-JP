---
title: 公開したサイトを使ってみる
description: サイトの作成時に公開サーバーに表示される URL を参照する方法を説明します。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: ebc4e1e7-34f0-4f4e-9f00-178dfda23ce4
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1195'
ht-degree: 1%

---

# 公開したサイトを使ってみる {#experience-the-published-site}

## Publishの新しいサイトを参照 {#browse-to-new-site-on-publish}

新しく作成された Communities サイトが公開されたら、公開サーバーで、サイトの作成時に表示される URL を参照します。次に例を示します。

* オーサー URL = https://localhost:4502/content/sites/engage/en.html
* PUBLISH URL = https://localhost:4503/content/sites/engage/en.html

オーサー環境とパブリッシュ環境で、どのメンバーがログインするかについての混乱を最小限にするために、インスタンスごとに異なるブラウザーを使用することをお勧めします。

公開されたサイトに初めて到達した場合、サイト訪問者は通常、既にログインしておらず、匿名となります。

`https://localhost:4503/content/sites/engage/en.html {#http-localhost-content-sites-engage-en-html}`

![authorpublished](assets/authorpublished.png)

## 匿名サイト訪問者 {#anonymous-site-visitor}

匿名のサイト訪問者には、UI に次が表示されます。

* サイトのタイトル（はじめにチュートリアル）
* プロファイルリンクがありません
* メッセージリンクなし
* 通知リンクなし
* 検索フィールド
* ログインリンク
* ブランドバナー
* 参照サイトテンプレートに含まれるコンポーネントのメニューリンク。

様々なリンクを選択すると、読み取り専用モードであることがわかります。

### JCR での匿名アクセスの防止 {#prevent-anonymous-access-on-jcr}

既知の制限では、サイトのコンテンツでは **匿名アクセスを許可** が無効になっていますが、jcr コンテンツおよび json を通じてコミュニティサイトのコンテンツが匿名訪問者に公開されます。 ただし、回避策として Sling の制限を使用して、この動作を制御できます。

jcr コンテンツと json を通じて匿名ユーザーがアクセスするコミュニティサイトのコンテンツを保護するには、次の手順に従います。

1. AEM オーサーインスタンスで、https:// hostname:port/editor.html/content/site/sitename.htmlに移動します。

   >[!NOTE]
   >
   >ローカライズされたサイトに移動しないでください。

1. **ページプロパティ** に移動します。

   ![page-properties](assets/page-properties.png)

1. 「**詳細**」タブに移動します。

1. **認証要件** を有効にします。

   ![&#x200B; サイト認証 &#x200B;](assets/site-authentication.png)

1. ログインページのパスを追加します。 例：**/content/......./GetStarted**.
1. ページを公開します。

## 信頼できるコミュニティ メンバー {#trusted-community-member}

このエクスペリエンスでは、[Aaron McDonald](/help/communities/tutorials.md#demo-users) が [&#x200B; コミュニティマネージャーとモデレーター &#x200B;](/help/communities/create-site.md#roles) の役割に割り当てられていることを前提としています。 ない場合は、オーサー環境に戻って [&#x200B; サイト設定を変更 &#x200B;](/help/communities/sites-console.md#modifying-site-properties)、コミュニティマネージャーとモデレーターの両方として Aaron McDonald を選択します。

右上隅の「`Log in`」を選択し、ユーザー名（aaron.mcdonald@mailinator.com）とパスワード（password）で署名します。 twitterまたはFacebookの資格情報でログインできることに注意してください。

![ログイン](assets/login.png)

コミュニティの登録メンバーとしてログインしたら、次のメニュー項目を確認して、コミュニティサイトをクリックして参照します。

* 「**プロファイル**」オプションを使用すると、プロファイルを表示および編集できます。
* 「[&#x200B; メッセージ &#x200B;](/help/communities/configure-messaging.md)」オプションを選択すると、ダイレクトメッセージのセクションに移動し、次の操作を実行できます。

   1. 受信（インボックス）、送信（送信済み項目）、削除（ごみ箱）したダイレクトメッセージを表示します。
   1. 新しいダイレクトメッセージを作成して、個人やグループに送信できるようにします。

* [&#x200B; 通知 &#x200B;](/help/communities/notifications.md) オプションを選択すると、「通知」セクションに移動し、興味のあるイベントを表示したり、通知設定を編集したりできます。
* [&#x200B; 管理 &#x200B;](/help/communities/published-site.md#moderationlink) モデレート権限がある場合は、AEM Communities モデレートページに移動します。

![adminscreen](assets/adminscreen.png)

選択した参照サイトテンプレートには最初にカレンダー関数、次にアクティビティストリーム関数、フォーラム関数などが含まれているので、カレンダーページがホームページであることに注意してください。 この構造は、[&#x200B; サイトテンプレート &#x200B;](/help/communities/sites.md#edit-site-template) コンソールから表示されるか、オーサー環境でサイトプロパティを変更する際に表示されます。

![sitetemplate](assets/sitetemplate.png)

>[!NOTE]
>
>Communities のコンポーネントと機能について詳しくは、以下を参照してください。
>
>* [Communities コンポーネント &#x200B;](/help/communities/author-communities.md) （作成者向け）
>* [&#x200B; コンポーネント、機能、機能の基本事項 &#x200B;](/help/communities/essentials.md) （開発者向け）

### フォーラムリンク {#forum-link}

「フォーラム」リンクを選択して、基本的なフォーラム機能を表示します。

メンバーは、新しいトピックを投稿したり、トピックをフォローしたりできます。

サイト訪問者は投稿を表示し、様々な方法で並べ替えることができます。

![forumlink](assets/forumlink.png)

### グループリンク {#groups-link}

Aaron はグループ管理者なので、「グループ」リンクを選択すると、グループテンプレート、画像、グループがオープンか秘密か、メンバーを招待するなどを選択してコミュニティグループを作成できます。

これは、パブリッシュ環境でグループを作成する例です。

グループはオーサー環境で作成し、オーサー環境のコミュニティサイト内で管理することもできます（[&#x200B; コミュニティグループコンソール &#x200B;](/help/communities/groups.md)）。 [&#x200B; オーサー環境でグループを作成する &#x200B;](/help/communities/nested-groups.md) のエクスペリエンスについては、このチュートリアルの次のステップで説明します。

![grouplink](assets/grouplink.png)

参照グループを作成します。

1. **新規グループ** を選択します
1. **「設定」タブ**

   * グループ名：`Sports`
   * 説明：`A parent group for various sporting groups`。
   * グループ URL 名：`sports`
   * `Open Group` を選択してください（コミュニティ メンバーの参加を許可します）

1. **「テンプレート」タブ**

   * `Reference Group` を選択します（ネストされたグループを許可する groups 関数が構造に含まれます）。

1. 「**グループを作成**」を選択します。

   ![creategroup](assets/creategroup.png)

新しいグループを作成したら **新しいスポーツグループを選択**、その中に（ネストされた） 2 つのグループを作成します。 サイト構造はグループ機能から開始できないので、スポーツ グループを開いた後で、グループ リンクを選択する必要があります。

![grouplink1](assets/grouplink1.png)

2 つ目のリンクセット（「`Blog`」で始まる）は、現在選択されているグループである「`Sports`」グループに属しています。 スポーツの `Groups` リンクを選択すると、スポーツグループ内に 2 つのグループをネストすることができます。

例として、2 つの `new groups` を追加します。

* `Baseball` という名前

   * `Open Group` として設定したままにします（必須メンバーシップ）。
   * 「テンプレート」タブで、「`Conversational Group`」を選択します。

* `Gymnastics` という名前

   * 設定を `Member Only Group` （制限付きメンバーシップ）に変更します。
   * 「テンプレート」タブで、「`Conversational Group`」を選択します。

**通知**:

* 両方のグループが表示される前に、ページを更新する必要がある場合があります。
* このテンプレートには groups 関数が含まれて *ないので* グループをさらにネストすることはできません。
* オーサー環境では、[&#x200B; グループコンソール &#x200B;](/help/communities/groups.md)3 つ目の選択肢として `Public Group` （オプションのメンバーシップ）が用意されています。

両方のグループを作成したら、野球グループ、開いているグループを選択し、そのリンクに注目してください。

`Discussions` `What's New` `Members`

グループのリンクはメインサイトのリンクの下に表示され、結果として次のように表示されます。

![grouplink2](assets/grouplink2.png)

作成者の場合 – 管理者権限で [Communities グループコンソールに移動し &#x200B;](/help/communities/members.md)Weston McCall を `Community Engage Gymnastics <uid> Members` グループに追加します。

公開を続け、Aaron McDonald としてログアウトし、スポーツグループのグループを匿名サイト訪問者として表示します。

* ホームページから
* リンク `Groups` 選択
* リンク `Sports` 選択
* スポーツの `Groups` リンクを選択する

野球グループのみが表示されます。

Weston McCall （weston.mccall@dodgit.com/パスワード）としてログインし、同じ場所に移動します。 Weston は、open `Baseball` グループと、private `Gymnastics` グループのどちらか `enter or Leave` も `Join` 定できます。

![grouplink3](assets/grouplink3.png)

### Web ページリンク {#web-page-link}

「Web ページ」リンクを選択して、サイトに含まれている基本 Web ページを表示します。 オーサー環境でこのページにコンテンツを追加するには、標準のAEM オーサリングツールを使用できます。

例えば、**オーサー** インスタンスに移動し、[Communities サイトコンソール &#x200B;](/help/communities/sites-console.md) で `engage` フォルダーを開き、「**サイトを開く**」アイコンを選択してオーサー編集モードに入ります。 次に、プレビューモードを選択して `Web Page` リンクを選択し、編集モードを選択してタイトルおよびテキスト コンポーネントを追加します。 最後に、ページのみ、またはサイト全体を再公開します。

![webpagelink](assets/webpagelink.png)

### モデレートリンク {#moderationlink}

コミュニティメンバーがモデレート権限を持っている場合は、「モデレート」リンクが表示されます。 リンクを選択すると、投稿されたコミュニティコンテンツが表示され、オーサー環境の [&#x200B; モデレートコンソール &#x200B;](/help/communities/moderate-ugc.md) と同様の方法でリンクを [&#x200B; モデレート &#x200B;](/help/communities/moderation.md) できます。

ブラウザーの「戻る」ボタンを使用して、公開されたサイトに戻ります。 ほとんどのコンソールは、パブリッシュ環境のグローバルナビゲーションからアクセスできません。

![moderationlink](assets/moderationlink.png)

## Self-Registration {#self-registration}

ログアウト後は、ユーザー登録を作成できます。

* `Log In` を選択します。
* `Sign up for a new account` を選択します。

![&#x200B; 登録 &#x200B;](assets/registration.png)

![&#x200B; 登録 &#x200B;](assets/signup.png)

デフォルトでは、メールアドレスはログイン ID です。 これをオフにすると、訪問者は自分のログイン ID （ユーザー名）を入力できるようになります。 ユーザー名は、パブリッシュ環境で一意である必要があります。

ユーザーの名前、メールおよびパスワードを指定した後、`Sign Up` を選択すると、ユーザーが作成され、署名できるようになります。

ログイン後、最初に表示されるページは `Profile` ページです。このページをパーソナライズできます。

![profile](assets/profile.png)

メンバーが自分のログイン ID を忘れた場合は、それが彼らの電子メールアドレスを使用して回復することが可能です。

![forgotusername](assets/forgotusername.png)
