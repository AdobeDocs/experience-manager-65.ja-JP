---
title: AEM Commerce - GDPR 対応
seo-title: AEM Commerce - GDPR Readiness
description: AEM Commerce で GDPR 要求を処理する手順とその使用方法について説明します。
seo-description: null
uuid: 7ca26587-8cce-4c75-8629-e0e5cfb8166c
contentOwner: carlino
discoiquuid: c637964a-dfcb-41fe-9c92-934620fe2cb3
exl-id: 3a483b9d-627a-41d3-8ac1-66f9c5e89ad5
source-git-commit: 3400df1ecd545aa0fb0e3fcdcc24f629ce4c99ba
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 94%

---

# AEM Commerce - GDPR 対応{#aem-commerce-gdpr-readiness}

>[!IMPORTANT]
>
>以下のセクションでは GDPR を例として使用していますが、詳細はすべてのデータ保護およびプライバシー規制（GDPR、CCPA など）に当てはまります。

データのプライバシー権に関する EU 一般データ保護規則（GDPR）が 2018年5月に発効します。[アドビプライバシーセンターの GDPR ページ](https://business.adobe.com/privacy/general-data-protection-regulation.html?lang=ja)を参照してください。

>[!NOTE]
>
>詳しくは、[AEM の GDPR 対応](/help/managing/data-protection-and-privacy.md)を参照してください。

![screen_shot_2018-03-22at111606](assets/screen_shot_2018-03-22at111606.jpg)

アドビのデフォルトのコマース統合では AEM がエクスペリエンスレイヤーとなり、サービスを利用して得られたデータをヘッドレスモードで動作する顧客のコマースプラットフォームに送り返します。

一部のコマースプラットフォームでは、プロファイル情報（`/home/users`）と（コマースプラットフォームにログインするための）コマーストークンが AEM 内に格納されます。これらのユースケースについては、[AEM プラットフォームでの GDPR 要求への対応](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md)をお読みください。

![screen_shot_2018-03-22at111621](assets/screen_shot_2018-03-22at111621.jpg)

## AEM Commerce での GDPR 要求の処理 {#handling-gdpr-requests-for-aem-commerce}

Salesforces Commerce Cloud 統合の場合、AEM Commerce には GDPR 関連の情報は一切格納されません。[Salesforce Cloud](https://documentation.b2c.commercecloud.salesforce.com/DOC1/index.jsp) にリクエストを転送してください。

hybris および HCL WebSphere® Commerce 統合の場合、AEM 内に若干のデータが存在します。[AEM Platform の GDPR 手順](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md)に従い、以下の質問について考察してください。

1. **データはどこに格納され、使用されているか？** キャッシュ内のユーザープロファイル情報（名前、コマースユーザー識別子、トークン、パスワード、住所のデータ）が AEM から示されます。
1. **対象となる GDPR データを誰と共有するか？** AEM Commerce 内の GDPR 関連データの更新は一切格納されず（前述の関連プロファイル情報は除く）、すべて管理元のコマースプラットフォームへと送り返されます。
1. **ユーザーデータの削除方法は？** AEM でユーザープロファイルを削除し、コマースプラットフォームでユーザーの削除を呼び出してください。

>[!NOTE]
>
>[hybris の wiki](https://wiki.hybris.com/) または [HCL WebSphere® Commerce のドキュメント](https://help.hcltechsw.com/commerce/index.html)を必要に応じて参照してください。
