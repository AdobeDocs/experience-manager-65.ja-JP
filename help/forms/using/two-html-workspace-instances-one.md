---
title: 2 つの AEM Forms ワークプレースインスタンスを 1 つのサーバー上にホストする
seo-title: 2 つの AEM Forms ワークプレースインスタンスを 1 つのサーバー上にホストする
description: LC 管理者が HTML WS をカスタマイズして 2 つのインスタンスを 1 つのサーバーにホストし、異なる URL を使ってアクセスできるようにする方法。
seo-description: LC 管理者が HTML WS をカスタマイズして 2 つのインスタンスを 1 つのサーバーにホストし、異なる URL を使ってアクセスできるようにする方法。
uuid: 0584f512-6b92-4418-b71c-93605cfa1927
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 1254a7c2-2c67-4661-803e-afd53e817916
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# 2 つの AEM Forms ワークプレースインスタンスを 1 つのサーバー上にホストする {#hosting-two-aem-forms-workspace-instances-on-one-server}

AEM Forms のデフォルトのインストールと設定では、1 つの AEM Forms ワークスペースのみがサーバー上で使用できます。ただし、AEM Forms ワークスペースの 2 つの異なるインスタンスを 1 つの AEM Forms サーバーにホストしたい場合があります。これら 2 つのインスタンスは異なる URL によってアクセス可能です。

AEM Forms 管理者はワークスペースをカスタマイズして、2 つの異なる URL を作成し、 2 つのワークスペースを同じサーバー上で使用できるようにします。In this customization article, we assume the two workspaces are accessible at `https://'[server]:[port]'/lc/ws` and `https://'[server]:[port]':/lc/ws2`.

以下の手順に従って AEM Forms ワークスペースを設定します。

1. AEM Forms ワークスペースの dev パッケージをサーバーにインストールします。作成方法については、[dev パッケージ](/help/forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)を参照してください。
1. Login to CRXDE Lite as an administrator, by accessing `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. /content の node ws をコピーし、それを /content にペーストします。node の名前を ws2 に変更します。「**[!UICONTROL すべて保存]**」をクリックします。このノードのプロパティで、`sling:resourceType` の値を ws2 に変更します。 「**[!UICONTROL すべて保存]**」をクリックします。

1. /libs にあるフォルダー ws を /apps にペーストします。このフォルダーの名前を ws2 に変更します。「**[!UICONTROL すべて保存]**」をクリックします。
1. In `GET.jsp` at `/apps/ws2`, make the following code changes. 次のコードを

   ```
   <html lang="en">
   <head>
       <meta charset="utf-8">
       <title>Workspace Next</title>
       <meta http-equiv="refresh" content="0;URL='/lc/libs/ws/index.html'" /><html lang="en">
   <head>
       <meta charset="utf-8">
       <title>Workspace Next</title>
       <meta http-equiv="refresh" content="0;URL='/lc/libs/ws/index.html'" />
   ```

   次のコードで置き換えます。

   ```
   <html lang="en">
   <head>
       <meta charset="utf-8">
       <title>Workspace Next</title>
       <meta http-equiv="refresh" content="0;URL='/lc/apps/ws2/index.html'" />
   ```

1. In `registry.js` at `/apps/ws2/js`, change path of templates to refer to templates at `/apps/ws2/js/runtime/templates`. 次のコードを

   ```css
   "tasklist" : {
   "name": "tasklist",
   "path": "tasklistview",
   "model": "tasklist",
   "template": "text!/lc/libs/ws/js/runtime/templates/tasklist.html",
   "utility": "utility",
   "view": "taskview",
   "errorModel": null
   }
   ```

   次のコードで置き換えます。

   ```css
   "tasklist" : {
   "name": "tasklist",
   "path": "tasklistview",
   "model": "tasklist",
   "template": "text!/lc/apps/ws2/js/runtime/templates/tasklist.html",
   "utility": "utility",
   "view": "taskview",
   "errorModel": null
   }
   ```

1. atおよ `userinfo.js` びで、string `/apps/ws2/js/runtime/models` を `/apps/ws2/js/runtime/views`に変更し `/lc/content/ws` ます `lc/content/ws2`。

1. で、関 `/apps/ws2/js/runtime/services/service.js`数内のパスをに変 `getLocalizationData` 更します `/lc/apps/ws2/Locale.html`。

1. To refer to `pdf.html` of the new Workspace, change the path of `pdf.html` in `/apps/ws2/js/runtime/views/forms/pdftaskform.js`.

1. To refer to `pdf.html` of the new Workspace, change paths of `pdf.html` and `WsNextAdapter.swf` in `startprocess.html`, `taskdetails.html`, and `processinstancehistory.html` at `/apps/ws2/js/runtime/templates`.

1. Copy `/etc/map/ws` folder and paste at `/etc/map`. この新しいフォルダーの名前を ws2 に変更します。「すべて保存」をクリックします。

1. In properties of `ws2`, change value of `sling:redirect` to `content/ws2`.

1. の値をからに変 `sling:match` 更します `^[^/\||]/[^/\||]/ws2$`。
