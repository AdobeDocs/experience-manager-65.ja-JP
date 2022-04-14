---
title: We.Gov リファレンスサイトの FOIA チュートリアル
seo-title: We.Gov reference site FOIA walkthrough
description: We.Gov リファレンスサイトのウォークスルーでは、情報公開法に基づいて個人から請求された情報の受け取りと開示を、どのように官公庁が AEM Forms を使用して行っているかを説明しています。
seo-description: See the We.Gov reference site walkthrough to understand how AEM Forms helps governments receive and impart information requested by individuals under the Freedom of Information Act.
uuid: 65d4233c-8dad-4e5e-8e39-22eb4f145adc
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: cef8f597-7935-4d98-aacf-9981470ab620
exl-id: 57b5ce89-6b01-4087-a485-6d9696f06378
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '834'
ht-degree: 100%

---

# We.Gov リファレンスサイトの情報公開法ウォークスルー {#we-gov-reference-site-foia-walkthrough}

## リファレンスサイトの情報公開法シナリオ {#reference-site-freedom-of-information-act-scenario}

We.Gov は、養子縁組をした場合に養親がチャイルドサポートの申込を行う公的機関です。We.Gov では、情報公開法の下、養親が下記の政府機関に情報を請求することが許可されています。

* アメリカ国防兵站局
* 国防総省監察総監室
* 司法省 - 情報政策室
* 海軍省
* 環境保護庁

情報公開法について詳しくは、[www.foia.gov](https://www.foia.gov) を参照してください。

このシナリオでは、次の人物が登場します。

* Sarah Rose（情報の請求者）
* John Jacobs（請求を処理し適切な部門へ転送する担当者）
* Gloria Rios（請求に応じて情報を提供する政府機関職員）

## Sarah が FOIA の下、情報の請求を開始 {#sarah-initiates-request-for-information-under-foia}

情報公開法に基づいて、Sarah は児童・家庭援護庁の 2013 年度から 2016 年度までの訴訟の記録の写しを請求します。Sarah は、この請求を司法省 - 情報政策室に提出し、印刷と郵送の費用として最大 100 米ドルを支払うことに署名します。

### 仕組み {#how-it-works}

### 実際の動作確認 {#see-it-yourself}

ブラウザーで、`https://<hostname>:<PublishPort>/wegov` を開きます。We.Gov サイトで、「申請」／「すべての申請」をタップします。「すべての申請」ページの「情報公開法の請求申請」で「申請」をタップします。

## Sarah が情報公開法に基づいて申請を開始 {#sarah-starts-her-application-for-information-under-foia}

Sarah は「**申請**」をクリックし、「情報公開法請求フォーム」ページで次を含む情報を入力します。

* **機関**：Sarah は、請求先の機関として「司法省 - 情報政策局」を指定します。

* **最大支払額**：Sarah は、印刷と郵送の費用として最大 100 米ドルを支払う意思があることを記入します。
* **請求内容の詳細**：Sarah は「児童・家庭援護庁の 2013 年度から 2016 年度までの訴訟の記録の写しの請求」と記入します。

![児童・家庭援護庁の 2013 年度から 2016 年度までの訴訟の記録の写しの請求](assets/sarahfiosform.png)

児童家庭援護庁の 2013 年度から 2016 年度までの訴訟の記録のコピーの請求

いつでも、Sarah は「Save」（保存）をタップしてドラフトを保存し、後でフォームを記入して送信することができます。Sarah はフォームを送信します。

>[!NOTE]
>
>resume-from-email ワークフローは、ログインしているユーザーでのみ機能します。リファレンスサイトのシナリオでは、ユーザー Sarah Rose が追加されていることを確認します。Sarah のログイン資格情報は `srose/password` です。

## John Jacobs が申込書を受信および承認 {#john-jacobs-receives-and-approves-the-application}

John Jacobs が請求を受信してそれを担当者に送ります。AEM インボックスでは、Gloria はすべての送信済み申込を 1 つの場所で見ることができます。

### 仕組み {#how-it-works-1}

Sarah が FOIA の申込書に入力して送信すると、請求のレコードが John Jacobs のインボックスに送信されます。John Jacobs は送信された申込書を確認し、承認または拒否することができます。

### 動作を確認 {#see-it-yourself-1}

次の場所にある AEM インボックスにアクセスします。https://&lt;***ホスト名***>:&lt;***公開ポート***>/content/we-finance/global/en/login.html?resource=/aem/inbox.htmlJohn Jacobs のユーザー名とパスワード（jjacobs／password）を使用して AEM インボックスにログインし、情報公開法の申請を確認します。Forms 中心のワークフロータスクで AEM インボックスを使用する方法について詳しくは、「[AEM インボックスでの Forms アプリケーションとタスクの管理](/help/forms/using/manage-applications-inbox.md)」を参照してください。

![johnjacobs](assets/johnjacobs.png)

John Jacobs は申し込みダッシュボードから申し込みを確認、承認、または拒否することができます。John Jacobs は申し込みの詳細を選択して開き、確認後に承認します。

![johnjacobstaskdetail-1](assets/johnjacobstaskdetail-1.png)

### <strong>Sarah が送信確認の電子メールを受信</strong> {#strong-sarah-receives-an-acknowledgement-email-strong}

John Jacobs が申し込みを承認した後、Sarah は We.Gov サイトから送信確認の電子メールを受け取ります。Sarah は、申し込みの処理にかかる料金と時間について通知を受けます。電子メールには、Sarah が申請を更新する場合の問い合わせ先として、電子メールと電話の詳細も含まれています。

![sarahroseemail](assets/sarahroseemail.png)

## Gloria は 2 次承認として FOIA の請求を受信 {#gloria-receives-the-foia-request-for-second-level-approval}

John Jacobs が必要な情報を記入し Sarah の請求を承認すると、請求は最終承認として Gloria Rios に進められます。Gloria は添付されたレコードのドキュメントを確認して、請求を承認します。

![gloriariosinbox](assets/gloriariosinbox.png)

### 仕組み {#how-it-works-2}

John Jacobs が FOIA の請求を承認すると、申込書の PDF またはレコードのドキュメントが作成され、Gloria Rios のインボックスに送信されます。Gloria は提出された請求を確認し、請求を承諾または却下することができます。

### 動作を確認 {#see-for-yourself}

次の場所で AEM インボックスにアクセスできます。https://&lt;***ホスト名***>:&lt;***公開ポート***>/content/we-finance/global/en/login.html?resource=/aem/inbox.htmlGloria Rios のユーザー名とパスワード（grios／password）を使用して AEM インボックスにログインし、情報公開法の請求を確認します。

Gloria は FOIA 請求を開いて詳細を確認します。請求の詳細を確認し、請求されたドキュメントの提供の可能性を確認した後、Gloria は請求を承認します。

![gloriariosapproves](assets/gloriariosapproves.png)

## Sarah は、請求が承認されたことを伝える通知を受信します。 {#sarah-receives-notification-that-her-request-is-approved}

Gloria がFOIA の請求を承認した後、Sarah は We.Gov サイトから申請が承認されたことを知らせる電子メールを受信します。電子メールには、ドキュメント提供の仮の予定と請求を追跡するための問い合わせの詳細も含まれています。

![sarahroseemailapproval](assets/sarahroseemailapproval.png)
