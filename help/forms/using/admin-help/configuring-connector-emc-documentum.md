---
title: Connector for EMC Documentum の設定
description: Connector for EMC Documentum を AEM Forms と EMC Documentum 間の通信を実現するように設定する方法について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: a31a496f-87b9-43c0-a98c-5f6ca5d11690
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1020'
ht-degree: 100%

---

# Connector for EMC Documentum の設定 {#configuring-connector-for-emc-documentum}

Connector for EMC Documentum は、AEM Forms と EMC Documentum 間の通信を実現します。その他の背景情報について詳しくは、[サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)にある「ECM 用コネクター」を参照してください。

Connector for EMC Documentum の設定には、サーバー接続とリポジトリ証明書の各設定が含まれます。

>[!NOTE]
>
>以前のリリースでは、ECM リポジトリにアセットを格納できました。最新のリリースでは、アセットが AEM Forms ネイティブリポジトリに格納され、リポジトリプロバイダサービスは推奨されなくなりました。ECM リポジトリから AEM Forms リポジトリへのアセットの移行は、AEM Forms への更新を実行する際に行われます。詳しくは、使用しているアプリケーションサーバー版の AEM Forms アップグレードガイドを参照してください。

## サーバー接続の設定 {#configuring-the-server-connection}

ここでは、環境設定ページで実行できる Connector for EMC Documentum のタスクについて説明します。

>[!NOTE]
>
>すべての設定を同時に行う場合は、「保存」を一度だけクリックする必要があります。

### サーバーを設定 {#configure-the-server}

接続ブローカーサーバー情報を設定する必要があります。この情報は、Documentum コンテンツリポジトリに接続し、Connector for EMC Documentum を起動するために必要です。

1. 管理コンソールで、サービス／Connector for EMC Documentum／環境設定をクリックします。
1. 「Documentum の設定情報」領域で、ホスト名または IP アドレスおよび接続ブローカーのポート番号を入力します。ポート番号は、正の整数（1489 など）である必要があります。
1. 「保存」をクリックします。

### プリンシパル秘密鍵証明書を設定 {#configure-principal-credentials}

プリンシパル秘密鍵証明書の設定時に指定するリポジトリ名は、明示的なリポジトリ名がログイン時に示されるかどうかによって異なります。

誤ったユーザー名やパスワードを入力すると、そのサービスが実行中かどうかに応じて、次の結果が得られます。

* サービス設定情報を保存したときに EMC Documentum Repository Provider サービスと EMC Documentum Content Repository Connector サービスの両方が停止している場合、エラーは表示されません。ただし、次回サービスを起動すると、例外が発生し、サービスは開始しません。
* サービス設定情報を保存したときに EMC Documentum Repository Provider サービスまたは EMC Documentum Content Repository Connector サービスのいずれかが起動している場合、サービスは秘密鍵証明書の情報をすぐに確認しようとします。この場合はエラーが発生し、設定情報は保存されません。

1. 管理コンソールで、サービス／Connector for EMC Documentum／環境設定をクリックします。
1. 「Documentum プリンシパル秘密鍵証明書に関する情報」領域で、上級管理者特権を持つユーザーのユーザー名とパスワードを入力します。
1. ログイン時に明示的なリポジトリ名が示されない場合は、秘密鍵証明書が関連付けられているリポジトリ名を入力します。
1. 「保存」をクリックします。

### リポジトリサービスプロバイダーの変更 {#change-the-repository-service-provider}

Documentum と共に使用するリポジトリサービスプロバイダーを設定できます。リポジトリサービスの呼び出しは、設定したプロバイダーに委任されます。以下のオプションが利用できます。

**現在のリポジトリサービスプロバイダー名：**&#x200B;現在のリポジトリサービスプロバイダーの名前

**ECM Documentum リポジトリプロバイダー：** Documentum リポジトリプロバイダーをリポジトリのプロバイダーにします。このオプションは非推奨です。

**リポジトリプロバイダー**：ネイティブのリポジトリプロバイダーをリポジトリのプロバイダーにします

>[!NOTE]
>
>リストに表示された以外のリポジトリサービスプロバイダーを選択するには、アプリケーションおよびサービス／サービスの管理でリポジトリサービスを設定します。<!-- Fix broken link (See Managing Services) -->

1. 管理コンソールで、サービス／Connector for EMC Documentum／環境設定をクリックします。
1. 「リポジトリサービスプロバイダー」領域で、代替リポジトリサービスプロバイダーを選択します。
1. 「保存」をクリックします。

## リポジトリ証明書の設定 {#configuring-repository-credentials}

Documentum 秘密鍵証明書情報は、AEM Forms のシステムコンテキストで使用されます。リポジトリ証明書は、Documentum の特定のリポジトリに固有のものです。任意の数のリポジトリに対して秘密鍵証明書を提供することができますが、各リポジトリに指定できる秘密鍵証明書のセットは 1 つだけです。

### リポジトリ証明書を追加 {#add-a-repository-credential}

1. 管理コンソールで、サービス／Connector for EMC Documentum／リポジトリ証明書設定をクリックします。
1. 「追加」をクリックします。Documentum システム資格情報ページが表示されます。
1. リポジトリの名前を入力します。
1. ユーザー名およびパスワードを入力します。
1. 「保存」をクリックします。

Content Repository Connector for EMC Documentum サービスや Repository Service for EMC Documentum が実行されている場合、資格情報は、データベースに保存される前に、指定したリポジトリに対して検証されます。資格情報が無効な場合または既に存在している場合は、エラーメッセージが表示されます。

### リポジトリ資格情報の削除 {#remove-a-repository-credential}

1. 管理コンソールで、サービス／Connector for EMC Documentum／環境設定をクリックします。
1. 資格情報を削除するリポジトリ横のチェックボックスをオンにし、「削除」をクリックします。選択したリポジトリに対する資格情報がデータベースから削除されます。

### リポジトリ資格情報のユーザー名とパスワードの変更 {#change-the-user-name-and-password-for-a-repository-credential}

1. 管理コンソールで、サービス／Connector for EMC Documentum／環境設定をクリックします。
1. 資格情報を編集するリポジトリの名前をクリックします。
1. リポジトリのユーザー名またはパスワード、あるいはこの両方を変更します。（リポジトリ名は読み取り専用です。）
1. 「保存」をクリックします。

Content Repository Connector for EMC Documentum サービスや Repository Service for EMC Documentum が実行されている場合、資格情報は、データベースに保存される前に、指定したリポジトリに対して検証されます。資格情報が無効な場合または既に存在している場合は、エラーメッセージが表示されます。

## Workspace タスクキューの共有リクエストの有効化 {#enable-the-request-for-sharing-of-workspace-task-queues}

Workspace タスクキューの共有リクエスト機能が Connector for EMC Documentum で正常に機能するように、いくつかの手順を手動で行う必要があります。

1. AEM Forms をデプロイして Workbench をインストールした後、Workbench にログインしてリソースビューを開きます。このビューから、QueueSharing.swf ファイルがある場所を調べることができます。
1. オペレーティングシステムに応じて、QueueSharing.swf ファイルをリソースビューから Windows デスクトップまたは同等の場所にドラッグします。
1. 管理コンソールで、サービス／Connector for EMC Documentum／環境設定をクリックします。
1. リポジトリサービスプロバイダー情報で、設定されているリポジトリプロバイダーを「EMC Documentum リポジトリプロバイダー」に変更します。
1. Workbench を起動し、QueueSharing.swf ファイルを最初にコピーした場所（例えば、Windows デスクトップまたは別の場所）から EMC Documentum リポジトリ内部の既存のディレクトリにコピーします。
1. Workbench のプロセスビューで、キュー共有プロセスを開きます。
1. 変数ビューで、「theForm」変数のプロパティを開き、手順 5 で QueueSharing.swf ファイルを配置したパスに合わせて URI を変更します。
1. プロセスを保存します。
1. 組織のポリシーに従って、プロセスを実稼動環境に移行します。
