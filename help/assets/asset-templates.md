---
title: アセットテンプレート
description: AEM Assetsのアセットテンプレートについて、およびアセットテンプレートを使用してマーケティングコラテラルを作成する方法について説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: c7d0bcbf39adfc7dfd01742651589efb72959603

---


# Asset templates {#asset-templates}

アセットテンプレートは、デジタルメディアや印刷メディア用に視覚的に豊富なコンテンツをすばやく再利用できる特別なアセットクラスです。 アセットテンプレートには、固定メッセージセクションと編集可能セクションの 2 つの部分があります。

固定メッセージセクションには、編集できないブランドロゴおよび著作権情報など、独自のコンテンツを含めることができます。編集可能なセクションには、フィールド内の視覚的な内容やテキスト的な内容を含めることができます。この内容は、メッセージをカスタマイズするために編集できます。

グローバルな署名を保護しながら、編集を制限する柔軟性が高まると、アセットテンプレートは様々な機能のコンテンツアーティファクトとして、コンテンツの迅速な適合と配信を実現する理想的な構成要素になります。 コンテンツを再利用することで、印刷やデジタルチャネルの管理に要するコストを削減し、これらのチャネル全体で一貫性のある全体的なエクスペリエンスを提供できます。

マーケティング担当者は、AEM Assets内にテンプレートを保存および管理し、単一のベーステンプレートを使用して、パーソナライズされた複数の印刷エクスペリエンスを簡単に作成できます。 顧客にマーケティングメッセージを明確に伝えるために、パンフレット、チラシ、はがき、名刺など、様々なタイプのマーケティング資料を作成できます。 また、既存の、または新しいプリント出力から複数ページのプリント出力をアセンブルできます。特に、デジタルおよびプリントエクスペリエンスを簡単に同時配信して、一貫性のある統合されたエクスペリエンスをユーザーに提供できます。

アセットテンプレートは主にAdobe InDesignファイルですが、Adobe InDesignに慣れていても素晴らしいアーティファクトを作成する上での障害とはなりません。 Adobe InDesignテンプレートのフィールドを、カタログの作成時に必要な製品フィールドにマップする必要はありません。 テンプレートは、Webインターフェイス上でWYSIWYGモードで直接編集できます。 ただし、Adobe InDesignで編集の変更を処理するには、まずAEM Assetsを設定してAdobe InDesignサーバーと統合する必要があります。

WebインターフェイスからAdobe InDesignテンプレートを編集できるので、クリエイティブとマーケティング担当者のコラボレーションが促進され、地域プロモーションの取り組みのタイムアウトが短縮されます。

アセットテンプレートを使用すると、次のことができます。

* Web インターフェイスから編集可能テンプレートフィールドを変更する
* フォントサイズ、スタイル、タイプなど、タグレベルでテキストの基本スタイルを制御する
* コンテンツピッカーを使用してテンプレート内の画像を変更する
* テンプレートの編集をプレビューする
* 複数のテンプレートファイルを統合して複数ページの成果物を作成する

販促物のテンプレートを選択すると、AEM Assets は、編集可能なテンプレートのコピーを作成します。元のテンプレートは保持されるので、全体的な表記の元の状態を保つことができ、再利用してブランドの一貫性を強制できます。

親フォルダー内の更新されたファイルを次の形式で書き出すことができます。

* INDD
* PDF
* JPG

また、これらの形式でローカルシステムに出力をダウンロードできます。

## 資料の作成 {#creating-a-collateral}

今後のキャンペーンのために、パンフレット、チラシおよび広告など、デジタルの印刷可能な販促物を作成し、世界中のアウトレットストアで共有するシナリオについて考えてみます。テンプレートに基づいた販促物の作成は、チャネルをまたいで統合されたカスタマーエクスペリエンスを実現するのに役立ちます。デザイナーは、InDesign などのクリエイティブソリューションを使用してキャンペーンテンプレート（単一ページまたは複数ページ）を作成し、テンプレートを AEM Assets にアップロードできます。コラテラルを作成する前に、1つ以上のINDDテンプレートをExperience Managerにアップロードし、Experience Managerで事前に使用できるようにします。

1. Experience Managerインターフェイスで、「アセット」をク [!UICONTROL リックしま]す。

1. オプションから、「**[!UICONTROL テンプレート]**」を選択します。

   ![chlimage_1-101](assets/chlimage_1-306.png)

1. Click **[!UICONTROL Create]**, and then choose the collateral you want to create from the menu. For example, choose **[!UICONTROL Brochure]**.

   ![chlimage_1-102](assets/chlimage_1-307.png)

1. 1つ以上のINDDテンプレートをExperience Managerにアップロードし、事前にExperience Managerで使用できるようにします。 Choose a template for your brochure, and click **[!UICONTROL Next]**.

   ![chlimage_1-103](assets/chlimage_1-308.png)

1. パンフレットの名前と、オプションで説明を指定します。

   ![chlimage_1-104](assets/chlimage_1-309.png)

1. （オプション）「タグ **** 」をクリックし、パンフレットの1つ以上のタグを選択します。 Click **[!UICONTROL Confirm]** to confirm your selection.

   ![chlimage_1-105](assets/chlimage_1-310.png)

1. 「**[!UICONTROL 作成]**」をクリックします。新しいパンフレットが作成されたことを確認するダイアログが表示されます。Click **[!UICONTROL Open]** to open the brochure in edit mode.

   <!--![chlimage_1-106](assets/.png) -->

   または、ダイアログを閉じて、開始したテンプレートページのフォルダーに移動し、作成したパンフレットを表示します。販促物のタイプがカード表示のサムネールに表示されます。例えば、この場合、サムネールにパンフレットと表示されます。

   ![chlimage_1-107](assets/chlimage_1-312.png)

## コラテラルの編集 {#editing-a-collateral}

販促物を作成したら、すぐに編集できます。または、テンプレートページやアセットページから開きます。

1. 販促物を編集するために開くには、次のいずれかの操作をおこないます。

   * Open the collateral (brochure in this case) you created in step 7 of [Create a collateral](/help/assets/asset-templates.md#creating-a-collateral).
   * From the Templates page, navigate to a folder where you created the collateral, and click the [!UICONTROL Edit] quick action on the thumbnail of a collateral.
   * In the asset page for the collateral, click **[!UICONTROL Edit]** from the toolbar.
   * Select the collateral and click **[!UICONTROL Edit]** from the toolbar.
   <!--![chlimage_1-108](assets/chlimage_1-313.png) -->

   アセットファインダーおよびテキストエディターがページの左側に表示されます。デフォルトで、テキストエディターが開きます。

   テキストエディターを使用して、テキストフィールドに表示させるテキストを変更します。タグレベルで、フォントサイズ、スタイル、カラーおよびタイプを変更できます。

   アセットファインダーを使用して、AEM Assets 内の画像を参照または検索し、テンプレート内の編集可能な画像を選択した画像と置き換えることができます。

   ![chlimage_1-109](assets/chlimage_1-314.png)

   編集可能であることは右側に表示されます。AEM Assets で編集可能なフィールドの場合、テンプレートの対応するフィールドが InDesign でタグ付けされている必要があります。つまり、InDesignで編集可能とマークする必要があります。

   ![chlimage_1-110](assets/chlimage_1-315.png)

   >[!NOTE]
   >
   >AEM Assets で InDesign テンプレートからデータを抽出して編集できるようにするために、AEM インスタンスが InDesign サーバーと統合されていることを確認します。For details, see [Integrating AEM Assets with InDesign Server](/help/assets/indesign.md).

1. 編集可能なフィールド内のテキストを変更するには、編集可能なフィールドのリストからテキストフィールドをクリックし、フィールド内のテキストを編集します。

   ![chlimage_1-111](assets/chlimage_1-316.png)

   提供されるオプションを使用して、テキストプロパティ（例えば、フォントスタイル、カラー、サイズなど）を編集できます。

1. 「 **[!UICONTROL プレビュー]** 」をクリックし、テキストの変更をプレビューします。

   ![chlimage_1-112](assets/chlimage_1-317.png)

1. To swap an image, click the **[!UICONTROL Asset Finder]**.

   ![chlimage_1-113](assets/chlimage_1-318.png)

1. 編集可能なフィールドのリストから画像フィールドを選択して、アセットピッカーから編集可能なフィールドに目的の画像をドラッグします。

   ![chlimage_1-114](assets/chlimage_1-319.png)

   また、キーワード、タグおよび公開ステータスに基づいて画像を検索できます。AEM Assets リポジトリを参照して、目的の画像の場所に移動できます。

   ![chlimage_1-115](assets/chlimage_1-320.png)

1. 「 **[!UICONTROL プレビュー]** 」をクリックし、画像をプレビューします。

   ![chlimage_1-116](assets/chlimage_1-321.png)

1. 複数ページのコラテラル内の特定のページを編集するには、下部のページナビゲーターを使用します。

   ![chlimage_1-117](assets/chlimage_1-322.png)

1. Click **[!UICONTROL Preview]**  on the toolbar to preview all the changes. Click **[!UICONTROL Done]** to save the editing changes to the collateral.

   >[!NOTE]
   >
   >「プレビュー」および「完了」アイコンは、販促物内の編集可能な画像フィールドに見つからないアイコンがない場合にのみ有効になります。販促物に見つからないアイコンがある場合、これは AEM が InDesign テンプレート内の画像を解決できないことが原因です。通常、AEM は次の場合に画像を解決できません。
   >
   >    * 画像は、基になるInDesignテンプレートに埋め込まれません。
   >    * 画像がローカルファイルシステムからリンクされている
   >
   >AEM が画像を解決できるようにするには、次の操作をおこないます。
   >
   >    * InDesign テンプレートを作成する際に画像を埋め込む（[リンクと埋め込みグラフィックについて](https://helpx.adobe.com/jp/indesign/using/graphics-links.html)を参照）。
   >    * ローカルファイルシステムに AEM をマウントして、見つからないアイコンを既存の AEM アセットにマッピングする。
   >
   >For more information around working with InDesign documents, see [Best Practices for Working with InDesign Documents in AEM](https://helpx.adobe.com/jp/experience-manager/kb/best-practices-idd-docs-aem.html).

1. パンフレットの PDF レンディションを生成するには、ダイアログで Acrobat オプションを選択し、「**[!UICONTROL 続行]**」をクリックします。
1. 開始したフォルダーに販促物が作成されます。レンディションを表示するには、販促物を開いて、グローバルナビゲーションリストから「**[!UICONTROL レンディション]**」を選択します。

   ![chlimage_1-118](assets/chlimage_1-323.png)

1. レンディションのリストでPDFレンディションをクリックし、PDFファイルをダウンロードします。 PDF ファイルを開いて、販促物を確認します。

   ![chlimage_1-119](assets/chlimage_1-324.png)

## Merge collateral {#merge-collateral}

1. Experience Managerインターフェイスで、ナビゲーションペ [!UICONTROL ージの] 「アセット」をクリックします。

1. オプションから、「**[!UICONTROL テンプレート]**」を選択します。

1. Click **[!UICONTROL Create]** and the choose **[!UICONTROL Merge]** from the menu.

   ![chlimage_1-120](assets/chlimage_1-325.png)

1. テンプレート [!UICONTROL の結合ページで] 、「結合」をクリッ **[!UICONTROL クします]**。

   ![chlimage_1-121](assets/chlimage_1-326.png)

1. マージする販促物の場所にナビゲートし、マージする販促物のサムネールをクリックして選択します。

   ![chlimage_1-122](assets/chlimage_1-327.png)

   また、「Omnisearch」ボックスからテンプレートを検索することもできます。

   ![chlimage_1-123](assets/chlimage_1-328.png)

   AEM Assets リポジトリまたはコレクションを参照して、目的のテンプレートの場所に移動し、統合するテンプレートを選択できます。

   ![chlimage_1-124](assets/chlimage_1-329.png)

   様々なフィルターを適用して、目的のテンプレートを検索できます。例えば、ファイルタイプやタグに基づいてテンプレートを検索できます。

   ![chlimage_1-125](assets/chlimage_1-330.png)

1. Click **[!UICONTROL Next]** from the toolbar.
1. In the **[!UICONTROL Preview &amp; Reorder]** screen, rearrange the templates if required and preview the selection of templates to merge. Then, click **[!UICONTROL Next]** from the toolbar.

   ![chlimage_1-126](assets/chlimage_1-331.png)

1. In the [!UICONTROL Configure Template] screen, specify a name for the collateral. オプションで、適切なタグを指定します。If you want to export the output in PDF format, select **[!UICONTROL Acrobat (.PDF)]**. デフォルトでは、販促物は JPG および InDesign 形式で書き出されます。To change the display thumbnail for the multi-page collateral, click **[!UICONTROL Change Thumbnail]**.

   ![chlimage_1-127](assets/chlimage_1-332.png)

1. Click **[!UICONTROL Save]** and then click **[!UICONTROL OK]** in the dialog to close the dialog. 複数ページのコラテラルが、最初に作成したフォルダに作成されます。

   >[!NOTE]
   >
   >統合された販促物を後で編集したり、他の販促物を作成するために使用したりすることはできません。
