---
title: Adobe Experience Manager Mobile - GDPR対応
description: Adobe Experience Managerが、GDPRへの準拠をどのように支援するのかをご確認ください。
contentOwner: trushton
exl-id: d06e675f-fb61-47da-85de-e0b50dd44153
solution: Experience Manager
feature: Mobile
role: User
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 2%
---
# AEM Mobile - GDPR 対応 {#aem-mobile-gdpr-readiness}

>[!IMPORTANT]
>
>GDPRは、以下のセクションの例として使用されますが、説明されている詳細は、すべてのデータ保護およびプライバシー規制（GDPR、CCPAなど）に適用されます。

{{ue-over-mobile}}

## AEM Mobile GDPR サポート {#aem-mobile-gdpr-support}

AEM Mobileには、GDPRへの準拠に関するお客様のサポートを行う準備が整っています。 AEM Mobileには個人情報は保存されません。 プロビジョニングを行っている場合は、Adobe IDを使用してAdobe Experience Mobileにログオンできます。

<!-- [https://aemmobile.adobe.com/signin/index.html](https://aemmobile.adobe.com/signin/index.html) -->

## Adobe Digital Publishing Suite {#adobe-digital-publishing-suite}

Adobeのデジタルパブリッシング製品（AEM Mobileより前）は、AdobeのGDPR対応イニシアチブをサポートしています。 [https://business.adobe.com/privacy/general-data-protection-regulation.html](https://business.adobe.com/privacy/general-data-protection-regulation.html?lang=ja)を参照してください。 以下では、Adobeと連携してGDPR リクエストを開始する方法など、Digital Publishing Suite製品のGDPR関連機能のサポートに関する詳細を説明します。

AEM Mobileと古いDigital Publishing Suite製品を混同しないようにするには、こちらからDigital Publishing Suite製品にログインします。

[https://acrobat.adobe.com/us/en/](https://acrobat.adobe.com/us/en/)

### GDPR要求の開始 {#initiating-a-gdpr-request}

Adobe カスタマーケアに連絡して、Digital Publishing SuiteのGDPR リクエストを開始できるようにしてください。

顧客データを検索するには、次のIDが必要です。 受け取ったサブセットは、他のIDがこのユーザーに適用されなかったことを意味します。

必須：

* お客様の契約ID: *dpsc-contractId*

次のうち少なくとも1つを指定してください。

* エンドユーザーのお客様が提供したOAuth ID （お客様のダイレクトエンタイトルメントシステムで使用されるID）: *dpsc-directEntitlementId*
* Windows アプリユーザーの場合、エンドユーザーのApp Store ID: *dpsc-windowsAppStoreId*
* エンドユーザーがDPS アプリとのやり取りに使用した電子メールアドレス：*email*

### よくある質問（FAQ） {#frequently-asked-questions-faq}

**DELETE リクエストを開始する際、AdobeはApp Storeの購入を削除しますか？**

Adobeは、App Storeで購入した情報（サブスクリプションなど）を削除しますが、App Storeで購入した情報は引き続き記録されます。 アプリ（エンドユーザー）がアプリストアにログインしている場合、その領収書は再度受け取られ、Adobeに送信されます。 その後、これらは新しい購入と見なされ、アプリによって復元され、再度アクセスできます。

**DELETE リクエストを開始する際、Adobeはお客様が提供した使用権限を削除していますか？**

Adobeは、顧客の追加の直接使用権限に関する情報を削除します。 アプリ（エンドユーザー）がお客様が使用したOAuth メカニズムにログインすると、情報がAdobeに送信され、サービスは追加の使用権限を再度取得します。

**エンドユーザーに期待される機能は何ですか？**

アプリに使用権限を割り当てるキーは、ビューアソフトウェアの一部としてデバイス上に存在するため、エンドユーザーはアプリをアンインストールする必要があります。 エンドユーザーは、アプリを再インストールした場合、既存の購入（アプリストアユーザーに関連付けられている）および直接使用権限（顧客のOAuth ユーザーに関連付けられている）がまだ復元されていることを認識する必要があります。

**アプリがデバイス上のユーザー間で共有されるとどうなりますか？**

Adobeには、特定のユーザーに直接関連付けられる情報が最小限に抑えられています。 ランダムに作成されたUUIDを使用してデータを関連付けます。このUUIDは、アプリのデータに保持され、アプリが開始するすべてのリクエストに渡されます。 つまり、同じデバイスでアプリを共有するエンドユーザーは同じUUIDを使用し、すべてのデータはGDPR要求を行う人が所有していると見なされます。 アクセス要求と削除要求の両方で、DPSCはアプリを共有するユーザーを1人と見なします。

**Analyticsでどのような個人データが追跡されますか？**

なし. 追跡されるデータがありますが、アプリレベルで（個人レベルではありません）。 これには、ローンチ、クラッシュ、クローズ、アクティビティ、購入、フォリオオーバーレイなどのイベントが含まれます。 地理的な場所、名前、デバイス ID、またはIP アドレスは追跡されません。

**エンドユーザーが情報を提供しましたが、何も見つかりませんでした。 なぜですか？**

Digital Publishing Suite製品の進化に伴い、サービスの実装も変更され、より多くのデータが不明化されました。 ユーザーが提供したデータを使用してデータが見つからない場合は、ユーザーのデータをその人に追跡できないことを意味します。

### 例 {#example}

Adobeカスタマーケアに連絡して、GDPR要求を開始できるようにしてください。

Digital Publishing Suite GDPR リクエストの入力と出力の例を次に示します。

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
