---
title: グループテンプレート
seo-title: グループテンプレート
description: グループテンプレートコンソールへのアクセス方法
seo-description: グループテンプレートコンソールへのアクセス方法
uuid: 4cf20c91-32b0-4051-a98d-44e4eb50a231
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: e9bfbbce-93fc-455c-a2f7-4ee44e63c03f
docset: aem65
role: Administrator
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 42%

---


# グループテンプレート {#group-templates}

グループテンプレートコンソールは、[サイトテンプレート](/help/communities/sites.md)コンソールに似ています。 どちらも、コミュニティサイトを形成する一連の事前に結線されたページと機能のブループリントです。 違いは、サイトテンプレートがメインコミュニティ用であり、グループテンプレートがコミュニティグループ用であり、メインコミュニティ内にネストされたサブコミュニティ用である点です。

[Groups関数](/help/communities/functions.md#groups-function)を含めることで、コミュニティグループをサイトテンプレートに組み込みます（これは、テンプレート内で最初の機能でも唯一の機能でもありません）。

Communities [機能パック 1](/help/communities/deploy-communities.md#latestfeaturepack) 以降、グループテンプレート内にグループ機能を含めることにより、グループをネストできるようになりました。

新しいコミュニティグループを作成するためのアクションが実行されると、そのグループのテンプレート（構造）が選択されます。 選択肢は、サイトまたはグループテンプレートに追加したときにグループ機能がどのように設定されたかによって異なります。

>[!NOTE]
>
>[コミュニティサイト](/help/communities/sites-console.md)、[コミュニティサイトテンプレート](/help/communities/sites.md)、[コミュニティグループテンプレート](/help/communities/tools-groups.md)、[コミュニティ機能](/help/communities/functions.md)の作成用のコンソールは、オーサー環境でのみ使用できます。

## Group Templates Console {#group-templates-console}

AEMオーサー環境でグループテンプレートコンソールにアクセスするには：

* **ツールを選択します。 |コミュニティ |グローバルナビゲーションからのグループテンプレート**。

このコンソールには、[コミュニティサイト](/help/communities/sites-console.md)を作成できるテンプレートが表示され、新しいグループテンプレートを作成できます。

![コミュニティグループテンプレート](assets/groups-template.png)

## Create Group Template {#create-group-template}

新しいグループテンプレートの作成を開始するには、「`Create`」を選択します。

するとサイトエディターパネルに移動します。パネルには以下の 3 つのサブパネルがあります。

### 基本情報 {#basic-info}

![site-basic-info](assets/site-basic-info.png)

基本情報パネルでは、名前、説明およびテンプレートを有効にするか無効にするかを設定します。

* **新規グループテンプレート名**

   テンプレート名ID。

* **説明**

   テンプレートの説明。

* **無効/有効**

   テンプレートを参照可能にするかどうかを制御する切り替えスイッチ。

#### サムネール {#thumbnail}

![site-thumbnail](assets/site-thumbnail.png)

（オプション）「画像をアップロード」アイコンを選択して、コミュニティサイトの作成者に対して、名前と説明に加えて「サムネール」を表示します。

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

例えば、フォーラムが必要な場合は、フォーラム機能をライブラリからテンプレートビルダーにドラッグ＆ドロップします。これにより、フォーラム設定ダイアログが開きます。 設定ダイアログについて詳しくは、[関数コンソール](/help/communities/functions.md)を参照してください。

このテンプレートに基づくサブコミュニティサイト（グループ）に必要な他のコミュニティ機能のドラッグ&amp;ドロップを続行します。

![ドラッグ機能](assets/dragfunctions.png)

必要な関数をすべてテンプレートビルダー領域にドロップして設定したら、右上隅の「**保存**」を選択します。

## グループテンプレートを編集 {#edit-group-template}

メインの[グループテンプレートコンソール](#group-templates-console)でコミュニティグループを表示しているときに、既存のサイトテンプレートを選択して編集できます。

グループテンプレートを編集しても、そのテンプレートを基に作成された既存のコミュニティサイトに影響が及ぶことはありません。その代わりに、直接[コミュニティサイトの構造を編集](/help/communities/sites-console.md#modify-structure)することができます。

このプロセスでは、[グループテンプレートの作成](#create-group-template)と同じパネルを使用します。
