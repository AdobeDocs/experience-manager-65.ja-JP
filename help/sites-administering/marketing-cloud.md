---
title: Adobe Experience Cloudとの統合
description: Adobe Experience ManagerとAdobe Experience Cloudを統合する方法を説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: ba518290-dd82-44dc-ae7c-c8152df89179
source-git-commit: a51a863a4edf7e8b951a8361c5c7f0517b09f12a
workflow-type: tm+mt
source-wordcount: '846'
ht-degree: 48%

---

# Adobe Experience Cloudとの統合{#integrating-with-the-adobe-marketing-cloud}

この [Adobe Experience Cloud](https://business.adobe.com/products/marketing-cloud/main.html)には、オンラインイニシアチブを成功に導くための実用的なリアルタイムのデータとインサイトを提供する、強力な web 分析および web サイト最適化製品が含まれます。 オンラインビジネスの最適化のための統合されたオープンなプラットフォームを提供します。 Cloud は、顧客インサイトの力を収集し、解放して、顧客の獲得、コンバージョン、保持の取り組みと、コンテンツの作成と配信を最適化する統合アプリケーションで構成されます。

Adobe Experience Manager(AEM) を使用すれば、Adobe Experience Cloudの次の製品とシームレスに統合できます。

* Adobe Analytics：マーケティング担当者は、オンライン戦略やマーケティング戦略に関して、すぐに利用可能なリアルタイムの情報を入手できます。
* Adobe Target：顧客へのオンラインコンテンツの関連性を継続的に高め、より多くのコンバージョンを生み出すための機能をマーケティング担当者に提供します。
* Adobe Dynamic Media Classic は、メディア管理の自動化、web パブリッシングの効率化、および web エクスペリエンスの強化をホストされた環境内で行います。
* Adobe Dynamic Tag Management：アドビやサードパーティのタグをいくつでもすばやく簡単に管理できる直感的なツールをマーケティング担当者に提供します。
<!-- Search&Promote is end of life as of September 1, 2022 * Adobe Search&Promote gives marketers the ability to control and optimize the search results on their sites. -->
* Adobe Campaign：メール配信コンテンツを Adobe Experience Manager で直接管理できます。

さらに、AEM を [Creative Cloud と統合](/help/assets/aem-cc-integration-best-practices.md)したり、[サードパーティのサービス](/help/sites-administering/third-party-services.md)と統合したりすることもできます。

## Adobe Analytics との統合 {#integrating-with-adobe-analytics}

[Adobe Analytics](https://business.adobe.com/products/analytics/adobe-analytics.html) は、様々なマーケティングチャネルにまたがるオンライン戦略全体からの統合データを 1 箇所で測定、分析、最適化できる場をディジタルマーケターに提供する、業界最先端のソリューションです。マーケティング担当者は、デジタル戦略やマーケティング施策に関して、すぐに利用可能なリアルタイムの web 分析情報を入手できます。Adobe Analyticsは、Web サイトで最も収益性の高いパスをすばやく特定し、トラフィックをセグメント化して価値の高い Web 訪問者を特定し、訪問者がサイトから出て行く場所を特定し、オンラインマーケティングキャンペーンの重要な成功指標を特定します。

Adobe Analytics を使用すると、サイトのデータを分析できます。

Adobe Analytics との統合によって、次の操作ができるようになります。

* Analytics のユーザートラッキングを有効にする。
* 実行モード（オーサー、パブリッシュなど）をそれぞれ異なるレポートスイートにマッピングする。
* ClientContext 変数をコンバージョン変数またはトラフィックプロパティとして送信します。
* 事前定義済みの変数マッピングを使用します。
* 完全なサイトセクションを一度に設定できます。
* カスタム定義イベントを追跡する。

AEMと Analytics の統合について詳しくは、 [Adobe Analyticsとの統合](/help/sites-administering/adobeanalytics.md).

[オプトインウィザード](/help/sites-administering/opt-in.md)を使用して簡単に統合を行うこともできます。

## Adobe Target との統合 {#integrating-with-adobe-target}

[Adobe Target](https://business.adobe.com/products/target/adobe-target.html) を使用すると、マーケティング担当者は、オンラインテストをデザインして実行し、行動に基づいたオーディエンスセグメントをその場で作成し、コンテンツとオンラインのエクスペリエンスを自動的にターゲット設定できるようになります。

現在、オンライン消費者は常にニーズを進化させ、幅広いサイトやコンテンツソースから選択できる、関連性の高いパーソナライズされたコンテンツも期待しています。 オンラインオーディエンスを惹きつけるには、どのオファーやコンテンツがオーディエンスに関連し、魅力的かをオンラインマーケターがすばやく特定することが重要です。 この知識に基づいて、マーケターは、サイトを継続的に発展させ、適切なコンテンツを様々なオーディエンスにターゲット設定する機能が必要になります。

[Adobe Targetとの統合](/help/sites-administering/target.md) では、サイトを Target と統合する方法について説明します。

[オプトインウィザード](/help/sites-administering/opt-in.md)を使用して簡単に統合を行うこともできます。

## Analytics と Target のオプトイン {#opting-in-to-analytics-and-target}

AEMは、Adobe AnalyticsおよびAdobe Targetと統合するための簡単なオプトイン手順を提供します。 管理者としてログインし、プロジェクトコンソールにアクセスすると、オプトインウィザードが表示されます。

![chlimage_1-107](assets/chlimage_1-107a.png)

Analytics や Target との統合をオプトインして、ページトラッキング機能、分析機能、パーソナライゼーション機能を使用できるようにします。 オプトインしたら、ユーザーアカウント情報を入力し、追跡するページを指定します。

詳しくは、 [Adobe AnalyticsとAdobe Targetのオプトイン。](/help/sites-administering/opt-in.md)

## Adobe Dynamic Media Classic との統合 {#integrating-with-scene}

Adobe Dynamic Media Classicは、Web、モバイル、電子メール、ソーシャルメディア、インターネットに接続されたディスプレイ、印刷物に対する動的マーケティングアセットや豊富な視覚的マーチャンダイジングの公開、管理、強化、配信を行うホストソリューションです。

Adobe Experience Manager では、デジタルアセットを Adobe Experience Manager から Dynamic Media Classic に直接公開でき、Dynamic Media Classic から Adobe Experience Manager にも公開できます。

また、Dynamic Media Classic に公開された Adobe Experience Manager アセットを、ベーシックズームやビデオなどの様々なビューアで表示できます。

Adobe Experience Manager と Dynamic Media Classic の統合方法について詳しくは、[Dynamic Media Classic との統合](/help/sites-administering/scene7.md)に関するドキュメントを参照してください。

## Adobe Dynamic Tag Management との統合 {#integrating-with-adobe-dynamic-tag-management}

[Adobe Dynamic Tag Management](https://business.adobe.com/products/experience-platform/adobe-experience-platform.html) は直感的なツールであり、このツールを使用することでマーケティング担当者は、アドビやサードパーティのタグを数に制限なく、すばやく簡単に管理できます。ほぼすべてのオンライン環境をより制御し、柔軟に最適化できるため、IT リソースへの依存を軽減できます。

[Adobe Dynamic Tag Management](/help/sites-administering/dtm.md) と AEM を統合すると、Dynamic Tag Management の web プロパティを使用して AEM サイトを追跡できます。

## Adobe Audience Manager との統合 {#integrating-with-adobe-audience-manager}

Audience Managerの統合は、AEM 6.3 で削除されました。

<!-- Search&Promote is end of life as of September 1, 2022 ## Integrating with Search&Promote {#integrating-with-search-promote} -->

<!-- Search&Promote is end of life as of September 1, 2022 Adobe Search&Promote enables marketers to optimizehow visitors browse, find, compare, and select relevant products and content on web and mobile sites. Businesses can easily promote priority items based on business objectives and visitor intent, as well as automate merchandising and promotions activity via KPI-based triggers or metrics. -->

<!-- Search&Promote is end of life as of September 1, 2022 Adobe Search&Promote is a reliable and scalable hosted site search application, capable of scaling to millions of pages or products, for heavily visited online businesses ranging from retail to news sites. It offers unprecedented levels of marketer control and metrics-based relevance. -->

<!-- Search&Promote is end of life as of September 1, 2022 For information about integrating AEM and Search&Promote, see [Integrating with Adobe Search&Promote](/help/sites-administering/search-and-promote.md). -->

## Adobe Campaign との統合 {#integrating-with-adobe-campaign}

[Adobe Campaign](https://business.adobe.com/products/campaign/adobe-campaign.html) では、メール配信コンテンツを Adobe Experience Manager で直接管理できます。

AEM と Adobe Campaign との統合方法について詳しくは、[Adobe Campaign との統合](/help/sites-administering/campaignstandard.md)を参照してください。