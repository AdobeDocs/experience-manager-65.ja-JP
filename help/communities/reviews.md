---
title: レビューおよびレビューの概要（表示）の使用
description: ページにレビューおよびレビューの概要コンポーネントを追加する方法を説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 170414a6-c40b-4ad2-9294-7c2266850c3d
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1290'
ht-degree: 2%

---

# レビューおよびレビューの概要（表示）の使用 {#using-reviews-and-reviews-summary-display}

この `Reviews` コンポーネントは、 [コメント](comments.md) および [評価](rating.md) コンポーネントを使用する準備が整いました。

この `Reviews Summary (Display)` コンポーネントは、のアクティブまたはクローズドインスタンスの概要を提供します `Reviews` サイトの他の場所に表示するコンポーネント。

>[!NOTE]
>
>レビューの匿名投稿はサポートされていません。 サイト訪問者が参加するには、登録（メンバーになる）とログインが必要です。 ログインした訪問者はいつでもレビューを更新できます。

## ページへのレビューの追加 {#adding-a-review-to-a-page}

を追加します `Reviews` オーサーモードのページにコンポーネントを追加する場合は、コンポーネントブラウザーを使用して次を見つけます `Communities / Reviews` そして、ユーザーがレビューできるように、ページ上の位置（機能に対する相対的な位置など）にドラッグします。

詳細については、 [Communities コンポーネントの基本](basics.md).

いつ [必要なクライアントサイドライブラリ](reviews-basics.md#essentials-for-client-side) が含まれる場合、このようにして `Reviews` コンポーネントが表示されます。

![create-review](assets/create-review.png)

## レビューの設定 {#configuring-reviews}

配置されたを選択します。 `Reviews` にアクセスして選択できるコンポーネント `Configure` アイコンをクリックします。このアイコンをクリックすると、編集ダイアログが開きます。

![configure-new](assets/configure-new.png)

の下 **[!UICONTROL 許可された評価]** タブで、メンバーに表示する評価の完全なリストを指定します。 最初の評価は、の平均評価を提供する評価なので、全体/一般評価にする必要があります。 `Review Summary (Display)` コンポーネント。 デフォルト設定の次の 2 つの評価には、「サブレート 1」または「サブレート 2」以外の別のタイトルを付ける必要があります。

![許可された評価](assets/configure-review1.png)

* **[!UICONTROL 許可された評価]**

  メンバーが選択できる評価のリスト。

  上向き矢印、下向き矢印、削除ボタンを使用して、表示されている選択項目を変更します。

  クリック **[!UICONTROL 項目を追加]** 別の評価の選択肢を追加します。

の下 **[!UICONTROL Required Ratings]** タブで、のリストから項目を再入力します **[!UICONTROL 許可された評価]** 評価には必須です。 アイテムが [ 許可された評価 ] タブでのみ指定されている場合、メンバーによって送信されたときにマークが付いていない状態になることがあります。

Web サイトでは、必須の評価にはアスタリスクが付いています。 アイテムが必須であり、マークされていない場合、メッセージがメンバーに表示され、すべての必要な評価がマークされるまで送信が拒否されます。

![必須評価](assets/configure-review2.png)

* **[!UICONTROL Required Ratings]**

  許可された評価のサブセット。必要な評価を示します。

  上向き矢印、下向き矢印、削除ボタンを使用して、表示されている選択項目を変更します。

  クリック **[!UICONTROL 項目を追加]** 別の応答選択を追加します。

>[!NOTE]
>
>項目が次に入力された場合 **[!UICONTROL Required Ratings]** で指定されていないタブ **[!UICONTROL 許可された評価]** タブ、それは評価する項目に含まれていません。

の下 **[!UICONTROL レビュー]** タブで、レビューの処理方法を指定します。

![レビュー](assets/configure-review3.png)

* **[!UICONTROL 返信を許可]**

  オンにすると、レビューへの返信が許可されます。 デフォルトではオフになっています。

* **[!UICONTROL クローズ]**

  オンにした場合、レビューは新しいレビューと返信に対してクローズされます。 デフォルトではオフになっています。

* **[!UICONTROL ファイルのアップロードを許可]**

  オンにした場合、レビュー用に添付ファイルをアップロードできます。 デフォルトではオフになっています。

* **最大ファイル サイズ**

  次の場合にのみ該当： **[!UICONTROL ファイルのアップロードを許可]** がチェックされます。 このフィールドでは、アップロードするファイルのサイズ（バイト単位）を制限します。 デフォルトは 10 MB です。

* **[!UICONTROL 最大メッセージ長]**

  テキストボックスに入力できる最大文字数。 デフォルトは 4096 文字です。

* **[!UICONTROL 許可されるファイルタイプ]**

  次の場合にのみ該当： **[!UICONTROL ファイルのアップロードを許可]** がチェックされます。 「ドット」区切り文字を使用したファイル拡張子のコンマ区切りリスト。 例：.jpg、.jpeg、.png、.doc、.docx、.pdf いずれかのファイルタイプを指定した場合、指定していないファイルタイプは許可されません。 デフォルトは、すべてのファイルタイプが許可されるように、何も指定されていません。

* **[!UICONTROL リッチテキストエディター]**

  オンにすると、マークアップを使用して投稿を入力できます。 デフォルトではオフになっています。

* **[!UICONTROL 投票を許可]**

  オンにした場合は、トピックの投票機能を含めます。 デフォルトではオフになっています。

の下 **[!UICONTROL ユーザーのモデレート]** タブで、投稿されたレビューの管理方法を指定します。 詳しくは、を参照してください [ユーザー生成コンテンツのモデレート](moderate-ugc.md).

![user-moderation](assets/configure-review4.png)

* **[!UICONTROL 事前モデレート]**

  オンにした場合、レビューは公開サイトに表示される前に承認する必要があります。 デフォルトではオフになっています。

* **[!UICONTROL レビューの削除]**

  オンにした場合、レビューを投稿したメンバーはレビューを削除できます。 デフォルトではオフになっています。

* **[!UICONTROL レビューを拒否]**

  オンにすると、モデレーターがレビューを拒否できるようになります。 デフォルトではオフになっています。

* **[!UICONTROL レビューを閉じる/再度開く]**

  オンにした場合、モデレーターがレビューを閉じて再度開くことを許可します。 デフォルトではオフになっています。

* **[!UICONTROL フラグのレビュー]**

  オンにした場合、メンバーが不適切なレビューとしてフラグを立てることを許可します。 デフォルトではオフになっています。

* **[!UICONTROL フラグの理由リスト]**

  オンにすると、メンバーは、レビューで不適切なフラグを設定した理由をドロップダウンリストから選択できます。 デフォルトではオフになっています。

* **[!UICONTROL カスタムフラグの理由]**

  オンにした場合、レビューに不適切なフラグを設定する独自の理由をメンバーが入力できるようになります。 デフォルトではオフになっています。

* **[!UICONTROL モデレートしきい値]**

  モデレーターに通知を送信する前に、レビューがメンバーによってフラグ付けされる必要がある回数を入力します。 デフォルトは 1 回（1）です。

* **[!UICONTROL フラグの上限]**

  レビューが公開ビューで非表示になるまでにフラグを付ける必要がある回数を入力します。 この数は、以上である必要があります **[!UICONTROL モデレートしきい値]**. デフォルトは 5 です。

### ページへのレビューの概要（表示）の追加 {#adding-a-review-summary-display-to-a-page}

を追加します `Reviews Summary (Display)` オーサーモードのページへのコンポーネントの移動

* `Communities / Reviews Summary (Display)`

アクティブまたはクローズ済みのレビューの概要を表示するページの上にドラッグします。

詳細については、 [Communities コンポーネントの基本](basics.md).

いつ [必要なクライアントサイドライブラリ](reviews-basics.md#essentials-for-client-side) が含まれる場合、このようにして `Reviews Summary (Display)`コンポーネントが表示されます。

![review-summary](assets/configure-review5.png)

>[!NOTE]
>
>「平均」は、要約されているレビューの「許可されている評価」タブにリストされている最初の項目の投票を反映しています。

### レビューの概要の設定（表示） {#configuring-reviews-summary-display}

配置されたを選択します。 `Reviews Summary (Display)` にアクセスして選択できるコンポーネント `Configure` アイコンをクリックします。このアイコンをクリックすると、編集ダイアログが開きます。

![設定](assets/configure-new.png)

の下 **[!UICONTROL 概要を確認]** タブ

![review-summary](assets/configure-review6.png)

* `Review Path`

  を入力するか、配置したインスタンスを参照します。 `reviews` コンポーネントを使用すると、例えばを以下の web ページに追加した場合に、要約できます。 [Geometrixxエンゲージメントサイト](getting-started.md) パスは次のようになります。

  `/content/sites/engage/en/page/jcr:content/content/primary/reviews`

* `Include histogram`

  オンにした場合、要約されているレビューの星評価の数を示す棒グラフの表示を含めます。 デフォルトではオフになっています。

### カスタムレビュータイプへの変更 {#changing-to-a-custom-review-type}

レビューコンポーネントでは、コメントシステムを使用します。

コメントリソースタイプを変更すると、コメントシステムはデフォルトを使用してコメントのインスタンスを生成しなくなり、開発者によってカスタマイズ（拡張）されたインスタンスを生成します。

カスタムリソースタイプがわかっている場合は、次のように入力します [デザインモード](../../help/sites-authoring/default-components-designmode.md) 配置されたをダブルクリックします。 `Comments` コンポーネント：追加のタブを持つダイアログを開きます。

の下 **[!UICONTROL リソースタイプ]** タブで、の新しいインスタンスのカスタム resourceType を指定します。 `Comments or Voting` コンポーネント：

![comments-voting](assets/configure-review7.png)

* **[!UICONTROL コメントリソースタイプ]**

  拡張されたの resourceType に移動します `comment`/apps 内のコンポーネント（単一のコメント）。 例えば、`/apps/social/commons/components/hbs/comments/comment` のように指定します。

  このリソースは、訪問者がコメントを投稿する際に作成された UGC の resourceType を識別します。

* **[!UICONTROL 投票リソースタイプ]**

  拡張されたの resourceType に移動します `voting`/apps 内のコンポーネント。 例えば、`/apps/social/components/hbs/voting` のように指定します。

  このリソースは、訪問者が投票を投稿する際に作成された UGC のリソースタイプを識別します。

* **[!UICONTROL コメントシステムのリソースタイプ]**

  拡張されたの resourceType に移動します `comments`コンポーネント（コメントシステム）:/apps ページテンプレート以外は空白のままにします [動的に含める](scf.md#add-or-include-a-communities-component) ページにリソースとして追加されるのではなく、基になるスクリプトのコメントシステム（コメントノード）。 詳しくは、 [`{{include}}` helper](handlebars-helpers.md#include).

## サイト訪問者エクスペリエンス {#site-visitor-experience}

### モデレーターと管理者 {#moderators-and-administrators}

ログインしたユーザーがモデレーターまたは管理者権限を持っている場合、レビューの作成者に関係なく、コンポーネントの設定で許可されたモデレートタスクを実行できます。

### メンバー {#members}

サイト訪問者がログインすると、設定に応じて、次の操作を行うことができます。

* 新しいレビューを投稿
* 独自のレビューを編集
* 独自のレビューを削除
* 他のユーザーのレビューコメントにフラグを付ける

メンバーごとに 1 つの評価のみが許可されます。 会員は、いつでも格付けを変更することができる。

### 匿名 {#anonymous}

ログインしていないサイト訪問者は、投稿されたレビューを読んだり、サポートされている場合は翻訳したりすることしかできませんが、評価やレビューを追加したり、他のユーザーのレビューコメントにフラグを立てたりすることはできません。

## 追加情報 {#additional-information}

詳しくは、 [Essentials のレビュー](reviews-basics.md) 開発者向けのページです。

投稿されたコメントのモデレートについては、次を参照してください [ユーザー生成コンテンツのモデレート](moderate-ugc.md).

投稿されたコメントの翻訳については、を参照してください [ユーザー生成コンテンツの翻訳](translate-ugc.md).
