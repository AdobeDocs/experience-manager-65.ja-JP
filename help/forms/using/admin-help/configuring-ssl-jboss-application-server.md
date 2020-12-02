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
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
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

1. コマンドプロンプトで、*[JAVA HOME]*/binに移動し、次のコマンドを入力して秘密鍵証明書とキーストアを作成します。

   `keytool -genkey -dname "CN=`*Host* `, OU=`*NameGroup* `, O=`*NameCompany* `,L=`*NameCity NameNameStateCountry Code&quot;* `, S=`** `, C=`key_ `-alias "AEMForms Cert"` `-keyalg RSA -keypass`** `-keystore`*passwordkeystorename* `.keystore`

   >[!NOTE]
   >
   >`[JAVA_HOME]`は、JDKがインストールされているディレクトリに置き換えます。イタリックのテキストは、環境に対応する値に置き換えます。 「Host Name」は、アプリケーションサーバーの完全修飾ドメイン名です。

1. パスワードの入力を求められたら、`keystore_password`を入力します。 キーストアおよびキーのパスワードは、同じである必要があります。

   >[!NOTE]
   >
   >この手順で入力した`keystore_password` *は、手順1で入力したのと同じパスワード(key_password)であるか、異なるパスワードである可能性があります。*

1. 次のいずれかのコマンドを入力して、*keystorename*.keystoreを`[appserver root]/server/[type]/conf`ディレクトリにコピーします。

   * (Windows Single Server) `copy` `keystorename.keystore[appserver root]\standalone\configuration`
   * (Windows Server Cluster)コピー`keystorename.keystore[appserver root]\domain\configuration`
   * （Linuxシングルサーバ） `cp keystorename.keystore [appserver root]/standalone/configuration`
   * （Linuxサーバークラスタ） `cp <em>keystorename</em>.keystore<em>[appserver root]</em>/domain/configuration`


1. 次のコマンドを入力して、証明書ファイルを書き出します。

   * （シングルサーバ） `keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer -keystore [appserver root]/standalone/configuration/keystorename.keystore`
   * （サーバークラスター） `keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer -keystore [appserver root]/domain/configuration/keystorename.keystore`

1. パスワードの入力を求められたら、*keystore_password*&#x200B;を入力します。
1. 次のコマンドを入力して、AEMForms_cert.cerファイルを&#x200B;*[appserver root] \conf*&#x200B;ディレクトリにコピーします。

   * (Windows Single Server) `copy AEMForms_cert.cer [appserver root]\standalone\configuration`
   * （Windows Serverクラスター） `copy AEMForms_cert.cer [appserver root]\domain\configuration`
   * （Linuxシングルサーバ） `cp AEMForms _cert.cer [appserver root]\standalone\configuration`
   * （Linuxサーバークラスタ） `cp AEMForms _cert.cer [appserver root]\domain\configuration`

1. 次のコマンドを入力して、証明書の内容を表示します。

   * `keytool -printcert -v -file [appserver root]\standalone\configuration\AEMForms_cert.cer`
   * `keytool -printcert -v -file [appserver root]\domain\configuration\AEMForms_cert.cer`

1. `[JAVA_HOME]\jre\lib\security`内のcacertsファイルへの書き込みアクセスを提供するには、必要に応じて、次のタスクを実行します。

   * （Windows）cacerts ファイルを右クリックして「プロパティ」を選択し、「読み取り専用」属性の選択を解除します。
   * (Linux)`chmod 777 cacerts`と入力します。

1. 次のコマンドを入力して、証明書ファイルを読み込みます。

   `keytool -import -alias “AEMForms Cert” -file`*AEMForms_* `.cer -keystore`*certJAVA_HOME* `\jre\lib\security\cacerts`

1. パスワードとして`changeit`と入力します。 Java インストールではこれがデフォルトのパスワードですが、システム管理者によって変更されている場合があります。
1. `Trust this certificate? [no]`：を求められたら、`yes`と入力します。 「Certificate was added to keystore」という確認メッセージが表示されます。
1. Workbench から SSL 経由で接続している場合は、Workbench コンピューターに証明書をインストールします。
1. テキストエディターで、編集用に次のファイルを開きます。

   * シングルサーバー — `[appserver root]`/standalone/configuration/lc_&lt;dbname/turnkey>.xml

   * サーバークラスタ — `[appserver root]`/domain/configuration/host.xml

   * サーバークラスタ — `[appserver root]`/domain/configuration/domain_&lt;dbname>.xml

1. 
   * **シングルサーバーの場合、** lc_&lt;dbaname/tunkey>.xml ファイルの &lt;security-realms> セクションに次のテキストを追加します。

   ```xml
   <security-realm name="SSLRealm">
   <server-identities>
   <ssl>
   <keystore path="C:/Adobe/Adobe_Experience_Manager_Forms/jboss/standalone/configuration/aemformses.keystore" keystore-password="changeit" alias="AEMformsCert" key-password="changeit"/>
   </ssl>
   </server-identities>
   </security-realm>
   ```

   次のコードの後にある`<server>`セクションを探します。

   `<http-listener name="default" socket-binding="http" redirect-socket="https" max-post-size="104857600"/>`

   上記のコードの後の &lt;server> セクションに次のテキストを追加します。

   ```xml
   <https-listener name="default-secure" socket-binding="https" security-realm="SSLRealm"/>
   ```

   * **サーバークラスター** の場合、すべてのノードの [appserver root] \domain\configuration\host.xmlディレクトリに、次の内容を &lt;security-realms> 節の後に追加します。

   ```xml
   <security-realm name="SSLRealm">
   <server-identities>
   <ssl>
   <keystore path="C:/Adobe/Adobe_Experience_Manager_Forms/jboss/standalone/configuration/aemformses.keystore" keystore-password="changeit" alias="AEMForms Cert" key-password="changeit"/>
   </ssl>
   </server-identities>
   </security-realm>
   ```

   サーバークラスターのプライマリノードの[appserver root]\domain\configuration\domain_&lt;dbname>.xmlで、次のコードの後にある&lt;server>セクションを探します。

   `<http-listener name="default" socket-binding="http" redirect-socket="https" max-post-size="104857600"/>`

   上記のコードの後の &lt;server> セクションに次のテキストを追加します。

   ```xml
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

      * コマンドプロンプトで&#x200B;*`[appserver root]`*/binに移動します。
      * 次のコマンドを入力して、サーバーを停止します。

         * (Windows) `shutdown.bat -S`
         * (Linux) `./shutdown.sh -S`
      * JBoss プロセスが完全にシャットダウンする（JBoss プロセスが、起動された端末にコントロールを返す）まで待機します。
      * 次のコマンドを入力して、サーバーを起動します。

         * (Windows) `run.bat -c <profile>`
         * (Linux) `./run.sh -c <profile>`



1. SSLを使用して管理コンソールにアクセスするには、Webブラウザーで`https://[host name]:'port'/adminui`と入力します。

   JBoss のデフォルト SSL ポートは 8443 です。以降 AEM Forms にアクセスするときはこのポートを指定します。

## CA からの秘密鍵証明書の要求  {#request-a-credential-from-a-ca}

1. コマンドプロンプトで、*[JAVA HOME]*/binに移動し、次のコマンドを入力してキーストアとキーを作成します。

   `keytool -genkey -dname "CN=`*Host* `, OU=`*NameGroup* `, O=`*NameCompany* `, L=`*NameCity* `, S=`** `, C=`*NameStateCountry Code*&quot;- `-alias "AEMForms Cert"` `-keyalg RSA -keypass`** `-keystore`*key_passwordkeystorename* `.keystore`

   >[!NOTE]
   >
   >*`[JAVA_HOME]`*&#x200B;は、JDKがインストールされているディレクトリに置き換えます。イタリックのテキストは、環境に対応する値に置き換えます。

1. 次のコマンドを入力して証明書要求を生成し、認証局に送信します

   `keytool -certreq -alias` &quot;AEMForms Cert&quot;  `-keystore`** `.keystore -file`*keystorenameAEMFormscertRequest.csr*

1. 証明書ファイルの要求が完了したら、次の手順を実行します。

## CA から取得した秘密鍵証明書の SSL を有効にするための使用  {#use-a-credential-obtained-from-a-ca-to-enable-ssl}

1. コマンドプロンプトで、*`[JAVA HOME]`*/binに移動し、次のコマンドを入力してCSRが署名されているCAのルート証明書を読み込みます。

   `keytool -import -trustcacerts -file` rootcert.pem -keystore` keystorename.keystore -alias root`

   ルート証明書がブラウザーにない場合は、ブラウザーにも読み込みます。

   >[!NOTE]
   >
   >*`[JAVA_HOME]`をJDKがインストールされているディレクトリに置き換え、斜体のテキストを環境に対応する値に置き換えます。*

1. コマンドプロンプトで、*`[JAVA HOME]`*/binに移動し、次のコマンドを入力して秘密鍵証明書をキーストアに読み込みます。

   `keytool -import -trustcacerts -file`** `.crt -keystore`*CACertificateNamekeystorename* `.keystore`

   >[!NOTE]
   >
   >* `[JAVA_HOME]`は、JDKがインストールされているディレクトリに置き換えます。イタリックのテキストは、環境に対応する値に置き換えます。
   >* 自己署名の公開証明書が存在する場合は、読み込んだ CA 署名付き証明書に置き換えられます。


1. SSL 秘密鍵証明書の作成の手順 13～18 を実行します。
