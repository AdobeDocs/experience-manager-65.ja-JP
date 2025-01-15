---
title: Adobe Experience Manager Mobile - GDPR 対応
description: Adobe Experience Managerが GDPR コンプライアンス義務を支援する準備ができている方法について説明します。
contentOwner: trushton
exl-id: d06e675f-fb61-47da-85de-e0b50dd44153
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 1%

---

# AEM Mobile - GDPR 対応 {#aem-mobile-gdpr-readiness}

>[!IMPORTANT]
>
>以下の節では GDPR を例として使用していますが、詳細はすべてのデータ保護およびプライバシー規制（GDPR、CCPA など）に適用できます。

{{ue-over-mobile}}

## AEM Mobile GDPR のサポート {#aem-mobile-gdpr-support}

AEM Mobileは、お客様の GDPR コンプライアンス義務を支援する準備が整っています。 AEM Mobileには個人データは保存されません。 プロビジョニングされている場合は、Adobe IDを使用して Experience Mobile のAdobeにログオンできます。

<!-- [https://aemmobile.adobe.com/signin/index.html](https://aemmobile.adobe.com/signin/index.html) -->

## Adobe Digital Publishing Suite {#adobe-digital-publishing-suite}

Adobeのデジタルパブリッシング製品（AEM Mobileに先行）は、Adobeの GDPR 対応イニシアチブをサポートします。 [https://business.adobe.com/privacy/general-data-protection-regulation.html](https://business.adobe.com/privacy/general-data-protection-regulation.html?lang=ja) を参照してください。 以下では、Adobeと連携して GDPR リクエストを開始する方法など、Digital Publishing Suite製品での GDPR 関連機能のサポートについて詳しく説明します。

AEM Mobileを古いDigital Publishing Suiteと混同しないために、次の場所からDigital Publishing Suite製品にログインできます。

[https://acrobat.adobe.com/us/en/](https://acrobat.adobe.com/us/en/)

### GDPR リクエストの開始 {#initiating-a-gdpr-request}

Digital Publishing Suiteに対する GDPR リクエストを開始するには、Adobeカスタマーケアにお問い合わせください。

顧客データを見つけるには、次の ID が必要です。 受信したサブセットは、他の ID がこのユーザーに適用されなかったことを意味します。

必須：

* 顧客の契約 ID:*dpsc-contractId*

次のうち少なくとも 1 つを指定します。

* エンドユーザーの顧客が指定した OAuth ID （顧客の直接使用権限システムで使用される ID）:*dpsc-directEntitlementId*
* Windows アプリユーザーの場合、エンドユーザーのApp Store ID:*dpsc-windowsAppStoreId*
* DPS アプリとやり取りするためにエンドユーザーが使用するメールアドレス：*email*

### よくある質問（FAQ） {#frequently-asked-questions-faq}

**Adobeは、DELETEリクエストの開始時にApp Storeの購入を削除しますか？**

Adobeは、アプリストアでの購入（サブスクリプションなど）に関する情報を削除しますが、購入はアプリストアに記録されたままになります。 アプリ（エンドユーザー）がアプリストアにログインすると、それらのレシートは再び取得され、Adobeに送信されます。 その後、それらは新しい購入と見なされ、再びアクセスでアプリによって復元されます。

**Adobeは、DELETEリクエストを行う際に、お客様が指定した使用権限を削除していますか？**

Adobeは、顧客の追加の直接使用権の許容量に関する情報を削除します。 アプリ（エンドユーザー）が、お客様が使用した OAuth メカニズムにログインすると、Adobeに情報が送信され、サービスは追加の使用権限を再度取得します。

**エンドユーザーに期待される機能**

アプリに使用権限を割り当てるキーはビューアソフトウェアの一部としてデバイスに存在するので、エンドユーザーはアプリをアンインストールする必要があります。 エンドユーザーは、アプリを再インストールする場合でも、既存の購入（アプリストアユーザーに関連付けられる）および直接の使用権限の許可（顧客の OAuth ユーザーに関連付けられる）は引き続き復元されることに注意する必要があります。

**デバイス上のユーザー間でアプリが共有されるとどうなりますか？**

Adobeには、特定のユーザーに直接関連付けられる最小限の情報があります。 アプリのデータに保持され、アプリが開始するすべてのリクエストで渡される、ランダムに作成された UUID を使用してデータを関連付けます。 つまり、同じデバイスでアプリを共有するエンドユーザーが同じ UUID を使用し、すべてのデータが GDPR リクエストを行ったユーザーによって所有されていると見なされます。 DPSC では、アクセスリクエストと削除リクエストの両方に対して、アプリを共有するユーザーが 1 人のユーザーと見なされます。

**Analytics ではどのような個人データが追跡されますか？**

なし. 追跡中のデータがありますが、それはアプリレベル（個人ではない）にあります。 これには、ローンチ、クラッシュ、クローズ、アクティビティ、購入、フォリオのオーバーレイなどのイベントが含まれます。 地理的な場所、名前、デバイス ID または IP アドレスは追跡されません。

**エンドユーザーが情報を提供しましたが、何も見つかりませんでした。 なぜいけないの？**

Digital Publishing Suite製品の進化に伴い、サービスの実装が変わり、より多くのデータが不明化されました。 ユーザーから提供されたデータを使用してデータが見つからない場合、ユーザーのデータをそのユーザーに遡って追跡することはできません。

### 例 {#example}

GDPR リクエストを開始するには、Adobeカスタマーケアにお問い合わせください。

Digital Publishing Suiteの GDPR リクエストの入力と結果の出力の例を次に示します。

#### 入力： {#inputs}

```
dpsc-contractId = "12345-1234-12416234" 
directEntitlementId = "1234-1234-1234" 
windowsAppStoreId = "testWinAppStoreId" 
email = "test@what.com"
```

#### 出力 {#outputs}

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
