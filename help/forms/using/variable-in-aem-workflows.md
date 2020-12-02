---
title: AEM Formsワークフローの変数
seo-title: AEM Formsワークフローの変数
description: 変数を作成し、変数の値を設定して、AEM Formsワークフロー手順で使用します。
seo-description: 変数を作成し、変数の値を設定して、AEM Formsワークフロー手順で使用します。
uuid: 634a75c4-4899-478f-9e5d-a870f5efa583
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: cbf4e35a-7905-44ab-ab68-fb443443f02d
docset: aem65
translation-type: tm+mt
source-git-commit: 252dac988c8256cf99ee8487feb937d5345ed797
workflow-type: tm+mt
source-wordcount: '2113'
ht-degree: 5%

---


# AEM Formsワークフローの変数{#variables-in-aem-forms-workflows}

ワークフローモデル内の変数は、そのデータ型に基づいて値を格納する方法です。 その後、任意のワークフロー手順で変数の名前を使用して、変数に保存されている値を取得できます。 変数名を使用して、ルーティング上の意思決定を行う式を定義することもできます。

AEMワークフローモデルでは、次のことができます。

* [データ型に格納する情報型に基づいて、](../../forms/using/variable-in-aem-workflows.md#create-a-variable) 変数を作成します。
* [変数の値を設定するには、「変数を設定」ワークフローの手順を使用し](../../forms/using/variable-in-aem-workflows.md#set-a-variable) ます。
* [すべてのAEM Formsワークフロー手順で](../../forms/using/variable-in-aem-workflows.md#use-a-variable) 変数を使用して、格納された値を取得し、OR分割とGOTOの手順でルーティング式を定義します。

次のビデオでは、AEMワークフローモデルで変数を作成、設定および使用する方法を示します。

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/variables_introduction_1_1.mp4)

変数は、既存の[MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html)インターフェイスの拡張です。 ECMAScriptで[MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html)を使用すると、変数を使用して保存されたメタデータにアクセスできます。

## 変数{#create-a-variable}を作成

変数は、ワークフローモデルのサイドキックにある「変数」セクションを使用して作成します。 AEMワークフロー変数は、次のデータ型をサポートしています。

* **プリミティブデータ型**:長い、重複、ブール、日付、文字列
* **複雑なデータ型**: [ドキュメント](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/aemfd/docmanager/Document.html)、 [XML](https://docs.oracle.com/javase/8/docs/api/org/w3c/dom/Document.html)、 [JSON](https://static.javadoc.io/com.google.code.gson/gson/2.3/com/google/gson/JsonObject.html)、フォームデータモデルの各インスタンス。

>[!NOTE]
>
>ワークフローでは、日付型変数に対してISO8601形式のみがサポートされています。

ドキュメントおよびフォームデータモデルのデータ型には、[AEM Formsアドオンパッケージ](https://helpx.adobe.com/jp/aem-forms/kb/aem-forms-releases.html)が必要です。  ArrayListデータ型を使用して、変数コレクションを作成します。 すべてのプリミティブデータ型と複合データ型に対してArrayList変数を作成できます。 例えば、ArrayList変数を作成し、その変数を使用して複数の文字列値を格納する場合は、「String」をサブタイプとして選択します。

次の手順を実行して、変数を作成します。

1. AEMインスタンスで、ツール![](/help/forms/using/assets/hammer.png)/ワークフロー/モデルに移動します。
1. 「**[!UICONTROL 作成]**」をタップし、ワークフローモデルのタイトルとオプション名を指定します。 モデルを選択し、**[!UICONTROL 編集]**&#x200B;をタップします。
1. ワークフローモデルのサイドキックにある変数アイコンをタップし、**[!UICONTROL 追加変数]**&#x200B;をタップします。

   ![変数を追加](assets/variables_add_variable_new.png)

1. Variable追加ダイアログで、名前を指定し、変数のタイプを選択します。
1. **[!UICONTROL タイプ]**&#x200B;ドロップダウンリストからデータタイプを選択し、次の値を指定します。

   * プリミティブデータ型 — 変数のオプションのデフォルト値を指定します。
   * JSONまたはXML — オプションのJSONまたはXMLスキーマパスを指定します。 このスキーマで使用可能なプロパティを別の変数にマッピングして保存する際に、スキーマパスが検証されます。
   * Form Data Model - Form Data Modelのパスを指定します。
   * ArrayList — コレクションのサブタイプを指定します。

1. 変数の説明（オプション）を指定し、![done_icon](assets/done_icon.png)をタップして変更を保存します。 変数は、左側のペインで使用可能なリストに表示されます。

変数を作成する場合、次のプラクティスをお勧めします。

* ワークフローで必要な数の変数を作成します。 ただし、データベースのリソースを確保するため、必要最低限の変数を使用し、必要に応じて変数を再利用してください。
* 変数では大文字と小文字が区別されます。ワークフローで変数を参照する場合は、大文字と小文字を同じにします。
* 変数名に特殊文字を使用しない

## 変数{#set-a-variable}を設定

変数の値を設定し、値が設定される順序を定義するには、変数の設定手順を使用します。 変数は、変数の設定手順で変数のマッピングが示される順序で設定されます。

変数値を変更すると、変更が発生したプロセスのインスタンスのみに影響します。例えば、ワークフローが開始され、変数データが変更されると、その変更はワークフローのそのインスタンスにのみ影響します。 この変更は、以前に開始された、または以降に開始されたワークフローの他のインスタンスには影響しません。

変数のデータタイプに応じて、次のオプションを使用して変数の値を設定できます。

* **リテラル：**&#x200B;指定する値が正確に分かっている場合は、このオプションを使用します。

* **式:式に基づいて値が計算される場合は、このオプションを** 使用します。式は、提供された式エディタで作成されます。

* **JSONドット表記：JSONまたはFDM型の変数から値を取得するには、このオプションを** 使用します。
* **XPATH:XML型の変数から値を取得するには、このオプションを** 使用します。

* **ペイロードとの相対：変数に保存する値が、ペイロードとの相対パスで使用可能な場合に** このオプションを使用します。

* **絶対パス：変数に保存する値が絶対パスで使用できる場合に** 使用します。

また、JSON DOT NotationまたはXPATH表記を使用して、JSONまたはXML型の変数の特定の要素を更新することもできます。

### 変数間追加のマッピング{#add-mapping-between-variables}

次の手順を実行して、変数間のマッピングを追加します。

1. ワークフローの編集ページで、ワークフローモデルのサイドキックにあるステップアイコンをタップします。
1. 「**変数を設定**」手順をワークフローエディターにドラッグ&amp;ドロップし、手順をタップして![設定_icon](assets/configure_icon.png)（設定）を選択します。
1. Set Variable（変数を設定）ダイアログで、**[!UICONTROL マッピング]**/**[!UICONTROL 追加マッピング]**&#x200B;を選択します。
1. 「**Map Variable**」セクションで、データを格納する変数を選択し、マッピングモードを選択して、変数に格納する値を指定します。 マッピングモードは、変数のタイプに応じて異なります。
1. 意味のある式を行うために、より多くの変数をマッピングします。 ![done_icon](assets/done_icon.png)をタップして変更を保存します。

### 例1:文字列変数{#example-query-an-xml-variable-to-set-value-for-a-string-variable}に値を設定するXML変数のクエリ

XMLファイルを保存するXML型の変数を選択します。 XML変数をクエリして、XMLファイルで使用可能なプロパティの文字列変数の値を設定します。 **XML変数**&#x200B;フィールドのXPATHを指定して、文字列変数に格納するプロパティを定義します。

この例では、**formdata** XML変数を選択して&#x200B;**cc-app.xml**&#x200B;ファイルを保存します。 **formdata**&#x200B;変数をクエリして、**emailaddress**&#x200B;文字列変数の値を設定し、**cc-app.xml**&#x200B;ファイルで使用できる&#x200B;**emailAddress**&#x200B;プロパティの値を保存します。

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/set_variable_example1.mp4 "変数の値の設定")

### 例2:式を使用して他の変数{#example2}に基づいて値を格納する

式を使用して変数の合計を計算し、結果を変数に格納します。

この例では、式エディターを使用して、**assetscost**&#x200B;変数と&#x200B;**balanceamount**&#x200B;変数の合計を計算し、結果を&#x200B;**totalvalue**&#x200B;変数に格納する式を定義します。

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/variables_expression.mp4)

## 式エディタ{#use-expression-editor}を使用

また、式を使用して、実行時に変数の値を計算します。 変数は、式を定義する式エディターを提供します。

式エディターを使用して、次の操作を行います。

* 他のワークフロー変数、数値または数学式を使用して、変数の値を設定します。
* ワークフロー変数、文字列、数値、または式を数学式内で使用する
* 条件を使用して、変数の値を追加設定します。
* 演算子を追加使用します。

![式エディター](assets/variables_expression_editor_new.png)

これは、次の変更を加えたアダプティブフォームのルールエディターに基づいています。 変数のルールエディター：

* 関数はサポートされません。
* ルールの表示サマリにUIを提供しない
* コードエディターがありません。
* オブジェクトの値の有効化と無効化をサポートしません。
* オブジェクトのプロパティの設定はサポートされません。
* Webサービスの呼び出しをサポートしません。

詳しくは、「[アダプティブフォームのルールエディター](../../forms/using/rule-editor.md)」を参照してください。

## 変数{#use-a-variable}を使用

変数を使用して、入力と出力を取得したり、ステップの結果を保存したりできます。 ワークフローエディターには、次の2種類のワークフロー手順が用意されています。

* 変数のサポートを含むワークフロー手順
* 変数をサポートしないワークフロー手順

### 変数{#workflow-steps-with-support-for-variables}をサポートするワークフロー手順

「移動先」、「分割」の各ステップと、すべてのAEM Formsワークフローステップで、変数がサポートされています。

#### OR分割ステップ{#or-split-step}

OR 分割は、ワークフロー内に分割を作成し、以降は 1 つのブランチだけがアクティブになります。これを使用すると、ワークフローに条件付き処理パスを導入できます。必要に応じて、各ブランチにワークフローステップを追加できます。

ブランチのルーティング式は、ルール定義、ECMAスクリプトまたは外部スクリプトを使用して定義できます。

変数を使用して、式エディターを使用してルーティング式を定義できます。 OR分割手順でのルーティング式の使用について詳しくは、[または分割手順](/help/sites-developing/workflows-step-ref.md#or-split)を参照してください。

この例では、ルーティング式を定義する前に、[例2](../../forms/using/variable-in-aem-workflows.md#example2)を使用して&#x200B;**totalvalue**&#x200B;変数の値を設定します。 **totalvalue**&#x200B;変数の値が50000より大きい場合、ブランチ1はアクティブです。 同様に、**totalvalue**&#x200B;変数の値が50000未満の場合に、Branch 2をアクティブにするルールを定義できます。

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/variables_orsplit_example.mp4)

同様に、アクティブなブランチを評価するルーティング式に対して、外部スクリプトパスを選択するか、ECMAスクリプトを指定します。 「**[!UICONTROL ブランチ名の変更]**」をタップして、ブランチの別の名前を指定します。

その他の例については、[ワークフローモデルの作成](../../forms/using/aem-forms-workflow.md#create-a-workflow-model)を参照してください。

#### ステップ{#go-to-step}に移動

**Gotoステップ**&#x200B;を使用すると、ルーティング式の結果に応じて、実行するワークフローモデルの次のステップを指定できます。

OR分割の手順と同様に、ルール定義、ECMAスクリプトまたは外部スクリプトを使用して、Goto手順のルーティング式を定義できます。

変数を使用して、式エディターを使用してルーティング式を定義できます。 Gotoステップでルーティング式を使用する方法について詳しくは、[Gotoステップ](/help/sites-developing/workflows-step-ref.md#goto-step)を参照してください。

![ルールに移動](assets/variables_goto_rule1_new.png)

この例では、**actiontaken**&#x200B;変数の値が&#x200B;**Need more info**&#x200B;と等しい場合、Goto手順で「Review Credit Card Application」を次の手順として指定します。

Goto手順でのルール定義の使用例については、[Forループのシミュレーション](/help/sites-developing/workflows-step-ref.md#simulateforloop)を参照してください。

#### Formsワークフロー中心のワークフローステップ{#forms-workflow-centric-workflow-steps}

すべてのAEM Formsワークフローステップで、変数がサポートされています。 詳しくは、[OSGi](../../forms/using/aem-forms-workflow-step-reference.md)でのForms中心のワークフローを参照してください。

### 変数{#workflow-steps-without-support-for-variables}をサポートしないワークフローステップ

[MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html)インターフェイスを使用して、変数をサポートしないワークフロー手順の変数にアクセスできます。

#### 変数の値{#retrieve-the-variable-value}を取得します

ECMAスクリプトで次のAPIを使用して、データ型に基づいて既存の変数の値を取得します。

| 変数データ型 | API |
|---|---|
| プリミティブ(長整数型、重複型、ブール型、日付型、文字列型) | workItem.getWorkflowData().getMetaDataMap().get(variableName, type) |
| ドキュメント | Packages.com.adobe.aemfd.docmanager.ドキュメントdoc = workItem.getWorkflowData().getMetaDataMap().get(&quot;docVar&quot;, Packages.com.adobe.aemfd.docmanager.ドキュメント.class); |
| XML | Packages.org.w3c.dom.ドキュメントxmlObject = workItem.getWorkflowData().getMetaDataMap().get(variableName, Packages.org.w3c.dom.ドキュメント.class); |
| フォームデータモデル | Packages.com.adobe.aem.aderame.api.FormDataModelInstance fdmObject = workItem.getWorkflowData().get(variableName, Packages.com.adobe.aem.api.FormDataModelInstance.class); |
| JSON | Packages.com.gogoogle.gson.JsonObject jsonObject = workItem.getWorkflowData().getMetaDataMap().get(variableName, Packages.com.google.gson.JsonObject.class); |

ドキュメントおよびフォームデータモデルの変数データ型には、[AEM Formsアドオンパッケージ](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)が必要です。

**例**

次のAPIを使用して、stringデータ型の値を取得します。

```javascript
workItem.getWorkflowData().getMetaDataMap().get(accname, Packages.java.lang.String)
```

#### 変数値{#update-the-variable-value}を更新

ECMAスクリプトで次のAPIを使用して、変数の値を更新します。

```javascript
workItem.getWorkflowData().getMetaDataMap().put(variableName, value)
```

**例**

```javascript
workItem.getWorkflowData().getMetaDataMap().put(salary, 50000)
```

**salary**&#x200B;変数の値を50000に更新します。

### ワークフローを呼び出す変数を設定{#apiinvokeworkflow}

APIを使用して変数を設定し、それらを渡してワークフローインスタンスを呼び出すことができます。

[workflowSession.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/WorkflowSession.html#startWorkflow-com.adobe.granite.workflow.model.WorkflowModel-com.adobe.granite.workflow.exec.WorkflowData-java.util.Map-) startWorkflowsは、モデル、wfData、metaDataを引数として使用します。MetaDataMapを使用して変数の値を設定します。

このAPIでは、**variableName**&#x200B;変数にmetaData.put(variableName, value)；を使用して&#x200B;**value**&#x200B;を設定します。

```javascript
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

**例**

**doc**&#x200B;ドキュメントオブジェクトをパス(&quot;a/b/c&quot;)に初期化し、**docVar**&#x200B;変数の値をドキュメントオブジェクトに保存されているパスに設定します。

```javascript
import com.adobe.granite.workflow.WorkflowSession;
import com.adobe.granite.workflow.exec.WorkflowData;
import com.adobe.granite.workflow.model.WorkflowModel;
import com.adobe.granite.workflow.metadata.MetaDataMap;
import com.adobe.aemfd.docmanager.Document;

/*This example assumes that you already have a workflowSession and modelId along with the payloadType and payload */
WorkflowData wfData = workflowSession.newWorkflowData(payloadType, payload);
MetaDataMap metaData = wfData.getMetaDataMap();
Document doc = new Document("/a/b/c");// initialize a document object
metaData.put("docVar",doc); //Assuming that you have created a variable "docVar" of type Document in your workflow model
WorkflowModel model = workflowSession.getModel(modelId);
workflowSession.startWorkflow(model, wfData, metaData);
```

## 変数の編集{#edit-a-variable}

1. ワークフローを編集ページで、ワークフローモデルのサイドキックにある変数アイコンをタップします。 左側のペインの「変数」セクションには、既存の変数がすべて表示されます。
1. 編集する変数名の横にある![編集](assets/edit.png)（編集）アイコンをタップします。
1. 変数情報を編集し、![done_icon](assets/done_icon.png)をタップして変更を保存します。 変数の&#x200B;**[!UICONTROL 名前]**&#x200B;フィールドと&#x200B;**[!UICONTROL タイプ]**&#x200B;フィールドは編集できません。

## 変数{#delete-a-variable}の削除

変数を削除する前に、ワークフローから変数の参照をすべて削除します。 この変数がワークフローで使用されていないことを確認します。

次の手順を実行して、変数を削除します。

1. ワークフローを編集ページで、ワークフローモデルのサイドキックにある変数アイコンをタップします。 左側のペインの「変数」セクションには、既存の変数がすべて表示されます。
1. 削除する変数名の横にある削除アイコンをタップします。
1. ![done_icon](assets/done_icon.png)をタップして、変数の確認と削除を行います。

## 参照 {#references}

AEM Formsのワークフロー手順で変数を使用する例については、[AEMワークフローの変数](https://helpx.adobe.com/experience-manager/kt/forms/using/authoring_variables_in_aem_forms-workflow1.html)を参照してください。
