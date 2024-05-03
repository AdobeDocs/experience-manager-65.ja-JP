---
title: ブランディングのための組織ロゴの変更
description: AEM Forms Workspace をブランド化するには、デフォルトのロゴをカスタマイズして組織のロゴを提供します。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 49572f2a-f3ec-4ee6-98b8-2563de1cf96c
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 100%

---

# ブランディングのための組織ロゴの変更 {#changing-the-organization-logo-for-branding}

組織のロゴは、AEM Forms Workspace の左上隅に表示されます。ロゴを更新するには、[AEM Forms Workspace のカスタマイズの一般的な手順](/help/forms/using/generic-steps-html-workspace-customization.md#generic-steps-for-html-workspace-customization)に従い、次の手順を実行します。

1. ロゴを作成してファイルに `NewWorkspace.png` と名前を付けます。WebDAV クライアントを使用して、/apps/ws/images フォルダーに画像ファイルを配置します。

   >[!NOTE]
   >
   >ロゴ画像の推奨サイズは 218 ピクセル × 20 ピクセル です。

   >[!NOTE]
   >
   >詳しくは、[WebDAV アクセス](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/webdav-access.html?lang=ja)を参照してください。

   [WebDAV アクセス](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/webdav-access.html?lang=ja)

1. 次のスタイルを追加することによって、/apps/ws/css/newStyle.css にあるスタイルシートの新しいロゴ画像を参照します。

   ```css
   #logo {
   
          background: url(../images/NewWorkspace.png) no-repeat 14px 11px;
   
   }
   ```
