---
title: コミュニティサイトコンソール
description: Communities のサイトコンソールにアクセスして、サイトの作成、編集、管理を行う方法を説明します。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: 426e3adf-3723-4d17-a988-6eb050939e68
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '3084'
ht-degree: 1%

---

# コミュニティサイトコンソール {#communities-sites-console}

コミュニティサイトコンソールを使用すると、次の場所にアクセスできます。

* サイトの作成
* サイト編集
* サイト管理
* [ ネストされたグループの作成と編集 ](/help/communities/groups.md) （サブコミュニティ）

[AEM Communitiesの概要 ](/help/communities/getting-started.md) を参照して、オーサー環境でコミュニティサイトをすばやく作成する方法や、オーサー環境とパブリッシュ環境からコミュニティグループを作成する方法を確認します。

>[!NOTE]
>
>[ コミュニティサイト ](/help/communities/sites-console.md)、[ コミュニティサイトテンプレート ](/help/communities/sites.md)、[ コミュニティグループテンプレート ](/help/communities/tools-groups.md)、および [ コミュニティ機能 ](/help/communities/functions.md) を作成するための主な Communities メニューは、オーサー環境でのみ使用できます。

## 前提条件 {#prerequisites}

コミュニティサイトを作成する前に、*必須* 次の操作が必要です。

* 1 つ以上のPublish インスタンスが実行中であることを確認します。
* [ トンネル サービス ](/help/communities/deploy-communities.md#tunnel-service-on-author) を有効にして、メンバーとメンバーグループを管理します。
* [ プライマリパブリッシャー ](/help/communities/deploy-communities.md#primary-publisher) を特定します。
* [ レプリケーションを設定 ](/help/communities/deploy-communities.md#replication-agents-on-author) プライマリ・パブリッシャ・ポートがデフォルトでない場合（4503）。

ベストプラクティスとして、サイトが多くの機能をサポートできるように準備するには、次の手順を実行します。

* [ 最新の機能パック ](/help/communities/deploy-communities.md#latestfeaturepack) をインストールします。
* AEM Communitiesに対して [Adobe Analytics](/help/communities/analytics.md) を有効にします。
* [ メール ](/help/communities/email.md) を設定
* [ コミュニティ管理者 ](/help/communities/users.md#creating-community-members) を特定します。
* ソーシャルログイン用に [OAuth ハンドラーを有効にする ](/help/communities/social-login.md#adobe-granite-oauth-authentication-handler)。

## Communities サイトコンソールへのアクセス {#accessing-communities-sites-console}

オーサー環境で Communities サイトコンソールにアクセスするには、次の手順を実行します。

* グローバルナビゲーションから：**[!UICONTROL コミュニティ]**/**[!UICONTROL サイト]**

コミュニティサイトコンソールには、既存のコミュニティサイトが表示されます。 このコンソールから、コミュニティサイトの作成、編集、管理、削除を行うことができます。

コミュニティサイトを作成するには、「**作成** アイコンを選択します。

既存のコミュニティ サイトにアクセスして、ネストされたグループの作成、変更、公開、エクスポート、追加を行うには、サイトのフォルダ アイコンを選択します。

## サイトの作成 {#site-creation}

サイト作成コンソールは、選択した [ コミュニティサイトテンプレート ](/help/communities/sites.md) と設定に基づいてサイトの機能を組み立てるステップバイステップのアプローチを提供します。

コンテンツの投稿、メッセージの送信、グループへの参加を行うには、サイト訪問者がログインする必要があるので、作成されたサイトにはいずれもログイン機能が含まれています。 その他の機能には、ユーザープロファイル、メッセージング、通知、サイトメニュー、検索、テーマ設定、ブランディングなどがあります。

プロセスを開始するには、Communities サイトコンソールの上部にある「`Create`」ボタンを選択します。

作成プロセスは、設定する一連の機能を含むパネルとして提示される一連の手順です（サブパネルとして提示）。 最後の手順でサイトをコミットする前に、**次へ** 手順に進むか **戻る** 前の手順に進むことができます。

### 手順 1：サイトテンプレート {#step-site-template}

![newsitetemplate](assets/newsitetemplate.png)

サイトテンプレートパネルで、タイトル、説明、サイトルート、ベース言語、名前、サイトテンプレートを指定します。

* **コミュニティサイトのタイトル**

  サイトの表示タイトル。

  タイトルは、公開されたサイトとサイト管理 UI に表示されます。

* **コミュニティサイトの説明**

  サイトの説明。

  公開されたサイトに説明が表示されません。

* **コミュニティサイトのルート**

  サイトのルートパス。

  デフォルトのルートは `/content/sites` ですが、ルートは web サイト内の任意の場所に移動できます。

* **コミュニティサイトのベース言語**

  （単一言語の場合は影響はありません：英語）プルダウンメニューを使用して、利用可能な言語から 1 つ *または複数* ベース言語を選択します。ドイツ語、イタリア語、フランス語、日本語、スペイン語、ポルトガル語（ブラジル）、中国語（繁体字）、中国語（簡体字）。 追加した言語ごとに 1 つのコミュニティサイトが作成され、[ 多言語サイトのコンテンツの翻訳 ](/help/sites-administering/translation.md) に記載されているベストプラクティスに従って、同じサイトフォルダー内に存在します。 各サイトのルートページには、選択した言語のいずれかの言語コード（英語の場合は「en」、フランス語の場合は「fr」など）で命名された子ページが含まれています。

* **コミュニティサイト名**:

  URL に表示されるサイトのルートページの名前。

   * サイトを作成した後で名前を変更することは容易ではないため、名前を再確認してください。
   * ベース URL （`https://server:port/site root/site name)` は、`Community Site Name` の下に表示されます。

   * 有効な URL の場合は、ベース言語コード + 「.html」を付加します

     *例えば*、次のように指定します。`https://localhost:4502/content/sites/mysight/en.html`

* **コミュニティサイトテンプレート** メニュー

  プルダウンメニューを使用して、使用可能な [ コミュニティサイトテンプレート ](/help/communities/tools.md) を選択します。

* 「**次へ**」を選択します。

### 手順 2：デザイン {#step-design}

デザインパネルには、テーマとブランディングバナーを選択する 2 つのサブパネルが含まれています。

#### コミュニティサイトテーマ {#community-site-theme}

![sitetheme](assets/sitetheme.png)

このフレームワークでは、`Twitter Bootstrap` を使用して、レスポンシブで柔軟なデザインをサイトに導入します。 多数のプリロードされたBootstrapテーマの 1 つを選択して、選択したコミュニティサイトテンプレートのスタイルを設定するか、Bootstrapテーマをアップロードできます。

選択すると、テーマに不透明な青のチェックマークが付けられます。

コミュニティサイトが公開されたら、[ プロパティを編集 ](#modifying-site-properties) し、別のテーマを選択できます。

#### コミュニティサイトのブランディング {#community-site-branding}

![site-branding](assets/site-branding.png)

コミュニティサイトのブランディングは、各ページの上部にヘッダーとして表示される画像です。

画像のサイズは、ブラウザーで予想されるページ表示の幅と同じ幅で、高さが 120 ピクセルである必要があります。

画像を作成または選択する際は、次の点に注意してください。

* 画像の高さは、画像の上端から測定して 120 ピクセルに切り抜かれます。
* 画像は、ブラウザーウィンドウの左端にピン留めされます。
* 画像の幅が…の場合のように、画像のサイズは変更されません。

   * ブラウザーの幅より小さい場合、画像は水平方向に繰り返されます。
   * ブラウザーの幅より大きい場合、画像は切り抜かれたように見えます。

* 「**次へ**」を選択します。

### 手順 3：設定 {#step-settings}

設定パネルには、サイトを作成するための最後の手順に進む前に設定する機能を示すいくつかのサブパネルが含まれています。

* [ユーザー管理](#user-management)
* [タグ設定](#tagging)
* [役割](#roles)
* [モデレート](#moderation)
* [ANALYTICS](#analytics)
* [翻訳](#translation)

>[!NOTE]
>
>**トンネル サービスを有効にする**
>
>いくつかの設定サブパネルでは、信頼できるメンバーを割り当てて、UGC を管理したり、グループを管理したり、パブリッシュ環境のイネーブルメントリソースの連絡先になることができます。
>
>この規則は、パブリッシュ側 [ ユーザーとユーザーグループ ](/help/communities/users.md) （メンバーとメンバーグループ）をオーサー環境で複製しないようにするためのものです。
>
>したがって、オーサー環境でコミュニティサイトを作成し、信頼できるメンバーを様々な役割に割り当てる場合、メンバーデータをパブリッシュ環境から取得する必要があります。
>
>これは、オーサー環境の ` [AEM Communities Publish Tunnel Service](/help/communities/deploy-communities.md#tunnel-service-on-author)` を有効にすることで実現されます。

#### ユーザー管理 {#user-management}

![createsitesettings](assets/createsitesettings.png)

* **ユーザー登録の許可**

  オンにすると、サイト訪問者は自己登録によってコミュニティメンバーになる場合があります。
これをオフにすると、コミュニティサイトは *制限* され、サイト訪問者はコミュニティサイトのメンバーグループに割り当てられるか、リクエストを送信するか、電子メールで招待を送信される必要があります。 オフにした場合は、匿名アクセスを許可しません。
*プライベート* コミュニティサイトの場合はオフにします。 デフォルトではオンになっています。

* **匿名アクセスを許可**

  オンにした場合、コミュニティサイトは *開いている* ので、すべてのサイト訪問者がサイトにアクセスできます。
オフにすると、ログインしたメンバーのみがサイトにアクセスできます。
*プライベート* コミュニティサイトの場合はオフにします。 デフォルトではオンになっています。

* **メッセージングを許可**

  オンにすると、メンバーは互いにメッセージを送信したり、コミュニティサイト内のグループにメッセージを送信したりできます。
オフにすると、メッセージングはコミュニティに設定されません。
デフォルトではオフになっています。

* **ソーシャルログインを許可：Facebook**

  オンにした場合、サイト訪問者がFacebook アカウントの資格情報を使用してログインできるようにします。 選択した [Facebook クラウド構成 ](/help/communities/social-login.md#create-a-facebook-connect-cloud-service) は、コミュニティ サイトを作成した後、コミュニティ サイトのメンバーグループにユーザーを追加するように構成する必要があります。
オフにすると、Facebook ログインは表示されません。
*プライベート* コミュニティサイトの場合は、オフのままにします。 デフォルトではオフになっています。

* **ソーシャルログインを許可：Twitter**

  オンにした場合、サイト訪問者がTwitterアカウントの資格情報を使用してログインできるようにします。 選択した [Twitter クラウド構成 ](/help/communities/social-login.md#create-a-twitter-connect-cloud-service) は、コミュニティ サイトを作成した後、コミュニティ サイトのメンバーグループにユーザーを追加するように構成する必要があります。
オフにすると、Twitterログインは表示されません。
*プライベート* コミュニティサイトの場合は、オフのままにします。 デフォルトではオフになっています。

>[!NOTE]
>
>**ソーシャルログインの許可**
>
>facebookとTwitterのサンプル構成が存在し、（実稼動環境 [ に対して選択可能である場合もありますが ](/help/sites-administering/production-ready.md)、カスタム FacebookとTwitterのアプリケーションを作成する必要があります。 [FacebookとTwitterを使用したソーシャルログイン ](/help/communities/social-login.md) を参照してください。

#### タグ設定 {#tagging}

![ サイトタグ付け ](assets/site-tagging.png)

コミュニティコンテンツに適用される可能性のあるタグは、[ タグ付けコンソール ](/help/sites-administering/tags.md#tagging-console) を通じて以前に定義されたタグ名前空間を選択して制御されます。

さらに、コミュニティサイトのタグ名前空間を選択すると、カタログとリソースを定義する際に表示される選択が制限されます。

* テキスト検索ボックス：サイトで使用できるタグを識別するために、入力を開始します。

#### 役割 {#roles}

![ コミュニティの役割 ](assets/site-admin-2.png)

[ コミュニティメンバーの役割 ](/help/communities/users.md) は、これらの設定で割り当てられます。

先行入力検索を使用すると、コミュニティメンバーを簡単に見つけることができます。

* **コミュニティマネージャー**

  入力を開始して、1 人以上のコミュニティメンバーまたはコミュニティメンバーやメンバーグループを管理できるメンバーグループを選択します。

* **コミュニティモデレーター**

  入力を開始して、ユーザー生成コンテンツのモデレーターとして信頼される 1 人以上のコミュニティメンバーまたはメンバーグループを選択します。

* **コミュニティ特権会員**

  [ コミュニティ機能 ](/help/communities/functions.md) に対してコンテンツを作成できるように、入力を開始して、1 つ以上のコミュニティメンバーまたはメンバーグループを選択し `Allow Privileged Member` す。

* **コミュニティ管理者**

  入力を開始して、他のサイト管理者やデフォルトのコミュニティ管理者に依存せずにサイト構造を処理できる 1 人または複数のサイト管理者を選択します。 任意の階層レベルにグループを作成でき、ネストされたグループのデフォルトの管理者になります（ただし、後でネストされたグループの管理者ロールから削除できます）。

#### モデレート {#moderation}

![ サイトのモデレート ](assets/site-moderation.png)

ユーザー生成コンテンツ（UGC）をモデレートするためのグローバル設定は、これらの設定で制御されます。 個々のコンポーネントには、モデレートを制御するための追加設定があります。

* **コンテンツはプレモデレートされています**

  オンにすると、投稿されたコミュニティコンテンツは、モデレーターが承認するまで表示されません。 デフォルトではオフになっています。 詳しくは、[ コミュニティコンテンツのモデレート ](/help/communities/moderate-ugc.md#premoderation) を参照してください。

* **コンテンツが非表示になる前のしきい値にフラグを設定**

  0 より大きい場合は、トピックまたは投稿がパブリック ビューから非表示になるまでに、そのトピックまたは投稿にフラグを設定する必要がある回数です。 -1 に設定すると、フラグが設定されたトピックまたは投稿がパブリック ビューから非表示になることはありません。 デフォルトは 5 です。

#### ANALYTICS {#analytics}

![site-analytics](assets/site-analytics.png)

* **Analytics を有効にする**

  Communities 機能にAdobe Analyticsが [ 設定 ](/help/communities/analytics.md) されている場合にのみ使用できます。
デフォルトではオフになっています。 オンにすると、追加の選択メニューが表示されます。

![site-analytics-enable](assets/site-analytics-enable.png)

* **クラウド設定フレームワークのリファレンス**

  プルダウンメニューから、このコミュニティサイト用に設定されたAnalytics Cloud サービスフレームワークを選択します。
  [Communities 機能のための Analytics 設定 ](/help/communities/analytics.md#aem-analytics-framework-configuration) ドキュメントのフレームワークの例を `Communities` に示します。

#### 翻訳 {#translation}

![ サイト翻訳 ](assets/site-translation.png)

* **機械翻訳を許可**

  オンにすると（デフォルトはオフ）、サイト内の UGC に対して機械翻訳が有効になります。 これは、サイトが多言語サイトとして設定されている場合でも、ページコンテンツなどの他のコンテンツには影響しません。 AEM Communitiesのライセンス取得済み翻訳サービスの設定について詳しくは、[ ユーザー生成コンテンツの翻訳 ](/help/communities/translate-ugc.md) を参照してください。 詳細については、[ 多言語サイトのコンテンツの翻訳 ](/help/sites-administering/translation.md) を参照してください。

![ 機械翻訳を許可 ](assets/allow-machine-translation.png)

* **選択した言語の機械翻訳を有効にする**

  機械翻訳に対して有効な言語は、デフォルトで [ 翻訳統合設定 ](/help/communities/translate-ugc.md#translation-integration-configuration) で指定されたシステム設定になります。 このサイトの既定の設定を上書きするには、既定の設定を削除するか、プルダウン メニューから他の言語を選択します。

* **翻訳プロバイダーの選択**

  デフォルトでは、サービスプロバイダーはデモ専用の `microsoft` を使用した体験版サービスです。 翻訳サービスプロバイダーのライセンスがない場合は、「機械翻訳を許可 **のチェックを外す必要があ** ます。

* **グローバル共有ストアの選択**

  複数の言語コピーを含む web サイトの場合、グローバル共有ストアは、各言語コピーから見える単一のスレッドの会話を提供します。 これは、言語コピーとして含まれる言語の 1 つを選択することで実現されます。 デフォルトは *グローバル共有ストアなし* です。

* **翻訳プロバイダー設定を選択**

  ライセンス取得済みの翻訳プロバイダー用に作成された [ 翻訳統合フレームワーク ](/help/sites-administering/tc-tic.md) を選択します。

* **コミュニティサイトの翻訳オプションを選択する**

   * **ページ全体を翻訳**

     ページ上のすべての UGC が、ページのベース言語に翻訳されます。

     デフォルトは *選択されていません*。

   * **選択のみを翻訳**

     選択すると、各投稿の横に翻訳オプションが表示され、個々の投稿をページのベース言語に翻訳できます。
デフォルトは *選択* です。

* **永続性オプションの選択**

   * **ユーザーリクエストに対する投稿を翻訳し、その後保持**
選択した場合、リクエストが行われるまでコンテンツは翻訳されません。 翻訳が完了すると、翻訳がリポジトリに保存されます。

     デフォルトは *選択されていません*。

   * **翻訳を永続化しない**

     選択した場合、翻訳はリポジトリに保存されません。

     選択しない場合、翻訳が保持されます。

     デフォルトは *選択されていません*。

* **スマートレンダリング**

  次のいずれかを選択します。

   * `Always show contributions in the original language`（デフォルト）
   * `Always show contributions in user preferred language`
   * `Show contributions in user preferred language for only logged-in users`

### 手順 4 :Communities サイトの作成 {#step-create-communities-site}

調整が必要な場合は、「戻る **ボタンを使用して調整を行** ます。

**作成** を選択して開始すると、サイトの作成プロセスを中断することはできません。

サイトを作成したら、次の操作を行います。

* URL （ノード名）の変更はサポートされていません。
* コミュニティサイトテンプレートに対するその後の変更は、作成されたコミュニティサイトには影響しません。
* コミュニティサイトテンプレートを無効にしても、作成したコミュニティサイトには影響しません。
* プロパティを変更することで、コミュニティサイトの [ 構造 ](#modify-structure) を編集できます。

![create-site](assets/create-site1.png)

処理が完了すると、新しいサイトのフォルダーが Communities サイトコンソールに表示されます。作成者はこのフォルダーからページコンテンツを追加でき、管理者はサイトのプロパティを変更できます。

![modify-site-property](assets/modify-site-property.png)

コミュニティサイトを編集するには、そのプロジェクトフォルダーを選択して開きます。

![site-project](assets/site-project.png)

マウスでサイトの上にマウスポインターを置くか、サイトカードに触れると、次のことを可能にするアイコンが表示されます。

* [オーサーモードでのサイトの編集](#authoring-site-content)
* [変更するサイトのプロパティを開く](#modifying-site-properties)
* [サイトの公開](#publishing-the-site)
* [サイトのエクスポート](#exporting-the-site)
* [サイトの削除](#deleting-the-site)

## サイトコンテンツのオーサリング {#authoring-site-content}

サイトのコンテンツは、他のAEM web サイトと同じツールを使用して作成できます。 サイトをオーサリング用に開くには、サイトにマウスのカーソルを合わせたときに表示される `Open Site` アイコンを選択します。 サイトが新しいタブで開き、Communities サイトコンソールに引き続きアクセスできるようになります。

![site-content](assets/site-content.png)

>[!NOTE]
>
>AEMに詳しくない場合は、[ 基本操作 ](/help/sites-authoring/basic-handling.md) および [ ページのオーサリングのクイックガイド ](/help/sites-authoring/qg-page-authoring.md) に関するドキュメントを参照してください。

## サイトのプロパティの変更 {#modifying-site-properties}

![edit-site](assets/edit-site.png)

サイト作成プロセスで指定した既存のサイトのプロパティは、サイトの上にマウスを置くと表示される `Edit Site` アイコンを選択して変更できます。

[ サイトの作成 ](#site-creation) セクションを `Details of the following properties match the descriptions provided in the` きます。

![modify-site-basicinfo](assets/modify-site-basicinfo.png)

### 基本の変更 {#modify-basic}

基本パネルでは、次の変更を行うことができます。

* コミュニティサイトのタイトル
* コミュニティサイトの説明

コミュニティサイト名は変更できません。

別のコミュニティサイトテンプレートを選択しても、テンプレートとサイトの間に接続が残らないので、既存のコミュニティサイトには影響しません。

代わりに、コミュニティサイトの [ 構造 ](#modify-structure) を変更できます。

### 構造を修正 {#modify-structure}

構造パネルを使用すると、選択したコミュニティサイトテンプレートから最初に作成した構造を変更できます。 パネルから、次の操作を実行できます。

* 追加の [ コミュニティ機能 ](/help/communities/functions.md) をサイト構造にドラッグ&amp;ドロップします。
* サイト構造内のコミュニティ機能のインスタンスで：

   * **`gear icon`**

     表示タイトルや URL 名、[ 権限のあるメンバーグループ ](/help/communities/users.md#privilegedmembersgroups) などの設定を編集します。

   * **`trashcan icon`**

     サイト構造から関数を削除（削除）します。

   * **`grid icon`**

     サイトの最上位のナビゲーションバーに表示される関数の順序を変更します。

>[!NOTE]
>
>サイト構造内のすべての関数の順序は、上部の関数を除いて変更できます。 したがって、コミュニティサイトのホームページは変更できません。

>[!CAUTION]
>
>* 表示タイトルを変更しても副作用はありませんが、コミュニティサイトに属するコミュニティ機能の URL 名を編集することはお勧めしません。
>
>例えば、URL の名前を変更しても既存の UGC は移動しないので、UGC は「失われます」と表示されます。

>[!CAUTION]
>
>groups 関数は、サイト構造内の *最初の関数でも唯一の関数でもな**てはなりません*。
>
>[page 関数 ](/help/communities/functions.md#page-function) など、その他の関数を最初に含めてリストする必要があります。

#### 例：コミュニティサイト構造へのカタログ機能の追加 {#example-adding-a-catalog-function-to-a-community-site-structure}

![add-catalog-site](assets/add-catalog-site.png)

### デザインを修正 {#modify-design}

デザインパネルを使用すると、新しいテーマを適用できます。

* [コミュニティサイトテーマ](#community-site-theme)
* [コミュニティサイトブランディング](#community-site-branding)

   * パネルの下部までスクロールして、ブランド画像を変更します。

### 設定の変更 {#modify-settings}

設定パネルを使用すると、コミュニティサイト作成の手順 3 のサブパネルにある設定のほとんどにアクセスできます。

* [User Management](#user-management)
* [タグ](#tagging)
* [モデレート](#moderation)
* [メンバーの役割](#roles)
* [Analytics](#analytics)
* [翻訳](#translation)

### サムネールを変更 {#modify-thumbnail}

サムネールパネルを使用すると、画像をアップロードして Communities サイトコンソール内のサイトを表すことができます。

## サイトの公開 {#publishing-the-site}

コミュニティサイトを新しく作成または変更した後、サイト上にマウスポインターを置くと表示される `Publish Site` アイコンを選択して、サイトを公開（アクティブ化）できます。

![publish-site](assets/publish-site.png)

サイトが正常に公開されたことを示すメッセージが表示されます。

![site-published](assets/site-published.png)

### ネストされたグループを使用した公開 {#publishing-with-nested-groups}

コミュニティサイトを公開した後、[ グループコンソール ](/help/communities/groups.md) を使用して作成された各サブコミュニティ（ネストされたグループ）を個別に公開する必要があります。

## サイトのエクスポート {#exporting-the-site}

![export-site](assets/export-site.png)

書き出しアイコンを選択し、マウスポインターをサイトの上に置くと、[ パッケージマネージャー ](/help/sites-administering/package-manager.md) に保存され、ダウンロードされるコミュニティサイトのパッケージを作成できます。

UGC はサイトパッケージには含まれていません。

## サイトの削除 {#deleting-the-site}

![deleteicon](assets/deleteicon.png)

コミュニティサイトを削除するには、コミュニティサイトコンソールでサイトにカーソルを合わせると表示される「サイトを削除」アイコンを選択します。 この操作により、UGC、ユーザーグループ、アセット、データベースレコードなど、サイトに関連付けられているすべての項目が削除されます。

## コミュニティユーザーグループを作成しました {#created-community-user-groups}

新しいコミュニティサイトが公開されると、様々な管理者やメンバーの役割に適した権限が設定された新しいメンバーグループ（パブリッシュ環境でユーザーグループが作成されます）が公開されます。

メンバーグループに対して作成される名前には、[ 手順 1](#step13asitetemplate) で指定した *site-name* （URL に表示される名前）が含まれます。 また、異なるコミュニティサイトルートに対して同じサイト名を持つコミュニティサイトやグループとの競合を避けるために、一意の ID も含まれます。

例えば、サイトの名前が「Getting Started Tutorial」の場合、モデレーターのユーザーグループはになります。

* タイトル：Community Engage モデレーター
* 名前：community-*engage-uid*-moderators

サイトの作成中にモデレータまたはグループ管理者の役割を割り当てられたメンバーは、適切なグループに割り当てられ、メンバーグループに割り当てられます。 これらのグループとメンバーの割り当ては、新しいサイトが公開されるときに公開時に作成されます。

詳しくは、[ ユーザーとユーザーグループの管理 ](/help/communities/users.md) を参照してください。

>[!NOTE]
>
>[ ソーシャルログインを許可：Facebook](#user-management) が有効になっている場合、ユーザーグループが `community-<site-name>-<uid>-members` 動した後で
>を作成した場合は、適用されている [Facebook cloud service](/help/communities/social-login.md#createafacebookcloudservice) を、このグループにユーザーを追加するように設定する必要があります。

## 認証エラーの設定 {#configure-for-authentication-error}

デフォルトでは、ユーザーが誤った資格情報を入力してログインできなかった場合に、コミュニティサイトはサンプルのログインページにリダイレクトされます。 このサンプルログインは、[ 実稼動サーバー ](/help/sites-administering/production-ready.md) には存在しません。

正しくリダイレクトするには、サイトを設定して公開にプッシュしたら、次の手順を実行して認証エラーを取得し、コミュニティサイトにリダイレクトするようにします。

* 各AEM パブリッシュインスタンスで。
* 管理者権限でログインします。
* [Web コンソール ](/help/sites-deploying/configuring-osgi.md) にアクセスします。

   * 例えば、[https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr) です。

* `Adobe Granite Login Selector Authentication Handler` を見つけます。
* `pencil` アイコンを選択して、設定を編集用に開くことができます。
* 次のように **ログインページマッピング** を入力します。

  `/content/sites/<site-name>/path/to/login/page:/content/sites/<site-name>`

  次に例を示します。
  `/content/sites/engage/en/signin:/content/sites/engage/en`

* 「**保存**」を選択します。

![auth-error](assets/auth-error.png)

### 認証リダイレクトのテスト {#test-authentication-redirection}

コミュニティサイトのログインページマッピングを使用して設定された同じAEM パブリッシュインスタンス：

* コミュニティサイトのホームページを参照します。

   * 例：[https://localhost:4503/content/sites/engage/en.html](https://localhost:4503/content/sites/engage/en.html)

* 「ログアウト」を選択します。
* 「ログイン」を選択します。
* ユーザー名「x」やパスワード「x」など、誤った認証情報を入力します。
* ログインページに「invalid login」というエラーが表示されます。

![test-authentication](assets/test-authentication.png)

## メインサイトコンソールからのコミュニティサイトへのアクセス {#accessing-community-sites-from-main-sites-console}

グローバルナビゲーションサイトコンソールから、コミュニティサイトは `Community Sites` フォルダーに入っています。

この方法でコミュニティサイトにアクセスできますが、管理タスクの場合は、コミュニティサイト コンソールからコミュニティサイトにアクセスする必要があります。

![access-site](assets/access-site.png)
