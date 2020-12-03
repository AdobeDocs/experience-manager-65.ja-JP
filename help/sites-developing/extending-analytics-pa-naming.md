---
title: Analytics 用のサーバー側ページネーミングの実装
seo-title: Analytics 用のサーバー側ページネーミングの実装
description: Adobe Analytics は、s.pageName プロパティを使用してページを一意に識別し、そのページのために収集されたデータを関連付けます
seo-description: Adobe Analytics は、s.pageName プロパティを使用してページを一意に識別し、そのページのために収集されたデータを関連付けます
uuid: 37b92099-0cce-4b2d-b55c-928f636dbd7e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: be2aa297-5b78-4b1d-8ff1-e6a585a177dd
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 72%

---


# Analytics 用のサーバー側ページネーミングの実装{#implementing-server-side-page-naming-for-analytics}

Adobe Analytics は、`s.pageName` プロパティを使用してページを一意に識別し、そのページのために収集されたデータを関連付けます。AEM から Analytics に送信されるこのプロパティに値を割り当てるには、通常は AEM 内で次のタスクを実行します。

* Analytics クラウドサービスフレームワークを使用して、CQ 変数を Analytics の `s.pageName` プロパティにマップする(「[コンポーネントデータとAdobe Analyticsプロパティとのマッピング](/help/sites-administering/adobeanalytics-mapping.md)」を参照)。

* ページコンポーネントを、`s.pageName` プロパティにマップする CQ 変数を含むようにデザインする(「[カスタムコンポーネント用のAdobe Analyticsトラッキングの導入](/help/sites-developing/extending-analytics-components.md)」を参照)。

Analytics レポートデータをサイトコンソールとコンテンツインサイトに公開するには、各ページの `s.pageName` プロパティの値が必要です。AEM Analytics Java APIは、`AnalyticsPageNameProvider`プロパティの値をSitesコンソールとContent Insightsに提供するために導入する&lt;a0/>インターフェイスを定義します。 `s.pageName``AnaltyicsPageNameProvider` サービスは、レポート生成のためにサーバー上の pageName プロパティを解決します。このプロパティは、追跡のためにクライアント上で Javascript を使用して動的に設定できるからです。

## デフォルトの Analytics ページ名プロバイダーサービス {#the-default-analytics-page-name-provider-service}

`DefaultPageNameProvider`サービスは、ページのAnalyticsデータの取得に使用する`s.pageName`プロパティの値を決定するデフォルトのサービスです。 このサービスは、AEM foundationページコンポーネント(`/libs/foundation/components/page`)と連携して動作します。 このページコンポーネントは、`s.pageName` プロパティにマップされる次の CQ 変数を定義します。

* `pagedata.path`：ページのパスに設定されます。
* `pagedata.title`：ページのタイトルに設定されます。
* `pagedata.navTitle`：ページのナビゲーションのタイトルに設定されます。

`DefaultPageNameProvider`サービスは、これらのCQ変数のうちどれがAnalyticsクラウドサービスフレームワークの`s.pageName`プロパティにマッピングされるかを決定します。 その後、Analytics レポートデータの取得に使用する適切なページプロパティを決定します。

* `pagedata.path`:サービスで  `page.getPath()`

* `pagedata.title`:サービスで  `page.getTitle()`

* `pagedata.navTitle`:サービスで  `page.getNavigationTitle()`

`page`オブジェクトは、ページの[ `com.day.cq.wcm.api.Page`](https://helpx.adobe.com/experience-manager/6-3/sites-developing/reference-materials/javadoc/com/day/cq/wcm/api/Page.html) Javaオブジェクトです。

フレームワークの`s.pageName`プロパティにCQ変数をマップしない場合、`s.pageName`の値はページパスから生成されます。 例えば、パス`/content/geometrixx/en`を持つページでは、`s.pageName`に対して値`content:geometrixx:en`を使用します。

>[!NOTE]
>
>DefaultPageNameProviderサービスは、100のサービスランクを使用します。

## Analytics レポートにおける連続性の維持 {#maintaining-continuity-in-analytics-reporting}

ページの分析データに関するすべての履歴を維持するには、一度も変更されたことがないページに使用される s.pageName プロパティの値が必要です。ただし、基盤ページコンポーネントが定義する分析プロパティは簡単に変更できます。例えば、ページを移動すると `pagedata.path` の値が変更され、レポート履歴の連続性が途切れて、次のようなことが起こります。

* 前のパスで収集されたデータは、このページと関連付けられなくなります。
* 以前に他のページが使用していたパスを別のページが使用する場合は、後から使用するほうのページがそのパスのデータを継承します。

レポートの連続性を保証するには、`s.pageName` の値に以下の性質を持たせる必要があります。

* 一意性。
* 安定性。
* 人間にとっての可読性。

例えば、カスタムページコンポーネントに、作成者がページの一意の ID を指定するために使用するページプロパティ（`s.pageProperties` プロパティの値として使用されるもの）を含めることができます。

* ページに含まれる Analytics 変数は、ページプロパティに保存されている一意の ID の値に設定されます。
* analytics変数は、Analyticsフレームワークの`s.pageProperties`プロパティにマップされます。
* AnalytcsPageNameProvider インターフェイスの実装は、このページプロパティの値を取得して、ページの Analytics データのクエリに使用します。

>[!NOTE]
>
>`s.pageName` の値について効果的な戦略を策定できるよう、Analytics のコンサルタントに相談してください。

### Analytics ページ名プロバイダーサービスの実装 {#implementing-an-analytics-page-name-provider-service}

`com.day.cq.analytics.sitecatalyst.AnalyticsPageNameProvider``s.pageName` インターフェイスを OSGi サービスとして実装し、 プロパティの値を取得するロジックをカスタマイズします。サイトページ分析およびコンテンツインサイトでこのサービスを使用して、Analytics からレポートデータを取得します。

AnalyticsPageNameProvider インターフェイスで定義されている次の 2 つのメソッドを実装する必要があります。

* `getPageName`:プ `String` ロパティとして使用する値を表す `s.pageName` 値を返します。

* `getResource`:プ `org.apache.sling.api.resource.Resource` ロパティに関連付けられているページを表す `s.pageName` オブジェクトを返します。

どちらのメソッドも`com.day.cq.analytics.sitecatalyst.AnalyticsPageNameContext`オブジェクトをパラメーターとして取ります。 `AnalyticsPageNameContext` クラスは、Analytics 呼び出しのコンテキストに関する以下の情報を提供します。

* ページリソースのベースパス。
* Analytics クラウドサービス設定の `Framework` オブジェクト。
* ページの `Resource` オブジェクト。
* ページの `ResourceResolver` オブジェクト。

このクラスは、ページ名の setter も提供します。

### サンプル AnalyticsPageNameProvider 実装  {#example-analyticspagenameprovider-implementation}

以下に示すサンプル `AnalyticsPageNameProvider` 実装は、以下のようなカスタムページコンポーネントをサポートしています。

* 基盤ページコンポーネントを拡張したコンポーネントです。
* このダイアログボックスには、作成者が`s.pageName`プロパティの値を指定するために使用するフィールドが含まれます。
* プロパティの値は、ページインスタンスの `jcr:content` ノードの pageName プロパティに保存されます。
* `s.pageName` プロパティを保存する Analytics プロパティは、`pagedata.pagename` です。このプロパティは、Analyticsフレームワークの`s.pageName`プロパティにマップされます。

以下に示す `getPageName` メソッドの実装は、フレームワークのマッピングが正しく設定されていれば、pageName ノードのプロパティの値を返します。

```java
public String getPageName(AnalyticsPageNameContext context) {
        String pageName = null;

        Framework framework = context.getFramework();
        Resource resource = context.getResource();

        if (resource != null && framework != null && framework.mapsSCVariable(S_PAGE_NAME)) {
            String cqVar = framework.getMapping(S_PAGE_NAME);
            Page page = resource.adaptTo(Page.class);
            if (cqVar.equals("pagedata.pagename")) {
                pageName = page.getProperties().get("pageName",null);
            }
        }
        return pageName;
    }
```

以下に示す getResource メソッドの実装は、ページの Resource オブジェクトを返します。

```java
     public Resource getResource(AnalyticsPageNameContext context) {
        Resource res = null;

        Framework framework = context.getFramework();
        ResourceResolver resolver = context.getResourceResolver();
        String pageName = context.getPageName();
        String basePath = context.getBasePath();

        if (pageName != null && basePath != null && resolver != null
                && framework != null && framework.mapsSCVariable(S_PAGE_NAME)) {
            String cqVar = framework.getMapping(S_PAGE_NAME);
            if (cqVar.equals("pagedata.pagename")) {
             Iterator<Resource>
             hits = resolver.findResources(createQuery(pageName, basePath, "pagename"), Query.JCR_SQL2);
             if (hits.hasNext()) {
              res = hits.next();
              res = res.getParent();
             }
            }
        }
        return res;
    }

    private String createQuery(String pageName, String basePath, String propName) {
        return "SELECT * FROM [cq:PageContent] WHERE ISDESCENDANTNODE(["
                + basePath + "]) and [" + propName + "] = \"" + pageName + "\"";
    }
```

以下のコードは、サービスを設定する SCR アノテーションを含む、クラス全体を表します。デフォルトのサービスをオーバーライドするサービスランキングが 200 であることに注意してください。

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * __________________
 *
 * Copyright 2019 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and may be covered by U.S. and Foreign Patents,
 * patents in process, and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.day.cq.analytics.sitecatalyst;

import java.util.Iterator;

import javax.jcr.query.Query;

import org.apache.sling.api.resource.Resource;
import org.apache.sling.api.resource.ResourceResolver;
import org.osgi.framework.Constants;
import org.osgi.service.component.annotations.Component;

import com.day.cq.analytics.sitecatalyst.AnalyticsPageNameContext;
import com.day.cq.analytics.sitecatalyst.AnalyticsPageNameProvider;
import com.day.cq.analytics.sitecatalyst.Framework;
import com.day.cq.wcm.api.Page;

import static com.day.cq.analytics.sitecatalyst.AnalyticsPageNameContext.S_PAGE_NAME;

/**
 * Default implementation of {@link AnalyticsPageNameProvider} that resolves
 * page title, path or navTitle if mapped in {@link Framework}.
 */
@Component(
    service = { AnalyticsPageNameProvider.class },
    property = {
        Constants.SERVICE_DESCRIPTION + "=Example Page Name Resolver implementation",
        Constants.SERVICE_RANKING + ":Integer=200"
    }
)
public class ExamplePageNameProvider implements AnalyticsPageNameProvider {
    public String getPageName(AnalyticsPageNameContext context) {
        String pageName = null;

        Framework framework = context.getFramework();
        Resource resource = context.getResource();

        if (resource != null && framework != null && framework.mapsSCVariable(S_PAGE_NAME)) {
            String cqVar = framework.getMapping(S_PAGE_NAME);
            Page page = resource.adaptTo(Page.class);
            if (cqVar.equals("pagedata.path")) {
                pageName = page.getProperties().get("pageName",null);
            }
        }
        return pageName;
    }

    public Resource getResource(AnalyticsPageNameContext context) {
        Resource res = null;

        Framework framework = context.getFramework();
        ResourceResolver resolver = context.getResourceResolver();
        String pageName = context.getPageName();
        String basePath = context.getBasePath();

        if (pageName != null && basePath != null && resolver != null
                && framework != null && framework.mapsSCVariable(S_PAGE_NAME)) {
            String cqVar = framework.getMapping(S_PAGE_NAME);
            if (cqVar.equals("pagedata.pagename")) {
                Iterator<Resource>
                hits = resolver.findResources(createQuery(pageName, basePath, "pagename"), Query.JCR_SQL2);
                if (hits.hasNext()) {
                    res = hits.next();
                    res = res.getParent();
                }
            }
        }
        return res;
    }

    private String createQuery(String pageName, String basePath, String propName) {
        return "SELECT * FROM [cq:PageContent] WHERE ISDESCENDANTNODE(["
                + basePath + "]) and [" + propName + "] = \"" + pageName + "\"";
    }
}
```

