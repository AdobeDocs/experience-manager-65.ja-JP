---
title: AdobeIMS認証および [!DNL Admin Console] AEMManaged Servicesのサポート
seo-title: AdobeIMS認証および [!DNL Admin Console] AEMManaged Servicesのサポート
description: AEMで [!DNL Admin Console] を使用する方法を学びます。
seo-description: AEMで [!DNL Admin Console] を使用する方法を学びます。
uuid: 3f5b32c7-cf62-41a4-be34-3f71bbf224eb
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: f6112dea-a1eb-4fd6-84fb-f098476deab7
translation-type: tm+mt
source-git-commit: a71c1e87dd5f01ba2584282e0960ca27d419adb0
workflow-type: tm+mt
source-wordcount: '1726'
ht-degree: 60%

---


# AdobeIMS認証と[!DNL Admin Console] AEMManaged Servicesのサポート{#adobe-ims-authentication-and-admin-console-support-for-aem-managed-services}

>[!NOTE]
>
>この機能は、Adobe Managed Services のお客様にのみご利用いただけます。

## 概要 {#introduction}

AEM 6.4.3.0では、AEMインスタンスとAdobeIMS(Identity Managementシステム)ベースの認証を&#x200B;**AEMManaged Services**&#x200B;のお客様に対して[!DNL Admin Console]サポートします。

AEM onboarding to [!DNL Admin Console]を使用すると、AEMManaged Servicesのお客様は1つのコンソールですべてのExperience Cloudユーザーを管理できます。 ユーザーとグループをAEMインスタンスに関連付けられた製品プロファイルに割り当て、特定のインスタンスにログインできます。

## 主なハイライト {#key-highlights}

* AEM の IMS 認証サポートは、AEM 作成者、管理者、または開発者のみを対象としており、サイト訪問者のような顧客サイトの外部エンドユーザーを対象としていません。
* [!DNL Admin Console]は、AEMManaged Servicesのお客様をIMS組織として、そのインスタンスを製品コンテキストとして表します。 顧客システムおよび製品管理者は、インスタンスへのアクセスを管理できるようになります。
* AEMManaged Servicesは顧客トポロジを[!DNL Admin Console]と同期します。 [!DNL Admin Console]には、インスタンスごとにAEMManaged Services製品コンテキストのインスタンスが1つあります。
* [!DNL Admin Console]内の製品プロファイルは、ユーザーがアクセスできるインスタンスを決定します
* お客様独自の SAML 2 準拠の ID プロバイダーを使用したフェデレーテッド認証がサポートされています。
* 個人用の Adobe ID ではなく、エンタープライズ ID またはフェデレーデッド ID（お客様のシングルサインオン用）のみがサポートされます。
* [!DNL User Management] (Adobe内 [!DNL Admin Console])は、引き続き顧客の管理者が所有します。

## アーキテクチャ {#architecture}

IMS 認証は、AEM と Adobe IMS エンドポイントの間で OAuth プロトコルを使用して機能します。ユーザーが IMS に追加され、Adobe Identity を持つようになると、IMS 資格情報を使用して AEM Managed Services インスタンスにログインできます。

ユーザーログインフローを以下に示します。ユーザーは IMS にリダイレクトされ、オプションで SSO 検証のためにカスタマー IDP にリダイレクトされてから、AEM にリダイレクトされます。

![image2018-9-23_23-55-8](assets/image2018-9-23_23-55-8.png)

## 設定方法 {#how-to-set-up}

### 組織を[!DNL Admin Console] {#onboarding-organizations-to-admin-console}にオンボーディング

お客様が[!DNL Admin Console]にオンボーディングするのは、AEM認証にAdobeIMSを使用する前提条件です。

最初のステップとして、Adobe IMS に組織をプロビジョニングする必要があります。[Adobe [!DNL Admin Console]](https://helpx.adobe.com/jp/enterprise/using/admin-console.html)では、Adobe企業のお客様はIMS組織として表されます。

AEMManaged Servicesのお客様は、既に組織をプロビジョニングしておく必要があります。また、IMSプロビジョニングの一環として、お客様のインスタンスを[!DNL Admin Console]で利用して、ユーザーの権利付与とアクセスを管理できます。

ユーザー認証のための IMS への移行は、AMS とお客様の共同作業となり、それぞれがワークフローを完了させます。

顧客が IMS 組織として存在し、AMS が顧客の IMS へのプロビジョニングを完了したら、次のような設定ワークフローを実行する必要があります。

![image2018-9-23_23-33-25](assets/image2018-9-23_23-33-25.png)

1. 指定されたシステム管理者が[!DNL Admin Console]にログインするための招待を受け取る
1. システム管理者は、ドメインの所有権を確認するためにドメインを要求する（この例では acme.com）
1. システム管理者はユーザーディレクトリを設定する
1. システム管理者は、SSO設定用に[!DNL Admin Console]にIDプロバイダー(IDP)を設定します。
1. AEM 管理者は、通常どおりローカルグループ、権限、および特権を管理する。「ユーザーとグループの同期」を参照してください。

>[!NOTE]
>
>IDP 設定を含む Adobe Identity Management Basics の詳細については、[このページ](https://helpx.adobe.com/jp/enterprise/using/set-up-identity.html)の記事を参照してください。
>
>エンタープライズ管理と[!DNL Admin Console]について詳しくは、[このページ](https://helpx.adobe.com/jp/enterprise/managing/user-guide.html)を参照してください。

### ユーザーを[!DNL Admin Console] {#onboarding-users-to-the-admin-console}にオンボーディング

お客様の規模と好みに応じて、ユーザーをオンボードする方法は 3 つあります。

1. [!DNL Admin Console]内にユーザーとグループを手動で作成
1. ユーザーと一緒に CSV ファイルをアップロードする
1. お客様のエンタープライズ Active Directory からユーザーとグループを同期する

#### [!DNL Admin Console] UI {#manual-addition-through-admin-console-ui}を介した手動の追加

ユーザーとグループは、[!DNL Admin Console] UIで手動で作成できます。 この方法は、管理するユーザー数が多くない場合に使用できます。（例：AEM ユーザーが 50 人未満の場合）

Analytics、Target、Creative Cloud などの他の Adobe 製品を管理するためにすでにこの方法を使用している場合は、ユーザーを手動で作成することもできます。

![image2018-9-23_20-39-9](assets/image2018-9-23_20-39-9.png)

#### [!DNL Admin Console] UI {#file-upload-in-the-admin-console-ui}でのファイルのアップロード

ユーザー作成を簡単に処理するには、CSV ファイルをアップロードしてまとめて追加します。

![image2018-9-23_18-59-57](assets/image2018-9-23_18-59-57.png)

#### ユーザー同期ツール {#user-sync-tool}

ユーザー同期ツール（UST）は、Active Directory または他のテスト済み OpenLDAP ディレクトリサービスを利用して、Adobe ユーザーを作成または管理することができます。対象ユーザーは、このツールをインストールおよび設定できる IT ID 管理者（エンタープライズディレクトリとシステムの管理者）です。オープンソースツールはカスタマイズ可能であるため、顧客は特定の要件に合うように開発者に修正させることができます。

ユーザー同期を実行すると、組織のActive Directory（または他の互換性のあるデータソース）からユーザーのリストが取得され、[!DNL Admin Console]内のユーザーのリストと比較されます。 次に、Adobe[!DNL User Management] APIを呼び出して、[!DNL Admin Console]が組織のディレクトリと同期されるようにします。 変化の流れは完全に一方向です。[!DNL Admin Console]で行った編集は、ディレクトリにプッシュされません。

このツールを使用すると、システム管理者は顧客のディレクトリ内のユーザーグループを製品構成と[!DNL Admin Console]内のユーザーグループにマッピングできます。新しいUSTバージョンでは、[!DNL Admin Console]内にユーザーグループを動的に作成することもできます。

ユーザー同期を設定するには、[[!DNL User Management]  API](https://www.adobe.io/apis/cloudplatform/usermanagement/docs/setup.html) を使用する場合と同様に、組織が一連の資格情報を作成する必要があります。

![image2018-9-23_13-36-56](assets/image2018-9-23_13-36-56.png)

ユーザー同期は、次の場所にある Adobe Github リポジトリを介して配布されます。

[https://github.com/adobe-apiplatform/user-sync.py/releases/latest](https://github.com/adobe-apiplatform/user-sync.py/releases/latest)

プレリリース版のバージョン2.4RC1は、動的グループ作成のサポートで利用でき、次の場所にあります。[https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1](https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1)

このリリースの主な機能は、[!DNL Admin Console]のユーザーメンバーシップに対して新しいLDAPグループを動的にマッピングする機能と、動的なユーザーグループの作成です。

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
>ユーザー同期ツールで使用される[!DNL User Management] APIは、この[場所](https://www.adobe.io/apis/cloudplatform/umapi-new.html)で扱います。

>[!NOTE]
>
>AEM IMS の設定は、Adobe Managed Services チームによって処理されます。ただし、お客様の管理者は必要に応じて変更することができます（例えば、自動グループメンバーシップやグループマッピングなど）。IMS クライアントは、ご自身の Managed Services チームによっても登録されます。

## 使用方法 {#how-to-use}

### [!DNL Admin Console] {#managing-products-and-user-access-in-admin-console}での製品とユーザーアクセスの管理

お客様の製品管理者が[!DNL Admin Console]にログインすると、AEMManaged Services製品コンテキストの複数のインスタンスが次のように表示されます。

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

[!DNL Admin Console]の初回セットアップ中にFederated IDPが設定された場合、ユーザーはSSO用のお客様のIDPにリダイレクトされます。

以下の例では、IDP は Okta です。

![screen_shot_2018-09-17at115734pm](assets/screen_shot_2018-09-17at115734pm.png)

認証が完了すると、ユーザーは AEM にリダイレクトされてログインします。

![screen_shot_2018-09-18at120124am](assets/screen_shot_2018-09-18at120124am.png)

### 既存ユーザーの移行 {#migrating-existing-users}

別の認証方式を使用していて、現在 IMS に移行されている既存の AEM インスタンスの場合、移行手順が必要です。

AEMリポジトリ内の既存のユーザー（ローカルソース、LDAPまたはSAML）は、User Migration Utilityを使用して、IDPとしてIMSに移行できます。

このユーティリティは、IMS プロビジョニングの一部として AMS チームによって実行されます。

### AEM での権限と ACL の管理  {#managing-permissions-and-acls-in-aem}

アクセス制御と権限は、AEMで引き続き管理されます。これは、IMSからのユーザーグループ(下の例ではAEM-GRP-008)と、権限とアクセス制御が定義されたローカルグループを分離することで実現できます。 IMS から同期されたユーザーグループは、ローカルグループに割り当てられ、権限を継承することができます。

以下の例では、同期グループをローカル *Dam_Users* グループに追加しています。

ここでは、[!DNL Admin Console]内のいくつかのグループにも1人のユーザーが割り当てられています。 （ユーザーとグループは、ユーザー同期ツールを使用してLDAPから同期できるか、ローカルに作成できます。上記の&#x200B;**Onboarding Users to the[!DNL Admin Console]**&#x200B;を参照してください）。

&amp;ast；ユーザーグループは、ユーザーがインスタンスにログインした場合にのみ同期されます。大量のユーザーとグループを持つお客様の場合は、グループ同期ユーティリティをAMSで実行して、上述のアクセス制御および権限管理用のグループを事前取得できます。

![screen_shot_2018-09-17at94207pm](assets/screen_shot_2018-09-17at94207pm.png)

ユーザーは、IMS の以下のグループの一部です。

![screen_shot_2018-09-17at94237pm](assets/screen_shot_2018-09-17at94237pm.png)

ユーザーがログインすると、以下に示すように、グループメンバーシップが同期されます。

![screen_shot_2018-09-17at94033pm](assets/screen_shot_2018-09-17at94033pm.png)

AEM では、IMS から同期されたユーザーグループを既存のローカルグループ（DAM ユーザーなど）にメンバーとして追加できます。

![screen_shot_2018-09-17at95804pm](assets/screen_shot_2018-09-17at95804pm.png)

以下に示すように、グループ *AEM-GRP_008* は DAM ユーザーの権限と特権を継承します。これは同期されたグループに対する権限を管理する効果的な方法であり、LDAP ベースの認証方法でも一般的に使用されています。

![screen_shot_2018-09-17at110505pm](assets/screen_shot_2018-09-17at110505pm.png)
