---
title: デプロイのベストプラクティス
description: 可能な限り効率的かつ最も効果的に Adobe Experience Manager（AEM）をデプロイおよび保持する方法について説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 4cbc0a30-d5f6-40ff-b7f6-8d64762e1970
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 100%

---

# デプロイのベストプラクティス{#deploying-best-practices}

デプロイのベストプラクティスでは、可能な限り効率的かつ最も効果的に Adobe Experience Manager（AEM）をデプロイおよび保持する方法について説明します。このトピックのリストには、AEM の様々な領域が含まれています。

次の領域では、ベストプラクティスのデプロイと保守、およびレコメンデーションに関するドキュメントが提供されています。

* [Oak](#oak)
* [Communities](#communities)
* [UI](#ui)
* [パフォーマンス](#performance)

管理、開発、オーサリングのベストプラクティスについては、次のページを参照してください。

* [管理のベストプラクティス](/help/sites-administering/administer-best-practices.md)
* [開発のベストプラクティス](/help/sites-developing/best-practices.md)
* [オーサリングのベストプラクティス](/help/sites-authoring/best-practices.md)

特定のドキュメントの説明とリンクは、以下の表に示されています。

## Oak {#oak}

[Oak](/help/sites-deploying/platform.md) は、AEM の基礎となっている、拡張性が高く、パフォーマンスに優れた階層コンテンツリポジトリです。

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
   <td>このドキュメントでは、バイナリデータおよびコンテンツノードの格納に関連するベストプラクティスについて説明します。Amazon S3 データストアの使用に関する情報が含まれます。</td>
  </tr>
  <tr>
   <td>Oak 内の検索</td>
   <td><a href="/help/sites-deploying/best-practices-for-queries-and-indexing.md">クエリとインデックス作成のベストプラクティス</a><br /> </td>
   <td>コンテンツにインデックスを付ける方法のベストプラクティスについて説明します。</td>
  </tr>
 </tbody>
</table>

## Communities {#communities}

AEM Communities を使用すると、オンプレミスのコミュニティの作成と管理が容易になります。AEM Communities のベストプラクティスは、こちらで説明しています。

[コミュニティコンテンツストア](/help/communities/working-with-srp.md) - ユーザー生成コンテンツ（UGC）のための新しい共有ストレージ機能と、基盤となる[トポロジ](/help/communities/topologies.md)の選択に関する考察について説明しています。

[コミュニティの推奨デプロイメント](/help/sites-deploying/recommended-deploys.md#considerations-for-aem-communities) - Communities の推奨されるデプロイメントについて説明します。|

## UI {#ui}

ユーザーインターフェイスに関するベストプラクティスは、こちらで説明しています。

[顧客向けのユーザーインターフェイスのレコメンデーション](/help/sites-deploying/ui-recommendations.md)

AEM には現在、クラシック UI とタッチ操作向け UI の 2 つが同じリリースに含まれています。そのため、どちらを使用するかを、プロジェクトの実装時にユーザーが決断する必要があります。このドキュメントは、適切な選択肢を見つける際に役立ちます。

## パフォーマンス {#performance}

パフォーマンスに関するベストプラクティスを以下に挙げます。

<table>
 <tbody>
  <tr>
   <td>品質保証のベストプラクティス</td>
   <td><a href="/help/sites-deploying/configuring-performance.md#best-practices-for-quality-assurance">品質保証のベストプラクティス</a></td>
   <td>特に<em>パブリッシュ</em>環境のパフォーマンステストのテストコンセプトを定義する際の問題を標準的な観点から概説します。主に QA エンジニア、プロジェクトマネージャー、システム管理者向けの内容となっています。</td>
  </tr>
  <tr>
   <td>CDN での Dispatcher の使用</td>
   <td><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=ja#using-dispatcher-with-a-cdn">CDN での Dispatcher の使用</a></td>
   <td>Akamai Edge Delivery または Amazon Cloud Front などのコンテンツ配信ネットワーク（CDN）は、エンドユーザーに近い場所からコンテンツを配信します。</td>
  </tr>
  <tr>
   <td>パフォーマンスの最適化</td>
   <td><a href="/help/sites-deploying/configuring-performance.md">パフォーマンスの最適化</a></td>
   <td>Web サイトが訪問者の要求に応答するまでにどの程度の時間がかかるかは、非常に重要な問題です。</td>
  </tr>
  <tr>
   <td>パフォーマンステスト</td>
   <td><a href="/help/sites-deploying/best-practices-for-performance-testing.md">パフォーマンステストのベストプラクティス</a></td>
   <td>AEM のデプロイメントのパフォーマンステストを実行する際のベストプラクティスについて説明します。<br /> </td>
  </tr>
 </tbody>
</table>
