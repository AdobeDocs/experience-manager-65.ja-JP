---
title: パーソナライズとコンテンツのターゲティング
seo-title: Personalization and Content Targeting
description: パーソナライズされたコンテンツを AEM で作成する方法を説明します。
seo-description: Learn how AEM can create personalized content
uuid: 3a1aaa3d-5f57-4fb7-a4be-523f0d274b79
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: 850da0da-f7c3-4dd7-bb06-404c14a2a791
exl-id: be34760a-875b-419d-9fa4-2359b314a3b7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '519'
ht-degree: 100%

---

# パーソナライズとコンテンツのターゲティング {#personalization}

## パーソナライゼーションとコンテンツのターゲティング {#personalization-and-content-targeting}

AEM には、ターゲットとなるコンテンツをオーサリングして、パーソナライズされたエクスペリエンスを提供するためのツールのフレームワークが用意されています。

## ターゲティングモード {#targeting-mode}

[AEM のターゲットモードを使用してターゲットコンテンツをオーサリングします。](/help/sites-authoring/content-targeting-touch.md)ターゲットモードと Target コンポーネントは、マーケティングアクティビティのエクスペリエンス用コンテンツを作成するためのツールを提供します。

## アクティビティ {#activities}

アクティビティは、マーケティング戦略を定義し、整理するためのものです。アクティビティは、ターゲットとするオーディエンスと、そのターゲット設定の適用期間から構成されます。

たとえば、We.Retail の商品カタログには、季節商品に注目したティーザーが掲載されています。Summer Sports アクティビティは、このティーザーが夏季のターゲットとするマーケティングセグメントを定義します。

アクティビティは、ページが使用する[ターゲティングエンジン](/help/sites-authoring/personalization.md#targeting-engine)も識別します。

ブランドのアクティビティを作成および管理するには、[アクティビティコンソール](/help/sites-authoring/activitylib.md)を使用します。[ターゲットコンテンツをオーサリング](/help/sites-authoring/content-targeting-touch.md)する際に、アクティビティを作成することもできます。

## エクスペリエンス {#experiences}

アクティビティごとに、ターゲットとするオーディエンスを識別する 1 つ以上のエクスペリエンスを定義します。AEM では、各エクスペリエンスを構成するコンテンツを自由に制御できます。

オーディエンスは、AEM または Adobe Target で作成されたマーケティングセグメントをベースとします。訪問者が Web ページを開くと、そのページのロジックによってオーディエンスが判断され、そのオーディエンス向けに作成されたコンテンツが表示されます。

例えば、あるアクティビティが「30 歳以上の女性」と「30 歳未満の女性」という 2 つの異なるオーディエンス用のエクスペリエンスを定義するものとします。We.Retail の女性向けページでは、エクスペリエンスごとに異なる商品が表示されます。

1 つのアクティビティに複数のエクスペリエンスを定義できます。[アクティビティコンソール](/help/sites-authoring/activitylib.md#adding-editing-an-activity-using-the-activities-console)または[ターゲットモード](/help/sites-authoring/content-targeting-touch.md#adding-and-removing-experiences-using-targeting-mode)を使用して、アクティビティにエクスペリエンスを追加できます。

## オファー {#offers}

オファーは、それぞれのエクスペリエンスでページ上に表示されるコンテンツです。オーディエンス向けコンテンツの効果を最大限に高めるには、異なるエクスペリエンスに異なるオファーを使用します。

たとえば、We.Retail サンプル Web サイトの女性向けページでは、オファーをティーザー画像として使用して、ページ上部に表示することができます。30 歳以上の女性向けエクスペリエンスと、30 歳未満の女性向けエクスペリエンスには、それぞれ異なるオファーをティーザーとして使用します。

複数のエクスペリエンスで使用できるオファーを作成するには、[オファーコンソール](/help/sites-authoring/offerlib.md)を使用します。[ターゲットコンテンツをオーサリング](/help/sites-authoring/content-targeting-touch.md)するときは、単一エクスペリエンス用のオファーを作成するか、オファーライブラリからオファーを追加します。

## ターゲティングエンジン {#targeting-engine}

ターゲティングエンジンは、ターゲットコンテンツ用のロジックを動かすメカニズムです。使用可能なターゲティングエンジンには AEM と Adobe Target の 2 種類があり、どちらを使用するかは[アクティビティ](/help/sites-authoring/activitylib.md)で設定します。

### AEM {#aem}

AEM は、ページリクエストの処理や、表示コンテンツの判断を行う組み込みのターゲティングエンジンを備えています。AEM ターゲティングエンジンを使用する場合、エクスペリエンスのオーディエンス定義に使用できるセグメントは、AEM で作成されるセグメントのみとなります。

### Adobe Target {#adobe-target}

Adobe Target ターゲティングエンジンを使用すると、ページの訪問から収集された情報が Adobe Target で追跡されます。

* このターゲティングエンジンを使用する場合、エクスペリエンスのオーディエンス定義には Adobe Target から読み込んだセグメントを使用します。
* Adobe Target エンジンを使用するアクティビティは、[Target と同期](/help/sites-authoring/activitylib.md#synchronizing-activities-with-adobe-target)します。

このエンジンを使用できるのは、[Adobe Target と統合](/help/sites-administering/opt-in.md)している場合のみです。
