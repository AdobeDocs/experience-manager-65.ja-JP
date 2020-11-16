---
title: ベストプラクティス
seo-title: ベストプラクティス
description: アドビのエンジニアリングチームとコンサルティングチームが管理者のために作成したベストプラクティスです。
seo-description: アドビのエンジニアリングチームとコンサルティングチームが管理者のために作成したベストプラクティスです。
uuid: 862d4fcf-ca61-4228-9344-b95a49b59b32
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8f6468a0-7721-454f-9334-c449968b8fe7
translation-type: tm+mt
source-git-commit: e594c53b2a26c1c9e484ac07220dc89c283cf7da
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 91%

---


# ベストプラクティス{#best-practices}

ベストプラクティスでは、AEM を可能な限り効率的かつ効果的に開発、管理または使用する方法を説明しています。AEM の様々な領域を対象としたトピックが順次追加されています。

次の領域について、ベストプラクティスに関するドキュメントが提供されています。

* [Assets](#assets)
* [Sites](#sites)

オーサリング、デプロイ、メンテナンスまたは開発のベストプラクティスについては、次のページを参照してください。

* [オーサリングのベストプラクティス](/help/sites-authoring/best-practices.md)
* [開発のベストプラクティス](/help/sites-developing/best-practices.md)
* [デプロイのベストプラクティス](/help/sites-deploying/best-practices.md)

以降の表では、特定のドキュメントの説明とリンクを示します。

## Assets {#assets}

ダイナミックメディア機能やダイナミックメディアクラシック統合を含む、アセットに関するベストプラクティスは、次の各トピックで説明されています。

<table>
 <tbody>
  <tr>
   <td>読み込み中のシステムの安定性とパフォーマンスを高めるための、アセットの周辺のさまざまな領域のベストプラクティス</td>
   <td><a href="/help/assets/best-practices-for-assets.md">Assets のベストプラクティス</a></td>
   <td>アセットに関する様々な領域のベストプラクティスガイドへのリンクが含まれています。 これらのガイドを確認すると、エンタープライズアセット管理システムを構築および管理する知識を習得し、そのツールを利用できるようになります。</td>
  </tr>
  <tr>
   <td>コンテンツの整理方法（フォルダー階層）</td>
   <td><a href="/help/assets/organize-assets.md">ファイル管理のベストプラクティス</a></td>
   <td>ビデオ、メタデータ、画像処理が常にフォルダーに適用されるので、処理プロファイルの多くはフォルダーに基づいています。このベストプラクティスドキュメントでは、フォルダー階層の定義およびセットアップ方法について説明します。フォルダー階層は、コンテンツの処理方法に大きく影響します。 </td>
  </tr>
  <tr>
   <td>Scene7 と AEM の統合</td>
   <td><a href="/help/sites-administering/scene7.md#best-practices-for-integrating-scene-with-aem">Scene7 と AEM の統合に関するベストプラクティス</a></td>
   <td><p>ポーリングインポーターを有効にすべき状況、統合を試す方法およびコンテンツブラウザーを使用すべき状況とアセットに直接アップロードすべき状況について説明します。</p> </td>
  </tr>
  <tr>
   <td>画像プリセットオプション</td>
   <td><a href="/help/assets/managing-image-presets.md#understanding-image-presets">画像プリセット</a>の概要および<a href="/help/assets/managing-image-presets.md#image-preset-options">画像プリセットのベストプラクティス</a></td>
   <td><a href="/help/assets/managing-image-presets.md">画像プリセットの管理</a>に関するドキュメントの一部として、これらのトピックでは画像プリセットの概要と、画像プリセットのオプションの選択に関するベストプラクティスについて説明します。</td>
  </tr>
  <tr>
   <td>ダイナミックメディアと、Scene7 の直接統合との比較</td>
   <td><a href="/help/sites-administering/scene7.md#aem-scene-integration-versus-dynamic-media">Scene7/AEM 統合と Dynamic Media の比較</a></td>
   <td>ダイナミックメディアソリューションの使用が適している状況、Scene7 と AEM を統合すべき状況またはその両方を使用すべき状況について説明します。</td>
  </tr>
 </tbody>
</table>

## Sites {#sites}

Web サイトコンテンツの管理と作成には、次に示すいくつかのベストプラクティスがあります。

<table>
 <tbody>
  <tr>
   <td>GDPR コンプライアンス</td>
   <td><a href="/help/sites-administering/gdpr-compliance-sites.md">AEM Sites GDPR コンプライアンス</a></td>
   <td>データのプライバシー権に関する EU 一般データ保護規則（GDPR）が 2018 年 5 月に発効します。AEM Sites は、GDPR に準拠しています。このページでは、AEM Sites での GDPR 要求の処理手順について詳しく説明します。プライベートデータの格納場所や、それらのデータを手動で、またはコードを使用して削除する方法について説明します。</td>
  </tr>
  <tr>
   <td>インスタンスのデフォルト UI の定義</td>
   <td><p><a href="/help/sites-authoring/select-ui.md#configuring-the-default-ui-for-your-instance">個別の例に合わせたデフォルト UI の設定</a></p> </td>
   <td>AEM には、タッチ操作向け UI とクラシック UI という 2 つの UI があります。ここでは、インスタンスのデフォルト UI の定義方法について詳しく説明します。</td>
  </tr>
  <tr>
   <td>マルチサイト管理</td>
   <td><a href="/help/sites-administering/msm-best-practices.md">MSM のベストプラクティス</a></td>
   <td>コンテンツのデプロイメントを自動化するための MSM の使用に関するベストプラクティスです。 </td>
  </tr>
  <tr>
   <td>コンテンツの翻訳</td>
   <td><a href="/help/sites-administering/tc-bp.md">翻訳のベストプラクティス</a></td>
   <td>複数言語に対応したサイトを計画および実装するためのベストプラクティスです。</td>
  </tr>
  <tr>
   <td>ユーザー管理</td>
   <td><a href="/help/sites-administering/security.md#best-practices">権限と特別な権限のベストプラクティス</a></td>
   <td>権限と特別な権限を使用する場合のベストプラクティスについて説明しています。 </td>
  </tr>
  <tr>
   <td>ワークフロー</td>
   <td><a href="/help/sites-developing/workflows-best-practices.md#configuration">ワークフローのベストプラクティス - 設定</a></td>
   <td>ワークフローを使用すると、Adobe Experience Manager（AEM）アクティビティを自動化し、AEM 環境で発生する大量のプロセスをワークフローで表現できます。したがって、ワークフローの実装の計画と設定は慎重におこなうことが強く推奨されます。</td>
  </tr>
 </tbody>
</table>

