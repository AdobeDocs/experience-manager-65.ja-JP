---
title: インターフェイスのカラースキーム変更
seo-title: インターフェイスのカラースキーム変更
description: AEM Forms Workspace ユーザーインターフェイス部分のカラースキームを選択して変更する方法。
seo-description: AEM Forms Workspace ユーザーインターフェイス部分のカラースキームを選択して変更する方法。
uuid: 32c32f7a-8271-4d2c-8a1f-ad5ab3c90b83
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 18dab82a-badf-4c32-83a2-cd5cb04cae89
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# インターフェイスのカラースキーム変更 {#changing-the-color-scheme-of-the-interface}

AEM Forms Workspace ユーザーインターフェイス部分のカラースキームを必要に合わせて変更できます。代表的なカラースキームのカスタマイズの例を以下にいくつか示します。In addition to the steps discussed in this article, see [Generic steps for AEM Forms workspace customization](/help/forms/using/generic-steps-html-workspace-customization.md).

## トップナビゲーションバー {#top-navigation-bar}

### 背景画像の使用 {#using-background-image}

AEM Forms Workspace 上部のナビゲーションバーを更新するには：

1. 背景画像を作成して色を更新します。ファイルに newBackground.jpg と名前を付けます。
1. WebDAV クライアントを使用して背景画像を /apps/ws/images フォルダーにアップロードします。

   >[!NOTE]
   >
   >For more information about WebDAV access, see [https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://docs.adobe.com/docs/en/crx/current/how_to/webdav_access.html).

1. 次のスタイルを追加することによって、/apps/ws/css/newStyle.css にある新しい背景画像を参照します。

   ```css
   #header {
       background:#292929 url(../images/newBackground.jpg) repeat-x;
   }
   ```

### CSS におけるカラープロパティの使用 {#using-color-property-in-css}

1. /apps/ws/css にある newStyle.css に次のスタイルを追加します。

   ```css
   #header {
   background : none;
   background-color: gray;
   }
   ```

## カテゴリコンポーネント {#category-component}

カテゴリコンポーネントは、左パネルでタスクのさまざまなカテゴリを表示します。 To change its color, define the background color in `.category` element of the CSS file.

## タスクコンポーネント {#task-component}

タスクは、TaskList コンポーネントと呼ばれる中央のパネルに表示されます。色を変更するには、スタイルシートの。タスクセレクターに関連付けられたスタイルを変更します。
