---
title: 顧客向けのユーザーインターフェイスのレコメンデーション
description: 従来のユーザーインターフェイスとタッチ操作向けのユーザーインターフェイスに関連する推奨事項のリストです。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
docset: aem65
exl-id: 7b71119a-ff58-47c0-aeef-a705ed8c40e0
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 30%

---

# 顧客向けのユーザーインターフェイスのレコメンデーション{#user-interface-recommendations-for-customers}

Adobe Experience Managerには、統合Experience CloudUI（タッチ操作対応 UI とも呼ばれます）とクラシック UI の 2 つの UI が用意されています。

このドキュメントは、お客様が状況に応じて使用する UI を選択できるようにガイドすることを目的としています。

目標条件：

* **UI（または標準の UI）** 5.6.0 でテクノロジープレビューとして導入され、以降のリリースで拡張された最新のユーザーインターフェイス。以前はタッチ操作向け UI またはタッチ UI と呼ばれていた Adobe Experience Cloud の統一されたユーザー体験を基盤としています。

* **クラシック UI**
2008 年の CQ 5.1 で導入された、ExtJS テクノロジーに基づくユーザーインターフェイス。

* **サイト管理者**
サイトの階層を管理（参照を移動、アクティベート、管理）して、新しいページを作成する機能。

* **ページオーサリング**
ページのコンテンツを追加および編集する機能。

* **DAM／アセット管理者**
デジタルアセット（画像、ビデオ、ドキュメント、ダウンロードを含む）を管理する機能。

* **ContextHub**&#x200B;訪問者に関する情報を集計し、様々な目的で使用する機能。サイトの訪問者をシミュレートするユーザーインターフェイスを備えています。AEM 6.2 より、以前の ClientContext に代わって ContextHub が使用されています。

## 一般 {#general}

過去数年の間に、Adobeは、すべてのAdobe Experience Cloudソリューションを統合ユーザーインターフェイスで更新しました。 Experience Cloud・ソリューションをまたいだユーザーは、アプリケーションの使用と運用に関する共通のパターンに基づいて、一貫した経験を得ることができます。 各リリースでは、Adobeは、様々なソリューションをまたいで作業しているお客様からのフィードバックに基づいて、ユーザーインターフェイスを絞り込んでいます。

2008 年に導入され、バージョン 5.0 ～ 5.6.1 を実行しているお客様が使用する、Adobe Experience Manager（旧称 CQ5）の元のユーザーインターフェイスは、AEM 6.5 に存在します。これにより、お客様は 6.5 に更新でき、同じユーザーインターフェイスを使用し続けながら、新しい機能を備えた更新済みプラットフォームのメリットを享受できます。

Adobeでは、2018/19で新しい UI への切り替えを計画することをお勧めします。 これは、6.5 へのアップデート中に実行することも、アップデート後の別のプロジェクトで実行することもできます。この場合、カスタマイズとコンポーネントダイアログに対する必要な調整が含まれます。

クラシック UI はAEM 6.4 で非推奨となり、Adobeはクラシック UI のそれ以上の機能強化を予定していません。 クラシック UI は廃止中は引き続き完全にサポートされます。

### ルールとレコメンデーション {#rules-and-recommendations}

Adobe Experience Manager 6.5 の製品管理からの推奨事項を次に示します。

<table>
 <tbody>
  <tr>
   <th>私のプロジェクト…</th>
   <th>レコメンデーション</th>
  </tr>
  <tr>
   <td>Adobe Experience Managerを使い始めたばかりです。</td>
   <td>デフォルトの UI を使用します。</td>
  </tr>
  <tr>
   <td><p>しばらくAEMを使用しています。</p> <p>標準搭載の製品 UI を使用し、サイト用のカスタムコンポーネントを開発しました。<br /> </p> </td>
   <td>
    <ol>
     <li>6.5 に更新しました。</li>
     <li>サイト管理やアセットなどにデフォルトの UI を使用します。 等。<br /> </li>
     <li>「ページを編集」アクションを設定して、クラシック UI のページエディターを開きます。 詳しくは、 <a href="#selecting-your-ui">UI の選択</a>.</li>
    </ol> <p>次に、第 2 段階で、次のようになります。</p>
    <ol>
     <li>Coral 3 ダイアログ形式を使用するようにコンポーネントダイアログを更新します。 Adobeは、 <a href="/help/sites-developing/modernization-tools.md">AEM Modernization Tools</a> をクリックして、コンポーネントを更新します。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>統合により、ClientContext を使用するサイトを構築したことがある。<br /> </td>
   <td>
    <ol>
     <li>6.5 に更新しました。</li>
     <li>サイト管理やアセットなどにデフォルトの UI を使用します。 等。</li>
     <li>「ページを編集」アクションを設定して、クラシック UI のページエディターを開きます。 詳しくは、 <a href="#selecting-your-ui">UI の選択</a>.</li>
    </ol> <p>次に、第 2 段階で、次のようになります。</p>
    <ol>
     <li>Coral 3 ダイアログ形式を使用するようにコンポーネントダイアログを更新します。 Adobeは、 <a href="/help/sites-developing/modernization-tools.md">AEM Modernization Tools</a> をクリックして、コンポーネントを更新します。</li>
     <li>ContextHub を設定し (ClientContextの代わり )、ContextHub を使用するようにページテンプレートを更新します。 ContextHub には、カスタムモードストアを読み込むことができる互換性ClientContextがあります。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><p>CQ/AEMを長年使用しています。</p> <p>製品 UI（Site Admin など）を拡張し、広範な編集ダイアログを使用してコンポーネントを構築済み。</p> </td>
   <td><p>6.5 に更新し、すべてのユーザーのページオーサリングのデフォルトとしてクラシック UI を設定します。 詳しくは、 <a href="#selecting-your-ui">UI の選択</a>.</p> <p>次に、プロジェクトを開始してカスタマイズを適用し、Coral 3 形式のコンポーネントダイアログを最適化します。 詳しくは、 <a href="#resources-to-help">役立つリソース</a>.<br /> </p> </td>
  </tr>
 </tbody>
</table>

### FAQ {#faq}

ナレッジベースの記事を参照してください。 [タッチ操作対応 UI オーサリングに関する FAQ](https://helpx.adobe.com/jp/experience-manager/kb/index/touchui_faq.html)（クラシック UI の廃止予定に関する情報など）

### UI の選択 {#selecting-your-ui}

システムを必要に応じて設定する方法について詳しくは、[UI の選択](/help/sites-authoring/select-ui.md)を参照してください。

### タッチ操作対応 UI のステータス {#touch-enabled-ui-status}

AEM 6.5 でのタッチ操作対応 UI の機能強化について詳しくは、 [新機能](/help/release-notes/release-notes.md#what-s-new) 」を参照してください。

全体的な概要については、[タッチ操作対応 UI 機能のステータス](/help/release-notes/touch-ui-features-status.md)ページを参照してください。

### 役立つリソース {#resources-to-help}

基本操作の背景情報は次のとおりです。

* [ページのオーサリング](/help/sites-authoring/page-authoring.md).

開発に関する詳細な情報は、次のとおりです。

* [タッチ操作対応 UI のアーキテクチャ](/help/sites-developing/touch-ui-concepts.md).
* [AEM 最新化ツール](/help/sites-developing/modernization-tools.md)を使用して、コンポーネントの編集ダイアログを、クラシック UI からタッチ操作対応 UI に変換します。

* [タッチ操作対応 UI の構造](/help/sites-developing/touch-ui-structure.md)

* [タッチ操作対応 UI のコンソールのカスタマイズ](/help/sites-developing/customizing-consoles-touch.md)（サンプルコードを含む）。

* [タッチ操作対応 UI のページオーサリングのカスタマイズ](/help/sites-developing/customizing-page-authoring-touch.md)（サンプルコードを含む）。

* [Granite UI ドキュメント](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)。
