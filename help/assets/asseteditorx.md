---
title: アセットエディターの拡張
description: カスタムコンポーネントを使用したアセットエディターの機能の拡張方法を説明します。
contentOwner: AG
role: User, Admin
feature: Developer Tools
exl-id: de1c63c1-a0e5-470b-8d83-b594513a5dbd
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 80%

---

# アセットエディターの拡張 {#extending-asset-editor}

アセットエディターは、アセット共有を使用して見つけたアセットをクリックすると開くページです。アセットエディターでは、メタデータ、サムネール、タイトルおよびタグなどのアセットの特性を編集できます。

事前設定済みの編集コンポーネントを使用してエディターを設定する方法については、[アセットエディターページの作成および設定](assets-finder-editor.md#creating-and-configuring-an-asset-editor-page)を参照してください。

既存のエディターコンポーネントを使用するだけでなく、[!DNL Adobe Experience Manager] デベロッパーは、独自のコンポーネントを作成することもできます。

## アセットエディターテンプレートの作成 {#creating-an-asset-editor-template}

Geometrixx には次のサンプルページがあります。

* Geometrixx サンプルページ：`/content/geometrixx/en/press/asseteditor.html`
* サンプルテンプレート：`/apps/geometrixx/templates/asseteditor`
* サンプルページコンポーネント：`/apps/geometrixx/components/asseteditor`

### Clientlib の設定 {#configuring-clientlib}

[!DNL Assets] コンポーネントでは、WCM 編集クライアントライブラリの拡張機能が使用されています。クライアントライブラリは通常、`init.jsp` に読み込まれます。

（コアの `init.jsp` での）デフォルトクライアントライブラリの読み込みとは異なり、[!DNL Assets] テンプレートは次の条件を満たす必要があります。

* テンプレートでは、（`cq.wcm.edit` ではなく）`cq.dam.edit` クライアントライブラリを組み込む必要があります。

* 無効な WCM モード（例：**パブリッシュ**&#x200B;への読み込み）でも、述語、アクション、レンズをレンダリングできるように、このクライアントライブラリを組み込む必要があります。

通常は、既存のサンプル `init.jsp`（`/apps/geometrixx/components/asseteditor/init.jsp`）をコピーすればこの要件を満たします。

### JS アクションの設定 {#configuring-js-actions}

一部の [!DNL Assets] コンポーネントでは `component.js` で定義されている JS 関数が必要です。このファイルをコンポーネントディレクトリにコピーしてリンクします。

```javascript
<script type="text/javascript" src="<%= component.getPath() %>/component.js"></script>
```

このサンプルでは、この JavaScript ソースを `head.jsp`（`/apps/geometrixx/components/asseteditor/head.jsp`）で読み込んでいます。

### 追加のスタイルシート {#additional-style-sheets}

一部の [!DNL Assets] コンポーネントでは、 ウィジェットライブラリが使用されます。コンテンツのコンテキストで適切にレンダリングするには、追加のスタイルシートを読み込む必要があります。 タグアクションコンポーネントには、もう 1 つ必要です。

```css
<link href="/etc/designs/geometrixx/ui.widgets.css" rel="stylesheet" type="text/css">
```

### Geometrixxスタイルシート {#geometrixx-style-sheet}

サンプルページコンポーネントでは、すべてのセレクターが `static.css`（`/etc/designs/geometrixx/static.css`）の `.asseteditor` で始まっている必要があります。ベストプラクティス：すべての `.asseteditor` セレクターをスタイルシートにコピーし、ルールを必要に応じて調整します。

### FormChooser：最終的に読み込まれるリソースの調整 {#formchooser-adjustments-for-eventually-loaded-resources}

アセットエディターはフォーム選択機能を使用します。この機能を使用すると、フォームセレクターとフォームのパスをアセットの URL に追加するだけで、同じフォームページ上のリソース（この場合はアセット）を編集できます。

次に例を示します。

* プレーンフォームページ：[http://localhost:4502/content/geometrixx/jp/press/asseteditor.html](http://localhost:4502/content/geometrixx/jp/press/asseteditor.html)
* フォームページに読み込まれるアセット：[http://localhost:4502/content/dam/geometrixx/icons/diamond.png.form.html/content/geometrixx/jp/press/asseteditor.html](http://localhost:4502/content/dam/geometrixx/icons/diamond.png.form.html/content/geometrixx/jp/press/asseteditor.html)

`head.jsp`（`/apps/geometrixx/components/asseteditor/head.jsp`）のサンプルハンドルは、次の処理をおこないます。

* アセットが読み込まれるか、またはプレーンフォームが表示される必要があるかを検出します。
* アセットが読み込まれると、parsys はプレーンフォームページでしか編集できないので、WCM モードを無効にします。
* アセットが読み込まれると、フォームページのタイトルではなくアセットのタイトルを使用します。

```javascript
 List<Resource> resources = FormsHelper.getFormEditResources(slingRequest);
    if (resources != null) {
        if (resources.size() == 1) {
            // single resource
            FormsHelper.setFormLoadResource(slingRequest, resources.get(0));
        } else if (resources.size() > 1) {
            // multiple resources
            // not supported by CQ 5.3
        }
    }
    Resource loadResource = (Resource) request.getAttribute("cq.form.loadresource");
    String title;
    if (loadResource != null) {
        // an asset is loaded: disable WCM
        WCMMode.DISABLED.toRequest(request);

        String path = loadResource.getPath();
        Asset asset = loadResource.adaptTo(Asset.class);
        try {
            // it might happen that the adobe xmp lib creates an array
            Object titleObj = asset.getMetadata("dc:title");
            if (titleObj instanceof Object[]) {
                Object[] titleArray = (Object[]) titleObj;
                title = (titleArray.length > 0) ? titleArray[0].toString() : "";
            } else {
                title = titleObj.toString();
            }
        }
        catch (NullPointerException e) {
            title = path.substring(path.lastIndexOf("/") + 1);
        }
    }
    else {
        title = currentPage.getTitle() == null ? currentPage.getName() : currentPage.getTitle();
    }
```

HTML 部分で、先頭のタイトルセット（アセットまたはページのタイトル）を使用します。

```html
<title><%= title %></title>
```

## シンプルなフォームフィールドコンポーネントの作成 {#creating-a-simple-form-field-component}

この例では、読み込んだアセットのメタデータを表示するコンポーネントを作成する方法を説明します。

1. プロジェクトディレクトリにコンポーネントフォルダー（`/apps/geometrixx/components/samplemeta` など）を作成します。
1. 次のスニペットを使用して `content.xml` を追加します。

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Image Dimension"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Asset Editor"/>
   ```

1. 次のスニペットを使用して `samplemeta.jsp` を追加します。

   ```javascript
   <%--
   
     Sample metadata field component
   
   --%><%@ page import="com.day.cq.dam.api.Asset,
                    java.security.AccessControlException" %><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   
       String value = "";
       String name = "dam:sampleMetadata";
       boolean readOnly = false;
   
       // If the form page is requested for an asset loadResource is the asset.
       Resource loadResource = (Resource) request.getAttribute("cq.form.loadresource");
   
       if (loadResource != null) {
   
           // Determine if the loaded asset is read only.
           Session session = slingRequest.getResourceResolver().adaptTo(Session.class);
           try {
               session.checkPermission(loadResource.getPath(), "set_property");
               readOnly = false;
           }
           catch (AccessControlException ace) {
               // checkPermission throws exception if asset is read only
               readOnly = true;
           }
           catch (RepositoryException re) {}
   
           // Get the value of the metadata.
           Asset asset = loadResource.adaptTo(Asset.class);
           try {
               value = asset.getMetadata(name).toString();
           }
           catch (NullPointerException npe) {
               // no metadata dc:description available
           }
       }
   %>
   <div class="form_row">
       <div class="form_leftcol">
           <div class="form_leftcollabel">Sample Metadata</div>
       </div>
       <div class="form_rightcol">
           <%
           if (readOnly) {
               %><c:out value="<%= value %>"/><%
           }
           else {
               %><input class="text" type="text" name="./jcr:content/metadata/<%= name %>" value="<c:out value="<%= value %>" />"><%
           }%>
       </div>
   </div>
   ```

1. コンポーネントを使用できるようにするには、コンポーネントを編集可能にする必要があります。コンポーネントを編集可能にするには、CRXDE Lite で、`cq:EditConfig` プライマリ型の `cq:editConfig` ノードを追加します。段落を削除できるよう、値を複数設定できるプロパティ `cq:actions` を追加し、値として `DELETE` のみを設定します。

1. ブラウザーを開き、サンプルページ（`asseteditor.html` など）でデザインモードに切り替え、段落システム用の新しいコンポーネントを有効にします。

1. **編集**&#x200B;モードで、新しいコンポーネント（**Sample Metadata** など）がサイドキック（**アセットエディター**&#x200B;グループ内）で使用できます。コンポーネントを挿入します。メタデータを保存するには、メタデータフォームに追加する必要があります。

## メタデータオプションを変更 {#modifying-metadata-options}

[メタデータフォーム](assets-finder-editor.md#metadata-form-and-text-field-configuring-the-view-metadata-component)で利用可能な名前空間を変更できます。

現在使用可能なメタデータは `/libs/dam/options/metadata` で定義されています。

* このディレクトリ内の第 1 レベルには、名前空間が含まれます。
* 各名前空間内の項目は、ローカルパーツ項目の結果など、メタデータを表します。
* メタデータコンテンツには、タイプの情報と複数値オプションが含まれます。

これらのオプションは `/apps/dam/options/metadata` で上書きできます。

1. `/libs` 配下のディレクトリを `/apps` の下にコピーします。

1. 項目を削除、変更、または追加します。

>[!NOTE]
>
>新しい名前空間を追加する場合は、リポジトリ/CRX に登録する必要があります。 送信しない場合は、メタデータフォームを送信するとエラーが発生します。
