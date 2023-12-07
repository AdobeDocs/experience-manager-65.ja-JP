---
title: Analytics 用のサーバーサイドのページネーミングの実装
description: Adobe Analyticsは、s.pageName プロパティを使用して、ページを一意に識別し、ページ用に収集されたデータを関連付けます
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 17a4e4dc-804e-44a9-9942-c37dbfc8016f
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '847'
ht-degree: 72%

---

# Analytics 用のサーバー側ページネーミングの実装{#implementing-server-side-page-naming-for-analytics}

Adobe Analytics は、`s.pageName` プロパティを使用してページを一意に識別し、そのページのために収集されたデータを関連付けます。AEM から Analytics に送信されるこのプロパティに値を割り当てるには、通常は AEM 内で次のタスクを実行します。

* Analytics クラウドサービスフレームワークを使用して、CQ 変数を Analytics の `s.pageName` プロパティにマップする（[コンポーネントデータと Adobe Analytics プロパティとのマッピング](/help/sites-administering/adobeanalytics-mapping.md)を参照）。

* ページコンポーネントを、`s.pageName` プロパティにマップする CQ 変数を含むようにデザインする（[カスタムコンポーネント用の Adobe Analytics トラッキング機能の実装](/help/sites-developing/extending-analytics-components.md)を参照）。

Analytics レポートデータをサイトコンソールとコンテンツインサイトに公開するには、各ページの `s.pageName` プロパティの値が必要です。Sites コンソールとコンテンツインサイトに `s.pageName` プロパティの値を指定するために実装した `AnalyticsPageNameProvider` インターフェイスを、AEM Analytics の Java API で定義します。お使いの `AnaltyicsPageNameProvider` サービスは、追跡のためにクライアント上で JavaScript を使用して動的に設定できるので、レポート目的でサーバー上の pageName プロパティを解決します。

## デフォルトの Analytics ページ名プロバイダーサービス {#the-default-analytics-page-name-provider-service}

これは、ページの Analytics データを取得するために使用される `s.pageName` プロパティの値を決定するデフォルトの `DefaultPageNameProvider` サービスです。このサービスは、AEM の基盤ページコンポーネント（`/libs/foundation/components/page`）と連携して動作します。このページコンポーネントは、`s.pageName` プロパティにマップされる次の CQ 変数を定義します。

* `pagedata.path`：ページのパスに設定されます。
* `pagedata.title`：ページのタイトルに設定されます。
* `pagedata.navTitle`：ページのナビゲーションのタイトルに設定されます。

`DefaultPageNameProvider` サービスは、Analytics クラウドサービスフレームワークの `s.pageName` プロパティにマッピングされる CQ 変数を決定します。その後、Analytics レポートデータの取得に使用する適切なページプロパティを決定します。

* `pagedata.path`：このサービスは `page.getPath()` を使用します

* `pagedata.title`：このサービスは `page.getTitle()` を使用します

* `pagedata.navTitle`：このサービスは `page.getNavigationTitle()` を使用します

The `page` オブジェクトが [`com.day.cq.wcm.api.Page`](https://helpx.adobe.com/jp/experience-manager/6-3/sites-developing/reference-materials/javadoc/com/day/cq/wcm/api/Page.html) ページの Java オブジェクト。

CQ 変数をフレームワークの `s.pageName` プロパティにマッピングしない場合、`s.pageName` の値はページのパスから生成されます。例えば、`/content/geometrixx/en` というパスを持つページでは、`s.pageName` に値 `content:geometrixx:en` を使用します。

>[!NOTE]
>
>DefaultPageNameProvider サービスは、サービスランキングとして 100 を使用します。

## Analytics レポートでの継続性の維持 {#maintaining-continuity-in-analytics-reporting}

ページの分析データの完全な履歴を保持するには、ページに使用される s.pageName プロパティの値が変更されない必要があります。 ただし、基盤ページコンポーネントで定義される分析プロパティは簡単に変更できます。 例えば、ページを移動すると、 `pagedata.path` とは、レポート履歴の継続性を壊します。

* 以前のパスで収集されたデータは、ページに関連付けられなくなります。
* 別のページが、別のページが 1 回使用したパスを使用している場合、そのパスのデータは異なるページに継承されます。

レポートの連続性を保証するには、`s.pageName` の値に以下の性質を持たせる必要があります。

* 一意。
* 安定しています。
* 人間が読み取り可能。

例えば、カスタムページコンポーネントに、作成者がページの一意の ID を指定するために使用するページプロパティ（`s.pageProperties` プロパティの値として使用されるもの）を含めることができます。

* ページに含まれる Analytics 変数は、ページプロパティに保存されている一意の ID の値に設定されます。
* Analytics 変数は、Analytics フレームワークの `s.pageProperties` プロパティにマッピングされます。
* AnalytcsPageNameProvider インターフェイスの実装は、このページプロパティの値を取得して、ページの Analytics データのクエリに使用します。

>[!NOTE]
>
>`s.pageName` の値について効果的な戦略を策定できるよう、Analytics のコンサルタントに相談してください。

### Analytics ページ名プロバイダーサービスの実装 {#implementing-an-analytics-page-name-provider-service}

`com.day.cq.analytics.sitecatalyst.AnalyticsPageNameProvider` インターフェイスを OSGi サービスとして実装し、`s.pageName` プロパティの値を取得するロジックをカスタマイズします。サイトページ分析およびコンテンツインサイトでは、このサービスを使用して Analytics からレポートデータを取得します。

AnalyticsPageNameProvider インターフェイスは、実装が必要な次の 2 つのメソッドを定義します。

* `getPageName`：`s.pageName` プロパティとして使用する値を表す `String` 値を返します。

* `getResource`：`s.pageName` プロパティに関連付けられたページを表す `org.apache.sling.api.resource.Resource` オブジェクトを返します。

どちらのメソッドも、`com.day.cq.analytics.sitecatalyst.AnalyticsPageNameContext` オブジェクトをパラメーターとして取ります。`AnalyticsPageNameContext` クラスは、Analytics 呼び出しのコンテキストに関する以下の情報を提供します。

* ページリソースのベースパス。
* Analytics クラウドサービス設定の `Framework` オブジェクト。
* ページの `Resource` オブジェクト。
* ページの `ResourceResolver` オブジェクト。

このクラスは、ページ名のセッターも提供します。

### AnalyticsPageNameProvider の実装例 {#example-analyticspagenameprovider-implementation}

以下に示すサンプル `AnalyticsPageNameProvider` 実装は、以下のようなカスタムページコンポーネントをサポートしています。

* 基盤ページコンポーネントを拡張したコンポーネントです。
* ダイアログボックスには、作成者が `s.pageName` プロパティの値を指定するためのフィールドが含まれます。
* プロパティの値は、ページインスタンスの `jcr:content` ノードの pageName プロパティに保存されます。
* `s.pageName` プロパティを保存する Analytics プロパティは、`pagedata.pagename` です。このプロパティは、Analytics フレームワークの `s.pageName` プロパティにマッピングされます。

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

次に示す getResource メソッドの実装は、ページの Resource オブジェクトを返します。

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

次のコードは、サービスを設定する SCR 注釈を含む、クラス全体を表しています。 サービスのランキングは 200 で、デフォルトのサービスを上書きします。

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
