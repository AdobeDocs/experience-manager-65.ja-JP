---
title: コミュニティグループ
description: コミュニティグループ機能を使用して、パブリッシュとオーサーで権限のあるユーザーが、コミュニティサイト内にサブコミュニティを動的に作成する方法を説明します。
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

この機能は、 [groups 関数](/help/communities/functions.md#groups-function) がに存在する [コミュニティサイト](/help/communities/sites-console.md) 構造。

A [コミュニティグループテンプレート](/help/communities/tools-groups.md) コミュニティグループが動的に作成される際に、コミュニティグループページのデザインを提供します。

グループ機能がコミュニティサイトの構造またはコミュニティサイトテンプレートに追加されると、グループ機能に 1 つ以上のグループテンプレートが選択されます。 このグループテンプレートのリストは、コミュニティサイト内からグループを動的に作成するメンバーまたは作成者に表示されます。

## 新しいグループの作成 {#creating-a-new-group}

コミュニティグループを作成できるかどうかは、 [参照サイトテンプレート](/help/communities/sites.md).

以下の例では、から作成したコミュニティサイトを使用しています `Reference Site Template` で説明されているように [AEM Communitiesの概要](/help/communities/getting-started.md) チュートリアル。

これは、次の場合にパブリッシュ環境で読み込まれるページです **グループ** メニュー項目が選択されました：

![new-group](assets/new-group.png)

選択した場合 **新規グループ** アイコンをクリックすると、編集ダイアログボックスが開きます。

の下 **設定** タブで、グループの基本機能を指定します。

![group-settings](assets/group-settings.png)

* **グループ名**

  コミュニティサイトに表示するグループのタイトル。 グループ名には、アンダースコア文字（_）やキーワード（resources、configuration など）は使用しないでください。

* **説明**

  コミュニティサイトに表示するグループの説明。

* **招待**

  グループに招待するメンバーのリスト。 先行入力検索では、招待するコミュニティメンバーの候補が表示されます。

* **グループ URL 名**

  URL の一部になるグループページの名前。

* **Open Group**

  選択 `Open Group` は、すべての匿名サイト訪問者がコンテンツを表示でき、選択を解除できることを示します `Member Only Group`.

* **メンバーのみのグループ**

  選択 `Member Only Group` グループのメンバーのみがコンテンツを表示でき、選択を解除できることを示します `Open Group`.

の下 **Template** タブをクリックして、コミュニティグループテンプレートのリストから選択できます。 これらのテンプレートは、グループ機能がコミュニティサイトの構造またはコミュニティサイトテンプレートに含まれた場合に指定されました。

![group-template](assets/group-template.png)

の下 **画像** 「」タブを使用して、コミュニティサイトのグループ ページにグループ用に表示する画像をアップロードできます。 デフォルトのスタイルシートでは、画像のサイズが 170 x 90 ピクセルに設定されます。

![group-image](assets/group-image.png)

を選択する **グループを作成**&#x200B;を選択すると、選択したテンプレートに基づいてグループのページが作成され、メンバーシップ用のユーザーグループが作成され、グループ ページが更新されて新しいサブコミュニティが表示されます。

例えば、画像のサムネールをアップロードした「フォーカスグループ」という新しいサブコミュニティを持つグループページは、次のように表示されます（コミュニティグループの管理者としてログインしたままです）。

![group-page](assets/group-page.png)

の選択 `Focus Group` リンクをクリックすると、ブラウザーにフォーカスグループページが開きます。このページは、選択したテンプレートに基づいた初期の表示であり、メインコミュニティサイトのメニューの下にサブメニューが含まれています。

![open-group-page](assets/open-group-page.png)

### コミュニティグループメンバーリストコンポーネント {#community-group-member-list-component}

この `Community Group Member List` コンポーネントは、グループテンプレートの開発者が使用することを目的としています。

### 追加情報 {#additional-information}

詳しくは、 [コミュニティグループの基本事項](/help/communities/essentials-groups.md) 開発者向けのページです。

コミュニティグループに関するその他の情報については、 [ユーザーとユーザーグループの管理](/help/communities/users.md).
