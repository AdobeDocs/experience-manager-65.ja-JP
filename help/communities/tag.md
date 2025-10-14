---
title: タグの基本事項
description: タグ付けが有効になっている状態で Communities コンポーネントが設定され、コミュニティメンバーがパブリッシュ環境で投稿したコンテンツにタグ付けできる場合について説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 6e8af8cf-1239-46f9-b2fe-4aa80abc86ea
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 5%

---

# タグの基本事項 {#tag-essentials}

タグ付けが有効になっている状態でAEM Communities コンポーネントが設定されると、コミュニティメンバーは、パブリッシュ環境で投稿するコンテンツにタグを付けることができます。

パブリッシュ環境で適用されるタグの基盤となるインフラストラクチャは、ページやアセットなど、オーサー環境のコンテンツに適用されるタグの基盤となるインフラストラクチャと同じです。

* タグの作成と管理については、[&#x200B; タグの管理 &#x200B;](../../help/sites-administering/tags.md) および [&#x200B; ユーザー生成コンテンツのタグ付け &#x200B;](tag-ugc.md) （UGC）を参照してください。

* [&#x200B; タグ付けフレームワーク &#x200B;](../../help/sites-developing/tags.md)、および [&#x200B; カスタムアプリケーション &#x200B;](../../help/sites-developing/building.md) にタグの追加と拡張を行う方法について詳しくは [&#128279;](../../help/sites-developing/framework.md) 開発者のためのタグ付け  を参照してください。

* パブリッシュ環境で UGC に適用されたタグをハイライト表示するために `social tag cloud` コンポーネントをページに追加する方法についてオーサー向けに詳しくは、[&#x200B; ソーシャルタグクラウドの使用 &#x200B;](tagcloud.md) を参照してください。

UGC のタグ付けは、（コミュニティサイト [&#x200B; または次のいずれかの機能を設定する際に有効にするこ &#x200B;](sites-console.md#tagging) ができます。

* [ブログ](blog-feature.md)
* [Calendar](calendar.md)
* [ファイルライブラリ](file-library.md)
* [フォーラム](forum.md)
* [Q&amp;A](working-with-qna.md)

## クライアントサイドの基本事項 {#essentials-for-client-side}

### ソーシャルタグクラウド {#social-tag-cloud}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/commons/components/hbs/tagcloud</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong> 含む </strong></a></td>
   <td>いいえ</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientlibs</strong></a></td>
   <td>cq.social.hbs.tagcloud</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/commons/components/hbs/tagcloud/tagcloud.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/commons/components/hbs/tagcloud/clientlibs/tagcloud.css</td>
  </tr>
  <tr>
   <td><strong>properties</strong></td>
   <td>詳しくは <a href="tagcloud.md"> ソーシャルタグクラウドの使用 </a> を参照してください。</td>
  </tr>
 </tbody>
</table>

* [クライアントサイドのカスタマイズ](client-customize.md)

## サーバーサイドの初期設定 {#essentials-for-server-side}

* [Social Tag Cloud API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/commons/tagcloud/api/package-summary.html)

* [&#x200B; ソーシャルタグマネージャー &#x200B;](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/commons/tagging/package-summary.html)

* [サーバーサイドのカスタマイズ](server-customize.md)

## タグ検索 {#tag-searching}

[&#x200B; 機能パック 1](deploy-communities.md#latestfeaturepack) （FP1）の時点では、[&#x200B; タグタイトル &#x200B;](../../help/sites-developing/framework.md#tag-characteristics) を使用してタグ検索が実行されています。

FP1 より前は、[&#x200B; タグ ID](../../help/sites-developing/framework.md#tagid) を使用して検索が実行されていました。
