---
title: コミュニティサイトコンソール
seo-title: コミュニティサイトコンソール
description: コミュニティサイトコンソールにアクセスする方法
seo-description: コミュニティサイトコンソールにアクセスする方法
uuid: 74134281-244c-40da-a941-7f2f3e706d4b
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 4130f952-5bb5-4e32-91d6-47b2885b30a4
docset: aem65
role: Administrator
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '3292'
ht-degree: 46%

---


# コミュニティサイトコンソール {#communities-sites-console}

コミュニティサイトコンソールでは、次の機能にアクセスできます。

* サイトの作成
* サイト編集
* サイト管理
* [ネストされたグループの作成と編集](/help/communities/groups.md) （サブコミュニティ）

オーサー環境で素早くコミュニティサイトを作成する方法や、オーサー環境とパブリッシュ環境からコミュニティグループを作成する方法については、[AEM Communities 使用の手引き](/help/communities/getting-started.md)を参照してください。

>[!NOTE]
>
>[コミュニティサイト](/help/communities/sites-console.md)、[コミュニティサイトテンプレート](/help/communities/sites.md)、[コミュニティグループテンプレート](/help/communities/tools-groups.md)、[コミュニティ機能](/help/communities/functions.md)の作成に使用する主なコミュニティメニューは、オーサー環境でのみ使用します。

## 前提条件 {#prerequisites}

コミュニティサイトを作成する前に、以下の手順をおこなう必要があります。**：

* 1つ以上のパブリッシュインスタンスが実行されていることを確認します。
* [トンネルサービス](/help/communities/deploy-communities.md#tunnel-service-on-author)を有効にして、メンバーとメンバーグループを管理します。
* [プライマリパブリッシャー](/help/communities/deploy-communities.md#primary-publisher)を特定します。
* [プライマリパ](/help/communities/deploy-communities.md#replication-agents-on-author) ブリッシャーポートがデフォルト(4503)でない場合は、レプリケーションを構成します。

サイトで様々な機能がサポートされるよう確実に準備するために、次の手順を実行することをお勧めします。

* [最新の機能パック](/help/communities/deploy-communities.md#latestfeaturepack)をインストールします。
* AEM Communitiesの[Adobe Analytics](/help/communities/analytics.md)を有効にします。
* [email](/help/communities/email.md)を設定します
* [コミュニティ管理者](/help/communities/users.md#creating-community-members)を特定します。
* [ソーシャルログイ](/help/communities/social-login.md#adobe-granite-oauth-authentication-handler) ン用にOAuthハンドラーを有効にします。

## コミュニティサイトコンソールへのアクセス {#accessing-communities-sites-console}

オーサー環境でコミュニティサイトコンソールにアクセスするには、次の手順を実行します。

* グローバルナビゲーションから：**[!UICONTROL コミュニティ]** > **[!UICONTROL サイト]**

コミュニティサイトコンソールには、既存のコミュニティサイトが表示されます。このコンソールから、コミュニティサイトを作成、編集、管理および削除できます。

新しいコミュニティサイトを作成するには、**作成**&#x200B;アイコンを選択します。

ネストされたグループのオーサリング、変更、公開、書き出しまたは追加をおこなうために既存のコミュニティサイトにアクセスするには、サイトのフォルダーアイコンを選択します。

例えば、次の画像は、2つのコミュニティサイト用のフォルダーを表示するメインのコミュニティサイトコンソールを示しています。[enable](/help/communities/getting-started-enablement.md)と[engage](/help/communities/getting-started.md):

![site-console](assets/site-console.png)

## サイト作成 {#site-creation}

サイト作成コンソールでは、選択した[コミュニティサイトテンプレート](/help/communities/sites.md)と設定に基づき、サイトの機能を段階的に組み立てることができます。

作成されるサイトには、いずれもログイン機能が含まれます。これは、サイト訪問者がコンテンツの投稿、メッセージの送信またはグループへの参加をおこなう前に、サインインする必要があるからです。その他の機能には、ユーザープロファイル、メッセージング、通知、サイトメニュー、検索、テーマ、ブランディングが含まれます。

コミュニティサイトコンソールの上部にある「`Create`」ボタンを選択すると、プロセスが開始されます。

作成プロセスでは、一連の手順がパネル形式で表示されます。パネルには、設定する機能セット（サブパネルとして表示）が含まれています。最後の手順でサイトをコミットする前に、**次の**&#x200B;または&#x200B;**前の手順に戻る**&#x200B;を選択できます。

### Step 1 : Site Template {#step-site-template}

![newsitetemplate](assets/newsitetemplate.png)

サイトテンプレートパネルでは、タイトル、説明、サイトのルート、ベース言語、名前およびサイトテンプレートを指定します。

* **コミュニティサイトのタイトル**

   サイトの表示タイトル。

   タイトルは、公開済みサイトとサイト管理UIに表示されます。

* **コミュニティサイトの説明**

   サイトの説明。

   この説明は、公開済みのサイトには表示されません。

* **コミュニティサイトのルート**

   サイトのルートパス。

   デフォルトのルートは`/content/sites`ですが、ルートはWebサイト内の任意の場所に移動できます。

* **コミュニティサイトのベース言語**

   (単一の言語の場合は手を付けないでおきます。英語)プルダウンメニューを使用して、ドイツ語、イタリア語、フランス語、日本語、スペイン語、ポルトガル語（ブラジル）、中国語（繁体字）、中国語（簡体字）の1つ以上の&#x200B;*ベース言語を選択します。*&#x200B;追加された言語ごとに1つのコミュニティサイトが作成され、[多言語サイトのコンテンツの翻訳](/help/sites-administering/translation.md)で説明されているベストプラクティスに従って、同じサイトフォルダー内に存在します。 各サイトのルートページには、選択したいずれかの言語の言語コード（例えば、英語では「en」、フランス語では「fr」）で名付けられた子ページが含まれます。

* **コミュニティサイト名**:

   URLに表示されるサイトのルートページの名前。

   * サイトの作成後に名前が簡単に変更されないので、名前を再度確認します。
   * ベースURL( `https://server:port/site root/site name)` )が`Community Site Name`の下に表示されます。

   * 有効なURLに、ベース言語コード+ &quot;.html&quot;を追加する

      *例：*  `https://localhost:4502/content/sites/mysight/en.html`

* **コミュニティサイトテンプレ** ートメニュー

   プルダウンメニューを使用して、利用可能な[コミュニティサイトテンプレート](/help/communities/tools.md)を選択します。

* 「**次へ**」を選択します。

### 手順 2：デザイン {#step-design}

デザインパネルには、テーマとブランドバナーを選択するための、以下の 2 つのサブパネルが含まれています。

#### コミュニティサイトテーマ {#community-site-theme}

![sitetheme](assets/sitetheme.png)

このフレームワークでは、レスポンシブで柔軟なサイトデザインを実現できるよう、[Twitter Bootstrap](https://twitterbootstrap.org/) を使用しています。プリロードされた多数のBootstrapテーマの1つを選択して、選択したコミュニティサイトテンプレートのスタイルを設定したり、Bootstrapテーマをアップロードしたりできます。

選択すると、テーマの上に不透明な青色のチェックマークのオーバーレイが表示されます。

コミュニティサイトの公開後は、[プロパティを編集](#modifying-site-properties)し、別のテーマを選択できます。

#### コミュニティサイトブランディング  {#community-site-branding}

![サイトブランディング](assets/site-branding.png)

コミュニティサイトブランディングとは、各ページ上部にヘッダーとして表示される画像のことです。

画像の幅は、予想されるブラウザー内でのページの表示に合わせます。画像の高さは 120 ピクセルにします。

画像を選択するときは、次の点に注意してください。

* 画像の高さは、画像の上端から120ピクセルに切り抜かれます。
* 画像は、ブラウザーウィンドウの左端に固定されます。
* 画像の幅が次の場合に、画像のサイズは変更されません。

   * ブラウザーの幅より小さい場合、画像は水平方向に繰り返されます。
   * ブラウザーの幅より大きい場合、画像は切り抜かれたように見えます。

* 「**次へ**」を選択します。

### 手順 3：設定  {#step-settings}

設定パネルには複数のサブパネルが含まれています。各サブパネルに表示される機能を設定した後に、サイト作成の最後の手順に進みます。

* [ユーザー管理](#user-management)
* [タグ付け](#tagging)
* [役割](#roles)
* [モデレート](#moderation)
* [Analytics ](#analytics)
* [翻訳](#translation)
* [イネーブルメント](#enablement)

>[!NOTE]
>
>**トンネルサービスの有効化**
>
>いくつかの設定サブパネルでは、信頼されているメンバーを、UGC のモデレーター、グループの管理者またはパブリッシュ環境でのイネーブルメントリソースの連絡先に割り当てることができます。
>
>慣例は、パブリッシュ側の[ユーザーとユーザーグループ](/help/communities/users.md)（メンバーとメンバーグループ）がオーサー環境で複製されないようにするためです。
>
>したがって、オーサー環境でコミュニティサイトを作成し、信頼されているメンバーを様々な役割に割り当てる場合は、パブリッシュ環境からメンバーのデータを取得する必要があります。
>
>これは、オーサー環境で` [AEM Communities Publish Tunnel Service](/help/communities/deploy-communities.md#tunnel-service-on-author)`を有効にすることで実現されます。

#### ユーザー管理 {#user-management}

![createsitesettings](assets/createsitesettings.png)

>[!NOTE]
>
>[イネーブルメントコミュニティサイト](/help/communities/overview.md#enablement-community)は非公開にすることをお勧めします（詳しくは、アカウント担当者にお問い合わせください）。
>
>コミュニティサイトを非公開にするとは、匿名のサイト訪問者に対してアクセスを拒否し、自己登録やソーシャルログインを使用禁止にすることです。

* **ユーザー登録を許可**

   オンにすると、サイト訪問者は自己登録によってコミュニティメンバーになる場合があります。
オフにすると、コミュニティサイトは*制限*され、サイト訪問者はコミュニティサイトのメンバーグループに割り当てられ、リクエストを行うか、電子メールで招待が送信されます。 オフにすると、匿名アクセスは許可されません。
非公開のコミュニティサイトの場合はオフにします。**&#x200B;初期設定はオンです。

* **匿名アクセスを許可**

   オンにすると、コミュニティサイトは「オープン」になり、サイト訪問者は誰でもサイトにアクセスできます。
オフにすると、サインイン済みのメンバーのみがサイトにアクセスできます。非公開のコミュニティサイトの場合はオフにします。 初期設定はオンです。

* **メッセージを許可**

   オンにすると、メンバーは互いにメッセージを送信し、コミュニティサイト内のグループにメッセージを送信できます。
オフにすると、コミュニティのメッセージング機能は設定されません。初期設定はオフです。

* **ソーシャルログインを許可 : Facebook**

   オンにすると、サイト訪問者はFacebookアカウントの資格情報を使用してログインできます。 選択した[Facebookクラウド設定](/help/communities/social-login.md#create-a-facebook-connect-cloud-service)を、コミュニティサイトの作成後にコミュニティサイトのメンバーグループにユーザーを追加するように設定する必要があります。
オフにすると、Facebook ログインは表示されません。非公開のコミュニティサイトの場合はオフのままにします。**&#x200B;初期設定はオフです。

* **ソーシャルログインを許可 : Twitter**

   オンにすると、サイト訪問者はTwitterアカウントの資格情報を使用してログインできます。 選択した[Twitterクラウド設定](/help/communities/social-login.md#create-a-twitter-connect-cloud-service)を、コミュニティサイトの作成後にコミュニティサイトのメンバーグループにユーザーを追加するように設定する必要があります。
オフにすると、Twitter ログインは表示されません。非公開のコミュニティサイトの場合はオフのままにします。**&#x200B;初期設定はオフです。

>[!NOTE]
>
>**ソーシャルログインの許可**
>
>Facebook と Twitter のサンプル設定が存在し、選択可能な場合がありますが、[実稼動環境](/help/sites-administering/production-ready.md)では、カスタム Facebook アプリケーションとカスタム Twitter アプリケーションを作成する必要があります。[Facebook と Twitter を使用したソーシャルログイン](/help/communities/social-login.md)を参照してください。

#### タグ付け {#tagging}

![サイトタグ付け](assets/site-tagging.png)

コミュニティコンテンツに適用できるタグを制御するには、以前に[タグ付けコンソール](/help/sites-administering/tags.md#tagging-console)で定義したタグ名前空間を選択します。

また、コミュニティサイトに対してタグ名前空間を選択すると、カタログとリソースを定義するときに表示される選択肢が制限されます。重要な情報については、[イネーブルメントリソースのタグ付け](/help/communities/tag-resources.md)を参照してください。

* テキスト検索ボックス：入力を開始して、サイトで使用可能なタグを特定します。

#### 役割 {#roles}

![コミュニティの役割](assets/site-admin-2.png)

[コミュニティメンバーの役割](/help/communities/users.md)は、これらの設定で割り当てます。

コミュニティメンバーは先行入力検索で簡単に検索できます。

* **コミュニティマネージャー**

   入力を開始して、コミュニティメンバーとメンバーグループを管理できる1人以上のコミュニティメンバーまたはメンバーグループを選択します。

* **コミュニティのモデレーター**

   入力を開始して、ユーザー生成コンテンツのモデレーターとして信頼される1人以上のコミュニティメンバーまたはメンバーグループを選択します。

* **コミュニティ権限を持つメンバー**

   [コミュニティ機能](/help/communities/functions.md)に対して`Allow Privileged Member`が選択されている場合に、1つ以上のコミュニティメンバーまたはメンバーグループを選択して、新しいコンテンツを作成できます。

* **コミュニティ管理者**

   入力を開始して、他のサイト管理者や既定のコミュニティ管理者とは関係なく、サイト構造を処理できる1人または複数のサイト管理者を選択します。 階層の任意のレベルでグループを作成し、ネストされたグループのデフォルトの管理者になることができます（ただし、後でネストされたグループの管理者の役割から削除することもできます）。

#### モデレート {#moderation}

![site-moderation](assets/site-moderation.png)

ユーザー生成コンテンツ（UGC）のモデレートのグローバル設定は、ここで制御します。個々のコンポーネントには、モデレートを制御するための追加設定があります。

* **コンテンツを事前にモデレート**

   オンにすると、投稿されたコミュニティコンテンツはモデレーターによって承認されるまで表示されません。 初期設定はオフです。詳しくは、[コミュニティコンテンツのモデレート](/help/communities/moderate-ugc.md#premoderation)を参照してください。

* **コンテンツが非表示になるまでのフラグ設定しきい値**

   0より大きい場合は、トピックまたは投稿に何回フラグが設定されたら、公開表示から非表示になります。 -1に設定した場合、フラグ付きのトピックまたは投稿が公開表示で非表示になることはありません。 初期設定は 5 です。

#### Analytics  {#analytics}

![site-analytics](assets/site-analytics.png)

* **Analytics を有効にする**

   Adobe Analyticsがコミュニティ機能用に[設定](/help/communities/analytics.md)されている場合にのみ使用できます。
初期設定はオフです。オンにすると、以下の追加選択メニューが表示されます。

![site-analytics-enable](assets/site-analytics-enable.png)

* **クラウド設定フレームワークの参照**

   プルダウンメニューから、このコミュニティサイト用に設定した Analytics クラウドサービスフレームワークを選択します。
   `Communities` は、コミュニティ機能向けのAnalytics設 [定ドキュメントのフレームワークの](/help/communities/analytics.md#aem-analytics-framework-configuration) 例です。

#### 翻訳 {#translation}

![site-translation](assets/site-translation.png)

* **機械翻訳を許可**

   オン（デフォルトはオフ）にすると、サイト内のUGCに対して機械翻訳が有効になります。 これは、サイトが多言語サイトとして設定されている場合でも、ページコンテンツなどの他のコンテンツには影響しません。 AEM Communities用のライセンス翻訳サービスの設定について詳しくは、[ユーザー生成コンテンツの翻訳](/help/communities/translate-ugc.md)を参照してください。 全体的な概要については、[多言語サイトのコンテンツの翻訳](/help/sites-administering/translation.md)を参照してください。

![allow-machine-translation](assets/allow-machine-translation.png)

* **選択した言語の機械翻訳を有効にする**

   機械翻訳が有効な言語は、[翻訳統合設定](/help/communities/translate-ugc.md#translation-integration-configuration)で指定されたシステム設定にデフォルトで設定されます。 これらのデフォルト設定は、デフォルトを削除したり、プルダウンメニューから他の言語を選択したりすることで、このサイトで上書きできます。

* **変換プロバイダーを選択**

   デフォルトでは、サービスプロバイダーは、デモのみ`microsoft`を使用する体験版サービスです。 翻訳サービスプロバイダーがライセンスされていない場合は、**機械翻訳を許可**&#x200B;をオフにする必要があります。

* **グローバル共有ストアを選択**

   複数の言語コピーがあるWebサイトの場合、グローバル共有ストアは各言語コピーから見える1つのスレッドの会話を提供します。 これを実現するには、言語コピーとして含まれているいずれかの言語を選択します。初期設定は&#x200B;*No Global Shared Store*&#x200B;です。

* **変換プロバイダー設定を選択**

   ライセンスされた翻訳プロバイダー用に作成された[翻訳統合フレームワーク](/help/sites-administering/tc-tic.md)を選択します。

* **コミュニティサイトの翻訳オプションを選択**

   * **ページ全体を翻訳**

      選択すると、ページ上のすべてのUGCがページの基本言語に翻訳されます。

      初期設定では選択されていません。**

   * **選択項目のみ翻訳**

      選択すると、各投稿の横に翻訳オプションが表示され、個々の投稿をページのベース言語に翻訳できます。
初期設定では選択されています。**

* **保持オプションを選択**

   * **ユーザーのリクエストにより貢献度を翻訳し、その後保持する**&#x200B;選択すると、リクエストがあるまでコンテンツは翻訳されません。翻訳後、翻訳はリポジトリに保存されます。

      初期設定では選択されていません。**

   * **翻訳を保持しない**

      選択した場合、翻訳はリポジトリに保存されません。

      選択されていないと、翻訳は保持されます。

      初期設定では選択されていません。**

* **スマートレンダリング**

   次のいずれかを選択します。

   * `Always show contributions in the original language` (デフォルト値)
   * `Always show contributions in user preferred language`
   * `Show contributions in user preferred language for only logged-in users`

#### イネーブルメント {#enablement}

![サイトの有効化](assets/site-enablement.png)

`ENABLEMENT`設定は、選択したコミュニティサイトテンプレートに[割り当て機能](/help/communities/functions.md#assignments-function)が含まれている場合に適用されます。この機能は、イネーブルメント機能がライセンスされ、[設定](/help/communities/enablement.md)されている場合に使用できます。 割り当て機能を含む参照サイトテンプレートは`Reference Structured Learning Site Template.`です

* **イネーブルメントマネージャー**
（必須）このイネーブルメントコミュニティを管理す `Community Enablementmanagers` るために選択できるのは、グループのメンバーのみです。イネーブルメントマネージャーは、メンバーをリソースに割り当てます。 [ユーザーとユーザーグループの管理](/help/communities/users.md)も参照してください。

* **Marketing Cloud 組織 ID**

   （オプション） [Video Heartbeat Analytics](/help/communities/analytics.md#video-heartbeat-analytics)ライセンスのID。

* 「**次へ**」を選択します。

### 手順 4：コミュニティサイトの作成  {#step-create-communities-site}

調整が必要な場合は、「**戻る**」ボタンを使用して調整します。

**作成**&#x200B;を選択して開始すると、サイトの作成プロセスを中断できません。

サイト作成後は、以下のようになります。

* URL（ノード名）の変更はサポートされていません。
* 今後、コミュニティサイトテンプレートを変更しても、作成したコミュニティサイトには影響しません。
* コミュニティサイトテンプレートを無効にしても、作成したコミュニティサイトには影響しません。
* コミュニティサイトの[STRUCTURE](#modify-structure)を編集するには、そのプロパティを変更します。

![create-site](assets/create-site1.png)

プロセスが完了すると、新しいサイトのフォルダーがコミュニティサイトコンソールに表示されます。このコンソールで、作成者がページコンテンツを追加したり、管理者がサイトのプロパティを変更したりできます。

![modify-site-property](assets/modify-site-property.png)

コミュニティサイトを変更するには、そのプロジェクトフォルダーを選択して開きます。

![site-project](assets/site-project.png)

サイトにマウスポインターを置くか、サイトカードに触れると、[オーサーモード](#authoring-site-content)でサイトを編集[、](#modifying-site-properties)変更用のサイトプロパティを開く[、](#publishing-the-site)を公開、[サイトを書き出す](#exporting-the-site)、[サイトを削除するアイコンが表示されます。](#deleting-the-site)

## サイトコンテンツのオーサリング {#authoring-site-content}

サイトのコンテンツは、他の AEM Web サイトと同じツールを使用してオーサリングできます。オーサリング用にサイトを開くには、サイトにマウスポインターを置くと表示される`Open Site`アイコンを選択します。 サイトが新しいタブで開き、コミュニティサイトコンソールにアクセスできるようになります。

![site-content](assets/site-content.png)

>[!NOTE]
>
>AEM に馴染みがない場合は、[基本操作](/help/sites-authoring/basic-handling.md)に関するドキュメントおよび[ページのオーサリングのクイックガイド](/help/sites-authoring/qg-page-authoring.md)を参照してください。

## サイトプロパティの変更  {#modifying-site-properties}

![サイトを編集](assets/edit-site.png)

サイトの作成プロセス中に指定した既存のサイトのプロパティを変更するには、サイトにマウスポインターを置くと表示される`Edit Site`アイコンを選択します。

`Details of the following properties match the descriptions provided in the` [サイト](#site-creation) 作成セクション。

![modify-site-basicinfo](assets/modify-site-basicinfo.png)

### 基本事項の変更 {#modify-basic}

BASICパネルでは、次の変更が可能です。

* コミュニティサイトのタイトル
* コミュニティサイトの説明

コミュニティサイト名は変更できません。

別のコミュニティサイトテンプレートを選択しても、テンプレートとサイトの間に関係は残っていないので、既存のコミュニティサイトに影響が及ぶことはありません。

その一方で、コミュニティサイトの[構造](#modify-structure)は変更できます。

### 構造の変更  {#modify-structure}

構造パネルでは、最初にコミュニティサイトテンプレートから作成された構造を変更できます。パネルから、次のことが可能です。

* 追加の[コミュニティ機能](/help/communities/functions.md)をサイト構造にドラッグ&amp;ドロップします。
* サイト構造内のコミュニティ機能のインスタンスで、次の操作を実行します。

   * **`gear icon`**

      表示タイトルやURL名*、[権限を持つメンバーグループ](/help/communities/users.md#privilegedmembersgroups)などの設定を編集します。

   * **`trashcan icon`**

      サイト構造から関数を削除（削除）します。

   * **`grid icon`**

      サイトのトップレベルナビゲーションバーに表示される機能の順序を変更します。

>[!NOTE]
>
>トップにある機能を除き、サイト構造のすべての機能の順序を変更できます。したがって、コミュニティサイトのホームページは変更できません。

>[!CAUTION]
>
>* 表示タイトルは副作用なく変更できますが、コミュニティサイトに属するコミュニティ機能のURL名を編集することはお勧めしません。
>
>
例えば、URL の名前を変更しても、既存の UGC は移動されません。そのため、UGC が「失われる」ことになります。

>[!CAUTION]
>
>グループ関数は、**&#x200B;を&#x200B;*の最初の関数にし、サイト構造内で唯一の*&#x200B;関数にしないでください。
>
>他の機能（[ページ機能](/help/communities/functions.md#page-function)など）を含め、その機能を 1 番目にリストする必要があります。

#### 例：コミュニティのサイト構造へのカタログ機能の追加  {#example-adding-a-catalog-function-to-a-community-site-structure}

![add-catalog-site](assets/add-catalog-site.png)

### デザインの変更 {#modify-design}

デザインパネルでは、適用する新しいテーマを選択できます。

* [コミュニティサイトテーマ](#community-site-theme)
* [コミュニティサイトブランディング](#community-site-branding)

   * パネルの下部までスクロールして、ブランド画像を変更します。

### 設定の変更 {#modify-settings}

設定パネルでは、コミュニティサイト作成の手順 3 のサブパネルにあるほとんどの設定にアクセスできます。

* [ユーザー管理](#user-management)
* [タグ](#tagging)
* [モデレート](#moderation)
* [メンバーの役割](#roles)
* [分析](#analytics)
* [翻訳](#translation)

### サムネイルの変更 {#modify-thumbnail}

サムネイルパネルでは、コミュニティサイトコンソールでサイトを表現する画像をアップロードできます。

### イネーブルメントの変更  {#modify-enablement}

イネーブルメントパネルでは、コミュニティサイトの作成中に表示された設定にアクセスできます。

[ENABLEMENT](#enablement)の説明を参照してください。

## サイトの公開 {#publishing-the-site}

コミュニティサイトを新しく作成または変更した後、サイト上にマウスポインターを置くと表示される`Publish Site`アイコンを選択して、サイトを公開（アクティブ化）できます。

![publish-site](assets/publish-site.png)

サイトが正常に公開されると、次のようなメッセージが表示されます。

![site-published](assets/site-published.png)

### ネストされたグループでの公開 {#publishing-with-nested-groups}

コミュニティサイトを公開した後、[グループコンソール](/help/communities/groups.md)を使用して作成された各サブコミュニティ（ネストされたグループ）を個別に公開する必要があります。

## サイトの書き出し  {#exporting-the-site}

![export-site](assets/export-site.png)

サイトにマウスポインターを置くと表示される書き出しアイコンを選択して、コミュニティサイトのパッケージを作成します。このパッケージは、[パッケージマネージャー](/help/sites-administering/package-manager.md)に格納され、ダウンロード可能になります。

UGC はサイトパッケージに含まれていません。

## サイトの削除 {#deleting-the-site}

![deleteicon](assets/deleteicon.png)

コミュニティサイトを削除するには、サイトを削除アイコンを選択します。このアイコンは、コミュニティサイトコンソール内でサイトにマウスポインターを置くと表示されます。サイトを削除すると、UGC やユーザーグループ、アセット、データベースレコードなど、そのサイトに関連付けられているアイテムがすべて削除されます。

## 作成されたコミュニティユーザーグループ {#created-community-user-groups}

新しいコミュニティサイトが公開されると、新しいメンバーグループが作成されます（ユーザーグループはパブリッシュ環境で作成されます）。各グループには、様々な管理の役割およびメンバーの役割に応じて適切な権限が設定されます。

メンバーグループ用に作成された名前には、[手順1](#step13asitetemplate)で指定された&#x200B;*site-name*（URLに表示される名前）と、コミュニティサイトやコミュニティサイトのルートが同じサイト名を持つグループとの競合を防ぐための一意のIDが含まれます。

例えば、「Getting Started Tutorial」というタイトルを持つサイトのサイト名が「engage」の場合、モデレーターのユーザーグループは次のようになります。

* タイトル：コミュニティ Engage モデレーター
* 名前：community-*engage-uid*-moderators

サイト作成中にモデレーターまたはグループ管理者の役割を割り当てられたメンバーは、適切なグループとメンバーグループに割り当てられます。これらのグループとメンバーの割り当ては、新しいサイトが公開されると、パブリッシュ環境で作成されます。

詳しくは、[ユーザーとユーザーグループの管理](/help/communities/users.md)を参照してください。

>[!NOTE]
>
>[ソーシャルログインを許可：Facebook](#user-management) が有効な場合は、以下に示すユーザーグループが作成された後に、
>
>* `community-<site-name>-<uid>-members`
>
>
が作成されたら、適用された[Facebook Cloud Service](/help/communities/social-login.md#createafacebookcloudservice)を設定して、このグループにユーザーを追加する必要があります。

## 認証エラーの設定 {#configure-for-authentication-error}

ユーザーが誤った資格情報を入力してログインに失敗した場合、コミュニティサイトはデフォルトでサンプルのログインページにリダイレクトします。このログイン例は、[実稼動サーバー](/help/sites-administering/production-ready.md)には存在しません。

正しくリダイレクトするには、サイトを設定してパブリッシュ環境にプッシュした後、以下の手順を実行し、認証失敗時にコミュニティサイトにリダイレクトされるようにします。

* 各AEMパブリッシュインスタンスで。
* 管理者権限でサインインします。
* [Webコンソール](/help/sites-deploying/configuring-osgi.md)にアクセスします。

   * 例えば、[https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)のようにします。

* `Adobe Granite Login Selector Authentication Handler`を探します。
* 「`pencil`」アイコンを選択して、設定を編集用に開きます。
* **Login Page Mappings**&#x200B;を次のように入力します。

   `/content/sites/<site-name>/path/to/login/page:/content/sites/<site-name>`

   以下に例を示します。
   `/content/sites/engage/en/signin:/content/sites/engage/en`

* 「**保存**」を選択します。

![auth-error](assets/auth-error.png)

### 認証リダイレクトのテスト {#test-authentication-redirection}

ログインページマッピングをコミュニティサイト用に設定した前述の AEM パブリッシュインスタンス上で、次の操作をおこないます。

* コミュニティサイトのホームページを参照します。

   * 例： [https://localhost:4503/content/sites/engage/en.html](https://localhost:4503/content/sites/engage/en.html)

* 「ログアウト」を選択します。
* 「ログイン」を選択します。
* ユーザー名「x」やパスワード「x」など、明らかに正しくない資格情報を入力します。
* ログインページに「無効なログイン」エラーが表示されます。

![test-authentication](assets/test-authentication.png)

## 主なサイトのコンソールからコミュニティサイトへのアクセス {#accessing-community-sites-from-main-sites-console}

グローバルナビゲーションのサイトコンソールから、コミュニティサイトは`Community Sites`フォルダーに配置されます。

コミュニティサイトにはこの方法でアクセスできますが、管理タスクをおこなう場合は、コミュニティサイトコンソールからコミュニティサイトにアクセスする必要があります。

![access-site](assets/access-site.png)



