---
title: SSL 設定の概要
description: SSL を設定して通信のセキュリティを強化する方法について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: fbe1487e-c830-4be8-9841-6022e6a98ae7
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 3%

---

# SSL 設定の概要 {#overview-of-configuring-ssl}

Secure Sockets Layer(SSL) 資格情報を作成し、アプリケーションサーバーで SSL を設定して、アプリケーションサーバーとの通信のセキュリティを強化できます。

セキュリティ製品の場合、Rights Managementには SSL の設定が必要です。 SSL 証明書を設定する場合は、必ず RSA キーのみを使用します。 DSA キーを使用した SSL 証明書はサポートされていません。

入力した情報は、自動インストール、自動インストールおよび手動インストールに適用されます。 SSL を設定するためのメソッドの例を示しています。 また、ネットワークや組織に適した他の方法を使用することもできます。

>[!NOTE]
>
>AEM forms モジュールのインストール、設定およびデプロイを完了し、アプリケーションサーバーで SSL を設定する前に、製品が正しく実行されていることを確認することをお勧めします。

>[!NOTE]
>
>SSL セキュリティ証明書および資格情報を作成する場合は、アプリケーションサーバーの実行に使用したのと同じユーザーアカウント権限を使用します。 他のユーザー権限を使用してアプリケーションサーバーを実行する場合、ContentRootURI が https を指すと、フォームが PDFForm のレンディションに対して正しくレンダリングされないことがあります。

SSL が有効な LDAP サーバーがある場合、User Management を設定して LDAP サーバーと連携します。 ( 詳しくは、 [SSL が有効な LDAP サーバー用の User Management の設定](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server).)
