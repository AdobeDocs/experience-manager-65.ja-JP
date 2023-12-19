---
title: User Management
description: User Management では、SAML を使用して、AEM Forms モジュールと Netegrity SiteMinder で保護されたアプリケーションとの間で SSO を有効にできます。このドキュメントでは、User Management について詳しく説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 1da1f6de-ac0d-4e0d-b8bb-956420e42699
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 100%

---

# User Management {#user-management}

User Management では、Security Assertion Markup Language（SAML）を使用して、AEM Forms モジュールと Netegrity SiteMinder で保護されたアプリケーションとの間でシングルサインオン（SSO）を有効にできます。SSO を実装すると、AEM Forms のユーザーログインページは不要になり、ユーザーが会社のポータルで既に認証されている場合は表示されません。

DB2 のデータベースおよびディレクトリ同期のパフォーマンスを向上させる方法については、[IBM DB2 データベース：定期保守のコマンドの実行](/help/forms/using/admin-help/ibm-db2-database-running-commands.md#ibm-db2-database-running-commands-for-regular-maintenance)を参照してください。

## SSL 対応の LDAP サーバーを対象とした User Management の設定 {#configuring-user-management-for-an-ssl-enabled-ldap-server}

SSL 対応の LDAP サーバーがある場合は、それと連携するように User Management を設定します（[SSL 対応の LDAP サーバーを対象とした User Management の設定](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server)を参照）。

## Document Security で使用するユーザー権限の設定 {#setting-user-privileges-for-use-with-document-security}

ユーザーおよびグループを作成するための適切な権限を持つ管理者ユーザーを作成します。AEM Forms 環境に Document Security が含まれている場合は、招待ユーザーおよびローカルユーザーを管理する権限を、これらのユーザーの管理者となるユーザーに付与します。また、管理コンソールのユーザーの役割を割り当てて、ユーザーに管理コンソールへのアクセス権を付与します（[役割の作成および設定](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles)を参照）。

選択したドメインのユーザーおよびグループを、ポリシーユーザーの検索中に表示するには、上級管理者またはポリシーセット管理者が、作成したポリシーセットごとに表示されるユーザーとグループのリストに対して、ドメイン（User Management で作成）を選択して追加する必要があります。

表示されるユーザーとグループのリストは、ポリシーセットコーディネーターに対して表示され、ポリシーに追加するユーザーまたはグループを選択する際にエンドユーザーが参照できるドメインを制限するために使用されます。このタスクを実行しない場合、ポリシーセットコーディネーターに対して、ポリシーに追加するユーザーまたはグループが表示されません。ポリシーセットコーディネーターは、特定のポリシーセットに複数存在する可能性があります。

>[!NOTE]
>
>ポリシーを作成するには、ドメインの作成を済ませておく必要があります。

### 表示されるユーザーおよびグループを設定 {#set-visible-users-and-groups}

AEM Forms 環境と Document Security をインストールして設定した後に、User Management で適切なドメインをすべて設定します。

1. 管理コンソールで、サービス／Document Security／ポリシーをクリックし、「ポリシーセット」タブをクリックします。
1. 「グローバルポリシーセット」を選択し、「表示されるユーザーとグループ」タブをクリックします。
1. 「ドメインを追加」をクリックし、必要に応じて既存のドメインを追加します。
1. サービス／Document Security／設定／マイポリシーに移動し、「表示されるユーザーとグループ」タブをクリックします。
1. 「ドメインを追加」をクリックし、必要に応じて既存のドメインを追加します。

## 管理者ユーザーの制限 {#administrator-user-restrictions}

特定の種類の管理者権限を持つユーザーは、セキュリティ上の理由から、Workspace のエンドユーザー web ページにアクセスできません。これらの web ページはファイアウォールの外部に存在することがあるので、管理レベルのタスクを許可するとセキュリティ上のリスクが生じる可能性があります。のエンドユーザー Web ページにアクセスできるのは、Workspace 管理者または Workspace ユーザーの権限を持つユーザーだけです。

>[!NOTE]
>
>AEM Forms のリリースでは Flex Workspace は廃止されています。
