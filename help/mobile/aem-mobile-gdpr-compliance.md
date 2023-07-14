---
title: Adobe Experience Manager Mobile - GDPR 対応
description: Adobe Experience Manager Mobile - GDPR 対応
uuid: 817c434f-4b78-40f7-99d6-6efafdedb77e
contentOwner: trushton
exl-id: d06e675f-fb61-47da-85de-e0b50dd44153
source-git-commit: 260f71acd330167572d817fdf145a018b09cbc65
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 2%

---

# AEM Mobile - GDPR 対応 {#aem-mobile-gdpr-readiness}

>[!IMPORTANT]
>
>以下の節では GDPR を例として使用していますが、詳細はすべてのデータ保護およびプライバシー規制に適用できます。（GDPR や CCPA など）

## AEM Mobile GDPR のサポート {#aem-mobile-gdpr-support}

AEM Mobileは、お客様が GDPR に準拠するための義務を果たすのを支援する準備が整っています。 AEM Mobileには個人データは保存されません。 プロビジョニングされている場合は、Adobe IDで Adobe Experience Mobile にログオンできます。

<!-- [https://aemmobile.adobe.com/signin/index.html](https://aemmobile.adobe.com/signin/index.html) -->

## Adobe Digital Publishing Suite {#adobe-digital-publishing-suite}

Adobeのデジタル出版製品 (AEM Mobileに先立つ ) は、Adobeの GDPR 対応に関する取り組みをサポートしています。 詳しくは、 [https://business.adobe.com/privacy/general-data-protection-regulation.html](https://business.adobe.com/privacy/general-data-protection-regulation.html?lang=ja). 以下に、GDPR 要求を開始するためのAdobeとの連携方法など、Digital Publishing Suite製品での GDPR 関連機能のサポートに関する詳細を示します。

AEM Mobileと古いDigital Publishing Suite製品を混同しないように、次の場所でDigital Publishing Suite製品にログインできます。

[https://acrobat.adobe.com/us/en/](https://acrobat.adobe.com/us/en/)

### GDPR 要求の開始 {#initiating-a-gdpr-request}

Adobeの GDPR リクエストを開始できるよう、カスタマーケアにお問い合わせください。Digital Publishing Suite

顧客データを検索するには、次の ID が必要です。 受け取ったサブセットは、他の ID がこのユーザーに適用されなかったことを示します。

必須:

* 顧客の契約 ID : *dpsc-contractId*

次のうち少なくとも 1 つを指定します。

* エンドユーザーが指定した OAuth ID（顧客の直接権利付与システムで使用される ID）: *dpsc-directEntitlementId*
* Windows アプリのユーザーの場合、エンドユーザーのApp Store ID は次のようになります。 *dpsc-windowsAppStoreId*
* エンドユーザーが DPS アプリの操作に使用した電子メールアドレス： *電子メール*

### よくある質問 (FAQ) {#frequently-asked-questions-faq}

**Adobeリクエストを開始すると、App Storeでの購入が削除されますか？**

Adobeは、アプリストアでの購入（購読など）に関する情報を削除しますが、購入はアプリストアで記録されたままです。 アプリ ( エンドAdobe) が App Store にログインすると、それらのレシートが再度取得され、後でに送信されます。これらは新規購入と見なされ、アプリによって再度アクセスできるように復元されます。

**Adobeは、ユーザーリクエストを開始する際に、お客様が提供したDELETEを削除しますか？**

Adobeは、顧客の追加の直接使用権限の許可を持つ情報を削除します。 アプリ（エンドユーザー）が、顧客が使用した OAuth メカニズムにログインすると、Adobeに情報が送信され、サービスが追加の使用権限を再度取得します。

**エンドユーザーに対して期待される操作**

アプリに権限を割り当てる際のキーは、ビューアソフトウェアの一部としてデバイス上に存在するので、エンドユーザーはアプリをアンインストールする必要があります。 エンドユーザーは、アプリを再インストールした場合、既存の購入（App Store ユーザーに関連付けられている）と直接の権利付与（顧客の OAuth ユーザーに関連付けられている）が引き続き復元されることを認識する必要があります。

**デバイス上のユーザー間でアプリを共有するとどうなりますか？**

Adobeは、特定のユーザーに直接関連付けられる最小限の情報を持ちます。 この変数は、ランダムに作成された UUID を使用してデータを関連付けます。この UUID は、アプリのデータに保持され、アプリが開始するリクエストごとに渡されます。 つまり、同じデバイスでアプリを共有するエンドユーザーは同じ UUID を使用し、すべてのデータは、GDPR 要求をおこなう人の所有と見なされます。 アクセス要求と削除要求の両方で、DPSC は、アプリを共有する人を 1 人の人物と見なします。

**Analytics で追跡される個人データは何ですか？**

なし. 追跡されているデータがありますが、アプリレベル（個人レベルではありません）です。 これには、起動、クラッシュ、閉じる、アクティビティ、購入、Folio オーバーレイなどのイベントが含まれます。 地理的な場所、名前、デバイス ID、IP アドレスは追跡されません。

**エンドユーザーが情報を入力しましたが、何も見つかりませんでした。 なぜ？**

Digital Publishing Suite 製品の進化に伴い、サービスの実装が変更され、より多くのデータが不明化されました。 ユーザーが指定したデータを使用してデータが見つからなかった場合、そのユーザーのデータをそのユーザーに追跡できないことを意味します。

### 例 {#example}

Adobeカスタマーケアに問い合わせて、GDPR リクエストを開始できます。

次に、Digital Publishing SuiteGDPR 要求の入力と結果の出力の例を示します。

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
