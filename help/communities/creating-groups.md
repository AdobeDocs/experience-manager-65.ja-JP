---
title: コミュニティグループ
description: コミュニティグループの作成
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: edcda6cb-df47-4afe-8a9a-82d8e386fe05
source-git-commit: e33816b3b8d190e185d2b23dad3a05aca272f01c
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 3%

---

# コミュニティグループ {#community-groups}

コミュニティグループ機能を使用すると、パブリッシュ環境とオーサー環境から、許可されたユーザー（コミュニティメンバーと作成者）がコミュニティサイト内でサブコミュニティを動的に作成できます。

この機能は、 [グループ機能](/help/communities/functions.md#groups-function) が [コミュニティサイト](/help/communities/sites-console.md) 構造。

A [コミュニティグループテンプレート](/help/communities/tools-groups.md) コミュニティグループを動的に作成する際のコミュニティグループページのデザインを提供します。

機能がコミュニティサイトの構造またはコミュニティサイトテンプレートに追加されると、グループ機能に対して 1 つ以上のグループテンプレートが選択されます。 このグループテンプレートのリストは、コミュニティサイト内から動的にグループを作成するメンバーまたは作成者に表示されます。

## 新しいグループの作成 {#creating-a-new-group}

コミュニティグループを作成する機能は、グループ機能を含むコミュニティサイト ( [参照サイトテンプレート](/help/communities/sites.md).

以下の例では、 `Reference Site Template` 例えば、 [AEM Communitiesの概要](/help/communities/getting-started.md) チュートリアル

これは、 **グループ** メニュー項目が選択されている：

![new-group](assets/new-group.png)

次の項目を選択した場合： **新しいグループ** アイコンをクリックすると、編集ダイアログが開きます。

の下 **設定** 「 」タブでは、グループの基本機能を使用できます。

![group-settings](assets/group-settings.png)

* **グループ名**

  コミュニティサイトに表示するグループのタイトル。 グループ名にはアンダースコア文字 (_) や、リソースや設定などのキーワードを使用しないでください。

* **説明**

  コミュニティサイトに表示するグループの説明。

* **招待**

  グループに招待するメンバーのリストです。 先行入力検索では、招待するコミュニティメンバーの提案を提供します。

* **グループ URL 名**

  URL の一部になるグループページの名前。

* **オープングループ**

  選択 `Open Group` 匿名のサイト訪問者がコンテンツを閲覧し、選択を解除できることを示します `Member Only Group`.

* **メンバーのみのグループ**

  選択 `Member Only Group` グループのメンバーのみがコンテンツを表示し、選択を解除できることを示します `Open Group`.

の下 **テンプレート** 「 」タブで、コミュニティグループテンプレートのリストから選択できます。 これらのテンプレートは、グループ機能がコミュニティサイトの構造またはコミュニティサイトテンプレートに含まれたときに指定されました。

![group-template](assets/group-template.png)

の下 **画像** 「 」タブでは、コミュニティサイトのグループページにグループ用に表示する画像をアップロードできます。 デフォルトのスタイルシートでは、画像のサイズが 170 x 90 ピクセルに設定されます。

![group-image](assets/group-image.png)

次を選択して **グループを作成**&#x200B;をクリックした場合、グループのページは選択したテンプレートに基づいて作成され、ユーザーグループがメンバーシップ用に作成され、グループページが更新されて新しいサブコミュニティが表示されます。

例えば、画像のサムネールがアップロードされた新しいサブコミュニティ「Focus Group」が付いたグループページは、次のように表示されます（コミュニティグループ管理者としてサインインしたまま）。

![group-page](assets/group-page.png)

の選択 `Focus Group` リンクは、ブラウザーでフォーカスグループページを開きます。このページは、選択したテンプレートに基づいて初期の外観を持ち、メインのコミュニティサイトのメニューの下にサブメニューが含まれています。

![open-group-page](assets/open-group-page.png)

### コミュニティグループメンバーリストコンポーネント {#community-group-member-list-component}

The `Community Group Member List` コンポーネントは、グループテンプレートの開発者が使用することを目的としています。

### 追加情報 {#additional-information}

詳しくは、 [コミュニティグループの基本事項](/help/communities/essentials-groups.md) 開発者向けのページ

コミュニティグループに関するその他の情報については、 [ユーザーとユーザーグループの管理](/help/communities/users.md).
