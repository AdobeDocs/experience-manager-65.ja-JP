---
title: Adobe Experience Manager Mobile コンテンツのパーソナライゼーション
description: ここでは、AEM作成者がAdobe Targetを使用してモバイルアプリコンテンツをパーソナライズできる、Adobeエクスペリエンス管理（AEM）のモバイルコンテンツパーソナライゼーション機能について説明します。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: 70d7ee0d-2f6d-4f97-a6e2-b02d84a0ca42
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '2571'
ht-degree: 2%

---

# AEM Mobile のコンテンツパーソナライゼーション{#aem-mobile-content-personalization}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアントサイドレンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)。

>[!NOTE]
>
>このドキュメントは、 [AEM Mobileの概要](/help/mobile/getting-started-aem-mobile.md) ガイド :AEM Mobileのリファレンスの推奨される出発点です。

AEM Mobileのコンテンツパーソナライゼーション機能では、 [AEM オーサー](#author) 次を使用してモバイルアプリのコンテンツをパーソナライズするには： [Adobe Target](https://business.adobe.com/products/target/adobe-target.html?lang=ja). これにより、モバイルアプリケーションユーザーにターゲット設定されたオファーを配信できます。 Adobe Experience Manager Mobileには、ユーザーの好みに合ったコンテンツを作成、ターゲット設定および配信する機能があります。

AEMでは、作成者がこのコンテンツの作成を開始するには、まず管理者と開発者が環境を準備する必要があります。

[AEM管理者](#administrator) AEM MobileとAdobe Target Cloud Service間の接続を確立するために必要です。

一方、AEM Mobileは [開発者](#developer) ターゲット設定されたコンテンツのオーサリングを容易にするために、既存のスクリプトを編集する必要があります。

## 管理者向け {#for-administrators}

コンテンツ作成者がモバイルアプリ用のターゲットコンテンツの生成を開始するには、いくつかの手順を実行する必要があります。ユーザーとグループに適切な権限セットを取得し、クラウドサービスを作成し、アクティビティ用のアプリケーションを設定して、最後にコンテンツを生成します。

この記事では、を設定するためのプロセスについて説明します [AEM Mobile ハイブリッド参照アプリケーション](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) （ターゲティング用）。

今後、AEM Mobile ハイブリッド参照アプリケーションが正常にデプロイされ、AEM Mobile Dashboard を介してアクセスできるようになることを想定しています。

作成者がアプリケーション内でターゲットコンテンツを生成する前に、AEM インスタンスは次の状態にする必要があります [Adobe Target Cloud Serviceで設定されます。](/help/mobile/aem-mobile-configuring-cloud-service.md)

### 権限 {#permissions}

パーソナライゼーションコンソールへのアクセスを必要とするユーザーは、 `target-activity-authors` グループ。

ユーザーとグループの設定の一環として、target-activity-group を apps-admins グループに追加することをお勧めします。 target-activity-authors グループを追加することで、ユーザーはパーソナライゼーションナビゲーションメニューのエントリを表示できます。

>[!NOTE]
>
>パーソナライゼーションAdmin Consoleへのアクセス権を付与するユーザーまたはグループを target-activity-authors グループに追加し忘れると、パーソナライゼーションコンソールが表示されなくなります。

### Cloud Services {#cloud-services}

モバイルアプリケーションでターゲットコンテンツを動作させるには、Adobe Target サービスとAdobe Mobile Services サービスの 2 つのサービスを設定する必要があります。 Adobe Target サービスは、クライアントリクエストを処理し、パーソナライズされたコンテンツを返すためのエンジンを提供します。 AdobeMobile Services サービスは、AMS Cordova プラグインが使用する ADBMobileConfig.json ファイルを介して、Adobe サービスとモバイルアプリケーション間の接続を提供します。 AEM Mobileのダッシュボードから、2 つのサービスを追加してアプリケーションを設定できます。

AEM Mobile ダッシュボードで、管理Cloud Serviceを見つけて、「+」ボタンをクリックします。

![chlimage_1-38](assets/chlimage_1-38.png)

Cloud Serviceを追加ウィザードで、「Adobe Target」クラウドサービスカードを選択し、「次へ」をクリックします。

![chlimage_1-39](assets/chlimage_1-39.png)

設定を選択ドロップダウンから、設定を作成するか、既存の設定から選択できます。 設定を作成するには、ドロップダウンから「設定を作成」を選択します。 Target 設定のタイトルを入力します。 Target アカウントに関連付けられているクライアントコード、メールおよびパスワードを入力します。 これらのフィールドの値が不明な場合は、Adobe Target サポートにお問い合わせください。 「検証」ボタンをクリックして、資格情報を検証します。 確認が完了したら、「送信」ボタンをクリックして、クラウドサービスを作成します。

>[!NOTE]
>
>作成されるクラウドサービスは、ウィザードを使用してモバイルアプリケーションに自動的に関連付けられます。 cq:cloudserviceconfig プロパティ値は、apps グループノードの jcr:content ノードに設定されます。 ハイブリッドアプリサンプルの場合、これは/content/mobileapps/hybrid-reference-app/jcr:content に設定され、値は/etc/cloudservices/testandtarget/adobe-target—aem-apps/framework にある自動生成されたフレームワークノードを指します。 フレームワークノードには、デフォルトで性別と年齢の 2 つのプロパティが設定されています。 このフレームワークは、AEMのプレビューでのみ使用され、デバイスには影響しません。

ウィザードが完了すると、Cloud Serviceを管理タイルに Target Cloud Service が表示されます。 ただし、これには、Adobeの Mobile Service アカウントが見つからないことに関する警告が含まれています。

![chlimage_1-40](assets/chlimage_1-40.png)

### Adobe Mobile Services {#adobe-mobile-services}

アプリケーションにもAdobe Mobile Services （AMS）アカウントをリンクする必要があります。AMS サービスは、Target クライアントコード情報を含む必須の ADBMobileConfig.json ファイルを提供します。 AMS アカウントとの関連付けを作成する前に、AMS への権限を持つユーザーが AMS アカウントを変更する必要があります。

### クライアントコード {#client-code}

AMS サービスにログインするには、次を参照してください [https://mobilemarketing.adobe.com](https://mobilemarketing.adobe.com/)をクリックし、モバイルアプリケーションを選択して、設定をクリックします。 「SDK ターゲットオプション」フィールドを見つけ、フィールドにクライアントコードを配置して、「保存」をクリックします。

![chlimage_1-41](assets/chlimage_1-41.png)

これで、クライアントコードがモバイルアプリケーションに関連付けられたので、AMS クラウドサービスがAdobeモバイルダッシュボードを使用して設定された場合、サービス設定の設定は ADBMobileConfig.json ファイルを使用して配信されます。

### Adobe Mobile Service Cloud Service {#adobe-mobile-service-cloud-service}

これで AMS が設定されたので、モバイルアプリケーションをAdobeモバイルダッシュボードに関連付けます。 AEM Mobile ダッシュボードで、管理Cloud Serviceを見つけて、「+」ボタンをクリックします。

![chlimage_1-42](assets/chlimage_1-42.png)

Adobe Mobile Services カードを選択し、「次へ」をクリックします。

![chlimage_1-43](assets/chlimage_1-43.png)

ウィザードを作成または選択の手順で、Mobile Service ドロップダウンを選択し、設定を作成エントリを選択します。 タイトル、会社名、ユーザー名、パスワードを入力し、適切なデータセンターを選択します。 これらの値がわからない場合は、Adobeの Mobile Service 管理者に問い合わせて値を取得してください。 すべてのフィールドに値を入力したら、 **検証**. 検証プロセスは AMS に移動し、アカウントの資格情報を検証します。検証が成功すると、モバイルアプリケーションのリストが入力され、関連するモバイルアプリケーションをドロップダウンから選択します。 クリック **Submit** ウィザードを完了します。 設定データおよびアプリケーションに関連する分析の取得には、プロセスに少し時間がかかる場合があります。 処理が完了したら、 **完了** をクリックして、Adobeモバイルダッシュボードに戻ります。

モバイルダッシュボードに戻ると、Cloud Serviceを管理タイルに AMS Cloud Service が含まれています。 また、分析指標タイルには、ライフサイクルレポートも表示されます。

![chlimage_1-44](assets/chlimage_1-44.png)

## 作成者の場合 {#for-authors}

**前提条件：** 前述のように、作成者が新しいターゲットコンテンツを生成するには、管理者がAdobe Target サービスへの接続を設定する必要があります。

管理者が 2 つのクラウドサービスを設定し、開発者が mobileappoffers ハンドラーを設定したら、コンテンツ作成者は、ターゲット設定されたエクスペリエンスの生成を開始できるようになります。

AEM Mobile アプリ内のターゲットコンテンツのオーサリングは、AEM Sitesのオーサリングと同様の手順に従います。

の概要については、こちらを参照してください [AEMでのターゲットコンテンツのオーサリング](/help/sites-authoring/personalization.md)

## 開発者向け {#for-developers}

モバイルアプリケーションを構築するAEM開発者は、コンポーネントを開発する際にAEM全体で一般的に使用されるパターンに引き続き従う必要があります。 ここでは、Adobeがコンテンツ作成者がターゲット設定されたコンテンツを作成するために必要な手順を説明します。

### Adobe Target コンテンツ同期ハンドラー {#adobe-target-contentsync-handlers}

ユーザーのデバイスにコンテンツを配信するために、AEM コンテンツ作成者によって作成されたオファーをレンダリングしてコンテンツを生成します。 ターゲットオファーのレンダリングを処理するために、オファーを処理する新しいコンテンツ同期ハンドラーが追加されました。 ハイブリッド参照アプリケーションをサンプルとして使用する場合、en （英語）コンテンツパッケージには、ContentSyncConfig とが含まれています [mobileapffers](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/aem-package/content-author/src/main/content/jcr_root/content/mobileapps/hybrid-reference-app/en/_jcr_content/pge-app/app-config-dev/targetOffers/.content.xml) ハンドラー。 次のステップは、デバイスへのオファーをレンダリングする場合に重要です。 mobileappoffers ハンドラーには、アプリケーションに使用されるパーソナライゼーションアクティビティへのパスを識別するパスプロパティがあります。

例えば、にアクティビティがあるとします */content/campaigns/hybridref*、このパスをコピーし、値としてに貼り付けます。 *パス* mobileappoffers ハンドラーのプロパティ。

>[!NOTE]
>
>ハイブリッド参照アプリケーションには、開発用と実稼動用の 2 つの mobileappoffers ハンドラーがあります。

mobileappoffers ハンドラーの path プロパティにアクティビティパスが設定されたら、ハンドラーを保存します。 これで、ハンドラーは、モバイルデバイス向けのオファーのレンダリングを開始する準備が整いました。

### レンダリングモード {#render-mode}

mobileappoffers ハンドラーの設定は、公開の設定と開発の設定で異なります。 パブリッシュの設定には、というプロパティがあります。 *renderMode* 値： *publish* cq:ContentSyncConfig ノードでを設定します。 mobileappoffers ハンドラーは renderMode を参照し、「公開」に設定されている場合は、作成された mbox id を編集します。 AEMで作成される mbox には、デフォルトで、mbox id に – author 値が付加されます。 これは、アクティビティが公開されていないことを示すステータスで、オファーの解決に未公開のキャンペーンを使用する必要があります。

Adobeモバイルダッシュボードを使用してコンテンツをステージングすると、ステージングされたコンテンツは実稼動用コンテンツと見なされ、開発以外のコンテンツ同期設定を使用してレンダリングされます。 この方法でレンダリングすると、—author がすべての mbox ID から削除され、公開済みアクティビティが Target サーバーで使用できるようになります。 ステージングされたコンテンツをテストする前に、アクティビティが既に公開されていることを確認します。

### パーソナライゼーションアプリの開発 {#personalization-app-development}

#### コンポーネント {#components}

コンテンツの基盤は、通常、HTL または JSP を使用しているかどうかに応じて、基本AEM ページコンポーネント wcm/foundation/components/page または foundation/components/page のいずれかを拡張するページコンポーネントです。 これらの手順の期間は、wcm/foundation/components/page コンポーネントの使用に焦点を当てています。 ページコンポーネントの基本構造は複数のスクリプトに分割されています。各スクリプトは、必要に応じてデベロッパーがコードを整理および上書きできるようにするための特別な目的を提供します。 パーソナライゼーションで関心のある 2 つのスクリプトは head.html と body.html です。 これらの 2 つのスクリプトは、Context Hub、Cloud Service、モバイルオーサリングをサポートするためにコードを挿入できる領域を提供します。

コンテンツターゲティングを有効にするために使用する 2 つの主なスクリプトの概要を次に示します。

#### head.html {#head-html}

作成者がコンテンツをターゲット設定できるようにするには、ターゲットメニューをページに追加して、作成者がコンテキストを編集モードからターゲティングモードに変更できるようにする必要があります。 この機能を有効にするには、開発者は head.html スクリプトを変更して、head.html の上部付近またはに近い次のコードのスニペットを含める必要があります &lt;title>&lt;/title> 可能な限り要素。

```xml
<meta data-sly-test="${!wcmmode.disabled}">
    <div data-sly-call="${clientLib.all @ categories='personalization.kernel'}" data-sly-unwrap></div>
    <div data-sly-resource="${'config' @ resourceType='cq/personalization/components/clientcontext_optimized/config'}" data-sly-unwrap></div>
    <div data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}" data-sly-unwrap></div>
</meta>
```

>[!NOTE]
>
>WCM モードが無効な場合にスクリプトを含めるだけで、WCM モードが無効な場合（詳しくはコンテンツ同期ハンドラーのセクションを参照）、スクリプトが最終的なアプリケーションコードに含まれません。

作成者がターゲットのコンテンツをプレビューできるようにするには、編集者がAdobe Target Cloud Service の設定を見つけられるようにする必要があります。 以下のコードブロックは、2 つの重要なスクリプトを追加します。 1 つ目は、ページが関連する Target Cloud Service を見つけて、Adobe Targetを呼び出す機能を追加する方法です。 2 つ目は cq.apps.targeting カテゴリの追加です。

この **cq.apps.targeting** カテゴリは、デフォルトの cq/personalization/component/target コンポーネントを上書きし、モバイルアプリケーションでの使用のために特別にオファーをレンダリングする mobileapps/components/target コンポーネントを使用します。 この詳細については、ターゲットコンポーネントの節で説明します。

コードは head.html に追加し、の終了直前に配置する必要があります。 &lt;/head> 要素。

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-include="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp" data-sly-unwrap></div>
    <meta data-sly-call="${clientLib.all @ categories='cq.apps.targeting'}" data-sly-unwrap></meta>
</div>
```

>[!NOTE]
>
>コードブロックは、無効になっていない WCM モードにラップされているので、コンテンツ作成者がコンテンツの作成に取り組んでいる間にのみ再生されます。 生成されたモバイルランタイムコードには、クラウドサービススクリプトは追加されません。

#### body.html {#body-html}

コンテンツ作成者が様々なペルソナをテストできるようにするには、body.html スクリプトに body 要素の最初の子として次のコードブロックを含める必要があります。

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-resource="${'clientcontext' @ resourceType='cq/personalization/components/clientcontext_optimized'}" data-sly-unwrap></div>
</div>
```

必要なコードの最後のビットは、body.html の末尾にあります。 このビットのコードは、関連するクラウドサービスを検索し、適切なターゲティングエンジンコードを挿入します。

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-resource="${'cloudservices' @ resourceType='cq/cloudserviceconfigs/components/servicecomponents'}" data-sly-unwrap></div>
</div>
```

### 参照アプリケーション {#reference-application}

head.html と body.html の例は、次にあります。 [AEM Mobile ハイブリッド参照アプリケーション](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) 2 つのスクリプト内でスクリプト ブロックを配置する場所を開発者に示します。

### コンテンツ同期ハンドラー {#content-sync-handlers}

コンテンツ作成者がモバイルアプリケーションのコンテンツの作成を完了したら、次の手順として、ソースをダウンロードしてアプリケーションを構築するか、公開するコンテンツをステージングします。 これを実現するために、開発者が関与する手順はいくつかあります。 コンテンツのレンダリングを支援するために、AEM Mobileではコンテンツ同期ハンドラーを使用してコンテンツをレンダリングし、パッケージ化します。 パーソナライゼーションのユースケースに、ターゲット設定されたコンテンツをレンダリングするための新しいコンテンツ同期ハンドラーが導入されました。 「mobileappoffers」ハンドラーは、コンテンツ作成者によって作成された、関連するターゲットオファーのレンダリング方法を認識しています。 mobileappoffers ハンドラーは抽象ページ更新ハンドラーを拡張するので、プロパティの多くは似ています。 mobileappoffers ハンドラーの詳細には、以下のプロパティがあります。

<table>
 <tbody>
  <tr>
   <td><strong>プロパティ</strong></td>
   <td><strong>値</strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td>書換え</td>
   <td>+ relativeParentPath<p> - 「/」</p> </td>
   <td>rewrite プロパティは、コンテンツ内のパスの書き換え方法を識別します。</td>
  </tr>
  <tr>
   <td>includedPageTypes</td>
   <td><p>"cq/personalization/components/teaserpage"、</p> <p>"cq/personalization/components/offerproxy"</p> </td>
   <td>includePageTypes プロパティはオプションです。デフォルトでは、リソースタイプが cq/personalization/components/teaserpage と cq/personalization/components/offerproxy のページに設定されます。 これら 2 つのリソースタイプは、コンテンツのターゲット設定時に使用されるデフォルトのリソースタイプです。 その他のリソースタイプをサポートする必要がある場合は、それらを includePageTypes のリストに追加します。</td>
  </tr>
  <tr>
   <td>locationRoot</td>
   <td>/content/mobileapps/&lt;app&gt;</td>
   <td>アプリの場所。</td>
  </tr>
  <tr>
   <td>タイプ</td>
   <td>mobileapffers</td>
   <td>mobileappoffers であるハンドラーの名前。</td>
  </tr>
  <tr>
   <td>セレクター</td>
   <td>タント</td>
   <td>ターゲットセレクターを使用して、ターゲットコンテンツをレンダリングします。 </td>
  </tr>
  <tr>
   <td>target ルート ディレクトリ</td>
   <td>www</td>
   <td>レンダリングされたコンテンツを保持するルートディレクトリ。</td>
  </tr>
  <tr>
   <td>includeImages</td>
   <td>true |false</td>
   <td>true の場合、オファーに含まれているすべての画像がレンダリングされます。 false の場合、画像はスキップされます。</td>
  </tr>
  <tr>
   <td>includeVideos</td>
   <td>true |false</td>
   <td>true の場合、オファーに含まれているすべてのビデオがレンダリングされます。 false の場合、ビデオはスキップされます。</td>
  </tr>
  <tr>
   <td>path</td>
   <td>/content/campaigns/&lt;brand&gt;</td>
   <td>オファーが参加しているキャンペーンのブランドを指します。 現在、すべてのオファーは同じキャンペーンから取得する必要があります。</td>
  </tr>
  <tr>
   <td>深い</td>
   <td>true |false</td>
   <td>true の場合は、すべての子ページを再帰的にレンダリングし、false の場合は再帰的にレンダリングしません。 </td>
  </tr>
  <tr>
   <td>拡張子</td>
   <td>html</td>
   <td>レンダリングするリソースの拡張子を設定します。 ページの拡張子が.html になるように html を設定します。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>この [AEM Mobile ハイブリッド参照アプリ](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) デフォルトの mobileappoffer ハンドラーの設定がある。 サンプルのパスプロパティは、キャンペーンの場所に応じるので、空です。 キャンペーン作成者がキャンペーンを作成したら、アプリ管理者は、キャンペーンを指すパスプロパティを指定して、キャンペーンをハンドラーに関連付ける必要があります。

### Target コンポーネント {#target-component}

特にモバイルアプリケーション用にコンテンツをレンダリングしやすくするために、AEM Mobileでは mobileapps/components/target コンポーネントを使用します。 モバイルターゲットコンポーネントは cq/personalization/components/target コンポーネントを拡張し、engine_tnt.jsp スクリプトをオーバーライドします。 engine_tnt.jsp を上書きすることで、AEM Mobileがモバイルアプリのユースケース用に生成されるHTMLを制御できます。 コンテンツ作成者のターゲットとなるすべてのコンポーネントに対し、関連する mbox が engine_tnt.jsp によって作成されます。

各 mbox に対して、の属性 **cq-targeting** を追加すると、アプリケーション開発者は使用するカスタムコードを記述し、好きなように使用できるようになります。 この [AEM Mobile ハイブリッド参照アプリ](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) には、cq-targeting 属性を使用するAngularディレクティブの例があります。 コンテンツ置換の概念は、いつ、どのように行うかは、モバイルアプリケーション開発者が決定します。 AEM /etc/clientlibs/mobileapps/js/mobileapps.jsを介して配信される Mobile SDK があり、Adobeターゲティングサービスを呼び出す API を提供します。 その呼び出しを行うタイミングは、アプリケーションの設計に従ってアプリケーション開発者が指定します。

## 次の手順 {#what-s-next}

1. [AEM Mobile アプリのエクスペリエンスを開始](/help/mobile/starting-aem-phonegap-app.md)
1. [アプリのコンテンツの管理](/help/mobile/phonegap-manage-app-content.md)
1. [アプリケーションの構築](/help/mobile/building-app-mobile-phonegap.md)
1. [Adobeモバイル分析を使用してアプリのパフォーマンスを追跡する](/help/mobile/phonegap-intro-to-app-analytics.md)
1. [Adobe Targetでパーソナライズされたアプリエクスペリエンスを提供する](/help/mobile/phonegap-aem-mobile-content-personalization.md)
1. [ユーザーへの重要なメッセージの送信](/help/mobile/phonegap-push-notifications.md)
