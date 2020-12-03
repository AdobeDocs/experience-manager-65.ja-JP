---
title: タッチ操作対応UIへの移行
seo-title: タッチ操作対応UIへの移行
description: タッチ操作対応UIへの移行
seo-description: タッチ操作対応UIへの移行
uuid: 47c43b56-532b-4ada-8503-04d66bab3564
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: introduction
discoiquuid: b315720f-e9b8-4063-99e2-1b9aa6bba460
docset: aem65
translation-type: tm+mt
source-git-commit: 5597fb39500ac1f85d03263bfa1e5239d35d2a2c
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 12%

---


# タッチ操作対応UIへの移行{#migration-to-the-touch-ui}

バージョン6.0以降、Adobe Experience Manager(AEM)は、*タッチ対応UI*（単に&#x200B;*タッチUI*&#x200B;とも呼ばれる）と呼ばれる新しいユーザーインターフェイスを導入しました。 これは、Adobe Marketing CloudおよびAdobeのユーザインターフェイスの全体的なガイドラインと一致します。 これは、従来のデスクトップ指向インターフェイス（*クラシックUI*）を備えたAEMの標準UIになりました。

クラシックUIを使用してAEMを使用している場合は、インスタンスを移行するための対策を講じる必要があります。 このページは、個々のリソースへのリンクを提供することで、スプリングボードとしての役割を果たすことを目的としています。

>[!NOTE]
>
>このような移行プロジェクトは、インスタンスに大きな影響を与える可能性があります。 推奨されるガイドラインについては、[プロジェクトの管理 — ベストプラクティス](/help/managing/best-practices.md)を参照してください。

## 基本知識 {#the-basics}

移行時には、クラシックUIとタッチUIの（主に）次の点に注意する必要があります。

<table>
 <tbody>
  <tr>
   <td>クラシック UI</td>
   <td>タッチ操作対応 UI</td>
  </tr>
  <tr>
   <td>JCRリポジトリでは、ノードの構造として記述されます。 UIの要素を表すすべてのノードを<em>ExtJSウィジェット</em>と呼び、<code>ExtJS</code>によってクライアント側にレンダリングします。</td>
   <td>JCRリポジトリでもノードの構造として説明されます。 ただし、この場合、すべてのノードはレンダリングを担当するSlingリソースタイプ（Slingコンポーネント）を参照します。 したがって、UIは（基本的に）サーバ側でレンダリングされます。</td>
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
     <li>命令部はリスナーを使用して直接埋め込まれるか、clientlibで管理されます。</li>
    </ul> </td>
   <td><p>JavaScriptの場所：</p>
    <ul>
     <li>命令部はダイアログ定義に埋め込むことはできません。責任の分離。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>イベント処理：</p>
    <ul>
     <li>ダイアログウィジェットはJavaScriptコードを直接参照します。</li>
    </ul> </td>
   <td><p>イベント処理：</p>
    <ul>
     <li>JavaScriptはダイアログのイベントを監視します。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>クライアントが実行したレンダリング：
    <ul>
     <li>クライアントはUIコンポーネントを動的に作成します。</li>
     <li>クライアントは、（JSONとして）コンポーネント定義をサーバーから要求（プル）します。</li>
    </ul> </td>
   <td>サーバーが実行したレンダリング：
    <ul>
     <li>クライアントは、関連するUIと共にページをリクエストします。</li>
     <li>サーバーはUIをHTMLドキュメントとして送信（プッシュ）します。Coral UIコンポーネントを使用しています。<br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

つまり、UIの一部をクラシックUIからタッチUIに移行するとは、*ExtJSウィジェット*&#x200B;を&#x200B;*Slingコンポーネント*&#x200B;に移行することです。 これを容易にするために、タッチUIはGranite UIフレームワークに基づいています。このフレームワークは、既にUI用のSlingコンポーネント（Granite UIコンポーネントと呼ばれます）を提供しています。

開始する前に、ステータスと関連する推奨事項を確認します。

* [タッチ操作対応UI機能のステータス](/help/release-notes/touch-ui-features-status.md)
* [顧客向けのユーザーインターフェイスの推奨事項](/help/sites-deploying/ui-recommendations.md)

タッチ操作対応UI開発の基本は、堅実な基盤を提供します。

* [AEM タッチ操作対応 UI の概念](/help/sites-developing/touch-ui-concepts.md)
* [AEM タッチ操作対応 UI の構造](/help/sites-developing/touch-ui-structure.md)

## ページオーサリングの移行{#migrating-page-authoring}

コンポーネントの移行時の主な要因は、ダイアログです。

* [AEMコンポーネントの開発](/help/sites-developing/developing-components.md) （タッチ操作対応UI）
* [クラシックコンポーネントからの移行](/help/sites-developing/developing-components.md#migrating-from-a-classic-component)
* [ダイアログ変換ツール](/help/sites-developing/dialog-conversion.md)  — クラシックUIコンポーネントのダイアログをタッチUIに変換するのに役立ちます。

   * タッチUIには、「タッチUIラッパー」内でクラシックUIダイアログを開く互換性レイヤーがありますが、機能には制限があり、長期的にはお勧めしません。

* [タッチ操作対応UIでのダイアログフィールドのカスタマイズ](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-customizing-dialog-fields-in-touch-ui.html)
* [新しい Granite UI フィールドコンポーネントの作成](/help/sites-developing/granite-ui-component.md)
* [ページオーサリングのカスタマイズ](/help/sites-developing/customizing-page-authoring-touch.md) （タッチ操作対応UI）

## コンソールの移行{#migrating-consoles}

また、コンソールをカスタマイズすることもできます。

* [コンソールのカスタマイズ](/help/sites-developing/customizing-consoles-touch.md) （タッチ操作対応UI用）

## 関連する考慮事項{#related-considerations}

タッチ操作対応UIへの移行とは直接の関係はありませんが、同時に検討する価値のある関連する問題があります。これらの問題も推奨される方法です。

* [テンプレート](/help/sites-developing/templates.md) - [編集可能なテンプレート](/help/sites-developing/page-templates-editable.md)
* [コアコンポーネント](https://docs.adobe.com/content/help/ja-JP/experience-manager-core-components/using/introduction.html)
* [HTL](https://docs.adobe.com/content/help/ja-JP/experience-manager-htl/using/overview.html)

>[!NOTE]
>
>[開発 — ベストプラクティス](/help/sites-developing/best-practices.md)も参照してください。

## その他のリソース{#further-resources}

AEMの開発に関する詳細は、次のリソースのコレクションを参照してください。

* [開発ユーザーガイド](/help/sites-developing/home.md)
* [Granite UI ドキュメント](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html)
* [AEM 6.5サイトのTutorialsとビデオ](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/overview.html)
* [AEM Sites の開発の手引き - WKND チュートリアル](/help/sites-developing/getting-started.md)
* [AEM Gems](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-index.html)
* [AEM Modernization Tools](https://opensource.adobe.com/aem-modernize-tools/)

>[!CAUTION]
>
>AEM Modernization Toolsはコミュニティでの取り組みであり、Adobeによるサポートや警戒は行われていません。

