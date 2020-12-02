---
title: デザインとデザイナー
seo-title: デザインとデザイナー
description: Web サイト用に、また AEM で、デザインの作成が必要になります。その場合はデザイナーを使用します
seo-description: Web サイト用に、また AEM で、デザインの作成が必要になります。その場合はデザイナーを使用します
uuid: b880ab49-8bea-4925-9b7b-e911ebda14ee
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: f9bcb6eb-1df4-4709-bcec-bef0931f797a
translation-type: tm+mt
source-git-commit: c13eabdf4938a47ddf64d55b00f845199591b835
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 51%

---


# デザインとデザイナー{#designs-and-the-designer}

>[!CAUTION]
>
>この記事では、クラシックUIを基にしてWebサイトを作成する方法を説明します。 アドビでは、[AEM Sites の開発の手引き](/help/sites-developing/getting-started.md)で詳しく説明しているように、Web サイトに最新の AEM テクノロジーを利用することをお勧めします。

Web サイト用に、また AEM で、デザインの作成が必要になります。その場合はデザイナーを使用します。

>[!NOTE]
>
>Web アクセシビリティについて詳しくは、[AEM と Web アクセシビリティのガイドライン](/help/managing/web-accessibility.md)を参照してください。

## デザイナーの使用  {#using-the-designer}

デザインは、「**ツール**」タブの&#x200B;**デザイン**&#x200B;セクションで定義できます。

![screen_shot_2012-02-01at30237pm](assets/screen_shot_2012-02-01at30237pm.png)

ここで、デザインの格納に必要な構造を作成し、必要なカスケーディングスタイルシート（CSS）および画像をアップロードできます。

デザインは`/etc/designs`の下に保存されます。 Webサイトに使用するデザインのパスは、`jcr:content`ノードの`cq:designPath`プロパティを使用して指定します。

![chlimage_1-74](assets/chlimage_1-74a.png)

>[!NOTE]
>
>デザインモードのページ上でおこなわれたすべての変更は、サイトのデザインノードの下に保持され、同じデザインを持つすべてのページに自動的に適用されます。

## 必要なもの  {#what-you-will-need}

デザインを実現するには、以下が必要です。

**CSS**  — カスケードスタイルシートは、ページ上の特定領域の形式を定義します。**画像**  — 背景やボタンなどの機能に使用する画像。

### Web サイトをデザインする際の考慮事項 {#considerations-when-designing-your-website}

Webサイトを開発する際は、`/etc/design/<project>`の下に画像とCSSファイルを保存して、次のスニペットに示すように、現在のデザインに基づいてリソースを参照できるようにすることをお勧めします。

```xml
<%= currentDesign.getPath() + "/static/img/icon.gif %>
```

前述の例では、いくつかのオファーの利点があります。

* 別々のデザインパスを使用しているサイトごとに、コンポーネントのルックアンドフィールを変化させることができます。
* Webサイトの再設計は、サイトのルートにある別のノードのデザインパスを`design/v1`から`design/v2.`に指定するだけで行えます

* `/etc/designs` とは、ツリ `/content` ーの下に何があるかを知りたがる外部ユーザを、ブラウザが保護しているのを目にする唯一の外部URL `/apps` です。上記のURLの利点は、アセットの公開をいくつかの異なる場所に制限するので、システム管理者がより高いセキュリティを設定するのに役立ちます。

