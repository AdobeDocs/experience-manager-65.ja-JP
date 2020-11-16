---
title: デプロイのベストプラクティス
seo-title: デプロイのベストプラクティス
description: デプロイおよび保守のベストプラクティス。
seo-description: デプロイおよび保守のベストプラクティス。
uuid: 4546ed2c-43d5-40f3-874f-567b324e78c2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 4b5c0677-c630-4fae-867e-4f4583ac8507
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 73%

---


# デプロイのベストプラクティス{#deploying-best-practices}

デプロイのベストプラクティスでは、AEM を可能な限り効率的かつ効果的にデプロイまたは保守する方法を説明しています。AEM の様々な領域を対象としたトピックが順次追加されています。

次の領域について、ベストプラクティスのデプロイと保守、および推奨事項に関するドキュメントが提供されています。

* [Oak](#oak)
* [Communities](#communities)
* [UI](#ui)
* [パフォーマンス](#performance)

管理、デプロイまたはオーサリングのベストプラクティスについては、次のページを参照してください。

* [管理のベストプラクティス](/help/sites-administering/administer-best-practices.md)
* [開発のベストプラクティス](/help/sites-developing/best-practices.md)
* [オーサリングのベストプラクティス](/help/sites-authoring/best-practices.md)

以降の表では、特定のドキュメントの説明とリンクを示します。

## Oak {#oak}

[Oak](/help/sites-deploying/platform.md) は、AEM の基礎となっている、拡張性の高い高性能の階層コンテンツリポジトリです。

<table>
 <tbody>
  <tr>
   <td><p>スケーラビリティ、パフォーマンスおよびディザスタリカバリ</p> </td>
   <td><a href="/help/sites-deploying/performance.md">パフォーマンスとスケーラビリティ</a></td>
   <td>技術的即応性、高いパフォーマンスおよび安定したディザスタリカバリ機能について説明したホワイトペーパーを提供しています。</td>
  </tr>
  <tr>
   <td>推奨される Oak のデプロイメント</td>
   <td><a href="/help/sites-deploying/recommended-deploys.md">推奨されるデプロイメント</a></td>
   <td>デプロイメントシナリオについて説明します。</td>
  </tr>
  <tr>
   <td>Mongo トポロジ</td>
   <td><a href="/help/sites-deploying/recommended-deploys.md">Mongo トポロジのベストプラクティス</a></td>
   <td>Mongo トポロジについて、いつ、どのトポロジを使用するかを説明します。</td>
  </tr>
  <tr>
   <td>データストアオプション</td>
   <td><a href="/help/sites-deploying/data-store-config.md">ノードストアとデータストアの設定</a></td>
   <td>バイナリデータおよびコンテンツノードの格納に関連するベストプラクティスについて説明します。Amazon S3 データストアの使用に関する情報が含まれます。</td>
  </tr>
  <tr>
   <td>Oak 内の検索</td>
   <td><a href="/help/sites-deploying/best-practices-for-queries-and-indexing.md">クエリとインデックスに関するベストプラクティス</a><br /> </td>
   <td>コンテンツにインデックスを付ける方法のベストプラクティスについて説明します。</td>
  </tr>
 </tbody>
</table>

## Communities {#communities}

AEM Communitiesはオンプレミスコミュニティの作成と管理を簡素化します。 AEM Communitiesのベストプラクティスは以下のとおりです。

[コミュニティコンテンツストア](/help/communities/working-with-srp.md) — ユーザ生成コンテンツ(UGC)の新しい共有ストレージ機能と、基盤となる [トポロジを選択する際の考慮点について説明します](/help/communities/topologies.md)。

[コミュニティの推奨デプロイメント](/help/sites-deploying/recommended-deploys.md#considerations-for-aem-communities) - Communitiesの推奨デプロイメントについて説明します。 |

## UI {#ui}

ユーザーインターフェイスに関するベストプラクティスは、こちらで説明しています。

[顧客向けのユーザーインターフェイスの推奨事項](/help/sites-deploying/ui-recommendations.md)

AEMには現在2つのUIがあります。従来のUIとタッチ操作向けUIが同じリリースに含まれています。したがって、お客様は、プロジェクトの導入時にどの使用を行うかを決定する必要があります。このドキュメントは、適切な選択肢を見つけるのに役立ちます。

## パフォーマンス {#performance}

パフォーマンスに関するベストプラクティスを以下に挙げます。

<table>
 <tbody>
  <tr>
   <td>品質保証のベストプラクティス</td>
   <td><a href="/help/sites-deploying/configuring-performance.md#best-practices-for-quality-assurance">品質保証のベストプラクティス</a></td>
   <td>A standardized overview of the issues involved with defining a Test Concept specifically for performance tests on your <em>publish</em> environment. 主に QA エンジニア、プロジェクトマネージャーおよびシステム管理者向けの内容となっています。</td>
  </tr>
  <tr>
   <td>CDN での Dispatcher の使用</td>
   <td><a href="https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html#using-dispatcher-with-a-cdn">CDN での Dispatcher の使用</a></td>
   <td>Akamai Edge Delivery または Amazon Cloud Front などのコンテンツ配信ネットワーク（CDN）は、エンドユーザーに近い場所からコンテンツを配信します。</td>
  </tr>
  <tr>
   <td>パフォーマンスの最適化</td>
   <td><a href="/help/sites-deploying/configuring-performance.md">パフォーマンスの最適化</a></td>
   <td>Web サイトが訪問者の要求に応答するまでにどの程度の時間がかかるかは、非常に重要な問題です。</td>
  </tr>
  <tr>
   <td>パフォーマンステスト</td>
   <td><a href="/help/sites-deploying/best-practices-for-performance-testing.md">パフォーマンステストに関するベストプラクティス</a></td>
   <td>AEM のデプロイメントのパフォーマンステストを実行する際のベストプラクティスについて説明します。<br /> </td>
  </tr>
 </tbody>
</table>

