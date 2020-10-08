---
title: サイトテンプレート
seo-title: サイトテンプレート
description: サイトテンプレートコンソールにアクセスする方法
seo-description: サイトテンプレートコンソールにアクセスする方法
uuid: d2f7556e-7e43-424e-82f1-41790aeb2d98
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 202d7dba-2b34-431d-b10f-87775632807f
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 61%

---


# サイトテンプレート {#site-templates}

The Site Templates console is very similar to the [Group Templates](tools-groups.md) console, which is focused on functions of interest to Community groups.

>[!NOTE]
>
>The consoles for the creation of [community sites](sites-console.md), [community site templates](sites.md), [community group templates](tools-groups.md) and [community functions](functions.md) are for use only in the author environment.

## Site Templates Console {#site-templates-console}

作成者環境でコミュニティサイトコンソールにアクセスするには：

* From global navigation: **[!UICONTROL Tools > Communities > Site Templates]**

このコンソールでは、[コミュニティサイト](sites-console.md)を作成できるテンプレートが表示されます。また、新しいサイトテンプレートを作成できます。

![site-template](assets/site-template.png)

## Create Site Template {#create-site-template}

To get started creating a new site template, select `Create`.

するとサイトエディターパネルに移動します。パネルには以下の 3 つのサブパネルがあります。

### Basic info {#basic-info}

![site-template-basicinfo](assets/site-template-basicinfo.png)

基本情報パネルでは、名前、説明およびテンプレートを有効にするか無効にするかを設定します。

* **[!UICONTROL コミュニティサイトテンプレート名]**

   テンプレート名ID。

* **[!UICONTROL コミュニティサイトテンプレートの説明]**

   テンプレートの説明。

* **[!UICONTROL 無効/有効]**

   テンプレートが参照可能かどうかを制御するトグルスイッチ。

### サムネール {#thumbnail}

![site-thumbnail](assets/site-thumbnail.png)

（オプション）コミュニティサイトの作成者に対し、名前と説明に加えてサムネイルを表示するには、画像をアップロードアイコンを選択します。

### 構造 {#structure}

![部位構造](assets/site-structure.png)

コミュニティ機能を追加するには、右側から左側にドラッグします。サイトメニューのリンクは追加した順番で表示されます。スタイルは、サイトの作成時にテンプレートに適用されます。

例えば、ホームページが必要な場合は、ページ機能をライブラリからテンプレートビルダーにドラッグ＆ドロップします。これにより、ページ設定ダイアログが開きます。 See the [functions console](functions.md) for information about the configuration dialogs.

このテンプレートをベースとするコミュニティサイトに必要な、他のコミュニティ機能を続けてドラッグ＆ドロップします。

ページ機能では空のページが作成されます。グループ機能は、コミュニティサイト内にグループサイト（サブコミュニティ）を作成する機能を提供します。

>[!CAUTION]
>
>The groups function must *not* be the *first nor the only* function in the site structure.
>
>他の機能（[ページ機能](functions.md#page-function)など）を含め、その機能を 1 番目にリストする必要があります。

![サイト編集者](assets/site-editor.png)

### グループ機能のためのグループテンプレート {#group-templates-for-groups-function}

サイトテンプレートにグループ機能を含める場合、パブリッシュ環境で新しいグループを作成するときに、グループテンプレート選択の仕様が設定により許可されている必要があります。

>[!CAUTION]
>
>The Groups function must *not* be the *first nor the only* function in the site structure.

![サイト関数](assets/site-functions.png)

2 つ以上のグループテンプレートを選択することにより、グループ管理者が実際にコミュニティで新しいグループを作成するときに、テンプレートを選択できるようになります。

![部位機能](assets/site-functions1.png)

## サイトテンプレートを編集 {#edit-site-template}

メインの[サイトテンプレートコンソール](#site-templates-console)でサイトテンプレートを表示しているときに、既存のサイトテンプレートを選択して編集できます。

このプロセスでは、[サイトテンプレートの作成](#create-site-template)と同じパネルを使用します。
