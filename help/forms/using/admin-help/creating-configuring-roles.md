---
title: ロールの作成および設定
seo-title: ロールの作成および設定
description: 既に User Management データベースの一部であるロールにユーザーおよびグループを関連付ける方法について説明します。ロールの作成、編集および削除もできます。
seo-description: 既に User Management データベースの一部であるロールにユーザーおよびグループを関連付ける方法について説明します。ロールの作成、編集および削除もできます。
uuid: e8e4331d-48e1-4fa9-8f44-f885f4ab1a54
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 737fb4d1-adef-47e1-9a0d-8cddd13132cb
translation-type: tm+mt
source-git-commit: 413af4ef9bc3652e05da78d622183bcf20a8bee7

---


# ロールの作成および設定{#creating-and-configuring-roles}

User Management Web ページでは、既に User Management データベースの一部であるロールにユーザーおよびグループを関連付けることができます。ロールの作成、編集および削除もできます。

User Management には、次の 2 種類のロールがあります。

**** 可変ロール：この種類のロールは編集および削除でき、ロール権限はこれらのロールタイプに対して追加および削除できます。 作成したロールはすべて可変ロールと見なされます。可変ロールにアサインされるユーザーおよびグループを追加または削除できます。

**** 不変ロール：User Managementに含まれるデフォルトのロールは不変ロールです。 このロールを編集または削除することはできません。ただし、不変ロールにアサインされるユーザーおよびグループを追加したり削除したりすることはできます。

可変ロールと不変ロールはどちらも AEM forms API を使用して作成することもできます。

## デフォルトのロール {#default-roles}

User Management データベースには、次のデフォルトのロールが含まれています。

**** 管理コンソールユーザー：管理コンソールにアクセスできます。

**** アプリケーション管理者：Workbenchのすべての機能を使用できます。 管理コンソールのアプリケーションおよびサービスページを使用して、サービスの実行時プロパティ、エンドポイント、およびセキュリティを設定できます。

**** AEM forms管理者：インストールされているすべてのサービスに対して、すべてのタスクを実行できます。

**** セキュリティ管理者：User Managementの設定を制御し、User Managerドメインに関連付けられているユーザーとグループを管理します

**** サービスユーザー：任意のサービスを表示して呼び出すことができます

**** 上級管理者：サービスを含む、システム内のすべての管理機能にアクセス可能

**** 信頼管理者：管理コンソールのTrust storeの管理ページで管理されるPKI信頼設定およびPKI秘密鍵証明書を管理できます。

### 追加のデフォルトのロール {#additional-default-roles}

インストールした AEM Forms コンポーネントによっては、次の追加のデフォルトのロールが含まれる場合があります。

**** ドキュメントアップロードアプリユーザ：Flex Remotingを使用してドキュメントをアップロードできます。

**** Forms管理者：管理コンソールのFormsページの設定を表示して変更できます。

**** AEM forms Contentspace管理者：管理コンソールのContent Services（非推奨）ページの設定を表示して変更できます。

**** AEM forms Contentspaceユーザー：Contentspace（非推奨）Webページにログインできます。

**** Documentum Connector管理者：管理コンソールのConnector for EMC Documentumページの設定を表示して変更できます。

**** AEM forms fileNet Connector管理者：管理コンソールのConnector for IBM fileNetページの設定を表示して変更できます。

**** AEM forms IBM CM Connector管理者：管理コンソールのConnector for IBM Content Managerページの設定を表示して変更できます。

**** Rights Management Administrator:すべてのサーバー設定に必要なすべてのタスクを、関連するRights Managementページで実行します

**** Rights Management End User:Rights ManagementエンドユーザーWebページにアクセスできます。

**** Rights Management Invite User:ユーザーを招待できます

**** Rights Management Manage Invited and Local Users:すべての招待ユーザーおよびローカルユーザーの管理に必要なタスクを、関連するRights Managementページで実行できます。

**** Rights Management Policy Set Administrator:すべてのポリシーセットに必要なすべてのタスクを、関連するRights Managementページで実行します

**** Rights Management Super Administrator:必要なすべてのタスクをRights Managementページから実行します

**** AEM forms Workspace管理者：管理コンソールのWorkspaceページの設定を表示して変更できます

***注意&#x200B;**：AEM Forms のリリースでは Flex Workspace は廃止されています。*

**** Workspaceユーザー：Workspaceエンドユーザーアプリケーションにログインできます。

**** Output管理者：管理コンソールのOutputページの設定を表示して変更できます。

**** PDFG管理者：管理コンソールのPDF Generatorページの設定を表示して変更できます。

**** PDFG User:PDF Generatorの管理者以外のすべての機能にアクセスできます。

**** Acrobat Reader DC Extensions webアプリケーション：Acrobat Reader DC Extensions webアプリケーションを使用できます。

>[!NOTE]
>
>特定の種類の管理者権限を持つユーザーは、セキュリティ上の理由から Workspace のエンドユーザー Web ページにアクセスできません。これらのページはファイアウォールの外部に存在することがあるので、管理レベルのタスクを許可することによってセキュリティ上の問題を引き起こす可能性があります。AEM Forms Workspace のエンドユーザー Web ページにアクセスできるのは、AEM Forms Workspace 管理者または AEM Forms Workspace ユーザーの権限を持つユーザーだけです。

>[!NOTE]
>
>AEM Forms のリリースでは Flex Workspace は廃止されています。

## ロールの作成 {#create-a-role}

1. 管理コンソールで、設定／User Management／ロールの管理をクリックし、「新規ロール」をクリックします。
1. 「ロール名」ボックスにロールの名前を入力し、必要に応じてロールの説明を入力して、「次へ」をクリックします。

   >[!NOTE]
   >
   >MySQL を使用する場合は、拡張文字だけが異なる同じ名前を使用して 2 つのロールを作成することはできません。例えば、ロール名 âbcdè が既に使用されている場合に、ロール名 abcde を作成しようとするとエラーが発生します。

1. 「権限を検索」をクリックして、ロールに追加する権限を選択します。
1. 「OK」をクリックし、「次へ」をクリックします。
1. ユーザーおよびグループにこのロールをアサインします。

   * 「ユーザーまたはグループを検索」をクリックします。
   * 「検索」ボックスに検索条件を入力します。
   * 「名前」、「電子メール」または「ユーザー ID」を選択し、「ユーザー」、「グループ」または「ユーザーとグループ」を選択します。
   * ドメインを選択し、表示する結果数を選択して、「検索」をクリックします。
   * このロールのアサイン先のユーザーとグループのチェックボックスを選択し、「OK」をクリックします。

1. ユーザーおよびグループの詳細を表示するには、そのエンティティを選択します。
1. 「OK」をクリックし、「完了」をクリックします。

## ロールの編集 {#edit-a-role}

1. 管理コンソールで、設定／User Management／ロールの管理をクリックし、「ロール名」をクリックします。

   デフォルトでは、ロールの管理ページに、User Management データベースに格納されているすべてのロールが表示されます。ロールのリストが大きい場合は、ページの最上部にある「検索」領域を使用して、特定のロール名を検索できます。

1. 編集するロールをクリックし、一般設定を編集して、「保存」をクリックします。
1. ロールの権限を編集するには、「権限」タブをクリックして次のタスクを実行します。

   * 新しい権限を追加するには、「権限を検索」をクリックして追加する権限のチェックボックスを選択し、「OK」をクリックして「保存」をクリックします。
   * ロールから権限を削除するには、目的の権限のチェックボックスを選択して「削除」をクリックし、「保存」をクリックします。

1. ロールのアサイン先を管理するには、「ロールのユーザー」タブをクリックし、次のタスクを実行します。

   * 新しいユーザーおよびグループにロールをアサインするには、「ユーザーまたはグループを検索」をクリックして検索情報を入力します。このロールをアサインするユーザーおよびグループのチェックボックスを選択して「OK」をクリックし、「保存」をクリックします。
   * ロールを削除するには、目的のユーザーまたはグループのチェックボックスを選択して「アサイン解除」をクリックし、「保存」をクリックします。

## ロールの削除 {#delete-a-role}

製品に含まれている AEM Forms のデフォルトのロールを除き、作成した任意のロールを削除できます。

1. 管理コンソールで、設定／User Management／ロールの管理をクリックし、「ロール名」をクリックします。

   デフォルトでは、ロールの管理ページに、User Management データベースに格納されているすべてのロールが表示されます。ロールのリストが大きい場合は、ページの最上部にある「検索」領域を使用して、特定のロール名を検索できます。

1. 削除するロールのチェックボックスを選択して「削除」をクリックし、「OK」をクリックします。

## ユーザーおよびグループへのロールのアサイン {#assign-a-role-to-users-and-groups}

1. 管理コンソールで、設定／User Management／ユーザーとグループをクリックします。
1. 検索条件を絞り込む情報を指定し、「検索」をクリックします。検索の結果がページの下部に表示されます。列見出しをクリックすると、リストを並べ替えることができます。
1. ロールに関連付けるユーザーおよびグループの横のチェックボックスを選択し、「ロールをアサイン」をクリックします。
1. ユーザーまたはグループにアサインするロールを選択し、「OK」をクリックします。

ロールの管理ページを使用してロールをアサインすることもできます。

## ロールにアサインされているユーザーおよびグループの確認 {#determine-who-is-assigned-to-a-role}

1. 管理コンソールで、設定／User Management／ロールの管理をクリックし、「ロール名」をクリックします。

   デフォルトでは、ロールの管理ページに、User Management データベースに格納されているすべてのロールが表示されます。ロールのリストが大きい場合は、ページの最上部にある「検索」領域を使用して、特定のロール名を検索できます。

1. ロールの詳細ページで「ロールのユーザー」タブをクリックします。ロールに直接関連付けられているユーザーおよびグループのリストが表示されます。

## ロールの権限の変更 {#change-role-permissions}

自分が作成したロールの権限を変更できます。製品に含まれている AEM Forms のデフォルトのロールの権限は変更できません。

1. 管理コンソールで、設定／User Management／ロールの管理をクリックし、「ロール名」をクリックします。

   デフォルトでは、ロールの管理ページに、User Management データベースに格納されているすべてのロールが表示されます。ロールのリストが大きい場合は、ページの最上部にある「検索」領域を使用して、特定のロール名を検索できます。

1. 権限を表示するロールを選択し、「権限」タブをクリックします。
1. 権限を変更するには、「権限を検索」をクリックしてロールに追加する権限のチェックボックスを選択し、「OK」をクリックして「保存」をクリックします。
1. 権限を削除するには、目的の権限を選択して「削除」をクリックし、「保存」をクリックします。

### AEM Forms の権限 {#aem-forms-permissions}

**** ADD_REMOVE_ENDPOINT_PERM:サービスのエンドポイントの追加、削除および変更

**** 管理コンソールログイン：管理コンソールの表示

**** Certificate Modify:Trust storeの証明書の信頼設定を変更します

**** Certificate Read:Trust storeの証明書を読み取ります

**** Certificate Write:証明書をTrust Storeに追加する

**** コンポーネントの追加：システムに新しいコンポーネントをインストールする

**** コンポーネントの削除：システム内の任意のコンポーネントを削除します

**** 読み取りコンポーネント：システム内の任意のコンポーネントを読み取ります

**** Contentspace管理者：Contentspace（非推奨）管理者の権限です

**** Contentspaceコンソールログイン：Contentspace（非推奨）コンソールログインの権限

**** コア設定コントロール：管理コンソールのコアシステム設定ページで設定を管理します

**** CREATE_VERSION_PERM:サービスの新しいバージョンの作成

**** Credential Modify:Trust Storeの署名資格情報を変更します

**** Credential Read:Trust Storeの署名証明書を読み取ります

**** Credential Write:署名証明書をTrust storeに追加する

**** CRL Modify:Trust StoreのCRL（証明書失効リスト）を変更します

**** CRL Read:Trust StoreのCRLを読み取ります

**** CRL Write:CRLをTrust storeに追加

**** 委任：リソースにACLを設定する

**** DELETE_VERSION_PERM:サービスのバージョンの削除

**** ドキュメントのアップロード：AEM formsでのドキュメントのアップロード

**** ドメインコントロール：User Managementドメインの設定（認証プロバイダーやディレクトリプロバイダーを含む）を作成、削除、または変更します

**** Event Type Edit:イベントタイプを編集

**** Identity Impersonation Control:User ManagerでIDを偽装する

**** INVOKE_PERM:サービスのすべての操作を呼び出す

**** LCDS Data Model Control:Data Servicesでのデータモデルの読み取りとデプロイ

**** License Managerの更新：ライセンス情報の更新

**** MODIFY_CONFIG_PERM:サービスの設定の変更

**TERM** Modify the version of a service

**** PDFGAdminPermission:PDFG管理者

**** PDFGUserPermission:PDFGユーザー

**** PERM_DCTM_ADMIN:Documentum Connector管理者

**** PERM_FILENET_ADMIN:FileNet Connector管理者

**** PERM_FORMS_ADMIN:Forms管理者

**** PERM_IBMCM_ADMIN:IBM CM Connector管理者

**** PERM_OUTPUT_ADMIN:Output管理者

**** PERM_READER_EXTENSIONS_WEB_APPLICATION:Acrobat Reader DC Extensions webアプリケーションの使用

**** PERM_SP_ADMIN:SharePoint Connectorの設定を管理

**** PERM_WORKSPACE_ADMIN:Workspace設定の管理

**** PERM_WORKSPACE_USER:Workspaceエンドユーザーアプリケーションにログインします。

**** プリンシパルコントロール：任意のドメインのユーザーとグループを管理し、任意のドメインのすべてのユーザーとグループのロール割り当てを管理します

**** Process Recording Read/Delete:ワークフロー監査インスタンスのリストと取得

**** PROCESS_OWNER_PERM:トレンドデータを表示し、プロセスから作成されたサービスに対して管理操作を実行します

**** 読み取り：リソースの内容の読み取り

**** READ_PERM:サービスの読み取りまたは表示

**** アサーションの更新：User Managementでのアサーションの更新

**** Repository Delegate:リソースにACLを設定する

**** Repository Read:リソースの内容の読み取り

**** Repository Traverse:リソースリクエストにリソースを含めるか、リソースのメタデータを読み取ります

**** Repository Write:リポジトリのメタデータとコンテンツの書き込み

**** Rights Management Change Policy Owner:ポリシー所有者の変更

**** Rights Management End User Console Login:Rights Management End User UIにログインします。

**** Rights Management Manage Configuration:サーバー設定の管理

**** Rights Management Manage Invited and Local Users:招待ユーザーとローカルユーザーの管理

**** Rights Management Manage Policy Sets:ポリシーセット内のすべてのポリシーとドキュメントを管理

**** Rights Management Policy Set Add Coordinator:ポリシーセットコーディネーターの権限の追加、削除、変更

**** Rights Management Policy Set Create Policy:ポリシーセットの新しいポリシーの作成

**** Rights Management Policy Set Delete Policy:ポリシーセットからのポリシーの削除

**** Rights Management Policy Set Edit Policy:ポリシーセット内のポリシーの編集

**** Rights Management Policy Set Manage Document Publisher:ポリシーセットを作成する場合は、ユーザーにドキュメント発行者のロールを割り当てます。 ドキュメント発行者は、ドキュメントをポリシーで保護するユーザーです。

**** Rights Management Policy Set Remove Coordinator:ポリシーセットコーディネーターのポリシーセットからの削除

**** Rights Management Policy Set Revoke Document:ポリシーセット内のドキュメントへのアクセス権限の失効

**** Rights Management Policy Set Switch Policy:ドキュメントのポリシーの切り替え

**** Rights Management Policy Set Unrevoke Document:ドキュメントの失効取り消し

**** Rights Management Policy Set View Event:ポリシーセット内のポリシーまたはドキュメントのポリシーイベントとドキュメントイベントの表示

**** Rights Management View Server Events:すべての監査イベントの検索と表示

**** Role Control:User Managementでのロールの作成、削除および変更

**** Service Activate:任意のサービスを開始し、呼び出しに使用できるようにします

**** サービスの追加：新しいサービスをサービスレジストリにデプロイします。 新しいプロセスとプロセスバリアントの追加が含まれます。

**** Service Deactivate:システム内のサービスを停止します

**** サービスの削除：プロセスおよびプロセスバリアントを含む、システム内のサービスを削除します

**** サービス呼び出し：実行時に使用可能なサービスレジストリの任意のサービスを呼び出します

**** サービスの変更：システム内の任意のサービスの設定プロパティを変更します。 IDE のサービスのロックとロック解除、サービスへのエンドポイントの追加、サービスからのエンドポイントの削除が含まれます。

**** Service Read:システム内のサービスを読み取ります。 すべてのプロセスとプロセスバリアントが含まれます。

**** SERVICE_AGENT_PERM:データを表示し、プロセスから作成されたサービスのプロセスインスタンスを操作します

**** SERVICE_MANAGER_PERM:プロセスから作成されたサービスに対するロードバランシングおよびその他の管理操作の実行

**** START_STOP_PERM:サービスの開始または停止

**** SUPERVISOR_PERM:プロセスから作成されたサービスのプロセスインスタンスデータの表示

**** トラバース：リソースリクエストにリソースを含めるか、リソースのメタデータを読み取ります

**** 書き込み：リポジトリのメタデータとコンテンツの書き込み

**Workbench でファイルを開く**

Workbench でリソースビューのコンテンツを表示し、ファイルを開いて表示するには、ユーザーに次の権限が必要です。

* Repository Read
* Repository Traverse
* Service Invoke
* Service Read

## ロールからのユーザーまたはグループの削除 {#remove-a-user-or-group-from-a-role}

ロールの管理ページを使用して、特定のロールからユーザーおよびグループを削除します。ユーザーまたはグループがロールアサインを継承している場合は、ユーザーまたはグループレベルでロールを削除することはできません。継承ツリーからユーザーまたはグループを削除するか、親からロールを削除します。

1. 管理コンソールで、設定／User Management／ロールの管理をクリックし、「ロール名」をクリックします。

   デフォルトでは、ロールの管理ページに、User Management データベースに格納されているすべてのロールが表示されます。ロールのリストが大きい場合は、ページの最上部にある「検索」領域を使用して、特定のロール名を検索できます。

1. ロールのリストで、更新するロールの名前をクリックし、「ロールのユーザー」タブをクリックします。ロールに関連付けられているユーザーおよびグループのリストが表示されます。
1. ロールから削除するユーザーおよびグループのチェックボックスを選択し、「アサイン解除」をクリックします。
1. 「保存」をクリックし、「OK」をクリックします。

