---
title: カタログの基本事項
seo-title: Catalog Essentials
description: カタログの概要
seo-description: Catalog overview
uuid: 788512bb-fa38-48fb-a769-1eaae6bb95a1
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 542467ef-3793-4347-8424-c365c5a166f6
exl-id: 4ca76b50-d56d-4f4d-be92-bf8929c5d754
source-git-commit: 1d334c42088342954feb34f6179dc5b134f81bb8
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 45%

---

# カタログの基本事項 {#catalog-essentials}

このページでは、イネーブルメントコミュニティサイトのカタログ機能の操作に関する基本情報をまとめています。

コミュニティサイトにカタログ機能が用意されている場合、コミュニティメンバーは、その機能を使用して、カタログに一覧表示された実施可能リソースを参照および選択できます。

この [ `enablement catalog` コンポーネント](catalog.md) コミュニティメンバーが [イネーブルメントリソース](resources.md). AEMタグの使用は、カタログ内のイネーブルメントリソースの外観を管理するうえで重要な役割を果たします。

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
   <td>いいえ</td>
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
   <td>詳しくは、 <a href="catalog.md">カタログ機能</a></td>
  </tr>
 </tbody>
</table>

## サーバー側の基本事項 {#essentials-for-server-side}

### カタログ機能 {#catalog-function}

を含むコミュニティサイト構造 [カタログ機能](functions.md#catalog-function)（設定済みを含む） `enablement catalog` コンポーネント。

### 事前フィルター {#pre-filters}

コミュニティサイトにカタログ機能が追加されている場合、事前フィルターを指定することで、カタログに表示されるイネーブルメントリソースと学習パスを制限できます。これは、サイトのカタログリソースのインスタンスでプロパティを設定することでおこなわれます。

例 [イネーブルメントチュートリアル](getting-started-enablement.md):

* 作成者
* 使用 [CRXDE](../../help/sites-developing/developing-with-crxde-lite.md)

   * 例： [https://&lt;server>:&lt;port>/crx/de](http://localhost:4502/crx/de)

* カタログページのカタログリソースに移動します。

   * 例：`/content/sites/enable/en/catalog/jcr:content/content/primary/catalog`

* 子フィルターノードを追加

   * を選択します。 `catalog`ノード
   * 選択 **[!UICONTROL ノードを作成]**

      * 名前：`filters`
      * 型：`nt:unstructured`
      * 「**[!UICONTROL すべて保存]**」を選択します。

* 追加 `se_resource-tags` プロパティを `filters` ノード

   * を選択します。 `filters` ノード
   * 複数のプロパティを追加する

      * 名前：`se_resource-tags`
      * タイプ：String
      * 値：&lt;*TagID[ を入力](#pre-filter-tagids)>*
         * 選択 **[!UICONTROL 複数]**
         * 選択 **[!UICONTROL 追加]**

            * ポップアップダイアログで、「 `+` タグ ID を追加するには、以下を実行します。

* コミュニティサイトを再公開

![configure-catalog](assets/configure-catalog.png)

#### 事前フィルター TagID {#pre-filter-tagids}

プリフィルター [タグ ID](../../help/sites-developing/framework.md#tagid) は、イネーブルメントリソースに適用されるタグと完全に一致する必要があります。 これらは、サイトの `resources` フォルダーでプロパティ `se_resource-tags` の値として確認できます。

![configure-filters](assets/configure-catalog1.png)

### リファレンス API {#reference-apis}

* [イネーブルメント API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/reporting/model/api/package-summary.html)

* [レポート API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/reporting/dv/api/package-summary.html)

* [レポート分析 API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/reporting/dv/model/api/package-summary.html)
