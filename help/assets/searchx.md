---
title: AEM Assetsの検索機能の拡張
description: AEM Assetsの検索機能をデフォルト以外に拡張します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# アセット検索の拡張 {#extending-assets-search}

Adobe Experience Manager(AEM)Assets検索機能を拡張できます。 AEM Assets はデフォルトで、文字列によってアセットを検索します。

検索は QueryBuilder インターフェイスを介して実行されるので、複数の述語を使用することで検索をカスタマイズできます。You can overlay the default set of predicates in the following directory: `/apps/dam/content/search/searchpanel/facets`.

AEM Assetsの管理パネルにタブを追加することもできます。

>[!CAUTION]
>
>AEM 6.4 以降、クラシック UI は廃止されます。For announcement, see [Deprecated and removed features](https://docs.adobe.com/content/help/en/experience-manager-64/release-notes/deprecated-removed-features.html). タッチ対応 UI を使用することをお勧めします。For customization, see [Search Facets](/help/assets/search-facets.md).

## オーバーレイ {#overlaying}

事前設定済みの述部をオーバーレイするには、ノードをからにコ `facets` ピーす `/libs/dam/content/search/searchpanel` るか、設定内の別の `/apps/dam/content/search/searchpanel/` プロパティを指定 `facetURL` します(デフォルトは「 `searchpanel``/libs/dam/content/search/searchpanel/facets.overlay.infinity.json`」)。

![screen_shot_2012-06-05at113619am](assets/screen_shot_2012-06-05at113619am.png)

>[!NOTE]
>
>デフォルトでは、/`apps` 配下のディレクトリ構造は存在しないので、新たに作成する必要があります。ノードのタイプが、/`libs` 配下のノードのタイプと一致するようにしてください。


## タブの追加 {#adding-tabs}

AEM Assets管理者で設定することで、追加の検索タブを追加できます。 追加のタブは以下の手順で作成します。

1. Create the folder structure `/apps/wcm/core/content/damadmin/tabs,`if it does not already exist, and copy the `tabs` node from `/libs/wcm/core/content/damadmin` and paste it.
1. 必要に応じて、2 つ目のタブを作成して設定します。

   >[!NOTE]
   >
   >When you create a second `siteadminsearchpanel`, be sure to set an `id` property in order to prevent form conflicts.

## カスタム述語の作成 {#creating-custom-predicates}

AEM Assetsには、アセット共有ページのカスタマイズに使用できる事前定義済み述語のセットが付属しています。 この方法でアセット共有をカスタマイズする方法については、[アセット共有ページの作成と設定](/help/assets/assets-finder-editor.md#creating-and-configuring-an-asset-share-page)で説明しています。

AEM 開発者は、既存の述語を使用するだけでなく、[Query Builder API](/help/sites-developing/querybuilder-api.md) を使用して独自の述語を作成することもできます。

カスタムの述語を作成するには、[ウィジェットフレームワーク](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html)に関する基本的な知識が必要です。

ベストプラクティスとしては、既存の述語をコピー後に変更することです。サンプルの述語は、**/libs/cq/search/components/predicates** にあります。

### 例：シンプルなプロパティ述語の作成 {#example-build-a-simple-property-predicate}

プロパティ述語の作成手順

1. プロジェクトディレクトリにコンポーネントフォルダーを作成します（**/apps/geometrixx/components/titlepredicate** など）。
1. 次の **content.xml** を追加します。

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Title Predicate"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Search"/>
   ```

1. ページの URL の末尾に `titlepredicate.jsp`.

   ```xml
   <%--
   
     Sample title predicate component
   
   --%><%@ page import="java.util.Calendar" %><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   
       // A unique id is necessary in case this predicate is inserted multiple times on the same page
       String elemId = "cq-predicate-" +  Long.toString(Calendar.getInstance().getTimeInMillis());
   
   %><div class="predicatebox">
   
       <div class="title">Title</div>
   
       <%-- The wrapper for the form elements. All items will be append to this wrapper. --%>
       <div id="<%= elemId %>" class="content"></div>
   
   </div><script type="text/javascript">
   
       CQ.Ext.onLoad(function() {
   
           var predicateName = "property";
           var propertyName = "jcr:content/metadata/dc:title";
           var elemId = "<%= elemId %>";
   
           // Get the page wide available QueryBuilder.
           var qb = CQ.search.Util.getQueryBuilder();
   
           // createId adds a counter to the predicate name - useful in case this predicate
           // is inserted multiple times on the same page.
           var id = qb.createId(predicateName);
   
           // Hidden field that defines the property to search for; in our case this
           // is the "dc:title" metadata. The name "property" (or "1_property", "2_property" etc.)
           // indicates the server to use the property predicate
           // (com.day.cq.search.eval.JcrPropertyPredicateEvaluator).
           qb.addField({
               "xtype": "hidden",
               "renderTo": elemId,
               "name": id,
               "value": propertyName
           });
   
           // The visible text field. The name has to be like the one of the hidden field above
           // plus the ".value" suffix.
           qb.addField({
               "xtype": "textfield",
               "renderTo": elemId,
               "name": id + ".value"
           });
   
           // Depending on the predicate additional parameters allow to configure the
           // predicate. Here we add an operation parameter to create a "like" query.
           // Again note the name set to the id and a suffix.
           qb.addField({
               "xtype": "hidden",
               "renderTo": elemId,
               "name": id + ".operation",
               "value": "like"
           });
       });
   </script>
   ```

1. コンポーネントを使用できるようにするには、それを編集可能にする必要があります。コンポーネントを編集可能にするには、CRXDE で、**cq:EditConfig** プライマリ型の **cq:editConfig** ノードを追加します。段落を削除できるように、**DELETE** という 1 つの値を持つ複数値プロパティ **cq:actions** を追加します。
1. ブラウザーを開き、サンプルページ（**press.html** など）でデザインモードに切り替えて、述語段落システムの新しいコンポーネント（「**左揃え**」など）を有効にします。

1. **編集**&#x200B;モードで、新しいコンポーネントがサイドキック（**検索**&#x200B;グループ）で使用できるようになります。「**Predicates**」列にコンポーネントを挿入し、「**Diamond**」などの検索語句を入力して、虫眼鏡アイコンをクリックして検索を開始します。

   >[!NOTE]
   >
   >検索時は、大文字と小文字の違いを含めて、語句を正確に入力してください。

### 例：シンプルなグループ述語の作成 {#example-build-a-simple-group-predicate}

グループ述語の作成手順

1. プロジェクトディレクトリにコンポーネントフォルダーを作成します（**/apps/geometrixx/components/picspredicate** など）。
1. 次の **content.xml** を追加します。

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Image Formats"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Search"/>
   ```

1. 次の **titlepredicate.jsp** を追加します。

   ```xml
   <%--
   
     Sample group predicate component
   
   --%><%@ page import="java.util.Calendar" %><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   
       // A unique id is necessary in case this predicate is inserted multiple times on the same page.
       String elemId = "cq-predicate-" +  Long.toString(Calendar.getInstance().getTimeInMillis());
   
   %><div class="predicatebox">
   
       <div class="title">Image Formats</div>
   
       <%-- The wrapper for the form elements. All items will be append to this wrapper. --%>
       <div id="<%= elemId %>" class="content"></div>
   
   </div><script type="text/javascript">
   
       CQ.Ext.onLoad(function() {
   
           var predicateName = "property";
           var propertyName = "jcr:content/metadata/dc:format";
           var elemId = "<%= elemId %>";
   
           // Get the page wide available QueryBuilder.
           var qb = CQ.search.Util.getQueryBuilder();
   
           // Create a unique group ID; will return e.g. "1_group".
           var groupId = qb.createGroupId();
   
           // Hidden field that defines the property to search for  - in our case "dc:format" -
           // and declares the group of predicates. "property" in the name ("1_group.property")
           // indicates to the server to use the "property predicate"
           // (com.day.cq.search.eval.JcrPropertyPredicateEvaluator).
           qb.addField({
               "xtype": "hidden",
               "renderTo": "<%= elemId %>",
               "name": groupId + "." + predicateName, // 1_group.property
               "value": propertyName
           });
   
           // Declare to combine the multiple values using OR.
           qb.add(new CQ.Ext.form.Hidden({
               "name": groupId + ".p.or",  // 1_group.p.or
               "value": "true"
           }));
   
           // The options
           var options = [
               { "label":"JPEG", "value":"image/jpeg"},
               { "label":"PNG",  "value":"image/png" },
               { "label":"GIF",  "value":"image/gif" }
           ];
   
           // Build a checkbox for each option.
           for (var i = 0; i < options.length; i++) {
               qb.addField({
                   "xtype": "checkbox",
                   "renderTo": "<%= elemId %>",
                   // 1_group.property.0_value, 1_group.property.1_value etc.
                   "name": groupId + "." +  predicateName + "." + i + "_value",
                   "inputValue": options[i].value,
                   "boxLabel": options[i].label,
                   "listeners": {
                       "check": function() {
                           // Submit the search form when checking/unchecking a checkbox.
                           qb.submit();
                       }
                   }
               });
           }
       });
   ```

1. コンポーネントを使用できるようにするには、それを編集可能にする必要があります。コンポーネントを編集可能にするには、CRXDE で、**cq:EditConfig** プライマリ型の **cq:editConfig** ノードを追加します。段落を削除できるように、**DELETE** という 1 つの値を持つ複数値プロパティ **cq:actions** を追加します。
1. ブラウザーを開き、サンプルページ（**press.html** など）でデザインモードに切り替えて、述語段落システムの新しいコンポーネント（「**左揃え**」など）を有効にします。
1. **編集**&#x200B;モードで、新しいコンポーネントがサイドキック（**検索**&#x200B;グループ）で使用できるようになります。「**Predicates**」列にコンポーネントを挿入します。

## インストール済みの述語ウィジェット {#installed-predicate-widgets}

次の述部は、事前設定済みのExtJSウィジェットとして使用できます。

### FulltextPredicate {#fulltextpredicate}

| プロパティ | タイプ | 説明 |
|---|---|---|
| predicateName | 文字列 | 述語の名前。デフォルト に設定`fulltext` |
| searchCallback | Function | Callback for triggering search on event `keyup`. デフォルト に設定`CQ.wcm.SiteAdmin.doSearch` |

### PropertyPredicate {#propertypredicate}

| プロパティ | タイプ | 説明 |
|---|---|---|
| predicateName | 文字列 | 述語の名前。デフォルト に設定`property` |
| propertyName | 文字列 | JCR プロパティの名前。デフォルト に設定`jcr:title` |
| defaultValue | 文字列 | 事前入力されたデフォルト値。 |

### PathPredicate {#pathpredicate}

| プロパティ | タイプ | 説明 |
|---|---|---|
| predicateName | 文字列 | 述語の名前。デフォルト に設定`path` |
| rootPath | 文字列 | 述語のルートパス。デフォルト に設定`/content/dam` |
| pathFieldPredicateName | 文字列 | デフォルト に設定`folder` |
| showFlatOption | Boolean | チェックボックスを表示するフラ `search in subfolders`グ。 デフォルトは true です |

### DatePredicate {#datepredicate}

| プロパティ | タイプ | 説明 |
|---|---|---|
| predicateName | 文字列 | 述語の名前。デフォルト に設定`daterange` |
| propertyname | 文字列 | JCR プロパティの名前。デフォルト に設定`jcr:content/jcr:lastModified` |
| defaultValue | 文字列 | 事前入力済みのデフォルト値 |

### OptionsPredicate {#optionspredicate}

| プロパティ | タイプ | 説明 |
|---|---|---|
| title | 文字列 | 最上部のタイトルを追加します |
| predicateName | 文字列 | 述語の名前。デフォルト に設定`daterange` |
| propertyname | 文字列 | JCR プロパティの名前。デフォルト に設定`jcr:content/metadata/cq:tags` |
| collapse | 文字列 | 折りたたみのレベル。デフォルト に設定`level1` |
| triggerSearch | Boolean | チェック時の検索を呼び出すためのフラグ。デフォルトは false です |
| searchCallback | Function | 検索を呼び出すためのコールバック。デフォルト に設定`CQ.wcm.SiteAdmin.doSearch` |
| searchTimeoutTime | 番号 | タイムアウト。この時間を過ぎると searchCallback が呼び出されます。デフォルトは 800ms です |

## 検索結果のカスタマイズ {#customizing-search-results}

アセット共有ページでの検索結果の表示方法は、選択したレンズによって制御されます。AEM Assets には、アセット共有ページのカスタマイズに使用できる、事前定義済みのレンズのセットが付属しています。この方法でアセット共有をカスタマイズする方法については、[アセット共有ページの作成と設定](/help/assets/assets-finder-editor.md#creating-and-configuring-an-asset-share-page)で説明しています。

AEM 開発者は、既存のレンズを使用するだけでなく、独自のレンズを作成することもできます。
