---
title: Sling アダプターの使用
description: Sling には、Adaptable インターフェイスを実装するオブジェクトを簡単に翻訳するためのアダプターパターンが用意されています
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: 6465e2c4-28e5-4fc8-8cca-7b632f10ba5a
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '2150'
ht-degree: 63%

---

# Sling アダプターの使用{#using-sling-adapters}

[Sling](https://sling.apache.org) は、[Adaptable](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) インターフェイスを実装するオブジェクトを適切に変換する[アダプターパターン](https://sling.apache.org/documentation/the-sling-engine/adapters.html)が用意されています。このインターフェイスは、オブジェクトを引数として渡されるクラスタイプに変換する汎用の [adaptTo()](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) メソッドを提供します。

例えば、リソースオブジェクトを対応するノードオブジェクトに変換するには、次の操作を実行します。

```java
Node node = resource.adaptTo(Node.class);
```

## ユースケース {#use-cases}

次のようなユースケースがあります。

* 実装用のオブジェクトの取得

  例えば、汎用の [`Resource`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/Resource.html) インターフェイスの JCR ベース実装では、基盤の JCR [`Node`](https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) にアクセスできます。

* 内部的なコンテキストオブジェクトを渡す必要があるオブジェクトのショートカット作成。

  例えば、JCR ベースの [`ResourceResolver`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/ResourceResolver.html) では、要求の [`JCR Session`](https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html) への参照を保持しています。この JCR セッションは、その要求セッションに基づいて動作する多くのオブジェクト（[`PageManager`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/PageManager.html) や [`UserManager`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/security/UserManager.html) など）を取得するために必要になります。

* サービスへのショートカット。

  稀なケース - `sling.getService()` も簡単に使用できます。

### 戻り値 Null {#null-return-value}

`adaptTo()` は null を返します。

これには、次のような様々な理由があります。

* 実装がターゲットのタイプをサポートしていない
* このケースを処理するアダプターファクトリがアクティブでない（サービスの参照が見つからないなどの理由で）
* 内部的な条件が合わなかった
* サービスを利用できない

null ケースを適切に処理することが重要です。JSP レンダリングの場合、JSP の失敗がコンテンツの一部になる場合は、JSP の失敗が許容されることがあります。

### キャッシュ {#caching}

パフォーマンスを改善する目的で、各実装では `obj.adaptTo()` 呼び出しから返されたオブジェクトを自由にキャッシュできます。`obj` が同じであれば、返されるオブジェクトも同じです。

このキャッシュ処理は、すべての `AdapterFactory` ベースのケースで実行されます。

ただし、一般的なルールはなく、オブジェクトは新しいインスタンスでも既存のインスタンスでもかまいません。つまり、どちらの動作にも依存できません。 重要なのは、特に `AdapterFactory` 内部において、このシナリオでオブジェクトが再利用可能であるということです。

### 仕組み {#how-it-works}

`Adaptable.adaptTo()` の実装には、様々な方法があります。

* オブジェクト自体による実装（このメソッド自体を実装して特定のオブジェクトにマッピングします）。
* [`AdapterFactory`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/AdapterFactory.html) を使用。これは、任意のオブジェクトをマッピングできます。

  オブジェクトは、引き続き `Adaptable` インターフェイスを実装し、[`SlingAdaptable`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/adapter/SlingAdaptable.html) を拡張する必要があります（これは、Central Adapter Manager の `adaptTo` 呼び出しを渡します）。

  これにより、`Resource` などの既存クラスの `adaptTo` メカニズムにフックを組み込むことができます。

* これら 2 つの組み合わせ。

最初のケースでは、Java™ docs に何の `adaptTo-targets` が可能かが示されます。ただし、JCR ベースのリソースなどの特定のサブクラスでは、多くの場合、これは不可能です。後者の場合、`AdapterFactory` の実装は通常、バンドルのプライベートクラスの一部なので、クライアント API で公開されず、Java™ docs にも表示されません。理論的には、[OSGi](/help/sites-deploying/configuring-osgi.md) サービスランタイムからすべての `AdapterFactory` 実装にアクセスし、「アダプタブル」（ソースとターゲット）の設定を調べることは可能ですが、相互にマッピングすることはできません。最終的には、これは内部ロジックに依存し、ドキュメントに記載する必要があります。従って、参照はこちらです。

## 参照 {#reference}

### Sling {#sling}

[**Resource**](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/Resource.html) は次の項目に適応します。

<table>
 <tbody>
  <tr>
   <td><a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">ノード</a></td>
   <td>このリソースが JCR ノードベースのリソースまたはノードを参照する JCR プロパティの場合。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Property.html">プロパティ</a></td>
   <td>このリソースが JCR プロパティベースのリソースである場合</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Item.html">項目</a></td>
   <td>このリソースが JCR ベースのリソース（ノードまたはプロパティ）の場合</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/util/Map.html">Map</a></td>
   <td>このリソースが JCR ノードベースのリソース（または値マップをサポートする他のリソース）の場合、プロパティのマップを返します</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a></td>
   <td>このリソースが JCR ノードベースのリソース（または値マップをサポートするその他のリソース）の場合、プロパティの使用しやすいマップを返します。また、<br /> <code><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/ResourceUtil.html">ResourceUtil.getValueMap(Resource)</a></code> を使用（null ケースを処理するなど）して達成できます。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/inherit/InheritanceValueMap.html">InheritanceValueMap</a></td>
   <td>の拡張 <a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a> これにより、プロパティを探す際にリソースの階層を考慮に入れることができます。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/ModifiableValueMap.html">ModifiableValueMap</a></td>
   <td>の拡張 <a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a>（そのノードのプロパティを変更できます）</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/io/InputStream.html">InputStream</a></td>
   <td>ファイルリソースのバイナリコンテンツを返します ( このリソースが JCR ノードベースのリソースで、ノードタイプが <code>nt:file</code> または <code>nt:resource</code>これがバンドルリソースの場合は、ファイルコンテンツ（このリソースがファイルシステムリソースの場合）、またはバイナリ JCR プロパティリソースのデータ。</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/net/URL.html">URL</a></td>
   <td>リソースへの URL を返します（このノードが JCR ノードベースのリソースの場合はこのノードのリポジトリ URL、このリソースがバンドルリソースの場合は jar バンドル URL、このリソースがファイルシステムリソースの場合はファイル URL）</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/io/File.html">ファイル</a></td>
   <td>このリソースがファイルシステムリソースである場合</td>
  </tr>
  <tr>
   <td><a href="https://sling.apache.org/apidocs/sling5/org/apache/sling/api/scripting/SlingScript.html">SlingScript</a></td>
   <td>このリソースが、Sling によってスクリプトエンジンが登録されているスクリプト（JSP ファイルなど）の場合</td>
  </tr>
  <tr>
   <td><a href="https://www.oracle.com/java/technologies/servlet-technology.html">サーブレット</a></td>
   <td>このリソースが、Sling によってスクリプトエンジンが登録されているスクリプト（JSP ファイルなど）である場合、またはこのリソースがサーブレットリソースである場合。</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/String.html">String</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Boolean.html">Boolean</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Long.html">Long</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Double.html">Double</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/util/Calendar.html">Calendar</a><br /> <a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Value.html">Value</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/String.html">String[]</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Boolean.html">Boolean[]</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Long.html">Long[]</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/util/Calendar.html">Calendar[]</a><br /> <a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Value.html">Value[]</a></td>
   <td>このリソースが JCR プロパティベースのリソースである（および値が適合する）場合、値を返します。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
   <td>このリソースが JCR ノードベースのリソースである場合</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/Page.html">ページ</a></td>
   <td>このリソースが JCR ノードベースのリソースで、ノードが <code>cq:Page</code> ( または <code>cq:PseudoPage</code>)</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/components/Component.html">コンポーネント</a></td>
   <td>これが <code>cq:Component</code> ノードリソース</td>
  </tr>  
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/designer/Design.html">デザイン</a></td>
   <td>このノードが設計ノード (<code>cq:Page</code>)</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/Template.html">テンプレート</a></td>
   <td>これが <code>cq:Template</code> ノードリソース</td>
  </tr>  
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/api/Blueprint.html">ブループリント</a></td>
   <td>これが <code>cq:Template</code> ノードリソース</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/dam/api/Asset.html">アセット</a></td>
   <td>このリソースが dam:Asset ノードリソースである場合</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/dam/api/Rendition.html">Rendition</a></td>
   <td>このリソースが dam:Asset レンディション（dam:Assert の rendition フォルダー以下にある nt:file）である場合。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/tagging/Tag.html">タグ</a></td>
   <td>これが <code>cq:Tag</code> ノードリソース</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/security/UserManager.html">UserManager</a></td>
   <td>このリソースが JCR ベースのリソースであり、ユーザーが UserManager へのアクセス権限を持っている場合の、JCR セッションに基づく</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">Authorizable</a></td>
   <td>Authorizable は、User と Group の共通の基本インターフェイスです</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/jackrabbit/api/security/user/User.html">User</a></td>
   <td>User は、認証済みであり、別のユーザーとして実行可能な特別な Authorizable です。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/search/SimpleSearch.html">SimpleSearch</a></td>
   <td>このリソースが JCR ベースのリソースである場合は、リソース以下で検索します ( または setSearchIn() を使用します )。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/workflow/status/WorkflowStatus.html">WorkflowStatus</a></td>
   <td>特定のページまたはワークフローのペイロードノード用のワークフローステータス</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/replication/ReplicationStatus.html">ReplicationStatus</a></td>
   <td>特定のリソースまたはその jcr:content サブノード（最初にチェックされたもの）のレプリケーションステータス</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/connector/ConnectorResource.html">ConnectorResource</a></td>
   <td>このリソースが JCR ノードベースのリソースである場合、特定のタイプに対する適応後のコネクタリソースを返します。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/contentsync/config/package-summary.html">Config</a></td>
   <td>これが <code>cq:ContentSyncConfig</code> ノードリソース</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/contentsync/config/package-summary.html">ConfigEntry</a></td>
   <td>これが以下の場合、 <code>cq:ContentSyncConfig</code> ノードリソース</td>
  </tr>
 </tbody>
</table>

[**ResourceResolver**](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/ResourceResolver.html) は次の項目に適応します。

<table>
 <tbody>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html">Session</a></td>
   <td>このリソースリゾルバーが JCR ベースのリソースリゾルバー（デフォルト）の場合の、要求の JCR セッション</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/PageManager.html">PageManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/components/ComponentManager.html">ComponentManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/designer/Designer.html">デザイナー</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/dam/api/AssetManager.html">AssetManager</a></td>
   <td>このリソースリゾルバーが JCR ベースのリソースリゾルバーである場合の、JCR セッションに基づく</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/tagging/TagManager.html">TagManager</a></td>
   <td>このリソースリゾルバーが JCR ベースのリソースリゾルバーである場合の、JCR セッションに基づく</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/jackrabbit/api/security/user/UserManager.html">UserManager</a></td>
   <td>UserManager は、認証可能なオブジェクト（ユーザーおよびグループ）へのアクセス権と手段を提供します。 UserManager は特定のセッションにバインドされています
   </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">Authorizable</a> </td>
   <td>現在のユーザー</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/jackrabbit/api/security/user/User.html">ユーザー</a><br /> </td>
   <td>現在のユーザー</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/search/QueryBuilder.html">QueryBuilder</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/Externalizer.html">Externalizer</a></td>
   <td>リクエストオブジェクトがない場合でも、絶対 URL を外部化するためのもの<br /> </td>
  </tr>
 </tbody>
</table>

[**SlingHttpServletRequest**](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/SlingHttpServletRequest.html) は次の項目に適応します。

現時点ではターゲットはありませんが、Adaptable を実装し、カスタムの AdapterFactory 内でソースとして使用することは可能です。

[**SlingHttpServletResponse**](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/SlingHttpServletResponse.html) は次の項目に適応します。

<table>
 <tbody>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/org/xml/sax/ContentHandler.html">ContentHandler</a><br />（XML）</td>
   <td>これが Sling リライター応答の場合</td>
  </tr>
 </tbody>
</table>

#### WCM {#wcm}

**[Page](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/Page.html)** は次の項目に適応します。

<table>
 <tbody>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/Resource.html">Resource</a><br /> </td>
   <td>ページのリソース</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
   <td>ラベル付きリソース (== this)</td>
  </tr>
  <tr>
   <td><a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">ノード</a></td>
   <td>ページのノード</td>
  </tr>
  <tr>
   <td>...</td>
   <td>ページのリソースが適応可能なすべての項目</td>
  </tr>
 </tbody>
</table>

**[Component](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/components/Component.html)** は次の項目に適応します。

| [Resource](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/Resource.html) | コンポーネントのリソース。 |
|---|---|
| [LabeledResource](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/LabeledResource.html) | ラベル付きリソース（== this）。 |
| [Node](https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | コンポーネントのノード。 |
| ... | コンポーネントのリソースが適応できるすべての項目。 |

**[Template](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/Template.html)** は次の項目に適応します。

<table>
 <tbody>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/Resource.html">Resource</a><a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html"><br /> </a></td>
   <td>テンプレートのリソース</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
   <td>ラベル付きリソース (== this)</td>
  </tr>
  <tr>
   <td><a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">ノード</a></td>
   <td>このテンプレートのノード</td>
  </tr>
  <tr>
   <td>...</td>
   <td>テンプレートのリソースが適応できるすべての項目。</td>
  </tr>
 </tbody>
</table>

#### セキュリティ {#security}

**Authorizable**、 **User および **グループ化** 次の項目に適応します。

| [Node](https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | ユーザーまたはグループのホームノードを返します。 |
|---|---|
| [ReplicationStatus](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/replication/ReplicationStatus.html) | ユーザーまたはグループのホームノードのレプリケーションステータスを返します。 |

#### DAM {#dam}

**Asset** は次の項目に適応します。

| [Resource](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/Resource.html) | アセットのリソース。 |
|---|---|
| [Node](https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | アセットのノード。 |
| ... | アセットのリソースが適応できるすべての項目。 |

#### タグ付け {#tagging}

**Tag** は次の項目に適応します。

| [Resource](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/Resource.html) | タグのリソース。 |
|---|---|
| [Node](https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | タグのノード。 |
| ... | タグのリソースが適応できるすべての項目。 |

#### その他 {#other}

さらに、Sling、JCR、OCM では、カスタム OCM（[オブジェクトとコンテンツのマッピング](https://jackrabbit.apache.org/jcr/object-content-mapping.html)）オブジェクト用の ` [AdapterFactory](https://sling.apache.org/site/adapters.html#Adapters-AdapterFactory)` も提供しています。
