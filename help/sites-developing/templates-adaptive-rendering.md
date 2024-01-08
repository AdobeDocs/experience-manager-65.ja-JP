---
title: アダプティブテンプレートレンダリング
description: Adobe Experience Managerでのアダプティブテンプレートのレンダリングについて説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: 58cac3b1-b7cd-44b2-b89b-f5ee8811c198
source-git-commit: b703f356f9475eeeafb1d5408c650d9c6971a804
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 12%

---

# アダプティブテンプレートレンダリング{#adaptive-template-rendering}

アダプティブテンプレートのレンダリングを使用すると、バリエーションを含むページを管理できます。 元々は、モバイルデバイス用の様々なHTML出力（機能電話とスマートフォンなど）の配信に役立ちました。この機能は、異なるマークアップやHTML出力が必要な様々なデバイスにエクスペリエンスを配信する必要がある場合に役立ちます。

## 概要 {#overview}

テンプレートはレスポンシブグリッドに基づいて構築され、これらのテンプレートに基づいて作成されたページは完全にレスポンシブで、クライアントデバイスのビューポートに自動的に調整されます。 作成者は、ページエディターのエミュレーターツールバーを使用して、レイアウトを特定のデバイスに設定できます。

また、アダプティブレンダリングをサポートするようにテンプレートを設定することもできます。 デバイスグループが適切に設定されている場合、エミュレーターモードでデバイスを選択する際に、URL 内で別のセレクターを使用してページがレンダリングされます。 セレクターを使用すると、特定のページレンダリングを URL 経由で直接呼び出すことができます。

デバイスグループを設定する際には注意が必要です。

* 各デバイスは、少なくとも 1 つのデバイスグループに属している必要があります。
* 1 つのデバイスが複数のデバイスグループに属する場合があります。
* デバイスは複数のデバイスグループに属することができるので、セレクターを組み合わせることができます。
* セレクターの組み合わせは、リポジトリ内に保持されるので、上から下へと評価されます。

>[!NOTE]
>
>デバイスグループ**レスポンシブデバイスにセレクターがないのは、レスポンシブデザインをサポートしていると認識されるデバイスは、アダプティブレイアウトを必要としないと見なされるからです

## 設定 {#configuration}

アダプティブレンダリングセレクターは、既存のデバイスグループに対して、または [自分で作成したグループ。](/help/sites-developing/mobile.md#device-groups)

この例では、既存のデバイスグループを設定します **スマートフォン** アダプティブレンダリングセレクターを **エクスペリエンスページ** We.Retail 内のテンプレート。

1. `http://localhost:4502/miscadmin#/etc/mobile/groups` で、アダプティブセレクターを必要とするデバイスグループを編集します。

   「**エミュレーターを無効にする**」オプションを設定して保存します。

   ![chlimage_1-157](assets/chlimage_1-157.png)

1. セレクターは、 **BlackBerry®** および **iPhone 4** デバイスグループが指定された **スマートフォン** 次の手順で、をテンプレートとページ構造に追加します。

   ![chlimage_1-158](assets/chlimage_1-158.png)

1. CRXDE Liteを使用して、複数値の文字列プロパティにデバイスグループを追加することで、テンプレートでデバイスグループを使用できるようにします `cq:deviceGroups` を使用して、テンプレートの構造を確認します。

   `/conf/<your-site>/settings/wcm/templates/<your-template>/structure/jcr:content`

   例えば、スマートフォンのデバイスグループを追加する場合は、次のようになります。

   `/conf/we-retail/settings/wcm/templates/experience-page/structure/jcr:content`

   ![chlimage_1-159](assets/chlimage_1-159.png)

1. CRXDE Liteを使用して、複数値の文字列プロパティにデバイスグループを追加することで、サイトでデバイスグループを使用できるようにします。 `cq:deviceGroups` を使用して、サイトの構造を確認します。

   `/content/<your-site>/jcr:content`

   例えば、 **スマートフォン** デバイスグループ：

   `/content/we-retail/jcr:content`

   ![chlimage_1-160](assets/chlimage_1-160.png)

現在は、 [エミュレーター](/help/sites-authoring/responsive-layout.md#layout-definitions-device-emulation-and-breakpoints) ページエディター内 ( 例えば、 [レイアウトの変更](/help/sites-authoring/responsive-layout.md)) をクリックして設定済みのデバイスグループのデバイスを選択すると、ページは URL の一部にセレクターを含めてレンダリングされます。

この例では、 **エクスペリエンスページ** テンプレートを作成し、エミュレーターで「 iPhone 4 」を選択すると、ページはセレクターを「 」として含めてレンダリングされます。 `arctic-surfing-in-lofoten.smart.html` の代わりに `arctic-surfing-in-lofoten.html`

このセレクターを使用してページを直接呼び出すこともできます。

![chlimage_1-161](assets/chlimage_1-161.png)
