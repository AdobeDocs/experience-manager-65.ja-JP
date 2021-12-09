---
title: Dynamic Media のアクセシビリティ
description: Dynamic MediaとDynamic Mediaビューアでのアクセシビリティのサポートについて説明します。
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
feature: Accessibility
role: User, Admin
exl-id: bbdb800c-b6f8-4506-b8ac-daf64edcd6c0
source-git-commit: 01de1d5064f5ebf00acd2fe9f138d852f41f7273
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 66%

---

# [!DNL Dynamic Media] でのアクセシビリティ {#working-with-three-d-assets-dm}

[!DNL Dynamic Media] では、オーサリングユーザーインターフェイス全体でキーボードコントロールおよび支援テクノロジー（JAWS スクリーンリーダーや NVDA スクリーンリーダーなど）をサポートしています。

## でのキーボードアクセシビリティのサポート [!DNL Dynamic Media]

理由： [!DNL Dynamic Media] は [!DNL Adobe Experience Manager Assets]キーボード制御の動作のほとんどは、 [!DNL Experience Manager Assets]. 例えば、 `Cancel` ボタンで [!DNL Dynamic Media] のと同じフォーカスハイライトを持つ [!DNL Experience Manager Assets]、および `Spacebar` キーと同様に [!DNL Experience Manager Assets]. 詳しくは、[Assets のキーボードショートカット](/help/assets/accessibility.md#keyboard-shortcuts)を参照してください。

の個々のユーザーインターフェイス要素でサポートされるキー操作 [!DNL Dynamic Media] は明確で発見しやすい でのキーボード制御 [!DNL Dynamic Media] は、次に関するものです。

* `Tab` と `Shift+Tab` のキー操作を使用して、ページ上のインタラクティブ要素間を移動できます。`Tab` を使用すると、タブ順序における次のユーザーインターフェイス要素に入力フォーカスが進みます。`Shift+Tab` を使用すると、入力フォーカスが前のユーザーインターフェイス要素に戻ります。フォーカストラバーサルは、画面上のユーザーインターフェイス要素の自然な位置に従い、左から右、上から下の順に移動します。また、フィールドにエラーがある場合は、`Tab` を押して、そのフィールドにフォーカスを移動できます。
* `Spacebar` キーと `Enter` キーを使用して、ボタン、ドロップダウンリストなどの標準的なユーザーインターフェイス要素をアクティブにできます。
* アクティブな要素にキーボードフォーカスのハイライト表示を行えます。入力フォーカスを持つユーザインターフェイス要素は、ユーザインターフェイス要素の周囲にレンダリングされた境界線として視覚的フォーカス表示を受け取る。
* ホットスポットエディターでは、矢印キーなどのいくつかのカスタムキー操作を使用して複雑なユーザーインターフェイス要素を操作し、ホットスポットの位置を変更できます。
* インタラクティブビデオエディターでは、`Spacebar` を使用して画像を選択し、それをセグメントに追加できます。さらに、`Backspace` キーを使用して、選択した項目を「**[!UICONTROL コンテンツ]**」タブから削除できます。また、必要に応じて `Tab` キーを押して、ページ上のインタラクティブ要素間を移動できます。
* 画像切り抜き／スマート切り抜きエディターで、次の操作を実行できます。
   * 矢印キーを使用して、フレームサイズの切り抜きや画像位置の変更、またはその両方を行います。
   * 最初の `Tab` ストップで画像フレーム全体がハイライト表示されます。その場合、キーボードの矢印キーを使用してフレームの位置を変更できます。
   * その次の 4 つの `Tab` ストップはフレームの四隅です。フレームの隅をフォーカスすると、その隅がハイライト表示されます。この場合も、キーボードの矢印キーを使用して、フォーカスされた隅を移動できます。詳しくは、 [単一画像のスマート切り抜きまたはスマートスウォッチの編集](/help/assets/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (AEM 6.5) or Coral Spectrum (in Skyline)) as entire AEM Assets.  -->

<!-- In the Hotspot editor, Dynamic Media lets you use arrow keys to control the position of a hot spot. See [Carousel Banners](/help/assets/dynamic-media/carousel-banners.md##adding-hotspots-or-image-maps-to-an-image-banner) or [Interactive Images](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)  -->

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## での支援テクノロジーのサポート [!DNL Dynamic Media] {#assistive-technology-support-for-dm}

[!DNL Dynamic Media] のユーザーインターフェイス要素は、スクリーンリーダーなどの支援テクノロジーと連携動作します。例えば、キーボードショートカット `D` を使用してランドマークを移動するときや、キーボードショートカット `R` を使用して領域を移動するときに、ページのランドマークが認識されます。また、見出しのキーボードショートカット `H` を使用して移動する際に、見出しの読み上げも行われます。

## でのキーボードアクセシビリティのサポート [!DNL Dynamic Media] 閲覧者 {#keyboard-accessibility-for-dm-viewers}

すべて（標準） [!DNL Dynamic Media] ビューアコンポーネントは、お客様にとってキーボードアクセシビリティをサポートしています。

詳しくは、『Dynamic Media ビューアリファレンスガイド』の[キーボードのアクセシビリティとナビゲーション](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/c-keyboard-accessibility.html?lang=ja)を参照してください。

## での支援テクノロジーのサポート [!DNL Dynamic Media] 閲覧者 {#assistive-technology-support-for-dm-viewers}

すべて [!DNL Dynamic Media] ビューアコンポーネントは、ARIA（アクセシブルなリッチインターネットアプリケーション）の役割と属性をサポートし、スクリーンリーダーなどの支援テクノロジーとの統合を強化します。
詳しくは、『Dynamic Media ビューアリファレンスガイド』の「ビューアのカスタマイズ」のトピックで、**支援テクノロジーのサポート**&#x200B;に関するヘルプトピックを参照してください。例えば、ビデオビューアの[支援テクノロジーのサポート](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html?lang=ja)や、インタラクティブ画像ビューアの[支援テクノロジーのサポート](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html#viewers-for-aem-assets-only)を参照してください。

## Dynamic Mediaでのクローズドキャプションのサポート {#closed-caption-support}

Dynamic Mediaでは、クローズドキャプションを使用したビデオおよびアダプティブビデオセットの配信がサポートされています。 キャプションは、ビデオコンテンツの上に表示する必要があります。

詳しくは、 [Dynamic Mediaのビデオ — ビデオへのクローズドキャプションまたは字幕の追加](/help/assets/video.md#adding-captions-to-video).

>[!MORELIKETHIS]
>
>* [アドビソリューションのアクセシビリティ](https://www.adobe.com/accessibility.html)
>* [ [!DNL Experience Manager Assets]](/help/assets/accessibility.md) でのアクセシビリティ

