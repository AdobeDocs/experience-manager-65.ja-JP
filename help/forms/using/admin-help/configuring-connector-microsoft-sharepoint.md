---
title: Connector for Microsoft SharePoint の設定
seo-title: Connector for Microsoft SharePoint の設定
description: Connector for Microsoft SharePoint を設定し、AEM Forms と Microsoft SharePoint 間の通信を実現します。
seo-description: Connector for Microsoft SharePoint を設定し、AEM Forms と Microsoft SharePoint 間の通信を実現します。
uuid: f1561b41-da20-4220-b13a-e78472a9449f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0ec881c9-8dcc-4847-9edf-24d9e6c4a7ea
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Connector for Microsoft SharePoint の設定 {#configuring-connector-for-microsoft-sharepoint}

Connector for Microsoft SharePoint は、AEM Forms と Microsoft SharePoint 間の通信を実現します。関連する参考情報については、「[サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)」の「Connectors for ECM」を参照してください。

1. 管理コンソールで、サービス／Connector for Microsoft SharePoint をクリックします。
1. SharePoint Server の次の設定を指定します。

   **SharePoint Serverホスト名：** SharePointサーバー上のWebアプリケーションのホスト名のポート番号を、形式で指定しま `[hostname]:'port'`す。

   **ユーザー名：** SharePointサーバーへの接続に使用するユーザーアカウント。

   **パスワード：** SharePointサーバーへの接続に使用するユーザーアカウントのパスワード

   **ドメイン名：** SharePointサーバーが存在するドメイン。

1. 「保存」をクリックします。

## Microsoft SharePoint Configuration サービス {#microsoft-sharepoint-configuration-service}

The Microsoft SharePoint configuration service `(MSSharePointConfigService)` lets you specify credentials for the AEM forms user that has impersonation permissions. 他のユーザーとしての権限については、「[Connector for Microsoft SharePoint の設定](https://help.adobe.com/en_US/AEMForms/6.1/SharePointConfig/index.html)」を参照してください。`MSSharePointConfigService` の設定を指定するには、次の手順を実行します。

1. 管理コンソールで、サービス／アプリケーションおよびサービス／サービスの管理をクリックします。
1. サービスのリストに移動して、`MSSharePointConfigService` をクリックします。
1. 設定ページで次の設定を指定します。

   * 仮装権限を持つユーザーのユーザー名
   * 上記ユーザーのパスワード

1. 「保存」をクリックします。

