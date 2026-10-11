---
title: Adobe Campaign のターゲット設定
description: セグメント化を設定した後で、Adobe Campaign のターゲット設定エクスペリエンスを作成できます。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
exl-id: fc6fccba-41c5-4c13-aac0-b4ef67767abe
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization,Integration
role: User,Admin,Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: e2c1b6d3-bb7e-4fe8-8c72-f7b403298e91
    internal-label: Authoring
  - id: eb3ad9f8-54a2-45f3-abb1-d3976415a718
    internal-label: Personalization
  - id: 243139ec-8e41-5296-a287-31343ab1bc0f
    internal-label: Integration
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 100%
---
# Adobe Campaign のターゲティング{#targeting-your-adobe-campaign}

Adobe Campaign のニュースレターのターゲット設定を行うには、まずセグメント化を設定する必要があります（セグメント化の設定は、クラシック UI でのみ使用可能です）（ClientContext）。 その後、Adobe Campaign 用のターゲット設定されたエクスペリエンスを作成できます。 ここでは、この両方について説明します。

## AEM でのセグメント化の設定 {#setting-up-segmentation-in-aem}

セグメント化を設定するには、クラシック UI を使用してセグメントを設定する必要があります。 残りの手順は、標準 UI で実行できます。

セグメント化の設定には、セグメント、ブランド、キャンペーンおよびエクスペリエンスの作成が含まれます。

>[!NOTE]
>
>セグメント ID は、Adobe Campaign 側のセグメント ID にマップする必要があります。

### セグメントの作成 {#creating-segments}

セグメントは次の手順で作成します。

1. **&lt;host>:&lt;port>/miscadmin#/etc/segmentation** で[セグメント化コンソール](http://localhost:4502/miscadmin#/etc/segmentation)を開きます。
1. ページを作成してタイトル（「**AC Segments**」など）を入力し、**セグメント（Adobe Campaign）**&#x200B;テンプレートを選択します。
1. 左側のツリー表示で、作成したページを選択します。
1. セグメントを作成し（例えば、男性ユーザーをターゲットにするセグメントを作成するには、作成した「Male」というセグメントの下にページを作成します）、**セグメント（Adobe Campaign）**&#x200B;テンプレートを選択します。
1. 作成したセグメントページを開き、サイドキックからそのページに&#x200B;**セグメント ID** をドラッグ＆ドロップします。
1. 特性をダブルクリックし、このセグメント（この例では、Adobe Campaign で定義されている男性セグメント）を表す ID（「**MALE**」など）を入力して、「**OK**」をクリックします。 次のメッセージ「*`targetData.segmentCode == "MALE"`*」が表示されます。
1. 同じステップを繰り返して、別のセグメント（例えば女性ユーザーをターゲティングしたセグメント）を作成します。

### ブランドの作成 {#creating-a-brand}

レポートは次の手順で作成します。

1. 「**Sites**」で **Campaigns** フォルダー（We.Retail 内など）に移動します。
1. 「**ページを作成**」をクリックし、ページのタイトル（「We.Retail Brand」など）を入力して、**ブランド**&#x200B;テンプレートを選択します。

### キャンペーンの作成 {#creating-a-campaign}

キャンペーンは次の手順で作成します。

1. 作成した&#x200B;**ブランド**&#x200B;ページを開きます。
1. 「**ページを作成**」をクリックし、ページのタイトル（「We.Retail Campaign」など）を入力し、**キャンペーン**&#x200B;テンプレートを選択して、「**作成**」をクリックします。

### エクスペリエンスの作成 {#creating-experiences}

セグメントのエクスペリエンスは次の手順で作成します。

1. 作成した&#x200B;**キャンペーン**&#x200B;ページを開きます。
1. 「**ページを作成**」をクリックし、ページのタイトル（この例では男性セグメント用のエクスペリエンスを作成するので「Male」など）を入力してセグメント用のエクスペリエンスを作成し、**エクスペリエンス**&#x200B;テンプレートを選択します。
1. 作成したエクスペリエンスページを開きます。
1. 「**編集**」をクリックして、「セグメント」の下の「**項目を追加**」をクリックします。
1. 男性セグメントへのパス（**/etc/segmentation/ac-segments/male** など）を入力し、「**OK**」をクリックします。 次のメッセージ「*エクスペリエンスは次を対象としています：男性*」が表示されます。
1. ここまでのステップを繰り返して、すべてのセグメント（女性をターゲットにするセグメントなど）用のエクスペリエンスを作成します。
