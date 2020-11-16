---
title: セグメント化の設定
seo-title: セグメント化の設定
description: AEM キャンペーンのセグメント化を設定する方法について説明します。
seo-description: AEM キャンペーンのセグメント化を設定する方法について説明します。
uuid: 604ca34d-cdb9-49ff-8f75-02a44b60a8a2
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: c68d5853-684f-42f2-a215-c1eaee06f58a
docset: aem65
translation-type: tm+mt
source-git-commit: 684d2d5f73d571a15c8155e7870134c28dc892b7
workflow-type: tm+mt
source-wordcount: '1080'
ht-degree: 79%

---


# セグメント化の設定 {#configuring-segmentation}

>[!NOTE]
>
>このドキュメントでは、ClientContext で使用するセグメント化の設定について説明します。タッチ UI で ContextHub を使用してセグメント化を設定するには、[ContextHub でのセグメント化の設定](/help/sites-administering/segmentation.md)を参照してください。

キャンペーンを作成する場合、セグメント化を考えることが重要になります。セグメント化の仕組みと主な用語について詳しくは、[セグメント化の用語](/help/sites-authoring/segmentation-overview.md)を参照してください。

サイト訪問者についてこれまでに収集した情報と、達成する目標に応じて、ターゲットコンテンツに必要なセグメントと戦略を定義する必要があります。

このようなセグメントを使用して、訪問者に特定のターゲットコンテンツを提供します。This content is maintained in the [Campaigns](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md) section of the website. ここで定義されたティーザーページは、任意のページでティーザー段落として追加できます。また、専用のコンテンツを適用できる訪問者セグメントを定義できます。

AEM を使用すると、セグメント、ティーザーおよびキャンペーンを簡単に作成できます。また、定義の結果を検証することもできます。

The **Segment Editor** allows you to easily define a segment:

![](assets/segmenteditor.png)

各セグメントを&#x200B;**編集**&#x200B;し、**タイトル**、**説明**&#x200B;および&#x200B;**ブースト**&#x200B;係数を指定できます。サイドキックを使用すると、**AND** および **OR** コンテナを追加して&#x200B;**セグメントロジック**&#x200B;を定義してから、必要な&#x200B;**セグメント特性**&#x200B;を追加して選択基準を定義できます。

## ブースト係数 {#boost-factor}

Each segment has a **Boost** parameter that is used as a weighting factor; a higher number indicates that the segment will be selected in preference to a segment with a lower number.

* 最小値：`0`
* 最大値：`1000000`

## セグメントのロジック {#segment-logic}

次のロジックコンテナはそのまま使用でき、選択したセグメントのロジックを構築できます。これらはサイドキックからエディターにドラッグできます。

<table>
 <tbody>
  <tr>
   <td> AND コンテナ<br /> </td>
   <td> The boolean AND operator.<br /> </td>
  </tr>
  <tr>
   <td> OR コンテナ<br /> </td>
   <td> ブールOR演算子。</td>
  </tr>
 </tbody>
</table>

## セグメントの特徴 {#segment-traits}

以下のセグメントの特性はすぐに使用できます。また、サイドキックからエディターにドラッグできます。

<table>
 <tbody>
  <tr>
   <td> IP 範囲<br /> </td>
   <td>訪問者に割り当てられる IP アドレスの範囲を定義します。<br /> </td>
  </tr>
  <tr>
   <td> ページヒット<br /> </td>
   <td>ページがリクエストされた頻度。<br /> </td>
  </tr>
  <tr>
   <td> ページプロパティ<br /> </td>
   <td>訪問したページのすべてのプロパティ。<br /> </td>
  </tr>
  <tr>
   <td> リファラルキーワード<br /> </td>
   <td>参照先の Web サイトの情報と照合するキーワード。<br /> </td>
  </tr>
  <tr>
   <td> スクリプト</td>
   <td>評価される Javascript 式。<br /> </td>
  </tr>
  <tr>
   <td> セグメントの参照 <br /> </td>
   <td>もう一方のセグメントへの参照。<br /> </td>
  </tr>
  <tr>
   <td> タグクラウド<br /> </td>
   <td>訪問したページのタグと照合されるタグ。<br /> </td>
  </tr>
  <tr>
   <td> ユーザーの年齢<br /> </td>
   <td>ユーザープロファイルから取得される年齢。<br /> </td>
  </tr>
  <tr>
   <td> ユーザープロパティ<br /> </td>
   <td>ユーザープロファイルで確認できるその他すべての情報。 </td>
  </tr>
 </tbody>
</table>

You can combine these traits using the boolean operators OR and AND (see [Creating a New Segment](#creating-a-new-segment)) to define the exact scenario for selecting this segment.

文全体が true と評価されると、このセグメントは解決されます。In the event of multiple segments being applicable, then the **[Boost](/help/sites-administering/campaign-segmentation.md#boost-factor)** factor is also used.

>[!CAUTION]
>
>セグメントエディターは、循環参照をチェックしません。例えば、セグメントAは別のセグメントBを参照し、次にセグメントAを参照します。セグメントAに循環参照が含まれていないことを確認する必要があります。

>[!NOTE]
>
>**_i18n** サフィックスを持つプロパティは、パーソナライズのUI clientlibの一部であるスクリプトによって設定されます。 UI は公開時には必要ないので、UI 関連の clientlib はすべて作成時に読み込まれます。
>
>Therefore when creating a segment with such properties is it normally necessary to rely on **browserFamily** for instance instead of **browserFamily_i18n**.

### 新しいセグメントの作成 {#creating-a-new-segment}

新しいセグメントを定義するには：

1. In the rail, choose **Tools > Operations > Configuration**.
1. 左側のウィンドウで&#x200B;**セグメント化**&#x200B;ページを開き、必要な場所に移動します。
1. **セグメント**&#x200B;テンプレートを使用して[新規ページ](/help/sites-authoring/editing-content.md#creatinganewpage)を作成します。
1. 新規ページを開いてセグメントエディターを表示します。

   ![](assets/screen_shot_2012-02-02at101726am.png)

1. サイドキックまたはコンテキストメニュー（通常、マウスを右クリックして「**新規...**」を選択すると、新規コンポーネントを挿入ウィンドウが表示される）を使用して、必要なセグメント特性を見つけます。それをデフォルトの **AND** コンテナに表示される&#x200B;**セグメントエディター**&#x200B;にドラッグします。
1. 新規の特性をダブルクリックして、例えばマウスの位置など、特定のパラメーターを編集します。

   ![](assets/screen_shot_2012-02-02at103135am.png)

1. 「**OK**」をクリックして定義を保存します。
1. セグメント設定を&#x200B;**編集**&#x200B;し、**タイトル**、**説明**&#x200B;および&#x200B;**[ブースト](#boost-factor)**&#x200B;係数を追加することができます。

   ![](assets/screen_shot_2012-02-02at103547am.png)

1. 必要に応じて特性を追加します。**セグメントロジック**&#x200B;にある「**AND コンテナ**」および「**OR コンテナ**」コンポーネントを使用してブール式を作成することができます。セグメントエディターでは、不要になった特性やコンテナを削除したり、コンポーネントをステートメント内の別の場所へドラッグしたりすることができます。

### AND コンテナと OR コンテナの使用 {#using-and-and-or-containers}

AEM で複雑なセグメントを作成できます。次の基本事項に留意してください。

* 定義の最上位レベルは必ず、最初に作成された AND コンテナになります。これは変更できませんが、他のセグメント定義には影響しません。
* コンテナのネストが意味のあるものになっていることを確認してください。コンテナは、ブール式の括弧として見ることができます。

次の例は以下のいづれかの訪問者を選択するために使用されます。

16 才～ 65 才の男性

または

16 才～ 62 才の女性

主要演算子に OR を使用するので、「**OR コンテナ**」で開始する必要があります。この中に 2 つの AND ステートメントを挿入し、個別の特性を追加できる「**AND コンテナ**」がそれぞれに必要になります。

![](assets/screen_shot_2012-02-02at105145am.png)

## セグメントの適用のテスト {#testing-the-application-of-a-segment}

セグメントを設定したら、**[クライアントコンテキスト](/help/sites-administering/client-context.md)**&#x200B;を使用して、考えられる結果についてテストすることができます。

1. テストするセグメントを選択します。
1. **[Ctrl + Alt + C](/help/sites-authoring/page-authoring.md#keyboardshortcuts)** キーを押して、**[クライアントコンテキスト](/help/sites-administering/client-context.md)**&#x200B;を開くと、収集されたデータが表示されます。For testing purposes you can **Edit** certain values, or **Load** another profile to see the impact there.

1. 定義した特性に応じて、現在のページで利用可能なデータはセグメント定義と一致する場合も一致しない場合もあります。一致のステータスは定義の下に表示されます。

例えば、単純なセグメントはユーザーの年齢と性別に基づいて定義できます。特定のプロファイルを読み込むと、セグメントが正常に解決されたことを示します。

![](assets/screen_shot_2012-02-02at105926am.png)

失敗したかが表示されます。

![](assets/screen_shot_2012-02-02at110019am.png)

>[!NOTE]
>
>すべての特性がただちに解決されます。ただし、ほとんどの特性はページを再読み込みしたときにのみ変更されます。マウス位置の変更はすぐに表示されるため、テストの際に便利です。

Such tests can also be performed on content pages and in combination with **Teaser** components.

ティーザー段落にマウスを置くと、適用されたセグメント、セグメントが解決されたかどうか、その結果として現在のティーザーインスタンスが選択された理由が表示されます。

![](assets/chlimage_1-47.png)

### セグメントの使用 {#using-your-segment}

セグメントは現在[キャンペーン](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md)で使用されます。これらのセグメントを使用して、特定のターゲット読者に向けられた実際のコンテンツを制御することができます。詳しくは、[セグメント化について](/help/sites-authoring/segmentation-overview.md)を参照してください。
