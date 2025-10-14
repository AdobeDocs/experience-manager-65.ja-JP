---
title: コミュニティグループ
description: コミュニティグループ機能を使用して、Publishおよびオーサーの承認済みユーザーによって、コミュニティサイト内にサブコミュニティを動的に作成する方法を説明します。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: edcda6cb-df47-4afe-8a9a-82d8e386fe05
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 1%

---

# コミュニティグループ {#community-groups}

コミュニティグループ機能は、権限のあるユーザー（コミュニティメンバーと作成者）がパブリッシュ環境とオーサー環境から、コミュニティサイト内にサブコミュニティを動的に作成する機能です。

この機能は、[groups 関数 &#x200B;](/help/communities/functions.md#groups-function) が [community site](/help/communities/sites-console.md) 構造に存在する場合に存在します。

[&#x200B; コミュニティグループテンプレート &#x200B;](/help/communities/tools-groups.md) は、コミュニティグループが動的に作成される際に、コミュニティグループページのデザインを提供します。

グループ機能がコミュニティサイトの構造またはコミュニティサイトテンプレートに追加されると、グループ機能に 1 つ以上のグループテンプレートが選択されます。 このグループテンプレートのリストは、コミュニティサイト内からグループを動的に作成するメンバーまたは作成者に表示されます。

## 新しいグループの作成 {#creating-a-new-group}

コミュニティグループを作成できるかどうかは、[&#x200B; 参照サイトテンプレート &#x200B;](/help/communities/sites.md) から作成されたような、groups 機能を含むコミュニティサイトが存在しているかどうかによって異なります。

以下の例では、「AEM Communities使用の手引き [&#x200B; チュートリアルの説明に従って、`Reference Site Template` から作成したコミュニティサイトを使用し &#x200B;](/help/communities/getting-started.md) す。

これは、「**グループ**」メニュー項目が選択されている場合に公開時に読み込まれるページです。

![new-group](assets/new-group.png)

「**新規グループ**」アイコンを選択すると、編集ダイアログボックスが開きます。

「**設定**」タブで、グループの基本機能を指定します。

![group-settings](assets/group-settings.png)

* **グループ名**

  コミュニティサイトに表示するグループのタイトル。 グループ名には、アンダースコア文字（_）やキーワード（resources、configuration など）は使用しないでください。

* **説明**

  コミュニティサイトに表示するグループの説明。

* **招待**

  グループに招待するメンバーのリスト。 先行入力検索では、招待するコミュニティメンバーの候補が表示されます。

* **グループ URL 名**

  URL の一部になるグループページの名前。

* **グループを開く**

  「`Open Group`」を選択すると、匿名サイト訪問者はそのコンテンツを表示でき、`Member Only Group` の選択を解除できます。

* **メンバー専用グループ**

  「`Member Only Group`」を選択すると、グループのメンバーのみがコンテンツを表示でき、選択を解除 `Open Group` きます。

「**テンプレート**」タブで、コミュニティグループテンプレートのリストから選択できます。 これらのテンプレートは、グループ機能がコミュニティサイトの構造またはコミュニティサイトテンプレートに含まれた場合に指定されました。

![group-template](assets/group-template.png)

「**画像**」タブでは、コミュニティサイトのグループ ページに、グループに表示する画像をアップロードできます。 デフォルトのスタイルシートでは、画像のサイズが 170 x 90 ピクセルに設定されます。

![group-image](assets/group-image.png)

**グループを作成** を選択すると、選択したテンプレートに基づいてグループのページが作成され、メンバーシップ用のユーザーグループが作成され、グループ ページが更新されて新しいサブコミュニティが表示されます。

例えば、画像のサムネールをアップロードした「フォーカスグループ」という新しいサブコミュニティを持つグループページは、次のように表示されます（コミュニティグループの管理者としてログインしたままです）。

![group-page](assets/group-page.png)

`Focus Group` のリンクを選択すると、ブラウザーにフォーカスグループページが開きます。このページは、選択したテンプレートに基づいた初期の表示であり、メインコミュニティサイトのメニューの下にサブメニューが含まれています。

![open-group-page](assets/open-group-page.png)

### コミュニティグループメンバーリストコンポーネント {#community-group-member-list-component}

`Community Group Member List` コンポーネントは、グループテンプレートの開発者が使用することを目的としています。

### 追加情報 {#additional-information}

詳しくは、開発者向けの [&#x200B; コミュニティグループの初期設定 &#x200B;](/help/communities/essentials-groups.md) ページを参照してください。

コミュニティグループに関するその他の情報については、[&#x200B; ユーザーとユーザーグループの管理 &#x200B;](/help/communities/users.md) を参照してください。
