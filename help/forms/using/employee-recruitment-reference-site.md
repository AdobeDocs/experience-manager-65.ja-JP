---
title: 従業員採用リファレンスサイトのチュートリアル
seo-title: 従業員採用
description: AEM Forms リファレンスサイトでは、どのようにして組織が AEM Forms の機能を使用して従業員採用ワークフローを実施しているのかを紹介しています。
seo-description: AEM Forms リファレンスサイトでは、どのようにして組織が AEM Forms の機能を使用して従業員採用ワークフローを実施しているのかを紹介しています。
uuid: 27e456ba-3c08-4c43-ad54-1ba0070995ad
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5f04b13e-ea40-4c86-9168-e020c52435a2
translation-type: tm+mt
source-git-commit: af326f2d2b278fe36df05afc8c172f74c99a064c
workflow-type: tm+mt
source-wordcount: '1435'
ht-degree: 90%

---


# 従業員採用 reference site walkthrough {#employee-recruitment-reference-site-walkthrough}

## 概要 {#overview}

We.Finance 社のリファレンスサイトポータルを使用すると、ユーザーは求人の募集に申し込むことができます。また、このポータルを使用して、候補者の面接スケジュール、ショートリスト、内部通信も管理します。 このサイトでは以下を管理します。

* 求人の検索と申し込みの管理
* 候補者の審査と最終候補者名簿
* 面接プロセス
* 候補者の詳細情報の収集
* 候補者の経歴の確認
* 選考した候補者へのオファーの展開

>[!NOTE]
>
>従業員採用のユースケースは、We.Finance と We.Gov のどちらのリファレンスサイトでもご覧いただけます。チュートリアルで使用する例、画像、説明は、We.Finance のリファレンスサイトを使用しています。ただし、これらのユースケースおよびレビューアーティファクトは We.Gov を使用しても実行できます。これを行うには、記述されている URL で **we-finance** を&#x200B;**we-gov** に置き換えます。

### 含まれているワークフローモデル {#workflow-models-involved}

従業員採用のユースケースには、2 つのワークフローが含まれています。

* 面接前 — We Finance社の従業員募集ワークフロー
* 面接後 — We Finance社員募集ポストインタビューワークフロー

これらのワークフローは、AEM で作成され、次の場所で見つかります。

`https://[authorHost]:[authorPort]/libs/cq/workflow/admin/console/content/models.html/etc/workflow/models/`

#### We Finance 従業員採用ワークフロー {#we-finance-employee-recruiting-workflow}

このドキュメントで後述されている We Finance 従業員採用ワークフローのモデルを以下に示します。

![we-finance-employee-recluiting-workflow](assets/we-finance-employee-recruiting-workflow.png)

#### We Finance 従業員採用面接後ワークフロー {#we-finance-employee-recruiting-post-interview-workflow}

このドキュメントで後述されている We Finance 従業員採用面接後ワークフローのモデルを以下に示します。

![we-finance-employee-recluiting-post-interview-workflow](assets/we-finance-employee-recruiting-post-interview-workflow.png)

### 登場人物 {#personas}

このシナリオでは、以下の人物が登場します。

* Sarah Rose （組織の求人に応募している候補者）
* John Jacobs （人材採用担当者）
* Gloria Rios （採用担当マネージャー）
* John Doe （HR 担当者）

## Sarah が求人に応募 {#sarah-applies-for-a-job}

Sarah Rose は、組織の求人を検索しています。Web ポータルにアクセスして、採用ページの求人リストを検索します。リストから適合する求人を見つけ、それに応募します。

![ホームページ](assets/home-page.png)

We.Finance ホームページ

![キャリアページ](assets/career-page.png)

We.Finance 採用ページ

Sarah は、掲載されている求人の「Apply」（申し込む）をクリックします。求人申込フォームが開きます。応募の詳細をすべて記入して送信します。

![求人申請書](assets/job-application-form.png)

### 仕組み {#how-it-works}

We.Finance ホームページと採用ページは、AEM サイトのページです。採用ページにはアダプティブフォームが埋め込まれており、繰り返し可能なパネルを使用して、サービスを利用している求人を取得し、ページ上に一覧表示します。アダプティブフォームは、で確認でき `https://[authorHost]:[authorPort]/editor.html/content/forms/af/we-finance/employee/recruitment/jobs.html`ます。

### 実際の動作確認 {#see-it-yourself}

に移動し、「 `https://[publishHost]:[publishPort]/content/we-finance/global/en.html` キャリア ****」をクリックします。 「**[!UICONTROL Search]**」（検索）をクリックして求人のリストを表示し、特定の仕事を見つけて「**[!UICONTROL Apply]**」（申し込む）をクリックします。フォームの詳細を記入し、申込書を送信します。

申込書に有効な電子メール ID を指定していることを確認してください。このチュートリアルで行われるすべての通信は、指定した電子メール ID を使用して行われます。

## John Jacobs は Sarah Rose のプロファイルを採用担当マネージャーの最終候補者名簿に記載 {#john-jacobs-shortlists-sarah-rose-s-profile-for-the-hiring-manager-s-screening}

Sarah によって送信された求人の申込書を組織が受信します。John Jacobs （採用担当者）は Sarah のプロファイルのレビューを割り当てられます。彼は AEM インボックスでプロファイルをレビューし、プロファイルが求人要件を満たしていることを確認して、「Shortlist」（最終候補者名簿）をクリックします。Sarah のプロファイルは採用マネージャーである Gloria Rios に転送され、承認を受けます。

![jjacobs-inbox-1](assets/jjacobs-inbox-1.png)

John の AEM インボックス

![候補者候補者リスト](assets/candidate-shortlist.png)

John Jacobs は、Sarah Rose のプロファイルを採用担当マネージャーの最終候補者名簿に追加

**仕組み**

求人申込フォームの送信アクションは、John Jacob のインボックスに申込書の審査タスクを作成するワークフローをトリガーします。John がレビューして申込書を最終候補者名簿に追加すると、ワークフローによって採用担当マネージャーである Gloria のインボックスにタスクが作成されます。

### 実際の動作確認 {#see-it-yourself-1}

Go to `https://[publishHost]:[publishPort]/content/we-finance/global/en/login.html?resource=/aem/inbox.html`and log in using jjacobs/password as username/password for John Jacobs. 候補者のプロファイルをレビューするタスクを開き、申込者を最終候補者名簿に追加します。

## Gloria が申込書をレビューし、申込者の面接を承認 {#gloria-reviews-the-application-and-approves-the-applicant-for-an-interview}

採用担当マネージャーである Gloria は、最終候補者名簿のプロファイルをタスクとして AEM インボックスに受信します。彼女は審査を行い、候補者である Sarah Rose の面接を承認します。

![ガラス箱](assets/gloriainbox.png)

Gloria の AEM インボックス

![gloriascheduleinterview](assets/gloriaschedulesinterview.png)

Gloria は Sarah Rose の面接を承認

**仕組み**

Gloria が候補者の面接を承認すると、ワークフローは We.Finance の採用担当者である John Doe の AEM インボックスにタスクを作成します。

### 実際の動作確認 {#see-it-yourself-2}

Go to `https://[publishHost]:[publishPort]/content/we-finance/global/en/login.html?resource=/aem/inbox.html` and log in using jjacobs/password as username/password for John Jacobs. 候補者のプロファイルをレビューするタスクを開き、申込者を最終候補者名簿に追加します。

Go to `https://[publishHost]:[publishPort]/content/we-finance/global/en/login.html?resource=/aem/inbox.html` and log in using grios/password as username/password for Gloria Rios. 候補者のプロファイルをレビューするタスクを開き、「Schedule Interview」（面接のスケジュール）をクリックします。

## John Doe が面接をスケジュール {#john-doe-schedules-an-interview}

John Doe は、インボックスに面接のスケジュールのタスクを受信します。John Doe はそのタスクを選択して開き、面接日時、場所、そして面接担当の HR を John Jacob に指定します。John Doe は「Send Invitation Email」（招待メールの送信）をクリックします。電子メールが Sarah に送信され、Sarah の面接タスクが採用担当マネージャーである Gloria に割り当てられます。

![johnjacobsaeinbox](assets/johnjacobsaeminbox.png)

John Doe の AEM インボックス

![johndoesscheduleinterview](assets/johndoescheduleinterview.png)

John Doe が面接をスケジュールし詳細を Sarah Rose に送信

## Sarah Rose は面接スケジュールが記載された電子メールを受信 {#sarah-rose-receives-the-email-with-interview-schedule}

Sarah Rose は、面接スケジュール、場所、およびその他の詳細が記載された電子メールを受信します。「Accept」（承諾）をクリックし、面接のスケジュールと場所について承諾します。詳細情報に従い、Sarah は面接に対応します。

![sarahroseinterviewemail](assets/sarahroseinterviewemail.png)

Sarah Rose が面接スケジュールを受信

## 面接後、採用担当マネージャーは Sarah Rose を最終候補者名簿に記載 {#after-the-interviews-the-hiring-manager-shortlists-sarah-rose}

Sarah Rose が面接を受けて合格すると、採用担当マネージャーである Gloria Rios は自分のインボックスから候補者選択タスクを開いて「Select」（選択）をクリックします。Gloria Rios の判断は HR 担当者である John Doe に伝達され、さらに処理が進められます。

![gloriarisinboxoffer](assets/gloriariosinboxoffer.png)

Gloria の AEM インボックス

![栄光選択候補](assets/gloriariosselectcandidate.png)

面接後、Gloria Rios は Sarah Rose を選択

## John Doe が詳細情報を要求 {#john-doe-requests-more-information}

候補者に組織への採用を通知する前に、経歴を確認する必要があります。John Doe は選択した応募者の詳細情報を開いて確認し、学歴と職歴の一部がまだ入力されていないことに気づきます。John Doe は、「Need More Information」（詳細情報が必要）をクリックします。

![johndoeinbox](assets/johndoeinbox.png)![johndoeneedmoreinformation](assets/johndoeneedmoreinformation.png)

John Doe は、Sarah Rose に学歴と職歴について詳細情報を要求

## Sarah Rose はさらに情報を求める電子メールを受信 {#sarah-rose-receives-an-email-requesting-further-information}

Sarah Rose は、申し込みの手続きを進めるには、さらに情報が必要であることを通知する電子メールを受信します。電子メールには、必要な情報の入力のためのリンクが含まれています。

![sarahrosemailmoredetails](assets/sarahroseemailmoredetails.png)

Sarah Rose は、申し込みの手続きを進めるにはさらに情報が必要であることを通知する電子メールを受信

Sarah は、電子メールの「Provide Details」（詳細を入力）リンクをクリックします。フォームが表示されます。Sarah は、John Doe が要求する学歴と職歴の詳細を入力し、「Submit」（送信）をクリックします。

![additionalinformation1](assets/additionalinformation1.png)

Sarah が電子メールのリンクをクリックし、追加情報フォームを開く

![additionalinformation2](assets/additionalinformation2.png)

Sarah は John Doe の要求に従って追加情報を入力し、「Submit」（送信）をクリック

## John Doe が選択した候補者プロファイルの追加情報を確認 {#john-doe-reviews-the-selected-candidate-profile-for-the-additional-information-provided}

John Doe は、候補者審査要求を選択して、開きます。John Doe は、Sarah が必要に応じてすべての情報を入力したことを確認します。申請書をレビューした後、John Doe は「Approve」（承認）をクリックします。John Doe の承認を受けて、Sarah Rose の経歴チェックの要求が John Jacobs に転送されます。

![johndoeadditioninformationinbox](assets/johndoeadditionainformationinbox.png)

John Doe の AEM インボックス

![johndoeadditioninformationreview-copy](assets/johndoeadditionalinformationreview-copy.png)

John Doe が Sarah により入力された追加情報を見直して承認

## John Jacobs が経歴チェック要求を受信 {#john-jacobs-receives-a-background-check-request}

John Jacobs は自分のインボックスに経歴チェック要求を確認します。John Jacobs はタスクを開いて、Sarah Rose の入力した情報を確認します。経歴チェックの実行後、John Jacobs は「Go Ahead」（続行）をクリックして、経歴チェックが完了したことを通知します。

![johnjaccobvisiongroundcheckinbox](assets/johnjacobsbackgroundcheckinbox.png)

John Jacobs の AEM インボックス

![johnjaccobvisiongroundcheckgoad](assets/johnjacobsbackgroundcheckgoahead.png)

経歴チェックの実行後、John Jacobs は「Go Ahead」（続行）をクリック

## John Doe は採用通知を Sarah Rose に送信 {#john-doe-sends-out-the-joining-letter-to-sarah-rose}

John Doe は、AEM インボックスに採用通知の送信要求を受信します。John はその要求を開いて詳細を確認します。John Doe は、採用通知の PDF を添付して、「Attach &amp; Send Joining Letter」（採用通知の添付と送信）をクリックします。

![johndojoiningletterinbox](assets/johndoejoiningletterinbox.png)

John Doe の AEM インボックス

![johndojoiningletterattachandsend](assets/johndoejoiningletterattachandsend.png)

John Doe は署名を求める採用通知を送信

## Sarah Rose が受信して採用通知に署名 {#sarah-rose-receives-and-signs-the-joining-letter}

Sarah Rose が署名を求める採用通知を受信します。Sarahは「ここをクリックしてレターに参加中」をクリックし、確認して署名します。 署名するフィールドのある採用通知の PDF が開きます。

![sarahrosejoiningletteremail](assets/sarahrosejoiningletteremail.png)

Sarah Rose が署名を求める採用通知を受信

Sarah は、手入力、描画による手書き、署名画像の挿入、またはモバイル機器のタッチスクリーンでの描画のいずれかによって署名できます。名前を入力し、「Click to Sign」をクリックして、Sarahが参加するレターの署名済みコピーをダウンロードします。

![sarahrosejoininglettersign](assets/sarahrosejoininglettersign.png)

Sarah は自分の名前を入力し、採用通知に署名

![sarahrosejoininglettersign2](assets/sarahrosejoininglettersign2.png)

Sarah は「Click To Sign」（クリックして署名）をクリックし、採用通知への署名を完了

