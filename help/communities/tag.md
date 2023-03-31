---
title: タグの基本事項
seo-title: Tag Essentials
description: タグの概要
seo-description: Tag overview
uuid: a5d52319-f821-4608-b0ab-abc8a1374343
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: d355a3ee-c8a8-4a07-8d28-d1a99bda315c
exl-id: 6e8af8cf-1239-46f9-b2fe-4aa80abc86ea
source-git-commit: 4dbbcc41757843d3b2d5a3bbb2656ef587e83d2c
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 5%

---

# タグの基本事項 {#tag-essentials}

AEM Communitiesコンポーネントでタグ付けが有効になっている場合、コミュニティメンバーは、パブリッシュ環境で投稿するコンテンツにタグ付けできます。

パブリッシュ環境で適用されるタグの基盤となるインフラストラクチャは、オーサー環境でコンテンツに適用されるタグ（ページやアセットなど）の場合と同じです。

* 詳しくは、 [タグの管理](../../help/sites-administering/tags.md) および [ユーザー生成コンテンツのタグ付け](tag-ugc.md) (UGC) を参照してください。

* 詳しくは、 [開発者向けタグ付け](../../help/sites-developing/tags.md) を参照してください。 [タグ付けフレームワーク](../../help/sites-developing/framework.md) にタグを追加したり、タグを拡張したりする [カスタムアプリケーション](../../help/sites-developing/building.md).

* 詳しくは、 [Social タグクラウドの使用](tagcloud.md) を参照してください。 `social tag cloud` コンポーネントをページに追加して、パブリッシュ環境で UGC に適用されたタグをハイライトします。

UGC のタグ付けは、 [コミュニティサイト](sites-console.md#tagging) または次の機能の 1 つ：

* [ブログ](blog-feature.md)
* [Calendar](calendar.md)
* [ファイルライブラリ](file-library.md)
* [フォーラム](forum.md)
* [Q&amp;A](working-with-qna.md)

## クライアント側の基本事項 {#essentials-for-client-side}

### ソーシャルタグクラウド {#social-tag-cloud}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/commons/components/hbs/tagcloud</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>包含可能な</strong></a></td>
   <td>いいえ</td>
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
   <td>詳しくは、 <a href="tagcloud.md">Social タグクラウドの使用</a></td>
  </tr>
 </tbody>
</table>

* [クライアント側のカスタマイズ](client-customize.md)

## サーバー側の基本事項 {#essentials-for-server-side}

* [Social タグクラウド API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/tagcloud/api/package-summary.html)

* [Social タグマネージャー](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/tagging/package-summary.html)

* [サーバー側のカスタマイズ](server-customize.md)

## タグ検索 {#tag-searching}

現在 [機能パック 1](deploy-communities.md#latestfeaturepack) (FP1)、タグ検索は [タグのタイトル](../../help/sites-developing/framework.md#tag-characteristics).

FP1 以前は、 [タグ id](../../help/sites-developing/framework.md#tagid).
