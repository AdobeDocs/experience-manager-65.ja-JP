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

---


# Migration to the Touch UI{#migration-to-the-touch-ui}

バージョン6.0以降、Adobe Experience Manager(AEM)では、タッチ対応UI *(タッチ操作対応UI* )と呼ばれる新しいユーザーインターフェイスが導入さ **&#x200B;れました。 Adobe Marketing cloudとAdobeユーザーインターフェイスの全体的なガイドラインに沿っています。 これは、従来のデスクトップ指向インターフェイスをクラシックUIと呼ぶAEMの標準UIに *なりました*。

AEMをクラシックUIで使用している場合は、インスタンスを移行するための対策を講じる必要があります。 このページは、個々のリソースへのリンクを提供することで、スプリングボードとしての役割を果たすことを目的としています。

>[!NOTE]
>
>このような移行プロジェクトは、インスタンスに大きな影響を与える可能性があります。 推奨されるガ [イドラインについては、「プロジェクトの管理](/help/managing/best-practices.md) — ベストプラクティス」を参照してください。

## 基本知識 {#the-basics}

移行時には、クラシックUIとタッチUIの主な違いを次に示します。

<table>
 <tbody>
  <tr>
   <td>クラシック UI</td>
   <td>タッチ操作対応 UI</td>
  </tr>
  <tr>
   <td>JCRリポジトリでは、ノードの構造として記述されます。 UIの要素を表すすべてのノードは <em>ExtJSウィジェットと呼ばれ</em> 、によってクライアント側にレンダリングされま <code>ExtJS</code>す。</td>
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
     <li>for example<br /> <code>cq/gui/components/authoring/dialog</code><br /> </li>
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
     <li>命令部分は、リスナーを使用して直接埋め込まれるか、clientlibで管理されます。</li>
    </ul> </td>
   <td><p>JavaScriptの場所：</p>
    <ul>
     <li>命令部は、ダイアログ定義に埋め込むことはできません。責任の分離。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>イベント処理：</p>
    <ul>
     <li>ダイアログウィジェットはJavaScriptコードを直接参照します。</li>
    </ul> </td>
   <td><p>イベント処理：</p>
    <ul>
     <li>JavaScriptはダイアログイベントを監視します。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>クライアントが実行するレンダリング：
    <ul>
     <li>クライアントはUIコンポーネントを動的に作成します。</li>
     <li>クライアントは、サーバーから（JSONとして）コンポーネント定義を要求します。</li>
    </ul> </td>
   <td>サーバーが実行するレンダリング：
    <ul>
     <li>クライアントは、関連するUIと共にページをリクエストします。</li>
     <li>サーバーはUIをHTMLドキュメントとして送信（プッシュ）します。Coral UIコンポーネントの使用」を参照してください。<br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

つまり、UIの一部をクラシックUIからタッチUIに移行するということは、 *ExtJSウィジェットを* Slingコンポーネントに移行する *ことを意*&#x200B;味します。 これを容易にするために、タッチUIはGranite UIフレームワークに基づいており、UI用のSlingコンポーネント（Granite UIコンポーネントと呼ばれます）が既に用意されています。

開始する前に、ステータスと関連するレコメンデーションを確認します。

* [タッチ操作対応UI機能の状態](/help/release-notes/touch-ui-features-status.md)
* [顧客向けのユーザーインターフェイスの推奨事項](/help/sites-deploying/ui-recommendations.md)

タッチ操作対応UI開発の基本は、次のような基本を提供します。

* [AEM タッチ操作対応 UI の概念](/help/sites-developing/touch-ui-concepts.md)
* [AEM タッチ操作対応 UI の構造](/help/sites-developing/touch-ui-structure.md)

## ページオーサリングの移行 {#migrating-page-authoring}

コンポーネントを移行する際の主な要因は、ダイアログです。

* [AEMコンポーネント](/help/sites-developing/developing-components.md) （タッチ操作対応UIを使用）の開発
* [クラシックコンポーネントからの移行](/help/sites-developing/developing-components.md#migrating-from-a-classic-component)
* [ダイアログ変換ツール](/help/sites-developing/dialog-conversion.md) — 従来のUIコンポーネントのダイアログをタッチUIに変換するのに役立ちます。

   * タッチUIには、「タッチUIラッパー」内でクラシックUIダイアログを開くための互換性レイヤーがありますが、機能には制限があり、長期的には推奨されません。

* [タッチ操作対応UIのダイアログフィールドのカスタマイズ](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-customizing-dialog-fields-in-touch-ui.html)
* [新しい Granite UI フィールドコンポーネントの作成](/help/sites-developing/granite-ui-component.md)
* [ページオーサリングのカスタマイズ](/help/sites-developing/customizing-page-authoring-touch.md) （タッチ操作対応UIを使用）

## コンソールの移行 {#migrating-consoles}

また、コンソールをカスタマイズすることもできます。

* [コンソールのカスタマイズ](/help/sites-developing/customizing-consoles-touch.md) （タッチ操作対応UI用）

## 関連する考慮事項 {#related-considerations}

タッチ操作対応UIへの直接の移行とは関係ありませんが、次のような推奨プラクティスがあるので、同時に検討する価値のある関連する問題があります。

* [テンプレート](/help/sites-developing/templates.md) — 編集可能 [なテンプレート](/help/sites-developing/page-templates-editable.md)
* [コアコンポーネント](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html)
* [HTL](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html)

>[!NOTE]
>
>「開発 — ベストプ [ラクティス」も参照してください](/help/sites-developing/best-practices.md)。

## その他のリソース {#further-resources}

AEMの開発に関する詳細は、以下のリソースを参照してください。

* [開発ユーザーガイド](/help/sites-developing/home.md)
* [Granite UI ドキュメント](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html)
* [AEM 6.5サイトのチュートリアルとビデオ](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/overview.html)
* [AEM Sites の開発の手引き - WKND チュートリアル](/help/sites-developing/getting-started.md)
* [AEM Gems](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-index.html)
* [AEM最新化ツール](https://opensource.adobe.com/aem-modernize-tools/)

>[!CAUTION]
>
>AEM Modernization toolsはコミュニティでの取り組みであり、アドビによるサポートや警告は行われていません。

