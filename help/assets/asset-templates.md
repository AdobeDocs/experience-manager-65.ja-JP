---
title: のアセットテンプレート [!DNL Adobe Experience Manager Assets]。
description: Learn about Asset templates in [!DNL Adobe Experience Manager Assets] and how to use asset templates to create marketing collateral.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 91caca39b0b6c5c0c98b58be02f518901a3d90e3
workflow-type: tm+mt
source-wordcount: '1554'
ht-degree: 32%

---


# Asset templates {#asset-templates}

アセットテンプレートは、デジタルメディアや印刷メディア向けに視覚的に豊富なコンテンツをすばやく再利用できる特別なアセットクラスです。 アセットテンプレートには、固定メッセージセクションと編集可能セクションの 2 つの部分があります。固定メッセージセクションには、編集できないブランドロゴおよび著作権情報など、独自のコンテンツを含めることができます。編集可能なセクションには、フィールド内の視覚的な内容とテキスト的な内容を含めることができます。これらの内容は、編集してメッセージをカスタマイズできます。

グローバルな署名を保護しながら編集を制限する柔軟性により、様々な機能のコンテンツアーティファクトとして、コンテンツの迅速な適合と配信に最適なアセットテンプレートを作成できます。 コンテンツを再利用することで、印刷チャネルやデジタルチャネルの管理コストを削減し、それらの管理全体にわたって一貫性のある全体的な体験を提供できます。

As a marketer, you can store and manage templates within [!DNL Experience Manager Assets] and use a single base template to create multiple personalized print experiences with ease. パンフレット、チラシ、はがき、名刺など、様々なタイプのマーケティング資料を作成して、顧客にマーケティングメッセージを明確に伝えることができます。 また、既存の、または新しいプリント出力から複数ページのプリント出力をアセンブルできます。特に、デジタルおよびプリントエクスペリエンスを簡単に同時配信して、一貫性のある統合されたエクスペリエンスをユーザーに提供できます。

While asset templates are mostly [!DNL Adobe InDesign] files, proficiency in [!DNL Adobe InDesign] is not a barrier to creating stellar artifacts. You need not map the fields of your [!DNL Adobe InDesign] template with your product fields that you otherwise require to when creating catalogs. テンプレートは、WYSIWYGモードで直接Webインターフェイス上で編集できます。 However, for [!DNL Adobe InDesign] to process your editing changes, you must first configure [!DNL Experience Manager Assets] to integrate with [!DNL Adobe InDesign Server].

Webインターフェイスから [!DNL Adobe InDesign] テンプレートを編集できるので、クリエイティブスタッフとマーケティングスタッフのコラボレーションが促進されます。 コンテンツの速度が速くなると、マーケティング関連資料の市場投入時間が短縮されます。

アセットテンプレートを使用すると、次のことを実行できます。

* Web インターフェイスから編集可能テンプレートフィールドを変更する.
* フォントサイズ、スタイル、タイプなど、タグレベルでテキストの基本スタイルを制御する.
* コンテンツピッカーを使用してテンプレート内の画像を変更する.
* テンプレートの編集をプレビューする.
* 複数のテンプレートファイルを統合して複数ページの成果物を作成する.

When you choose a template for your collateral, [!DNL Experience Manager Assets] creates a copy of the template that you can edit. 元のテンプレートは保持されるので、全体的な表記の元の状態を保つことができ、再利用してブランドの一貫性を強制できます。

更新したファイルは、親フォルダー内のINDD、PDFまたはJPG形式で書き出すことができます。 これらの形式の出力は、ローカルファイルシステムにダウンロードすることもできます。

## 販促資料の作成 {#creating-a-collateral}

今後のキャンペーンのために、パンフレット、チラシおよび広告など、デジタルの印刷可能な販促物を作成し、世界中のアウトレットストアで共有するシナリオについて考えてみます。テンプレートに基づいた販促物の作成は、チャネルをまたいで統合されたカスタマーエクスペリエンスを実現するのに役立ちます。Designers can create the campaign templates (single-page or multi-page) using a creative solution, such as [!DNL InDesign] and upload the templates to [!DNL Experience Manager Assets] for you. コラテラルを作成する前に、1つ以上のINDDテンプレートをにアップロードし、あらかじめ利用できるようにしてお [!DNL Experience Manager] きます。

1. インター [!DNL Experience Manager] フェイスで、「 [!UICONTROL アセット]」をクリックします。

1. オプションから、「**[!UICONTROL テンプレート]**」を選択します。

   ![chlimage_1-101](assets/chlimage_1-306.png)

1. Click **[!UICONTROL Create]**, and then choose the collateral you want to create from the menu. For example, choose **[!UICONTROL Brochure]**.

   ![chlimage_1-102](assets/chlimage_1-307.png)

1. 1つ以上のINDDテンプレートをにアップロードし、あらかじめ利用でき [!DNL Experience Manager] るようにします。 Choose a template for your brochure, and click **[!UICONTROL Next]**.

   ![chlimage_1-103](assets/chlimage_1-308.png)

1. パンフレットの名前と、オプションで説明を指定します。

   ![chlimage_1-104](assets/chlimage_1-309.png)

1. （オプション）「 **[!UICONTROL タグ]** 」をクリックし、パンフレットに使用するタグを1つ以上選択します。 Click **[!UICONTROL Confirm]** to confirm your selection.

   ![chlimage_1-105](assets/chlimage_1-310.png)

1. 「**[!UICONTROL 作成]**」をクリックします。新しいパンフレットが作成されたことを確認するダイアログが表示されます。Click **[!UICONTROL Open]** to open the brochure in edit mode.

   <!--![chlimage_1-106](assets/.png) -->

   または、ダイアログを閉じて、開始したテンプレートページのフォルダーに移動し、作成したパンフレットを表示します。販促物のタイプがカード表示のサムネールに表示されます。For example, in this case, the word [!UICONTROL Brochure] is displayed on the thumbnail.

   ![chlimage_1-107](assets/chlimage_1-312.png)

## コラテラルの編集 {#editing-a-collateral}

販促物を作成したら、すぐに編集できます。Alternatively, you open it from the [!UICONTROL Templates] page or the asset page.

1. 販促物を編集するために開くには、次のいずれかの操作をおこないます。

   * Open the collateral (brochure in this case) you created in step 7 of [Create a collateral](/help/assets/asset-templates.md#creating-a-collateral).
   * From the Templates page, navigate to a folder where you created the collateral, and click the [!UICONTROL Edit] quick action on the thumbnail of a collateral.
   * In the asset page for the collateral, click **[!UICONTROL Edit]** from the toolbar.
   * Select the collateral and click **[!UICONTROL Edit]** from the toolbar.

   <!--![chlimage_1-108](assets/chlimage_1-313.png) -->

   アセットファインダーおよびテキストエディターがページの左側に表示されます。デフォルトで、テキストエディターが開きます。

   テキストエディターを使用して、テキストフィールドに表示させるテキストを変更します。タグレベルで、フォントサイズ、スタイル、カラーおよびタイプを変更できます。

   Using the asset finder, you can browse or search for images within [!DNL Experience Manager Assets] and replace the editable images in the template with images of your choice.

   ![chlimage_1-109](assets/chlimage_1-314.png)

   編集可能であることは右側に表示されます。For a field to be editable in [!DNL Experience Manager Assets], corresponding field in the template must be tagged in [!DNL InDesign]. In other words, they should be marked as editable in [!DNL InDesign].

   ![chlimage_1-110](assets/chlimage_1-315.png)

   >[!NOTE]
   >
   >Ensure that your [!DNL Experience Manager] deployment is integrated with an [!DNL InDesign Server] to enable [!DNL Experience Manager Assets] to extract data from the [!DNL InDesign] template and make it available for editing. 詳しくは、Experience ManagerアセットとInDesign Serverの [統合を参照してください](/help/assets/indesign.md)。

1. 編集可能なフィールド内のテキストを変更するには、編集可能なフィールドのリストからテキストフィールドをクリックし、フィールド内のテキストを編集します。

   ![chlimage_1-111](assets/chlimage_1-316.png)

   提供されたオプションを使用して、フォントスタイル、色、サイズなどのテキストプロパティを編集できます。

1. 「 **[!UICONTROL プレビュー]** 」をクリックして、テキストの変更をプレビューします。

   ![chlimage_1-112](assets/chlimage_1-317.png)

1. To swap an image, click the **[!UICONTROL Asset Finder]**.

   ![chlimage_1-113](assets/chlimage_1-318.png)

1. 編集可能なフィールドのリストから画像フィールドを選択して、アセットピッカーから編集可能なフィールドに目的の画像をドラッグします。

   ![chlimage_1-114](assets/chlimage_1-319.png)

   また、キーワード、タグおよび公開ステータスに基づいて画像を検索できます。You can browse through the [!DNL Experience Manager Assets] repository and navigate to the location of the desired image.

   ![chlimage_1-115](assets/chlimage_1-320.png)

1. 「 **[!UICONTROL プレビュー]** 」をクリックしてプレビューを行います。

   ![chlimage_1-116](assets/chlimage_1-321.png)

1. 複数ページのコラテラル内の特定のページを編集するには、下部のページナビゲーターを使用します。

   ![chlimage_1-117](assets/chlimage_1-322.png)

1. Click **[!UICONTROL Preview]** on the toolbar to preview all the changes. Click **[!UICONTROL Done]** to save the editing changes to the collateral.

   >[!NOTE]
   >
   >「プレビュー」オプションと「完了」オプションは、コラテラル内の編集可能な画像フィールドに、見つからないアイコンがない場合にのみ有効です。 If there are missing icons in your collateral, it is because [!DNL Experience Manager] is unable to resolve the images in the [!DNL InDesign] template. Usually, [!DNL Experience Manager] is unable to resolve images in the following cases:
   >
   >* Images are not embedded in the underlying [!DNL InDesign] template.
   >* 画像がローカルファイルシステムからリンクされている.

   >
   >To enable [!DNL Experience Manager] to resolve images, do the following:
   >
   >* Embed images while creating [!DNL InDesign] templates (See [About links and embedded graphics](https://helpx.adobe.com/jp/indesign/using/graphics-links.html)).
   >* Mount [!DNL Experience Manager] to your local file system, and then map missing icons with existing assets in [!DNL Experience Manager].

   >
   >For more information around working with [!DNL InDesign] documents, see [best practices to work with InDesign documents in Experience Manager](https://helpx.adobe.com/jp/experience-manager/kb/best-practices-idd-docs-aem.html).

1. パンフレットの PDF レンディションを生成するには、ダイアログで Acrobat オプションを選択し、「**[!UICONTROL 続行]**」をクリックします。
1. 開始したフォルダーに販促物が作成されます。レンディションを表示するには、販促物を開いて、グローバルナビゲーションリストから「**[!UICONTROL レンディション]**」を選択します。

   ![chlimage_1-118](assets/chlimage_1-323.png)

1. レンディションのリストでPDFレンディションをクリックし、PDFファイルをダウンロードします。 PDF ファイルを開いて、販促物を確認します。

   ![chlimage_1-119](assets/chlimage_1-324.png)

## Merge collateral {#merge-collateral}

1. インター [!DNL Experience Manager] フェイスで、ナビゲーションページの「 [!UICONTROL アセット] 」をクリックします。

1. オプションから、「**[!UICONTROL テンプレート]**」を選択します。

1. Click **[!UICONTROL Create]** and the choose **[!UICONTROL Merge]** from the menu.

   ![chlimage_1-120](assets/chlimage_1-325.png)

1. テン [!UICONTROL プレートの結合] ページで、「アセットを **[!UICONTROL 結合]** 」をクリックし、アセットを ![追加します](assets/do-not-localize/assets_add_icon.png)。

1. マージするコラテラルの場所に移動し、マージするコラテラルのサムネールをクリックして選択します。

   ![chlimage_1-122](assets/chlimage_1-327.png)

   また、「Omnisearch」ボックスからテンプレートを検索することもできます。

   ![chlimage_1-123](assets/chlimage_1-328.png)

   You can browse through the [!DNL Experience Manager Assets] repository or collections, and navigate to the location of the desired templates and then select them to merge.

   ![chlimage_1-124](assets/chlimage_1-329.png)

   様々なフィルターを適用して、目的のテンプレートを検索できます。例えば、ファイルタイプやタグに基づいてテンプレートを検索できます。

   ![chlimage_1-125](assets/chlimage_1-330.png)

1. Click **[!UICONTROL Next]** from the toolbar.
1. In the **[!UICONTROL Preview &amp; Reorder]** screen, rearrange the templates if required and preview the selection of templates to merge. Then, click **[!UICONTROL Next]** from the toolbar.

   ![chlimage_1-126](assets/chlimage_1-331.png)

1. In the [!UICONTROL Configure Template] screen, specify a name for the collateral. オプションで、適切なタグを指定します。If you want to export the output in PDF format, select **[!UICONTROL Acrobat (.PDF)]**. By default, the collateral is exported in JPG and [!DNL InDesign] format. To change the display thumbnail for the multi-page collateral, click **[!UICONTROL Change Thumbnail]**.

   ![chlimage_1-127](assets/chlimage_1-332.png)

1. Click **[!UICONTROL Save]** and then click **[!UICONTROL OK]** in the dialog to close the dialog. 複数ページのコラテラルは、最初に使用したフォルダーに作成されます。

   >[!NOTE]
   >
   >統合された販促物を後で編集したり、他の販促物を作成するために使用したりすることはできません。

## ベストプラクティスと制限事項 {#best-practices-limitations-tips}

* の [!DNL InDesign] エディターはタグレベルで [!DNL Experience Manager] 機能し、1つのタグの下にあるすべてのテキストは単一のエンティティと見なされます。 編集時にテキストの書式設定とスタイルを保持するには、各段落（または異なるスタイルのテキスト）に個別にタグを付けます。
