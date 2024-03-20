---
title: We.Retail のコンテンツフラグメントの使用
description: We.Retail による Adobe Experience Manager のコンテンツフラグメントの使用方法について説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 1e5d8184-7164-4984-b43e-421015e8bf52
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 100%

---

# We.Retail のコンテンツフラグメントの使用{#trying-out-content-fragments-in-we-retail}

コンテンツフラグメントを使用すると、チャネルに特化しないコンテンツをチャネル固有のバリエーションと共に作成できます。（Adobe Experience Manager の標準のインスタンスで使用できる）**We.Retail** には、基本のサンプルとして **Arctic Surfing in Lofoten** フラグメントが用意されています。このフラグメントは、次のことを示しています。

* Adobe Experience Manager（AEM）のコンテンツフラグメントは、[ページに依存しないアセット](/help/assets/content-fragments/content-fragments.md)として作成および管理されます。これにより、チャネルに依存しないコンテンツを様々なバリエーション（チャネル固有）で作成できます。

   * [We.Retail でのコンテンツフラグメントアセットの場所](#where-to-find-content-fragments-in-we-retail)を参照してください。

* その後、コンテンツページを[オーサリングする際に、これらのフラグメントとそれらのバリエーションを使用](/help/sites-authoring/content-fragments.md)できます。

   * [We.Retail でコンテンツフラグメントが使用される場所](#where-content-fragments-are-used-in-we-retail)を参照してください。

コンテンツフラグメントの作成、管理、使用および開発に関する完全なドキュメントについて：

* [その他の情報](#further-information)を参照してください。

>[!NOTE]
>
>**コンテンツフラグメント**&#x200B;と&#x200B;**[エクスペリエンスフラグメント](/help/sites-authoring/experience-fragments.md)**&#x200B;は、AEM 内の異なる機能です。
>
>* **コンテンツフラグメント**&#x200B;はエディトリアルコンテンツで、主にテキストや関連する画像です。これらは、デザインやレイアウトを含まない純粋なコンテンツです。
>* **エクスペリエンスフラグメント**&#x200B;は完全にレイアウトされたコンテンツであり、web ページのフラグメントです。
>
>エクスペリエンスフラグメントには、コンテンツフラグメントの形式でコンテンツを含めることができますが、その逆はできません。

## We.Retail でのコンテンツフラグメントの場所 {#where-to-find-content-fragments-in-we-retail}

We.Retail には、様々なコンテンツフラグメントのサンプルがあり、**Assets**／**ファイル**／**We.Retail**／**英語**／**エクスペリエンス**&#x200B;からアクセスできます。

これには、関連するビジュアルアセットと組み合わせられたフラグメントである **Arctic Surfing in Lofoten** などがあります。

* **Assets**／**ファイル**／**We.Retail**／**英語**／**エクスペリエンス**／**Arctic Surfing in Lofoten** の順に移動します。

   * [http://localhost:4502/assets.html/content/dam/we-retail/jp/experiences/arctic-surfing-in-lofoten](http://localhost:4502/assets.html/content/dam/we-retail/jp/experiences/arctic-surfing-in-lofoten)

![cf-44](assets/cf-44.png)

**Arctic Surfing in Lofoten** フラグメントを選択し、編集することができます。

* [http://localhost:4502/editor.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten/arctic-surfing-in-lofoten](http://localhost:4502/editor.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten/arctic-surfing-in-lofoten)

ここで、タブ（左側パネル）を使って、フラグメントの[編集と管理](/help/assets/content-fragments/content-fragments.md)を実行できます。

<!--![cf-45-aa](do-not-localize/cf-45-aa.png) ![cf-45-a](do-not-localize/cf-45-a.png) ASSET does not exist-->

* **[マークダウン](/help/assets/content-fragments/content-fragments-variations.md)**&#x200B;を含む[バリエーション](/help/assets/content-fragments/content-fragments-markdown.md)
* **[関連コンテンツ](/help/assets/content-fragments/content-fragments-assoc-content.md)**
* **[メタデータ](/help/assets/content-fragments/content-fragments-metadata.md)**

![cf-46](assets/cf-46.png)

## We.Retail でコンテンツフラグメントが使用される場所 {#where-content-fragments-are-used-in-we-retail}

[コンテンツフラグメントを使用したページオーサリング](/help/sites-authoring/content-fragments.md)を説明するために、次のような様々なサンプルページが用意されています。

* [http://localhost:4502/sites.html/content/we-retail/language-masters/en/experience](http://localhost:4502/sites.html/content/we-retail/language-masters/en/experience)

例えば、**Arctic Surfing in Lofoten** のコンテンツフラグメントは、次の手順に沿って Sites ページで参照できます。

* **Sites**／**We.Retail**／**言語マスター**／**英語**／**エクスペリエンス**&#x200B;の順に移動します。その後、**Arctic Surfing in Lofoten** を開いて編集をおこないます。

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
