---
title: Web アプリケーションでの AEM Forms Workspace コンポーネントの統合
seo-title: Integrating AEM Forms workspace components in web applications
description: 独自の Web アプリケーションで AEM Forms Workspace コンポーネントを再利用して、機能を強化し密接な統合を提供する方法。
seo-description: How to reuse AEM Forms workspace components in your own webapps to leverage functionality and provide tight integration.
uuid: bb9b8aa0-3f41-4f44-8eb7-944e778ee8a6
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 6be87939-007e-42c7-8a41-e34ac2b8bed4
exl-id: bb4a500d-c34f-4586-83f0-ad7ef69b4fb1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '344'
ht-degree: 100%

---

# Web アプリケーションでの AEM Forms Workspace コンポーネントの統合 {#integrating-aem-forms-workspace-components-in-web-applications}

AEM Forms Workspace [コンポーネント](/help/forms/using/description-reusable-components.md) を固有の Web アプリケーションで使用することができます。以下のサンプルの実装は、CRX™ インスタンスにインストールされた AEM Forms Workspace Dev パッケージのコンポーネントを使用して Web アプリケーションを作成します。下記のソリューションをカスタマイズして、個々のニーズに合わせます。サンプルの実装は、Web ポータル内部の `UserInfo`、`FilterList`、`TaskList` コンポーネントを再利用します。

1. `https://'[server]:[port]'/lc/crx/de/` で CRXDE Lite 環境にログインします。AEM Forms Workspace Dev パッケージがインストールされていることを確認します。
1. パス `/apps/sampleApplication/wscomponents` を作成します。
1. css、images、js/libs、js/runtime、および js/registry.js をコピーします

   * コピー元：`/libs/ws`
   * コピー先：`/apps/sampleApplication/wscomponents`。

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

1. /content の下に名前 `sampleApplication` およびタイプ `nt:unstructured` のノードを作成します。このノードのプロパティで、タイプ文字列の `sling:resourceType` と値 `sampleApplication` を追加します。このノードのアクセス制御リストで、jcr:read 権限を許可する `PERM_WORKSPACE_USER` にエントリを追加します。また、`/apps/sampleApplication` のアクセス制御リストで、jcr:read privileges 権限を許可する `PERM_WORKSPACE_USER` のエントリを追加します。
1. `/apps/sampleApplication/wscomponents/js/registry.js` でテンプレート値のパスを `/lc/libs/ws/` から `/lc/apps/sampleApplication/wscomponents/` にアップデートします。
1. `/apps/sampleApplication/GET.jsp`/ にあるポータルホームページの JSP ファイルで、次のコードを追加してポータル内部の必要なコンポーネントを含めます。

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

1. ポータルの CSS を修正し、ポータル上の必要なコンポーネントのレイアウト、配置、スタイルを設定します。たとえば、このポータルの背景色を黒色に保持して userInfo コンポーネントも同様に表示するとします。それには、以下のようにして `/apps/sampleApplication/wscomponents/css/style.css` の背景色を変更します。

   ```css
   body {
       font-family: "Myriad pro", Arial;
       background: #000;    //This was origianlly #CCC
       position: relative;
       margin: 0 auto;
   }
   ```
