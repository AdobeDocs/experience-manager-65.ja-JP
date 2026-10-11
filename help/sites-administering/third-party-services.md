---
title: サードパーティのサービスとの統合
description: AEM をサードパーティのサービスと統合する方法について説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: 50b70e47-a801-4f0a-be92-4427c4b2cad1
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: 243139ec-8e41-5296-a287-31343ab1bc0f
    internal-label: Integration
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 100%
---
# サードパーティのサービスとの統合{#integrating-with-third-party-services}

AEM は標準で、アドビ製品以外の次の製品と統合できます。

* Amazon SNS 接続 - Amazon Web Services
* BrightEdge Content Optimizer - 検索用に最適化されたコンテンツ
* ExactTarget - メールマーケティング
* Facebook Connect - ソーシャルネットワーキング
* 一般的な分析スニペット - 分析
* Microsoft® Translator またはその他の機械翻訳プロバイダー
* Pushwoosh 接続 - アプリ - プッシュ通知
* Salesforce - 販売および CRM ソフトウェア
* Twitter - ソーシャルネットワーキング
* YouTube - ビデオ共有
<!-- * Silverpop Engage - marketing automation, email, mobile, and social NO LONGER EXISTS; ITS REPLACEMENT IS UNKNOWN -->

また、AEM を [Adobe Creative Cloud](/help/assets/aem-cc-integration-best-practices.md) と統合できます。

## Salesforce との統合 {#integrating-with-salesforce}

Salesforce.com は企業向けのクラウドコンピューティングを提供し、ソーシャルエンタープライズへの移行を支援します。

AEM サイトと Salesforce の統合については、[Salesforce との統合](/help/sites-administering/salesforce.md)を参照してください。

<!--
THE INFORMATION BELOW APPEARS OBSOLETE; first URL is a 404. I could not find a suitable replacement for it.
## Integrating with Silverpop Engage {#integrating-with-silverpop-engage}

>[!NOTE]
>
>Silverpop Engage integration is not available out of the box. To integrate AEM with Silverpop Engage, [download the package](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/aem620/product/cq-mcm-integrations-silverpop-content) from Package Share.

Silverpop Engage provides marketing automation, email, mobile, and social.

For information about integrating your AEM site and ExactTarget, see [Integrating with Silverpop Engage](/help/sites-administering/silverpop.md).
-->

## ExactTarget との統合 {#integrating-with-exacttarget}

ExactTarget のメールマーケティングソリューションを使用すると、あらゆる規模の組織において、ターゲットを厳選し、ミッションクリティカルな完全統合型のメールキャンペーンを企画して実施できます。

AEM サイトと ExactTarget の統合については、[ExactTarget との統合](/help/sites-administering/exacttarget.md)を参照してください。

## Facebook および Twitter との統合 {#integrating-with-facebook-and-twitter}

Facebook および Twitter は広く普及しているソーシャルネットワーキングサービスです。 AEM と Facebook および Twitter の統合によって、組織が所有しているデジタル資産に Facebook または Twitter のログインオプションを付けて、プロファイル情報に基づいてユーザーエクスペリエンスをパーソナライズすることができます。 マーケターは、プロファイル情報を他のソースのデータ（顧客関係管理システムや web サイトのプロファイルなど）と組み合わせて、統一されたユーザービューを作成することもできます。

詳しくは、[ソーシャルログイン](/help/communities/social-login.md)を参照してください。

## その他のプロバイダーとの統合 {#integrating-with-other-providers}

AEM では、[一般的な分析スニペット](/help/sites-administering/external-providers.md)を使用して、その他の外部プロバイダーに接続できます。
