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

## 公開時に新しいサイトを参照 {#browse-to-new-site-on-publish}

新しく作成された Communities サイトが公開されたら、公開サーバーで、サイトの作成時に表示される URL を参照します。次に例を示します。

* オーサー URL = https://localhost:4502/content/sites/engage/en.html
* 公開 URL = https://localhost:4503/content/sites/engage/en.html

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

既知の制限では、jcr コンテンツおよび json を通じて、コミュニティサイトのコンテンツが匿名訪問者に公開されます **匿名アクセスを許可** は、サイトのコンテンツに対して無効になっています。 ただし、回避策として Sling の制限を使用して、この動作を制御できます。

jcr コンテンツと json を通じて匿名ユーザーがアクセスするコミュニティサイトのコンテンツを保護するには、次の手順に従います。

1. AEM オーサーインスタンスで、https:// hostname:port/editor.html/content/site/sitename.htmlに移動します。

   >[!NOTE]
   >
   >ローカライズされたサイトに移動しないでください。

1. に移動 **ページプロパティ**.

   ![page-properties](assets/page-properties.png)

1. 「**詳細**」タブに移動します。

1. Enable （有効） **認証要件**.

   ![site-authentication](assets/site-authentication.png)

1. ログインページのパスを追加します。 例： **/content/......./GetStart**.
1. ページを公開します。

## 信頼できるコミュニティ メンバー {#trusted-community-member}

このエクスペリエンスでは、次のことを前提としています [アーロン・マクドナルド](/help/communities/tutorials.md#demo-users) さんはの役割を割り当てられました [コミュニティマネージャーとモデレーター](/help/communities/create-site.md#roles). そうでない場合は、オーサー環境に戻って次の操作を行います。 [サイト設定の変更](/help/communities/sites-console.md#modifying-site-properties) コミュニティマネージャーとモデレーターの両方に Aaron McDonald を選択します。

右上隅のを選択します。 `Log in`さらに、ユーザー名（aaron.mcdonald@mailinator.com）とパスワード（password）で署名します。 twitterまたはFacebookの資格情報でログインできることに注意してください。

![ログイン](assets/login.png)

コミュニティの登録メンバーとしてログインしたら、次のメニュー項目を確認して、コミュニティサイトをクリックして参照します。

* **Profile** オプションを使用すると、プロファイルを表示および編集できます。
* [メッセージ](/help/communities/configure-messaging.md) オプションを選択すると、「ダイレクトメッセージ」セクションに移動し、次の操作を実行できます。

   1. 受信（インボックス）、送信（送信済み項目）、削除（ごみ箱）したダイレクトメッセージを表示します。
   1. 新しいダイレクトメッセージを作成して、個人やグループに送信できるようにします。

* [通知](/help/communities/notifications.md) オプションを選択すると、「通知」セクションに移動し、興味のあるイベントを表示したり、通知設定を編集したりできます。
* [管理](/help/communities/published-site.md#moderationlink) モデレート権限がある場合は、AEM Communities モデレートページに移動します。

![adminscreen](assets/adminscreen.png)

選択した参照サイトテンプレートには最初にカレンダー関数、次にアクティビティストリーム関数、フォーラム関数などが含まれているので、カレンダーページがホームページであることに注意してください。 この構造は、 [サイトテンプレート](/help/communities/sites.md#edit-site-template) コンソールを使用するか、オーサー環境でサイトプロパティを変更する場合は、次の操作を行います。

![sitetemplate](assets/sitetemplate.png)

>[!NOTE]
>
>Communities のコンポーネントと機能について詳しくは、以下を参照してください。
>
>* [Communities コンポーネント](/help/communities/author-communities.md) （作成者の場合）
>* [コンポーネント、機能、機能の基本事項](/help/communities/essentials.md) （開発者向け）

### フォーラムリンク {#forum-link}

「フォーラム」リンクを選択して、基本的なフォーラム機能を表示します。

メンバーは、新しいトピックを投稿したり、トピックをフォローしたりできます。

サイト訪問者は投稿を表示し、様々な方法で並べ替えることができます。

![forumlink](assets/forumlink.png)

### グループリンク {#groups-link}

Aaron はグループ管理者なので、「グループ」リンクを選択すると、グループテンプレート、画像、グループがオープンか秘密か、メンバーを招待するなどを選択してコミュニティグループを作成できます。

これは、パブリッシュ環境でグループを作成する例です。

グループはオーサー環境で作成し、オーサー環境のコミュニティサイト内で管理することもできます（[コミュニティグループコンソール](/help/communities/groups.md)）に設定します。 の経験 [オーサー環境でのグループの作成](/help/communities/nested-groups.md) このチュートリアルの次はです。

![grouplink](assets/grouplink.png)

参照グループを作成します。

1. を選択 **新規グループ**
1. **「設定」タブ**

   * グループ名： `Sports`
   * 説明： `A parent group for various sporting groups`.
   * グループ URL 名： `sports`
   * を選択 `Open Group` （参加による任意のコミュニティメンバーの参加を許可）

1. **「テンプレート」タブ**

   * を選択 `Reference Group` （ネストされたグループを許可する groups 関数が含まれます）

1. を選択 **グループを作成**

   ![creategroup](assets/creategroup.png)

新しいグループの作成後、 **新しいスポーツグループを選択します** （ネストされた） 2 つのグループをグループ内に作成します。 サイト構造はグループ機能から開始できないので、スポーツ グループを開いた後で、グループ リンクを選択する必要があります。

![grouplink1](assets/grouplink1.png)

で始まる 2 番目のリンクセット `Blog`は、現在選択されているグループ、 `Sports` グループ。 スポーツを選ぶ&#39; `Groups` リンク、スポーツグループ内に 2 つのグループをネストすることが可能です。

例として、2 つを追加します `new groups`.

* という名前のもの `Baseball`

   * として設定したままにする `Open Group` （必須メンバーシップ）。
   * 「テンプレート」タブで、次を選択します。 `Conversational Group`.

* という名前のもの `Gymnastics`

   * 設定をに変更します。 `Member Only Group` （会員制限）
   * 「テンプレート」タブで、次を選択します。 `Conversational Group`.

**注意**:

* 両方のグループが表示される前に、ページを更新する必要がある場合があります。
* このテンプレート *ではない* groups 関数を含めると、グループをさらにネストすることはできません。
* オーサー環境では、 [グループコンソール](/help/communities/groups.md) 3 つ目の選択肢として、 `Public Group` （任意メンバーシップ）。

両方のグループを作成したら、野球グループ、開いているグループを選択し、そのリンクに注目してください。

`Discussions` `What's New` `Members`

グループのリンクはメインサイトのリンクの下に表示され、結果として次のように表示されます。

![grouplink2](assets/grouplink2.png)

オーサー環境で – 管理者権限で、に移動します。 [コミュニティグループコンソール](/help/communities/members.md) に Weston McCall を追加します。 `Community Engage Gymnastics <uid> Members` グループ。

公開を続け、Aaron McDonald としてログアウトし、スポーツグループのグループを匿名サイト訪問者として表示します。

* ホームページから
* を選択 `Groups` リンク
* を選択 `Sports` リンク
* スポーツを選択&#39; `Groups` リンク

野球グループのみが表示されます。

Weston McCall （weston.mccall@dodgit.com/パスワード）としてログインし、同じ場所に移動します。 Weston が以下を実行できることに注意してください `Join` オープン `Baseball` とのグループ化 `enter or Leave` 私人 `Gymnastics` グループ。

![grouplink3](assets/grouplink3.png)

### Web ページリンク {#web-page-link}

「Web ページ」リンクを選択して、サイトに含まれている基本 Web ページを表示します。 オーサー環境でこのページにコンテンツを追加するには、標準のAEM オーサリングツールを使用できます。

例えば、 **作成者** インスタンスで、を開きます `engage` フォルダーの場所 [コミュニティサイトコンソール](/help/communities/sites-console.md)を選択し、 **Open Site** アイコンをクリックして、オーサー編集モードに入ります。 次に、プレビューモードを選択して、 `Web Page` リンクをクリックし、「編集モード」を選択して、タイトルおよびテキスト コンポーネントを追加します。 最後に、ページのみ、またはサイト全体を再公開します。

![webpagelink](assets/webpagelink.png)

### モデレートリンク {#moderationlink}

コミュニティメンバーがモデレート権限を持っている場合は、「モデレート」リンクが表示されます。 リンクを選択すると、投稿されたコミュニティコンテンツが表示され、次の操作を実行できます [モデレート](/help/communities/moderate-ugc.md) ～と同様の方法で [モデレートコンソール](/help/communities/moderation.md) オーサー環境で実行します。

ブラウザーの「戻る」ボタンを使用して、公開されたサイトに戻ります。 ほとんどのコンソールは、パブリッシュ環境のグローバルナビゲーションからアクセスできません。

![moderationlink](assets/moderationlink.png)

## Self-Registration {#self-registration}

ログアウト後は、ユーザー登録を作成できます。

* `Log In` を選択します。
* `Sign up for a new account` を選択します。

![登録](assets/registration.png)

![登録](assets/signup.png)

デフォルトでは、メールアドレスはログイン ID です。 これをオフにすると、訪問者は自分のログイン ID （ユーザー名）を入力できるようになります。 ユーザー名は、パブリッシュ環境で一意である必要があります。

ユーザーの名前、メールおよびパスワードを指定した後、を選択します。 `Sign Up` ユーザーを作成し、署名できるようにします。

ログイン後、最初に表示されるページは次のとおりです `Profile` パーソナライズ可能なページ。

![profile](assets/profile.png)

メンバーが自分のログイン ID を忘れた場合は、それが彼らの電子メールアドレスを使用して回復することが可能です。

![forgotusername](assets/forgotusername.png)
