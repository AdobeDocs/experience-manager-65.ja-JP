---
title: JEE Workbench上のAEM Formsのexecute scriptサービスを使用してXMLデータを作成する方法を教えてください。
description: JEE上のAEM Forms Workbenchでのexecute scriptサービスを使用したXMLデータの作成
source-git-commit: 730ae7cd6cd04eb6377b37eafe29db597e93cce3
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 0%

---

# JEE上のAEM Forms Workbenchでのexecute scriptサービスを使用したXMLデータの作成 {#using-execute-script-service-forms-jee-workbench}

例えば、JEE上のAEM Forms Process Managementワークフローには、次のような多くのXMLが関係しています。XML情報は、プロセスで構築され、JEE Workspace上のAEM FormsのFlexアプリケーションに送信され、システム設定に使用されたり、フォームとの間で情報を渡したりすることができます。 JEE上のAEM Forms開発者がXMLを管理する必要がある場合は多くありますが、その場合はXMLをJEE上のAEM Formsプロセスで管理する必要が生じます。

単純なXML設定を扱う場合、`Set Value`サービス(JEE上のデフォルトのAEM Formsサービス)を使用できます。 このサービスは、プロセスデータモデル内の1つ以上のデータ項目の値を設定します。 非常に単純な条件ロジック「もしこれなら、そのシナリオ」の場合、このサービスは目的に合う可能性があります。

ただし、より複雑な状況では、Set Valueサービスはあまり有効ではありません。 このような状況では、Javaのようなプログラミング言語で提供されるような、より堅牢なプログラミングコマンドのセットに依存する必要があります。 Set Valueサービス内の単純なテキストからXMLドキュメントを作成するよりも、Javaを使用して複雑なXMLを作成する方がはるかに簡単で明確です。 さらに、Set Valueサービス内よりもJavaに条件付きプログラミングを含める方が簡単です。

## プロセスでのExecute Scriptサービスの使用 {#using-execute-script-service-in-process}

JEE上のAEM Forms Workbenchで使用可能なJEE上の標準のAEM Formsサービスのセット内で、は`Execute Script`サービスです。 このサービスを使用すると、プロセス内でスクリプトを実行でき、そのための`executeScript`操作を提供できます。

### 「スクリプトを実行」サービスをアクティビティとして定義したアプリケーションとプロセスの作成 {#create-an-application}

このチュートリアルでは、アプリケーションとプロセスの作成全体が範囲外ですが、この手順のために、「DemoApplication02」という名前のアプリケーションを作成しました。 アプリケーションが既に作成されている場合は、このアプリケーションでexecuteScriptサービスを呼び出すプロセスを作成する必要があります。 `Execute Script`サービスを含むプロセスをアプリケーションに追加するには：

1. アプリケーションを右クリックし、「[!UICONTROL 新規]」を選択します。 [!UICONTROL 新しい]スライドアウトメニューで、「[!UICONTROL プロセス]」を選択します。 必要に応じてプロセスに名前を付け、説明を追加し、このプロセスを表すアイコンを選択します。 このチュートリアルの目的で、プロセスを作成し、`executeScriptDemoProcess`という名前を付けました。
1. スタートポイントを定義するか、後でスタートポイントを追加する単純なオプトを定義します。
1. プロセスが作成され、[!UICONTROL プロセスデザイン]ウィンドウで自動的に開きます。 このウィンドウで、Process Designウィンドウの上部にあるActivity Pickerアイコンをクリックし、新しいアクティビティをスイムレーンにドラッグします。 この時点で、[!UICONTROL アクティビティウィンドウの定義]が表示されます（下図を参照）。
   ![アクティビティの定義](assets/define-activity.jpg)
1. executeScriptサービスは、`Foundation`サービスセットの下にあります。 サービス名には、操作名`executeScript`を持つ`Execute Script – 1.0`が表示されます。 クリックしてこの項目を選択します。
1. これで、このプロセスが作成され、デフォルトでは、左側のウィンドウに[!UICONTROL プロセスのプロパティ]ウィンドウが表示されます。

#### 「スクリプトを実行」サービスを使用したプロセスへのスクリプトの追加 {#add-script-to-process-with-execute-script}

「スクリプトを実行」サービスアクティビティを定義してプロセスを作成したら、このプロセスにスクリプトを追加できます。 このプロセスにスクリプトを追加するには：

1. [!UICONTROL プロセスのプロパティ]パレットに移動します。 このパレット内で、「[!UICONTROL 入力]」セクションを展開し、「。..」アイコンをクリックします。

1. 表示されるテキストボックスにスクリプトを記述します。 スクリプトが書き込まれたら、[OK]を押します（下図を参照）。
   ![Execute Script](assets/execute-script.jpg)

## Execute Scriptサービスを使用したXMLの作成 {#create-xml-execute-script-service}

Execute Scriptサービスを含むプロセスが作成されたら、このスクリプトを使用してXMLを作成できます。 1つは、上記の「`Execute Script`サービスを使用してプロセスにスクリプトを追加する」の節で説明したテキストボックスに、以下に示すスクリプトを記述します。

**Execute Scriptサービスのテクノロジーについて**

Execute Scriptサービスの能力と制限を知るには、サービスの技術的基盤を知る必要があります。 JEE上のAEM Formsでは、Apache Xerces Document Object Model(DOM)パーサーを使用して、プロセス内でXML変数を作成し、保存します。 Xercesは、W3Cのドキュメントオブジェクトモデル仕様のJava実装です。[ここで](https://dom.spec.whatwg.org/)を定義します。 DOMの仕様は、1998年から続くXMLを操作する標準的な方法です。 XercesのJava実装であるXerces-Jは、DOM Level 2 version 1.0をサポートしています。

XML変数の格納に使用されるJavaクラスは次のとおりです。

* org.apache.xerces.dom.NodeImplおよび

* org.apache.xerces.dom.DocumentImpl

DocumentImplはNodeImplのサブクラスなので、XMLプロセス変数がNodeImplの派生であると想定できます。 NodeImpl [のドキュメントは、こちら](http://xerces.apache.org/xerces-j/apiDocs/org/apache/xerces/dom/NodeImpl.html)を参照してください。

**Execute Scriptサービスを使用したサンプルXML作成**

次に、Execute Scriptサービス内でのXMLの作成例を示します。 プロセスにはXML型の変数nodeが含まれます。 このアクティビティの最終結果は、XMLドキュメントになります。 このドキュメントの内容、またはプロセス全体への適用方法は、このチュートリアルでは範囲外です。最終的には、アプリケーション全体でXMLが何を行う必要があるかが決まります。 XMLは、JEE上のAEM Formsのフォームとプロセスで多くの目的に使用できます。これは、単純なXMLドキュメントを出力するための「スクリプトを実行」アクティビティのコーディング方法を示したものです。

XMLを出力する単純なJavaスクリプトは次のようになります。

```xml
import org.apache.xerces.dom.DocumentImpl;

import org.w3c.dom.Document;

import org.w3c.dom.Element;



Document document = new DocumentImpl();

Element topLevelResources = document.createElement("resources");

Element resource = document.createElement("resource");

resource.setAttribute("id", "first item id");

resource.setAttribute("value", "first item value");

topLevelResources.appendChild(resource);

document.appendChild(topLevelResources);

patExecContext.setProcessDataValue("/process_data/node", document);
```

>[!NOTE]
>
>上記のDOMオブジェクトをスクリプトに読み込む必要があります。

この単純なスクリプトの結果は、次の変数ノードが設定された新しいXMLドキュメントになります。

```xml
<resources>

<resource id="first item id" value="first item value"/>

</resources>
```

**反復ループを使用したXMLへのノードの追加**

ノードは、プロセス内の既存のXML変数にも追加できます。 変数nodeには、先ほど作成したXMLオブジェクトが含まれます。

```xml
Document document = patExecContext.getProcessDataValue("/process_data/node");

NodeList childNodes = document.getChildNodes();

int numChildren = childNodes.getLength();

for (int i = 0; i < numChildren; i++)

{

Node currentChild = childNodes.item(i);

if (currentChild.getNodeType() == Node.ELEMENT_NODE)

{

// found the top level node

Element newResource = document.createElement("resource");

newResource.setAttribute("id", "second item id");

newResource.setAttribute("value", "second item value");

currentChild.appendChild(newResource);

break;

}

}

patExecContext.setProcessDataValue("/process_data/node", document);
The variable node in the XML is now set to:

<resources> 

<resource id="first item id" value="first item value"/> 

<resource id="second item id" value="second item value"/> 

</resources>
```



