---
title: データ保護とデータプライバシーに関する規制 - Adobe Experience Manager の対応
description: 様々なデータ保護およびデータプライバシー規制に対する Adobe Experience Manager のサポートについて説明します。これには、EU 一般データ保護規則（GDPR）、カリフォルニア州消費者プライバシー法および新しい AEM プロジェクトを実装する際の準拠方法が含まれます。
contentOwner: AEM Docs
topic-tags: introduction, grdp
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
docset: aem65
exl-id: 46c1ca14-78f6-4b33-9fdf-1b90a9875f66
solution: Experience Manager, Experience Manager 6.5
feature: Compliance
role: Developer,Leader,Architect,Data Architect,User
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '890'
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

アドビは、お客様のプライバシー管理者または AEM 管理者がデータ保護およびデータプライバシーリクエストを処理するためのドキュメントとプロシージャ（使用可能な場合 API を使用）を提供しています。これは、これらの規制に準拠するのに役立ちます。ドキュメントに記載されたプロシージャを参照すれば、外部のポータルやサービスから、または API が利用可能な場合は API を呼び出して、規制のリクエストを手動で実行することができます。

>[!CAUTION]
>
>ここで説明する詳細は、Adobe Experience Manager に限定されます。
>
>別のアドビオンデマンドサービスからのデータは、関連するプライバシーリクエストとともに、そのサービスに対するアクションが必要となります。
>
>詳しくは、[アドビのプライバシーセンター](https://www.adobe.com/jp/privacy.html)を参照してください。

## はじめに {#introduction}

Adobe Experience Manager のインスタンスと、それらで実行されるアプリケーションは、アドビのお客様によって所有、運用されています。

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

   * 顧客が、事業体やサービスプロバイダー、データ管理者、データ処理者などの規制上の役割を効果的に管理します。

   * 次の図に示すように、Adobe Experience Platform Privacy Service は AEM のワークフローの一部ではありません。

* AEM には、顧客のプライバシー管理者や AEM 管理者が、手動または API を使用して（使用可能な場合）、プライバシー規制のリクエストを実行するためのドキュメントと手順が含まれています。

* 新しいサービスや UI は追加されていません。

   * 代わりに、プライバシー規制のリクエストを処理する顧客 UI／ポータルで使用する手順と API が文書化されています。

* AEM には、プライバシーリクエストワークフローをサポートする標準のツールは含まれません。

   * アドビは、顧客のプライバシー管理者や AEM 管理者向けのドキュメントやプロシージャを提供し、プライバシー規制に関連するリクエストを手動で実行できるようにします。

アドビは、Adobe Experience Manager のアクセス、削除、オプトアウトに関するプライバシーリクエストを処理するプロシージャを提供しています。場合によっては、自動化に役立つように、顧客が開発したポータルまたはスクリプトから呼び出すことができる API を使用できます。

次の図に、プライバシーリクエストワークフローを示します（Adobe Experience Manager 6.5 を使用した例）。

![データ保護とプライバシー](assets/data-protection-and-privacy-01.png)

## Adobe Experience Manager と規制への対応 {#aem-and-regulatory-readiness}

AEM の製品範囲に関する規制ドキュメントについては、以下の節を参照してください。

## AEM の基盤 {#aem-foundation}

[AEM 基盤のデータ保護およびプライバシーリクエストの処理](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md)を参照してください。

## 集計した使用状況の統計の収集を AEM でオプトインする方法 {#aem-opting-into-aggregate-usage-statistics-collection}

詳しくは、[集計された使用状況の統計の収集](/help/sites-deploying/opt-in-aggregated-usage-statistics.md)を参照してください。

## AEM Sites {#aem-sites}

[AEM Sites - データ保護とプライバシー対応](/help/sites-administering/gdpr-compliance-sites.md)を参照してください。

## AEM Commerce {#aem-commerce}

[AEM Commerce - データ保護とプライバシー対応](/help/sites-administering/gdpr-compliance-commerce.md)を参照してください。

## AEM Mobile {#aem-mobile}

[AEM Mobile - データ保護とプライバシー対応](/help/mobile/aem-mobile-gdpr-compliance.md)を参照してください。

## Adobe Target および Adobe Analytics との AEM 統合 {#aem-integration-with-adobe-target-adobe-analytics}

これらの Adobe Experience Manager 統合は、データ保護およびプライバシー（GDPR や CCPA など）に対応したサービスと共に行われます。Adobe Target や Adobe Analytics の個人データは、統合に関連して AEM に保存されません。

詳しくは、以下のトピックを参照してください。

* [Adobe Target - プライバシーの概要](https://developer.adobe.com/target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation/?lang=ja)

* [Adobe Analytics データプライバシーのワークフロー](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/data-governance/an-gdpr-workflow.html?lang=ja)

## AEM Communities {#aem-communities}

AEM Communities は、[標準搭載の API](/help/communities/user-ugc-management-service.md) で、データの移植性、アクセス権、忘れられる権利をデータ主体に提供します。これらの API を使用すると、ユーザー作成コンテンツの一括削除および一括書き出しが可能になり、認証可能な ID によって識別されたユーザーアカウントが無効になります。ただし、CRXDE Lite 内のユーザーノードを削除することで、ユーザーアカウントの永久的な削除を実現し、システムから簡単なオプトアウトの必要性に対処します。

また、AEM Communities は一括モデレートコンソールを使用して設計に基づいてプライバシーを提供し、権限を持つメンバーがユーザーの投稿や詳細を検索および削除できるようにします。メンバー管理コンソールを使用すると、投稿者を禁止するまでの制限を実行できます。さらに、データ主体に対し、データ主体が作成した投稿の削除を許可します。

## AEM Forms {#aem-forms}

AEM Forms には、ビジネスプロセスを調整し、デジタルトランザクションを完了させるために、データをキャプチャ、処理、保存するコンポーネントとワークフローが含まれています。コンポーネントによって使用するデータストアは異なり、カスタムデータストアとの統合も可能です。次のドキュメントでは、コンポーネントのデータ保護およびプライバシー（GDPR や CCPA など）ワークフローをサポートするためのユーザーデータへのアクセスと処理に関する手順とガイドラインを説明します。

* [フォームポータル](/help/forms/using/forms-portal-handling-user-data.md)
* [Correspondence Management](/help/forms/using/correspondence-management-handling-user-data.md)
* [Adobe Sign との統合](/help/forms/using/integration-adobe-sign-handling-user-data.md)
* [OSGi でのフォームに特化したワークフロー](/help/forms/using/forms-workflow-osgi-handling-user-data.md)
* [Forms JEE ワークフロー](/help/forms/using/forms-workflow-jee-handling-user-data.md)（AEM Forms JEE のみ）
* [ドキュメントセキュリティ](/help/forms/using/document-security-handling-user-data.md)（AEM Forms JEE のみ）
* [ユーザー管理](/help/forms/using/user-management-handling-user-data.md)（AEM Forms JEE のみ）
