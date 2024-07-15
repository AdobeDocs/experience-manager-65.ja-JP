---
title: レンダリングと配信
description: Sling のデフォルトサーブレットを使用してAdobe Experience Manager コンテンツをレンダリングし、JSON およびその他の形式をレンダリングする方法を説明します。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
exl-id: f0c543ae-33ed-40bb-9eb7-0dc3bdea69e0
solution: Experience Manager
feature: Mobile
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 12%

---

# レンダリングと配信{#rendering-and-delivery}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアントサイドレンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)。

Adobe Experience Manager（AEM）のコンテンツは、[Sling デフォルトサーブレット ](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) を使用して簡単にレンダリングし、[JSON](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html#default-json-rendering) やその他の形式をレンダリングできます。

これらの標準レンダリングは、通常、リポジトリをウォークして、コンテンツをそのまま返します。

AEMは、Sling を介して、カスタム sling レンダラーの開発とデプロイをサポートし、レンダリングされたスキーマとコンテンツを完全に制御できます。

Content Services のデフォルトレンダラーは、標準の Sling のデフォルトとカスタム開発の間のギャップを埋め、開発なしでレンダリングされたコンテンツの多くの側面をカスタマイズおよび制御できるようにします。

次の図に、コンテンツサービスのレンダリングを示します。

![chlimage_1-15](assets/chlimage_1-15.png)

## JSON のリクエスト {#requesting-json}

**&lt;RESOURCE.caas[ を使用します。&lt;EXPORT-CONFIG][。&lt;EXPORT-CONFIG].json**:JSON をリクエストします。

<table>
 <tbody>
  <tr>
   <td>RESOURCE</td>
   <td>/content/entities の下のエンティティリソース <br /> または/content の下 <br /> コンテンツリソース</td>
  </tr>
  <tr>
   <td>EXPORT-CONFIG</td>
   <td><p><strong> オプション </strong><br /> </p> <p>/apps/mobileapps/caas/exportConfigs/EXPORT-CONFIG の下にあるエクスポート設定 <br /> 省略すると <br /> デフォルトのエクスポート設定が適用されます </p> </td>
  </tr>
  <tr>
   <td>DEPTH-INT</td>
   <td><strong> オプション </strong><br />Sling レンダリングで使用される、子のレンダリング用の <br /> 深度の再帰</td>
  </tr>
 </tbody>
</table>

## 書き出し設定の作成 {#creating-export-configs}

書き出し設定を作成して、JSON レンダリングをカスタマイズできます。

*/apps/mobileapps/caas/exportConfigs.* に設定ノードを作成できます。

| ノード名 | 設定の名前（セレクターをレンダリングする場合） |
|---|---|
| jcr:primaryType | nt:unstructured |

次の表に、書き出し設定のプロパティを示します。

<table>
 <tbody>
  <tr>
   <td><strong>名前</strong></td>
   <td><strong>型</strong></td>
   <td><strong>デフォルト （設定されていない場合）</strong></td>
   <td><strong>値</strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td>includeComponents</td>
   <td>String[]</td>
   <td>すべてを含める</td>
   <td>sling:resourceType</td>
   <td>json エクスポートから指定された sling:resourceType を持つノードの詳細を除外</td>
  </tr>
  <tr>
   <td>excludeComponent</td>
   <td>String[]</td>
   <td>除外なし</td>
   <td>sling:resourceType</td>
   <td>json エクスポートから指定された sling:resourceType を持つノードの詳細のみを含める</td>
  </tr>
  <tr>
   <td>excludePropertyPrefix</td>
   <td>String[]</td>
   <td>除外なし</td>
   <td>プロパティ接頭辞</td>
   <td>指定したプレフィックスで始まるプロパティを JSON 書き出しから除外します</td>
  </tr>
  <tr>
   <td>excludeProperties</td>
   <td>String[]</td>
   <td>除外なし</td>
   <td>プロパティ名</td>
   <td>指定したプロパティを JSON エクスポートから除外</td>
  </tr>
  <tr>
   <td>includeProperties</td>
   <td>String[]</td>
   <td>すべてを含める</td>
   <td>プロパティ名</td>
   <td><p>excludePropertyPrefix が設定されている場合 <br /> 除外するプレフィックスに一致しているにもかかわらず、指定されたプロパティが含まれます。</p> <p>それ以外の場合（除外プロパティは無視）、これらのプロパティのみを含めます</p> </td>
  </tr>
  <tr>
   <td>includeChildren</td>
   <td>String[]</td>
   <td>すべてを含める</td>
   <td>子の名前</td>
   <td>指定した子を JSON エクスポートから除外</td>
  </tr>
  <tr>
   <td>excludeChild</td>
   <td>String[]<br /> <br /> </td>
   <td>除外なし</td>
   <td>子の名前</td>
   <td>json エクスポートから指定した子のみを含め、その他を除外</td>
  </tr>
  <tr>
   <td>renameProperties</td>
   <td>String[]<br /> <br /> </td>
   <td>何も名前変更しない</td>
   <td>&lt;actual_property_name&gt;,&lt;replacement_property_name&gt;</td>
   <td>置換を使用したプロパティ名の変更</td>
  </tr>
 </tbody>
</table>

### リソースタイプ書き出しの上書き {#resource-type-export-overrides}

*/apps/mobileapps/caas/exportConfigs.* に設定ノードを作成します。

| name | resourceTypeOverrides |
|---|---|
| jcr:primaryType | nt:unstructured |

次の表に、プロパティを示します。

<table>
 <tbody>
  <tr>
   <td><strong>名前</strong></td>
   <td><strong>型</strong></td>
   <td><strong>デフォルト （設定されていない場合）</strong></td>
   <td><strong>値</strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td>&lt;SELECTOR_TO_INC&gt;</td>
   <td>String[] </td>
   <td>-</td>
   <td>sling:resourceType</td>
   <td>次の sling リソースタイプの場合、デフォルトの CaaS json 書き出しを返しません。<br /> リソースを &lt;RESOURCE&gt; としてレンダリングすることで <br /> 顧客の JSON 書き出しを返します。&lt;SELECTOR_TO_INC&gt;.json </td>
  </tr>
 </tbody>
</table>

### 既存のコンテンツサービスの書き出し設定 {#existing-content-services-export-configs}

コンテンツサービスには、次の 2 つの書き出し設定が含まれます。

* デフォルト （設定が指定されていません）
* ページ（サイトページをレンダリングする場合）

#### デフォルトの書き出し設定 {#default-export-configuration}

要求された URI に設定が指定されている場合、Content Services のデフォルトの書き出し設定が適用されます。

&lt;RESOURCE>.caas[.&lt;DEPTH-INT>].json

<table>
 <tbody>
  <tr>
   <td><strong>名前</strong></td>
   <td><strong>値</strong></td>
  </tr>
  <tr>
   <td>excludeProperties</td>
   <td> </td>
  </tr>
  <tr>
   <td>excludePropertyPrefix</td>
   <td>jcr:,sling:,cq:,oak:,pge-</td>
  </tr>
  <tr>
   <td>includeProperties</td>
   <td>jcr:text、text<br />jcr:title、title<br />jcr:description、description<br />jcr:lastModified、lastModified<br />cq:tags、tags<br />cq:lastModified、lastModified</td>
  </tr>
  <tr>
   <td>includeComponents</td>
   <td> </td>
  </tr>
  <tr>
   <td>excludeComponent</td>
   <td> </td>
  </tr>
  <tr>
   <td>includeChildren</td>
   <td> </td>
  </tr>
  <tr>
   <td>excludeChild</td>
   <td> </td>
  </tr>
  <tr>
   <td>Sling JSON の上書き</td>
   <td>foundation/components/image<br />wcm/foundation/components/image<br /> mobileapps/caas/components/data/contentReference<br /> mobileapps/caas/components/data/assetlist</td>
  </tr>
 </tbody>
</table>

#### ページエクスポート設定 {#page-export-configuration}

この設定は、デフォルトを拡張して、子ノードの下に子のグループを含めます。

&lt;SITE_PAGE>.caas.page[.&lt;DEPTH-INT>].json

### その他のリソース {#additional-resources}

コンテンツサービスのその他のトピックについて詳しくは、次のリソースを参照してください。

* [モデルの開発](/help/mobile/administer-mobile-apps.md)
* [コンテンツサービスのオーサリング](/help/mobile/develop-content-as-a-service.md)
* [コンテンツサービスの管理](/help/mobile/developing-content-services.md)
