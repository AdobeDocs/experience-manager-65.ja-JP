---
title: Query Builder 用のカスタム述語エバリュエーターの実装
seo-title: Query Builder 用のカスタム述語エバリュエーターの実装
description: Query Builder を使用すると、コンテンツリポジトリへのクエリを簡単に実行できます
seo-description: Query Builder を使用すると、コンテンツリポジトリへのクエリを簡単に実行できます
uuid: e71be518-027c-4792-9e02-06405804d9d2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: ef253905-87da-4fa2-9f6c-778f1b12bd58
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 73%

---


# Query Builder 用のカスタム述語エバリュエーターの実装{#implementing-a-custom-predicate-evaluator-for-the-query-builder}

ここでは、カスタム述語エバリュエーターを実装して、[Query Builder](/help/sites-developing/querybuilder-api.md) を拡張する方法について説明します。

## 概要 {#overview}

[Query Builder](/help/sites-developing/querybuilder-api.md) を使用すると、コンテンツリポジトリへのクエリを簡単に実行できます。CQ には、データの処理に役立つ一連の述語エバリュエーターが付属しています。

しかし、カスタム述語エバリュエーターを実装することによって、複雑さを軽減し、セマンティックを向上させて、クエリを単純化することができます。

他にも、カスタム述語では、以下のような XPath では直接実行できないことも実行できます。

* 何らかのサービスの何らかのデータの検索
* 計算に基づくカスタムフィルタリング

>[!NOTE]
>
>カスタム述語を実装する際は、パフォーマンスの問題を考慮する必要があります。

>[!NOTE]
>
>クエリの例については、[Query Builder](/help/sites-developing/querybuilder-api.md) の節を参照してください。

GitHub のコード

このページのコードは GitHub にあります

* [GitHubでaem-search-custom-predicate-evaluatorプロジェクトを開きます](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator)
* プロジェクトを [ZIP ファイル](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/archive/master.zip)としてダウンロードします

### 述語エバリュエーターの詳細 {#predicate-evaluator-in-detail}

述語エバリュエーターは、クエリの制約を定義する特定の述語を評価します。

特定の JCR クエリに対する高度な検索制約（&quot;width > 200&quot; など）を、実際のコンテンツモデルに合わせてマッピングします（例：metadata/@width > 200）。ノードを手動でフィルタリングして、制約をチェックすることもできます。

>[!NOTE]
>
>`PredicateEvaluator` および `com.day.cq.search` パッケージについて詳しくは、[Java のドキュメント](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/search/package-summary.html)を参照してください。

### レプリケーションメタデータ用のカスタム述語エバリュエーターの実装 {#implementing-a-custom-predicate-evaluator-for-replication-metadata}

例として、レプリケーション・メタデータに基づくデータを支援するカスタム述語評価基準を作成する方法を説明します。

* `cq:lastReplicated`：最終レプリケーションアクションの日付を格納

* `cq:lastReplicatedBy`：最終レプリケーションアクションを呼び出したユーザーの ID を格納

* `cq:lastReplicationAction`：最終レプリケーションアクション（アクティベート、アクティベート解除など）を格納

#### デフォルトの述語エバリュエーターを使用したレプリケーションメタデータのクエリ {#querying-replication-metadata-with-default-predicate-evaluators}

The following query fetches the list of nodes in `/content` branch that have been activated by `admin` since the beginning of the year.

```xml
path=/content

1_property=cq:lastReplicatedBy
1_property.value=admin

2_property=cq:lastReplicationAction
2_property.value=Activate

daterange.property=cq:lastReplicated
daterange.lowerBound=2013-01-01T00:00:00.000+01:00
daterange.lowerOperation=>=
```

このクエリは有効ですが、解読しにくく、3 つのレプリケーションプロパティ間の関係が一目ではわかりません。カスタム述語エバリュエーターを実装すると、複雑さが軽減され、このクエリのわかりやすさが向上します。

#### 目的 {#objectives}

`ReplicationPredicateEvaluator` の目的は、以下のような構文を使用して上記のクエリをサポートすることです。

```xml
path=/content

replic.by=admin
replic.since=2013-01-01T00:00:00.000+01:00
replic.action=Activate
```

レプリケーションメタデータ述語をカスタム述語評価子でグループ化すると、意味のあるクエリを作成するのに役立ちます。

#### Maven 依存関係の更新 {#updating-maven-dependencies}

>[!NOTE]
>
>Maven を使用した新しい AEM プロジェクトの設定については、[Apache Maven を使用した AEM プロジェクトの構築方法](/help/sites-developing/ht-projects-maven.md)で説明されています。

まず、プロジェクトの Maven 依存関係を更新する必要があります。`PredicateEvaluator` は `cq-search` アーティファクトの一部なので、Maven の pom ファイルに追加する必要があります。

>[!NOTE]
>
>The scope of the `cq-search` dependency is set to `provided` because `cq-search` will be provided by the `OSGi` container.

pom.xml

The following snippet shows the differences, in [unified diff format](https://ja.wikipedia.org/wiki/Diff#.E3.83.A6.E3.83.8B.E3.83.95.E3.82.A1.E3.82.A4.E3.83.89.E5.BD.A2.E5.BC.8F_.28Unified_format.29)

```
@@ -120,6 +120,12 @@
             <scope>provided</scope>
         <dependency>
+            <groupid>com.day.cq</groupid>
+            <artifactid>cq-search</artifactid>
+            <version>5.6.4</version>
+            <scope>provided</scope>
+        </dependency>
+        <dependency>
             <groupid>junit</groupid>
             <artifactid>junit</artifactid>
             <version>3.8.1</version></dependency>
```

[aem-search-custom-predicate-evaluator](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator)- [pom.xml](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/raw/7aed6b35b4c8dd3655296e1b10cf40c0dd1eaa61/pom.xml)

#### ReplicationPredicateEvaluator の作成 {#writing-the-replicationpredicateevaluator}

The `cq-search` project contains the `AbstractPredicateEvaluator` abstract class. This can be extended with a few steps to implement your own custom predicate evaluator `(PredicateEvaluator`).

>[!NOTE]
>
>次の手順では、データをフィルタリングする `Xpath` 式を作成する方法について説明します。Another option would be to implement the `includes` method that selects data on a row basis. 詳しくは、[Java のドキュメント](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/PredicateEvaluator.html#includes28comdaycqsearchpredicatejavaxjcrqueryrowcomdaycqsearchevalevaluationcontext29)を参照してください。

1. `com.day.cq.search.eval.AbstractPredicateEvaluator` を拡張する新しい Java クラスを作成します。
1. Annotate your class with a `@Component` like the following

   src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java

   The following snippet shows the differences, in [unified diff format](https://ja.wikipedia.org/wiki/Diff#.E3.83.A6.E3.83.8B.E3.83.95.E3.82.A1.E3.82.A4.E3.83.89.E5.BD.A2.E5.BC.8F_.28Unified_format.29)

```
@@ -19,8 +19,11 @@
  */
 package com.adobe.aem.docs.search;

+import org.apache.felix.scr.annotations.Component;
+
 import com.day.cq.search.eval.AbstractPredicateEvaluator;

+@Component(metatype = false, factory = "com.day.cq.search.eval.PredicateEvaluator/repli")
 public class ReplicationPredicateEvaluator extends AbstractPredicateEvaluator {

 }
```

[aem-search-custom-predicate-evaluator](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator)- [src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/raw/ec70fac35fbd0d132e00c6066a204804e9cbe70f/src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java)

>[!NOTE]
>
>The `factory`must be a unique string starting with `com.day.cq.search.eval.PredicateEvaluator/`and ending with the name of your custom `PredicateEvaluator`.

>[!NOTE]
>
>`PredicateEvaluator` の名前は述語名で、クエリを組み立てる際に使用されます。

1. オーバーライド：

   ```java
   public String getXPathExpression(Predicate predicate, EvaluationContext context)
   ```

   オーバーライドメソッドでは、引数に指定された `Xpath` に基づいて `Predicate` 式を組み立てます。

### レプリケーションメタデータ用のカスタム述語エバリュエーターの例 {#example-of-a-custom-predicate-evalutor-for-replication-metadata}

この `PredicateEvaluator` の完全な実装は、次のクラスのようになります。

src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java

```
/*
 * #%L
 * aem-docs-custom-predicate-evaluator
 * %%
 * Copyright (C) 2013 Adobe Research
 * %%
 * Licensed under the Apache License, Version 2.0 (the "License");
 * you may not use this file except in compliance with the License.
 * You may obtain a copy of the License at
 *
 *      http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 * #L%
 */

package com.adobe.aem.docs.search;

import org.apache.felix.scr.annotations.Component;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.day.cq.search.Predicate;
import com.day.cq.search.eval.AbstractPredicateEvaluator;
import com.day.cq.search.eval.EvaluationContext;

@Component(metatype = false, factory = "com.day.cq.search.eval.PredicateEvaluator/repli")

public class ReplicationPredicateEvaluator extends AbstractPredicateEvaluator {

    static final String PE_NAME = "replic";


    static final String PN_LAST_REPLICATED_BY = "cq:lastReplicatedBy";
    static final String PN_LAST_REPLICATED = "cq:lastReplicated";
    static final String PN_LAST_REPLICATED_ACTION = "cq:lastReplicationAction";

    static final String PREDICATE_BY = "by";
    static final String PREDICATE_SINCE = "since";
    static final String PREDICATE_SINCE_OP = " >= ";
    static final String PREDICATE_ACTION = "action";

    Logger log = LoggerFactory.getLogger(getClass());

    /**
     * Returns a XPath expression filtering by replication metadata.
     *
     * @see com.day.cq.search.eval.AbstractPredicateEvaluator#getXPathExpression(com.day.cq.search.Predicate,
     *      com.day.cq.search.eval.EvaluationContext)
     */

    @Override

    public String getXPathExpression(Predicate predicate,
            EvaluationContext context) {

        log.debug("predicate {}", predicate);

        String date = predicate.get(PREDICATE_SINCE);
        String user = predicate.get(PREDICATE_BY);
        String action = predicate.get(PREDICATE_ACTION);

        StringBuilder sb = new StringBuilder();

        if (date != null) {

            sb.append(PN_LAST_REPLICATED).append(PREDICATE_SINCE_OP);
            sb.append("xs:dateTime('").append(date).append("')");

        }

        if (user != null) {

            addAndOperator(sb);
            sb.append(PN_LAST_REPLICATED_BY);
            sb.append("='").append(user).append("'");

        }

        if (action != null) {

            addAndOperator(sb);
            sb.append(PN_LAST_REPLICATED_ACTION);
            sb.append("='").append(action).append("'");

        }

        String xpath = sb.toString();

        log.debug("xpath **{}**", xpath);

        return xpath;

    }

    /**
     * Add an and operator if the builder is not empty.
     *
     * @param sb a {@link StringBuilder} containing the query under construction
     */

    private void addAndOperator(StringBuilder sb) {

        if (sb.length() != 0) {

            sb.append(" and ");

        }

    }

}
```

[aem-search-custom-predicate-evaluator](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator)- [src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/blob/master/src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java)
