---
title: Adobe Target Cloud Service の設定
description: このページでは、ユーザーとグループに対する適切な権限のセットを取得する方法、クラウドサービスを作成する方法、アクティビティのアプリケーションを設定する方法、最後にコンテンツを生成する方法について説明します。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: d370d772-ef4d-4f38-826c-e90d07735822
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1274'
ht-degree: 2%

---

# Adobe Target Cloud Service の設定 {#configuring-adobe-target-cloud-service}

>[!NOTE]
>
>Adobeは、単一ページアプリケーションのフレームワークベースのクライアントサイドレンダリング（React など）を必要とするプロジェクトでは、SPA Editor を使用することをお勧めします。 [詳細情報](/help/sites-developing/spa-overview.md)。

>[!NOTE]
>
>このドキュメントは、 [Adobe Experience Manager(AEM)Mobile の概要](/help/mobile/getting-started-aem-mobile.md) ガイド (AEM Mobileリファレンスの出発点として推奨 )。

コンテンツ作成者がモバイルアプリ用のターゲットコンテンツの生成を開始する前に、いくつかの手順を組み合わせる必要があります。ユーザーとグループに対する適切な権限のセットの取得、クラウドサービスの作成、アクティビティ用のアプリケーションの設定、最後にコンテンツの生成です。

今後の想定は、 [AEM Mobile Hybrid Reference Application](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) は、AEM Mobile Dashboard を通じて正常にデプロイされ、アクセスできるようになりました。

## 権限 {#permissions}

パーソナライゼーションコンソールへのアクセスを必要とするユーザーは、 `target-activity-authors` グループ化します。 ユーザーとグループの設定の一環として、 target-activity-group を apps-admins グループに追加することをお勧めします。 target-activity-authors グループを追加すると、パーソナライゼーションのナビゲーションメニューエントリを表示できます。

パーソナライゼーションAdmin Consoleにアクセスするユーザーまたはグループを target-activity-authors グループに追加し忘れると、ユーザーはパーソナライゼーションコンソールを表示できなくなります。

## Cloud Services {#cloud-services}

モバイルアプリケーションでターゲットコンテンツを機能させるには、Adobe TargetサービスとAdobeMobile Services サービスの 2 つのサービスを設定する必要があります。 Adobe Targetサービスは、クライアントリクエストを処理し、パーソナライズされたコンテンツを返すためのエンジンを提供します。 AdobeMobile Services サービスは、AMS Cordova プラグインで使用される ADBMobileConfig.json ファイルを介して、Adobe サービスとモバイルアプリケーション間の接続を提供します。 AEM Mobile Dashboard から、2 つのサービスを追加してアプリケーションを設定できます。

## Adobe Target Cloud Service {#adobe-target-cloud-service}

AEM Mobileダッシュボードで「Cloud Serviceを管理」を探し、「+」ボタンをクリックします。

![chlimage_1-8](assets/chlimage_1-8.png)

Cloud Serviceの追加ウィザードで、「Adobe Target」クラウドサービスカードを選択し、「次へ」をクリックします。

![chlimage_1-9](assets/chlimage_1-9.png)

「 Select a Configuration 」ドロップダウンで、設定を作成するか、既存の設定から選択できます。 設定を作成するには、ドロップダウンから「設定を作成」を選択します。 Target 設定のタイトルを入力します。 Target アカウントに関連付けられているクライアントコード、電子メール、およびパスワードを入力します。 これらのフィールドの値が不明な場合は、Adobe Targetサポートにお問い合わせください。 「検証」ボタンをクリックして、認証情報を検証します。 検証が完了したら、「送信」ボタンをクリックしてクラウドサービスを作成します。

作成されたクラウドサービスは、ウィザードによってモバイルアプリケーションに自動的に関連付けられます。 cq:cloudserviceconfigs プロパティ値は、 apps group ノードの jcr:content ノードに対して設定されます。 ハイブリッドアプリのサンプルでは、自動生成されたフレームワークノードを指す値が/etc/cloudservices/testandtarget/adobe-target—aem-apps/framework にある/content/mobileapps/hybrid-reference-app/jcr:content に設定されます。 フレームワークノードには、デフォルトで設定される性別と年齢の 2 つのプロパティがあります。 フレームワークはAEMのプレビューでのみ使用され、デバイスには影響しません。

ウィザードが完了すると、Cloud Serviceを管理タイルに Target Cloud Service が表示されますが、AdobeMobile Services アカウントが見つからないことに関する警告が表示されます。

![chlimage_1-10](assets/chlimage_1-10.png)

## AdobeMobile Service {#adobe-mobile-service}

Adobeの Mobile Services(AMS) アカウントをアプリケーションにリンクする必要があります。AMS サービスは、Target のクライアントコード情報を含む必要な ADBMobileConfig.json ファイルを提供します。 AMS アカウントとの関連付けを作成する前に、AMS に対する権限を持つユーザーが AMS アカウントを変更する必要があります。

### クライアントコード {#client-code}

AMS サービスへのログインには、以下の手順に従ってください。 [https://mobilemarketing.adobe.com](https://mobilemarketing.adobe.com/)、モバイルアプリケーションを選択し、「設定」をクリックします。 「 SDK Target オプション」フィールドを探し、フィールドにクライアントコードを配置して、「保存」をクリックします。

![chlimage_1-11](assets/chlimage_1-11.png)

これで、クライアントコードがモバイルAdobeに関連付けられました。AMS クラウドサービスが Mobile Dashboard で設定されると、サービス設定の設定が ADBMobileConfig.json ファイルを介して配信されます。

### AdobeMobile Service Could Service {#adobe-mobile-service-could-service}

AMS が設定されたので、Mobile Dashboard でモバイルアプリケーションをAdobeに関連付けます。 AEM Mobileダッシュボードで「Cloud Serviceを管理」を探し、「+」ボタンをクリックします。

![chlimage_1-12](assets/chlimage_1-12.png)

「AdobeMobile Services 」カードを選択し、「次へ」をクリックします。

![chlimage_1-13](assets/chlimage_1-13.png)

作成または選択ウィザードの手順で、「 Mobile Service 」ドロップダウンを選択し、「設定を作成」エントリを選択します。 役職、会社、ユーザー名、パスワードを入力し、適切なデータセンターを選択します。 これらの値が不明な場合は、AdobeMobile Service 管理者に問い合わせて取得してください。 すべてのフィールドに入力したら、 **検証**. 検証プロセスが AMS に移動し、アカウントの資格情報が検証されます。検証が成功すると、モバイルアプリケーションのリストが表示され、ドロップダウンから関連するモバイルアプリケーションを選択します。 「送信」ボタンをクリックして、ウィザードを完了します。 このプロセスでは、設定データと、アプリケーションに関連する分析を取得するのに少し時間がかかる場合があります。 処理が完了したら、「 **完了** モーダルから「モバイルAdobe」に戻ります。

モバイルダッシュボードに戻ると、Cloud Serviceを管理タイルに AMS クラウドサービスが含まれます。 また、指標を分析タイルには、ライフサイクルレポートが表示されます。

![chlimage_1-14](assets/chlimage_1-14.png)

## Target コンテンツ同期ハンドラー {#target-content-sync-handlers}

ユーザーのデバイスにコンテンツを配信するために、AEMコンテンツ作成者が作成したオファーをレンダリングすることで、コンテンツが生成されます。 ターゲットオファーのレンダリングを処理するために、オファーを処理する新しいコンテンツ同期ハンドラーが追加されました。 Hybrid Reference Application をサンプルとして使用すると、en（英語）コンテンツパッケージには ContentSyncConfig が含まれ、 [mobileappoffers](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/aem-package/content-author/src/main/content/jcr_root/content/mobileapps/hybrid-reference-app/en/_jcr_content/pge-app/app-config-dev/targetOffers/.content.xml) ハンドラー 次の手順は、オファーをデバイスにレンダリングする際に非常に重要です。 mobileappoffers ハンドラーには、アプリケーションで使用されるパーソナライゼーションアクティビティへのパスを識別する path プロパティがあります。

例えば、 */content/campaigns/hybridref*、このパスをコピーし、値として *パス* mobileappoffers ハンドラーのプロパティ。

ハイブリッド参照アプリケーションの場合、開発用と生産用の 2 つの mobileappoffers ハンドラーがあります。

mobileappoffers ハンドラーの path プロパティにアクティビティのパスを設定したら、ハンドラーを保存します。 これで、ハンドラーは、モバイルデバイス用のオファーのレンダリングを開始する準備が整いました。

### レンダリングモード {#render-mode}

mobileappoffers ハンドラーの設定は、公開設定と開発設定で異なります。 パブリッシュ設定の場合、という名前のプロパティがあります。 *renderMode* 値を持つ *公開* cq:ContentSyncConfig ノードで設定します。 mobileappoffers ハンドラーは renderMode を参照し、publish に設定されている場合は、作成される mbox ID を編集します。 デフォルトでは、AEMで作成された mbox には、mbox ID に —author 値が追加されます。 これは、アクティビティが公開されておらず、オファーの解決に未公開のキャンペーンを使用する必要があることを示します。

コンテンツがAdobeのモバイルダッシュボードでステージングされる場合、ステージング済みコンテンツは、実稼動準備済みコンテンツと見なされ、開発用以外のコンテンツ同期設定でレンダリングされます。 この方法でレンダリングすると、—author がすべての mbox ID から削除され、公開済みのアクティビティが Target サーバーで使用できるようになります。 ステージングされたコンテンツをテストする前に、アクティビティが公開されていることを確認します。

## コンテンツの作成 {#creating-content}

これで、クラウドサービスが作成され、mobileappoffers ハンドラーが設定されたので、コンテンツ作成者はターゲットエクスペリエンスの生成を開始できます。
