---
title: ランディングページと Adobe Analytics の統合
seo-title: Integrating Landing Pages with Adobe Analytics
description: ランディングページと Adobe Analytics を統合する方法について説明します。
seo-description: Learn how to integrate landing pages with Adobe Analytics.
uuid: 8f6672d1-497f-4ccb-b3cc-f6120fc467ba
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 8ae7ccec-489b-4d20-ac56-6101402fb18a
exl-id: da3f7b7e-87e5-446a-9a77-4b12b850a381
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 100%

---

# ランディングページと Adobe Analytics の統合{#integrating-landing-pages-with-adobe-analytics}

AEM は、次に示すコールトゥアクション（CTA）コンポーネントを使用することにより、ランディングページのソリューションを [Adobe Analytics](https://www.omniture.com/jp/products/analytics/sitecatalyst) と統合しました。

1. クリックスルーコンポーネント
1. グラフィックリンクコンポーネント

これらのコンポーネントによって、Adobe Analytics の変数（トラフィック変数、コンバージョン変数）を使用してマッピングできる特定の属性、および Adobe Analytics に情報を送信するための成功イベントが公開されます。

## 前提条件 {#prerequisites}

[既存の AEM と Adobe Analytics の統合](/help/sites-administering/adobeanalytics.md)について確認し、この統合がどのように機能するかを把握することをお勧めします。

## マッピングに使用できるコンポーネント {#components-available-for-mapping}

AEM で、サイドキックに表示される&#x200B;**コールトゥアクション**&#x200B;コンポーネント（**クリックスルーリンク**&#x200B;と&#x200B;**グラフィックリンク**）を Adobe Analytics 変数にマッピングできます。

![chlimage_1-21](assets/chlimage_1-21a.jpeg)

### Adobe Analytics へのランディングページコンポーネントのマッピング {#mapping-landing-page-components-to-adobe-analytics}

ランディングページコンポーネントを Adobe Analytics にマッピングするには：

1. Adobe Analytics 設定を作成し、新しいフレームワークを作成したら、ドロップダウンメニューから適切なレポートスイートを選択します。この結果、Adobe Analytics の変数が取得され、コンテンツファインダーに表示されます。
1. コールトゥアクション（CTA）コンポーネントを、サイドキックからページ中央のマッピング領域の適切な場所にドラッグ＆ドロップします。

<table>
 <tbody>
  <tr>
   <td><strong>コンポーネント名</strong></td>
   <td><strong>公開される属性</strong></td>
   <td><strong>属性の意味</strong></td>
  </tr>
  <tr>
   <td><strong>CTA クリックスルーリンク</strong></td>
   <td><i>eventdata.clickthroughLinkLabel</i> <br /> </td>
   <td>リンクのラベル（リンクのテキスト） </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clickthroughLinkTarget</i> <br /> </td>
   <td>リンクをクリックしたときの移動先 </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.events.clickthroughLinkClick</i> <br /> </td>
   <td>クリックイベント </td>
  </tr>
  <tr>
   <td><strong>CTA グラフィックリンク</strong></td>
   <td><i>eventdata.clicktroughImageLabel</i> <br /> </td>
   <td>CTA 画像のタイトル </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clicktroughImageTarget</i> <br /> </td>
   <td>リンクを含む画像をクリックしたときの移動先</td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clicktroughImageAsset</i> <br /> </td>
   <td>リポジトリ内の画像アセットへのパス </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.events.clicktroughImageClick</i> <br /> </td>
   <td>クリックイベント</td>
  </tr>
 </tbody>
</table>

1. コンテンツファインダーで、これらの公開される属性と Adobe Analytics 変数をマッピングします。これで、フレームワークを使用できるようになります。
1. 新しいランディングページを作成するか、既存の CTA コンポーネントを含む既存のランディングページを開き、サイドキックで「**ページプロパティ**」の「**Cloud Services**」タブをクリックし（タッチ操作向け UI では、**プロパティを開く**&#x200B;を選択して「**Cloud Services**」をクリックし）、ランディングページで使用するフレームワークを設定します。ドロップダウンリストからフレームワークを選択します。

   ![chlimage_1-25](assets/chlimage_1-25a.png)

1. ランディングページを含むフレームワークを設定したら、実装されたコンポーネントが使用できるようになり、CTA でのクリックがすべて Adobe Analytics に記録されます。
