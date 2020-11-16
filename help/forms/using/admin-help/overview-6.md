---
title: SSL 設定の概要
seo-title: SSL 設定の概要
description: SSL を設定して通信のセキュリティを強化する方法について説明します。
seo-description: SSL を設定して通信のセキュリティを強化する方法について説明します。
uuid: 3e99d2bf-137b-45ba-8384-309624094623
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8e107abb-861f-4063-b600-c87e34639019
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 100%

---


# SSL 設定の概要 {#overview-of-configuring-ssl}

Secure Sockets Layer（SSL）秘密鍵証明書を作成し、アプリケーションサーバーで SSL を設定して、アプリケーションサーバーとの通信のセキュリティを強化できます。

Rights Management はセキュリティ製品なので、SSL の設定が必要です。SSL 証明書を設定する場合は、RSA キーのみを使用していることを確認してください。DSA キーによる SSL 証明書はサポートされていません。

ここでの情報は、自動インストールと手動インストールの両方に適用されます。SSL の設定方法の例を紹介します。ネットワークまたは組織により適した他の方法を使用することもできます。

>[!NOTE]
>
>アプリケーションサーバーで SSL を設定する前に、AEM Forms モジュールのインストール、設定およびデプロイを完了し、製品が正常に動作することを確認しておくことをお勧めします。

>[!NOTE]
>
>SSL セキュリティ証明書および秘密鍵証明書を作成するときは、アプリケーションサーバーを実行するのに使用したユーザーアカウント権限と同じユーザーアカウント権限を使用します。他のユーザー権限を使用してアプリケーションサーバーを実行している場合は、ContentRootURI が https を指すときに、そのフォームで PDFForm のレンダリングが正しく行われないことがあります。

SSL 対応 LDAP サーバーがある場合、それと連携するように UserManagement を設定します（[SSL 対応の LDAP サーバーを対象とした User Management の設定](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server)を参照）。
