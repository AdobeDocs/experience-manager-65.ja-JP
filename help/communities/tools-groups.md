---
title: グループテンプレート
seo-title: Group Templates
description: グループテンプレートコンソールへのアクセス方法
seo-description: How to access the Group Templates console
uuid: 4cf20c91-32b0-4051-a98d-44e4eb50a231
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: e9bfbbce-93fc-455c-a2f7-4ee44e63c03f
docset: aem65
role: Admin
exl-id: aed2c3f2-1b5e-4065-8cec-433abb738ef5
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 42%

---

# グループテンプレート {#group-templates}

グループテンプレートコンソールは、 [サイトテンプレート](/help/communities/sites.md) コンソール。 どちらも、コミュニティサイトを形成する一連の事前に配線されたページと機能のブループリントです。 異なる点は、サイトテンプレートがメインコミュニティ用であり、グループテンプレートがコミュニティグループ用であり、メインコミュニティ内にネストされたサブコミュニティ用である点です。

コミュニティグループは、 [グループ機能](/help/communities/functions.md#groups-function) （テンプレート内で最初に使用することも、唯一の機能として使用することもできません）。

Communities [機能パック 1](/help/communities/deploy-communities.md#latestfeaturepack) 以降、グループテンプレート内にグループ機能を含めることにより、グループをネストできるようになりました。

新しいコミュニティグループを作成するためのアクションが実行されると、そのグループのテンプレート（構造）が選択されます。 選択できる項目は、サイトまたはグループテンプレートに追加したときにグループ機能がどのように設定されたかによって異なります。

>[!NOTE]
>
>作成用のコンソール [コミュニティサイト](/help/communities/sites-console.md), [コミュニティサイトテンプレート](/help/communities/sites.md), [コミュニティグループテンプレート](/help/communities/tools-groups.md) および [コミュニティ機能](/help/communities/functions.md) は、オーサー環境でのみ使用されます。

## グループテンプレートコンソール {#group-templates-console}

AEM オーサー環境でグループテンプレートコンソールにアクセスするには：

* 選択 **ツール |コミュニティ |グループテンプレート，** グローバルナビゲーションから。

このコンソールには、 [コミュニティサイト](/help/communities/sites-console.md) を作成し、新しいグループテンプレートを作成できます。

![コミュニティグループテンプレート](assets/groups-template.png)

## Create Group Template {#create-group-template}

新しいグループテンプレートの作成を開始するには、 `Create`.

するとサイトエディターパネルに移動します。パネルには以下の 3 つのサブパネルがあります。

### 基本情報 {#basic-info}

![site-basic-info](assets/site-basic-info.png)

基本情報パネルでは、名前、説明およびテンプレートを有効にするか無効にするかを設定します。

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
>AEM 6.1 Communities FP4 以前のバージョンを使用している場合は、グループテンプレートにグループ機能を追加しないでください。
>
>ネストされたグループの機能を使用できるのは、Communities [FP1](/help/communities/communities.md#latestfeaturepack) 以降です。
>
>テンプレート内の 1 番目の機能または唯一の機能としてグループ機能を追加することはまだできません。

![グループテンプレートエディター](assets/template-editor.png)

コミュニティ機能を追加するには、右側から左側にドラッグします。サイトメニューのリンクは追加した順番で表示されます。スタイルは、サイトの作成時にテンプレートに適用されます。

例えば、フォーラムが必要な場合は、フォーラム機能をライブラリからテンプレートビルダーにドラッグ＆ドロップします。これにより、フォーラム設定ダイアログが開きます。 詳しくは、 [関数コンソール](/help/communities/functions.md) を参照してください。

このテンプレートに基づくサブコミュニティサイト（グループ）に必要なその他のコミュニティ機能のドラッグ&amp;ドロップを続行します。

![ドラッグ関数](assets/dragfunctions.png)

必要なすべての関数をテンプレートビルダー領域にドロップし、設定したら、「 」を選択します。 **保存** をクリックします。

## グループテンプレートを編集 {#edit-group-template}

メインの[グループテンプレートコンソール](#group-templates-console)でコミュニティグループを表示しているときに、既存のサイトテンプレートを選択して編集できます。

グループテンプレートを編集しても、そのテンプレートを基に作成された既存のコミュニティサイトに影響が及ぶことはありません。その代わりに、直接[コミュニティサイトの構造を編集](/help/communities/sites-console.md#modify-structure)することができます。

このプロセスでは、[グループテンプレートの作成](#create-group-template)と同じパネルを使用します。
