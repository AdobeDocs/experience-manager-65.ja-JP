---
title: サイトテンプレート
description: サイトテンプレートコンソールへのアクセス方法
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 05a944a3-adb1-47b4-b4a5-15bac91c995e
source-git-commit: ab3d016c7c9c622be361596137b150d8719630bd
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 4%

---

# サイトテンプレート {#site-templates}

サイトテンプレートコンソールは、 [グループテンプレート](tools-groups.md) コミュニティグループに関心のある機能に焦点を当てたコンソール。

>[!NOTE]
>
>作成用のコンソール [コミュニティサイト](sites-console.md), [コミュニティサイトテンプレート](sites.md), [コミュニティグループテンプレート](tools-groups.md)、および [コミュニティ機能](functions.md) は、オーサー環境でのみ使用されます。

## サイトテンプレートコンソール {#site-templates-console}

オーサー環境でコミュニティサイトコンソールにアクセスするには、次の手順を実行します。

* グローバルナビゲーションから： **[!UICONTROL ツール/コミュニティ/サイトテンプレート]**

このコンソールには、 [コミュニティサイト](sites-console.md) を作成して、新しいサイトテンプレートを作成できます。

![site-template](assets/site-template.png)

## サイトテンプレートを作成 {#create-site-template}

サイトテンプレートの作成を開始するには、「 `Create`.

3 つのサブパネルを含むサイトエディターパネルが開きます。

### 基本情報 {#basic-info}

![site-template-basicinfo](assets/site-template-basicinfo.png)

基本情報パネルで、名前と説明、およびテンプレートの有効/無効を設定します。

* **[!UICONTROL コミュニティサイトテンプレート名]**

  テンプレート名 ID。

* **[!UICONTROL コミュニティサイトテンプレートの説明]**

  テンプレートの説明。

* **[!UICONTROL 無効/有効]**

  テンプレートを参照可能にするかどうかを制御する切り替えスイッチ。

### サムネール {#thumbnail}

![site-thumbnail](assets/site-thumbnail.png)

（オプション）「画像をアップロード」アイコンを選択して、コミュニティサイトの作成者に対して、名前と説明に加えてサムネールを表示します。

### 構造 {#structure}

![サイト構造](assets/site-structure.png)

コミュニティ機能を追加するには、サイトメニューのリンクが表示される順に、右側から左にドラッグします。 スタイルは、サイトの作成時にテンプレートに適用されます。

例えば、ホームページが必要な場合は、ライブラリからページ機能をドラッグし、テンプレートビルダーの下にドロップします。 これにより、ページ設定ダイアログが開きます。 詳しくは、 [関数コンソール](functions.md) を参照してください。

このテンプレートに基づいて、コミュニティサイトに必要な他のコミュニティ機能を引き続きドラッグ&amp;ドロップします。

ページ関数は、空のページを提供します。 グループ機能を使用すると、コミュニティサイト内にグループサイト（サブコミュニティ）を作成できます。

>[!CAUTION]
>
>Groups 関数を使用する必要があります。 *最初でもなく、唯一でもない* 関数を使用して、サイト構造内で使用できます。
>
>その他の関数 ( [ページ関数](functions.md#page-function)、を含め、最初にリストする必要があります。

![site-editor](assets/site-editor.png)

### グループ機能のグループテンプレート {#group-templates-for-groups-function}

サイトテンプレートにグループ機能を含める場合、設定では、パブリッシュ環境で新しいグループを作成する際に使用できるグループテンプレートの選択肢を指定する必要があります。

>[!CAUTION]
>
>Groups 関数を使用する必要があります。 *最初でもなく、唯一でもない* 関数を使用して、サイト構造内で使用できます。

![site-functions](assets/site-functions.png)

2 つ以上のコミュニティグループテンプレートを選択すると、コミュニティでグループを実際に作成する際に、グループ管理者に選択肢が提供されます。

![site-function](assets/site-functions1.png)

## サイトテンプレートを編集 {#edit-site-template}

メインでサイトテンプレートを表示する場合 [サイトテンプレートコンソール](#site-templates-console)の場合は、編集用に既存のサイトテンプレートを選択できます。

このプロセスは、 [サイトテンプレートの作成](#create-site-template).
