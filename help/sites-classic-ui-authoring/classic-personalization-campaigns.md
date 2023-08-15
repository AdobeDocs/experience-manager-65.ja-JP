---
title: キャンペーンの管理
description: キャンペーン管理は、デジタルマーケターに対して、パーソナライズされたコンテンツを配信し、訪問者に向けた専用のエクスペリエンスを作成する機会を提供します。 Web、E メール、Mobile Services 全体でマーケティングキャンペーンを調整し、訪問者を惹きつけることができます。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: d1741525-a475-4a76-bd16-55318023495e
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '621'
ht-degree: 20%

---


# キャンペーンの管理 {#campaign-management}

キャンペーン管理は、デジタルマーケターに対して、パーソナライズされたコンテンツを配信し、訪問者に向けた専用のエクスペリエンスを作成する機会を提供します。

Web、E メール、Mobile Services 全体でマーケティングキャンペーンを調整し、訪問者を惹きつけることができます。 コンテンツの作成、訪問者のセグメント化、プッシュ、特定のユーザープロファイル向けのターゲットコンテンツのプロモーション、複数のチャネルにわたるキャンペーンの管理をおこなうことができます。

このドキュメントでは、キャンペーンを構成する様々な要素について説明します。 詳しくは、次のドキュメントを参照してください。

* [ティーザーと戦略 ](/help/sites-classic-ui-authoring/classic-personalization-campaigns-teasers-strategy.md)
* [メールマーケティング](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email.md)
* [ランディングページ](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md)
* [Target オファー](/help/sites-classic-ui-authoring/classic-personalization-campaigns-target-offers.md)
* [Marketing Campaign Manager の使用 ](/help/sites-classic-ui-authoring/classic-personalization-campaigns-mktg-manager.md)
* [セグメント化について ](/help/sites-classic-ui-authoring/classic-personalization-campaigns-segmentation.md)
* [キャンペーンの設定 ](/help/sites-classic-ui-authoring/classic-personalization-campaigns-setting-up-your.md)

キャンペーン管理は、次の様々な要素で構成されています。

* **ブランド**
Adobe Experience Manager(AEM) では、ブランドは最上位の単位で、 **キャンペーン**.

* **キャンペーン**
キャンペーンは個人の集まりです **エクスペリエンス**.

* **エクスペリエンス**
フォーカスされたコンテンツは、様々なエクスペリエンスを形成し、次の場所で訪問者に表示されます。 **タッチポイント**. 次のような様々なタイプのエクスペリエンスを使用できます。

   * **ティーザー**
     [ティーザーページ／段落](#teasers)を使用して、特定の訪問者&#x200B;**セグメント**&#x200B;を、その訪問者の関心に基づきフォーカスされたコンテンツに誘導します。

     ティーザーページでは、次のことが可能です。

      * 訪問者が選択できる様々なオプションを提示する
      * 特定の訪問者セグメントに基づくティーザー段落を 1 つだけ表示します。 例えば、表示されるティーザー段落は、訪問者の年齢によって異なる場合があります。

     通常、ティーザーページは、特定の期間、次のティーザーページに置き換えられるまで持続する一時的なアクションです。

   * **ニュースレター**

     [メール通信](#emailmarketing)を使用してユーザーとの関係を深め、web サイトを訪問するよう促します。通常はニュースレターの形式で、お客様の **リード** ( これらは、 **リスト**) をクリックします。 **注意：**&#x200B;この機能がさらに強化される予定はありません。お勧めは次のとおりです。 [Adobe CampaignとAEMの統合の使用](/help/sites-administering/campaign.md).

   * **Adobe Target**

     これにより、Adobe Target（旧称 Test&amp;Target）との統合が可能になり、マーケティング担当者は、オンラインコンテンツを継続的に作成するのに必要な機能を備えたコンバージョン Web サイト最適化ツールを提供し、顧客の生み出すコンバージョン率を高めます。 Adobe Targetは、テストの設計と実行、オーディエンスセグメントの作成、コンテンツのターゲティングを 1 つのアプリケーションから行うための直感的なインターフェイスを提供します。

* **タッチポイント**

  これらは、訪問者とキャンペーンの間の連絡先です。 タッチポイントは、作成したエクスペリエンスに関連付けられています。

  例えば、ティーザーの場合はティーザー段落が配置されているコンテンツページで、ニュースレターの場合はメーリングリストです。

* **リード数**

  訪問者について収集した情報で、これらの訪問者への連絡方法がリードの基盤となります。**注意：**&#x200B;この機能がさらに強化される予定はありません。

  お勧めは次のとおりです。 [Adobe CampaignとAEMの統合の使用](/help/sites-administering/campaign.md).

* **リスト**

  リードはリストにグループ化され、リードに対して一括的なアクションを実行できます。 **注意：**&#x200B;この機能がさらに強化される予定はありません。

  お勧めは次のとおりです。 [Adobe CampaignとAEMの統合を使用します。](/help/sites-administering/campaign.md)

* **セグメント**

  サイトにアクセスする訪問者は、様々な関心と目的を持っています。Web サイト上のアクティビティ、登録されたプロファイル情報、他の Web サイト上のアクティビティなどの要因に従ってこれを分析すると、セグメントを定義できます。 一致するセグメントに従って、訪問者のニーズと興味に合わせてコンテンツをターゲット設定できます。

* **MCM**

  マーケティングキャンペーンマネージャー (MCM) は、キャンペーン、ブランド、エクスペリエンス、タッチポイント、リード、リスト、セグメントおよびレポートの作成および制御に必要なすべての機能にアクセスできるコンソールです。

  様々な場所 ( **キャンペーン**) またはを次の URL などに置き換えます。

  `http://localhost:4502/libs/mcm/content/admin.html`
