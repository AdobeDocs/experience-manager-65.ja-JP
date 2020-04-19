---
title: Connector for IBM FileNet の設定
seo-title: Connector for IBM FileNet の設定
description: AEM Forms と IBM FileNet 間の通信を有効化するように Connector for IBM FileNet を設定する方法について説明します。
seo-description: AEM Forms と IBM FileNet 間の通信を有効化するように Connector for IBM FileNet を設定する方法について説明します。
uuid: 29d4e221-97f7-4cfb-b7e4-75a8289d2604
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: be4994de-12f8-436e-926a-49a6783b006e
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7

---


# Connector for IBM FileNet の設定 {#configuring-connector-for-ibm-filenet}

Connector for IBM FileNet は、AEM Forms と IBM FileNet 間の通信を実現します。関連する参考情報については、「[サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)」の「Connectors for ECM」を参照してください。

>[!NOTE]
>
>以前のリリースでは、ECM リポジトリにアセットを格納できました。このリリースでは、アセットが AEM Forms ネイティブリポジトリに格納され、Repository Provider サービスは推奨されなくなりました。ECM リポジトリから AEM Forms リポジトリへのアセットの移行は、AEM Forms への更新を実行するときに行われます。詳しくは、使用しているアプリケーションサーバー版の AEM Forms アップグレードガイドを参照してください。

## Content Engine への接続の設定 {#configure-the-connection-to-the-content-engine}

IBM FileNet P8 Content Engine では、FileNet コンテンツリポジトリで企業コンテンツおよび顧客が定義したビジネスオブジェクトを管理するためのソフトウェアサービスを使用できます。

1. 管理コンソールで、サービス／Connector for IBM FileNet をクリックします。
1. 「コンテンツエンジンの URL」ボックスに、完全な接続 URL を入力します。次に例を示します。

   CEWS トランスポートで FileNet Content Engine 4.x を使用している場合は、次のように入力します。

   `cemp:https://ContentEngineHostNameorIP:port/wsi/FNCEWS40DIME?jaasConfigurationName=FileNetP8WSI`

   EJB トランスポートで FileNet Content Engine 4.x を使用している場合は、次のように入力します。EJB トランスポートは WebLogic でのみサポートされています。

   `cemp:t3://ContentEngineHostNameorIP:port/FileNet/Engine?jaasConfigurationName=FileNetP8Engine`

1. 「資格情報の保護スキーム」リストで、次の保護レベルのいずれかを選択します。

   * **消去：**&#x200B;保護されていないモードでネットワーク全体に秘密鍵証明書を送信します。
   * **暗号化：**&#x200B;暗号化された秘密鍵証明書をネットワーク全体に送信します。

1. 「暗号化ファイルの場所」ボックスに、暗号化ファイルへのパスを入力します。

   * 秘密鍵証明書の保護スキームとして「消去」を選択した場合、このキーワードとその値は無視されます。
   * 秘密鍵証明書の保護スキームとして「暗号化」を選択した場合、入力したパスは、使用される暗号キーを含む forms サーバー上の暗号化ファイルの場所を指します。

1. 「初期設定のオブジェクトストア」ボックスに、AEM Forms がデフォルトで接続するオブジェクトストアコネクタを入力します。
1. 「ユーザー名」ボックスに、前の手順で指定したデフォルトオブジェクトストアへのアクセス権を持つユーザーのユーザー名を入力します。
1. 「パスワード」ボックスにユーザーのパスワードを入力し、「保存」をクリックします。

## プロセスエンジン設定の指定 {#configure-the-process-engine-settings}

Connector for IBM FileNet には、IBM FileNet Process Engine とのやり取りに使用される Process Engine Connector for IBM FileNet サービスが含まれています。このサービスの設定を指定することができます。

1. 管理コンソールで、サービス／Connector for IBM FileNet をクリックします。
1. Process Engine Connector for IBM FileNet サービスを使用できるようにするには、「プロセスエンジンコネクタサービスを使用」を選択します。
1. 「プロセスルーター／接続ポイント」ボックスに、ホスト名または IP アドレス、ポート番号、プロセスルーター名を入力します。次に例を示します。

   `rmi://ProcessEngineHostNameorIP:port/Name`

1. 「ユーザー名」ボックスに、プロセスエンジンへの接続に使用するユーザー名を入力します。
1. 「パスワード」ボックスにプロセスエンジンへの接続に使用するパスワードを入力し、「保存」をクリックします。

## サービス設定の検証 {#validation-of-service-settings}

Content Engine への接続またはプロセスエンジン設定を指定する場合に誤ったユーザー名やパスワードを入力すると、そのサービスが実行中かどうかに応じて、次の結果になります。

* サービス設定情報を保存したときに IBM FileNet 用の Repository Provider サービスと Content Repository Connector for IBM FileNet サービスの両方が停止している場合、エラーは表示されません。ただし、次回サービスを起動すると、例外が発生し、サービスは起動しません。
* サービス設定情報を保存したときに IBM FileNet 用の Repository Provider サービスまたは Content Repository Connector for IBM FileNet サービスのいずれかが起動している場合、サービスは資格情報をすぐに確認しようとします。この場合、エラーが発生し、設定情報は保存されません。

## リポジトリサービスプロバイダーの変更 {#change-the-repository-service-provider}

FileNet と共に使用するリポジトリサービスプロバイダーを設定できます。リポジトリサービスの呼び出しは、設定したプロバイダーに対して委任されます。

以下のオプションが利用できます。

**現在のリポジトリプロバイダー名：** 現在のリポジトリサービスプロバイダー名

**IBM FileNetリポジトリプロバイダー：** FileNetリポジトリプロバイダーをリポジトリのプロバイダーにします。 このオプションは非推奨です。

**リポジトリプロバイダー：** ネイティブリポジトリプロバイダーをリポジトリのプロバイダーにします。

>[!NOTE]
>
>リストに表示された以外のリポジトリサービスプロバイダーを選択するには、アプリケーションおよびサービスで「RepositoryService」を設定します<!-- Fix broken link(See Managing Services) -->

1. 管理コンソールで、サービス／Connector for IBM FileNet をクリックします。
1. 「リポジトリサービスプロバイダー」領域で、代替リポジトリサービスプロバイダーを選択し、「保存」をクリックします。
