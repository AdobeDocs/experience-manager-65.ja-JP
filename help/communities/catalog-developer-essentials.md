---
title: カタログの基本事項
seo-title: カタログの基本事項
description: カタログの概要
seo-description: カタログの概要
uuid: 788512bb-fa38-48fb-a769-1eaae6bb95a1
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 542467ef-3793-4347-8424-c365c5a166f6
translation-type: tm+mt
source-git-commit: 82affd528f2526384b319fe89082e0f574ab5855
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 46%

---


# カタログの基本事項 {#catalog-essentials}

このページでは、イネーブルメントコミュニティサイトのカタログ機能の操作に関する基本情報をまとめています。

コミュニティサイトにカタログ機能が用意されている場合、コミュニティメンバーは、その機能を使用して、カタログに一覧表示された実施可能リソースを参照および選択できます。

The [ `enablement catalog` component](catalog.md) allows community members to access a catalog of [enablement resources](resources.md). AEMタグの使用は、カタログ内の有効化リソースの外観を管理する上で重要な部分です。

[実施可能リソースのタグ付け](tag-resources.md)を参照してください。

## クライアント側の基本事項 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/enablement/components/hbs/catalog</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>インクルード可能</strong></a></td>
   <td>不可</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.enablement.hbs.breadcrumbs<br /> cq.social.enablement.hbs.catalog<br /> cq.social.enablement.hbs.resource<br /> cq.social.enablement.hbs.learningpath</td>
  </tr>
  <tr>
   <td> <strong>テンプレート</strong></td>
   <td> /libs/social/enablement/components/hbs/catalog/catalog.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/enablement/components/hbs/catalog/clientlibs/catalog.css</td>
  </tr>
  <tr>
   <td><strong> properties</strong></td>
   <td>See <a href="catalog.md">Catalog Feature</a></td>
  </tr>
 </tbody>
</table>

## サーバー側の基本事項 {#essentials-for-server-side}

### カタログ機能 {#catalog-function}

A community site structure that includes the [Catalog function](functions.md#catalog-function), includes a configured `enablement catalog` component.

### 事前フィルター {#pre-filters}

コミュニティサイトにカタログ機能が追加されている場合、事前フィルターを指定することで、カタログに表示されるイネーブルメントリソースと学習パスを制限できます。これは、サイトのカタログリソースのインスタンスにプロパティを設定することで行います。

Using the example of the [Enablement Tutorial](getting-started-enablement.md):

* 作成者
* Using [CRXDE](../../help/sites-developing/developing-with-crxde-lite.md)

   * Such as [https://&lt;server>:&lt;port>/crx/de](http://localhost:4502/crx/de)

* カタログページでカタログリソースに移動します。

   * 例：`/content/sites/enable/en/catalog/jcr:content/content/primary/catalog`

* 追加子フィルターノード

   * Select the `catalog`node
   * Select **[!UICONTROL Create Node]**

      * 名前：`filters`
      * タイプ：`nt:unstructured`
      * 「**[!UICONTROL すべて保存]**」を選択します。

* 追加 `se_resource-tags``filters` ノードのプロパティ

   * Select the `filters` node
   * マルチ追加プロパティ

      * 名前：`se_resource-tags`
      * タイプ：String
      * 値：&lt;*TagID[を入力](#pre-filter-tagids)>*
         * Select **[!UICONTROL Multi]**
         * Select **[!UICONTROL Add]**

            * In popup dialog, select `+` to add additional pre-filter TagIDs

* コミュニティサイトの再公開

![chlimage_1-189](assets/chlimage_1-189.png)

#### 事前フィルター TagID {#pre-filter-tagids}

The pre-filter [TagIDs](../../help/sites-developing/framework.md#tagid) must exactly match the tags applied to the enablement resources. これらは、サイトの `resources` フォルダーでプロパティ `se_resource-tags` の値として確認できます。

![chlimage_1-190](assets/chlimage_1-190.png)

### リファレンス API {#reference-apis}

* [イネーブルメント API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/client/api/package-summary.html)

* [レポート API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/client/reporting/api/package-summary.html)

* [レポート分析 API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/client/reporting/analytics/api/package-summary.html)

