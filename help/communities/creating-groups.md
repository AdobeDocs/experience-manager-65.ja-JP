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
exl-id: edcda6cb-df47-4afe-8a9a-82d8e386fe05
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 37%

---

# コミュニティグループ {#community-groups}

コミュニティグループ機能は、パブリッシュ環境とオーサー環境から許可されたユーザー（コミュニティメンバーと作成者）がコミュニティサイト内でサブコミュニティを動的に作成する機能です。

この機能は、[グループ関数](/help/communities/functions.md#groups-function)が[コミュニティサイト](/help/communities/sites-console.md)構造に存在する場合に使用できます。

[コミュニティグループテンプレート](/help/communities/tools-groups.md)は、コミュニティグループが動的に作成される際のコミュニティグループページのデザインを提供します。

グループ機能をコミュニティサイトの構造またはコミュニティサイトテンプレートに追加すると、1 つ以上のテンプレートがグループ機能用に選択されます。このグループテンプレートのリストは、コミュニティサイト内から新しいグループを動的に作成するメンバーまたは作成者に表示されます。

## 新しいグループの作成 {#creating-a-new-group}

新しいコミュニティグループを作成する機能は、[参照サイトテンプレート](/help/communities/sites.md)から作成したコミュニティサイトなど、グループ機能を含むコミュニティサイトが存在することに依存します。

以降の例では、 [AEM Communities](/help/communities/getting-started.md)使用の手引きのチュートリアルで説明したように、 `Reference Site Template`から作成したコミュニティサイトを使用します。

これは、**Groups**&#x200B;メニュー項目が選択された場合にパブリッシュ時に読み込まれるページです。

![new-group](assets/new-group.png)

「**新しいグループ**」アイコンを選択すると、編集ダイアログが開きます。

「**設定**」タブでは、グループの基本機能を指定します。

![group-settings](assets/group-settings.png)

* **Group Name**

   コミュニティサイトに表示するグループのタイトル。

* **説明**

   コミュニティサイトに表示するグループの説明。

* **招待**

   グループに参加するよう招待するメンバーのリスト。 先行入力検索によって、招待する推奨コミュニティメンバーが表示されます。

* **グループ URL 名**

   URLの一部となるグループページの名前。

* **オープングループ**

   「`Open Group`」を選択すると、匿名のサイト訪問者がコンテンツを閲覧できることを示し、「`Member Only Group`」の選択を解除します。

* **メンバーのみのグループ**

   `Member Only Group`を選択すると、グループのメンバーのみがコンテンツを表示でき、`Open Group`の選択が解除されます。

「**テンプレート**」タブでは、次の操作が可能です。
コミュニティサイトの構造またはコミュニティサイトテンプレートにグループ機能を含めたときに指定したコミュニティグループテンプレートのリストから選択します。

![group-template](assets/group-template.png)

「**画像**」タブでは、コミュニティサイトのグループページにグループ用に表示する画像をアップロードできます。デフォルトのスタイルシートでは、画像のサイズが170 x 90ピクセルに設定されます。

![group-image](assets/group-image.png)

「**グループを作成**」ボタンを選択すると、選択したテンプレートをベースとしてグループのページが作成され、ユーザーグループがメンバーシップ用に作成され、新しいサブコミュニティを表示するようにグループページが更新されます。

例えば、画像サムネイルがアップロードされた「Focus Group」というタイトルの新しいサブコミュニティを含むグループページは、次のように表示されます（引き続きコミュニティグループ管理者としてサインインしています）。

![group-page](assets/group-page.png)

`Focus Group`リンクを選択すると、ブラウザーでフォーカスグループページが開きます。このページは、選択したテンプレートに基づいて初期表示され、メインコミュニティサイトのメニューの下にサブメニューが表示されます。

![open-group-page](assets/open-group-page.png)

### コミュニティグループメンバーのリストコンポーネント {#community-group-member-list-component}

`Community Group Member List`コンポーネントは、グループテンプレートの開発者が使用することを目的としています。

### 追加情報 {#additional-information}

詳しくは、開発者向けの[コミュニティグループの基本事項](/help/communities/essentials-groups.md)ページを参照してください。

コミュニティグループに関連するその他の情報は、[ユーザーとユーザーグループの管理](/help/communities/users.md)を参照してください。
