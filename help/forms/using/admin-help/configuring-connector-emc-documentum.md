---
title: Connector for EMC Documentum の設定
description: AEM forms と EMC Documentum 間の通信を可能にするように Connector for EMC Documentum を設定する方法について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: a31a496f-87b9-43c0-a98c-5f6ca5d11690
source-git-commit: fc2f26a69c208947c14e8c6036825bb217901481
workflow-type: tm+mt
source-wordcount: '1023'
ht-degree: 9%

---

# Connector for EMC Documentum の設定 {#configuring-connector-for-emc-documentum}

Connector for EMC Documentum は、AEM forms と EMC Documentum 間の通信を可能にします。 その他の背景情報については、 [サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

Connector for EMC Documentum の設定では、サーバー接続とリポジトリの資格情報を設定します。

>[!NOTE]
>
>以前のリリースでは、ECM リポジトリにアセットを保存できました。 現在のリリースでは、アセットはAEM forms ネイティブリポジトリに保存され、Repository Provider サービスは非推奨（廃止予定）となっています。 ECM リポジトリからAEM forms リポジトリへのアセットの移行は、AEM forms へのアップグレードの実行時におこなわれます。 詳しくは、ご使用のアプリケーションサーバー版の『 AEM forms アップグレードガイド』を参照してください。

## サーバー接続の設定 {#configuring-the-server-connection}

このトピックでは、設定ページで実行できる Connector for EMC Documentum のタスクについて説明します。

>[!NOTE]
>
>すべての設定を同時に構成する場合は、「保存」を 1 回クリックするだけで済みます。

### サーバーの設定 {#configure-the-server}

接続ブローカーサーバー情報を構成する必要があります。 この情報は、Documentum コンテンツリポジトリに接続し、Connector for EMC Documentum を起動する際に必要です。

1. 管理コンソールで、サービス/Connector for EMC Documentum/設定をクリックします。
1. [Documentum Configuration Information] 領域で、ホスト名または IP アドレスと、接続ブローカーのポート番号を入力します。 ポート番号は正の整数（例：1489）にする必要があります。
1. 「保存」をクリックします。

### プリンシパル秘密鍵証明書の設定 {#configure-principal-credentials}

プリンシパル秘密鍵証明書を設定する際に指定するリポジトリ名は、ログイン時に明示的なリポジトリ名が指定されているかどうかによって異なります。

誤ったユーザー名やパスワードを入力した場合は、サービスが現在実行中かどうかに応じて、次の結果が返されます。

* EMC Documentum Repository Provider サービスと EMC Documentum Content Repository Connector サービスの両方が停止している場合、サービス構成情報を保存してもエラーは表示されません。 ただし、次回サービスを開始する際には例外が発生し、サービスは開始されません。
* EMC Documentum Repository Provider サービスまたは EMC Documentum Content Repository Connector サービスが起動した場合、サービス設定情報を保存すると、サービスは資格情報情報を直ちに検証しようとします。 この場合、エラーが発生し、設定情報は保存されません。

1. 管理コンソールで、サービス/Connector for EMC Documentum/設定をクリックします。
1. 「Documentum プリンシパル秘密鍵証明書情報」領域で、上級管理者権限を持つユーザーのユーザー名とパスワードを入力します。
1. ログイン時に明示的なリポジトリ名が指定されない場合は、資格情報が関連付けられているリポジトリ名を入力します。
1. 「保存」をクリックします。

### リポジトリサービスプロバイダーの変更 {#change-the-repository-service-provider}

Documentum で使用するリポジトリサービスプロバイダーを設定できます。 リポジトリサービスの呼び出しは、設定するプロバイダーに委任されます。 以下のオプションが利用できます。

**現在のリポジトリサービスプロバイダー名：**&#x200B;現在のリポジトリサービスプロバイダーの名前

**ECM Documentum リポジトリプロバイダー：** Documentum リポジトリプロバイダーをリポジトリのプロバイダーにします。このオプションは非推奨です。

**リポジトリプロバイダー**：ネイティブのリポジトリプロバイダーをリポジトリのプロバイダーにします

>[!NOTE]
>
>リストに表示された以外のリポジトリサービスプロバイダーを選択するには、アプリケーションおよびサービス／サービスの管理でリポジトリサービスを設定します。<!-- Fix broken link (See Managing Services) -->

1. 管理コンソールで、サービス/Connector for EMC Documentum/設定をクリックします。
1. 「リポジトリ・サービス・プロバイダ情報」領域で、代替リポジトリ・サービス・プロバイダを選択します。
1. 「保存」をクリックします。

## リポジトリの資格情報の設定 {#configuring-repository-credentials}

Documentum 秘密鍵証明書情報は、AEM forms システムコンテキストで使用されます。 リポジトリの資格情報は、Documentum の特定のリポジトリに固有です。 任意の数のリポジトリに対する資格情報を指定できますが、指定できる資格情報はリポジトリごとに 1 つだけです。

### リポジトリ証明書の追加 {#add-a-repository-credential}

1. 管理コンソールで、サービス/Connector for EMC Documentum/リポジトリ秘密鍵証明書の設定をクリックします。
1. 「追加」をクリックします。[Documentum システム認証情報 ] ページが表示されます。
1. リポジトリの名前を入力します。
1. ユーザー名とパスワードを入力します。
1. 「保存」をクリックします。

Content Repository Connector for EMC Documentum サービスや Repository Service for EMC Documentum が実行されている場合、資格情報情報は、データベースに保存される前に、指定したリポジトリに対して検証されます。 資格情報が無効または存在する場合は、エラーメッセージが表示されます。

### リポジトリの秘密鍵証明書の削除 {#remove-a-repository-credential}

1. 管理コンソールで、サービス/Connector for EMC Documentum/設定をクリックします。
1. 資格情報を削除するリポジトリの横にあるチェックボックスを選択し、「削除」をクリックします。 選択したリポジトリの資格情報がデータベースから削除されます。

### リポジトリ証明書のユーザー名とパスワードの変更 {#change-the-user-name-and-password-for-a-repository-credential}

1. 管理コンソールで、サービス/Connector for EMC Documentum/設定をクリックします。
1. 資格情報を編集するリポジトリの名前をクリックします。
1. リポジトリのユーザー名またはパスワード、あるいはその両方を変更します。 （リポジトリ名は読み取り専用です。）
1. 「保存」をクリックします。

Content Repository Connector for EMC Documentum サービスや Repository Service for EMC Documentum が実行されている場合、資格情報情報は、データベースに保存される前に、指定したリポジトリに対して検証されます。 資格情報が無効または存在する場合は、エラーメッセージが表示されます。

## Workspace のタスクキュー共有のリクエストを有効にする {#enable-the-request-for-sharing-of-workspace-task-queues}

Workspace のタスクキュー共有のリクエスト機能が Connector for EMC Documentum で正しく機能するようにするには、手動の手順が必要です。

1. AEM forms がデプロイされ、Workbench がインストールされたら、Workbench にログインし、Resources ビューを開きます。 このビューから QueueSharing.swf ファイルを配置する場所を決定します。
1. QueueSharing.swf ファイルを Resources View から Windows デスクトップにドラッグするか、オペレーティングシステムに応じて同等の場所にドラッグします。
1. 管理コンソールで、サービス/Connector for EMC Documentum/設定をクリックします。
1. 「Repository Service Provider Information」で、設定済みのリポジトリ・プロバイダを「EMC Documentum Repository Provider」に変更します。
1. Workbench を起動し、最初にコピーした場所（例えば、Windows デスクトップまたは別の場所）から EMC Documentum リポジトリ内の既存のディレクトリに QueueSharing.swf ファイルをコピーします。
1. Workbench の Processes ビューで、Queue Sharing プロセスを開きます。
1. Variables ビューで、「theForm」変数のプロパティを開き、手順 5 で QueueSharing.swf ファイルを配置したパスに合わせて URI を変更します。
1. プロセスを保存します。
1. 組織のポリシーに従って、プロセスを実稼動環境に移行します。
