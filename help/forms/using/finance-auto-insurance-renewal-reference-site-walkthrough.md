---
title: We.Finance 自動保険更新リファレンスサイトのチュートリアル
seo-title: We.Finance 自動保険更新リファレンスサイトのチュートリアル
description: We.Finance 自動保険更新リファレンスサイトのチュートリアル
uuid: c749a6f7-71f1-4f47-b824-9c7b699072c7
contentOwner: dekalra
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
discoiquuid: ad450124-49a5-4afb-aac3-ed3733d6504b
docset: aem65
translation-type: tm+mt
source-git-commit: a873cf3e7efd3bc9cd4744bf09078d9040efcdda
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 33%

---


# We.Finance 自動保険更新リファレンスサイトのチュートリアル{#we-finance-auto-insurance-renewal-reference-site-walkthrough}

## We.Finance リファレンスサイトのシナリオ  {#we-finance-reference-site-scenario}

We.Financeサイトは、AEM Formsの対話型通信機能を学ぶのに役立つ金融サービスサイトです。

AEMフォームとMicrosoft Dynamicsとの統合が、金融サービス会社での顧客体験をパーソナライズする方法を示すWe.Finance Auto Insuranceの使用例の詳細なチュートリアルをご覧ください。 インタラクティブウォークスルーは、複雑なデジタルトランザクションの実装と、金融会社での顧客とのやり取りを容易にするように設計されています。

**まず、ユースケースをご覧ください。**

Sarah Rose は We.Finance 社の既存の顧客で、自動保険契約を購入しています。今が保険を更新する時だ We.Finance 社の保険営業担当である Gloria Rios は、Sarah に契約の更新について通知します。Sarah は電子メールに記載されている手順に従い、プロセスを正常に完了します。

## 自動保険申し込みのチュートリアル  {#auto-insurance-application-walkthrough}

We.Finance自動保険申込シナリオは、ユーザーに対する視覚的なナレーションで、次の2人の人物に基づいています。

* Sarah Rose（We.Finance 社の顧客）
* Gloria Rios（We.Finance 社の保険営業担当）

### Gloria が We.Finance 社から保険契約の更新通知を送信する  {#gloria-sends-an-insurance-policy-renewal-communication-from-we-finance}

GloriaはAEMインスタンスにログインし、**自動保険更新**&#x200B;をクリックしてから、**Open Agent UIをクリックします。**&#x200B;クリックすると、保険ドキュメントにSarah Roseのポリシーの詳細が事前入力されます。「**Submit** 」をクリックすると、「 Submission Initiated 」という画面にメッセージが表示され、数秒後に「 Submitted Successfully 」と表示されます。

Sarahが「Your Auto Insurance Renewal」という件名の電子メールを受信します。

![エージェント UI](assets/agent_ui_email_new.png)

#### 実際の動作確認 {#see-it-yourself}

**Adobe Experience Manager** > **Forms** > **Forms&amp;ドキュメント** > **We.Finance** > **自動保険**&#x200B;に移動します。 「Auto Insurance Renewal **interactive communication**」を選択し、「**Open Agent UI**」をクリックします。 エージェント UI でインタラクティブ通信が開きます。ポリシードキュメントが添付された電子メールを受信する有効な電子メールアドレスを入力し、「送信」をクリックします。

`https://[authorHost]: authorPort]/aem/formdetails.html/content/dam/formsanddocuments/we-finance/autoinsurance/auto-insurance-renewal.`から直接、保険の自動更新の対話型通信にアクセスして確認できます

### Sarah は We.Finance 社から保険契約の更新通知を受信し、更新を決める {#sarah-receives-an-insurance-policy-renewal-communication-from-we-finance-and-decides-to-renew}

Sarahは、We.Financeから添付ファイルが添付された電子メールを受信します。この電子メールにより、自動保険のポリシーがまもなく期限切れになることを通知します。 添付ファイルは、彼女の自動保険レターの印刷版です。

**「今すぐ更新**」をクリックし、自動保険のレターのWebバージョンに誘導されます。 このレターの上に、Sarahはポリシーの有効期限が切れるまでの日数を見つけます。 このページでは、Sarahは保険契約の詳細(ポリシー番号、支払期限額、割引オファー、ロイヤルティ報酬など)の基本的な概要を確認できます。 Sarahは再度、ポリシーの下部にある「**今すぐ更新**」をクリックします。

![ref1](assets/ref1.png)

#### 仕組み {#how-it-works}

自動保険レターのWebおよび印刷出力は、Interactive Communicationsのマルチチャネル機能を使用して作成されます。

電子メールに含まれている「今すぐ更新する」ボタンは、自動保管更新の申し込みにリンクされます。これはパブリッシュインスタンス上のインタラクティブ通信です。

#### 実際の動作確認  {#see-it-yourself-1}

PDF が添付された電子メールを受信します。このPDFは、自動保険レターの印刷版です。 「**今すぐ更新**」をクリックして、ポリシーのWebバージョンを表示します。 個人情報とポリシーの詳細を確認し、[**今すぐ更新**]をクリックすると、別の対話型通信が開きます。

電子メールの「**今すぐ更新**」ボタンをクリックすると、SarahはポリシーのWebバージョンに移動します。 次の URL にアクセスできます。

`https://[authorServer]:[authorPort]/content/document.html?schema=fdm&documentId=/content/forms/af/we-finance/autoinsurance/auto-insurance-renewal/channels/web.html&customerId=1`

自動保険の更新の詳細な概要を確認し、ページの下部にある&#x200B;**今すぐ更新**&#x200B;をクリックします。

### 支払いページの表示 {#sarah-reaches-the-payment-page}

We.Finance 社の支払いページが表示されます。Sarahは、自分のレコードと共にPolicy Number and Date of Expirationを再確認します。 ページの右側で、Sarahは更新の支払要約を合計金額の10%プレミアム割引で確認します。

#### 仕組み {#how-it-works-1}

「今すぐ更新」ボタンをクリックすると、支払いページに移動します。 支払いページはアダプティブフォームです。

#### 実際の動作確認 {#see-it-yourself-2}

「**今すぐ更新する**」をクリックして支払いページにアクセスします。クレジットカード情報を入力し、「**支払い**」をクリックします。

オーサリングインスタンスで、支払いページには、

`https://[authorServer]:[authorPort]/content/document.html?documentId=/content/forms/af/we-finance/credit-card/ccbillpayment.html&schema=fdm&customerId=1`

### Sarah は支払いを行ってプロセスを完了する {#sarah-makes-the-payment-and-completes-the-process}

Sarahはクレジットカードの詳細を入力し、「**支払いを行う**」をクリックします。

#### 仕組み {#how-it-works-2}

Sarah がクレジットカードの詳細を入力して「送信」をクリックすると、クレジットカードによる支払い処理が行われ、アダプティブォームで設定された「ありがとうございます」メッセージが画面に表示されます。

#### 実際の動作確認  {#see-it-yourself-3}

確認メッセージは、「支払いを行う」をクリックした後、

`https://[authorServer]:[authorPort]/content/forms/af/we-finance/credit-card/ccbillpayment/jcr:content/guideContainer.guideThankYouPage.html?owner=admin&status=Submitted`
