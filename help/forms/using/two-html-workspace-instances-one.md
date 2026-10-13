---
title: 2 つの AEM Forms ワークプレースインスタンスを 1 つのサーバー上にホストする
description: LC 管理者が HTML WS をカスタマイズして 2 つのインスタンスを 1 つのサーバーにホストし、異なる URL を使ってアクセスできるようにする方法。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 32a546fc-e33f-46f9-ac3b-45eca0e12239
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 97aafc4b-2598-52d6-9012-295a95969e38
    internal-label: HTML5 Forms
  - id: 59f95943-e802-56ac-990d-21ab923984c1
    internal-label: Mobile Forms
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 100%
---
# 2 つの AEM Forms ワークプレースインスタンスを 1 つのサーバー上にホストする {#hosting-two-aem-forms-workspace-instances-on-one-server}

AEM Forms のデフォルトのインストールと設定では、1 つの AEM Forms ワークスペースのみがサーバー上で使用できます。 ただし、AEM Forms ワークスペースの 2 つの異なるインスタンスを 1 つの AEM Forms サーバーにホストしたい場合があります。 これら 2 つのインスタンスは異なる URL によってアクセス可能です。

AEM Forms 管理者はワークスペースをカスタマイズして、2 つの異なる URL を作成し、 2 つのワークスペースを同じサーバー上で使用できるようにします。 このカスタマイズ記事では、2 つのワークスペースが `https://'[server]:[port]'/lc/ws` と `https://'[server]:[port]':/lc/ws2` でアクセスできると仮定しています。

以下の手順に従って AEM Forms ワークスペースを設定します。

1. AEM Forms ワークスペースの dev パッケージをサーバーにインストールします。 作成方法については、[dev パッケージ](/help/forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)を参照してください。
1. `https://'[server]:[port]'/lc/crx/de/index.jsp` にアクセスして、管理者として CRXDE Lite にログインします。
1. /content の node ws をコピーし、それを /content にペーストします。 node の名前を ws2 に変更します。 「**[!UICONTROL すべて保存]**」をクリックします。 このノードのプロパティで、`sling:resourceType` の値を ws2 に変更します。 「**[!UICONTROL すべて保存]**」をクリックします。

1. /libs にあるフォルダー ws をコピーして /apps にペーストします。 このフォルダーの名前を ws2 に変更します。 「**[!UICONTROL すべて保存]**」をクリックします。
1. `GET.jsp` にある `/apps/ws2` で、次のコード変更を行います。 次を

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

1. `registry.js` にある `/apps/ws2/js` で、テンプレートのパスを、`/apps/ws2/js/runtime/templates` にあるテンプレートを参照するように変更します。 次のコードを

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

1. `/etc/map/ws`フォルダーをコピーし、`/etc/map`にペーストします。 この新しいフォルダーの名前を ws2 に変更します。 「すべて保存」をクリックします。

1. `ws2`のプロパティで、`sling:redirect`の値を`content/ws2`に変更します。

1. 値を`sling:match`から`^[^/\||]/[^/\||]/ws2$`に変更します。
