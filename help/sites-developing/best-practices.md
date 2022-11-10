---
title: ベストプラクティス
seo-title: Best Practices
description: Adobe のエンジニアリングチームとコンサルティングチームは、AEM 開発者向けの包括的なベストプラクティスを策定しました
seo-description: Adobe Engineering and Consulting teams have developed a comprehensive set of best practices for AEM developers
uuid: f962c31f-8140-482f-b189-16376e23bfed
contentOwner: Justin Edelson
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 99678c1a-81f3-4fb3-bf73-98f0691c3fb6
exl-id: 0a478e80-c1b2-46c1-a6be-794d78b85d69
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 98%

---

# ベストプラクティス{#best-practices}

## 開発者向けのベストプラクティス - はじめに {#best-practices-for-developers-getting-started}

アドビのエンジニアリングチームとコンサルティングチームは、AEM 開発者向けの包括的なベストプラクティスを策定しました。Adobe の開発者は、これらのベストプラクティスに沿って、中核となる AEM 製品の更新やお客様の実装に合わせたカスタムコードを開発しています。

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

具体的なドキュメントについては、後述の表に説明とリンクを示します。

管理、デプロイとメンテナンスまたはオーサリングのベストプラクティスについては、次のページを参照してください。

* [ベストプラクティスの管理](/help/sites-administering/administer-best-practices.md)
* [オーサリングのベストプラクティス](/help/sites-authoring/best-practices.md)
* [デプロイのベストプラクティス](/help/sites-deploying/best-practices.md)

## サイト {#sites}

Web サイトコンテンツの管理と作成には、次に示すいくつかのベストプラクティスがあります。

<table>
 <tbody>
  <tr>
   <td>標準のタッチ操作対応 UI の基本となる概念</td>
   <td><p><a href="/help/sites-developing/touch-ui-concepts.md">タッチ操作対応 UI：概念</a></p> <p><a href="/help/sites-developing/touch-ui-structure.md">タッチ操作対応 UI：構造</a></p> </td>
   <td>タッチ操作対応 UI の概念および構造の概要を説明しています。</td>
  </tr>
  <tr>
   <td>タッチ対応 UI：コンソールのカスタマイズ </td>
   <td><a href="/help/sites-developing/customizing-consoles-touch.md">タッチ操作対応 UI のコンソールのカスタマイズ</a></td>
   <td>タッチ操作対応 UI のコンソールを拡張するための最適な方法を説明しています。</td>
  </tr>
  <tr>
   <td>タッチ操作対応 UI：ページオーサリングのカスタマイズ</td>
   <td><a href="/help/sites-developing/customizing-page-authoring-touch.md">タッチ操作対応 UI のページオーサリングのカスタマイズ</a></td>
   <td>タッチ操作対応 UI のページオーサリングを拡張する方法を説明しています。</td>
  </tr>
  <tr>
   <td>ワークフロー</td>
   <td><a href="/help/sites-developing/workflows-best-practices.md">ワークフローの作成と拡張</a></td>
   <td><p>ワークフローを利用すると、Adobe Experience Manager（AEM）のアクティビティを自動化し、AEM 環境内でおこなわれる大量の処理を表現できるので、ワークフローを導入する際は入念にプランを立てることを強くお勧めします。</p> </td>
  </tr>
 </tbody>
</table>

## コミュニティ {#communities}

[AEM Communities](/help/communities/overview.md) を使用すると、オンプレミスのコミュニティの作成と管理が容易になります。

Communities のベストプラクティスは、こちらで説明しています。

|  |  |  |
|---|---|---|
| ユーザー生成コンテンツ（UGC）の操作に関するベストプラクティス | [コーディングのガイドライン](/help/communities/code-guide.md) | [ソーシャルコンポーネントフレームワーク](/help/communities/scf.md)（SCF）のための、柔軟で移植性の高いコードを開発するためのガイドラインです。 |
| Communities コンポーネントの使用例 | [コミュニティコンポーネントガイド](/help/communities/components-guide.md) | インタラクティブな開発ツールです。 |

## ツール／HTL {#tooling-htl}

HTML Template Language（HTL）は、AEM 6.0 で導入された新しい HTML テンプレートシステムです。JSP や ESP に代わって、AEM ではこのテンプレートシステムが推奨されます。

|  |  |  |
|---|---|---|
| HTL の概要 | [HTL の概要と構文](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html) | このドキュメントでは、HTL とは何か、HTL に移行する方法、サンプルプロジェクト、構文、式およびステートメントを説明しています。 |
| Java での API の使用 | [HTL Java Use-API](https://helpx.adobe.com/jp/experience-manager/htl/using/use-api.html) | HTL Java Use-API を使用すると、HTL ファイルからカスタム Java クラスのヘルパーメソッドへのアクセスが可能になります。 |

>[!NOTE]
>
>次の複数パートのチュートリアルでは、新しい AEM プロジェクトを設定するためのベストプラクティスとして、コアコンポーネント、編集可能なテンプレート、クライアントライブラリ、コンポーネント開発について説明します。
>[AEM Sites の概要 - WKND チュートリアル](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop.html)
