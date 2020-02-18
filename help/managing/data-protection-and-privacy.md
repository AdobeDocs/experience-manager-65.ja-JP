---
title: データ保護とデータプライバシーに関する規制 — Adobe Experience Manager Readiness
seo-title: Adobe Experience Manager Readiness for Data Protection and Data Privacy Regulations;（GDPR、CCPAなど）
description: '様々なデータ保護およびデータプライバシー規制に対するAdobe Experience Managerのサポートについて説明します。eu General Data Protection Regulation(GDPR)、California Consumer Privacy Act、および新しいAEMプロジェクトを導入する際の準拠方法を含む。 '
seo-description: '様々なデータ保護およびデータプライバシー規制に対するAdobe Experience Managerのサポートについて説明します。eu General Data Protection Regulation(GDPR)、California Consumer Privacy Act、および新しいAEMプロジェクトを導入する際の準拠方法を含む。 '
uuid: 9b0b8101-929c-4232-8c6e-1f9b8b2e0aa2
contentOwner: aheimoz
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: grdp
discoiquuid: 0bcd7ac4-3071-466d-bd11-701f35ccf5bd
docset: aem65
translation-type: tm+mt
source-git-commit: 9b16c8ae2ee28c60f35f9e0f990d79173463c33b

---


# Adobe Experience Manager Readiness for Data Protection and Data Privacy Regulations {#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>本書の内容は、法律上の助言とはならず、法律上の助言の代替としての意味も持たない。
>
>データ保護およびデータプライバシー規制に関するアドバイスについては、貴社の法務部にお問い合わせください。

>[!NOTE]
>
>プライバシーに関する問題に対するアドビの対応、およびアドビのお客様にとっての意味について詳しくは、アドビのプライバシーセ [ンターを参照してください](https://www.adobe.com/privacy.html)。

アドビは、お客様のプライバシー管理者またはAEM管理者に対し、データ保護とデータプライバシーの要請を処理し、お客様がこれらの規制に準拠できるよう支援するため、ドキュメントと手順を提供しています。 ドキュメントに記載された手順により、顧客は手動で、または、可能な場合は外部のポータルやサービスからAPIに呼び出すことで、規制要求を実行できます。

>[!CAUTION]
>
>ここで説明する詳細は、Adobe Experience Managerに限定されています。
>
>別のアドビオンデマンドサービスのデータは、関連するプライバシーリクエストと共に、そのサービスに対して行う必要があります。
>
>詳しくは、アドビのプライバ [シーセンターを参照してください](https://www.adobe.com/privacy.html)。

## 概要 {#introduction}

Adobe Experience Managerのインスタンスとそれらで実行されるアプリケーションは、アドビのお客様が所有し、運用します。

その結果、GDPR、CCPAなどのデータ保護に関する規制は、お客様の責任が大きく左右されます。

簡単に説明すると、データのプライバシーと保護に関する規制には、次の役割を果たす新しいルールが含まれます。

* CCPA（ビジネス・エンティティ）およびGDPR（データ・コントローラ）

* CCPA（サービス・プロバイダ）およびGDPR（データ・プロセッサ）

この規則の主な規定は次の通りである。

1. 個人データの定義を拡張し、すべての一意のIDを含める。を直接または間接的に識別可能なデータに含める場合と同様です。

2. 同意要件の強化。

3. 削除権限（データ消去）に重点を置くようになりました。

4. データ販売のオプトアウトを参照してください。

Adobe Experience Managerの場合：

* インスタンスとそれら上で実行されるアプリケーションは、顧客が所有し、操作します。

   * つまり、ビジネス・エンティティやサービス・プロバイダ、データ・コントローラ、データ・プロセッサなど、規制上の役割を顧客が効果的に管理できます。

   * 次の図に示すように、Adobe Experience PlatformプライバシーサービスはAEMのワークフローには含まれません。

* AEMには、お客様のプライバシー管理者やAEM管理者がプライバシー規制の要請を実行するためのドキュメントと手順が含まれています。手動で、またはAPIを使用して（可能な場合）。

* 新しいサービスまたはUIが追加されていません。

   * 代わりに、プライバシー規制の要求を処理する顧客UI/ポータルで使用するための手順とAPIについて説明します。

* AEMには、プライバシーリクエストのワークフローをサポートする追加設定なしのツールは含まれません。

   * アドビは、お客様のプライバシー管理者やAEM管理者に対して、プライバシー規制に関連する要求を手動で実行できるようにドキュメントと手順を提供します。

アドビは、Adobe Experience Managerのアクセス、削除およびオプトアウトに関するプライバシーリクエストを処理する手順を提供しています。 場合によっては、自動化を支援するために、顧客が開発したポータルまたはスクリプトから呼び出すことのできるAPIが存在します。

次の図に、プライバシーリクエストのワークフローがどのようになるかを示します（Adobe Experience Manager 6.5を使用して図を示します）。

![データ保護とプライバシー](assets/data-protection-and-privacy-01.png)

## Adobe Experience ManagerとRegulatory Readiness {#aem-and-regulatory-readiness}

AEMの製品領域に関する規制に関するドキュメントについては、以下の節を参照してください。

## AEM の基盤 {#aem-foundation}

「AEM Foundation [のデータ保護およびプライバシー要求の処理」を参照してください](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md)。

## 集計した使用状況の統計の収集を AEM でオプトインする方法 {#aem-opting-into-aggregate-usage-statistics-collection}

[集計した使用状況の統計の収集](/help/sites-deploying/opt-in-aggregated-usage-statistics.md)を参照してください。

## AEM Sites {#aem-sites}

詳しくは、 [AEMサイト — データ保護とプライバシーの準備を参照してください。](/help/sites-administering/gdpr-compliance-sites.md)

## AEM Commerce {#aem-commerce}

「 [AEMコマース — データ保護とプライバシーの準備」を参照してください](/help/sites-administering/gdpr-compliance-commerce.md)。

## AEM Mobile {#aem-mobile}

AEM Mobile - Data Protection and Privacy Readinessを参照してください [](/help/mobile/aem-mobile-gdpr-compliance.md)。

## Adobe Target および Adobe Analytics との AEM 統合 {#aem-integration-with-adobe-target-adobe-analytics}

これらのAdobe Experience Manager統合は、データ保護とプライバシー（GDPRやCCPAなど）対応のサービスと連携しています。 Adobe targetまたはAdobe Analyticsの個人データは、統合に関連してAEMに保存されません。
詳しくは、次のセクションを参照してください。

* [Adobe Target — プライバシーの概要](https://docs.adobe.com/content/help/en/target/using/implement-target/before-implement/privacy/privacy.html)

* [Adobe Analyticsデータプライバシーワークフロー](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-workflow.html)

## AEM Communities {#aem-communities}

AEM Communities は[デフォルトの API](/help/communities/user-ugc-management-service.md) を通じて、データのポータビリティ権、アクセス権および削除権をデータ主体に提供します。これらの API を使用すれば、ユーザー生成コンテンツの一括削除や一括書き出し、および許可可能 ID で識別されたユーザーアカウントの無効化が可能となります。ただし、CRXDE Lite でユーザーノードを削除してユーザーアカウントを永続的に削除することもできるので、システムからの容易なオプトアウト、という要求に応えることができます。

さらに AEM Communities では、一括モデレーションコンソールを通じて「プライバシーバイデザイン」が実現されます。このコンソールでは、権限を持つメンバーがユーザーの貢献や詳細を検索および削除できます。メンバー管理コンソールを使用すれば、制限を設けてある貢献者の参加を禁止することさえできます。このコンソールではさらに、データ主体が自身の作成した貢献を削除することもできます。

## AEM Forms {#aem-forms}

AEM Forms に含まれるコンポーネントやワークフローは、ビジネスプロセスの調整やデジタルトランザクションの実行のためにデータをキャプチャ、処理および格納します。コンポーネントごとに異なるデータストアが使用されますが、コンポーネントをカスタムデータストアと統合することも可能です。以下のドキュメントでは、コンポーネントのデータ保護とプライバシー（GDPRやCCPAなど）ワークフローをサポートするためにユーザーデータにアクセスし、処理する手順とガイドラインを説明しています。

* [フォームポータル](/help/forms/using/forms-portal-handling-user-data.md)
* [Correspondence Management](/help/forms/using/correspondence-management-handling-user-data.md)
* [Adobe Sign との統合](/help/forms/using/integration-adobe-sign-handling-user-data.md)
* [OSGi でのフォームに特化したワークフロー](/help/forms/using/forms-workflow-osgi-handling-user-data.md)
* [Forms JEE のワークフロー](/help/forms/using/forms-workflow-jee-handling-user-data.md)（AEM Forms JEE のみ）
* [Document Security](/help/forms/using/document-security-handling-user-data.md)（AEM Forms JEE のみ）
* [ユーザー管理](/help/forms/using/user-management-handling-user-data.md)（AEM Forms JEE のみ）
