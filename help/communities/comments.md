---
title: コメントの使用
seo-title: コメントの使用
description: サインインしているサイト訪問者はコメント機能を使用して、意見や知識を共有できます
seo-description: サインインしているサイト訪問者はコメント機能を使用して、意見や知識を共有できます
uuid: 40acd962-846c-483c-b789-aab3a7d2b31b
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 216cfb3e-777e-4773-afba-749debdca000
docset: aem65
exl-id: 30baebd9-13c5-4fde-a494-85601abc32a5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '994'
ht-degree: 32%

---

# コメントの使用 {#using-comments}

## はじめに {#introduction}

サインインしているサイト訪問者（メンバー）は、コメント機能を使用して、サイト上のコンテンツに関する意見や知識を共有できます。この機能は、他の機能に既に存在する場合も多いですが、どのWebサイトにも追加できます。

このドキュメントでは、次の内容について説明します。

* ページに`Comments`を追加しています。
* `Comments`コンポーネントの設定。

>[!NOTE]
>
>匿名でのコメント投稿はサポートされていません。サイト訪問者が参加するには、登録（メンバーになる）し、サインインする必要があります。

### コメントをページに追加 {#adding-comments-to-a-page}

`Comments`コンポーネントをオーサリングモードでページに追加するには、コンポーネントブラウザーを使用して

* `Communities / Comments`

コンポーネントを探し、ページ上の適切な位置（ユーザーにコメントしてもらう機能の近くなど）や、単にページの下部にドラッグします。

必要な情報については、[コミュニティコンポーネントの基本](/help/communities/basics.md)を参照してください。

[必須のクライアント側ライブラリ](/help/communities/essentials-comments.md#essentials-for-client-side)を含めると、`Comments`コンポーネントは次のように表示されます。

![comments-component](assets/comments-component.png)

>[!NOTE]
>
>1つのページに存在できる`Comments`コンポーネントは1つだけです。 一部のコミュニティ機能には、ブログ、カレンダー、フォーラム、Q&amp;A、レビューなどのコメントが既に含まれています。

### コメントの設定 {#configuring-comments}

配置済みの`Comments`コンポーネントを選択し、`Configure`アイコンを選択すると、編集ダイアログが開きます。

![設定アイコン](assets/configure.png)

![commentsettings](assets/commentssettings.png)

#### 「コメント」タブ{#comments-tab}

「**コメント**」タブでは、訪問者によるコメントの入力方法を指定します。

* **返信を許可**

   オンにすると、メンバーは既存のコメントに返信できます。 デフォルト値はオフです。

* **1 ページのコメント数**

   1ページに表示するコメントの数と表示する返信の数を制限します。 初期設定は 10 です。

* **ファイルのアップロードを許可**

   オンにすると、ファイルをアップロードするオプションにテキスト入力ボックスが表示されます。 デフォルト値はオフです。

* **最大ファイルサイズ**

   「ファイルのアップロードを許可」がオンの場合にのみ関連します。 この値は、アップロードするファイルのサイズを制限します。 デフォルトは 10 MB です。

* **メッセージの最大長**

   テキストボックスに入力できる最大文字数。 初期設定は 4096 文字です。

* **許可されるファイルタイプ**

   「ファイルのアップロードを許可」がオンの場合にのみ関連します。 区切り文字「ドット」を使用したファイル名拡張子のコンマ区切りリスト。 例：.jpg, .jpeg, .png, .doc, .docx, .pdf）。ファイルタイプを指定した場合、指定しなかったファイルは許可されません。 デフォルトでは、すべてのファイルタイプが許可されるように指定されていません。

* **リッチテキストエディター**

   オンにすると、コメントはマークアップを使用して入力されます。 デフォルト値はオフです。

* **投票を許可**

   オンにすると、上下に投票するオプションにテキスト入力ボックスが表示されます。 デフォルト値はオフです。

* **フォローを許可**

   オンにすると、メンバーはコメントをフォローできます。 デフォルト値はオフです。

* **バッジを表示**

   オンにすると、獲得および授与されたバッジを表示できます。 デフォルト値はオフです。

#### 「ユーザーモデレート」タブ{#user-moderation-tab}

「**ユーザーモデレート**」タブで、投稿されたコメントの管理方法を指定します。 詳しくは、[ユーザー生成コンテンツのモデレート](/help/communities/moderate-ugc.md)を参照してください。

* **事前モデレート**

   オンにすると、コメントを発行サイトに表示する前に承認する必要があります。 デフォルト値はオフです。

* **コメントを削除**

   オンにすると、コメントを投稿したメンバーはコメントを削除できます。 デフォルト値はオフです。

* **コメントを拒否**

   オンにすると、モデレーターはコメントを拒否できます。 デフォルト値はオフです。

* **コメントを閉じる / 再度開く**

   オンにすると、モデレーターはコメントを閉じたり、再度開いたりできます。 デフォルト値はオフです。

* **コメントにフラグを設定**

   オンにすると、メンバーはコメントに「不適切」のフラグを設定できます。 デフォルト値はオフです。

* **フラグ設定理由リスト**

   オンにすると、メンバーはコメントに「不適切」のフラグを設定した理由をドロップダウンリストから選択できます。 デフォルト値はオフです。

* **カスタムフラグ設定理由**

   オンにすると、メンバーはコメントに「不適切」のフラグを設定した独自の理由を入力できます。 デフォルト値はオフです。

* **モデレートのしきい値**

   メンバーがコメントに何回フラグを設定したらモデレーターに通知するかを入力します。 初期設定は1回です。

* **フラグ付けの制限**

   コメントに何回フラグを設定したら、公開表示から非表示にするかを入力します。 この数値は、**モデレートのしきい値**&#x200B;以上にする必要があります。 初期設定は 5 です。

#### 「並べ替え設定」タブ{#sort-settings-tab}

「**並べ替え設定**」タブで、投稿されたコメントを表示する際の並べ替え方法を指定します。

* **並べ替えフィールド**

   プルダウンして、`Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed`または`Most Liked`のいずれかを選択します。

* **並べ替え順序**

   プルダウンして、`Ascending`または`Descending`のいずれかを選択します。

### カスタムコメントタイプへの変更 {#changing-to-a-custom-comment-type}

「コメントリソースタイプ」を変更すると、コメントシステムはデフォルトを使用してコメントのインスタンスを生成しなくなり、開発者がカスタマイズ（拡張）したコメントのインスタンスを生成します。

カスタムリソースタイプがわかったら、[デザインモード](/help/sites-authoring/default-components-designmode.md)に入り、配置された`Comments`コンポーネントをダブルクリックして、追加のタブを含むダイアログを開きます。

「**リソースタイプ**」タブで、`Comments or Voting`コンポーネントの新しいインスタンスのカスタムresourceTypeを指定します。

![resource-type](assets/resource-type.png)

* **コメントリソースタイプ**

   /apps内の拡張`comment`コンポーネント（単一のコメント）のresourceTypeに移動します。 例：`/apps/social/commons/components/hbs/comments/comment`

   このリソースは、訪問者がコメントを投稿したときに作成されるUGCのresourceTypeを識別します。

* **投票リソースタイプ**

   /apps内の拡張`voting`コンポーネントのresourceTypeに移動します。 例：`/apps/social/components/hbs/voting`

   このリソースは、訪問者が投票を投稿したときに作成されるUGCのリソースタイプを識別します。

* **コメントシステムリソースタイプ**

   /apps内の拡張`comments`コンポーネント（コメントシステム）のresourceTypeに移動します。 ページテンプレート[で、コメントシステムが基になるスクリプトにリソース（コメントノード）としてページに追加されるのではなく、](/help/communities/scf.md#add-or-include-a-communities-component)が動的に含まれる場合を除き、空のままにします。 詳しくは、[{{include}}ヘルパー](/help/communities/handlebars-helpers.md#include)を参照してください。

### サイト訪問者のエクスペリエンス {#site-visitor-experience}

#### モデレーターおよび管理者 {#moderators-and-administrators}

サインインしているユーザーがモデレーター権限または管理者権限を持っている場合は、誰がコメントを作成したかにかかわらず、コンポーネントの設定によって許可されているモデレートタスクを実行できます。

#### メンバー {#members}

サイト訪問者がサインインすると、設定に応じて次のことができます。

* 新しいコメントを投稿
* 自分のコメントを編集する
* 自分のコメントを削除する
* 他のユーザーのコメントにフラグを設定する

#### 匿名 {#anonymous}

サインインしていないサイト訪問者は、投稿されたコメントを閲覧することしかできず（サポートされている場合は翻訳も可）、コメントを追加したり、他のユーザーのコメントにフラグを設定することはできません。

### 追加情報 {#additional-information}

詳しくは、開発者向けの[コメントの基本事項](/help/communities/essentials-comments.md)ページを参照してください。

投稿されたコメントのモデレートについては、[ユーザー生成コンテンツのモデレート](/help/communities/moderate-ugc.md)を参照してください。

投稿されたコメントの翻訳については、[ユーザー生成コンテンツの翻訳](/help/communities/translate-ugc.md)を参照してください。
