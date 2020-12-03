---
title: タグライブラリ
seo-title: タグライブラリ
description: Granite、CQ および Sling のタグライブラリを使用すると、テンプレートやコンポーネントの JSP スクリプトで使用する特定の機能にアクセスできます
seo-description: Granite、CQ および Sling のタグライブラリを使用すると、テンプレートやコンポーネントの JSP スクリプトで使用する特定の機能にアクセスできます
uuid: e622d47b-cfb3-4b4a-b8e3-e1adee294219
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 6678e3c3-fb0f-4300-8838-38f23f14db07
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379
workflow-type: tm+mt
source-wordcount: '2487'
ht-degree: 62%

---


# タグライブラリ{#tag-libraries}

Granite、CQ および Sling のタグライブラリを使用すると、テンプレートやコンポーネントの JSP スクリプトで使用する特定の機能にアクセスできます。

## Granite タグライブラリ  {#granite-tag-library}

Granite タグライブラリには便利な機能が用意されています。

Granite UI コンポーネントの jsp スクリプトを開発する場合は、スクリプトの先頭に次のコードをインクルードすることをお勧めします。

```xml
<%@include file="/libs/granite/ui/global.jsp"%>
```

global では、[Sling ライブラリ](/help/sites-developing/taglib.md#sling-tag-library)も宣言します。

```xml
<%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling" %>
```

### <ui:includeClientLib> {#ui-includeclientlib}

`<ui:includeClientLib>`タグには、AEM htmlクライアントライブラリが含まれます。このライブラリは、js、css、またはテーマライブラリにすることができます。 jsやcssなど、異なるタイプの複数の挿入タグの場合は、このタグをJSPで複数回使用する必要があります。 このタグは、` [com.adobe.granite.ui.clientlibs.HtmlLibraryManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/ui/clientlibs/HtmlLibraryManager.html)` サービスインターフェイスを囲む便利なラッパーです。

このタグの属性を以下に示します。

**カテゴリ**  — カンマ区切りのクライアントライブラリカテゴリのリスト。指定したカテゴリの JavaScript ライブラリと CSS ライブラリがすべてインクルードされます。テーマ名は要求から抽出されます。

等価な式: `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeIncludes`

**テーマ**  — カンマ区切りのクライアントライブラリカテゴリのリスト。指定したカテゴリのテーマに関連するライブラリ（CSS と JS の両方）がすべてインクルードされます。テーマ名は要求から抽出されます。

等価な式: `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeThemeInclude`

**js**  — カンマで区切られたクライアントライブラリカテゴリのリスト。指定したカテゴリの JavaScript ライブラリがすべてインクルードされます。

等価な式: `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeJsInclude`

**css**  — カンマで区切られたクライアントライブラリカテゴリのリスト。指定したカテゴリの CSS ライブラリがすべてインクルードされます。

等価な式: `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeCssInclude`

**themed**  — 主題設定されたライブラリまたは主題設定されていないライブラリのみを示すフラグを含めます。省略すると、どちらのライブラリもインクルードされます。純粋な JS または CSS のインクルードにのみ適用します（カテゴリまたはテーマのインクルードには適用されません）。

`<ui:includeClientLib>`タグは、JSPで次のように使用できます。

```xml
<%-- all: js + theme (theme-js + css) --%>
<ui:includeClientLib categories="cq.wcm.edit" />

<%-- only js libs --%>
<ui:includeClientLib js="cq.collab.calendar, cq.security" />

<%-- theme only (theme-js + css) --%>
<ui:includeClientLib theme="cq.collab.calendar, cq.security" />

<%-- css only --%>
<ui:includeClientLib css="cq.collab.calendar, cq.security" />
```

## CQ タグライブラリ {#cq-tag-library}

CQ タグライブラリには便利な機能が用意されています。

スクリプトで CQ タグライブラリを使用するには、スクリプトを次のコードで開始する必要があります。

```xml
<%@taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %>
```

>[!NOTE]
>
>`/libs/foundation/global.jsp`ファイルがスクリプトに含まれると、taglibが自動的に宣言されます。

AEM コンポーネントの jsp スクリプトを開発する場合は、スクリプトの先頭に次のコードをインクルードすることをお勧めします。

```xml
<%@include file="/libs/foundation/global.jsp"%>
```

sling、CQ、jstl taglibを宣言し、[ `<cq:defineObjects />`](#amp-lt-cq-defineobjects)タグで定義されている、定期的に使用されるスクリプティングオブジェクトを公開します。 これにより、コンポーネントの jsp コードが短縮および簡略化されます。

### <cq:text> {#cq-text}

`<cq:text>`タグは、JSP内のコンポーネントテキストを出力する便利なタグです。

このタグのオプションの属性を以下に示します。

**property**  — 使用するプロパティの名前。この名前は現在のリソースを基準とした相対名です。

**value**  — 出力に使用する値。この属性が存在する場合は、property 属性の使用が上書きされます。

**oldValue** - diff出力に使用する値。この属性が存在する場合は、property 属性の使用が上書きされます。

**escapeXml**  — 結果の文字列内の文字 &lt;>、&amp;、&#39;、&#39;を、対応する文字エンティティコードに変換するかどうかを定義します。デフォルト値は false です。オプションの書式設定の後はエスケープが適用されます。

**format**  — オプションのjava.text.Format。テキストの書式設定に使用します。

**noDiff**  - diff情報が存在する場合でも、diff出力の計算を省略します。

**tagClass**  — 空でない出力を囲む要素のCSSクラス名。空の場合は、要素が追加されません。

**tagName**  — 空でない出力を囲む要素の名前。デフォルト値は DIV です。

**placeholder**  — 編集モードでnullまたは空のテキスト（プレースホルダーなど）に使用するデフォルト値。オプションの書式設定およびエスケープの後にデフォルトチェックが実行され、そのまま出力に書き込まれます。デフォルト値は次のとおりです。

`<div><span class="cq-text-placeholder">&para;</span></div>`

**default** -nullまたは空のテキストに使用するデフォルト値。オプションの書式設定およびエスケープの後にデフォルトチェックが実行され、そのまま出力に書き込まれます。

`<cq:text>`タグをJSPで使用する例をいくつか示します。

```xml
<cq:text property="jcr:title" tagName="h2"/>
<cq:text property="jcr:description" tagName="p"/>

<cq:text value="<%= listItem.getTitle() %>" tagName="h4" placeholder="" />
<cq:text value="<%= listItem.getDescription() %>" tagName="p" placeholder=""/>

<cq:text property="jcr:title" value="<%= title %>" tagName="h3"/><%
    } else if (type.equals("link")) {
        %><cq:text property="jcr:title" value="<%= "\u00bb " + title %>" tagName="p" tagClass="link"/><%
    } else if (type.equals("extralarge")) {
        %><cq:text property="jcr:title" value="<%= title %>" tagName="h1"/><%
    } else {
        %><cq:text property="jcr:title" value="<%= title %>" tagName="h2"/><%

<cq:text property="jcr:description" placeholder="" tagName="small"/>

<cq:text property="tableData"
               escapeXml="false"
               placeholder="<img src=\"/libs/cq/ui/resources/0.gif\" class=\"cq-table-placeholder\" alt=\"\">"
    />

<cq:text property="text"/>

<cq:text property="image/jcr:description" placeholder="" tagName="small"/>
<cq:text property="text" tagClass="text"/>
```

### <cq:setContentBundle> {#cq-setcontentbundle}

`<cq:setContentBundle>`タグは、i18nローカライゼーションコンテキストを作成し、`javax.servlet.jsp.jstl.fmt.localizationContext`設定変数に保存します。

このタグの属性を以下に示します。

**language**  — リソースバンドルを取得するロケールの言語。

**source**  — ロケールの取得元。次のいずれかの値に設定できます。

* **static**  — ロケールが使用可能な場合は `language` 属性から取得され、それ以外の場合はサーバーのデフォルトロケールから取得されます。

* **page**  — ロケールは、現在のページまたはリソース（使用可能な場合）の言語から取得され、使用可能な場合は `language` 属性から取得されます。それ以外の場合は、サーバーのデフォルトロケールから取得されます。

* **request**  — ロケールは、リクエストのロケール(  `request.getLocale()`)から取得されます。

* **auto**  — ロケールが使用可能な場合は `language` 属性から取得され、使用可能な場合は現在のページまたはリソースの言語から取得されます。それ以外の場合はリクエストから取得されます。

`source` 属性が設定されていない場合：

* `language`属性が設定されている場合、`source`属性のデフォルトは&quot;`static`です。

* `language`属性が設定されていない場合、`source`属性のデフォルトは`auto`です。

「コンテンツバンドル」は、標準のJSTL `<fmt:message>`タグで単純に使用できます。 キーによるメッセージのルックアップは次の 2 つの処理で構成されます。

1. 最初に、現在レンダリングされている基盤となるリソースの JCR プロパティが翻訳用に検索されます。これにより、JCR プロパティの値を編集するためのシンプルなコンポーネントのダイアログを定義できます。
1. ノードにキーと完全に同じ名前のプロパティが含まれていない場合、代替策は、sling要求(`SlingHttpServletRequest.getResourceBundle(Locale)`)からリソースバンドルを読み込むことです。 このバンドルの言語またはロケールは、`<cq:setContentBundle>`タグの言語およびソース属性によって定義されます。

`<cq:setContentBundle>`タグは、JSPでは次のように使用できます。

言語を定義するページの場合：

```xml
... %><cq:setContentBundle source="page"/><%  %>
<div class="error"><fmt:message key="Hello"/>
</div> ...
```

ユーザーがパーソナライズしたページの場合：

```xml
... %><cq:setContentBundle scope="request"/><% %>
<div class="error"><fmt:message key="Hello"/>
</div> ...
```

### <cq:include> {#cq-include}

`<cq:include>`タグは、現在のページにリソースを含めます。

このタグの属性を以下に示します。

**flush**

* ターゲットをインクルードする前に出力をフラッシュするかどうかを定義するブール値。

**path**

* 現在の要求の処理にインクルードするリソースオブジェクトのパス。このパスが相対パスの場合は、スクリプトが特定のリソースをインクルードする現在のリソースのパスに追加されます。path と resourceType または script を指定する必要があります。

**resourceType**

* インクルードするリソースのリソースタイプ。リソースタイプが設定されている場合、このパスはリソースオブジェクトの正確なパスである必要があります。この場合、パスへのパラメーター、セレクターおよび拡張子の追加はサポートされません。
* インクルードするリソースがリソースに解決できない path 属性と共に指定されている場合、タグではパスとこのリソースタイプから合成リソースオブジェクトを作成できます。
* path と resourceType または script を指定する必要があります。

**script**

* インクルードする jsp スクリプト。path と resourceType または script を指定する必要があります。

**ignoreComponentHierarchy**

* スクリプト解決の際にコンポーネントの階層を無視するかどうかを制御するブール値。true の場合は、検索パスだけが使用されます。

**例:**

```xml
<%@taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %><%
%><div class="center">
    <cq:include path="trail" resourceType="foundation/components/breadcrumb" />
    <cq:include path="title" resourceType="foundation/components/title" />
    <cq:include script="redirect.jsp"/>
    <cq:include path="par" resourceType="foundation/components/parsys" />
</div>
```

スクリプトを含めるには、`<%@ include file="myScript.jsp" %>`または`<cq:include script="myScript.jsp" %>`を使用する必要がありますか？

* `<%@ include file="myScript.jsp" %>`ディレクティブは、完全なファイルを現在のファイルに含めるようJSPコンパイラに通知します。 これにより、インクルードするファイルのコンテンツが元のファイルに直接貼り付けられるかのように処理されます。
* `<cq:include script="myScript.jsp">`タグを使用すると、ファイルは実行時に含まれます。

`<cq:include>`または`<sling:include>`を使用しますか？

* AEMコンポーネントを開発する場合、Adobeは`<cq:include>`を使用することを推奨します。
* `<cq:include>` script属性を使用する場合、名前を指定してスクリプトファイルを直接含めることができます。これにより、コンポーネントとリソースタイプの継承が考慮されます。多くの場合、この方法はセレクターと拡張子を使用する Sling のスクリプト解決を厳守するよりも簡単です。

### <cq:includeClientLib> {#cq-includeclientlib}

>[!CAUTION]
>
>`<cq:includeClientLib>` はAEM 5.6以降で非推奨となっています。代わりに使用 [ `<ui:includeClientLib>`](/help/sites-developing/taglib.md#ui-includeclientlib) します。

`<cq:includeClientLib>`タグには、AEM htmlクライアントライブラリが含まれます。このライブラリは、js、css、またはテーマライブラリにすることができます。 jsやcssなど、異なるタイプの複数の挿入タグの場合は、このタグをJSPで複数回使用する必要があります。 このタグは、`com.day.cq.widget.HtmlLibraryManager` サービスインターフェイスを囲む便利なラッパーです。

このタグの属性を以下に示します。

**カテゴリ**  — カンマ区切りのクライアントライブラリカテゴリのリスト。指定したカテゴリの JavaScript ライブラリと CSS ライブラリがすべてインクルードされます。テーマ名は要求から抽出されます。

等価な式: `com.day.cq.widget.HtmlLibraryManager#writeIncludes`

**テーマ**  — カンマ区切りのクライアントライブラリカテゴリのリスト。指定したカテゴリのテーマに関連するライブラリ（CSS と JS の両方）がすべてインクルードされます。テーマ名は要求から抽出されます。

次と等価：`com.day.cq.widget.HtmlLibraryManager#`writeThemeInclude

**js**  — カンマで区切られたクライアントライブラリカテゴリのリスト。指定したカテゴリの JavaScript ライブラリがすべてインクルードされます。

等価な式: `com.day.cq.widget.HtmlLibraryManager#writeJsInclude`

**css**  — カンマで区切られたクライアントライブラリカテゴリのリスト。指定したカテゴリの CSS ライブラリがすべてインクルードされます。

等価な式: `com.day.cq.widget.HtmlLibraryManager#writeCssInclude`

**themed**  — 主題設定されたライブラリまたは主題設定されていないライブラリのみを示すフラグを含めます。省略すると、どちらのライブラリもインクルードされます。純粋な JS または CSS のインクルードにのみ適用します（カテゴリまたはテーマのインクルードには適用されません）。

`<cq:includeClientLib>`タグは、JSPで次のように使用できます。

```xml
<%-- all: js + theme (theme-js + css) --%>
<cq:includeClientLib categories="cq.wcm.edit" />

<%-- only js libs --%>
<cq:includeClientLib js="cq.collab.calendar, cq.security" />

<%-- theme only (theme-js + css) --%>
<cq:includeClientLib theme="cq.collab.calendar, cq.security" />

<%-- css only --%>
<cq:includeClientLib css="cq.collab.calendar, cq.security" />
```

### <cq:defineObjects> {#cq-defineobjects}

`<cq:defineObjects>`タグは、次のように定期的に使用され、開発者が参照できるスクリプティングオブジェクトを公開します。 また、[ `<sling:defineObjects>`](#amp-lt-sling-defineobjects)タグで定義されたオブジェクトも公開します。

**componentContext**

* 要求の現在のコンポーネントのコンテキストオブジェクト（com.day.cq.wcm.api.components.ComponentContext インターフェイス）

**component**

* 現在のリソースの現在の AEM コンポーネントのオブジェクト（com.day.cq.wcm.api.components.Component インターフェイス）

**currentDesign**

* 現在のページの現在のデザインオブジェクト（com.day.cq.wcm.api.designer.Design インターフェイス）

**currentPage**

* 現在の AEM WCM ページオブジェクト（com.day.cq.wcm.api.Page インターフェイス）

**currentStyle**

* 現在のセルの現在のスタイルオブジェクト（com.day.cq.wcm.api.designer.Style インターフェイス）

**designer**

* デザイン情報にアクセスするために使用するデザイナーオブジェクト（com.day.cq.wcm.api.designer.Designer インターフェイス）

**editContext**

* AEM コンポーネントのコンテキストの編集オブジェクト（com.day.cq.wcm.api.components.EditContext インターフェイス）

**pageManager**

* ページレベルの操作用のページマネージャーオブジェクト（com.day.cq.wcm.api.PageManager インターフェイス）

**pageProperties**

* 現在のページのページプロパティオブジェクト（org.apache.sling.api.resource.ValueMap）

**プロパティ**

* 現在のリソースのプロパティオブジェクト（org.apache.sling.api.resource.ValueMap）

**resourceDesign**

* リソースページのデザインオブジェクト（com.day.cq.wcm.api.designer.Design インターフェイス）

**resourcePage**

* リソースページオブジェクト（com.day.cq.wcm.api.Page インターフェイス）
* このタグの属性を以下に示します。

**requestName**

* sling から継承

**responseName**

* sling から継承

**resourceName**

* sling から継承

**nodeName**

* sling から継承

**logName**

* sling から継承

**resourceResolverName**

* sling から継承

**slingName**

* sling から継承

**componentContextName**

* wcm に特有

**editContextName**

* wcm に特有

**propertiesName**

* wcm に特有

**pageManagerName**

* wcm に特有

**currentPageName**

* wcm に特有

**resourcePageName**

* wcm に特有

**pagePropertiesName**

* wcm に特有

**componentName**

* wcm に特有

**designerName**

* wcm に特有

**currentDesignName**

* wcm に特有

**resourceDesignName**

* wcm に特有

**currentStyleName**

* wcm に特有

**例**

```xml
<%@page session="false" contentType="text/html; charset=utf-8" %><%
%><%@ page import="com.day.cq.wcm.api.WCMMode" %><%
%><%@taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %><%
%><cq:defineObjects/>
```

>[!NOTE]
>
>`/libs/foundation/global.jsp`ファイルをスクリプトに含めると、`<cq:defineObjects />`タグが自動的に含まれます。

### <cq:requestURL> {#cq-requesturl}

`<cq:requestURL>`タグは、現在のリクエストURLをJspWriterに書き込みます。 2つのタグ[ `<cq:addParam>`](#amp-lt-cq-addparam)と[ `<cq:removeParam>`](#amp-lt-cq-removeparam)が書き込まれる前に、このタグの本文内で使用して現在のリクエストURLを変更できます。

これにより、様々なパラメーターを使用して現在のページへのリンクを作成できます。例えば、次のように要求を変換できます。

`mypage.html?mode=view&query=something` 対象 `mypage.html?query=something`.

`addParam`または`removeParam`を使用すると、指定したパラメーターのオカレンスのみが変更され、その他のすべてのパラメーターは影響を受けません。

`<cq:requestURL>` に属性がありません。

例：

```xml
<a href="<cq:requestURL><cq:removeParam name="language"/></cq:requestURL>">remove filter</a>
```

```xml
<a title="filter results" href="<cq:requestURL><cq:addParam name="language" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a>
```

### <cq:addParam> {#cq-addparam}

`<cq:addParam>`タグは、指定された名前と値を持つリクエストパラメーターを含む[ `<cq:requestURL>`](#amp-lt-cq-requesturl)タグに追加します。

このタグの属性を以下に示します。

**name**

* 追加するパラメーターの名前

**value**

* 追加するパラメーターの値

**例:**

```xml
<a title="filter results" href="<cq:requestURL><cq:addParam name="language" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a>
```

### <cq:removeParam> {#cq-removeparam}

`<cq:removeParam>`タグは、囲まれた[ `<cq:requestURL>`](#amp-lt-cq-requesturl)タグから、指定された名前と値を持つリクエストパラメーターを削除します。 値が指定されていない場合は、特定の名前を持つすべてのパラメーターが削除されます。

このタグの属性を以下に示します。

**name**

* 削除するパラメーターの名前

例：

```xml
<a href="<cq:requestURL><cq:removeParam name="language"/></cq:requestURL>">remove filter</a>
```

## Sling タグライブラリ  {#sling-tag-library}

Sling タグライブラリには Sling の便利な機能が用意されています。

スクリプトで Sling タグライブラリを使用する場合は、スクリプトを次のコードで開始する必要があります。

```xml
<%@ taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %>
```

>[!NOTE]
>
>`/libs/foundation/global.jsp`ファイルがスクリプトに含まれると、sling taglibが自動的に宣言されます。

### <sling:include> {#sling-include}

`<sling:include>`タグは、現在のページにリソースを含めます。

このタグの属性を以下に示します。

**フラッシュ**

* ターゲットをインクルードする前に出力をフラッシュするかどうかを定義するブール値。

**resource**

* 現在の要求の処理にインクルードするリソースオブジェクト。resource または path を指定する必要があります。どちらも指定されている場合は、resource が優先されます。

**path**

* 現在の要求の処理にインクルードするリソースオブジェクトのパス。このパスが相対パスの場合は、スクリプトが特定のリソースをインクルードする現在のリソースのパスに追加されます。resource または path を指定する必要があります。どちらも指定されている場合は、resource が優先されます。

**resourceType**

* インクルードするリソースのリソースタイプ。リソースタイプが設定されている場合、このパスはリソースオブジェクトの正確なパスである必要があります。この場合、パスへのパラメーター、セレクターおよび拡張子の追加はサポートされません。
* インクルードするリソースがリソースに解決できない path 属性と共に指定されている場合、タグではパスとこのリソースタイプから合成リソースオブジェクトを作成できます。

**replaceSelectors**

* ディスパッチの際に、セレクターがこの属性の値に置き換えられます。

**addSelectors**

* ディスパッチの際に、この属性の値がセレクターに追加されます。

**replaceSuffix**

* ディスパッチの際に、サフィックスがこの属性の値に置き換えられます。

>[!NOTE]
>
>`<sling:include>`タグに含まれるリソースとスクリプトの解像度は、通常のSling URLの解像度と同じです。 デフォルトでは、セレクター、拡張子など の値を現在のリクエストに含めるスクリプトにも使用します。 これらは、タグ属性を使用して変更できます。例えば、`replaceSelectors="foo.bar"`ではセレクターを上書きできます。

例：

```xml
<div class="item"><sling:include path="<%= pathtoinclude %>"/></div>
```

```xml
<sling:include resource="<%= par %>"/>
```

```xml
<sling:include addSelectors="spool"/>
```

```xml
<sling:include resource="<%= par %>" resourceType="<%= newType %>"/>
```

```xml
<sling:include resource="<%= par %>" resourceType="<%= newType %>"/>
```

```xml
<sling:include replaceSelectors="content" />
```

### <sling:defineObjects> {#sling-defineobjects}

`<sling:defineObjects>`タグは、次のように定期的に使用されるスクリプティングオブジェクトを公開します。このスクリプティングオブジェクトは開発者が参照できます。

**slingRequest**

* HTTP 要求ヘッダー情報へのアクセスを提供する SlingHttpServletRequest オブジェクト。標準の HttpServletRequest を拡張します。また、Sling に特有の要素（リソース、パス情報、セレクターなど）へのアクセスを提供します。

**slingResponse**

* サーバーで作成される HTTP 応答にアクセスを提供する SlingHttpServletResponse オブジェクト。現時点では、拡張元の HttpServletResponse と同じです。**request**
* 純粋な HttpServletRequest である標準の JSP 要求オブジェクト。**response**
* 純粋な HttpServletResponse である標準の JSP 応答オブジェクト。

**resourceResolver**

* 現在の ResourceResolver オブジェクト。slingRequest.getResourceResolver() と同じです。

。**sling**

* SlingScriptHelper オブジェクト。スクリプト用の便利なメソッドが格納されています。主なメソッドは、他のリソースの応答をこの応答内にインクルードする（例：ヘッダーの html スニペットを埋め込む）ための sling.include(&#39;/some/other/resource&#39;) と、Sling で使用可能な OSGi サービス（スクリプト言語に応じたクラス表記）を取得するための sling.getService(foo.bar.Service.class) です。

**リソース**

* 処理する現在のリソースオブジェクト（要求の URL によって異なります）。slingRequest.getResource() と同じです。

**currentNode**

* 現在のリソースが JCR ノードを指す場合（通常は Sling の場合）に、ノードオブジェクトへの直接アクセスを提供します。それ以外の場合、このオブジェクトは定義されません。

**log**

* スクリプト内から Sling ログシステムへのログ記録のための SLF4J ロガーを提供します。例えば、log.info(&quot;Executing my script&quot;) のように指定します。

* このタグの属性を以下に示します。

**requestName**

**responseName**

**nodeName**

**logName resourceResolverName**

**slingName**

**例：**

```xml
<%@page session="false" %><%
%><%@page import="com.day.cq.wcm.foundation.forms.ValidationHelper"%><%
%><%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %><%
%><sling:defineObjects/>
```

## JSTL タグライブラリ  {#jstl-tag-library}

[JavaServer Pages Standardタグライブラリ](https://www.oracle.com/technetwork/java/index-jsp-135995.html)には、便利なタグや標準タグがたくさん含まれています。 taglibの中核となる、書式設定と関数は、次のスニペットのように`/libs/foundation/global.jsp`で定義されます。

### /libs/foundation/global.jsp からの抜粋{#extract-of-libs-foundation-global-jsp}

```xml
<%@taglib prefix="c" uri="https://java.sun.com/jsp/jstl/core" %>
<%@taglib prefix="fmt" uri="https://java.sun.com/jsp/jstl/fmt" %>
<%@taglib prefix="fn" uri="https://java.sun.com/jsp/jstl/functions" %>
```

前述のように`/libs/foundation/global.jsp`ファイルを読み込んだ後、`c`、`fmt`、`fn`のプリフィックスを使用して、これらのtaglibにアクセスできます。 JSTL の公式ドキュメントは[「The Java EE 5 Tutorial」の「JavaServer Pages Standard Tag Library」](https://docs.oracle.com/javaee/5/tutorial/doc/bnakc.html)にあります。
