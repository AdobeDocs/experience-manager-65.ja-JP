---
title: コンテンツページへのワークフローの適用
description: オーサリングでは、ワークフローを呼び出して、ページにアクションを実行できます。複数のワークフローを適用することもできます。
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
docset: aem65
exl-id: e00da2b3-046a-4d93-aed0-07dd8c66899f
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 90%

---

# ページへのワークフローの適用 {#applying-workflows-to-pages}

オーサリングでは、ワークフローを呼び出して、ページにアクションを実行することができます。複数のワークフローを適用することもできます。

ワークフローを適用する際には、次の情報を指定します。

* 適用されるワークフロー。
（AEM 管理者によって割り当てられた、アクセス権限がある）任意のワークフローを適用できます。
* オプションで、ユーザーのインボックス内のワークフローインスタンスの特定に役立つタイトル。
* ワークフローのペイロード。1 つ以上のページを指定できます。

ワークフローは、次の場所から開始できます。

* [サイトコンソール](#starting-a-workflow-from-the-sites-console)。
* [ページの編集中に「ページ情報](#starting-a-workflow-from-the-page-editor)」から。

>[!NOTE]
>
>関連トピック：
>
>* [DAM アセットにワークフローを適用する方法](/help/assets/assets-workflow.md)
>* [プロジェクトワークフローの操作](/help/sites-authoring/projects-with-workflows.md)。
>

>[!NOTE]
>
>AEM 管理者は[他のいくつかの方法を使用してワークフローを開始](/help/sites-administering/workflows-starting.md)できます。

## Sites コンソールからのワークフローの開始 {#starting-a-workflow-from-the-sites-console}

ワークフローは以下のいずれかから開始できます。

* [サイトツールバーの「作成」オプション](#starting-a-workflow-from-the-sites-toolbar)。
* [サイトコンソールのタイムラインレール](#starting-a-workflow-from-the-timeline)。

どちらの場合も、次の操作が必要です。

* [ワークフローを作成ウィザードでワークフローの詳細を指定します](#specifying-workflow-details-in-the-create-workflow-wizard)。

### Sites ツールバーからのワークフローの開始 {#starting-a-workflow-from-the-sites-toolbar}

**サイト**&#x200B;コンソールのツールバーからワークフローを開始できます。

1. 必要なページに移動して選択します。

1. これでツールバーの「**作成**」オプションで「**ワークフロー**」を選択できます。

   ![screen_shot_2019-03-06at121237pm](assets/screen_shot_2019-03-06at121237pm.png)

1. **ワークフローを作成**&#x200B;ウィザードは、[ワークフローの詳細を指定](#specifying-workflow-details-in-the-create-workflow-wizard)するのに役立ちます。

### タイムラインからのワークフローの開始 {#starting-a-workflow-from-the-timeline}

**タイムライン**&#x200B;から、選択したリソースに適用されるワークフローを開始できます。

1. [リソースを選択](/help/sites-authoring/basic-handling.md#viewingandselectingyourresources)し、[タイムライン](/help/sites-authoring/basic-handling.md#timeline)を開きます（またはタイムラインを開いてからリソースを選択します）。
1. コメントフィールドの横にある矢印を使用すると、「**ワークフローを開始**」が表示されます。

   ![screen-shot_2019-03-05at120026](assets/screen-shot_2019-03-05at120026.png)

1. **ワークフローを作成**&#x200B;ウィザードは、[ワークフローの詳細を指定](#specifying-workflow-details-in-the-create-workflow-wizard)するのに役立ちます。

### ワークフローを作成ウィザードでのワークフローの詳細の指定 {#specifying-workflow-details-in-the-create-workflow-wizard}

**ワークフローを作成**&#x200B;ウィザードは、ワークフローを選択し、必要な詳細を指定するのに役立ちます。

**ワークフローを作成**&#x200B;ウィザードを次のいずれかから開きます。

* [サイトツールバーの「作成」オプション](#starting-a-workflow-from-the-sites-toolbar)。
* [サイトコンソールのタイムラインレール](#starting-a-workflow-from-the-timeline)。

次の詳細を指定できます。

1. **プロパティ**&#x200B;の手順では、ワークフローの基本オプションを定義します。

   * **ワークフローモデル**
   * **ワークフロータイトル**

      * このインスタンスのタイトルを指定して、後の段階で識別しやすくできます。

   ワークフローモデルに応じて、次のオプションも使用できます。これにより、ペイロードとして作成されたパッケージを、ワークフローの完了後も保持できます。

   * **ワークフローパッケージを維持**
   * **パッケージタイトル**

      * 識別に役立つように、パッケージのタイトルを指定できます。

   >[!NOTE]
   >
   >ワークフローが[マルチリソースサポート](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support)のために設定されており、複数のリソースが選択されている場合は、**ワークフローパッケージを維持**&#x200B;オプションが使用できます。

   完了したら、「**次へ**」を使用して続行します。

   ![wf-52](assets/wf-52.png)

1. **スコープ**&#x200B;ステップで、以下のものを選択できます。

   * **コンテンツを追加** 開く [パスブラウザー](/help/sites-authoring/author-environment-tools.md#path-browser) 追加のリソースを選択します。ブラウザーで、 **選択** をクリックして、コンテンツをワークフローインスタンスに追加します。

   * 追加のアクションを表示するための既存のリソース

      * 「**子を含める**」で、ワークフローに含まれるそのリソースの子を指定します。ダイアログボックスが開き、以下に従って選択を絞り込むことができます。

         * 直近の子のみを含める。
         * 変更されたページのみを含める。
         * 既に公開済みのページのみを含める。

        指定した子は、ワークフローが適用されるリソースのリストに追加されます。

      * 「**選択項目を削除**」で、そのリソースをワークフローから削除します。

   ![wf-53](assets/wf-53.png)

   >[!NOTE]
   >
   >追加リソースを追加する場合は、「**戻る**」を使用して、**プロパティ**&#x200B;ステップで「**ワークフローパッケージを維持**」の設定を調整できます。

1. 「**作成**」を使用して、ウィザードを閉じ、ワークフローインスタンスを作成します。通知はサイトコンソールに表示されます。

## ページエディターからのワークフローの開始 {#starting-a-workflow-from-the-page-editor}

ページの編集時に、ツールバーから「**ページ情報**」を選択できます。ドロップダウンメニューには、「**ワークフローで開始**」オプションがあります。これにより、必要なワークフローと必要に応じてタイトルを指定できるダイアログボックスが開きます。

![wf-54](assets/wf-54.png)
