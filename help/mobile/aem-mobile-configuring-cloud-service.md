---
title: Adobe Target Cloud Service の設定
description: このページでは、ユーザーとグループの適切な権限セットの取得方法、クラウドサービスの作成方法、アクティビティ用のアプリケーションの設定方法、最後にコンテンツの生成方法を説明します。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: d370d772-ef4d-4f38-826c-e90d07735822
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1254'
ht-degree: 4%

---

# Adobe Target Cloud Service の設定 {#configuring-adobe-target-cloud-service}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアントサイドレンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)。

>[!NOTE]
>
>このドキュメントは [Adobe Experience Manager（AEM） Mobile の概要 ](/help/mobile/getting-started-aem-mobile.md) ガイドの一部であり、AEM Mobile リファレンスの出発点として推奨されています。

コンテンツ作成者がモバイルアプリ用のターゲットコンテンツの生成を開始するには、いくつかの手順を実行する必要があります。ユーザーとグループに適切な権限セットを取得し、クラウドサービスを作成し、アクティビティ用のアプリケーションを設定して、最後にコンテンツを生成します。

今後、[AEM Mobile ハイブリッド参照アプリケーション ](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) が正常にデプロイされ、AEM Mobile Dashboard を介してアクセスできるようになることを想定しています。

## 権限 {#permissions}

パーソナライゼーションコンソールへのアクセスを必要とするユーザーは、`target-activity-authors` グループに属している必要があります。 ユーザーとグループの設定の一環として、target-activity-group を apps-admins グループに追加することをお勧めします。 target-activity-authors グループを追加すると、Personalizationのナビゲーションメニューエントリを表示できます。

パーソナライゼーションAdmin Consoleへのアクセス権を付与するユーザーまたはグループを target-activity-authors グループに追加し忘れると、パーソナライゼーションコンソールが表示されなくなります。

## クラウドサービス {#cloud-services}

モバイルアプリケーションでターゲットコンテンツを動作させるには、Adobe Target サービスとAdobe Mobile Services サービスの 2 つのサービスを設定する必要があります。 Adobe Target サービスは、クライアントリクエストを処理し、パーソナライズされたコンテンツを返すためのエンジンを提供します。 AdobeMobile Services サービスは、AMS Cordova プラグインが使用する ADBMobileConfig.json ファイルを介して、Adobe サービスとモバイルアプリケーション間の接続を提供します。 AEM Mobileのダッシュボードから、2 つのサービスを追加してアプリケーションを設定できます。

## Adobe Target Cloud Service {#adobe-target-cloud-service}

AEM Mobile ダッシュボードで、管理Cloud Serviceを見つけて、「+」ボタンをクリックします。

![chlimage_1-8](assets/chlimage_1-8.png)

Cloud Serviceを追加ウィザードで、「Adobe Target」クラウドサービスカードを選択し、「次へ」をクリックします。

![chlimage_1-9](assets/chlimage_1-9.png)

設定を選択ドロップダウンから、設定を作成するか、既存の設定から選択できます。 設定を作成するには、ドロップダウンから「設定を作成」を選択します。 Target 設定のタイトルを入力します。 Target アカウントに関連付けられているクライアントコード、メールおよびパスワードを入力します。 これらのフィールドの値が不明な場合は、Adobe Target サポートにお問い合わせください。 「検証」ボタンをクリックして、資格情報を検証します。 確認が完了したら、「送信」ボタンをクリックして、クラウドサービスを作成します。

作成されるクラウドサービスは、ウィザードを使用してモバイルアプリケーションに自動的に関連付けられます。 cq:cloudserviceconfig プロパティ値は、apps グループノードの jcr:content ノードに設定されます。 ハイブリッドアプリサンプルの場合、設定は/content/mobileapps/hybrid-reference-app/jcr:content に設定され、値は自動生成されたフレームワークノードを指します。は、/etc/cloudservices/testandtarget/adobe-target—aem-apps/framework にあります。 フレームワークノードには、デフォルトで性別と年齢の 2 つのプロパティが設定されています。 このフレームワークは、AEMのプレビューでのみ使用され、デバイスには影響しません。

ウィザードが完了すると、Cloud Serviceを管理タイルに Target Cloud Service が表示されますが、Adobe Mobile Service アカウントが見つからないことに関する警告が表示されます。

![chlimage_1-10](assets/chlimage_1-10.png)

## Adobeモバイルサービス {#adobe-mobile-service}

アプリケーションにもAdobe Mobile Services （AMS）アカウントをリンクする必要があります。AMS サービスは、Target クライアントコード情報を含む必須の ADBMobileConfig.json ファイルを提供します。 AMS アカウントとの関連付けを作成する前に、AMS への権限を持つユーザーが AMS アカウントを変更する必要があります。

### クライアントコード {#client-code}

AMS サービスにログインするには、[https://mobilemarketing.adobe.com](https://mobilemarketing.adobe.com/) にアクセスし、モバイルアプリケーションを選択して、設定をクリックします。 「SDK ターゲットオプション」フィールドを見つけ、フィールドにクライアントコードを配置して、「保存」をクリックします。

![chlimage_1-11](assets/chlimage_1-11.png)

これで、クライアントコードがモバイルアプリケーションに関連付けられたので、AMS クラウドサービスがAdobeモバイルダッシュボードを使用して設定された場合、サービス設定の設定は ADBMobileConfig.json ファイルを使用して配信されます。

### Adobe モバイル サービスのサービス {#adobe-mobile-service-could-service}

これで AMS が設定されたので、モバイルアプリケーションをAdobeモバイルダッシュボードに関連付けます。 AEM Mobile ダッシュボードで、管理Cloud Serviceを見つけて、「+」ボタンをクリックします。

![chlimage_1-12](assets/chlimage_1-12.png)

Adobe Mobile Services カードを選択し、「次へ」をクリックします。

![chlimage_1-13](assets/chlimage_1-13.png)

ウィザードを作成または選択の手順で、Mobile Service ドロップダウンを選択し、設定を作成エントリを選択します。 タイトル、会社名、ユーザー名、パスワードを入力し、適切なデータセンターを選択します。 これらの値がわからない場合は、Adobeの Mobile Service 管理者に問い合わせて値を取得してください。 すべてのフィールドに入力したら、「**確認**」をクリックします。 検証プロセスは AMS に移動し、アカウントの資格情報を検証します。検証が成功すると、モバイルアプリケーションのリストが生成され、関連するモバイルアプリケーションをドロップダウンから選択します。 「送信」ボタンをクリックして、ウィザードを完了します。 設定データおよびアプリケーションに関連する分析の取得には、プロセスに少し時間がかかる場合があります。 プロセスが完了したら、モーダルの「**完了**」をクリックして、Adobeモバイルダッシュボードに戻ります。

モバイルダッシュボードに戻ると、Cloud Serviceを管理タイルに AMS Cloud Service が含まれています。 また、分析指標タイルには、ライフサイクルレポートも表示されます。

![chlimage_1-14](assets/chlimage_1-14.png)

## Target コンテンツ同期ハンドラー {#target-content-sync-handlers}

ユーザーのデバイスにコンテンツを配信するために、AEM コンテンツ作成者によって作成されたオファーをレンダリングしてコンテンツを生成します。 ターゲットオファーのレンダリングを処理するために、オファーを処理する新しいコンテンツ同期ハンドラーが追加されました。 ハイブリッド参照アプリケーションをサンプルとして使用する場合、en （英語）コンテンツパッケージには、[mobileappoffers](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/aem-package/content-author/src/main/content/jcr_root/content/mobileapps/hybrid-reference-app/en/_jcr_content/pge-app/app-config-dev/targetOffers/.content.xml) ハンドラーを持つ ContentSyncConfig が含まれています。 次のステップは、デバイスへのオファーをレンダリングする場合に重要です。 mobileappoffers ハンドラーには、アプリケーションに使用されるパーソナライゼーションアクティビティへのパスを識別するパスプロパティがあります。

例えば、*/content/campaigns/hybridref* にアクティビティがある場合、このパスをコピーして、mobileappoffers ハンドラーの *path* プロパティの値として貼り付けます。

ハイブリッド参照アプリケーションには、開発用と実稼動用の 2 つの mobileappoffers ハンドラーがあります。

mobileappoffers ハンドラーの path プロパティにアクティビティパスが設定されたら、ハンドラーを保存します。 これで、ハンドラーは、モバイルデバイス向けのオファーのレンダリングを開始する準備が整いました。

### レンダリングモード {#render-mode}

mobileappoffers ハンドラーの設定は、公開の設定と開発の設定で異なります。 パブリッシュ設定には、cq:ContentSyncConfig ノードに値が *publish* に設定された *renderMode* というプロパティがあります。 mobileappoffers ハンドラーは renderMode を参照し、「公開」に設定されている場合は、作成された mbox id を編集します。 AEMで作成される mbox には、デフォルトで、mbox id に – author 値が付加されます。 これは、アクティビティが公開されていないことを示すステータスで、オファーの解決に未公開のキャンペーンを使用する必要があります。

Adobeモバイルダッシュボードを使用してコンテンツをステージングすると、ステージングされたコンテンツは実稼動用コンテンツと見なされ、開発以外のコンテンツ同期設定を使用してレンダリングされます。 このようにレンダリングすると、—author がすべての mbox ID から削除され、公開済みアクティビティが Target サーバーで使用できるようになります。 ステージングされたコンテンツをテストする前に、アクティビティが公開されていることを確認します。

## コンテンツの作成 {#creating-content}

クラウドサービスが作成され、mobileappoffers ハンドラーが設定されたので、コンテンツ作成者はターゲット設定されたエクスペリエンスの生成を開始できます。
