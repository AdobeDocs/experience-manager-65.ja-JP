---
title: クラウドサービスの設定
seo-title: クラウドサービスの設定
description: 既存のインスタンスを拡張して、独自の設定を作成できます
seo-description: 既存のインスタンスを拡張して、独自の設定を作成できます
uuid: 9d20c3a4-2a12-4d3c-80c3-fcac3137a675
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: d25c03bf-6eaa-45f4-ab60-298865935a62
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# クラウドサービスの設定{#cloud-service-configurations}

設定は、サービス設定を保存するためのロジックと構造を提供するようにデザインされています。

既存のインスタンスを拡張して、独自の設定を作成できます。

## 概念 {#concepts}

設定の作成に用いられる原則は、以下の概念に基づいています。

* サービスやアダプターを使用して、設定を取得する。
* 設定（プロパティや段落など）は、親から継承される。
* パスによって、分析ノードから参照される。
* 簡単に拡張できる。
* [Adobe Analyticsなど、より複雑な設定を柔軟に対応できます](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics)。
* 依存関係のサポート(例： [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics) プラグインには [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics) 設定が必要)。

## 構造 {#structure}

設定のベースパスは次のとおりです。

`/etc/cloudservices` です。

設定のタイプごとに、テンプレートとコンポーネントが提供されます。これによって、カスタマイズしてから大部分のニーズを満たせる設定テンプレートを作成できます。

新しいサービスの設定を行うには、次の操作を行う必要があります。

* ～にサービスページを作る

   `/etc/cloudservices`

* この下に次のコンポーネントを作成します。

   * 設定テンプレート
   * 設定コンポーネント

テンプレートとコンポーネントは、`sling:resourceSuperType` をそれぞれ次の場所から継承する必要があります。ベーステンプレート：

`cq/cloudserviceconfigs/templates/configpage`

ベースコンポーネント：

`cq/cloudserviceconfigs/components/configpage`

サービスプロバイダーは、サービスページも提供する必要があります。

`/etc/cloudservices/<service-name>`

### テンプレート {#template}

テンプレートは、次のベーステンプレートを拡張します。

`cq/cloudserviceconfigs/templates/configpage`

そして、カスタムコンポーネントを指す `resourceType` を定義します。

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

コンポーネントは、次のベースコンポーネントを拡張します。

`cq/cloudserviceconfigs/templates/configpage`

```xml
/libs/cq/analytics/components/sitecatalystpage

/libs/cq/analytics/components/generictrackerpage
```

テンプレートとコンポーネントを設定したら、次の場所の下にサブページを追加して、設定を追加できます。

`/etc/cloudservices/<service-name>`

### コンテンツモデル {#content-model}

The content model is stored as `cq:Page` under:

`/etc/cloudservices/<service-name>(/*)`

```xml
/etc/cloudservices
/etc/cloudservices/service-name
/etc/cloudservices/service-name/config
/etc/cloudservices/service-name/config/inherited-config
```

The configurations are stored under the subnode `jcr:content`.

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

API に関する参考ドキュメントは、[com.day.cq.wcm.webservicesupport](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/webservicesupport/package-summary.html) を参照してください。

### AEM の統合 {#aem-integration}

Available services are listed in the **Cloud Services** tab of the **Page Properties** dialog (of any page that inherits from `foundation/components/page` or `wcm/mobile/components/page`).

このタブでは以下についても表示されます。

* サービスを有効にできる場所へのリンク
* パスフィールドから設定（サービスのサブノード）を選択する

#### パスワードの暗号化 {#password-encryption}

サービスのユーザー資格情報を保存する際は、すべてのパスワードを暗号化する必要があります。

非表示のフォームフィールドを追加することによって、パスワードを暗号化できます。This field should have the annotation `@Encrypted` in the property name; i.e. for the `password` field the name would be written as:

`password@Encrypted`

すると、`CryptoSupport` によって、プロパティが（`EncryptionPostProcessor` サービスを使用して）自動的に暗号化されます。

>[!NOTE]
>
>これは、標準の ` [SlingPostServlet](https://sling.apache.org/site/manipulating-content-the-slingpostservlet-servletspost.html)` アノテーションに似ています。

>[!NOTE]
>
>By default the `EcryptionPostProcessor` only encrypts `POST` requests made to `/etc/cloudservices`.

#### サービスページの jcr:content ノード用の追加プロパティ {#additional-properties-for-service-page-jcr-content-nodes}

<table>
 <tbody>
  <tr>
   <td><strong>プロパティ</strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td>componentReference</td>
   <td>コンポーネントへの参照パスをページに自動的に含めます。<br />追加機能および JS インクルージョンに使用されます。<br /> これには、ページ上のコンポーネントが含まれ<br /> (通常 <code> cq/cloudserviceconfigs/components/servicecomponents</code><br /> はタグの前 <code>body</code> に)、<br /> AnalyticsとTargetの場合は、これを使用して、訪問者の行動を追跡するJavaScript呼び出しなどの追加機能を含めます。</td>
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
   <td>一覧表示に使用するサービスランキング。</td>
  </tr>
  <tr>
   <td>selectableChildren</td>
   <td>ページのプロパティダイアログに設定を表示するためのフィルター。</td>
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
   <td>ページのプロパティダイアログでの表示／非表示。デフォルトでは表示（オプション）。</td>
  </tr>
 </tbody>
</table>

### ユースケース {#use-cases}

デフォルトでは、以下のサービスが提供されます。

* [トラッカースニペット](/help/sites-administering/external-providers.md)（Google、WebTrends など）
* [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics)
* [Test&amp;Target](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-target)
* [Search&amp;Promote](/help/sites-administering/marketing-cloud.md#integrating-with-search-promote)
* [Scene7](/help/sites-administering/marketing-cloud.md#integrating-with-scene)

>[!NOTE]
>
>[カスタムクラウドサービスの作成](/help/sites-developing/extending-cloud-config-custom-cloud.md)も参照してください。

