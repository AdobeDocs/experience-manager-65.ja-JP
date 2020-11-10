---
title: 検索機能を拡張。
description: 検索機能をデフォルト以 [!DNL Adobe Experience Manager Assets] 外にも拡張できます。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 12c56c27c7f97f1029c757ec6d28f482516149d0
workflow-type: tm+mt
source-wordcount: '838'
ht-degree: 77%

---


# Assets の検索機能の拡張 {#extending-assets-search}

You can extend [!DNL Adobe Experience Manager Assets] search capabilities. Out of the box, [!DNL Experience Manager Assets] searches for assets by strings.

検索は QueryBuilder インターフェイスを介して実行されるので、複数の述語を使用して検索をカスタマイズできます。`/apps/dam/content/search/searchpanel/facets` ディレクトリにあるデフォルトの述語セットをオーバーレイできます。

You can also add additional tabs to the [!DNL Assets] admin panel.

>[!CAUTION]
>
>As of [!DNL Experience Manager] 6.4, Classic UI is deprecated. For announcement, see [deprecated and removed features](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/deprecated-removed-features.html). Adobeでは、タッチ対応UIの使用をお勧めします。 For customization, see [search facets](/help/assets/search-facets.md).

## オーバーレイ {#overlaying}

To overlay the pre-configured predicates, copy the `facets` node from `/libs/dam/content/search/searchpanel` to `/apps/dam/content/search/searchpanel/` or specify another `facetURL` property in the `searchpanel` configuration (the default is to `/libs/dam/content/search/searchpanel/facets.overlay.infinity.json`).

![screen_shot_2012-06-05at113619am](assets/screen_shot_2012-06-05at113619am.png)

>[!NOTE]
>
>デフォルトでは、の下のディレクトリ構造 `/apps` は存在しないので作成します。 ノードのタイプが、`/libs` 配下のノードのタイプと一致するようにしてください。

## タブの追加 {#adding-tabs}

You can add additional search tabs by configuring them in the [!DNL Assets] admin interface. 追加のタブは以下の手順で作成します。

1. フォルダー構造 `/apps/wcm/core/content/damadmin/tabs,` がまだ存在しない場合は作成し、`tabs` ノードを `/libs/wcm/core/content/damadmin` からコピーして貼り付けます。
1. 必要に応じて、2 つ目のタブを作成し設定します。

   >[!NOTE]
   >
   >2 つ目の `siteadminsearchpanel` を作成する場合は、フォームの競合を避けるために `id` プロパティを必ず設定してください。

## カスタム述語の作成 {#creating-custom-predicates}

[!DNL Assets] には、アセット共有ページのカスタマイズに使用できる、事前定義済みの一連の述語が付属しています。Customizing an Asset Share in this way is covered in [create and configure an Asset Share page](/help/assets/assets-finder-editor.md#creating-and-configuring-an-asset-share-page).

In addition to using pre-existing predicates, [!DNL Experience Manager] developers can also create their own predicates using the [Query Builder API](/help/sites-developing/querybuilder-api.md).

カスタム述語を作成するには、[ウィジェットフレームワーク](https://helpx.adobe.com/jp/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html)に関する基本的な知識が必要です。

ベストプラクティスは、既存の述語をコピー後に変更することです。サンプルの述語は、**/libs/cq/search/components/predicates** にあります。

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

1. 次の `titlepredicate.jsp`.を追加します。

   ```java
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

1. コンポーネントを使用できるようにするには、コンポーネントを編集可能にする必要があります。コンポーネントを編集可能にするには、CRXDE で、**cq:EditConfig** プライマリ型の **cq:editConfig** ノードを追加します。段落を削除できるよう、値を複数設定できるプロパティ **cq:actions** を追加し、値として **DELETE** のみを設定します。
1. ブラウザーを開き、サンプルページ（**press.html** など）でデザインモードに切り替えて、述語段落システムの新しいコンポーネント（「**左揃え**」など）を有効にします。

1. **編集**&#x200B;モードでは、新しいコンポーネントがサイドキックで使用できるようになります（**検索**&#x200B;グループ内）。「**Predicates**」列にコンポーネントを挿入し、「**Diamond**」などの検索語句を入力して、虫眼鏡アイコンをクリックして検索を開始します。

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

   ```java
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

1. コンポーネントを使用できるようにするには、コンポーネントを編集可能にする必要があります。コンポーネントを編集可能にするには、CRXDE で、**cq:EditConfig** プライマリ型の **cq:editConfig** ノードを追加します。段落を削除できるよう、値を複数設定できるプロパティ **cq:actions** を追加し、値として **DELETE** のみを設定します。
1. ブラウザーを開き、サンプルページ（**press.html** など）でデザインモードに切り替えて、述語段落システムの新しいコンポーネント（「**左揃え**」など）を有効にします。
1. **編集**&#x200B;モードでは、新しいコンポーネントがサイドキックで使用できるようになります（**検索**&#x200B;グループ内）。「**Predicates**」列にコンポーネントを挿入します。

## インストール済みの述語ウィジェット {#installed-predicate-widgets}

次の述部は、事前設定済みのExtJSウィジェットとして使用できます。

### FulltextPredicate {#fulltextpredicate}

| プロパティ | 型 | 説明 |
|---|---|---|
| predicateName | String | 述語の名前。デフォルト に設定`fulltext` |
| searchCallback | Function | Callback for triggering search on event `keyup`. デフォルト に設定`CQ.wcm.SiteAdmin.doSearch` |

### PropertyPredicate {#propertypredicate}

| プロパティ | 型 | 説明 |
|---|---|---|
| predicateName | String | 述語の名前。デフォルト に設定`property` |
| propertyName | String | JCR プロパティの名前。デフォルト に設定`jcr:title` |
| defaultValue | String | 事前入力されたデフォルト値。 |

### PathPredicate {#pathpredicate}

| プロパティ | 型 | 説明 |
|---|---|---|
| predicateName | String | 述語の名前。デフォルト に設定`path` |
| rootPath | String | 述語のルートパス。デフォルト に設定`/content/dam` |
| pathFieldPredicateName | String | デフォルト に設定`folder` |
| showFlatOption | Boolean | チェックボックスを表示するフラグ `search in subfolders`。 デフォルトは true です |

### DatePredicate {#datepredicate}

| プロパティ | 型 | 説明 |
|---|---|---|
| predicateName | String | 述語の名前。デフォルト に設定`daterange` |
| propertyname | String | JCR プロパティの名前。デフォルト に設定`jcr:content/jcr:lastModified` |
| defaultValue | String | 事前入力されたデフォルト値 |

### OptionsPredicate {#optionspredicate}

| プロパティ | 型 | 説明 |
|---|---|---|
| title | String | 最上部のタイトルを追加します |
| predicateName | String | 述語の名前。デフォルト に設定`daterange` |
| propertyname | String | JCR プロパティの名前。デフォルト に設定`jcr:content/metadata/cq:tags` |
| collapse | String | 折りたたみのレベル。デフォルト に設定`level1` |
| triggerSearch | Boolean | チェック時の検索を呼び出すためのフラグ。デフォルトは false です |
| searchCallback | Function | 検索を呼び出すためのコールバック。デフォルト に設定`CQ.wcm.SiteAdmin.doSearch` |
| searchTimeoutTime | Number | タイムアウト。この時間を過ぎると searchCallback が呼び出されます。デフォルトは 800ms です |

## 検索結果のカスタマイズ {#customizing-search-results}

アセット共有ページでの検索結果の表示方法は、選択したレンズによって制御されます。[!DNL Experience Manager Assets] には、アセット共有ページのカスタマイズに使用できる、事前定義済みのレンズのセットが付属しています。この方法でアセット共有をカスタマイズする方法については、[アセット共有ページの作成と設定](/help/assets/assets-finder-editor.md#creating-and-configuring-an-asset-share-page)で説明しています。

In addition to using pre-existing lenses, [!DNL Experience Manager] developers can also create their own lenses.
