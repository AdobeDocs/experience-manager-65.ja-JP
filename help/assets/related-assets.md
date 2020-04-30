---
title: 関連アセット
description: 共通の属性を共有するデジタルアセットを関連付ける方法を説明します。 また、デジタルアセット間のソースから派生する関係を作成します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 90f9c0b60d4b0878f56eefea838154bb7627066d

---


# 関連アセット {#related-assets}

[!DNL Adobe Experience Manager Assets] 関連アセット機能を使用して、組織のニーズに基づいて手動でアセットを関連付けることができます。 例えば、ライセンスファイルを、類似のトピックのアセットまたは画像／ビデオに関連付けることができます。特定の共通属性を共有するアセットを関連付けることができます。この機能を使用して、アセット間にソース／派生関係を作成することもできます。例えば、INDD ファイルから生成した PDF ファイルがある場合、その PDF ファイルをソースの INDD ファイルに関連付けることができます。

この機能を使用すると、ベンダーや代理店と低解像度のPDFファイルやJPGファイルを共有し、高解像度のINDDファイルを要求された場合にのみ利用できるように柔軟に調整できます。

>[!NOTE] アセットの関連付けと関連付け解除を行えるのは、アセットの編集権限を持つユーザーだけです。
>

## アセットの関連付け {#relating-assets}

1. From the Experience Manager interface, open the **[!UICONTROL Properties]** page for an asset that you want to relate.

   ![アセットのプロパティページを開き、アセットを関連付けます。](assets/asset-properties-relate-assets.png)

   *図：アセッ[!DNL Assets]トを関連付けるプロパティページ。*

   または、リスト表示からアセットを選択します。

   ![chlimage_1-273](assets/chlimage_1-273.png)

   コレクションからアセットを選択することもできます。

   ![chlimage_1-274](assets/chlimage_1-274.png)

1. 選択したアセットに別のアセットを関連付けるには、ツールバーの「**[!UICONTROL 関連付け]**」アイコンをクリックまたはタップします。

   ![chlimage_1-275](assets/chlimage_1-275.png)

1. 次のいずれかの操作をおこないます。

   * アセットのソースファイルを関連付けるには、リストから「**[!UICONTROL ソース]**」を選択します。
   * 派生ファイルを関連付けるには、リストから「**[!UICONTROL 派生]**」を選択します。
   * アセット間に双方向の関係を作成するには、リストから「**[!UICONTROL その他]**」を選択します。
   ![chlimage_1-276](assets/chlimage_1-276.png)

1. **[!UICONTROL アセットを選択]**&#x200B;画面から、関連付けをおこなうアセットの場所に移動して、選択します。

   ![chlimage_1-277](assets/chlimage_1-277.png)

1. 「**[!UICONTROL 確認]**」アイコンをクリックまたはタップします。
1. 「**[!UICONTROL OK]**」をクリックまたはタップして、ダイアログを閉じます。手順 3 で選択した関係に応じて、関連付けられたアセットが「**[!UICONTROL 関連]**」セクションの適切なカテゴリに表示されます。例えば、関連付けたアセットが現在のアセットのソースファイルの場合は、「**[!UICONTROL ソース]**」に表示されます。

   ![chlimage_1-278](assets/chlimage_1-278.png)

1. To un-relate an asset, click/tap **[!UICONTROL Unrelate]** from the toolbar.

   ![chlimage_1-279](assets/chlimage_1-279.png)

1. Select the asset(s) you want to un-relate from the **[!UICONTROL Remove Relations]** dialog, and the click/tap **[!UICONTROL Unrelate]**.

   ![chlimage_1-280](assets/chlimage_1-280.png)

1. 「**[!UICONTROL OK]**」をクリックまたはタップして、ダイアログを閉じます。関係を削除したアセットは、「**[!UICONTROL 関連]**」セクションの関連付けられたアセットのリストから削除されます。

## 関連アセットの翻訳 {#translating-related-assets}

関連アセット機能を使用してアセット間でソース／派生関係を作成すると、翻訳ワークフローにも役立ちます。When you run a translation workflow on a derived asset, [!DNL Experience Manager Assets] automatically fetches any asset that the source file references and includes it for translation. このようにして、ソースアセットに参照されているアセットが、ソースおよび派生アセットとともに翻訳されます。例えば、以下のように英語のコピーに派生アセットおよびそのソースファイルが含まれている場合を考えてみます。

![chlimage_1-281](assets/chlimage_1-281.png)

If the source file is related to another asset, [!DNL Experience Manager Assets] fetches the referenced asset and includes it for translation.

![アセットのプロパティページに、変換に含める関連アセットのソースファイルが表示されます。](assets/asset-properties-source-asset.png)

*図：翻訳に含める関連アセットのソースアセット。*

1. [新しい翻訳プロジェクトを作成](translation-projects.md#create-a-new-translation-project)の手順に従って、ソースフォルダー内のアセットをターゲット言語に翻訳します。例えば、この場合はアセットをフランス語に翻訳します。

1. From the [!UICONTROL Projects] page, open the translation folder.

   ![chlimage_1-283](assets/chlimage_1-283.png)

1. プロジェクトタイルをクリックまたはタップして詳細ページを開きます。

   ![chlimage_1-284](assets/chlimage_1-284.png)

1. 「翻訳ジョブ」カードの下にある省略記号をクリックまたはタップして、翻訳ステータスを表示します。

   ![chlimage_1-285](assets/chlimage_1-285.png)

1. アセットを選択し、ツールバーの「**[!UICONTROL アセットで表示]**」をクリックまたはタップして、アセットの翻訳ステータスを表示します。

   ![chlimage_1-286](assets/chlimage_1-286.png)

1. ソースに関連付けられているアセットが翻訳されているかどうかを確認するには、ソースアセットをクリックまたはタップします。

   ![chlimage_1-287](assets/chlimage_1-287.png)

1. ソースに関連付けられているアセットを選択し、「**[!UICONTROL アセットで表示]**」をクリックまたはタップします。翻訳された関連アセットが表示されます。

   ![chlimage_1-288](assets/chlimage_1-288.png)
