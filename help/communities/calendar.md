---
title: カレンダー機能
seo-title: カレンダー機能
description: コミュニティイベント情報をカレンダー形式で提供します
seo-description: コミュニティイベント情報をカレンダー形式で提供します
uuid: 262f6afa-d8aa-4815-8440-a8ed5668c76d
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 70fa0b9c-cb98-45c4-9c94-bef4a9f3741e
docset: aem65
translation-type: tm+mt
source-git-commit: 5b8b1544645465d10e7c2018364b6a74f1ad9a8e

---


# カレンダー機能 {#calendar-feature}

## 概要 {#introduction}

カレンダー機能は、すべてのサイト訪問者またはサインインしているサイト訪問者（コミュニティメンバー）のみが閲覧できるコミュニティイベント情報をカレンダー形式で提供します。イベントを追加できるのは許可されたメンバーだけです。

ドキュメントのこのセクションでは、以下の内容について説明します。

* カレンダー機能のAEMサイトへの追加
* Configuration settings for `Calendar`components

## カレンダーをページに追加 {#adding-a-calendar-to-a-page}

To add a `Calendar` component to a page in author mode, use the component browser to locate

* `Communities / Calendar`

コンポーネントを探し、ページ上の適切な位置（ユーザーにレビューしてもらう機能の近くなど）にドラッグします。

For necessary information, visit [Communities Components Basics](/help/communities/basics.md).

When the [required client-side libraries](/help/communities/calendar-basics-for-developers.md#essentials-for-client-side) are included, this is how the `Calendar` component will appear.

![chlimage_1-147](assets/chlimage_1-147.png)

### カレンダーの設定 {#configuring-calendar}

Select the placed `Calendar`component to access and select the `Configure` icon which opens the edit dialog.

![chlimage_1-148](assets/chlimage_1-148.png) ![chlimage_1-149](assets/chlimage_1-149.png)

#### 「設定」タブ{#settings-tab}

Under the **Settings** tab, specify whether or not to allow tags to be applied to calendar entries.

* **1 ページのイベント数**

   1ページに表示するイベントの数を定義します。 初期設定は 10 です。

* **モデレート**

   オンにした場合、カレンダーイベントとコメントの投稿は、公開サイトに表示される前に承認する必要があります。 初期設定はオフです。

* **閉じる**

   このオプションを選択すると、カレンダーは新しいイベントエントリとコメントに閉じられます。 初期設定はオフです。

* **リッチテキストエディター**

   チェックすると、カレンダーイベントとコメントがマークアップと共に入力される場合があります。 初期設定はオンです。

* **タグ付けを許可**

   If checked, allow members to add tag labels to the events they post (see **Tag field** tab). 初期設定はオンです。

* **ファイルのアップロードを許可**

   このオプションを選択すると、添付ファイルをカレンダーイベントまたはコメントに追加できます。 初期設定はオンです。

* **フォローを許可**

   このオプションを選択すると、カレンダーに投稿されたイベントをメンバーがフォローできるようになります。 初期設定はオンです。

* **最大ファイルサイズ**

   がオンの場合のみ `Allow File Uploads` 関連します。 このフィールドは、アップロードされるファイルのサイズ（バイト単位）を制限します。 初期設定は104857600(10 Mb)です。

* **許可されるファイルタイプ**

   がオンの場合のみ `Allow File Uploads` 関連します。 ドット付きのファイル拡張子をコンマ区切りで指定します（例：.jpg, .jpeg, .png, .doc, .docx, .pdf）。ファイルの種類が指定されている場合、指定されていないファイルはアップロードできません。 初期設定は、すべてのファイルタイプが許可されるように指定されない。

* **添付する画像ファイルの最大サイズ**

   「ファイルのアップロードを許可」がオンの場合にのみ関連します。 アップロードされた画像ファイルの最大バイト数。 デフォルトは2097152* **(2 Mb)です。

* **許可されるカバー画像タイプ**

   「ドット」区切り文字を使用した画像ファイル拡張子のコンマ区切りリスト。 デフォルトは `.jpg,.jpeg,.png,.gif,.bmp` です。

* **スレッド化された返信を許可**

   オンにすると、カレンダーイベントに投稿されたコメントへの返信を許可します。 初期設定はオンです。

* **ユーザーによるコメントおよびイベントの削除を許可**

   オンにすると、メンバーは投稿したコメントやカレンダーイベントを削除できます。 初期設定は** **チェック済みです。

* **投票を許可**

   オンにした場合、カレンダーイベントに投票機能を含めます。 初期設定はオンです。

* **パンくずリストを表示**

   イベントページのパンくずリストを表示します. 初期設定はオンです。

* **日付範囲フィルター**

   カレンダーイベントリストのページフィルターの「終了日」の値を計算するために、現在の日付に追加する日数を定義します。 初期設定値は30です。

* **おすすめコンテンツを許可**

   If checked, the idea is able to be identified as [featured content](/help/communities/featured.md). 初期設定はオフです。

Under the **User Moderation** tab, specify how the posted topics and replies (user generated content) are managed. For more information, see [Moderating User Generated Content](/help/communities/moderate-ugc.md).

#### 「ユーザーモデレート」タブ{#user-moderation-tab}

* **投稿を拒否**

   このオプションを選択すると、信頼できるメンバーのモデレーターは、投稿を拒否し、投稿が公開フォーラムに表示されないようにします。 初期設定はオンです。

* **イベントを閉じる / 再度開く**

   このオプションを選択すると、信頼できるメンバーのモデレーターがイベントを閉じて、さらに編集やコメントを行ったり、イベントを再度開いたりできます。 初期設定はオンです。

* **投稿にフラグを設定**

   このオプションを選択すると、他のユーザーのイベントやコメントに不適切なフラグを付けることができます。 デフォルトはチェック済み**です。**

* **フラグ設定理由リスト**

   このオプションを選択すると、イベントやコメントに不適切なフラグを付ける理由を、ドロップダウンリストからメンバーが選択できるようになります。 初期設定はオフです。

* **カスタムフラグ設定理由**

   このオプションを選択すると、イベントやコメントに不適切なフラグを付ける理由をメンバーが自分で入力できるようになります。 初期設定はオフです**。**

* **モデレートのしきい値**

   モデレーターに通知する前に、メンバーがイベントまたはコメントにフラグを付ける必要がある回数を入力します。 初期設定は1（1回）です。

* **フラグ付けの制限**

   イベントまたはコメントが公開ビューに表示されなくなる前にフラグ付けされる必要がある回数を入力します。 -1に設定した場合、フラグ付けされたトピックまたはコメントは公開ビューで非表示になりません。 そうでない場合、この数値はモデレートしきい値以上にする必要があります。 初期設定は 5 です。

#### 「タグフィールド」タブ{#tag-field-tab}

「**タグフィールド**」タブでは、「**設定**」タブでタグ付けが許可されている場合に、適用できるタグを名前空間に従って制限します。

* **許可された名前空間**

   「**設定**」 `Allow Tagging` タブでチェックされている場合に関連します。 適用できるタグは、チェックされた名前空間カテゴリ内のタグに制限されます。 名前空間のリストには、「Standard Tags」（デフォルトの名前空間）と「Include All Tags」が含まれます。 初期設定はオフで、すべての名前空間が許可されます。

* **推奨の制限**

   フォーラムへの投稿に対して提案として表示するタグの数を入力します。 初期設定は**-**1 （制限なし）です。

>[!NOTE]
>
>新しいタグ名前空間（分類）の追加方法については、「[タグの管理](/help/sites-administering/tags.md)」を参照してください。

#### 「翻訳」タブ {#translation-tab}

「**翻訳**」タブでは、コミュニティサイトの翻訳が有効になっている場合に、特定の投稿だけでなくスレッド全体（イベントとコメント）を翻訳するかどうかを設定できます。

* **すべてを翻訳**

   オンにすると、イベントとコメントがユーザーの好みの言語に変換されます。 初期設定はオンです。

## サイト訪問者のエクスペリエンス {#site-visitor-experience}

パブリッシュ環境では、カレンダー機能はデフォルトの日付範囲を持つ検索フィールドと、その範囲内に含まれるすべてのカレンダーイベントを表示します。

カレンダーイベントを選択すると、その詳細、説明およびコメントが表示されます。

その他の機能は、サイト訪問者がモデレーターか、管理者か、コミュニティメンバーか、権限を持つメンバーか、匿名かによって異なります。

### モデレーターおよび管理者 {#moderators-and-administrators}

サインインしているユーザーがモデレーター権限または管理者権限を持っている場合は、すべてのカレンダーイベントと、イベントに投稿されたコメントに対して、（コンポーネントの設定で許可されている）[モデレートタスク](/help/communities/moderate-ugc.md)を実行できます。

![chlimage_1-150](assets/chlimage_1-150.png)

#### メンバー {#members}

When the signed in user is a community member or [privileged member](/help/communities/users.md#privileged-members-group) (depending on configuration), they are able to select `New Event` to create and post a new calendar event.

具体的には、次のことが考えられます。

* 新しいカレンダーイベントの作成
* カレンダーイベントへのコメントの投稿
* 独自のカレンダーイベントまたはコメントの編集
* 独自のカレンダーイベントまたはコメントの削除
* 他のユーザーのカレンダーイベントまたはコメントにフラグを付ける

![chlimage_1-151](assets/chlimage_1-151.png)![chlimage_1-152](assets/chlimage_1-152.png)

#### 匿名 {#anonymous}

サインインしていないサイト訪問者は、投稿されたカレンダーイベントを閲覧することしかできず（サポートされている場合は翻訳も可）、イベントまたはコメントを追加したり、他のユーザーのイベントまたはコメントにフラグを設定することはできません。

![chlimage_1-153](assets/chlimage_1-153.png)

## 追加情報 {#additional-information}

More information may be found on the [Calendar Essentials](/help/communities/calendar-basics-for-developers.md) page for developers.

カレンダーイベントとコメントのモデレートについては、「[ユーザー生成コンテンツのモデレート](/help/communities/moderate-ugc.md)」を参照してください。

For tagging calendar events and comments, see [Tagging User Generated Content](/help/communities/tag-ugc.md).

For translation of calendar events and comments, see [Translating User Generated Content](/help/communities/translate-ugc.md).
