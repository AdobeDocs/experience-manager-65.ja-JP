---
title: グループテンプレート
description: コミュニティサイトを形成する一連の有線化済みのページや機能に対して、グループテンプレートコンソールにアクセスする方法を説明します。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: aed2c3f2-1b5e-4065-8cec-433abb738ef5
source-git-commit: 00b6f2f03470aca7f87717818d0dfcd17ac16bed
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 3%

---

# グループテンプレート {#group-templates}

グループテンプレートコンソールは、 [サイトテンプレート](/help/communities/sites.md) コンソール。 どちらも、コミュニティサイトを形成する一連の事前に配線されたページと機能のブループリントです。 異なる点は、サイトテンプレートがメインコミュニティ用であり、グループテンプレートがコミュニティグループ用であり、サブコミュニティがメインコミュニティ内にネストされている点です。

コミュニティグループをサイトテンプレートに組み込むには、 [Groups 関数 [Groups かんすう ]](/help/communities/functions.md#groups-function) （テンプレート内で最初に使用することも、唯一の機能として使用することもできません）。

コミュニティの時点 [機能パック 1](/help/communities/deploy-communities.md#latestfeaturepack)の場合は、グループテンプレート内にグループ機能を含めることで、グループをネストできます。

コミュニティグループの作成に対するアクションが実行されると、そのグループのテンプレート（構造）が選択されます。 選択できる項目は、サイトまたはグループテンプレートに追加したときにグループ機能がどのように設定されたかによって異なります。

>[!NOTE]
>
>作成用のコンソール [コミュニティサイト](/help/communities/sites-console.md), [コミュニティサイトテンプレート](/help/communities/sites.md), [コミュニティグループテンプレート](/help/communities/tools-groups.md)、および [コミュニティ機能](/help/communities/functions.md) は、オーサー環境でのみ使用されます。

## グループテンプレートコンソール {#group-templates-console}

AEMオーサー環境でグループテンプレートコンソールにアクセスするには：

* 選択 **ツール |コミュニティ |グループテンプレート，** グローバルナビゲーションから。

このコンソールには、 [コミュニティサイト](/help/communities/sites-console.md) を作成し、新しいグループテンプレートを作成できます。

![コミュニティグループテンプレート](assets/groups-template.png)

## グループテンプレートを作成 {#create-group-template}

グループテンプレートの作成を開始するには、「 `Create`.

これにより、次の 3 つのサブパネルを含むサイトエディターパネルが表示されます。

### 基本情報 {#basic-info}

![site-basic-info](assets/site-basic-info.png)

基本情報パネルで、名前と説明、およびテンプレートの有効/無効を設定します。

* **新規グループテンプレート名**

  テンプレート名 ID。

* **説明**

  テンプレートの説明。

* **無効/有効**

  テンプレートを参照可能にするかどうかを制御する切り替えスイッチ。

#### サムネール {#thumbnail}

![site-thumbnail](assets/site-thumbnail.png)

（オプション）「画像をアップロード」アイコンを選択して、コミュニティサイトの作成者に対して、名前と説明に加えてサムネールを表示します。

#### 構造 {#structure}

>[!CAUTION]
>
>AEM 6.1 Communities FP4 以前を操作する場合は、グループテンプレートにグループ機能を追加しないでください。
>
>ネストされたグループ機能は、コミュニティで利用できます。 [FP1](/help/communities/communities.md#latestfeaturepack).
>
>グループ機能をテンプレートの最初の関数または唯一の関数として追加することは、まだできません。

![グループテンプレートエディター](assets/template-editor.png)

コミュニティ機能を追加するには、サイトメニューのリンクが表示される順に、右側から左にドラッグします。 スタイルは、サイトの作成時にテンプレートに適用されます。

例えば、フォーラムが必要な場合は、フォーラム機能をライブラリからドラッグし、テンプレートビルダーの下にドロップします。 その結果、フォーラム設定ダイアログが開きます。 詳しくは、 [関数コンソール](/help/communities/functions.md) を参照してください。

このテンプレートに基づくサブコミュニティサイト（グループ）に必要なその他のコミュニティ機能のドラッグ&amp;ドロップを続行します。

![ドラッグ関数](assets/dragfunctions.png)

必要なすべての関数をテンプレートビルダー領域にドロップし、設定したら、「 」を選択します。 **保存** をクリックします。

## グループテンプレートを編集 {#edit-group-template}

メインでコミュニティグループを表示する場合 [グループテンプレートコンソール](#group-templates-console)の場合は、編集用に既存のグループテンプレートを選択できます。

グループテンプレートを編集しても、テンプレートから既に作成されているコミュニティサイトには影響しません。 直接 [コミュニティサイトを編集](/help/communities/sites-console.md#modify-structure)の構造が代わりに使用されます。

このプロセスは、 [グループテンプレートの作成](#create-group-template).
