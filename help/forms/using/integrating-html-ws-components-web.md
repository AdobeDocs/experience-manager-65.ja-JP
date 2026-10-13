---
title: Web アプリケーションでの AEM Forms ワークスペースコンポーネントの統合
description: 独自の web アプリケーションで AEM Forms Workspace コンポーネントを再利用して、機能を使用し密接な統合を提供する方法。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: bb4a500d-c34f-4586-83f0-ad7ef69b4fb1
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: Admin, User, Developer
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
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 91%
---
# Web アプリケーションでの AEM Forms ワークスペースコンポーネントの統合 {#integrating-aem-forms-workspace-components-in-web-applications}

AEM Forms Workspace [コンポーネント](/help/forms/using/description-reusable-components.md) を固有の web アプリケーションで使用することができます。 以下のサンプルの実装は、CRX™ インスタンスにインストールされた AEM Forms Workspace Dev パッケージのコンポーネントを使用して web アプリケーションを作成します。 下記のソリューションをカスタマイズして、個々のニーズに合わせます。 サンプルの実装は、Web ポータル内部の `UserInfo`、`FilterList`、`TaskList` コンポーネントを再利用します。

1. `https://'[server]:[port]'/lc/crx/de/` で CRXDE Lite 環境にログインします。 AEM Forms Workspace Dev パッケージがインストールされていることを確認します。
1. パス `/apps/sampleApplication/wscomponents` を作成します。
1. css、images、js/libs、js/runtime、および js/registry.js をコピーします

   * コピー元：`/libs/ws`
   * 移動先`/apps/sampleApplication/wscomponents`

1. /apps/sampleApplication/wscomponents/js フォルダー内に demomain.js ファイルを作成します。 コードを /libs/ws/js/main.js から demomain.js にコピーします。
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

1. /content の下に名前 `sampleApplication` およびタイプ `nt:unstructured` のノードを作成します。 このノードのプロパティで、タイプ文字列の `sling:resourceType` と値 `sampleApplication` を追加します。 このノードのアクセス制御リストで、jcr:read権限を許可する`PERM_WORKSPACE_USER`のエントリを追加します。 また、`/apps/sampleApplication`のアクセス制御リストに、`PERM_WORKSPACE_USER`のエントリを追加して、jcr:read権限を許可します。
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
   >各コンポーネントはレンダリングする際にコンポーネントタグ（クラス gcomponent を所有）に追加されます。 ホームページにこれらのタグが含まれていることを確認します。 これらの基本制御タグの詳細については、AEM Forms Workspace の `html.jsp` ファイルを参照してください。

1. コンポーネントをカスタマイズするには、以下のように必要なコンポーネントの既存のビューを拡張します。

   ```javascript
   define([
       'jquery',
       'underscore',
       'backbone',
       'runtime/views/userinfo'],
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

1. ポータルの CSS を修正し、ポータル上の必要なコンポーネントのレイアウト、配置、スタイルを設定します。 例えば、このポータルの背景色を黒色に保持して userInfo コンポーネントも同様に表示するとします。 それには、以下のようにして `/apps/sampleApplication/wscomponents/css/style.css` の背景色を変更します。

   ```css
   body {
       font-family: "Myriad pro", Arial;
       background: #000;    //This was origianlly #CCC
       position: relative;
       margin: 0 auto;
   }
   ```
