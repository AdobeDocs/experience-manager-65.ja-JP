---
title: ブランディングのための組織ロゴの変更
seo-title: Changing the organization logo for branding
description: AEM Forms Workspace をブランド化するには、デフォルトのロゴをカスタマイズして組織のロゴを提供します。
seo-description: To brand AEM Forms workspace provide the logo of your organization by customizing the default logo.
uuid: f0c340ee-2e54-4bb0-9c30-383cc1bbadb8
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 2c651302-f4ef-4211-b897-f5942ed0ffb1
exl-id: 49572f2a-f3ec-4ee6-98b8-2563de1cf96c
source-git-commit: 30327950779337ce869b6ca376120bc09826be21
workflow-type: ht
source-wordcount: '133'
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
   >WebDAV アクセスの詳細については、 [https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ja) を参照してください。

1. 次のスタイルを追加することによって、/apps/ws/css/newStyle.css にあるスタイルシートの新しいロゴ画像を参照します。

   ```css
   #logo {
   
          background: url(../images/NewWorkspace.png) no-repeat 14px 11px;
   
   }
   ```
