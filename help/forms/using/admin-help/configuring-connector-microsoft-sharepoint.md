---
title: Connector for Microsoft SharePoint の設定
seo-title: Configuring Connector for Microsoft SharePoint
description: Connector for Microsoft SharePoint を設定し、AEM Forms と Microsoft SharePoint 間の通信を実現します。
seo-description: Configure Connector for Microsoft SharePoint to enable communication between AEM forms and Microsoft SharePoint.
uuid: f1561b41-da20-4220-b13a-e78472a9449f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0ec881c9-8dcc-4847-9edf-24d9e6c4a7ea
exl-id: a8be58f1-1961-4bf5-aaad-feb4489fb389
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '213'
ht-degree: 100%

---

# Connector for Microsoft SharePoint の設定 {#configuring-connector-for-microsoft-sharepoint}

Connector for Microsoft SharePoint は、AEM Forms と Microsoft SharePoint 間の通信を実現します。関連する参考情報については、「[サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)」の「Connectors for ECM」を参照してください。

1. 管理コンソールで、サービス／Connector for Microsoft SharePoint をクリックします。
1. SharePoint Server の次の設定を指定します。

   **SharePoint サーバーホスト名**：SharePoint サーバー上の eb アプリケーションのホスト名ポート番号（`[hostname]:'port'` の形式）。

   **ユーザー名**：SharePoint サーバーへの接続に使用するユーザーアカウントのパスワード。

   **パスワード**：SharePoint サーバーへの接続に使用するユーザーアカウントのパスワード。

   **ドメイン名**：SharePoint サーバーがあるドメイン。

1. 「保存」をクリックします。

## Microsoft SharePoint Configuration サービス {#microsoft-sharepoint-configuration-service}

Microsoft SharePoint Configuration サービス（`(MSSharePointConfigService)`）を使用して、他のユーザーとしての権限（仮想権限）を持つ AEM Forms ユーザー用に秘密鍵証明書を指定できます。他のユーザーとしての権限については、「[Connector for Microsoft SharePoint の設定](https://help.adobe.com/ja_JP/AEMForms/6.1/SharePointConfig/index.html)」を参照してください。`MSSharePointConfigService` の設定を指定するには、次の手順を実行します。

1. 管理コンソールで、サービス／アプリケーションおよびサービス／サービスの管理をクリックします。
1. サービスのリストに移動して、`MSSharePointConfigService` をクリックします。
1. 設定ページで次の設定を指定します。

   * 仮装権限を持つユーザーのユーザー名
   * 上記ユーザーのパスワード

1. 「保存」をクリックします。
