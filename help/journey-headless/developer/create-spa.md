---
title: オプション — Adobe Experience Managerを使用したシングルページアプリケーション (SPA) の作成方法
description: Adobe Experience Manager(AEM) ヘッドレス開発者ジャーニーのこのオプションの継続では、AEMでヘッドレス配信を従来のフルスタック CMS 機能と組み合わせる方法と、AEM SPA Editor フレームワークを使用して編集可能なSPAを作成する方法を学びます。
exl-id: 91eadda2-b881-4e4a-867f-8c5c54e8f8b4
source-git-commit: 3885cc51f7e821cdb352737336a29f9c4f0c2f41
workflow-type: tm+mt
source-wordcount: '1264'
ht-degree: 54%

---

# AEM で単一ページアプリケーション（SPA）を作成する方法 {#create-spa}

このオプションの継続では、 [AEMヘッドレス開発者ジャーニー、](overview.md) Adobe Experience Manager(AEM) がヘッドレス配信を従来のフルスタック CMS 機能と組み合わせる方法、およびAEM SPAエディターフレームワークを使用して編集可能なSPAを作成し、外部SPAを統合して、必要に応じて編集機能を有効にする方法を説明します。

## これまでの説明内容 {#story-so-far}

ここまでで、[AEM ヘッドレスデベロッパージャーニー](overview.md)をすべて完了し、AEM におけるヘッドレス配信の基本（以下の内容）を理解できました。

* ヘッドレスコンテンツ配信とヘッドフルコンテンツ配信の違い
* AEM のヘッドレス機能
* AEM ヘッドレスプロジェクトを編成する方法
* AEM でヘッドレスコンテンツを作成する方法
* AEM でヘッドレスコンテンツを取得および更新する方法
* AEM ヘッドレスプロジェクトの運用を開始する方法

これで、最初のAEMヘッドレスプロジェクトを利用した運用が開始されるか、またはその知識が得られました。 おめでとうございます。

それでは、ジャーニーの続編であるこのオプションパートになぜ取り組むのでしょうか。おそらく、 [はじめに](getting-started.md#integration-levels)AEMがヘッドレス配信と従来のフルスタックモデルをサポートするだけでなく、両方の利点を組み合わせたハイブリッドモデルをサポートする方法についても簡単に説明しました。 従来のヘッドレスモデルでは不可能ですが、このようなハイブリッドモデルでは、特定のプロジェクトに対して、かつてないほどの柔軟性をもたらすことができます。

この記事は、AEMで編集可能な独自のシングルページアプリケーション (SPA) を作成する方法を詳しく調べ、AEMヘッドレスに関するお客様の知識に基づいて構築されます。 この方法では、コンテンツを作成してSPAにヘッドレスに配信できますが、SPAはAEMで編集可能なままです。

## 目的 {#objective}

このドキュメントは、AEM SPA Editor フレームワークを使用して単一ページアプリケーションを開発する方法を理解するのに役立ちます。このドキュメントを読み終えると、次をできるようになります。

* SPA エディターの基本的な機能を理解する。
* 完全に編集可能な AEM 対応 SPA を作成するための要件がわかる。
* 外部 SPA を AEM に統合する方法を理解する。
* サーバーサイドレンダリングを実装する方法と実装しない方法を理解します。

## 要件と前提条件 {#requirements-prerequisites}

AEMでSPAの使用を開始する前に、いくつかの要件があります。

### 知識 {#knowledge}

* React または Angular フレームワークを使用した SPA の開発経験
* AEM の基本的なスキル - コンテンツフラグメントの作成とエディターの使用
* ドキュメントを必ず確認してください [AEMのヘッドフルとヘッドレス](/help/sites-developing/headful-headless.md) を参照して、可能な様々なレベルのSPA統合を理解してください。

### ツール {#tools}

* プロジェクトの導入をテストするためのサンドボックスへのアクセス
* ローカル開発モデリングとテスト用のデータインスタンス
* 既存の外部 SPA（オプション、選択した統合モデルによる）
* AEM プロジェクトアーキタイプ

## SPA について  {#what-is-a-spa}

単一ページアプリケーション (SPA) は、クライアントサイドでレンダリングされ、主に JavaScript 主導で、Ajax 呼び出しに依存してデータを読み込み、ページを動的に更新する点で、従来のページとは異なります。 ほぼすべてのコンテンツは、1 回のページ読み込みで 1 回取得され、ユーザーによるページとのやり取りに基づいて、必要に応じて追加のリソースが非同期に読み込まれます。

これにより、ページを更新する必要が減り、シームレスで高速な、ネイティブアプリのエクスペリエンスに近いものをユーザーに提供できます。

AEM SPA エディターを使用すると、フロントエンド開発者は AEM のサイトに統合できる SPA を作成でき、コンテンツ作成者は SPA コンテンツを他の AEM コンテンツと同様に簡単に編集できます。

## SPA が注目される理由  {#why-spa}

より速く、流動的で、よりネイティブアプリケーションのようになることで、SPAは、Web ページの訪問者だけでなく、SPAの仕組みの性質上、マーケターや開発者にとっても魅力的なエクスペリエンスになります。

SPA とその使用理由について詳しくは、[その他のリソース](#additional-resources)の節を参照して、詳細なドキュメントへのリンクをクリックしてください。

## AEM での SPA の処理方法

AEM で単一ページアプリケーションを開発する場合、フロントエンド開発者は SPA を作成する際に標準的なベストプラクティスを順守するものと想定します。フロントエンド開発者は、次の一般的なベストプラクティスとAEM固有の原則に従えば、SPAはAEMとコンテンツオーサリング機能と共に機能します。

* **移動可能** - その他のあらゆるコンポーネントと同様に、SPA コンポーネントは可能な限り移動可能な状態で構築する必要があります。SPA は、移動可能で再利用可能なコンポーネントを使用して構築する必要があります。
* **AEM Drives サイト構造**  — フロントエンド開発者はコンポーネントを作成し、内部構造を所有しますが、AEMを利用してサイトのコンテンツ構造を定義します。
* **動的レンダリング** - すべてのレンダリングは動的である必要があります。
* **動的ルーティング** - SPA がルーティングを担当し、AEM がリッスンしてそれに基づいて取得します。どのルーティングも動的である必要があります。

AEM での SPA の処理方法について詳しくは、[その他のリソース](#additional-resources)の節を参照して、詳細なドキュメントへのリンクをクリックしてください。

## AEM SPA Editor {#aem-spa-editor}

React やAngularなどの一般的なSPAフレームワークを使用して構築されたサイトは、動的 JSON を介してコンテンツを読み込むので、AEMページエディターで編集コントロールを配置するために必要なHTML構造は提供されません。

AEM 内で SPA の編集を有効にするには、SPA の JSON 出力と AEM リポジトリーのコンテンツモデルとの間でマッピングを行い、変更をコンテンツに保存できるようにする必要があります。

AEMでのSPAのサポートには、イベントの送信に使用できるページエディターに読み込まれる際にSPA JS コードとやり取りするシン JS レイヤーが導入され、編集コントロールの場所をアクティブにして、コンテキスト内編集が可能になります。 この機能は、SPAのコンテンツを Content Services を使用して読み込む必要があるので、Content Services API エンドポイントの概念に基づいて構築されます。

AEM SPA Editor について詳しくは、[その他のリソース](#additional-resources)の節を参照して、詳細なドキュメントへのリンクをクリックしてください。

## 既存の SPA への対応 {#existing-spas}

既存のSPAがある場合、AEMではAEMへの埋め込みがサポートされているので、AEMエディターでコンテンツ作成者に表示できます。 これは、コンテンツフラグメントを介して作成したコンテンツが、使用されるエンドアプリケーションのコンテキストで表示される場合に役立ちます。

また、AEM Editor 内で、特定の編集機能を外部SPAに対して有効にすることもできます。

RemotePage コンポーネントを使用すると、AEM で外部 SPA をレンダリングできます。

外部 SPA を AEM で編集可能にする方法について詳しくは、[その他のリソース](#additional-resources)の節を参照して、詳細なドキュメントへのリンクをクリックしてください。

## 次の手順 {#what-is-next}

独自の AEM 対応 SPA の開発に取りかかるには、次のドキュメントを確認してください。

* [SPA WKND チュートリアル](/help/sites-developing/spa-wknd.md)
* [React の使用を開始する](/help/sites-developing/spa-getting-started-react.md)
* [Angular の使用を開始する](/help/sites-developing/spa-getting-started-angular.md)

既存のSPAをAEMで使用するように適応させる必要がある場合は、次のドキュメントを確認します。

* [RemotePage コンポーネント](/help/sites-developing/spa-remote-page.md)
* [AEM 内での外部 SPA の編集](/help/sites-developing/spa-edit-external.md)

AEM の SPA トピックをさらに詳しく解説する[その他のリソース](#additional-resources)については、以下を参照してください。

## その他のリソース {#additional-resources}

以下の追加リソースでは、このドキュメントで言及したいくつかの概念について詳しく説明しています。

* [AEM におけるヘッドフルとヘッドレス](/help/sites-developing/headful-headless.md) - AEM で使用可能な様々な配信モデルの説明
* [SPA の概要およびガイド.](/help/sites-developing/spa-walkthrough.md) - AEM における SPA の優れた入門的解説
* [AEM 向け SPA の開発](/help/sites-developing/spa-architecture.md) - AEM 対応 SPA の開発方法に関するガイドライン
* [SPA エディターの概要](/help/sites-developing/spa-overview.md) - SPA エディターの仕組みの説明
* [サーバーサイドレンダリング](/help/sites-developing/spa-ssr.md) - SSR をAEM SPA用に設定する方法
* [SPA Reference Documents](/help/sites-developing/spa-reference-materials.md)  — オープンソースのAEM SPA GitHub プロジェクトへの JavaScript API リファレンスとリンク
* [コンテンツフラグメント](/help/assets/content-fragments/content-fragments.md) - コンテンツフラグメントの作成方法
* [AEM プロジェクトアーキタイプ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja) - Web サイトの出発点として、ベストプラクティスに基づいた最小限の Adobe Experience Manager（AEM）プロジェクトを作成する Maven テンプレート
