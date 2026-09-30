---
title: クラウドサービス設定
description: 既存のインスタンスを拡張して、独自の設定を作成できます
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 20a19ee5-7113-4aca-934a-a42c415a8d93
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 9f5812d7b252bcf39896b4fbf2e3ac5c24bdb808
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 85%
---
# クラウドサービス設定{#cloud-service-configurations}

設定は、サービス設定を保存するためのロジックと構造を提供するようにデザインされています。

既存のインスタンスを拡張して、独自の設定を作成できます。

## 概念 {#concepts}

設定の作成に用いられる原則は、以下の概念に基づいています。

* サービスやアダプターを使用して、設定を取得する。
* 設定（プロパティや段落など）は、親から継承される。
* パスによって、分析ノードから参照される。
* 簡単に拡張できる。
* [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics) など、より複雑な設定に対応できる柔軟性がある。
* 依存関係のサポート（例：[Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics) プラグインには [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics) 設定）。

## 構造 {#structure}

設定のベースパスは次のとおりです。

`/etc/cloudservices`

設定のタイプごとに、テンプレートとコンポーネントが提供されます。 これによって、カスタマイズしてから大部分のニーズを満たせる設定テンプレートを作成できます。

新しいサービス用の設定を行うには、以下の操作を実行します。

* 次の場所にサービスページを作成します。

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

API に関する参考ドキュメントは、[com.day.cq.wcm.webservicesupport](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/javadoc/com/day/cq/wcm/webservicesupport/package-summary.html) を参照してください。

### AEM の統合 {#aem-integration}

使用可能なサービスが、（`foundation/components/page` または `wcm/mobile/components/page` から継承されたいずれかのページの）**ページのプロパティ**&#x200B;ダイアログの「**クラウドサービス**」タブに一覧表示されます。

このタブでは以下についても表示されます。

* サービスを有効にできる場所へのリンク
* パスフィールドから設定（サービスのサブノード）を選択する

#### パスワードの暗号化 {#password-encryption}

サービスのユーザー資格情報を保存する際は、すべてのパスワードを暗号化する必要があります。

非表示のフォームフィールドを追加することによって、パスワードを暗号化できます。 このフィールドでは、プロパティ名にアノテーション `@Encrypted` が必要です。すなわち、`password` フィールドの場合、名前は次のようになります。

`password@Encrypted`

すると、`CryptoSupport` によって、プロパティが（`EncryptionPostProcessor` サービスを使用して）自動的に暗号化されます。

>[!NOTE]
>
>これは、標準の ` [SlingPostServlet](https://sling.apache.org/site/manipulating-content-the-slingpostservlet-servletspost.html)` アノテーションに似ています。

>[!NOTE]
>
>デフォルトでは、`EcryptionPostProcessor` は、`/etc/cloudservices` に対する `POST` リクエストのみを暗号化します。

#### サービスページ jcr:content ノードの追加プロパティ {#additional-properties-for-service-page-jcr-content-nodes}

<table>
 <tbody>
  <tr>
   <td><strong>プロパティ</strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td>componentReference</td>
   <td>ページに自動的に含めるコンポーネントへの参照パス。<br /> これは、追加機能とJSのインクルージョンに使用されます。<br /> これには、<br /> <code> cq/cloudserviceconfigs/components/servicecomponents</code><br />が含まれるページ上のコンポーネントが含まれます（通常は<code>body</code> タグの前）。<br /> Adobe AnalyticsとAdobe Targetの場合は、これを使用して、JavaScript呼び出しなどの追加機能を追加して訪問者の動作を追跡します。</td>
  </tr>
  <tr>
   <td>説明</td>
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
   <td>サービス web サイトへの URL。</td>
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
<!-- Search&Promote is end of life as of September 1, 2022 * [Search&Promote](/help/sites-administering/marketing-cloud.md#integrating-with-search-promote) -->
* [Dynamic Media](/help/sites-administering/marketing-cloud.md#integrating-with-scene)

>[!NOTE]
>
>[カスタムクラウドサービスの作成](/help/sites-developing/extending-cloud-config-custom-cloud.md)も参照してください。
