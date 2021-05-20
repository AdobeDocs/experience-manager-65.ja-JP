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
exl-id: b6ded6ac-4fb1-49f9-b272-16774c3e89a3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 33%

---

# We.Finance 自動保険更新リファレンスサイトのチュートリアル{#we-finance-auto-insurance-renewal-reference-site-walkthrough}

## We.Finance リファレンスサイトのシナリオ  {#we-finance-reference-site-scenario}

We.Finance社のサイトは、AEM Formsのインタラクティブ通信機能を学ぶのに役立つ金融サービスサイトです。

We.Finance Auto Insuranceの使用例の詳細なチュートリアルを参照して、AEM FormsとMicrosoft Dynamicsとの統合が、金融サービス会社での顧客体験をパーソナライズする方法を示します。 このインタラクティブなガイドは、金融会社での複雑なデジタル取引や顧客とのコミュニケーションの実装を容易にするように設計されています。

**まず、ユースケースをご覧ください。**

Sarah Rose は We.Finance 社の既存の顧客で、自動保険契約を購入しています。今が保険の更新の時期だ。 We.Finance 社の保険営業担当である Gloria Rios は、Sarah に契約の更新について通知します。Sarah は電子メールに記載されている手順に従い、プロセスを正常に完了します。

## 自動保険申し込みのチュートリアル  {#auto-insurance-application-walkthrough}

We.Finance自動保険の申し込みシナリオは、ユーザーに対する視覚的なナレーションであり、次の2人のペルソナに基づいています。

* Sarah Rose（We.Finance 社の顧客）
* Gloria Rios（We.Finance 社の保険営業担当）

### Gloria が We.Finance 社から保険契約の更新通知を送信する  {#gloria-sends-an-insurance-policy-renewal-communication-from-we-finance}

GloriaがAEMインスタンスにログインし、「**保険の自動更新**」をクリックしてから「**エージェントUIを開く」をクリックします。**&#x200B;クリックすると、Sarah Roseのポリシーの詳細が保険のドキュメントに事前入力されます。Gloriaは「**送信**」をクリックし、「送信開始済み」というメッセージが数秒後に「送信に成功しました」というメッセージが画面に表示されます。

Sarahは「Your Auto Insurance Renewal」（自動保険更新）という件名の電子メールを受信します。

![エージェント UI](assets/agent_ui_email_new.png)

#### 実際の動作確認 {#see-it-yourself}

**Adobe Experience Manager** > **Forms** > **Formsとドキュメント** > **We.Finance** > **自動保険**&#x200B;に移動します。 自動保険更新&#x200B;**インタラクティブ通信**&#x200B;を選択し、**エージェントUIを開く**&#x200B;をクリックします。 エージェント UI でインタラクティブ通信が開きます。ポリシードキュメントが添付された電子メールを受け取る有効な電子メールアドレスを入力し、「送信」をクリックします。

`https://[authorHost]: authorPort]/aem/formdetails.html/content/dam/formsanddocuments/we-finance/autoinsurance/auto-insurance-renewal.`から直接、自動保険更新のインタラクティブ通信にアクセスして確認できます。

### Sarah は We.Finance 社から保険契約の更新通知を受信し、更新を決める {#sarah-receives-an-insurance-policy-renewal-communication-from-we-finance-and-decides-to-renew}

Sarahは、自動保険のポリシーの有効期限が近づいていることを知らせる、We.Finance社からの添付ファイルを含む電子メールを受信します。 添付ファイルは、彼女の自動保険レターの印刷版です。

Sarahは「 **今すぐ更新** 」をクリックし、自動保険レターのWeb版にリダイレクトされます。 このレターの上に、Sarahはポリシーの有効期限が切れるまでの残り日数を見つけます。 このページでは、Sarahは保険契約の詳細（ポリシー番号、支払額、割引オファーやロイヤルティ報酬など）の基本的な概要を提供します。 Sarahは再度、ポリシーの下部にある「**今すぐ更新**」をクリックします。

![ref1](assets/ref1.png)

#### 仕組み {#how-it-works}

自動保険レターのWeb出力と印刷出力は、インタラクティブ通信のマルチチャネル機能を使用して作成されます。

電子メールに含まれている「今すぐ更新する」ボタンは、自動保管更新の申し込みにリンクされます。これはパブリッシュインスタンス上のインタラクティブ通信です。

#### 実際の動作確認  {#see-it-yourself-1}

PDF が添付された電子メールを受信します。PDFは、自動保険レターの印刷版です。 「**今すぐ更新**」をクリックして、ポリシーのWebバージョンに移動します。 個人情報とポリシーの詳細を確認し、[**今すぐ更新**]をクリックすると、別のインタラクティブ通信が表示されます。

電子メールの「**今すぐ更新**」ボタンを押すと、SarahはポリシーのWebバージョンに移動します。 次の URL にアクセスできます。

`https://[authorServer]:[authorPort]/content/document.html?schema=fdm&documentId=/content/forms/af/we-finance/autoinsurance/auto-insurance-renewal/channels/web.html&customerId=1`

自動保険更新の詳細な概要を確認し、ページ下部の「**今すぐ更新**」をクリックします。

### 支払いページの表示 {#sarah-reaches-the-payment-page}

We.Finance 社の支払いページが表示されます。Sarahは、自分のレコードと共にポリシー番号と有効期限を再確認します。 ページの右側で、Sarahは更新の「Payment Summary」をチェックし、合計金額に対して10%のプレミアム割引を適用します。

#### 仕組み {#how-it-works-1}

「今すぐ更新」ボタンをクリックすると、支払いページに移動します。 支払いページはアダプティブフォームです。

#### 実際の動作確認 {#see-it-yourself-2}

「**今すぐ更新する**」をクリックして支払いページにアクセスします。クレジットカード情報を入力し、**支払いを行う**&#x200B;をクリックします。

オーサリングインスタンスの支払いページには、

`https://[authorServer]:[authorPort]/content/document.html?documentId=/content/forms/af/we-finance/credit-card/ccbillpayment.html&schema=fdm&customerId=1`

### Sarah は支払いを行ってプロセスを完了する {#sarah-makes-the-payment-and-completes-the-process}

Sarahはクレジットカードの詳細を入力し、「**支払いを行う**」をクリックします。

#### 仕組み {#how-it-works-2}

Sarah がクレジットカードの詳細を入力して「送信」をクリックすると、クレジットカードによる支払い処理が行われ、アダプティブォームで設定された「ありがとうございます」メッセージが画面に表示されます。

#### 実際の動作確認  {#see-it-yourself-3}

「支払いを行う」をクリックした後に確認メッセージを表示できます。

`https://[authorServer]:[authorPort]/content/forms/af/we-finance/credit-card/ccbillpayment/jcr:content/guideContainer.guideThankYouPage.html?owner=admin&status=Submitted`
