---
title: 拡張スマートタグ
description: 拡張スマートタグ
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# 拡張スマートタグ {#enhanced-smart-tags}

## 拡張スマートタグの概要 {#overview-of-enhanced-smart-tags}

デジタルアセットを扱う組織では、アセットメタデータで分類に基づく統制語彙を使用することがますます多くなっています。これには、基本的に、従業員、パートナーおよび顧客が特定のクラスのデジタルアセットを参照したり、検索したりする場合によく使用するキーワードのリストが含まれます。分類に基づく統制語彙によりアセットをタグ付けすると、タグベースの検索でアセットを特定し、取得することが容易になります。

自然言語語彙と比較して、ビジネス上の分類に基づいたデジタルアセットのタグ付けでは、デジタルアセットを会社のビジネスと容易に連携させることができ、関連性の最も高いアセットが検索で表示されるようになります。

例えば、自動車メーカーでは、プロモーションキャンペーンを計画するために様々なモデルの画像を検索する際、関連性の高い画像のみが表示されるように、モデル名を使用して車の画像をタグ付けすることができます。

スマートコンテンツサービスで適切なタグを適用するには、分類を認識するようにサービスをトレーニングする必要があります。サービスをトレーニングするにはまず、アセットのセットとそれらのアセットを最も的確に表すタグをキュレーションします。これらのタグをアセットに適用し、トレーニングワークフローを実行してサービスがこれを学習できるようにします。

タグのトレーニングが完了して準備が整ったら、サービスは、タグ付けワークフローを通じてこれらのタグをアセットに適用できるようになります。

スマートコンテンツサービスでは、バックグラウンドで Adobe Sensei の AI フレームワークを使用して、タグ構造およびビジネス上の分類に基づいてその画像認識アルゴリズムのトレーニングをおこないます。その後、このコンテンツインテリジェンスを使用して、アセットの個々のセットに関連性の高いタグが適用されます。

スマートコンテンツサービスは、Adobe I/O 上にホストされるクラウドサービスです。このサービスを Adobe Experience Manager（AEM）で使用するには、システム管理者が AEM インスタンスを Adobe I/O と統合する必要があります。

要約すると、スマートコンテンツサービスを使用するための主な手順は次のとおりです。

* 使用開始
* アセットおよびタグの検討（分類の定義）
* スマートコンテンツサービスのトレーニング
* 自動タグ付け

![フローチャート](assets/flowchart.gif)

## 前提条件 {#prerequisites}

Adobe I/O で統合を作成してスマートコンテンツサービスを使用する前に、以下の事項を確認します。

* 組織の管理者権限を持つ Adobe ID アカウントがあること。
* 組織でスマートコンテンツサービスが有効化されていること。

## 使用開始 {#onboarding}

Smart Content Serviceは、AEMのアドオンとして購入できます。購入後、Adobe IOへのリンクを含む電子メールが組織の管理者に送信されます。

管理者は、そのリンクにアクセスしてスマートコンテンツサービスを AEM と統合することができます。このサービスを AEM Assets と統合するには、](config-smart-tagging.md)スマートタグの設定[を参照してください。

管理者がサービスを設定し、AEM でユーザーを追加すると、使用開始プロセスは完了です。

>[!NOTE]
>
>AEM 6.3以前のバージョンを使用し、アセットのタグ付けサービスが必要な場合は、「スマートタグ」を参照 [してください](https://helpx.adobe.com/experience-manager/6-3/assets/using/touch-ui-smart-tags.html)。 スマートタグは最新のAI機能を使用しないので、強化されたスマートタグサービスに比べて精度が低くなります。

## アセットとタグの確認 {#reviewing-assets-and-tags}

使用開始プロセスが完了したら、まず、ビジネスのコンテキストにおいて各画像を最も的確に表すタグのセットを識別します。

次に、各画像をレビューして、特定のビジネス要件について製品を最も的確に表す画像のセットを識別します。Ensure that the assets in your curated set conform to [Smart Content Service training guidelines](smart-tags-training-guidelines.md).

アセットをフォルダーに追加し、プロパティページで各アセットにタグを適用します。その後、このフォルダーに対してトレーニングワークフローを実行します。キュレーション後のアセットセットを使用すると、スマートコンテンツサービスで分類の定義を使用して、より多くのアセットを効果的にトレーニングできます。

>[!NOTE]
>
>1. トレーニングは元に戻すことができないプロセスです。キュレーション後のアセットセット内のタグを十分に確認してから、スマートコンテンツサービスに対してそれらのタグのトレーニングを実施することをお勧めします。
>1. Please do read [Smart Content Service training guidelines](smart-tags-training-guidelines.md) before starting training for any tag.
>1. スマートコンテンツサービスのトレーニングを初めておこなうときには、少なくとも 2 つの異なるタグについてトレーニングすることをお勧めします。


## スマートコンテンツサービスのトレーニング {#training-the-smart-content-service}

スマートコンテンツサービスでビジネス上の分類を認識できるように、ビジネスに関連するタグが既に含まれているアセットのセットに対してサービスを実行します。トレーニングが完了すると、サービスは、類似するアセットのセットに同じ分類を適用できるようになります。

サービスのトレーニングを複数回実施すると、関連性の高いタグを適用する能力が向上します。トレーニングサイクルが終了するたびに、タグ付けワークフローを実行し、アセットが適切にタグ付けされるかどうかを確認します。

スマートコンテンツサービスのトレーニングは、定期的に実施することも、必要に応じて実施することもできます。

>[!NOTE]
>
>トレーニングワークフローは、フォルダーに対してのみ実行されます。

### 定期的なトレーニング {#periodic-training}

スマートコンテンツサービスを有効にして、フォルダー内のアセットおよび関連するタグに関する定期的なトレーニングを実施することができます。Open the properties page of your asset folder, select **[!UICONTROL Enable Smart Tags]** under the **[!UICONTROL Details]** tab, and save the changes.

![enable_smart_tags](assets/enable_smart_tags.png)

フォルダーに対してこのオプションを選択すると、トレーニングワークフローが自動的に実行され、フォルダーのアセットおよびそのタグに関するスマートコンテンツサービスのトレーニングが実施されます。デフォルトでは、トレーニングワークフローは週に 1 回、土曜日の午前 0 時 30 分に実行されます。

### オンデマンドのトレーニング {#on-demand-training}

ワークフローコンソールから、必要に応じていつでもスマートコンテンツサービスのトレーニングをおこなうことができます。

1. AEM のロゴをタップまたはクリックし、**[!UICONTROL ツール／ワークフロー／モデル]**&#x200B;に移動します。
1. **[!UICONTROL ワークフローモデル]**&#x200B;ページで、「**[!UICONTROL スマートタグトレーニング]**」ワークフローを選択し、ツールバーの「**[!UICONTROL ワークフローを開始]**」をタップまたはクリックします。
1. **[!UICONTROL ワークフローを実行]**&#x200B;ダイアログで、サービスのトレーニングに使用するタグ付けされたアセットが格納されているペイロードフォルダーを参照します。
1. ワークフローのタイトルを指定し、コメントを追加します。次に、「**[!UICONTROL 実行]**」をタップまたはクリックします。アセットとタグがトレーニングのために送信されます。

   ![workflow_dialog](assets/workflow_dialog.png)

>[!NOTE]
>
>フォルダー内のアセットがトレーニング用に処理されると、変更されたアセットのみが後続のトレーニングサイクルで処理されます。

### トレーニングレポートの表示 {#viewing-training-reports}

アセットのトレーニングセット内のタグに関するスマートコンテンツサービスのトレーニングが実施されたかどうかを確認するには、レポートコンソールでトレーニングワークフローレポートを調べます。

1. Tap/click the AEM logo, and go to **[!UICONTROL Tools > Assets > Reports]**.
1. **[!UICONTROL アセットレポート]**&#x200B;ページで、「**[!UICONTROL 作成]**」をタップまたはクリックします。
1. Select the **[!UICONTROL Smart Tags Training]** report, and then tap/click **[!UICONTROL Next]** from the toolbar.
1. レポートのタイトルと説明を指定します。「**[!UICONTROL レポートをスケジュール]**」で、「**[!UICONTROL 今すぐ]**」オプションを選択したままにします。レポートを後で生成するようにスケジュールするには、「**[!UICONTROL 後で]**」を選択し、日時を指定します。次に、ツールバーの「**[!UICONTROL 作成]**」をタップまたはクリックします。
1. **[!UICONTROL アセットレポート]**&#x200B;ページで、生成したレポートを選択します。To view the report, tap **[!UICONTROL View]** from the toolbar.
1. レポートの詳細をレビューします。

   レポートには、トレーニングしたタグのトレーニングステータスが表示されます。The green color in the **[!UICONTROL Training Status]** column indicates that the Smart Content Service is trained for the tag. 黄色は、特定のタグに関するサービスのトレーニングが完全には実施されていないことを示します。この場合、特定のタグを含む画像をさらに追加し、トレーニングワークフローを実行して、そのタグに関するサービスのトレーニングを完全に実施します。

   このレポートにタグが表示されない場合は、それらのタグに関するトレーニングワークフローを再度実行してください。

1. To download the report, select it from the list, and tap **[!UICONTROL Download]** from the toolbar. レポートが Excel ファイルとしてダウンロードされます。

## アセットの自動タグ付け {#tagging-assets-automatically}

スマートコンテンツサービスのトレーニングが完了したら、タグ付けワークフローを実行して、類似するアセットの個々のセットに適切なタグを自動的に適用することができます。

タグ付けワークフローは、定期的に実行することも、必要に応じて実行することもできます。

>[!NOTE]
>
>タグ付けワークフローは、アセットとフォルダーの両方に対して実行されます。

### 定期的なタグ付け {#periodic-tagging}

スマートコンテンツサービスを有効にして、フォルダー内のアセットを定期的にタグ付けすることができます。Open the properties page of your asset folder, select **[!UICONTROL Enable Smart Tags]** under the **[!UICONTROL Details]** tab, and save the changes.

フォルダーに対してこのオプションを選択すると、Smart Content Serviceはフォルダー内のアセットに自動的にタグを付けます。 デフォルトでは、タグ付けワークフローは毎日午前12:00に実行されます。

### オンデマンドのタグ付け {#on-demand-tagging}

次の場所からタグ付けワークフローを実行して、アセットをすぐにタグ付けすることができます。

* ワークフローコンソール
* タイムライン

>[!NOTE]
>
>タイムラインからタグ付けワークフローを実行する場合、一度に最大 15 個のアセットにタグを適用できます。

#### Tag assets from the workflow console {#tagging-assets-from-the-workflow-console}

1. AEM のロゴをタップまたはクリックし、**[!UICONTROL ツール／ワークフロー／モデル]**&#x200B;に移動します。
1. From the **[!UICONTROL Workflow Models]** page, select the **[!UICONTROL DAM Smart Tags Assets]** workflow and then tap/click **[!UICONTROL Start Workflow]** from the toolbar.

   ![dam_smart_tag_workflow](assets/dam_smart_tag_workflow.png)

1. In the **[!UICONTROL Run Workflow]** dialog, browse to the payload folder containing assets on which you want to apply your tags automatically.
1. ワークフローのタイトルとオプションのコメントを指定します。次に、「**[!UICONTROL 実行]**」をタップまたはクリックします。

   ![tagging_dialog](assets/tagging_dialog.png)

   アセットフォルダーに移動してタグをレビューし、スマートコンテンツサービスによってアセットが適切にタグ付けされているかどうかを確認します。For details, see [Managing Smart Tags](managing-smart-tags.md).

#### Tag assets from the timeline {#tagging-assets-from-the-timeline}

1. Assets のユーザーインターフェイスで、スマートタグを適用するアセットが格納されているフォルダーまたは特定のアセットを選択します。
1. Experience Managerのロゴをタップし、タイムラインを開きます。
1. Tap the arrow at the bottom, and then tap/click **[!UICONTROL Start Workflow]**.

   ![start_workflow](assets/start_workflow.png)

1. 「**[!UICONTROL DAM スマートタグアセット]**」ワークフローを選択し、ワークフローのタイトルを指定します。
1. 「**[!UICONTROL 開始]**」をタップまたはクリックします。ワークフローによってアセットにタグが適用されます。アセットフォルダーに移動してタグをレビューし、スマートコンテンツサービスによってアセットが適切にタグ付けされているかどうかを確認します。For details, see [Managing Smart Tags](managing-smart-tags.md).

>[!NOTE]
>
>後続のタグ付けサイクルでは、変更されたアセットのみが、新しくトレーニングされたタグで再度タグ付けされます。
>
>ただし、タグ付けワークフローの最後のタグ付けサイクルと現在のタグ付けサイクルの間のギャップが24時間を超える場合は、変更されていないアセットにもタグが付けられます。
>
>定期的なタグ付けワークフローについては、間隔が 6 ヶ月を超えると、変更されていないアセットがタグ付けされます。
