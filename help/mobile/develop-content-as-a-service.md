---
title: コンテンツ配信
seo-title: コンテンツ配信
description: コンテンツ配信
seo-description: 'null'
uuid: 1e7bea34-ca50-41ed-8295-fa182c27fa69
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 3d65cc6b-5721-472f-a805-588d50f3571b
exl-id: 85e73679-684e-402f-8186-8b56d8bd9372
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 61%

---

# コンテンツ配信{#content-delivery}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアント側レンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)

モバイルアプリは、目的とするアプリエクスペリエンスを配信するために、AEM 内のあらゆるコンテンツを必要に応じて利用できなければなりません。

これには例えば、アセット、サイトコンテンツ、CaaS コンテンツ、無線（OTA）コンテンツ、独自の構造を持つカスタムコンテンツなどが含まれます。

>[!NOTE]
>
>**Over-the-Air Contentは、ContentSyncハ** ンドラーを使用して、上記のいずれかから取得できます。無線コンテンツを使用すると、パッケージと配信を Zip して一括で処理したり、アップデートやパッケージを保守したりできます。

コンテンツサービスは、主に 3 種類の要素を配信します。

1. **Assets**
1. **パッケージド HTML コンテンツ（HTML／CSS／JS）**
1. **チャネル独立コンテンツ**

![chlimage_1-154](assets/chlimage_1-154.png)

## Assets {#assets}

アセットコレクションは、他のコレクションの参照を含む AEM 構成要素です。

アセットコレクションは、コンテンツサービスを介して公開できます。リクエストでアセットコレクションを呼び出すと、アセットのリストであるオブジェクト（アセットのURLを含む）が返されます。 アセットは URL を介してアクセスされ、その URL はオブジェクトの形で提供されます。以下に例を示します。

* ページエンティティは、画像参照を含む JSON（ページオブジェクト）を返します。画像参照は、画像のアセットバイナリの取得に使用されるURLです。
* フォルダー内のアセットのリストをリクエストすると、JSON と、そのフォルダー内のすべてのエンティティに関する詳細が返されます。そのリストはオブジェクトです。 この JSON は、そのフォルダー内の各アセットのアセットバイナリを取得するために使用する URL 参照を含みます。

### アセットの最適化 {#asset-optimization}

コンテンツサービスは、デバイス用に最適化されたアセットを返します。これは、コンテンツサービスの重要な機能です。これにより、ローカルデバイスのストレージニーズが軽減され、アプリのパフォーマンスが向上します。

アセットの最適化は、API リクエストで提供される情報に基づく、サーバー側の機能です。可能な限り、同様の要求でアセットレンディションを再生成する必要がないように、アセットレンディションをキャッシュする必要があります。

### アセットのワークフロー {#assets-workflow}

次に、アセットのワークフローを示します。

1. 既製の AEM で使用可能なアセット参照
1. モデルを選択してアセット参照エンティティを作成
1. エンティティを編集

   1. アセットまたはアセットコレクションの選択
   1. JSON レンダリングをカスタマイズ

次の図に、**アセット参照ワークフロー**&#x200B;を示します。

![chlimage_1-155](assets/chlimage_1-155.png)

### アセットの管理 {#managing-assets}

コンテンツサービスは、他の AEM コンテンツを介して参照できない、AEM の管理対象アセットへのアクセスを提供します。

#### 既存の管理対象アセット  {#existing-managed-assets}

既存の AEM Sites および Assets ユーザーは、AEM Assets を使用して、すべてのチャネルのすべてのデジタル要素を管理しています。ネイティブモバイルアプリを開発中で、AEM Assetsが管理する複数のアセットを使用する必要があります。 例えば、ロゴ、背景画像、ボタンアイコンなど。

現在、これらのアセットは、アセットリポジトリ全体にわたって保存されています。アプリが参照する必要があるファイルは次の場所にあります。

* /content/dam/geometrixx-outdoors/brand/logo_light.png
* /content/dam/geometrixx-outdoors/brand/logo_dark.png
* /content/dam/geometrixx-outdoors/styles/backgrounds/grey_blue.jpg
* /content/dam/geometrixx-outdoors/brand/icons/app/cart.png
* /content/dam/geometrixx-outdoors/brand/icons/app/home.png

#### CS アセットエンティティへのアクセス  {#accessing-cs-asset-entities}

ここでは、ページは既に使用可能になっているものとします。API を利用してページを使用可能にする手順については触れません（この手順については、AEM UI に関する説明で触れます）。アセットエンティティが作成され、「appImages」スペースに追加されました。 スペースの下に、組織のための追加のフォルダーが作成されました。 したがって、アセットエンティティは次のようにAEM JCRに保存されます。

* /content/entities/appImages/logos/logo_light
* /content/entities/appImages/logos/logo_dark
* /content/entities/appImages/bkgnd/grey_blue
* /content/entities/appImages/icons/cart
* /content/entities/appImages/icons/home

#### 使用可能なアセットエンティティのリストの取得  {#getting-a-list-of-available-asset-entities}

アプリ開発者は、アセットエンティティを取得することで、使用可能なアセットのリストを取得できます。Content Servicesのスペースエンドポイントは、WebサービスAPI SDKを通じてこの情報を提供できます。

結果として取得できるリストは、「icons」フォルダー内のアセットのリストを提供する JSON 形式のオブジェクトです。

![chlimage_1-156](assets/chlimage_1-156.png)

#### 画像の取得 {#getting-an-image}

JSON は、コンテンツサービスによって生成される各画像に URL を提供します。

「cart」画像のバイナリを取得するために、クライアントライブラリは再度使用されます。

## パッケージド HTML コンテンツ {#packaged-html-content}

コンテンツのレイアウトを維持するには、HTML コンテンツが必要です。これは、Webコンテナ（Cordova Webビューなど）を使用してコンテンツを表示するネイティブアプリケーションで役立ちます。

AEM コンテンツサービスは、API を介してモバイルアプリに HTML コンテンツを提供できます。AEMコンテンツをHTMLとして公開する場合、AEMコンテンツソースを指すHTMLページエンティティが作成されます。

次のオプションを検討します。

* **Zipファイル：** デバイス上で適切に表示する最良の機会を得るために、ページのすべての参照資料（CSS、JavaScript、アセットなど）を — は、応答と共に単一の圧縮ファイルに含まれます。 HTMLページ内の参照は、これらのファイルの相対パスを使用するように調整されます。
* **ストリーミング：** 必要なファイルのマニフェストをAEMから取得します。次に、これ以降のリクエストでは、このマニフェストを使用してすべてのファイル（HTML、CSS、JS など）をリクエストします。

![chlimage_1-157](assets/chlimage_1-157.png)

## チャネル独立コンテンツ {#channel-independent-content}

チャネルに依存しないコンテンツは、レイアウト、コンポーネント、その他のチャネル固有の情報を気にせずに、ページなどのAEMコンテンツ構成を公開する方法です。

これらのコンテンツエンティティは、コンテンツモデルを使用して AEM 構成要素を JSON 形式に変換することで生成されます。結果のJSONデータには、コンテンツのデータに関する情報(AEMリポジトリから切り離されている)が含まれます。 これには、メタデータの返信、アセットへのAEM参照リンク、およびコンテンツ構造間の関係（エンティティ階層を含む）が含まれます。

### チャネル独立コンテンツの管理 {#managing-channel-independent-content}

コンテンツは、いくつかの方法でアプリにアクセスできます。

1. AEM 無線を介してコンテンツの ZIP を取得します。

   * コンテンツ同期ハンドラーは、zipパッケージを直接更新するか、既存のコンテンツレンダラーを呼び出すことで更新できます

      * プラットフォームハンドラー
      * AEMM ハンドラー
      * カスタムハンドラー

1. コンテンツレンダラーを介してコンテンツを直接取得します。

   * 既製のデフォルト Sling レンダラー
   * AEM Mobile／コンテンツサービスのコンテンツレンダラー
   * カスタムレンダー
