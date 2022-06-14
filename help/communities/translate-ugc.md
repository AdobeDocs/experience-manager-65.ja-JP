---
title: ユーザー生成コンテンツの翻訳
seo-title: Translating User Generated Content
description: 翻訳機能の仕組み
seo-description: How the translation feature works
uuid: 7ee3242c-2aca-4787-a60d-b807161401ad
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: bfaf80c5-448b-47fb-9f22-57ee0eb169b2
role: Admin
exl-id: ac54f06e-1545-44bb-9f8f-970f161ebb72
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '1108'
ht-degree: 62%

---

# ユーザー生成コンテンツの翻訳 {#translating-user-generated-content}

AEM Communities の翻訳機能は、[ソーシャルコンポーネントフレームワーク（SCF）](scf.md)を使用することで、[ページコンテンツの翻訳](../../help/sites-administering/translation.md)という概念を、コミュニティサイトに投稿されたユーザー生成コンテンツ（UGC）にまで拡張します。

UGC を翻訳することにより、言語の障壁が取り除かれ、サイト訪問者とメンバーがグローバルなコミュニティを体験できます。

例えば以下のような場合が考えられます。：

* フランスのメンバーは、多国籍料理の Web サイトのコミュニティフォーラムに、フランス語でレシピを投稿します。
* 他の日本人は、この翻訳機能を使って、フランス語から日本語へのトリガーを行っています。
* 日本語でレシピを読んだ後、日本から来たメンバーは日本語でコメントを投稿します。
* フランスのメンバーは、翻訳機能を使用して日本語のコメントをフランス語に翻訳します。
* グローバル通信。

## 概要 {#overview}

この節では、特に翻訳サービスと UGC の連動について説明します。AEM を [翻訳サービスプロバイダー](../../help/sites-administering/translation.md#connectingtoatranslationserviceprovider)に接続する方法と、[翻訳統合フレームワーク](../../help/sites-administering/tc-tic.md)を設定して翻訳サービスを Web サイトに統合する方法については既に知っているものとして説明を進めます。

翻訳サービスプロバイダーがサイトに関連付けられているときは、そのサイトの各言語コピーで、SCF コンポーネントを通じて投稿された UGC（コメントなど）のスレッドが独自に保持されます。

翻訳サービスプロバイダーに加えて翻訳フレームワークが設定されているときは、サイトの各言語コピーが UGC の 1 つのスレッドを共有できるので、言語コピー間のグローバルな情報通信を実現できます。言語別のディスカッションスレッドの代わりに、設定された [グローバル共有ストア](#global-translation-of-ugc) どの言語コピーから表示されているかに関係なく、スレッド全体を表示できます。 さらに、地域別などのグローバル参加者の論理的なグループ化に対して、異なるグローバル共有ストアを指定して、複数の翻訳統合設定を設定できます。

## デフォルトの翻訳サービス {#the-default-translation-service}

AEM Communitiesには [試用ライセンス](../../help/sites-administering/tc-msconf.md#microsoft-translator-trial-license) の [デフォルトの翻訳サービス](../../help/sites-administering/tc-msconf.md) 複数の言語で有効になっています。

条件 [コミュニティサイトの作成](sites-console.md)の場合、デフォルトの翻訳サービスは `Allow Machine Translation` が [翻訳](sites-console.md#translation) サブパネル

>[!CAUTION]
>
>デフォルトの翻訳サービスは、デモ目的でのみ提供されています。
>
>実稼動システムでは、ライセンスを取得した翻訳サービスが必要です。ライセンスがない場合、デフォルトの翻訳サービスを [オフにする](../../help/sites-administering/tc-msconf.md#microsoft-translator-trial-license-geometrixx-outdoors).

## UGC のグローバル翻訳 {#global-translation-of-ugc}

Web サイトに[複数の言語コピー](../../help/sites-administering/tc-prep.md)がある場合、デフォルトの翻訳サービスでは、あるサイトで入力された UGC が別のサイトで入力された UGC と関連している可能性は認識されません。その UGC が本質的に同じコンポーネント（そのコンポーネントを含んでいるページの言語コピー）で生成された場合でも同様です。

これは、「いくつかのグループがそれぞれ別のグループの人のコメントは気にせずに会話している状況」と、「1 つの大きなグループに属する全員が同じ会話に参加している状況」の違いに似ています。

「1 つのグループでの会話」が必要な場合は、複数の言語コピーを持つ Web サイト全体のグローバル翻訳を有効にして、どの言語コピーからでもスレッド全体を見られるようにする必要があります。

例えば、基本となるサイトにフォーラムを設け、いくつかの言語コピーを作成し、グローバル翻訳を有効にした場合は、ある言語コピーで作成されたフォーラムに投稿されたトピックは、すべての言語コピーで表示されます。これは返信の場合でも同様で、どの言語コピーから返信が入力されたかは関係ありません。その結果、トピックが表示されている言語コピーに関係なく、トピックと返信のスレッド全体が表示されます。

>[!CAUTION]
>
>グローバル翻訳を設定する前に存在していた UGC は表示されなくなります。
>
>UGC が [共通店](working-with-srp.md)に設定されている場合は、言語固有の UGC の場所の下に配置されますが、グローバル翻訳の設定後に追加された新しいコンテンツは、グローバル共有ストアの場所から取得されます。
>
>言語別のコンテンツをグローバル共有ストアに移動または統合する移行ツールはありません。

### 翻訳統合の設定 {#translation-integration-configuration}

新しい翻訳統合を作成するには、以下の手順を実行します。この操作により、オーサーインスタンスで翻訳サービスコネクターと Web サイトが統合されます。

* 管理者としてログイン
* 次の [メインメニュー](http://localhost:4502/)
* 「**[!UICONTROL ツール]**」を選択します
* 選択 **[!UICONTROL 運用]**
* 選択 **[!UICONTROL クラウド]**
* 選択 **[!UICONTROL Cloud Services]**
* 下にスクロールして **[!UICONTROL 翻訳の統合]**

   ![translation-integration](assets/translation-integration.png)

* 選択 **[!UICONTROL 設定を表示]**

   ![show-configuration](assets/translation-integration1.png)

* 選択 `[+]` 隣のアイコン **[!UICONTROL 利用可能な設定]** 新しい設定を作成するには

#### 設定を作成ダイアログ {#create-configuration-dialog}

![create-configuration](assets/translation-integration2.png)

* **[!UICONTROL 親設定]**

   （必須）通常はデフォルトのままにします。 デフォルトは `/etc/cloudservices/translation` です。

* **[!UICONTROL タイトル]**

   （必須）任意の表示タイトルを入力します。 デフォルト値はありません。

* **[!UICONTROL 名前]**

   （オプション）設定の名前を入力します。 初期設定はタイトルをベースにしたノード名です。

* 「**[!UICONTROL 作成]**」を選択します。

#### 翻訳設定ダイアログ {#translation-config-dialog}

![configuration-dialog](assets/translation-integration3.png)

詳細な手順については、 [翻訳統合設定の作成](../../help/sites-administering/tc-tic.md#creating-a-translation-integration-configuration)

* **[!UICONTROL サイト]** タブ：をデフォルトのままにすることができます。

* **[!UICONTROL コミュニティ]**&#x200B;タブ：
   * **[!UICONTROL 翻訳プロバイダー]**&#x200B;ドロップダウンリストから翻訳プロバイダーを選択します。初期設定は です。 
`microsoft`、試用サービス。

   * **[!UICONTROL コンテンツのカテゴリ]**&#x200B;翻訳対象のコンテンツを説明するカテゴリを選択します。初期設定は です。 
`General.`

   * **[!UICONTROL 一般的なストアのパスとして使用するロケールを選択]**（オプション）UGC を格納するためのロケールを選択すると、すべての言語コピーからの投稿が 1 つのグローバルな会話に表示されます。慣例により、 [ベース言語](sites-console.md#translation) を参照してください。 選択 `No Common Store` グローバル翻訳を無効にします。 デフォルトでは、グローバル翻訳は無効です。

* **[!UICONTROL Assets]** タブ：をデフォルトのままにすることができます。
* 「**[!UICONTROL OK]**」を選択します。

#### アクティベーション {#activation}

新しい翻訳統合クラウドサービスは、パブリッシュ環境に対してアクティベートする必要があります。Web サイトに関連付けられている場合、まだアクティベートされていない場合、関連付けられているページが公開される際に、このクラウドサービス設定の公開を求めるメッセージがアクティベーションワークフローに表示されます。

## 翻訳設定の管理 {#managing-translation-settings}

>[!NOTE]
>
>**設定言語**
>
>投稿が設定言語と異なるかどうかを検出するために、サイト訪問者の設定言語を確定する必要があります。
>
>設定言語とは、サイト訪問者がサインインして言語設定を指定したときに、ユーザープロファイルに登録される言語の設定です。
>
>サイト訪問者が匿名の場合、または言語設定を自分のプロファイルに登録していない場合は、ページテンプレートのベース言語が設定言語になります。

### ユーザーによる設定 {#user-preference}

#### ユーザープロファイル {#user-profile}

どのコミュニティサイトにも、メンバー用のユーザープロファイルがあります。サインインしたメンバーはこのプロファイルを編集して、自分の情報をコミュニティに公開したり、自分用の設定を保存したりできます。

こうした設定の 1 つに、コミュニティコンテンツを常に指定の言語で表示するかどうかのオプションがあります。デフォルトでは、設定は設定されておらず、デフォルトでシステム設定になります。 ユーザーは、設定を [ オン ] または [ オフ ] に変更し、システム設定を上書きできます。

ページが自動的にユーザーの設定言語に翻訳される場合も、元のテキストを表示したり、翻訳を改善したりするための UI を使用できます。

![ユーザープロファイル](assets/translation-integration4.png)

### コミュニティサイトの設定 {#community-site-setting}

コミュニティサイトを作成すると、翻訳オプションを有効化して設定できます。翻訳設定は、匿名のサイト訪問者が表示できるコンテンツに対して有効ですが、ユーザーのプロファイル設定によって上書きされます。
