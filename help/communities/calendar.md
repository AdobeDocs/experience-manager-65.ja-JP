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
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# カレンダー機能{#calendar-feature}

## 概要 {#introduction}

カレンダー機能は、すべてのサイト訪問者またはサインインしているサイト訪問者（コミュニティメンバー）のみが閲覧できるコミュニティイベント情報をカレンダー形式で提供します。イベントを追加できるのは許可されたメンバーだけです。

ドキュメントのこのセクションでは、以下の内容について説明します。

* カレンダー機能を AEM サイトに追加
* configuration settings for `Calendar`components

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

「**設定**」タブで、カレンダーエントリにタグを適用するかどうかを指定します。

* **1 ページのイベント数** 1 ページに表示するイベント数を定義します。初期設定は 10 です。

* **モデレート**&#x200B;オンにすると、カレンダーイベントおよびコメントの投稿を公開サイト上に表示する前に承認が必要になります。初期設定はオフです。

* **閉じる**&#x200B;オンにすると、カレンダーは新しいイベントエントリやコメントを受け付けなくなります。初期設定はオフです。

* **リッチテキストエディター**&#x200B;オンにすると、マークアップを使用してカレンダーイベントおよびコメントを入力できます。初期設定はオンです。

* **タグ付けを許可**&#x200B;オンにすると、メンバーは自分が投稿したイベントにタグラベルを付加できます（「**タグフィールド**」タブを参照）。初期設定はオンです。

* **ファイルのアップロードを許可**&#x200B;オンにすると、カレンダーイベントまたはコメントに添付ファイルを付加できます。初期設定はオンです。

* **フォローを許可**&#x200B;オンにすると、メンバーはカレンダーに投稿されたイベントをフォローできます。初期設定はオンです。

* **「Max File Size** Relevant only if `Allow File Uploads` is」をオンにした場合。 このフィールドは、アップロードするファイルのサイズ（バイト単位）を制限します。 初期設定は104857600(10 Mb)です。

* **「Allowed File Types** Relevant only if `Allow File Uploads` 」がオンの場合。 ドット付きのファイル拡張子をコンマ区切りで指定します（例：.jpg, .jpeg, .png, .doc, .docx, .pdf）。ファイルタイプを指定した場合、指定しなかったファイルはアップロードできません。 初期設定はnoneで、すべてのファイルタイプが許可されます。

* **「ファイルのアップロードを許可」がオン**&#x200B;になっている場合にのみ、「添付画像ファイルの最大サイズ」が関連します。 アップロードされた画像ファイルの最大バイト数。 初期設定は2097152** **(2 Mb)です。

* **許可されるカバー画像タイプ**&#x200B;ドット付きの画像ファイル拡張子のコンマ区切りリストデフォルトは `.jpg,.jpeg,.png,.gif,.bmp` です。

* **スレッド化された返信を許可**&#x200B;オンにすると、カレンダーイベントに投稿されたコメントへの返信を許可します。初期設定はオンです。

* **ユーザーによるコメントおよびイベントの削除を許可**&#x200B;オンにすると、メンバーは自分が投稿したコメントおよびカレンダーイベントを削除できます。初期設定は** **checkedです。

* **投票を許可**&#x200B;オンにすると、カレンダーイベントに投票機能が組み込まれます。初期設定はオンです。

* **パンくずリストを表示**&#x200B;イベントページにパンくずリストを表示します。初期設定はオンです。

* **日付範囲フィルター**&#x200B;カレンダーイベントリストページフィルターの「終了日」の値を計算するために、現在の日付に追加される日数を定義します。初期設定の数値は30です。

* **おすすめコンテンツを許可**&#x200B;オンにすると、アイデアを[おすすめコンテンツ](/help/communities/featured.md)として指定できます。初期設定はオフです。

「**ユーザーモデレート**」タブで、投稿されたトピックと返信（ユーザー生成コンテンツ）の管理方法を指定します。 For more information, see [Moderating User Generated Content](/help/communities/moderate-ugc.md).

#### 「ユーザーモデレート」タブ{#user-moderation-tab}

* **投稿を拒否**&#x200B;オンにすると、信頼されているメンバーモデレーターが投稿を拒否して、公開フォーラムへの表示を止めることができます。初期設定はオンです。

* **イベントを閉じる／再度開く**&#x200B;オンにすると、信頼されているメンバーモデレーターが、イベントをそれ以上編集およびコメントできないように閉じたり、再度開いたりすることができます。初期設定はオンです。

* **投稿にフラグを設定**&#x200B;オンにすると、メンバーは他のメンバーのイベントまたはコメントに「不適切」のフラグを設定できます。デフォルトはチェック済み**.**

* **フラグ設定理由リスト**&#x200B;オンにすると、メンバーはイベントまたはコメントに「不適切」のフラグを設定した理由をドロップダウンリストから選択できます。初期設定はオフです。

* **カスタムフラグ設定理由**&#x200B;オンにすると、メンバーはイベントまたはコメントに「不適切」のフラグを設定した独自の理由を入力できます。初期設定はオフです**.**

* **モデレートのしきい値**&#x200B;メンバーがイベントまたはコメントに何回フラグを設定したらモデレーターに通知するかを指定します。初期設定は1（1回）です。

* **フラグ付けの制限**&#x200B;イベントまたはコメントに何回フラグが設定されたら、公開表示から非公開にするかを指定します。-1に設定した場合、フラグ付けされたトピックまたはコメントは公開ビューで非表示になりません。 そうでない場合、この数値はモデレートのしきい値以上にする必要があります。 初期設定は 5 です。

#### 「タグフィールド」タブ{#tag-field-tab}

Under the **Tag field** tab, the tags which may be applied, if allowed under the **Settings **tab, are limited according to namespaces chosen.

* ****Settings ****&#x200B;タブでチェ `Allow Tagging` ック済みの場合は、「Namespaces Relevant」を使用できます。 適用できるタグは、チェックされた名前空間カテゴリ内のタグに制限されます。 名前空間のリストには、「Standard Tags」（デフォルトの名前空間）と「Include All Tags」が含まれます。 初期設定はnoneで、すべての名前空間が許可されます。

* **推奨の制限**&#x200B;フォーラムに投稿するメンバーに表示する推奨タグの数を入力します。初期設定は**-**1（制限なし）です。

>[!NOTE]
>
>新しいタグ名前空間（分類）の追加方法については、「[タグの管理](/help/sites-administering/tags.md)」を参照してください。

#### 「翻訳」タブ {#translation-tab}

「**Translation **」タブで、コミュニティサイトの翻訳が有効な場合、特定の投稿ではなくスレッド全体（イベントおよびコメント）を翻訳するように翻訳を設定できます。

* **すべてを翻訳**&#x200B;オンにすると、イベントとコメントがユーザーの選択した言語に翻訳されます。初期設定はオンです。

## サイト訪問者のエクスペリエンス {#site-visitor-experience}

パブリッシュ環境では、カレンダー機能はデフォルトの日付範囲を持つ検索フィールドと、その範囲内に含まれるすべてのカレンダーイベントを表示します。

カレンダーイベントを選択すると、その詳細、説明およびコメントが表示されます。

その他の機能は、サイト訪問者がモデレーターか、管理者か、コミュニティメンバーか、権限を持つメンバーか、匿名かによって異なります。

### モデレーターおよび管理者 {#moderators-and-administrators}

サインインしているユーザーがモデレーター権限または管理者権限を持っている場合は、すべてのカレンダーイベントと、イベントに投稿されたコメントに対して、（コンポーネントの設定で許可されている）[モデレートタスク](/help/communities/moderate-ugc.md)を実行できます。

![chlimage_1-150](assets/chlimage_1-150.png)

#### メンバー {#members}

When the signed in user is a community member or [privileged member](/help/communities/users.md#privileged-members-group) (depending on configuration), they are able to select `New Event` to create and post a new calendar event.

具体的には、次のことが可能です。

* 新しいカレンダーイベントを作成する
* カレンダーイベントにコメントを投稿する
* 自分のカレンダーイベントまたはコメントを編集する
* 自分のカレンダーイベントまたはコメントを削除する
* 他のメンバーのカレンダーイベントまたはコメントにフラグを設定する

![chlimage_1-151](assets/chlimage_1-151.png) ![chlimage_1-152](assets/chlimage_1-152.png)

#### 匿名 {#anonymous}

サインインしていないサイト訪問者は、投稿されたカレンダーイベントを閲覧することしかできず（サポートされている場合は翻訳も可）、イベントまたはコメントを追加したり、他のユーザーのイベントまたはコメントにフラグを設定することはできません。

![chlimage_1-153](assets/chlimage_1-153.png)

## 追加情報 {#additional-information}

More information may be found on the [Calendar Essentials](/help/communities/calendar-basics-for-developers.md) page for developers.

カレンダーイベントとコメントのモデレートについては、「[ユーザー生成コンテンツのモデレート](/help/communities/moderate-ugc.md)」を参照してください。

For tagging calendar events and comments, see [Tagging User Generated Content](/help/communities/tag-ugc.md).

For translation of calendar events and comments, see [Translating User Generated Content](/help/communities/translate-ugc.md).
