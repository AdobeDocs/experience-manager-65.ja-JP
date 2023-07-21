---
title: 2 つの AEM Forms ワークプレースインスタンスを 1 つのサーバー上にホストする
description: LC 管理者がHTMLWS をカスタマイズして、異なる URL を介してアクセス可能な単一のサーバー上で 2 つのインスタンスをホストする方法。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 32a546fc-e33f-46f9-ac3b-45eca0e12239
source-git-commit: a56d5121a6ce11b42a6c30dae9e479564d16af27
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 43%

---

# 2 つの AEM Forms ワークプレースインスタンスを 1 つのサーバー上にホストする {#hosting-two-aem-forms-workspace-instances-on-one-server}

AEM Formsのデフォルトのインストールと設定では、1 つのAEM Forms Workspace のみをサーバー上で使用できます。 ただし、場合によっては、AEM Forms Workspace の 2 つの異なるインスタンスを 1 つのAEM Forms Server でホストする必要があります。 2 つのインスタンスには、異なる URL からアクセスできます。

AEM Formsの管理者は、ワークスペースをカスタマイズして 2 つの異なる URL を作成し、2 つのワークスペースを同じサーバーで使用できるようにします。 このカスタマイズ記事では、2 つのワークスペースが次の場所からアクセス可能であると仮定できます。 `https://'[server]:[port]'/lc/ws` および `https://'[server]:[port]':/lc/ws2`.

次の手順に従って、AEM Forms Workspace を設定します。

1. サーバーにAEM Forms Workspace の dev パッケージをインストールします。 詳しくは、 [開発パッケージ](/help/forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)を参照してください。
1. にアクセスして、CRXDE Liteに管理者としてログインします。 `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. ノード ws を/content にコピーし、/content に貼り付けます。 ノード名を ws2 に変更します。 「**[!UICONTROL すべて保存]**」をクリックします。このノードのプロパティで、`sling:resourceType` の値を ws2 に変更します。「**[!UICONTROL すべて保存]**」をクリックします。

1. /libs からフォルダー ws をコピーし、/apps に貼り付けます。 フォルダーの名前を ws2 に変更します。 「**[!UICONTROL すべて保存]**」をクリックします。
1. `GET.jsp` にある `/apps/ws2` で、次のコード変更を行います。次を

   ```html
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

   ```html
   <html lang="en">
   <head>
       <meta charset="utf-8">
       <title>Workspace Next</title>
       <meta http-equiv="refresh" content="0;URL='/lc/apps/ws2/index.html'" />
   ```

1. `registry.js` にある `/apps/ws2/js` で、テンプレートのパスを、`/apps/ws2/js/runtime/templates` にあるテンプレートを参照するように変更します。次のコードを

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

1. `userinfo.js`にある`/apps/ws2/js/runtime/models`および`/apps/ws2/js/runtime/views`で、文字列を`/lc/content/ws`から`lc/content/ws2`に変更します。

1. `/apps/ws2/js/runtime/services/service.js`で、 `getLocalizationData`関数のパスを`/lc/apps/ws2/Locale.html`に指すように変更します。

1. 新しいワークスペースの`pdf.html`に参照するには、`/apps/ws2/js/runtime/views/forms/pdftaskform.js`にある`pdf.html`のパスを変更します。

1. 新しいワークスペースの`pdf.html`に参照するには、 `startprocess.html`にある`pdf.html`と`WsNextAdapter.swf`、および`/apps/ws2/js/runtime/templates`で`taskdetails.html`と`processinstancehistory.html` のパスを変更します。

1. `/etc/map/ws`フォルダーをコピーし、`/etc/map`にペーストします。新しいフォルダーの名前を ws2 に変更します。 「すべて保存」をクリックします。

1. `ws2`のプロパティで、`sling:redirect`の値を`content/ws2`に変更します。

1. 値を`sling:match`から`^[^/\||]/[^/\||]/ws2$`に変更します。
