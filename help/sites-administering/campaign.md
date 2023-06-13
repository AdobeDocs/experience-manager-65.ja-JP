---
title: AEM 6.5 とAdobe Campaignの統合
description: Adobe Campaignとの統合に対するAEM 6.5 のサポートについて説明します。
uuid: 6113279e-d1f5-46c3-ac94-50270fa55060
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: fd96f30c-0616-445e-adb9-050d52862ffc
exl-id: ab41e540-1d43-4fc2-99d4-621ff2290e77
source-git-commit: 6fe5e617ceac3c97a77de2d574ec370f30887330
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 9%

---


# AEM 6.5 とAdobe Campaignの統合{#integrating-with-adobe-campaign}

Adobe Campaignとの統合に対するAEM 6.5 のサポートについて説明します。

Adobe Campaignは、オンラインおよびオフラインのあらゆるチャネルにわたってキャンペーンをパーソナライズし、実施するための一連のソリューションです。

>[!NOTE]
>
>このドキュメントでは、Adobe CampaignとAEM 6.5( オンプレミスまたは AMS がホストするAEMソリューション ) の統合について説明します。
>
>クラウドネイティブなAEMソリューションである、Adobe CampaignとAEM as a Cloud Serviceの統合について詳しくは、 [この文書をご覧ください。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/integrations/campaign.html)

## Adobe Campaign Classic との統合 {#acc}

Adobe Campaign Classic(ACC) バージョンは多数あります。 AEMとの統合のサポートは、実装した ACC のバージョンによって異なります。AEMがAdobe管理サービス (AMS) にオンプレミスでインストールされている場合は、そのバージョンに依存します。

| ACC バージョン | AEM 6.5 との統合 <br>オンプレミス | AEM 6.5 との統合<br>AMS |
|---|---|---|
| [v7](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=ja) | サポート対象 | サポート対象 |
| [v8](https://experienceleague.adobe.com/docs/campaign-v8.html) | サポート対象 | サポート対象 |
| Web UI* | サポート対象 | サポート対象 |

*Adobe Campaign Classicの Web UI は、2023 年末に予定されています。

次のドキュメントでは、AEMとAdobe Campaign Classicを統合する方法について説明します。

* [Adobe Campaign Classicとの統合](/help/sites-administering/campaignonpremise.md)  — 統合の設定手順の詳細を説明します。

次の追加のドキュメントでは、統合の使用方法を説明します。

* [電子メールコアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/email/introduction.html) - AEMで Campaign コンテンツを作成する際に使用できる標準的な E メールコンポーネントについて説明します。
* [Adobe Campaign Classic統合のトラブルシューティング](/help/sites-administering/troubleshooting-campaignintegration.md) - AEMと ACC の統合で最も一般的な問題を修正する方法について説明します。

## Adobe Campaign Standard との統合 {#acs}

の統合 [Adobe Campaign Standard](https://experienceleague.adobe.com/docs/campaign-standard.html) AEMを使用する (ACS) 場合、AEMが Manage Services(AMS) のオンプレミスにインストールされているかどうかによって異なります。

| AEM 6.5 との統合 <br>オンプレミス | AEM 6.5 との統合<br>AMS |
|---|---|
| サポート対象 | サポート対象 |
| サポート対象 | サポート対象 |

次のドキュメントでは、AEMとAdobe Campaign Standardを統合する方法について説明します。

* [Adobe Campaign Standard との統合](/help/sites-administering/campaignstandard.md)

次の追加のドキュメントでは、統合の使用方法を説明します。

* [電子メールコアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/email/introduction.html)
