---
title: 翻訳するアセットの準備
description: 言語ルートフォルダーを作成して、多言語アセットをサポートする翻訳用のアセットを準備します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 57%

---


# 翻訳するアセットの準備 {#preparing-assets-for-translation}

多言語アセットとは、複数の言語のバイナリ、メタデータ、タグを含むアセットです。通常、アセットのバイナリ、メタデータ、タグに使用される言語は 1 つですが、多言語プロジェクト用に他の言語へと翻訳されます。

In [!DNL Adobe Experience Manager Assets], multilingual assets are included in folders, where each folder contains the assets in a different language.

各言語のフォルダーは言語コピーと呼ばれます。言語コピーのルートフォルダー（言語ルート）が、言語コピー内のコンテンツの言語を識別します。For example, */content/dam/it* is the Italian language root for the Italian language copy. ソースアセットの翻訳の実行時に適切な言語がターゲットになるように、言語コピーは、[正しく設定された言語ルート](preparing-assets-for-translation.md#creating-a-language-root)を使用する必要があります。

最初にアセットを追加した言語コピーが言語プライマリです。言語プライマリは、他の言語に翻訳されるソースです。サンプルフォルダー階層にはいくつかの言語ルートが含まれています。

```
 /content
  /- dam
   |- en
   |- fr
   |- de
   |- es
   |- it
   |- ja
   |- zh
```

翻訳するアセットを準備するには、次の手順を実行します。

1. 言語プライマリの言語ルートを作成します。例えば、サンプルフォルダー階層の英語言語コピーの言語ルートは `/content/dam/en` です。Ensure that the language root is correctly configured according to the information in [Create a Language Root](preparing-assets-for-translation.md#creating-a-language-root).

1. 言語プライマリにアセットを追加します。
1. 言語コピーが必要な各ターゲット言語の言語ルートを作成します。

## Create a language root {#creating-a-language-root}

言語ルートを作成するには、フォルダーを作成し、「名前」プロパティの値として ISO 言語コードを使用します。言語ルートを作成したら、言語ルート内の任意のレベルに言語コピーを作成できます。

例えば、サンプル階層のイタリア語言語コピーのルートページの「名前」プロパティは `it` になります。The Name property is used as the name of the asset node in the repository, and therefore determines the path of the assets. (`https://[aem_server]:[port]/assets.html/content/dam/it/`).

1. From the [!DNL Assets] console, click **[!UICONTROL Create]** and choose **[!UICONTROL Folder]** from the menu.

   ![フォルダーを作成](assets/Create-folder.png)

1. In the **[!UICONTROL Name]** field type the country code in the format of `<language-code>`.

   ![フォルダー内の追加言語コード](assets/Add-language-code-in-folder.png)

1. 「**[!UICONTROL 作成]**」をクリックします。The language root is created in the [!DNL Assets] console.

## 言語ルートの表示 {#viewing-language-roots}

[!DNL Experience Manager] インターフェイスには、内で作成された言語ルートのリストを表示する **[!UICONTROL 参照]** パネルが用意されて [!DNL Assets]います。

1. In the [!DNL Assets] console, select the language primary for which you want to create language copies.
1. 左側のレールで、「 **[!UICONTROL 参照]** 」オプションを選択し、  参照ペインを開きます。

   ![chlimage_1-122](assets/chlimage_1-122.png)

1. In the References pane, click **[!UICONTROL Language Copies]**. The [!UICONTROL Language Copies] panel shows the language copies of the assets.

   ![言語コピー](assets/lang-copy2.png)
