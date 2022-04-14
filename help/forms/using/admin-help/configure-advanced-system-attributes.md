---
title: 詳細なシステム属性の設定
seo-title: Configure advanced system attributes
description: システム属性の詳細設定ページを使用して、ファイルの書き出し、編集、読み込みを行うことなく、設定ファイルの特定の設定を変更します。
seo-description: Use the Configure Advanced System Attributes page to modify certain settings in the configuration file without the need to export, edit, and import the file.
uuid: 6bcfbaa9-f492-46aa-97d2-00fc3e67d0d7
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 533ad3f7-3905-420d-8bb9-8ae8f14fb28e
exl-id: 809af2c0-6f5c-4dd4-af48-dbf476c9ea45
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '475'
ht-degree: 100%

---

# 詳細なシステム属性の設定 {#configure-advanced-system-attributes}

システム属性の詳細設定ページを使用して、ファイルの書き出し、編集、読み込みを行うことなく、設定ファイルの特定の設定を変更します。（[設定ファイルの読み込みと書き出し](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file)を参照）。

1. 管理コンソールで、**[!UICONTROL 設定／User Management／設定／システム属性の詳細設定]**&#x200B;をクリックしてください。
1. （オプション）次のセッション属性を変更します。

   **セッションのタイムアウト制限（分）：**&#x200B;ユーザーが自動的にシステムからログアウトするまでの時間（分）。デフォルトでは、Workbench などの AEM Forms のコンポーネントは、動作状況に関係なく 2 時間後にタイムアウトになり、ユーザーは再度ログインする必要があります。有効な値は `1`～`1440` です。デフォルト値は `120`（2 時間）です。この設定では、設定ファイルの `SAML/Producer/assertionValidityInMinutes` エントリキーがアップデートされます。

   >[!NOTE]
   >
   >セッションのタイムアウト制限を 10 分未満に設定しないでください。10 分未満では、システムが正しく機能しない可能性があります。推奨される値は 10～120 (分) です。

   **アサーションのしきい値（秒）：**&#x200B;クラスター内の AEM Forms アプリケーションサーバー間で発生するシステム時間の時間差が原因となる遅延を相殺するバッファー時間。AEM Forms のユーザーのログイン時間は、このプロパティで指定された時間（秒）だけ遡ります。有効な値は `0`～`3600` です。デフォルト値は `60` です。この設定では、設定ファイルの `SAML/Producer/assertionThresholdInSeconds` エントリキーがアップデートされます。

   **アサーションの最大更新可能回数：**&#x200B;ログインを必要とせずにユーザーセッションが透過的に更新される最大回数。有効な値は `0`～`9999` です。`0` に設定すると、アサーションは更新されません。デフォルト値は 10 です。この設定では、設定ファイルの `SAML/Producer/maxAssertionRenewalCount` エントリキーが更新されます。

1. （オプション）次のディレクトリ同期属性のいずれかを変更します。

   **同期統計ログ：** User Management で、同期処理中に詳細な統計情報をログに記録するかどうかを指定します。（[同期中の詳細なログの有効化または無効化](/help/forms/using/admin-help/synchronizing-directories.md#enable-or-disable-detailed-logging-during-synchronization)を参照）。

   **同期完了の Cron 形式：** User Management で失敗した同期を再試行する間隔。（[ディレクトリ同期の再試行オプションの設定](/help/forms/using/admin-help/synchronizing-directories.md#configure-the-directory-synchronization-retry-option)を参照。）

   **クラスターのジョブロックのタイムアウト（分）：**&#x200B;クラスター環境で使用されます。1 つのノードで同期が失敗し、クラスターのロックが解放されない場合、この値が、他のノードが強制的にロックを取得するまでの待ち時間（分）を指定します。デフォルト値は `15` 分です。有効な値は `1`～`1440` 分です。

1. （オプション）次の属性を変更し、「**[!UICONTROL OK]**」をクリックしてください。

   **User Manager イベント監査：**&#x200B;ディレクトリ同期イベントと認証イベントの監査（成功、失敗、ロックアウトなど）を有効にするにはこのオプションを選択します。デフォルトでは、Rights Management などの監査を必要とするコンポーネントをインストールしない限り、このオプションは選択されません。この設定では、設定ファイルの `APSAuditService` エントリキーがアップデートされます。

   **動的グループの自動作成：**&#x200B;メールのドメインに基づいた動的グループの自動作成を有効にします。（[動的グループの作成](/help/forms/using/admin-help/creating-configuring-groups.md#create-a-dynamic-group)を参照。）

また、「再読み込み」をクリックして、元の User Management 設定に戻すこともできます。
