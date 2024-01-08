---
title: コミュニティサイトの作成
description: Adobe Experience Manager Communities サイトの作成方法を説明します。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: d4c1895f-421c-4146-b94a-8d11065ef9e3
source-git-commit: f03d0ab9d0f491441378e16e1590d33651f064b5
workflow-type: tm+mt
source-wordcount: '1556'
ht-degree: 1%

---

# コミュニティサイトの作成{#author-a-new-community-site}

## コミュニティサイトを作成する {#create-a-community-site}

オーサーインスタンスを使用してコミュニティサイトを作成します。 AEMオーサーインスタンス上：

1. 管理者権限でログインします。
1. グローバルナビゲーションから、に移動します。 **[!UICONTROL Communities]** > **[!UICONTROL Sites]**.

コミュニティサイトコンソールでは、コミュニティサイトを作成する手順を示すウィザードを使用できます。 次の項目に進みます。 `Next` 手順または `Back` を前の手順に戻してから、最後の手順でサイトをコミットします。

コミュニティサイトの作成を開始するには：

* を選択します。 `Create` 」ボタンをクリックします。

![createcommunitysite](assets/createcommunitysite.png)

### 手順 1：サイトテンプレート {#step-site-template}

![サイトを作成するテンプレート](assets/create-site.png)

次の日： [サイトテンプレートの手順](/help/communities/sites-console.md#step2013asitetemplate)、タイトル、説明、URL の名前を入力し、コミュニティサイトテンプレートを選択します。次に例を示します。

* **コミュニティサイトのタイトル**: `Getting Started Tutorial`
* **コミュニティサイトの説明**: `A site for engaging with the community.`
* **コミュニティサイトのルート**:（デフォルトのルートの場合は空白のままにします） `/content/sites`)
* **クラウド設定**:（クラウド設定が指定されていない場合は空白にします）指定したクラウド設定へのパスを指定します。
* **コミュニティサイトの基本言語**:（単一言語の場合は「未変更」をそのままにします。英語）ドロップダウンリストを使用して、1 つを選択します。 *またはその他* 使用可能な言語 ( ドイツ語、イタリア語、フランス語、日本語、スペイン語、ポルトガル語（ブラジル）、中国語（繁体字）、中国語（簡体字）)) のベース言語。 追加された言語ごとに 1 つのコミュニティサイトが作成され、 [多言語サイトのコンテンツの翻訳](/help/sites-administering/translation.md). 各サイトのルートページには、選択した言語の 1 つの言語コード（英語の場合は「en」、フランス語の場合は「fr」など）で名前が付けられた子ページが含まれます。

* **コミュニティサイト名**: engage

   * サイトの作成後に名前が簡単に変更されないので、名前を再確認します。
   * 初期 URL はコミュニティサイト名の下に表示されます
   * 有効な URL に、ベース言語コード+ &quot;.html&quot;を追加します。
   * *例：*, https://localhost:4502/content/sites/ `engage/en.html`

* **テンプレート**：プルダウンして選択します。 `Reference Site`

* 「**次へ**」を選択します。

### 手順 2：デザイン {#step-design}

デザインの手順は、テーマとブランディングバナーを選択するための 2 つの節で説明します。

#### コミュニティサイトのテーマ {#community-site-theme}

テンプレートに適用するスタイルを選択します。 選択すると、テーマはチェックマークでオーバーレイされます。

#### コミュニティサイトのブランディング {#community-site-branding}

（オプション）サイトのページ全体に表示するバナー画像をアップロードします。 バナーは、ブラウザーの左端、コミュニティサイトのヘッダーとナビゲーションリンクの間に固定されています。 バナーの高さは 120 ピクセルに切り抜かれます。 バナーのサイズは、ブラウザーの幅と 120 ピクセルの高さに合わせて変更されません。

![community-site-branding](assets/community-site-branding.png)

![upload-image-site](assets/upload-image-site.png)

「**次へ**」を選択します。

### 手順 3：設定 {#step-settings}

設定ステップで、選択する前に `Next`の 7 つのセクションで、ユーザー管理、タグ付け、モデレート、グループ管理、分析および翻訳に関する設定にアクセスできます。

#### User Management {#user-management}

のすべてのチェックボックスをオンにします。 [ユーザー管理](/help/communities/sites-console.md#user-management)

* サイト訪問者に自己登録を許可するには
* サイト訪問者がサインインせずにサイトを表示できるようにするには
* メンバーが他のコミュニティメンバーからメッセージを送受信できるようにするには
* プロファイルの登録と作成の代わりにFacebookでのログインを許可するには
* プロファイルの登録と作成を行う代わりに、Twitterを使用したログインを許可するには

>[!NOTE]
>
>実稼動環境では、カスタムのFacebookおよびTwitterアプリケーションを作成する必要があります。 詳しくは、 [facebookとTwitterを使用したソーシャルログイン](/help/communities/social-login.md).

![コミュニティサイト設定](assets/site-settings.png)

#### タグ付け {#tagging}

コミュニティコンテンツに適用されるタグは、以前に [タグ付けコンソール](/help/sites-administering/tags.md#tagging-console) ( 例えば [チュートリアル名前空間](/help/communities/setup.md#create-tutorial-tags)) をクリックします。

名前空間を検索するには、先頭入力検索を使用すると簡単です。 例：

* 型 `tut`
* `Tutorial` を選択します。

![タグ付け](assets/tagging.png)

#### 役割 {#roles}

[コミュニティメンバーの役割](/help/communities/users.md) は、「役割」セクションの設定を通じて割り当てられます。

コミュニティメンバー（またはメンバーのグループ）がコミュニティマネージャーとしてサイトを体験するには、先行入力検索を使用して、ドロップダウンのオプションからメンバーまたはグループ名を選択します。

例：

* 型 `q`
* クインハーパーを選択

>[!NOTE]
>
>[トンネルサービス](https://helpx.adobe.com/experience-manager/6-3/help/communities/deploy-communities.html#tunnel-service-on-author) パブリッシュ環境にのみ存在するメンバーとグループを選択できます。

![新しいサイトでのユーザーの役割](assets/site-admin-1.png)

#### モデレート {#moderation}

のデフォルトのグローバル設定を受け入れる [モデレート](/help/communities/sites-console.md#moderation) ユーザー生成コンテンツ (UGC)。

![モデレート](assets/moderation1.png)

#### ANALYTICS {#analytics}

Adobe Analyticsがライセンスされ、Analytics Cloudのサービスとフレームワークが設定されている場合は、Analytics を有効にしてフレームワークを選択できます。

詳しくは、 [コミュニティ機能用の Analytics 設定](/help/communities/analytics.md).

![分析](assets/analytics.png)

#### 翻訳 {#translation}

The [翻訳設定](/help/communities/sites-console.md#translation) サイトのベース言語と、UGC を翻訳できるかどうか、および翻訳可能な場合はどの言語に翻訳するかを指定します。

* チェック **機械翻訳を許可**
* デフォルトの機械翻訳サービスで翻訳用に選択されたデフォルトの言語をそのままにします
* デフォルトの翻訳プロバイダーと設定のままにします。
* 言語コピーがないので、グローバルストアは不要です
* 選択 **ページ全体を翻訳**
* デフォルトの永続性オプションをそのままにする

![translation-settings](assets/translation-settings.png)

### 手順 4：コミュニティサイトを作成する {#step-create-communities-site}

選択 **を作成します。**

![create-site](assets/create-site2.png)

処理が完了すると、新しいサイトのフォルダーがコミュニティ — サイトコンソールに表示されます。

![communitiessitesconsole](assets/communitiessitesconsole.png)

## コミュニティサイトを公開 {#publish-the-community-site}

作成したサイトは、コミュニティ — サイトコンソール、および新しいサイトを作成できる同じコンソールから管理する必要があります。

コミュニティサイトのフォルダーを選択して開いた後、サイトアイコンの上にマウスポインターを置くと、次の 4 つのアクションアイコンが表示されます。

![siteactionicons-1](assets/siteactionicons-1.png)

4 つ目の省略記号アイコン（その他のアクション）を選択すると、「サイトを書き出し」および「サイトを削除」オプションが表示されます。

![siteactionsnew-1](assets/siteactionsnew-1.png)

左から右に、次のように表示されます。

* **サイトを開く**

  鉛筆アイコンを選択すると、コミュニティサイトがオーサリング編集モードで開き、ページコンポーネントを追加または設定できます。

* **サイトを編集**

  プロパティアイコンを選択すると、コミュニティサイトが開き、タイトルやテーマの変更などのプロパティを変更できます。

* **サイトを公開**

  世界のアイコンを選択すると、コミュニティサイトが公開されます（例えば、パブリッシュサーバーがローカルマシンで実行されている場合は、デフォルトで localhost:4503 に公開されます）。

* **サイトを書き出し**

  書き出しアイコンを選択すると、コミュニティサイトのパッケージが作成され、そのパッケージがに保存されます。 [パッケージマネージャー](/help/sites-administering/package-manager.md) とダウンロードされました。 UGC はサイトパッケージに含まれていません。

* **サイトを削除**

  削除アイコンを選択すると、内からコミュニティサイトが削除されます。 **[!UICONTROL コミュニティ/サイトコンソール]**. この操作により、UGC、ユーザーグループ、アセット、データベースレコードなど、サイトに関連するすべての項目が削除されます。

![siteactions](assets/siteactions.png)

>[!NOTE]
>
>パブリッシュインスタンスにデフォルトポート 4503 を使用しない場合は、デフォルトレプリケーションエージェントを編集して、ポート番号を正しい値に設定します。
>
>オーサーインスタンスで、メインメニューから次の操作を実行します。
>
>1. に移動します。 **[!UICONTROL ツール]** > **[!UICONTROL 運用]** > **[!UICONTROL レプリケーション]** メニュー。
>1. 選択 **[!UICONTROL 作成者のエージェント]**.
>1. 選択 **[!UICONTROL デフォルトエージェント (publish)]**.
>1. 次の隣 **[!UICONTROL 設定]**&#x200B;を選択します。 **[!UICONTROL 編集]**.
>1. エージェント設定のポップアップダイアログで、 **[!UICONTROL 輸送]** タブをクリックします。
>1. URI で、ポート番号 4503 を目的のポート番号に変更します。 例えば、ポート 6103 を使用するには、 https://localhost:6103/bin/receive?sling:authRequestLogin=1と入力します。
>1. 「**[!UICONTROL OK]**」を選択します。
>1. （オプション）「 」を選択します。 **[!UICONTROL クリア]** または **[!UICONTROL 再試行を強制]** レプリケーションキューをリセットします。

### 公開を選択 {#select-publish}

パブリッシュサーバーが実行されていることを確認したら、世界アイコンを選択してコミュニティサイトを公開します。

![publish-site](assets/publish-site.png)

コミュニティサイトが正常に公開されると、「サイトが公開されました」というメッセージが短時間表示されます。

### 新しいコミュニティユーザーグループ {#new-community-user-groups}

新しいコミュニティサイトと共に、様々な管理機能に対して適切な権限が設定された新しいユーザーグループが作成されます。 詳しくは、 [コミュニティサイトのユーザーグループ](/help/communities/users.md#usergroupsforcommunitysites).

この新しいコミュニティサイトでは、手順 1 でサイト名「engage」を指定すると、 [グループコンソール](/help/communities/members.md) （グローバルナビゲーション：コミュニティ、グループ）:

* コミュニティエンゲージコミュニティマネージャー
* コミュニティエンゲージグループ管理者
* コミュニティエンゲージメンバー
* コミュニティエンゲージモデレーター
* コミュニティエンゲージ権限を持つメンバー
* コミュニティエンゲージサイトコンテンツマネージャー

[Aaron McDonald](/help/communities/tutorials.md#demo-users) は、次のメンバーです：

* コミュニティエンゲージコミュニティマネージャー
* コミュニティエンゲージモデレーター
* コミュニティエンゲージメンバー（間接的にモデレーターグループのメンバーとして）

![user-group](assets/user-group.png)

#### https://localhost:4503/content/sites/engage/en.html {#http-localhost-content-sites-engage-en-html}

![エンゲージ](assets/engage.png)

## 認証エラー用の設定 {#configure-for-authentication-error}

サイトが設定され、パブリッシュにプッシュされると、 [ログインのマッピングの構成](/help/communities/sites-console.md#configure-for-authentication-error) ( `Adobe Granite Login Selector Authentication Handler`) をパブリッシュインスタンスでクリックします。 ログイン資格情報が正しく入力されていない場合、認証エラーによりコミュニティサイトのログインページが再度表示され、エラーメッセージが表示されるという利点があります。

を追加します。 `Login Page Mapping` as

* `/content/sites/engage/en/signin:/content/sites/engage/en`

## オプションの手順 {#optional-steps}

### デフォルトのホームページの変更 {#change-the-default-home-page}

公開サイトをデモ用に使用する場合は、デフォルトのホームページを新しいサイトに変更すると便利です。

そのためには、 [CRXDE](https://localhost:4503/crx/de) を編集するには Lite を使用します。 [resource-mapping](/help/sites-deploying/resource-mapping.md) パブリッシュに関するテーブル。

作業を開始するには：

1. パブリッシュインスタンスで、管理者権限でログインします。
1. 参照先 [https://localhost:4503/crx/de](https://localhost:4503/crx/de).
1. プロジェクトブラウザで、を展開します。 `/etc/map.`
1. を選択します。 `http` ノード：

   * 選択 **ノードを作成：**

      * **名前** localhost.4503 (do) *not* 使用&#39;:&#39;)

      * **タイプ** [sling:Mapping](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)

1. 新しく作成された `localhost.4503` 選択されたノード：

   * プロパティを追加：

   * **名前** sling:match
      * **タイプ** 文字列
      * **値** localhost.4503/$ （「$」文字で終わる必要があります）

   * プロパティを追加：

      * **名前** sling:internalRedirect
      * **タイプ** 文字列
      * **値** /content/sites/engage/en.html

1. 選択 **すべて保存します。**
1. （オプション）閲覧履歴を削除します。
1. https://localhost:4503/を参照します。

   * https://localhost:4503/content/sites/engage/en.htmlに到着します。

>[!NOTE]
>
>無効にするには、 `sling:match` プロパティ値に「x」を付ける — `xlocalhost.4503/$`  — および **すべて保存**.

![optional-steps](assets/optional-steps.png)

#### トラブルシューティング：マップ保存エラー {#troubleshooting-error-saving-map}

変更を保存できない場合は、ノード名が `localhost.4503`（ドット区切り記号を使用し、使用しない） `localhost:4503` 「コロン」区切り文字を使用する場合は、 `localhost`は有効な名前空間のプレフィックスではありません。

![error-message](assets/error-message.png)

#### トラブルシューティング：リダイレクトに失敗 {#troubleshooting-fail-to-redirect}

&#39;**$**&#39; （正規表現の末尾） `sling:match`文字列が重要なので、 `https://localhost:4503/` がマッピングされている場合、リダイレクト値の前に、URL の server:port の後に存在する可能性のある任意のパスが付きます。 したがって、AEMがログインページにリダイレクトしようとすると、失敗します。

### サイトの変更 {#modify-the-site}

サイトが最初に作成された後、作成者は [サイトを開くアイコン](/help/communities/sites-console.md#authoring-site-content) を使用して、標準のAEMオーサリングアクティビティを実行します。

また、管理者は [サイトを編集アイコン](/help/communities/sites-console.md#modifying-site-properties) をクリックして、サイトのプロパティ（タイトルなど）を変更します。

変更後は、次の操作をおこなってください。 **保存** および re **公開** サイト。

>[!NOTE]
>
>AEMに詳しくない場合は、 [基本操作](/help/sites-authoring/basic-handling.md) および [ページのオーサリングのクイックガイド](/help/sites-authoring/qg-page-authoring.md).
