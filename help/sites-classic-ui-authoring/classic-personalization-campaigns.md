---
title: キャンペーンの管理
seo-title: キャンペーンの管理
description: キャンペーン管理では、デジタルマーケティング担当者は、パーソナライズされたコンテンツを配信し、訪問者に対して個別のエクスペリエンスを作成できます。これにより、Web、電子メールおよびモバイルサービス内のマーケティングキャンペーンを統合し、訪問者との関係を深めることができます。
seo-description: キャンペーン管理では、デジタルマーケティング担当者は、パーソナライズされたコンテンツを配信し、訪問者に対して個別のエクスペリエンスを作成できます。これにより、Web、電子メールおよびモバイルサービス内のマーケティングキャンペーンを統合し、訪問者との関係を深めることができます。
uuid: 202d614b-a607-45de-8c24-1ee66b230315
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: e8b70971-4f23-45f8-8c23-e147413243c2
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 88%

---


# キャンペーンの管理{#campaign-management}

キャンペーン管理では、デジタルマーケティング担当者は、パーソナライズされたコンテンツを配信し、訪問者に対して個別のエクスペリエンスを作成できます。

これにより、Web、電子メールおよびモバイルサービス内のマーケティングキャンペーンを統合し、訪問者との関係を深めることができます。複数のチャネルにわたり、コンテンツの作成、訪問者のセグメント化、特定のユーザープロファイルに対するターゲットコンテンツのプッシュと促進をおこなうことができます。

このドキュメントでは、キャンペーンを構成する様々な要素について説明します。詳細な情報は、次のドキュメントを参照してください。

* [ティーザーと戦略](/help/sites-classic-ui-authoring/classic-personalization-campaigns-teasers-strategy.md)
* [電子メールマーケティング](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email.md)
* [ランディングページ](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md)
* [Target オファー](/help/sites-classic-ui-authoring/classic-personalization-campaigns-target-offers.md)
* [Marketing Campaign Manager の使用](/help/sites-classic-ui-authoring/classic-personalization-campaigns-mktg-manager.md)
* [セグメント化について](/help/sites-classic-ui-authoring/classic-personalization-campaigns-segmentation.md)
* [キャンペーンの設定](/help/sites-classic-ui-authoring/classic-personalization-campaigns-setting-up-your.md)

キャンペーン管理は、次の様々な要素から構成されています。

* **ブランド**
AEMでは、ブランドは最上位レベルのユニットで、 
**キャンペーン**.

* **キャンペーン**&#x200B;キャンペーンは、個々の 
**エクスペリエンス**.

* **エクスペリエンス**&#x200B;特化されたコンテンツは様々なエクスペリエンスを形成し、次の場所で訪問者に提示します。 
**タッチポイント**. 次のような様々なタイプのエクスペリエンスが使用できます。

   * **Teaser**
      [Teaserページ/段落](#teasers) は、特定の訪問者 **** セグメントを関心に焦点を当てたコンテンツに導くために使用します。

      Teaser ページでは、次のようなことができます。

      * 訪問者が選択できる選択肢の範囲を表示します。
      * 特定の訪問者セグメントに基づくティーザー段落を 1 つだけ表示します。例えば、訪問者の年齢に応じてティーザー段落を表示できます。

      通常、Teaser ページは、次の Teaser ページに変わるまでの特定の期間継続する一時的なアクションです。

   * **ニュースレター**

      [電子メール通信](#emailmarketing) (E-mail Communications)は、ユーザーを惹きつけ、Webサイトに来るよう促すために使用します。 通常はニュースレターの形式で&#x200B;**リード**（通常は&#x200B;**リスト**&#x200B;にグループ化されます）に送信されます。**注意：**&#x200B;この機能がさらに強化される予定はありません。[Adobe Campaign や AEM との統合を利用](/help/sites-administering/campaign.md)することをお勧めします。

   * **Adobe Target**

       Adobe Target （旧称 Test&amp;Target）と統合します。これにより、マーケティング担当者はコンバージョン Web サイト最適化ツールを使用できるようになります。このツールには、オンラインコンテンツおよびオファーと顧客との関連性を継続的に高め、より多くのコンバージョンを生み出すために必要な機能があります。Adobe Target の直感的なインターフェイスにより、テストのデザインと実行、オーディエンスセグメントの作成、およびコンテンツのターゲット設定ができます。これらの機能はすべて 1 つのアプリケーションから提供されます。


* **タッチポイント**

   訪問者とキャンペーンとの接点です。タッチポイントは、作成したエクスペリエンスに関連付けられます。

   例えば、Teaser の場合は Teaser 段落が配置されているコンテンツページ、ニュースレターの場合はメーリングリストです。

* **リード数**

   訪問者について収集した情報で、これらの訪問者への連絡方法がリードの基盤となります。**注意：**&#x200B;この機能がさらに強化される予定はありません。

   [Adobe Campaign や AEM との統合を利用](/help/sites-administering/campaign.md)することをお勧めします。

* **リスト**

   リードは通常、リストにグループ分けされ、これらのリード全体に対してアクションを実行することができます。**注意：**&#x200B;この機能がさらに強化される予定はありません。

   Recommendation is to [leverage Adobe Campaign and the integration to AEM.](/help/sites-administering/campaign.md)

* **セグメント**

   サイトにアクセスする訪問者は、様々な関心と目的を持っています。Web サイト上でのアクティビティ、登録されたプロファイル情報、および他の Web サイト上でのアクティビティに基づき訪問者の関心や目的を分析することにより、セグメントを定義できます。一致するセグメントに基づいて、訪問者のニーズと関心に特化したコンテンツを表示できます。

* **MCM**

   Marketing Campaign Manager（MCM）は、キャンペーン、ブランド、エクスペリエンス、タッチポイント、リード、リスト、セグメントおよびレポートの作成および制御に必要なすべての機能にアクセスできるコンソールです。

   様々な場所（「**キャンペーン**」のラベル）から、または次の URL などを使用してアクセスできます。

   `http://localhost:4502/libs/mcm/content/admin.html`

