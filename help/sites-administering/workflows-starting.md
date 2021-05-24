---
title: ワークフローの開始
seo-title: ワークフローの開始
description: AEM でワークフローを開始する方法について説明します。
seo-description: AEM でワークフローを開始する方法について説明します。
uuid: 0648d335-ecce-459d-95fd-3d4d76181b32
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: e9ab4796-a050-40de-b073-af7d33cff009
exl-id: 84a1964c-4121-4763-b946-9eee6093747d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '804'
ht-degree: 59%

---

# ワークフローの開始{#starting-workflows}

ワークフローを管理しているとき、ワークフローは様々な方法で開始できます。

* 手動：

   * [ワークフローモデル](#workflow-models)から。
   * [バッチ処理](#workflow-packages-for-batch-processing)用のワークフローパッケージを使用して。

* 自動：

   * [ランチャーを使用](#workflows-launchers)してノードの変更に応答して。

>[!NOTE]
>
>作成者はその他の方法も使用できます。詳しくは、次を参照してください。
>
>* [ページへのワークフローの適用](/help/sites-authoring/workflows-applying.md)
* [DAM アセットにワークフローを適用する方法](/help/assets/assets-workflow.md)
* [AEM フォーム](https://helpx.adobe.com/jp/aem-forms/6-2/aem-workflows-submit-process-form.html)
* [翻訳プロジェクト](/help/sites-administering/tc-manage.md)



## ワークフローモデル {#workflow-models}

ワークフローモデルコンソールにリストされている[モデルの 1 つに基づいて](/help/sites-administering/workflows.md#workflow-models-and-instances)ワークフローを開始できます。必須の情報はペイロードのみですが、タイトルやコメントも同様に追加できます。

## ワークフローランチャー {#workflows-launchers}

ワークフローランチャーはコンテンツリポジトリ内の変更を監視し、変更されたノードの場所とリソースの種類に応じて、ワークフローを起動します。

**Launcher**&#x200B;を使用すると、次の操作を実行できます。

* 特定のノードに対して既に起動されているワークフローを確認する。
* 特定のノードまたはノードの種類が変更されたときに起動するワークフローを選択する。
* 既存のワークフローとノード間の関係を削除する。

ランチャーは任意のノードに対して作成できます。ただし、特定のノードに変更した場合、ワークフローは起動されません。次のパス以下のノードに変更した場合、ワークフローは起動されません。

* `/var/workflow/instances`
* `/home/users`ブランチ内の任意の場所にあるワークフローインボックスノード
* `/tmp`
* `/var/audit`
* `/var/classes`
* `/var/eventing`
* `/var/linkchecker`
* `/var/mobile`
* `/var/statistics`

   * 例外：`/var/statistics/tracking` *do*&#x200B;の下のノードに変更を加えると、ワークフローが起動します。

標準インストールには、様々な定義が含まれています。それらの定義は、デジタル資産管理およびソーシャルコラボレーションのタスクに対して使用されます。

![wf-100](assets/wf-100.png)

## バッチ処理用のワークフローパッケージ {#workflow-packages-for-batch-processing}

ワークフローパッケージは、処理のペイロードとしてワークフローに渡すことができるパッケージで、複数のリソースを処理できます。

ワークフローパッケージの特徴は次のとおりです。

* 一連のリソース（ページ、アセットなど）へのリンクが含まれます。
* 作成日、パッケージの作成者、簡単な説明など、パッケージの情報が保持されます。
* 特別なページテンプレートを使用して定義されます。このようなページでは、ユーザーがパッケージのリソースを指定できます。
* 複数回使用できます。
* ワークフローインスタンスの実行中にユーザーが変更できます（リソースを追加または削除できます）。

## モデルコンソールからのワークフローの開始 {#starting-a-workflow-from-the-models-console}

1. **ツール**、**ワークフロー**、**モデル**&#x200B;を使用して、**モデル**&#x200B;コンソールに移動します。
1. （コンソールの表示に従って）ワークフローを選択します。必要に応じて、検索機能（左上）を使用することもできます。

   ![wf-103](assets/wf-103.png)

   >[!NOTE]
   **[一時的](/help/sites-developing/workflows.md#transient-workflows)**&#x200B;インジケーターは、ワークフローの履歴が保持されないワークフローを示します。

1. ツールバーの「**ワークフローを開始**」を選択します。
1. ワークフローを実行ダイアログが開き、次の内容を指定できます。

   * **ペイロード**

      ページ、ノード、アセット、パッケージなどのリソースを指定できます。

   * **タイトル**

      このインスタンスを識別するのに役立つタイトル（オプション）。

   * **コメント**

      このインスタンスの詳細を示すコメント（オプション）。
   ![wf-104](assets/wf-104.png)

## ランチャー設定の作成 {#creating-a-launcher-configuration}

1. **ツール**、**ワークフロー**、**ランチャー**&#x200B;の順に使用して、**ワークフローランチャー**&#x200B;コンソールに移動します。
1. 「**作成**」を選択し、「**ランチャーを追加**」を選択してダイアログを開きます。

   ![wf-105](assets/wf-105.png)

   * **イベントタイプ**

      ワークフローを起動するイベントタイプ：

      * 作成日
      * 変更済み
      * 削除
   * **ノードタイプ**

      ワークフローランチャーが適用されるノードのタイプ。

   * **パス**

      ワークフローランチャーを適用するパス。

   * **実行モード**

      ワークフローランチャーが適用されるサーバーの種類。 **オーサー**、**パブリッシュ**、または&#x200B;**オーサーとパブリッシュ**&#x200B;を選択します。

   * **条件**

      評価時に、ワークフローが起動するかどうかを決定するノード値の条件のリスト。 例えば、次の条件では、ノードの 1 つのプロパティ名に「ユーザー」という値が含まれる場合、ワークフローが起動されます。

      name==User

   * **特長**

      有効にする機能のリスト。 ドロップダウンセレクターを使用して、必要な機能を選択します。

   * **無効にされた機能**

   無効にする機能のリスト。 ドロップダウンセレクターを使用して、必要な機能を選択します。

   * **ワークフローモデル**

      「Event Type」が、定義された「Condition」の下の「Nodetype」や「Path」で発生した場合に起動するワークフロー。

   * **説明**

      ランチャー設定を説明し、識別するための独自のテキスト。

   * **アクティベート**

      ワークフローランチャーをアクティブ化するかどうかを制御します。

      * 設定プロパティが満たされた場合にワークフローを起動するには、「**有効にする**」を選択します。
      * （設定プロパティが満たされた場合でも）ワークフローを実行しないときは、「**無効にする**」を選択します。
   * **リストを除外**

      ワークフローをトリガーするかどうかを決定する際に除外する（無視する）JCRイベントを指定します。

      このランチャープロパティは、項目のコンマ区切りリストです。&quot;

      * `property-name` 指定したプ `jcr` ロパティ名でトリガーされたイベントを無視します。&quot;
      * `event-user-data:<*someValue*>` は、 `*<someValue*`API `user-data` (https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/observation/ObservationManager.html#setUserData(java.lang.String)で設定された [ `ObservationManager` >]を含むイベントを無視します。

      次に例を示します。

      `jcr:lastModified,dc:modified,dc:format,jcr:lastModifiedBy,imageMap,event-user-data:changedByWorkflowProcess`

      この機能を使用して、除外する項目を追加することで、別のワークフロープロセスによってトリガーされた変更を無視できます。

      `event-user-data:changedByWorkflowProcess`





1. 「**作成**」を選択してランチャーを作成し、コンソールに戻ります。

   該当するイベントが発生すると、ランチャーが実行されてワークフローが開始します。

## ランチャー設定の管理  {#managing-a-launcher-configuration}

ランチャー設定を作成したら、同じコンソールを使用してインスタンスを選択し、「**プロパティを表示**」（および編集）または「**削除**」を使用できます。
