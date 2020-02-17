---
title: イネーブルメントのための新しいコミュニティサイトの作成
seo-title: イネーブルメントのための新しいコミュニティサイトの作成
description: イネーブルメントのためのコミュニティサイトの作成
seo-description: イネーブルメントのためのコミュニティサイトの作成
uuid: a75fa566-a570-45fd-aabc-23651ef819cc
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: b9333558-6af9-46b2-9f03-3722645c69a6
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# イネーブルメントのための新しいコミュニティサイトの作成{#author-a-new-community-site-for-enablement}

## コミュニティサイトを作成 {#create-community-site}

[コミュニティサイトの作成](/help/communities/sites-console.md) (Community Site Creation)では、コミュニティサイトの作成手順を案内するウィザードを使用します。 It is possible to move forward to the `Next`step or `Back`to the previous step before committing the site in the final step.

新しいコミュニティサイトの作成を開始するには：

[オーサーインスタンス](https://localhost:4502/)を使用します。

* 管理者権限でサインインします。
* navigate to **Communities,** **Sites**

* 「**作成**」を選択します。

### 手順 1：サイトテンプレート {#step-site-template}

![有効化サイトテンプレート](assets/enablement-site-template.png)

「**サイトテンプレート**」の手順では、URL のタイトル、説明、名前を入力し、コミュニティサイトテンプレートを選択します。次に例を示します。

* **コミュニティサイトのタイトル**: `Enablement Tutorial`

* **コミュニティサイトの説明**: `A site for enabling the community to learn.`

* **コミュニティサイトのルート**:(デフォルトのルートの場合は空白のままにし `/content/sites`ます)。

* **クラウド設定**：（クラウド設定が指定されていない場合は空欄のままにする）指定されたクラウド設定へのパスを入力します。
* **コミュニティサイトの基本言語**:(単一言語の場合は手を付けないでください。英語)ドロップダウンを使用して ** 、使用可能な言語(ドイツ語、イタリア語、フランス語、日本語、スペイン語、ポルトガル語（ブラジル）、中国語（繁体字）、中国語（簡体字）)から1つ以上のベース言語を選択します。 One community site will be created for each language added, and will exist within the same site folder following the best practice described in [Translating Content for Multilingual Sites](/help/sites-administering/translation.md). 各サイトのルートページには、選択したいずれかの言語の言語コード（例えば、英語では「en」、フランス語では「fr」）で名付けられた子ページが含まれます。

* **コミュニティサイト名**: `enable`

   * 初期 URL は、コミュニティサイト名の下に表示されます。
   * 有効な URL に、ベース言語コード + 「.html」を追加します。
      *例えば*、https://localhost:4502/content/sites/ `enable/en.html`

* **リファレンスサイトテンプレート**:引っ張って選ぶ `Reference Structured Learning Site Template`

「**次へ**」を選択します。

### 手順 2：デザイン {#step-design}

デザインの手順は、テーマとブランディングバナーを選択するための2つのセクションで示されます。

#### コミュニティサイトテーマ {#community-site-theme}

目的のスタイルを選択し、テンプレートに適用します。選択すると、テーマはチェックマーク付きでオーバーレイされます。

#### コミュニティサイトブランディング {#community-site-branding}

（オプション）サイトページに表示するバナー画像をアップロードします。バナーはブラウザーの左端およびコミュニティサイトヘッダーとメニュー（ナビゲーションリンク）の間に固定されます。バナーの高さは 120 ピクセルに切り詰められます。バナーがブラウザーの幅や 120 ピクセルの高さに合わせてリサイズされることはありません。

![chlimage_1-2](assets/chlimage_1-2.png) ![chlimage_1](assets/chlimage_1.jpeg)

「**次へ**」を選択します。

### 手順 3：設定 {#step-settings}

On the Settings step, before selecting `Next`, notice there are seven sections providing access to configurations involving user management, tagging, roles, moderation, analytics, translation, and enablement.

#### ユーザー管理 {#user-management}

It is recommended that [enablement communities](/help/communities/overview.md#enablement-community) be private.

コミュニティサイトを非公開にするとは、匿名のサイト訪問者に対してアクセスを拒否し、自己登録やソーシャルログインを使用禁止にすることです。

Ensure most checkboxes are deselected for [User Management](/help/communities/sites-console.md#user-management) :

* サイト訪問者の自己登録を禁止します。
* 匿名のサイト訪問者によるサイト表示を禁止します。
* コミュニティメンバー間のメッセージングを許可するかどうかは任意とします。
* Facebook を使用したログインを禁止します。
* Twitter を使用したログインを禁止します。

![chlimage_1-3](assets/chlimage_1-3.png)

#### タグ付け {#tagging}

The tags which may be applied to community content are controlled by selecting AEM namespaces previously defined through the [Tagging Console](/help/sites-administering/tags.md#tagging-console) (such as the [Tutorial namespace](/help/communities/enablement-setup.md#create-tutorial-tags)).

また、コミュニティサイトに対してタグ名前空間を選択すると、カタログとイネーブルメントリソースを定義するときに表示される選択肢が制限されます。See [Tagging Enablement Resources](/help/communities/tag-resources.md) for important information.

名前空間は先行入力検索で簡単に検索できます。例：

* 「tut」と入力します
* select `Tutorial`

![chlimage_1-4](assets/chlimage_1-4.png)

### 役割 {#roles}

[コミュニティメンバの役割は](/help/communities/users.md) 、[役割]セクションの設定を通じて割り当てられます。

コミュニティメンバー（またはメンバーのグループ）がコミュニティマネージャーとしてサイトを体験できるようにするには、先読み検索を使用し、ドロップダウンのオプションからメンバー名またはグループ名を選択します。

例：

* 「q」と入力します。
* 「[Quinn Harper](/help/communities/enablement-setup.md#publishcreateenablementmembers)」を選択します。

>[!NOTE]
>
>[トンネルサービス](/help/communities/deploy-communities.md#tunnel-service-on-author) では、パブリッシュ環境にのみ存在するメンバーとグループを選択できます。

![実施可能な役割](assets/site-admin.png)

#### モデレート {#moderation}

ユーザー生成コンテンツ（UGC）を[モデレート](/help/communities/sites-console.md#moderation)する場合は、デフォルトのグローバル設定を受け入れます。

![chlimage_1-5](assets/chlimage_1-5.png)

#### Analytics {#analytics}

ドロップダウンから、このコミュニティサイト用に設定されたAnalyticsクラウドサービスフレームワークを選択します。

スクリーンショットに表示されている選択肢「`Communities`」は、[設定ドキュメント](/help/communities/analytics.md#aem-analytics-framework-configuration)のフレームワークの例です。

![chlimage_1-6](assets/chlimage_1-6.png)

#### TRANSLATION {#translation}

[翻訳設定](/help/communities/sites-console.md#translation)では、UGC の翻訳を許可するかどうかと、どの言語に翻訳するかを指定します。

* 「**機械翻訳を許可**」をオンにします。
* デフォルト設定を使用します。

![chlimage_1-7](assets/chlimage_1-7.png)

#### イネーブルメント {#enablement}

1 つのイネーブルメントコミュニティに対し、1 人以上のコミュニティ実施可能マネージャーを指定する必要があります。

* **有効化マネージャ**（必須）グループのメンバーを `Community Enablement Managers` 選択して、このコミュニティサイトを管理できます。

   * 「s」と入力します。
   * select `Sirius Nilson`

* **Marketing cloud組織ID**（オプション）有効化レポートにビデオハートビート分析を含める [場合に必要なAdobe AnalyticsアカウントのID](/help/communities/analytics.md#video-heartbeat-analytics) 。

![chlimage_1-8](assets/chlimage_1-8.png)

「**次へ**」を選択します。

### 手順 4：コミュニティサイトの作成 {#step-create-community-site}

Select **Create.**

![chlimage_1-9](assets/chlimage_1-9.png)

プロセスが完了すると、新しいサイトのフォルダーがコミュニティサイトコンソールに表示されます。

![enablementsitecreated](assets/enablementsitecreated.png)

### 新しいコミュニティサイトの公開 {#publish-the-new-community-site}

作成したサイトは、コミュニティ - サイトコンソールで管理する必要があります。このコンソールは、新しいサイトを作成するコンソールと同じものです。

コミュニティサイトのフォルダーを選択した後、サイトアイコンにマウスカーソルを合わせると、4 つのアクションアイコンが表示されます。

![siteactionicons](assets/siteactionicons.png)

省略記号アイコン（その他のアクションアイコン）を選択すると、「サイトを書き出し」および「サイトを削除」オプションが表示されます。

![siteactionsnew](assets/siteactionsnew.png)

各アイコンの機能は次のとおりです（左から右の順に説明）。

* **サイトを開く**&#x200B;鉛筆のアイコンを選択すると、コミュニティサイトをオーサリング編集モードで開いて、ページコンポーネントを追加したり設定したりできます。

* **サイトを編集**&#x200B;プロパティアイコンを選択すると、コミュニティサイトを開いて、タイトルなどのプロパティを変更したり、テーマを変更したりできます。

* **サイトを公開**&#x200B;地球のアイコンを選択すると、コミュニティサイトが（デフォルトでは localhost:4503 に）公開されます。

* **サイトを書き出し**&#x200B;書き出しアイコンを選択すると、コミュニティサイトのパッケージが作成され、[パッケージマネージャー](/help/sites-administering/package-manager.md)に保存されて、ダウンロードされます。UGC はサイトパッケージに含まれていません。

* **サイトを削除**&#x200B;コミュニティサイトを削除するには、サイトを削除アイコンを選択します。このアイコンは、コミュニティサイトコンソール内でサイトにマウスポインターを置くと表示されます。サイトを削除すると、UGC やユーザーグループ、アセット、データベースレコードなど、そのサイトに関連付けられているアイテムがすべて削除されます。

![enablesiteactions](assets/enablesiteactions.png)

#### サイトの公開 {#select-publish}

地球のアイコンを選択して、コミュニティサイトを公開します。

![chlimage_1-10](assets/chlimage_1-10.png)

サイトが公開されると、次のようなメッセージが表示されます。

![chlimage_1-11](assets/chlimage_1-11.png)

## コミュニティのユーザーとユーザーグループ {#community-users-user-groups}

### 新しいコミュニティユーザーグループの確認 {#notice-new-community-user-groups}

新しいコミュニティサイトとともに、新しいユーザーグループが作成されます。各グループには、様々な管理機能に応じて適切な権限が設定されています。For details, visit [User Groups for Community Sites](/help/communities/users.md#usergroupsforcommunitysites).

For this new community site, given the site name &quot;enable&quot; in Step 1, the new user groups that exist in the publish environment may be seen from the [Communities Members &amp; Groups console](/help/communities/members.md#groups-console) :

![chlimage_1-12](assets/chlimage_1-12.png)

### 「Community Enable Members」グループへのメンバー割り当て{#assign-members-to-community-enable-members-group}

On author, with the tunnel service enabled, it is possible to assign the [users created during Initial Setup](/help/communities/enablement-setup.md#publishcreateenablementmembers) to the Community Members group for the newly created community site.

コミュニティグループコンソールでは、メンバーを個別に追加したり、グループのメンバーシップを使用して追加したりできます。

In this example, the group `Community Ski Class` is added as a member of the group `Community Enable Members` as well as member `Quinn Harper`.

* **コミュニティ／グループ**&#x200B;コンソールに移動します。
* select *Community Enable Members* group
* 「**メンバーをグループに追加**」検索ボックスに「ski」と入力します。
* select *Community Ski Class* (group of learners)
* 検索ボックスに「quinn」と入力します。
* 「*Quinn Harper*」（イネーブルメントリソース連絡先）を選択します。

* 「**保存**」を選択します。

![chlimage_1-13](assets/chlimage_1-13.png)

## パブリッシュ側の設定 {#configurations-on-publish}

`https://localhost:4503/content/sites/enable/en.html {#http-localhost-content-sites-enable-en-html}`

![chlimage_1-14](assets/chlimage_1-14.png)

### 認証エラーの設定 {#configure-for-authentication-error}

Once a site has been configured and pushed to publish, [configure login mapping](/help/communities/sites-console.md#configure-for-authentication-error) ( `Adobe Granite Login Selector Authentication Handler`) on the publish instance. ログイン資格情報が正しく入力されない場合、認証エラーはコミュニティサイトのログインページを再表示し、エラーメッセージが表示されるという利点があります。

名前を付けて `Login Page Mapping` 追加

* `/content/sites/enable/en/signin:/content/sites/enable/en`

### （オプション）デフォルトのホームページの変更{#optional-change-the-default-home-page}

公開サイトをデモ目的で操作するときは、デフォルトのホームページを新しいサイトに変更すると便利です。

これをおこなうには、[CRX|DE](https://localhost:4503/crx/de) Lite を使用して、パブリッシュ側で[リソースマッピング](/help/sites-deploying/resource-mapping.md)テーブルを編集します。

開始するには、次のようにします。

1. 公開時に CRXDE にアクセスし、管理者権限を使用してサインインします

   * 例えば、https://localhost:4503/crx/deを参照し [て](https://localhost:4503/crx/de) 、 `admin/admin`

1. in the project browser, expand `/etc/map`
1. select the `http` node

   * 「**ノードを作成**」を選択します。

      * **名前** localhost.4503

         (do *not* use &#39;:&#39;)

      * **Type** [sling:Mapping](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)

1. with newly created `localhost.4503` node selected

* プロパティを追加します。

   * **名前**：sling:match
   * **タイプ**：String
   * **値**：localhost.4503/$

      （「$」文字で終わる必要があります）

* プロパティを追加します。

   * **名前**：sling:internalRedirect
   * **タイプ**：String
   * **値**：/content/sites/enable/en.html

1. 「**すべて保存**」を選択します。
1. （オプション）ブラウジング履歴を削除します。
1. https://localhost:4503/を参照します。

* https://localhost:4503/content/sites/enable/en.htmlに到着する

>[!NOTE]
>
>To disable, simply pre-pend the `sling:match` property value with an &#39;x&#39; - `xlocalhost.4503/$` - and **Save All**.

![chlimage_1-15](assets/chlimage_1-15.png)

#### トラブルシューティング：マップ保存エラー {#troubleshooting-error-saving-map}

変更を保存できない場合は、ノード名が `localhost.4503`（区切り文字が「ドット」）となっているかを確認してください。`localhost:4503` は有効な名前空間のプレフィックスではないので、`localhost`（区切り文字が「コロン」）という表記は正しくありません。

![chlimage_1-16](assets/chlimage_1-16.png)

#### トラブルシューティング：リダイレクト失敗 {#troubleshooting-fail-to-redirect}

The &#39;**$**&#39; at the end of the regular expression `sling:match`string is crucial, so that only exactly `https://localhost:4503/` is mapped, else the redirect value is prepended to any path that might exist after the server:port in the URL. したがって、AEMがログインページにリダイレクトしようとすると失敗します。

## コミュニティサイトの変更 {#modifying-the-community-site}

サイトを最初に作成した後、作成者は[サイトを開くアイコン](/help/communities/sites-console.md#authoring-site-content)を使用して、標準的な AEM のオーサリングアクティビティを実行できます。

また、管理者は[サイトを編集アイコン](/help/communities/sites-console.md#modifying-site-properties)を使用して、タイトルなどのサイトプロパティを変更できます。

変更後は、必ず&#x200B;**保存**&#x200B;して再&#x200B;**公開**&#x200B;してください。

>[!NOTE]
>
>AEM に馴染みがない場合は、[基本操作](/help/sites-authoring/basic-handling.md)に関するドキュメントおよび[ページのオーサリングのクイックガイド](/help/sites-authoring/qg-page-authoring.md)を参照してください。

### カタログの追加 {#add-a-catalog}

このコミュニティサイトに選択されたコミュニティサイトテンプレートには、カタログ機能が含まれています。

含まれていない場合は、カタログ機能を簡単に追加できます。これにより、イネーブルメントリソースや学習パスに割り当てられていないコミュニティの他のメンバーが、カタログからイネーブルメントリソースを選択できるようになります。

サイト構造にカタログ機能が既に含まれている場合、タイトルが変わることがあります。

To modify the site&#39;s structure, navigate to the **Communities, Sites** console, open the `enable` folder, and select the **Edit Site **icon to access the properties of `Enablement Tutorial`.

構造パネルを選択し、カタログを追加するか、既存のカタログを変更します。

* **タイトル**: `Ski Catalog`

* **URL**: `catalog`

* **すべての名前空間を選択**：デフォルトのままにします。
* 「**Save**」を選択します。

![chlimage_1-17](assets/chlimage_1-17.png)

位置アイコンを使用し、カタログ機能を Assignments の後の 2 番目の位置に移動します。

![chlimage_1-18](assets/chlimage_1-18.png)

右上隅の「**保存**」を選択してコミュニティサイトに対する変更を保存します。

その後、サイトを再び&#x200B;**公開**&#x200B;します。

