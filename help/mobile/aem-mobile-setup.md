---
title: AEM Mobile のセットアップ
seo-title: AEM Mobile SetUp
description: このページでは、AEM Mobileを設定し、AEM内でコンテンツを作成および管理できるようにする方法について説明します。 このページでは、AEMインスタンスをクラウドベースのAEM Mobile On-demand Servicesアカウントおよびプロジェクトと統合する方法について説明します。
seo-description: Follow this page for setting up AEM Mobile and thus allowing the user to create and manage the content within AEM. This page provides information on integrating the AEM instance with the cloud-based AEM Mobile On-Demand Services account and project(s).
uuid: 03bf5b56-7750-4f76-b079-43761367655a
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-on-demand-services-app
discoiquuid: 393cf504-917e-4bf6-9a8b-b7a5bd862c65
exl-id: 0ead982d-2315-4947-b762-596aa2aa42a1
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '929'
ht-degree: 3%

---

# AEM Mobile のセットアップ{#aem-mobile-setup}

>[!NOTE]
>
>Adobeは、単一ページアプリケーションのフレームワークベースのクライアントサイドレンダリング（React など）を必要とするプロジェクトでは、SPA Editor を使用することをお勧めします。 [詳細情報](/help/sites-developing/spa-overview.md)。

>[!CAUTION]
>
>AEM 6.2 または 6.3 からAEM 6.5 に移行する既存のAEM Mobile Apps のお客様は、引き続き PackageShare からパッケージをダウンロードしてAEM Mobile Apps を使用できます。 ただし、AEM 6.5 の新規インストールでは、AEM Mobile Apps 機能はサポートされません。

AEMを使用してAEM Mobileアプリ用のコンテンツを作成するには、AEMインスタンスをクラウドベースのAEM Mobile On-demand Servicesアカウントおよびプロジェクトと統合する必要があります。

AEM Mobileを設定し、ユーザーがAEM内でコンテンツを作成および管理できるようにするには、次の手順に従います。

## AEM Mobile Provisioning {#aem-mobile-provisioning}

AEM Mobileの設定を開始するには、次の操作が必要です。

* **API キーのリクエスト**:On-Demand Services API にアクセスするには、API キーをリクエストする必要があります。 API キーをリクエストするには、 [PDF型](https://helpx.adobe.com/digital-publishing-solution/help/aem-mobile-end-of-life-faq.html). 入力したフォームをAdobe Developerサポートに送信します。 [wwds@adobe.com](mailto:wwds@adobe.com)

* **デバイス ID とデバイストークンの生成**:API キーを受け取ったら、デバイス ID とデバイストークンを生成できます。 に移動します。 `https://aex.aemmobile.adobe.com` 次の操作を実行します。

   * API キーの指定
   * 次の権限でAEM Mobileプロジェクトに追加したAdobe IDでログインします（以下の手順でプロジェクトを作成します）。

      * 管理/プロジェクトとユーザーを管理
      * コンテンツ/コンテンツの追加と編集、コンテンツの削除、コンテンツの表示、コンテンツの公開

すべての条件が満たされた場合、デバイス ID とデバイストークンが生成されます。

>[!NOTE]
>
>Adobe IDには、AEM Mobileプロジェクトでのアクセス権が付与されている必要があります。 詳しくは、 [AEM Mobileのアカウント管理](https://helpx.adobe.com/digital-publishing-solution/help/aem-mobile-end-of-life-faq.html) 」をオンラインヘルプに追加しました。

## AEM Mobile用プロジェクトの作成 {#creating-projects-for-aem-mobile}

プロジェクトを作成する際には、ターゲットとするすべてのプラットフォームの設定を指定します。iOS、Android、Windows、デスクトップ Web Viewer。 指定するプロジェクト設定の多くは、アプリの動作に影響します。

プロジェクトを作成するには、マスター管理者の役割を持つAdobe IDを使用して On-Demand Services ポータルにログインする必要があります。 プロジェクトを編集するには、マスター管理者の役割か、 **プロジェクトとユーザーを管理** 権限。

>[!NOTE]
>
>AEM Mobileでのプロジェクトの作成について詳しくは、 [ここ](https://helpx.adobe.com/digital-publishing-solution/help/creating-projects.html).

## AEM Mobile Connector の設定 {#configuring-an-aem-mobile-connector}

AEMの設定では、コネクタの設定に次の手順を実行します。 AEM Mobileコネクタの設定が完了したら、ユーザーグループと権限を設定できます。

AEM Mobile On-Demand コネクタは、AEM Mobileが管理するコンテンツをAdobe Experience Manager Mobileの On-Demand サービスとバインドするために使用されます。 これにより、コンテンツ作成者は、AEMツールを使用してモバイルアプリケーション用の資料を作成および管理し、AEM Mobileの On-Demand サービスを使用してモバイルコンテンツを簡単に配布できます。

>[!NOTE]
>
>これは、AEMインスタンスをセットアップする 1 回限りの手順です。

### AEM Mobile On-demand Services Client の設定 {#configuring-aem-mobile-on-demand-services-client}

AEM Mobile統合が正しく機能するには、設定手順を完了する必要があります。

1. OSGi サービス設定に移動

   1. AEM /ツール/操作/ Web コンソール
   1. スクロールするか、 ***Experience ManagerMobile On-demand Services クライアント ( 旧AdobeDigital Publishing Solution クライアント )***

1. 編集 ***Experience ManagerMobile On-demand Services クライアント***

   1. **（必須）** 必須フィールドを入力：

      1. クライアント ID.
      1. クライアントの秘密鍵.

   1. **（オプション）** 既存の値を編集します。

1. 変更を保存します。
1. 次に設定例を示します。

![chlimage_1-53](assets/chlimage_1-53.png)

### AEM Mobile On-demand Services CloudService の設定 {#configuring-aem-mobile-on-demand-services-cloudservice}

1. Cloud Services

   1. AEM /ツール/デプロイメント > [CloudServices](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html). スクロールするか、 ***Adobe Experience Manager Mobile On-demand Services***

1. 選択 ***今すぐ設定*** または ***設定を表示*** 「新しい設定を追加」アイコンを選択します。

1. 新しい設定を作成

   1. タイトルと名前を入力
   1. デバイス ID を入力
   1. デバイストークンを入力
   1. 選択 ***デバイス設定をテスト*** 入力した値を検証するには
   1. OK を選択

## AEM Mobileユーザーの役割の追加と権限の割り当て {#adding-aem-mobile-user-roles-and-assigning-permissions}

プロジェクトを作成したら、役割を作成し、ユーザーにアクセス権を付与する必要があります。 マスター管理者のみ、役割を作成および編集できます。 ロールを作成する際には、権限が割り当てられているユーザーの機能（または権限）を有効にします。 例えば、アプリの作成権限を含む役割と、コンテンツの作成および公開権限を含む役割を作成できます。

AEM Mobileアプリの開発では、次の 3 つの異なる役割が存在します。

* 管理者
* デベロッパー
* オーサー

アプリの作成やコンテンツの作成および公開など、様々な権限を持つロールの作成について詳しくは、 [ユーザー・ロールの作成とアクセス権の付与](https://helpx.adobe.com/digital-publishing-solution/help/account-admin-dps.html) (AEM Mobileヘルプ )

>[!NOTE]
>
>アプリコンテンツの管理には、開発者、コンテンツ作成者、管理者が共同で取り組む必要があります。 作成者はページを操作します。ページは、アプリ開発者が生成したテンプレートやコンポーネントに基づいています。 最後に、管理者は更新されたアプリコンテンツを戦略的に公開します。 AEMグループと権限の設定は、アプリダッシュボードまたはコントロールセンターでのグループと権限の役割を定義します。
>
>AEM Mobile Dashboard について詳しくは、 [ここ](/help/mobile/mobile-apps-ondemand-application-dashboard.md).

アプリの作成やコンテンツの作成および公開など、様々な権限を持つ役割の作成が完了したら、 [**ユーザーおよびユーザーグループの設定**](/help/mobile/aem-mobile-configure-users.md) モバイルアプリのオーサリングと管理をサポートするようにユーザーとグループを設定する場合。

### その他のリソース {#additional-resources}

AEM Mobile On-demand Services App の作成に関する他の 2 つの役割と責務について詳しくは、次のリソースを参照してください。

* [AEM Mobile On-demand Services向けAEMコンテンツの開発](/help/mobile/aem-mobile-on-demand.md)
* [AEM Mobile On-demand Servicesアプリ用AEMコンテンツのオーサリング](/help/mobile/mobile-apps-ondemand.md)

>[!NOTE]
>
>ページや記事の参照を含む、アプリのコンテンツをプレビューするには、 [プリフライトでのプレビュー](/help/mobile/aem-mobile-manage-ondemand-services.md).
