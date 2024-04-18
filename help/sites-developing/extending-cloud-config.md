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
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 31%

---

# クラウドサービス設定{#cloud-service-configurations}

設定は、サービス設定を保存するためのロジックと構造を提供するように設計されています。

既存のインスタンスを拡張して、独自の設定を作成できます。

## 概念  {#concepts}

設定の開発に使用される原則は、次の概念に基づいています。

* サービス/アダプタは、構成を取得するために使用されます。
* 設定（プロパティや段落など）は、親から継承されます。
* Analytics ノードからパス別に参照されます。
* 容易に拡張可能。
* [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics) など、より複雑な設定に対応できる柔軟性がある。
* 依存関係のサポート（例： [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics) プラグインには、 [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics) 設定）。

## 構造 {#structure}

設定のベースパスは次のとおりです。

`/etc/cloudservices`。

設定のタイプごとに、テンプレートとコンポーネントが用意されています。 これにより、カスタマイズした後に大部分のニーズを満たすことができる設定テンプレートを使用できます。

新しいサービスの設定を指定するには、次の手順を実行します。

* にサービスページを作成します。

  `/etc/cloudservices`

* この下で：

   * 設定テンプレート
   * 設定コンポーネント

テンプレートとコンポーネントは、`sling:resourceSuperType` をそれぞれ次の場所から継承する必要があります。ベーステンプレート：

`cq/cloudserviceconfigs/templates/configpage`

ベースコンポーネント：

`cq/cloudserviceconfigs/components/configpage`

サービスプロバイダーは、サービスページも提供する必要があります。

`/etc/cloudservices/<service-name>`

### テンプレート {#template}

テンプレートによって基本テンプレートが拡張されます。

`cq/cloudserviceconfigs/templates/configpage`

および定義 `resourceType` はカスタムコンポーネントを指しています。

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

コンポーネントは、次のように基本コンポーネントを拡張する必要があります。

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

API に関するリファレンスドキュメントについては、次を参照してください。 [com.day.cq.wcm.webservicesupport](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/webservicesupport/package-summary.html).

### AEM の統合 {#aem-integration}

使用可能なサービスが、（`foundation/components/page` または `wcm/mobile/components/page` から継承されたいずれかのページの）**ページのプロパティ**&#x200B;ダイアログの「**クラウドサービス**」タブに一覧表示されます。

このタブには次の機能もあります。

* サービスを有効にできる場所へのリンク
* パスフィールドから設定（サービスのサブノード）を選択

#### パスワードの暗号化 {#password-encryption}

サービスのユーザー資格情報を保存する場合、すべてのパスワードを暗号化する必要があります。

これを行うには、非表示のフォームフィールドを追加します。 このフィールドには、注釈が必要です。 `@Encrypted` プロパティ名。つまり、 `password` フィールド名は次のように記述されます。

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
   <td>ページに自動的に含まれるコンポーネントへの参照パス。<br /> これは、追加機能や JS の包含に使用されます。<br /> このプロパティには、<br /> <code> cq/cloudserviceconfigs/components/servicecomponents</code><br /> が（通常は <code>body</code> タグの前に）含まれるページ上のコンポーネントが含まれます。<br /> Adobe AnalyticsおよびAdobe Targetの場合、このプロパティを使用して、訪問者の行動を追跡する JavaScript 呼び出しなどの追加機能を含めます。</td>
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
   <td>Listings で使用するサービスランキング。</td>
  </tr>
  <tr>
   <td>selectableChild</td>
   <td>ページプロパティダイアログに設定を表示するためのフィルター。</td>
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
   <td>ページプロパティダイアログでの表示。デフォルトで表示（オプション）</td>
  </tr>
 </tbody>
</table>

### ユースケース {#use-cases}

これらのサービスはデフォルトで提供されます。

* [トラッカースニペット](/help/sites-administering/external-providers.md) （Google、WebTrends など）
* [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics)
* [Test&amp;Target](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-target)
<!-- Search&Promote is end of life as of September 1, 2022 * [Search&Promote](/help/sites-administering/marketing-cloud.md#integrating-with-search-promote) -->
* [Dynamic Media](/help/sites-administering/marketing-cloud.md#integrating-with-scene)

>[!NOTE]
>
>[カスタムクラウドサービスの作成](/help/sites-developing/extending-cloud-config-custom-cloud.md)も参照してください。
