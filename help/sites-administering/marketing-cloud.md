---
title: Adobe Marketing Cloud との統合
description: Adobe Experience Manager と Adobe Marketing Cloud を統合する方法を学びます。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: ba518290-dd82-44dc-ae7c-c8152df89179
source-git-commit: 58594be73372e128ba999a8290615fbcb447084e
workflow-type: ht
source-wordcount: '873'
ht-degree: 100%

---

# Adobe Marketing Cloud との統合{#integrating-with-the-adobe-marketing-cloud}

[Adobe Marketing Cloud](https://www.adobe.com/jp/solutions/digital-marketing.html) には、すぐに利用可能なリアルタイムのデータおよび情報を提供してオンラインビジネスを成功に導く、強力な Web 分析および Web サイト最適化製品が含まれています。Adobe Marketing Cloud は、オンラインビジネス最適化のための統合されたオープンプラットフォームを提供します。Adobe Marketing Cloud は、顧客のインサイトを収集してその力を解き放ち、顧客の獲得、コンバージョンおよび維持の取り組みやコンテンツの作成および配信を最適化する統合アプリケーションにより構成されます。

Adobe Experience Manager（AEM）は、Adobe Marketing Cloud の次の製品とシームレスに統合できます。

* Adobe Analytics：マーケティング担当者は、オンライン戦略やマーケティング戦略に関して、すぐに利用可能なリアルタイムの情報を入手できます。
* Adobe Target：顧客へのオンラインコンテンツの関連性を継続的に高め、より多くのコンバージョンを生み出すための機能をマーケティング担当者に提供します。
* Adobe Dynamic Media Classic は、メディア管理の自動化、web パブリッシングの効率化、および web エクスペリエンスの強化をホストされた環境内で行います。
* Adobe Dynamic Tag Management：アドビやサードパーティのタグをいくつでもすばやく簡単に管理できる直感的なツールをマーケティング担当者に提供します。
<!-- Search&Promote is end of life as of September 1, 2022 * Adobe Search&Promote gives marketers the ability to control and optimize the search results on their sites. -->
* Adobe Campaign：メール配信コンテンツを Adobe Experience Manager で直接管理できます。

さらに、AEM を [Creative Cloud と統合](/help/assets/aem-cc-integration-best-practices.md)したり、[サードパーティのサービス](/help/sites-administering/third-party-services.md)と統合したりすることもできます。

## Adobe Analytics との統合 {#integrating-with-adobe-analytics}

[Adobe Analytics](https://www.omniture.com/jp/products/analytics/sitecatalyst) は、様々なマーケティングチャネルにまたがるオンライン戦略全体からの統合データを 1 箇所で測定、分析、最適化できる場をディジタルマーケターに提供する、業界最先端のソリューションです。マーケティング担当者は、デジタル戦略やマーケティング施策に関して、すぐに利用可能なリアルタイムの web 分析情報を入手できます。Adobe Analytics を使用すると、マーケティング担当者は Web サイト内で最も収益性に優れたパスの迅速な特定、価値の高い Web の訪問者を見分けるためのトラフィックの区分、訪問者がサイトを離れた経路の判断、およびオンラインマーケティングキャンペーンにとって重要な成功指標の特定をおこなうことができます。

Adobe Analytics を使用すると、サイトのデータを分析できます。

Adobe Analytics との統合によって、次の操作ができるようになります。

* Analytics のユーザートラッキングを有効にする。
* 実行モード（オーサー、パブリッシュなど）をそれぞれ異なるレポートスイートにマッピングする。
* ClientContext の変数をコンバージョン変数またはトラフィックプロパティとして送信する。
* 定義済みの変数マッピングを使用する。
* 完全なサイトセクションの設定を一度におこなう。
* カスタム定義のイベントを追跡する。

AEM と Analytics の統合について詳しくは、[Adobe Analytics との統合](/help/sites-administering/adobeanalytics.md)を参照してください。

[オプトインウィザード](/help/sites-administering/opt-in.md)を使用して簡単に統合を行うこともできます。

## Adobe Target との統合 {#integrating-with-adobe-target}

[Adobe Target](https://www.omniture.com/jp/products/conversion/test-and-target) を使用すると、マーケティング担当者は、オンラインテストをデザインして実行し、行動に基づいたオーディエンスセグメントをその場で作成し、コンテンツとオンラインのエクスペリエンスを自動的にターゲット設定できるようになります。

今日のオンラインユーザーは常にニーズを進化させてきており、幅広いサイトやコンテンツのソースから、関連性があり、パーソナライズまでされたコンテンツを選択できることを期待します。オンラインオーディエンスを引き付けるには、オンラインマーケティング担当者が、オーディエンスとの関連性がある魅力的なオファーやコンテンツをすぐに特定できることが不可欠です。この知識によって武装しながら、継続的にサイトを進化させ、様々なオーディエンスに対して適切なコンテンツをターゲティングできる必要があります。

[Adobe Target との統合](/help/sites-administering/target.md)では、サイトと Target の統合方法について説明しています。

[オプトインウィザード](/help/sites-administering/opt-in.md)を使用して簡単に統合を行うこともできます。

## Analytics および Target へのオプトイン {#opting-in-to-analytics-and-target}

AEM は、Adobe Analytics および Adobe Target と統合するための簡単なオプトイン手順を提供しています。管理者としてログインしてプロジェクトコンソールにアクセスすると、オプトインウィザードが表示されます。

![chlimage_1-107](assets/chlimage_1-107a.png)

Analytics や Target との統合をオプトインすれば、そのページ追跡機能や分析機能、およびパーソナライゼーション機能を利用できるようになります。オプトインするときに、ユーザーアカウント情報を入力して、追跡するページを指定する必要があります。

詳しくは、[Adobe Analytics および Adobe Target との統合のオプトイン](/help/sites-administering/opt-in.md)を参照してください。

## Adobe Dynamic Media Classic との統合 {#integrating-with-scene}

Adobe Dynamic Media Classic は、動的なマーケティングアセットやリッチなビジュアルマーチャンダイジングを公開、管理、強化したり、web、モバイル、メール、ソーシャルメディア、インターネットに接続されたディスプレイやプリンターへ配信したりするためのホスト型ソリューションです。

Adobe Experience Manager では、デジタルアセットを Adobe Experience Manager から Dynamic Media Classic に直接公開でき、Dynamic Media Classic から Adobe Experience Manager にも公開できます。

また、Dynamic Media Classic に公開された Adobe Experience Manager アセットを、ベーシックズームやビデオなどの様々なビューアで表示できます。

Adobe Experience Manager と Dynamic Media Classic の統合方法について詳しくは、[Dynamic Media Classic との統合](/help/sites-administering/scene7.md)に関するドキュメントを参照してください。

## Adobe Dynamic Tag Management との統合 {#integrating-with-adobe-dynamic-tag-management}

[Adobe Dynamic Tag Management](https://www.adobe.com/jp/solutions/digital-marketing/dynamic-tag-management.html) は直感的なツールであり、このツールを使用することでマーケティング担当者は、アドビやサードパーティのタグを数に制限なく、すばやく簡単に管理できます。ほぼすべてのオンラインアセットをより細かく、より柔軟に最適化でき、かつ IT リソースへの依存度を減らすことができます。

[Adobe Dynamic Tag Management](/help/sites-administering/dtm.md) と AEM を統合すると、Dynamic Tag Management の web プロパティを使用して AEM サイトを追跡できます。

## Adobe Audience Manager との統合 {#integrating-with-adobe-audience-manager}

Audience Manager 統合は AEM 6.3 では削除されています。

<!-- Search&Promote is end of life as of September 1, 2022 ## Integrating with Search&Promote {#integrating-with-search-promote} -->

<!-- Search&Promote is end of life as of September 1, 2022 Adobe Search&Promote enables marketers to optimizehow visitors browse, find, compare, and select relevant products and content on web and mobile sites. Businesses can easily promote priority items based on business objectives and visitor intent, as well as automate merchandising and promotions activity via KPI-based triggers or metrics. -->

<!-- Search&Promote is end of life as of September 1, 2022 Adobe Search&Promote is a reliable and scalable hosted site search application, capable of scaling to millions of pages or products, for heavily visited online businesses ranging from retail to news sites. It offers unprecedented levels of marketer control and metrics-based relevance. -->

<!-- Search&Promote is end of life as of September 1, 2022 For information about integrating AEM and Search&Promote, see [Integrating with Adobe Search&Promote](/help/sites-administering/search-and-promote.md). -->

## Adobe Campaign との統合 {#integrating-with-adobe-campaign}

[Adobe Campaign](https://www.adobe.com/jp/solutions/campaign-management.html) では、電子メール配信コンテンツを Adobe Experience Manager で直接管理できます。

AEM と Adobe Campaign との統合方法について詳しくは、[Adobe Campaign との統合](/help/sites-administering/campaignstandard.md)を参照してください。

## Livefyre との統合 {#integrating-with-livefyre}

AEM と Livefyre については、次を参照してください。

* [Livefyre 使用の手引き](https://answers.livefyre.com/developers/getting-started)

* [Livefyre と AEM](https://answers.livefyre.com/product/livefyre-for-adobe-experience-manager-aem/livefyre-for-adobe-experience-manager/)
