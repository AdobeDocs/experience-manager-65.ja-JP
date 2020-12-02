---
title: レビューおよびレビューの概要（表示）の使用
seo-title: レビューおよびレビューの概要（表示）の使用
description: レビューおよびレビューの概要コンポーネントをページに追加
seo-description: レビューおよびレビューの概要コンポーネントをページに追加
uuid: bd1ccee7-b26b-4a27-b1ea-89609f5080af
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: bf4e7809-8def-4647-aaa6-3ac36865511f
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '1311'
ht-degree: 33%

---


# レビューおよびレビューの概要（表示）の使用  {#using-reviews-and-reviews-summary-display}

`Reviews`コンポーネントは、[コメント](comments.md)と[評価](rating.md)コンポーネントの組み合わせで、使用可能です。

`Reviews Summary (Display)`コンポーネントは、サイトの他の場所に表示する`Reviews`コンポーネントのアクティブインスタンスまたは閉じたインスタンスの概要を提供します。

>[!NOTE]
>
>匿名でのレビュー投稿はサポートされていません。サイト訪問者は参加するには、登録（会員になる）し、サインインする必要があります。 ログインした訪問者は、いつでもレビューを更新できます。

## レビューをページに追加 {#adding-a-review-to-a-page}

作成者モードで`Reviews`コンポーネントをページに追加するには、コンポーネントブラウザーを使用して`Communities / Reviews`を検索し、ページ上にドラッグして配置します。例えば、ユーザーが確認できる機能に対する相対位置です。

必要な情報については、[Communities Components Basics](basics.md)を参照してください。

[必要なクライアント側ライブラリ](reviews-basics.md#essentials-for-client-side)が含まれる場合、`Reviews`コンポーネントは次のように表示されます。

![作成レビュー](assets/create-review.png)

## レビューの設定 {#configuring-reviews}

アクセスする配置済みの`Reviews`コンポーネントを選択し、編集ダイアログを開く`Configure`アイコンを選択します。

![configure-new](assets/configure-new.png)

「**[!UICONTROL 許可されている評価]**」タブで、メンバーに表示する評価の完全なリストを指定します。 最初の評価は`Review Summary (Display)`コンポーネントの平均評価を提供する評価なので、全体/一般の評価である必要があります。 デフォルト設定の次の2つの評価には、「サブレーティング1」または「サブレーティング2」以外の異なるタイトルを付ける必要があります。

![許可格付け](assets/configure-review1.png)

* **[!UICONTROL 許可された評価]**

   メンバーが選択できる評価のリスト。

   表示される選択肢を変更するには、上向き矢印、下向き矢印および削除ボタンを使用します。

   評価の選択肢を追加するには、「**[!UICONTROL 項目を追加]**」をクリックします。

「**[!UICONTROL 必須の評価]**」タブで、**[!UICONTROL 評価する必要のある評価]**&#x200B;のリストから項目を再入力します。 [評価の許可]タブで項目が指定されていない場合は、その項目がメンバによって送信されたときにマークが付いていない状態になることがあります。

Web サイト上では、必須の評価はアスタリスク付きで表示されます。項目が必須でマークが付いていない場合は、メンバーにメッセージが表示され、必須の評価がすべてマークされるまで送信が拒否されます。

![必須評価](assets/configure-review2.png)

* **[!UICONTROL 必須の評価]**

   許可されている評価のサブセット。必要な評価を示します。

   表示される選択肢を変更するには、上向き矢印、下向き矢印および削除ボタンを使用します。

   回答の選択肢を追加するには、「**[!UICONTROL 項目を追加]**」をクリックします。

>[!NOTE]
>
>**[!UICONTROL 「**[!UICONTROL &#x200B;許可された評価&#x200B;]**」タブで指定されていない「&lt;a0/>必須の評価]**」タブに項目が入力された場合、評価する項目にはその項目が含まれません。

「**[!UICONTROL レビュー]**」タブで、レビューの処理方法を指定します。

![レビュー](assets/configure-review3.png)

* **[!UICONTROL 応答を許可]**

   オンの場合、レビューへの返信を許可します。 初期設定はオフです。

* **[!UICONTROL 閉じる]**

   このオプションを選択すると、レビューは新しいレビューと返信に対して閉じられます。 初期設定はオフです。

* **[!UICONTROL ファイルのアップロードを許可]**

   このオプションを選択すると、レビュー用に添付ファイルをアップロードできます。 初期設定はオフです。

* **最大ファイルサイズ**

   「**[!UICONTROL ファイルのアップロードを許可]**」がオンの場合にのみ関連します。 このフィールドは、アップロードするファイルのサイズ（バイト単位）を制限します。デフォルトは 10 MB です。

* **[!UICONTROL メッセージの最大長]**

   テキストボックスに入力できる最大文字数。 初期設定は 4096 文字です。

* **[!UICONTROL 許可されるファイルタイプ]**

   「**[!UICONTROL ファイルのアップロードを許可]**」がオンの場合にのみ関連します。 ドット付きのファイル拡張子をコンマ区切りで指定します（例：.jpg, .jpeg, .png, .doc, .docx, .pdf）。ファイルの種類を指定すると、指定されていないファイルは許可されません。 初期設定は、すべてのファイルタイプを許可するように指定されません。

* **[!UICONTROL リッチテキストエディター]**

   オンの場合、投稿はマークアップと共に入力される場合があります。 初期設定はオフです。

* **[!UICONTROL 投票を許可]**

   オンの場合、トピックに投票機能を含めます。 初期設定はオフです。

「**[!UICONTROL ユーザーモデレート]**」タブで、投稿されたレビューの管理方法を指定します。 詳しくは、[ユーザー生成コンテンツのモデレート](moderate-ugc.md)を参照してください。

![user-moderation](assets/configure-review4.png)

* **[!UICONTROL 事前モデレート]**

   オンにした場合、レビューが発行サイトに表示される前に、レビューを承認する必要があります。 初期設定はオフです。

* **[!UICONTROL レビューを削除]**

   オンの場合、レビューを投稿したメンバーには、レビューを削除する機能が与えられます。 初期設定はオフです。

* **[!UICONTROL レビューを拒否]**

   オンの場合、モデレーターがレビューを拒否できます。 初期設定はオフです。

* **[!UICONTROL レビューを閉じる / 再度開く]**

   オンにした場合、モデレーターがレビューを閉じて再度開くことを許可します。 初期設定はオフです。

* **[!UICONTROL レビューにフラグを設定]**

   このオプションを選択すると、メンバーは不適切としてレビューにフラグを付けることができます。 初期設定はオフです。

* **[!UICONTROL フラグ設定理由リスト]**

   このオプションを選択すると、レビューに不適切としてフラグを付ける理由をドロップダウンリストから選択できます。 初期設定はオフです。

* **[!UICONTROL カスタムフラグ設定理由]**

   このオプションを選択すると、レビューに不適切としてフラグを付ける場合に、メンバーが自分の理由でレビューを入力できるようになります。 初期設定はオフです。

* **[!UICONTROL モデレートのしきい値]**

   メンバーがレビューにフラグを付ける必要がある回数を入力します。この回数を超えるとモデレーターに通知されます。 初期設定は1回です。

* **[!UICONTROL フラグ付けの制限]**

   レビューが公開表示に表示されなくなるまでにフラグを付ける必要がある回数を入力します。 この数値は、**[!UICONTROL モデレートしきい値]**&#x200B;以上にする必要があります。 初期設定は 5 です。

### レビューの概要（表示）をページに追加 {#adding-a-review-summary-display-to-a-page}

作成者モードで`Reviews Summary (Display)`コンポーネントをページに追加するには、コンポーネントを見つけます

* `Communities / Reviews Summary (Display)`

コンポーネントを探し、ページ上のアクティブなレビューまたは閉じられたレビューを表示する位置にドラッグします。

必要な情報については、[Communities Components Basics](basics.md)を参照してください。

[必要なクライアント側ライブラリ](reviews-basics.md#essentials-for-client-side)が含まれる場合、`Reviews Summary (Display)`コンポーネントは次のように表示されます。

![レビュー概要](assets/configure-review5.png)

>[!NOTE]
>
>「平均」は、要約するレビューの「許可された評価」タブに指定されている最初の項目への投票を反映します。

### レビューの概要（表示）の設定  {#configuring-reviews-summary-display}

アクセスする配置済みの`Reviews Summary (Display)`コンポーネントを選択し、編集ダイアログを開く`Configure`アイコンを選択します。

![設定](assets/configure-new.png)

「**[!UICONTROL レビューの概要]**」タブでは、以下の項目を設定します。

![レビュー概要](assets/configure-review6.png)

* `Review Path`

   集計する`reviews`コンポーネントの配置済みインスタンスを入力または参照します。例えば、[GeometrixxエンゲージメントサイトのWebページに追加した場合、](getting-started.md)のパスは次のようになります。

   `/content/sites/engage/en/page/jcr:content/content/primary/reviews`

* `Include histogram`

   選択した場合、集計するレビューに含まれる各星評価の数を示す棒グラフを表示します。 初期設定はオフです。

### カスタムレビュータイプへの変更 {#changing-to-a-custom-review-type}

レビューコンポーネントは、コメントシステムを使用します。

コメントリソースタイプを変更すると、デフォルトを使用するコメントのインスタンスではなく、開発者によってカスタマイズ（拡張）されたコメントのインスタンスが生成されるようになります。

カスタムリソースタイプがわかったら、[デザインモード](../../help/sites-authoring/default-components-designmode.md)に入り、重複が配置した`Comments`コンポーネントをクリックして、追加のタブを含むダイアログを開きます。

「**[!UICONTROL リソースタイプ]**」タブで、`Comments or Voting`コンポーネントの新しいインスタンスのカスタムresourceTypeを指定します。

![コメント投票](assets/configure-review7.png)

* **[!UICONTROL コメントリソースタイプ]**

   /apps内の拡張`comment`コンポーネント（1つのコメント）のresourceTypeに移動します。 例： `/apps/social/commons/components/hbs/comments/comment`

   このリソースは、訪問者がコメントを投稿したときに作成されたUGCのresourceTypeを識別します。

* **[!UICONTROL 投票リソースタイプ]**

   /apps内の拡張`voting`コンポーネントのresourceTypeに移動します。 例： `/apps/social/components/hbs/voting`

   このリソースは、訪問者が投票を行ったときに作成されたUGCのリソースタイプを識別します。

* **[!UICONTROL コメントシステムリソースタイプ]**

   /apps内の拡張`comments`コンポーネント（コメントシステム）のresourceTypeに移動します。 ページテンプレート[で、コメントシステムが基になるスクリプトに](scf.md#add-or-include-a-communities-component)動的に含まれている場合を除き、ページにリソース（コメントノード）として追加されるのではなく、空白のままにします。 詳しくは、[{{include}}ヘルパー](handlebars-helpers.md#include)を参照してください。

## サイト訪問者のエクスペリエンス {#site-visitor-experience}

### モデレーターおよび管理者 {#moderators-and-administrators}

サインインしているユーザーがモデレーター権限または管理者権限を持っている場合は、誰がレビューを作成したかにかかわらず、コンポーネントの設定によって許可されているモデレートタスクを実行できます。

### メンバー  {#members}

サイト訪問者がログインしたとき、設定に応じて、次の操作が行われます。

* 新しいレビューの投稿
* 自分のレビューの編集
* 自分のレビューの削除
* 他のユーザーのレビューコメントにフラグを付ける

1 人のメンバーが付けられる評価は 1 つだけです。メンバーは、いつでも評価を変更できます。

### 匿名  {#anonymous}

サインインしていないサイト訪問者は、投稿されたレビューを閲覧することしかできず（サポートされている場合は翻訳も可）、評価またはレビューを追加したり、他のユーザーのレビューコメントにフラグを設定することはできません。

## 追加情報 {#additional-information}

詳しくは、開発者向けの[Review Essentials](reviews-basics.md)ページを参照してください。

投稿されたコメントのモデレートについては、[ユーザー生成コンテンツのモデレート](moderate-ugc.md)を参照してください。

投稿されたコメントの翻訳については、[ユーザー生成コンテンツの翻訳](translate-ugc.md)を参照してください。
