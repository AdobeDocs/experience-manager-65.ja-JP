---
title: JBoss Application Server に対する SSL の設定
seo-title: JBoss Application Server に対する SSL の設定
description: JBoss Application Server に対する SSL の設定方法について説明します。
seo-description: JBoss Application Server に対する SSL の設定方法について説明します。
uuid: 7c13cf00-ea89-4894-a4fc-aaeec7ae9f66
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c187daa4-41b7-47dc-9669-d7120850cafd
translation-type: tm+mt
source-git-commit: b703c59d7d913fc890c713c6e49e7d89211fd998
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 50%

---


# JBoss Application Server に対する SSL の設定 {#configuring-ssl-for-jboss-application-server}

JBoss Application Server で SSL を設定するには、認証時に SSL 秘密鍵証明書が必要です。秘密鍵証明書は、Java keytool を使用して作成するか、認証局（CA）から要求して読み込むことができます。その後、JBoss で SSL を有効にする必要があります。

1 つのコマンドでキーストアの作成に必要なすべての情報を指定することによって、keytool を実行できます。

ここでの手順では次のように指定します。

* `[appserver root]` は、AEM formsを実行するアプリケーションサーバーのホームディレクトリです。
* `[type]` は、実行したインストールの種類に応じて異なるフォルダー名です。

## SSL 秘密鍵証明書の作成 {#create-an-ssl-credential}

1. In a command prompt, navigate to *[JAVA HOME]*/bin and type the following command to create the credential and keystore:

   `keytool -genkey -dname "CN=`*Host NameGroupGroup *`, OU=`*会社* 名 `, O=`*NameNameNameNameNameNameNameNameStateStateCountryCode City_key *`,L=`**`, S=`**`, C=``-alias "AEMForms Cert"``-keyalg RSA -keypass`**`-keystore`*_passwordkeystorename *`.keystore`

   >[!NOTE]
   >
   >Replace `[JAVA_HOME]` with the directory where the JDK is installed, and replace the text in italic with values that correspond with your environment. 「Host Name」は、アプリケーションサーバーの完全修飾ドメイン名です。

1. Enter the `keystore_password` when prompted for a password. キーストアおよびキーのパスワードは、同じである必要があります。

   >[!NOTE]
   >
   >The `keystore_password` *ntered at this step may be the same password (key_password) that you entered in step 1, or it may be different.*

1. Copy the *keystorename*.keystore to the `[appserver root]/server/[type]/conf` directory by typing one of the following commands:

   * (Windows Single Server) `copy` `keystorename.keystore[appserver root]\standalone\configuration`
   * (Windows Server Cluster)コピー `keystorename.keystore[appserver root]\domain\configuration`
   * （Linuxシングルサーバ） `cp keystorename.keystore [appserver root]/standalone/configuration`
   * (Linux Server Cluster) `cp <em>keystorename</em>.keystore<em>[appserver root]</em>/domain/configuration`


1. 次のコマンドを入力して、証明書ファイルを書き出します。

   * （シングルサーバ） `keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer -keystore [appserver root]/standalone/configuration/keystorename.keystore`
   * （サーバークラスター） `keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer -keystore [appserver root]/domain/configuration/keystorename.keystore`

1. パスワードの入力を求められたら、*keystore_password*&#x200B;を入力します。
1. Copy the AEMForms_cert.cer file to the *[appserver root]\conf *directory by typing the following command:

   * (Windows Single Server) `copy AEMForms_cert.cer [appserver root]\standalone\configuration`
   * （Windows Serverクラスタ） `copy AEMForms_cert.cer [appserver root]\domain\configuration`
   * （Linuxシングルサーバ） `cp AEMForms _cert.cer [appserver root]\standalone\configuration`
   * (Linux Server Cluster) `cp AEMForms _cert.cer [appserver root]\domain\configuration`

1. 次のコマンドを入力して、証明書の内容を表示します。

   * `keytool -printcert -v -file [appserver root]\standalone\configuration\AEMForms_cert.cer`
   * `keytool -printcert -v -file [appserver root]\domain\configuration\AEMForms_cert.cer`

1. To provide write access to the cacerts file in `[JAVA_HOME]\jre\lib\security`, if required, perform the following task:

   * （Windows）cacerts ファイルを右クリックして「プロパティ」を選択し、「読み取り専用」属性の選択を解除します。
   * (Linux)タイプ `chmod 777 cacerts`

1. 次のコマンドを入力して、証明書ファイルを読み込みます。

   `keytool -import -alias “AEMForms Cert” -file`*AEMForms_cert *`.cer -keystore`*JAVA_HOME* `\jre\lib\security\cacerts`

1. Type `changeit` as the password. Java インストールではこれがデフォルトのパスワードですが、システム管理者によって変更されている場合があります。
1. プロンプトに対して `Trust this certificate? [no]`次のように入力し `yes`ます。 「Certificate was added to keystore」という確認メッセージが表示されます。
1. Workbench から SSL 経由で接続している場合は、Workbench コンピューターに証明書をインストールします。
1. テキストエディターで、編集用に次のファイルを開きます。

   * Single Server - `[appserver root]`/standalone/configuration/lc_&lt;dbname/turnkey>.xml

   * Server Cluster - `[appserver root]`/domain/configuration/host.xml

   * Server Cluster - `[appserver root]`/domain/configuration/domain_&lt;dbname>.xml

1. 
   * **シングルサーバーの場合、** lc_&lt;dbaname/tunkey>.xml ファイルの &lt;security-realms> セクションに次のテキストを追加します。

   ```as3
   <security-realm name="SSLRealm">
   <server-identities>
   <ssl>
   <keystore path="C:/Adobe/Adobe_Experience_Manager_Forms/jboss/standalone/configuration/aemformses.keystore" keystore-password="changeit" alias="AEMformsCert" key-password="changeit"/>
   </ssl>
   </server-identities>
   </security-realm>
   ```

   Locate the `<server>` section present after the following code:

   `<http-listener name="default" socket-binding="http" redirect-socket="https" max-post-size="104857600"/>`

   上記のコードの後の &lt;server> セクションに次のテキストを追加します。

   ```
   <https-listener name="default-secure" socket-binding="https" security-realm="SSLRealm"/>
   ```

   * **サーバークラスターの場合** 、すべてのノードの [appserver root]\domain\configuration\host.xmlディレクトリに、&lt;security-realms>セクションの後に次の内容を追加します。

   ```as3
   <security-realm name="SSLRealm">
   <server-identities>
   <ssl>
   <keystore path="C:/Adobe/Adobe_Experience_Manager_Forms/jboss/standalone/configuration/aemformses.keystore" keystore-password="changeit" alias="AEMForms Cert" key-password="changeit"/>
   </ssl>
   </server-identities>
   </security-realm>
   ```

   On the primary node of the Server Cluster, in the [appserver root]\domain\configuration\domain_&lt;dbname>.xml, locate the &lt;server> section present after the following code:

   `<http-listener name="default" socket-binding="http" redirect-socket="https" max-post-size="104857600"/>`

   上記のコードの後の &lt;server> セクションに次のテキストを追加します。

   ```
   <https-listener name="default-secure" socket-binding="https" security-realm="SSLRealm"/>
   ```

1. `keystoreFile` 属性および `keystorePass` 属性の値を、キーストアの作成時に指定したキーストアパスワードに変更します。
1. アプリケーションサーバーを再起動します。

   * 自動インストールの場合：

      * Windows のコントロールパネルで、「管理ツール」をクリックして「サービス」をクリックします。
      * JBoss for Adobe Experience Manager forms を選択します。
      * 操作／停止を選択します。
      * サービスのステータスが停止になるまで待機します。
      * 操作／開始を選択します。
   * Adobe により事前設定された、または手動で設定した JBoss インストールの場合：

      * From a command prompt, navigate to *`[appserver root]`*/bin.
      * 次のコマンドを入力して、サーバーを停止します。

         * (Windows) `shutdown.bat -S`
         * (Linux) `./shutdown.sh -S`
      * JBoss プロセスが完全にシャットダウンする（JBoss プロセスが、起動された端末にコントロールを返す）まで待機します。
      * 次のコマンドを入力して、サーバーを起動します。

         * (Windows) `run.bat -c <profile>`
         * (Linux) `./run.sh -c <profile>`



1. To access administration console using SSL, type `https://[host name]:'port'/adminui` in a web browser:

   JBoss のデフォルト SSL ポートは 8443 です。以降 AEM Forms にアクセスするときはこのポートを指定します。

## CA からの秘密鍵証明書の要求 {#request-a-credential-from-a-ca}

1. In a command prompt, navigate to *[JAVA HOME]*/bin and type the following command to create the keystore and the key:

   `keytool -genkey -dname "CN=`*Host NameGroup *`, OU=`*会社* 名 `, O=`**`, L=`**`, S=`**`, C=`**`-alias "AEMForms Cert"``-keyalg RSA -keypass`**`-keystore`*名City NameCityNameCityNameStateCountryCountryCodeKeyKeyPasswordNameKeyGroupNameGroupNameGroupNameNameGroupNameNameGroupNameGroupNameNameGroupName *`.keystore`

   >[!NOTE]
   >
   >Replace *`[JAVA_HOME]`* with the directory where the JDK is installed, and replace the text in italic with values that correspond with your environment.

1. 次のコマンドを入力して証明書要求を生成し、認証局に送信します

   `keytool -certreq -alias` &quot;AEMForms Cert&quot; `-keystore`*keystorename *`.keystore -file`*AEMFormscertRequest.csr*

1. 証明書ファイルの要求が完了したら、次の手順を実行します。

## CA から取得した秘密鍵証明書の SSL を有効にするための使用 {#use-a-credential-obtained-from-a-ca-to-enable-ssl}

1. In a command prompt, navigate to *`[JAVA HOME]`*/bin and type the following command to import the root certificate of the CA with which the CSR has been signed:

   `keytool -import -trustcacerts -file` rootcert.pem -keystore` keystorename.keystore -alias root`

   ルート証明書がブラウザーにない場合は、ブラウザーにも読み込みます。

   >[!NOTE]
   >
   >Replace *`[JAVA_HOME]`with the directory where the JDK is installed, and replace the text in italic with values that correspond with your environment.*

1. In a command prompt, navigate to *`[JAVA HOME]`*/bin and type the following command to import the credential into the keystore:

   `keytool -import -trustcacerts -file`*CACertificateName *`.crt -keystore`*keystorename* `.keystore`

   >[!NOTE]
   >
   >* Replace `[JAVA_HOME]` with the directory where the JDK is installed, and replace the text in italic with values that correspond with your environment.
   >* 自己署名の公開証明書が存在する場合は、読み込んだ CA 署名付き証明書に置き換えられます。


1. SSL 秘密鍵証明書の作成の手順 13～18 を実行します。
