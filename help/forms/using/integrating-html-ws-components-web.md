---
title: Web アプリケーションでの AEM Forms Workspace コンポーネントの統合
seo-title: Web アプリケーションでの AEM Forms Workspace コンポーネントの統合
description: 独自の Web アプリケーションで AEM Forms Workspace コンポーネントを再利用して、機能を強化し密接な統合を提供する方法。
seo-description: 独自の Web アプリケーションで AEM Forms Workspace コンポーネントを再利用して、機能を強化し密接な統合を提供する方法。
uuid: bb9b8aa0-3f41-4f44-8eb7-944e778ee8a6
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 6be87939-007e-42c7-8a41-e34ac2b8bed4
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 74%

---


# Web アプリケーションでの AEM Forms Workspace コンポーネントの統合 {#integrating-aem-forms-workspace-components-in-web-applications}

AEM Forms Workspace [コンポーネント](/help/forms/using/description-reusable-components.md) を固有の Web アプリケーションで使用することができます。以下のサンプルの実装は、CRX™ インスタンスにインストールされた AEM Forms Workspace Dev パッケージのコンポーネントを使用して Web アプリケーションを作成します。下記のソリューションをカスタマイズして、個々のニーズに合わせます。The sample implementation reuses `UserInfo`, `FilterList`, and `TaskList`components inside a web portal.

1. でCRXDE Lite環境にログインし `https://'[server]:[port]'/lc/crx/de/`ます。 AEM Forms Workspace Dev パッケージがインストールされていることを確認します。
1. パスを作成し `/apps/sampleApplication/wscomponents`ます。
1. css、images、js/libs、js/runtime、および js/registry.js を

   * `/libs/ws` から
   * を `/apps/sampleApplication/wscomponents`.

1. /apps/sampleApplication/wscomponents/js フォルダー内部に demomain.js ファイルを作成します。コードを /libs/ws/js/main.js から demomain.js にコピーします。
1. demomain.js で、コードを削除してルーターを初期化し、以下のコードを追加します。

   ```javascript
   require(['initializer','runtime/util/usersession'],
       function(initializer, UserSession) {
           UserSession.initialize(
               function() {
                   // Render all the global components
                   initializer.initGlobal();
               });
       });
   ```

1. Create a node under /content by name `sampleApplication` and type `nt:unstructured`. In the properties of this node add `sling:resourceType` of type String and value `sampleApplication`. このノードのアクセス制御リストで、jcr:read 権限を許可する `PERM_WORKSPACE_USER` にエントリを追加します。Also, in the Access Control List of `/apps/sampleApplication` add an entry for `PERM_WORKSPACE_USER` allowing jcr:read privileges.
1. のパスをからに `/apps/sampleApplication/wscomponents/js/registry.js` 更新し、テンプレート値 `/lc/libs/ws/` に `/lc/apps/sampleApplication/wscomponents/` 対して適用。
1. In your portal home page JSP file at `/apps/sampleApplication/GET.jsp`, add the following code to include the required components inside the portal.

   ```jsp
   <script data-main="/lc/apps/sampleApplication/wscomponents/js/demomain" src="/lc/apps/sampleApplication/wscomponents/js/libs/require/require.js"></script>
   <div class="UserInfoView gcomponent" data-name="userinfo"></div>
   <div class="filterListView gcomponent" data-name="filterlist"></div>
   <div class="taskListView gcomponent" data-name="tasklist"></div>
   ```

   AEM Forms Workspace コンポーネントに必要な CSS ファイルも含めます。

   >[!NOTE]
   >
   >各コンポーネントはレンダリングする際にコンポーネントタグ（クラス gcomponent を所有）に追加されます。ホームページにこれらのタグが含まれていることを確認します。これらの基本制御タグの詳細については、AEM Forms Workspace の `html.jsp` ファイルを参照してください。

1. コンポーネントをカスタマイズするには、以下のように必要なコンポーネントの既存のビューを拡張します。

   ```javascript
   define([
       ‘jquery’,
       ‘underscore’,
       ‘backbone’,
       ‘runtime/views/userinfo'],
       function($, _, Backbone, UserInfo){
           var demoUserInfo = UserInfo.extend({
               //override the functions to customize the functionality
               render: function() {
                   UserInfo.prototype.render.call(this); // call the render function of the super class
                   …
                   //other tasks
                   …
               }
           });
           return demoUserInfo;
   });
   ```

1. ポータルの CSS を修正し、ポータル上の必要なコンポーネントのレイアウト、配置、スタイルを設定します。たとえば、このポータルの背景色を黒色に保持して userInfo コンポーネントも同様に表示するとします。You can do this by changing background color in `/apps/sampleApplication/wscomponents/css/style.css` as follows:

   ```css
   body {
       font-family: "Myriad pro", Arial;
       background: #000;    //This was origianlly #CCC
       position: relative;
       margin: 0 auto;
   }
   ```
