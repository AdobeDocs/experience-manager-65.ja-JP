---
title: ユーザー管理
seo-title: ユーザー管理
description: User Management では、SAML を使用して、AEM Forms モジュールと Netegrity SiteMinder で保護されたアプリケーションとの間の SSO を有効化できます。このドキュメントでは、User Management の詳細について説明します。
seo-description: User Management では、SAML を使用して、AEM Forms モジュールと Netegrity SiteMinder で保護されたアプリケーションとの間の SSO を有効化できます。このドキュメントでは、User Management の詳細について説明します。
uuid: f0c8331a-d995-483d-97b7-259df53b1a1a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 10e6177a-8228-4515-aba9-bbe59bede449
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 100%

---


# ユーザー管理 {#user-management}

User Management では、Security Assertion Markup Language（SAML）を使用して、AEM Forms モジュールと Netegrity SiteMinder で保護されたアプリケーションとの間のシングルサインオン（SSO）を有効化できます。SSO を使用すると、ユーザーが会社のポータルで既に認証されている場合、AEM forms ユーザーのログインページは不要になり、ログインページは表示されません。

DB2 のデータベースおよびディレクトリの同期パフォーマンスを向上させる方法については、[IBM DB2 データベース：定期保守のコマンドの実行](/help/forms/using/admin-help/ibm-db2-database-running-commands.md#ibm-db2-database-running-commands-for-regular-maintenance)を参照してください。

## SSL 対応の LDAP サーバーを対象とした User Management の設定 {#configuring-user-management-for-an-ssl-enabled-ldap-server}

SSL 対応 LDAP サーバーがある場合、それと連携するように UserManagement を設定します（[SSL 対応の LDAP サーバーを対象とした User Management の設定](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server)を参照）。

## Document Security で使用するためのユーザー権限の設定 {#setting-user-privileges-for-use-with-document-security}

ユーザーおよびグループを作成するための適切な権限を持つ管理者ユーザーを作成します。AEM Forms 環境に Document Security が含まれている場合は、招待ユーザーおよびローカルユーザーを管理するための権限を、これらのユーザーの管理者となるユーザーに与えます。また、管理コンソールへのアクセスをユーザーに提供するために、管理者コンソールユーザーのロールも割り当てます。（[ロールの作成および設定](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles)を参照）。

選択したドメインのユーザーおよびグループをポリシーのユーザー検索で表示するには、スーパー管理者またはポリシーセット管理者が、作成した各ポリシーセットについて表示されるユーザーおよびグループのリストに対して、ドメイン（UserManagement で作成）を選択して追加する必要があります。

表示されるユーザーおよびグループのリストは、ポリシーセットコーディネーターに対して表示されるもので、ポリシーに追加するユーザーまたはグループを選択するときにエンドユーザーが参照できるドメインを制限するために使用します。このタスクを実行しない場合は、ポリシーセットコーディネーターに対して、ポリシーに追加するユーザーまたはグループが表示されません。ポリシーセットコーディネーターは、特定のポリシーセットに複数存在する可能性があります。

>[!NOTE]
>
>ポリシーを作成するには、ドメインの作成を済ませておく必要があります。

### 表示されるユーザーおよびグループの設定 {#set-visible-users-and-groups}

AEM Forms 環境と Document Security をインストールおよび設定した後、該当するすべてのドメインを User Management で設定します。

1. 管理コンソールで、サービス／Document Security／ポリシーをクリックし、「ポリシーセット」タブをクリックします。
1. 「グローバルポリシーセット」を選択し、「表示されるユーザーとグループ」タブをクリックします。
1. 「ドメインを追加」をクリックし、必要に応じて既存のドメインを追加します。
1. サービス／Document Security／設定／マイポリシーに移動し、「表示されるユーザーとグループ」タブをクリックします。
1. 「ドメインを追加」をクリックし、必要に応じて既存のドメインを追加します。

## 管理者ユーザーの制限 {#administrator-user-restrictions}

特定の種類の管理者権限を持つユーザーは、セキュリティ上の理由から Workspace のエンドユーザー Web ページにアクセスできません。これらの Web ページはファイアウォールの外部に存在することがあるため、管理者レベルのタスクを許可することによってセキュリティ上の問題を引き起こす可能性があります。 のエンドユーザー Web ページにアクセスできるのは、Workspace 管理者または Workspace ユーザーの権限を持つユーザーだけです。

>[!NOTE]
>
>AEM Forms のリリースでは Flex Workspace は廃止されています。

