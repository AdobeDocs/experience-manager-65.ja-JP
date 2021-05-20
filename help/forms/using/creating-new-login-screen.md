---
title: 新しいログイン画面の作成
seo-title: 新しいログイン画面の作成
description: AEM Forms Workspace または Forms Manager を例にした、LiveCycle モジュールのログインページの変更方法。
seo-description: AEM Forms Workspace または Forms Manager を例にした、LiveCycle モジュールのログインページの変更方法。
uuid: 2d4a72f4-cc9a-412d-856d-0fca75f1272b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 35497785-263d-44b1-9ee4-85921997295b
docset: aem65
exl-id: 5cb906b6-6a3c-498c-94f5-27a9071ea934
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 60%

---

# 新規ログイン画面の作成{#creating-a-new-login-screen}

AEM Forms ログイン画面を使用するすべての AEM Forms モジュールのログイン画面を変更することができます。例えば、変更すると Forms Manager および AEM Forms Workspace の両方のログイン画面に影響が及びます。

## 前提条件 {#prerequisite}

1. `/lc/crx/de`に管理者権限でログインします。
1. 次のアクションを実行します。

   1. 階層構造を複製します。の`/libs/livecycle/core/content`を`/apps/livecycle/core/content`に配置します。

      同じ（ノード/フォルダー）プロパティおよびアクセス制御を保持します。

   1. コンテンツフォルダーをコピーします。

      追加の: `/libs/livecycle/core`

      を: `/apps/livecycle/core`.

   1. `/apps/livecycle/core`フォルダーの内容を削除します。

1. 次の操作を実行します。

   1. 階層構造を複製します。の`/libs/livecycle/core/components/login`を`/apps/livecycle/core/components/login`に配置します。 同じ（ノード/フォルダー）プロパティおよびアクセス制御を保持します。

   1. componentsフォルダーをコピーします。`/libs/livecycle/core`から`/apps/livecycle/core`まで。

   1. フォルダーの内容を削除します。`/apps/livecycle/core/components/login`.

### 新しいロケールの追加 {#adding-a-new-locale}

1. `i18n`フォルダーをコピーします。

   * コピー元：`/libs/livecycle/core/components/login`
   * コピー先：`/apps/livecycle/core/components/login`

1. `i18n`内のフォルダー（`en`を除く）をすべて削除します。

1. フォルダー `en` で、以下のアクションを実行します。

   1. フォルダーの名前をサポートするロケール名に変更します。（例：`ar`）。

   1. プロパティ`jcr:language`の値を`ar`（`ar`フォルダー用）に変更します。
   >[!NOTE]
   >
   >`ar-DZ` のようにロケールが言語と国コードの組み合わせである場合は、フォルダー名とプロパティ値を `ar-DZ` に変更します。

1. コピー `login.jsp`:

   * コピー元：`/libs/livecycle/core/components/login`
   * コピー先：`/apps/livecycle/core/components/login`

1. `/apps/livecycle/core/components/login/login.jsp`のコードの次のスニペットを変更します。

***ロケールが言語コードである場合***

```jsp
String browserLocale = "en";

    for(int i=0; i<locales.length; i++)
    {
        String prioperty = locales[i];
        if(prioperty.trim().startsWith("en")) {
            browserLocale = "en";
            break;
        }
        if(prioperty.trim().startsWith("de")){
            browserLocale = "de";
            break;
        }
        if(prioperty.trim().startsWith("ja")){
            browserLocale = "ja";
            break;
        }
        if(prioperty.trim().startsWith("fr")){
            browserLocale = "fr";
            break;
        }
    }
```

To

```jsp
String browserLocale = "en";
    for(int i=0; i<locales.length; i++)
    {
        String prioperty = locales[i];
        if(prioperty.trim().startsWith("ar")) {
            browserLocale = "ar";
            break;
        }
        if(prioperty.trim().startsWith("en")) {
            browserLocale = "en";
            break;
        }
        if(prioperty.trim().startsWith("de")){
            browserLocale = "de";
            break;
        }
        if(prioperty.trim().startsWith("ja")){
            browserLocale = "ja";
            break;
        }
        if(prioperty.trim().startsWith("fr")){
            browserLocale = "fr";
            break;
        }
    }
```

```jsp
String browserLocale = "en";

    for(int i=0; i<locales.length; i++)
    {
        String prioperty = locales[i];
        if(prioperty.trim().startsWith("en")) {
            browserLocale = "en";
            break;
        }
        if(prioperty.trim().startsWith("de")){
            browserLocale = "de";
            break;
        }
        if(prioperty.trim().startsWith("ja")){
            browserLocale = "ja";
            break;
        }
        if(prioperty.trim().startsWith("fr")){
            browserLocale = "fr";
            break;
        }
    }
```

設定値

```jsp
String browserLocale = "en";
    for(int i=0; i<locales.length; i++)
    {
        String prioperty = locales[i];
        if(prioperty.trim().equalsIgnoreCase("ar-DZ")) {
            browserLocale = "ar-DZ";
            break;
        }
        if(prioperty.trim().startsWith("en")) {
            browserLocale = "en";
            break;
        }
        if(prioperty.trim().startsWith("de")){
            browserLocale = "de";
            break;
        }
        if(prioperty.trim().startsWith("ja")){
            browserLocale = "ja";
            break;
        }
        if(prioperty.trim().startsWith("fr")){
            browserLocale = "fr";
            break;
        }
    }
```

***デフォルトのロケールを変更するには***

```jsp
   String browserLocale = "en";
   for(int i=0; i<locales.length; i++)

   To

   String browserLocale = "ar";
   for(int i=0; i<locales.length; i++)
```

### 新しいテキストの追加、または既存のテキストの変更  {#adding-new-text-or-modifying-existing-text}

1. `i18n`フォルダーをコピーします。

   * コピー元：`/libs/livecycle/core/components/login`
   * コピー先：`/apps/livecycle/core/components/login`

1. ここで、テキストを変更するノード（該当するロケールコードフォルダの下）のプロパティ `sling:message` の値を変更します。翻訳は、ノードのプロパティ `sling:key` の値に示されているキーを介して行われます。

1. 新しいキーと値のペアを追加するには、次のアクションを実行します。次に続くスクリーンショットの例を確認してください。

   1. `sling:MessageEntry` タイプのノードを作成するか、またはすべてのロケールフォルダーの下で既存のノードをコピーして名前を変更します。
   1. コピー `login.jsp` :

      * コピー元：`/libs/livecycle/core/components/login`

      * コピー先：`/apps/livecycle/core/components/login`
   1. `/apps/livecycle/core/components/login/login.jsp`を変更して、新しく追加したテキストを取り込みます。

   ![新しいキーと値のペアを追加する](assets/capture_new.png)

   ```jsp
   div class="loginContent">
   
                       <span class="loginFlow"></code>
                       <span class="loginVersion"><%= i18n.get("Version: 11.0.0") %></code>
                       <span class="loginTitle"><%= i18n.get("Login") %></code>
                       <% if (loginFailed) {%>
   ```

   設定値

   ```jsp
   div class="loginContent">
   
                       <span class="loginFlow"></code>
                       <span class="loginVersion"><%= i18n.get("My Welcome Message") %></code>
                       <span class="loginVersion"><%= i18n.get("Version: 11.0.0") %></code>
                       <span class="loginTitle"><%= i18n.get("Login") %></code>
                       <% if (loginFailed) {%>
   ```

### 新しいスタイルの追加、または既存のスタイルの変更 {#adding-new-style-or-modifying-existing-style}

1. `login`ノードをコピーします。

   * コピー元：`/libs/livecycle/core/content`
   * コピー先：`/apps/livecycle/core/content`

1. ノード`/apps/livecycle/core/content/login.`から`login.js`と`jquery-1.8.0.min.js`を削除します。
1. CSS ファイルのスタイルを変更します。
1. 新しいスタイルを追加するには：

   1. `/apps/livecycle/core/content/login/login.css`に新しいスタイルを追加する
   1. コピー `login.jsp`

      * コピー元：`/libs/livecycle/core/components/login`

      * コピー先：`/apps/livecycle/core/components/login`
   1. `/apps/livecycle/core/components/login/login.jsp`を変更して、新しく追加したスタイルを取り込みます。



以下に例を示します。

* `/apps/livecycle/core/content/login/login.css`に次を追加します。

```
css.newLoginContentArea {
    width: 700px;
    padding: 100px 0px 0px 100px;
   }
```

* `/apps/livecycle/core/components/login.jsp`でフォローを変更します。


   ```jsp
   <div class="loginContentArea">
   ```

   設定値

   ```jsp
   <div class="newLoginContentArea">
   ```

>[!NOTE]
>
>`/apps/livecycle/core/content/login`（`/libs/livecycle/core/content/login`からコピー）内の既存の画像が削除された場合は、対応する参照をCSSから削除します。

### 新しい画像の追加 {#add-new-images}

1. 新しいスタイルの追加または既存のスタイルの変更の手順に従います（前述）。
1. `/apps/livecycle/core/content/login`に新しい画像を追加します。 画像を追加するには：

   1. WebDAV クライアントをインストールします。
   1. webDAVクライアントを使用して`/apps/livecycle/core/content/login`フォルダーに移動します。 詳しくは、次を参照してください。[https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://docs.adobe.com/docs/en/crx/current/how_to/webdav_access.html).

   1. 新しい画像を追加します。

1. `/apps/livecycle/core/content/login`に追加された新しい画像に対応する新しいスタイルを`/apps/livecycle/core/content/login/login.css,`に追加します。
1. `/apps/livecycle/core/components`の`login.jsp`で新しいスタイルを使用します。

以下に例を示します。


```css
.newLoginContainerBkg {

 background-image: url(my_Bg.gif);
 background-repeat: no-repeat;
 background-position: left top;
 width: 727px;
}
```


    * /apps/livecycle/core/components/login.jspで以下を変更します。

```jsp
<div class="loginContainerBkg">
```

設定値

```jsp
<div class="newLginContainerBkg">
```
