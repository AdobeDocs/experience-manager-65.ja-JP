---
title: 新しいコミュニティサイトの作成
seo-title: 新しいコミュニティサイトの作成
description: 新しい AEM Communities サイトを作成する方法
seo-description: 新しい AEM Communities サイトを作成する方法
uuid: 4f609f5f-ef07-44fc-aeb3-1c616e120d46
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 8ae324ea-8b84-47a3-aabf-1fee2a3bd46d
docset: aem65
exl-id: d4c1895f-421c-4146-b94a-8d11065ef9e3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1661'
ht-degree: 43%

---

# 新しいコミュニティサイトの作成{#author-a-new-community-site}

## コミュニティサイトの作成 {#create-a-community-site}

オーサーインスタンスを使用してコミュニティサイトを作成します。 AEMオーサーインスタンスで、次の操作を実行します。

1. 管理者権限でサインインします。
1. グローバルナビゲーションから、**[!UICONTROL コミュニティ]**/**[!UICONTROL サイト]**&#x200B;に移動します。

コミュニティサイトコンソールでは、コミュニティサイトを作成する手順を案内するウィザードが提供されます。最後の手順でサイトをコミットする前に、`Next`または`Back`を前の手順に進むことができます。

新しいコミュニティサイトの作成を開始するには：

* 「`Create`」ボタンを選択します。

![createcommunitysite](assets/createcommunitysite.png)

### Step 1 : Site Template {#step-site-template}

![サイトを作成するテンプレート](assets/create-site.png)

[「サイトテンプレート」の手順](/help/communities/sites-console.md#step2013asitetemplate)では、URL のタイトル、説明、名前を入力し、コミュニティサイトテンプレートを選択します。次に例を示します。

* **コミュニティサイトのタイトル**: `Getting Started Tutorial`
* **コミュニティサイトの説明**: `A site for engaging with the community.`
* **コミュニティサイトのルート**:(デフォルトのルートの場合は空白のままにし `/content/sites`ます)。
* **クラウド設定**：（クラウド設定が指定されていない場合は空欄のままにする）指定されたクラウド設定へのパスを入力します。
* **コミュニティサイトのベース言語**:（単一の言語に対しては手を加えないでください）。英語)ドロップダウンリストを使用し *て、使用可能な言語(ドイツ語、イタリア語、フランス語、日本語、スペイン語、ポルトガル語（ブラジル）、中国語(繁体* 語)、中国語（簡体字）の中から1つ以上を選択します。追加された言語ごとに1つのコミュニティサイトが作成され、[多言語サイトのコンテンツの翻訳](/help/sites-administering/translation.md)で説明されているベストプラクティスに従って、同じサイトフォルダー内に存在します。 各サイトのルートページには、選択したいずれかの言語の言語コード（例えば、英語では「en」、フランス語では「fr」）で名付けられた子ページが含まれます。

* **コミュニティサイト名**：engage

   * サイトの作成後に名前が容易に変更されないので、名前を再確認します。
   * コミュニティサイト名の下に初期URLが表示されます。
   * 有効なURLに、ベース言語コード+ &quot;.html&quot;を追加する
   * *例：* https://localhost:4502/content/sites/  `engage/en.html`

* **テンプレート**:～を選ぶ  `Reference Site`

* 「**次へ**」を選択します。

### 手順 2：デザイン {#step-design}

デザインの手順は、テーマとブランディングのバナーを選択する2つの節で説明します。

#### コミュニティサイトテーマ {#community-site-theme}

目的のスタイルを選択し、テンプレートに適用します。選択すると、テーマはチェックマークでオーバーレイされます。

#### コミュニティサイトブランディング {#community-site-branding}

（オプション）サイトページ全体に表示するバナー画像をアップロードします。 バナーは、ブラウザーの左端、コミュニティサイトのヘッダーとナビゲーションリンクの間に固定されます。 バナーの高さは 120 ピクセルに切り詰められます。バナーがブラウザーの幅や 120 ピクセルの高さに合わせてリサイズされることはありません。

![community-site-branding](assets/community-site-branding.png)

![upload-image-site](assets/upload-image-site.png)

「**次へ**」を選択します。

### 手順 3：設定 {#step-settings}

設定の手順で`Next`を選択する前に、ユーザー管理、タグ付け、モデレート、グループ管理、分析、翻訳およびイネーブルメントに関する設定にアクセスできる7つのセクションがあることに注意してください。

イネーブルメント機能の使用を体験するには、 [AEM Communities for Enablement](/help/communities/getting-started-enablement.md)の手引きを参照してください。

#### ユーザー管理 {#user-management}

「[ユーザー管理](/help/communities/sites-console.md#user-management)」タブのチェックボックスをすべてオンにします。

* サイト訪問者の自己登録を許可するには
* サイト訪問者がサインインせずにサイトを表示できるようにするには
* メンバーが他のコミュニティメンバーからメッセージを送受信できるようにするには
* プロファイルの登録と作成の代わりにFacebookでのログインを許可するには
* プロファイルの登録と作成の代わりにTwitterでのログインを許可するには

>[!NOTE]
>
>実稼動環境では、カスタムの Facebook アプリケーションおよび Twitter アプリケーションを作成する必要があります。[Facebook と Twitter を使用したソーシャルログイン](/help/communities/social-login.md)を参照してください。

![コミュニティサイトの設定](assets/site-settings.png)

#### タグ付け {#tagging}

コミュニティコンテンツに適用できるタグを制御するには、[タグ付けコンソール](/help/sites-administering/tags.md#tagging-console)で以前に定義したAEM名前空間（[Tutorial namespace](/help/communities/setup.md#create-tutorial-tags)など）を選択します。

名前空間は先行入力検索で簡単に検索できます。例：

* タイプ `tut`
*  `Tutorial`

![tagging](assets/tagging.png)

#### 役割 {#roles}

[コミュニティメ](/help/communities/users.md) ンバーの役割は、役割セクションの設定を使用して割り当てられます。

コミュニティメンバー（またはメンバーのグループ）がコミュニティマネージャーとしてサイトを体験するには、先頭入力検索を使用して、ドロップダウンのオプションからメンバーまたはグループ名を選択します。

例：

* タイプ `q`
* [Quinn Harper](/help/communities/enablement-setup.md#publishcreateenablementmembers)を選択します。

>[!NOTE]
>
>[トンネル](https://helpx.adobe.com/experience-manager/6-3/help/communities/deploy-communities.html#tunnel-service-on-author) サービスを使用すると、パブリッシュ環境にのみ存在するメンバーとグループを選択できます。

![新しいサイトでのユーザーの役割](assets/site-admin-1.png)

#### モデレート {#moderation}

[モデレート](/help/communities/sites-console.md#moderation)ユーザー生成コンテンツ(UGC)のデフォルトのグローバル設定を受け入れます。

![モデレート](assets/moderation1.png)

#### ANALYTICS {#analytics}

Adobe Analytics のライセンスを持っていて、Analytics のクラウドサービスおよびフレームワークが設定されている場合は、Analytics を有効にしてフレームワークを選択できます。

[コミュニティ機能のための Analytics の設定](/help/communities/analytics.md)を参照してください。

![分析](assets/analytics.png)

#### 翻訳 {#translation}

[翻訳設定](/help/communities/sites-console.md#translation)では、サイトの基本言語に加えて、UGC の翻訳を許可するかどうかと、どの言語に翻訳するかを指定します。

* 「**機械翻訳を許可**」をオンにします。
* デフォルトの機械翻訳サービスで翻訳用に選択されたデフォルトの言語をそのままにします
* デフォルトの翻訳プロバイダーと設定をそのまま使用
* 言語コピーがないので、グローバルストアは不要です
* **ページ全体を翻訳**&#x200B;を選択します。
* デフォルトの永続性オプションを維持

![translation-settings](assets/translation-settings.png)

#### イネーブルメント {#enablement}

エンゲージメントコミュニティを作成する場合は空白のままにします。

[イネーブルメントコミュニティ](/help/communities/overview.md#enablement-community)をすばやく作成する方法のチュートリアルについて詳しくは、[イネーブルメントのための AEM Communities 使用の手引き](/help/communities/getting-started-enablement.md)を参照してください。

「**次へ**」を選択します。

![有効化](assets/enablement.png)

### 手順 4：コミュニティサイトの作成 {#step-create-communities-site}

「**作成**」を選択します。

![create-site](assets/create-site2.png)

プロセスが完了すると、新しいサイトのフォルダーがコミュニティサイトコンソールに表示されます。

![communitiessitesconsole](assets/communitiessitesconsole.png)

## コミュニティサイト{#publish-the-community-site}を公開します。

作成したサイトは、コミュニティ - サイトコンソールで管理する必要があります。このコンソールは、新しいサイトを作成するコンソールと同じものです。

コミュニティサイトのフォルダーを選択して開いた後、サイトアイコンにマウスカーソルを合わせると 4 つのアクションアイコンが表示されます。

![siteactionicons-1](assets/siteactionicons-1.png)

4つ目の省略記号アイコン（その他のアクション）を選択すると、「サイトを書き出し」および「サイトを削除」オプションが表示されます。

![siteactionsnew-1](assets/siteactionsnew-1.png)

各アイコンの機能は次のとおりです（左から右の順に説明）。

* **サイトを開く**

   鉛筆アイコンを選択すると、コミュニティサイトがオーサリング編集モードで開き、ページコンポーネントの追加や設定をおこなえます。

* **サイトを編集**

   プロパティアイコンを選択してコミュニティサイトを開き、タイトルやテーマの変更などのプロパティを変更します。

* **サイトを公開**

   世界のアイコンを選択してコミュニティサイトを公開します（例えば、パブリッシュサーバーがローカルマシンで実行されている場合は、デフォルトでlocalhost:4503に公開されます）。

* **サイトを書き出し**

   書き出しアイコンを選択して、コミュニティサイトのパッケージを作成します。このパッケージが、[パッケージマネージャー](/help/sites-administering/package-manager.md)に格納され、ダウンロード可能になります。UGC はサイトパッケージに含まれていません。

* **サイトを削除**

   **[!UICONTROL コミュニティ/サイトコンソール]**&#x200B;内からコミュニティサイトを削除するには、削除アイコンを選択します。 サイトを削除すると、UGC やユーザーグループ、アセット、データベースレコードなど、そのサイトに関連付けられているアイテムがすべて削除されます。

![siteactions](assets/siteactions.png)

>[!NOTE]
>
>パブリッシュインスタンスにデフォルトポートの 4503 を使用していない場合は、デフォルトのレプリケーションエージェントを編集し、ポート番号を正しい値に設定します。
>
>オーサーインスタンスで、メインメニューから：
>
>1. **[!UICONTROL ツール]** / **[!UICONTROL 操作]** / **[!UICONTROL レプリケーション]**&#x200B;メニューに移動します。
>1. 「**[!UICONTROL 作成者のエージェント]**」を選択します。
>1. 「**[!UICONTROL デフォルトエージェント(publish)]**」を選択します。
>1. 「**[!UICONTROL 設定]**」の横にある「**[!UICONTROL 編集]**」を選択します。
>1. エージェント設定のポップアップダイアログで、「**[!UICONTROL Transport]**」タブを選択します。
>1. URIで、ポート番号4503を目的のポート番号に変更します。 例えば、ポート6103を使用するには、次のようにします。https://localhost:6103/bin/receive?sling:authRequestLogin=1
>1. 「**[!UICONTROL OK]**」を選択します。
>1. （オプション）「**[!UICONTROL クリア]**」または「**[!UICONTROL 再試行を強制]**」を選択して、レプリケーションキューをリセットします。


### サイトの公開 {#select-publish}

公開サーバーが実行中であることを確認したら、地球のアイコンを選択して、コミュニティサイトを公開します。

![publish-site](assets/publish-site.png)

コミュニティサイトが正常に公開されると、「サイトが公開されました」というメッセージが短時間表示されます。

### 新しいコミュニティユーザーグループ{#new-community-user-groups}

新しいコミュニティサイトとともに、新しいユーザーグループが作成されます。各グループには、様々な管理機能に応じて適切な権限が設定されています。詳しくは、[コミュニティサイトのユーザーグループ](/help/communities/users.md#usergroupsforcommunitysites)を参照してください。

この新しいコミュニティサイトでは、手順 1 で「engage」というサイト名を指定したので、[グループコンソール](/help/communities/members.md)（グローバルナビゲーション：コミュニティ／グループ）で以下に示す 4 つの新しいユーザーグループを確認できます。

* コミュニティEngageコミュニティマネージャー
* コミュニティEngageグループ管理者
* コミュニティ Engage メンバー
* コミュニティ Engage モデレーター
* コミュニティEngageの権限を持つメンバー
* Community Engageサイトコンテンツマネージャー

[Aaron McDonald](/help/communities/tutorials.md#demo-users)は

* コミュニティEngageコミュニティマネージャー
* コミュニティ Engage モデレーター
* コミュニティ Engage メンバー（モデレーターグループのメンバーとして間接的に）

![user-group](assets/user-group.png)

#### https://localhost:4503/content/sites/engage/en.html {#http-localhost-content-sites-engage-en-html}

![関与する](assets/engage.png)

## 認証エラーの設定 {#configure-for-authentication-error}

サイトが設定され、パブリッシュにプッシュされたら、パブリッシュインスタンス上で[ログインマッピング](/help/communities/sites-console.md#configure-for-authentication-error)(`Adobe Granite Login Selector Authentication Handler`)を設定します。 ログイン資格情報が正しく入力されない場合、認証エラーによってコミュニティサイトのログインページが再表示され、エラーメッセージが表示されるという利点があります。

`Login Page Mapping`を

* `/content/sites/engage/en/signin:/content/sites/engage/en`

## オプションの手順 {#optional-steps}

### デフォルトのホームページの変更 {#change-the-default-home-page}

公開サイトをデモ目的で操作するときは、デフォルトのホームページを新しいサイトに変更すると便利です。

そのためには、[CRXDE](https://localhost:4503/crx/de) Liteを使用して、パブリッシュ環境で[リソースマッピング](/help/sites-deploying/resource-mapping.md)テーブルを編集する必要があります。

作業を開始するには：

1. パブリッシュインスタンスで、管理者権限でログインします。
1. [https://localhost:4503/crx/de](https://localhost:4503/crx/de)を参照します。
1. プロジェクトブラウザで、`/etc/map.`を展開します。
1. `http`ノードを選択します。

   * **ノードを作成**&#x200B;を選択します。

      * **** Namelocalhost.4503 (&#39;:&#39; ** は使用しない)

      * **** [型：マッピング](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)

1. 新しく作成された`localhost.4503`ノードを選択した状態：

   * プロパティの追加：

   * **名前**：sling:match
      * **タイプ**：String
      * **** Valuelocalhost.4503/$（「$」文字で終わる必要があります）
   * プロパティの追加：

      * **名前**：sling:internalRedirect
      * **タイプ**：String
      * **値**：/content/sites/engage/en.html


1. 「**すべて保存**」を選択します。
1. （オプション）閲覧履歴を削除します。
1. https://localhost:4503/を参照します。

   * https://localhost:4503/content/sites/engage/en.htmlにアクセスします。

>[!NOTE]
>
>無効にするには、`sling:match`プロパティの値の先頭に「x」、「&lt;a1/」、「**すべて保存**」を付けます。`xlocalhost.4503/$`

![optional-steps](assets/optional-steps.png)

#### トラブルシューティング：マップ保存エラー {#troubleshooting-error-saving-map}

変更を保存できない場合は、ノード名が`localhost.4503`で、区切り文字が「ドット」であることを確認し、区切り文字が「コロン」でないことを確認してください。`localhost`は有効な名前空間プレフィックスではありません。`localhost:4503`

![error-message](assets/error-message.png)

#### トラブルシューティング：リダイレクト失敗 {#troubleshooting-fail-to-redirect}

正規表現`sling:match`文字列の末尾にある「**$**」は重要なので、正確に`https://localhost:4503/`のみがマッピングされます。そうでない場合、リダイレクト値には、URLのserver:portの後に存在する任意のパスのプレフィックスが付きます。 したがって、AEMがログインページにリダイレクトしようとすると、失敗します。

### サイトの変更 {#modify-the-site}

サイトを最初に作成した後、作成者は[サイトを開くアイコン](/help/communities/sites-console.md#authoring-site-content)を使用して、標準的な AEM のオーサリングアクティビティを実行できます。

また、管理者は[サイトを編集アイコン](/help/communities/sites-console.md#modifying-site-properties)を使用して、タイトルなどのサイトプロパティを変更できます。

変更後は、必ず&#x200B;**保存**&#x200B;して再&#x200B;**公開**&#x200B;してください。

>[!NOTE]
>
>AEM に馴染みがない場合は、[基本操作](/help/sites-authoring/basic-handling.md)に関するドキュメントおよび[ページのオーサリングのクイックガイド](/help/sites-authoring/qg-page-authoring.md)を参照してください。
