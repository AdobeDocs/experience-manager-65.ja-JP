---
title: キャンペーンの管理
description: キャンペーン管理では、デジタルマーケターは、パーソナライズされたコンテンツを配信し、訪問者に対して個別のエクスペリエンスを作成できます。これにより、web、メールおよびモバイルサービス内のマーケティングキャンペーンを統合し、訪問者との関係を深めることができます。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: d1741525-a475-4a76-bd16-55318023495e
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: ht
source-wordcount: '620'
ht-degree: 100%

---


# キャンペーンの管理 {#campaign-management}

キャンペーン管理では、デジタルマーケターは、パーソナライズされたコンテンツを配信し、訪問者に対して個別のエクスペリエンスを作成できます。

これにより、web、メールおよびモバイルサービス内のマーケティングキャンペーンを統合し、訪問者との関係を深めることができます。コンテンツの作成、訪問者のセグメント化、特定のユーザープロファイルに対するターゲットコンテンツのプッシュと促進を行い、複数のチャネルにわたりキャンペーンを管理できます。

このドキュメントでは、キャンペーンを構成する様々な要素について説明します。詳しくは、以下のドキュメントを参照してください。

* [ティーザーと戦略 ](/help/sites-classic-ui-authoring/classic-personalization-campaigns-teasers-strategy.md)
* [メールマーケティング](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email.md)
* [ランディングページ](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md)
* [Target オファー](/help/sites-classic-ui-authoring/classic-personalization-campaigns-target-offers.md)
* [Marketing Campaign Manager の使用 ](/help/sites-classic-ui-authoring/classic-personalization-campaigns-mktg-manager.md)
* [セグメント化について ](/help/sites-classic-ui-authoring/classic-personalization-campaigns-segmentation.md)
* [キャンペーンの設定 ](/help/sites-classic-ui-authoring/classic-personalization-campaigns-setting-up-your.md)

キャンペーン管理は、以下の様々な要素で構成されています。

* **ブランド**
Adobe Experience Manager（AEM）では、ブランドは最上位の単位で、**キャンペーン**&#x200B;のコレクションを形成します。

* **キャンペーン**
キャンペーンは個別の**エクスペリエンス**&#x200B;のコレクションです。

* **エクスペリエンス**
フォーカスされたコンテンツは様々なエクスペリエンスを形成し、**タッチポイント**&#x200B;で訪問者に提示されます。以下のような様々なタイプのエクスペリエンスが使用できます。

   * **ティーザー**
     [ティーザーページ／段落](#teasers)を使用して、特定の訪問者&#x200B;**セグメント**&#x200B;を、その訪問者の関心に基づきフォーカスされたコンテンツに誘導します。

     ティーザーページでは、次のようなことができます。

      * 訪問者が選択できる様々なオプションを提示します。
      * 特定の訪問者セグメントに基づくティーザー段落を 1 つだけ表示します。例えば、訪問者の年齢によって異なるティーザー段落を表示できます。

     通常、ティーザーページは、後続のティーザーページに変わるまでの特定の期間継続する一時的なアクションです。

   * **ニュースレター**

     [メール通信](#emailmarketing)を使用してユーザーとの関係を深め、web サイトを訪問するよう促します。通常はニュースレターの形式で、**リード**（通常は&#x200B;**リスト**&#x200B;にグループ化されます）に送信されます。**メモ：**&#x200B;この機能がさらに強化される予定はありません。[Adobe Campaign や AEM との統合を利用](/help/sites-administering/campaign.md)することをお勧めします。

   * **Adobe Target**

     Adobe Target（旧称 Test&amp;Target）と統合します。これにより、マーケターはコンバージョン web サイト最適化ツールを使用できるようになります。このツールには、オンラインコンテンツおよびオファーと顧客との関連性を継続的に高め、より多くのコンバージョンを生み出すために必要な機能があります。Adobe Target の直感的なインターフェイスにより、テストのデザインと実行、オーディエンスセグメントの作成、およびコンテンツのターゲティングができます。これらの機能はすべて 1 つのアプリケーションから提供されます。

* **タッチポイント**

  訪問者とキャンペーンとの接点です。タッチポイントは、作成したエクスペリエンスに関連付けられます。

  例えば、ティーザーの場合はティーザー段落が配置されているコンテンツページであり、ニュースレターの場合はメーリングリストです。

* **リード数**

  訪問者について収集した情報で、これらの訪問者への連絡方法がリードの基盤となります。**注意：**&#x200B;この機能がさらに強化される予定はありません。

  [Adobe Campaign や AEM との統合を利用](/help/sites-administering/campaign.md)することをお勧めします。

* **リスト**

  リードはリストにグループ化されているため、これらのリード全体に対してアクションを実行することができます。**メモ：**&#x200B;この機能がさらに強化される予定はありません。

  [Adobe Campaign や AEM との統合を利用](/help/sites-administering/campaign.md)することをお勧めします。

* **セグメント**

  サイトにアクセスする訪問者は、様々な関心と目的を持っています。Web サイト上でのアクティビティ、登録されたプロファイル情報、および他の web サイト上でのアクティビティなどの要素に応じて分析すると、セグメントの定義に役立ちます。そうすると、一致するセグメントに基づいて、訪問者のニーズと関心に合わせてコンテンツを絞り込むことができます。

* **MCM**

  Marketing Campaign Manager（MCM）は、キャンペーン、ブランド、エクスペリエンス、タッチポイント、リード、リスト、セグメントおよびレポートの作成と制御に必要なすべての機能にアクセスできるコンソールです。

  様々な場所（**キャンペーン**&#x200B;のラベル付き）またはを次の URL などを使用してアクセスできます。

  `http://localhost:4502/libs/mcm/content/admin.html`
