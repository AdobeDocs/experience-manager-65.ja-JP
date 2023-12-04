---
title: We.Finance リファレンスサイトの住宅ローンワークフローのための Microsoft Dynamics 365 の設定
description: We.Finance リファレンスサイトの住宅ローンワークフローに対するアダプティブフォームを通じて、Microsoft&reg; Dynamics 365 サービスを使用する方法を説明します。
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: develop, Configuration
exl-id: 2ac37dc5-d88d-4f98-8576-cd2ca6f0ea3a
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 35%

---

# We.Finance リファレンスサイトの住宅ローンワークフローのための Microsoft Dynamics 365 の設定 {#configure-microsoft-dynamics-for-the-home-mortgage-workflow-of-the-we-finance-reference-site}

We.Finance リファレンスサイトの住宅ローンワークフローに対するアダプティブフォームを通じて、Microsoft® Dynamics 365 サービスを使用する方法を説明します。

## 概要 {#overview}

Microsoft® Dynamics 365 は、顧客関係管理（CRM）および企業資源計画（ERP）用のソフトウェアで、顧客の口座や連絡先、潜在顧客、顧客機会、顧客事例を作成して管理する企業ソリューションを提供します。

AEM Forms はクラウドサービスを提供して、Dynamics 365 を [Forms データ統合](/help/forms/using/data-integration.md)モジュールに統合します。Microsoft® Dynamics を使用した住宅ローン申し込みのチュートリアルのシナリオを使用する前に、Microsoft® Dynamics 365 を We.Finance 参照サイトで使用するために設定をおこなう必要があります。

## 前提条件 {#prerequisites}

Dynamics 365 のセットアップと設定を開始する前に、次の点を確認してください。

* AEM 6.3 Forms Service Pack 1 以降
* Microsoft® Dynamics 365 アカウント
* Microsoft® Azure Active Directory を使用した Dynamics 365 サービスの登録済みアプリケーション
* 登録済みアプリケーションのクライアント ID とクライアントの秘密鍵

## 住宅ローン計算ツールをサイトのホームページにリンクする {#link-the-home-mortgage-calculator-with-your-site-home-page}

1. オーサーインスタンスで、次のページに移動します。

   `https://[server]:[port]/editor.html/content/we-finance/global/en/loan-landing-page.html`

1. 下にスクロールして住宅ローン計算機を表示します。
1. 右側の列の（計算ツールの）パネルをハイライト表示し、を選択してポップアップメニューを表示します。 ポップアップメニューで、「設定」を選択します。 「AEM Formsコンテナを編集」ダイアログが表示されます。

   ![calculatorconfigurepanel](assets/calculatorconfigurepanel.png)

1. AEM Formsコンテナを編集ダイアログで、アセットパスを参照し、次のパスにある home-mortgage-calculator を選択して、「 」を選択します。 **確認**:

   formsanddocuments/We.Finance/MS Dynamics/

   ![selectassetpath](assets/selectassetpath.png)

1. 「**完了**」を選択します。
1. 編集したページを公開します。

   >[!NOTE]
   >
   >計算フィールドと FDM の連結は、We.Finance リファレンスサイトパッケージを通じて事前に設定されています。 連結を表示するには、オーサリングモードでフォームを開き、フィールドの連結参照を確認します。

1. 住宅ローン申し込みの申し込みの申し込み者レコードを保存するカスタムエンティティを作成するには、AEMFormsFSIRefsite_1_0.zip ソリューションパッケージをMicrosoft® Dynamics インスタンスに読み込みます。

   1. パッケージのダウンロード元：

      `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/AEMFormsFSIRefsite_1_0.zip`

   1. ソリューションパッケージを Microsoft® Dynamics インスタンスに読み込みます。Microsoft® Dynamics インスタンスで、に移動します。 **設定** > **ソリューション** 次に、「 **インポート**.

1. リファレンスサイトで使用するユーザーの連絡先の詳細を設定するには、Sarah Rose Contact.CSV パッケージをMicrosoft® Dynamics インスタンスにインポートします。

   1. パッケージのダウンロード元：

      `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/Sarah%20Rose%20Contact.csv`

   1. パッケージを Microsoft® Dynamics インスタンスに読み込みます。Microsoft® Dynamics インスタンスで、に移動します。 **セールス** > **連絡先** 次に、「 **データを読み込み**.
