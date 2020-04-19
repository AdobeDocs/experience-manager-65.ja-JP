---
title: Connector for EMC Documentum の設定
seo-title: Connector for EMC Documentum の設定
description: Connector for EMC Documentum を AEM Forms と EMC Documentum 間の通信を実現するように設定する方法について説明します。
seo-description: Connector for EMC Documentum を AEM Forms と EMC Documentum 間の通信を実現するように設定する方法について説明します。
uuid: fc96900a-ec8a-4efd-ad8e-25e9967e649b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e62370a7-9d9e-43a3-8014-8e53800c870d
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7

---


# Connector for EMC Documentum の設定 {#configuring-connector-for-emc-documentum}

Connector for EMC Documentum は、AEM Forms と EMC Documentum 間の通信を実現します。関連する参考情報については、「[サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)」の「Connectors for ECM」を参照してください。

Connector for EMC Documentum の設定には、サーバー接続とリポジトリ証明書の各設定が含まれます。

>[!NOTE]
>
>以前のリリースでは、ECM リポジトリにアセットを格納できました。最新のリリースでは、アセットが AEM Forms ネイティブリポジトリに格納され、Repository Provider サービスは推奨されなくなりました。ECM リポジトリから AEM Forms リポジトリへのアセットの移行は、AEM Forms への更新を実行するときに行われます。詳しくは、使用しているアプリケーションサーバー版の AEM Forms アップグレードガイドを参照してください。

## サーバー接続の設定 {#configuring-the-server-connection}

ここでは、環境設定ページで実行できる Connector for EMC Documentum のタスクについて説明します。

>[!NOTE]
>
>すべての設定を同時に行う場合は、「保存」をクリックする必要があるのは一度だけです。

### サーバーの設定 {#configure-the-server}

接続ブローカーサーバー情報を設定する必要があります。この情報は、Documentum コンテンツリポジトリに接続し、Connector for EMC Documentum を起動するために必要です。

1. 管理コンソールで、サービス／Connector for EMC Documentum／環境設定をクリックします。
1. 「Documentum の設定情報」領域で、ホスト名または IP アドレスおよび接続ブローカーのポート番号を入力します。ポート番号は、正の整数（例えば、1489）である必要があります。
1. 「保存」をクリックします。

### プリンシパル秘密鍵証明書の設定 {#configure-principal-credentials}

プリンシパル秘密鍵証明書の設定時に指定するリポジトリ名は、明示的なリポジトリ名がログイン時に示されるかどうかによって異なります。

誤ったユーザー名やパスワードを入力すると、そのサービスが実行中かどうかに応じて、次の結果になります。

* サービス設定情報を保存したときに EMC Documentum Repository Provider サービスと EMC Documentum Content Repository Connector サービスの両方が停止している場合、エラーは表示されません。ただし、次回サービスを起動すると、例外が発生し、サービスは起動しません。
* サービス設定情報を保存したときに EMC Documentum Repository Provider サービスまたは EMC Documentum Content Repository Connector サービスのいずれかが起動している場合、サービスは秘密鍵証明書の情報をすぐに確認しようとします。この場合、エラーが発生し、設定情報は保存されません。

1. 管理コンソールで、サービス／Connector for EMC Documentum／環境設定をクリックします。
1. 「Documentum プリンシパル秘密鍵証明書に関する情報」領域で、上級管理者特権を持つユーザーのユーザー名とパスワードを入力します。
1. ログイン時に明示的なリポジトリ名が示されない場合は、秘密鍵証明書が関連付けられているリポジトリ名を入力します。
1. 「保存」をクリックします。

### リポジトリサービスプロバイダーの変更 {#change-the-repository-service-provider}

Documentum と共に使用するリポジトリサービスプロバイダーを設定できます。リポジトリサービスの呼び出しは、設定したプロバイダーに対して委任されます。以下のオプションが利用できます。

**現在のリポジトリサービスプロバイダー名：** 現在のリポジトリサービスプロバイダー名

**ECM Documentumリポジトリプロバイダ：** Documentumリポジトリプロバイダーをリポジトリのプロバイダーにします。 このオプションは非推奨です。

**リポジトリプロバイダー：** ネイティブリポジトリプロバイダーをリポジトリのプロバイダーにします。

>[!NOTE]
>
>To select a repository service provider other than those listed, configure RepositoryService in Applications and Services > Service Management. <!-- Fix broken link (See Managing Services) -->.

1. 管理コンソールで、サービス／Connector for EMC Documentum／環境設定をクリックします。
1. 「リポジトリサービスプロバイダー」領域で、代替リポジトリサービスプロバイダーを選択します。
1. 「保存」をクリックします。

## リポジトリ証明書の設定 {#configuring-repository-credentials}

Documentum 秘密鍵証明書情報は、AEM Forms のシステムコンテキストで使用されます。リポジトリ証明書は、Documentum の特定のリポジトリに固有のものです。任意の数のリポジトリに対して秘密鍵証明書を提供することができますが、各リポジトリに指定できる秘密鍵証明書のセットは 1 つだけです。

### リポジトリ証明書の追加 {#add-a-repository-credential}

1. 管理コンソールで、サービス／Connector for EMC Documentum／リポジトリ証明書の設定をクリックします。
1. 「追加」をクリックします。Documentum システム秘密鍵証明書に関する情報ページが表示されます。
1. リポジトリの名前を入力します。
1. ユーザー名およびパスワードを入力します。
1. 「保存」をクリックします。

Content Repository Connector for EMC Documentum サービスや Repository Service for EMC Documentum が実行されている場合、秘密鍵証明書情報は、データベースに保存される前に、指定したリポジトリに対して検証されます。秘密鍵証明書が無効な場合または既に存在している場合は、エラーメッセージが表示されます。

### リポジトリ証明書の削除 {#remove-a-repository-credential}

1. 管理コンソールで、サービス／Connector for EMC Documentum／環境設定をクリックします。
1. 証明書を削除するリポジトリ横のチェックボックスをオンにし、「削除」をクリックします。選択したリポジトリに対する秘密鍵証明書がデータベースから削除されます。

### リポジトリ証明書のユーザー名とパスワードの変更 {#change-the-user-name-and-password-for-a-repository-credential}

1. 管理コンソールで、サービス／Connector for EMC Documentum／環境設定をクリックします。
1. 証明書を編集するリポジトリの名前をクリックします。
1. リポジトリのユーザー名またはパスワード、あるいはこの両方を変更します（リポジトリ名は読み取り専用です）。
1. 「保存」をクリックします。

Content Repository Connector for EMC Documentum サービスや Repository Service for EMC Documentum が実行されている場合、秘密鍵証明書情報は、データベースに保存される前に、指定したリポジトリに対して検証されます。秘密鍵証明書が無効な場合または既に存在している場合は、エラーメッセージが表示されます。

## Workspace のタスクキュー共有の要求の有効化 {#enable-the-request-for-sharing-of-workspace-task-queues}

Workspace のタスクキュー共有の要求機能が Connector for EMC Documentum で正常に機能するように、いくつかの手順を手動で行う必要があります。

1. AEM Forms をデプロイして Workbench をインストールした後、Workbench にログインしてリソースビューを開きます。このビューから、QueueSharing.swf ファイルがある場所を調べることができます。
1. QueueSharing.swf ファイルをリソースビューから Windows デスクトップに、またはオペレーティングシステムに応じてそれに対応する場所にドラッグします。
1. 管理コンソールで、サービス／Connector for EMC Documentum／環境設定をクリックします。
1. 「リポジトリサービスプロバイダー」情報で、設定されているリポジトリプロバイダーを「EMC Documentum リポジトリプロバイダー」に変更します。
1. Workbench を起動し、QueueSharing.swf ファイルを最初にコピーした場所（例えば、Windows デスクトップまたは別の場所）から EMC Documentum リポジトリ内部の既存のディレクトリにコピーします。
1. Workbench のプロセスビューで、Queue Sharing プロセスを開きます。
1. 変数ビューで、「theForm」変数のプロパティを開き、手順 5 で QueueSharing.swf ファイルを配置したパスに合わせて URI を変更します。
1. プロセスを保存します。
1. 組織のポリシーに従って、プロセスを実稼働環境に移行します。

