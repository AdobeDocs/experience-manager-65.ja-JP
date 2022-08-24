---
title: コミュニティグループ
seo-title: Community Groups
description: コミュニティグループの作成
seo-description: Creating community groups
uuid: c677d23d-5edb-414c-9013-130c88c2ea52
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: d94708ee-ca6b-420c-9536-6889d752f9de
docset: aem65
exl-id: edcda6cb-df47-4afe-8a9a-82d8e386fe05
source-git-commit: 1074843a0105df39382b64defe66fc262986b9c9
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 35%

---

# コミュニティグループ {#community-groups}

コミュニティグループ機能を使用すると、パブリッシュ環境とオーサー環境から、許可されたユーザー（コミュニティメンバーと作成者）がコミュニティサイト内でサブコミュニティを動的に作成できます。

この機能は、 [グループ機能](/help/communities/functions.md#groups-function) が [コミュニティサイト](/help/communities/sites-console.md) 構造。

A [コミュニティグループテンプレート](/help/communities/tools-groups.md) コミュニティグループを動的に作成する際のコミュニティグループページのデザインを提供します。

グループ機能をコミュニティサイトの構造またはコミュニティサイトテンプレートに追加すると、1 つ以上のテンプレートがグループ機能用に選択されます。このグループテンプレートのリストは、コミュニティサイト内から新しいグループを動的に作成するメンバーまたは作成者に表示されます。

## 新しいグループの作成 {#creating-a-new-group}

新しいコミュニティグループを作成する機能は、グループ機能を含むコミュニティサイト ( [参照サイトテンプレート](/help/communities/sites.md).

以下の例では、 `Reference Site Template` 例えば、 [AEM Communitiesの概要](/help/communities/getting-started.md) チュートリアル

これは、 **グループ** メニュー項目が選択されている：

![new-group](assets/new-group.png)

「**新しいグループ**」アイコンを選択すると、編集ダイアログが開きます。

「**設定**」タブでは、グループの基本機能を指定します。

![group-settings](assets/group-settings.png)

* **Group Name**

   コミュニティサイトに表示するグループのタイトル。 アンダースコア文字 (_) や、リソースや設定などのキーワードをグループ名に使用することは避けてください。

* **説明**

   コミュニティサイトに表示するグループの説明。

* **招待**

   グループに参加するよう招待するメンバーのリスト。 先行入力検索によって、招待する推奨コミュニティメンバーが表示されます。

* **グループ URL 名**

   URL の一部になるグループページの名前。

* **オープングループ**

   選択 `Open Group` 匿名のサイト訪問者がコンテンツを閲覧できることを示し、その選択を解除します `Member Only Group`.

* **メンバーのみのグループ**

   選択 `Member Only Group` グループのメンバーのみがコンテンツを表示でき、選択を解除できることを示します `Open Group`.

以下 **テンプレート** 「 」タブでは、コミュニティサイトの構造やコミュニティサイトテンプレートにグループ機能が含まれたときに指定されたコミュニティグループテンプレートのリストから選択できます。

![group-template](assets/group-template.png)

「**画像**」タブでは、コミュニティサイトのグループページにグループ用に表示する画像をアップロードできます。デフォルトのスタイルシートでは、画像のサイズが 170 x 90 ピクセルに設定されます。

![group-image](assets/group-image.png)

「**グループを作成**」ボタンを選択すると、選択したテンプレートをベースとしてグループのページが作成され、ユーザーグループがメンバーシップ用に作成され、新しいサブコミュニティを表示するようにグループページが更新されます。

例えば、画像サムネイルがアップロードされた「Focus Group」というタイトルの新しいサブコミュニティを含むグループページは、次のように表示されます（引き続きコミュニティグループ管理者としてサインインしています）。

![group-page](assets/group-page.png)

の選択 `Focus Group` リンクはブラウザでフォーカスグループページを開きます。このページは、選択したテンプレートに基づいて初期の外観を持ち、メインのコミュニティサイトのメニューの下にサブメニューが含まれています。

![open-group-page](assets/open-group-page.png)

### コミュニティグループメンバーのリストコンポーネント {#community-group-member-list-component}

この `Community Group Member List` コンポーネントは、グループテンプレートの開発者が使用することを目的としています。

### 追加情報 {#additional-information}

詳しくは、 [コミュニティグループの基本事項](/help/communities/essentials-groups.md) 開発者向けのページ

コミュニティグループに関連するその他の情報は、[ユーザーとユーザーグループの管理](/help/communities/users.md)を参照してください。
