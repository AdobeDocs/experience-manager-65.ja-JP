---
title: AEM Forms Workspace のカスタマイズの一般的な手順
seo-title: AEM Forms Workspace のカスタマイズの一般的な手順
description: AEM Forms Workspace ユーザーインターフェイスをカスタマイズする方法。
seo-description: AEM Forms Workspace ユーザーインターフェイスをカスタマイズする方法。
uuid: da6310b4-1c58-468d-85c6-975fd2c141f9
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: dd3218c4-2bb2-40fc-9141-5823b0ea4224
docset: aem65
exl-id: 45e50b47-1b36-4937-9e1a-cc7bfb953861
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 40%

---

# AEM Forms Workspace のカスタマイズの一般的な手順に従います。  {#generic-steps-for-aem-forms-workspace-customization}

カスタマイズを実行するための一般的な手順を以下に示します。

1. `https://'[server]:[port]'/lc/crx/de/index.jsp`にアクセスしてCRXDE Liteにログインします。
1. `ws`という名前の`sling:Folder`フォルダーが存在しない場合は、`/apps`に作成します。 `sling:Folder`フォルダーを作成するには、`apps`フォルダーを右クリックし、**[!UICONTROL 作成]** / **[!UICONTROL ノードを作成]**&#x200B;を選択します。 名前を`ws`に指定し、タイプを`sling:Folder`に選択して、「**[!UICONTROL OK]**」をクリックします。 「**[!UICONTROL すべて保存]**」をクリックします。
1. `/apps/ws`を参照し、「**[!UICONTROL アクセス制御]**」タブに移動します。
1. 「**[!UICONTROL リポジトリ]**」オプションを選択します。 「**[!UICONTROL アクセス制御]**」リストで、「**[!UICONTROL +]**」をクリックして新しいエントリを追加します。 もう一度「**[!UICONTROL +]**」をクリックします。
1. **PERM_WORKSPACE_USER**&#x200B;プリンシパルを検索して選択します。

   ![HTML Workspace をカスタマイズするための汎用手順の一部として PERM_WORKSPACE_USER プリンシパルを選択します](assets/perm_workspace_user.png)

1. プリンシパルに`jcr:read`権限を付与します。
1. 「**[!UICONTROL すべて保存]**」をクリックします。
1. `GET.jsp`、`index`および`html.jsp`ファイルを`/libs/ws`フォルダーから`/apps/ws`フォルダーにコピーします。
1. `/apps/ws`フォルダーの`/libs/ws/locales`フォルダーをコピーします。 「**[!UICONTROL すべて保存]**」をクリックします。
1. `GET.jsp`ファイル内の参照と相対パスを更新し、「**[!UICONTROL すべて保存]**」をクリックします。

   ```javascript
   <meta http-equiv="refresh" content="0;URL='/lc/apps/ws/index.html'" />
   ```

1. CSS のカスタマイズは以下のようにして実行します。

   1. `/apps/ws`フォルダーに移動し、`css`という名前の新しいフォルダーを作成します。

   1. `css`フォルダーに、`newStyle.css`という名前の新しいファイルを作成します。

   1. `/apps/ws/html`.jspを開き、

   ```javascript
   <link lang="en" rel="stylesheet" type="text/css" href="css/style.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="css/jquery-ui.css"/>
   ```

   コピー先：

   ```javascript
   <link lang="en" rel="stylesheet" type="text/css" href="../../libs/ws/css/style.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="css/newStyle.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="../../libs/ws/css/jquery-ui.css"/>
   ```

   >[!NOTE]
   >
   >上に示すように、ユーザー定義CSSファイルのエントリを、style.cssのエントリの後に配置します。

1. /apps/ws/html.jsp ファイルで、

   ```jsp
   <script data-main="js/main" src="js/libs/require/require.js"></script>
   ```

   コピー先：

   ```jsp
   <script data-main="js/main" src="../../libs/ws/js/libs/require/require.js"></script>
   ```

1. 以下の操作を実行します。

   1. `js`という名前のフォルダーを`/apps/ws`に作成します。 「**[!UICONTROL すべて保存]**」をクリックします。

   1. `libs`という名前のフォルダーを`/apps/ws/js`に作成します。 「**[!UICONTROL すべて保存]**」をクリックします。

   1. `/libs/ws/js/libs/jqueryui`フォルダーを`/apps/ws/js/libs`にコピーします。 「**[!UICONTROL すべて保存]**」をクリックします。

1. HTML のカスタマイズは以下のようにして実行します。

   1. `/apps/ws/js`の下に、`runtime`という名前のフォルダーを作成します。 「**[!UICONTROL すべて保存]**」をクリックします。

   1. `/apps/ws/js/runtime`の下に、`templates`という名前のフォルダーを作成します。 「**[!UICONTROL すべて保存]**」をクリックします。

   1. `/libs/ws/js/main.js` を `/apps/ws/js/main.js` にコピーします。

   1. /libs/ws/js/registry.jsを`/apps/ws/js/registry.js`にコピーします。

1. 「**[!UICONTROL Save All]**」をクリックし、キャッシュをクリアして AEM Forms Workspace を更新します。

   URL `https://'[server]:[port]'/lc/ws`にアクセスし、管理者/パスワードの資格情報を使用してログインします。 ブラウザーは`https://'[server]:[port]'/lc/apps/ws/index.html`にリダイレクトします。
