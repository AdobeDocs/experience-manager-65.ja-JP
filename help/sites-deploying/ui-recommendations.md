---
title: 顧客向けのユーザーインターフェイスのレコメンデーション
description: クラシックユーザーインターフェイスおよびタッチ操作向けユーザーインターフェイスに関連する推奨事項のリスト。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
docset: aem65
exl-id: 7b71119a-ff58-47c0-aeef-a705ed8c40e0
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 8f638eb384bdca59fb6f4f8990643e64f34622ce
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 79%

---

# 顧客向けのユーザーインターフェイスのレコメンデーション{#user-interface-recommendations-for-customers}

Adobe Experience Manager には、統合された Experience Cloud UI（タッチ操作対応 UI とも呼ばれます）とクラシック UI の 2 つの UI が付属しています。

このドキュメントでは、状況に応じて顧客がどの UI の使用を選択する必要があるかについて説明します。

関連用語：

* **UI （または標準UI）**
テクノロジープレビューとして5.6.0に導入され、その後のリリースで拡張された最新のユーザーインターフェイス。 以前はタッチ操作向け UI またはタッチ UI と呼ばれていた Adobe Experience Cloud の統一されたユーザー体験を基盤としています。

* **クラシック UI**
2008年にCQ 5.1で導入されたExtJS技術に基づくユーザーインターフェイス。

* **サイト管理者**
サイト階層の管理（移動、アクティブ化、管理された参照）と新しいページの作成の機能。

* **ページオーサリング**
ページのコンテンツを追加/編集する機能。

* **DAM/Assets管理者**
デジタルアセット（画像、動画、ドキュメント、ダウンロードなど）を管理する機能。

* **ContextHub**
訪問者に関する情報を集約し、さまざまな目的で使用する機能。 サイトの訪問者をシミュレートするユーザーインターフェイスを備えています。 AEM 6.2 より、以前の ClientContext に代わって ContextHub が使用されています。

## 一般 {#general}

過去数年にわたり、アドビではすべての Adobe Experience Cloud ソリューションを統一されたユーザーインターフェイスに更新してきました。 Experience Cloud ソリューションのユーザーには、アプリケーションの使用および操作方法について共通のパターンを持つ一貫性のある体験が提供されます。 すべてのリリースで、様々なソリューションを使用している顧客からのフィードバックに基づいて、アドビはユーザーインターフェイスを改善しています。

2008年に導入され、バージョン 5.0 ～ 5.6.1を実行しているお客様が使用するAdobe Experience Manager（以前はCQ5として知られていました）の元のユーザーインターフェイスは、AEM 6.5にあります。 これにより、顧客は同じユーザーインターフェイスを使い続けながら、新しい機能を備えた更新されたプラットフォームのメリットを享受しながら、6.5に更新できます。

お客様には、2018 年または 2019 年に新しい UI への切り替えを予定することをお勧めしています。 この切り替えは、6.5 にアップデートするときに（またはアップデート後に個別のプロジェクトで）行うことができます。その際に、カスタマイズとコンポーネントダイアログの調整が必要になります。

クラシック UI は AEM 6.4 で廃止されました。アドビは今後クラシック UI を拡張する予定はありません。 クラシック UI は廃止中は引き続き完全にサポートされます。

### ルールとレコメンデーション {#rules-and-recommendations}

Adobe Experience Manager 6.5 に関する製品管理からの推奨事項を以下のリストに示します。

<table>
 <tbody>
  <tr>
   <th>マイプロジェクト</th>
   <th>レコメンデーション</th>
  </tr>
  <tr>
   <td>Adobe Experience Manager を使い始めようとしている。</td>
   <td>デフォルトの UI を使用する。</td>
  </tr>
  <tr>
   <td><p>AEM をしばらくの間使用している。</p> <p>製品の UI をそのまま使用していて、Sites のカスタムコンポーネントを開発している。<br /> </p> </td>
   <td>
    <ol>
     <li>6.5 へのアップデート</li>
     <li>サイト管理、アセットなどに既定のUIを使用する<br /> </li>
     <li>クラシック UI のページエディターを表示するよう「ページを編集」アクションを設定します。 <a href="#selecting-your-ui">UI の選択</a>を参照してください。</li>
    </ol> <p>次に第 2 段階として、</p>
    <ol>
     <li>Coral 3 ダイアログ形式を使用するようにコンポーネントダイアログを更新します。 アドビでは、コンポーネントの更新に <a href="/help/sites-developing/modernization-tools.md">AEM 最新化ツール</a>を使用することをお勧めします。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>統合により、ClientContext を使用するサイトを構築したことがある。<br /> </td>
   <td>
    <ol>
     <li>6.5 へのアップデート</li>
     <li>サイト管理、アセットなどにデフォルトのUIを使用します。</li>
     <li>クラシック UI のページエディターを表示するよう「ページを編集」アクションを設定します。 <a href="#selecting-your-ui">UI の選択</a>を参照してください。</li>
    </ol> <p>次に第 2 段階として、</p>
    <ol>
     <li>Coral 3 ダイアログ形式を使用するようにコンポーネントダイアログを更新します。 アドビでは、コンポーネントの更新に <a href="/help/sites-developing/modernization-tools.md">AEM 最新化ツール</a>を使用することをお勧めします。</li>
     <li>ContextHub（ClientContext の後継）を設定し、ContextHub を使用するようページテンプレートを更新します。 Context Hub には、カスタム ClientContext ストアの読み込みを許可する互換モードが用意されています。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><p>CQ／AEM を長年使用している。</p> <p>製品 UI（サイト管理者など）を拡張し、詳細な編集ダイアログでコンポーネントを構築したことがある。</p> </td>
   <td><p>6.5 にアップデートし、すべてのユーザーに対するページオーサリングのデフォルトとしてクラシック UI を設定します。 <a href="#selecting-your-ui">UI の選択</a>を参照してください。</p> <p>次に、プロジェクトを開始してカスタマイズを適用し、コンポーネントダイアログを Coral 3 形式で最適化します。 <a href="#resources-to-help">役に立つリソース</a>を参照してください。<br /> </p> </td>
  </tr>
 </tbody>
</table>

### UI の選択 {#selecting-your-ui}

システムを必要に応じて設定する方法について詳しくは、[UI の選択](/help/sites-authoring/select-ui.md)を参照してください。

### タッチ操作対応 UI のステータス {#touch-enabled-ui-status}

AEM 6.5 でのタッチ操作対応 UI の機能強化について詳しくは、リリースノートの[新機能](/help/release-notes/release-notes.md#what-s-new)を参照してください。

全体的な概要については、[タッチ操作対応 UI 機能のステータス](/help/release-notes/touch-ui-features-status.md)ページを参照してください。

### 役に立つリソース {#resources-to-help}

基本処理の背景情報については、以下を参照してください。

* [ページのオーサリング](/help/sites-authoring/page-authoring.md).

開発情報について詳しくは、以下を参照してください。

* [タッチ操作対応 UI のアーキテクチャ](/help/sites-developing/touch-ui-concepts.md)。
* [AEM 最新化ツール](/help/sites-developing/modernization-tools.md)を使用して、コンポーネントの編集ダイアログを、クラシック UI からタッチ操作対応 UI に変換します。

* [タッチ操作対応 UI の構造](/help/sites-developing/touch-ui-structure.md)

* [タッチ操作対応 UI のコンソールのカスタマイズ](/help/sites-developing/customizing-consoles-touch.md)（サンプルコードを含む）。

* [タッチ操作対応 UI のページオーサリングのカスタマイズ](/help/sites-developing/customizing-page-authoring-touch.md)（サンプルコードを含む）。

* [Granite UI ドキュメント](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)。
