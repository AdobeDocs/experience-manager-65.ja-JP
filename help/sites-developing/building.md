---
title: AEM アプリケーションへのタグの作成
seo-title: AEM アプリケーションへのタグの作成
description: カスタム AEM アプリケーション内のタグまたは拡張タグをプログラムで操作します
seo-description: カスタム AEM アプリケーション内のタグまたは拡張タグをプログラムで操作します
uuid: 0549552e-0d51-4162-b418-babf4ceee046
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 032aea1f-0105-4299-8d32-ba6bee78437f
translation-type: tm+mt
source-git-commit: 1493b301ecf4c25f785495e11ead352de600ddb7
workflow-type: tm+mt
source-wordcount: '893'
ht-degree: 41%

---


# AEM アプリケーションへのタグの作成{#building-tagging-into-an-aem-application}

カスタム AEM アプリケーション内のタグまたは拡張タグをプログラムで操作するために、このページでは、次の使用方法を説明します。

* [タグ付け API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/package-summary.html)

が

* [タグフレームワーク](/help/sites-developing/framework.md)

タグに関する関連情報については、次を参照してください。

* [タグの作成と管理、および適用されたコンテンツタグに関する情報は、](/help/sites-administering/tags.md) タグの管理を参照してください。
* コンテンツのタグ付けについては、[タグの使用](/help/sites-authoring/tags.md)を参照してください。

## タグ付け API の概要  {#overview-of-the-tagging-api}

AEM の[タグフレームワーク](/help/sites-developing/framework.md)の実装により、JCR API を使用してタグおよびタグコンテンツを管理できます。TagManagerでは、`cq:tags`文字列配列プロパティの値として入力したタグは重複しないように保証され、既存でないタグを指すTagIDは削除され、移動または結合されたタグのTagIDが更新されます。 TagManager は、間違った変更を元に戻す JCR 監視リスナーを使用します。メインクラスは [com.day.cq.tagging](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/package-summary.html) パッケージ内にあります。

* JcrTagManagerFactory - `TagManager` の JCR ベースの実装を返します。タグ付け API のリファレンス実装です。
* `TagManager`  — パスと名前によるタグの解決と作成を可能にします。
* `Tag`  — タグオブジェクトを定義します。

### JCR ベースの TagManager の取得 {#getting-a-jcr-based-tagmanager}

TagManager インスタンスを取得するには、JCR `Session` を取得して `getTagManager(Session)` ) を呼び出す必要があります。

```java
@Reference
JcrTagManagerFactory jcrTagManagerFactory;

TagManager tagManager = jcrTagManagerFactory.getTagManager(session);
```

通常の Sling コンテキストでは、`TagManager` を `ResourceResolver` に適合させることもできます。

```java
TagManager tagManager = resourceResolver.adaptTo(TagManager.class);
```

### Tag オブジェクトの取得 {#retrieving-a-tag-object}

`Tag` は、既存のタグを解決するか新しいタグを作成することにより、`TagManager` を介して取得できます。

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

`Tags`をJCR `Nodes`にマッピングするJCRベースの実装の場合、リソース（例：`/content/cq:tags/default/my/tag`）がある場合は、Slingの`adaptTo`メカニズムを直接使用できます。

```java
Tag tag = resource.adaptTo(Tag.class);
```

タグは*aリソース（ノードではない）からしか変換できませんが、タグは*aノードとリソースの両方*に変換できます。

```java
Node node = tag.adaptTo(Node.class);
Resource node = tag.adaptTo(Resource.class);
```

>[!NOTE]
>
>`Node`はSling `Adaptable.adaptTo(Class)`メソッドを実装していないので、`Node`から`Tag`に直接適応させることはできません。

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
>使用可能な `RangeIterator` を次に示します。
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

`CQ.tagging.TagInputField` は、タグを入力するためのフォームウィジェットです。既存のタグから選択できるポップアップメニューを備えており、自動入力などの機能もあります。xtypeは`tags`です。

## タグのガベージコレクター {#the-tag-garbage-collector}

タグガベージコレクターは、非表示で未使用のタグをクリーンアップするバックグラウンドサービスです。 非表示および未使用のタグは、`/content/cq:tags`の下のタグで、`cq:movedTo`プロパティを持ち、コンテンツノードでは使用されません。数は0です。 この遅延削除プロセスを使用すると、移動や結合操作の一環としてコンテンツノード（`cq:tags`プロパティ）を更新する必要がありません。 `cq:tags`プロパティの参照は、`cq:tags`プロパティが更新されると自動的に更新されます。例えば、ページプロパティダイアログを使用します。

タグガベージコレクターは、デフォルトで1日に1回実行されます。 これは、次の場所で設定できます。

```xml
http://localhost:4502/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector
```

## タグ検索およびタグリスト {#tag-search-and-tag-listing}

タグおよびタグ一覧の検索は次のように動作します。

* TagIDを検索すると、`cq:movedTo`プロパティがTagIDに設定され、`cq:movedTo` TagIDを通じて検索されます。

* 「タグタイトル」を検索すると、`cq:movedTo`プロパティを持たないタグのみが検索されます。

## 他の言語のタグ {#tags-in-different-languages}

タグの管理に関するドキュメントで説明されているように、[異なる言語でのタグの管理](/help/sites-administering/tags.md#managing-tags-in-different-languages)の節では、タグ`title`を異なる言語で定義できます。 次に、言語に依存するプロパティがタグノードに追加されます。 このプロパティは`jcr:title.<locale>`の形式を持ちます。例：`jcr:title.fr`（フランス語訳） `<locale>` は、小文字のISOロケール文字列である必要があり、「 — 」の代わりに「_」を使用します。例： `de_ch`.

**Animals**&#x200B;タグを&#x200B;**製品**&#x200B;ページに追加すると、値`stockphotography:animals`がノード/content/geometrixx/en/products/jcr:contentのプロパティ`cq:tags`に追加されます。 翻訳は、タグノードから参照されます。

サーバー側 API には、ローカライズされた `title` 関連のメソッドがあります。

* [com.day.cq.tagging.Tag](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/Tag.html)

   * getLocalizedTitle(Locale locale)
   * getLocalizedTitlePaths()
   * getLocalizedTitles()
   * getTitle(Locale locale)
   * getTitlePath(Locale locale)

* [com.day.cq.tagging.TagManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/TagManager.html)

   * canCreateTagByTitle(String tagTitlePath, Locale)
   * createTagByTitle(String tagTitlePath, Locale locale)
   * resolveByTitle(String tagTitlePath, Locale locale)

AEM では、言語はページ言語またはユーザー言語のどちらかから取得できます。

* JSPでページ言語を取得するには：

   * `currentPage.getLanguage(false)`

* JSPでユーザー言語を取得するには：

   * `slingRequest.getLocale()`

`currentPage` および `slingRequest` は、[&lt;cq:definedObjects>](/help/sites-developing/taglib.md) タグを介して JSP で使用できます。

タグ付けの場合、ローカライズはコンテキストに依存します。タグの `titles` はページ言語、ユーザー言語またはそれ以外の任意の言語で表示することができます。

### タグを編集ダイアログへの新しい言語の追加 {#adding-a-new-language-to-the-edit-tag-dialog}

次の手順では、**タグ編集**&#x200B;ダイアログに新しい言語（フィンランド語）を追加する方法を説明します。

1. **CRXDE**&#x200B;で、ノード`/content/cq:tags`の複数値のプロパティ`languages`を編集します。

1. 追加`fi_fi` — フィンランド語のロケールを表し、変更を保存します。

新しい言語（フィンランド語）が、ページプロパティのタグダイアログと、**タグ付け**&#x200B;コンソールでタグを編集する際の&#x200B;**タグの編集**&#x200B;ダイアログで使用できるようになりました。

>[!NOTE]
>
>新しい言語は、AEMで認識される言語の1つである必要があります。つまり、`/libs/wcm/core/resources/languages`の下のノードとして使用できる必要があります。

