---
title: Connector for Microsoft SharePoint の設定
description: Connector for Microsoft SharePoint を設定し、AEM Forms と Microsoft SharePoint 間の通信を実現します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: a8be58f1-1961-4bf5-aaad-feb4489fb389
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms
source-git-commit: 9f59606bb58b9e90f07bd22e89f3213afb54a697
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 100%

---

# Connector for Microsoft SharePoint の設定 {#configuring-connector-for-microsoft-sharepoint}

Connector for Microsoft SharePoint は、AEM Forms と Microsoft SharePoint 間の通信を実現します。その他の背景情報について詳しくは、[サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)にある「ECM 用コネクター」を参照してください。

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

   * 偽装権限を持つユーザーのユーザー名
   * 上記ユーザーのパスワード

1. 「保存」をクリックします。
