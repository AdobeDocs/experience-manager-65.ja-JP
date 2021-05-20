---
title: 翻訳するアセットの準備
description: 多言語アセットをサポートするための翻訳用アセットを準備するには、言語ルートフォルダーを作成します。
contentOwner: AG
role: Business Practitioner, Administrator
feature: プロジェクト
exl-id: eee768e3-3eb4-46fa-b9ae-9ef8764a3a94
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 62%

---

# 翻訳するアセットの準備 {#preparing-assets-for-translation}

多言語アセットとは、複数の言語のバイナリ、メタデータ、タグを含むアセットです。通常、アセットのバイナリ、メタデータ、タグに使用される言語は 1 つですが、多言語プロジェクト用に他の言語へと翻訳されます。

[!DNL Adobe Experience Manager Assets]では、多言語アセットがフォルダーに含まれ、各フォルダーには異なる言語のアセットが格納されます。

各言語のフォルダーは言語コピーと呼ばれます。言語コピーのルートフォルダー（言語ルート）が、言語コピー内のコンテンツの言語を識別します。例えば、 */content/dam/it*&#x200B;はイタリア語の言語コピー用のイタリア語言語ルートです。 ソースアセットの翻訳の実行時に適切な言語がターゲットになるように、言語コピーは、[正しく設定された言語ルート](preparing-assets-for-translation.md#creating-a-language-root)を使用する必要があります。

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

1. 言語プライマリの言語ルートを作成します。例えば、サンプルフォルダー階層の英語言語コピーの言語ルートは `/content/dam/en` です。[言語ルートの作成](preparing-assets-for-translation.md#creating-a-language-root)の情報に従って言語ルートが正しく設定されていることを確認します。

1. 言語プライマリにアセットを追加します。
1. 言語コピーが必要な各ターゲット言語の言語ルートを作成します。

## 言語ルート{#creating-a-language-root}の作成

言語ルートを作成するには、フォルダーを作成し、「名前」プロパティの値として ISO 言語コードを使用します。言語ルートを作成したら、言語ルート内の任意のレベルに言語コピーを作成できます。

例えば、サンプル階層のイタリア語言語コピーのルートページの「名前」プロパティは `it` になります。「名前」プロパティは、リポジトリー内の asset ノードの名前として使用されます。そのため、このプロパティによってアセットのパスが指定されます(`https://[aem_server]:[port]/assets.html/content/dam/it/`)。

1. [!DNL Assets]コンソールで「**[!UICONTROL 作成]**」をクリックし、メニューから「**[!UICONTROL フォルダー]**」を選択します。

   ![フォルダーを作成](assets/Create-folder.png)

1. 「**[!UICONTROL 名前]**」フィールドに、国コードを`<language-code>`の形式で入力します。

   ![フォルダーへの言語コードの追加](assets/Add-language-code-in-folder.png)

1. 「**[!UICONTROL 作成]**」をクリックします。言語ルートは[!DNL Assets]コンソールに作成されます。

## 言語ルートの表示 {#viewing-language-roots}

[!DNL Experience Manager] インターフェイスに **** は、内で作成された言語ルートのリストを表示する参照パネルが用意されて [!DNL Assets]います。

1. [!DNL Assets]コンソールで、言語コピーを作成する言語プライマリを選択します。
1. 左側のレールから、「**[!UICONTROL 参照]**」オプションを選択して、[!UICONTROL 参照]ウィンドウを開きます。

   ![chlimage_1-122](assets/chlimage_1-122.png)

1. 参照パネルで、「**[!UICONTROL 言語コピー]**」をクリックします。 [!UICONTROL 言語コピー]パネルに、アセットの言語コピーが表示されます。

   ![言語コピー](assets/lang-copy2.png)
