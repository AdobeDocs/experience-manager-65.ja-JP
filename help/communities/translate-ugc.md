---
title: ユーザー生成コンテンツの翻訳
description: UGC コンテンツの翻訳により、言語の障壁を取り除き、サイトの訪問者やメンバーがグローバルコミュニティを体験できるようにする方法を学びます。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: ac54f06e-1545-44bb-9f8f-970f161ebb72
source-git-commit: b8887b4a6f757352e9dbfdf074c10e9ccd6dbd4f
workflow-type: tm+mt
source-wordcount: '1112'
ht-degree: 1%

---

# ユーザー生成コンテンツの翻訳 {#translating-user-generated-content}

Adobe Experience Manager(AEM)Communities の翻訳機能は、 [ページコンテンツの翻訳](../../help/sites-administering/translation.md) を使用してコミュニティサイトに投稿されたユーザー生成コンテンツ (UGC) に [ソーシャルコンポーネントフレームワーク (SCF) コンポーネント](scf.md).

UGC の翻訳により、サイトの訪問者やメンバーは言語の障壁を取り除くことで、グローバルなコミュニティを体験できます。

例として、次のような場合を考えてみます。

* フランスのメンバーは、多国籍料理の Web サイトのコミュニティフォーラムに、フランス語でレシピを投稿します。
* 他の日本人は、この翻訳機能を使って、フランス語から日本語へのトリガーを行っています。
* 日本語でレシピを読んだ後、日本から来たメンバーは日本語でコメントを投稿します。
* フランスのメンバーは、翻訳機能を使用して日本語のコメントをフランス語に翻訳します。
* グローバル通信。

## 概要 {#overview}

この節では、翻訳サービスと UGC の連携の仕組みについて具体的に説明します。 また、AEMを [翻訳サービスプロバイダー](../../help/sites-administering/translation.md#connectingtoatranslationserviceprovider) を設定し、 [翻訳統合フレームワーク](../../help/sites-administering/tc-tic.md).

翻訳サービスプロバイダーがサイトに関連付けられている場合、サイトの各言語コピーは、コメントなどの SCF コンポーネントを通じて投稿された UGC の独自のスレッドを維持します。

翻訳サービスプロバイダーに加えて翻訳統合を設定すると、サイトの各言語コピーで UGC の 1 つのスレッドを共有し、言語コピー間でグローバルに通信できます。 言語別のディスカッションスレッドの代わりに、設定された [グローバル共有ストア](#global-translation-of-ugc) どの言語コピーから表示されているかに関係なく、スレッド全体を表示できます。 さらに、地域別などのグローバル参加者の論理的なグループ化に対して、異なるグローバル共有ストアを指定して、複数の翻訳統合設定を設定できます。

## デフォルトの翻訳サービス {#the-default-translation-service}

AEM Communitiesには [試用ライセンス](../../help/sites-administering/tc-msconf.md#microsoft-translator-trial-license) の [デフォルトの翻訳サービス](../../help/sites-administering/tc-msconf.md) 複数の言語で有効になっています。

条件 [コミュニティサイトの作成](sites-console.md)の場合、デフォルトの翻訳サービスは、 `Allow Machine Translation` が [翻訳](sites-console.md#translation) サブパネル。

>[!CAUTION]
>
>デフォルトの翻訳サービスはデモ用です。
>
>実稼動システムの場合は、ライセンスされた翻訳サービスが必要です。 ライセンスがない場合、デフォルトの翻訳サービスを [オフにする](../../help/sites-administering/tc-msconf.md#microsoft-translator-trial-license-geometrixx-outdoors).

## UGC のグローバル翻訳 {#global-translation-of-ugc}

Web サイトに複数の [言語コピー](../../help/sites-administering/tc-prep.md)に設定されている場合、あるサイトに入力された UGC が別のサイトに入力された UGC に関連している可能性があることをデフォルトの翻訳サービスが認識しません。 これは、UGC が同じコンポーネント（コンポーネントを含むページの言語コピー）によって生成される場合に当てはまります。

トピックについて話し合う人々のグループに似ています。 彼らは、大きなグループの誰もが 1 つの会話に参加するのに比べて、自分のグループ以外のグループで行われたコメントに気づかない。

「1 つのグループでの会話」が必要な場合は、複数の言語コピーを持つ Web サイト全体でグローバル翻訳を有効にして、どの言語コピーから表示されているかに関係なく、スレッド全体を表示できます。

例えば、ベースサイト上にフォーラムが確立され、言語コピーが作成され、グローバル翻訳が有効になっている場合、1 つの言語コピーでフォーラムに投稿されたトピックがすべての言語コピーに表示されます。 返信元の言語コピーが入力された言語に関係なく、返信に対しても同じことが言えます。 その結果、トピックが表示されている言語コピーに関係なく、トピックと返信のスレッド全体が表示されます。

>[!CAUTION]
>
>グローバル翻訳前に存在していた UGC は表示されなくなりました。
>
>UGC が [共通店](working-with-srp.md)に設定されている場合は、言語固有の UGC の場所の下に配置されますが、グローバル翻訳の設定後に追加された新しいコンテンツは、グローバル共有ストアの場所から取得されます。
>
>言語固有のコンテンツをグローバル共有ストアに移動または結合するための移行ツールは用意されていません。

### 翻訳統合の設定 {#translation-integration-configuration}

翻訳統合を作成するには、翻訳サービスコネクタをオーサーインスタンス上の Web サイトに統合します。

* 管理者としてログイン
* 次から： [メインメニュー](http://localhost:4502/)
* 「**[!UICONTROL ツール]**」を選択します
* 選択 **[!UICONTROL 運用]**
* 選択 **[!UICONTROL クラウド]**
* 選択 **[!UICONTROL Cloud Service]**
* 下にスクロールして **[!UICONTROL 翻訳の統合]**

  ![translation-integration](assets/translation-integration.png)

* 選択 **[!UICONTROL 設定を表示]**

  ![show-configuration](assets/translation-integration1.png)

* 選択 `[+]` 隣のアイコン **[!UICONTROL 利用可能な設定]** 設定を作成できます。

#### 設定を作成ダイアログ {#create-configuration-dialog}

![create-configuration](assets/translation-integration2.png)

* **[!UICONTROL 親設定]**

  （必須）通常はデフォルトのままにします。 デフォルトは `/etc/cloudservices/translation` です。

* **[!UICONTROL タイトル]**

  （必須）任意の表示タイトルを入力します。 デフォルト値はありません。

* **[!UICONTROL 名前]**

  （オプション）設定の名前を入力します。 初期設定は、タイトルに基づくノード名です。

* 選択 **[!UICONTROL 作成]**

#### 翻訳設定ダイアログ {#translation-config-dialog}

![configuration-dialog](assets/translation-integration3.png)

詳しい手順については、 [翻訳統合設定の作成](../../help/sites-administering/tc-tic.md#creating-a-translation-integration-configuration).

* **[!UICONTROL Sites]** タブ：デフォルトのままにできます。

* **[!UICONTROL Communities]** タブ：
   * **[!UICONTROL 翻訳プロバイダー]**
ドロップダウンリストから翻訳プロバイダーを選択します。 デフォルトはです。 `microsoft`、試用サービス。

   * **[!UICONTROL コンテンツカテゴリ]**
翻訳されるコンテンツを説明するカテゴリを選択します。 初期設定は です。`General.`

   * **[!UICONTROL ロケールを選択…]**
（オプション）UGC を保存するロケールを選択すると、すべての言語コピーからの投稿が 1 つのグローバル会話に表示されます。 慣例により、 [ベース言語](sites-console.md#translation) を参照してください。 選択 `No Common Store` グローバル翻訳を無効にします。 デフォルトでは、グローバル翻訳は無効になっています。

* **[!UICONTROL Assets]** タブ：デフォルトのままにできます。
* 選択 **[!UICONTROL OK]**

#### アクティベーション {#activation}

新しい翻訳統合クラウドサービスをパブリッシュ環境に対してアクティブ化する必要があります。 Web サイトに関連付けられている場合、まだアクティベートされていない場合、関連付けられているページが公開される際に、アクティベーションワークフローによって、このクラウドサービス設定の公開が求められます。

## 翻訳設定の管理 {#managing-translation-settings}

>[!NOTE]
>
>**優先言語**
>
>投稿が優先言語とは異なる言語であるかどうかを検出する場合は、サイト訪問者の優先言語を確立する必要があります。
>
>優先言語とは、サイト訪問者がサインインし、言語の設定を指定した場合にユーザーのプロファイルで設定される言語の設定です。
>
>サイト訪問者が匿名の場合、またはプロファイルで言語設定が指定されていない場合、優先言語はページテンプレートの基本言語になります。

### ユーザーの環境設定 {#user-preference}

#### ユーザープロファイル {#user-profile}

すべてのコミュニティサイトは、サインインしたメンバーが編集して、自分自身をコミュニティに特定し、自分の環境設定を設定できるユーザープロファイルを提供します。

その 1 つは、コミュニティのコンテンツを常に優先言語で表示するかどうかです。 デフォルトでは、設定は設定されておらず、デフォルトではシステム設定になります。 この設定を [ オン ] または [ オフ ] に変更して、システム設定を上書きできます。

ページがユーザーの優先言語に自動翻訳される場合でも、元のテキストを表示し、翻訳を改善するための UI が引き続き利用可能になります。

![ユーザープロファイル](assets/translation-integration4.png)

### コミュニティサイト設定 {#community-site-setting}

コミュニティサイトを作成する際に、翻訳オプションを有効にして設定できます。 翻訳設定は、匿名のサイト訪問者が表示できるコンテンツに対して有効ですが、ユーザーのプロファイル設定によって上書きされます。
