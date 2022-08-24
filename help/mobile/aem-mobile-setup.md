---
title: AEM Mobile のセットアップ
seo-title: AEM Mobile SetUp
description: このページでは、AEM Mobile のセットアップをおこない、ユーザーが AEM 内でコンテンツを作成および管理できるようにする方法について説明します。このページは、AEM インスタンスをクラウドベースの AEM Mobile On-demand Services アカウントおよびプロジェクトと統合する詳細について説明します。
seo-description: Follow this page for setting up AEM Mobile and thus allowing the user to create and manage the content within AEM. This page provides information on integrating the AEM instance with the cloud-based AEM Mobile On-Demand Services account and project(s).
uuid: 03bf5b56-7750-4f76-b079-43761367655a
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-on-demand-services-app
discoiquuid: 393cf504-917e-4bf6-9a8b-b7a5bd862c65
exl-id: 0ead982d-2315-4947-b762-596aa2aa42a1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '946'
ht-degree: 71%

---

# AEM Mobile のセットアップ{#aem-mobile-setup}

>[!NOTE]
>
>アドビは、シングルページアプリケーションフレームワークをベースにしたクライアント側のレンダリング（React など）を必要とするプロジェクトには SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)を参照してください。

>[!CAUTION]
>
>AEM 6.2 または 6.3 から AEM 6.5 に移行する既存の AEM Mobile アプリユーザーは、[PackageShare からパッケージ](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/compatpack/aem-mobile-package)をダウンロードすれば、AEM Mobile アプリを引き続き使用できます。ただし、AEM 6.5 の新規インストールは、AEM Mobile アプリ機能をサポートしていません。

AEM を使用して AEM Mobile アプリ用のコンテンツを作成するには、AEM インスタンスをクラウドベースの AEM Mobile On-demand Services アカウントおよびプロジェクトと統合する必要があります。

以下の手順に従って、AEM Mobile の設定をおこない、ユーザーが AEM 内でコンテンツを作成および管理できるようにします。

## AEM Mobile のプロビジョニング {#aem-mobile-provisioning}

AEM Mobile のセットアップを始めるには、以下の作業が必要です。

* **API キーのリクエスト**:On-Demand Services API にアクセスするには、API キーをリクエストする必要があります。 API キーをリクエストするには、[PDF フォーム](https://helpx.adobe.com/jp/digital-publishing-solution/help/integrating-dps.html)に記入します。入力したフォームをAdobe Developerサポートに送信します。 [wwds@adobe.com](mailto:wwds@adobe.com)

* **デバイス ID とデバイストークンの生成**:API キーを受け取ったら、デバイス ID とデバイストークンを生成できます。 に移動します。 [https://aex.aemmobile.adobe.com](https://aex.aemmobile.adobe.com/) 次の操作を実行します。

   * API キーを提供します。
   * 以下の権限で AEM Mobile プロジェクトに追加した Adobe ID でログインします（プロジェクト作成手順については以下を参照してください）。

      * 管理：プロジェクトとユーザーを管理
      * コンテンツ：コンテンツを追加／編集、コンテンツを削除、コンテンツを表示、コンテンツを公開

すべての条件が満たされた場合、デバイス ID とデバイストークンが生成されます。

>[!NOTE]
>
>Adobe ID には、AEM Mobile プロジェクトへのアクセス権が与えられている必要があります。オンラインヘルプの [AEM Mobile のアカウント管理](https://helpx.adobe.com/jp/digital-publishing-solution/help/account-admin-dps.html)を参照してください。

## AEM Mobile のプロジェクトの作成 {#creating-projects-for-aem-mobile}

プロジェクトを作成する場合、iOS、Android、Windows、デスクトップ Web Viewer など、ターゲットとするプラットフォームの設定を指定します。指定する多くのプロジェクト設定は、アプリの動作に影響します。

プロジェクトを作成するには、マスター管理者の役割を持つ Adobe ID を使用して、On-demand Services ポータルにサインインする必要があります。プロジェクトを編集するには、マスター管理者の役割か、 **プロジェクトとユーザーを管理** 権限。

>[!NOTE]
>
>AEM Mobileでのプロジェクトの作成について詳しくは、 [ここ](https://helpx.adobe.com/jp/digital-publishing-solution/help/creating-projects.html).

## AEM Mobile コネクタの設定 {#configuring-an-aem-mobile-connector}

AEMの設定では、コネクタの設定に次の手順を実行します。 AEM Mobile コネクタの設定が完了すると、ユーザーはユーザーグループおよび権限を設定できます。

AEM Mobile On-Demand コネクタは、AEM Mobile で管理するコンテンツを Adobe Experience Manager Mobile On-demand Services にバインドするために使用します。これにより、コンテンツ作成者は AEM のツールを使用してモバイルアプリケーション向けの素材を作成および管理しつつ、AEM Mobile On-demand Services を使用してモバイルコンテンツを容易に配布できます。

>[!NOTE]
>
>この手順は、AEM インスタンスのセットアップ時に 1 回のみおこないます。

### AEM Mobile On-demand Services Client の設定 {#configuring-aem-mobile-on-demand-services-client}

AEM Mobile 統合が正しく機能するには、設定手順を完了する必要があります。

1. OSGI サービスの設定に移動します。

   1. AEM／ツール／運営／Web コンソールを選択します。
   1. スクロールするか、 ***Experience ManagerMobile On-demand Services クライアント ( 旧AdobeDigital Publishing Solution クライアント )***

1. 編集 ***Experience ManagerMobile On-demand Services クライアント***

   1. **（必須）** 必須フィールドを入力：

      1. クライアント ID
      1. クライアントの秘密鍵.
   1. **（オプション）** 既存の値を編集します。


1. 変更を保存します。
1. 次に設定の例を示します。

![chlimage_1-53](assets/chlimage_1-53.png)

### AEM Mobile On-demand Services クラウドサービスの設定 {#configuring-aem-mobile-on-demand-services-cloudservice}

1. クラウドサービスに移動します。

   1. AEM /ツール/デプロイメント > [CloudServices](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html). スクロールするか、 ***Adobe Experience Manager Mobile On-demand Services***

1. 選択 ***今すぐ設定*** または ***設定を表示*** 「新しい設定を追加」アイコンを選択します。

1. 新しい設定を作成します。

   1. タイトルと名前を入力
   1. デバイス ID を入力
   1. 「デバイストークン」を入力します。
   1. 選択 ***デバイス設定をテスト*** 入力した値を検証するには
   1. 「OK」を選択します。

## AEM Mobile のユーザーの役割の追加と権限の割り当て {#adding-aem-mobile-user-roles-and-assigning-permissions}

プロジェクトを作成したら、役割を作成してユーザーにアクセス権を付与する必要があります。マスター管理者のみが、役割を作成および編集できます。役割を作成し、ユーザーに役割を割り当てると、その役割に含まれる機能（または権限）が有効になります。例えば、アプリの構築権限を含む役割を作成したり、コンテンツの作成と公開の権限を含む役割を作成したりできます。

AEM Mobile アプリの開発では、3 つの異なる役割が存在します。

* 管理者
* デベロッパー
* オーサー

アプリの作成やコンテンツの作成および公開など、様々な権限を持つロールの作成について詳しくは、 [ユーザー・ロールの作成とアクセス権の付与](https://helpx.adobe.com/digital-publishing-solution/help/account-admin-dps.html) (AEM Mobileヘルプ )

>[!NOTE]
>
>アプリコンテンツを管理するには、開発者、コンテンツ作成者および管理者が連携して作業する必要があります。作成者は、アプリ開発者が生成したテンプレートおよびコンポーネントに基づいて、ページを操作します。最後に、管理者が更新されたアプリコンテンツを戦略的に公開します。AEM のグループや権限を設定することで、アプリダッシュボードやコントロールセンターでのユーザーの役割が定義されます。
>
>AEM Mobile Dashboard について詳しくは、 [ここ](/help/mobile/mobile-apps-ondemand-application-dashboard.md).

アプリの作成やコンテンツの作成および公開など、様々な権限を持つ役割の作成が完了したら、 [**ユーザーおよびユーザーグループの設定**](/help/mobile/aem-mobile-configure-users.md) モバイルアプリのオーサリングと管理をサポートするようにユーザーとグループを設定する場合。

### その他のリソース {#additional-resources}

AEM Mobile On-demand Services アプリ作成のその他の 2 つの役割および責任について詳しくは、以下のリソースを参照してください。

* [AEM Mobile On-demand Services の AEM コンテンツの開発](/help/mobile/aem-mobile-on-demand.md)
* [AEM Mobile On-demand Services アプリの AEM コンテンツのオーサリング](/help/mobile/mobile-apps-ondemand.md)

>[!NOTE]
>
>ページや記事の参照を含め、アプリコンテンツをプレビューするには、[プリフライトによるプレビュー](/help/mobile/aem-mobile-manage-ondemand-services.md)を参照してください。
