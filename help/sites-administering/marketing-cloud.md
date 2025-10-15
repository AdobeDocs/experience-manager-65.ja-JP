---
title: Adobe Experience Cloud との統合
description: Adobe Experience Manager と Adobe Experience Cloud を統合する方法について説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: ba518290-dd82-44dc-ae7c-c8152df89179
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 100%

---

# Adobe Experience Cloud との統合{#integrating-with-the-adobe-marketing-cloud}

[Adobe Experience Cloud](https://business.adobe.com/jp/products/marketing-cloud/main.html?lang=ja) には、実用的なリアルタイムのデータやインサイトを提供してオンラインイニシアチブを成功に導く、強力な web 分析と web サイト最適化製品が含まれています。また、オンラインビジネスを最適化するための統合されたオープンプラットフォームを提供します。Adobe Experience Cloud は、顧客のインサイトを収集してその力を解き放ち、顧客獲得、コンバージョン、保持の取り組み、コンテンツの作成および配信を最適化する統合アプリケーションで構成されています。

Adobe Experience Manager（AEM）を使用すると、Adobe Experience Cloud の次の製品とシームレスに統合できます。

* Adobe Analytics：マーケターは、オンライン戦略やマーケティング戦略に関して、すぐに利用可能なリアルタイムの情報を入手できます。
* Adobe Target：顧客へのオンラインコンテンツの関連性を継続的に高め、より多くのコンバージョンを生み出すための機能をマーケターに提供します。
* Adobe Dynamic Media Classic は、メディア管理の自動化、web パブリッシングの効率化、および web エクスペリエンスの強化をホストされた環境内で行います。
* Adobe Dynamic Tag Management：アドビやサードパーティのタグをいくつでもすばやく簡単に管理できる直感的なツールをマーケターに提供します。
<!-- Search&Promote is end of life as of September 1, 2022 * Adobe Search&Promote gives marketers the ability to control and optimize the search results on their sites. -->
* Adobe Campaign：メール配信コンテンツを Adobe Experience Manager で直接管理できます。

さらに、AEM を [Creative Cloud と統合](/help/assets/aem-cc-integration-best-practices.md)したり、[サードパーティのサービス](/help/sites-administering/third-party-services.md)と統合したりすることもできます。

## Adobe Analytics との統合 {#integrating-with-adobe-analytics}

[Adobe Analytics](https://business.adobe.com/jp/products/analytics/adobe-analytics.html?lang=ja) は、様々なマーケティングチャネルにまたがるオンライン戦略全体からの統合データを 1 箇所で測定、分析、最適化できる場をディジタルマーケターに提供する、業界最先端のソリューションです。マーケターは、デジタル戦略やマーケティング施策に関して、すぐに利用可能なリアルタイムの web 分析情報を入手できます。Adobe Analytics を使用すると、マーケティング担当者は web サイト内で最も収益性の高いパスを迅速に特定し、トラフィックをセグメント化して高価値な web 訪問者を見つけ出し、訪問者がサイトから離れた場所を確認し、オンラインマーケティングキャンペーンの重要な成功指標を明らかにすることができます。

Adobe Analytics を使用すると、サイトのデータを分析できます。

Adobe Analytics との統合によって、次の操作ができるようになります。

* Analytics のユーザートラッキングを有効にする。
* 実行モード（オーサー、パブリッシュなど）をそれぞれ異なるレポートスイートにマッピングする。
* クライアントコンテキスト変数をコンバージョン変数またはトラフィックプロパティとして送信する。
* 定義済みの変数マッピングを使用する。
* 完全なサイトセクションを一度に設定する。
* カスタム定義イベントを追跡する。

AEMと Analytics の統合について詳しくは、[Adobe Analytics との統合](/help/sites-administering/adobeanalytics.md)を参照してください。

[オプトインウィザード](/help/sites-administering/opt-in.md)を使用して簡単に統合を行うこともできます。

## Adobe Target との統合 {#integrating-with-adobe-target}

[Adobe Target](https://business.adobe.com/jp/products/target/adobe-target.html?lang=ja) を使用すると、マーケターは、オンラインテストをデザインして実行し、行動に基づいたオーディエンスセグメントをその場で作成し、コンテンツとオンラインのエクスペリエンスを自動的にターゲット設定できるようになります。

現在、オンライン消費者のニーズは常に変化しており、消費者は利用できる様々なサイトやコンテンツソースの中から、関連性が高く、パーソナライズされたコンテンツを選択したいと考えています。オンラインオーディエンスを引き付けるには、オンラインマーケターが、オーディエンスにとって関連性が高く魅力的なオファーやコンテンツをすばやく特定することが重要です。この知識に基づいて、マーケターはサイトを継続的に発展させ、様々なオーディエンスに適切なコンテンツをターゲット設定する必要があります。

[Adobe Target との統合](/help/sites-administering/target.md)では、サイトと Adobe Target を統合する方法について説明します。

[オプトインウィザード](/help/sites-administering/opt-in.md)を使用して簡単に統合を行うこともできます。

## Analytics と Target のオプトイン {#opting-in-to-analytics-and-target}

AEM には、Adobe Analytics や Adobe Target と統合するための簡単なオプトイン手順が用意されています。管理者としてログインし、プロジェクトコンソールにアクセスすると、オプトインウィザードが表示されます。

![chlimage_1-107](assets/chlimage_1-107a.png)

Analytics や Target との統合をオプトインすると、ページトラッキング機能、分析機能、パーソナライズ機能を使用できるようになります。オプトインするときには、ユーザーアカウント情報を入力し、追跡するページを指定します。

詳細情報は、[Adobe Analytics と Adobe Target のオプトイン](/help/sites-administering/opt-in.md)を参照してください。

## Adobe Dynamic Media Classic との統合 {#integrating-with-scene}

Adobe Dynamic Media Classic は、動的なマーケティングアセットやリッチなビジュアルマーチャンダイジングを公開、管理、強化したり、web、モバイル、メール、ソーシャルメディア、インターネットに接続されたディスプレイやプリンターへ配信したりするためのホスト型ソリューションです。

Adobe Experience Manager では、デジタルアセットを Adobe Experience Manager から Dynamic Media Classic に直接公開でき、Dynamic Media Classic から Adobe Experience Manager にも公開できます。

また、Dynamic Media Classic に公開された Adobe Experience Manager アセットを、ベーシックズームやビデオなどの様々なビューアで表示できます。

Adobe Experience Manager と Dynamic Media Classic の統合方法について詳しくは、[Dynamic Media Classic との統合](/help/sites-administering/scene7.md)に関するドキュメントを参照してください。

## Adobe Dynamic Tag Management との統合 {#integrating-with-adobe-dynamic-tag-management}

[Adobe Dynamic Tag Management](https://business.adobe.com/jp/products/experience-platform/adobe-experience-platform.html?lang=ja) は直感的なツールであり、このツールを使用することでマーケターは、アドビやサードパーティのタグを数に制限なく、すばやく簡単に管理できます。IT リソースへの依存度を減らしながら、オンライン上のほぼすべてのアセットを最適化するためのコントロールと柔軟性を向上することができます。

[Adobe Dynamic Tag Management](/help/sites-administering/dtm.md) と AEM を統合すると、Dynamic Tag Management の web プロパティを使用して AEM Sites を追跡できます。

## Adobe Audience Manager との統合 {#integrating-with-adobe-audience-manager}

Audience Manager の統合は、AEM 6.3 で削除されました。

<!-- Search&Promote is end of life as of September 1, 2022 ## Integrating with Search&Promote {#integrating-with-search-promote} -->

<!-- Search&Promote is end of life as of September 1, 2022 Adobe Search&Promote enables marketers to optimizehow visitors browse, find, compare, and select relevant products and content on web and mobile sites. Businesses can easily promote priority items based on business objectives and visitor intent, and automate merchandising and promotions activity via KPI-based triggers or metrics. -->

<!-- Search&Promote is end of life as of September 1, 2022 Adobe Search&Promote is a reliable and scalable hosted site search application, capable of scaling to millions of pages or products, for heavily visited online businesses ranging from retail to news sites. It offers unprecedented levels of marketer control and metrics-based relevance. -->

<!-- Search&Promote is end of life as of September 1, 2022 For information about integrating AEM and Search&Promote, see [Integrating with Adobe Search&Promote](/help/sites-administering/search-and-promote.md). -->

## Adobe Campaign との統合 {#integrating-with-adobe-campaign}

[Adobe Campaign](https://business.adobe.com/jp/products/campaign/adobe-campaign.html?lang=ja) では、メール配信コンテンツを Adobe Experience Manager で直接管理できます。

AEM と Adobe Campaign との統合方法について詳しくは、[Adobe Campaign との統合](/help/sites-administering/campaignstandard.md)を参照してください。