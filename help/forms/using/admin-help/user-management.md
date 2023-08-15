---
title: ユーザー管理
seo-title: User Management
description: User Management では、SAML を使用して、AEM forms モジュールと Netegrity SiteMinder で保護されたアプリケーションとの間で SSO を有効にできます。 このドキュメントでは、User Management の詳細を説明します。
seo-description: User Management lets you enable SSO between AEM forms modules and Netegrity SiteMinder-protected applications by using SAML. This document provides more information about User Management.
uuid: f0c8331a-d995-483d-97b7-259df53b1a1a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 10e6177a-8228-4515-aba9-bbe59bede449
exl-id: 1da1f6de-ac0d-4e0d-b8bb-956420e42699
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 6%

---

# User Management {#user-management}

User Management では、Security Assertion Markup Language(SAML) を使用して、AEM forms モジュールと Netegrity SiteMinder で保護されたアプリケーションとの間でシングルサインオン (SSO) を有効にできます。 SSO を実装すると、AEM forms のユーザーログインページは不要になり、ユーザーが会社のポータルで既に認証されている場合は表示されません。

DB2 のデータベースおよびディレクトリ同期のパフォーマンスを向上させる方法については、 [IBM DB2 データベース：定期メンテナンス用のコマンドの実行](/help/forms/using/admin-help/ibm-db2-database-running-commands.md#ibm-db2-database-running-commands-for-regular-maintenance).

## SSL が有効な LDAP サーバー用の User Management の設定 {#configuring-user-management-for-an-ssl-enabled-ldap-server}

SSL が有効な LDAP サーバーがある場合、User Management を設定して LDAP サーバーと連携します。 ( 詳しくは、 [SSL が有効な LDAP サーバー用の User Management の設定](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server).)

## Document Security で使用するユーザー権限の設定 {#setting-user-privileges-for-use-with-document-security}

ユーザーおよびグループを作成するための適切な権限を持つ管理者ユーザーを作成します。 AEM forms 環境に Document Security が含まれる場合は、招待ユーザーおよびローカルユーザーを管理する権限を、これらのユーザーの管理者になるユーザーに付与します。 また、管理コンソールの「ユーザーの役割」を割り当てて、ユーザーに管理コンソールへのアクセス権を付与します。 ( 詳しくは、 [ロールの作成と設定](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles).)

ポリシー・ユーザーの検索中に選択したドメインのユーザーとグループを表示するには、スーパー管理者またはポリシー・セット管理者が、作成した各ポリシー・セットの表示されるユーザーとグループ・リストにドメイン（User Management で作成）を選択して追加する必要があります。

表示されるユーザーとグループの一覧は、ポリシーセットコーディネーターに表示され、ポリシーに追加するユーザーまたはグループを選択する際にエンドユーザーが参照できるドメインを制限するために使用されます。 このタスクを実行しない場合、ポリシーセットコーディネーターは、ポリシーに追加するユーザーまたはグループを見つけられません。 任意のポリシーセットに対して、複数のポリシーセットコーディネーターを設定できます。

>[!NOTE]
>
>ドメインの作成は、ポリシーを作成する前におこなう必要があります。

### 表示されるユーザーおよびグループの設定 {#set-visible-users-and-groups}

AEM forms 環境を Document Security でインストールして設定した後、User Management で適切なドメインをすべて設定します。

1. 管理コンソールで、サービス/Document Security/ポリシーをクリックし、「ポリシーセット」タブをクリックします。
1. 「グローバルポリシーセット」を選択し、「表示されるユーザーとグループ」タブをクリックします。
1. 「ドメインを追加」をクリックし、必要に応じて既存のドメインを追加します。
1. サービス/Document Security/設定/マイポリシーに移動し、「表示されるユーザーとグループ」タブをクリックします。
1. 「ドメインを追加」をクリックし、必要に応じて既存のドメインを追加します。

## 管理者ユーザーの制限 {#administrator-user-restrictions}

特定の種類の管理者権限を持つユーザーは、セキュリティ上の理由から、Workspace のエンドユーザー Web ページにアクセスできません。 これらの Web ページはファイアウォールの外部に存在する可能性があるので、管理レベルのタスクを許可するとセキュリティ上のリスクが生じる可能性があります。 のエンドユーザー Web ページにアクセスできるのは、Workspace 管理者または Workspace ユーザーの権限を持つユーザーだけです。

>[!NOTE]
>
>AEM Forms のリリースでは Flex Workspace は廃止されています。
