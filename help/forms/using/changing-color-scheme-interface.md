---
title: インターフェイスのカラースキームの変更
description: AEM Forms Workspace のユーザーインターフェイス部分のカラースキームを選択的に変更する方法。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: e0a261a2-518b-4984-a5b5-24f0b9222e24
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '209'
ht-degree: 100%

---

# インターフェイスのカラースキームの変更 {#changing-the-color-scheme-of-the-interface}

AEM Forms Workspace のユーザーインターフェイス部分のカラースキームは、要件に合わせて変更できます。代表的なカラースキームのカスタマイズの例を以下にいくつか示します。この記事の手順に加えて、「[AEM Forms Workspace のカスタマイズの一般的な手順](/help/forms/using/generic-steps-html-workspace-customization.md)」を参照してください。

## 上部ナビゲーションバー {#top-navigation-bar}

### 背景画像の使用 {#using-background-image}

AEM Forms Workspace の上部にあるナビゲーションバーを更新する手順は次のとおりです。

1. 背景画像を作成してカラーを更新します。ファイルに newBackground.jpg と名前を付けます。
1. WebDAV クライアントを使用して、背景画像を /apps/ws/images フォルダーにアップロードします。

   >[!NOTE]
   >
   >詳しくは、[WebDAV アクセス](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/webdav-access.html?lang=ja)を参照してください。

1. 次のスタイルを追加して、/apps/ws/css/newStyle.css の新しい背景画像を参照します。

   ```css
   #header {
       background:#292929 url(../images/newBackground.jpg) repeat-x;
   }
   ```

### CSS のカラープロパティの使用 {#using-color-property-in-css}

1. /apps/ws/css にある newStyle.css に次のスタイルを追加します。

   ```css
   #header {
   background : none;
   background-color: gray;
   }
   ```

## カテゴリコンポーネント {#category-component}

カテゴリコンポーネントは、左パネルでタスクのさまざまなカテゴリを表示します。この色を変更するには、CSS ファイルの`.category`要素で、背景色を定義します。

## タスクコンポーネント {#task-component}

タスクは、TaskList コンポーネントと呼ばれる中央のパネルに表示されます。色を変更するには、スタイルシートにある .task セレクターに関連付けられたスタイルを変更します。
