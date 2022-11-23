---
title: データ保護とデータプライバシーに関する規制 - Adobe Experience Manager の対応
seo-title: Adobe Experience Manager Readiness for Data Protection and Data Privacy Regulations; such as GDPR, CCPA, etc
description: 様々なデータ保護およびデータプライバシー規則に対する Adobe Experience Manager のサポートについて説明します。これには、EU 一般データ保護規則（GDPR）、カリフォルニア州消費者プライバシー法および新規 AEM プロジェクトを実装する際に準拠する方法が含まれます。
seo-description: Learn about Adobe Experience Manager support for the various Data Protection and Data Privacy Regulations; including the EU General Data Protection Regulation (GDPR), the California Consumer Privacy Act and how to comply when implementing a new AEM project.
uuid: 9b0b8101-929c-4232-8c6e-1f9b8b2e0aa2
contentOwner: AEM Docs
topic-tags: introduction, grdp
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
discoiquuid: 0bcd7ac4-3071-466d-bd11-701f35ccf5bd
docset: aem65
exl-id: 46c1ca14-78f6-4b33-9fdf-1b90a9875f66
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: ht
source-wordcount: '923'
ht-degree: 100%

---

# データ保護およびデータプライバシーに関する規制に対する Adobe Experience Manager の対応 {#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>このドキュメントの内容は法的な助言にはならず、その代用になるものでもありません。
>
>データ保護およびデータプライバシー規制に関するアドバイスについては、自社の法務部門にお問い合わせください。

>[!NOTE]
>
>アドビのプライバシーに関する問題への対応と、アドビのお客様への影響について詳しくは、[アドビのプライバシーセンター](https://www.adobe.com/jp/privacy.html)をご覧ください。

アドビは、お客様のプライバシー管理者または AEM 管理者がデータ保護およびデータプライバシーリクエストを処理するためのドキュメントおよび手順（利用可能な場合は API も）を提供しており、お客様がこれらの規則に準拠できるように支援をしています。ドキュメントに記載された手順を参照すれば、外部のポータルやサービスから手動で、または API が利用可能な場合は API を呼び出して、規制のリクエストを実行することができます。

>[!CAUTION]
>
>ここで説明する詳細は、Adobe Experience Manager に限定されます。
>
>別のアドビオンデマンドサービスからのデータは、関連するプライバシー要求とともに、そのサービスでの対応が必要となります。
>
>詳しくは、[アドビのプライバシーセンター](https://www.adobe.com/jp/privacy.html)を参照してください。

## はじめに {#introduction}

Adobe Experience Manager のインスタンスと、それらで実行されるアプリケーションは、Adobe のお客様によって所有され、運用されています。

その結果、GDPR、CCPA などのデータ保護規制は、主に顧客の責任となります。

簡単に紹介すると、データのプライバシーと保護に関する規制には、次の役割を担う者が従うべき新しいルールが含まれます。

* 事業体（CCPA）および／またはデータ管理者（GDPR）

* サービスプロバイダー（CCPA）および／またはデータ処理者（GDPR）

このような規則の主な条項は次の通りです。

1. 個人データの定義を拡大してすべての固有の ID を含むようにし、直接および間接的に識別可能なデータとする。

2. 同意に関する要件の強化。

3. 削除権（データ消去）への重点的な取り組み。

4. データの販売のオプトアウト。

Adobe Experience Manager の場合：

* インスタンスと、それらに対して実行されるアプリケーションは、顧客が所有および運用します。

   * これは、顧客が、事業体やサービスプロバイダー、データ管理者、データ処理者などの規制上の役割を効果的に管理することを意味します。

   * 次の図に示すように、Adobe Experience Platform Privacy Service は AEM のワークフローには含まれていません。

* AEM には、顧客のプライバシー管理者や AEM 管理者が、手動または API を使用して（使用可能な場合）、プライバシー規制のリクエストを実行するためのドキュメントと手順が含まれています。

* 新しいサービスや UI は追加されていません。

   * 代わりに、プライバシー規制のリクエストを処理する顧客 UI／ポータルで使用する手順と API が文書化されています。

* AEM には、プライバシーリクエストワークフローをサポートする標準のツールは含まれません。

   * アドビは、顧客のプライバシー管理者や AEM 管理者向けのドキュメントや手順を提供し、プライバシー規制に関連するリクエストを手動で実行できるようにします。

Adobe は、Adobe Experience Manager のアクセス、削除、オプトアウトに関するプライバシーリクエストを処理する手順を提供しています。場合によっては、自動化に役立つように、顧客が開発したポータルまたはスクリプトから呼び出すことができる API が存在します。

次の図に、プライバシーリクエストワークフローを示します（Adobe Experience Manager 6.5 を使用した例）。

![データ保護とプライバシー](assets/data-protection-and-privacy-01.png)

## Adobe Experience Manager と規制への対応 {#aem-and-regulatory-readiness}

AEM の製品範囲に関する規制ドキュメントについては、以下の節を参照してください。

## AEM の基盤 {#aem-foundation}

[AEM 基盤のデータ保護およびプライバシーリクエストの処理](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md)を参照してください。

## 集計した使用状況の統計の収集を AEM でオプトインする方法 {#aem-opting-into-aggregate-usage-statistics-collection}

[集計した使用状況の統計の収集](/help/sites-deploying/opt-in-aggregated-usage-statistics.md)を参照してください。

## AEM Sites {#aem-sites}

[AEM Sites - データ保護とプライバシー対応](/help/sites-administering/gdpr-compliance-sites.md)を参照してください。

## AEM Commerce {#aem-commerce}

[AEM Commerce - データ保護とプライバシー対応](/help/sites-administering/gdpr-compliance-commerce.md)を参照してください。

## AEM Mobile {#aem-mobile}

[AEM Mobile - データ保護とプライバシー対応](/help/mobile/aem-mobile-gdpr-compliance.md)を参照してください。

## Adobe Target および Adobe Analytics との AEM 統合 {#aem-integration-with-adobe-target-adobe-analytics}

これらの Adobe Experience Manager 統合は、データ保護およびプライバシー（GDPR や CCPA など）に対応したサービスと共に行われます。Adobe Target や Adobe Analytics の個人データは、統合に関連して AEM に保存されません。
詳しくは、次のセクションを参照してください。

* [Adobe Target - プライバシーの概要](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/privacy.html?lang=ja)

* [Adobe Analytics データプライバシーのワークフロー](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/an-gdpr-workflow.html?lang=ja)

## AEM Communities {#aem-communities}

AEM Communities は[デフォルトの API](/help/communities/user-ugc-management-service.md) を通じて、データのポータビリティ権、アクセス権および削除権をデータ主体に提供します。これらの API を使用すれば、ユーザー生成コンテンツの一括削除や一括書き出し、および許可可能 ID で識別されたユーザーアカウントの無効化が可能となります。ただし、CRXDE Lite でユーザーノードを削除してユーザーアカウントを永続的に削除することもできるので、システムからの容易なオプトアウト、という要求に応えることができます。

さらに AEM Communities では、一括モデレーションコンソールを通じて「プライバシーバイデザイン」が実現されます。このコンソールでは、権限を持つメンバーがユーザーの貢献や詳細を検索および削除できます。メンバー管理コンソールを使用すれば、制限を設けてある貢献者の参加を禁止することさえできます。このコンソールではさらに、データ主体が自身の作成した貢献を削除することもできます。

## AEM Forms {#aem-forms}

AEM Forms に含まれるコンポーネントやワークフローは、ビジネスプロセスの調整やデジタルトランザクションの実行のためにデータをキャプチャ、処理および格納します。コンポーネントごとに異なるデータストアが使用されますが、コンポーネントをカスタムデータストアと統合することも可能です。次のドキュメントでは、コンポーネントのデータ保護およびプライバシー（GDPR や CCPA など）ワークフローをサポートするためのユーザーデータへのアクセスと処理に関する手順とガイドラインを説明します。

* [フォームポータル](/help/forms/using/forms-portal-handling-user-data.md)
* [Correspondence Management](/help/forms/using/correspondence-management-handling-user-data.md)
* [Adobe Sign との統合](/help/forms/using/integration-adobe-sign-handling-user-data.md)
* [OSGi でのフォームに特化したワークフロー](/help/forms/using/forms-workflow-osgi-handling-user-data.md)
* [Forms JEE のワークフロー](/help/forms/using/forms-workflow-jee-handling-user-data.md)（AEM Forms JEE のみ）
* [Document Security](/help/forms/using/document-security-handling-user-data.md)（AEM Forms JEE のみ）
* [ユーザー管理](/help/forms/using/user-management-handling-user-data.md)（AEM Forms JEE のみ）
