---
title: We.Gov および We.Finance リファレンスサイトのウォークスルー
seo-title: We.Gov and We.Finance reference site walkthrough
description: We.Gov と We.Finance のデモパッケージを使用した AEM Forms のタスクを、架空のユーザーとグループを使用して実行します。
seo-description: Use fictitious users and groups to perform AEM Forms tasks using We.Gov and We.Finance demo package.
uuid: 797e301a-36ed-4bae-9ea8-ee77285c786d
contentOwner: anujkapo
discoiquuid: ddb3778b-be06-4cde-bc6e-0994efa42b18
docset: aem65
exl-id: 288d5459-bc69-4328-b6c9-4b4960bf4977
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2526'
ht-degree: 100%

---

# We.Gov および We.Finance リファレンスサイトのチュートリアル {#we-gov-reference-site-walkthrough}

## 前提条件 {#pre-requisites}

[We.Gov および We.Finance リファレンスサイトのセットアップと設定](../../forms/using/forms-install-configure-gov-reference-site.md)の説明に従ってリファレンスサイトを設定します。

## ユーザーストーリー {#user-story}

* AEM Forms

   * フォームの自動変換
   * オーサリング
   * フォームデータモデル／データソース

* AEM Forms

   * データキャプチャ
   * （オプション）データ統合（MS Dynamics）
   * （オプション）Adobe Sign

* ワークフロー
* メール通知
* （オプション）顧客とのコミュニケーション

   * 印刷チャネル
   * Web チャネル

* Adobe Analytics
* データソースの統合

### 架空のユーザーおよびグループ {#fictitious-users-and-groups}

We.Gov デモパッケージには、次の架空ユーザーが組み込まれています。

* **Aya Tan**：政府機関からサービスを受ける資格のある市民

![架空のユーザー](/help/forms/using/assets/aya_tan_new.png)

* **George Lang**：We.Gov エージェンシーのビジネスアナリスト

![架空のユーザー](/help/forms/using/assets/george_lang.png)

* **Camila Santos**：We.Gov エージェンシーの CX リード

![架空のユーザー](/help/forms/using/assets/camila_santos.png)

次のグループも含まれます。

* **We.Gov Forms ユーザー**

   * George Lang（メンバー）
   * Camila Santos（メンバー）

* **We.Gov ユーザー**

   * George Lang（メンバー）
   * Camila Santos（メンバー）
   * Aya Tan（メンバー）

### デモの概要用語集 {#demo-overview-terms-legend}

1. **別のユーザーとして実行する**：AEM デモで定義されたユーザーとグループ。
1. **ボタン**：移動のための色付きの長方形または丸付き矢印。
1. **クリック**：ユーザーストーリー内でのアクションの実行。
1. **リンク**：We.Gov サイトのメインメニューの上部にあります。
1. **ユーザーの手順**：ユーザーのストーリーを進める際に従う数字が付いた一連の手順です。
1. **フォームポータル**：*https://&lt;aemserver>:&lt;port>/content/we-gov/formsportal.html*
1. **モバイル表示**：We.Gov ユーザーは、サイズが変更されたブラウザーでモバイルビューをレプリケートできます。
1. **デスクトップ表示**：We.Gov ユーザーは、ノート PC またはデスクトップでデモを表示できます。
1. **事前スクリーニングフォーム**：We.Gov サイトのホームページ上のフォーム。
1. **アダプティブフォーム**：We.Gov デモの登録申し込みフォーム。

   *https://&lt;aemserver>:&lt;port>/content/forms/af/adobe-gov-forms/enrollment-application-for-health-benefits.html*

1. **Adobe We.Gov サイト**：*https://&lt;aemserver>:&lt;port>/content/we-gov/home.html*
1. **アドビインボックス**：AEM バックエンドの上部メニューバーにある [ベルのアイコン](assets/bell.svg)。

   *https://&lt;aemserver>:&lt;port>/aem/start.html*

1. **メールクライアント**：メールを表示する希望の方法（Gmail、Outlook）
1. **CTA**：コールトゥアクション
1. **移動**：ブラウザページ上で特定の参照点を見つける。
1. **AFC**：フォームの自動変換

## フォームの自動変換（Camila） {#automated-forms-conversion}

**この節**：Camila による CX リードには、紙ベースのプロセスの一部として使用された既存の PDF ベースのフォームがあります。 最新化の取り組みの一環として、Camila はこの PDF フォームを使用して、最新のアダプティブフォームを自動的に作成したいと考えています。

### フォームの自動変換 - We.Gov（Camila） {#automated-forms-conversion-wegov}

1. *&lt;aemserver>:&lt;port>/aem/start.html* に移動します。 

1. 以下の資格情報を使用してログインします。
   * **ユーザー**：camila.santos
   * **パスワード**：password
1. メインページから、Forms／Forms とドキュメント／AEM Forms We.gov Forms／AFC を選択します。
1. Camila は AEM Forms に PDF をアップロードします。

   ![フォームをアップロード](assets/aftia-upload-form.jpg)

1. Camilla は次に、PDF フォームを選択し、**自動変換を開始**&#x200B;をクリックして、変換処理を開始します。 フォームを変換した場合は、**変換を上書き**&#x200B;をクリックする必要がある場合があります。

   >[!NOTE]
   >
   >AFC の設定は、エンドユーザーに対して事前設定されているため、変更しないでください。

   * **オプション**：アクセシブルな Ultramarine テーマを使用する場合は、「アダプティブフォームのテーマを指定」をクリックし、オプションの一覧に表示される Accessible-Ultramarine テーマを選択してください。

   ![変換処理を開始](assets/aftia-start-conversion.jpg)

   ![Ultramarine テーマ](assets/aftia-upload-conversion-settings.jpg)

   変換処理中に完了率のステータスが表示されます。 **変換済み**&#x200B;のステータスが表示されたら、**出力**&#x200B;フォルダーをクリックし、アダプティブフォームを選択し、**編集**&#x200B;をクリックして、変換済のフォームを開きます。

1. Camilla はフォームを確認し、すべてのフィールドが存在することを確認します

   ![コンバージョンを確認](assets/aftia-review-conversion.jpg)

1. Camilla がフォームの編集を開始します。 Camila は、ルートパネル／編集（レンチ）を選択し、パネルレイアウトドロップダウンメニューから「上部のタブ」を選択し、「チェックボックス」を選択します。

   ![プロパティを確認](assets/aftia-review-properties.jpg)

1. 次に、Camilla は必要な CSS とフィールドの変更をすべて追加して、最終製品に仕上げます。

   ![CSS を追加](assets/aftia-add-css.jpg)

### フォームデータモデルとデータソース（Camila） {#data-sources}

**この節**：ドキュメントを変換してアダプティブフォームを作成したら、Camila はアダプティブフォームをデータソースに接続する必要があります。

1. [フォームの自動変換 - We.Gov](#automated-forms-conversion-wegov) で変換されたフォームのプロパティを開きます。

1. 次に、Camila はフォームモデルを選択／選択フォームドロップダウンからフォームデータモデルを選択／オプションのリストから We.gov 登録 FDM を選択します。

1. 「保存して閉じる」ボタンをクリックします。

   ![FDM 選択](assets/aftia-select-fdm.jpg)

1. Camila が&#x200B;**出力**&#x200B;フォルダーをクリックし、アダプティブフォームを選択して&#x200B;**編集**&#x200B;をクリックすると、完成した We.Gov フォームが開きます。
1. Camila がアダプティブフォームフィールドを選択し、![設定アイコン](assets/configure-icon.svg)をクリックします。**連結参照**&#x200B;フィールドを使用して、フォームデータモデルエンティティとの連結を作成します。アダプティブフォーム内のすべてのフィールドに対して、この手順を繰り返します。

### フォームアクセシビリティテスト（Camila） {#form-accessibility-testing}

Camila はまた、作成されたコンテンツが企業標準に従って正しく構築され、完全にアクセス可能であることを検証します。

1. Camila が&#x200B;**出力**&#x200B;フォルダーを開き、アダプティブフォームを選択して&#x200B;**プレビュー**&#x200B;をクリックすると、完成した We.Gov フォームが開きます。

1. Chrome デベロッパーツール内の「監査」タブを開きます。

1. アクセシビリティチェックを実行して、アダプティブフォームを検証します。

   ![アクセシビリティチェック](assets/aftia-accessibility.jpg)

## アダプティブフォームモバイルビューのデモ（Aya） {#mobile-view-demo}

**デモの前に、この節を実行する必要があります。**

**ユーザー手順：**

1. *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html* に移動します。
1. 以下の資格情報を使用してログインします。

   1. **ユーザー**：aya.tan
   1. **パスワード**：password

1. ブラウザーウィンドウのサイズを変更するか、ブラウザーのエミュレーターを使用してモバイルデバイスのサイズを複製します。

### We.Gov Web サイト（Aya） {#aya-user-story-we-gov-website}

![架空のユーザー](/help/forms/using/assets/aya_tan_new-1.png)

**この節**：Aya は市民です。 彼女は友人から、自分が政府機関からサービスを受ける資格があるかもしれないと聞きます。 Aya は携帯電話から We.Gov の Web サイトにアクセスし、自身が対象となるサービスの詳細を確認します。

### We.Gov プリスクリーン（Aya） {#aya-user-story-we-gov-pre-screener}

Aya は、携帯電話で短いアダプティブフォームに入力して適格性を確認するための質問に回答します。

**ユーザーの手順：**

1. 各ドロップダウンフィールドで選択を行います。

   >[!NOTE]
   >
   >年収が 200,000 ドルを超えるユーザーは対象外となります。

1. 「**自分が対象か確認する**」ボタンをクリックします。
1. 「**今すぐ申請**」ボタンをクリックして続行します。

   ![今すぐ申請リンク](/help/forms/using/assets/apply_now_link.png)

### We.Gov アダプティブフォーム（Aya） {#aya-user-story-we-gov-adaptive-form}

Aya は自分が対象であると判断し、モバイルデバイスでサービスをリクエストする申し込みフォームへの入力を開始します。

Aya は、サービスリクエストの申し込みを完了する前に、自宅でドキュメントを確認する必要があります。 Aya は保存してモバイルデバイスからアプリを終了します。

**ユーザーの手順：**

1. 「基本情報」フィールドに入力します。次の必須フィールドとドロップダウンがあります。

   1. 基本情報

      1. 名前（名）
      1. 名前（姓）
      1. 生年月日
      1. メール

1. 次の&#x200B;**動的ロジック**&#x200B;を使用して、**家族状況**&#x200B;ドロップダウンを使用して動的機能を示します。

   1. **未婚**：近親者パネルを表示
   1. **既婚**：扶養家族（配偶者）パネルを表示
   1. **離別**：近親者パネルを表示
   1. **死別**：近親者パネルを表示
   1. **子供の有無**：（はい／いいえ）扶養者（子供）パネルを表示するラジオボタン。

      1. 「追加」ボタンと「削除」ボタンを使用して、複数の扶養家族（子供）パネルを追加または削除します。

1. 灰色のメニューバーの右矢印をクリックします。
1. 下部にある「保存」ボタンをクリックします。

   ![アダプティブフォームの詳細](/help/forms/using/assets/adaptive_form.png)

## デスクトップデモ {#desktop-demo}

**この節：** 自宅に戻ると、Aya は必要な情報を見つけ、デスクトップからアプリを再開しました。 Aya はオンラインフォームポータルに移動し、申請を再開します。 いくつかのシンプルなカスタマイズ機能を使用すると、代理店は自動的にリンクを生成し、メールでアプリケーションを再開することもできます。

### アダプティブフォーム（Aya）- 続き {#aya-user-story-continued-adaptive-form}

**ユーザーの手順：**

1. *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html* に移動します。
1. ナビゲーションバーで、「**オンラインサービス**」を選択してクリックします。
1. ドラフトフォームパネルから、既存の「医療補助の登録申請書」を選択します。

   ![医療補助の登録申請書](/help/forms/using/assets/enrollment_application.png)

   ルックアンドフィールは同じで、データを再度入力する必要はありません。

   **ユーザー手順：**

1. 右側の円 CTA をクリックして、次のセクションに移動します。

   ![右側の円の CTA](/help/forms/using/assets/right_circle_cta_new.png)

   Aya が最後に入力した時点までフォームに情報が格納されます。Aya はすべての情報を入力し、提出する準備が整いました。

   ![アダプティブフォームの送信](/help/forms/using/assets/submit_adaptive_form.png)

   >[!NOTE]
   >
   >Aya は、電話番号欄に入力するとき、ダッシュ、スペース、ハイフンを含まない連続した 11 桁の数字を入力する必要があります。

   送信すると、ありがとうページが Aya に届きます。オプションで、記録文書をメールで受け取り、Adobe Sign で電子的に署名することもできます。

### オプション：Adobe Sign（Aya） {#adobe-sign}

**ユーザー手順：**

1. メールクライアントに移動し、 Adobe Sign メールを検索します。
1. Adobe Sign へのリンクをクリックします。

   ![Adobe Sign リンク](/help/forms/using/assets/adobe_sign_link.png)

**ユーザー手順：**

1. 「**同意します**」ボックスにチェックを入れます。
1. 「**同意する**」をクリックします。
1. レビュー済みドキュメントの下部までスクロールします。
1. ハイライトされた黄色のタブをクリックして、ドキュメントに署名します。

   ![ドキュメントに署名](/help/forms/using/assets/sign_document_new.png) ![テストドキュメントに署名](/help/forms/using/assets/sign_test_document.png)

## 政府職員（George） {#government-agent-george}

![政府職員の George](/help/forms/using/assets/george_lang-1.png)

**このセクション：** George は、Aya がサービスを要求している政府機関のビジネスアナリストです。George は 1 つのダッシュボードで、自分に割り当てられたすべてのサービスリクエストの申請書を確認できます。

### AEM インボックス（George） {#george-user-story-aem-inbox}

**ユーザー手順：**

1. *https://&lt;aemserver>:&lt;port>/aem/start.html* に移動します。
1. ユーザーアイコン（右上隅）をクリックして「**ログアウト**」を選択します。現在管理者ユーザーとしてログインしている場合は「**別のユーザーとして実行する**」メニューオプションを選択します。

   1. 以下の資格情報を使用してログインします。

      1. **ユーザー：** george.lang
      1. **パスワード：** password
   1. または別のユーザーとして実行：

      1. 「**別のユーザーとして実行する**」フィールドに「**George**」と入力します。

      1. 「OK」をクリックして、別のユーザーとして実行します。


1. 右上隅の「通知」（ベル）アイコンをクリックします。
1. 「**すべて表示**」をクリックしてインボックスに移動します。
1. インボックスから、最新の「**医療保障給付申請の確認**」タスクを開きます。

   ![医療保障給付申請の確認](/help/forms/using/assets/health_benefits.png)

### オプション：AEM インボックスと MS Dynamics （George） {#george-user-story-aem-inbox-and-ms-dynamics}

データ統合と自動ワークフローにより、Aya の申請書が、データの送信時に自動的に生成された CRM レコードとともに表示されます。

**ユーザー手順：**

1. 読み取り専用アダプティブフォームを開いて検査します。
1. 「**MS Dynamics を開く**」ボタンをクリックして、MS Dynamics レコードを新しいウィンドウで開きます。
1. CRM で、すべての情報の更新を確認できます。

   1. オプションで、レビューのメモを Dynamics に直接追加します。

1. 閉じて、AEM インボックス に戻ります。

   ![MS Dynamics レコード](/help/forms/using/assets/ms_dynamics.png)

### AEM インボックスに戻る（George） {#george-user-story-back-to-aem-inbox}

George が Aya の申請を承認すると、既存の自動ワークフローにより、Aya にも確認メールが送信されます。

**ユーザーの手順：**

1. 左上隅に移動して「**承認**」をクリックし、申請を承認します。
1. モーダルには、CX リードに対するメッセージを残すことができます。
1. 「完了」をクリックします。
1. （市民の役割）メールクライアントを開いて、Aya に送信されたメールを表示します。

   ![Aya に送信されたメールを表示](/help/forms/using/assets/email_client.png)

## CX リード（Camila） {#cx-lead-camila}

![Camila（CX リード）](/help/forms/using/assets/camila_santos-1.png)

**このセクション：** CX リード（Camila）は、承認された政府サービスの利用方法を Aya に説明するため、歓迎の電話をかけます。

### （オプション） AEM インボックスと MS Dynamics {#camila-user-story-aem-inbox-ms-dynamics}

**ユーザーの手順：**

1. *https://&lt;aemserver>:&lt;port>/aem/start.html* に移動します。
1. ユーザーアイコン（右上隅）をクリックして「**ログアウト**」を選択します。現在管理者ユーザーとしてログインしている場合は「**別のユーザーとして実行する**」メニューオプションを選択します。

   1. 以下の資格情報を使用してログインします。

      1. **ユーザー**：camila.santos
      1. **パスワード**：password
   1. または別のユーザーとして実行：

      1. 「**別のユーザーとして実行する**」フィールドに「**Camilia**」と入力します。

      1. 「OK」をクリックして、別のユーザーとして実行します。


1. 右上隅にある「通知」（ベル）アイコンをクリックします。
1. 「**すべて表示**」をクリックしてインボックスに移動します。
1. インボックスから、最新の「**新規連絡先の承認**」タスクを開きます。

![新規連絡先の承認](/help/forms/using/assets/new_contact_approval.png)

**（オプション）ユーザーの手順：**

1. 読み取り専用アダプティブフォームを開いて検査します。
1. 「**MS Dynamics を開く**」ボタンをクリックして、MS Dynamics レコードを新しいウィンドウで開きます。
1. CRM で、すべての情報の更新を確認できます。

   1. 必要に応じて、新規の通話アクティビティを Dynamics に直接追加します。
   1. 「**アクティビティ**」セクションを開きます。
   1. 「**新規通話**」オプションをクリックします。
   1. 通話の詳細を追加します。
   1. 保存してウィンドウを閉じます。

1. AEM に戻り、左上隅に移動して「**送信**」をクリックし、申請書を送信します。
1. モーダルで、メッセージを残すことができます。
1. 「完了」をクリックします。

   ![「アクティビティ」タブ](/help/forms/using/assets/activities_tab.png) ![新しい連絡先を確認](/help/forms/using/assets/confirm_new_contact.png)

## （オプション）市民用ウェルカムキット（Aya） {#welcome-kit-citizen-aya}

**このセクション：** Aya は、インタラクティブな通信へのリンクが含まれたメールを受信します。この通信には、Aya への給付が要約され、入力すべき申請書のフィールドも含まれています。メールには、給付説明書が PDF で添付され、インタラクティブな通信のためのレターへのリンクが付いています（インタラクティブな通信と同じテーマやブランディングが使用されます）。

### メールクライアント通知（Aya） {#aya-user-story-email-client}

**ユーザーの手順：**

1. ウェルカムキットのメールを探して開きます。
1. ページ下部の添付 PDF ファイルまでスクロールします。
1. クリックして、添付 PDF を開きます。
1. メールクライアントで上にスクロールし、「**ウェルカムキットをオンラインで表示**」をクリックします。

   1. 同じドキュメントの web チャネルバージョンが開きます。

1. PDF を直接参照するには：

   *https://&lt;aemserver>:&lt;port>/aem/formdetails.html/content/dam/formsanddocuments/adobe-gov-forms/welcome-handbook/we-gov-welcome-handbook*

1. IC を直接参照するには：

   *https://&lt;aemserver>:&lt;port>/content/dam/formsanddocuments/adobe-gov-forms/welcome-handbook/we-gov-welcome-handbook/jcr:content?channel=web&amp;mode=preview&amp;wcmmode=disabled*

   ![ウェルカム給付ハンドブック](/help/forms/using/assets/welcome_benefits_handbook.png) ![インタラクティブ通信リンク](/help/forms/using/assets/interactive_communication.png)

## 市民用更新リマインダー（Aya） {#renewal-reminder-citizen-aya}

**このセクション：** Camila は 1 年後の通信リマインダーのスケジュールを設定します（メールを自動化／実行するワークフロー手順）。

### メールクライアント通知（Aya） {#aya-user-story-email-client-updated}

**ユーザーの手順：**

1. メールクライアントに移動します。
1. 更新リマインダーのメールを探して開きます。
1. 「**新しい申請書を送信**」ボタンをクリックしてアダプティブフォームを開きます。

   1. このセクションは、フェーズ 2 でデータの事前入力に対応するために、意図的に空のままにしています。

   ![更新リマインダーメール](/help/forms/using/assets/renewal_reminder_email.png)

## （オプション）フォームデータモデル（Camila） {#form-data-model}

**この節**：Camila は AEM Forms データ統合に移動し、フォームデータモデル統合で外部データソースに送信した情報が確かに存在することを確認するために、簡単なテストを実施します。

### フォームデータモデル（Camila） {#form-data-model-camila}

**この節**：Camila はデータソースのページに移動し、サーバーによって Derby データベース内でレプリケートされたデータを検証します。

1. ユーザーエクスペリエンスが終了し、ユーザーによる送信が完了したら、Camila は AEM Forms の「データソース」タブ（**Forms** > **データ統合**）に移動します。

1. 次に、Camila は AEM Forms の&#x200B;**We.gov FDM**&#x200B;を選択して、**We.gov 登録 FDM**&#x200B;を編集します。

1. Camila はテストする必要がある&#x200B;**連絡先** > **読み取りサービス**&#x200B;を選択します。

   ![連絡先読み取りサービス](assets/aftia-contact-read-service.jpg)

1. Camila はテストサービスに連絡先 ID を入力し、「テスト」ボタンをクリックします。例えばフォームを送信した場合、1 または 2 です。フォームを送信していない場合、データは返されません。

   ![連絡先読み取りサービス](assets/aftia-test-service.jpg)

1. その後、Caimla はデータがデータソースに正常に挿入されたことを検証できます。

   * Derby DS 内のデータは、次のような形式です。

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

## （オプション）分析（Camila） {#analytics-cx-lead-camila}

**この節：** Camila は、ダッシュボードに移動してエージェンシーの KPI を確認します。例えば、サービス申込書を記入し始めた後に放棄した市民の割合、申込書の提出から承認または却下の回答までの平均時間、市民に送信した特典ハンドブックの使用状況などです。

### Adobe Analytics Sites レポート（Camila） {#camila-reviews-sites-reporting-we-gov-adobe-analytics}

1. *https://&lt;aemserver>:&lt;port>/sites.html/content*&#x200B;に移動します。
1. 「**AEM Forms We.Gov サイト**」を選択して、サイトのページを表示します。
1. サイトページの 1 つ（例：ホーム）を選択し、**分析と推奨事項**&#x200B;を選択します。

   ![分析と推奨事項](/help/forms/using/assets/analytics_recommendation.jpg)

1. このページには、AEM Sites ページに関連する Adobe Analytics から取得した情報が表示されます（メモ：設計上、この情報は Adobe Analytics から定期的に更新されますが、リアルタイムには表示されません）。

   ![Adobe Analytics 主要指標](/help/forms/using/assets/analytics_key_metrics.jpg)

1. ページビューページ（ステップ 3 でアクセス）に戻ると、「**リスト表示**」の項目を表示する表示設定を変更することで、ページビュー情報を表示することもできます。
1. 「**表示**」ドロップダウンメニューで「**リスト表示**」を選択します。

   ![表示ドロップダウンメニューのリスト表示](/help/forms/using/assets/list_view_view_dropdown.jpg)

1. 同じメニューから「**設定を表示**」を選択し、「**分析**」セクションから表示する列を選択します。

   ![列の表示を設定](/help/forms/using/assets/view_setting_analytics.jpg)

1. 「**更新**」をクリックして、新しい列を使用可能にします。

   ![新しい列を使用可能にする](/help/forms/using/assets/new_columns_available.jpg)

### Adobe Analytics Forms レポート（Camila） {#camila-reviews-forms-reporting-we-gov-adobe-analytics}

1. 次に移動します。

   *https://&lt;aemserver>:&lt;port>/aem/forms.html/content/dam/formsanddocuments/adobe-gov-forms*

1. 「**医療保障給付申込書**」アダプティブフォームを選択してから、「**分析レポート**」オプションを選択してください。

   ![医療保障給付申請](/help/forms/using/assets/analytics_report_benefits.jpg)

1. ページが読み込まれるのを待ち、分析レポートデータを表示します。

   ![分析レポートデータ](/help/forms/using/assets/analytics_report_data_updated.jpg)
