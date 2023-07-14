---
title: クラウドサービス設定
description: 既存のインスタンスを拡張して、独自の設定を作成できます
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 20a19ee5-7113-4aca-934a-a42c415a8d93
source-git-commit: 260f71acd330167572d817fdf145a018b09cbc65
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 31%

---

# クラウドサービス設定{#cloud-service-configurations}

設定は、サービス設定を保存するためのロジックと構造を提供するように設計されています。

既存のインスタンスを拡張して、独自の設定を作成できます。

## 概念  {#concepts}

設定の開発に使用する原則は、次の概念に基づいています。

* サービス/アダプタは、構成を取得するために使用されます。
* 設定（例えば、プロパティ/段落）は親から継承されます。
* Analytics ノードからパスで参照されます。
* 容易に拡張可能。
* [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics) など、より複雑な設定に対応できる柔軟性がある。
* 依存関係のサポート ( 例： [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics) プラグインには [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics) 設定 )。

## 構造 {#structure}

設定のベースパスは次のとおりです。

`/etc/cloudservices`。

設定のタイプごとに、テンプレートとコンポーネントが提供されます。 これにより、カスタマイズ後にほとんどのニーズを満たす設定テンプレートを使用できます。

新しいサービスの設定を行うには、次の手順を実行します。

* サービスページをに作成する

  `/etc/cloudservices`

* この下に、

   * 設定テンプレート
   * 設定コンポーネント

テンプレートとコンポーネントは、`sling:resourceSuperType` をそれぞれ次の場所から継承する必要があります。ベーステンプレート：

`cq/cloudserviceconfigs/templates/configpage`

または基本コンポーネント

`cq/cloudserviceconfigs/components/configpage`

サービスプロバイダーは、サービスページも提供する必要があります。

`/etc/cloudservices/<service-name>`

### テンプレート {#template}

テンプレートは、基本テンプレートを拡張したものです。

`cq/cloudserviceconfigs/templates/configpage`

および `resourceType` カスタムコンポーネントを指す

```xml
/libs/cq/analytics/templates/sitecatalyst
sling:resourceSuperType = cq/cloudserviceconfigs/templates/configpage
allowedChildren = /libs/cq/analytics/templates/sitecatalyst
allowedPaths = /etc/cloudservices/analytics/*, /etc/cloudservices/analytics/.*
componentReference = cq/analytics/components/sitecatalyst
jcr:content/
cq:designPath = /etc/designs/cloudservices
sling:resourceType = cq/analytics/components/sitecatalystpage

/libs/cq/analytics/templates/generictracker
sling:resourceSuperType = cq/cloudservices/templates/configpage
allowedChildren = /libs/cq/analytics/templates/generictracker
allowedPaths = /etc/cloudservices/analytics/*, /etc/cloudservices/analytics/.*
jcr:content/
cq:designPath = /etc/designs/cloudservices
sling:resourceType = cq/analytics/components/generictrackerpage
```

### コンポーネント {#components}

コンポーネントは、次の基本コンポーネントを拡張する必要があります。

`cq/cloudserviceconfigs/templates/configpage`

```xml
/libs/cq/analytics/components/sitecatalystpage

/libs/cq/analytics/components/generictrackerpage
```

テンプレートとコンポーネントを設定した後、次の場所にサブページを追加して設定を追加できます。

`/etc/cloudservices/<service-name>`

### コンテンツモデル {#content-model}

コンテンツモデルは、次の場所の下に `cq:Page` として保存されます。

`/etc/cloudservices/<service-name>(/*)`

```xml
/etc/cloudservices
/etc/cloudservices/service-name
/etc/cloudservices/service-name/config
/etc/cloudservices/service-name/config/inherited-config
```

設定は、サブノード `jcr:content` の下に保存されます。

* ダイアログで定義される固定プロパティは、`jcr:node` に直接保存する必要があります。
* （`parsys` または `iparsys` を使用する）動的要素は、サブノードを使用してコンポーネントデータを保存します。

```xml
/etc/cloudservices/service/config/jcr:content as nt:unstructured
propertyname
*
par/component/ as cq:Component
propertyname
*
```

### API {#api}

API に関するリファレンスドキュメントについては、 [com.day.cq.wcm.webservicesupport](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/webservicesupport/package-summary.html).

### AEM の統合 {#aem-integration}

使用可能なサービスが、（`foundation/components/page` または `wcm/mobile/components/page` から継承されたいずれかのページの）**ページのプロパティ**&#x200B;ダイアログの「**クラウドサービス**」タブに一覧表示されます。

「 」タブには次の項目も表示されます。

* サービスを有効にできる場所へのリンク
* パスフィールドから設定（サービスのサブノード）を選択します

#### パスワードの暗号化 {#password-encryption}

サービスのユーザー資格情報を保存する場合は、すべてのパスワードを暗号化する必要があります。

これを行うには、非表示のフォームフィールドを追加します。 このフィールドには注釈が必要です `@Encrypted` プロパティ名につまり、 `password` フィールドの名前は次のように書き込まれます。

`password@Encrypted`

すると、`CryptoSupport` によって、プロパティが（`EncryptionPostProcessor` サービスを使用して）自動的に暗号化されます。

>[!NOTE]
>
>これは、標準の ` [SlingPostServlet](https://sling.apache.org/site/manipulating-content-the-slingpostservlet-servletspost.html)` アノテーションに似ています。

>[!NOTE]
>
>デフォルトでは、`EcryptionPostProcessor` は、`/etc/cloudservices` に対する `POST` リクエストのみを暗号化します。

#### サービスページの jcr:content ノード用の追加プロパティ {#additional-properties-for-service-page-jcr-content-nodes}

<table>
 <tbody>
  <tr>
   <td><strong>プロパティ</strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td>componentReference</td>
   <td>ページに自動的に含まれるコンポーネントへの参照パス。<br /> これは、追加機能および JS インクルージョンに使用されます。<br /> このプロパティには、<br /> <code> cq/cloudserviceconfigs/components/servicecomponents</code><br /> が（通常は <code>body</code> タグの前に）含まれるページ上のコンポーネントが含まれます。<br /> Adobe AnalyticsとAdobe Targetの場合、これを使用して、訪問者の行動を追跡する JavaScript 呼び出しなどの追加機能を含めます。</td>
  </tr>
  <tr>
   <td>description</td>
   <td>サービスの簡単な説明。<br /> </td>
  </tr>
  <tr>
   <td>descriptionExtended</td>
   <td>サービスの詳細な説明。</td>
  </tr>
  <tr>
   <td>ranking</td>
   <td>リストに使用するサービスランキング。</td>
  </tr>
  <tr>
   <td>selectableChildren</td>
   <td>設定をページのプロパティダイアログに表示するためのフィルター。</td>
  </tr>
  <tr>
   <td>serviceUrl</td>
   <td>サービス Web サイトへの URL。</td>
  </tr>
  <tr>
   <td>serviceUrlLabel</td>
   <td>サービス URL のラベル。</td>
  </tr>
  <tr>
   <td>thumbnailPath</td>
   <td>サービスのサムネールへのパス。</td>
  </tr>
  <tr>
   <td>visible</td>
   <td>ページプロパティダイアログでの表示デフォルトで表示（オプション）</td>
  </tr>
 </tbody>
</table>

### ユースケース {#use-cases}

これらのサービスは、デフォルトで提供されています。

* [トラッカースニペット](/help/sites-administering/external-providers.md) (Google、WebTrends など )
* [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics)
* [Test&amp;Target](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-target)
<!-- Search&Promote is end of life as of September 1, 2022 * [Search&Promote](/help/sites-administering/marketing-cloud.md#integrating-with-search-promote) -->
* [Dynamic Media](/help/sites-administering/marketing-cloud.md#integrating-with-scene)

>[!NOTE]
>
>[カスタムクラウドサービスの作成](/help/sites-developing/extending-cloud-config-custom-cloud.md)も参照してください。
