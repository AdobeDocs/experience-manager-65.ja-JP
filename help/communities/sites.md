---
title: サイトテンプレート
seo-title: Site Templates
description: サイトテンプレートコンソールにアクセスする方法
seo-description: How to access the Site Templates console
uuid: d2f7556e-7e43-424e-82f1-41790aeb2d98
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 202d7dba-2b34-431d-b10f-87775632807f
role: Admin
exl-id: 05a944a3-adb1-47b4-b4a5-15bac91c995e
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 62%

---

# サイトテンプレート {#site-templates}

サイトテンプレートコンソールは、 [グループテンプレート](tools-groups.md) コミュニティグループに関心のある機能に焦点を当てたコンソール。

>[!NOTE]
>
>作成用のコンソール [コミュニティサイト](sites-console.md), [コミュニティサイトテンプレート](sites.md), [コミュニティグループテンプレート](tools-groups.md) および [コミュニティ機能](functions.md) は、オーサー環境でのみ使用されます。

## サイトテンプレートコンソール {#site-templates-console}

オーサー環境でコミュニティサイトコンソールに移動するには、：

* グローバルナビゲーションから： **[!UICONTROL ツール/コミュニティ/サイトテンプレート]**

このコンソールでは、[コミュニティサイト](sites-console.md)を作成できるテンプレートが表示されます。また、新しいサイトテンプレートを作成できます。

![site-template](assets/site-template.png)

## サイトテンプレートを作成 {#create-site-template}

新しいサイトテンプレートの作成を開始するには、「 `Create`.

するとサイトエディターパネルに移動します。パネルには以下の 3 つのサブパネルがあります。

### 基本情報 {#basic-info}

![site-template-basicinfo](assets/site-template-basicinfo.png)

基本情報パネルでは、名前、説明およびテンプレートを有効にするか無効にするかを設定します。

* **[!UICONTROL コミュニティサイトテンプレート名]**

   テンプレート名 ID。

* **[!UICONTROL コミュニティサイトテンプレートの説明]**

   テンプレートの説明。

* **[!UICONTROL 無効/有効]**

   テンプレートを参照可能にするかどうかを制御する切り替えスイッチ。

### サムネール {#thumbnail}

![site-thumbnail](assets/site-thumbnail.png)

（オプション）コミュニティサイトの作成者に対し、名前と説明に加えてサムネイルを表示するには、画像をアップロードアイコンを選択します。

### 構造 {#structure}

![サイト構造](assets/site-structure.png)

コミュニティ機能を追加するには、右側から左側にドラッグします。サイトメニューのリンクは追加した順番で表示されます。スタイルは、サイトの作成時にテンプレートに適用されます。

例えば、ホームページが必要な場合は、ページ機能をライブラリからテンプレートビルダーにドラッグ＆ドロップします。これにより、ページ設定ダイアログが開きます。 詳しくは、 [関数コンソール](functions.md) を参照してください。

このテンプレートをベースとするコミュニティサイトに必要な、他のコミュニティ機能を続けてドラッグ＆ドロップします。

ページ機能では空のページが作成されます。グループ機能を使用すると、コミュニティサイト内にグループサイト（サブコミュニティ）を作成できます。

>[!CAUTION]
>
>グループ機能は、 *not* は *最初でも唯一でも* 関数を使用して、サイト構造内で使用できます。
>
>他の機能（[ページ機能](functions.md#page-function)など）を含め、その機能を 1 番目にリストする必要があります。

![site-editor](assets/site-editor.png)

### グループ機能のためのグループテンプレート {#group-templates-for-groups-function}

サイトテンプレートにグループ機能を含める場合、パブリッシュ環境で新しいグループを作成するときに、グループテンプレート選択の仕様が設定により許可されている必要があります。

>[!CAUTION]
>
>Groups 関数を使用する必要があります。 *not* は *最初でも唯一でも* 関数を使用して、サイト構造内で使用できます。

![site-functions](assets/site-functions.png)

2 つ以上のグループテンプレートを選択することにより、グループ管理者が実際にコミュニティで新しいグループを作成するときに、テンプレートを選択できるようになります。

![site-function](assets/site-functions1.png)

## サイトテンプレートを編集 {#edit-site-template}

メインの[サイトテンプレートコンソール](#site-templates-console)でサイトテンプレートを表示しているときに、既存のサイトテンプレートを選択して編集できます。

このプロセスでは、[サイトテンプレートの作成](#create-site-template)と同じパネルを使用します。
