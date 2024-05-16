---
title: We.Gov リファレンスサイトの FOIA チュートリアル
description: We.Gov リファレンスサイトのウォークスルーでは、情報公開法に基づいて個人から請求された情報の受け取りと開示を、どのように官公庁が AEM Forms を使用して行っているかを説明しています。
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 57b5ce89-6b01-4087-a485-6d9696f06378
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '842'
ht-degree: 100%

---

# We.Gov リファレンスサイトの情報公開法ウォークスルー {#we-gov-reference-site-foia-walkthrough}

## リファレンスサイトの情報公開法のシナリオ {#reference-site-freedom-of-information-act-scenario}

We.Gov は、養子縁組をした場合に養親がチャイルドサポートの申込を行う公的機関です。We.Gov では、情報公開法に基づき、養親が下記の政府機関に情報を請求することが許可されています。

* アメリカ国防兵站局
* 国防総省監察総監室
* 司法省情報政策室
* 海軍省
* 環境保護庁

情報公開法について詳しくは、[https://www.foia.gov/](https://www.foia.gov) を参照してください。

このシナリオでは、次の人物が登場します。

* Sarah Rose（情報の請求者）
* John Jacobs（請求を処理し適切な部門へ転送する担当者）
* Gloria Rios（請求に応じて情報を提供する政府機関職員）

## Sarah が情報公開法に基づいて情報の請求を開始 {#sarah-initiates-request-for-information-under-foia}

情報公開法に基づいて、Sarah は児童・家庭援護庁の 2013 年度から 2016 年度までの訴訟の記録の写しを請求します。Sarah はこの請求を司法省情報政策室に送信し、印刷費と郵送費として最大 100 米ドルを支払うことを表明します。

### 仕組み {#how-it-works}

### 実際の動作確認 {#see-it-yourself}

ブラウザーで、`https://<hostname>:<PublishPort>/wegov` を開きます。We.Gov サイトで、申請／すべての申請を選択します。「すべての申請」ページの「情報公開法の請求申請」で「申請」を選択します。

## Sarah が情報公開法に基づいて申請を開始 {#sarah-starts-her-application-for-information-under-foia}

Sarah は「**申請**」をクリックし、「情報公開法請求フォーム」ページで次を含む情報を入力します。

* **機関**：Sarah は、請求先の機関として「司法省 - 情報政策局」を指定します。

* **最大支払額**：Sarah は、印刷費と郵送費として最大 100 米ドルを支払う意思があることを記入します。
* **請求内容の詳細**：Sarah は「児童・家庭援護庁の 2013 年度から 2016 年度までの訴訟の記録の写しの請求」と記入します。

![児童・家庭援護庁の 2013 年度から 2016 年度までの訴訟の記録の写しの請求](assets/sarahfiosform.png)

児童・家庭援護庁の 2013 年度から 2016 年度までの訴訟の記録の写しの請求

Sarah はいつでも「**保存**」を選択してフォームの下書きを保存し、後でフォームに戻って入力して送信することができます。Sarah はフォームを送信します。

>[!NOTE]
>
>メールからの再開ワークフローは、ログインしたユーザーに対してのみ機能します。リファレンスサイトのシナリオで、Sarah Rose というユーザーが追加されていることを確認します。Sarah のログイン資格情報は `srose/password` です。

## John Jacobs が申請書を受信および承認 {#john-jacobs-receives-and-approves-the-application}

John Jacobs が請求を受け取り、適切な担当者に送ります。AEM インボックスを使用すると、John は送信されたすべての申請書を 1 か所で表示できます。

### 仕組み {#how-it-works-1}

Sarah が情報公開法の申請書に記入して送信すると、申請のレコードが John Jacobs のインボックスに送信されます。John Jacobs は、送信された申請書を表示し、承認または却下できます。

### 動作を確認 {#see-it-yourself-1}

次の場所で AEM インボックスにアクセスできます：https://&lt;***hostname***>:&lt;***PublishPort***>/content/we-finance/global/en/login.html?resource=/aem/inbox.htmlJohn Jacobs のユーザー名とパスワード（jjacobs／password）を使用して AEM インボックスにログインし、情報公開法の申請を確認します。Forms 中心のワークフロータスクで AEM インボックスを使用する方法について詳しくは、「[AEM インボックスでの Forms アプリケーションとタスクの管理](/help/forms/using/manage-applications-inbox.md)」を参照してください。

![johnjacobs](assets/johnjacobs.png)

John Jacobs は申請ダッシュボードから申請書を表示し、承認または却下できます。John Jacobs は申請の詳細を選択して開き、確認した後、承認します。

![johnjacobstaskdetail-1](assets/johnjacobstaskdetail-1.png)

### <strong>Sarah が承認メールを受信</strong> {#strong-sarah-receives-an-acknowledgement-email-strong}

John Jacobs がアプリケーションを承認した後、Sarah は We.Gov サイトから承認メールを受け取ります。Sarah は、アプリケーションの処理にかかる料金と時間について通知を受けます。メールには、Sarah がアプリケーションに関する最新情報を得るために連絡できるメールと電話の詳細も含まれています。

![sarahroseemail](assets/sarahroseemail.png)

## Gloria は第 2 レベルの承認を求める FOIA のリクエストを受信 {#gloria-receives-the-foia-request-for-second-level-approval}

John Jacobs が必要な情報を入力し、Sarah のリクエストを承認した後、Gloria Rios が最終承認を行います。Gloria は添付されたレコードのドキュメントをレビューし、リクエストを承認します。

![gloriariosinbox](assets/gloriariosinbox.png)

### 仕組み {#how-it-works-2}

John Jacobs が FOIA リクエストを承認すると、アプリケーションの PDF またはレコードのドキュメントが作成され、Gloria Rios のインボックスに送信されます。Gloria は提出された請求を確認し、請求を承諾または却下することができます。

### 動作を確認 {#see-for-yourself}

次の場所で AEM インボックスにアクセスできます：https://&lt;***hostname***>:&lt;***PublishPort***>/content/we-finance/global/en/login.html?resource=/aem/inbox.htmlGloria Rios のユーザー名とパスワード（grios/password）を使用して AEM インボックスにログインし、FOIS のリクエストを確認します。

Gloria はリクエストを開き、FOIA リクエストの詳細を調べます。リクエストの詳細をレビューし、必要なドキュメントを提供できるかどうかを確認した後、Gloria はリクエストを承認します。

![gloriariosapproves](assets/gloriariosapproves.png)

## Sarah が、リクエストが承認されたという通知を受信 {#sarah-receives-notification-that-her-request-is-approved}

Gloria が FOIA のリクエストを承認した後、Sarah はリクエストの承認を通知するメールを受け取ります。このメールには、ドキュメントを提出するための暫定的なスケジュールと、リクエストのフォローアップのための連絡先の詳細に関する情報も含まれています。

![sarahroseemailapproval](assets/sarahroseemailapproval.png)
