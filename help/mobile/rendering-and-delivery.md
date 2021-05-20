---
title: レンダリングと配信
seo-title: レンダリングと配信
description: レンダリングと配信
seo-description: 'null'
uuid: 1253b6a5-6bf3-42b1-be3a-efa23b6ddb51
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 672d5b1e-6b2f-4afe-ab04-c398e5ef45d5
exl-id: f0c543ae-33ed-40bb-9eb7-0dc3bdea69e0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 40%

---

# レンダリングと配信{#rendering-and-delivery}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアント側レンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)を参照してください。

AEMコンテンツは、[Sling Default Servlets](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html)を介して簡単にレンダリングでき、[JSON](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html#default-json-rendering)やその他の形式をレンダリングできます。

これらの既製のレンダラーは一般に、リポジトリを調べて、コンテンツをそのまま返します。

また、AEM は、Sling を介して、レンダリングされるスキーマとコンテンツのフルコントロールを取得するカスタム sling レンダラーの開発および展開もサポートします。

Content Services Default Rendererは、標準のSling DefaultsとCustom Developmentの間のギャップを埋め、開発を行わずにレンダリングされたコンテンツの多くの側面をカスタマイズおよび制御できます。

次の図に、コンテンツサービスのレンダリングの構造を示します。

![chlimage_1-15](assets/chlimage_1-15.png)

## JSON のリクエスト {#requesting-json}

**&lt;RESOURCE.caas[を使用します。&lt;EXPORT-CONFIG][.&lt;export-config>.jsontoは** JSONをリクエストします。]

<table>
 <tbody>
  <tr>
   <td>リソース</td>
   <td>/content/entities<br />または<br />の下のエンティティリソース/contentの下のコンテンツリソース</td>
  </tr>
  <tr>
   <td>EXPORT-CONFIG</td>
   <td><p><strong>オプション</strong><br /> </p> <p>/apps/mobileapps/caas/exportConfigs/EXPORT-CONFIG<br /> <br />にある書き出し設定を省略すると、デフォルトの書き出し設定が適用されます </p> </td>
  </tr>
  <tr>
   <td>DEPTH-INT</td>
   <td><strong></strong><br /> <br /> Slingレンダリングで使用される子のレンダリング用のOPTIONALdepth再帰</td>
  </tr>
 </tbody>
</table>

## 書き出し設定の作成 {#creating-export-configs}

書き出し設定を作成して、JSON レンダリングをカスタマイズできます。

設定ノードは、*/apps/mobileapps/caas/exportConfigs.*&#x200B;の下に作成できます。

| ノード名 | 設定の名前（レンダリングセレクター用） |
|---|---|
| jcr:primaryType | nt:unstructured |

次の表に、書き出し設定のプロパティを示します。

<table>
 <tbody>
  <tr>
   <td><strong>名前</strong></td>
   <td><strong>型</strong></td>
   <td><strong>デフォルト（設定されていない場合）</strong></td>
   <td><strong>値</strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td>includeComponents</td>
   <td>String[]</td>
   <td>すべてを含む</td>
   <td>sling:resourceType</td>
   <td>JSON書き出しから、指定されたsling:resourceTypeを持つノードの詳細を除外</td>
  </tr>
  <tr>
   <td>excludeComponents</td>
   <td>String[]</td>
   <td>何も除外しない</td>
   <td>sling:resourceType</td>
   <td>JSON書き出しから指定されたsling:resourceTypeを持つノードの詳細のみを含める</td>
  </tr>
  <tr>
   <td>excludePropertyPrefixes</td>
   <td>String[]</td>
   <td>何も除外しない</td>
   <td>プロパティのプレフィックス</td>
   <td>指定されたプレフィックスで始まるプロパティをJSON書き出しから除外する</td>
  </tr>
  <tr>
   <td>excludeProperties</td>
   <td>String[]</td>
   <td>何も除外しない</td>
   <td>プロパティ名</td>
   <td>JSON書き出しから指定したプロパティを除外する</td>
  </tr>
  <tr>
   <td>includeProperties</td>
   <td>String[]</td>
   <td>すべてを含む</td>
   <td>プロパティ名</td>
   <td><p>excludePropertyPrefixesが<br />に設定されている場合、除外するプレフィックスと一致するにもかかわらず、指定されたプロパティが含まれます。</p> <p>else （excludeプロパティは無視）は、次のプロパティのみを含みます。</p> </td>
  </tr>
  <tr>
   <td>includeChildren</td>
   <td>String[]</td>
   <td>すべてを含む</td>
   <td>子の名前</td>
   <td>JSON書き出しから指定した子を除外</td>
  </tr>
  <tr>
   <td>excludeChildren</td>
   <td>String[]<br /> <br /> </td>
   <td>何も除外しない</td>
   <td>子の名前</td>
   <td>JSON書き出しから指定された子のみを含め、他の子を除外する</td>
  </tr>
  <tr>
   <td>renameProperties</td>
   <td>String[]<br /> <br /> </td>
   <td>何も変更しない</td>
   <td>&lt;actual_property_name&gt;,&lt;replacement_property_name&gt;</td>
   <td>置換を使用してプロパティを名前変更</td>
  </tr>
 </tbody>
</table>

### リソースタイプの書き出しの上書き {#resource-type-export-overrides}

*/apps/mobileapps/caas/exportConfigs.*&#x200B;の下に設定ノードを作成します。

| name | resourceTypeOverrides |
|---|---|
| jcr:primaryType | nt:unstructured |

次の表に、プロパティを示します。

<table>
 <tbody>
  <tr>
   <td><strong>名前</strong></td>
   <td><strong>型</strong></td>
   <td><strong>デフォルト（設定されていない場合）</strong></td>
   <td><strong>値</strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td>&lt;selector_to_inc&gt;</td>
   <td>String[] </td>
   <td>-</td>
   <td>sling:resourceType</td>
   <td>次のSlingリソースタイプの場合は、デフォルトのCaaS json書き出しを返さないでください。<br /> リソースを<br /> &lt;resource&gt;としてレンダリングして、顧客のJSON書き出しを返します。&lt;selector_to_inc&gt;.json </td>
  </tr>
 </tbody>
</table>

### 既存のコンテンツサービスの書き出し設定 {#existing-content-services-export-configs}

コンテンツサービスには 2 つの書き出し設定があります。

* デフォルト（設定が指定されていません）
* ページ（サイトのページをレンダリングする）

#### デフォルト書き出し設定  {#default-export-configuration}

リクエストされた URI に設定が指定されている場合は、コンテンツサービスのデフォルト書き出し設定が適用されます。

&lt;RESOURCE>.caas[.&lt;depth-int>].json

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
   <td>excludePropertyPrefixes</td>
   <td>jcr:,sling:,cq:,oak:,pge-</td>
  </tr>
  <tr>
   <td>includeProperties</td>
   <td>jcr:text,text<br /> jcr:title,title<br /> jcr:description,description<br /> jcr:lastModified,lastModified<br /> cq:tags,tags<br /> cq:lastModified,lastModified</td>
  </tr>
  <tr>
   <td>includeComponents</td>
   <td> </td>
  </tr>
  <tr>
   <td>excludeComponents</td>
   <td> </td>
  </tr>
  <tr>
   <td>includeChildren</td>
   <td> </td>
  </tr>
  <tr>
   <td>excludeChildren</td>
   <td> </td>
  </tr>
  <tr>
   <td>Sling JSONの上書き</td>
   <td>foundation/components/image<br /> wcm/foundation/components/image<br /> mobileapps/caas/components/data/contentReference<br /> mobileapps/caas/components/data/assetlist</td>
  </tr>
 </tbody>
</table>

#### ページ書き出し設定 {#page-export-configuration}

この設定は、デフォルトを拡張して、子要素ノードの下にグループ化された子要素を含めます。

&lt;SITE_PAGE>.caas.page[.&lt;depth-int>].json

### その他のリソース {#additional-resources}

コンテンツサービスの追加トピックについて詳しくは、次のリソースを参照してください。

* [モデルの開発](/help/mobile/administer-mobile-apps.md)
* [コンテンツサービスのオーサリング](/help/mobile/develop-content-as-a-service.md)
* [コンテンツサービスの管理](/help/mobile/developing-content-services.md)
