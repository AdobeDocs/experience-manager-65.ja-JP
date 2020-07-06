---
title: コミュニティグループ
seo-title: コミュニティグループ
description: コミュニティグループの作成
seo-description: コミュニティグループの作成
uuid: c677d23d-5edb-414c-9013-130c88c2ea52
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: d94708ee-ca6b-420c-9536-6889d752f9de
docset: aem65
translation-type: tm+mt
source-git-commit: 43663703a79b95ccdb83eb9b5730143bde101305
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 38%

---


# コミュニティグループ {#community-groups}

コミュニティグループ機能は、サブコミュニティを発行ユーザーと発言者環境から許可されたユーザー（コミュニティのメンバーと発言者）がコミュニティサイト内で動的に作成する機能です。

This ability is present when the [groups function](/help/communities/functions.md#groups-function) is present in the [community site](/help/communities/sites-console.md) structure.

A [community group template](/help/communities/tools-groups.md) provides the design of the community group page when a community group is dynamically created.

グループ機能をコミュニティサイトの構造またはコミュニティサイトテンプレートに追加すると、1 つ以上のテンプレートがグループ機能用に選択されます。このリストのグループテンプレートは、コミュニティサイト内から動的に新しいグループを作成するメンバーまたは作成者に表示されます。

## 新しいグループの作成 {#creating-a-new-group}

The ability to create a new community group relies on the existence of a community site which includes the groups function, such as one created from the [Reference Site Template](/help/communities/sites.md).

The examples that follow use the community site created from the `Reference Site Template` as described in the [Getting Started with AEM Communities](/help/communities/getting-started.md) tutorial.

This is the page that loads on publish when the **Groups** menu item is selected:

![chlimage_1-236](assets/chlimage_1-236.png)

「**新しいグループ**」アイコンを選択すると、編集ダイアログが開きます。

「**設定**」タブでは、グループの基本機能を指定します。

![chlimage_1-237](assets/chlimage_1-237.png)

* **Group Name**

   コミュニティサイトに表示するグループのタイトル。

* **説明**

   コミュニティサイトに表示するグループの説明です。

* **招待**

   グループへの参加を招待するリスト。 先行入力検索によって、招待する推奨コミュニティメンバーが表示されます。

* **グループ URL 名**

   URLに含まれるグループページの名前。

* **オープングループ**

   を選択 `Open Group` すると、匿名サイト訪問者がコンテンツに表示する可能性があることを示し、選択が解除され `Member Only Group`ます。

* **メンバーのみのグループ**

   を選択す `Member Only Group` ると、グループのメンバーだけがコンテンツを表示できることを示し、選択が解除され `Open Group`ます。

Under the **Template** tab is the ability to
select from the list of community group templates that were specified when the groups function was included in the community site&#39;s structure or in a community site template.

![chlimage_1-238](assets/chlimage_1-238.png)

「**画像**」タブでは、コミュニティサイトのグループページにグループ用に表示する画像をアップロードできます。初期設定のスタイルシートでは、画像のサイズが170 x 90ピクセルに設定されます。

![chlimage_1-239](assets/chlimage_1-239.png)

「**グループを作成**」ボタンを選択すると、選択したテンプレートをベースとしてグループのページが作成され、ユーザーグループがメンバーシップ用に作成され、新しいサブコミュニティを表示するようにグループページが更新されます。

例えば、画像サムネイルがアップロードされた「Focus Group」というタイトルの新しいサブコミュニティを含むグループページは、次のように表示されます（引き続きコミュニティグループ管理者としてサインインしています）。

![chlimage_1-240](assets/chlimage_1-240.png)

Selecting the `Focus Group` link will open the Focus Group page in the browser, which has an initial appearance based on the chosen template, and includes a submenu underneath the main community site&#39;s menu:

![chlimage_1-241](assets/chlimage_1-241.png)

### コミュニティグループメンバーのリストコンポーネント {#community-group-member-list-component}

この `Community Group Member List` コンポーネントは、グループテンプレートの開発者が使用することを目的としています。

### 追加情報 {#additional-information}

More information may be found on the [Community Group Essentials](/help/communities/essentials-groups.md) page for developers.

コミュニティグループに関連するその他の情報は、[ユーザーとユーザーグループの管理](/help/communities/users.md)を参照してください。
