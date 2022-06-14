---
title: 翻訳するアセットの準備
description: 多言語アセットをサポートするための翻訳用アセットを準備するには、言語ルートフォルダーを作成します。
contentOwner: AG
role: User, Admin
feature: Projects
exl-id: eee768e3-3eb4-46fa-b9ae-9ef8764a3a94
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 100%

---

# 翻訳するアセットの準備 {#preparing-assets-for-translation}

多言語アセットとは、複数の言語のバイナリ、メタデータ、タグを含むアセットです。通常、アセットのバイナリ、メタデータ、タグに使用される言語は 1 つですが、多言語プロジェクト用に他の言語へと翻訳されます。

[!DNL Adobe Experience Manager Assets] では、多言語アセットはフォルダーに含まれ、各フォルダーに異なる言語のアセットが格納されます。

各言語のフォルダーは言語コピーと呼ばれます。言語コピーのルートフォルダー（言語ルート）が、言語コピー内のコンテンツの言語を識別します。例えば、*/content/dam/it* はイタリア語の言語コピー用のイタリア語言語ルートです。ソースアセットの翻訳の実行時に適切な言語がターゲットになるように、言語コピーは、[正しく設定された言語ルート](preparing-assets-for-translation.md#creating-a-language-root)を使用する必要があります。

最初にアセットを追加した言語コピーが言語プライマリです。言語プライマリは、他の言語に翻訳されるソースです。サンプルフォルダー階層にはいくつかの言語ルートが含まれています。

```shell
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

1. 言語プライマリの言語ルートを作成します。例えば、サンプルフォルダー階層の英語言語コピーの言語ルートは `/content/dam/en` です。[言語ルートの作成](preparing-assets-for-translation.md#creating-a-language-root)に記載の情報に従って言語ルートが正しく設定されていることを確認してください。

1. 言語プライマリにアセットを追加します。
1. 言語コピーが必要な各ターゲット言語の言語ルートを作成します。

## 言語ルートの作成 {#creating-a-language-root}

言語ルートを作成するには、フォルダーを作成し、「名前」プロパティの値として ISO 言語コードを使用します。言語ルートを作成したら、言語ルート内の任意のレベルに言語コピーを作成できます。

例えば、サンプル階層のイタリア語言語コピーのルートページの「名前」プロパティは `it` になります。「名前」プロパティは、リポジトリー内の asset ノードの名前として使用されます。そのため、このプロパティによってアセットのパスが指定されます(`https://[aem_server]:[port]/assets.html/content/dam/it/`).

1. [!DNL Assets] コンソールで「**[!UICONTROL 作成]**」をクリックし、メニューから「**[!UICONTROL フォルダー]**」を選択します。

   ![フォルダーを作成](assets/Create-folder.png)

1. 「**[!UICONTROL 名前]**」フィールドに、`<language-code>` の形式で国コードを入力します。

   ![フォルダーに言語コードを追加](assets/Add-language-code-in-folder.png)

1. 「**[!UICONTROL 作成]**」をクリックします。[!DNL Assets] コンソール内に言語ルートが作成されます。

## 言語ルートの表示 {#viewing-language-roots}

[!DNL Experience Manager] インターフェイスには&#x200B;**[!UICONTROL 参照]**&#x200B;パネルがあります。このパネルには、[!DNL Assets] 内で作成した言語ルートのリストが表示されます。

1. [!DNL Assets] コンソールで、言語コピーを作成するプライマリ言語を選択します。
1. 左側のパネルから、「**[!UICONTROL 参照]**」オプションを選択して[!UICONTROL 参照]ペインを開きます。

   ![chlimage_1-122](assets/chlimage_1-122.png)

1. 参照パネルで、「**[!UICONTROL 言語コピー]**」をクリックします。アセットの言語コピーが[!UICONTROL 言語コピー]パネルに表示されます。

   ![言語コピー](assets/lang-copy2.png)
