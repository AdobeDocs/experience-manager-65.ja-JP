---
title: We.Retail のコンテンツフラグメントの使用
seo-title: We.Retail のコンテンツフラグメントの使用
description: We.Retail のコンテンツフラグメントの使用
seo-description: 'null'
uuid: 66daddfe-8e98-47b6-8499-db055887ac17
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: d1326737-f378-46d0-9916-61ead4d31639
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 79%

---


# We.Retail のコンテンツフラグメントの使用{#trying-out-content-fragments-in-we-retail}

コンテンツフラグメントを使用すると、チャネルに特化しないコンテンツをチャネル固有のバリエーションと共に作成できます。**We.Retail** (AEMの標準搭載インスタンスで利用可能)は、 **Lofotenasの** Arctic Surfingフラグメントを基本的なサンプルとして提供しています。このフラグメントは、次のことを示しています。

* Adobe Experience Manager（AEM）のコンテンツフラグメントは、[ページに依存しないアセット](/help/assets/content-fragments/content-fragments.md)として作成および管理されます。コンテンツフラグメントを使用すると、チャネルに特化しないコンテンツをチャネル固有のバリエーションと共に作成できます。

   * [Web.Retailのコンテンツフラグメントアセットを検索する場所](#where-to-find-content-fragments-in-we-retail)を参照してください。

* その後、コンテンツページを[オーサリングする際に、これらのフラグメントとそれらのバリエーションを使用](/help/sites-authoring/content-fragments.md)できます。

   * [Web.Retailでコンテンツフラグメントが使用される場所](#where-content-fragments-are-used-in-we-retail)を参照してください。

コンテンツフラグメントの作成、管理、使用および開発に関する完全なドキュメントについて：

* [詳細情報](#further-information)を参照

>[!NOTE]
>
>**コンテンツフラグメント**&#x200B;と&#x200B;**[エクスペリエンスフラグメント](/help/sites-authoring/experience-fragments.md)**&#x200B;は、AEM 内の異なる機能です。
>
>* **コンテンツフラグメント**&#x200B;は、主にテキストや関連画像などの編集コンテンツです。これは、デザインやレイアウトを含まない純粋なコンテンツです。
>* **エクスペリエンスフラグメント**&#x200B;は完全にレイアウトされたコンテンツであり、Web ページのフラグメントです。

>
>
エクスペリエンスフラグメントには、コンテンツフラグメントの形式でコンテンツを含めることができますが、その逆はできません。

## We.Retail でのコンテンツフラグメントの場所 {#where-to-find-content-fragments-in-we-retail}

Web.Retailにはいくつかのサンプルコンテンツフラグメントがあります。**アセット**、**ファイル**、**We.Retail**、**英語**、**エクスペリエンス**&#x200B;を経由して移動します。

これには、関連するビジュアルアセットと組み合わせられたフラグメントである **Arctic Surfing in Lofoten** などがあります。

* **アセット**、**ファイル**、**We.Retail**、**英語**、**エクスペリエンス**、**Ratic Surfing in Lofoten**&#x200B;を通じて移動します。

   * [http://localhost:4502/assets.html/content/dam/we-retail/jp/experiences/arctic-surfing-in-lofoten](http://localhost:4502/assets.html/content/dam/we-retail/jp/experiences/arctic-surfing-in-lofoten)

![cf-44](assets/cf-44.png)

**Arctic Surfing in Lofoten** フラグメントを選択し、編集することができます。

* [http://localhost:4502/editor.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten/arctic-surfing-in-lofoten](http://localhost:4502/editor.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten/arctic-surfing-in-lofoten)

ここでは、タブ（左側のパネル）を使用してフラグメントを[編集および管理](/help/assets/content-fragments/content-fragments.md)できます。

<!--![](do-not-localize/cf-45-aa.png) ![](do-not-localize/cf-45-a.png) ASSET does not exist-->

* **[マークダウン](/help/assets/content-fragments/content-fragments-variations.md)**&#x200B;を含む[バリエーション](/help/assets/content-fragments/content-fragments-markdown.md)
* **[関連コンテンツ](/help/assets/content-fragments/content-fragments-assoc-content.md)**
* **[メタデータ](/help/assets/content-fragments/content-fragments-metadata.md)**

![cf-46](assets/cf-46.png)

## We.Retail でコンテンツフラグメントが使用される場所 {#where-content-fragments-are-used-in-we-retail}

[コンテンツフラグメントを使用したページオーサリング](/help/sites-authoring/content-fragments.md)の例を示すために、次のような様々なサンプルページが用意されています。

* [http://localhost:4502/sites.html/content/we-retail/language-masters/en/experience](http://localhost:4502/sites.html/content/we-retail/language-masters/en/experience)

例えば、**Arctic Surfing in Lofoten**&#x200B;コンテンツフラグメントは、サイトページで参照されます。

* **サイト**、**We.Retail**、**言語マスター**、**英語**、**エクスペリエンス**&#x200B;を通じて移動します。 その後、**Arctic Surfing in Lofoten** を開いて編集をおこないます。

   * [http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html](http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html)

![cf-53](assets/cf-53.png)

## その他の情報 {#further-information}

詳しくは、以下を参照してください。

* [コンテンツフラグメントの操作](/help/assets/content-fragments/content-fragments.md)

   * コンテンツフラグメントアセットを作成、編集および管理する方法について説明します。

* [コンテンツフラグメントを使用したページのオーサリング](/help/sites-authoring/content-fragments.md)

   * ページのオーサリング時にコンテンツフラグメントを使用します。

* [AEM の開発 - コンテンツフラグメント用コンポーネント](/help/sites-developing/components-content-fragments.md)

   * コンテンツフラグメント用コンポーネントの概要です。

* [コンテンツフラグメントの開発と拡張](/help/sites-developing/customizing-content-fragments.md)

   * コンテンツフラグメントの開発と拡張に役立つ情報です。

