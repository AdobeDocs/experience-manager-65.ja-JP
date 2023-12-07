---
title: Connector for Microsoft SharePoint の設定
description: Connector for Microsoft SharePointを設定して、AEM forms とMicrosoft SharePoint間の通信を有効にします。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: a8be58f1-1961-4bf5-aaad-feb4489fb389
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 60%

---

# Connector for Microsoft SharePoint の設定 {#configuring-connector-for-microsoft-sharepoint}

Connector for Microsoft SharePointは、AEM forms とMicrosoft SharePoint間の通信を可能にします。 その他の背景情報については、 [サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

1. 管理コンソールで、サービス/Microsoft SharePoint用コネクタをクリックします。
1. SharePoint Server の次の設定を指定します。

   **SharePoint サーバーホスト名**：SharePoint サーバー上の eb アプリケーションのホスト名ポート番号（`[hostname]:'port'` の形式）。

   **ユーザー名**：SharePoint サーバーへの接続に使用するユーザーアカウントのパスワード。

   **パスワード**：SharePoint サーバーへの接続に使用するユーザーアカウントのパスワード。

   **ドメイン名**：SharePoint サーバーがあるドメイン。

1. 「保存」をクリックします。

## Microsoft SharePoint Configuration Service {#microsoft-sharepoint-configuration-service}

Microsoft SharePoint Configuration サービス（`(MSSharePointConfigService)`）を使用して、他のユーザーとしての権限（仮想権限）を持つ AEM Forms ユーザー用に秘密鍵証明書を指定できます。他のユーザーとしての権限については、「[Connector for Microsoft SharePoint の設定](https://help.adobe.com/ja_JP/AEMForms/6.1/SharePointConfig/index.html)」を参照してください。`MSSharePointConfigService` の設定を指定するには、次の手順を実行します。

1. 管理コンソールで、サービス／アプリケーションおよびサービス／サービスの管理をクリックします。
1. サービスのリストに移動して、`MSSharePointConfigService` をクリックします。
1. 設定ページで、次の設定を指定します。

   * 他のユーザーとしての権限を持つユーザーのユーザー名
   * 上記のユーザーのパスワード

1. 「保存」をクリックします。
