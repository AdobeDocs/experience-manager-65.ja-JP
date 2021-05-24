---
title: タッチUIへの移行
seo-title: タッチUIへの移行
description: タッチUIへの移行
seo-description: タッチUIへの移行
uuid: 47c43b56-532b-4ada-8503-04d66bab3564
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: introduction
discoiquuid: b315720f-e9b8-4063-99e2-1b9aa6bba460
docset: aem65
exl-id: 33dc1ee7-1e34-43d8-9265-c66535f5e002
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 14%

---

# タッチ操作対応UIへの移行{#migration-to-the-touch-ui}

バージョン6.0以降、Adobe Experience Manager(AEM)では、*タッチ操作対応UI*（単に&#x200B;*タッチUI*&#x200B;とも呼ばれる）と呼ばれる新しいユーザーインターフェイスが導入されました。 これは、Adobe Marketing Cloudおよび全体的なAdobeユーザーインターフェイスのガイドラインに従います。 これは、従来のデスクトップ指向のインターフェイス（*クラシックUI*&#x200B;と呼ばれる）を備えたAEMの標準UIになりました。

クラシックUIでAEMを使用している場合は、インスタンスを移行するための対策を講じる必要があります。 このページは、個々のリソースへのリンクを提供することで、スプリングボードとして機能することを目的としています。

>[!NOTE]
>
>このような移行プロジェクトは、インスタンスに大きな影響を与える可能性があります。 推奨されるガイドラインについては、[プロジェクトの管理 — ベストプラクティス](/help/managing/best-practices.md)を参照してください。

## 基本知識 {#the-basics}

移行時には、クラシックUIとタッチUIの（主な）違いを次に示します。

<table>
 <tbody>
  <tr>
   <td>クラシック UI</td>
   <td>タッチ操作対応 UI</td>
  </tr>
  <tr>
   <td>ノードの構造としてJCRリポジトリに記述されます。 UIの要素を表すすべてのノードは、<em>ExtJSウィジェット</em>と呼ばれ、<code>ExtJS</code>によってクライアント側にレンダリングされます。</td>
   <td>JCRリポジトリでもノードの構造として説明されています。 ただし、この場合、すべてのノードは、レンダリングを担当するSlingリソースタイプ（Slingコンポーネント）を参照します。 したがって、UIは（基本的に）サーバーサイドでレンダリングされます。</td>
  </tr>
  <tr>
   <td><p><code>sling:resourceType</code></p>
    <ul>
     <li>未使用</li>
    </ul> </td>
   <td><code>sling:resourceType</code>
    <ul>
     <li>使用済み</li>
     <li>例：<br /> <code>cq/gui/components/authoring/dialog</code><br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>ダイアログノード：</p>
    <ul>
     <li>名前: <code>dialog</code></li>
     <li>jcr:primaryType: <code>cq:Dialog</code></li>
    </ul> </td>
   <td><p>ダイアログノード：</p>
    <ul>
     <li>名前: <code>cq:dialog</code></li>
     <li>jcr:primaryType: <code>nt:unstructured</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>JavaScriptの場所：</p>
    <ul>
     <li>必須部分は、リスナーを使用して直接埋め込むか、clientlibで管理します。</li>
    </ul> </td>
   <td><p>JavaScriptの場所：</p>
    <ul>
     <li>必須部分は、ダイアログ定義に埋め込むことはできません。責任の分離。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>イベントの処理：</p>
    <ul>
     <li>ダイアログウィジェットはJavaScriptコードを直接参照します。</li>
    </ul> </td>
   <td><p>イベントの処理：</p>
    <ul>
     <li>JavaScriptがダイアログイベントを観察します。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>クライアントによるレンダリング：
    <ul>
     <li>クライアントはUIコンポーネントを動的に作成します。</li>
     <li>クライアントは、（JSONとして）サーバーからコンポーネント定義を要求（プル）します。</li>
    </ul> </td>
   <td>サーバーによるレンダリング：
    <ul>
     <li>クライアントは、関連するUIと共にページを要求します。</li>
     <li>サーバーは、UIをHTMLドキュメントとして送信（プッシュ）します。Coral UIコンポーネントを使用します。<br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

つまり、UIのセクションをクラシックUIからタッチUIに移行すると、*ExtJSウィジェット*&#x200B;を&#x200B;*Slingコンポーネント*&#x200B;に移行することになります。 これを容易にするために、タッチUIは、Granite UIフレームワークに基づいており、既にUI用のSlingコンポーネント（Granite UIコンポーネント）が提供されています。

開始する前に、ステータスと関連するレコメンデーションを確認します。

* [タッチ操作対応UI機能のステータス](/help/release-notes/touch-ui-features-status.md)
* [顧客向けのユーザーインターフェイスの推奨事項](/help/sites-deploying/ui-recommendations.md)

タッチUIの開発の基本は、次のように明確な基盤を提供します。

* [AEM タッチ操作対応 UI の概念](/help/sites-developing/touch-ui-concepts.md)
* [AEM タッチ操作対応 UI の構造](/help/sites-developing/touch-ui-structure.md)

## ページオーサリングの移行{#migrating-page-authoring}

コンポーネントを移行する際の主な要因は、ダイアログです。

* [AEMコンポーネントの開発](/help/sites-developing/developing-components.md) （タッチ操作対応UIを使用）
* [クラシックコンポーネントからの移行](/help/sites-developing/developing-components.md#migrating-from-a-classic-component)
* [AEM Modernization Tools](/help/sites-developing/modernization-tools.md)  — クラシックUIコンポーネントのダイアログをタッチUIに変換するのに役立ちます。

   * タッチUIには、「タッチUIラッパー」内でクラシックUIダイアログを開くための互換性レイヤーがありますが、機能は限られているので、長期的にはお勧めしません。

* [タッチUIのダイアログフィールドのカスタマイズ](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-customizing-dialog-fields-in-touch-ui.html)
* [新しい Granite UI フィールドコンポーネントの作成](/help/sites-developing/granite-ui-component.md)
* [ページオーサリングのカスタマイズ](/help/sites-developing/customizing-page-authoring-touch.md) （タッチ操作対応UIを使用）

## コンソールの移行{#migrating-consoles}

また、コンソールをカスタマイズすることもできます。

* [コンソールのカスタマイズ](/help/sites-developing/customizing-consoles-touch.md) （タッチ操作対応UI用）

## 関連する考慮事項{#related-considerations}

タッチUIへの移行とは直接関連していませんが、同時に検討する価値のある関連する問題もあります。これらも推奨される方法です。

* [テンプレート](/help/sites-developing/templates.md)  — 編集可能な [テンプレート](/help/sites-developing/page-templates-editable.md)
* [コアコンポーネント](https://docs.adobe.com/content/help/ja/experience-manager-core-components/using/introduction.html)
* [HTL](https://docs.adobe.com/content/help/ja/experience-manager-htl/using/overview.html)

>[!NOTE]
>
>[開発 — ベストプラクティス](/help/sites-developing/best-practices.md)も参照してください。

## その他のリソース{#further-resources}

AEMの開発について詳しくは、以下のリソースのコレクションを参照してください。

* [開発ユーザーガイド](/help/sites-developing/home.md)
* [Granite UI ドキュメント](https://helpx.adobe.com/jp/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html)
* [AEM 6.5 SitesのTutorialsとビデオ](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/overview.html)
* [AEM Sites の開発の手引き - WKND チュートリアル](/help/sites-developing/getting-started.md)
* [AEM Gems](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-index.html)
* [AEM Modernization Tools](https://opensource.adobe.com/aem-modernize-tools/)

>[!CAUTION]
>
>AEM Modernization Toolsはコミュニティの取り組みであり、Adobeによるサポートや保証はありません。
