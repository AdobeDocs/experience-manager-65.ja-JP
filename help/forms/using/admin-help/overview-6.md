---
title: SSL 設定の概要
description: SSL を設定して通信のセキュリティを強化する方法について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: fbe1487e-c830-4be8-9841-6022e6a98ae7
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 100%
---
# SSL 設定の概要 {#overview-of-configuring-ssl}

Secure Sockets Layer（SSL）資格情報を作成し、アプリケーションサーバーで SSL を設定して、アプリケーションサーバーとの通信のセキュリティを強化できます。

Rights Management はセキュリティ製品なので、SSL の設定が必要です。 SSL 証明書を設定する場合は、RSA キーのみを使用していることを確認してください。 DSA キーによる SSL 証明書はサポートされていません。

ここでの情報は、ターンキーインストール、自動インストール、手動インストールに適用されます。 SSL の設定方法の例を紹介します。 ネットワークまたは組織に、より適した他の方法を使用することもできます。

>[!NOTE]
>
>アプリケーションサーバーで SSL を設定する前に、AEM Forms モジュールのインストール、設定およびデプロイを完了し、製品が正常に動作することを確認しておくことをお勧めします。

>[!NOTE]
>
>SSL セキュリティ証明書および資格情報を作成するときは、アプリケーションサーバーを実行するのに使用したユーザーアカウント権限と同じ権限を使用します。 他のユーザー権限を使用してアプリケーションサーバーを実行している場合は、ContentRootURI が https を指すときに、そのフォームで PDFForm のレンダリングが正しく行われないことがあります。

SSL 対応の LDAP サーバーがある場合は、それと連携するようにユーザー管理を設定します （[SSL 対応の LDAP サーバーを対象としたユーザー管理の設定](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server)を参照）。
