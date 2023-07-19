---
title: コンテンツ配信
seo-title: Content Delivery
description: コンテンツ配信
seo-description: null
uuid: 1e7bea34-ca50-41ed-8295-fa182c27fa69
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 3d65cc6b-5721-472f-a805-588d50f3571b
exl-id: 85e73679-684e-402f-8186-8b56d8bd9372
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '969'
ht-degree: 1%

---

# コンテンツ配信{#content-delivery}

>[!NOTE]
>
>Adobeは、単一ページアプリケーションのフレームワークベースのクライアントサイドレンダリング（React など）を必要とするプロジェクトでは、SPA Editor を使用することをお勧めします。 [詳細情報](/help/sites-developing/spa-overview.md)。

モバイルアプリでは、ターゲットとするアプリエクスペリエンスを配信するために、必要に応じてAEM内の任意のコンテンツやすべてのコンテンツを使用できるようにする必要があります。

これには、アセット、サイトコンテンツ、CaaS コンテンツ（オーバーザエア）コンテンツ、独自の構造を持つカスタムコンテンツの使用が含まれます。

>[!NOTE]
>
>**放送中のコンテンツ** は、ContentSync ハンドラーを使用して上記のいずれかから取得できます。 zip を介したパッケージと配信のバッチ化、アップデートやパッケージの維持に使用できます。

コンテンツサービスが提供するマテリアルには、主に次の 3 つのタイプがあります。

1. **Assets**
1. **パッケージHTMLコンテンツ (HTML/CSS/JS)**
1. **チャネルに依存しないコンテンツ**

![chlimage_1-154](assets/chlimage_1-154.png)

## アセット {#assets}

アセットコレクションは、他のコレクションへの参照を含むAEM構成です。

アセットコレクションは、コンテンツサービスを通じて公開できます。 リクエストでアセットコレクションを呼び出すと、アセットのリストであるオブジェクト（URL を含む）が返されます。 アセットには URL でアクセスします。 URL はオブジェクトで指定されます。 例：

* ページエンティティは、画像参照を含む JSON（ページオブジェクト）を返します。 画像参照は、画像のアセットバイナリを取得するために使用される URL です。
* フォルダー内のアセットのリストをリクエストすると、JSON とそのフォルダー内のすべてのエンティティに関する詳細が返されます。 そのリストはオブジェクトです。 この JSON には、そのフォルダー内の各アセットのアセットバイナリを取得するために使用される URL 参照が含まれています。

### アセットの最適化 {#asset-optimization}

Content Services の主な価値は、デバイス用に最適化されたアセットを返す機能です。 これにより、ローカルデバイスのストレージのニーズが減り、アプリのパフォーマンスが向上します。

アセットの最適化は、API リクエストで提供される情報に基づいて、サーバー側の関数になります。 可能な限り、アセットレンディションをキャッシュする必要があります。これにより、同様の要求でアセットレンディションを再生成する必要がなくなります。

### Assets ワークフロー {#assets-workflow}

アセットワークフローは次のとおりです。

1. すぐに使用できるAEMでのアセット参照
1. モデルに指定されたアセット参照エンティティを作成
1. エンティティを編集

   1. アセットまたはアセットコレクションを選択
   1. JSON レンダリングのカスタマイズ

次の図に、 **アセット参照ワークフロー**:

![chlimage_1-155](assets/chlimage_1-155.png)

### アセットの管理 {#managing-assets}

コンテンツサービスは、AEMで管理されるアセットに対し、他のAEMコンテンツを介して参照されないアクセス権を提供します。

#### 既存の管理対象アセット {#existing-managed-assets}

既存のAEM Sitesおよび Assets ユーザーは、AEM Assetsを使用してすべてのチャネルのすべてのデジタル資料を管理しています。 ネイティブモバイルアプリを開発中で、AEM Assetsが管理する複数のアセットを使用する必要があります。 例えば、ロゴ、背景画像、ボタンアイコンなどです。

現在、これらは Assets リポジトリーに分散されています。 アプリが参照する必要があるファイルは次の場所にあります。

* /content/dam/geometrixx-outdoors/brand/logo_light.png
* /content/dam/geometrixx-outdoors/brand/logo_dark.png
* /content/dam/geometrixx-outdoors/styles/backgrounds/gray_blue.jpg
* /content/dam/geometrixx-outdoors/brand/icons/app/cart.png
* /content/dam/geometrixx-outdoors/brand/icons/app/home.png

#### CS アセットエンティティへのアクセス {#accessing-cs-asset-entities}

ここでは、ページが API を通じてどのように利用可能になるか (AEM UI の説明で説明します ) の手順を取り除き、既に実行済みであるとします。 アセットエンティティが作成され、「appImages」スペースに追加されました。 組織のために、スペースの下に追加のフォルダが作成されました。 したがって、アセットエンティティはAEM JCR に次のように保存されます。

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

JSON は、コンテンツサービスによって画像に生成された各画像の URL を提供します。

「買い物かご」画像のバイナリを取得するために、クライアントライブラリが再び使用されます。

## パッケージHTMLコンテンツ {#packaged-html-content}

HTMLコンテンツは、コンテンツのレイアウトを維持する必要があるお客様に必要です。 これは、Web コンテナ（Cordova Web ビューなど）を使用してコンテンツを表示するネイティブアプリケーションで役立ちます。

AEM Content Services は、API を介してモバイルアプリにHTMLコンテンツを提供できます。 AEMコンテンツをHTMLとして公開したい場合は、AEMコンテンツソースを指すHTMLページエンティティを作成します。

次のオプションを考慮します。

* **Zip ファイル：** デバイス上で適切に表示する最良の機会を得るには、ページのすべての参照資料（CSS、JavaScript、アセットなど）を  — 応答と共に単一の圧縮ファイルに含まれます。 HTMLページ内の参照は、これらのファイルの相対パスを使用するように調整されます。
* **ストリーミング：** AEMから必要なファイルのマニフェストを取得します。 そのマニフェストを使用して、すべてのファイル (HTML、CSS、JS など ) を とその後のリクエストを含める。

![chlimage_1-157](assets/chlimage_1-157.png)

## チャネルに依存しないコンテンツ {#channel-independent-content}

チャネルに依存しないコンテンツは、レイアウト、コンポーネント、その他のチャネル固有の情報を気にすることなく、ページなどのAEMコンテンツ構成を公開する方法です。

これらのコンテンツエンティティは、コンテンツモデルを使用して生成され、AEMの構造を JSON 形式に変換します。 結果の JSON データには、AEMリポジトリから切り離された、コンテンツのデータに関する情報が含まれます。 これには、メタデータの返信、アセットへのAEM参照リンク、およびコンテンツ構造（エンティティ階層を含む）間の関係が含まれます。

### チャネルに依存しないコンテンツの管理 {#managing-channel-independent-content}

コンテンツは、いくつかの方法でアプリにアクセスできます。

1. GETコンテンツ ZIP(AEM Over-the-Air 経由 )

   * コンテンツ同期ハンドラーは、zip パッケージを直接更新するか、既存のコンテンツレンダラーを呼び出すことで更新できます

      * プラットフォームハンドラー
      * AEM ハンドラー
      * カスタムハンドラー

1. GETレンダラーを介した直接のデータコンテンツ

   * デフォルトの Sling レンダラー（標準搭載）
   * AEM Mobile/Content Services コンテンツレンダラー
   * カスタムレンダリング
