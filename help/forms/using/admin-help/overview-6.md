---
title: SSL 設定の概要
description: SSL を設定して通信のセキュリティを強化する方法について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: fbe1487e-c830-4be8-9841-6022e6a98ae7
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 100%

---

# SSL 設定の概要 {#overview-of-configuring-ssl}

Secure Sockets Layer（SSL）資格情報を作成し、アプリケーションサーバーで SSL を設定して、アプリケーションサーバーとの通信のセキュリティを強化できます。

Rights Management はセキュリティ製品なので、SSL の設定が必要です。SSL 証明書を設定する場合は、RSA キーのみを使用していることを確認してください。DSA キーによる SSL 証明書はサポートされていません。

ここでの情報は、自動インストールと手動インストールの両方に適用されます。SSL の設定方法の例を紹介します。ネットワークまたは組織に、より適した他の方法を使用することもできます。

>[!NOTE]
>
>アプリケーションサーバーで SSL を設定する前に、AEM Forms モジュールのインストール、設定およびデプロイを完了し、製品が正常に動作することを確認しておくことをお勧めします。

>[!NOTE]
>
>SSL セキュリティ証明書および資格情報を作成するときは、アプリケーションサーバーを実行するのに使用したユーザーアカウント権限と同じ権限を使用します。他のユーザー権限を使用してアプリケーションサーバーを実行している場合は、ContentRootURI が https を指すときに、そのフォームで PDFForm のレンダリングが正しく行われないことがあります。

SSL 対応の LDAP サーバーがある場合は、それと連携するように User Management を設定します（[SSL 対応の LDAP サーバーを対象とした User Management の設定](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server)を参照）。
