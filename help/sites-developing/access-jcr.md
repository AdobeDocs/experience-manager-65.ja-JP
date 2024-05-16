---
title: AEM JCR へのプログラムからのアクセス方法
description: Adobe Experience Cloud の構成要素の AEM リポジトリ内にあるノードおよびプロパティをプログラムで変更できます
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: fe946b9a-b29e-4aa5-b973-e2a652417a55
solution: Experience Manager, Experience Manager Sites
feature: Developing,JCR
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: ht
source-wordcount: '567'
ht-degree: 100%

---

# AEM JCR へのプログラムからのアクセス方法{#how-to-programmatically-access-the-aem-jcr}

Adobe Experience の構成要素の Adobe CQ リポジトリ内にあるノードおよびプロパティをプログラムで変更できます。CQ リポジトリにアクセスするには、Java™ Content Repository（JCR）API を使用します。Java™ JCR API を使用すれば、Adobe CQ リポジトリ内にあるコンテンツに対して、作成、置換、更新および削除（CRUD）ができます。Java™ JCR API について詳しくは、[https://jackrabbit.apache.org/jcr/jcr-api.html](https://jackrabbit.apache.org/jcr/jcr-api.html) を参照してください。

>[!NOTE]
>
>この開発向けの記事では、外部 Java™ アプリケーションから Adobe CQ JCR を変更します。これに対して、OSGi バンドル内から JCR API を使用して JCR を変更することもできます。詳しくは、[Java™ コンテンツリポジトリへの CQ データの永続化](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=ja)を参照してください。

>[!NOTE]
>
>JCR API を使用するには、Java™ アプリケーションのクラスパスに `jackrabbit-standalone-2.4.0.jar` ファイルを追加します。この JAR ファイルは Java™ JCR API web ページ（[https://jackrabbit.apache.org/jcr/jcr-api.html](https://jackrabbit.apache.org/jcr/jcr-api.html)）から取得できます。

>[!NOTE]
>
>JCR Query API を使用して Adobe CQ JCR へのクエリーを実行する方法については、[JCR API を使用した Adobe Experience Manager データのクエリー](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/query-builder/querybuilder-api.html?lang=ja)を参照してください。

## リポジトリインスタンスの作成 {#create-a-repository-instance}

リポジトリに接続して接続を確立するには様々な方法がありますが、この開発向け記事では、`org.apache.jackrabbit.commons.JcrUtils` クラスに属する静的メソッドを使用します。このメソッドの名前は `getRepository` です。このメソッドは、Adobe CQ サーバーの URL を表す文字列パラメーターを受け取ります。例えば、`http://localhost:4503/crx/server` のように指定します。

次のコード例に示すように、`getRepository` メソッドは `Repository` インスタンスを返します。

```java
//Create a connection to the AEM JCR repository running on local host
Repository repository = JcrUtils.getRepository("http://localhost:4503/crx/server");
```

## Session インスタンスの作成 {#create-a-session-instance}

`Repository` インスタンスは CRX リポジトリを表します。`Repository` インスタンスを使用して、このリポジトリとのセッションを確立します。セッションを作成するには、`Repository` インスタンスの `login` メソッドを呼び出して `javax.jcr.SimpleCredentials` オブジェクトを渡します。`login` メソッドは、`javax.jcr.Session` インスタンスを返します。

`SimpleCredentials` オブジェクトを作成するには、コンストラクターを使用して、次の文字列値を渡します。

* ユーザー名
* 対応するパスワード

2 番目のパラメーターを渡す場合は、文字列オブジェクトの `toCharArray` メソッドを呼び出します。次のコードは、`javax.jcr.Sessioninstance` を返す `login` メソッドの呼び出し方法を示します。

```java
//Create a Session instance
javax.jcr.Session session = repository.login( new SimpleCredentials("admin", "admin".toCharArray()));
```

## ノードインスタンスの作成 {#create-a-node-instance}

`Session` インスタンスを使用して `javax.jcr.Node` インスタンスを作成します。`Node` インスタンスを使用すると、ノード操作を実行できます。例えば、ノードを作成できます。ルートノードを表すノードを作成するには、次のコード行のように、`Session` インスタンスの `getRootNode` メソッドを呼び出します。

```java
//Create a Node
Node root = session.getRootNode();
```

`Node` インスタンスを作成すると、別のノードを作成してそのノードに値を追加するなどのタスクを実行できます。例えば、以下のコードでは、2 つのノードを作成し、2 番目のノードに値を追加します。

```java
// Store content
Node day = adobe.addNode("day");
day.setProperty("message", "Adobe CQ is part of the Adobe Digital Marketing Suite!");
```

## ノードの値の取得 {#retrieve-node-values}

ノードとその値を取得するには、`Node` インスタンスの `getNode` メソッドを呼び出して、ノードの完全修飾パスを表す文字列値を渡します。前のコードの例で作成したノードの構造について考えてみましょう。以下のコードに示すように、「day」ノードを取得するには、「adobe/day」を指定します。

```java
// Retrieve content
Node node = root.getNode("adobe/day");
System.out.println(node.getPath());
System.out.println(node.getProperty("message").getString());
```

## Adobe CQ リポジトリ内でのノードの作成 {#create-nodes-in-the-adobe-cq-repository}

次の Java™ コードの例は、Adobe CQ に接続し、`Session` インスタンスを作成して、新しいノードを追加する Java™ クラスを表しています。ノードにデータ値が割り当てられ、ノードの値とそのパスがコンソールに書き出されます。セッションが完了したら、必ずログアウトしてください。

```java
/*
 * This Java Quick Start uses the jackrabbit-standalone-2.4.0.jar
 * file. See the previous section for the location of this JAR file
 */

import javax.jcr.Repository;
import javax.jcr.Session;
import javax.jcr.SimpleCredentials;
import javax.jcr.Node;

import org.apache.jackrabbit.commons.JcrUtils;
import org.apache.jackrabbit.core.TransientRepository;

public class GetRepository {

public static void main(String[] args) throws Exception {

try {

    //Create a connection to the CQ repository running on local host
    Repository repository = JcrUtils.getRepository("http://localhost:4503/crx/server");

   //Create a Session
   javax.jcr.Session session = repository.login( new SimpleCredentials("admin", "admin".toCharArray()));

  //Create a node that represents the root node
  Node root = session.getRootNode();

  // Store content
  Node adobe = root.addNode("adobe");
  Node day = adobe.addNode("day");
  day.setProperty("message", "Adobe CQ is part of the Adobe Digital Marketing Suite!");

  // Retrieve content
  Node node = root.getNode("adobe/day");
  System.out.println(node.getPath());
  System.out.println(node.getProperty("message").getString());

  // Save the session changes and log out
  session.save();
  session.logout();
  }
 catch(Exception e){
  e.printStackTrace();
  }
 }
}
```

このコード例全体を実行してノードを作成した後、以下の図に示すように、**[!UICONTROL CRXDE Lite]** で新しいノードを確認できます。

![chlimage_1-68](assets/chlimage_1-68a.png)
