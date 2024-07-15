---
title: サイトテンプレート
description: サイトテンプレート コンソールにアクセスしてコミュニティサイトを作成する方法を説明します。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 05a944a3-adb1-47b4-b4a5-15bac91c995e
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 3%

---

# サイトテンプレート {#site-templates}

サイトテンプレート コンソールは、コミュニティグループが関心を持つ機能に焦点を当てた [ グループテンプレート ](tools-groups.md) コンソールに似ています。

>[!NOTE]
>
>[ コミュニティサイト ](sites-console.md)、[ コミュニティサイトテンプレート ](sites.md)、[ コミュニティグループテンプレート ](tools-groups.md)、および [ コミュニティ機能 ](functions.md) の作成用のコンソールは、オーサー環境でのみ使用されます。

## サイトテンプレートコンソール {#site-templates-console}

オーサー環境でコミュニティサイトコンソールにアクセスするには、次の手順を実行します。

* グローバルナビゲーションから：**[!UICONTROL ツール/コミュニティ/サイトテンプレート]**

このコンソールには、[ コミュニティサイト ](sites-console.md) を作成できるテンプレートが表示され、新しいサイトテンプレートを作成できます。

![site-template](assets/site-template.png)

## サイトテンプレートを作成 {#create-site-template}

サイトテンプレートの作成を開始するには、「`Create`」を選択します。

これにより、3 つのサブパネルを含むサイトエディターパネルが開きます。

### 基本情報 {#basic-info}

![site-template-basicinfo](assets/site-template-basicinfo.png)

基本情報パネルで、名前、説明、テンプレートが有効か無効かが設定されます。

* **[!UICONTROL コミュニティサイトテンプレート名]**

  テンプレート名 ID。

* **[!UICONTROL コミュニティサイトテンプレートの説明]**

  テンプレートの説明。

* **[!UICONTROL 無効/有効]**

  テンプレートを参照可能にするかどうかを制御する切り替えスイッチ。

### サムネール {#thumbnail}

![site-thumbnail](assets/site-thumbnail.png)

（オプション）「画像をアップロード」アイコンを選択して、コミュニティサイトの作成者に名前と説明と共にサムネールを表示します。

### 構造 {#structure}

![site-structure](assets/site-structure.png)

コミュニティ機能を追加するには、サイト メニューのリンクが表示される順序で右から左にドラッグします。 スタイルは、サイトの作成中にテンプレートに適用されます。

例えば、ホームページが必要な場合は、Page 関数をライブラリからドラッグして、テンプレートビルダーの下にドロップします。 その結果、ページ設定ダイアログが開きます。 設定ダイアログについて詳しくは、[ 関数コンソール ](functions.md) を参照してください。

このテンプレートに基づいて、引き続き、コミュニティサイトに必要な他のコミュニティ機能をドラッグ&amp;ドロップします。

page 関数は空のページを提供します。 グループ機能を使用すると、コミュニティサイト内にグループサイト（サブコミュニティ）を作成できます。

>[!CAUTION]
>
>Groups 関数は、サイト構造内の最初の関数でも唯一の関数でもな *必要があり* す。
>
>[page 関数 ](functions.md#page-function) など、その他の関数を最初に含めてリストする必要があります。

![site-editor](assets/site-editor.png)

### Groups 関数用のグループ テンプレート {#group-templates-for-groups-function}

サイトテンプレートにグループ機能を含める場合、設定では、パブリッシュ環境で新しいグループを作成する際に、許可されるグループテンプレートの選択肢を指定する必要があります。

>[!CAUTION]
>
>Groups 関数は、サイト構造内の最初の関数でも唯一の関数でもな *必要があり* す。

![site-functions](assets/site-functions.png)

2 つ以上のコミュニティグループテンプレートを選択することで、コミュニティ内で実際にグループを作成する際に、グループ管理者に選択肢が提供されます。

![site-function](assets/site-functions1.png)

## サイトテンプレートを編集 {#edit-site-template}

メインの [ サイトテンプレート コンソール ](#site-templates-console) でサイトテンプレートを表示すると、既存のサイトテンプレートを選択して編集することができます。

このプロセスでは、[ サイトテンプレートの作成 ](#create-site-template) と同じパネルを使用できます。
