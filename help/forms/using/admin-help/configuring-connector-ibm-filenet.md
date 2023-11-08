---
title: Connector for IBM FileNet の設定
seo-title: Configuring Connector for IBM FileNet
description: AEM forms とIBM FileNet 間の通信を可能にするIBM FileNet 用 Connector の設定方法について説明します。
seo-description: Learn how to configure the Connector for IBM FileNet to enable communication between AEM forms and IBM FileNet.
uuid: 29d4e221-97f7-4cfb-b7e4-75a8289d2604
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: be4994de-12f8-436e-926a-49a6783b006e
exl-id: f4045df5-a35b-41d7-910e-971017148597
source-git-commit: c4cd9a61a226ace2a72d60b5b7b7432de12cb873
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 17%

---

# Connector for IBM FileNet の設定 {#configuring-connector-for-ibm-filenet}

Connector for IBM FileNet は、AEM forms とIBM FileNet 間の通信を可能にします。 その他の背景情報については、 [サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>以前のリリースでは、ECM リポジトリにアセットを保存できました。 このリリースでは、アセットはAEM forms ネイティブリポジトリに保存され、Repository Provider サービスは非推奨（廃止予定）となりました。 ECM リポジトリからAEM forms リポジトリへのアセットの移行は、AEM forms へのアップグレードの実行時におこなわれます。 詳しくは、ご使用のアプリケーションサーバー版の『 AEM forms アップグレードガイド』を参照してください。

## コンテンツエンジンへの接続を設定 {#configure-the-connection-to-the-content-engine}

IBM FileNet P8 Content Engine は、FileNet コンテンツリポジトリ内のエンタープライズコンテンツと顧客定義ビジネスオブジェクトを管理するためのソフトウェアサービスを提供します。

1. 管理コンソールで、サービス/IBM FileNet 用コネクタをクリックします。
1. 「コンテンツエンジンの URL 」ボックスに、完全な接続 URL を入力します。 次に例を示します。

   FileNet Content Engine 4.x を CEWS トランスポートで使用する場合は、次のように入力します。

   `cemp:https://ContentEngineHostNameorIP:port/wsi/FNCEWS40DIME?jaasConfigurationName=FileNetP8WSI`

   EJB トランスポートで FileNet Content Engine 4.x を使用している場合は、次のように入力します。EJB トランスポートは WebLogic でのみサポートされています。

   `cemp:t3://ContentEngineHostNameorIP:port/FileNet/Engine?jaasConfigurationName=FileNetP8Engine`

1. 「資格情報の保護スキーム」リストで、次の保護レベルのいずれかを選択します。

   * **消去：**&#x200B;保護されていないモードでネットワーク全体に資格情報を送信します。
   * **暗号化：**&#x200B;暗号化された資格情報をネットワーク全体に送信します。

1. 「Encryption File Location」ボックスに、暗号化ファイルのパスを入力します。

   * 秘密鍵証明書の保護スキームとして「消去」を選択した場合、このキーワードとその値は無視されます。
   * 秘密鍵証明書保護スキームとして「対称」を選択した場合、入力したパスは、使用する暗号鍵が含まれているForms Server 上の暗号化ファイルの場所を指します。

1. 「デフォルトのオブジェクトストア」ボックスに、AEM forms がデフォルトで接続するオブジェクトストアコネクタを入力します。
1. 「ユーザー名」ボックスに、前の手順で指定したデフォルトのオブジェクトストアへのアクセス権を持つユーザーのユーザー名を入力します。
1. 「パスワード」ボックスにユーザーのパスワードを入力し、「保存」をクリックします。

## プロセスエンジン設定の指定 {#configure-the-process-engine-settings}

IBM FileNet 用 Connector には、IBM FileNet Process Engine とのやり取りに使用されるIBM FileNet 用 Process Engine Connector サービスが含まれています。 このサービスの設定を構成できます。

1. 管理コンソールで、サービス/IBM FileNet 用コネクタをクリックします。
1. IBM FileNet サービス用の Process Engine Connector を使用できるようにするには、「Use Process Engine Connector Service」を選択します。
1. 「Process Router/Connection Point」ボックスに、ホスト名または IP アドレスとポート番号、その後にプロセスルーターの名前を入力します。 次に例を示します。

   `rmi://ProcessEngineHostNameorIP:port/Name`

1. 「ユーザー名」ボックスに、プロセスエンジンの接続に使用するユーザー名を入力します。
1. 「パスワード」ボックスに、プロセスエンジンの接続に使用するパスワードを入力し、「保存」をクリックします。

## サービス設定の検証 {#validation-of-service-settings}

Content Engine への接続を設定する際に誤ったユーザー名やパスワードを入力した場合、またはプロセスエンジンの設定を行った場合は、サービスが現在実行中かどうかに応じて、次の結果が得られます。

* サービス設定情報を保存したときにIBM FileNet の Repository Provider サービスとIBM FileNet の Content Repository Connector の両方が停止した場合、エラーは表示されません。 ただし、次回サービスを開始する際には例外が発生し、サービスは開始されません。
* IBM FileNet の Repository Provider サービスまたはIBM FileNet の Content Repository Connector を起動した場合、サービス設定情報を保存すると、サービスは資格情報の検証を直ちに試みます。 この場合、エラーが発生し、設定情報は保存されません。

## リポジトリサービスプロバイダーの変更 {#change-the-repository-service-provider}

FileNet で使用するリポジトリサービスプロバイダーを設定できます。 リポジトリサービスの呼び出しは、設定するプロバイダーに委任されます。

以下のオプションが利用できます。

**現在のリポジトリプロバイダー名：** 現在のリポジトリサービスプロバイダーの名前

**IBM FileNet リポジトリプロバイダー：** FileNet リポジトリプロバイダーをリポジトリのプロバイダーにします。 このオプションは非推奨です。

**リポジトリプロバイダー：**&#x200B;ネイティブのリポジトリプロバイダーをリポジトリのプロバイダーにします。

>[!NOTE]
>
>リストに表示された以外のリポジトリサービスプロバイダーを選択するには、アプリケーションおよびサービスで「RepositoryService」を設定します<!-- Fix broken link(See Managing Services) -->

1. 管理コンソールで、サービス/IBM FileNet 用コネクタをクリックします。
1. 「リポジトリサービスプロバイダー」領域で、代替リポジトリサービスプロバイダーを選択し、「保存」をクリックします。
