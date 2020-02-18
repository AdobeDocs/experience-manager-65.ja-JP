---
title: We.Gov リファレンスサイトのチュートリアル
seo-title: We.Gov リファレンスサイトのチュートリアル
description: We.Govデモパッケージを使用してAEM Formsのタスクを実行するには、架空のユーザーおよびグループを使用します。
seo-description: We.Govデモパッケージを使用してAEM Formsのタスクを実行するには、架空のユーザーおよびグループを使用します。
uuid: 797e301a-36ed-4bae-9ea8-ee77285c786d
contentOwner: anujkapo
discoiquuid: ddb3778b-be06-4cde-bc6e-0994efa42b18
docset: aem65
translation-type: tm+mt
source-git-commit: 3226edb575de3d9f8bff53f5ca81e2957f37c544

---


# We.Gov リファレンスサイトのチュートリアル{#we-gov-reference-site-walkthrough}

## 前提条件 {#pre-requisites}

Set up the reference site as described in [Set up and configure We.Gov reference site](../../forms/using/forms-install-configure-gov-reference-site.md).

## ユーザーストーリー {#user-story}

* AEM Forms

   * データ取得
   * データ統合(MS Dynamics)
   * Adobe Sign

* ワークフロー
* 顧客との連絡

   * 印刷チャネル
   * Web チャネル

* Adobe Analytics

### Fictitious users and groups {#fictitious-users-and-groups}

We.Govデモパッケージには、次の組み込みの架空のユーザーが含まれています。

* **綾丹**:官庁から送達を受ける資格のある市民

![架空のユーザー](/help/forms/using/assets/aya_tan_new.png)

* **ジョージ・ラン**&#x200B;グ：We.Govエージェンシー・ビジネス・アナリスト

![架空のユーザー](/help/forms/using/assets/george_lang.png)

* **カミラ・サントス**:We.Gov Agency CXリード

![架空のユーザー](/help/forms/using/assets/camila_santos.png)

次のグループも含まれます。

* **We.Gov Formsユーザー**

   * ジョージ・ラング（会員）
   * カミラサントス（会員）

* **We.Govユーザー**

   * ジョージ・ラング（会員）
   * カミラサントス（会員）
   * 綾丹（会員）

### デモ概要用語の凡例 {#demo-overview-terms-legend}

1. **偽装**:AEMデモでのユーザーとグループの定義。
1. **ボタン**:ナビゲーション用の色付きの長方形または丸付き矢印。
1. **クリック**:ユーザーストーリー内のアクションを実行する場合。
1. **リンク**:We.Govサイトのメインメニューの上部にあります。
1. **User Instructions**:ユーザーのストーリー内を移動する際に実行する一連の数値手順です。
1. **フォームポータル**: *https://&lt;aemserver>:&lt;port>/content/we-gov/formsportal.html*
1. **モバイルビュー**:We.Govユーザー。再サイズのブラウザーでモバイルビューを複製します。
1. **Desktop View**:We.govユーザーは、ノートパソコンまたはデスクトップでデモを閲覧できます。
1. **事前スクリーンフォーム**:We.Govサイトのホームページのフォーム。
1. **アダプティブフォーム**:We.govデモの登録申込フォーム。

   *https://&lt;aemserver>:&lt;port>/content/forms/af/adobe-gov-forms/enrollment-application-for-health-benefits.html*

1. **Adobe Web.Govサイト**: *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html*
1. **Adobe Inbox**:AEMバックエンドの上部メニ [ューバー] 「ベル」アイコン。

   *https://&lt;aemserver>:&lt;port>/aem/start.html*

1. **電子メールクライアント**:電子メールを表示する優先方法(Gmail、Outlook)
1. **CTA**:誘い文句（CTA：コールトゥアクション）
1. **移動**:ブラウザページ上の特定の基準点を指定する場合。

## モバイルビューデモ {#mobile-view-demo}

**この節は、デモの前に実行する必要があります。**

**ユーザー手順：**

1. 移動先： *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html*
1. ログイン先：

   1. **ユーザー**:aya.tan
   1. **パスワード**：password

1. ブラウザーウィンドウのサイズを変更するか、ブラウザーのエミュレーターを使用してモバイルデバイスのサイズを複製します。

### Ayaユーザーストーリー（We.Gov webサイト） {#aya-user-story-we-gov-website}

![架空のユーザー](/help/forms/using/assets/aya_tan_new-1.png)

**この節**:綾は市民だ。 彼女は友人から、政府機関からサービスを受ける資格があると聞く。 Ayaは携帯電話からWe.Govのウェブサイトにアクセスし、資格を持つサービスの詳細を知る。

### Ayaユーザーストーリー（We.Govプリスクリーン） {#aya-user-story-we-gov-pre-screener}

Ayaは、携帯電話で短いアダプティブフォームに入力して、適格性を確認するための質問に回答します。

**ユーザー手順：**

1. 各ドロップダウンフィールドを選択します。

   1. 注意：年間20万ドルを超える収益を得たユーザーは、資格がありません。

1. 「自分が適格か&#x200B;**どうか」をクリックします。**” button.
1. 「**Apply Now**」ボタンをクリックして続行します。

   ![「今すぐ適用」リンク](/help/forms/using/assets/apply_now_link.png)

### Ayaユーザーストーリー（We.Govアダプティブフォーム） {#aya-user-story-we-gov-adaptive-form}

Ayaは資格があると知り、モバイルデバイスでのサービスをリクエストする申込書の記入を開始します。

Ayaは、サービスリクエスト申込書を完成させる前に、自宅でいくつかのドキュメントを確認する必要があります。 Savesはアプリを保存し、終了します。

**ユーザー手順：**

1. 「基本情報」フィールドに入力します。次に、必須フィールドとドロップダウンを示します。

   1. 基本情報

      1. 名
      1. ミドルネーム
      1. 姓
      1. 優先名
      1. DOB
      1. 性別
   1. 連絡先情報

      1. 住所
      1. 市区町村
      1. 電話番号
      1. 郵便番号
      1. 電子メール
      1. 都道府県
   1. 格闘

      1. 家族ステータス



1. 次の動的論理を使用し **て** 、「ファミリーステータス」ドロップダウンを使用した動的 **機能を示します** 。

   1. **単一**:キンパネルの隣に表示
   1. **既婚**:婚姻状況依存パネルの表示
   1. **離婚**:キンパネルの隣に表示
   1. **妻**:キンパネルの隣に表示
   1. **子供はいる？**:（はい/いいえ）子依存パネルを表示するラジオボタン。

      1. （追加/削除）ボタンをクリックして、複数の子依存パネルを追加/削除します。

1. 灰色のメニューバーの右矢印をクリックします。
1. 下部にある「保存」ボタンをクリックします。

   ![アダプティブフォームの詳細](/help/forms/using/assets/adaptive_form.png)

## デスクトップデモ {#desktop-demo}

**** このセクション：自宅で、綾さんは必要な情報を見つけ、デスクトップから申込書を再開します。 Ayaはオンラインフォームポータルに移動して申込を再開します。 簡単なカスタマイズで、代理店は自動的にリンクを生成し、電子メールで申込を再開することもできます。

### Ayaユーザーストーリー（続きのアダプティブフォーム） {#aya-user-story-continued-adaptive-form}

**ユーザー手順：**

1. https://&lt;aemserver>:&lt; *port>/content/we-gov/home.htmlに移動します。*
1. ナビゲーションバーで「**Online Services**」をクリックします。
1. 「Draft Forms」パネルから、既存の「Enrollment Application For Health Benefits」を選択します。

   ![健康給付登録申請](/help/forms/using/assets/enrollment_application.png)

   外観と操作性は同じで、データを再入力する必要はありません。

   **ユーザー手順：**

1. 右の「円CTA」をクリックして、次のセクションに移動します。

   ![右円CTA](/help/forms/using/assets/right_circle_cta_new.png)

   フォームは、Ayaの最後のエントリの時点まで入力されます。 綾さんは彼女の情報をすべて入力し、送信する準備ができています。

   ![アダプティブフォームの送信](/help/forms/using/assets/submit_adaptive_form.png)

   Ayaが開いた電子メールを受け取った後、AyaはAdobe signを使用して電子署名を行う準備が整いました。

**ユーザー手順：**

1. 送信後、「ありがとうございます」ページが表示されます。
1. 電子メールクライアントに移動し、Adobe sign電子メールを探します。
1. Adobe signへのリンクをクリックします。

   ![Adobe Signリンク](/help/forms/using/assets/adobe_sign_link.png)

**ユーザー手順：**

1. 「**I agree**」ボックスを選択します。
1. 「受け入れ&#x200B;****」をクリックします。
1. レビュー済みのドキュメントの一番下までスクロールします。
1. 強調表示された黄色のタブをクリックして、ドキュメントに署名します。

   ![ドキュメントへの署名](/help/forms/using/assets/sign_document_new.png)![テストドキュメントへの署名](/help/forms/using/assets/sign_test_document.png)

## 政府代理人(George) {#government-agent-george}

![ジョージ政府代理](/help/forms/using/assets/george_lang-1.png)

**** このセクション：ジョージは、アヤ政府機関のビジネスアナリストで、サービスを要請している。 Georgeは1つのダッシュボードを持ち、レビュー用に割り当てられたすべてのサービスリクエストアプリを確認できます。

### Georgeユーザーストーリー（AEM受信トレイ） {#george-user-story-aem-inbox}

**ユーザー手順：**

1. https://&lt;aemserver>:&lt; *port>/aem/start.htmlに移動します。*
1. ユーザーアイコン（右上隅）をクリックし、「**Sign Out**」（サインアウト）または「**Impersonate as**」（次の形式で動作）メニューオプションを使用します（現在管理ユーザーとログインしている場合）。

   1. ログイン先：

      1. **** ユーザー：george.lang
      1. **パスワード：** password
   1. または次のようになります。

      1. 「次の形式で&#x200B;**動作する**」フィールドに「**George**」と入力します。

      1. 「OK」をクリックして偽装します。


1. 右上隅の通知（ベル）アイコンをクリックします。
1. 「すべて表示&#x200B;**」をクリックし**、受信トレイに移動します。
1. インボックスから、最新の「**Health Benefits Application Review**」タスクを開きます。

   ![ヘルスメリットの申し込みレビュー](/help/forms/using/assets/health_benefits.png)

### Georgeユーザーストーリー（AEM受信トレイとMS Dynamics） {#george-user-story-aem-inbox-and-ms-dynamics}

データの統合と自動化されたワークフローにより、Ayaのアプリケーションが、データの送信時に自動的に生成されたCRMレコードと共に表示されます。

**ユーザー手順：**

1. 読み取り専用アダプティブフォームを開き、調査します。
1. [MS Dynamicsを開く&#x200B;****]ボタンをクリックして、MS Dynamicsレコードを新しいウィンドウで開きます。
1. CRMでは、すべての情報を更新できます

   1. 必要に応じて、Dynamicsに直接レビューメモを追加します。

1. 閉じて、AEMインボックスに戻ります。

   ![MS Dynamicsレコード](/help/forms/using/assets/ms_dynamics.png)

### George User Story（AEMの受信トレイに戻る） {#george-user-story-back-to-aem-inbox}

GeorgeはAyaの申込を承認し、既存の自動化ワークフローのおかげで、Ayaに確認の電子メールも送信します。

**ユーザー手順：**

1. 左上隅に移動し、「**Approve**」をクリックして申込を承認します。
1. モーダルでは、CXリードに対するメッセージを残すことができます。
1. 「完了」をクリックします。
1. （市民の役割）電子メールクライアントを開き、Ayaに送信された電子メールを表示します。

   ![Ayaに送信された電子メールの表示](/help/forms/using/assets/email_client.png)

## CXリーダー(Camila) {#cx-lead-camila}

![カミラ（CXリード）](/help/forms/using/assets/camila_santos-1.png)

**** このセクション：CXのリードは、Ayaとの歓迎電話を設定し、承認された政府サービスの利用方法を説明します。

### カミラユーザーストーリー（AEMインボックスおよびMS Dynamics） {#camila-user-story-aem-inbox-ms-dynamics}

**ユーザー手順：**

1. https://&lt;aemserver>:&lt; *port>/aem/start.htmlに移動します。*
1. ユーザーアイコン（右上隅）をクリックし、「**Sign Out**」（サインアウト）または「**Impersonate as**」（次の形式で動作）メニューオプションを使用します（現在管理ユーザーとログインしている場合）。

   1. ログイン先：

      1. **ユーザー**:camila.santos
      1. **パスワード**：password
   1. または次のようになります。

      1. 「次の形式で&#x200B;**動作する**」フィールドに「**Camila**」と入力します。

      1. 「OK」をクリックして偽装します。


1. 右上隅の通知（ベル）アイコンをクリックします。
1. 「すべて表示&#x200B;**」をクリックし**、受信トレイに移動します。
1. 受信トレイから、最新の「新しい連絡先&#x200B;**の承認**」タスクを開きます。

   ![新しい連絡先の承認](/help/forms/using/assets/new_contact_approval.png)

   **ユーザー手順：**

1. 読み取り専用アダプティブフォームを開き、調査します。
1. [MS Dynamicsを開く&#x200B;****]ボタンをクリックして、MS Dynamicsレコードを新しいウィンドウで開きます。
1. CRMでは、すべての情報を更新できます

   1. 必要に応じて、新しい呼び出しアクティビティをDynamicsに直接追加します。
   1. 「アクティビティ&#x200B;****」セクションを開きます。
   1. 「新しい電話」オ&#x200B;**プションをクリック**&#x200B;します。
   1. 電話の詳細を追加します。
   1. ウィンドウを保存して閉じます。

1. AEMに戻り、左上隅に移動し、「送信」をクリックし&#x200B;**て**、申込を送信します。
1. モーダルでは、メッセージを残すことができます。
1. 「完了」をクリックします。

   ![[アクティビティ]タブ](/help/forms/using/assets/activities_tab.png) [ ![新しい連絡先の確認]](/help/forms/using/assets/confirm_new_contact.png)

## ウェルカムキット市民（綾） {#welcome-kit-citizen-aya}

**** このセクション：Ayaは、メリットを要約し、入力するフォームフィールドも含むインタラクティブなコミュニケーションへのリンクを含む電子メールを受信します。 PDFのメリットに関する説明を添付し、（インタラクティブ通信と同じテーマ/ブランドを持つ）メール内のインタラクティブ通信レターにリンクします。

### Ayaユーザーストーリー（Eメールクライアント） {#aya-user-story-email-client}

**ユーザー手順：**

1. ウェルカムキットの電子メールを探して開きます。
1. ページ下部のPDF添付ファイルまでスクロールします。
1. PDF添付ファイルをクリックして開きます。
1. 電子メールクライアントを上にスクロールして、「ウェルカムキットをオンラ&#x200B;**インで表示**」をクリックします。

   1. 同じドキュメントのWebチャネルバージョンが開きます。

1. PDFを直接参照するには：

   *https://&lt;aemserver>:&lt;port>/aem/formdetails.html/content/dam/formsanddocuments/adobe-gov-forms/welcome-handbook/web-gov-welcome-handbook*

1. 導入コンサルタントへの直接的なクイック・リファレンス：

   *https://&lt;aemserver>:&lt;port>/content/dam/formsanddocuments/adobe-gov-forms/welcome-handbook/web-gov-welcome-handbook/jcr:channel=web&amp;mode=preview&amp;wcmmode=disabled*

   ![Welcome Benefits Handbook](/help/forms/using/assets/welcome_benefits_handbook.png) ![Interactive Communication Link](/help/forms/using/assets/interactive_communication.png)

## 更新リマインダー市民(Aya) {#renewal-reminder-citizen-aya}

**** このセクション：カミラはまた、1年後に通信リマインダーを予定している。 （電子メールを自動化/実行するワークフロー手順）。

### Ayaユーザーストーリー（Eメールクライアント） {#aya-user-story-email-client-1}

**ユーザー手順：**

1. 電子メールクライアントに移動します。
1. 更新リマインダの電子メールを探して開きます。
1. 「**Submit a new application**」ボタンをクリックして、アダプティブフォームを開きます。

   1. このセクションは、フェーズ2で事前入力されたデータをサポートするために、意図的に空のままにしておきます。
   ![更新リマインダーの電子メール](/help/forms/using/assets/renewal_reminder_email.png)

## Analytics CXリーダー(Camila) {#analytics-cx-lead-camila}

**** このセクション：Camilaは、エージェンシーKPI内で確認できるダッシュボードに移動します。例えば、サービスリクエストフォームへの記入と放棄を開始する市民の割合、リクエスト提出から承認/拒否への対応までの平均時間、市民に送信した給付金ハンドブックのエンゲージメント統計などです。

### カミラレビューサイトレポート(We.Gov Adobe Analytics) {#camila-reviews-sites-reporting-we-gov-adobe-analytics}

1. https://&lt;aemserver>:&lt; *port>/sites.html/contentに移動します。*
1. 「**AEM Forms Web.Govサイト**」を選択して、サイトページを表示します。
1. サイトページ（例：ホーム）の1つを選択し、「**Analytics &amp; Recommendations**」を選択します。

   ![解析と推奨](/help/forms/using/assets/analytics_recommendation.jpg)

1. このページには、AEMサイトページに関連するAdobe Analyticsから取得した情報が表示されます(注意：設計により、この情報はAdobe Analyticsから定期的に更新され、リアルタイムでは表示されません)。

   ![Adobe Analyticsの主要指標](/help/forms/using/assets/analytics_key_metrics.jpg)

1. ページビューページ（手順3.でアクセス）に戻ると、「リストビュー」に項目を表示するように表示設定を変更して、ページビュー情報を表示するこ&#x200B;**ともできます**。
1. [表示&#x200B;**]ドロップダウンメニューを見つけ、[リス**&#x200B;ト表示&#x200B;****]を選択します。

   ![「表示」ドロップダウンメニューのリスト表示](/help/forms/using/assets/list_view_view_dropdown.jpg)

1. 同じメニューから「設定を&#x200B;**表示**」を選択し、「**Analytics**」セクションから表示する列を選択します。

   ![列の表示の設定](/help/forms/using/assets/view_setting_analytics.jpg)

1. [更新&#x200B;****]をクリックして新しい列を利用可能にします。

   ![新しい列を使用可能にする](/help/forms/using/assets/new_columns_available.jpg)

### カミラレビューフォームレポート(We.Gov Adobe Analytics) {#camila-reviews-forms-reporting-we-gov-adobe-analytics}

1.  に移動します。

   *https://&lt;aemserver>:&lt;port>/aem/forms.html/content/dam/formsanddocuments/adobe-gov-forms*

1. 「Enrollment Application For Health Benefits **」アダプティブフォームを選択し、「** Analytics Report ****」オプションを選択します。

   ![健康給付登録申請](/help/forms/using/assets/analytics_report_benefits.jpg)

1. ページが読み込まれるのを待って、Analyticsレポートデータを表示します。

   ![Analyticsレポートデータ](/help/forms/using/assets/analytics_report_data_updated.jpg)

