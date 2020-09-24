---
title: 翻訳のベストプラクティス
seo-title: 翻訳のベストプラクティス
description: アドビのエンジニアリングおよびコンサルティングチームがまとめたベストプラクティスを確認し、翻訳プロジェクトの導入および運用に役立ててください。
seo-description: アドビのエンジニアリングおよびコンサルティングチームがまとめたベストプラクティスを確認し、翻訳プロジェクトの導入および運用に役立ててください。
uuid: 3bac1d73-9696-4c9b-8bdd-6f00fac40cf7
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features, best-practices
content-type: reference
discoiquuid: 1554010e-a1d1-4edf-b28f-9eead8f83b4a
translation-type: tm+mt
source-git-commit: a929252a13f66da8ac3e52aea0655b12bdd1425f
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 64%

---


# 翻訳のベストプラクティス{#translation-best-practices}

## 一般 {#general}

グローバル Web プレゼンスの作成や拡張は複雑なプロセスになる可能性がありますが、事前に AEM について適切に考慮および計画しておけば、作業を簡略化してグローバルなビジネス目標をサポートできます。

* **最初のサイトを実装する前に** 、グローバルな拡張を計画します。サイトが短い通知で実装された場合に、既存のサイトをグローバルな範囲に適合させるのは、通常、最初にグローバルな拡張を計画するよりも難しくなります。

   * Assess the current state of your organization’s localization maturity. Determine whether you have the **tools**, **processes** and **resources** in place to support global expansion.
   * Be aware of **global regulations** and **regional language preferences**. Design flexible content structures and processes that can accommodate a changing global business environment.

* Determine a **governance** model that supports your global business and use AEM mechanisms like MSM and user permissions to enforce your chosen model. For example, determine if content will be centrally authored and “pushed” or “pulled” to regions/countries. Determine what content can be unlocked and altered in the geographies. Determine who is responsible for initiating and managing translations.
* リソースに余裕がある場合は、必要なツール、プロセスおよびベンダーとの関係の専門知識を養うことのできる中央のチームが翻訳アクティビティを管理することをお勧めします。
* **グローバルな構造とプロセスを計画**、 **プロトタイプ** 、 **テストし** 、ビジネスをサポートし、各地の関係者から必要なサポートを受けられるようにします。

## サイト構造 {#site-structure}

* サイト構造を設計する場合は、最初にコンテンツを調査し、どこでどのような言語コンテンツをオーサリングするかを特定します。この位置をサイトのトップレベルにしてください。
* トップレベルのオーサリングサイトと各国のサイト間の&#x200B;**言語ベースの構造**&#x200B;を 3 レベル以下にすることをお勧めします。
* **W3C 標準**&#x200B;に準拠する言語／国のサイト命名規則を使用します。
* 地域別および国別のコンテンツの配信方法を指定します。言語を共有する国について検討してください。言語マスター（アクティベートされていないページのレイヤー）を作成することをお勧めします。言語マスターを使用すると、翻訳コンテンツをレビューおよび変更してから、対象の言語を共有する国のサイトに対してプッシュまたはプルできます。
* 言語マスターを作成するには、言語コピーを使用するアプローチと MSM／ライブコピーを使用するアプローチの 2 つがあります。

   * 言語コピーアプローチは、AEM の標準の翻訳統合フレームワークで使用されるアプローチなので、非常に簡単に開始できます。このフレームワークが提供するユーザーインターフェイスでは、初期段階でメイン言語マスター（英語など）からその他の言語マスターにコンテンツの変更を簡単に反映して翻訳できます。ただし、プロジェクトの規模が大きくなるのに伴い、ページや言語も増加し、それらの翻訳を管理するためにワークフローの自動化の必要性が増してきます。
   * MSM／ライブコピーアプローチは、より大規模で複雑なサイトにおける高度な使用事例に対応するための代替手法です。英語と言語マスターの間の複雑な継承関係を処理したり、既存の翻訳を上書きするリスクを軽減したりするには、強力なガバナンスとワークフローの自動処理が最初から必要になります。これには、いくつかの翻訳コネクターを利用して対応できます。See [MSM and Multilingual Sites](/help/sites-administering/msm-best-practices.md#msm-and-multilingual-websites) for more information.

* マスター言語にグローバルなバリエーションがある場合は、MSM を使用して、翻訳に使用するグローバルマスターからライブコピーを作成できます。例えば、英語（米国）のマスターでグローバルオーサリングが実行される場合は、各国対応の英語のマスターを、他の言語に翻訳するためのライブコピーおよび基盤として作成します。
* MSM を使用して、翻訳済みの言語マスターから各国のサイトを作成し、同じ言語を共有するサイトにコンテンツをロールアウトします。例えば、フランス語の言語マスターをフランス、ベルギーおよびスイスのサイトにロールアウトできます。
* 実装を開始する前に、まず計画、プロトタイプ作成およびテストを実施します。

## 翻訳のプロセスと方法 {#translation-processes-and-methods}

* Engage a **localization service provider (LSP)** with expertise in translation and related localization activities. LSPs can help to scale your global business by providing a breadth of resources and technologies to improve efficiency and save translation costs:

   * 一部の LSP はサービスプロバイダーでもありテクノロジプロバイダーでもあります。また、多くの LSP に自社の翻訳プラットフォームへの参加を許可している独立したテクノロジプロバイダーも存在します。
   * The **AEM Translation Framework** supports integration with a variety of translation technology providers for both machine and human translation.
   * コンテンツの翻訳を自動化するための [AEM システムにおける LSP のコネクターの統合](/help/sites-administering/translation.md)方法、または LSP や翻訳テクノロジプロバイダーを採用しない場合やテスト用に翻訳プロジェクトの作成、書き出し、読み込みを手動でおこなう方法を確認します。

* Choose a **translation method** that best suits the content.

   * **人による翻訳** は、メッセージングや品質の期待が高く、コンテンツがサイト上でしばらくの間生きる、マーケティングページなどのコンテンツに最適です。
   * **機械翻訳は** 、公開に要する時間が非常に重要で、品質の期待が緩和される、または人による翻訳コストが非常に高い場合に、大量の翻訳に適した選択肢となります。サポートのナレッジベースとユーザー生成コンテンツは、一般に機械翻訳です。

* ローカリゼーションサービスプロバイダー、アドビのコンサルティング、システムインテグレーターの専門知識を活用して、多言語サイトの構造の計画、プロトタイプの作成およびテストを実施します。

