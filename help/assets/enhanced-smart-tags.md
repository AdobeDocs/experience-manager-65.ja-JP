---
title: 拡張スマートタグ
description: 拡張スマートタグ
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5599e0d4a3e52a4ad98b776b9178722c7ac47cbc
workflow-type: tm+mt
source-wordcount: '1522'
ht-degree: 64%

---


# 拡張スマートタグ {#enhanced-smart-tags}

デジタルアセットを扱う組織では、アセットメタデータで分類に基づく統制語彙を使用することがますます多くなっています。これには、基本的に、従業員、パートナーおよび顧客が特定のクラスのデジタルアセットを参照したり、検索したりする場合によく使用するキーワードのリストが含まれます。分類に基づく統制語彙によりアセットをタグ付けすると、タグベースの検索でアセットを特定し、取得することが容易になります。

自然言語語彙と比較して、ビジネス上の分類に基づいたデジタルアセットのタグ付けでは、デジタルアセットを会社のビジネスと容易に連携させることができ、関連性の最も高いアセットが検索で表示されるようになります。

例えば、自動車メーカーでは、プロモーションキャンペーンを計画するために様々なモデルの画像を検索する際、関連性の高い画像のみが表示されるように、モデル名を使用して車の画像をタグ付けすることができます。

スマートコンテンツサービスで適切なタグを適用するには、分類を認識するようにサービスをトレーニングする必要があります。サービスをトレーニングするにはまず、アセットのセットとそれらのアセットを最も的確に表すタグをキュレーションします。これらのタグをアセットに適用し、トレーニングワークフローを実行してサービスがこれを学習できるようにします。

タグのトレーニングが完了して準備が整ったら、サービスは、タグ付けワークフローを通じてこれらのタグをアセットに適用できるようになります。

背景には、スマートコンテンツサービスは、Adobe SenseiAIフレームワークを使用して、タグ構造とビジネス分類に対する画像認識アルゴリズムのトレーニングを行っています。 その後、このコンテンツインテリジェンスを使用して、アセットの個々のセットに関連性の高いタグが適用されます。

Smart Content Service is a cloud service that is hosted on Adobe I/O. To use it in [!DNL Adobe Experience Manager], the system administrator must integrate your [!DNL Experience Manager] deployment with Adobe I/O.

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
* Smart Content Services Baseパッケージは、 [!DNL Sites][!DNL Assets] Baseパッケージとアドオンがライセンスされている展開にのみ追加できます。

## 使用開始 {#onboarding}

The Smart Content Service is available for purchase as an add-on to [!DNL Experience Manager]. 購入後、AdobeI/Oへのリンクを含む電子メールが組織の管理者に送信されます。

The administrator can follow the link to integrate the Smart Content Service with [!DNL Experience Manager]. To integrate the service with [!DNL Experience Manager Assets], see [Configure Smart Tags](config-smart-tagging.md).

The onboarding process is complete when the administrator configures the service and adds users in [!DNL Experience Manager].

>[!NOTE]
>
>6.3以前のバージョンを使用していて、アセットにタグ付けサービスが必要な場合は、 [!DNL Experience Manager] スマートタグを参照してください [](https://helpx.adobe.com/experience-manager/6-3/assets/using/touch-ui-smart-tags.html)。 スマートタグは最新のAI機能を使用しないので、高度なスマートタグサービスに比べて正確性が低くなります。

## アセットとタグの確認 {#reviewing-assets-and-tags}

オンボードに入った後、まず最初に行いたいのは、ビジネスの中でこれらのイメージを最も適切に表すタグのセットを特定することです。

次に、各画像をレビューして、特定のビジネス要件について製品を最も的確に表す画像のセットを識別します。Ensure that the assets in your curated set conform to [Smart Content Service training guidelines](/help/assets/config-smart-tagging.md#training-the-smart-content-service).

アセットをフォルダーに追加し、プロパティページで各アセットにタグを適用します。その後、このフォルダーに対してトレーニングワークフローを実行します。キュレーション後のアセットセットを使用すると、スマートコンテンツサービスで分類の定義を使用して、より多くのアセットを効果的にトレーニングできます。

>[!NOTE]
>
>1. トレーニングは元に戻すことができないプロセスです。キュレーション後のアセットセット内のタグを十分に確認してから、スマートコンテンツサービスに対してそれらのタグのトレーニングを実施することをお勧めします。
>1. タグのトレーニングを行う前に、 [Smart Content Serviceのトレーニングガイドラインを参照してください](/help/assets/config-smart-tagging.md#training-the-smart-content-service)。
>1. スマートコンテンツサービスのトレーニングを初めておこなうときには、少なくとも 2 つの異なるタグについてトレーニングすることをお勧めします。


## Understand [!DNL Experience Manager] search results with smart tags {#understandsearch}

By default, [!DNL Experience Manager] search combines the search terms with an `AND` clause. スマートタグを使用しても、このデフォルトの動作は変わりません。スマートタグを使用すると、適用されたスマートタグ内にある検索用語のいずれかを探すための `OR` 句が追加されます。例えば、「`woman running`」を検索する場合を考えます。デフォルトでは、「`woman`」のみ、または「`running`」のみがメタデータに含まれているアセットは、検索結果に表示されません。しかし、スマートタグを使って「`woman`」または「`running`」のどちらかがタグ付けされているアセットは、そうした検索クエリに表示されます。つまり、検索結果は、以下を組み合わせたものになります。

* 「`woman`」と「`running`」の両方のキーワードがメタデータ内にあるアセット。

* 上記どちらかのキーワードがメタデータ内にあるアセット。

メタデータフィールド内のすべての検索用語に一致する検索結果が最初に表示され、スマートタグ内の検索用語のいずれかに一致する検索結果はその後に表示されます。上記の例の場合、検索結果が表示される順序はおおよそ次のようになります。

1. 各種メタデータフィールド内の「`woman running`」に一致するもの。
1. スマートタグ内の「`woman running`」に一致するもの。
1. スマートタグ内の「`woman`」または「`running`」に一致するもの。

>[!CAUTION]
>
>Luceneのインデックス作成が終了した場合 [!DNL Adobe Experience Manager] 、スマートタグに基づく検索が期待どおりに動作しません。

## アセットの自動タグ付け {#tagging-assets-automatically}

スマートコンテンツサービスのトレーニングが完了したら、タグ付けワークフローを実行して、類似するアセットの個々のセットに適切なタグを自動的に適用することができます。

タグ付けワークフローは、定期的に実行することも、必要に応じて実行することもできます。

>[!NOTE]
>
>タグ付けワークフローは、アセットとフォルダーの両方に対して実行されます。

### 定期的なタグ付け {#periodic-tagging}

スマートコンテンツサービスを有効にして、フォルダー内のアセットを定期的にタグ付けすることができます。Open the properties page of your asset folder, select **[!UICONTROL Enable Smart Tags]** under the **[!UICONTROL Details]** tab, and save the changes.

フォルダーに対してこのオプションを選択すると、Smart Content Serviceはフォルダー内のアセットに自動的にタグを付けます。 デフォルトでは、タグ付けワークフローは毎日午前12時に実行されます。

### オンデマンドのタグ付け {#on-demand-tagging}

タグ付けワークフローは、ワークフローコンソールまたはタイムラインからトリガーして、アセットに即座にタグ付けすることができます。

>[!NOTE]
>
>タイムラインからタグ付けワークフローを実行する場合、一度に最大 15 個のアセットにタグを適用できます。

#### ワークフローコンソールからのアセットのタグ付け {#tagging-assets-from-the-workflow-console}

1. In [!DNL Experience Manager] interface, go to **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. **[!UICONTROL ワークフローモデル]**&#x200B;ページで、「**[!UICONTROL DAM スマートタグアセット]**」ワークフローを選択し、ツールバーの「**[!UICONTROL ワークフローを開始]**」をクリックします。

   ![dam_smart_tag_workflow](assets/dam_smart_tag_workflow.png)

1. **[!UICONTROL ワークフローを実行]**&#x200B;ダイアログで、タグを自動的に適用するアセットが格納されているペイロードフォルダーを参照します。
1. ワークフローのタイトルとオプションのコメントを指定します。「**[!UICONTROL 実行]**」をクリックします。

   ![tagging_dialog](assets/tagging_dialog.png)

   アセットフォルダーに移動してタグをレビューし、スマートコンテンツサービスによってアセットが適切にタグ付けされているかどうかを確認します。

#### タイムラインからのアセットのタグ付け {#tagging-assets-from-the-timeline}

1. From the [!DNL Assets] user interface, select the folder containing assets or specific assets to which you want to apply smart tags.
1. 左上隅から、**[!UICONTROL タイムライン]**&#x200B;を開きます。
1. 左側のサイドバーの下部からアクションを開き、「**[!UICONTROL 開始ワークフロー]**」をクリックします。

   ![start_workflow](assets/start_workflow.png)

1. 「**[!UICONTROL DAM スマートタグアセット]**」ワークフローを選択し、ワークフローのタイトルを指定します。
1. 「**[!UICONTROL 開始]**」をクリックします。ワークフローによってアセットにタグが適用されます。アセットフォルダーに移動してタグをレビューし、スマートコンテンツサービスによってアセットが適切にタグ付けされているかどうかを確認します。

>[!NOTE]
>
>後続のタグ付けサイクルでは、新しくトレーニングされたタグを使用して、変更したアセットのみが再度タグ付けされます。ただし、タグ付けワークフローの最後のタグ付けサイクルと現在のタグ付けサイクルの間のギャップが 24 時間を超える場合は、変更されないアセットもタグ付けされます。定期的なタグ付けワークフローについては、時間の間隔が 6 ヶ月を超えると、変更されていないアセットがタグ付けされます。

## 適用したスマートタグをキュレーションまたはモデレートします {#manage-smart-tags}

スマートタグをキュレーションして、ブランド画像に割り当てられている不正確なタグを削除し、最も関連性の高いタグのみを表示できます。

また、スマートタグをモデレートすると、画像が最も関連性の高いタグの検索結果に表示されるようになるので、画像のタグベース検索の精度が向上します。実質的には、検索結果に関連性のない画像が表示されないようにすることができます。

タグに高いランクを割り当てて、画像に関して関連性を高めることもできます。画像のタグのランクを高くすることで、特定のタグに基づいて検索が実行されたときに、その画像が検索結果に表示される可能性が高くなります。

1. オムニサーチボックスで、タグに基づいてアセットを検索します。
1. 検索結果を調査し、検索に関連性のない画像を特定します。
1. Select the image, and click **[!UICONTROL Manage Tags]** from the toolbar.
1. **[!UICONTROL タグを管理]**&#x200B;ページで、タグを調査します。If you don&#39;t want the image to be searched based on a specific tag, select the tag and then click **[!UICONTROL Delete]** from the toolbar. または、タグの横に表示される `x` 記号をクリックします。
1. Optionally, to assign a higher rank to a tag, select the tag and click **[!UICONTROL Promote]** from the toolbar. 昇格したタグは、「**[!UICONTROL タグ]**」セクションに移動されます。
1. Click **[!UICONTROL Save]** and then click **[!UICONTROL OK]**
1. Navigate to the **[!UICONTROL Properties]** page for the image. 昇格したタグにより関連性が高く、検索結果の前の方に表示されることを確認します。

## ヒントと制限事項 {#tips-best-practices-limitations}

* Smart Content Servicesの使用は、タグ付き画像の年間使用量が最大200万個に制限されています。 処理およびタグ付けされた重複画像は、それぞれタグ付けされた画像としてカウントされます。
* タイムラインからタグ付けワークフローを実行する場合、一度に最大 15 個のアセットにタグを適用できます。
