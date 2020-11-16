---
title: 顧客向けのユーザーインターフェイスの推奨事項
seo-title: 顧客向けのユーザーインターフェイスの推奨事項
description: クラシックユーザーインターフェイスおよびタッチ操作向けユーザーインターフェイスに関連する推奨事項のリスト。
seo-description: クラシックユーザーインターフェイスおよびタッチ操作向けユーザーインターフェイスに関連する推奨事項のリスト。
uuid: 9ec2c9de-a79e-4f2c-a90f-b38ba9553e07
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8f06d4b6-7d30-4ebc-9c6a-3bb8607a9be8
docset: aem65
translation-type: tm+mt
source-git-commit: 5597fb39500ac1f85d03263bfa1e5239d35d2a2c
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 99%

---


# 顧客向けのユーザーインターフェイスの推奨事項{#user-interface-recommendations-for-customers}

Adobe Experience Manager には、統合された Experience Cloud UI（タッチ操作対応 UI とも呼ばれます）とクラシック UI の2 つの UI が付属しています。

ここでは、状況に応じて顧客がどの UI の使用を選択する必要があるかについて説明します。

関連用語：

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

過去数年にわたり、アドビではすべての Adobe Experience Cloud ソリューションを統一されたユーザーインターフェイスに更新してきました。Experience Cloud ソリューションのユーザーには、アプリケーションの使用および操作方法について共通のパターンを持つ一貫性のある体験が提供されます。すべてのリリースで、様々なソリューションを使用している顧客からのフィードバックに基づいて、アドビはユーザーインターフェイスを改善しています。

2008 年に登場し、Adobe Experience Manager（旧称 CQ5）のバージョン 5.0 ～ 5.6.1 で使用されていた元のユーザーインターフェイスも、引き続き AEM 6.5 に残されています。そのため、6.5 にアップデートしても、従来と同じユーザーインターフェイスを使用して、新しい機能を含むアップデートされたプラットフォームを利用することができます。

お客様には、2018 年または 2019 年に新しい UI への切り替えを予定することをお勧めしています。この切り替えは、6.5 にアップデートするときに（またはアップデート後に個別のプロジェクトで）おこなうことができます。その際に、カスタマイズとコンポーネントダイアログの調整が必要になります。

クラシック UI は AEM 6.4 で廃止されました。Adobe は今後クラシック UI を拡張する予定はありません。クラシック UI は廃止中は引き続き完全にサポートされます。

### ルールと推奨事項 {#rules-and-recommendations}

Adobe Experience Manager 6.5 に関する製品管理からの推奨事項を以下のリストに示します。

<table>
 <tbody>
  <tr>
   <th>プロジェクトの状況</th>
   <th>推奨事項</th>
  </tr>
  <tr>
   <td>Adobe Experience Manager を使い始めようとしている。</td>
   <td>デフォルトの UI を使用します。</td>
  </tr>
  <tr>
   <td><p>AEM をしばらくの間使用している。</p> <p>製品の UI をそのまま使用していて、サイトのカスタムコンポーネントを開発している。<br /> </p> </td>
   <td>
    <ol>
     <li>6.5 にアップデートします。</li>
     <li>サイト管理、アセットなどには、デフォルトの UI を使用します等。<br /> </li>
     <li>クラシック UI のページエディターを表示するよう「ページを編集」のアクションを設定します。<a href="#selecting-your-ui">UI の選択</a>を参照してください。</li>
    </ol> <p>次に第 2 段階として、</p>
    <ol>
     <li>Coral 3 ダイアログ形式を使用するようにコンポーネントダイアログを更新します。コンポーネントの更新には、<a href="/help/sites-developing/dialog-conversion.md">ダイアログ変換ツール</a>を使用することをお勧めします。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>統合により、ClientContext を使用するサイトを構築したことがある。<br /> </td>
   <td>
    <ol>
     <li>6.5 にアップデートします。</li>
     <li>サイト管理、アセットなどには、デフォルトの UI を使用します等。</li>
     <li>クラシック UI のページエディターを表示するよう「ページを編集」のアクションを設定します。<a href="#selecting-your-ui">UI の選択</a>を参照してください。</li>
    </ol> <p>次に第 2 段階として、</p>
    <ol>
     <li>Coral 3 ダイアログ形式を使用するようにコンポーネントダイアログを更新します。コンポーネントの更新には、<a href="/help/sites-developing/dialog-conversion.md">ダイアログ変換ツール</a>を使用することをお勧めします。</li>
     <li>ContextHub（ClientContext の後継）を設定し、ContextHub を使用するようページテンプレートを更新します。ContextHub には、カスタムの ClientContext のストアを読み込むことができる互換モードがあります。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><p>CQ／AEM を長年使用している。</p> <p>製品 UI（サイト管理者など）を拡張し、詳細な編集ダイアログでコンポーネントを構築したことがある。</p> </td>
   <td><p>6.5 にアップデートし、すべてのユーザーに対するページオーサリングのデフォルトとしてクラシック UI を設定します。<a href="#selecting-your-ui">UI の選択</a>を参照してください。</p> <p>次に、プロジェクトを開始してカスタマイズを適用し、コンポーネントダイアログを Coral 3 形式で最適化します。<a href="#resources-to-help">役に立つリソース</a>を参照してください。<br /> </p> </td>
  </tr>
 </tbody>
</table>

### FAQ {#faq}

詳しくは、ナレッジベースの記事 [Touch UI Authoring FAQ](https://helpx.adobe.com/experience-manager/kb/index/touchui_faq.html) を参照してください。クラシック UI の廃止予定に関する情報も提供しています。

### UI の選択 {#selecting-your-ui}

システムを必要に応じて設定する方法について詳しくは、[UI の選択](/help/sites-authoring/select-ui.md)を参照してください。

### タッチ操作対応 UI のステータス {#touch-enabled-ui-status}

AEM 6.5 でのタッチ操作対応 UI の機能強化について詳しくは、リリースノートの[新機能](/help/release-notes/release-notes.md#what-s-new)を参照してください。

全体的な概要については、[タッチ操作対応 UI 機能のステータス](/help/release-notes/touch-ui-features-status.md)ページを参照してください。

### 役に立つリソース {#resources-to-help}

基本処理の背景情報については、以下を参照してください。

* [ページのオーサリング](/help/sites-authoring/page-authoring.md)。

開発情報について詳しくは、以下を参照してください。

* [タッチ操作対応 UI のアーキテクチャ](/help/sites-developing/touch-ui-concepts.md)。
* [ダイアログ変換ツール](/help/sites-developing/dialog-conversion.md)を使用して、コンポーネントの編集ダイアログを、クラシック UI からタッチ操作対応 UI に変換。

* [タッチ操作対応 UI の構造](/help/sites-developing/touch-ui-structure.md)

* [タッチ操作対応 UI のコンソールのカスタマイズ](/help/sites-developing/customizing-consoles-touch.md)（サンプルコードを含む）。

* [タッチ操作対応 UI のページオーサリングのカスタマイズ](/help/sites-developing/customizing-page-authoring-touch.md)（サンプルコードを含む）。

* [タッチ操作対応カスタマイズでの AEM Gem セッション](https://docs.adobe.com/content/ddc/en/gems/user-interface-customization-for-aem-6.html)。
* [Granite UI ドキュメント](https://helpx.adobe.com/jp/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)。

