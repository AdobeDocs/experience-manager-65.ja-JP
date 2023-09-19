---
title: We.Finance 自動保険更新リファレンスサイトのチュートリアル
description: We.Finance Auto Insurance Renewal リファレンスサイトの説明を参照してください。
contentOwner: dekalra
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
docset: aem65
exl-id: b6ded6ac-4fb1-49f9-b272-16774c3e89a3
source-git-commit: 65c5a4442f17e6bc52deaa1588f535a05698083f
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# We.Finance 自動保険更新リファレンスサイトのチュートリアル{#we-finance-auto-insurance-renewal-reference-site-walkthrough}

## We.Finance リファレンスサイトのシナリオ  {#we-finance-reference-site-scenario}

We.Finance サイトは、AEM Formsのインタラクティブ通信機能を学ぶのに役立つ金融サービスサイトです。

AEM forms とMicrosoft® Dynamics との統合が、金融サービス会社での顧客体験をパーソナライズする方法を示す、We.Finance 自動保険の使用例に関する詳細な説明を読みます。 このインタラクティブなチュートリアルは、金融会社における複雑なデジタルトランザクションや、顧客とのコミュニケーションの実装を容易にすることを目的としています。

**まず、ユースケースをご覧ください。**

Sarah Rose は We.Finance 社の既存の顧客で、自動保険ポリシーを購入しています。Sarah が保険契約を更新するのは今年のその時です。 Gloria Rios は彼女の保険代理店です。 We.Finance 社は、Sarah に対し、ポリシーの更新に関するリマインダーを送信します。 Sarah は電子メールに記載された指示に従い、処理を正常に完了します。

## 自動保険申し込みのチュートリアル {#auto-insurance-application-walkthrough}

We.Finance 社の自動保険申し込みのシナリオでは、次の 2 人の人物を使用して視覚的に説明します。

* Sarah Rose（We.Finance 社の顧客）
* Gloria Rios（We.Finance 社の保険代理店）

### Gloria が We.Finance 社から保険契約の更新に関する連絡を送信 {#gloria-sends-an-insurance-policy-renewal-communication-from-we-finance}

Gloria がAEMインスタンスにログインし、「 」をクリックします。 **自動保険の更新** その後、 **エージェント UI を開く**. 」をクリックします。クリックすると、Sarah Rose のポリシーの詳細が保険関連ドキュメントに表示されます。Gloria がクリック **送信** 画面に「送信開始」と表示され、数秒後に「送信に成功しました」と表示されます。

Sarah は「自動保険更新」という件名のメールを受信します。

![エージェント UI](assets/agent_ui_email_new.png)

#### 実際の動作確認 {#see-it-yourself}

**Adobe Experience Manager** ／**フォーム** ／ **フォームとドキュメント** ／**We.Finance**／**自動保険**&#x200B;に移動します。「自動保険更新／**インタラクティブ通信**」を選択し、「**エージェント UI を開く**」をクリックします。エージェント UI でインタラクティブ通信が開きます。有効な電子メールアドレスを入力して、ポリシードキュメントが添付された電子メールを受信し、「送信」をクリックします。

`https://[authorHost]: authorPort]/aem/formdetails.html/content/dam/formsanddocuments/we-finance/autoinsurance/auto-insurance-renewal.` から自動保険更新インタラクティブ通信に直接アクセスして確認することができます。

### Sarah は We.Finance 社から保険ポリシーの更新通知を受信し、更新を決めます {#sarah-receives-an-insurance-policy-renewal-communication-from-we-finance-and-decides-to-renew}

Sarah は、We.Finance 社から添付ファイルを含む電子メールを受信し、自動保険のポリシーが期限切れになることを Sarah に通知します。 添付ファイルは、Sarah の自動保険レターの印刷版です。

Sarah が「 **今すぐ更新する**」をクリックすると、自動保険レターの Web 版にリダイレクトされます。この手紙の上に、Sarah は自分のポリシーが期限切れになるまでの残り時間を見つけます。 Sarah は、保険番号、支払い金額、割引キャンペーン、ロイヤルティ報酬など、保険ポリシーの詳細情報の概要をこのページで確認できます。Sarah はポリシーの下部の&#x200B;**今すぐ更新する**&#x200B;を再度クリックします。

![ref1](assets/ref1.png)

#### 仕組み {#how-it-works}

自動保険レターの Web 版と印刷版は、インタラクティブ通信のマルチチャンネル機能を使用して作成されます。

電子メール内の「今すぐ更新する」ボタンは、Auto Insurance Renew アプリケーションにリンクされています。これは、パブリッシュインスタンス上のインタラクティブ通信です。

#### 実際の動作確認 {#see-it-yourself-1}

添付のPDFを含む電子メールを受信した。 PDF は自動保険レターの印刷版です。「**今すぐ更新する**」をクリックしてポリシーの Web 版にアクセスします。自分の個人情報やポリシーの詳細を確認し、**今すぐ更新する**&#x200B;をクリックすると、別のインタラクティブ通信が表示されます。

The **今すぐ更新** ボタンをクリックすると、Sarah は Web 上のポリシーに移動します。 次の URL にアクセスできます。

`https://[authorServer]:[authorPort]/content/document.html?schema=fdm&documentId=/content/forms/af/we-finance/autoinsurance/auto-insurance-renewal/channels/web.html&customerId=1`

自動保険更新の詳細な概要を確認してからページ下部の&#x200B;**今すぐ更新する**&#x200B;をクリックします。

### Sarah は支払いページを表示します {#sarah-reaches-the-payment-page}

We.Finance 社の支払いページが表示されます。Sarah は、自分の記録と照らし合わせて、ポリシー番号と有効期限を再確認します。ページの右側で、Sarah は更新の「支払いの概要」をチェックし、合計金額に対して 10%のプレミアム割引を適用します。

#### 仕組み {#how-it-works-1}

「今すぐ更新」ボタンをクリックすると、支払いページが表示されます。支払いページはアダプティブフォームです。

#### 実際の動作確認 {#see-it-yourself-2}

「**今すぐ更新する**」をクリックして支払いページにアクセスします。クレジットカード情報を入力し、「**支払う**」をクリックします。

以下のオーサリングインスタンスから支払いページにアクセスすることができます。

`https://[authorServer]:[authorPort]/content/document.html?documentId=/content/forms/af/we-finance/credit-card/ccbillpayment.html&schema=fdm&customerId=1`

### Sarah は支払いを行ってプロセスを完了します {#sarah-makes-the-payment-and-completes-the-process}

Sarah はクレジットカードの詳細を入力し、**支払う**&#x200B;をクリックします。

#### 仕組み {#how-it-works-2}

Sarah がクレジットカードの詳細を入力して「送信」をクリックすると、クレジットカードの支払いが処理され、アダプティブフォームで設定した「ありがとうございます」メッセージが画面に表示されます。

#### 実際の動作確認 {#see-it-yourself-3}

「支払う」をクリックすると、確認メッセージが以下の URL に表示されます。

`https://[authorServer]:[authorPort]/content/forms/af/we-finance/credit-card/ccbillpayment/jcr:content/guideContainer.guideThankYouPage.html?owner=admin&status=Submitted`
