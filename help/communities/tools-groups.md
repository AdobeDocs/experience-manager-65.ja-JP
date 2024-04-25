---
title: グループテンプレート
description: コミュニティサイトを形成する事前定義済みの一連のページや機能のグループテンプレートコンソールにアクセスする方法を説明します。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: aed2c3f2-1b5e-4065-8cec-433abb738ef5
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 2%

---

# グループテンプレート {#group-templates}

グループテンプレート コンソールは、次に類似しています [サイトテンプレート](/help/communities/sites.md) コンソール。 どちらも、コミュニティサイトを形成する、事前定義済みの一連のページおよび機能のブループリントです。 違いは、サイトテンプレートがメインコミュニティ用であり、グループテンプレートがコミュニティグループ（メインコミュニティ内にネストされたサブコミュニティ）用である点です。

コミュニティグループは、 [Groups 関数](/help/communities/functions.md#groups-function) （テンプレート内の最初の関数でも、唯一の関数でもない可能性があります）。

コミュニティの場合 [機能パック 1](/help/communities/deploy-communities.md#latestfeaturepack)グループテンプレート内に Groups 関数を含めることで、グループをネストできます。

コミュニティグループを作成するアクションが実行された瞬間に、グループのテンプレート（構造）が選択されます。 選択は、サイトまたはグループ テンプレートに追加したときに Groups 関数がどのように構成されたかによって異なります。

>[!NOTE]
>
>の作成のためのコンソール [コミュニティサイト](/help/communities/sites-console.md), [コミュニティサイトテンプレート](/help/communities/sites.md), [コミュニティグループテンプレート](/help/communities/tools-groups.md)、および [コミュニティ機能](/help/communities/functions.md) は、オーサー環境でのみ使用します。

## グループテンプレートコンソール {#group-templates-console}

AEM オーサー環境でグループテンプレートコンソールにアクセスするには：

* を選択 **ツール | コミュニティ | グループテンプレート、** グローバルナビゲーションから。

このコンソールには、が含まれているテンプレートが表示されます [コミュニティサイト](/help/communities/sites-console.md) を作成し、新しいグループテンプレートを作成できます。

![コミュニティグループテンプレート](assets/groups-template.png)

## グループテンプレートを作成 {#create-group-template}

グループテンプレートの作成を開始するには、以下を選択します `Create`.

これにより、3 つのサブパネルを含むサイトエディターパネルが表示されます。

### 基本情報 {#basic-info}

![site-basic-info](assets/site-basic-info.png)

基本情報パネルで、名前、説明、テンプレートが有効か無効かが設定されます。

* **新規グループテンプレート名**

  テンプレート名 ID。

* **説明**

  テンプレートの説明。

* **無効/有効**

  テンプレートを参照可能にするかどうかを制御する切り替えスイッチ。

#### サムネール {#thumbnail}

![site-thumbnail](assets/site-thumbnail.png)

（オプション）「画像をアップロード」アイコンを選択して、コミュニティサイトの作成者に名前と説明と共にサムネールを表示します。

#### 構造 {#structure}

>[!CAUTION]
>
>AEM 6.1 Communities FP4 以前を使用している場合は、グループテンプレートに groups 関数を追加しないでください。
>
>ネストされたグループ機能は、Communities 以降で使用できます [FP1](/help/communities/communities.md#latestfeaturepack).
>
>Groups 関数をテンプレートの最初の関数または唯一の関数として追加することは、まだ許可されていません。

![グループテンプレートエディター](assets/template-editor.png)

コミュニティ機能を追加するには、サイト メニューのリンクが表示される順序で右から左にドラッグします。 スタイルは、サイトの作成中にテンプレートに適用されます。

例えば、フォーラムが必要な場合は、フォーラム関数をライブラリからドラッグして、テンプレートビルダーの下にドロップします。 その結果、「フォーラム設定」ダイアログが開きます。 を参照してください。 [関数コンソール](/help/communities/functions.md) 設定ダイアログについて詳しくは、「」を参照してください。

このテンプレートをベースとするサブコミュニティサイト（グループ）に必要なその他のコミュニティ機能を引き続きドラッグ&amp;ドロップします。

![ドラッグ関数](assets/dragfunctions.png)

必要なすべての関数をテンプレートビルダー領域にドロップして設定したら、次のオプションを選択します **保存** 右上隅

## グループテンプレートの編集 {#edit-group-template}

メインでコミュニティグループを表示する場合 [グループテンプレートコンソール](#group-templates-console)を使用すれば、既存のグループテンプレートを選択して編集できます。

グループテンプレートを編集しても、そのテンプレートから既に作成されたコミュニティサイトには影響しません。 直接可能です [コミュニティサイトの編集](/help/communities/sites-console.md#modify-structure)代わりに、の構造を使用します。

このプロセスでは、と同じパネルが提供されます [グループテンプレートの作成](#create-group-template).
