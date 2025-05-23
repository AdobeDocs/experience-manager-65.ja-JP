---
title: ユーザー作成コンテンツの翻訳
description: UGC コンテンツの翻訳により、サイト訪問者やメンバーが言語の障壁を取り除いて、グローバルコミュニティを体験できるようにする方法を説明します。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: ac54f06e-1545-44bb-9f8f-970f161ebb72
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1111'
ht-degree: 3%

---

# ユーザー作成コンテンツの翻訳 {#translating-user-generated-content}

Adobe Experience Manager（AEM） Communities の翻訳機能は、[ ソーシャルコンポーネントフレームワーク（SCF）コンポーネント ](../../help/sites-administering/translation.md) を使用して、コミュニティサイトに投稿されたユーザー生成コンテンツ（UGC[ にページコンテンツの翻訳 ](scf.md) の概念を拡張します。

UGC の翻訳により、サイト訪問者やメンバーは、言語の障壁を取り除くことで、グローバルコミュニティを体験できます。

例として、次を考えます。

* あるフランス人のメンバーは、多国籍の料理ウェブサイトのコミュニティフォーラムにフランス語のレシピを投稿している。
* フランス語から日本語へのトリガー変換は、翻訳機能を使って行っています。
* 日本語でレシピを読んだ後、日本のメンバーが日本語でコメントを投稿します。
* フランスのメンバーは、翻訳機能を使用して、日本語のコメントをフランス語に翻訳します。
* グローバル通信。

## 概要 {#overview}

この節では、翻訳サービスと UGC の連携について具体的に説明します。 また、AEMを [ 翻訳サービスプロバイダー ](../../help/sites-administering/translation.md#connectingtoatranslationserviceprovider) に接続する方法と、[ 翻訳統合フレームワーク ](../../help/sites-administering/tc-tic.md) を設定してそのサービスを web サイトに統合する方法について理解していることを前提としています。

翻訳サービスプロバイダーがサイトに関連付けられている場合、サイトの各言語コピーは、コメントなどの SCF コンポーネントを通じて投稿された UGC の独自のスレッドを維持します。

翻訳サービスプロバイダーに加えて翻訳統合が設定されている場合、サイトの各言語コピーが UGC の単一のスレッドを共有することが可能になり、言語コピー間のグローバルなコミュニケーションが可能になります。 言語によって分離されたディスカッションスレッドの代わりに、設定された [ グローバル共有ストア ](#global-translation-of-ugc) を使用すると、どの言語コピーが表示されているかに関係なく、スレッド全体を表示できます。 さらに、地域ごとのグローバル参加者の論理グループに対して、異なるグローバル共有ストアを指定することで、複数の翻訳統合設定を設定できます。

## デフォルトの翻訳サービス {#the-default-translation-service}

AEM Communitiesには、複数の言語に対して有効な [&#128279;](../../help/sites-administering/tc-msconf.md#microsoft-translator-trial-license) デフォルトの翻訳サービス [ 用の ](../../help/sites-administering/tc-msconf.md) 体験版ライセンス  が含まれています。

[ コミュニティサイトの作成 ](sites-console.md) 時に、[ 翻訳 ](sites-console.md#translation) サブパネルから `Allow Machine Translation` がオンになると、デフォルトの翻訳サービスが有効になります。

>[!CAUTION]
>
>デフォルトの翻訳サービスはデモ専用です。
>
>実稼動システムには、ライセンスを取得した翻訳サービスが必要です。 ライセンスがない場合、デフォルトの翻訳サービスは [ オフ ](../../help/sites-administering/tc-msconf.md#microsoft-translator-trial-license-geometrixx-outdoors) にする必要があります。

## UGC のグローバル翻訳 {#global-translation-of-ugc}

Web サイトに複数の [ 言語コピー ](../../help/sites-administering/tc-prep.md) がある場合、デフォルトの翻訳サービスでは、あるサイトで入力された UGC が別のサイトで入力された UGC と関連している可能性があることを認識しません。 これは、UGC が同じコンポーネント（コンポーネントを含んだページの言語コピー）によって生成される場合に当てはまります。

トピックについて話し合う人々のグループに似ています。 1 つの会話に参加する大規模なグループの全員と比較して、自分のグループ以外のグループで行われたコメントに気づかない。

「1 つのグループ会話」が必要な場合は、複数の言語コピーを持つ web サイトをまたいでグローバル翻訳を有効にすることができます。これにより、表示されている言語コピーに関係なく、スレッド全体が表示されます。

例えば、ベースサイトでフォーラムが作成され、言語コピーが作成され、グローバル翻訳が有効になっている場合、ある言語コピーで作成されたフォーラムに投稿されたトピックは、すべての言語コピーに表示されます。 同じことが、返信がどの言語コピーから入力されたかに関係なく、すべての返信に当てはまります。 その結果、トピックと返信のスレッド全体が、トピックが表示されている言語コピーに関係なく表示されます。

>[!CAUTION]
>
>グローバル翻訳前に存在していた UGC は、表示されなくなります。
>
>UGC は [ 共通ストア ](working-with-srp.md) に残りますが、言語固有の UGC の場所に配置され、グローバル翻訳の設定後に追加された新しいコンテンツはグローバル共有ストアの場所から取得されます。
>
>言語固有のコンテンツをグローバル共有ストアに移動または結合するための移行ツールはありません。

### 翻訳統合の設定 {#translation-integration-configuration}

翻訳サービスコネクタをオーサーインスタンスの web サイトに統合する翻訳統合を作成するには、次のようにします。

* 管理者としてログイン
* [ メインメニュー ](http://localhost:4502/) から
* 「**[!UICONTROL ツール]**」を選択します
* 「**[!UICONTROL 操作]**」を選択します。
* **[!UICONTROL Cloud]** を選択します。
* **[!UICONTROL 人のCloud Serviceを選択]**
* 下にスクロールして、「翻訳統合 **[!UICONTROL を表示します]**

  ![ 翻訳の統合 ](assets/translation-integration.png)

* 「**[!UICONTROL 設定を表示]**」を選択します

  ![show-configuration](assets/translation-integration1.png)

* **[!UICONTROL 利用可能 `[+]` 設定]** の横にあるアイコンを選択して、設定を作成できます。

#### 設定を作成ダイアログ {#create-configuration-dialog}

![create-configuration](assets/translation-integration2.png)

* **[!UICONTROL 親設定]**

  （必須）通常、デフォルトのままにします。 デフォルトは `/etc/cloudservices/translation` です。

* **[!UICONTROL タイトル]**

  （必須）任意の表示タイトルを入力します。 デフォルト値はありません。

* **[!UICONTROL 名前]**

  （オプション）設定の名前を入力します。 デフォルトは、タイトルに基づくノード名です。

* 「**[!UICONTROL 作成]**」を選択します。

#### 翻訳設定ダイアログ {#translation-config-dialog}

![ 設定ダイアログ ](assets/translation-integration3.png)

手順について詳しくは、[ 翻訳統合設定の作成 ](../../help/sites-administering/tc-tic.md#creating-a-translation-integration-configuration) を参照してください。

* **[!UICONTROL Sites]** タブ：デフォルトのままにすることができます。

* **[!UICONTROL コミュニティ]** タブ：
   * **[!UICONTROL 翻訳プロバイダー]**
ドロップダウンリストから翻訳プロバイダーを選択します。 デフォルトは `microsoft` （体験版サービス）です。

   * **[!UICONTROL コンテンツのカテゴリ]**
翻訳対象のコンテンツを説明するカテゴリを選択します。 デフォルトは `General.`

   * **[!UICONTROL ロケールを選択…]**
（オプション） UGC を格納するロケールを選択すると、すべての言語コピーからの投稿が 1 つのグローバルな会話に表示されます。 慣例により、web サイトの[ベース言語](sites-console.md#translation)のロケールを選択してください。`No Common Store` を選択すると、グローバル翻訳が無効になります。 デフォルトでは、グローバル翻訳は無効です。

* 「**[!UICONTROL Assets]**」タブ：をデフォルトのままにすることができます。
* 「**[!UICONTROL OK]**」を選択します。

#### アクティベーション {#activation}

新しい translation integration cloud service をPublish環境に対してアクティブ化する必要があります。 まだアクティベートされていない場合は、web サイトに関連付けると、関連付けられているページが公開されたときに、アクティベーションワークフローでこのクラウドサービス設定を公開するように求められます。

## 翻訳設定の管理 {#managing-translation-settings}

>[!NOTE]
>
>**優先言語**
>
>投稿が優先言語と異なる言語であるかどうかを検出する場合は、サイト訪問者の優先言語を確立する必要があります。
>
>優先言語とは、サイト訪問者がログインし、言語の環境設定を指定した場合に、ユーザーのプロファイルで設定される言語の環境設定です。
>
>サイト訪問者が匿名の場合やプロファイルで言語の環境設定を指定していない場合、優先言語がページテンプレートのベース言語になります。

### ユーザーの環境設定 {#user-preference}

#### ユーザープロファイル {#user-profile}

すべてのコミュニティサイトはユーザープロファイルを提供しています。このユーザープロファイルは、サインインしたメンバーが編集してコミュニティに対して自分自身を識別したり、自分の環境設定を設定したりできます。

このような設定の 1 つは、コミュニティコンテンツを常に優先言語で表示するかどうかです。 デフォルトでは、この設定は設定されておらず、デフォルトはシステム設定になります。 ユーザーは、設定をオンまたはオフに変更して、システム設定を上書きできます。

ページをユーザーの優先言語に自動翻訳する場合でも、元のテキストを表示して翻訳を改善するための UI は引き続き使用できます。

![user-profile](assets/translation-integration4.png)

### コミュニティサイト設定 {#community-site-setting}

コミュニティサイトを作成する際に、翻訳オプションを有効にして設定できます。 翻訳設定は、コンテンツの匿名サイト訪問者が閲覧できる場合に有効ですが、ユーザーのプロファイル設定によって上書きされます。
