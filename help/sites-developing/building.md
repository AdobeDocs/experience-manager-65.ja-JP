---
title: AEM アプリケーションへのタグ付けの構築
seo-title: Building Tagging into an AEM Application
description: カスタム AEM アプリケーション内のタグまたは拡張タグをプログラムで操作します
seo-description: Programmatically work with tags or extending tags within a custom AEM application
uuid: 0549552e-0d51-4162-b418-babf4ceee046
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 032aea1f-0105-4299-8d32-ba6bee78437f
feature: Tagging
exl-id: d885520d-d0ed-45fa-8511-faa2495d667a
source-git-commit: 325af649564d93beedfc762a8f5beacec47b1641
workflow-type: tm+mt
source-wordcount: '887'
ht-degree: 67%

---

# AEM アプリケーションへのタグ付けの構築{#building-tagging-into-an-aem-application}

カスタムAEMアプリケーション内のタグや拡張タグをプログラムで操作する場合、このページでは、

* [タグ付け API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/tagging/package-summary.html)

これは

* [タグ付けフレームワーク](/help/sites-developing/framework.md)

タグに関する関連情報については、次を参照してください。

* [タグの管理](/help/sites-administering/tags.md) タグの作成と管理、およびタグが適用されるコンテンツについて説明します。
* [タグの使用](/help/sites-authoring/tags.md) コンテンツのタグ付けについて詳しくは、を参照してください。

## タグ付け API の概要 {#overview-of-the-tagging-api}

AEM の[タグ付けフレームワーク](/help/sites-developing/framework.md)の実装により、JCR API を使用してタグおよびタグコンテンツを管理できます。TagManager は、`cq:tags` 文字列配列プロパティに値として入力されたタグが重複しないようにして、存在しないタグを指している TagID を削除し、移動または結合されたタグの TagID を更新してください。TagManager は、間違った変更を元に戻す JCR 監視リスナーを使用します。メインクラスは [com.day.cq.tagging](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/index.html?com/day/cq/tagging/package-summary.html) パッケージ内にあります。

* JcrTagManagerFactory - `TagManager` の JCR ベースの実装を返します。タグ付け API のリファレンス実装です。
* `TagManager` - パスと名前を使用して、タグを解決して作成できます。
* `Tag` - タグオブジェクトを定義します。

### JCR ベースの TagManager の取得 {#getting-a-jcr-based-tagmanager}

TagManager インスタンスを取得するには、JCR が必要です `Session` および `getTagManager(Session)`:

```java
@Reference
JcrTagManagerFactory jcrTagManagerFactory;

TagManager tagManager = jcrTagManagerFactory.getTagManager(session);
```

一般的な Sling コンテキストでは、 `TagManager` から `ResourceResolver`:

```java
TagManager tagManager = resourceResolver.adaptTo(TagManager.class);
```

### Tag オブジェクトの取得 {#retrieving-a-tag-object}

A `Tag` は、 `TagManager`（既存のタグを解決するか作成する）:

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

`Tags` を JCR `Nodes` にマップする JCR ベースの実装の場合、リソースがあれば（例：`/content/cq:tags/default/my/tag`）、Sling の `adaptTo` メカニズムを直接使用できます。

```java
Tag tag = resource.adaptTo(Tag.class);
```

タグは、ノードからではなく、*リソース *からのみ変換できますが、ノードとリソースの両方に変換できます。

```java
Node node = tag.adaptTo(Node.class);
Resource node = tag.adaptTo(Resource.class);
```

>[!NOTE]
>
>`Node` は Sling の `Adaptable.adaptTo(Class)` メソッドを実装しないので、`Node` を `Tag` に直接適合させることはできません。

### タグの取得と設定 {#getting-and-setting-tags}

```java
// Getting the tags of a Resource:
Tag[] tags = tagManager.getTags(resource);

// Setting tags to a Resource:
tagManager.setTags(resource, tags);
```

### タグの検索 {#searching-for-tags}

```java
// Searching for the Resource objects that are tagged with the tag object:
Iterator<Resource> it = tag.find();

// Retrieving the usage count of the tag object:
long count = tag.getCount();

// Searching for the Resource objects that are tagged with the tagID String:
 RangeIterator<Resource> it = tagManager.find(tagID);
```

>[!NOTE]
>
>次の有効な `RangeIterator` を使用できます。
>
>`com.day.cq.commons.RangeIterator`

### タグの削除 {#deleting-tags}

```java
tagManager.deleteTag(tag);
```

### タグの複製 {#replicating-tags}

タグのタイプは `Replicator` なので、タグで複製サービス（`nt:hierarchyNode`）を使用できます。

```java
replicator.replicate(session, replicationActionType, tagPath);
```

## クライアント側でのタグ付け {#tagging-on-the-client-side}

フォームウィジェット `CQ.tagging.TagInputField` は、タグを入力するためのものです。 既存のタグから選択できるポップアップメニューを備えており、自動入力などの機能もあります。xtype は `tags` です。

## タグのガベージコレクター {#the-tag-garbage-collector}

タグのガベージコレクターは、非表示および未使用のタグをクリーンアップするバックグラウンドサービスです。非表示および未使用のタグとは、`cq:movedTo`プロパティが設定された`/content/cq:tags`の下にあるタグのことで、コンテンツノードでは使用されません（カウントはゼロになります）。この遅延削除プロセスを使用すると、コンテンツノード ( `cq:tags` プロパティ ) は、移動または結合操作の一環として更新する必要はありません。 `cq:tags` プロパティの参照は、`cq:tags` プロパティがアップデートされると自動的にアップデートされます（例：ページプロパティダイアログを介して）。

タグのガベージコレクターは、デフォルトで 1 日に 1 回実行されます。次の場所で設定できます。

```xml
http://localhost:4502/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector
```

## タグ検索およびタグ一覧 {#tag-search-and-tag-listing}

タグ検索およびタグ一覧は次のように動作します。

* TagID の検索では、`cq:movedTo` プロパティが TagID に設定されているタグを検索します。`cq:movedTo` の TagID に従って検索します。

* タグタイトルの検索では、`cq:movedTo` プロパティのないタグのみを検索します。

## 他の言語のタグ {#tags-in-different-languages}

タグの管理に関するドキュメントの[他の言語でのタグ管理](/help/sites-administering/tags.md#managing-tags-in-different-languages)の節で説明されているように、タグの `title` は別の言語で定義できます。言語に依存するプロパティがタグノードに追加されます。このプロパティは `jcr:title.<locale>` の形式を持ちます（例：フランス語訳は `jcr:title.fr`）この `<locale>` は小文字の ISO ロケール文字列である必要があり、「 — 」の代わりに「_」を使用します。次に例を示します。 `de_ch`.

**Animals** タグが **Products** ページに追加されると、値 `stockphotography:animals` は /content/geometrixx/en/products/jcr:content ノードの `cq:tags` プロパティに追加されます。翻訳は、タグノードから参照されます。

サーバーサイド API には、ローカライズされた `title` 関連のメソッドがあります。

* [com.day.cq.tagging.Tag](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/index.html?com/day/cq/tagging/Tag.html)

   * getLocalizedTitle(Locale locale)
   * getLocalizedTitlePaths()
   * getLocalizedTitles()
   * getTitle(Locale locale)
   * getTitlePath(Locale locale)

* [com.day.cq.tagging.TagManager](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/index.html?com/day/cq/tagging/TagManager.html)

   * canCreateTagByTitle(String tagTitlePath, Locale locale)
   * createTagByTitle(String tagTitlePath, Locale locale)
   * resolveByTitle(String tagTitlePath, Locale locale)

AEM では、言語はページ言語またはユーザー言語のどちらかから取得できます。

* JSP でページ言語を取得するには：

   * `currentPage.getLanguage(false)`

* JSP でユーザー言語を取得するには：

   * `slingRequest.getLocale()`

この `currentPage` および `slingRequest` は、 [&lt;cq:definedobjects>](/help/sites-developing/taglib.md) タグを使用します。

タグ付けの場合、ローカリゼーションはタグとしてのコンテキストに依存します `titles`は、ページ言語、ユーザー言語またはその他の言語で表示できます。

### タグを編集ダイアログへの新しい言語の追加 {#adding-a-new-language-to-the-edit-tag-dialog}

以下の手順では、 **タグ編集** ダイアログ：

1. **CRXDE** で、ノード `/content/cq:tags` の複数値プロパティ `languages` を編集します。

1. フィンランド語のロケールを表す `fi_fi` を追加して、変更を保存してください。

**タグ付け**&#x200B;コンソールでタグを編集する際に、ページプロパティタグダイアログと&#x200B;**タグを編集**&#x200B;ダイアログで、新しい言語（フィンランド語）を使用できるようになりました。

>[!NOTE]
>
>新しい言語は、AEMで認識される言語の 1 つである必要があります。 つまり、以下のノードとして使用できる必要があります。 `/libs/wcm/core/resources/languages`.

>[!CAUTION]
>
>サービスパックをインストールすると、/content/cq:tags ノードの languages プロパティがデフォルトにリセットされます。 したがって、インストール前にプロパティから追加する必要があります。
