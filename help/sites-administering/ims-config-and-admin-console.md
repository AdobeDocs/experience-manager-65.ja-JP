---
title: Adobe IMS認証および [!DNL Admin Console] Adobe Experience Manager Managed Servicesのサポート
description: 使用方法 [!DNL Admin Console] Adobe Experience Manager
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: 95eae97c-01c2-4f5c-8068-f504eab7c49e
feature: Security
source-git-commit: 260f71acd330167572d817fdf145a018b09cbc65
workflow-type: tm+mt
source-wordcount: '1669'
ht-degree: 57%

---

# AEM Managed Services に対する Adobe IMS 認証および [!DNL Admin Console] のサポート {#adobe-ims-authentication-and-admin-console-support-for-aem-managed-services}

>[!NOTE]
>
>この機能は、Adobe Managed Services のお客様のみが利用できます。

>[!NOTE]
>
>Adobe Experience Manager(AEM) は、現在、プロファイルへのグループの割り当てをサポートしていません。 代わりに、ユーザーを個別に追加する必要があります。

## はじめに {#introduction}

AEM 6.4.3.0 では、AEM インスタンスに対する [!DNL Admin Console] のサポートおよび **AEM Managed Services** のお客様のための Adobe IMS（Identity Management System）ベースの認証が導入されました。

AEM が [!DNL Admin Console] をオンボーディングしたことにより、AEM Managed Services のお客様は 1 つのコンソールですべての Experience Cloud ユーザーを管理できます。AEMインスタンスに関連付けられた製品プロファイルにユーザーを割り当てて、特定のインスタンスにログインできます。

## 主なハイライト {#key-highlights}

* AEM IMS 認証のサポートは、AEM オーサー、管理者またはデベロッパーに対してのみ有効で、サイト訪問者などの顧客サイトの外部エンドユーザーには適用されません
* [!DNL Admin Console] は、AEM Managed Services の顧客を IMS 組織として、それらのインスタンスを製品コンテキストとして表します。顧客システムおよび製品管理者は、インスタンスへのアクセスを管理できるようになります。
* AEM Managed Services は、顧客のトポロジと [!DNL Admin Console] を同期させます。[!DNL Admin Console] では、インスタンスごとに AEM Managed Services 製品コンテキストのインスタンスが 1 つあります。
* [!DNL Admin Console] の製品プロファイルによって、ユーザーがアクセスできるインスタンスが決まります。
* お客様独自の SAML 2 準拠 ID プロバイダーを使用したフェデレーテッド認証がサポートされます
* 個人のAdobeID ではなく、Enterprise ID または Federated ID のみ（お客様のシングルサインオン用）がサポートされます。
* [!DNL User Management]（Adobe [!DNL Admin Console] での）は、引き続きカスタマー管理者によって所有されます。

## アーキテクチャ {#architecture}

IMS 認証は、AEMとAdobe IMSエンドポイントの間で OAuth プロトコルを使用して機能します。 ユーザーが IMS に追加され、Adobe ID を持つようになると、IMS 資格情報を使用して AEM Managed Services インスタンスにログインできます。

ユーザーログインフローを以下に示します。ユーザーは IMS にリダイレクトされ、必要に応じて SSO 検証のために顧客 IDP にリダイレクトされてから、AEMにリダイレクトされます。

![image2018-9-23_23-55-8](assets/image2018-9-23_23-55-8.png)

## 設定方法 {#how-to-set-up}

### [!DNL Admin Console] への組織のオンボーディング {#onboarding-organizations-to-admin-console}

[!DNL Admin Console] へお客様をオンボーディングすることは、AEM 認証に Adobe IMS を使用するための前提条件です。

最初のステップとして、Adobe IMS に組織をプロビジョニングする必要があります。Adobe Enterprise のお客様は、[Adobe  [!DNL Admin Console]](https://helpx.adobe.com/jp/enterprise/using/admin-console.html) に IMS 組織として表されています。

AEM Managed Services のお客様は、すでに組織がプロビジョニングされています。また、IMS プロビジョニングの一環として、ユーザーの使用権限とアクセスを管理するために、[!DNL Admin Console] でカスタマーインスタンスを利用できるようになります。

ユーザー認証のための IMS への移行は、AMS とお客様の共同作業となり、それぞれがワークフローを完了させます。

顧客が IMS 組織として存在し、AMS が顧客の IMS へのプロビジョニングを完了したら、次のような設定ワークフローを実行する必要があります。

![image2018-9-23_23-33-25](assets/image2018-9-23_23-33-25.png)

1. 指定されたシステム管理者が [!DNL Admin Console] にログインするための招待を受け取る
1. システム管理者がドメインを要求して、ドメイン（この例では acme.com）の所有権を確認します。
1. システム管理者はユーザーディレクトリを設定します
1. システム管理者は、SSO 設定用に [!DNL Admin Console] の ID プロバイダ（IDP）を設定します。
1. AEM管理者は、通常どおりローカルグループ、権限および権限を管理します。 ユーザーとグループの同期を参照してください。

>[!NOTE]
>
>IDP 設定を含む、Adobe Identity Management Basics の詳細については、[このページ](https://helpx.adobe.com/jp/enterprise/using/set-up-identity.html)の記事を参照してください。
>
>Enterprise Administration と [!DNL Admin Console] の詳細については、[このページ](https://helpx.adobe.com/jp/enterprise/managing/user-guide.html)の記事を参照してください。

### [!DNL Admin Console] へのユーザーのオンボーディング {#onboarding-users-to-the-admin-console}

ユーザーをオンボードする方法は、お客様の規模と好みに応じて 3 つあります。

1. ユーザーとグループを手動で [!DNL Admin Console] に作成する
1. ユーザーを含む CSV ファイルのアップロード
1. お客様のエンタープライズ Active Directory からユーザーとグループを同期します。

#### [!DNL Admin Console] UI を利用した手動での追加 {#manual-addition-through-admin-console-ui}

ユーザーとグループは、[!DNL Admin Console] の UI で手動で作成できます。管理するユーザーが多くない場合は、この方法を使用できます。 例えば、AEMユーザーが 50 人未満の場合、

また、Adobe Analytics、Adobe Target、Adobe Creative Cloudなどの他のAdobe製品の管理に既にこの方法を使用している場合は、手動でユーザーを作成することもできます。

![image2018-9-23_20-39-9](assets/image2018-9-23_20-39-9.png)

#### [!DNL Admin Console] UI でのファイルのアップロード {#file-upload-in-the-admin-console-ui}

CSV ファイルをアップロードしてユーザーをまとめて登録すると、ユーザーの作成を簡単に処理できます。

![image2018-9-23_18-59-57](assets/image2018-9-23_18-59-57.png)

#### ユーザー同期ツール {#user-sync-tool}

Adobe同期ツール (UST) を使用すると、企業のお客様は、Active Directory またはテスト済みの他の OpenLDAP ディレクトリサービスを使用するユーザーを作成または管理できます。 対象ユーザーは、ツールをインストールおよび設定できる IT ID 管理者（Enterprise Directory および System Admin）です。 オープンソースツールはカスタマイズ可能なので、顧客は独自の要件に合わせて開発者が変更できます。

ユーザー同期が実行されると、組織の Active Directory（または他の互換性のあるデータソース）からユーザーのリストを取得し、それを [!DNL Admin Console]. その後、Adobeを呼び出します [!DNL User Management] API で [!DNL Admin Console] は組織のディレクトリと同期されます。 変化の流れは完全に一つの方法です。編集内容 [!DNL Admin Console] ディレクトリにプッシュアウトされないでください。

このツールを使用すると、システム管理者は、お客様のディレクトリ内のユーザーグループを、 [!DNL Admin Console]また、新しい UST バージョンでは、 [!DNL Admin Console].

ユーザー同期を設定するには、[[!DNL User Management] API](https://www.adobe.io/apis/cloudplatform/usermanagement/docs/setup.html) を使用する場合と同様に、お客様の組織で一連の資格情報を作成する必要があります。

![image2018-9-23_13-36-56](assets/image2018-9-23_13-36-56.png)

ユーザー同期は、次の場所にある Adobe Github リポジトリを介して配布されます。

[https://github.com/adobe-apiplatform/user-sync.py/releases/latest](https://github.com/adobe-apiplatform/user-sync.py/releases/latest)

次の場所にあるプレリリースバージョンの 2.4RC1 は、動的グループの作成をサポートしています。[https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1](https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1)

このリリースの主な機能は、[!DNL Admin Console] でユーザーのメンバーシップに合わせて新しい LDAP グループを動的にマッピングする機能と、動的にユーザーグループを作成する機能です。

新しいグループ機能の詳細については、こちらを参照してください。

[https://adobe-apiplatform.github.io/user-sync.py/en/user-manual/advanced_configuration.html#additional-group-options](https://adobe-apiplatform.github.io/user-sync.py/en/user-manual/advanced_configuration.html#additional-group-options)

>[!NOTE]
>
>ユーザー同期ツールについて詳しくは、[ドキュメントページ](https://adobe-apiplatform.github.io/user-sync.py/en/)を参照してください。
>
>
>ユーザー同期ツールでは、[ここ](https://adobe-apiplatform.github.io/umapi-documentation/en/UM_Authentication.html)に説明されている手順を使用して、Adobe I/O クライアント UMAPI として登録する必要があります。
>
>Adobe I/O コンソールのドキュメントは[ここ](https://developer.adobe.com/developer-console/docs/guides/)を参照してください。
>
>
>ユーザー同期ツールで使用する [!DNL User Management] API については、[この場所](https://adobe-apiplatform.github.io/umapi-documentation/en/)を参照してください。

>[!NOTE]
>
>AEM IMS の設定は、Adobe Managed Services チームによって処理されます。 ただし、顧客管理者は要件（自動グループメンバーシップやグループマッピングなど）に従って変更できます。 IMS クライアントもManaged Servicesチームによって登録されます。

## 使用方法 {#how-to-use}

### [!DNL Admin Console] での製品とユーザーアクセスの管理 {#managing-products-and-user-access-in-admin-console}

お客様の製品管理者が [!DNL Admin Console] にログインすると、次に示すように、AEM Managed Services 製品コンテキストの複数のインスタンスが表示されます。

![screen_shot_2018-09-17at105804pm](assets/screen_shot_2018-09-17at105804pm.png)

この例では、*AEM-MS-Onboard* 組織には、ステージング、実稼働など、さまざまなトポロジと環境にまたがる 32 のインスタンスがあります。

![screen_shot_2018-09-17at105517pm](assets/screen_shot_2018-09-17at105517pm.png)

詳細を確認するとインスタンスを識別できます。

![screen_shot_2018-09-17at105601pm](assets/screen_shot_2018-09-17at105601pm.png)

各製品コンテキストのインスタンスの下に、関連する製品プロファイルがあります。この製品プロファイルは、ユーザーにアクセス権を割り当てる際に使用します。

![image2018-9-18_7-48-50](assets/image2018-9-18_7-48-50.png)

この製品プロファイルの下に追加されたユーザーは、次の例に示すように、そのインスタンスにログインできます。

![screen_shot_2018-09-17at105623pm](assets/screen_shot_2018-09-17at105623pm.png)

### AEMへのログイン {#logging-into-aem}

#### ローカル管理者ログイン {#local-admin-login}

ログイン画面にはローカルでログインするオプションがあるので、AEMは引き続き管理者ユーザーのローカルログインをサポートできます。

![screen_shot_2018-09-18at121056am](assets/screen_shot_2018-09-18at121056am.png)

#### IMS ベースのログイン {#ims-based-login}

他のユーザーの場合は、IMS がインスタンスに設定された後に、IMS ベースのログインを使用できます。ユーザーが最初にクリックした **Adobe** を次に示します。

![image2018-9-18_0-10-32](assets/image2018-9-18_0-10-32.png)

その後、ユーザーは IMS ログイン画面にリダイレクトされ、資格情報を入力します。

![screen_shot_2018-09-17at115629pm](assets/screen_shot_2018-09-17at115629pm.png)

[!DNL Admin Console] の初期設定中にフェデレーテッド IDP が設定される場合、ユーザーは SSO 用のカスタマー IDP にリダイレクトされます。

次の例では、IDP は Okta です。

![screen_shot_2018-09-17at115734pm](assets/screen_shot_2018-09-17at115734pm.png)

認証が完了すると、ユーザーは AEM にリダイレクトされてログインします。

![screen_shot_2018-09-18at120124am](assets/screen_shot_2018-09-18at120124am.png)

### 既存のユーザーの移行 {#migrating-existing-users}

別の認証方法を使用しており、現在 IMS に移行中の既存のAEMインスタンスの場合は、移行手順が必要です。

AEM リポジトリ内の既存ユーザー（LDAP または SAML を介してローカルに提供される）は、IDP がユーザー移行ユーティリティを使用しているため、IMS を指すように移行できます。

このユーティリティは、IMS プロビジョニングの一環として AMS チームによって実行されます。

### AEMでの権限と ACL の管理 {#managing-permissions-and-acls-in-aem}

アクセス制御と権限は、引き続きAEMで管理されます。これをおこなうには、IMS からのユーザーグループ ( 以下の例ではAEM-GRP-008) と、権限とアクセス制御が定義されているローカルグループを分離します。 IMS から同期されたユーザーグループは、ローカルグループに割り当てられ、権限を継承することができます。

以下の例では、同期グループをローカル *Dam_Users* グループに追加しています。

ここでは、ユーザーは [!DNL Admin Console] のいくつかのグループにも割り当てられています。（ユーザーとグループは、ユーザー同期ツールを使用して LDAP から同期することも、ローカルに作成することもできます）。 詳しくは、 **ユーザーの[!DNL Admin Console]** 以前の )。

>[!NOTE]
>
>ユーザーグループは、ユーザーがインスタンスにログインした場合にのみ同期されます。

![screen_shot_2018-09-17at94207pm](assets/screen_shot_2018-09-17at94207pm.png)

ユーザーは、IMS の以下のグループの一部です。

![screen_shot_2018-09-17at94237pm](assets/screen_shot_2018-09-17at94237pm.png)

ユーザーがログインすると、以下に示すように、グループメンバーシップが同期されます。

![screen_shot_2018-09-17at94033pm](assets/screen_shot_2018-09-17at94033pm.png)

AEMでは、IMS から同期されたユーザーグループを既存のローカルグループ（DAM ユーザーなど）にメンバーとして追加できます。

![screen_shot_2018-09-17at95804pm](assets/screen_shot_2018-09-17at95804pm.png)

以下に示すように、グループは *AEM-GRP_008* は、DAM ユーザーの権限と権限を継承します。 これは、同期されたグループの権限を効果的に管理する方法で、LDAP ベースの認証方法でも一般的に使用されます。

![screen_shot_2018-09-17at110505pm](assets/screen_shot_2018-09-17at110505pm.png)
