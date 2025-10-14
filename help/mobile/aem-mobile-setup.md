---
title: AEM Mobile のセットアップ
description: このページでは、AEM Mobileを設定し、Adobe Experience Manager（AEM）内でコンテンツを作成および管理する方法について説明します。 AEM インスタンスとクラウドベースのAEM Mobile On-demand Services アカウントおよびプロジェクトの統合について説明します。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-on-demand-services-app
exl-id: 0ead982d-2315-4947-b762-596aa2aa42a1
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '889'
ht-degree: 1%

---

# AEM Mobile のセットアップ{#aem-mobile-setup}

{{ue-over-mobile}}

>[!CAUTION]
>
>Adobe Experience Manager（AEM）モバイルアプリの既存のお客様がAEM 6.2 または 6.3 からAEM 6.5 に移行する場合は、Package Share からパッケージをダウンロードすることで、AEM Mobile アプリを引き続き使用できます。 ただし、AEM 6.5 の新規インストールでは、AEM Mobile アプリ機能はサポートされていません。

AEMを使用してAEM Mobile アプリ用のコンテンツを作成するには、AEM インスタンスをクラウドベースのAEM Mobile On-demand Services アカウントおよびプロジェクトに統合する必要があります。

次の手順に従って、AEM Mobileを設定し、ユーザーがAEM内でコンテンツを作成および管理できるようにします。

## AEM Mobile プロビジョニング {#aem-mobile-provisioning}

AEM Mobileの設定を開始するには、次の操作を行う必要があります。

* **API キーのリクエスト**: On-Demand Services API にアクセスするには、API キーをリクエストする必要があります。 API キーをリクエストするには、[PDFフォーム &#x200B;](https://helpx.adobe.com/jp/digital-publishing-solution/help/aem-mobile-end-of-life-faq.html) に入力します。 入力済みのフォームをAdobe Developer サポートに送信：[wwds@adobe.com](mailto:wwds@adobe.com)

* **デバイス ID とデバイストークンの生成**:API キーを受け取ったら、デバイス ID とデバイストークンを生成できます。 `https://aex.aemmobile.adobe.com` に移動して、次の操作を実行します。

   * API キーの指定
   * 次の権限を持つAEM Mobile プロジェクトに追加したAdobe IDでログインします（プロジェクトを作成するには、次の手順を参照してください）

      * 管理/ プロジェクトとユーザーの管理
      * コンテンツ / コンテンツの追加と編集、コンテンツの削除、コンテンツの表示、Publish コンテンツ

すべての条件が満たされた場合、デバイス ID とデバイストークンが生成されます。

>[!NOTE]
>
>必要なAdobe IDには、AEM Mobile プロジェクトへのアクセス権を付与する必要があります。 オンラインヘルプの [AEM Mobileのアカウント管理 &#x200B;](https://helpx.adobe.com/jp/digital-publishing-solution/help/aem-mobile-end-of-life-faq.html) を参照してください。

## AEM Mobileのプロジェクトの作成 {#creating-projects-for-aem-mobile}

プロジェクトを作成する場合は、ターゲットとするプラットフォーム（iOS、Android™、Windows、デスクトップ Web ビューア）の設定を指定します。 指定するプロジェクト設定の多くは、アプリの動作に影響を与えます。

プロジェクトを作成するには、マスター管理者のロールを持つAdobe IDを使用して On-Demand Services ポータルにログインする必要があります。 プロジェクトを編集するには、マスター管理者ロールまたは **プロジェクトとユーザーの管理** 権限を持つユーザーロールが必要です。

>[!NOTE]
>
>AEM Mobileでのプロジェクトの作成について詳しくは、[&#x200B; こちら &#x200B;](https://helpx.adobe.com/jp/digital-publishing-solution/help/creating-projects.html) をクリックしてください。

## AEM Mobile Connector の設定 {#configuring-an-aem-mobile-connector}

AEMのセットアップには、コネクタ設定の次の手順が含まれます。 AEM Mobile コネクタの設定が完了したら、ユーザーは、ユーザーグループと権限を設定できます。

AEM Mobile On-Demand コネクタは、AEM Mobileの管理コンテンツをAdobe Experience Manager Mobileの On-Demand サービスにバインドするために使用されます。 これにより、コンテンツ作成者は、AEM ツールを使用してモバイルアプリケーション用の資料を作成および管理しながら、AEM Mobileのオンデマンド サービスを使用してモバイルコンテンツを簡単に配布できます。

>[!NOTE]
>
>これは、AEM インスタンスを設定するための 1 回限りの手順です。

### AEM Mobile On-demand Services クライアントの設定 {#configuring-aem-mobile-on-demand-services-client}

AEM Mobile統合が正しく機能するように、設定手順を実行します。

1. OSGI サービス設定に移動します

   1. AEM/ツール/操作/Web コンソール
   1. スクロールするか、***Experience Manager Mobile On-demand Services Client （以前はAdobeデジタル公開ソリューションクライアント）を検索しま***。

1. ***Experience Manager Mobile On-Demand Services クライアント*** を編集します

   1. **（必須）** 必須フィールドを入力します。

      1. クライアント ID。
      1. クライアントの秘密鍵。

   1. **（任意）** 既存の値を編集します。

1. 変更を保存します。
1. 設定例を次に示します。

![chlimage_1-53](assets/chlimage_1-53.png)

### AEM Mobile On-demand Services CloudService の設定 {#configuring-aem-mobile-on-demand-services-cloudservice}

1. Cloud Serviceに移動します。

   1. AEM/ツール/デプロイメント/[CloudServices](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html) に移動します。 スクロールするか、***Adobe Experience Manager Mobile On-demand Services*** を検索します

1. ***今すぐ設定*** または ***設定を表示*** を選択し、設定を追加アイコンを選択します。

1. 設定の作成

   1. タイトルと名前を入力
   1. デバイス Id を入力
   1. デバイストークンを入力
   1. ***デバイス設定をテスト*** を選択すると、入力した値を検証できます
   1. 「OK」を選択します。

## AEM Mobile ユーザーの役割の追加と権限の割り当て {#adding-aem-mobile-user-roles-and-assigning-permissions}

プロジェクトの作成後、役割を作成し、ユーザーにアクセス権を付与する必要があります。 マスター管理者のみが、ロールを作成および編集できます。 役割を作成する際は、権限が割り当てられているユーザーに対して機能（または権限）を有効にします。 例えば、アプリを作成するための権限を含む 1 つの役割と、コンテンツを作成および公開するための権限を含む別の役割を作成できます。

AEM Mobile アプリケーションの開発には、次の 3 つの異なるロールがあります。

* 管理者
* 開発者
* 作成者

様々な権限（アプリの構築やコンテンツの作成および公開など）を持つロールの作成について詳しくは、AEM Mobile ヘルプの [&#x200B; ユーザーロールの作成とアクセスの許可 &#x200B;](https://helpx.adobe.com/jp/digital-publishing-solution/help/account-admin-dps.html) をクリックしてください。

>[!NOTE]
>
>アプリコンテンツの管理には、開発者、コンテンツ作成者および管理者の協力が必要です。 作成者がページを操作します。これは、アプリ開発者が生成したテンプレートとコンポーネントに基づいて行われます。 最後に、管理者は、更新されたアプリコンテンツを戦略的に公開します。 AEMのグループと権限を設定すると、そのグループと権限のロールが App Dashboard または Control Center で定義されます。
>
>[AEM Mobile ダッシュボード &#x200B;](/help/mobile/mobile-apps-ondemand-application-dashboard.md) を参照してください。

アプリケーションの構築や、コンテンツの作成および公開など、様々な権限を持つ役割の作成が完了したら、[**ユーザーおよびユーザーグループの設定**](/help/mobile/aem-mobile-configure-users.md) を参照してください。 これにより、モバイルアプリのオーサリングと管理をサポートするユーザーとグループを設定できます。

### その他のリソース {#additional-resources}

AEM Mobile On-demand Services アプリケーションを作成するための他の 2 つの役割と責務について詳しくは、次の資料を参照してください。

* [AEM Mobile On-demand Services用AEM コンテンツの開発](/help/mobile/aem-mobile-on-demand.md)
* [AEM Mobile On-demand Services アプリケーション用AEM コンテンツのオーサリング](/help/mobile/mobile-apps-ondemand.md)

>[!NOTE]
>
>ページの参照や記事を含む、アプリのコンテンツをプレビューするには、[&#x200B; プリフライトを使用したプレビュー &#x200B;](/help/mobile/aem-mobile-manage-ondemand-services.md) を参照してください。
