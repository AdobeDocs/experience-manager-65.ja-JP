---
title: データ保護とデータプライバシーに関する規制 - Adobe Experience Manager の対応
description: 様々なデータ保護およびデータプライバシー規制に対するAdobe Experience Managerのサポートについて説明します。 これには、EU 一般データ保護規則 (GDPR)、カリフォルニア州消費者プライバシー法および新しいAEMプロジェクトを実装する際の準拠方法が含まれます。
uuid: 9b0b8101-929c-4232-8c6e-1f9b8b2e0aa2
contentOwner: AEM Docs
topic-tags: introduction, grdp
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
discoiquuid: 0bcd7ac4-3071-466d-bd11-701f35ccf5bd
docset: aem65
exl-id: 46c1ca14-78f6-4b33-9fdf-1b90a9875f66
source-git-commit: d8ae63edd71c7d27fe93d24b30fb00a29332658d
workflow-type: tm+mt
source-wordcount: '907'
ht-degree: 41%

---

# データ保護およびデータプライバシーに関する規制に対する Adobe Experience Manager の対応 {#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>このドキュメントの内容は法的な助言にはならず、その代用になるものでもありません。
>
>データ保護およびデータプライバシー規制に関するアドバイスについては、お客様の企業の法務部門にお問い合わせください。

>[!NOTE]
>
>プライバシーに関する問題に対するAdobeの対応と、プライバシーをご利用のお客様にとっての意味について詳しくは、 [Adobeプライバシーセンター](https://www.adobe.com/jp/privacy.html).

Adobeは、お客様のプライバシー管理者またはAEM管理者がデータ保護およびデータプライバシー要求を処理するためのドキュメントと手順（API が使用可能な場合）を提供しています。 これは、これらの規制に準拠するのに役立ちます。 手順を説明しているので、お客様は手動で規制リクエストを実行するか、可能な場合は外部のポータルやサービスから API を呼び出すことで規制リクエストを実行できます。

>[!CAUTION]
>
>ここで説明する詳細は、Adobe Experience Manager に限定されます。
>
>別のAdobeオンデマンドサービスのデータと関連するプライバシーリクエストでは、そのサービスに対して行うアクションが必要です。
>
>詳しくは、 [Adobeプライバシーセンター](https://www.adobe.com/jp/privacy.html).

## はじめに {#introduction}

Adobe Experience Managerのインスタンスと、それらで実行されるアプリケーションは、Adobeの顧客が所有および操作します。

その結果、GDPR、CCPA などのデータ保護規制は、主に顧客の責任となります。

簡単な紹介として、データのプライバシーと保護に関する規制には、次の役割を持つ新しいルールが含まれます。

* 事業体（CCPA）および／またはデータ管理者（GDPR）

* サービスプロバイダー（CCPA）および／またはデータ処理者（GDPR）

このような規則の主な条項は次の通りです。

1. 個人データの定義を拡大してすべての固有の ID を含むようにし、直接および間接的に識別可能なデータとする。

2. 同意に関する要件の強化。

3. 削除権（データ消去）への重点的な取り組み。

4. データの販売のオプトアウト。

Adobe Experience Manager の場合：

* インスタンスと、それらに対して実行されるアプリケーションは、顧客が所有および運用します。

   * お客様は、ビジネスエンティティおよびサービスプロバイダ、データ管理者、データ処理者など、規制上の役割を管理します。

   * 次の図に示すように、Adobe Experience Platform Privacy ServiceはAEMのワークフローに含まれていません。

* AEM には、顧客のプライバシー管理者や AEM 管理者が、手動または API を使用して（使用可能な場合）、プライバシー規制のリクエストを実行するためのドキュメントと手順が含まれています。

* 新しいサービスや UI は追加されていません。

   * 代わりに、プライバシー規制のリクエストを処理する顧客 UI／ポータルで使用する手順と API が文書化されています。

* AEMには、プライバシーリクエストワークフローをサポートするための既製のツールは含まれていません。

   * Adobeは、お客様のプライバシー管理者とAEM管理者に関するドキュメントと手順を提供し、プライバシー規制に関連するリクエストを手動で実行できます。

Adobeは、Adobe Experience Managerのアクセス、削除およびオプトアウトに関連するプライバシーリクエストを処理する手順を提供しています。 お客様が開発したポータルやスクリプトから呼び出して、自動化に役立つ API を利用できる場合があります。

次の図に、プライバシーリクエストワークフローを示します（Adobe Experience Manager 6.5 を使用した例）。

![データ保護とプライバシー](assets/data-protection-and-privacy-01.png)

## Adobe Experience Manager と規制への対応 {#aem-and-regulatory-readiness}

AEMの製品領域については、以下の規制に関するドキュメントの節を参照してください。

## AEM の基盤 {#aem-foundation}

[AEM 基盤のデータ保護およびプライバシーリクエストの処理](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md)を参照してください。

## AEM Opting Into Aggregate Usage Statistics Collection {#aem-opting-into-aggregate-usage-statistics-collection}

詳しくは、 [集計された使用状況の統計の収集](/help/sites-deploying/opt-in-aggregated-usage-statistics.md).

## AEM Sites {#aem-sites}

[AEM Sites - データ保護とプライバシー対応](/help/sites-administering/gdpr-compliance-sites.md)を参照してください。

## AEM Commerce {#aem-commerce}

[AEM Commerce - データ保護とプライバシー対応](/help/sites-administering/gdpr-compliance-commerce.md)を参照してください。

## AEM Mobile {#aem-mobile}

[AEM Mobile - データ保護とプライバシー対応](/help/mobile/aem-mobile-gdpr-compliance.md)を参照してください。

## Adobe Target および Adobe Analytics との AEM 統合 {#aem-integration-with-adobe-target-adobe-analytics}

これらの Adobe Experience Manager 統合は、データ保護およびプライバシー（GDPR や CCPA など）に対応したサービスと共に行われます。Adobe Target や Adobe Analytics の個人データは、統合に関連して AEM に保存されません。


詳しくは、以下のトピックを参照してください。

* [Adobe Target - プライバシーの概要](https://developer.adobe.com/target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation/?lang=en)

* [Adobe Analytics データプライバシーのワークフロー](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/data-governance/an-gdpr-workflow.html)

## AEM Communities {#aem-communities}

AEM Communitiesは、データの移植性、アクセス権、忘れられる権利をデータ主体に提供します [標準搭載の API](/help/communities/user-ugc-management-service.md). これらの API を使用すると、ユーザー生成コンテンツの一括削除および一括書き出しが可能になり、許可可能 ID を使用して識別されたユーザーアカウントが無効になります。 ただし、CRXDE Lite内のユーザーノードを削除することで、ユーザーアカウントの恒久的な削除を実現でき、システムから簡単なオプトアウトの必要性に対処します。

また、AEM Communitiesは一括モデレートコンソールを使用して設計に基づいてプライバシーを提供し、権限を持つメンバーがユーザーの投稿と詳細を検索および削除できるようにします。 メンバー管理コンソールを使用すると、投稿者を禁止するポイントに制限できます。 さらに、データ主体に対し、データ主体が作成した投稿の削除を許可します。

## AEM Forms {#aem-forms}

AEM Formsには、ビジネスプロセスを調整し、デジタルトランザクションを完了させるために、データをキャプチャ、処理、保存するコンポーネントとワークフローが含まれています。 コンポーネントが異なれば、使用するデータストアも異なり、カスタムデータストアとの統合も可能です。 次のドキュメントでは、コンポーネントのデータ保護およびプライバシー（GDPR や CCPA など）ワークフローをサポートするためのユーザーデータへのアクセスと処理に関する手順とガイドラインを説明します。

* [フォームポータル](/help/forms/using/forms-portal-handling-user-data.md)
* [Correspondence Management](/help/forms/using/correspondence-management-handling-user-data.md)
* [Adobe Sign との統合](/help/forms/using/integration-adobe-sign-handling-user-data.md)
* [OSGi でのフォームに特化したワークフロー](/help/forms/using/forms-workflow-osgi-handling-user-data.md)
* [Forms JEE ワークフロー](/help/forms/using/forms-workflow-jee-handling-user-data.md) (AEM Forms JEE のみ )
* [Document Security](/help/forms/using/document-security-handling-user-data.md) (AEM Forms JEE のみ )
* [ユーザー管理](/help/forms/using/user-management-handling-user-data.md) (AEM Forms JEE のみ )
