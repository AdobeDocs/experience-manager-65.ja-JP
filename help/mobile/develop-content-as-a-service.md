---
title: コンテンツ配信
description: Adobe Experience Managerのすべてのコンテンツを使用してターゲットのアプリエクスペリエンスを提供する方法について説明します。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
exl-id: 85e73679-684e-402f-8186-8b56d8bd9372
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 3%

---

# コンテンツ配信{#content-delivery}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアントサイドレンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)。

モバイルアプリは、ターゲット設定されたアプリエクスペリエンスを提供するために、必要に応じてAEMのすべてのコンテンツを使用できる必要があります。

これには、アセット、サイトコンテンツ、CaaS コンテンツ（OTA）、独自の構造を持つカスタムコンテンツの使用が含まれます。

>[!NOTE]
>
>**OTC コンテンツ** は、ContentSync ハンドラーを介して上記の任意の場所から取得できます。 このパラメーターを使用すると、ZIP 形式でパッケージと配信をバッチ処理し、それらのパッケージのアップデートを管理できます。

コンテンツサービスが提供する資料には、主に次の 3 つのタイプがあります。

1. **Assets**
1. **パッケージ化されたHTMLコンテンツ（HTML/CSS/JS）**
1. **チャネルに依存しないコンテンツ**

![chlimage_1-154](assets/chlimage_1-154.png)

## アセット {#assets}

アセットコレクションは、他のコレクションへの参照を含むAEM構成です。

アセットコレクションは、コンテンツサービスを通じて公開できます。 リクエストでアセットコレクションを呼び出すと、アセットのリストであるオブジェクト（その URL も含む）が返されます。 アセットには URL 経由でアクセスできます。 URL はオブジェクトで指定されます。 次に例を示します。

* ページエンティティは、画像参照を含む JSON （ページオブジェクト）を返します。 画像参照は、画像のアセットバイナリを取得するために使用される URL です。
* フォルダー内のアセットのリストを要求すると、そのフォルダー内のすべてのエンティティの詳細を含む JSON が返されます。 そのリストはオブジェクトです。 JSON には、そのフォルダー内の各アセットのアセットバイナリを取得するために使用される URL 参照があります。

### アセットの最適化 {#asset-optimization}

コンテンツサービスの主な価値は、デバイスに最適化されたアセットを返す機能です。 これにより、ローカルデバイスストレージのニーズが軽減され、アプリのパフォーマンスが向上します。

アセットの最適化は、API リクエストで提供される情報に基づくサーバーサイド関数です。 可能な限りアセットレンディションをキャッシュして、類似のリクエストがアセットレンディションの再生成を必要としないようにします。

### アセットワークフロー {#assets-workflow}

アセットのワークフローは次のとおりです。

1. AEMですぐに使用できるアセット参照
1. モデルが指定されたアセット参照エンティティを作成
1. エンティティを編集

   1. アセットまたはアセットコレクションを選択
   1. JSON レンダリングのカスタマイズ

次の図は、 **アセット参照のワークフロー**:

![chlimage_1-155](assets/chlimage_1-155.png)

### アセットの管理 {#managing-assets}

コンテンツサービスは、他のAEM コンテンツを介して参照されないAEMで管理されるアセットへのアクセスを提供します。

#### 既存の管理アセット {#existing-managed-assets}

AEM Sitesと Assets のユーザーは、AEM Assetsを使用して、すべてのチャネルに関するデジタルマテリアルをすべて管理しています。 ネイティブモバイルアプリを開発しており、AEM Assetsが管理する複数のアセットを使用する必要があります。 例えば、ロゴ、背景画像、ボタンアイコンなどです。

現在、これらはアセットリポジトリ内に分散されています。 アプリが参照する必要があるファイルは次のとおりです。

* /content/dam/geometrixx-outdoors/brand/logo_light.png
* /content/dam/geometrixx-outdoors/brand/logo_dark.png
* /content/dam/geometrixx-outdoors/styles/backgrounds/grey_blue.jpg
* /content/dam/geometrixx-outdoors/brand/icons/app/cart.png
* /content/dam/geometrixx-outdoors/brand/icons/app/home.png

#### CS アセットエンティティへのアクセス {#accessing-cs-asset-entities}

API を使用してページを使用可能にする方法の手順を現時点で脇に置いて（AEM UI の説明で説明されています）、完了していると仮定します。 アセットエンティティが作成され、「appImages」スペースに追加されました。 組織目的で、追加のフォルダーがスペースの下に作成されました。 そのため、アセットエンティティは、次のようにAEM JCR に保存されます。

* /content/entities/appImages/logos/logo_light
* /content/entities/appImages/logos/logo_dark
* /content/entities/appImages/bkgnd/gray_blue
* /content/entities/appImages/icons/cart
* /content/entities/appImages/icons/home

#### 使用可能なアセットエンティティのリストの取得 {#getting-a-list-of-available-asset-entities}

アプリ開発者は、アセットエンティティを取得することで、使用可能なアセットのリストを取得できます。 コンテンツサービス スペースエンドポイントは、web サービス API SDK を通じてその情報を提供できます。

その結果、「icons」フォルダー内のアセットのリストを提供する JSON 形式のオブジェクトが得られます。

![chlimage_1-156](assets/chlimage_1-156.png)

#### 画像の取得 {#getting-an-image}

JSON は、コンテンツサービスによって生成された各画像の URL を画像に提供します。

「cart」画像のバイナリを取得するには、クライアントライブラリを再度使用します。

## パッケージ化されたHTMLコンテンツ {#packaged-html-content}

コンテンツのレイアウトを維持する必要があるお客様には、HTMLコンテンツが必要です。 これは、web コンテナを使用するネイティブアプリケーション（Cordova web ビューなど）でコンテンツを表示する場合に役立ちます。

AEM コンテンツサービスは、API を介して、モバイルアプリにHTMLコンテンツを提供します。 AEM コンテンツをHTMLとして公開したいお客様は、AEM コンテンツソースを指すHTMLページエンティティを作成できます。

次のオプションが考慮されます。

* **Zip ファイル：** デバイスで適切に表示する最適な機会を得るために、ページの参照されるマテリアル（css、JavaScript、アセットなど）が、応答と共に単一の圧縮ファイルに含まれます。 HTMLページの参照は、これらのファイルへの相対パスを使用するように調整できます。
* **ストリーミング：** 必要なファイルのマニフェストをAEMから取得します。 次に、そのマニフェストを使用して、後続のリクエストですべてのファイル（HTML、CSS、JS など）をリクエストします。

![chlimage_1-157](assets/chlimage_1-157.png)

## チャネルに依存しないコンテンツ {#channel-independent-content}

チャネルに依存しないコンテンツは、レイアウト、コンポーネント、その他のチャネル固有の情報を気にすることなく、ページなどのAEM コンテンツ構成を公開する方法です。

これらのコンテンツエンティティは、AEM構造を JSON 形式に変換するコンテンツモデルを使用して生成されます。 結果として得られる JSON データには、AEM リポジトリから切り離されたコンテンツデータに関する情報が含まれています。 これには、アセットへのメタデータおよびAEM参照リンクの返しや、コンテンツ構造間の関係（エンティティ階層を含む）が含まれます。

### チャネルに依存しないコンテンツの管理 {#managing-channel-independent-content}

コンテンツは、いくつかの方法でアプリに到達することができます。

1. AEM Over-the-Air を使用したGETコンテンツの ZIPS

   * コンテンツ同期ハンドラーでは、zip パッケージを直接更新することも、既存のコンテンツレンダラーを呼び出して更新することもできます

      * Platform ハンドラー
      * AEM ハンドラー
      * カスタムハンドラー

1. コンテンツレンダラーを介したGETコンテンツの直接取得

   * 標準のデフォルト Sling レンダラー
   * AEM Mobile/コンテンツサービスコンテンツレンダラー
   * カスタムレンダリング
