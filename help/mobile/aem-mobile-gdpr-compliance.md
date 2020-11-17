---
title: AEM Mobile - GDPR 対応
seo-title: AEM Mobile - GDPR 対応
description: 'null'
seo-description: 'null'
uuid: 817c434f-4b78-40f7-99d6-6efafdedb77e
contentOwner: trushton
discoiquuid: 9399dd3d-a485-4f53-a6f2-7b190da4235b
translation-type: tm+mt
source-git-commit: 85a3dac5db940b81da9e74902a6aa475ec8f1780
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 84%

---


# AEM Mobile - GDPR 対応 {#aem-mobile-gdpr-readiness}

>[!IMPORTANT]
>
>以下の節ではGDPRを例に挙げていますが、詳細はデータ保護とプライバシーに関するすべての規制に適用されます。GDPR、CCPAなど

## AEM Mobile の GDPR サポート {#aem-mobile-gdpr-support}

AEM Mobile は、GDPR コンプライアンスの義務に関してお客様を支援する準備ができています。個人データは AEM Mobile には保存されません。プロビジョニングされている場合は、Adobe ID で Adobe Experience Mobile にログインすることができます。

[https://aemmobile.adobe.com/signin/index.html](https://aemmobile.adobe.com/signin/index.html)

## Adobe Digital Publishing Suite {#adobe-digital-publishing-suite}

アドビのデジタルパブリッシング製品（AEM Mobile の先行製品）では、アドビによる GDPR 対応の取り組みをサポートしています。[https://www.adobe.com/jp/privacy/general-data-protection-regulation.html](https://www.adobe.com/jp/privacy/general-data-protection-regulation.html) を参照してください。以下では、アドビと協力して GDPR 要求を開始する方法など、Digital Publishing Suite 製品における GDPR 関連機能のサポートの詳細について説明します。

AEM Mobile と以前の Digital Publishing Suite 製品を混同しないように、以下から Digital Publishing Suite 製品にログインできるようになっています。

[https://digitalpublishing.acrobat.com/ja/welcome.html](https://digitalpublishing.acrobat.com/ja/welcome.html)

### GDPR 要求の開始 {#initiating-a-gdpr-request}

Digital Publishing Suite の GDPR 要求を開始する場合は、アドビカスタマーケアにお問い合わせください。

顧客データを検索するには、以下の ID が必要です。サブセットを受け取った場合は、それ以外の ID がこのユーザーに該当しなかったことを意味します。

必須：

* 顧客の契約 ID：*dpsc-contractId*

次のうち少なくとも1つを指定します。

* エンドユーザーの顧客提供 OAuth ID（顧客の直接権利付与システムで使用されている ID）：*dpsc-directEntitlementId*
* Windows アプリユーザーの場合は、エンドユーザーの App Store ID：*dpsc-windowsAppStoreId*
* エンドユーザーが DPS App とのやり取りに使用する電子メールアドレス：*email*

### Frequently Asked Questions (FAQ) {#frequently-asked-questions-faq}

**Adobeは、DELETEリクエストを開始する際に、App Storeでの購入を削除しますか？**

アドビが削除するのは、App Store での購入品に関する情報（例：サブスクリプションなど）です。購入品そのものは App Store の記録に残っています。アプリ（エンドユーザー）が App Store にログインしたら、それらのレシートが再度取り出されてアドビに送信されます。それ以降は、新しい購入品と見なされ、再度アクセスできるようにアプリで復元されます。

**Adobeは、DELETE要求を開始する際に、ユーザーが提供したエンタイトルメントを削除しますか。**

アドビが削除するのは、顧客の追加の直接権利付与に関する情報です。顧客が使用した OAuth メカニズムにアプリ（エンドユーザー）がログインした場合は、アドビに情報が送信され、サービスによって追加の権利（資格情報）が再び取り出されます。

**エンドユーザーに対する期待値**

エンドユーザーは、アプリをアンインストールする必要があります。これは、アプリに権利を割り当てる際のキーが、ビューアソフトウェアの一部としてデバイス上に存在しているからです。アプリを再インストールすると、（App Store ユーザーに関連付けられている）既存の購入品も（顧客の OAuth ユーザーに関連付けられている）直接の権利付与も復元されます。

**アプリがデバイス上のユーザー間で共有されるとどうなりますか？**

アドビでは、特定のユーザーに直接結び付く情報はほとんど保有していません。データは、ランダムに生成される UUID を使用して関連付けられます。その ID は、アプリのデータに格納され、アプリで要求が開始されるたびに渡されます。つまり、同じデバイスでアプリを共有するエンドユーザーは同じ UUID を使用することになり、GDPR 要求をおこなうユーザーがすべてのデータを所有していると見なされます。アクセス要求と削除要求の場合、DPSC では、アプリを共有している複数のユーザーが 1 人のユーザーと見なされます。

**Analyticsで追跡される個人データ**

なし. 追跡されるデータはありますが、それは（個人データではなく）アプリレベルのデータです。例えば、起動、クラッシュ、終了、アクティビティ、購入、Folio オーバーレイなどのイベントが含まれます。地理的位置、氏名、デバイス ID、IP アドレスなどは追跡されません。

**エンドユーザーが自分自身の情報を指定しても、データが見つかりませんでした。Why not?**

Digital Publishing Suite 製品が進化するにつれて、サービスの実装が変更され、難読化されるデータが増えてきました。ユーザーが提供した情報を使用してもデータが見つからない場合は、その情報からそのユーザーにさかのぼれないことを意味します。

### 例 {#example}

GDPR 要求を開始する場合は、アドビカスタマーケアにお問い合わせください。

Digital Publishing Suite GDPRリクエストの入力と出力の例を次に示します。

#### Inputs: {#inputs}

```
dpsc-contractId = “12345-1234-12416234” 
directEntitlementId = “1234-1234-1234” 
windowsAppStoreId = “testWinAppStoreId” 
email = “test@what.com”
```

#### 出力： {#outputs}

```
{

    "jobId": "test-1524750204384",

    "product": "DPSC",

    "action": "access",

    "userIDS": [

        {

        "namespace": "email",

        "value": "test@what.com"

        },

        {

        "namespace": "windowsAppStoreId",

        "value": "testWinAppStoreId"

        },

        {

        "namespace": "directEntitlementId",

        "value": "1234-1234-1234"

        }

    ],

    "receiptData": {

    "recordsFound": 6,

    "recordsAffected": 0,

    "tablesModified": 0,

    "subscriptionsFound": 24,

    "entitlementsFound": 24

    },

    "records": {

        "DPS_Stage_EntitlementUserDevices": [

        {

            "user_id": "testc685-c9ca-4c1e-a11b-07d10ec724cf",

            "device_id": "appleStore:test1b16-f032-4d9c-9200-0d19999405c4",

            "account_id": "test@what.com"

        },

        {

            "user_id": "test967d-5179-4dc6-958c-facd9d94da38",

            "device_id": "appleStore:test3f07-d5aa-4b32-8fac-b2b690b7ccd7",

            "account_id": "test@what.com"

        },

        {

            "user_id": "test1838-6494-4e74-912c-1edf61581d0e",

            "device_id": "appleStore:test3813-f8cc-49ce-b021-50eb0814a3bb",

            "account_id": "1234-1234-1234"

        },

        {

            "user_id": "test5468-1a11-4e4c-be43-274181a9ef81",

            "device_id": "appleStore:testf082-2783-498d-ab62-b1b2e3eb67ae",

            "account_id": "1234-1234-1234"

        }

        ],

            "DPS_Stage_EntitlementUsers": [

        {

            "id": "store:test04a7-33a3-4b90-863d-79981ead0f19:appleStore",

            "part_id": "0",

            "alias_user_id": "testWinAppStoreId"

        },

        {

            "id": "internal:testd2da-0606-4444-87ef-0d5a1d4a121d:adobe",

            "part_id": "0",

            "user_id": "test@what.com"

        }

        ],

            "DPS_Stage_Subscriptions": [

        {

            "id": "appleStore:testc685-c9ca-4c1e-a11b-07d10ec724cf",

            "account_id": "test3531-a209-4391-beb9-951c7822244e",

            "overflow": "test4e59-86a8-4b75-b699-77e980c287ab",

            "entitlement_count": "12"

        },

        {

            "id": "appleStore:test5468-1a11-4e4c-be43-274181a9ef81",

            "account_id": "test491b-379e-4d24-96ef-e481bf8d3062",

            "overflow": "test931b-7422-485d-85a5-134828187b6c",

            "entitlement_count": "12"

        }

        ],

            "DPS_Stage_Entitlements": [

        {

            "id": "samsungStore:testc685-c9ca-4c1e-a11b-07d10ec724cf",

            "account_id": "test7332-60a0-42b8-a508-474668d83d2e",

            "overflow": "test9bc3-94d0-43cf-b132-0629868f7d9d",

            "entitlement_count": "12"

        },

        {

            "id": "appleStore:test5468-1a11-4e4c-be43-274181a9ef81",

            "account_id": "testf766-102a-460d-8f5a-42f7bb9d68b7",

            "overflow": "test4d96-2197-45a8-9caf-2aa2846b770c",

            "entitlement_count": "12"

        }

        ],

            "s3Buckets": {

            "name": "DPS-Entitlements-Overflow",

            "folder": "stage/",

            "overflows": {

            "subscriptions": [

            "test4e59-86a8-4b75-b699-77e980c287ab",

            "test931b-7422-485d-85a5-134828187b6c"

        ],

            "entitlements": [

            "test9bc3-94d0-43cf-b132-0629868f7d9d",

            "test4d96-2197-45a8-9caf-2aa2846b770c"

                ]

            }

        }

    }

}
```

