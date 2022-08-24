---
title: 'カスタム検索フォームのアップグレード '
seo-title: Upgrading Custom Search Forms
description: この記事では、カスタム検索フォームを機能させるために、アップグレード後に必要となる調整について説明します。
seo-description: This article details the adjustments that are required after an upgrade in order for the custom search forms to function.
uuid: 35b8fbb9-5951-4e1c-bf04-4471a55b9cb0
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: a08cee9c-e981-4483-8bdc-e6353977f854
feature: Upgrading
exl-id: 797bbdf9-917a-4537-a5f9-bf2682db968b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1685'
ht-degree: 100%

---

# カスタム検索フォームのアップグレード {#upgrading-custom-search-forms}

AEM 6.2 では、カスタマイズされた検索フォームのリポジトリ内の保存場所が変更されました。アップグレード時に、6.1 での保存場所

* /apps/cq/gui/content/facets

から次の新しい場所に移動されます。

* /conf/global/settings/cq/search/facets

このため、フォームを引き続き機能させるには、アップグレード後に手動での変更が必要になります。

カスタマイズされたデフォルトのフォームだけでなく、新しい検索フォームも変更が必要です。

詳しくは、[検索ファセット](/help/assets/search-facets.md)に関するドキュメントを参照してください。

## resourceType プロパティの変更 {#changing-the-resourcetype-property}

特に指定のない限り、アップグレード後に実行する必要がある変更の大部分では、設定済みのカスタム検索フォームの `sling:resourceType` プロパティを変更する必要があります。この変更は、プロパティがレンダリングスクリプトの正しい場所を指すようにするうえで必要です。

このプロパティを変更するには、次の手順を実行します。

1. `https://server:port/crx/de/index.jsp` に移動して CRXDE Lite を開きます
1. 以下の[カスタム検索フォーム](/help/sites-deploying/upgrading-custom-search-forms.md#list-of-custom-search-forms)のリストに指定されているとおりに、変更する必要があるノードの場所を参照します。
1.  ノードをクリックします。右側のプロパティパネルで、**sling:resourceType** プロパティをクリックして変更します。
1. 最後に、「**すべて保存**」ボタンをクリックして、変更を保存します。

## カスタム検索フォームのリスト {#list-of-custom-search-forms}

すべてのカスタム検索フォームと、アップグレード後に必要な変更点のリストを以下に示します。これらは、 `/conf/global/settings/cq/search/facets/sites/items` の名前を指しています。

### 「fulltext」というノード名を持つフルテキストの述語 {#fulltext-predicate-with-node-name-fulltext}

<table>
 <tbody>
  <tr>
   <td>6.1 のデフォルトの検索フォームのノード</td>
   <td>fulltext</td>
  </tr>
  <tr>
   <td><p>6.1 のリソースタイプ</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicates/fulltextpredicate</p> </td>
  </tr>
  <tr>
   <td>6.2 のリソースタイプ</td>
   <td>n/a</td>
  </tr>
 </tbody>
</table>

AEM 6.1 では、標準のフルテキストの述語は検索フォームの一部でした。6.2 では、フルテキストフィールドが OmniSearch で置き換えられました。この述語はプログラムによってスキップされ、削除可能です。

**アクション：**&#x200B;ノードを完全に削除します。

### その他のフルテキストの述語 {#other-fulltext-predicates}

<table>
 <tbody>
  <tr>
   <td>6.1 のデフォルトの検索フォームのノード</td>
   <td>該当なし</td>
  </tr>
  <tr>
   <td><p>6.1 のリソースタイプ</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicates/fulltextpredicate</p> </td>
  </tr>
  <tr>
   <td>6.2 のリソースタイプ</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicates/fulltextpredicate</p> </td>
  </tr>
 </tbody>
</table>

**アクション：** `resourceType` プロパティを変更します（上記の 6.2 の場所のように「**/coral**」を付加します）。

### パスブラウザーの述語 {#path-browser-predicates}

<table>
 <tbody>
  <tr>
   <td>6.1 のデフォルトの検索フォームのノード<br /><br /> </td>
   <td>path</td>
  </tr>
  <tr>
   <td><p>6.1 のリソースタイプ</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicates/pathpredicate</p> </td>
  </tr>
  <tr>
   <td>6.2 のリソースタイプ</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicates/pathpredicate</p> </td>
  </tr>
 </tbody>
</table>

**アクション：** `resourceType` プロパティを変更します（上記の 6.2 の場所のように「**/coral**」を付加します）。

### タグの述語 {#tags-predicates}

<table>
 <tbody>
  <tr>
   <td>6.1 のデフォルトの検索フォームのノード<br /><br /> </td>
   <td>タグ</td>
  </tr>
  <tr>
   <td><p>6.1 のリソースタイプ</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicates/tagspredicate</p> </td>
  </tr>
  <tr>
   <td>6.2 のリソースタイプ</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicates/tagspredicate</p> </td>
  </tr>
 </tbody>
</table>

**アクション：** **resourceType** プロパティを変更します（上記の 6.2 の場所のように、「**/coral**」を付加します）。

### ページステータスの述語 {#page-status-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1 のデフォルトの検索フォームのノード<br /><br /> </td>
   <td>pagestatuspredicate</td>
  </tr>
  <tr>
   <td><p>6.1 のリソースタイプ</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/pagestatuspredicate</p> </td>
  </tr>
  <tr>
   <td>6.2 のリソースタイプ</td>
   <td>該当なし</td>
  </tr>
 </tbody>
</table>

ページステータスは、2 つのオプションプロパティの述語で置き換えられました。1 つは公開の述語で、もう 1 つはライブコピーステータスの述語です。

**アクション：**

* `pagestatuspredicate` ノードを削除する
* ノードをコピーする

   * `/libs/settings/cq/search/facets/sites/jcr:content/items/publishstatuspredicate`
   * コピー先：`/conf/global/settings/cq/search/facets/sites/jcr:content/items`

* ノードをコピーする

   * `/libs/settings/cq/search/facets/sites/jcr:content/items/livecopystatuspredicate`
   * コピー先：`/conf/global/settings/cq/search/facets/sites/jcr:content/items`

* `analyticspredicate` ノードの `listOrder` プロパティが「**8**」に設定されていることを確認します。この設定は、競合を避けるために必要です。

### 日付範囲の述語 {#date-range-predicates}

<table>
 <tbody>
  <tr>
   <td>6.1 のデフォルトの検索フォームのノード<br /><br /> </td>
   <td>daterangepredicate</td>
  </tr>
  <tr>
   <td>6.1 のリソースタイプ</td>
   <td>cq/gui/components/common/admin/customsearch/searchpredicates/daterangepredicate</td>
  </tr>
  <tr>
   <td>6.2 のリソースタイプ</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicates/daterangepredicate</p> </td>
  </tr>
 </tbody>
</table>

**アクション：** `resourceType` プロパティを調整します（上記の 6.2 の場所のように「**/coral**」を付加します）。

### 非表示のフィルター {#hidden-filter}

<table>
 <tbody>
  <tr>
   <td>6.1 のデフォルトの検索フォームのノード<br /><br /> </td>
   <td>type</td>
  </tr>
  <tr>
   <td><p>6.1 のリソースタイプ</p> </td>
   <td><p>granite/ui/components/foundation/form/hidden</p> </td>
  </tr>
  <tr>
   <td>6.2 のリソースタイプ</td>
   <td><p>granite/ui/components/foundation/form/hidden</p> </td>
  </tr>
 </tbody>
</table>

**アクション：**&#x200B;何も変更しません。

### Analytics の述語 {#analytics-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1 のデフォルトの検索フォームのノード<br /><br /> </td>
   <td>analyticspredicate</td>
  </tr>
  <tr>
   <td><p>6.1 のリソースタイプ</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/analyticspredicate</p> </td>
  </tr>
  <tr>
   <td>6.2 のリソースタイプ</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/analyticspredicate</p> </td>
  </tr>
 </tbody>
</table>

**アクション：** `resourceType` プロパティを調整します（上記の 6.2 の場所のように「**/coral**」を付加します）。

### 範囲の述語 {#range-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1 のデフォルトの検索フォームのノード<br /><br /> </td>
   <td>該当なし</td>
  </tr>
  <tr>
   <td><p>6.1 のリソースタイプ</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/rangepredicate</p> </td>
  </tr>
  <tr>
   <td>6.2 のリソースタイプ</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/rangepredicate</p> </td>
  </tr>
 </tbody>
</table>

**アクション：** `resourceType` プロパティを調整します（上記の 6.2 の場所のように「**/coral**」を付加します）。

>[!NOTE]
>
>注意：6.1 とは異なり、範囲の述語は検索バーにタグをレンダリングしなくなりました。

### オプションプロパティの述語 {#options-property-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1 のデフォルトの検索フォームのノード<br /><br /> </td>
   <td>該当なし</td>
  </tr>
  <tr>
   <td><p>6.1 のリソースタイプ</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/optionspredicate</p> </td>
  </tr>
  <tr>
   <td>6.2 のリソースタイプ</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/optionspredicate</p> </td>
  </tr>
 </tbody>
</table>

**アクション：** `resourceType` プロパティを変更します（上記の 6.2 の場所のように「**/coral**」を付加します）。

### スライダー範囲の述語 {#slider-range-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1 のデフォルトの検索フォームのノード<br /><br /> </td>
   <td>該当なし</td>
  </tr>
  <tr>
   <td><p>6.1 のリソースタイプ</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/sliderrangepredicate</p> </td>
  </tr>
  <tr>
   <td>6.2 のリソースタイプ</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/sliderrangepredicate</p> </td>
  </tr>
 </tbody>
</table>

**アクション：** `resourceType` プロパティを変更します（上記の 6.2 の場所のように「**/coral**」を付加します）。

### コンポーネントの述語 {#components-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1 のデフォルトの検索フォームのノード<br /><br /> </td>
   <td>該当なし</td>
  </tr>
  <tr>
   <td><p>6.1 のリソースタイプ</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/componentspredicate</p> </td>
  </tr>
  <tr>
   <td>6.2 のリソースタイプ</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/componentspredicate</p> </td>
  </tr>
 </tbody>
</table>

**アクション：** `resourceType` プロパティを変更します（上記の 6.2 の場所のように「**/coral**」を付加します）。

### 作成者の述語 {#author-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1 のデフォルトの検索フォームのノード<br /><br /> </td>
   <td>該当なし</td>
  </tr>
  <tr>
   <td><p>6.1 のリソースタイプ</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/userpredicate</p> </td>
  </tr>
  <tr>
   <td>6.2 のリソースタイプ</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/userpredicate</p> </td>
  </tr>
 </tbody>
</table>

**アクション：** `resourceType` プロパティを変更します（上記の 6.2 の場所のように「**/coral**」を付加します）。

### テンプレートの述語 {#templates-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1 のデフォルトの検索フォームのノード<br /><br /> </td>
   <td>該当なし</td>
  </tr>
  <tr>
   <td><p>6.1 のリソースタイプ</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/templatespredicate</p> </td>
  </tr>
  <tr>
   <td>6.2 のリソースタイプ</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/templatespredicate</p> </td>
  </tr>
 </tbody>
</table>

**アクション：** `resourceType` プロパティを変更します（上記の 6.2 の場所のように「**/coral**」を付加します）。

## アセット管理者の検索レール {#assets-admin-search-rail}

以下のノードは `/conf/global/settings/dam/search/facets/assets/items` の名前を指しています。

### 「fulltext」というノード名を持つフルテキストの述語 {#fulltext-predicate-with-node-name-fulltext-1}

| 6.1 のデフォルトの検索フォームのノード | fulltext |
|---|---|
| 6.1 のリソースタイプ | dam/gui/components/admin/customsearch/searchpredicates/fulltextpredicate |
| 6.2 のリソースタイプ | 該当なし |

6.1 では、標準のフルテキストの述語は検索フォームの一部でした。6.2 では、フルテキストフィールドが OmniSearch で置き換えられました。この述語はプログラムによってスキップされ、削除可能です。

**アクション：**&#x200B;上述のノードを削除します。

### パスブラウザーの述語 {#path-browser-predicates-1}

| 6.1 のデフォルトの検索フォームのノード | pathbrowser |
|---|---|
| 6.1 のリソースタイプ | dam/gui/components/admin/customsearch/searchpredicates/pathbrowserpredicate |
| 6.2 のリソースタイプ | dam/gui/coral/components/admin/customsearch/searchpredicates/pathbrowserpredicate |

**アクション：** `resourceType` プロパティを調整します（上記の 6.2 の場所のように「**/coral**」を付加します）。

### MIME タイプの述語 {#mime-type-predicates}

| 6.1 のデフォルトの検索フォームのノード | mimetype |
|---|---|
| 6.1 のリソースタイプ | dam/gui/components/admin/customsearch/searchpredicates/optionspredicate |
| 6.2 のリソースタイプ | dam/gui/coral/components/admin/customsearch/searchpredicates/optionspredicate |

**アクション：** `resourceType` プロパティを調整します（上記の 6.2 の場所のように「**/coral**」を付加します）。

### ファイルサイズの述語 {#file-size-predicates}

| 6.1 のデフォルトの検索フォームのノード | filesize |
|---|---|
| 6.1 のリソースタイプ | dam/gui/components/admin/customsearch/searchpredicates/filesizepredicate |
| 6.2 のリソースタイプ | dam/gui/coral/components/admin/customsearch/searchpredicates/sliderangepredicate |

**アクション：**&#x200B;上記の 6.2 の場所に示すように、`resourceType` を調整します。

### 最終変更アセットの述語 {#asset-last-modified-predicates}

| 6.1 のデフォルトの検索フォームのノード | assetlastmodifiedpredicate |
|---|---|
| 6.1 のリソースタイプ | dam/gui/components/admin/customsearch/searchpredicates/assetlastmodifiedpredicate |
| 6.2 のリソースタイプ | dam/gui/coral/components/admin/customsearch/searchpredicates/assetlastmodifiedpredicate |

アクション：resourceType プロパティを調整します（上記の 6.2 の場所のように「/coral」を付加します）。

### 公開の述語 {#publish-predicate}

| 6.1 のデフォルトの検索フォームのノード | publish |
|---|---|
| 6.1 のリソースタイプ | dam/gui/components/admin/customsearch/searchpredicates/publishpredicate |
| 6.2 のリソースタイプ | dam/gui/coral/components/admin/customsearch/searchpredicates/publishpredicate |

**アクション：**

* `resourceType` プロパティを調整します（上記の 6.2 の場所のように「**/coral**」を付加します）。

* 値 `/libs/dam/options/predicates/publish` の（String 型の）`optionPaths` プロパティを追加します。

* ブール値 `true` の `singleSelect` プロパティを追加します。

### ステータスの述語 {#status-predicates}

| 6.1 のデフォルトの検索フォームのノード | status |
|---|---|
| 6.1 のリソースタイプ | dam/gui/components/admin/customsearch/searchpredicates/optionspredicate |
| 6.2 のリソースタイプ | dam/gui/coral/components/admin/customsearch/searchpredicates/optionspredicate |

**アクション：** `resourceType` プロパティを調整します（上記の 6.2 の場所のように「**/coral**」を付加します）。

### 有効期限ステータスの述語 {#expiry-status-predicates}

| 6.1 のデフォルトの検索フォームのノード | expirystatus |
|---|---|
| 6.1 のリソースタイプ | dam/gui/components/admin/customsearch/searchpredicates/expiredassetpredicate |
| 6.2 のリソースタイプ | dam/gui/coral/components/admin/customsearch/searchpredicates/expiredassetpredicate |

**アクション：** `resourceType` プロパティを変更します（上記の 6.2 の場所のように「**/coral**」を付加します）。

### メタデータの妥当性の述語 {#metadata-validity-predicates}

| 6.1 のデフォルトの検索フォームのノード | metadatavalidity |
|---|---|
| 6.1 のリソースタイプ | dam/gui/components/admin/customsearch/searchpredicates/optionspredicate |
| 6.2 のリソースタイプ | dam/gui/coral/components/admin/customsearch/searchpredicates/optionspredicate |

**アクション：** `resourceType` プロパティを調整します（上記の 6.2 の場所のように「**/coral**」を付加します）。

### 評価の述語 {#rating-predicates}

| 6.1 のデフォルトの検索フォームのノード | 評価 |
|---|---|
| 6.1 のリソースタイプ | dam/gui/components/admin/customsearch/searchpredicates/ratingpredicate |
| 6.2 のリソースタイプ | dam/gui/coral/components/admin/customsearch/searchpredicates/sliderangepredicate |

**アクション：** `resourceType` プロパティを調整します（上記の 6.2 の場所のように「**/coral**」を付加します）。

### 向きの述語 {#orientation-predicate}

| 6.1 のデフォルトの検索フォームのノード | 向き |
|---|---|
| 6.1 のリソースタイプ | dam/gui/components/admin/customsearch/searchpredicates/tagsfilterpredicate |
| 6.2 のリソースタイプ | cq/gui/components/coral/common/admin/customsearch/searchpredicates/tagspredicate |

**アクション：**

* `resourceType` プロパティを変更します（上記の 6.2 の場所のように「**/coral**」を付加します）。

* 同じノードの `fieldLabel` プロパティと同じ値を持つ `text` プロパティを追加します。

* 同じノードの `emptyText` プロパティと同じ値を持つ `text` プロパティを追加します。

* 同じノードの `rootPath` プロパティと同じ値を持つ `optionPaths` プロパティを追加します。

### スタイルの述語 {#style-predicate}

| 6.1 のデフォルトの検索フォームのノード | style |
|---|---|
| 6.1 のリソースタイプ | dam/gui/components/admin/customsearch/searchpredicates/tagsfilterpredicate |
| 6.2 のリソースタイプ | cq/gui/components/coral/common/admin/customsearch/searchpredicates/tagspredicate |

**アクション：**

* `resourceType` プロパティを変更します（上記の 6.2 の場所のように「**/coral**」を付加します）。

* 同じノードの `fieldLabel` プロパティと同じ値を持つ `text` プロパティを追加します。

* 同じノードの `emptyText` プロパティと同じ値を持つ `text` プロパティを追加します。

* 同じノードの `rootPath` プロパティと同じ値を持つ `optionPaths` プロパティを追加します。

### ビデオ形式の述語 {#video-format-predicates}

| 6.1 のデフォルトの検索フォームのノード | videoFormat |
|---|---|
| 6.1 のリソースタイプ | dam/gui/components/admin/customsearch/searchpredicates/optionspredicate |
| 6.2 のリソースタイプ | dam/gui/coral/components/admin/customsearch/searchpredicates/optionspredicate |

**アクション：** `resourceType` プロパティを変更します（上記の 6.2 の場所のように「**/coral**」を付加します）。

### メインアセットの述語 {#mainasset-predicate}

| 6.1 のデフォルトの検索フォームのノード | mainasset |
|---|---|
| 6.1 のリソースタイプ | granite/ui/components/foundation/form/hidden |
| 6.2 のリソースタイプ | granite/ui/components/coral/foundation/form/hidden |

**アクション：** `resourceType` プロパティを変更します（上記の 6.2 の場所のように「**/coral**」を付加します）。
