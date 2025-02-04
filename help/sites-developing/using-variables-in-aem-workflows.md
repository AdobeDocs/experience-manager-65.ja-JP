---
title: AEM ワークフローの変数
description: 変数を作成し、その変数の値を設定し、OR 分岐および移動 AEM ワークフローステップで使用します。
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
docset: aem65
exl-id: c8aeceec-860c-49ee-b681-d7107e52020d
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: bdbf9b73553c42865560c76eebab76e2fc397fdf
workflow-type: tm+mt
source-wordcount: '1935'
ht-degree: 100%

---

# AEM ワークフローの変数{#variables-in-aem-workflows}

ワークフローモデルの変数は、そのデータタイプに基づいて値を格納する方法です。ワークフローステップで変数の名前を使用して、変数に格納されている値を取得できます。変数名を使用して、ルーティング上の決定を行う式を定義することもできます。

AEM ワークフローモデルでは、次のことができます。

* 保存する情報タイプに基づいて、データタイプの [変数を作成します](/help/sites-developing/using-variables-in-aem-workflows.md#create-a-variable)。
* [変数の値を設定する](/help/sites-developing/using-variables-in-aem-workflows.md#set-a-variable)には、「変数を設定する」ワークフローステップを使用します。
* OR 分岐と移動 AEM ワークフローステップで[変数を使用](/help/sites-developing/using-variables-in-aem-workflows.md#use-a-variable)して、ルーティングを決定するための式を定義できるようにします。また、AEM Forms のすべてのワークフローステップで変数を使用することもできます。

次のビデオでは、AEM ワークフローモデルで変数を作成、設定および使用する方法を示します。

<!-- FUTURE ERROR: YouTube and mp4 videos are not supported -->

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/usevariables_example.mp4)

変数は、[MetaDataMap](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) インターフェイスの拡張です。ECMAScript で [MetaDataMap](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) を使用すると、変数を使用して保存されたメタデータにアクセスできます。

## 変数の作成 {#create-a-variable}

変数は、ワークフローモデルのサイドキックにある「変数」セクションを使用して作成します。AEM ワークフロー変数は、次のデータタイプをサポートしています。

* **プリミティブデータタイプ**：Long、Double、Boolean、Date、String
* **複雑なデータタイプ**：[XML](https://docs.oracle.com/javase/8/docs/api/org/w3c/dom/Document.html) および [JSON](https://www.javadoc.io/doc/com.google.code.gson/gson/2.3/com/google/gson/JsonObject.html)

>[!NOTE]
>
>ワークフローでは、日付タイプの変数に対して ISO8601 形式のみをサポートします。

AEM Forms ワークフローで使用できるその他の複雑なデータタイプについては、[AEM Forms ワークフローの変数](/help/forms/using/variable-in-aem-workflows.md)を参照してください。ArrayList データタイプを使用して、変数コレクションを作成します。すべてのプリミティブデータタイプと複合データタイプに対して ArrayList 変数を作成できます。例えば、ArrayList 変数を作成し、サブタイプとして String を選択して、変数を使用して複数の文字列値を格納します。

変数を作成するには：

1. AEM インスタンスで、ツール／ワークフロー／モデルに移動します。
1. 「**[!UICONTROL 作成]**」を選択し、ワークフローモデルのタイトルとオプションの名前を指定します。モデルを選択し、「**[!UICONTROL 編集]**」を選択します。
1. ワークフローモデルのサイドキックにある使用可能な変数アイコンを選択し、「**[!UICONTROL 変数を追加]**」を選択します。

   ![変数を追加](assets/variables_add_variable_new.png)

1. 変数を追加ダイアログで、名前を指定し、変数のタイプを選択します。
1. 「**[!UICONTROL タイプ]**」ドロップダウンリストからデータタイプを選択し、次の値を指定します。

   * プリミティブデータタイプ - 変数のオプションのデフォルト値を指定します。
   * JSON または XML - オプションの JSON または XML スキーマパスを指定します。システムは、このスキーマで使用可能なプロパティを別の変数にマッピングおよび保存しながら、スキーマパスを検証します。
   * フォームデータモデル - フォームデータモデルのパスを指定します。
   * ArrayList - コレクションのサブタイプを指定します。

1. 変数の説明（オプション）を指定し、ボックス内のチェックマークで示される ![「保存」アイコンを選択します。](assets/Done_Icon.png) をタップして、変更を保存します。変数は、左側のペインで使用可能なリストに表示されます。

変数を作成する場合、次のプラクティスをお勧めします。

* ワークフローで必要な数の変数を作成します。ただし、データベースのリソースを確保するため、必要最低限の変数を使用し、必要に応じて変数を再利用してください。
* 変数では大文字と小文字が区別されます。ワークフローで変数を参照する場合には同じように大文字と小文字を区別してください。
* 変数名に特殊文字を使用しないでください。

## 変数の設定 {#set-a-variable}

「変数を設定」ステップを使用して、変数の値を設定し、値が設定される順序を定義できます。変数は、変数マッピングが「変数を設定」ステップにリストされている順序で設定されます。

変数値を変更すると、変更が発生したプロセスのインスタンスのみに影響します。例えば、ワークフローが開始され変数データが変更されると、変更はそのワークフローのインスタンスのみに影響します。変更は、以前に開始された、または後で開始されたワークフローの他のインスタンスには影響しません。

変数のデータタイプに応じて、次のオプションを使用して変数の値を設定できます。

* **リテラル：**&#x200B;指定する値が正確に分かっている場合は、このオプションを使用します。
* **式：**&#x200B;使用する値が式に基づいて計算される場合は、このオプションを使用します。式は、提供された式エディターで作成されます。
* **JSON ドット表記：**&#x200B;このオプションを使用して、JSON または FDM タイプの変数から値を取得します。
* **XPATH：**&#x200B;このオプションを使用して XML タイプ変数から値を取得します。
* **ペイロード基準：**&#x200B;変数として格納する値が、ペイロードを基準としたパスにある場合は、このオプションを使用します。
* **絶対パス：**&#x200B;変数として格納する値が絶対パスにある場合は、このオプションを使用します。

また、JSON DOT 表記法または XPATH 表記法を使用して、JSON または XML タイプの変数の特定の要素を更新することもできます。

### 変数間マッピングの追加 {#add-mapping-between-variables}

変数間マッピングを追加するには、次の手順を実行します。

1. ワークフローの編集ページで、ワークフローモデルのサイドキックにある「ステップ」アイコンを選択します。
1. 「**変数を設定**」ステップをワークフローエディターにドラッグ＆ドロップし、ステップを選択してレンチで示される ![「設定」アイコンを選択します。](assets/configure_icon.png)（設定）。
1. 「変数を設定」ダイアログで、 **[!UICONTROL マッピング]**／**[!UICONTROL マッピングを追加]** を選択します。
1. 「**変数のマップ**」セクションで、データを格納する変数を選択し、マッピングモードを選択して、変数に格納する値を指定します。マッピングモードは、変数のタイプによって異なります。
1. より多くの変数をマッピングして、有意義な式を作成できるようにします。ボックス内のチェックマークで示される ![ 保存アイコンを選択します。](assets/Done_Icon.png) をタップして、変更を保存します。

### 例 1：XML 変数をクエリして、文字列変数の値を設定 {#example-query-an-xml-variable-to-set-value-for-a-string-variable}

XML ファイルを保存する XML タイプの変数を選択します。XML 変数をクエリして、XML ファイルで使用可能なプロパティの文字列変数の値を設定します。「**XML 変数に XPATH を指定**」フィールドを使用して、文字列変数に格納するプロパティを定義します。

この例では、**formdata** XML 変数を選択して **cc-app.xml** ファイルを格納します。**formdata** 変数をクエリすることで、**cc-app.xml** ファイルで使用可能な **emailAddress** プロパティの値を格納する **emailaddress** 文字列変数の値を設定できます。

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/set_variable_example1.mp4 "変数の値を設定")

### 例 2：式を使用して、他の変数に基づいて値を格納 {#example2}

式を使用して変数の和を計算し、結果を変数に格納します。

この例では、式エディターを使用して式を定義し、**assetscost** 変数と **balanceamount** 変数の和を計算し、その結果を **totalvalue** 変数に格納します。

<!-- FUTURE ERROR: YouTube and mp4 videos are not supported -->

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/variables_expression.mp4)

## 式エディターの使用 {#use-expression-editor}

実行時の変数の値を計算するのにも式を使用します。変数は、式を定義する式エディターを提供します。

式エディターを使用して、次の操作を行います。

* 他のワークフロー変数、数値または数式を使用して、変数の値を設定します。
* ワークフロー変数、文字列、数値、または式を数式内で使用
* 変数の値を設定できるように、条件を追加します。
* 条件の間に演算子を追加します。

![式エディター](assets/variables_expression_editor_new.png)

これは、次の変更を加えたアダプティブフォームのルールエディターに基づいています。変数のルールエディター：

* 関数はサポートしていません。
* ルールの概要を表示するための UI は提供していません。
* コードエディターはありません。
* オブジェクトの値の有効化と無効化はサポートしていません。
* オブジェクトのプロパティの設定はサポートしていません。
* Web サービスの呼び出しはサポートしていません。

詳しくは、[アダプティブフォームのルールエディター](/help/forms/using/rule-editor.md)を参照してください。

## 変数を使用 {#use-a-variable}

変数を使用して、入力と出力を取得したり、ステップの結果を保存したりできます。ワークフローエディターには、次の 2 種類のワークフローステップが用意されています。

* 変数をサポートするワークフローステップ
* 変数をサポートしないワークフローステップ

### 変数をサポートするワークフローステップ {#workflow-steps-with-support-for-variables}

移動ステップ、OR‧分割ステップ、およびすべての‧AEM‧Forms‧Workflow‧ステップでは、変数をサポートしています。

#### OR 分割ステップ {#or-split-step}

OR 分割は、ワークフロー内に分割を作成し、以降は 1 つの分岐だけがアクティブになります。これを使用すると、ワークフローに条件付き処理パスを導入できます。必要に応じて、各分岐にワークフローステップを追加できます。

分岐のルーティング式は、ルール定義、ECMA スクリプト、または外部スクリプトを使用して定義できます。

変数を使用して、式エディターを使用したルーティング式を定義できます。OR 分割ステップでルーティング式を使用する方法について詳しくは、「[OR 分割ステップ](/help/sites-developing/workflows-step-ref.md#or-split)」を参照してください。

この例では、ルーティング式を定義する前に、[例 2 ](/help/sites-developing/using-variables-in-aem-workflows.md#example2)を使用して **totalvalue** 変数の値を設定します。**totalvalue** 変数の値が 50000 より大きい場合、分岐 1 はアクティブになります。同様に、**totalvalue** 変数の値が 50000 未満の場合に、Branch 2 をアクティブにするルールを定義できます。

<!-- FUTURE ERROR: YouTube and mp4 videos are not supported -->

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/variables_orsplit_example.mp4)

同様に、外部スクリプトパスを選択するか、ルーティング式の ECMA スクリプトを指定して、アクティブな分岐を評価します。「**[!UICONTROL 分岐名の変更]**」を選択して、分岐に別名を指定します。

その他の例については、[ワークフローモデルの作成](/help/forms/using/aem-forms-workflow.md#create-a-workflow-model)を参照してください。

#### 移動ステップ {#go-to-step}

**移動ステップ**&#x200B;を使用すると、ルーティング式の結果に応じて、ワークフローモデルで次に実行するステップを指定できます。

OR 分割ステップと同様に、ルール定義、ECMA スクリプト、または外部スクリプトを使用して、移動ステップのルーティング式を定義できます。

変数を使用して、式エディターを使用したルーティング式を定義できます。移動ステップでルーティング式を使用する方法について詳しくは、「[移動ステップ](/help/sites-developing/workflows-step-ref.md#goto-step)」を参照してください。

![移動のルール](assets/variables_goto_rule1_new.png)

この例では、**actiontaken** 変数の値が **Need more info** に等しい場合、移動ステップは次のステップとして「Review Credit Card Application」を指定します。

移動ステップでのルール定義の使用するその他の例については、[For ループのシミュレーション](/help/sites-developing/workflows-step-ref.md#simulateforloop)を参照してください。

#### Forms ワークフロー中心のワークフローステップ {#forms-workflow-centric-workflow-steps}

すべての AEM Forms Workflow ステップは、変数をサポートします。詳しくは、[OSGi での Forms 中心のワークフローを参照してください](/help/forms/using/aem-forms-workflow-step-reference.md)。

### 変数をサポートしないワークフローステップ {#workflow-steps-without-support-for-variables}

[MetaDataMap](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) インターフェイスを使用して、変数をサポートしないワークフロー手順の変数にアクセスできます。

#### 変数値の取得 {#retrieve-the-variable-value}

データタイプに基づいて既存の変数の値を取得するには、ECMA スクリプトで次の API を使用します。

| 変数データタイプ | API |
|---|---|
| プリミティブ（Long、Double、Boolean、Date、String） | workItem.getWorkflowData().getMetaDataMap().get(variableName, type) |
| XML | Packages.org.w3c.dom.Document xmlObject = workItem.getWorkflowData().getMetaDataMap().get(variableName, Packages.org.w3c.dom.Document.class); |
| JSON | Packages.com.google.gson.JsonObject jsonObject = workItem.getWorkflowData().getMetaDataMap().get(variableName, Packages.com.google.gson.JsonObject.class); |

AEM Forms ワークフローで使用できる追加の複雑な変数データタイプの API について詳しくは、 [AEM Forms ワークフローの変数](/help/forms/using/variable-in-aem-workflows.md)を参照してください。

**例**

次の API を使用して、string データタイプの値を取得します。

```
workItem.getWorkflowData().getMetaDataMap().get(accname, Packages.java.lang.String)
```

#### 変数値の更新 {#update-the-variable-value}

変数の値を更新するには、ECMA スクリプトで次の API を使用します。

```
workItem.getWorkflowData().getMetaDataMap().put(variableName, value)
```

**例**

```
workItem.getWorkflowData().getMetaDataMap().put(salary, 50000)
```

**Salary** 変数の値を 50000 に更新します。

### ワークフローを呼び出す変数の設定 {#apiinvokeworkflow}

API を使用して変数を設定し、それらを渡してワークフローインスタンスを呼び出すことができます。

[workflowSession.startWorkflows](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/granite/workflow/WorkflowSession.html?lang=ja#startWorkflow-com.adobe.granite.workflow.model.WorkflowModel-com.adobe.granite.workflow.exec.WorkflowData-java.util.Map-) は、モデル、wfData、metaData を引数として使用します。MetaDataMap を使用して変数の値を設定します。

この API では、 **variableName** 変数は metaData.put(variableName, value) を使用して **value** に設定されます。

```java
import com.adobe.granite.workflow.model.WorkflowModel;
import com.adobe.granite.workflow.metadata.MetaDataMap;
import com.adobe.aemfd.docmanager.Document;

/*Assume that you already have a workflowSession and modelId along with the payloadType and payload*/
WorkflowData wfData = workflowSession.newWorkflowData(payloadType, payload);
MetaDataMap metaData = wfData.getMetaDataMap();
metaData.put(variableName, value); //Create a variable "variableName" in your workflow model
WorkflowModel model = workflowSession.getModel(modelId);
workflowSession.startWorkflow(model, wfData, metaData);
```

## 変数の編集 {#edit-a-variable}

1. ワークフローの編集ページで、ワークフローモデルのサイドキックにある「変数」アイコンを選択します。左側のペインの「変数」セクションには、既存のすべての変数が表示されます。
1. 鉛筆記号で示される ![「編集」アイコンを選択します。編集する変数名の横にある ](assets/edit.png)（編集）アイコン。
1. 変数情報を編集し、チェックマークで示される ![ 保存アイコンを選択します。](assets/Done_Icon.png) をタップして、変更を保存します。変数の「**[!UICONTROL 名前]**」フィールドと「**[!UICONTROL タイプ]**」フィールドは編集できません。

## 変数の削除 {#delete-a-variable}

変数を削除する前に、ワークフローから変数のすべての参照を削除します。この変数がワークフローで使用されていないことを確認します。

変数を削除するには：

1. ワークフローの編集ページで、ワークフローモデルのサイドキックにある「変数」アイコンを選択します。左側のペインの「変数」セクションには、既存のすべての変数が表示されます。
1. 削除する変数名の横にある「削除」アイコンを選択します。
1. チェックマーク記号で示される ![ 完了アイコンを選択します。](assets/Done_Icon.png)確認して変数を削除します。
