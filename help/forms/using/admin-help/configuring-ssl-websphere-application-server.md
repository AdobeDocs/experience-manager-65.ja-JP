---
title: WebSphere Application Server に対する SSL の設定
seo-title: WebSphere Application Server に対する SSL の設定
description: WebSphere Application Server に対する SSL の設定方法について説明します。
seo-description: WebSphere Application Server に対する SSL の設定方法について説明します。
uuid: f939a806-346e-41e0-b2c0-6d0ba83f8f6f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7c0efcb3-5b07-4090-9119-b7318c8b7980
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1240'
ht-degree: 96%

---


# WebSphere Application Server に対する SSL の設定 {#configuring-ssl-for-websphere-application-server}

ここでは、IBM WebSphere Application Server で SSL を設定する次の手順について説明します。

## WebSphere でのローカルユーザーアカウントの作成 {#creating-a-local-user-account-on-websphere}

SSL を有効にするために、WebSphere はローカル OS ユーザーレジストリ内のシステムの管理権限を持つユーザーアカウントにアクセスする必要があります。

* （Windows）Windows ユーザーを新規作成します。このユーザーは、管理者グループに属し、オペレーティングシステムの一部としての役割を果たす権限を持つように設定します（[WebSphere 用の Windows ユーザーの作成](configuring-ssl-websphere-application-server.md#create-a-windows-user-for-websphere)を参照）。
* （Linux、UNIX）root ユーザーまたは root 権限を持つ別のユーザーのアカウントを使用できます。WebSphere で SSL を有効にする際に、そのユーザーのサーバー ID とパスワードを使用します。

### WebSphere 用の Linux または UNIX ユーザーの作成 {#create-a-linux-or-unix-user-for-websphere}

1. ルートユーザーとしてログインします。
1. コマンドプロンプトに次のコマンドを入力して、新しいユーザーを作成します。

   * (Linux and Sun Solaris) `useradd`
   * (IBM AIX) `mkuser`

1. コマンドプロンプトで `passwd` と入力して、新しいユーザーのパスワードを設定します。
1. （Linux および Solaris）コマンドプロンプトでパラメーターを付けずに `pwconv` と入力して、シャドーパスワードファイルを作成します。

   >[!NOTE]
   >
   >（Linux および Solaris）WebSphere Application Server のローカル OS セキュリティレジストリが機能するには、シャドーパスワードファイルが存在している必要があります。シャドーパスワードファイルは通常、**/etc/shadow** という名前で、/etc/passwd ファイルを基にして作成されます。シャドーパスワードファイルが存在しないと、グローバルセキュリティを有効にしてユーザーレジストリをローカル OS として設定した後でエラーが発生します。

1. /etc ディレクトリにあるグループファイルをテキストエディターで開きます。
1. 手順 2 で作成したユーザーを `root` グループに追加します。
1. ファイルを保存して閉じます。
1. （SSL を有効にした UNIX）root ユーザーとして WebSphere を起動し、停止します。

### WebSphere 用の Windows ユーザーの作成 {#create-a-windows-user-for-websphere}

1. 管理者ユーザーアカウントを使用して Windows にログインします。
1. 「**スタート／コントロールパネル／管理ツール／コンピュータ管理／ローカルユーザーとグループ**&#x200B;を選択します。
1. ユーザーを右クリックして「**New User**」を選択します。
1. 該当するボックスにユーザー名とパスワードを入力し、必要に応じて他のボックスの情報も入力します。
1. 「**User Must Change Password At Next Login**」の選択を解除し、「**Create**」をクリックして「**Close**」をクリックします。
1. 「**Users**」をクリックし、作成したユーザーを右クリックして「**Properties**」を選択します。
1. 「**Member Of**」タブをクリックして、「**Add**」をクリックします。
1. 「選択するオブジェクト名を入力してください」ボックスに、`Administrators` と入力し、「名前の確認」をクリックしてグループ名が正しいことを確認します。
1. 「**OK**」をクリックしてから、「**OK**」を再びクリックします。
1. 「**スタート／コントロールパネル／管理ツール／ローカルセキュリティポリシー／ローカルポリシー**」を選択します。
1. 「ユーザー権利の割り当て」をクリックし、「オペレーティングシステムの一部として機能」を右クリックして、「プロパティ」を選択します。
1. 「**ユーザーまたはグループの追加**」をクリックします。
1. 「Enter The Object Names To Select 」ボックスに、手順 4 で作成したユーザーの名前を入力し、「**Check Names**」をクリックして名前が正しいことを確認してから、「**OK**」をクリックします。
1. 「**OK**」をクリックして、「Act As Part Of The Operating System」プロパティダイアログボックスを閉じます。

### WebSphere が新規作成したユーザーを管理者として使用するように設定します {#configure-websphere-to-use-the-newly-created-user-as-administrator}

1. WebSphere が実行中であることを確認します。
1. WebSphere 管理コンソールで、「**Security／Global Security**」を選択します。
1. 「Administrative」セキュリティで、「**Administrative user roles**」を選択します。
1. 「追加」をクリックして次の手順を実行します。

   1. Type **&amp;ast;** in the search box and click search.
   1. ロールの下の「**Administrator**」をクリックします。
   1. 新規作成したユーザーを「Mapped to role」に追加し、「Administrator」にマッピングします。

1. 「**OK**」をクリックして変更を保存します。
1. WebSphere プロファイルを再起動します。

##  管理セキュリティの有効化 {#enable-administrative-security}

1. WebSphere 管理コンソールで「**Security／Global Security**」を選択します。
1. 「**Security Configuration Wizard**」をクリックします。
1. 「**Enable Application Security**」チェックボックスが有効になっていることを確認します。「**次へ**」をクリックします。
1. **Federated Repositories** を選択し、「**Next**」をクリックします。
1. 設定する資格情報を指定し、「**Next**」をクリックします。
1. 「**Finish**」をクリックします。
1. WebSphere プロファイルを再起動します。

   WebSphere はデフォルトのキーストアと信頼ストアを使用して起動します。

## SSL の有効化 (カスタムキーと信頼ストア) {#enable-ssl-custom-key-and-truststore}

信頼ストアとキーストアは ikeyman ユーティリティまたは管理コンソールを使用して作成できます。 ikeyman を正しく機能させるために、WebSphere インストールパスに括弧が入っていないことを確認してください。

1. WebSphere Administrative Console で「**Security／SSL certificate and key management**」を選択します。
1. 「Related items」で「**Keystores and certificates**」をクリックします。
1. 「**Key store usages**」ドロップダウンで、「**SSL Keystores**」が選択されていることを確認します。「**新規**」をクリックします。
1. 論理名と説明を入力します。
1. キーストアを作成する場所のパスを指定します。 ikeyman を使用してキーストアを既に作成済みの場合、キーストアファイルへのパスを指定します。
1. パスワードを指定して確認します。
1. キーストアタイプを選択して、「**Apply**」をクリックします。
1. マスター構成を保存します。
1. 「**Personal Certificate**」をクリックします。
1. ikeyman を使用してキーストアを既に作成済みの場合、証明書が表示されます。作成済みでない場合は、次の手順を実行して新しい自己署名証明書を追加する必要があります。

   1. 「**Create／Self-signed Certificate**」を選択します。
   1. 証明書フォームで適切な値を指定します。エイリアスと共通名をマシンの完全修飾ドメイン名として保存してください。
   1. 「**適用**」をクリックします。

1. 手順 2 ～ 10 を繰り返して、信頼ストアを作成します。

## カスタムキーストアと信頼ストアをサーバーに適用します {#apply-custom-keystore-and-truststore-to-the-server}

1. WebSphere Administrative Console で「**Security／SSL certificate and key management**」を選択します。
1. 「**Manage endpoint security configuration**」をクリックします。ローカルトポロジマップが開きます。
1. 「Inbound」でノードの直接の子を選択します。
1. 「Related items」で「**SSL configurations**」を選択します。
1. 「**NodeDeafultSSLSetting**」を選択します。
1. 信頼ストア名とキーストア名のドロップダウンリストで、作成したカスタムの信頼ストアとキーストアを選択します。
1. 「**適用**」をクリックします。
1. マスター構成を保存します。
1. WebSphere プロファイルを再起動します。

   これで、プロファイルは SSl 設定と証明書の上で実行されます。

## AEM Forms ネイティブのサポートの有効化 {#enabling-support-for-aem-forms-natives}

1. WebSphere Administrative Console で「**Security／Global Security**」を選択します。
1. 「Authentication」セクションで「**RMI/IIOP security**」を開き、「**CSIv2 inbound communications**」をクリックします。
1. 「Transport」ドロップダウンリストで「**SSL-supported**」が選択されていることを確認します。
1. WebSphere プロファイルを再起動します。

## https で始まる URL を変換するための WebSphere の設定 {#configuring-websphere-to-convert-urls-that-begins-with-https}

https で始まる URL を変換するには、その URL の署名者証明書を WebSphere サーバーに追加します。

**https 対応サイト用署名者証明書の作成**

1. WebSphere が実行中であることを確認します。
1. WebSphere Administrative Console で、「Signer certificates」に移動し、Security／SSL Certificate and Key Management／Key Stores and Certificates／NodeDefaultTrustStore／Signer Certificates をクリックします。
1. 「Retrieve From Port」をクリックし、次のタスクを実行します。

   * 「Host」ボックスに URL を入力します。For example, type `www.paypal.com`.
   * 「Port」ボックスに、`443` と入力します。このポートがデフォルトの SSL ポートです。
   * 「Alias」ボックスに別名を入力します。

1. 「Retrieve Signer Information」をクリックし、情報が取得されたことを確かめます。
1. 「Apply」をクリックし、「Save」をクリックします。

証明書が追加されたサイトでの、HTML から PDF への変換は、Generate PDF サービスからできるようになります。

>[!NOTE]
>
>アプリケーションが WebSphere の内部から SSL サイトに接続するには、署名者証明書が必要です。この証明書は、SSL のハンドシェイク時に接続のリモート側から送信された証明書を、Java Secure Socket Extensions（JSSE）が確認するために使用されます。

## 動的ポートの設定 {#configuring-dynamic-ports}

IBM WebSphere では、グローバルセキュリティが有効な場合、ORB.init() への複数の呼び出しは許可されません。恒久的な制限については、https://www-01.ibm.com/support/docview.wss?uid=swg1PK58704を参照してください。

動的ポートを設定し、問題を解決するには、次の手順を実行してください。

1. WebSphere Administrative Console で、**Servers**／**Server Types**／**WebSphere application server** に移動します。
1. 環境設定のセクションで、使用するサーバーを選択します。
1. 「**Configuration**」タブで、「**Communications**」セクションの下で「**Ports**」を展開し、「**Details**」をクリックします。
1. 次のポート番号をクリックし、「**port number**」を 0 に変更して「**OK**」をクリックします。

   * `ORB_LISTENER_ADDRESS`
   * `SAS_SSL_SERVERAUTH_LISTENER_ADDRESS`
   * `CSIV2_SSL_SERVERAUTH_LISTENER_ADDRESS`
   * `CSIV2_SSL_MUTUALAUTH_LISTENER_ADDRESS`

## sling.properties ファイルを構成します。{#configure-the-sling-properties-file}

1. Open `[aem-forms_root]`\crx-repository\launchpad\sling.properties file for editing.
1. プロパティを見つけ `sling.bootdelegation.ibm` て、その値フィールド `com.ibm.websphere.ssl.*`に追加します。 更新されたフィールドは次のようになります。

   ```java
   sling.bootdelegation.ibm=com.ibm.xml.*, com.ibm.websphere.ssl.*
   ```

1. ファイルを保存し、サーバーを再起動します。

