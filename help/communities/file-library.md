---
title: ファイルライブラリ機能
seo-title: ファイルライブラリ機能
description: ファイルライブラリ機能により、サインインしたサイト訪問者がファイルをアップロード、管理、ダウンロードできるようになります
seo-description: ファイルライブラリ機能により、サインインしたサイト訪問者がファイルをアップロード、管理、ダウンロードできるようになります
uuid: e78a90bd-f1d3-44f8-98eb-1498a55e8217
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: ea2b23af-49c3-409b-a041-43c42d846f21
docset: aem65
translation-type: tm+mt
source-git-commit: 58a06c1a16c62bffad2893fbec0b32d2ce7267a7

---


# ファイルライブラリ機能{#file-library-feature}

## 概要 {#introduction}

ファイルライブラリ機能は、サインインしているサイト訪問者（コミュニティメンバー）がコミュニティサイト内でファイルをアップロード、管理およびダウンロードする場所を提供します。

ドキュメントのこのセクションでは、以下の内容について説明します。：

* AEMサイトへのファイルライブラリ機能の追加
* Configuration settings for the `File Library` component.

### ファイルライブラリをページに追加 {#adding-a-file-library-to-a-page}

To add a `File Library` component to a page in author mode, locate the component

* `Communities / File Library`

コンポーネントを探し、ページ上の位置にドラッグします。

For necessary information, visit [Communities Components Basics](/help/communities/basics.md).

When the [required client-side libraries](/help/communities/essentials-file-library.md#essentials-for-client-side) are included, this is how the `File Library` component will appear:

![chlimage_1-145](assets/chlimage_1-145.png)

### ファイルライブラリの設定 {#configuring-file-library}

Select the placed `File Library` component to access and select the `Configure` icon which opens the edit dialog.

![chlimage_1-146](assets/chlimage_1-146.png) ![forum-config-1](assets/forum-config-1.png)

#### 「コメント」タブ{#comments-tab}

「**コメント**」タブでは、アップロードしたファイルに対するコメントを表示するかどうかと、その方法を指定します。

* **ファイルへのコメントを許可**

   オンの場合、アップロードされたファイルに対するコメントを許可します。 初期設定はオフです。

* **1 ページのコメント数**

   1ページに表示するコメントの数と表示する返信の数を制限します。 デフォルトは **10** です。

* **最大ファイルサイズ**

   この値によって、アップロードするファイルサイズが制限されます。デフォルトの制限は104857600(10 Mb)です。

* **メッセージの最大長**

   テキストボックスに入力できる最大文字数。 初期設定は 4096 文字です。

* **許可されるファイルタイプ**

   ドット付きのファイル拡張子をコンマ区切りで指定します（例：.jpg, .jpeg, .png, .doc, .docx, .pdf）。ファイルの種類を指定すると、指定されていないファイルは許可されません。 デフォルトでは、すべてのファイルタイプが許可されるように指定されていません。

* **リッチテキストエディター**

   チェックすると、コメントがマークアップと共に入力される場合があります。 初期設定はオフです。

* **コメントを削除**

   このオプションを選択すると、ユーザーは自分のコメントを削除できます。 初期設定はオンです。

* **タグ付けを許可**

   チェックすると、ファイルにタグを追加する機能が有効になります。 初期設定はオフです。

* **許可された名前空間**

   「タグ付けを許可」を選択すると、使用可能なタグは、選択した名前空間に限定されます。 名前空間が選択されていない場合、すべての名前空間が許可されます。初期設定はすべての名前空間です。

* **推奨の制限**

   「タグ付けを許可」をオンにした場合、この設定により、表示する推奨タグの数が制限されます。 -1 に設定した場合、制限はありません。初期設定は -1 です。

* **投票を許可**

   オンにすると、ファイルの投票機能が有効になります。 初期設定はオフです。

* **フォローを許可**

   If checked, include the following feature for blog articles, which allows members to be [notified](/help/communities/notifications.md) of new posts. 初期設定はオフです。

* **メンションを有効化**

   有効にすると、登録済みコミュニティユーザーは、他の登録済みメンバー（名、姓、ユーザー名を使用）を識別し、共通の@user-name構文を使用してタグ付けできます。 タグ付きユーザーは、メンションに関する通知を受信します。

* **最大メンション数**

   投稿で許可するメンションの最大数を制限します。 初期設定は 10 です。

* **UI メンションパターン**

   投稿内の登録ユーザーにタグ(@mention)を付けるために許可されたパターン文字列を指定します。 例：～{{familyName}}{{givenName}}

* **スレッド化された返信を許可**

   オンの場合、投稿されたコメントへの返信を許可します。 初期設定はオフです。

#### 「ユーザーモデレート」タブ {#user-moderation-tab}

「**ユーザーモデレート**」タブでは、コメントが許可されている場合に、コメントのモデレートを設定します。

* **事前モデレート**

   このチェックボックスをオンにすると、コメントは発行サイトに表示される前に承認する必要があります。 初期設定はオフです。

* **コメントを削除**

   オンにすると、訪問者がコメントを投稿したときに、コメントを削除する機能が提供されます。 初期設定はオンです。

* **コメントを拒否**

   オンにした場合、信頼できるメンバーのモデレーターがコメントを拒否することを許可します。 初期設定はオフです。

* **コメントを閉じる / 再度開く**

   オンにした場合、信頼できるメンバーのモデレーターがコメントを閉じて再度開くことを許可します。 初期設定はオフです。

* **コメントにフラグを設定**

   このオプションを選択すると、訪問者はコメントに不適切なフラグを付けることができます。 初期設定はオフです。

* **フラグ設定理由リスト**

   このオプションを選択すると、訪問者は、コメントに不適切なフラグを付ける理由をドロップダウンリストから選択できます。 初期設定はオフです。

* **カスタムフラグ設定理由**

   このオプションを選択すると、訪問者はコメントに不適切なフラグを付ける理由を入力できます。 初期設定はオフです。

* **モデレートのしきい値**

   モデレーターに通知する前に、コメントに訪問者がフラグを付ける必要のある回数を入力します。 Default is one time (**1**).

* **フラグ付けの制限**

   コメントが公開表示に表示される前にフラグ付けされる必要がある回数を入力します。 This number must be greater than or equal to the **Moderation Threshold**. 初期設定は 5 です。

### 「並べ替え設定」タブ{#sort-settings-tab}

並べ替え

デフォルトとして設定

### 追加情報 {#additional-information}

More information may be found on the [File Library Essentials](/help/communities/essentials-file-library.md) page for developers.

投稿されたトピックとコメントのモデレートについては、[ユーザー生成コンテンツのモデレート](/help/communities/moderate-ugc.md)を参照してください。

投稿されたトピックとコメントのタグ付けについては、[ユーザー生成コンテンツのタグ付け](/help/communities/tag-ugc.md)を参照してください。
