---
title: コンテンツ配信
description: Adobe Experience Managerのすべてのコンテンツを使用して、ターゲットアプリのエクスペリエンスを配信する方法について説明します。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
exl-id: 85e73679-684e-402f-8186-8b56d8bd9372
source-git-commit: 06a6d4e0ba2aeaefcfb238233dd98e8bbd6731da
workflow-type: tm+mt
source-wordcount: '978'
ht-degree: 1%

---

# コンテンツ配信{#content-delivery}

>[!NOTE]
>
>Adobeは、単一ページアプリケーションのフレームワークベースのクライアントサイドレンダリング（React など）を必要とするプロジェクトでは、SPA Editor を使用することをお勧めします。 [詳細情報](/help/sites-developing/spa-overview.md)。

モバイルアプリでは、ターゲットとするアプリエクスペリエンスを配信するために、必要に応じてAEM内のすべてのコンテンツを使用できるようにする必要があります。

これには、アセット、サイトコンテンツ、CaaS コンテンツ（オーバーザエア）コンテンツ、独自の構造を持つカスタムコンテンツの使用が含まれます。

>[!NOTE]
>
>**放送中のコンテンツ** は、ContentSync ハンドラーを使用して上記のいずれかから取得できます。 zip を使用してパッケージと配信をバッチ処理し、更新やそれらのパッケージを維持するために使用できます。

コンテンツサービスが提供するマテリアルには、主に次の 3 つのタイプがあります。

1. **Assets**
1. **パッケージHTMLコンテンツ (HTML/CSS/JS)**
1. **チャネルに依存しないコンテンツ**

![chlimage_1-154](assets/chlimage_1-154.png)

## アセット {#assets}

アセットコレクションは、他のコレクションへの参照を含むAEM構成です。

アセットコレクションは、コンテンツサービスを通じて公開できます。 リクエストでアセットコレクションを呼び出すと、アセットのリストであるオブジェクト（URL を含む）が返されます。 アセットには URL でアクセスします。 URL はオブジェクトで指定されます。 次に例を示します。

* ページエンティティは、画像参照を含む JSON（ページオブジェクト）を返します。 画像参照は、画像のアセットバイナリを取得するために使用される URL です。
* フォルダー内のアセットのリストをリクエストすると、JSON とそのフォルダー内のすべてのエンティティに関する詳細が返されます。 そのリストはオブジェクトです。 この JSON には、そのフォルダー内の各アセットのアセットバイナリを取得するために使用される URL 参照が含まれています。

### アセットの最適化 {#asset-optimization}

Content Services の主な価値は、デバイス用に最適化されたアセットを返す機能です。 これにより、ローカルデバイスのストレージのニーズが減り、アプリのパフォーマンスが向上します。

アセットの最適化は、API リクエストで提供される情報に基づくサーバー側の関数です。 可能な限り、アセットレンディションをキャッシュする必要があります。これにより、同様の要求でアセットレンディションを再生成する必要がなくなります。

### Assets ワークフロー {#assets-workflow}

アセットワークフローは次のとおりです。

1. すぐに使用できるAEMでのアセット参照
1. モデルに指定されたアセット参照エンティティの作成
1. エンティティを編集

   1. アセットまたはアセットコレクションを選択
   1. JSON レンダリングのカスタマイズ

次の図に、 **アセット参照ワークフロー**:

![chlimage_1-155](assets/chlimage_1-155.png)

### アセットの管理 {#managing-assets}

コンテンツサービスは、AEMが管理するアセットに対し、他のAEMコンテンツを介して参照できないアクセス権を提供します。

#### 既存の管理対象アセット {#existing-managed-assets}

AEM Sitesと Assets のユーザーは、AEM Assetsを使用してすべてのチャネルのすべてのデジタルマテリアルを管理しています。 ネイティブモバイルアプリを開発中で、AEM Assetsが管理する複数のアセットを使用する必要があります。 例えば、ロゴ、背景画像、ボタンアイコンなどです。

現在、これらは Assets リポジトリーに分散されています。 アプリが参照する必要があるファイルは、次の場所にあります。

* /content/dam/geometrixx-outdoors/brand/logo_light.png
* /content/dam/geometrixx-outdoors/brand/logo_dark.png
* /content/dam/geometrixx-outdoors/styles/backgrounds/gray_blue.jpg
* /content/dam/geometrixx-outdoors/brand/icons/app/cart.png
* /content/dam/geometrixx-outdoors/brand/icons/app/home.png

#### CS アセットエンティティへのアクセス {#accessing-cs-asset-entities}

ここでは、ページが API 経由で利用可能になる方法 (AEM UI の説明で説明 ) の手順を取り除き、既に実行されているとします。 アセットエンティティが作成され、「appImages」スペースに追加されました。 組織のために、スペースの下に追加のフォルダが作成されました。 したがって、アセットエンティティはAEM JCR に次のように保存されます。

* /content/entities/appImages/logos/logo_light
* /content/entities/appImages/logos/logo_dark
* /content/entities/appImages/bkgnd/gray_blue
* /content/entities/appImages/icons/cart
* /content/entities/appImages/icons/home

#### 使用可能なアセットエンティティのリストの取得 {#getting-a-list-of-available-asset-entities}

アプリ開発者は、使用可能なアセットのリストを取得できます。そのためには、アセットエンティティを取得します。 Content Services のスペースエンドポイントは、Web サービス API SDK を通じてこの情報を提供できます。

結果として、「icons」フォルダー内のアセットのリストを提供する JSON 形式のオブジェクトが生成されます。

![chlimage_1-156](assets/chlimage_1-156.png)

#### 画像の取得 {#getting-an-image}

JSON は、Content Services で生成された各画像の URL を画像に提供します。

「買い物かご」画像のバイナリを取得するために、クライアントライブラリが再び使用されます。

## パッケージ化されたHTMLコンテンツ {#packaged-html-content}

HTMLコンテンツは、コンテンツのレイアウトを維持する必要があるお客様に必要です。 これは、Web コンテナ（Cordova Web ビューなど）を使用してコンテンツを表示するネイティブアプリケーションで役立ちます。

AEM Content Services は、API を介してモバイルアプリにHTMLコンテンツを提供します。 AEMコンテンツをHTMLとして公開したい場合は、AEMコンテンツソースを指すHTMLページエンティティを作成できます。

次のオプションを考慮します。

* **Zip ファイル：** デバイス上で適切に表示できる最良の機会を得るには、ページで参照されている material-css、JavaScript、アセットなどを、応答と共に単一の圧縮ファイルに含めます。 HTMLページ内の参照を調整して、これらのファイルの相対パスを使用できます。
* **ストリーミング：** AEMから必要なファイルのマニフェストを取得します。 その後、そのマニフェストを使用して、後続のリクエストですべてのファイル (HTML、CSS、JS など ) をリクエストします。

![chlimage_1-157](assets/chlimage_1-157.png)

## チャネルに依存しないコンテンツ {#channel-independent-content}

チャネルに依存しないコンテンツは、レイアウトやコンポーネントなどのチャネル固有の情報を気にすることなく、ページなどのAEMコンテンツ構成を公開する方法です。

これらのコンテンツエンティティは、コンテンツモデルを使用して生成され、AEMの構造を JSON 形式に変換します。 結果の JSON データには、AEMリポジトリから切り離されたコンテンツのデータに関する情報が含まれます。 これには、メタデータの返信やアセットへのAEM参照リンク、およびコンテンツ構造間の関係（エンティティ階層を含む）が含まれます。

### チャネルに依存しないコンテンツの管理 {#managing-channel-independent-content}

コンテンツは、いくつかの方法でアプリにアクセスできます。

1. AEM Over-the-Air を介したGETコンテンツ ZIP

   * コンテンツ同期ハンドラーは、zip パッケージを直接更新するか、既存のコンテンツレンダラーを呼び出すことで更新できます

      * プラットフォームハンドラー
      * AEMハンドラー
      * カスタムハンドラー

1. GETレンダラーを介して直接コンテンツを作成する

   * デフォルトの Sling レンダラー（標準搭載）
   * AEM Mobile/Content Services コンテンツレンダラー
   * カスタムレンダリング
