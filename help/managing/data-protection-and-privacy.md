---
title: データ保護およびデータプライバシーに関する規制 — Adobe Experience Manager対応
seo-title: データ保護およびデータプライバシーに関する規制に対するAdobe Experience Managerの対応GDPR、CCPAなど
description: '様々なデータ保護およびデータプライバシー規制に対するAdobe Experience Managerのサポートについて説明します。EU一般データ保護規則(GDPR)、カリフォルニア州消費者プライバシー法、新しいAEMプロジェクトを実装する際の準拠方法を含みます。 '
seo-description: '様々なデータ保護およびデータプライバシー規制に対するAdobe Experience Managerのサポートについて説明します。EU一般データ保護規則(GDPR)、カリフォルニア州消費者プライバシー法、新しいAEMプロジェクトを実装する際の準拠方法を含みます。 '
uuid: 9b0b8101-929c-4232-8c6e-1f9b8b2e0aa2
contentOwner: aheimoz
topic-tags: introduction, grdp
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
discoiquuid: 0bcd7ac4-3071-466d-bd11-701f35ccf5bd
docset: aem65
exl-id: 46c1ca14-78f6-4b33-9fdf-1b90a9875f66
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '981'
ht-degree: 23%

---

# Adobe Experience Managerでのデータ保護およびデータプライバシーに関する規制への対応{#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>このドキュメントの内容は法的な助言にはならず、その代用になるものでもありません。
>
>データ保護およびデータプライバシー規制に関するアドバイスについては、貴社の法務部門にお問い合わせください。

>[!NOTE]
>
>Adobeのプライバシーに関する問題への対応と、Adobeのお客様への影響について詳しくは、[Adobeのプライバシーセンター](https://www.adobe.com/privacy.html)を参照してください。

Adobeは、お客様のプライバシー管理者またはAEM管理者がデータ保護およびデータプライバシー要求を処理し、お客様がこれらの規制に準拠できるよう支援するために、ドキュメントと手順（APIが利用可能な場合）を提供しています。 ドキュメントに記載されている手順を使用すると、お客様は、手動で、または（利用可能な場合は）外部のポータルやサービスからAPIを呼び出すことで、規制リクエストを実行できます。

>[!CAUTION]
>
>ここで説明する詳細は、Adobe Experience Managerのみに制限されています。
>
>別のAdobeオンデマンドサービスのデータと、関連するプライバシーリクエストは、そのサービスで実行する必要があるアクションを必要とします。
>
>詳しくは、[Adobeのプライバシーセンター](https://www.adobe.com/privacy.html)を参照してください。

## はじめに {#introduction}

Adobe Experience Managerのインスタンスと、それらで実行されるアプリケーションは、アドビのお客様が所有および操作します。

その結果、GDPR、CCPAなどのデータ保護規制は、お客様の責任が大きくなります。

簡単な紹介として、データのプライバシーと保護に関する規制には、次の役割が適用される新しいルールが含まれます。

* ビジネスエンティティ(CCPA)やデータ管理者(GDPR)

* サービスプロバイダー(CCPA)およびデータプロセッサー(GDPR)

この規則の主な規定は次の通りである。

1. すべての一意のIDを含むように個人データの定義を拡張。を直接的および間接的に特定できるデータに含める場合と同様です。

2. 同意に関する要件を強化しました。

3. 削除権限（データ消去）に重点を置きます。

4. データの販売のオプトアウト。

Adobe Experience Managerの場合：

* インスタンスと、それらに対して実行されるアプリケーションは、顧客が所有および操作します。

   * これは、お客様が、ビジネス・エンティティやサービス・プロバイダ、データ管理者、データ処理者などの規制上の役割を効果的に管理することを意味します。

   * 次の図に示すように、Adobe Experience Platform Privacy ServiceはAEMのワークフローに含まれません。

* AEMには、お客様のプライバシー管理者やAEM管理者がプライバシー規制リクエストを実行するためのドキュメントと手順が含まれています。手動で、またはAPIを使用して（使用可能な場合）。

* 新しいサービスやUIが追加されていません。

   * 代わりに、プライバシー規制要求を処理する顧客UI/ポータルで使用する手順とAPIについて説明しています。

* AEMには、プライバシーリクエストワークフローをサポートする標準のツールは含まれません。

   * Adobeは、お客様のプライバシー管理者やAEM管理者向けのドキュメントや手順を提供し、プライバシー規制に関連するリクエストを手動で実行できるようにします。

Adobeは、Adobe Experience Managerのアクセス、削除およびオプトアウトに関するプライバシーリクエストを処理する手順を提供しています。 場合によっては、自動化に役立つように、顧客が開発したポータルまたはスクリプトから呼び出すことができるAPIが存在します。

次の図に、プライバシーリクエストワークフローがどのようになるかを示します(Adobe Experience Manager 6.5を使用した例)。

![データ保護とプライバシー](assets/data-protection-and-privacy-01.png)

## Adobe Experience Managerと規制対応{#aem-and-regulatory-readiness}

AEMの製品領域に関する規制ドキュメントについては、以下の節を参照してください。

## AEM の基盤 {#aem-foundation}

[AEM Foundationのデータ保護およびプライバシー要求の処理](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md)を参照してください。

## 集計した使用状況の統計の収集を AEM でオプトインする方法 {#aem-opting-into-aggregate-usage-statistics-collection}

[集計した使用状況の統計の収集](/help/sites-deploying/opt-in-aggregated-usage-statistics.md)を参照してください。

## AEM Sites {#aem-sites}

[AEM Sites — データ保護とプライバシー対応を参照してください。](/help/sites-administering/gdpr-compliance-sites.md)

## AEM Commerce {#aem-commerce}

[AEM Commerce - Data Protection and Privacy Readiness](/help/sites-administering/gdpr-compliance-commerce.md)を参照してください。

## AEM Mobile {#aem-mobile}

[AEM Mobile — データ保護とプライバシーの対応](/help/mobile/aem-mobile-gdpr-compliance.md)を参照してください。

## Adobe Target および Adobe Analytics との AEM 統合 {#aem-integration-with-adobe-target-adobe-analytics}

これらのAdobe Experience Manager統合は、データ保護およびプライバシー（GDPRやCCPAなど）に対応したサービスと組み合わせています。 Adobe TargetやAdobe Analyticsの個人データは、統合に関連してAEMに保存されません。
詳しくは、次のセクションを参照してください。

* [Adobe Target — プライバシーの概要](https://docs.adobe.com/content/help/en/target/using/implement-target/before-implement/privacy/privacy.html)

* [Adobe Analytics Data Privacy Workflow](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-workflow.html)

## AEM Communities {#aem-communities}

AEM Communities は[デフォルトの API](/help/communities/user-ugc-management-service.md) を通じて、データのポータビリティ権、アクセス権および削除権をデータ主体に提供します。これらの API を使用すれば、ユーザー生成コンテンツの一括削除や一括書き出し、および許可可能 ID で識別されたユーザーアカウントの無効化が可能となります。ただし、CRXDE Lite でユーザーノードを削除してユーザーアカウントを永続的に削除することもできるので、システムからの容易なオプトアウト、という要求に応えることができます。

さらに AEM Communities では、一括モデレーションコンソールを通じて「プライバシーバイデザイン」が実現されます。このコンソールでは、権限を持つメンバーがユーザーの貢献や詳細を検索および削除できます。メンバー管理コンソールを使用すれば、制限を設けてある貢献者の参加を禁止することさえできます。このコンソールではさらに、データ主体が自身の作成した貢献を削除することもできます。

## AEM Forms  {#aem-forms}

AEM Forms に含まれるコンポーネントやワークフローは、ビジネスプロセスの調整やデジタルトランザクションの実行のためにデータをキャプチャ、処理および格納します。コンポーネントごとに異なるデータストアが使用されますが、コンポーネントをカスタムデータストアと統合することも可能です。次のドキュメントでは、コンポーネントのデータ保護とプライバシー（GDPRやCCPAなど）ワークフローをサポートするためのユーザーデータへのアクセスと処理の手順とガイドラインを説明します。

* [フォームポータル](/help/forms/using/forms-portal-handling-user-data.md)
* [Correspondence Management](/help/forms/using/correspondence-management-handling-user-data.md)
* [Adobe Sign との統合](/help/forms/using/integration-adobe-sign-handling-user-data.md)
* [OSGi でのフォームに特化したワークフロー](/help/forms/using/forms-workflow-osgi-handling-user-data.md)
* [Forms JEE のワークフロー](/help/forms/using/forms-workflow-jee-handling-user-data.md)（AEM Forms JEE のみ）
* [Document Security](/help/forms/using/document-security-handling-user-data.md)（AEM Forms JEE のみ）
* [ユーザー管理](/help/forms/using/user-management-handling-user-data.md)（AEM Forms JEE のみ）
