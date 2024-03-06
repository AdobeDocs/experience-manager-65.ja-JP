---
title: AEM 6.5 と Adobe Campaign の統合
description: Adobe Campaign との統合に対する AEM 6.5 のサポートについて説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: ab41e540-1d43-4fc2-99d4-621ff2290e77
source-git-commit: dac156251ae48e9d83e84ba6a4685689def9e396
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 72%

---


# AEM 6.5 と Adobe Campaign の統合{#integrating-with-adobe-campaign}

Adobe Campaign との統合に対する AEM 6.5 のサポートについて説明します。

Adobe Campaign は、オンラインおよびオフラインのあらゆるチャネルをまたいでキャンペーンをパーソナライズして実施するための一連のソリューションです。

>[!NOTE]
>
>このドキュメントでは、Adobe Campaign と、オンプレミスまたは AMS でホストされている AEM ソリューションである AEM 6.5 との統合について説明します。
>
>クラウドネイティブなAEMソリューションである、Adobe CampaignとAEM as a Cloud Serviceの統合について詳しくは、 [このドキュメントを参照してください。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/integrations/campaign.html?lang=ja)

## Adobe Campaign Classic との統合 {#acc}

Adobe Campaign Classic（ACC）には複数のバージョンがあります。AEM との統合のサポートは、実装した ACC のバージョンと、AEM が Adobe Manage Services（AMS）のオンプレミスにインストールされているかどうかによって異なります。

| ACC バージョン | AEM 6.5 オンプレミス<br>との統合 | AEM 6.5 AMS<br>との統合 |
|---|---|---|
| [v7](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=ja) | サポート対象 | サポート対象 |
| [v8 クライアントコンソール](https://experienceleague.adobe.com/docs/campaign-v8.html?lang=ja) | サポート対象 | サポート対象 |
| [v8 Web ユーザーインターフェイス](https://experienceleague.adobe.com/docs/campaign-web/v8/campaign-web-home.html) | サポート対象 | サポート対象 |

次のドキュメントでは、AEM を Adobe Campaign Classic と統合する方法について説明します。

* [Adobe Campaign Classic との統合](/help/sites-administering/campaignonpremise.md) - 統合の設定について段階的に詳しく説明します。

次の追加ドキュメントでは、統合の使用方法について説明します。

* [メールコアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/email/introduction.html?lang=ja) - AEM で Campaign コンテンツを作成するために使用できる標準のメールコンポーネントについて説明します。
* [Adobe Campaign Classic 統合のトラブルシューティング](/help/sites-administering/troubleshooting-campaignintegration.md) - AEM と ACC の統合に関する最も一般的な問題を修正する方法について説明します。


次のドキュメントでは、AEM as a Cloud ServiceとAdobe Campaign v8 Web ユーザーインターフェイスを統合する方法について説明します。

* [Adobe Campaign v8 Web ユーザーインターフェイスでのAdobe Experience Manager as a Cloud Service でのテンプレートの管理](https://experienceleague.adobe.com/docs/campaign-web/v8/integrations/aem-content.html) - AEMテンプレートとの統合の設定と使用に関する詳しい手順を説明します。
* [Adobe Campaign v8 Web ユーザーインターフェイスでのAdobe Experience Manager as a Cloud Service でのアセットの管理](https://experienceleague.adobe.com/docs/campaign-web/v8/integrations/aem-assets.html) - AEM Assetsとの統合の設定と使用に関する詳しい手順を説明します。


## Adobe Campaign Standard との統合 {#acs}

[Adobe Campaign Standard](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=ja)（ACS）と AEM の統合は、AEM が Adobe Manage Services（AMS）のオンプレミスにインストールされているかどうかによって異なります。

| AEM 6.5 オンプレミス<br>との統合 | AEM 6.5 AMS<br> との統合 |
|---|---|
| サポート対象 | サポート対象 |
| サポート対象 | サポート対象 |

次のドキュメントでは、AEM を Adobe Campaign Standard と統合する方法について説明します。

* [Adobe Campaign Standard との統合](/help/sites-administering/campaignstandard.md)

次の追加ドキュメントでは、統合の使用方法について説明します。

* [メールコアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/email/introduction.html?lang=ja)
