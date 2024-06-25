---
title: JBoss Application Server に対する SSL の設定
description: JBoss Application Server での SSL の設定方法について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 8eb4f691-a66b-498e-8114-307221f63718
solution: Experience Manager, Experience Manager Forms
feature: Document Security
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: ht
source-wordcount: '904'
ht-degree: 100%

---

# JBoss Application Server に対する SSL の設定 {#configuring-ssl-for-jboss-application-server}

JBoss Application Server で SSL を設定するには、認証用の SSL 秘密鍵証明書が必要です。資格情報は、Java keytool を使用して作成するか、認証局（CA）からリクエストして読み込むことができます。その後、JBoss で SSL を有効にする必要があります。

keytool を使用すると、キーストアの作成に必要なすべての情報を 1 つのコマンドで指定できます。

この手順では次のように指定します。

* `[appserver root]` は、AEM Forms を実行するアプリケーションサーバーのホームディレクトリです。
* `[type]` は、実行したインストールの種類に応じて異なる、フォルダー名です。

## SSL 資格情報の作成 {#create-an-ssl-credential}

1. コマンドプロンプトで、*[JAVA HOME]*／bin に移動し、次のコマンドを入力して資格情報とキーストアを作成してください。

   `keytool -genkey -dname "CN=`*ホスト名* `, OU=`*グループ名* `, O=`*会社名* `,L=`*市区町村名* `, S=`*都道府県* `, C=`国コード&quot;`-alias "AEMForms Cert"` `-keyalg RSA -keypass`*key_password* `-keystore`*keystorename* `.keystore`

   >[!NOTE]
   >
   >`[JAVA_HOME]` は JDK がインストールされているディレクトリに置き換え、斜体のテキストは自分の環境に対応する値に置き換えます。「Host Name」は、アプリケーションサーバーの完全修飾ドメイン名です。

1. パスワードの入力を求められたら、`keystore_password` を入力します。キーストアおよびキーのパスワードは、同じである必要があります。

   >[!NOTE]
   >
   >この手順で入力された `keystore_password` *は、手順 1 で入力したパスワード（key_password）と同じである場合も、異なる場合もあります。*

1. 次のいずれかのコマンドを入力して、*keystorename*.keystore を `[appserver root]/server/[type]/conf` ディレクトリにコピーします。

   * （Windows シングルサーバー）`copy` `keystorename.keystore[appserver root]\standalone\configuration`
   * （Windows サーバークラスター）`keystorename.keystore[appserver root]\domain\configuration` をコピー
   * （Linux シングルサーバー）`cp keystorename.keystore [appserver root]/standalone/configuration`
   * （Linux サーバークラスター）`cp <em>keystorename</em>.keystore<em>[appserver root]</em>/domain/configuration`


1. 次のコマンドを入力して、証明書ファイルを書き出します。

   * （シングルサーバー）`keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer -keystore [appserver root]/standalone/configuration/keystorename.keystore`
   * （サーバークラスター）`keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer -keystore [appserver root]/domain/configuration/keystorename.keystore`

1. パスワードの入力を求められたら、*keystore_password*&#x200B;を入力します。
1. 次のコマンドを入力して、AEMForms_cert.cer ファイルを *[appserver root]¥conf* ディレクトリにコピーします。

   * （Windows シングルサーバー）`copy AEMForms_cert.cer [appserver root]\standalone\configuration`
   * （Windows サーバークラスター）`copy AEMForms_cert.cer [appserver root]\domain\configuration`
   * （Linux シングルサーバー）`cp AEMForms _cert.cer [appserver root]\standalone\configuration`
   * （Linux サーバークラスター）`cp AEMForms _cert.cer [appserver root]\domain\configuration`

1. 次のコマンドを入力して、証明書の内容を表示します。

   * `keytool -printcert -v -file [appserver root]\standalone\configuration\AEMForms_cert.cer`
   * `keytool -printcert -v -file [appserver root]\domain\configuration\AEMForms_cert.cer`

1. `[JAVA_HOME]\jre\lib\security` の cacerts ファイルへの書き込みアクセス権を付与するには、必要に応じて次のタスクを実行します。

   * （Windows）cacerts ファイルを右クリックして「プロパティ」を選択し、「読み取り専用」属性の選択を解除します。
   * （Linux）タイプ `chmod 777 cacerts`

1. 次のコマンドを入力して、証明書ファイルを読み込みます。

   `keytool -import -alias "AEMForms Cert" -file`*AEMForms_cert* `.cer -keystore`*JAVA_HOME* `\jre\lib\security\cacerts`

1. パスワードとして`changeit`を入力します。Java インストールではこれがデフォルトのパスワードですが、システム管理者によって変更されている場合があります。
1. `Trust this certificate? [no]` の入力を求められた場合、`yes` と入力します。「証明書がキーストアに追加されました」という確認メッセージが表示されます。
1. Workbench から SSL 経由で接続している場合は、Workbench コンピューターに証明書をインストールします。
1. テキストエディターで、次のファイルを開いて編集します。

   * シングルサーバー - `[appserver root]`¥standalone¥configuration¥lc_&lt;dbname/turnkey>.xml

   * サーバークラスター - `[appserver root]`¥domain¥configuration¥host.xml

   * サーバークラスター - `[appserver root]`¥domain¥configuration¥domain_&lt;dbname>.xml

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

   次のコードの後の`<server>`セクションを探します。

   `<http-listener name="default" socket-binding="http" redirect-socket="https" max-post-size="104857600"/>`

   上記のコードの後の &lt;server> セクションに次のテキストを追加します。

   ```xml
   <https-listener name="default-secure" socket-binding="https" security-realm="SSLRealm"/>
   ```

   * **サーバークラスターの場合、**&#x200B;すべてのノード上の [appserver root]domain¥configuration¥host.xml の &lt;security-realms> セクションの後に次のテキストを追加します。

   ```xml
   <security-realm name="SSLRealm">
   <server-identities>
   <ssl>
   <keystore path="C:/Adobe/Adobe_Experience_Manager_Forms/jboss/standalone/configuration/aemformses.keystore" keystore-password="changeit" alias="AEMForms Cert" key-password="changeit"/>
   </ssl>
   </server-identities>
   </security-realm>
   ```

   サーバークラスターのプライマリノード上の [appserver root]¥domain¥configuration¥domain_&lt;dbname>.xml で、次のコードの後に表示される &lt;server> セクションを探してください。

   `<http-listener name="default" socket-binding="http" redirect-socket="https" max-post-size="104857600"/>`

   上記のコードの後の &lt;server> セクションに次のテキストを追加します。

   ```xml
   <https-listener name="default-secure" socket-binding="https" security-realm="SSLRealm"/>
   ```

1. `keystoreFile` 属性および `keystorePass` 属性の値を、キーストアの作成時に指定したキーストアパスワードに変更します。
1. アプリケーションサーバーを再起動します。

   * 自動インストールの場合：

      * Windows のコントロールパネルで、「管理ツール」をクリックして「サービス」をクリックします。
      * JBoss for Adobe Experience Manager Forms を選択します。
      * 操作／停止を選択します。
      * サービスのステータスが停止になるまで待ちます。
      * 操作／開始を選択します。

   * アドビにより事前設定された JBoss または手動で設定した JBoss のインストールの場合：

      * コマンドプロンプトで、*`[appserver root]`*¥bin に移動します。
      * 次のコマンドを入力して、サーバーを停止します。

         * (Windows) `shutdown.bat -S`
         * (Linux) `./shutdown.sh -S`

      * JBoss プロセスが完全にシャットダウンする（JBoss プロセスが起動したターミナルにコントロールを返す）まで待ちます。
      * 次のコマンドを入力して、サーバーを起動します。

         * (Windows) `run.bat -c <profile>`
         * (Linux) `./run.sh -c <profile>`

1. SSL を使用して管理コンソールにアクセスするには、web ブラウザーで `https://[host name]:'port'/adminui` を入力してください。

   JBoss のデフォルト SSL ポートは 8443 です。以降、AEM Forms にアクセスする際はこのポートを指定します。

## CA に証明書をリクエスト {#request-a-credential-from-a-ca}

1. コマンドプロンプトで、*[JAVA HOME]*/bin に移動し、次のコマンドを入力してキーストアとキーを作成してください。

   `keytool -genkey -dname "CN=`*ホスト名* `, OU=`*グループ名* `, O=`*会社名* `, L=`*市区町村名* `, S=`*都道府県* `, C=`*国コード*&quot; `-alias "AEMForms Cert"` `-keyalg RSA -keypass`-*key_password* `-keystore`*keystorename* `.keystore`

   >[!NOTE]
   >
   >*`[JAVA_HOME]`* を JDK がインストールされているディレクトリに置き換え、斜体のテキストは自分の環境に対応する値に置き換えます。

1. 次のコマンドを入力して証明書要求を生成し、認証局に送信します

   `keytool -certreq -alias`「AEMForms Cert」`-keystore`*keystorename* `.keystore -file`*AEMFormscertRequest.csr*

1. 証明書ファイルの要求が完了したら、次の手順を実行します。

## CA から入手した証明書を使用して SSL を有効化 {#use-a-credential-obtained-from-a-ca-to-enable-ssl}

1. コマンドプロンプトで、*`[JAVA HOME]`*¥bin に移動し、次のコマンドを入力して CSR が署名された CA のルート証明書を読み込みます。

   `keytool -import -trustcacerts -file`rootcert.pem -keystore` keystorename.keystore -alias root`

   ルート証明書がブラウザーにない場合は、ブラウザーにも読み込みます。

   >[!NOTE]
   >
   >*`[JAVA_HOME]`を JDK がインストールされているディレクトリに置き換え、斜体のテキストは自分の環境に対応する値に置き換えます。*

1. コマンドプロンプトで、*`[JAVA HOME]`*¥bin に移動し、次のコマンドを入力して資格情報をキーストアに読み込みます。

   `keytool -import -trustcacerts -file`*CACertificateName* `.crt -keystore`*keystorename* `.keystore`

   >[!NOTE]
   >
   >* `[JAVA_HOME]` を JDK がインストールされているディレクトリに置き換え、斜体のテキストは自分の環境に対応する値に置き換えます。
   >* 自己署名の公開証明書が存在する場合は、読み込んだ CA 署名付き証明書に置き換えられます。

1. SSL 証明書の作成の手順 13～18 を実行します。
