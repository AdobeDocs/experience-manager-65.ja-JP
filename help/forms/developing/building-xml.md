---
title: JEE Workbench 上の AEM Forms で Execute Script サービスを使用して XML データを作成する方法を教えてください。
description: JEE Workbench 上の AEM Forms の Execute Script サービスを使用した XML データの作成
exl-id: 2ec57cd4-f41b-4e5c-849d-88ca3d2cfe19
source-git-commit: 37d2c70bff770d13b8094c5959e488f5531aef55
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 99%

---

# JEE Workbench 上の AEM Forms の Execute Script サービスを使用した XML データの作成 {#using-execute-script-service-forms-jee-workbench}

JEE プロセス管理ワークフロー上の AEM Forms に関連している XML は数多くあります。例えば、XML 情報をプロセス内で構築したり、JEE ワークスペース上の AEM Forms の Flex アプリケーションに送信したり、システム設定に使用したりできますし、フォームとの間で情報を渡す場合に使用することができます。JEE 上の AEM Forms 開発者による XML の管理が必要となるインスタンスは多くありますが、そのうちの多くで、XML を JEE プロセス上の AEM Forms で管理する必要があります。

単純な XML 設定を扱う場合、`Set Value` サービスを使用することができます。これは JEE サービス上のデフォルトの AEM Forms です。プロセスデータモデルの 1 つ以上のデータ項目の値を設定します。非常に単純な条件ロジックである「もし～なら～である」という形式のシナリオの場合、このサービスが適している可能性があります。

しかし、より複雑な状況では、Set Value サービスはそれほど有効ではありません。このような場合、Java のようなプログラミング言語で提供されるコマンドなど、より堅牢な一連のプログラミングコマンドが必要となります。Set Value サービス内の単純なテキストから XML ドキュメントを作成するよりも、Java を使用して複雑な XML を作成する方がより簡単でより明確でしょう。さらに、条件付きプログラミングは Set Value サービスよりも Java で追加する方が簡単です。

## プロセスでの Execute Script サービスの使用 {#using-execute-script-service-in-process}

JEE Workbench の AEM Forms で使用可能な JEE サービス上の標準の AEM Forms のセットの中に `Execute Script` サービスがあります。このサービスではプロセスでスクリプトの実行が可能で、そのための `executeScript` 操作を使用できます。

### 「スクリプトを実行」サービスをアクティビティとして定義したアプリケーションとプロセスの作成 {#create-an-application}

アプリケーションやプロセス全体の作成は、このチュートリアルの対象外ですが、この手順のために、「DemoApplication02」という名前のアプリケーションを作成しました。アプリケーションが既に作成されている場合は、このアプリケーションでプロセスを作成して executeScript サービスを呼び出す必要があります。`Execute Script` サービスが含まれるアプリケーションにプロセスを追加するには以下の手順に従います。

1. アプリケーションを右クリックし、「[!UICONTROL 新規]」を選択してください。[!UICONTROL 新規]スライドアウトメニューで[!UICONTROL プロセス]を選択します。プロセスに適切な名前を付け、必要に応じて説明を追加し、このプロセスを表すアイコンを選択してください。このチュートリアル用に、プロセスを作成し、`executeScriptDemoProcess`という名前を付けました。
1. スタートポイントを定義するか、後でスタートポイントを追加するよう指定してください。
1. これでプロセスが作成され、 [!UICONTROL プロセスデザイン]ウィンドウで自動的に開きます。このウィンドウで、Process Design ウィンドウの上部にある「アクティビティピッカー」アイコンをクリックし、新しいアクティビティをスイムレーンにドラッグしてください。この時点で、[!UICONTROL アクティビティを定義ウィンドウ]が表示されます（下図を参照）。
   ![アクティビティを定義](assets/define-activity.jpg)
1. executeScript サービスは、 サービスの `Foundation` セットにあります。サービス名にこのオブジェクトが `Execute Script – 1.0` として表示され、操作名には `executeScript` と表示されます。この項目をクリックして選択します。
1. このプロセスが作成され、デフォルトでは[!UICONTROL プロセスのプロパティ]ウィンドウが左側のパネルに表示されます。

#### 「Execute Script」サービスを使用したプロセスへのスクリプトの追加 {#add-script-to-process-with-execute-script}

「Execute Script」サービスアクティビティを定義してプロセスを作成すると、このプロセスにスクリプトを追加できるようになります。このプロセスにスクリプトを追加するには、以下の手順に従います。

1. [!UICONTROL プロセスプロパティ]パレットに移動します。このパレット内で、「[!UICONTROL 入力]」セクションを展開し、「...」アイコンをクリックします。

1. 表示されるテキストボックスに、スクリプトを記述します。スクリプトの記述が完了したら、「OK」を押します（下図を参照）。
   ![Execute Script](assets/execute-script.jpg)

## Execute Script サービスを使用した XML の作成 {#create-xml-execute-script-service}

Execute Script サービスを含むプロセスが作成されたら、このスクリプトを使用して XML を作成できます。上の「`Execute Script`サービスを使用したプロセスへのスクリプトの追加」の節で説明されたテキストボックスで、以下のスクリプトを記述できます。

**Execute Script サービスのテクノロジーについて**

Execute Script サービスの機能と限界を制限事項するには、サービスの技術的基盤を理解する必要があります。JEE 上の AEM Forms は、Apache Xerces ドキュメントオブジェクトモデル（DOM）パーサーを使用して、プロセス内で XML 変数を作成し、保存します。Xerces は、W3C のドキュメントオブジェクトモデル仕様の Java 実装です。定義については[こちら](https://dom.spec.whatwg.org/)を参照してください。DOM 仕様は XML を操作する標準的な方法で、1998 年から存在します。Xerces の Java 実装である Xerces-J は、DOM Level 2 version 1.0 をサポートしています。

XML 変数の格納に使用される Java クラスは次のとおりです。

* org.apache.xerces.dom.NodeImpl および

* org.apache.xerces.dom.DocumentImpl

DocumentImpl は NodeImpl のサブクラスなので、XML プロセス変数は NodeImpl の派生であると想定できます。NodeImpl のドキュメントは、[こちら](https://xerces.apache.org/xerces-j/apiDocs/org/apache/xerces/dom/NodeImpl.html)で参照できます。

**Execute Script サービスを使用したサンプル XML の作成**

次に、Execute Script サービス内での XML の作成例を以下に示します。プロセスには、XML 型の変数ノードが含まれています。このアクティビティの最終結果は、XML ドキュメントになります。このドキュメントの内容、またはプロセス全体への適用方法は、このチュートリアルの対象外です。ここでは、XML がアプリケーション全体で実行する必要がある処理を説明します。概要で説明したように、XML は JEE 上の AEM Forms のプロセスで多くの目的に使用できます。ここでは、単純な XML ドキュメントを出力するスクリプトを実行アクティビティのコーディング方法について説明します。

XML を出力する単純な Java スクリプトは次のようになります。

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
>前述の DOM オブジェクトをスクリプトに読み込む必要があります。

この単純なスクリプトの結果は、次のように変数ノードが設定された新しい XML ドキュメントになります。

```xml
<resources>

<resource id="first item id" value="first item value"/>

</resources>
```

**反復ループを使用した XML へのノードの追加**

ノードは、プロセス内の既存の XML 変数にも追加できます。変数ノードには、先ほど作成した XML オブジェクトが含まれます。

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
