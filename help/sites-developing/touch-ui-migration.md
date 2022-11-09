---
title: タッチ UI への移行
seo-title: Migration to the Touch UI
description: タッチ UI への移行
seo-description: Migration to the Touch UI
uuid: 47c43b56-532b-4ada-8503-04d66bab3564
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: introduction
discoiquuid: b315720f-e9b8-4063-99e2-1b9aa6bba460
docset: aem65
exl-id: 33dc1ee7-1e34-43d8-9265-c66535f5e002
source-git-commit: 53c39e4aa250b18d4fae0327b313b18901677f2c
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 100%

---

# タッチ UI への移行{#migration-to-the-touch-ui}

バージョン 6.0 以降、Adobe Experience Manager（AEM）では、*タッチ操作対応 UI*（単に&#x200B;*タッチ UI*&#x200B;とも呼ばれます）をクリックします。これは、Adobe Marketing Cloud と、全体的な Adobe ユーザーインターフェイスのガイドラインに合わせて表示されます。これは AEM の標準的な UI で、レガシーでデスクトップ向けのインターフェースは&#x200B;*クラシック UI* と呼ばれています。

クラシック UI で AEM を使用している場合は、インスタンスを移行するために対処する必要があります。このページは、それぞれのリソースへのリンクを提供することで、スプリングボードとしての役割を果たすことを目的としています。

>[!NOTE]
>
>このような移行プロジェクトは、インスタンスに大きな影響を与える可能性があります。詳しくは、[プロジェクトの管理 — ベストプラクティス](/help/managing/best-practices.md)を参照してください。

## 基本知識 {#the-basics}

移行時には、クラシック UI とタッチ UI の、次の（大きな）違いに注意する必要があります。

<table>
 <tbody>
  <tr>
   <td>クラシック UI</td>
   <td>タッチ操作対応 UI</td>
  </tr>
  <tr>
   <td>JCR リポジトリでノードの構造として記述されます。UI の要素を表すすべてのノードは <em>ExtJS ウィジット</em>と呼ばれ、<code>ExtJS</code> によってクライアントサイドでレンダリングされます。</td>
   <td>JCR リポジトリでもノードの構造として説明されています。ただし、この場合、すべてのノードは Sling リソースタイプ（Sling コンポーネント）を参照し、そのレンダリングを担当します。したがって、UI は（基本的に）サーバーサイドでレンダリングされます。</td>
  </tr>
  <tr>
   <td><p><code>sling:resourceType</code></p>
    <ul>
     <li>未使用</li>
    </ul> </td>
   <td><code>sling:resourceType</code>
    <ul>
     <li>使用済み</li>
     <li>例えば、次のように参照します。<br /> <code>cq/gui/components/authoring/dialog</code><br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>ダイアログノード：</p>
    <ul>
     <li>名前： <code>dialog</code></li>
     <li>jcr:primaryType: <code>cq:Dialog</code></li>
    </ul> </td>
   <td><p>ダイアログノード：</p>
    <ul>
     <li>名前： <code>cq:dialog</code></li>
     <li>jcr:primaryType: <code>nt:unstructured</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>JavaScript の場所：</p>
    <ul>
     <li>必須部分は、リスナーを使用して直接埋め込むか、clientlib で管理します。</li>
    </ul> </td>
   <td><p>JavaScript の場所：</p>
    <ul>
     <li>必須部分は、ダイアログ定義に埋め込むことはできません。これは、責任の分離です。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>イベントの処理：</p>
    <ul>
     <li>ダイアログウィジェットは JavaScript コードを直接参照します。</li>
    </ul> </td>
   <td><p>イベントの処理：</p>
    <ul>
     <li>JavaScript は、ダイアログイベントを監視します。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>クライアントがレンダリングを実行：
    <ul>
     <li>クライアントは UI コンポーネントを動的に作成します。</li>
     <li>クライアントは、（JSON 形式で）サーバーからコンポーネント定義をリクエスト（プル）します。</li>
    </ul> </td>
   <td>サーバーがレンダリングを実行：
    <ul>
     <li>クライアントは、関連する UI と共にページを要求します。</li>
     <li>サーバーは UI を HTML ドキュメントとして送信（プッシュ）します。Coral UI コンポーネントを使用します。<br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

つまり、UI の一部をクラシック UI からタッチ UI に移行するということは、*ExtJS ウィジェット*&#x200B;を *Sling コンポーネント*&#x200B;に移行することを意味します。これを容易にするために、タッチ UI は、Granite UI フレームワークに基づいています。このフレームワークは、既に UI 用の Sling コンポーネント（Granite UI コンポーネントと呼ばれます）を提供しています。

開始する前に、ステータスと関連する推奨事項を確認してください。

* [タッチ操作対応 UI 機能のステータス](/help/release-notes/touch-ui-features-status.md)
* [顧客向けのユーザーインターフェイスの推奨事項](/help/sites-deploying/ui-recommendations.md)

タッチ UI の開発の基本は、堅牢な基礎を提供します。

* [AEM タッチ操作対応 UI の概念](/help/sites-developing/touch-ui-concepts.md)
* [AEM タッチ操作対応 UI の構造](/help/sites-developing/touch-ui-structure.md)

## ページオーサリングの移行 {#migrating-page-authoring}

コンポーネントを移行する際、ダイアログは主な要因です。

* [AEM コンポーネントの開発](/help/sites-developing/developing-components.md) （タッチ操作対応 UI を使用）
* [クラシックコンポーネントからの移行](/help/sites-developing/developing-components.md#migrating-from-a-classic-component)
* [AEM 最新化ツール](/help/sites-developing/modernization-tools.md) — クラシック UI コンポーネントのダイアログをタッチ UI に変換することに役立ちます。

   * タッチ UI には、「タッチ UI のラッパー」内でクラシック UI ダイアログを開くための互換性レイヤーがありますが、機能が限られているので、長期的には推奨されません。

* [タッチ UI でのダイアログフィールドのカスタマイズ](https://helpx.adobe.com/jp/experience-manager/kt/eseminars/gems/aem-customizing-dialog-fields-in-touch-ui.html)
* [新しい Granite UI フィールドコンポーネントの作成](/help/sites-developing/granite-ui-component.md)
* [ページオーサリングのカスタマイズ](/help/sites-developing/customizing-page-authoring-touch.md)（タッチ操作対応 UI を使用）

## コンソールの移行 {#migrating-consoles}

コンソールをカスタマイズすることもできます。

* [コンソールのカスタマイズ](/help/sites-developing/customizing-consoles-touch.md)（タッチ操作対応 UI 用）

## 関連する考慮事項 {#related-considerations}

タッチ UI への移行とは直接関係ありませんが、移行に際して検討を推奨する関連事項として、次のものがあります。

* [テンプレート](/help/sites-developing/templates.md) - [編集可能なテンプレート](/help/sites-developing/page-templates-editable.md)
* [コアコンポーネント](https://docs.adobe.com/content/help/ja-JP/experience-manager-core-components/using/introduction.html)
* [HTL](https://docs.adobe.com/content/help/ja/experience-manager-htl/using/overview.html)

>[!NOTE]
>
>[開発 - ベストプラクティス](/help/sites-developing/best-practices.md)も参照してください。

## その他のリソース {#further-resources}

AEM の開発について詳しくは、以下のリソースのコレクションを参照してください。

* [ユーザーガイドの作成](/help/sites-developing/home.md)
* [Granite UI ドキュメント](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html)
* [AEM 6.5 Sites のチュートリアルとビデオ](https://docs.adobe.com/content/help/ja-JP/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)
* [AEM Sites の開発の手引き - WKND チュートリアル ](/help/sites-developing/getting-started.md)
* [AEM Gems](https://helpx.adobe.com/jp/experience-manager/kt/eseminars/gems/aem-index.html)
* [AEM 最新化ツール](https://opensource.adobe.com/aem-modernize-tools/)

>[!CAUTION]
>
>AEM 最新化ツールはコミュニティの取り組みであり、アドビによるサポートまたは保証の対象外です。
