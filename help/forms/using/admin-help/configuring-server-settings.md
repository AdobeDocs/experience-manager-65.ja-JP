---
title: サーバー設定の指定
seo-title: Configuring Server Settings
description: サーバー設定ページから、電子メール、タスク通知、管理者通知の設定にアクセスできます。
seo-description: The Server Settings page provides access to email, task notification and administrator notification settings.
uuid: 73b51ac0-56e5-4748-bb33-e3986c69eb2d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e047a95e-0acb-438a-8d27-f005c0adc508
exl-id: 362b7b91-c58b-4e47-a6ef-56a4b54a100c
source-git-commit: c4cd9a61a226ace2a72d60b5b7b7432de12cb873
workflow-type: tm+mt
source-wordcount: '2623'
ht-degree: 18%

---

# サーバー設定の指定 {#configuring-server-settings}

サーバー設定ページから、Forms ワークフローの様々な設定にアクセスできます。

* **電子メールの設定** これにより、送信する電子メールメッセージを有効にし、それらのメッセージに使用する電子メールサーバー設定を有効にします。 ( 詳しくは、 [電子メールの設定](configuring-server-settings.md#configuring-email-settings).)
* **タスク通知の設定**：エンドユーザーおよびグループに、タスクに関するメール通知で送信されるメッセージを有効化、無効化または変更することができます。（[ユーザーおよびグループへの通知の設定](configuring-server-settings.md#configuring-notifications-for-users-and-groups)を参照してください）。
* **管理者通知の設定**：管理タスクについてのメール通知で送信されるメッセージを有効化、無効化または変更することができます。( 詳しくは、 [管理者への通知の設定](configuring-server-settings.md#configuring-notifications-for-administrators).)

## 電子メールの設定 {#configuring-email-settings}

Forms Server の電子メールアカウントを指定し、この電子メールアカウントを使用して、AEM forms のユーザーおよび管理者に電子メールメッセージを送信できます。 これらの電子メールメッセージは、完了する必要があるタスクをユーザーに通知し、期限に達したタスクをユーザーに通知し、発生したプロセスエラーを管理者に通知するために使用されます。

AEM forms とユーザーの間で電子メールメッセージを送信できるようにするには、電子メールの設定ページで、送信電子メールを設定します。 送信メールは SMTP サーバーを使用する必要があります。

AEM forms がユーザーからの受信電子メールメッセージを受信して処理できるようにするには、Complete Task サービスの電子メールエンドポイントを作成します。 ( 詳しくは、 [Complete Task サービス用の電子メールエンドポイントの作成](/help/forms/using/admin-help/configuring-email-endpoints.md#create-an-email-endpoint-for-the-complete-task-service)) をクリックします。

電子メールを使用せずにプロセスを設計および実装する場合は、電子メールの設定ページでオプションを設定する必要はありません。

### 送信メールの設定 {#configure-outgoing-email-settings}

1. 管理コンソールで、サービス/forms ワークフロー/サーバー設定/電子メールの設定をクリックします。
1. 「送信メッセージを有効にする」を選択します。
1. 「SMTP サーバー」ボックスに、電子メールサーバーの名前または IP アドレスを入力します。 forms ワークフローからのすべての通知電子メールメッセージは、この電子メールサーバーから送信されます。
1. 「ユーザー名」ボックスと「パスワード」ボックスに、SMTP サーバーが認証を要求する際に使用するログイン名とパスワードを入力します。 匿名ログインが許可されている場合は、空白のままにします。
1. 「電子メールアドレス」ボックスに、forms ワークフローが送信する電子メールメッセージの返信先アドレスとして使用する電子メールアドレスを入力します。

   >[!NOTE]
   >
   >Microsoft Exchange Server を使用していて、電子メールアドレスが無効な電子メールアドレスの場合、Microsoft Exchange Server は配布リストに電子メールを送信できません。 この問題を解決するには、Microsoft Exchange Server 上の配信リスト毎に「**外部コミュニケーションを有効化**」オプションを選択します。

1. 「保存」をクリックします。

>[!NOTE]
>
>誤った情報を入力した場合は、「キャンセル」をクリックして、前に表示したページに戻ることができます。

### AEM Forms Workspace を使用するための電子メールテンプレートの設定 {#configuring-email-templates-to-use-html-workspace}

>[!NOTE]
>
>AEM Forms のリリースでは Flex Workspace は廃止されています。

デフォルトでは、AEM forms から送信される電子メールには、Flex Workspace(JEE 上のAEM forms では廃止 ) へのリンクが含まれています。 AEM Forms Workspace へのリンクを含む電子メールを送信するようにAEM forms を設定できます。 Flex Workspace(JEE 上のAEM forms では廃止されています ) に対するAEM Forms Workspace のメリットについて詳しくは、 [この](/help/forms/using/features-html-workspace-available-flex.md) 記事。

1. 管理コンソールで、ホーム/サービス/forms ワークフロー/サーバー設定/タスク通知をクリックします。
1. タスク割り当てテンプレートを開きます。
1. タスク通知のテンプレートを次のように設定します。 `https://@@notification-host@@:8080/lc/libs/ws/index.html?taskId=@@taskid@@`

   ```java
   https://@@notification-host@@:8080/lc/libs/ws/index.html?taskId=@@taskid@@
   ```

## ユーザーおよびグループへの通知の設定 {#configuring-notifications-for-users-and-groups}

タスク通知ページでは、forms ワークフローがユーザーおよびグループに送信する電子メール通知を生成する際に使用するテンプレートを設定できます。 フォームワークフロー変数を使用して、通知をカスタマイズし、書式設定することができます。

ユーザーおよびグループに対して、次のタイプの通知を設定できます。

* reminders
* タスクの割り当て
* 締切

グループに関する電子メール通知を生成するには、User Management でグループの電子メールアドレスを指定します。 <!--Fix broken link See Setting up and organizing users -->Forms Workflow によってメール通知がグループに送信されると、そのグループ内の、メールアドレスが指定されている各メンバーがそのメール通知を受け取ります。グループのメンバーが電子メール通知を受け取り、タスクを要求する場合、メンバーは電子メール通知の要求リンクをクリックし、Workspace でタスクの詳細ページを開く必要があります。 メンバーはここから、作業項目を要求または要求して開くことができます。

>[!NOTE]
>
>AEM Forms のリリースでは Flex Workspace は廃止されています。

### ユーザーまたはグループのリマインダーの設定 {#configure-reminders-for-users-or-groups}

タスクの完了期限が近づいたら、割り当てられたユーザーまたはグループにリマインダー通知を送信できます。 リマインダー通知を送信するタイミングを正確に決定するルールは、プロセス開発者が決定します。

1. 管理コンソールで、サービス/Forms workflow/サーバー設定/タスク通知をクリックします。
1. 「通知タイプ」で、「リマインダー」（ユーザーの場合）または「グループ — リマインダー」（グループの場合）をクリックします。
1. 「リマインダーを有効にする」または「グループ — リマインダーを有効にする」を選択します。
1. （ユーザー通知のみ）リマインダーの電子メールメッセージにフォームとそのデータの添付ファイルを含めるには、「フォームデータを含める」を選択します。
1. 「件名」ボックスに、電子メールメッセージの件名行のテキストを入力します。 このフィールドには、デフォルトのテキストが事前入力されています。 このフィールドのカスタマイズについて詳しくは、 [通知の内容のカスタマイズ](configuring-server-settings.md#customizing-the-content-of-notifications).
1. 「通知テンプレート」ボックスに、電子メールメッセージの本文のテキストを入力します。 このフィールドには、デフォルトのテキストが事前入力されています。 このフィールドのカスタマイズについて詳しくは、 [通知の内容のカスタマイズ](configuring-server-settings.md#customizing-the-content-of-notifications).
1. 「メッセージの形式」リストで、E メールメッセージの送信形式 (「HTML」または「テキスト」) を選択します。 デフォルトの形式は「HTML」です。
1. 「 E メールのエンコーディング」リストで、E メールメッセージに使用するエンコーディング形式を選択します。 デフォルトは UTF-8 で、日本以外のほとんどのユーザーが使用します。 日本のユーザーは ISO2022-JPを選択できます。
1. 「保存」をクリックします。

### ユーザーまたはグループのタスク割り当て通知を設定する {#configure-task-assignment-notifications-for-users-or-groups}

タスクが割り当てられたときに、タスクの割り当て通知をユーザーまたはグループに送信できます。

1. 管理コンソールで、サービス/Forms workflow/サーバー設定/タスク通知をクリックします。
1. 「通知タイプ」で、「タスクの割り当て」（ユーザーの場合）または「グループ — タスクの割り当て」（グループの場合）をクリックします。
1. ユーザーに対しては「タスクの割り当てを有効にする」を選択するか、グループに対しては「グループ — タスクの割り当てを有効にする」を選択します。
1. （ユーザー通知のみ）タスクの割り当て電子メールメッセージにフォームとそのデータの添付ファイルを含めるには、「フォームデータを含める」を選択します。
1. 「件名」ボックスに、電子メールメッセージの件名行のテキストを入力します。 このフィールドには、デフォルトのテキストが事前入力されています。 このフィールドのカスタマイズについて詳しくは、 [通知の内容のカスタマイズ](configuring-server-settings.md#customizing-the-content-of-notifications).
1. 「通知テンプレート」ボックスに、電子メールメッセージの本文のテキストを入力します。 このフィールドには、デフォルトのテキストが事前入力されています。 このフィールドのカスタマイズについて詳しくは、 [通知の内容のカスタマイズ](configuring-server-settings.md#customizing-the-content-of-notifications).
1. 「メッセージの形式」リストで、E メールメッセージの送信形式 (「HTML」または「テキスト」) を選択します。 デフォルトの形式は「HTML」です。
1. 「 E メールのエンコーディング」リストで、E メールメッセージに使用するエンコーディング形式を選択します。 デフォルトは UTF-8 で、日本以外のほとんどのユーザーが使用します。 日本のユーザーは ISO2022-JPを選択できます。
1. 「保存」をクリックします。

### ユーザーまたはグループへのデッドライン通知の設定 {#configure-deadline-notifications-for-users-or-groups}

割り当てられたタスクの実行期限が過ぎると、ユーザーおよびグループにデッドライン通知を送信できます。 ユーザーは割り当てられたタスクを実行できなくなったので、デッドライン通知は通常情報提供です。

1. 管理コンソールで、サービス/Forms workflow/サーバー設定/タスク通知をクリックします。
1. 「通知タイプ」で、「期限」（ユーザーの場合）または「グループ — 期限」（グループの場合）をクリックします。
1. 「期限を有効にする」または「グループ — 期限を有効にする」を選択します。
1. 「件名」ボックスに、電子メールメッセージの件名行のテキストを入力します。 このフィールドには、デフォルトのテキストが事前入力されています。 このフィールドのカスタマイズについて詳しくは、 [通知の内容のカスタマイズ](configuring-server-settings.md#customizing-the-content-of-notifications).
1. 「通知テンプレート」ボックスに、電子メールメッセージの本文のテキストを入力します。 このフィールドには、デフォルトのテキストが事前入力されています。 このフィールドのカスタマイズについて詳しくは、 [通知の内容のカスタマイズ](configuring-server-settings.md#customizing-the-content-of-notifications).
1. 「メッセージの形式」リストで、E メールメッセージの送信形式 (「HTML」または「テキスト」) を選択します。 デフォルトの形式は「HTML」です。
1. 「 E メールのエンコーディング」リストで、E メールメッセージに使用するエンコーディング形式を選択します。 デフォルトは UTF-8 で、日本以外のほとんどのユーザーが使用します。 日本のユーザーは ISO2022-JPを選択できます。
1. 「保存」をクリックします。

### すべてのメールに対して DO NOTDELETEタグを非表示にする {#hide-the-do-not-delete-tag-for-all-emails}

人間中心のプロセスで送信されたすべてのメールで、DO NOT DELETE 追跡タグを非表示にするようメールを設定できます。

<!-- 
For details, see [How to hide the 'DO-NOT-DELETE' tag with CSS](https://blogs.adobe.com/LiveCycleHelp/2013/09/how-to-hide-the-do-not-delete-tag-with-css.html) 
-->

## 管理者への通知の設定 {#configuring-notifications-for-administrators}

管理者に送信される電子メール通知を生成する際に forms ワークフローで使用するテンプレートを設定できます。

管理者には、次の種類の通知を設定できます。

* 停止したブランチ
* 停止した操作

### 停止したブランチの通知の設定 {#configure-stalled-branch-notifications}

ブランチが停止した場合（意図的またはエラーが原因で停止した場合）、管理者または別のユーザーに電子メール通知を送信して、問題を調査できます。

1. 管理コンソールで、サービス/Forms workflow/サーバー設定/管理者通知をクリックします。
1. 「通知タイプ」で、「停止したブランチ」をクリックします。
1. 「停止したブランチを有効にする」を選択します。
1. 「電子メールアドレス」ボックスに、分岐が停止したときに通知するユーザーのアドレスを入力します。 user@domain.comの形式を使用し、各アドレスをコンマで区切ります。 通常、この電子メールアドレスは管理者向けです。
1. 「件名」ボックスに、電子メールメッセージの件名行のテキストを入力します。 このフィールドには、デフォルトのテキストが事前入力されています。 このフィールドのカスタマイズについて詳しくは、 [通知の内容のカスタマイズ](configuring-server-settings.md#customizing-the-content-of-notifications).
1. 「通知テンプレート」ボックスに、電子メールメッセージの本文のテキストを入力します。 このフィールドには、デフォルトのテキストが事前入力されています。 このフィールドのカスタマイズについて詳しくは、 [通知の内容のカスタマイズ](configuring-server-settings.md#customizing-the-content-of-notifications).
1. 「メッセージの形式」リストで、E メールメッセージの送信形式 (「HTML」または「テキスト」) を選択します。 デフォルトの形式は「HTML」です。
1. 「 E メールのエンコーディング」リストで、E メールメッセージに使用するエンコーディング形式を選択します。 デフォルトは UTF-8 で、日本以外のほとんどのユーザーが使用します。 日本のユーザーは ISO2022-JPを選択できます。
1. 「保存」をクリックします。

### 停止した操作の通知の設定 {#configure-stalled-operation-notifications}

操作が停止した場合（意図的またはエラーが原因で停止した場合）、問題を調査できる管理者または別のユーザーに電子メール通知を送信できます。

1. 管理コンソールで、サービス/Forms workflow/サーバー設定/管理者通知をクリックします。
1. 「通知タイプ」で、「停止した操作」をクリックします。
1. 「停止した操作を有効にする」を選択します。
1. 「電子メールアドレス」ボックスに、操作が停止したときに通知するユーザーのアドレスを入力します。 user@domain.comの形式を使用し、各アドレスをコンマで区切ります。 通常、この電子メールアドレスは管理者向けです。
1. 「件名」ボックスに、電子メールメッセージの件名行のテキストを入力します。 このフィールドには、デフォルトのテキストが事前入力されています。 このフィールドのカスタマイズについて詳しくは、 [通知の内容のカスタマイズ](configuring-server-settings.md#customizing-the-content-of-notifications)
1. 「通知テンプレート」ボックスに、電子メールメッセージの本文のテキストを入力します。 このフィールドには、デフォルトのテキストが事前入力されています。 このフィールドのカスタマイズについて詳しくは、 [通知の内容のカスタマイズ](configuring-server-settings.md#customizing-the-content-of-notifications).
1. 「保存」をクリックします。

## 通知の内容のカスタマイズ {#customizing-the-content-of-notifications}

タスクの通知ページと管理者の通知ページには、通知メッセージをカスタマイズする次の機能が用意されています。

* リッチテキストエディター
* 変数ピッカー
* URL 生成

### リッチテキストエディター {#rich-text-editor}

通知テンプレート領域は、電子メール通知メッセージのHTMLを生成できるリッチテキストエディターです。 「通知テンプレート」ボックスの下にあるフォントおよび段落書式設定オプションを使用できます。 オプションには、フォントタイプ、サイズ、スタイル、色、段落の整列と箇条書きが含まれます。

### URL 生成 {#url-generation}

タスク通知の場合のみ、Formsワークフローには、事前に定義された 2 つの URL 設定が含まれています。この設定は、「URL 生成」リストから「通知テンプレート」ボックスにドラッグして、カスタマイズできます。

* OpenTask は、 Reminder および Task Assignment 通知タイプで使用できます。 この URL は、Workspace のタスクへのリンクを提供し、ユーザーは電子メール通知からタスクにすばやくアクセスできます。 OpenTask URL を「通知テンプレート」ボックスにドラッグすると、URL は次の形式で表示されます。

  `https://@@notification-host@@:<PORT>/workpace/Main.html?taskId=@@taskid@@`

* ClaimTask は、「グループ — リマインダー」および「グループ — タスクの割り当て」通知タイプで使用できます。 この URL は、Workspace のタスクの詳細ページへのリンクを提供します。ユーザーは、作業項目を要求または要求して開くことができます。 ClaimTask URL を「通知テンプレート」ボックスにドラッグすると、URL は次の形式になります。

  `https://@@notification-host@@:<PORT>/workpace/Main.html?taskId=@@taskid@@`

>[!NOTE]
>
>AEM Forms のリリースでは Flex Workspace は廃止されています。

ソリューションをクラスター環境にデプロイする場合は、`@@notification-host@@` をクラスターアドレスに置き換えます。

`<`*PORT* `>` はアプリケーションサーバーの HTTP リスナーのポート番号です。サポートされるアプリケーションサーバーのデフォルトの HTTP リスナーポートは、以下のとおりです。

**JBoss：** 8080

**Oracle WebLogic Server：** 7001

**IBM WebSphere：** 9080

これらの URL を正しく機能させるには、`<`*PORT* `>` を環境に適したポート番号に置き換えます。

>[!NOTE]
>
>Forms以外のカスタム Web アプリケーションを使用して、ユーザーにタスクへのアクセスを提供する場合は、代わりに、カスタムアプリケーションに適した URL 形式を使用する必要があります。

### 変数ピッカー {#variable-picker}

変数選択リストには、件名ボックスまたは通知テンプレートボックスにドラッグ&amp;ドロップできる便利な変数が表示されます。 「件名」ボックスまたは「通知テンプレート」ボックスに変数をドロップすると、実際の Forms ワークフローの変数名の両端に 2 つの @ 記号が付いたものに変わります（「`@@taskid@@`.@@」など）。

ユーザーまたはグループへのリマインダー、タスクの割り当て、およびデッドラインの場合、「件名」ボックスと「通知テンプレート」ボックスで以下の変数を使用できます。

**description** Workbench 内のプロセスのユーザー手順で定義された説明プロパティの内容。ユーザー手順は、開始ポイント、タスクの割り当て操作、または複数のタスクの割り当て操作です。

**instructions** Workbench 内のプロセスのユーザー手順で定義された、タスクの手順プロパティの内容。

**notification-host** AEM Forms アプリケーションサーバーのホスト名。

**process-name** プロセスの名前。

**operation-name** 手順の名前。

**taskid** 現在のタスクの一意の ID。

**actions** 受信者がクリックできる有効なルート（承認、却下など）の番号付きリストを作成します。

グループリマインダー、グループタスクの割り当て、グループのデッドラインの場合、次の変数も使用できます。

**group-name** 作業項目に割り当てられたグループの名前。

>[!NOTE]
>
>変数に値がない場合は、何も返されません。

停止したブランチの場合、「件名」ボックスと「通知テンプレート」ボックスで、以下の変数を使用できます。

**branch-id** 分岐の識別子。

**process-id** プロセスインスタンスの識別子。

**notification-host** AEM Forms アプリケーションサーバーのホスト名。

停止した操作の場合は、次の変数を「件名」ボックスおよび「通知テンプレート」ボックスで使用できます。

**action-id** 操作の識別子。

**branch-id** 分岐の識別子。

**process-id** プロセスインスタンスの識別子。

**notification-host** AEM Forms アプリケーションサーバーのホスト名。

### 「件名」ボックスでの変数の使用 {#using-a-variable-in-the-subject-box}

[ タスクの割り当て ] 通知の [ 件名 ] ボックスに次のテキストを入力する場合：

`Please complete task @@taskid@@`

タスク 376 が割り当てられると、ユーザーは次の件名のメールを受け取ります。

`Please complete task 376`

### 「通知テンプレート」ボックスでの変数の使用 {#using-variables-in-the-notification-template-box}

停止したブランチの通知の「通知テンプレート」ボックスに、次のテキストを入力する場合：

`Branch @@branch-id@@ has stalled! You have received this notification from @@notification-host@@.`

ブランチ番号が 4868 で、サーバー名が `ServerXYZ` の場合、管理者は次の内容のメールを受け取ります。

`Branch 4868 has stalled! You have received this notification from ServerXYZ.`

## Business Activity Monitoring 接続の設定 {#configuring-business-activity-monitoring-connections}

オプションのモジュールである Business Activity Monitoring は、運用状況と主要業績評価指標をリアルタイムに把握できる一連の運用ダッシュボードを提供します。

BAM の構成設定ページで、BAM を実行するサーバーへの接続を設定し、プロセス関連のイベントを追跡してそのサーバーに送信できるようにします。

1. 管理コンソールで、サービス/Formsワークフロー/サーバー設定/BAM 構成設定をクリックします。
1. 「BAM ホスト」ボックスに、BAM を実行するサーバーの名前を入力します。 デフォルトは localhost です。
1. 「BAM ポート」ボックスに、BAM を実行するサーバーへの接続に使用するポートを入力します。 JBoss のデフォルトの BAM ポートは 8080、WebLogic は 7001、WebSphere は 9080 です。
1. 「サーバーホスト」ボックスに、ホストForms Server の名前または IP アドレスを入力します。 デフォルト値は localhost です。
1. 「 Server Port 」ボックスに、Forms Server で使用するポート番号を入力します。
1. 「ユーザー名」ボックスと「パスワード」ボックスに、BAM サーバーにアクセスする適切なユーザー ID とパスワードを入力します。 デフォルトのユーザー名は CognosNowAdmin で、デフォルトのパスワードは manager です。
1. 「保存」をクリックします。
