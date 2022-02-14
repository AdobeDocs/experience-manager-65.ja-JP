---
title: 'キャンペーンの管理 '
seo-title: Campaign Management
description: キャンペーン管理では、デジタルマーケティング担当者は、パーソナライズされたコンテンツを配信し、訪問者に対して個別のエクスペリエンスを作成できます。これにより、Web、電子メールおよびモバイルサービス内のマーケティングキャンペーンを統合し、訪問者との関係を深めることができます。
seo-description: Campaign management provides digital marketers the opportunity to deliver personalized content and so create dedicated experiences for visitors. It allows you to orchestrate your marketing campaigns across the web, email and mobile services and so engage your visitors.
uuid: 202d614b-a607-45de-8c24-1ee66b230315
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: e8b70971-4f23-45f8-8c23-e147413243c2
exl-id: d1741525-a475-4a76-bd16-55318023495e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '628'
ht-degree: 100%

---

# キャンペーンの管理 {#campaign-management}

キャンペーン管理では、デジタルマーケティング担当者は、パーソナライズされたコンテンツを配信し、訪問者に対して個別のエクスペリエンスを作成できます。

これにより、Web、電子メールおよびモバイルサービス内のマーケティングキャンペーンを統合し、訪問者との関係を深めることができます。複数のチャネルにわたり、コンテンツの作成、訪問者のセグメント化、特定のユーザープロファイルに対するターゲットコンテンツのプッシュと促進をおこなうことができます。

このドキュメントでは、キャンペーンを構成する様々な要素について説明します。詳細な情報は、次のドキュメントを参照してください。

* [ティーザーと戦略 ](/help/sites-classic-ui-authoring/classic-personalization-campaigns-teasers-strategy.md)
* [メールマーケティング](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email.md)
* [ランディングページ](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md)
* [Target オファー](/help/sites-classic-ui-authoring/classic-personalization-campaigns-target-offers.md)
* [Marketing Campaign Manager の使用 ](/help/sites-classic-ui-authoring/classic-personalization-campaigns-mktg-manager.md)
* [セグメント化について ](/help/sites-classic-ui-authoring/classic-personalization-campaigns-segmentation.md)
* [キャンペーンの設定 ](/help/sites-classic-ui-authoring/classic-personalization-campaigns-setting-up-your.md)

キャンペーン管理は、次の様々な要素から構成されています。

* **ブランド**
AEM では、ブランドは最上位の単位であり、 
**キャンペーン**&#x200B;のコレクションを形成します。

* **Campaigns**
キャンペーンは個別の 
**エクスペリエンス**&#x200B;のコレクションです。

* **エクスペリエンス**
様々なエクスペリエンスを形成するフォーカスされたコンテンツです。 
それぞれの&#x200B;**タッチポイント**&#x200B;で訪問者に表示されます。次のような様々なタイプのエクスペリエンスが使用できます。

   * **Teaser**
      [ティーザーページ／段落](#teasers)を使用して、特定の訪問者&#x200B;**セグメント**&#x200B;を、その訪問者の関心に基づきフォーカスされたコンテンツに誘導します。

      Teaser ページでは、次のようなことができます。

      * 訪問者が選択できる選択肢の範囲を表示します。
      * 特定の訪問者セグメントに基づくティーザー段落を 1 つだけ表示します。例えば、訪問者の年齢に応じてティーザー段落を表示できます。

      通常、Teaser ページは、次の Teaser ページに変わるまでの特定の期間継続する一時的なアクションです。

   * **ニュースレター**

      [メール通信](#emailmarketing)を使用してユーザーとの関係を深め、web サイトを訪問するよう促します。通常はニュースレターの形式で&#x200B;**リード**（通常は&#x200B;**リスト**&#x200B;にグループ化されます）に送信されます。**注意：**&#x200B;この機能がさらに強化される予定はありません。[Adobe Campaign や AEM との統合を利用](/help/sites-administering/campaign.md)することをお勧めします。

   * **Adobe Target**

       Adobe Target （旧称 Test&amp;Target）と統合します。これにより、マーケティング担当者はコンバージョン web サイト最適化ツールを使用できるようになります。このツールには、オンラインコンテンツおよびオファーと顧客との関連性を継続的に高め、より多くのコンバージョンを生み出すために必要な機能があります。Adobe Target の直感的なインターフェイスにより、テストのデザインと実行、オーディエンスセグメントの作成、およびコンテンツのターゲット設定ができます。これらの機能はすべて 1 つのアプリケーションから提供されます。


* **タッチポイント**

   訪問者とキャンペーンとの接点です。タッチポイントは、作成したエクスペリエンスに関連付けられます。

   例えば、Teaser の場合は Teaser 段落が配置されているコンテンツページ、ニュースレターの場合はメーリングリストです。

* **リード数**

   訪問者について収集した情報で、これらの訪問者への連絡方法がリードの基盤となります。**注意：**&#x200B;この機能がさらに強化される予定はありません。

   [Adobe Campaign や AEM との統合を利用](/help/sites-administering/campaign.md)することをお勧めします。

* **リスト**

   リードは通常、リストにグループ分けされ、これらのリード全体に対してアクションを実行することができます。**注意：**&#x200B;この機能がさらに強化される予定はありません。

   [Adobe Campaign の利用や AEM との統合環境の利用](/help/sites-administering/campaign.md)をお勧めします。

* **セグメント**

   サイトにアクセスする訪問者は、様々な関心と目的を持っています。Web サイト上でのアクティビティ、登録されたプロファイル情報、および他の Web サイト上でのアクティビティに基づき訪問者の関心や目的を分析することにより、セグメントを定義できます。一致するセグメントに基づいて、訪問者のニーズと関心に特化したコンテンツを表示できます。

* **MCM**

   Marketing Campaign Manager（MCM）は、キャンペーン、ブランド、エクスペリエンス、タッチポイント、リード、リスト、セグメントおよびレポートの作成および制御に必要なすべての機能にアクセスできるコンソールです。

   様々な場所（「**キャンペーン**」のラベル）から、または次の URL などを使用してアクセスできます。

   `http://localhost:4502/libs/mcm/content/admin.html`
