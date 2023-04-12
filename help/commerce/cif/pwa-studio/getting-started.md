---
title: AEM Extension for PWA Studio の概要
description: PWA Studio で、ヘッドレスの AEM Content and Commerce プロジェクトをデプロイする方法について説明します。
topics: Commerce
feature: Commerce Integration Framework
thumbnail: 37843.jpg
exl-id: de7b8f05-b6b7-4105-84a5-940c16ebf2b4
source-git-commit: e05f6cd7cf17f4420176cf76f28cb469bcee4a0a
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 68%

---

# AEM Extension for PWA Studio の概要 {#getting-started-pwa}

PWA Studio は GraphQL により初期設定で Adobe Commerce とシームレスに統合されており、革新的で魅力的なストアフロントやその他のデジタルエクスペリエンスを作成するためのオプションを無制限に提供します。

コンテンツフラグメントは、構造が事前定義されたコンテンツの要素です。この構造により、GraphQL を様々な形式（JSON や Markdown など）の API として使用しながら、ヘッドレスな方法でコンテンツを利用し、独立してレンダリングすることができます。コンテンツフラグメントには、GraphQL に必要なすべてのデータタイプとフィールドが含まれているので、アプリケーションは利用可能な情報のみをリクエストして、期待する情報だけを受け取ることができます。コンテンツフラグメントの構造は柔軟なので、複数の場所や複数のチャネルでの使用にも適しています。

Adobe Experience Manager のコンテンツフラグメントモデルエディターを使用すれば、必要な構造を簡単に設計できます。Adobe Experience Manager コンテンツフラグメント（または他の任意のデータ）を PWA Studio アプリケーションと統合するうえでの主な課題は、複数の GraphQL エンドポイントからデータを取得することです。これは、PWA Studioが単一のAdobe Commerce GraphQLエンドポイントで動作するように設定されていないからです。

## アーキテクチャ {#architecture}

![PWA ヘッドレスアーキテクチャ](/help/commerce/cif/assets/pwa-studio/PWA-Studio_Architecture.png)

## PWA Studio のセットアップ {#setup-pwa}

PWA Studioアプリを設定するには、Adobe Commerceに従います。 [PWA Studio文書](https://developer.adobe.com/commerce/pwa-studio/tutorials/).

PWA Studio を AEM の GraphQL エンドポイントに接続するには、[AEM Extension for PWA Studio](https://github.com/adobe/aem-pwa-studio-extensions) を使用します。

1. リポジトリをチェックアウトします。

1. PWA Studio アプリケーションで、この拡張機能を開発依存コンポーネントとして追加します。

   ```javascript
   yarn add --dev file:{path-to-extension}/extension
   ```

1. PWA Studio アプリケーションに Apollo Link ラッパーを追加します。pwa-root/src/index.js で、次の変更を行います。

   ```javascript
     import { linkWrapper } from '@adobe/pwa-studio-aem-cfm-blog-extension';
   
   // ...
   
   <Adapter apiBase={apiBase} apollo={{ link: linkWrapper(apolloLink) }} store={store}>
   ```

   詳細は、 [linkWrapper.js](https://github.com/adobe/aem-pwa-studio-extensions/blob/master/aem-cfm-blog-extension/extension/src/linkWrapper.js).

1. ブログエントリを使用してナビゲーションコンポーネントを拡張するには、pwa-root/local-intercept.js を次のように変更します。

   ```javascript
   const addBlogToNavigation = require('@adobe/pwa-studio-aem-cfm-blog-extension/src/addBlogToNavigation');
   
   function localIntercept(targets) {
       addBlogToNavigation(targets);
   }    
   ```

   ナビゲーションコンポーネントのカスタマイズについて詳しくは、[addBlogToNavigation.js](https://github.com/adobe/aem-pwa-studio-extensions/blob/master/aem-cfm-blog-extension/extension/src/addBlogToNavigation.js) と、PWA Studio の[拡張フレームワーク](https://developer.adobe.com/commerce/pwa-studio/guides/general-concepts/extensibility/)に関するドキュメントを参照してください。

1. Apollo クライアントは、AEM GraphQLエンドポイントを次の場所に置くことを想定しています： `<https://pwa-studio/endpoint.js>`. エンドポイントをこの場所にマッピングするには、PWA Studioアプリケーションの UPPOURD 設定をカスタマイズします。a.宛先 `pwa-root/.env`で、 AEM_CFM_GRAPHQL変数を追加し、AEMコンテンツフラグメントGraphQLエンドポイントを指すように調整します。

   例：AEM_CFM_GRAPHQL=<http://localhost:4503/content/graphql/global>

   b. UPWARD 設定にプロキシリゾルバーを追加します。UPWARD 設定は例えば次のようになります。

```json
   response:
     resolver: conditional
     when:
       - matches: request.url.pathname
         pattern: ^/endpoint.json(/|$)
         use: aemProxy
     default: veniaResponse

   aemProxy:
     resolver: proxy
     target: env.AEM_CFM_GRAPHQL
     ignoreSSLErrors: true

   status: response.status
   headers: response.headers
   body: response.body
```

## AEM のセットアップ {#setup-aem}

AEMコンテンツフラグメントのドキュメントに従って、AEMプロジェクトのGraphQLエンドポイントを設定します。 また、AEMプロジェクトに次の設定を追加して、PWA StudioアプリケーションがGraphQLエンドポイントにアクセスできるようにします。

* Adobe Granite クロスオリジンリソース共有ポリシー（com.adobe.granite.cors.impl.CORSPolicyImpl）

   を `allowedorigin` プロパティをPWA・アプリケーションの完全なホスト名に追加します。

   例：`<https://pwa-studio-test-vflyn.local.pwadev:9366>`

* Apache Sling Referrer Filter（org.apache.sling.security.impl.ReferrerFilter.cfg.json）

   allow.hosts プロパティに PWA アプリケーションのホスト名を設定します。

   例：pwa-studio-test-vflyn.local.pwadev

両方の設定の完全な例については、<https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cfm-blog-extension/aem/config/src/main/content/jcr_root/apps/blog-demo/config> を参照してください。

GraphQLエンドポイントを紹介するために、Adobeは、コンテンツパッケージを介して、いくつかのサンプルコンテンツフラグメントモデルおよびデータを準備しました。 これらのコンポーネントは、拡張機能に付属する React コンポーネントとPWA Studioします。

## 使用方法 {#how-to-use}

この拡張機能は、PWA Studio アプリケーションを AEM に接続して、GraphQL でコンテンツを取得し、レンダリングする方法の実装例と考えることができます。

ユースケースに応じて、独自のカスタムコンテンツフラグメントモデルを作成します。このモデルが、独自の React コンポーネントで利用できるカスタム GraphQL スキーマになります。

実稼動のセットアップは、様々な点で異なるものになる可能性があります。

* Apollo クライアントをカスタマイズする代わりに、AEMとAdobe Commerce GraphQLのデータを組み合わせた単一のフェデレーテッドGraphQLエンドポイントを使用できます。
* PWA Studio アプリケーションでは、UPWARD 設定のプロキシを介さずに、AEM GraphQL エンドポイント URL を直接使用することもできます。プロキシは別のレイヤー（CDN など）に移動することもできます。
* また、このアプローチは、エンドユーザーにPWA Studio・アプリケーションを提供する方法によっても大きく異なります。

この拡張機能には 2 つの例が用意されています。

### ブログ {#blog}

いくつかのコンテンツフラグメントモデルに基づいてブログ投稿を表示します。また、AEM GraphQLエンドポイントと連携するように Apollo クライアントを設定する方法や、PWA Studioでナビゲーションコンポーネントを拡張する方法の例も含まれています。 詳しくは、[GitHub](https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cfm-blog-extension) を参照してください。

### PDP エンリッチメント {#pdp-enrichment}

マーケターが、コンテンツフラグメントとして管理される追加コンテンツを使用して PDP を簡単に拡充できます。詳しくは、[GitHub](https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cif-product-page-extension) を参照してください。
