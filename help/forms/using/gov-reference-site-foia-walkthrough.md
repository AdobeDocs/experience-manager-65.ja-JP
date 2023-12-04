---
title: We.Gov リファレンスサイトの FOIA チュートリアル
description: We.Gov リファレンスサイトのチュートリアルを参照して、AEM Formsが、情報自由法の下で、政府が個人から要求された情報を受け取り、提供する方法を理解できるようにします。
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 57b5ce89-6b01-4087-a485-6d9696f06378
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 22%

---

# We.Gov リファレンスサイトの情報公開法ウォークスルー {#we-gov-reference-site-foia-walkthrough}

## リファレンスサイト情報自由法のシナリオ {#reference-site-freedom-of-information-act-scenario}

We.Gov は、養子を養子にした場合に養親が子供のサポートを申し込める国営組織です。 また、We.Gov は、情報の自由法に基づき、次の政府部門から情報を要求することも可能です。

* 防衛物流庁
* 検査官総監国防総省
* 司法省 — 情報政策局
* 海軍省
* 環境保護庁

情報の自由法について詳しくは、 [https://www.foia.gov/](https://www.foia.gov).

このシナリオでは、次の人物が登場します。

* Sarah Rose（情報の請求者）
* John Jacobs（リクエストを処理する人物）は、リクエストを適切な部門に転送します。
* Gloria Rios（要求に応じて情報を提供する政府職員）

## Sarah が FOIA の下で情報の要求を開始 {#sarah-initiates-request-for-information-under-foia}

Freedom of Information Act では、Sarah は 2013 年から 2016 年まで、「Administration for Children and Familys」（子供と家族のための管理）ケースログのコピーを要求します。 Sarah はこの申請を法務省 — 情報政策局に送信し、また、Sarah は印刷費用と送料費用に対して最大 100 米ドルを支払うことを義務付けています。

### 仕組み {#how-it-works}

### 実際の動作確認 {#see-it-yourself}

ブラウザーで、`https://<hostname>:<PublishPort>/wegov` を開きます。We.Gov サイトで、「Applications」>「All Applications」を選択します。 「全アプリケーション」ページで、「FOIA 要求のアプリケーション」の下の「適用」を選択します。

## Sarah が情報公開法に基づいて申請を開始 {#sarah-starts-her-application-for-information-under-foia}

Sarah は「**申請**」をクリックし、「情報公開法請求フォーム」ページで次を含む情報を入力します。

* **機関**：Sarah は、請求先の機関として「司法省 - 情報政策局」を指定します。

* **～まで支払う**:Sarah は、印刷および送料の費用として最大 100 米ドルを支払う準備ができていることを指定します。
* **請求内容の詳細**：Sarah は「児童・家庭援護庁の 2013 年度から 2016 年度までの訴訟の記録の写しの請求」と記入します。

![児童・家庭援護庁の 2013 年度から 2016 年度までの訴訟の記録の写しの請求](assets/sarahfiosform.png)

児童・家庭援護庁の 2013 年度から 2016 年度までの訴訟の記録の写しの請求

Sarah は、いつでも **保存** フォームの下書きを保存し、後でフォームに戻ってフォームに入力し、送信します。 Sarah はフォームを送信します。

>[!NOTE]
>
>電子メールからの再開ワークフローは、ログインしたユーザーに対してのみ機能します。 リファレンスサイトのシナリオで、Sarah Rose というユーザーが追加されていることを確認します。 Sarah のログイン資格情報は `srose/password` です。

## John Jacobs が申込書を受信し、承認します {#john-jacobs-receives-and-approves-the-application}

John Jacobs が要求を受け取り、適切な人にルーティングします。 AEM Inbox を使用すると、John は送信されたすべてのアプリを 1 か所で表示できます。

### 仕組み {#how-it-works-1}

Sarah が FOIA 申込書に記入して送信すると、申込書のレコードが John Jacobs のインボックスに送信されます。 John Jacobs は、送信された申込書を表示し、承認または拒否できます。

### 動作を確認 {#see-it-yourself-1}

AEMインボックスには、https://&lt; からアクセスできます。***hostname***>:&lt;***PublishPort***>/content/we-finance/global/en/login.html?resource=/aem/inbox.html. John Jacobs のユーザー名とパスワードとして jjacobs/password を使用してAEM Inbox にログインし、FOIA アプリケーションを確認します。 Forms 中心のワークフロータスクで AEM インボックスを使用する方法について詳しくは、「[AEM インボックスでの Forms アプリケーションとタスクの管理](/help/forms/using/manage-applications-inbox.md)」を参照してください。

![johnjacobs](assets/johnjacobs.png)

John Jacobs は、申し込みダッシュボードから申し込みを表示、承認または拒否できます。 John Jacobs はリクエストの詳細を選択して開き、リクエストをレビューした後、承認します。

![johnjacobstaskdetail-1](assets/johnjacobstaskdetail-1.png)

### <strong>Sarah が確認メールを受信</strong> {#strong-sarah-receives-an-acknowledgement-email-strong}

John Jacobs が申込を承認した後、Sarah は We.Gov サイトから確認の電子メールを受け取ります。 Sarah は、申し込みの処理に必要な料金と時間を通知されます。 電子メールには、Sarah が問い合わせ可能な電子メールと電話の詳細も含まれています。

![sarahroseemail](assets/sarahroseemail.png)

## Gloria は第 2 レベルの承認を求める FOIA のリクエストを受け取ります {#gloria-receives-the-foia-request-for-second-level-approval}

John Jacobs が必要な情報を入力し、Sarah の要求を承認した後、最終的な承認を得るために Gloria Rios に送信されます。 Gloria は添付のレコードのドキュメントをレビューし、リクエストを承認します。

![gloriariosinbox](assets/gloriariosinbox.png)

### 仕組み {#how-it-works-2}

John Jacobs が FOIA 要求を承認すると、申込書のPDFまたはレコードのドキュメントが作成され、Gloria Rios の受信ボックスに送信されます。 Gloria は提出された請求を確認し、請求を承諾または却下することができます。

### 動作を確認 {#see-for-yourself}

AEMインボックスには、https://&lt; からアクセスできます。***hostname***>:&lt;***PublishPort***>/content/we-finance/global/en/login.html?resource=/aem/inbox.html. Gloria Rios のユーザー名とパスワードとして grios/password を使用してAEM Inbox にログインし、FOIS リクエストを確認します。

Gloria はリクエストを開き、FOIA リクエストの詳細を調べます。 要求の詳細を確認し、必要なドキュメントを提供する実行可能性を確認した後、Gloria は要求を承認します。

![gloriariosapproves](assets/gloriariosapproves.png)

## Sarah は、要求が承認されたという通知を受け取ります {#sarah-receives-notification-that-her-request-is-approved}

Gloria が FOIA の申請を承認した後、Sarah は申請が承認されたことを知らせる電子メールを受信します。 また、電子メールには、ドキュメントを提供するための暫定的なタイムラインに関する情報と、リクエストのフォローアップに関する連絡先の詳細も含まれています。

![sarahroseemailapproval](assets/sarahroseemailapproval.png)
