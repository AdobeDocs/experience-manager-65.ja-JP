---
title: AEM Managed Services に対する Adobe IMS 認証およびアドミンコンソールのサポート
seo-title: AEM Managed Services に対する Adobe IMS 認証およびアドミンコンソールのサポート
description: AEMで管理コンソールを使用する方法を説明します。
seo-description: AEMで管理コンソールを使用する方法を説明します。
uuid: 3f5b32c7-cf62-41a4-be34-3f71bbf224eb
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: f6112dea-a1eb-4fd6-84fb-f098476deab7
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d

---


# AEM Managed Services に対する Adobe IMS 認証およびアドミンコンソールのサポート {#adobe-ims-authentication-and-admin-console-support-for-aem-managed-services}

>[!NOTE]
>
>この機能は、Adobe Managed Services のお客様にのみご利用いただけます。

## 概要 {#introduction}

AEM 6.4.3.0 introduces Admin Console support for AEM instances and Adobe IMS(Identity Management System) based authentication for **AEM Managed Services** customers.

AEM がアドミンコンソールをオンボーディングしたことにより、AEM Managed Servicesのお客様は 1 つのコンソールですべての Experience Cloud ユーザーを管理できます。ユーザーとグループをAEMインスタンスに関連付けられた製品プロファイルに割り当てて、特定のインスタンスにログインできます。

## 主なハイライト {#key-highlights}

* AEM の IMS 認証サポートは、AEM 作成者、管理者、または開発者のみを対象としており、サイト訪問者のような顧客サイトの外部エンドユーザーを対象としていません。
* アドミンコンソールは、AEM Managed Services の顧客を IMS 組織として、それらのインスタンスを製品コンテキストとして表します。顧客システムおよび製品管理者は、インスタンスへのアクセスを管理できるようになります。
* AEM Managed Services は、顧客のトポロジとアドミンコンソールを同期させます。アドミンコンソールでは、インスタンスごとに AEM Managed Services 製品コンテキストのインスタンスが 1 つあります。
* アドミンコンソールの製品プロファイルによって、ユーザーがアクセスできるインスタンスが決まります。
* お客様独自の SAML 2 準拠の ID プロバイダーを使用したフェデレーテッド認証がサポートされています。
* 個人用の Adobe ID ではなく、エンタープライズ ID またはフェデレーデッド ID（お客様のシングルサインオン用）のみがサポートされます。
* ユーザー管理（Adobe Admin Console内）は、引き続き顧客管理者が所有します。

## アーキテクチャ {#architecture}

IMS 認証は、AEM と Adobe IMS エンドポイントの間で OAuth プロトコルを使用して機能します。ユーザーが IMS に追加され、Adobe Identity を持つようになると、IMS 資格情報を使用して AEM Managed Services インスタンスにログインできます。

ユーザーログインフローを以下に示します。ユーザーは IMS にリダイレクトされ、オプションで SSO 検証のためにカスタマー IDP にリダイレクトされてから、AEM にリダイレクトされます。

![image2018-9-23_23-55-8](assets/image2018-9-23_23-55-8.png)

## 設定方法 {#how-to-set-up}

### アドミンコンソールへの組織のオンボーディング {#onboarding-organizations-to-admin-console}

アドミンコンソールへお客様をオンボーディングすることは、AEM 認証に Adobe IMS を使用するための前提条件です。

最初のステップとして、Adobe IMS に組織をプロビジョニングする必要があります。Adobe Enterprise のお客様は、[Adobe Admin Console](https://helpx.adobe.com/enterprise/using/admin-console.html) に IMS 組織として表されています。

AEM Managed Servicesのお客様は、既に組織をプロビジョニングしておく必要があります。また、IMSプロビジョニングの一環として、顧客インスタンスを管理コンソールで使用して、ユーザーの権利付与とアクセスを管理できます。

ユーザー認証のための IMS への移行は、AMS とお客様の共同作業となり、それぞれがワークフローを完了させます。

顧客が IMS 組織として存在し、AMS が顧客の IMS へのプロビジョニングを完了したら、次のような設定ワークフローを実行する必要があります。

![image2018-9-23_23-33-25](assets/image2018-9-23_23-33-25.png)

1. 指定されたシステム管理者が管理コンソールへのログインの招待を受け取ります
1. システム管理者は、ドメインの所有権を確認するためにドメインを要求する（この例では acme.com）
1. システム管理者はユーザーディレクトリを設定する
1. システム管理者は、SSO 設定用に管理コンソールの ID プロバイダ（IDP）を設定する
1. AEM 管理者は、通常どおりローカルグループ、権限、および特権を管理する。「ユーザーとグループの同期」を参照

>[!NOTE]
>
>IDP 設定を含む Adobe Identity Management Basics の詳細については、[このページ](https://helpx.adobe.com/enterprise/using/set-up-identity.html)の記事を参照してください。
>
>Enterprise Administration と Admin Console の詳細については、[このページ](https://helpx.adobe.com/enterprise/managing/user-guide.html)の記事を参照してください。

### アドミンコンソールへのユーザーのオンボード {#onboarding-users-to-the-admin-console}

お客様の規模と好みに応じて、ユーザーをオンボードする方法は 3 つあります。

1. アドミンコンソールでユーザーとグループを手動作成する
1. ユーザーと一緒に CSV ファイルをアップロードする
1. お客様のエンタープライズ Active Directory からユーザーとグループを同期する

#### アドミンコンソール UI による手動追加 {#manual-addition-through-admin-console-ui}

ユーザーとグループは、アドミンコンソールの UI で手動で作成できます。この方法は、管理するユーザー数が多くない場合に使用できます。（例：AEM ユーザーが 50 人未満の場合）

Analytics、Target、Creative Cloud などの他の Adobe 製品を管理するためにすでにこの方法を使用している場合は、ユーザーを手動で作成することもできます。

![image2018-9-23_20-39-9](assets/image2018-9-23_20-39-9.png)

#### アドミンコンソール UI でのファイルアップロード {#file-upload-in-the-admin-console-ui}

ユーザー作成を簡単に処理するには、CSV ファイルをアップロードしてまとめて追加します。

![image2018-9-23_18-59-57](assets/image2018-9-23_18-59-57.png)

#### ユーザー同期ツール {#user-sync-tool}

ユーザー同期ツール（UST）は、Active Directory または他のテスト済み OpenLDAP ディレクトリサービスを利用して、Adobe ユーザーを作成または管理することができます。対象ユーザーは、このツールをインストールおよび設定できる IT ID 管理者（エンタープライズディレクトリとシステムの管理者）です。オープンソースツールはカスタマイズ可能であるため、顧客は特定の要件に合うように開発者に修正させることができます。

ユーザー同期が実行されると、組織の Active Directory（または他の互換性のあるデータソース）からユーザー一覧を取得し、それをアドミンコンソール内のユーザー一覧と比較します。その後、アドミンコンソールを組織のディレクトリと同期するために、Adobe User Management API を呼び出します。変更の流れは完全に一方向です。アドミンコンソールで行った編集はディレクトリにプッシュされません。

このツールを使用すると、システム管理者はお客様のディレクトリにあるユーザーグループをアドミンコンソールの製品設定とユーザーグループにマッピングできます。また、新しい UST バージョンでは、アドミンコンソールで動的にユーザーグループを作成することもできます。

To set up User Sync, the organization needs to create a set of credentials in the same way they would use the [User Management API](https://www.adobe.io/apis/cloudplatform/usermanagement/docs/setup.html).

![image2018-9-23_13-36-56](assets/image2018-9-23_13-36-56.png)

ユーザー同期は、次の場所にある Adobe Github リポジトリを介して配布されます。

[https://github.com/adobe-apiplatform/user-sync.py/releases/latest](https://github.com/adobe-apiplatform/user-sync.py/releases/latest)

Note that a pre-release version 2.4RC1 is available with dynamic group creation support and can be found here: [https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1](https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1)

このリリースの主な機能は、アドミンコンソールでユーザーのメンバーシップに合わせて新しい LDAP グループを動的にマッピングする機能と、動的なユーザーグループ作成です。

新しいグループ機能の詳細については、次を参照してください。

[https://github.com/adobe-apiplatform/user-sync.py/blob/v2/docs/en/user-manual/advanced_configuration](https://github.com/adobe-apiplatform/user-sync.py/blob/v2/docs/en/user-manual/advanced_configuration.md#additional-group-options)

>[!NOTE]
>
>ユーザー同期ツールの詳細については、[ドキュメントページ](https://adobe-apiplatform.github.io/user-sync.py/en/)を参照してください。
>
>
>ユーザー同期ツールは、[ここ](https://adobe-apiplatform.github.io/umapi-documentation/en/UM_Authentication.html)に説明されている手順を使用して、Adobe I/O クライアント UMAPI として登録する必要があります。
>
>Adobe I/O コンソールのドキュメントは[ここ](https://www.adobe.io/apis/cloudplatform/console.html)を参照してください。
>
>
>The User Management API that is used by the User Sync Tool is covered at this [location](https://www.adobe.io/apis/cloudplatform/umapi-new.html).

>[!NOTE]
>
>AEM IMS の設定は、Adobe Managed Services チームによって処理されます。ただし、お客様の管理者は必要に応じて変更することができます（例えば、自動グループメンバーシップやグループマッピングなど）。IMS クライアントは、ご自身の Managed Services チームによっても登録されます。

## 使用方法 {#how-to-use}

### アドミンコンソールでの製品とユーザーアクセスの管理 {#managing-products-and-user-access-in-admin-console}

顧客の製品管理者がアドミンコンソールにログインすると、以下に示すように、AEM Managed Services 製品コンテキストの複数のインスタンスが表示されます。

![screen_shot_2018-09-17at105804pm](assets/screen_shot_2018-09-17at105804pm.png)

この例では、*AEM-MS-Onboard* 組織は、Stage、Prod など、さまざまなトポロジと環境にまたがる 32 のインスタンスがあります。

![screen_shot_2018-09-17at105517pm](assets/screen_shot_2018-09-17at105517pm.png)

詳細を確認してインスタンスを識別できます。

![screen_shot_2018-09-17at105601pm](assets/screen_shot_2018-09-17at105601pm.png)

各製品コンテキストインスタンスの下に、関連付けられた製品プロファイルがあります。この製品プロファイルは、ユーザーおよびグループにアクセス権を割り当てるために使用されます。

![image2018-9-18_7-48-50](assets/image2018-9-18_7-48-50.png)

この製品プロファイルの下に追加されたすべてのユーザーおよびグループは、以下の例に示すように、そのインスタンスにログインできます。

![screen_shot_2018-09-17at105623pm](assets/screen_shot_2018-09-17at105623pm.png)

### AEM へのログイン {#logging-into-aem}

#### ローカル管理者ログイン {#local-admin-login}

AEM では引き続き、管理ユーザーのローカルログインをサポートし、ログイン画面にはローカルでログインするオプションがあります。

![screen_shot_2018-09-18at121056am](assets/screen_shot_2018-09-18at121056am.png)

#### IMS ベースのログイン {#ims-based-login}

他のユーザーの場合は、IMS がインスタンスに設定された後に、IMS ベースのログインを使用できます。ユーザーはまず、下に示すように、「**Sign in with Adobe**」ボタンをクリックします。

![image2018-9-18_0-10-32](assets/image2018-9-18_0-10-32.png)

その後、ユーザーは IMS ログイン画面にリダイレクトされ、資格情報を入力します。

![screen_shot_2018-09-17at115629pm](assets/screen_shot_2018-09-17at115629pm.png)

アドミンコンソールの初期設定中にフェデレーテッド IDP が設定される場合、ユーザーは SSO 用のカスタマー IDP にリダイレクトされます。

以下の例では、IDP は Okta です。

![screen_shot_2018-09-17at115734pm](assets/screen_shot_2018-09-17at115734pm.png)

認証が完了すると、ユーザーは AEM にリダイレクトされてログインします。

![screen_shot_2018-09-18at120124am](assets/screen_shot_2018-09-18at120124am.png)

### 既存ユーザーの移行 {#migrating-existing-users}

別の認証方式を使用していて、現在 IMS に移行されている既存の AEM インスタンスの場合、移行手順が必要です。

AEMリポジトリ内の既存のユーザー（ローカルで、LDAPまたはSAML経由）は、User Migration Utilityを使用して、IMSをIDPとして指すように移行できます。

このユーティリティは、IMS プロビジョニングの一部として AMS チームによって実行されます。

### AEM での権限と ACL の管理 {#managing-permissions-and-acls-in-aem}

アクセス制御と権限はAEMで引き続き管理され、IMSから来るユーザーグループ（下の例ではAEM-GRP-008）と、権限とアクセス制御が定義されているローカルグループを分離することで、これを実現できます。 IMS から同期されたユーザーグループは、ローカルグループに割り当てられ、権限を継承することができます。

In the example below, we are adding synced groups to the local *Dam_Users* group as an example.

ここでは、ユーザーはアドミンコンソールのいくつかのグループにも割り当てられています。( Please note that the users and groups can be synced from LDAP using the user sync tool or created locally, please see the section **Onboarding Users to the Admin Console** above).

&amp;ast；ユーザーグループは、ユーザーがインスタンスにログインした場合にのみ同期されます。大量のユーザーとグループを持つお客様の場合は、AMSでグループ同期ユーティリティを実行して、上記のアクセス制御と権限管理のためのグループを事前取得できます。

![screen_shot_2018-09-17at94207pm](assets/screen_shot_2018-09-17at94207pm.png)

ユーザーは、IMS の以下のグループの一部です。

![screen_shot_2018-09-17at94237pm](assets/screen_shot_2018-09-17at94237pm.png)

ユーザーがログインすると、以下に示すように、グループメンバーシップが同期されます。

![screen_shot_2018-09-17at94033pm](assets/screen_shot_2018-09-17at94033pm.png)

AEM では、IMS から同期されたユーザーグループを既存のローカルグループ（DAM ユーザーなど）にメンバーとして追加できます。

![screen_shot_2018-09-17at95804pm](assets/screen_shot_2018-09-17at95804pm.png)

以下に示すように、グループ *AEM-GRP_008* は DAM ユーザーの権限と特権を継承します。これは同期されたグループに対する権限を管理する効果的な方法であり、LDAP ベースの認証方法でも一般的に使用されています。

![screen_shot_2018-09-17at110505pm](assets/screen_shot_2018-09-17at110505pm.png)

