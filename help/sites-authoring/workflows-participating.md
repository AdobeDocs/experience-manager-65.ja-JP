---
title: 'ワークフローへの参加 '
seo-title: Participating in Workflows
description: ワークフローには通常、ページまたはアセットでユーザーがアクティビティを実行する必要があるステップが含まれています。
seo-description: Workflows typically include steps that require a person to perform an activity on a page or asset.
uuid: 15d56bcc-1e84-4cc0-8b71-7fb906cd7ff7
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: f170613c-329e-446b-9ac3-350615f1bfb6
docset: aem65
exl-id: e47270e8-bace-4d0f-a088-7269b6356315
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '1525'
ht-degree: 100%

---

# ワークフローへの参加 {#participating-in-workflows}

ワークフローには通常、ページまたはアセットでユーザーがアクティビティを実行する必要があるステップが含まれています。ワークフローでアクティビティを実行するユーザーまたはグループを選択し、その人物やグループに作業項目を割り当てます。ユーザーは通知を受け取り、次の適切なアクションを取ることができます。

* [通知の表示](#notifications-of-available-workflow-actions)
* [参加者ステップの完了](#completing-a-participant-step)
* [参加者ステップの委任](#delegating-a-participant-step)
* [参加者ステップでの前のステップの実行](#performing-step-back-on-a-participant-step)
* [ワークフロー項目を開いて、詳細を表示（またはアクションを実行）](#opening-a-workflow-item-to-view-details-and-take-actions)
* [ワークロードペイロード（複数のリソース）を表示](#viewing-the-workflow-payload-multiple-resources)

## 使用可能なワークフローアクションの通知 {#notifications-of-available-workflow-actions}

作業項目（**コンテンツを承認**&#x200B;など）が割り当てられると、様々なアラートや通知が表示されます。

* [通知](/help/sites-authoring/inbox.md)インジケーター（ツールバー）が増加されます

   ![](do-not-localize/wf-57.png)

* 通知[インボックス](/help/sites-authoring/inbox.md)に項目がリストされます

   ![wf-58](assets/wf-58.png)

* ページエディターを使用しているときは、ステータスバーに以下のものが表示されます。

   * アクティベーションのリクエストなど、ページに適用されるワークフローの名前。
   * 完了、委任、詳細表示など、ワークフローの現在のステップで現在のユーザーが使用できる何らかのアクション。
   * ページが対象であるワークフローの数。以下の操作を実行できます。

      * 左／右の矢印を使用して、多様なワークフローのステータス情報を移動できます。
      * 実際の数字をクリック／タップして、すべての適用可能なワークフローのドロップダウンリストを開いてから、ステータスバーに表示するワークフローを選択します。

   ![wf-59](assets/wf-59.png)

   >[!NOTE]
   >
   >ステータスバーは、例えば `workflow-users` グループのメンバーなど、ワークフロー特権のあるユーザーだけに表示されます。
   >
   >
   >現在のユーザーがワークフローの現在のステップに直接関与している場合に、アクションが表示されます。

* **タイムライン**&#x200B;をリソースのために開くとき、ワークフローステップが表示されます。アラートバナーをクリック／タップすると、使用可能なアクションも表示されます。

   ![screen_shot_2019-03-05at120453](assets/screen-shot_2019-03-05at120453.png)

### 参加者ステップの完了 {#completing-a-participant-step}

項目を完了してワークフローを次のステップに進めることができます。

このアクションでは、以下を指定できます。

* **次のステップ**：取るべき次のステップ。提供されたリストから選択できます。
* **コメント**：必要な場合

次のいずれかで参加者ステップを完了できます。

* [インボックス ](#completing-a-participant-step-inbox)
* [ページエディター](#completing-a-participant-step-page-editor)
* [タイムライン](#completing-a-participant-step-timeline)
* [詳細を表示するためにワークフロー項目を開く](#opening-a-workflow-item-to-view-details-and-take-actions)とき

#### 参加者ステップの完了 - インボックス {#completing-a-participant-step-inbox}

以下の手順を使用して作業項目を完了します。

1. **[AEM インボックス](/help/sites-authoring/inbox.md)**&#x200B;を開きます。
1. アクションを実行するワークフロー項目を選択します（サムネールをタップまたはクリック）。
1. ツールバーの「**完了**」を選択します。
1. 「**作業項目を完了**」ダイアログボックスが開きます。ドロップダウンセレクターで「**次のステップ**」を選択し、必要に応じて&#x200B;**コメント**&#x200B;を追加します。
1. 「**OK**」を使用してステップを完了します（または「**キャンセル**」を使用してアクションを中止します）。

#### 参加者ステップの完了 - ページエディター {#completing-a-participant-step-page-editor}

以下の手順を使用して作業項目を完了します。

1. 「[編集するページ](/help/sites-authoring/managing-pages.md#opening-a-page-for-editing)」を開きます。
1. 上部のステータスバーの「**完了**」を選択します。
1. 「**作業項目を完了**」ダイアログボックスが開きます。ドロップダウンセレクターで「**次のステップ**」を選択し、必要に応じて&#x200B;**コメント**&#x200B;を追加します。
1. 「**OK**」を使用してステップを完了します（または「**キャンセル**」を使用してアクションを中止します）。

#### 参加者ステップの完了 - タイムライン {#completing-a-participant-step-timeline}

タイムラインを使用してステップを完了または進めることもできます。

1. 必要なページを選択して&#x200B;**タイムライン**&#x200B;を開きます（または&#x200B;**タイムライン**&#x200B;を開いてからページを選択します）。

   ![screen-shot_2019-03-05at120744](assets/screen-shot_2019-03-05at120744.png)

1. アラートバナーをクリックまたはタップして使用できるアクションを表示します。「**次へ**」を選択します。

   ![screen-shot_2019-03-05at120453-1](assets/screen-shot_2019-03-05at120453-1.png)

1. ワークフローによっては、次のステップを選択できます。

   ![screen-shot_2019-03-05at120905](assets/screen-shot_2019-03-05at120905.png)

1. 「**次へ**」を選択して、アクションを確定します。

### 参加者ステップの委任 {#delegating-a-participant-step}

ステップが割り当てられているが、何らかの理由によってアクションを実行できない場合、そのステップを別のユーザーまたはグループに委任できます。

委任できるユーザーは、作業項目の割り当て先によって異なります。

* 作業項目がグループに割り当てられた場合、グループメンバーに委任できます。
* 作業項目がグループに割り当てられ、ユーザーに委任された場合、グループメンバーおよびグループに委任できます。
* 作業項目が 1 人のユーザーに割り当てられた場合、作業項目を委任することはできません。

このアクションでは、以下を指定できます。

* **ユーザー**：委任対象のユーザー。提供されるリストから選択できます。
* **コメント**：必要な場合

参加者ステップは次のいずれかから委任できます。

* [インボックス ](#delegating-a-participant-step-inbox)
* [ページエディター](#delegating-a-participant-step-page-editor)
* [タイムライン](#delegating-a-participant-step-timeline)
* [詳細を表示するためにワークフロー項目を開く](#opening-a-workflow-item-to-view-details-and-take-actions)とき

#### 参加者ステップの委任 - インボックス {#delegating-a-participant-step-inbox}

以下の手順を使用して作業項目を委任します。

1. **[AEM インボックス](/help/sites-authoring/inbox.md)**&#x200B;を開きます。
1. アクションを実行するワークフロー項目を選択します（サムネールをタップまたはクリック）。
1. ツールバーの「**委任**」を選択します。
1. ダイアログが開きます。ドロップダウンセレクターから「**ユーザー**」（グループも可）を指定し、必要に応じて&#x200B;**コメント**&#x200B;を追加します。
1. 「**OK**」を使用してステップを完了します（または「**キャンセル**」を使用してアクションを中止します）。

#### 参加者ステップの委任 - ページエディター {#delegating-a-participant-step-page-editor}

以下の手順を使用して作業項目を委任します。

1. 「[編集するページ](/help/sites-authoring/managing-pages.md#opening-a-page-for-editing)」を開きます。
1. 上部のステータスバーの「**委任**」を選択します。
1. ダイアログが開きます。ドロップダウンセレクターから「**ユーザー**」（グループも可）を指定し、必要に応じて&#x200B;**コメント**&#x200B;を追加します。
1. 「**OK**」を使用してステップを完了します（または「**キャンセル**」を使用してアクションを中止します）。

#### 参加者ステップの委任 - タイムライン {#delegating-a-participant-step-timeline}

タイムラインを使用してステップを委任または割り当てることもできます。

1. 必要なページを選択して&#x200B;**タイムライン**&#x200B;を開きます（または&#x200B;**タイムライン**&#x200B;を開いてからページを選択します）。
1. アラートバナーをクリックまたはタップして使用できるアクションを表示します。「**担当者を変更**」を選択します。

   ![screen-shot_2019-03-05at120453-2](assets/screen-shot_2019-03-05at120453-2.png)

1. 新しい割り当て先を指定します。

   ![screen-shot_2019-03-05at121025](assets/screen-shot_2019-03-05at121025.png)

1. 「**割り当て**」を選択して、アクションを確定します。

### 参加者ステップでの前のステップの実行 {#performing-step-back-on-a-participant-step}

あるステップまたは一連のステップを繰り返す必要がある場合は、以前のステップに戻すことができます。これによって、ワークフロー内の以前に発生したステップを、再処理のために選択できます。ワークフローが指定したステップに戻り、そこから続行されます。

このアクションでは、以下を指定できます。

* **以前のステップ**：戻り先のステップ。表示されるリストから選択できます
* **コメント**：必要な場合

以下のいずれかから参加者ステップで前のステップを実行することができます。

* [インボックス ](#performing-step-back-on-a-participant-step-inbox)
* [ページエディター](#performing-step-back-on-a-participant-step-page-editor)
* [タイムライン](#performing-step-back-on-a-participant-step-timeline)
* [詳細を表示するためにワークフロー項目を開く](#opening-a-workflow-item-to-view-details-and-take-actions)とき

#### 参加者ステップでの前のステップの実行 - インボックス {#performing-step-back-on-a-participant-step-inbox}

以下の手順を使用して、前のステップを実行します。

1. **[AEM インボックス](/help/sites-authoring/inbox.md)**&#x200B;を開きます。
1. アクションを実行するワークフロー項目を選択します（サムネールをタップまたはクリック）。
1. 「**ステップバック**」を選択して、ダイアログを開きます。

1. 「**前のステップ**」を指定し、必要に応じて&#x200B;**コメント**&#x200B;を追加します。
1. 「**OK**」を使用してステップを完了します（または「**キャンセル**」を使用してアクションを中止します）。

#### 参加者ステップでの前のステップの実行 - ページエディター {#performing-step-back-on-a-participant-step-page-editor}

以下の手順を使用して、前のステップを実行します。

1. 「[編集するページ](/help/sites-authoring/managing-pages.md#opening-a-page-for-editing)」を開きます。
1. 上部のステータスバーの「**前のステップ**」を選択します。
1. 「**前のステップ**」を指定し、必要に応じて&#x200B;**コメント**&#x200B;を追加します。
1. 「**OK**」を使用してステップを完了します（または「**キャンセル**」を使用してアクションを中止します）。

#### 参加者ステップでの前のステップの実行 - タイムライン {#performing-step-back-on-a-participant-step-timeline}

タイムラインを使用して前のステップにロール（ステップ）バックすることもできます。

1. 必要なページを選択して&#x200B;**タイムライン**&#x200B;を開きます（または&#x200B;**タイムライン**&#x200B;を開いてからページを選択します）。
1. アラートバナーをクリックまたはタップして使用できるアクションを表示します。「**ロールバック**」を選択します。

   ![screen-shot_2019-03-05at121131](assets/screen-shot_2019-03-05at121131.png)

1. ワークフローの戻し先のステップを指定します。

   ![screen-shot_2019-03-05at121158](assets/screen-shot_2019-03-05at121158.png)

1. 「**ロールバック**」を選択して、アクションを確定します。

### ワークフロー項目を開いて詳細を表示（およびアクションを実行） {#opening-a-workflow-item-to-view-details-and-take-actions}

ワークフロー作業項目の詳細を表示して、適切なアクションを実行します。

ワークフロー詳細がタブに表示され、適切なアクションがツールバーに表示されます。

* 「**作業項目**」タブ

   ![wf-72](assets/wf-72.png)

* 「**ワークフロー情報**」タブ：

   ![wf-73](assets/wf-73.png)

   [ワークフローステージ](/help/sites-developing/workflows.md#workflow-stages)がモデルに設定されている場合は、これらに従って進行状況を表示できます。

   ![wf-107](assets/wf-107.png)

* 「**コメント**」タブ：

   ![wf-75](assets/wf-75.png)

以下のいずれかから作業項目の詳細を開くことができます。

* [インボックス ](#performing-step-back-on-a-participant-step-inbox)
* [ページエディター](#performing-step-back-on-a-participant-step-page-editor)

#### ワークフロー詳細を開く - インボックス {#opening-workflow-details-inbox}

ワークフロー項目を開き、詳細を表示するには

1. **[AEM インボックス](/help/sites-authoring/inbox.md)**&#x200B;を開きます。
1. アクションを実行するワークフロー項目を選択します（サムネールをタップまたはクリック）。
1. 「**開く**」を選択して、「情報」タブを開きます。

1. 必要に応じて、適切なアクションを選択し、詳細を入力して「**OK**」（または「**キャンセル**」）で確認します。
1. 「**保存**」または「**キャンセル**」を使用して終了します。

#### ワークフロー詳細を開く - ページエディター {#opening-workflow-details-page-editor}

ワークフロー項目を開き、詳細を表示するには

1. 「[編集するページ](/help/sites-authoring/managing-pages.md#opening-a-page-for-editing)」を開きます。
1. ステータスバーの「**詳細の表示**」を選択して、「情報」タブを開きます。

1. 必要に応じて、適切なアクションを選択し、詳細を入力して「**OK**」（または「**キャンセル**」）で確認します。
1. 「**保存**」または「**キャンセル**」を使用して終了します。

### ワークフローペイロード（複数リソース）の表示  {#viewing-the-workflow-payload-multiple-resources}

ワークフローインスタンスに関連付けられたペイロードの詳細を表示できます。最初にパッケージの中のリソースが表示されるので、ドリルダウンして、個別のページを表示できます。

ワークフローインスタンスのペイロードおよびリソースを表示するには

1. **[AEM インボックス](/help/sites-authoring/inbox.md)**&#x200B;を開きます。
1. アクションを実行するワークフロー項目を選択します（サムネールをタップまたはクリック）。
1. ツールバーの「**ペイロードを表示**」を選択して、ダイアログを開きます。

   ワークフローパッケージは単にリポジトリー内のパスへのポインターのコレクションなので、ここでエントリを追加／削除／変更して、ワークフローパッケージから参照されるものを調整できます。**リソース定義**&#x200B;を使用して新しいエントリを追加します。

   ![wf-78](assets/wf-78.png)

1. リンクは、個別のページを開くために使用できます。
