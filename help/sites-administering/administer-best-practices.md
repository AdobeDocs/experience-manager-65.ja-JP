---
title: 管理者が作業を開始しやすくするためのベストプラクティス
description: アドビのエンジニアリングチームとコンサルティングチームが管理者のために作成したベストプラクティスです。
uuid: 862d4fcf-ca61-4228-9344-b95a49b59b32
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8f6468a0-7721-454f-9334-c449968b8fe7
exl-id: 576d87c8-cc96-45a0-b3cf-defb440babbb
source-git-commit: 5bdf42d1ce7b2126bfb2670049deec4b6eaedba2
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 97%

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

特定のドキュメントの説明とリンクは、以下の表に示されています。

## Assets {#assets}

Dynamic Media 機能や Dynamic Media Classic 統合などの、Assets のベストプラクティスについては、次のトピックで説明されています。

<table>
 <tbody>
  <tr>
   <td>負荷時のシステムの安定性とパフォーマンスを向上を実現するための Assets における様々な領域でのベストプラクティス</td>
   <td><a href="/help/assets/best-practices-for-assets.md">Assets のベストプラクティス</a></td>
   <td>Assets に関する様々な領域でのベストプラクティスガイドへのリンクが記載されています。 これらのガイドを確認すると、エンタープライズアセット管理システムを構築および管理する知識を習得し、そのツールを利用できるようになります。</td>
  </tr>
  <tr>
   <td>コンテンツの整理方法（フォルダー階層）</td>
   <td><a href="/help/assets/organize-assets.md">ファイル管理のベストプラクティス</a></td>
   <td>ほとんどの処理プロファイルはフォルダーベースです。ビデオ、メタデータ、画像処理は常にフォルダーに適用されます。 このベストプラクティスドキュメントでは、フォルダー階層の定義およびセットアップ方法について説明します。フォルダー階層は、コンテンツの処理方法に大きく影響します。 </td>
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

Web サイトのコンテンツの管理とオーサリングには、次のようなベストプラクティスがあります。

<table>
 <tbody>
  <tr>
   <td>GDPR コンプライアンス</td>
   <td><a href="/help/sites-administering/gdpr-compliance-sites.md">AEM Sites GDPR コンプライアンス</a></td>
   <td>データのプライバシー権に関する EU 一般データ保護規則（GDPR）が 2018年5月に発効します。AEM Sites は GDPR に準拠しています。このページでは、AEM Sites での GDPR 要求の処理手順について詳しく説明します。プライベートデータの格納場所や、それらのデータを手動で、またはコードを使用して削除する方法について説明します。</td>
  </tr>
  <tr>
   <td>インスタンスのデフォルト UI の定義</td>
   <td><p><a href="/help/sites-authoring/select-ui.md#configuring-the-default-ui-for-your-instance">個別の例に合わせたデフォルト UI の設定</a></p> </td>
   <td>AEM には、タッチ操作向け UI とクラシック UI という 2 つの UI があります。この節では、個別の例に合わせたデフォルト UI の定義方法について詳しく説明します。</td>
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
