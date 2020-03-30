---
title: We.Finance リファレンスサイトの住宅ローンワークフローのための Microsoft Dynamics 365 の設定
seo-title: We.Finance リファレンスサイトの住宅ローンワークフローのための Microsoft Dynamics 365 の設定
description: We.Finance リファレンスサイトの住宅ローンワークフローでアダプティブフォームを通じて Microsoft Dynamics 365 を活用する方法について説明します
seo-description: We.Finance リファレンスサイトの住宅ローンワークフローでアダプティブフォームを通じて Microsoft Dynamics 365 を活用する方法について説明します
uuid: a0656d90-84c7-46d1-9a16-dadcc19ff9ef
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: Configuration
discoiquuid: 6b31397a-fb06-4043-9368-59fb4fce8afa
translation-type: tm+mt
source-git-commit: f323b490c37effc3cbb36c793b62fa788eca9545

---


# We.Finance リファレンスサイトの住宅ローンワークフローのための Microsoft Dynamics 365 の設定 {#configure-microsoft-dynamics-for-the-home-mortgage-workflow-of-the-we-finance-reference-site}

We.Finance リファレンスサイトの住宅ローンワークフローでアダプティブフォームを通じて Microsoft Dynamics 365 を活用する方法について説明します

## 概要 {#overview}

Microsoft® Dynamics 365は、顧客アカウント、連絡先、リード、オポチュニティ、およびケースを作成および管理するエンタープライズソリューションを提供する、顧客関係管理(CRM)およびエンタープライズリソース計画(ERP)ソフトウェアです。

AEM Forms provides a cloud service to integrate Dynamics 365 with [Forms Data Integration](/help/forms/using/data-integration.md) module. [Microsoft® Dynamics を使用した住宅ローン申し込みのチュートリアル](/help/forms/using/finance-reference-site-walkthrough.md#home-mortgage-application-walkthrough-with-microsoft-dynamics)では、We.Finance リファレンスサイトで Microsoft® Dynamics を使用して Forms データを統合している場合、顧客が住宅ローンを申し込む際にどのようにサイトを利用しているのかを示しています。Microsoft® Dynamicsシナリオでホーム住宅ローン申し込みのチュートリアルを使用する前に、We.Financeリファレンスサイトで使用するMicrosoft® Dynamics 365を設定する必要があります。

## 前提条件 {#prerequisites}

Dynamics 365 のセットアップと設定に進む前に、以下を実行または入手している必要があります。

* [AEM Forms リファレンスサイトのセットアップおよび設定](/help/forms/using/setup-reference-sites.md)。

* AEM 6.3 Forms Service Pack 1 以降
* Microsoft® Dynamics 365 のアカウント
* Microsoft® Azure Active DirectoryにDynamics 365サービスのアプリケーションを登録しました
* 登録済みアプリケーションのクライアントIDとクライアントシークレット

## サイトのホームページと住宅ローン計算機のリンク {#link-the-home-mortgage-calculator-with-your-site-home-page}

1. オーサーインスタンスで次のページに移動します。

   `https://[server]:[port]/editor.html/content/we-finance/global/en/loan-landing-page.html`

1. 住宅ローン計算機まで下にスクロールします。
1. 計算機の右側の列を反転させてから、タップしてポップアップメニューを表示します。ポップアップメニューで、「設定」をタップします。AEM Form コンテナを編集ダイアログが表示されます。

   ![calculatorconfigurepanel](assets/calculatorconfigurepanel.png)

1. AEM Form コンテナを編集ダイアログで、アセットのパスを参照してから以下のパスにある home-mortgage-calculator を選択して「**確認**」をタップします。

   formsanddocuments/We.Finance/MS Dynamics/

   ![selectassetpath](assets/selectassetpath.png)

1. 「**Done**」をタップします。
1. 編集したページを発行します。

   >[!NOTE]
   >
   >計算機フィールドと FDM の連結は、We.Finance 参照サイトのパッケージで事前に設定されています。連結を表示するには、オーサリングモードでフォームを開き、フィールドの連結の参照を確認します。

1. 住宅ローン申し込みの申請者の記録を保存するためにカスタムエンティティを作成するには、AEMFormsFSIRefsite_1_0.zip ソリューションパッケージを Microsoft® Dynamics インスタンスに読み込みします。

   1. パッケージを次の場所からダウンロードします。

      `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/AEMFormsFSIRefsite_1_0.zip`

   1. ソリューションパッケージを Microsoft® Dynamics インスタンスに読み込みます。In your Microsoft® Dynamics instance, go to **Settings** > **Solutions** and then tap **Import**.

1. refsite で使用する連絡先の詳細を設定するには、Sarah Rose Contact.CSV パッケージを Microsoft® Dynamics インスタンスにインポートします。

   1. パッケージを次の場所からダウンロードします。

      `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/Sarah%20Rose%20Contact.csv`

   1. パッケージを Microsoft® Dynamics インスタンスにインポートします。In your Microsoft® Dynamics instance, go to **Sales** > **Contacts** and then tap **Import Data**.

