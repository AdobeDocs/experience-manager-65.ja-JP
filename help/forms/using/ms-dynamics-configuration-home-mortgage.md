---
title: We.Finance リファレンスサイトの住宅ローンワークフローのための Microsoft Dynamics 365 の設定
seo-title: Configure Microsoft Dynamics 365 for the home mortgage workflow of the We.Finance reference site
description: We.Finance リファレンスサイトの住宅ローンワークフローでアダプティブフォームを通じて Microsoft Dynamics 365 を活用する方法について説明します
seo-description: Learn how to leverage the Microsoft® Dynamics 365 services through adaptive forms for the home mortgage workflow of the We.Finance Reference site
uuid: a0656d90-84c7-46d1-9a16-dadcc19ff9ef
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: develop, Configuration
discoiquuid: 6b31397a-fb06-4043-9368-59fb4fce8afa
exl-id: 2ac37dc5-d88d-4f98-8576-cd2ca6f0ea3a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '398'
ht-degree: 100%

---

# We.Finance リファレンスサイトの住宅ローンワークフローのための Microsoft Dynamics 365 の設定 {#configure-microsoft-dynamics-for-the-home-mortgage-workflow-of-the-we-finance-reference-site}

We.Finance リファレンスサイトの住宅ローンワークフローでアダプティブフォームを通じて Microsoft Dynamics 365 を活用する方法について説明します

## 概要 {#overview}

Microsoft® Dynamics 365 は、顧客関係管理（CRM）および企業資源計画（ERP）用のソフトウェアで、顧客の口座や連絡先、潜在顧客、顧客機会、顧客事例を作成して管理する企業ソリューションを提供します。

AEM Forms はクラウドサービスを提供して、Dynamics 365 を [Forms データ統合](/help/forms/using/data-integration.md)モジュールに統合します。Microsoft® Dynamics を使用した住宅ローン申し込みのチュートリアルのシナリオを使用する前に、Microsoft® Dynamics 365 を We.Finance 参照サイトで使用するために設定をおこなう必要があります。

## 前提条件 {#prerequisites}

Dynamics 365 のセットアップと設定に進む前に、以下を実行または入手している必要があります。

* AEM 6.3 Forms Service Pack 1 以降
* Microsoft® Dynamics 365 のアカウント
* Microsoft® Azure Active Directory を使用した Dynamics 365 サービスの登録済みアプリケーション
* 登録済みアプリケーションのクライアント ID とクライアントの秘密鍵

## サイトのホームページと住宅ローン計算機のリンク {#link-the-home-mortgage-calculator-with-your-site-home-page}

1. オーサーインスタンスで次のページに移動します。

   `https://[server]:[port]/editor.html/content/we-finance/global/en/loan-landing-page.html`

1. 住宅ローン計算機まで下にスクロールします。
1. 計算機の右側の列を反転させてから、タップしてポップアップメニューを表示します。ポップアップメニューで、「設定」をタップします。AEM Form コンテナを編集ダイアログが表示されます。

   ![calculatorconfigurepanel](assets/calculatorconfigurepanel.png)

1. AEM Form コンテナを編集ダイアログでアセットのパスを参照し、以下のパスにある home-mortgage-calculator を選択して「**確認**」をタップします。

   formsanddocuments/We.Finance/MS Dynamics/

   ![selectassetpath](assets/selectassetpath.png)

1. 「**完了**」をタップします。
1. 編集したページを発行します。

   >[!NOTE]
   >
   >計算機フィールドと FDM の連結は、We.Finance 参照サイトのパッケージで事前に設定されています。連結を表示するには、オーサリングモードでフォームを開き、フィールドの連結の参照を確認します。

1. 住宅ローン申し込みの申請者の記録を保存するためにカスタムエンティティを作成するには、AEMFormsFSIRefsite_1_0.zip ソリューションパッケージを Microsoft® Dynamics インスタンスに読み込みします。

   1. パッケージを次の場所からダウンロードします。

      `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/AEMFormsFSIRefsite_1_0.zip`

   1. ソリューションパッケージを Microsoft® Dynamics インスタンスに読み込みます。Microsoft® Dynamics インスタンスで、**設定**／**ソリューション**&#x200B;に移動し、「**読み込み**」をタップします。

1. refsite で使用する連絡先の詳細を設定するには、Sarah Rose Contact.CSV パッケージを Microsoft® Dynamics インスタンスにインポートします。

   1. パッケージを次の場所からダウンロードします。

      `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/Sarah%20Rose%20Contact.csv`

   1. パッケージを Microsoft® Dynamics インスタンスに読み込みます。Microsoft® Dynamics インスタンスで、**営業**／**連絡先**&#x200B;に移動し、「**データを読み込み**」をタップします。
