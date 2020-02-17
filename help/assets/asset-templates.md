---
title: アセットテンプレート
description: AEM Assetsのアセットテンプレートと、アセットテンプレートを使用してマーケティングコラテラルを作成する方法について説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 70a88085a0fd6e949974aa7f1f92fdc3def3d98e

---


# Asset templates {#asset-templates}

アセットテンプレートは、デジタルメディアや印刷メディア用に視覚的に豊富なコンテンツをすばやく再利用できる特別なアセットクラスです。 アセットテンプレートには、固定メッセージセクションと編集可能セクションの 2 つの部分があります。

固定メッセージセクションには、編集できないブランドロゴおよび著作権情報など、独自のコンテンツを含めることができます。編集可能なセクションには、フィールド内の視覚的な内容やテキスト的な内容を含めることができ、編集してメッセージをカスタマイズできます。

グローバルな署名を保護しながら、限られた編集を柔軟に行えるので、コンテンツの迅速な適合と配信を実現するための最適な構築ブロックとなり、様々な機能のコンテンツアーティファクトとなります。 コンテンツを再利用することで、印刷チャネルとデジタルチャネルの管理コストを削減し、これらのチャネル間で全体的で一貫性のあるエクスペリエンスを提供できます。

マーケティング担当者は、AEM Assets内にテンプレートを保存および管理し、単一のベーステンプレートを使用して、パーソナライズされた複数の印刷エクスペリエンスを簡単に作成できます。 パンフレット、チラシ、はがき、名刺など、様々なタイプのマーケティング資料を作成して、顧客にマーケティングメッセージを明確に伝えることができます。 また、既存の、または新しいプリント出力から複数ページのプリント出力をアセンブルできます。特に、デジタルおよびプリントエクスペリエンスを簡単に同時配信して、一貫性のある統合されたエクスペリエンスをユーザーに提供できます。

アセットテンプレートは主にAdobe inDesignファイルですが、Adobe inDesignに精通していることは、優れたアーティファクトを作成する上での障害とはなりません。 Adobe inDesignテンプレートのフィールドを、カタログの作成時に必要な製品フィールドにマップする必要はありません。 テンプレートは、WYSIWYGモードでWebインターフェイス上で直接編集できます。 ただし、Adobe inDesignで編集の変更を処理するには、まずAEM Assetsを設定してAdobe inDesignサーバーと統合する必要があります。

Adobe inDesignテンプレートをWebインターフェイスから編集できるので、クリエイティブとマーケティング担当者のコラボレーションが促進され、地域プロモーションの取り組みのマーケティングに要する時間が短縮されます。

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

## 販促資料の作成 {#creating-a-collateral}

今後のキャンペーンのために、パンフレット、チラシおよび広告など、デジタルの印刷可能な販促物を作成し、世界中のアウトレットストアで共有するシナリオについて考えてみます。テンプレートに基づいた販促物の作成は、チャネルをまたいで統合されたカスタマーエクスペリエンスを実現するのに役立ちます。デザイナーは、InDesign などのクリエイティブソリューションを使用してキャンペーンテンプレート（単一ページまたは複数ページ）を作成し、テンプレートを AEM Assets にアップロードできます。コラテラルを作成する前に、1つ以上のINDDテンプレートをExperience Managerにアップロードし、Experience Managerで事前に使用できるようにします。

1. AEMロゴをクリックまたはタップし、「アセット」をクリックまたはタップします。

1. オプションから、「**[!UICONTROL テンプレート]**」を選択します。

   ![chlimage_1-101](assets/chlimage_1-306.png)

1. 「**[!UICONTROL 作成]**」をクリックまたはタップし、メニューから作成する販促物を選択します。For example, choose **[!UICONTROL Brochure]**.

   ![chlimage_1-102](assets/chlimage_1-307.png)

1. 1つ以上のINDDテンプレートをExperience Managerにアップロードし、Experience Managerで事前に使用できるようにします。 パンフレット用のテンプレートを選択して、「**[!UICONTROL 次へ]**」をクリックまたはタップします。

   ![chlimage_1-103](assets/chlimage_1-308.png)

1. パンフレットの名前と、オプションで説明を指定します。

   ![chlimage_1-104](assets/chlimage_1-309.png)

1. （オプション）「タグ **** 」をタップし、パンフレットに使用する1つまたは複数のタグを選択します。 Tap **[!UICONTROL Confirm]** to confirm your selection.

   ![chlimage_1-105](assets/chlimage_1-310.png)

1. 「**[!UICONTROL 作成]**」をクリックします。新しいパンフレットが作成されたことを確認するダイアログが表示されます。「**[!UICONTROL 開く]**」をクリックまたはタップして、パンフレットを編集モードで開きます。

   <!--![chlimage_1-106](assets/.png) -->

   または、ダイアログを閉じて、開始したテンプレートページのフォルダーに移動し、作成したパンフレットを表示します。販促物のタイプがカード表示のサムネールに表示されます。例えば、この場合、サムネールにパンフレットと表示されます。

   ![chlimage_1-107](assets/chlimage_1-312.png)

## コラテラルの編集 {#editing-a-collateral}

販促物を作成したら、すぐに編集できます。または、テンプレートページやアセットページから開きます。

1. 販促物を編集するために開くには、次のいずれかの操作をおこないます。

   * Open the collateral (brochure in this case) you created in step 7 of [Create a collateral](/help/assets/asset-templates.md#creating-a-collateral).
   * テンプレートページで、販促物を作成したフォルダーに移動して、販促物のサムネール上にある編集クイックアクションをクリックまたはタップします。
   * In the asset page for the collateral, tap **[!UICONTROL Edit]** from the toolbar.
   * コラテラルを選択し、ツールバー **[!UICONTROL から]** 「編集」をタップします。
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

1. 編集可能なフィールドのテキストを変更するには、編集可能なフィールドのリストからテキストフィールドをクリックまたはタップして、フィールドのテキストを編集します。

   ![chlimage_1-111](assets/chlimage_1-316.png)

   提供されるオプションを使用して、テキストプロパティ（例えば、フォントスタイル、カラー、サイズなど）を編集できます。

1. 「プレビ **[!UICONTROL ュー]** 」をタップして、テキストの変更をプレビューします。

   ![chlimage_1-112](assets/chlimage_1-317.png)

1. To swap an image, tap the **[!UICONTROL Asset Finder]**.

   ![chlimage_1-113](assets/chlimage_1-318.png)

1. 編集可能なフィールドのリストから画像フィールドを選択して、アセットピッカーから編集可能なフィールドに目的の画像をドラッグします。

   ![chlimage_1-114](assets/chlimage_1-319.png)

   また、キーワード、タグおよび公開ステータスに基づいて画像を検索できます。AEM Assets リポジトリを参照して、目的の画像の場所に移動できます。

   ![chlimage_1-115](assets/chlimage_1-320.png)

1. 「プレビ **[!UICONTROL ュー]** 」をタップして画像をプレビューします。

   ![chlimage_1-116](assets/chlimage_1-321.png)

1. 複数ページのコラテラル内の特定のページを編集するには、下部のページナビゲーターを使用します。

   ![chlimage_1-117](assets/chlimage_1-322.png)

1. Tap **[!UICONTROL Preview]**  on the toolbar to preview all the changes. Click/tap **[!UICONTROL Done]** to save the editing changes to the collateral.

   >[!NOTE]
   >
   >「プレビュー」および「完了」アイコンは、販促物内の編集可能な画像フィールドに見つからないアイコンがない場合にのみ有効になります。販促物に見つからないアイコンがある場合、これは AEM が InDesign テンプレート内の画像を解決できないことが原因です。通常、AEM は次の場合に画像を解決できません。
   >
   >    * 画像が基になるInDesignテンプレートに埋め込まれない
   >    * 画像がローカルファイルシステムからリンクされている
   >
   >AEM が画像を解決できるようにするには、次の操作をおこないます。
   >
   >    * InDesign テンプレートを作成する際に画像を埋め込む（[リンクと埋め込みグラフィックについて](https://helpx.adobe.com/indesign/using/graphics-links.html)を参照）。
   >    * ローカルファイルシステムに AEM をマウントして、見つからないアイコンを既存の AEM アセットにマッピングする。
   >
   >For more information around working with InDesign documents, see [Best Practices for Working with InDesign Documents in AEM](https://helpx.adobe.com/experience-manager/kb/best-practices-idd-docs-aem.html).

1. パンフレットの PDF レンディションを生成するには、ダイアログで Acrobat オプションを選択し、「**[!UICONTROL 続行]**」をクリックします。
1. 開始したフォルダーに販促物が作成されます。レンディションを表示するには、販促物を開いて、グローバルナビゲーションリストから「**[!UICONTROL レンディション]**」を選択します。

   ![chlimage_1-118](assets/chlimage_1-323.png)

1. レンディションのリストからPDFレンディションをクリックまたはタップして、PDFファイルをダウンロードします。 PDF ファイルを開いて、販促物を確認します。

   ![chlimage_1-119](assets/chlimage_1-324.png)

## Merge collateral {#merge-collateral}

1. AEM のロゴをクリックまたはタップして、ナビゲーションページの「アセット」をクリックまたはタップします。
1. オプションから、「**[!UICONTROL テンプレート]**」を選択します。
1. Click/tap **[!UICONTROL Create]** and the choose **[!UICONTROL Merge]** from the menu.

   ![chlimage_1-120](assets/chlimage_1-325.png)

1. テンプレート [!UICONTROL の結合ページで] 、「結合」をタッ **[!UICONTROL プします]**。

   ![chlimage_1-121](assets/chlimage_1-326.png)

1. 統合する販促物の場所に移動して、統合する販促物のサムネールをクリックまたはタップして選択します。

   ![chlimage_1-122](assets/chlimage_1-327.png)

   「Omnisearch」ボックスからテンプレートを検索することもできます。

   ![chlimage_1-123](assets/chlimage_1-328.png)

   AEM Assets リポジトリまたはコレクションを参照して、目的のテンプレートの場所に移動し、統合するテンプレートを選択できます。

   ![chlimage_1-124](assets/chlimage_1-329.png)

   様々なフィルターを適用して、目的のテンプレートを検索できます。例えば、ファイルタイプやタグに基づいてテンプレートを検索できます。

   ![chlimage_1-125](assets/chlimage_1-330.png)

1. ツールバーから「**[!UICONTROL 次へ]**」をクリックまたはタップします。
1. In the **[!UICONTROL Preview &amp; Reorder]** screen, rearrange the templates if required and preview the selection of templates to merge. 次に、ツールバーから「]**次へ**[!UICONTROL 」をクリックまたはタップします。

   ![chlimage_1-126](assets/chlimage_1-331.png)

1. テンプレートを設定画面で、コラテラルの名前を指定します。 オプションで、適切なタグを指定します。PDF 形式で出力を書き出す場合、「**Acrobat（.PDF）**」オプションを選択します。デフォルトでは、販促物は JPG および InDesign 形式で書き出されます。To change the display thumbnail for the multi-page collateral, click/tap **[!UICONTROL Change Thumbnail]**.

   ![chlimage_1-127](assets/chlimage_1-332.png)

1. ダイアログで「**[!UICONTROL 保存]**」をクリックまたはタップし、「**[!UICONTROL OK]**」をクリックまたはタップしてダイアログを閉じます。複数ページのコラテラルが、最初に使用したフォルダーに作成されます。

   >[!NOTE]
   >
   >統合された販促物を後で編集したり、他の販促物を作成するために使用したりすることはできません。
