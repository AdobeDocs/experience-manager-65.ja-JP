---
title: タグの基本事項
seo-title: タグの基本事項
description: タグの概要
seo-description: タグの概要
uuid: a5d52319-f821-4608-b0ab-abc8a1374343
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: d355a3ee-c8a8-4a07-8d28-d1a99bda315c
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 61%

---


# タグの基本事項 {#tag-essentials}

AEM Communities コンポーネントの設定でタグ付けを有効化すると、コミュニティメンバーは、パブリッシュ環境で投稿するコンテンツをタグ付けできるようになります。

パブリッシュ環境で適用されるタグの基礎となるインフラストラクチャは、オーサー環境でコンテンツ（ページやアセットなど）に適用されるタグの場合と同じです。

* See [Administering Tags](../../help/sites-administering/tags.md) and [Tagging User Generated Content](tag-ugc.md) (UGC) for information about creating and managing tags.

* See [Tagging for Developers](../../help/sites-developing/tags.md) for information about the [tagging framework](../../help/sites-developing/framework.md) as well as including and extending tags in [custom applications](../../help/sites-developing/building.md).

* See [Using Social Tag Cloud](tagcloud.md) for information for authors on how to add a `social tag cloud` component to a page to highlight the tags applied to UGC in the publish environment.

* カタログのリソースをタグ付けする方法については、[イネーブルメントリソースのタグ付け](tag-resources.md)を参照してください。

UGC のタグ付けは、[コミュニティサイト](sites-console.md#tagging)または次のいずれかの機能を設定する際に有効化することができます。

* [ブログ](blog-feature.md)
* [カレンダー](calendar.md)
* [ファイルライブラリ](file-library.md)
* [フォーラム](forum.md)
* [Q&amp;A](working-with-qna.md)

## クライアント側の基本事項 {#essentials-for-client-side}

### Social タグクラウド {#social-tag-cloud}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/commons/components/hbs/tagcloud</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>インクルード可能</strong></a></td>
   <td>不可</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.tagcloud</td>
  </tr>
  <tr>
   <td> <strong>テンプレート</strong></td>
   <td> /libs/social/commons/components/hbs/tagcloud/tagcloud.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/commons/components/hbs/tagcloud/clientlibs/tagcloud.css</td>
  </tr>
  <tr>
   <td><strong>properties</strong></td>
   <td>See <a href="tagcloud.md">Using Social Tag Cloud</a></td>
  </tr>
 </tbody>
</table>

* [クライアント側のカスタマイズ](client-customize.md)

## サーバー側の基本事項 {#essentials-for-server-side}

* [Social タグクラウド API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/tagcloud/api/package-summary.html)

* [Social タグマネージャー](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/tagging/package-summary.html)

* [サーバー側のカスタマイズ](server-customize.md)

## タグの検索 {#tag-searching}

[機能パック 1](deploy-communities.md#latestfeaturepack)（FP1）以降では、[タグタイトル](../../help/sites-developing/framework.md#tag-characteristics)を使用して、タグの検索を実行します。

FP1 より前では、[タグ ID](../../help/sites-developing/framework.md#tagid) を使用して、タグの検索を実行していました。
