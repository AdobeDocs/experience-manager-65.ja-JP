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
exl-id: c81c5910-b6c9-41bd-8840-a6782792701f
source-git-commit: adbdff9ff5b5bd8f5f6b22fb724a0e5273072de2
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 46%

---

# デザインとデザイナー{#designs-and-the-designer}

>[!CAUTION]
>
>この記事では、クラシックUIに基づくWebサイトの作成方法について説明します。 アドビでは、[AEM Sites の開発の手引き](/help/sites-developing/getting-started.md)で詳しく説明しているように、Web サイトに最新の AEM テクノロジーを利用することをお勧めします。

デザイナーは、AEMの[クラシックUI](/help/release-notes/touch-ui-features-status.md)を使用して、Webサイト用のデザインを作成する際に使用します。

>[!NOTE]
>
>Web アクセシビリティについて詳しくは、[AEM と Web アクセシビリティのガイドライン](/help/managing/web-accessibility.md)を参照してください。

## デザイナーの使用  {#using-the-designer}

デザインは、「**ツール**」タブの&#x200B;**designs**&#x200B;セクションで定義できます。

![screen_shot_2012-02-01at30237pm](assets/screen_shot_2012-02-01at30237pm.png)

ここで、デザインの格納に必要な構造を作成し、必要なカスケーディングスタイルシート（CSS）および画像をアップロードできます。

デザインは`/apps/<your-project>`の下に格納されます。 Webサイトに使用するデザインへのパスは、`jcr:content`ノードの`cq:designPath`プロパティを使用して指定します。

![chlimage_1-74](assets/chlimage_1-74a.png)

>[!NOTE]
>
>デザインモードのページ上でおこなわれたすべての変更は、サイトのデザインノードの下に保持され、同じデザインを持つすべてのページに自動的に適用されます。

## 必要なもの  {#what-you-will-need}

デザインを実現するには、以下が必要です。

**CSS**  — カスケーディングスタイルシートは、ページ上の特定の領域の形式を定義します。**画像**  — 背景、ボタンなどの機能に使用する画像。

### Web サイトをデザインする際の考慮事項 {#considerations-when-designing-your-website}

Webサイトを開発する際は、`/apps/<your-project>`の下に画像とCSSファイルを保存し、次のスニペットで説明するように、現在のデザインに基づいてリソースを参照できるようにすることを強くお勧めします。

```xml
<%= currentDesign.getPath() + "/static/img/icon.gif %>
```

前述の例には、次のような利点があります。

* 別々のデザインパスを使用しているサイトごとに、コンポーネントのルックアンドフィールを変化させることができます。
* Webサイトの再設計は、デザインパスを`design/v1`から`design/v2.`までの間、サイトのルートにある別のノードに向けることで簡単におこなえます

* `/etc/designs` と `/content` は、ブラウザーが外部ユーザーの保護を確認する唯一の外部URLで、ツリーの下に何があるかを確認 `/apps` します。上記のURLの利点は、アセットの公開をいくつかの異なる場所に制限するので、システム管理者がより高いセキュリティを設定するのに役立ちます。
