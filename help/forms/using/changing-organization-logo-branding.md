---
title: ブランディングのための組織ロゴの変更
seo-title: ブランディングのための組織ロゴの変更
description: AEM Forms Workspace をブランディングするには、デフォルトのロゴをカスタマイズして組織のロゴを指定します。
seo-description: AEM Forms Workspace をブランディングするには、デフォルトのロゴをカスタマイズして組織のロゴを指定します。
uuid: f0c340ee-2e54-4bb0-9c30-383cc1bbadb8
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 2c651302-f4ef-4211-b897-f5942ed0ffb1
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# ブランディングのための組織ロゴの変更 {#changing-the-organization-logo-for-branding}

組織ロゴは AEM Forms Workspace の左上隅に表示されます。ロゴを更新するには、[AEM Forms Workspace のカスタマイズの一般的な手順](/help/forms/using/generic-steps-html-workspace-customization.md#generic-steps-for-html-workspace-customization)および次の手順に従います。

1. ロゴを作成してファイルに `NewWorkspace.png` と名前を付けます。WebDAV クライアントを使用して画像ファイルを /apps/ws/images フォルダーに配置します。

   >[!NOTE]
   >
   >ロゴの画像の推奨サイズは 218 ピクセル × 20 ピクセルです。

   >[!NOTE]
   >
   >For more information about WebDAV access, see [https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://docs.adobe.com/docs/en/crx/current/how_to/webdav_access.html).

1. 次のスタイルを追加することによって、/apps/ws/css/newStyle.css にあるスタイルシートの新しいロゴ画像を参照します。

   ```css
   #logo {
   
          background: url(../images/NewWorkspace.png) no-repeat 14px 11px;
   
   }
   ```
