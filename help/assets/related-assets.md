---
title: 関連アセット
description: 一部の共通属性を共有するデジタルアセットを関連付ける方法について説明します。また、デジタルアセット間にソースから派生した関係を作成します。
contentOwner: AG
role: User
feature: Collaboration,Asset Management
exl-id: ddb69727-74a0-4a4d-a14e-7d3bb5ceea2a
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 100%

---

# 関連アセット {#related-assets}

[!DNL Adobe Experience Manager Assets] では、関連するアセット機能を使用して、組織のニーズに基づいて手動でアセットを関連付けることができます。例えば、ライセンスファイルを、類似のトピックのアセットまたは画像／ビデオに関連付けることができます。特定の共通属性を共有するアセットを関連付けることができます。この機能を使用して、アセット間にソース／派生関係を作成することもできます。例えば、INDD ファイルから生成した PDF ファイルがある場合、その PDF ファイルをソースの INDD ファイルに関連付けることができます。

この機能を使用すると、ベンダーや代理店と低解像度の PDF ファイルや JPG ファイルを共有し、高解像度の INDD ファイルは必要な場合のみ利用できるように柔軟に指定できます。

>[!NOTE]
>
>アセットに対する編集権限を持つユーザーのみが、アセットの関連付けと関連付け解除を行うことができます。

## アセットの関連付け {#relating-assets}

1. [!DNL Experience Manager] のインターフェイスから、関連付けるアセットの **[!UICONTROL プロパティ]**&#x200B;ページを開きます。

   ![アセットのプロパティページを開きアセットを関連付ける](assets/asset-properties-relate-assets.png)

   *図：[!DNL Assets] [!UICONTROL プロパティ]ページでのアセットの関連付け。*

   または、リスト表示からアセットを選択します。

   ![chlimage_1-273](assets/chlimage_1-273.png)

   コレクションからアセットを選択することもできます。

   ![chlimage_1-274](assets/chlimage_1-274.png)

1. 選択したアセットに別のアセットを関連付けるには、ツールバーの「**[!UICONTROL 関連付け]**」![relate assets](assets/do-not-localize/link-relate.png) アイコンをクリックします。
1. 次のいずれかの操作をおこないます。

   * アセットのソースファイルを関連付けるには、リストから「**[!UICONTROL ソース]**」を選択します。
   * 派生ファイルを関連付けるには、リストから「**[!UICONTROL 派生]**」を選択します。
   * アセット間に双方向の関係を作成するには、リストから「**[!UICONTROL その他]**」を選択します。

1. **[!UICONTROL アセットを選択]**&#x200B;画面から、関連付けをおこなうアセットの場所に移動して、選択します。

   ![chlimage_1-277](assets/chlimage_1-277.png)

1. 「**[!UICONTROL 確認]**」をクリックします。
1. 「**[!UICONTROL OK]**」をクリックして、ダイアログを閉じます。手順 3 で選択した関係に応じて、関連付けられたアセットが「**[!UICONTROL 関連]**」セクションの適切なカテゴリに表示されます。例えば、関連付けたアセットが現在のアセットのソースファイルの場合は、「**[!UICONTROL ソース]**」に表示されます。

   ![chlimage_1-278](assets/chlimage_1-278.png)

1. アセットの関連付けを解除するには、「**[!UICONTROL 関連付けを解除]**」![unrelate assets](assets/do-not-localize/link-unrelate-icon.png) をクリックします。

1. **[!UICONTROL 関係を削除]**&#x200B;ダイアログで関連付けを解除するアセットを選択して、「**[!UICONTROL 関連付けを解除]**」をクリックまたはタップします。

   ![chlimage_1-280](assets/chlimage_1-280.png)

1. 「**[!UICONTROL OK]**」をクリックして、ダイアログを閉じます。関係を削除したアセットは、「**[!UICONTROL 関連]**」セクションの関連付けられたアセットのリストから削除されます。

## 関連アセットの翻訳 {#translating-related-assets}

関連アセット機能を使用してアセット間でソースと派生の関係を作成すると、翻訳ワークフローにも役立ちます。派生アセットで翻訳ワークフローを実行すると、[!DNL Experience Manager Assets] はソースファイルが参照するすべてのアセットを自動的に取得し、翻訳用に組み込みます。このようにして、ソースアセットに参照されているアセットが、ソースおよび派生アセットとともに翻訳されます。例えば、以下のように英語のコピーに派生アセットおよびそのソースファイルが含まれている場合を考えてみます。

![chlimage_1-281](assets/chlimage_1-281.png)

ソースファイルが別のアセットに関連付けられている場合、[!DNL Experience Manager Assets] は参照されているアセットを取得し、翻訳用に組み込みます。

![アセットのプロパティページに、翻訳に含める関連アセットのソースファイルが表示されます](assets/asset-properties-source-asset.png)

*図：翻訳に含める関連アセットのソースアセット。*

1. [新しい翻訳プロジェクトを作成](translation-projects.md#create-a-new-translation-project)の手順に従って、ソースフォルダー内のアセットをターゲット言語に翻訳します。例えば、この場合はアセットをフランス語に翻訳します。

1. [!UICONTROL プロジェクト]ページから、翻訳フォルダーを開きます。

1. プロジェクトタイルをクリックして詳細ページを開きます。

   ![chlimage_1-284](assets/chlimage_1-284.png)

1. 「翻訳ジョブ」カードの下にある省略記号をクリックして、翻訳ステータスを表示します。

   ![chlimage_1-285](assets/chlimage_1-285.png)

1. アセットを選択してツールバーの「**[!UICONTROL アセットで表示]**」をクリックし、アセットの翻訳ステータスを表示します。

   ![chlimage_1-286](assets/chlimage_1-286.png)

1. ソースに関連付けられているアセットが翻訳されているかどうかを確認するには、ソースアセットをクリックします。

1. ソースに関連付けられているアセットを選択し、「**[!UICONTROL アセットで表示]**」をクリックします。翻訳された関連アセットが表示されます。
