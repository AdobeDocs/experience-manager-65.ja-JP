---
title: AEM 開発者向けのベストプラクティス
description: アドビのエンジニアリングチームとコンサルティングチームは、AEM 開発者向けの包括的なベストプラクティスを策定しました。
contentOwner: Justin Edelson
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 0a478e80-c1b2-46c1-a6be-794d78b85d69
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 100%

---

# ベストプラクティス{#best-practices}

## 開発者向けのベストプラクティス - はじめに {#best-practices-for-developers-getting-started}

アドビのエンジニアリングチームとコンサルティングチームは、AEM 開発者向けの包括的なベストプラクティスを策定しました。アドビの開発者は、コアとなる AEM 製品のアップデートと顧客実装のための顧客コードを開発する際に、これらのベストプラクティスに従ってください。

AEM 開発プロジェクトを開始する前に、まず、次のベストプラクティスを確認してください。

* [開発の手法](/help/sites-developing/development-practices.md)
* [コンテンツのアーキテクチャ](/help/sites-developing/content-architecture.md)
* [ソフトウェアのアーキテクチャ](/help/sites-developing/software-architecture.md)
* [コーディングのヒント](/help/sites-developing/coding-tips.md)
* [コードの落とし穴](/help/sites-developing/code-pitfalls.md)
* [JCR 統合](/help/sites-developing/jcr-integration.md)
* [OSGi バンドル](/help/sites-developing/osgi-bundles.md)
* [Java API のベストプラクティス](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/understand-java-api-best-practices.html?lang=ja)

### ベストプラクティスに関する追加情報 {#additional-best-practices-information}

次の領域について、開発のベストプラクティスに特有のドキュメントが提供されています。

* [Sites](#sites)
* [Communities](/help/sites-developing/best-practices.md#communities)
* [ツール／HTL](/help/sites-developing/best-practices.md#tooling-htl)

特定のドキュメントの説明とリンクは、以下の表に示されています。

管理、デプロイ、メンテナンス、オーサリングのベストプラクティスについては、次のページのいずれかを参照してください。

* [ベストプラクティスの管理](/help/sites-administering/administer-best-practices.md)
* [オーサリングのベストプラクティス](/help/sites-authoring/best-practices.md)
* [デプロイのベストプラクティス](/help/sites-deploying/best-practices.md)

## Sites {#sites}

web サイトのコンテンツの管理とオーサリングには、次のようなベストプラクティスがあります。

<table>
 <tbody>
  <tr>
   <td>標準のタッチ操作対応 UI の基本となっている一部の理論。</td>
   <td><p><a href="/help/sites-developing/touch-ui-concepts.md">タッチ操作対応 UI：概念</a></p> <p><a href="/help/sites-developing/touch-ui-structure.md">タッチ操作対応 UI：構造</a></p> </td>
   <td>タッチ操作対応 UI の概念および構造の概要を説明しています。</td>
  </tr>
  <tr>
   <td>タッチ対応 UI：コンソールのカスタマイズ </td>
   <td><a href="/help/sites-developing/customizing-consoles-touch.md">タッチ操作対応 UI のコンソールのカスタマイズ</a></td>
   <td>このドキュメントでは、タッチ操作対応 UI のコンソールを拡張する最適な方法について説明します。</td>
  </tr>
  <tr>
   <td>タッチ操作対応 UI：ページオーサリングのカスタマイズ</td>
   <td><a href="/help/sites-developing/customizing-page-authoring-touch.md">タッチ操作対応 UI のページオーサリングのカスタマイズ</a></td>
   <td>タッチ操作対応 UI 用にページオーサリングを拡張する方法について説明します。</td>
  </tr>
  <tr>
   <td>ワークフロー</td>
   <td><a href="/help/sites-developing/workflows-best-practices.md">ワークフローの作成と拡張</a></td>
   <td><p>ワークフローを使用すると、Adobe Experience Manager（AEM）アクティビティを自動化し、AEM 環境で発生する大量の処理を表現できるため、ワークフローの実装は慎重に計画するようにしてください。</p> </td>
  </tr>
 </tbody>
</table>

## Communities {#communities}

[AEM Communities](/help/communities/overview.md) を使用すると、オンプレミスのコミュニティの作成と管理が容易になります。

Communities のベストプラクティスは、こちらで説明しています。

|  |  |  |
|---|---|---|
| ユーザー生成コンテンツ（UGC）の操作に関するベストプラクティス | [コーディングのガイドライン](/help/communities/code-guide.md) | [ソーシャルコンポーネントフレームワーク](/help/communities/scf.md)（SCF）のための、柔軟で移植性の高いコードを開発するためのガイドラインです。 |
| Communities コンポーネントの使用例 | [コミュニティコンポーネントガイド](/help/communities/components-guide.md) | インタラクティブな開発ツールです。 |

## ツール／HTL {#tooling-htl}

HTML テンプレート言語（HTL）は、AEM 6.0 で導入された新しい HTML テンプレートシステムです。JSP と ESP に代わり、AEM で推奨されるテンプレートシステムになります。

|  |  |  |
|---|---|---|
| HTL の概要 | [HTL の概要と構文](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=ja) | このドキュメントでは、HTL の概要、HTL への移行方法、サンプルプロジェクト、構文、式、ステートメントについて説明します |
| Java での API の使用 | [HTL Java Use-API](https://helpx.adobe.com/jp/experience-manager/htl/using/use-api.html) | HTL Java Use-API を使用すると、HTL ファイルからカスタム Java クラスのヘルパーメソッドへのアクセスが可能になります。 |

>[!NOTE]
>
>次の複数パートのチュートリアルでは、新しい AEM プロジェクトを設定するためのベストプラクティスとして、コアコンポーネント、編集可能なテンプレート、クライアントライブラリ、コンポーネント開発について説明します。
>[AEM Sites の概要 - WKND チュートリアル](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop.html)
