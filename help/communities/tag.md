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

* タグの作成と管理については、[タグ](../../help/sites-administering/tags.md)と[ユーザ生成コンテンツのタグ付け](tag-ugc.md)(UGC)を参照してください。

* [タグ付けフレームワーク](../../help/sites-developing/framework.md)の詳細については、[開発者のタグ付け](../../help/sites-developing/tags.md)を参照してください。また、[カスタムアプリケーション](../../help/sites-developing/building.md)にタグを含めたり、タグを拡張したりする方法についても説明します。

* 発行環境で`social tag cloud`コンポーネントをページに追加してUGCに適用されたタグを強調表示する方法については、「[Social Tag Cloud](tagcloud.md)の使用」を参照してください。

* カタログのリソースをタグ付けする方法については、[イネーブルメントリソースのタグ付け](tag-resources.md)を参照してください。

UGC のタグ付けは、[コミュニティサイト](sites-console.md#tagging)または次のいずれかの機能を設定する際に有効化することができます。

* [ブログ](blog-feature.md)
* [カレンダー](calendar.md)
* [ファイルライブラリ](file-library.md)
* [フォーラム](forum.md)
* [Q&amp;A](working-with-qna.md)

## クライアント側の基本事項  {#essentials-for-client-side}

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
   <td>「<a href="tagcloud.md">Socialタグクラウドの使用</a>」を参照してください。</td>
  </tr>
 </tbody>
</table>

* [クライアント側のカスタマイズ](client-customize.md)

## サーバー側の基本事項  {#essentials-for-server-side}

* [Social タグクラウド API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/tagcloud/api/package-summary.html)

* [Social タグマネージャー](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/tagging/package-summary.html)

* [サーバー側のカスタマイズ](server-customize.md)

## タグの検索 {#tag-searching}

[機能パック 1](deploy-communities.md#latestfeaturepack)（FP1）以降では、[タグタイトル](../../help/sites-developing/framework.md#tag-characteristics)を使用して、タグの検索を実行します。

FP1 より前では、[タグ ID](../../help/sites-developing/framework.md#tagid) を使用して、タグの検索を実行していました。
