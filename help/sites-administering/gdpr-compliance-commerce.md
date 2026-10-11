---
title: AEM Commerce - GDPR 対応
description: AEM Commerce で GDPR リクエストを処理する手順とその使用方法について説明します。
contentOwner: carlino
exl-id: 3a483b9d-627a-41d3-8ac1-66f9c5e89ad5
solution: Experience Manager, Experience Manager Sites
feature: Compliance
role: Admin, Developer, Leader, User
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: b1210526-416b-4ef6-bcc0-1692e99f30e9
    internal-label: Administration and security
subfeature_v2:
  - id: c42c36cf-eeed-484a-8b39-a33a68192a07
    internal-label: Compliance
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 80%
---
# AEM Commerce - GDPR 対応{#aem-commerce-gdpr-readiness}

>[!IMPORTANT]
>
>以下のセクションでは GDPR を例として使用していますが、詳細はすべてのデータ保護およびプライバシー規制（GDPR、CCPA など）に当てはまります。

データのプライバシー権に関する EU 一般データ保護規則（GDPR）が 2018年5月に発効します。 [アドビプライバシーセンターの GDPR ページ](https://business.adobe.com/jp/privacy/general-data-protection-regulation.html?lang=ja)を参照してください。

>[!NOTE]
>
>詳しくは、[AEM の GDPR 対応](/help/managing/data-protection-and-privacy.md)を参照してください。

![screen_shot_2018-03-22at111606](assets/screen_shot_2018-03-22at111606.jpg)

アドビのデフォルトのコマース統合では AEM がエクスペリエンスレイヤーとなり、サービスを利用して得られたデータをヘッドレスモードで動作する顧客のコマースプラットフォームに送り返します。

一部のコマースプラットフォームでは、プロファイル情報（`/home/users`）と（コマースプラットフォームにログインするための）コマーストークンが AEM 内に格納されます。 これらのユースケースについては、[AEM プラットフォームでの GDPR 要求への対応](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md)をお読みください。

![screen_shot_2018-03-22at111621](assets/screen_shot_2018-03-22at111621.jpg)

## AEM Commerce での GDPR 要求の処理 {#handling-gdpr-requests-for-aem-commerce}

Salesforces Commerce Cloud 統合の場合、AEM Commerce には GDPR 関連の情報は一切格納されません。 [Salesforce Cloud](https://documentation.b2c.commercecloud.salesforce.com/DOC1/index.jsp) にリクエストを転送してください。

hybris および HCL WebSphere® Commerce 統合の場合、AEM 内に若干のデータが存在します。 [AEM Platform の GDPR 手順](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md)に従い、以下の質問について考察してください。

1. **自分のデータはどこに保存または使用されていますか？** AEMから表示される、名前、コマースユーザーID、トークン、パスワード、アドレスデータなどのキャッシュされたユーザープロファイル情報。
1. **対象となるGDPR データを誰と共有しますか？** AEM Commerce内のGDPR関連データは、更新されても（前述の関連プロファイル情報を除く）保存されることはありませんが、コマースプラットフォームにプロキシされて戻されます。
1. **ユーザーデータの削除方法は？** AEM でユーザープロファイルを削除し、コマースプラットフォームでユーザーの削除を呼び出してください。

>[!NOTE]
>
>[hybris の wiki](https://wiki.hybris.com/) または [HCL WebSphere® Commerce のドキュメント](https://help.hcltechsw.com/commerce/index.html)を必要に応じて参照してください。
