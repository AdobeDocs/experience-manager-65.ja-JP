---
title: AEM Mobile のセットアップ
seo-title: AEM Mobile のセットアップ
description: このページでは、AEM Mobile のセットアップをおこない、ユーザーが AEM 内でコンテンツを作成および管理できるようにする方法について説明します。このページは、AEM インスタンスをクラウドベースの AEM Mobile On-demand Services アカウントおよびプロジェクトと統合する詳細について説明します。
seo-description: このページでは、AEM Mobile のセットアップをおこない、ユーザーが AEM 内でコンテンツを作成および管理できるようにする方法について説明します。このページは、AEM インスタンスをクラウドベースの AEM Mobile On-demand Services アカウントおよびプロジェクトと統合する詳細について説明します。
uuid: 03bf5b56-7750-4f76-b079-43761367655a
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-on-demand-services-app
discoiquuid: 393cf504-917e-4bf6-9a8b-b7a5bd862c65
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '990'
ht-degree: 72%

---


# AEM Mobile のセットアップ{#aem-mobile-setup}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアント側レンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)を参照してください。

>[!CAUTION]
>
>AEM 6.2 または 6.3 から AEM 6.5 に移行する既存の AEM Mobile アプリユーザーは、[PackageShare からパッケージ](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/compatpack/aem-mobile-package)をダウンロードすれば、AEM Mobile アプリを引き続き使用できます。ただし、AEM 6.5 の新規インストールは、AEM Mobile アプリ機能をサポートしていません。

AEM を使用して AEM Mobile アプリ用のコンテンツを作成するには、AEM インスタンスをクラウドベースの AEM Mobile On-demand Services アカウントおよびプロジェクトと統合する必要があります。

以下の手順に従って、AEM Mobile の設定をおこない、ユーザーが AEM 内でコンテンツを作成および管理できるようにします。

## AEM Mobile のプロビジョニング {#aem-mobile-provisioning}

AEM Mobile のセットアップを始めるには、以下の作業が必要です。

* **APIキーのリクエスト**:On-Demand Services APIにアクセスするには、APIキーをリクエストする必要があります。 API キーをリクエストするには、[PDF フォーム](https://helpx.adobe.com/jp/digital-publishing-solution/help/integrating-dps.html)に記入します。Send the completed form to Adobe Developer Support: [wwds@adobe.com](mailto:wwds@adobe.com)

* **デバイスIDとデバイストークンの生成**:APIキーを受け取ったら、デバイスIDとデバイストークンを生成できます。 Go to [https://aex.aemmobile.adobe.com](https://aex.aemmobile.adobe.com/) and do the following:

   * API キーを提供します。
   * 以下の権限で AEM Mobile プロジェクトに追加した Adobe ID でログインします（プロジェクト作成手順については以下を参照してください）。

      * 管理：プロジェクトとユーザーを管理
      * コンテンツ：コンテンツを追加／編集、コンテンツを削除、コンテンツを表示、コンテンツを公開

すべての条件が満たされると、デバイスIDとデバイストークンが生成されます。

>[!NOTE]
>
>Adobe ID には、AEM Mobile プロジェクトへのアクセス権が与えられている必要があります。オンラインヘルプの [AEM Mobile のアカウント管理](https://helpx.adobe.com/jp/digital-publishing-solution/help/account-admin-dps.html)を参照してください。

## AEM Mobile のプロジェクトの作成 {#creating-projects-for-aem-mobile}

プロジェクトを作成する場合、iOS、Android、Windows、デスクトップ Web Viewer など、ターゲットとするプラットフォームの設定を指定します。指定する多くのプロジェクト設定は、アプリの動作に影響します。

プロジェクトを作成するには、マスター管理者の役割を持つ Adobe ID を使用して、On-demand Services ポータルにサインインする必要があります。Editing a project requires either a Master Admin role or a user role with a **Manage Projects and Users** permission.

>[!NOTE]
>
>To learn more about Creating Projects in AEM Mobile, click [here](https://helpx.adobe.com/jp/digital-publishing-solution/help/creating-projects.html).

## AEM Mobile コネクタの設定 {#configuring-an-aem-mobile-connector}

AEMのセットアップでは、コネクタの設定に次の手順を実行します。 AEM Mobile コネクタの設定が完了すると、ユーザーはユーザーグループおよび権限を設定できます。

AEM Mobile On-Demand コネクタは、AEM Mobile で管理するコンテンツを Adobe Experience Manager Mobile On-demand Services にバインドするために使用します。これにより、コンテンツ作成者は AEM のツールを使用してモバイルアプリケーション向けの素材を作成および管理しつつ、AEM Mobile On-demand Services を使用してモバイルコンテンツを容易に配布できます。

>[!NOTE]
>
>この手順は、AEM インスタンスのセットアップ時に 1 回のみおこないます。

### AEM Mobile On-demand Services Client の設定 {#configuring-aem-mobile-on-demand-services-client}

AEM Mobile 統合が正しく機能するには、設定手順を完了する必要があります。

1. OSGI サービスの設定に移動します。

   1. AEM／ツール／運営／Web コンソールを選択します。
   1. Scroll or search for ***Experience Manager Mobile On-demand Services Client (was Adobe Digital Publishing Solution Client)***

1. Edit ***Experience Manager Mobile On-demand Services Client***

   1. **（必須）** ：必須フィールドを入力します。

      1. クライアント ID
      1. クライアントの秘密鍵
   1. **（オプション）** 、既存の値を編集します。


1. 変更内容を保存します。
1. 次に設定の例を示します。

![chlimage_1-53](assets/chlimage_1-53.png)

### AEM Mobile On-demand Services クラウドサービスの設定 {#configuring-aem-mobile-on-demand-services-cloudservice}

1. クラウドサービスに移動します。

   1. AEM > Tools > Deployment> [CloudServices](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html). Scroll or search for ***Adobe Experience Manager Mobile On-demand Services***

1. Select ***Configure now*** or ***Show Configurations*** and select the add new configuration icon

1. 新しい設定を作成します。

   1. タイトルと名前を入力
   1. デバイスIDを入力
   1. 「デバイストークン」を入力します。
   1. Select ***Test Device Configuration*** to validate entered values
   1. 「OK」を選択します。

## AEM Mobile のユーザーの役割の追加と権限の割り当て {#adding-aem-mobile-user-roles-and-assigning-permissions}

プロジェクトを作成したら、役割を作成してユーザーにアクセス権を付与する必要があります。マスター管理者のみが、役割を作成および編集できます。役割を作成し、ユーザーに役割を割り当てると、その役割に含まれる機能（または権限）が有効になります。例えば、アプリの構築権限を含む役割を作成したり、コンテンツの作成と公開の権限を含む役割を作成したりできます。

AEM Mobile アプリの開発では、3 つの異なる役割が存在します。

* Administrator
* デベロッパー
* 作成者

For more information on creating roles with different permissions such as for app building or for creating and publishing content, click [Creating User Roles and Granting Access](https://helpx.adobe.com/jp/digital-publishing-solution/help/account-admin-dps.html) in AEM Mobile Help.

>[!NOTE]
>
>アプリコンテンツを管理するには、開発者、コンテンツ作成者および管理者が連携して作業する必要があります。作成者は、アプリ開発者が生成したテンプレートおよびコンポーネントに基づいて、ページを操作します。最後に、管理者が更新されたアプリコンテンツを戦略的に公開します。AEM のグループや権限を設定することで、アプリダッシュボードやコントロールセンターでのユーザーの役割が定義されます。
>
>For more information on AEM Mobile Dashboard, click [here](/help/mobile/mobile-apps-ondemand-application-dashboard.md).

Once you are done creating roles with different permissions such as for app building or for creating and publishing content, see [**Configure your User and User Groups**](/help/mobile/aem-mobile-configure-users.md) to configure your users and groups to support the authoring and mangement of your mobile apps.

### その他のリソース {#additional-resources}

AEM Mobile On-demand Services アプリ作成のその他の 2 つの役割および責任について詳しくは、以下のリソースを参照してください。

* [AEM Mobile On-demand Services の AEM コンテンツの開発](/help/mobile/aem-mobile-on-demand.md)
* [AEM Mobile On-demand Services アプリの AEM コンテンツのオーサリング](/help/mobile/mobile-apps-ondemand.md)

>[!NOTE]
>
>ページや記事の参照を含め、アプリコンテンツをプレビューするには、[プリフライトによるプレビュー](/help/mobile/aem-mobile-manage-ondemand-services.md)を参照してください。
