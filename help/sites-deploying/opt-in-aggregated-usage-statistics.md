---
title: 集計した使用状況の統計の収集をオプトインする方法
description: 集計した使用状況の統計をオプトインする方法を説明します。
contentOwner: raiman
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
docset: aem65
exl-id: e626bdd8-b7ae-4de5-a0a0-47fb74c080d7
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 49%

---

# 集計した使用状況の統計の収集をオプトインする方法{#opting-into-aggregated-usage-statistics-collection}

## はじめに {#introduction}

Adobe Experience Manager（AEM）とのやり取りの方法に関するAdobe統計情報を送信することで、Adobe Experience Cloudの改善に役立てることができます。 この情報は、会社のサイト訪問者に関するデータを含まず、Adobeがユーザーエクスペリエンスを提供、サポート、向上させるために使用されるだけです。

タッチ UI または web コンソールを使用して、使用状況の統計の収集をオプトインできます。

>[!NOTE]
>
>GDPR や CCPA など、様々なデータ保護およびプライバシー規制があります。AEM Sites では、データ保護やプライバシーコンプライアンスに関する義務をお客様が果たすのを支援する準備が整っています。このページでは、集計した使用状況の統計の収集をオプトイン（またはオプトアウト）する手順を説明します。
>
>詳しくは、[アドビのプライバシーセンター](https://www.adobe.com/jp/privacy.html)も参照してください。

>[!NOTE]
>
>オプトアウトは、 [Web コンソール](/help/sites-deploying/opt-in-aggregated-usage-statistics.md#opt-in-by-using-the-web-console) または、AEM オプトイン画面でオプトインオプションを選択しないことで解決できます。

## タッチ UI を使用したオプトイン {#opt-in-by-using-the-touch-ui}

AEMを初めて起動する際に、次のようにタッチ UI を使用してオプトインできます。

1. AEM ナビゲーション画面で、 **受信トレイ** （ベル）アイコン。

   ![usage_statisticsnavigationscreen](assets/usage_statisticsnavigationscreen.png)

1. ドロップダウンリストで、「**集計した使用状況の統計の収集を有効にする**」を選択します。

   ![usage_statisticsnavigationscreen2](assets/usage_statisticsnavigationscreen2.png)

1. オプトイン画面で、「**集計した使用状況の統計の収集を許可**」を選択します。

   ![usage_statisticsopt-inscreen](assets/usage_statisticsopt-inscreen.png)

1. クリック &quot;**完了**」と入力します。

## Web コンソールを使用したオプトイン {#opt-in-by-using-the-web-console}

次のように、web コンソールを使用してオプトイン（またはオプトアウト）できます。

1. AEM ナビゲーション画面で、**ツール**／**操作** の順にクリックします。

   ![usage_statisticsopsdashboard](assets/usage_statisticsopsdashboard.png)

1. 操作ウィンドウで「**Web コンソール**」をクリックします。

   ![usage_statisticswebconsole](assets/usage_statisticswebconsole.png)

1. 「**Aggregated Usage Statistics Collection**」を探します。
1. **編集**&#x200B;アイコンをクリックします。

   ![usage_statisticscollectedit](assets/usage_statisticscollectionedit.png)

1. 「**Enabled**」チェックボックスをオンにします。または、使用状況の統計の収集をオプトアウトする場合は、このチェックボックスをオフにします。

   ![usage_statisticsselect](assets/usage_statisticsselect.png)

1. 「**保存**」をクリックします。
