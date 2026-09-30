---
title: タグの基本事項
description: コミュニティコンポーネントがタグ付けを有効にして設定されている場合、コミュニティメンバーはパブリッシュ環境で投稿したコンテンツにタグ付けすることができます。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 6e8af8cf-1239-46f9-b2fe-4aa80abc86ea
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 9f5812d7b252bcf39896b4fbf2e3ac5c24bdb808
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 5%
---
# タグの基本事項 {#tag-essentials}

AEM Communities コンポーネントでタグ付けが有効になっている場合、コミュニティメンバーは、パブリッシュ環境で投稿したコンテンツにタグ付けすることができます。

パブリッシュ環境で適用されるタグの基礎となるインフラストラクチャは、ページやアセットなど、オーサー環境でコンテンツに適用されるタグと同じです。

* タグの作成と管理について詳しくは、[ タグの管理](../../help/sites-administering/tags.md)および[ ユーザー生成コンテンツのタグ付け](tag-ugc.md) （UGC）を参照してください。

* [ タグ付けフレームワーク ](../../help/sites-developing/framework.md)と、[ カスタムアプリケーション ](../../help/sites-developing/building.md)でのタグの追加と拡張について詳しくは、[開発者向けタグ付け](../../help/sites-developing/tags.md)を参照してください。

* パブリッシュ環境でUGCに適用されたタグをハイライト表示するために`social tag cloud` コンポーネントをページに追加する方法については、[ ソーシャルタグクラウドの使用](tagcloud.md)を参照してください。

UGCのタグ付けは、[ コミュニティサイト ](sites-console.md#tagging)または次のいずれかの機能を設定する際に有効にすることができます。

* [ブログ](blog-feature.md)
* [Calendar](calendar.md)
* [ファイルライブラリ](file-library.md)
* [フォーラム](forum.md)
* [Q&amp;A](working-with-qna.md)

## クライアントサイドの基本 {#essentials-for-client-side}

### ソーシャルタグクラウド {#social-tag-cloud}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/commons/components/hbs/tagcloud</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>包含可能</strong></a></td>
   <td>いいえ</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.tagcloud</td>
  </tr>
  <tr>
   <td> <strong> テンプレート </strong></td>
   <td> /libs/social/commons/components/hbs/tagcloud/tagcloud.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/commons/components/hbs/tagcloud/clientlibs/tagcloud.css</td>
  </tr>
  <tr>
   <td><strong>properties</strong></td>
   <td><a href="tagcloud.md"> ソーシャルタグクラウドの使用</a>を参照してください</td>
  </tr>
 </tbody>
</table>

* [クライアントサイドのカスタマイズ](client-customize.md)

## サーバーサイドの基本 {#essentials-for-server-side}

* [Social Tag Cloud API](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/javadoc/com/adobe/cq/social/commons/tagcloud/api/package-summary.html)

* [Social Tag Manager](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/javadoc/com/adobe/cq/social/commons/tagging/package-summary.html)

* [サーバーサイドのカスタマイズ](server-customize.md)

## タグ検索 {#tag-searching}

[機能パック 1](deploy-communities.md#latestfeaturepack) （FP1）の時点では、[ タグタイトル ](../../help/sites-developing/framework.md#tag-characteristics)を使用してタグ検索が実行されています。

FP1以前は、[ タグ ID](../../help/sites-developing/framework.md#tagid)を使用して検索を実行していました。
