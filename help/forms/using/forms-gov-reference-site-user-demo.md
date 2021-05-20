---
title: We.GovおよびWe.Financeリファレンスサイトのチュートリアル
seo-title: We.GovおよびWe.Financeリファレンスサイトのチュートリアル
description: 架空のユーザーとグループを使用して、We.GovおよびWe.Financeのデモパッケージを使用してAEM Formsのタスクを実行します。
seo-description: 架空のユーザーとグループを使用して、We.GovおよびWe.Financeのデモパッケージを使用してAEM Formsのタスクを実行します。
uuid: 797e301a-36ed-4bae-9ea8-ee77285c786d
contentOwner: anujkapo
discoiquuid: ddb3778b-be06-4cde-bc6e-0994efa42b18
docset: aem65
exl-id: 288d5459-bc69-4328-b6c9-4b4960bf4977
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2548'
ht-degree: 1%

---

# We.GovおよびWe.Financeリファレンスサイトのチュートリアル{#we-gov-reference-site-walkthrough}

## 前提条件 {#pre-requisites}

[We.GovおよびWe.Financeのリファレンスサイト](../../forms/using/forms-install-configure-gov-reference-site.md)の設定の説明に従って、リファレンスサイトを設定します。

## ユーザーストーリー{#user-story}

* AEM Forms

   * 自動フォーム変換
   * オーサリング
   * フォームデータモデル/データソース

* AEM Forms

   * データキャプチャ
   * （オプション）データ統合(MS Dynamics)
   * （オプション）Adobe Sign

* ワークフロー
* 電子メール通知
* （オプション）顧客とのコミュニケーション

   * 印刷チャネル
   * Web チャネル

* Adobe Analytics
* データソースの統合

### 架空のユーザーとグループ{#fictitious-users-and-groups}

We.Govデモパッケージには、次の組み込みの架空のユーザーが含まれています。

* **綾丹**:官庁の送達を受ける資格を有する国民

![架空のユーザー](/help/forms/using/assets/aya_tan_new.png)

* **ジョージ・ラング**:We.Gov Agencyビジネスアナリスト

![架空のユーザー](/help/forms/using/assets/george_lang.png)

* **カミラ・サントス**:We.Gov Agency CXリード

![架空のユーザー](/help/forms/using/assets/camila_santos.png)

次のグループも含まれます。

* **We.Gov Forms Users**

   * ジョージ・ラング（メンバー）
   * カミラ・サントス（メンバー）

* **We.Govユーザー**

   * ジョージ・ラング（メンバー）
   * カミラ・サントス（メンバー）
   * 綾丹（メンバー）

### デモ概要用語の凡例{#demo-overview-terms-legend}

1. ****&#x200B;として実行：AEMデモでユーザーとグループを定義しました。
1. **ボタン**:ナビゲーション用の色付きの長方形または丸い矢印。
1. ****&#x200B;をクリックします。ユーザストーリー内でアクションを実行する。
1. **リンク**:We.Govサイトのメインメニューの上部にあります。
1. **ユーザーの手順**:ユーザーのストーリーをナビゲートする際に従う一連の数値ステップ。
1. **Formsポータル**: *https://&lt;aemserver>:&lt;port>/content/we-gov/formsportal.html*
1. **モバイルビュー**:We.Govユーザー。再サイズのブラウザーでモバイルビューを複製します。
1. **デスクトップ表示**:We.govユーザーがノートパソコンまたはデスクトップでデモを表示。
1. **スクリーン前のフォーム**:We.Govサイトのホームページのフォーム。
1. **アダプティブフォーム**:We.govデモの登録申込フォーム。

   *https://&lt;aemserver>:&lt;port>/content/forms/af/adobe-gov-forms/enrollment-application-for-health-benefits.html*

1. **AdobeWe.Govサイト**: *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html*
1. **Adobeインボックス**:AEMバックエンドの上部のメニ [ューバ](assets/bell.svg) ーBellアイコン。

   *https://&lt;aemserver>:&lt;port>/aem/start.html*

1. **電子メールクライアント**:Eメールを表示する推奨方法(Gmail、Outlook)
1. **CTA**:行動喚起
1. **移動**:ブラウザページ上で特定の参照点を見つけるには
1. **AFC**:automated forms conversion

## automated forms conversion（カミラ） {#automated-forms-conversion}

**この節**:Camila CX Leadは、紙ベースのプロセスの一部として使用された既存のPDFベースのフォームを持っています。最新化の取り組みの一環として、SarahはこのPDFフォームを使用して、新しい最新のアダプティブFormsを自動的に作成したいと考えています。

### automated forms conversion- We.Gov (Camila) {#automated-forms-conversion-wegov}

1. *https://&lt;aemserver>:&lt;port>/aem/start.html*&#x200B;に移動します。

1. ログイン方法：
   * **ユーザー**:camila.santos
   * **パスワード**：password
1. メインページから、Forms/Formsとドキュメント/AEM Forms We.gov Forms/AFCを選択します。
1. CamilaはPDFをAEM Formsにアップロードします。

   ![フォームのアップロード](assets/aftia-upload-form.jpg)

1. 次に、CamillaがPDFフォームを選択し、「**自動変換を開始**」をクリックして変換プロセスを開始します。 フォームを変換した場合は、「**変換後の値を上書き**」をクリックする必要が生じる場合があります。

   >[!NOTE]
   >
   >AFCの設定は、エンドユーザーに対して事前に設定されています。つまり、変更しないでください。

   * **オプション**:アクセシブルなUltramarineテーマを使用する場合は、「アダプティブフォームのテーマを指定」をクリックし、オプションのリストに表示されるAccessible-Ultramarineテーマを選択します。

   ![変換の開始](assets/aftia-start-conversion.jpg)

   ![Ultramarine テーマ](assets/aftia-upload-conversion-settings.jpg)

   コンバージョン中に完了率のステータスが表示されます。 ステータスに「**変換済み**」と表示されたら、「**出力**」フォルダーをクリックし、アダプティブフォームを選択して「**編集**」をクリックし、変換後のフォームを開きます。

1. Camillaはフォームをレビューし、すべてのフィールドが存在することを確認します

   ![変換のレビュー](assets/aftia-review-conversion.jpg)

1. Camillaがフォームの編集を開始します。 Sarahは、「パネルレイアウト」ドロップダウンメニューから「ルートパネル/編集（レンチ） 」を選択し、「チェック」ボックスを選択します。

   ![プロパティの確認](assets/aftia-review-properties.jpg)

1. 次に、必要なCSSとフィールドの変更をすべて追加して最終製品を作成します。

   ![CSSを追加](assets/aftia-add-css.jpg)

### フォームデータモデルとデータソース(Camila) {#data-sources}

**この節**:ドキュメントが変換されてアダプティブフォームが作成されたら、Camilaはアダプティブフォームをデータソースに接続する必要があります。

1. [Automated forms conversion- We.Gov](#automated-forms-conversion-wegov)で変換されたフォームのプロパティが開きます。

1. 次に、「次から選択」ドロップダウンから「フォームモデル」>「フォームデータモデルを選択」を選択し、「次のリストからWe.gov登録FDMを選択」を選択します。

1. 「保存して閉じる」ボタンのクリック数。

   ![FDMの選択](assets/aftia-select-fdm.jpg)

1. Camilaは&#x200B;**output**&#x200B;フォルダーをクリックし、アダプティブフォームを選択して「**編集**」をクリックし、完成したWe.Govフォームを開きます。
1. Camilaはアダプティブフォームフィールドを選択し、![設定アイコン](assets/configure-icon.svg)をクリックします。 Sarahは、「**参照をバインド**」フィールドを使用して、フォームデータモデルエンティティとの連結を作成します。 アダプティブフォーム内のすべてのフィールドに対して、この手順を繰り返します。

### フォームアクセシビリティテスト(Camila) {#form-accessibility-testing}

また、Camilaは、作成されたコンテンツが企業の標準に従って正しく完全にアクセス可能に構築されていることを検証します。

1. Camilaは&#x200B;**output**&#x200B;フォルダーをクリックし、アダプティブフォームを選択して「**プレビュー**」をクリックし、完成したWe.Govフォームを開きます。

1. Chrome Developer Tool内で「監査」タブを開きます。

1. アダプティブフォームを検証するために、アクセシビリティチェックを実行します。

   ![アクセシビリティチェック](assets/aftia-accessibility.jpg)

## アダプティブフォームモバイルビューデモ(Aya) {#mobile-view-demo}

**この節は、デモの前に実行する必要があります。**

**ユーザーの手順：**

1. 次の場所に移動します。*https://&lt;aemserver>:&lt;port>/content/we-gov/home.html*
1. ログイン方法：

   1. **ユーザー**:aya.tan
   1. **パスワード**：password

1. ブラウザーウィンドウのサイズを変更するか、ブラウザーのエミュレーターを使用してモバイルデバイスのサイズを複製します。

### We.Gov Website (Aya) {#aya-user-story-we-gov-website}

![架空のユーザー](/help/forms/using/assets/aya_tan_new-1.png)

**この節**:綾は市民だ。彼女は友人から、政府機関からサービスを受ける資格があるかもしれないと聞いた。 Ayaは、携帯電話からWe.GovのWebサイトにアクセスし、彼女が受ける資格のあるサービスに関する詳細を学びます。

### We.Govプリスクリーン(Aya) {#aya-user-story-we-gov-pre-screener}

Ayaは、携帯電話で短いアダプティブフォームに入力して適格性を確認するための質問に回答します。

**ユーザーの手順：**

1. 各ドロップダウンフィールドで選択を行います。

   >[!NOTE]
   >
   >年間200,000ドルを超える収益を上げるユーザーは、資格を持ちません。

1. 「**Am I Eligible?**” button.
1. 「**今すぐ適用**」ボタンをクリックして次に進みます。

   ![「今すぐ適用」リンク](/help/forms/using/assets/apply_now_link.png)

### We.Govアダプティブフォーム(Aya) {#aya-user-story-we-gov-adaptive-form}

綾さんは資格があることを知り、モバイルデバイスでサービスをリクエストする申し込みを始めます。

Ayaは、サービスリクエストの申し込みを完了する前に、自宅でいくつかのドキュメントを確認する必要があります。 Sarahはモバイルデバイスからアプリを保存し、終了します。

**ユーザーの手順：**

1. 「基本情報」フィールドに入力します。以下は必須フィールドとドロップダウンです。

   1. 基本情報

      1. firstName
      1. 姓
      1. 生年月日
      1. 電子メール

1. 次の&#x200B;**動的ロジック**&#x200B;を使用して、**ファミリステータス**&#x200B;ドロップダウンを使用して動的機能を示します。

   1. **単一**:キンパネルの次に表示
   1. **既婚**:婚姻状況に応じたパネルを表示
   1. **離婚**:キンパネルの次に表示
   1. **妻**:キンパネルの次に表示
   1. **子供は？**:（はい/いいえ）子依存パネルを表示するラジオボタン。

      1. （追加/削除）ボタンを使用して、複数の子依存パネルを追加/削除します。

1. 灰色のメニューバーの右向き矢印をクリックします。
1. 下部にある「保存」ボタンをクリックします。

   ![アダプティブフォームの詳細](/help/forms/using/assets/adaptive_form.png)

## デスクトップデモ{#desktop-demo}

**この節：** 自宅に戻ると、Ayaは彼女が必要とする情報を見つけ、デスクトップからアプリケーションを再開します。Ayaはオンラインフォームポータルに移動し、申込を再開します。 一部のシンプルなカスタマイズ機能を使用すると、エージェントは自動的にアプリを再開するためのリンクを生成し、電子メールで送信することもできます。

### 続きアダプティブフォーム(Aya) {#aya-user-story-continued-adaptive-form}

**ユーザーの手順：**

1. *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html*&#x200B;に移動します。
1. ナビゲーションバーで、「**Online Services**」をクリックします。
1. 「ドラフトForms」パネルから、既存の「健康保険の登録申請」を選択します。

   ![健康給付の登録申請](/help/forms/using/assets/enrollment_application.png)

   ルックアンドフィールは同じで、データを再入力する必要はありません。

   **ユーザーの手順：**

1. 右側の円CTAをクリックして、次のセクションに移動します。

   ![右円CTA](/help/forms/using/assets/right_circle_cta_new.png)

   フォームは、Ayaの最後のエントリの時点まで入力されます。 亜矢は彼女の情報をすべて入力し、提出する準備ができている。

   ![アダプティブフォームを送信する](/help/forms/using/assets/submit_adaptive_form.png)

   >[!NOTE]
   >
   >Ayaが電話番号フィールドに入力する場合、ダッシュ、スペース、ハイフンを含まない、連続した11桁の数字で入力する必要があります。

   亜矢が送られた後、Thank Youページが届きます。 必要に応じて、Adobe Signで電子署名用の電子メールも受け取ります。

### オプション：Adobe Sign（綾） {#adobe-sign}

**ユーザーの手順：**

1. 電子メールクライアントに移動し、Adobe Sign電子メールを探します。
1. Adobe Signへのリンクをクリックします。

   ![Adobeサインリンク](/help/forms/using/assets/adobe_sign_link.png)

**ユーザーの手順：**

1. 「**I agree**」ボックスをオンにします。
1. 「**受け入れ**」をクリックします。
1. レビュー済みのドキュメントの下部までスクロールします。
1. 強調表示された黄色のタブをクリックして、ドキュメントに署名します。

   ![ドキュメントに署](/help/forms/using/assets/sign_document_new.png) ![名するテストドキュメントに署名する](/help/forms/using/assets/sign_test_document.png)

## 政府エージェント(George) {#government-agent-george}

![ジョージ政府代理](/help/forms/using/assets/george_lang-1.png)

**本節：** Georgeは、政府機関Ayaのビジネスアナリストで、サービスを要請しています。ジョージは1つのダッシュボードを持っていて、レビュー用に割り当てられたサービスリクエストのアプリケーションをすべて確認できます。

### AEM Inbox(George) {#george-user-story-aem-inbox}

**ユーザーの手順：**

1. *https://&lt;aemserver>:&lt;port>/aem/start.html*&#x200B;に移動します。
1. ユーザーアイコン（右上隅）をクリックし、「**ログアウト**」または「**次のユーザーとして動作**」メニューオプションを使用します。

   1. ログイン方法：

      1. **ユーザー：** george.lang
      1. **パスワード：** password
   1. または次のユーザーとして実行：

      1. 「**次のユーザーとして実行**」フィールドに&quot;**George**&quot;と入力します。

      1. 「 OK 」をクリックして、別のユーザーとして実行します。


1. 右上隅にある通知（ベル）アイコンをクリックします。
1. 「**すべて表示**」をクリックして、インボックスに移動します。
1. インボックスから、最新の「**Health Benefits Application Review**」タスクを開きます。

   ![ヘルス・メリット・アプリケーション・レビュー](/help/forms/using/assets/health_benefits.png)

### オプション：AEM Inbox &amp; MS Dynamics(George) {#george-user-story-aem-inbox-and-ms-dynamics}

データ統合と自動ワークフローのおかげで、Ayaのアプリケーションが表示され、データの送信時に自動的に生成されたCRMレコードも表示されます。

**ユーザーの手順：**

1. 読み取り専用のアダプティブフォームを開き、検査します。
1. 「**Open MS Dynamics**」ボタンをクリックして、新しいウィンドウでMS Dynamicsレコードを開きます。
1. CRMでは、すべての情報を更新できます

   1. 必要に応じて、Dynamicsに直接レビューノートを追加します。

1. 閉じて、AEM Inboxに戻ります。

   ![MS Dynamicsレコード](/help/forms/using/assets/ms_dynamics.png)

### AEM Inbox(George)に戻る{#george-user-story-back-to-aem-inbox}

ジョージはAyaの申し込みを承認し、既存の自動化されたワークフローのおかげで、Ayaにも確認のEメールが送信されます。

**ユーザーの手順：**

1. 左上隅に移動し、「**承認**」をクリックして、アプリを承認します。
1. モーダルには、CXリードに関するメッセージを残すことができます。
1. 「完了」をクリックします。
1. （市民の役割） Eメールクライアントを開いて、Ayaに送信されたEメールを表示します。

   ![綾に送信されたEメールを表示する](/help/forms/using/assets/email_client.png)

## CXリード(Camila) {#cx-lead-camila}

![Camila（CXリード）](/help/forms/using/assets/camila_santos-1.png)

**この節：** Camila the CX Leadは、Ayaに対して歓迎の電話を設定し、彼女が承認された政府サービスの利用方法を説明します。

### （オプション） AEM Inbox &amp; MS Dynamics {#camila-user-story-aem-inbox-ms-dynamics}

**ユーザーの手順：**

1. *https://&lt;aemserver>:&lt;port>/aem/start.html*&#x200B;に移動します。
1. ユーザーアイコン（右上隅）をクリックし、「**ログアウト**」または「**次のユーザーとして動作**」メニューオプションを使用します。

   1. ログイン方法：

      1. **ユーザー**:camila.santos
      1. **パスワード**：password
   1. または次のユーザーとして実行：

      1. 「**次のユーザーとして実行**」フィールドに&quot;**Camila**&quot;と入力します。

      1. 「 OK 」をクリックして、別のユーザーとして実行します。


1. 右上隅にある通知（ベル）アイコンをクリックします。
1. 「**すべて表示**」をクリックして、インボックスに移動します。
1. インボックスから、最新の「**新しい連絡先の承認**」タスクを開きます。

![新しい連絡先の承認](/help/forms/using/assets/new_contact_approval.png)

**（オプション）ユーザーの手順：**

1. 読み取り専用のアダプティブフォームを開き、検査します。
1. 「**Open MS Dynamics**」ボタンをクリックして、新しいウィンドウでMS Dynamicsレコードを開きます。
1. CRMでは、すべての情報を更新できます

   1. 必要に応じて、新しい呼び出しアクティビティをDynamicsに直接追加します。
   1. 「**アクティビティ**」セクションを開きます。
   1. 「**新しい電話**」オプションをクリックします。
   1. 電話の詳細を追加します。
   1. ウィンドウを保存して閉じます。

1. AEMに戻り、左上隅に移動し、「**送信**」をクリックして申込を送信します。
1. モーダルでは、メッセージを残すことができます。
1. 「完了」をクリックします。

   ![「アクティビティ」](/help/forms/using/assets/activities_tab.png) ![タブ新しい連絡先の確認](/help/forms/using/assets/confirm_new_contact.png)

## （オプション）ウェルカムキット市民(Aya) {#welcome-kit-citizen-aya}

**この節：** Ayaは、Eメールを受信します。Eメールには、Ayaの利点をまとめ、入力するフォームフィールドも含まれるインタラクティブ通信へのリンクが含まれます。PDFの特典明細書を添付し、メール内のインタラクティブ通信レターにリンクします（インタラクティブ通信と同じテーマ/ブランディングを使用）。

### 電子メールクライアント通知(Aya) {#aya-user-story-email-client}

**ユーザーの手順：**

1. ウェルカムキットの電子メールを探して開きます。
1. ページ下部のPDF添付ファイルまでスクロールします。
1. PDF添付ファイルをクリックして開きます。
1. Eメールクライアントで上にスクロールし、「**ウェルカムキットをオンラインで表示**」をクリックします。

   1. 同じドキュメントのWebチャネルバージョンが開きます。

1. PDFを直接参照するには：

   *https://&lt;aemserver>:&lt;port>/aem/formdetails.html/content/dam/formsanddocuments/adobe-gov-forms/welcome-handbook/we-gov-welcome-handbook*

1. ICを直接参照するには：

   *https://&lt;aemserver>:&lt;port> /content/dam/formsanddocuments/adobe-gov-forms/welcome-handbook/we-gov-welcome-handbook/jcr:content?channel=web&amp;mode=preview&amp;wcmmode=disabled*

   ![ウェルカム特典ハン](/help/forms/using/assets/welcome_benefits_handbook.png) ![ドブックインタラクティブ通信リンク](/help/forms/using/assets/interactive_communication.png)

## 更新リマインダー市民(Aya) {#renewal-reminder-citizen-aya}

**この節：** Camilaは、1年後に通信リマインダーのスケジュールも設定します。（電子メールを自動化/実行するワークフローステップ）。

### 電子メールクライアント通知(Aya) {#aya-user-story-email-client-updated}

**ユーザーの手順：**

1. 電子メールクライアントに移動します。
1. 更新リマインダーの電子メールを探して開きます。
1. 「**新しいアプリケーションを送信**」ボタンをクリックして、アダプティブフォームを開きます。

   1. このセクションは、フェーズ2でのデータの事前入力をサポートするために、意図的に空のままにしています。

   ![更新リマインダー電子メール](/help/forms/using/assets/renewal_reminder_email.png)

## （オプション）フォームデータモデル(Camila) {#form-data-model}

**この節**:CamilaはAEM Formsのデータ統合に移動し、クイックテストを実行して、フォームデータモデル統合を介して外部データソースに送信された情報が実際に存在することを確認できます。

### フォームデータモデル(Camila) {#form-data-model-camila}

**この節**:Camilaはデータソースページに移動し、Derbyデータベース内でサーバーがレプリケートしたデータを検証します。

1. ユーザーエクスペリエンスが完了し、ユーザーの送信が完了したら、CamilaはAEM Forms内の「データソース」タブに移動します(**Forms**/**データ統合**)

1. 次に、AEM Forms **We.gov FDM**&#x200B;を選択し、**We.gov Enrollment FDM**&#x200B;を編集します。

1. 次に、テスト対象の&#x200B;**Contact** > **Read Service**&#x200B;を選択します。

   ![連絡先読み取りサービス](assets/aftia-contact-read-service.jpg)

1. 次に、Camilaは連絡先IDをテストサービスに提供し、「テスト」ボタンをクリックします。 例えば、1または2（フォームを送信した場合）。 フォームを送信していない場合、データは返されません。

   ![連絡先読み取りサービス](assets/aftia-test-service.jpg)

1. その後、データがデータソースに正常に挿入されたことを確認できます。

   * Derby DS内のデータは、次の形式に似ています。

   ```xml
      [
         {
         "ADDRESS_COUNTRY": "USA",
         "LAST_NAME": "Tan",
         "ADDRESS_CITY": "New York",
         "FIRST_NAME": "Aya",
         "ADDRESS_STATE": "AL",
         "ADDRESS_LINE1": "123 Street crescent",
         "GENDER_CODE": "2",
         "ADDRESS_LINE2": "123 Street crescent",
         "ADDRESS_POSTAL_CODE": "90210",
         "BIRTH_DATE": "1991-12-12",
         "CONTACT_ID": 1,
         "MIDDLE_NAME": "M",
         "HAS_CHILDREN_CODE": "0"
         }
   ]
   ```

## （オプション） Analytics(Camila) {#analytics-cx-lead-camila}

**この節：** Camilaは、サービスリクエストフォームの記入と放棄を開始する市民の割合、承認/拒否応答のリクエスト送信から平均時間、市民に送信した福利厚生ハンドブックのエンゲージメント統計など、エージェンシーKPI全体を確認できるダッシュボードに移動します。

### Adobe Analytics Sitesレポート(Camila) {#camila-reviews-sites-reporting-we-gov-adobe-analytics}

1. *https://&lt;aemserver>:&lt;port>/sites.html/content*&#x200B;に移動します。
1. 「**AEM Forms We.Gov Site**」を選択して、サイトのページを表示します。
1. サイトページの1つ（例：ホーム）を選択し、「**Analytics &amp; Recommendations**」を選択します。

   ![分析と推奨事項](/help/forms/using/assets/analytics_recommendation.jpg)

1. このページには、AEM Sitesページに関連するAdobe Analyticsから取得した情報が表示されます(注：デザインにより、この情報はAdobe Analyticsから定期的に更新され、リアルタイムには表示されません)。

   ![Adobe Analytics主要指標](/help/forms/using/assets/analytics_key_metrics.jpg)

1. （手順3.でアクセスした）ページビューページに戻ると、「**リストビュー**」の項目を表示するように表示設定を変更して、ページビュー情報を表示することもできます。
1. 「**表示**」ドロップダウンメニューを探し、「**リスト表示**」を選択します。

   ![表示ドロップダウンメニューのリスト表示](/help/forms/using/assets/list_view_view_dropdown.jpg)

1. 同じメニューから「**設定を表示**」を選択し、「**Analytics**」セクションから表示する列を選択します。

   ![列の表示の設定](/help/forms/using/assets/view_setting_analytics.jpg)

1. 「**更新**」をクリックして、新しい列を使用可能にします。

   ![新しい列を使用可能にする](/help/forms/using/assets/new_columns_available.jpg)

### Adobe Analytics Formsレポート(Camila) {#camila-reviews-forms-reporting-we-gov-adobe-analytics}

1.  に移動します。

   *https://&lt;aemserver>:&lt;port>/aem/forms.html/content/dam/formsanddocuments/adobe-gov-forms*

1. 「**Enrollment Application For Health Benefits**」アダプティブフォームを選択し、「**Analytics Report**」オプションを選択します。

   ![健康給付の登録申請](/help/forms/using/assets/analytics_report_benefits.jpg)

1. ページが読み込まれ、Analyticsレポートデータが表示されます。

   ![Analyticsレポートデータ](/help/forms/using/assets/analytics_report_data_updated.jpg)
