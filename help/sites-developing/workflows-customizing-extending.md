---
title: ワークフロー機能の拡張
seo-title: Extending Workflow Functionality
description: ワークフロー機能の拡張
seo-description: null
uuid: 9f4ea2a8-8b21-4e7c-ac73-dd37d9ada111
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: f23408c3-6b37-4047-9cce-0cab97bb6c5c
exl-id: 9e205912-50a6-414a-b8d4-a0865269d0e0
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '3584'
ht-degree: 70%

---

# ワークフロー機能の拡張{#extending-workflow-functionality}

このトピックでは、ワークフローのカスタムステップコンポーネントを開発し、プログラムによるワークフローとのやり取りの方法について説明します。

カスタムワークフローステップの作成には、次のアクティビティが含まれます。

* ワークフローステップコンポーネントを開発します。
* ステップ機能を OSGi サービスまたは ECMA スクリプトとして実装します。

また、 [プログラムとスクリプトからワークフローを操作する](/help/sites-developing/workflows-program-interaction.md).

## ワークフローステップのコンポーネント — 基本 {#workflow-step-components-the-basics}

ワークフローステップコンポーネントは、ワークフローモデルを作成する際のステップの外観と動作を定義します。

* ワークフローのサイドキックのカテゴリとステップの名前。
* ワークフローモデルでのステップの外観。
* コンポーネントのプロパティを設定するための編集ダイアログ。
* 実行時に実行されるサービスまたはスクリプト。

[すべてのコンポーネント](/help/sites-developing/components.md)と同様、ワークフローステップコンポーネントは、`sling:resourceSuperType` プロパティに指定されたコンポーネントから継承します。次の図は、すべてのワークフローステップコンポーネントの基礎を形成する `cq:component` ノードの階層を示しています。この図には、**プロセスステップ**、**参加者ステップ**&#x200B;および&#x200B;**動的参加者ステップ**&#x200B;コンポーネントも含まれています。これらのコンポーネントは、カスタムステップコンポーネント作成の最も一般的で基本的な出発点になります。

![aem_wf_componentinherit](assets/aem_wf_componentinherit.png)

>[!CAUTION]
>
>`/libs` パス内の設定は&#x200B;***一切***&#x200B;変更しないでください。
>
>`/libs` コンテンツは、インスタンスを次回アップグレードするとき（場合によってはホットフィックスまたは機能パックを適用したとき）に上書きされるからです。
>
>設定およびその他の変更に推奨される方法は次のとおりです。
>
>1. 必要な項目（例：`/libs` にある項目）を、`/apps` の下で再作成します
>2. `/apps` 内で必要な変更を加えます

`/libs/cq/workflow/components/model/step` コンポーネントは、**プロセスステップ**、**参加者ステップ**&#x200B;および&#x200B;**動的参加者ステップ**&#x200B;の各コンポーネントの最も近い共通の上位です。これらのコンポーネントはすべて、次の項目を継承します。

* `step.jsp`

  `step.jsp` スクリプトは、ステップコンポーネントがモデルに追加されると、そのタイトルをレンダリングします。

  ![wf-22-1](assets/wf-22-1.png)

* [cq:dialog](/help/sites-developing/developing-components.md#creating-and-configuring-a-dialog)

  次のタブを持つダイアログ

   * **共通**:（タイトルと説明の編集用）
   * **詳細**:電子メール通知プロパティを編集する場合。

  ![wf-44](assets/wf-44.png) ![wf-45](assets/wf-45.png)

  >[!NOTE]
  >
  >ステップコンポーネントの編集ダイアログのタブがこのデフォルトの外観と一致しない場合、ステップコンポーネントには、これらの継承されたタブをオーバーライドするスクリプト、ノードプロパティまたはダイアログタブが定義されています。

### ECMA スクリプト {#ecma-scripts}

次のオブジェクトは（ステップタイプに応じて）ECMA スクリプト内で使用できます。

* [WorkItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/exec/WorkItem.html) workItem
* [WorkflowSession](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/WorkflowSession.html) workflowSession
* [WorkflowData](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/exec/WorkflowData.html) workflowData
* `args`：プロセスの引数を格納する配列

* `sling`：他の OSGi サービスへのアクセス用
* `jcrSession`

### MetaDataMaps {#metadatamaps}

ワークフローメタデータを使用して、ワークフローの有効期間中に必要な情報を保持できます。 ワークフローステップの一般的な要件は、そのワークフローで以降に使用するデータを保持したり、保持されているデータを取得することです。

MetaDataMap オブジェクトには、`Workflow` オブジェクト、`WorkflowData` オブジェクトおよび `WorkItem` オブジェクトの 3 タイプがあります。いずれも、メタデータを保存するという同じ目的があります。

WorkItem には、作業項目（例えば、step）の実行中にのみ使用できる独自の MetaDataMap があります。

`Workflow` MetaDataMap と `WorkflowData` MetaDataMap は両方とも、ワークフロー全体で共有されます。このような場合は、`WorkflowData` MetaDataMap のみを使用することをお勧めします。

## カスタムワークフローステップコンポーネントの作成 {#creating-custom-workflow-step-components}

ワークフローステップのコンポーネントは、 [他のどの要素と同じ方法で作成される](/help/sites-developing/components.md).

（既存の）ベースステップコンポーネントのいずれかから継承するには、次のプロパティを `cq:Component` ノードに追加します。

* 名前：`sling:resourceSuperType`
* 型：`String`
* 値：ベースコンポーネントに解決される次のパスのいずれか

   * `cq/workflow/components/model/process`
   * `cq/workflow/components/model/participant`
   * `cq/workflow/components/model/dynamic_participant`

### ステップインスタンスのデフォルトのタイトルおよび説明の指定 {#specifying-the-default-title-and-description-for-step-instances}

次の手順を使用して、 **タイトル** および **説明** フィールド **共通** タブをクリックします。

>[!NOTE]
>
>次の要件の両方が満たされた場合に、ステップインスタンスにフィールド値が表示されます。
>
>* ステップの編集ダイアログでは、次の場所にタイトルと説明が保存されます。>
>* `./jcr:title`
>* `./jcr:description` の場所
>
>  この要件が満たされるのは、ステップの編集ダイアログが、`/libs/cq/flow/components/step/step` コンポーネントが実装する「共通」タブを使用しているときです。
>
>* ステップコンポーネントまたはそのコンポーネントの上位が、`/libs/cq/flow/components/step/step` コンポーネントが実装する `step.jsp` スクリプトをオーバーライドしていない。

1. `cq:Component` ノードの下に、次のノードを追加します。

   * 名前：`cq:editConfig`
   * 型：`cq:EditConfig`

   >[!NOTE]
   >
   >cq:editConfig ノードについて詳しくは、[コンポーネントの編集動作の設定](/help/sites-developing/developing-components.md#configuring-the-edit-behavior)を参照してください。

1. `cq:EditConfig` ノードの下に、次のノードを追加します。

   * 名前：`cq:formParameters`
   * 型：`nt:unstructured`

1. 次の名前の `String` プロパティを `cq:formParameters` ノードに追加します。

   * `jcr:title`：この値が「**共通**」タブの「**タイトル**」フィールドに設定されます。
   * `jcr:description`：この値が「**共通**」タブの「**説明**」フィールドに設定されます。

### ワークフローメタデータにプロパティ値を保存中 {#saving-property-values-in-workflow-metadata}

>[!NOTE]
>
>詳しくは、 [データの保持とアクセス](#persisting-and-accessing-data). 特に、実行時のプロパティ値へのアクセスについて詳しくは、 [実行時のダイアログプロパティ値へのアクセス](#accessing-dialog-property-values-at-runtime).

`cq:Widget` 項目の name プロパティで、ウィジェットの値を保存する JCR ノードを指定します。ワークフローステップコンポーネントのダイアログ内のウィジェットが `./metaData` ノードに値を保存すると、ワークフロー `MetaDataMap` に値が追加されます。

例えば、ダイアログのテキストフィールドは、次のプロパティを持つ `cq:Widget` ノードです。

| 名前 | タイプ | 値 |
|---|---|---|
| `xtype` | `String` | `textarea` |
| `name` | `String` | `./metaData/subject` |
| `fieldLabel` | `String` | `Email Subject` |

このテキストフィールドに指定された値がワークフローインスタンスの ` [MetaDataMap](#metadatamaps)` オブジェクトに追加され、`subject` キーに関連付けられます。

>[!NOTE]
>
>キーが `PROCESS_ARGS` の場合、この値は `args` 変数を使用して ECMA スクリプト実装ですぐに使用できます。この場合、name プロパティの値は `./metaData/PROCESS_ARGS.`

### ステップ実装のオーバーライド {#overriding-the-step-implementation}

ワークフローモデルの開発者は、デザイン時に、ベースステップコンポーネントごとに次の主要機能を設定できます。

* プロセスステップ：実行時に実行されるサービスまたは ECMA スクリプト。
* 参加者ステップ：生成された作業項目を割り当てるユーザーの ID。
* 動的参加者ステップ：作業項目を割り当てるユーザーの ID を選択するサービスまたは ECMA スクリプト。

特定のワークフローシナリオで使用するコンポーネントに焦点を当てるには、デザインで主要な機能を設定し、モデル開発者が変更する機能を削除します。

1. cq:component ノードの下に、次のノードを追加します。

   * 名前：`cq:editConfig`
   * 型：`cq:EditConfig`

   cq:editConfig ノードについて詳しくは、 [コンポーネントの編集動作の設定](/help/sites-developing/developing-components.md#configuring-the-edit-behavior).

1. cq:EditConfig ノードの下に、次のノードを追加します。

   * 名前：`cq:formParameters`
   * 型：`nt:unstructured`

1. `String` プロパティを `cq:formParameters` ノードに追加します。コンポーネントのスーパータイプによって、プロパティの名前が次のように決定されます。

   * プロセスステップ：`PROCESS`
   * 参加者ステップ：`PARTICIPANT`
   * 動的参加者ステップ: `DYNAMIC_PARTICIPANT`

1. プロパティの値を次のように指定します。

   * `PROCESS`：ステップの動作を実装する ECMA スクリプトへのパスまたはサービスの PID。
   * `PARTICIPANT`：作業項目を割り当てられたユーザーの ID。
   * `DYNAMIC_PARTICIPANT`：作業項目を割り当てるユーザーを選択する ECMA スクリプトへのパスまたはサービスの PID。

1. モデル開発者がプロパティ値を変更できないようにするために、コンポーネントのスーパータイプのダイアログをオーバーライドします。

### フォームとダイアログを参加者ステップに追加 {#adding-forms-and-dialogs-to-participant-steps}

参加者ステップコンポーネントをカスタマイズして、次に示す[フォーム参加者ステップ](/help/sites-developing/workflows-step-ref.md#form-participant-step)コンポーネントと[ダイアログ参加者ステップ](/help/sites-developing/workflows-step-ref.md#dialog-participant-step)コンポーネントの機能を提供するようにします。

* 生成された作業項目を開いたときに、フォームを表示する
* 生成された作業項目を完了したときに、カスタムダイアログを表示する

新しいコンポーネントに対して、以下の手順を実行します（[カスタムワークフローステップコンポーネントの作成](#creating-custom-workflow-step-components)を参照）。

1. `cq:Component` ノードの下に、次のノードを追加します。

   * 名前：`cq:editConfig`
   * 型：`cq:EditConfig`

   cq:editConfig ノードについて詳しくは、[コンポーネントの編集動作の設定](/help/sites-developing/components-basics.md#edit-behavior)を参照してください。

1. cq:EditConfig ノードの下に、次のノードを追加します。

   * 名前：`cq:formParameters`
   * 型：`nt:unstructured`

1. 作業項目を開くとフォームが表示されるようにするには、次のプロパティを `cq:formParameters` ノードに追加します。

   * 名前：`FORM_PATH`
   * 型：`String`
   * 値：フォームに解決されるパス

1. 作業項目を完了するとカスタムダイアログが表示されるようにするには、次のプロパティを `cq:formParameters` ノードに追加します。

   * 名前：`DIALOG_PATH`
   * 型：`String`
   * 値：ダイアログに解決されるパス

### ワークフローステップのランタイム動作の設定 {#configuring-the-workflow-step-runtime-behavior}

`cq:Component` ノードの下に、`cq:EditConfig` ノードを追加します。その下に、`nt:unstructured` ノードを（必ず `cq:formParameters` という名前で）追加し、そのノードに次のプロパティを追加してください。

* 名前：`PROCESS_AUTO_ADVANCE`

   * 型：`Boolean`
   * 値：

      * `true` に設定した場合、ワークフローはそのステップを実行して続行します。これはデフォルト値であり、推奨もされています。
      * `false` に設定した場合、ワークフローはそのステップを実行して停止します。これには追加の処理が必要なので、`true` に設定することをお勧めします。

* 名前：`DO_NOTIFY`

   * 型：`Boolean`
   * 値：ユーザー参加手順に関して電子メール通知を送信する必要があるかどうかを示します（また、メールサーバーが正しく設定されていると仮定）。

## データの保持とアクセス {#persisting-and-accessing-data}

### 後続のワークフローステップのデータを保持する {#persisting-data-for-subsequent-workflow-steps}

ワークフローメタデータを使用して、ワークフローの有効期間中およびステップの間に必要な情報を保持できます。 ワークフローステップの一般的な要件は、将来の使用のためにデータを保持するか、以前の手順から永続化されたデータを取得することです。

ワークフローメタデータは、[`MetaDataMap`](#metadatamaps) オブジェクトに保存されます。Java API が提供する [`Workflow.getWorkflowData`](https://helpx.adobe.com/jp/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/Workflow.html) メソッドは、適切な `MetaDataMap` オブジェクトを提供する [`WorkflowData`](https://helpx.adobe.com/jp/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/WorkflowData.html) オブジェクトを返します。この `WorkflowData` `MetaDataMap` オブジェクトは、ステップコンポーネントの OSGi サービスまたは ECMA スクリプトで使用できます。

#### Java {#java}

`WorkflowProcess` 実装の実行メソッドは、`WorkItem` オブジェクトに渡されます。このオブジェクトを使用して、現在のワークフローインスタンスの `WorkflowData` オブジェクトを取得します。次の例では、ワークフローの `MetaDataMap` オブジェクトに項目を追加してから、各項目を記録しています。(「mykey」、「My Step Value」) 項目は、ワークフローの後続のステップで使用できます。

```java
public void execute(WorkItem item, WorkflowSession session, MetaDataMap args) throws WorkflowException {

    MetaDataMap wfd = item.getWorkflow().getWorkflowData().getMetaDataMap();

    wfd.put("mykey", "My Step Value");

    Set<String> keyset = wfd.keySet();
    Iterator<String> i = keyset.iterator();
    while (i.hasNext()){
     Object key = i.next();
     log.info("The workflow medata includes key {} and value {}",key.toString(),wfd.get(key).toString());
    }
}
```

#### ECMA スクリプト {#ecma-script}

`graniteWorkItem` 変数は、現在の `WorkItem` Java オブジェクトの ECMA スクリプト表現です。したがって、`graniteWorkItem` 変数を使用して、ワークフローメタデータを取得できます。次の ECMA スクリプトを使用すると、ワークフローの `MetaDataMap` オブジェクトに項目を追加してから各項目を記録する&#x200B;**プロセスステップ**&#x200B;を実装できます。その後、これらの項目は、ワークフローの後続ステップで使用可能です。

>[!NOTE]
>
>ステップスクリプトですぐ使用できる `metaData` 変数は、ステップのメタデータです。ステップのメタデータは、ワークフローのメタデータとは異なります。

```
var currentDateInMillis = new Date().getTime();

graniteWorkItem.getWorkflowData().getMetaDataMap().put("hardcodedKey","theKey");

graniteWorkItem.getWorkflowData().getMetaDataMap().put("currentDateInMillisKey",currentDateInMillis);

var iterator = graniteWorkItem.getWorkflowData().getMetaDataMap().keySet().iterator();
while (iterator.hasNext()){
    var key = iterator.next();
    log.info("Workflow metadata key, value = " + key.toString() + ", " + graniteWorkItem.getWorkflowData().getMetaDataMap().get(key));
}
```

### 実行時のダイアログプロパティ値へのアクセス {#accessing-dialog-property-values-at-runtime}

ワークフローインスタンスの `MetaDataMap` オブジェクトは、ワークフローの有効期間全体を通したデータの保存と取得に役立ちます。ワークフローステップコンポーネントの実装では、特に実行時のコンポーネントプロパティ値を取得するときに `MetaDataMap` が役立ちます。

>[!NOTE]
>
>プロパティをワークフローメタデータとして保存するコンポーネントダイアログの設定については、[ワークフローメタデータへのプロパティ値の保存](#saving-property-values-in-workflow-metadata)を参照してください。

ワークフローの `MetaDataMap` は、Java および ECMA スクリプトプロセス実装で次のように使用できます。

* WorkflowProcess インターフェイスの Java 実装では、`args` パラメーターがワークフローの `MetaDataMap` オブジェクトです。

* ECMA スクリプト実装では、`args` 変数と `metadata` 変数を使用して値を利用できます。

### 例：プロセスステップコンポーネントの引数の取得 {#example-retrieving-the-arguments-of-the-process-step-component}

**プロセスステップ**&#x200B;コンポーネントの編集ダイアログには、**Arguments** プロパティが含まれます。 **引数** プロパティの値はワークフローメタデータに保存され、`PROCESS_ARGS` キーと関連付けられます。

次の図では、**引数**&#x200B;プロパティの値は `argument1, argument2` です。

![wf-24](assets/wf-24.png)

#### Java {#java-1}

次の Java コードは、`WorkflowProcess` 実装の `execute` メソッドです。このメソッドは、`PROCESS_ARGS` キーと関連付けられている `args` `MetaDataMap` に値を記録します。

```java
public void execute(WorkItem item, WorkflowSession session, MetaDataMap args) throws WorkflowException {
     if (args.containsKey("PROCESS_ARGS")){
      log.info("workflow metadata for key PROCESS_ARGS and value {}",args.get("PROCESS_ARGS","string").toString());
     }
    }
```

この Java 実装を使用するプロセスステップが実行されると、ログには次のエントリが含まれます。

```xml
16.02.2018 12:07:39.566 *INFO* [JobHandler: /var/workflow/instances/server0/2018-02-16/model_855140139900189:/content/we-retail/de] com.adobe.example.workflow.impl.process.LogArguments workflow metadata for key PROCESS_ARGS and value argument1, argument2
```

#### ECMA スクリプト {#ecma-script-1}

次の ECMA スクリプトは、 **処理ステップ**. 引数の数と引数の値が記録されます。

```
var iterator = graniteWorkItem.getWorkflowData().getMetaDataMap().keySet().iterator();
while (iterator.hasNext()){
    var key = iterator.next();
    log.info("Workflow metadata key, value = " + key.toString() + ", " + graniteWorkItem.getWorkflowData().getMetaDataMap().get(key));
}
log.info("hardcodedKey "+ graniteWorkItem.getWorkflowData().getMetaDataMap().get("hardcodedKey"));
log.info("currentDateInMillisKey "+ graniteWorkItem.getWorkflowData().getMetaDataMap().get("currentDateInMillisKey"));
```

>[!NOTE]
>
>この節では、プロセスステップの引数を使用する方法について説明します。 この情報は、動的参加者選択にも適用されます。

>[!NOTE]
>ワークフローメタデータにコンポーネントのプロパティを保存するもう 1 つの例については、「例：ロガーワークフローステップの作成」を参照してください。この例では、メタデータ値を PROCESS_ARGS 以外のキーに関連付けるダイアログを使用します。

### スクリプトとプロセスの引数 {#scripts-and-process-arguments}

**プロセスステップ**&#x200B;コンポーネント用のスクリプト内で、引数は `args` オブジェクトを通して使用できます。

カスタムステップコンポーネントを作成するときには、スクリプト内で `metaData` オブジェクトを使用できます。このオブジェクトの使用は、単一の文字列引数に限定されます。

## プロセスステップの実装の開発 {#developing-process-step-implementations}

ワークフローのプロセス中にプロセスステップが開始されると、ステップは OSGi サービスにリクエストを送信するか、ECMA スクリプトを実行します。 ワークフローで必要なアクションを実行するサービスまたは ECMA スクリプトを開発します。

>[!NOTE]
>
>プロセスステップコンポーネントとサービスまたはスクリプトの関連付けについて詳しくは、 [処理ステップ](/help/sites-developing/workflows-step-ref.md#process-step) または [ステップ実装の上書き](#overriding-the-step-implementation).

### Java クラスを使用したプロセスステップの実装 {#implementing-a-process-step-with-a-java-class}

OSGi サービスコンポーネント（Java バンドル）としてプロセスステップを定義するには：

1. バンドルを作成し、OSGi コンテナにデプロイします。 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)、または [Eclipse](/help/sites-developing/howto-projects-eclipse.md) を使用したバンドルの作成に関するドキュメントを参照してください。

   >[!NOTE]
   >
   >OSGI コンポーネントでは、`WorkflowProcess` インターフェイスをその `execute()` メソッドを使用して実装する必要があります。以下のコード例を参照してください。

   >[!NOTE]
   >
   >パッケージ名は、`maven-bundle-plugin` 設定の `<*Private-Package*>` セクションに追加する必要があります。

1. SCR プロパティ`process.label`を追加し、必要な値を設定してください。これは、汎用の&#x200B;**プロセスステップ**&#x200B;コンポーネントを使用するときに、プロセスステップがリストされる名前になります。次の例を参照してください。
1. **モデル**&#x200B;エディターで、汎用の&#x200B;**プロセスステップ**&#x200B;コンポーネントを使用して、プロセスステップをワークフローに追加します。
1. （**プロセスステップ**&#x200B;の）編集ダイアログで、**プロセス**&#x200B;タブに移動してから、プロセスの実装を選択してください。
1. コード内で引数を使用する場合は、**プロセスの引数**&#x200B;を設定します。例：false。
1. ステップとワークフローモデルの両方に対する変更を保存します（モデルエディターの左上隅）。

Java メソッド（それぞれ実行可能な Java メソッドを実装するクラス）は、OSGi サービスとして登録され、実行時にいつでもメソッドを追加することができます。

次の OSGI コンポーネントは、ペイロードがページの場合、プロパティ`approved`をページコンテンツノードに追加します。

```java
package com.adobe.example.workflow.impl.process;

import com.adobe.granite.workflow.WorkflowException;
import com.adobe.granite.workflow.WorkflowSession;
import com.adobe.granite.workflow.exec.WorkItem;
import com.adobe.granite.workflow.exec.WorkflowData;
import com.adobe.granite.workflow.exec.WorkflowProcess;
import com.adobe.granite.workflow.metadata.MetaDataMap;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Service;

import org.osgi.framework.Constants;

import javax.jcr.Node;
import javax.jcr.RepositoryException;
import javax.jcr.Session;

/**
 * Sample workflow process that sets an <code>approve</code> property to the payload based on the process argument value.
 */
@Component
@Service
public class MyProcess implements WorkflowProcess {

 @Property(value = "An example workflow process implementation.")
 static final String DESCRIPTION = Constants.SERVICE_DESCRIPTION;
 @Property(value = "Adobe")
 static final String VENDOR = Constants.SERVICE_VENDOR;
 @Property(value = "My Sample Workflow Process")
 static final String LABEL="process.label";

 private static final String TYPE_JCR_PATH = "JCR_PATH";

 public void execute(WorkItem item, WorkflowSession session, MetaDataMap args) throws WorkflowException {
  WorkflowData workflowData = item.getWorkflowData();
  if (workflowData.getPayloadType().equals(TYPE_JCR_PATH)) {
   String path = workflowData.getPayload().toString() + "/jcr:content";
   try {
    Session jcrSession = session.adaptTo(Session.class);
    Node node = (Node) jcrSession.getItem(path);
    if (node != null) {
     node.setProperty("approved", readArgument(args));
     jcrSession.save();
    }
   } catch (RepositoryException e) {
    throw new WorkflowException(e.getMessage(), e);
   }
  }
 }

 private boolean readArgument(MetaDataMap args) {
  String argument = args.get("PROCESS_ARGS", "false");
  return argument.equalsIgnoreCase("true");
 }
}
```

>[!NOTE]
>
>プロセスが 3 回連続で失敗した場合、1 つの項目がワークフロー管理者のインボックスに配置されます。

### ECMAScript の使用 {#using-ecmascript}

ECMA スクリプトを使用すると、スクリプト開発者はプロセスステップを実装できます。 スクリプトは JCR リポジトリに配置され、そこから実行されます。

次の表に、ワークフロー Java API のオブジェクトへのアクセスを提供する、スクリプトを処理するためにすぐに使用できる変数を示します。

| Java クラス | スクリプト変数名 | 説明 |
|---|---|---|
| `com.adobe.granite.workflow.exec.WorkItem` | `graniteWorkItem` | 現在のステップインスタンス。 |
| `com.adobe.granite.workflow.WorkflowSession` | `graniteWorkflowSession` | 現在のステップインスタンスのワークフローセッション。 |
| `String[]`（プロセス引数を含む） | `args` | ステップの引数。 |
| `com.adobe.granite.workflow.metadata.MetaDataMap` | `metaData` | 現在のステップインスタンスのメタデータ。 |
| `org.apache.sling.scripting.core.impl.InternalScriptHelper` | `sling` | Sling ランタイム環境へのアクセスを提供します。 |

次のサンプルスクリプトは、ワークフローペイロードを表す JCR ノードにアクセスする方法を示しています。 `graniteWorkflowSession`変数を JCR セッション変数に適応させます。この変数を使用して、ペイロードパスからノードを取得します。

```
var workflowData = graniteWorkItem.getWorkflowData();
if (workflowData.getPayloadType() == "JCR_PATH") {
    var path = workflowData.getPayload().toString();
    var jcrsession = graniteWorkflowSession.adaptTo(Packages.javax.jcr.Session);
    var node = jcrsession.getNode(path);
    if (node.hasProperty("approved")){
     node.setProperty("approved", args[0] == "true" ? true : false);
     node.save();
 }
}
```

次のスクリプトは、ペイロードが画像（`.png` ファイル）かどうかをチェックして、その画像から白黒の画像を作成し、兄弟ノードとして保存します。

```
var workflowData = graniteWorkItem.getWorkflowData();
if (workflowData.getPayloadType() == "JCR_PATH") {
    var path = workflowData.getPayload().toString();
    var jcrsession = graniteWorkflowSession.adaptTo(Packages.javax.jcr.Session);
    var node = jcrsession.getRootNode().getNode(path.substring(1));
     if (node.isNodeType("nt:file") && node.getProperty("jcr:content/jcr:mimeType").getString().indexOf("image/") == 0) {
        var is = node.getProperty("jcr:content/jcr:data").getStream();
        var layer = new Packages.com.day.image.Layer(is);
        layer.grayscale();
                var parent = node.getParent();
                var gn = parent.addNode("grey" + node.getName(), "nt:file");
        var content = gn.addNode("jcr:content", "nt:resource");
                content.setProperty("jcr:mimeType","image/png");
                var cal = Packages.java.util.Calendar.getInstance();
                content.setProperty("jcr:lastModified",cal);
                var f = Packages.java.io.File.createTempFile("test",".png");
        var tout = new Packages.java.io.FileOutputStream(f);
        layer.write("image/png", 1.0, tout);
        var fis = new Packages.java.io.FileInputStream(f);
                content.setProperty("jcr:data", fis);
                parent.save();
        tout.close();
        fis.close();
        is.close();
        f.deleteOnExit();
    }
}
```

スクリプトを使用するには：

1. （例えば、CRXDE Lite で）スクリプトを作成して、リポジトリ内の`//apps/workflow/scripts/`の下に保存します。
1. **プロセスステップ**&#x200B;の編集ダイアログでスクリプトを識別するタイトルを指定するには、次のプロパティをスクリプトの `jcr:content`ノードに追加します。

   | 名前 | タイプ | 値 |
   |---|---|---|
   | `jcr:mixinTypes` | `Name[]` | `mix:title` |
   | `jcr:title` | `String` | 編集ダイアログに表示される名前。 |

1. を編集します。 **処理ステップ** インスタンスを作成し、使用するスクリプトを指定します。

## 参加者選択の開発 {#developing-participant-choosers}

の参加者選択を作成できます。 **動的参加者ステップ** コンポーネント。

ワークフローの途中で&#x200B;**動的参加者ステップ**&#x200B;が開始されると、生成された作業項目を割り当てることのできる参加者をステップが判断する必要があります。そのためには、ステップで次のいずれかを実行します。

* OSGi サービスにリクエストを送信
* ECMA スクリプトを実行して参加者を選択します

ワークフローの要件に従って参加者を選択するサービスまたは ECMA スクリプトを作成できます。

>[!NOTE]
>
>を **動的参加者ステップ** サービスまたはスクリプトを含むコンポーネントについては、 [動的参加者ステップ](/help/sites-developing/workflows-step-ref.md#dynamic-participant-step) または [ステップ実装の上書き](#persisting-and-accessing-data).

### Java クラスを使用した参加者選択の開発 {#developing-a-participant-chooser-using-a-java-class}

参加者ステップを OSGI サービスコンポーネント（Java クラス）として定義するには：

1. OSGI コンポーネントは、`getParticipant()` メソッドを使用して `ParticipantStepChooser` インターフェースを実装する必要があります。以下のコード例を参照してください。

   バンドルを作成し、OSGi コンテナにデプロイします。

1. SCR プロパティ`chooser.label`を追加し、必要に応じて値を設定します。これは、**動的参加者ステップ**&#x200B;コンポーネントを使用して、参加者選択に列挙される名前となります。次に例を示します。

   ```java
   package com.adobe.example.workflow.impl.process;
   
   import com.adobe.granite.workflow.WorkflowException;
   import com.adobe.granite.workflow.WorkflowSession;
   import com.adobe.granite.workflow.exec.ParticipantStepChooser;
   import com.adobe.granite.workflow.exec.WorkItem;
   import com.adobe.granite.workflow.exec.WorkflowData;
   import com.adobe.granite.workflow.metadata.MetaDataMap;
   
   import org.apache.felix.scr.annotations.Component;
   import org.apache.felix.scr.annotations.Property;
   import org.apache.felix.scr.annotations.Service;
   
   import org.osgi.framework.Constants;
   
   /**
    * Sample dynamic participant step that determines the participant based on a path given as argument.
    */
   @Component
   @Service
   
   public class MyDynamicParticipant implements ParticipantStepChooser {
   
    @Property(value = "An example implementation of a dynamic participant chooser.")
    static final String DESCRIPTION = Constants.SERVICE_DESCRIPTION;
       @Property(value = "Adobe")
       static final String VENDOR = Constants.SERVICE_VENDOR;
       @Property(value = "Dynamic Participant Chooser Process")
       static final String LABEL=ParticipantStepChooser.SERVICE_PROPERTY_LABEL;
   
       private static final String TYPE_JCR_PATH = "JCR_PATH";
   
       public String getParticipant(WorkItem workItem, WorkflowSession workflowSession, MetaDataMap args) throws WorkflowException {
           WorkflowData workflowData = workItem.getWorkflowData();
           if (workflowData.getPayloadType().equals(TYPE_JCR_PATH)) {
               String path = workflowData.getPayload().toString();
               String pathFromArgument = args.get("PROCESS_ARGS", String.class);
               if (pathFromArgument != null && path.startsWith(pathFromArgument)) {
                   return "admin";
               }
           }
           return "administrators";
       }
   }
   ```

1. **モデル**&#x200B;エディターで、汎用の&#x200B;**動的参加者ステップ**&#x200B;コンポーネントを使用して、動的参加者ステップをワークフローに追加します。
1. 編集ダイアログで、**参加者選択**&#x200B;タブを選択してから、選択の実装を選択してください。
1. コード内で引数を使用する場合は、**プロセスの引数**&#x200B;を設定します。この例の場合は `/content/we-retail/de` です。
1. ステップとワークフローモデルの両方の変更を保存します。

### ECMA スクリプトを使用した参加者選択の開発 {#developing-a-participant-chooser-using-an-ecma-script}

ECMA スクリプトを作成して、 **参加者ステップ** が生成されました。 スクリプトには、`getParticipant`という関数を含める必要があります。この関数は引数が不要で、ユーザーまたはグループの ID を格納した`String`を返します。

スクリプトは JCR リポジトリに配置され、そこから実行されます。

次の表に、スクリプト内のワークフロー Java オブジェクトに即座にアクセスできる変数を示します。

| Java クラス | スクリプト変数名 |
|---|---|
| `com.adobe.granite.workflow.exec.WorkItem` | `graniteWorkItem` |
| `com.adobe.granite.workflow.WorkflowSession` | `graniteWorkflowSession` |
| `String[]`（プロセスの引数を格納） | `args` |
| `com.adobe.granite.workflow.metadata.MetaDataMap` | `metaData` |
| `org.apache.sling.scripting.core.impl.InternalScriptHelper` | `sling` |

```
function getParticipant() {
    var workflowData = graniteWorkItem.getWorkflowData();
    if (workflowData.getPayloadType() == "JCR_PATH") {
        var path = workflowData.getPayload().toString();
        if (path.indexOf("/content/we-retail/de") == 0) {
            return "admin";
        } else {
            return "administrators";
        }
    }
}
```

1. （例えば、CRXDE Lite で）スクリプトを作成して、リポジトリ内の `//apps/workflow/scripts` の下に保存します。
1. **プロセスステップ**&#x200B;の編集ダイアログでスクリプトを識別するタイトルを指定するには、次のプロパティをスクリプトの `jcr:content`ノードに追加します。

   | 名前 | タイプ | 値 |
   |---|---|---|
   | `jcr:mixinTypes` | `Name[]` | `mix:title` |
   | `jcr:title` | `String` | 編集ダイアログに表示される名前。 |

1. [動的参加者ステップ](/help/sites-developing/workflows-step-ref.md#dynamic-participant-step)インスタンスを編集し、使用するスクリプトを指定してください。

## ワークフローパッケージの処理 {#handling-workflow-packages}

[ワークフローパッケージ](/help/sites-authoring/workflows-applying.md#specifying-workflow-details-in-the-create-workflow-wizard) をワークフローに渡して処理できます。 ワークフローパッケージには、ページやアセットなどのリソースへの参照が含まれています。

>[!NOTE]
>
>次のワークフロープロセスステップは、一括ページアクティベーション用のワークフローパッケージを受け入れます。
>
>* [`com.day.cq.wcm.workflow.process.ActivatePageProcess`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/workflow/process/ActivatePageProcess.html)
>* [`com.day.cq.wcm.workflow.process.DeactivatePageProcess`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/workflow/process/DeactivatePageProcess.html)
>

パッケージリソースを取得して処理するワークフローステップを作成できます。`com.day.cq.workflow.collection`パッケージの以下の構成要素は、ワークフローパッケージへのアクセスを可能にします。

* `ResourceCollection`：ワークフローパッケージクラスです。
* `ResourceCollectionUtil`：ResourceCollection オブジェクトの取得に使用されます。
* `ResourceCollectionManager`：コレクションを作成および取得します。実装は、OSGi サービスとしてデプロイされます。

次の Java クラスの例は、パッケージリソースの取得方法を示しています。

```java
package com.adobe.example;

import java.util.ArrayList;
import java.util.List;

import com.day.cq.workflow.WorkflowException;
import com.day.cq.workflow.WorkflowSession;
import com.day.cq.workflow.collection.ResourceCollection;
import com.day.cq.workflow.collection.ResourceCollectionManager;
import com.day.cq.workflow.collection.ResourceCollectionUtil;
import com.day.cq.workflow.exec.WorkItem;
import com.day.cq.workflow.exec.WorkflowData;
import com.day.cq.workflow.exec.WorkflowProcess;
import com.day.cq.workflow.metadata.MetaDataMap;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Service;
import org.apache.felix.scr.annotations.Reference;
import org.osgi.framework.Constants;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import javax.jcr.Node;
import javax.jcr.PathNotFoundException;
import javax.jcr.RepositoryException;
import javax.jcr.Session;

@Component
@Service
public class LaunchBulkActivate implements WorkflowProcess {

 private static final Logger log = LoggerFactory.getLogger(LaunchBulkActivate.class);

 @Property(value="Bulk Activate for Launches")
  static final String PROCESS_NAME ="process.label";
 @Property(value="A sample workflow process step to support Launches bulk activation of pages")
 static final String SERVICE_DESCRIPTION = Constants.SERVICE_DESCRIPTION;

 @Reference
 private ResourceCollectionManager rcManager;
public void execute(WorkItem workItem, WorkflowSession workflowSession) throws Exception {
    Session session = workflowSession.getSession();
    WorkflowData data = workItem.getWorkflowData();
    String path = null;
    String type = data.getPayloadType();
    if (type.equals(TYPE_JCR_PATH) && data.getPayload() != null) {
        String payloadData = (String) data.getPayload();
        if (session.itemExists(payloadData)) {
            path = payloadData;
        }
    } else if (data.getPayload() != null && type.equals(TYPE_JCR_UUID)) {
        Node node = session.getNodeByUUID((String) data.getPayload());
        path = node.getPath();
    }

    // CUSTOMIZED CODE IF REQUIRED....

    if (path != null) {
        // check for resource collection
        ResourceCollection rcCollection = ResourceCollectionUtil.getResourceCollection((Node)session.getItem(path), rcManager);
        // get list of paths to replicate (no resource collection: size == 1
        // otherwise size >= 1
        List<String> paths = getPaths(path, rcCollection);
        for (String aPath: paths) {

            // CUSTOMIZED CODE....

        }
    } else {
        log.warn("Cannot process because path is null for this " + "workitem: " + workItem.toString());
    }
}

/**
 * helper
 */
private List<String> getPaths(String path, ResourceCollection rcCollection) {
    List<String> paths = new ArrayList<String>();
    if (rcCollection == null) {
        paths.add(path);
    } else {
        log.debug("ResourceCollection detected " + rcCollection.getPath());
        // this is a resource collection. the collection itself is not
        // replicated. only its members
        try {
            List<Node> members = rcCollection.list(new String[]{"cq:Page", "dam:Asset"});
            for (Node member: members) {
                String mPath = member.getPath();
                paths.add(mPath);
            }
        } catch(RepositoryException re) {
            log.error("Cannot build path list out of the resource collection " + rcCollection.getPath());
        }
    }
    return paths;
}
}
```

## 例：カスタムステップの作成 {#example-creating-a-custom-step}

独自のカスタムステップの作成を簡単に開始するには、次の場所から既存のステップをコピーします。

`/libs/cq/workflow/components/model`

### 基本ステップの作成 {#creating-the-basic-step}

1. /apps の下にパスを再作成します。例：

   `/apps/cq/workflow/components/model`

   新しいフォルダーのタイプは `nt:folder` です。

   ```xml
   - apps
     - cq
       - workflow (nt:folder)
         - components (nt:folder)
           - model (nt:folder)
   ```

   >[!NOTE]
   >
   >この手順は、クラシック UI モデルエディターには適用されません。

1. 次に、コピーした手順を/apps フォルダーに配置します。例：

   `/apps/cq/workflow/components/model/myCustomStep`

   この結果、カスタマイズしたステップの例を示すと次のようになります。

   ![wf-34](assets/wf-34.png)

   >[!CAUTION]
   >
   >標準 UI ではカードに表示されるのはタイトルのみで、説明は表示されないので、クラシック UI エディター用の `details.jsp` は不要です。

1. このノードに次のプロパティを適用します。

   `/apps/cq/workflow/components/model/myCustomStep`

   **対象プロパティ：**

   * `sling:resourceSuperType`

     既存のステップから継承する必要があります。

      この例では、`cq/workflow/components/model/step` の基本ステップから継承していますが、`participant` や `process` などの他のスーパータイプも使用できます。

   * `jcr:title`

     コンポーネントがステップブラウザー（ワークフローモデルエディターの左側のパネル）に一覧表示されたときに表示されるタイトルです。

   * `cq:icon`

     ステップの [Coral アイコン](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html)を指定するために使用されます。

   * `componentGroup`

     次のいずれかを指定する必要があります。

      * コラボレーションワークフロー
      * DAM ワークフロー
      * Forms のワークフロー
      * プロジェクト
      * WCM ワークフロー
      * ワークフロー

   ![wf-35](assets/wf-35.png)

1. 以上でワークフローを開いて編集できるようになります。ステップブラウザーで、フィルターを適用して&#x200B;**カスタムステップ**&#x200B;を表示できます。

   ![wf-36](assets/wf-36.png)

   **カスタムステップ**&#x200B;をモデルにドラッグすると、カードが表示されます。

   ![wf-37](assets/wf-37.png)

   このステップで `cq:icon` が定義されていない場合は、タイトルの最初の 2 文字を使用したデフォルトのアイコンが表示されます。次に例を示します。

   ![wf-38](assets/wf-38.png)

#### ステップ設定ダイアログの定義 {#defining-the-step-configure-dialog}

後 [基本ステップの作成](#creating-the-basic-step)、ステップの定義 **設定** ダイアログの内容は次のとおりです。

1. ノード`cq:editConfig`のプロパティを次のように設定します。

   **対象プロパティ：**

   * `cq:inherit`

     `true`に設定すると、ステップコンポーネントは`sling:resourceSuperType`で指定したステップのプロパティを継承します。

   * `cq:disableTargeting`

      必要に応じて設定します。

   ![wf-39](assets/wf-39.png)

1. ノード`cq:formsParameter`のプロパティを次のように設定します。

   **対象プロパティ：**

   * `jcr:title`

     モデルマップのステップカードと、**カスタム - ステップのプロパティ**&#x200B;設定ダイアログの&#x200B;**タイトル**&#x200B;フィールドに、デフォルトのタイトルを設定します。

   * 独自のカスタムプロパティも定義できます。

   ![wf-40](assets/wf-40.png)

1. ノード`cq:listeners`のプロパティを設定します。

   `cq:listener` ノードとそのプロパティを利用すると、ステップをモデルページにドラッグしたり、ステップのプロパティを編集したりして、タッチ操作対応 UI のモデルエディターでイベントに対処するイベントハンドラーを設定できます。

   **対象プロパティ：**

   * `afterMove: REFRESH_PAGE`
   * `afterdelete: CQ.workflow.flow.Step.afterDelete`
   * `afteredit: CQ.workflow.flow.Step.afterEdit`
   * `afterinsert: CQ.workflow.flow.Step.afterInsert`

   この設定は、エディターを適切に機能させるために必要です。 ほとんどの場合、この設定は変更しないでください。

   ただし、`cq:inherit` を true に設定（上記のように `cq:editConfig` ノードで設定）するとこの設定を継承できるので、ステップの定義に明示的に含める必要はありません。継承されない場合は、次のプロパティと値を指定したこのノードを追加する必要があります。

   この例では継承が有効になっているので、`cq:listeners`ノードを削除できます。削除しても、ステップは正常に機能します。

   ![wf-41](assets/wf-41.png)

1. これで、ステップのインスタンスをワークフローモデルに追加できます。ステップを&#x200B;**設定**&#x200B;する際は、次のダイアログが表示されます。

   ![wf-42](assets/wf-42.png) ![wf-43](assets/wf-43.png)

#### この例で使用するマークアップのサンプル {#sample-markup-used-in-this-example}

カスタムステップのマークアップは、コンポーネントのルートノードの `.content.xml` で表現されます。この例で使用する `.content.xml` のサンプルは次のとおりです。

`/apps/cq/workflow/components/model/myCustomStep/.content.xml`

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
    cq:icon="bell"
    jcr:primaryType="cq:Component"
    jcr:title="My Custom Step"
    sling:resourceSuperType="cq/workflow/components/model/process"
    allowedParents="[*/parsys]"
    componentGroup="Workflow"/>
```

この例で使用する `_cq_editConfig.xml` のサンプルは次のとおりです。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:nt="https://www.jcp.org/jcr/nt/1.0"
    cq:disableTargeting="{Boolean}true"
    cq:inherit="{Boolean}true"
    jcr:primaryType="cq:EditConfig">
    <cq:formParameters
        jcr:primaryType="nt:unstructured"
        jcr:title="My Custom Step Card"
        SAMPLE_PROPERY="sample value"/>
    <cq:listeners
        jcr:primaryType="cq:EditListenersConfig"
        afterdelete="CQ.workflow.flow.Step.afterDelete"
        afteredit="CQ.workflow.flow.Step.afterEdit"
        afterinsert="CQ.workflow.flow.Step.afterInsert"
        afterMove="REFRESH_PAGE"/>
</jcr:root>
```

この例で使用する `_cq_dialog/.content.xml` のサンプルは次のとおりです。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:nt="https://www.jcp.org/jcr/nt/1.0"
    jcr:primaryType="nt:unstructured"
    jcr:title="My Custom - Step Properties"
    sling:resourceType="cq/gui/components/authoring/dialog">
    <content
        jcr:primaryType="nt:unstructured"
        sling:resourceType="granite/ui/components/coral/foundation/tabs">
        <items jcr:primaryType="nt:unstructured">
            <common
                cq:hideOnEdit="true"
                jcr:primaryType="nt:unstructured"
                jcr:title="Common"
                sling:resourceType="granite/ui/components/coral/foundation/fixedcolumns"/>
            <process
                cq:hideOnEdit="true"
                jcr:primaryType="nt:unstructured"
                jcr:title="Process"
                sling:resourceType="granite/ui/components/coral/foundation/fixedcolumns"/>
            <mycommon
                jcr:primaryType="nt:unstructured"
                jcr:title="Common"
                sling:resourceType="granite/ui/components/coral/foundation/fixedcolumns">
                <items jcr:primaryType="nt:unstructured">
                    <columns
                        jcr:primaryType="nt:unstructured"
                        sling:resourceType="granite/ui/components/coral/foundation/container">
                        <items jcr:primaryType="nt:unstructured">
                            <title
                                jcr:primaryType="nt:unstructured"
                                sling:resourceType="granite/ui/components/coral/foundation/form/textfield"
                                fieldLabel="Title"
                                name="./jcr:title"/>
                            <description
                                jcr:primaryType="nt:unstructured"
                                sling:resourceType="granite/ui/components/coral/foundation/form/textarea"
                                fieldLabel="Description"
                                name="./jcr:description"/>
                        </items>
                    </columns>
                </items>
            </mycommon>
            <advanced
                jcr:primaryType="nt:unstructured"
                jcr:title="Advanced"
                sling:resourceType="granite/ui/components/coral/foundation/fixedcolumns">
                <items jcr:primaryType="nt:unstructured">
                    <columns
                        jcr:primaryType="nt:unstructured"
                        sling:resourceType="granite/ui/components/coral/foundation/container">
                        <items jcr:primaryType="nt:unstructured">
                            <email
                                jcr:primaryType="nt:unstructured"
                                sling:resourceType="granite/ui/components/coral/foundation/form/checkbox"
                                fieldDescription="Notify user via email."
                                fieldLabel="Email"
                                name="./metaData/PROCESS_AUTO_ADVANCE"
                                text="Notify user via email."
                                value="true"/>
                        </items>
                    </columns>
                </items>
            </advanced>
        </items>
    </content>
</jcr:root>
```

>[!NOTE]
>
>ダイアログ定義の共通ノードとプロセスノードに注目してください。 これらは、カスタムステップのスーパータイプとして使用したプロセスステップから継承されます。
>
>`sling:resourceSuperType : cq/workflow/components/model/process`

>[!NOTE]
>
>クラシック UI のモデルエディターのダイアログは、標準のタッチ操作対応 UI のエディターでも利用できます。
>
>ただし、従来の UI ステップダイアログを標準の UI ダイアログにアップグレードする場合は、AEM にある[最新化ツール](/help/sites-developing/modernization-tools.md)を使用できます。変換後も、特定の用途に合わせてダイアログに手動で変更を加えることができます。
>
>* アップグレードしたダイアログが空の場合は、同様の機能を持つ `/libs` のダイアログを解決策の例として参考にできます。次に例を示します。
>
>* `/libs/cq/workflow/components/model`
>* `/libs/cq/workflow/components/workflow`
>* `/libs/dam/components`
>* `/libs/wcm/workflow/components/autoassign`
>* `/libs/cq/projects`
>
>  `/libs` 内の設定は参考にするだけに留め、変更しないでください。既存のステップを活用する場合は、`/apps` にコピーし、そこで変更を加えてください。
