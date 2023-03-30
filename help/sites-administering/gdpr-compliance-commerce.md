---
title: AEM Commerce - GDPR 対応
seo-title: AEM Commerce - GDPR Readiness
description: "AEM Commerce - GDPR 対応"
seo-description: null
uuid: 7ca26587-8cce-4c75-8629-e0e5cfb8166c
contentOwner: carlino
discoiquuid: c637964a-dfcb-41fe-9c92-934620fe2cb3
exl-id: 3a483b9d-627a-41d3-8ac1-66f9c5e89ad5
source-git-commit: 71842228dd3cb1ce3b79728912e8333d25fccefc
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 15%

---

# AEM Commerce - GDPR 対応{#aem-commerce-gdpr-readiness}

>[!IMPORTANT]
>
>以下の節では GDPR を例として使用していますが、詳細はすべてのデータ保護およびプライバシー規制に適用できます。（GDPR や CCPA など）

データのプライバシー権に関する EU 一般データ保護規則（GDPR）が 2018 年 5 月に発効します。詳しくは、 [GDPR ページ (Adobeプライバシーセンター )](https://business.adobe.com/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>詳しくは、 [AEM GDPR 対応](/help/managing/data-protection-and-privacy.md) 詳しくは、を参照してください。

![screen_shot_2018-03-22at111606](assets/screen_shot_2018-03-22at111606.jpg)

Adobeの標準のコマース統合では、AEMがエクスペリエンスレイヤーとなり、サービスを消費し、ヘッドレスモードで実行される顧客コマースプラットフォームにデータを送り返します。

一部のコマースプラットフォームでは、Adobeはプロファイル情報 ( `/home/users`) およびコマーストークン（コマースプラットフォームにログオンするため）をAEMで設定します。 これらの使用例については、 [AEM Platform に対する GDPR 要求の処理](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md).

![screen_shot_2018-03-22at111621](assets/screen_shot_2018-03-22at111621.jpg)

## AEM Commerce での GDPR 要求の処理 {#handling-gdpr-requests-for-aem-commerce}

SalesforceCommerce Cloud統合の場合、AEM Commerce は GDPR 関連の情報を格納しません。 リクエストを [Salesforce Cloud](https://documentation.b2c.commercecloud.salesforce.com/DOC1/index.jsp).

hybris と HCL WebSphere® Commerce の統合の場合、AEMにはいくつかのデータがあります。 以下を使用： [AEM Platform GDPR の手順](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md) そして、次の質問を考慮します。

1. **データはどこに保存/使用されますか？** AEMから表示される名前、コマースユーザー識別子、トークン、パスワード、住所データなど、キャッシュされたユーザープロファイル情報。
1. **対象となる GDPR データを誰と共有すればよいですか？** AEM Commerce での GDPR 関連データの更新は（前述の関連するプロファイル情報を除く）保存されず、コマースプラットフォームにプロキシされて返されます。
1. **ユーザーデータの削除方法は？** AEMのユーザープロファイルを削除し、コマースプラットフォームでユーザーの削除を呼び出します。

>[!NOTE]
>
>以下をご覧ください： [hybris wiky](https://wiki.hybris.com/) または [HCL WebSphere® Commerce ドキュメント](https://help.hcltechsw.com/commerce/index.html)（必要に応じて）
