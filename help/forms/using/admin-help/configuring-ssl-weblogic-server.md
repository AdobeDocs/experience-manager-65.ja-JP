---
title: WebLogic Server に対する SSL の設定
seo-title: WebLogic Server に対する SSL の設定
description: WebLogic Server で使用する SSL 秘密鍵証明書を作成する方法と、WebLogic Server 用の SSL を設定する方法について説明します。
seo-description: WebLogic Server で使用する SSL 秘密鍵証明書を作成する方法と、WebLogic Server 用の SSL を設定する方法について説明します。
uuid: 8ee979fd-2615-451b-a607-4f73ecfed4f9
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 968c2574-ec9a-45ca-9c64-66f4caeec285
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# WebLogic Server に対する SSL の設定 {#configuring-ssl-for-weblogic-server}

WebLogic Server に SSL を設定するには、認証用の SSL 秘密鍵証明書が必要です。Java keytool を使用し、次のタスクを実行して秘密鍵証明書を作成できます。

* 公開鍵と秘密鍵のキーペアを作成し、単一要素の証明書チェーンとして保存されている X.509 v1 自己署名証明書の公開鍵をラップして、証明書チェーンと秘密鍵を新しいキーストアに保存します。このキーストアがアプリケーションサーバーのカスタム ID キーストアになります。
* 秘密鍵証明書を抽出し、新しいキーストアに挿入します。このキーストアがアプリケーションサーバーのカスタム信頼キーストアになります。

その後、作成したカスタム ID キーストアとカスタム信頼キーストアを使用するように、WebLogic を設定します。また、キーストアファイルの作成に使用する識別名には、WebLogic をホストするコンピューターの名前が含まれていないので、WebLogic のホスト名の検証機能を無効にします。

## WebLogic Server で使用する SSL 秘密鍵証明書の作成 {#creating-an-ssl-credential-for-use-on-weblogic-server}

keytool コマンドは通常 Java の jre/bin ディレクトリにあります。このコマンドでは、次の表に示す複数のオプションとオプション値を指定する必要があります。

<table>
 <thead>
  <tr>
   <th><p>Keytool オプション</p></th>
   <th><p>説明</p></th>
   <th><p>オプション値</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>-alias</p></td>
   <td><p>キーストアのエイリアス。</p></td>
   <td>
    <ul>
     <li><p>カスタムIDキーストア： <code>ads-credentials</code></p></li>
     <li><p>カスタム信頼キーストア： <code>bedrock</code></p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-keyalg</p></td>
   <td><p>キーペアの生成に使用するアルゴリズム。</p></td>
   <td><p>RSA</p><p>会社の方針に合わせて別のアルゴリズムを使用することもできます。</p></td>
  </tr>
  <tr>
   <td><p>-keystore</p></td>
   <td><p>キーストアファイルの場所と名前。</p><p>場所は、ファイルの絶対パスとして指定します。または、keytool コマンドを入力したコマンドプロンプトの現在のディレクトリを基準とした相対ディレクトリとして指定します。</p></td>
   <td>
    <ul>
     <li><p>Custom Identity keystore: <code>[</code><i>appserverdomain]</i><code>/adobe/</code><i>[server name]</i><code>/ads-ssl.jks</code></p></li>
     <li><p>Custom Trust keystore: <code>[</code><i>appserverdomain]</i><code>/adobe/</code><i>[server name]</i><code>/ads-ca.jks</code></p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-file</p></td>
   <td><p>証明書ファイルの場所と名前。</p></td>
   <td><code> ads-ca.cer</code></td>
  </tr>
  <tr>
   <td><p>-validity</p></td>
   <td><p>証明書が有効と見なされる日数。</p></td>
   <td><p>3650</p><p>会社の方針に合わせて別の値を使用することもできます。</p></td>
  </tr>
  <tr>
   <td><p>-storepass</p></td>
   <td><p>キーストアの内容を保護するためのパスワード。 </p></td>
   <td>
    <ul>
     <li><p>カスタム ID キーストア：キーストアパスワードは、管理コンソールの Trust Store コンポーネント用に指定した SSL 秘密鍵証明書パスワードと一致させる必要があります。</p></li>
     <li><p>カスタム信頼キーストア：カスタム ID キーストアに使用したものと同じパスワードを使用します。</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-keypass</p></td>
   <td><p>キーペアの秘密鍵を保護するためのパスワード。</p></td>
   <td><p>Use the same password that you used for the <code>-storepass</code> option. キーパスワードは 6 文字以上で指定する必要があります。</p></td>
  </tr>
  <tr>
   <td><p>-dname</p></td>
   <td><p>キーストアを所有している人物を特定する識別名。</p></td>
   <td><p><code>"CN=</code><code>[User name]</code><code>,OU=</code><code>[Group Name]</code><code>, O=</code><code>[Company Name]</code><code>, L=</code><code>[City Name]</code><code>, S=</code><code>[State or province]</code><code>, C=</code><code>[Country Code]</code><code>"</code></p>
    <ul>
     <li><p><code><i>[User name]</i></code> は、キーストアを所有するユーザーのIDです。</p></li>
     <li><p><code><i>[Group Name]</i></code> は、キーストアの所有者が属する企業グループのIDです。</p></li>
     <li><p><code><i>[Company Name]</i></code> は組織の名前です。</p></li>
     <li><p><code><i>[City Name]</i></code> は、組織の所在地の市区町村です。</p></li>
     <li><p><code><i>[State or province]</i></code> は、組織の所在地の都道府県です。</p></li>
     <li><p><code><i>[Country Code]</i></code> は、組織の所在国を示す2文字のコードです。</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

keytool コマンドの使用方法について詳しくは、JDK マニュアルに含まれている keytool.html ファイルを参照してください。

## カスタム ID および信頼キーストアの作成 {#create-the-custom-identity-and-trust-keystores}

1. From a command prompt, navigate to *[appserverdomain]*/adobe/*[server name]*.
1. 以下のコマンドを入力します。

   `[JAVA_HOME]/bin/keytool -genkey -v -alias ads-credentials -keyalg RSA -keystore "ads-credentials.jks" -validity 3650 -storepass store_password -keypass key_password -dname "CN=Hostname, OU=Group Name, O=Company Name, L=City Name, S=State,C=Country Code`

   >[!NOTE]
   >
   >Replace `[JAVA_HOME]`*with the directory where the JDK is installed, and replace the text in italic with values that correspond with your environment.*

   次に例を示します。

   ```as3
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -genkey -v -alias ads-credentials -keyalg RSA -keystore "ads-credentials.jks" -validity 3650 -storepass P@ssw0rd -keypass P@ssw0rd -dname "CN=wasnode01, OU=LC, O=Adobe, L=Noida, S=UP,C=91
   ```

   The Custom Identity keystore file named ‘‘ads-credentials.jks” is created in the [appserverdomain]/adobe/[server name] directory.

1. 次のコマンドを入力して、ads-credentials キーストアから証明書を抽出します。

   [JAVA_HOME]`/bin/keytool -export -v -alias ads-credentials`

   `-file "ads-ca.cer" -keystore "ads-credentials.jks"`

   `-storepass` `*store*`*_**password**

   >[!NOTE]
   >
   >Replace `[JAVA_HOME]` with the directory where the JDK is installed, and replace `store`*_*`password`* with the password for the Custom Identity keystore.*

   次に例を示します。

   ```as3
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -export -v -alias ads-credentials -file "ads-ca.cer" -keystore "ads-credentials.jks" -storepass P@ssw0rd
   ```

   The certificate file named “ads-ca.cer” is created in the [appserverdomain]/adobe/[*server name*] directory.

1. ads-ca.cer ファイルを、アプリケーションサーバーとのセキュリティで保護された通信を必要とする任意のホストコンピューターにコピーします。
1. 次のコマンドを入力して、証明書を新しいキーストアファイル（カスタム信頼キーストア）に挿入します。

   [JAVA_HOME] `/bin/keytool -import -v -noprompt -alias bedrock -file "ads-ca.cer" -keystore "ads-ca.jks" -storepass store_password -keypass key_password`

   >[!NOTE]
   >
   >Replace `[JAVA_HOME]` with the directory where the JDK is installed, and replace `store`*_*`password`and`key`*_* `password` *with your own passwords.*

   次に例を示します。

   ```as3
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -import -v -noprompt -alias bedrock -file "ads-ca.cer" -keystore "ads-ca.jks" -storepass Password1 -keypass Password1
   ```

The Custom Trust keystore file named ‘‘ads-ca.jks’’ is created in the [appserverdomain]/adobe/&#39;server&#39; directory.

作成したカスタム ID キーストアとカスタム信頼キーストアを使用するように、WebLogic を設定します。また、キーストアファイルの作成に使用する識別名には、WebLogic Server をホストするコンピューターの名前が含まれていないので、WebLogic のホスト名の検証機能を無効にします。

## SSL を使用する WebLogic の設定 {#configure-weblogic-to-use-ssl}

1. Start the WebLogic Server administration console by typing `https://`*[host name ]*`:7001/console`in the URL line of a web browser.
1. Under Environment, in Domain Configurations, select **Servers > &#39;server&#39; > Configuration > General**.
1. 「General」の「Configuration」で、「**Listen Port Enabled**」と「**SSL Listen Port Enabled**」が選択されていることを確認します。有効でない場合は、次の手順を実行します。

   1. 「Change Center」で、「**Lock &amp; Edit**」をクリックし、選択内容と値を変更します。
   1. 「**Listen Port Enabled**」と「**SSL Listen Port Enabled**」チェックボックスを確認します。

1. このサーバーが管理対象サーバーである場合は、リスンポートを未使用のポート番号（8001 など）に、SSL リスンポートを未使用のポート番号（8002 など）に変更します。スタンドアロンサーバーの場合、デフォルトの SSL ポートは 7002 です。
1. 「**Release Configuration**」をクリックします。
1. Under Environment, in Domain Configurations, click **Servers >[*Managed Server*]> Configuration > General**.
1. 「General」の「Configuration」で「**Keystores**」を選択します。
1. 「Change Center」で、「**Lock &amp; Edit**」をクリックし、選択内容と値を変更します。
1. 「**Change**」をクリックしてキーストアリストをドロップダウンリストとして取得し、「**Custom Identity And Custom Trust**」を選択します。
1. 「ID」で、次の値を指定します。

   **Custom Identity Keystore**: *[appserverdomain]*/adobe/*[server name]*/ads-credentials.jks。ここで、*[appserverdomain] *は実際のサーバー名、 *[]* サーバー名はアプリケーションサーバーの名前です。

   **Custom Identity Keystore Type**：JKS

   **Custom Identity Keystore Passphrase**：*mypassword* カスタム ID キーストアパスワード)

1. 「Trust」で、次の値を指定します。

   **Custom Trust Keystore File Name**: `*[appserverdomain]*/adobe/*'server'*/ads-ca.jks`は、 `*[appserverdomain]*` 実際のパス

   **Custom Trust Keystore Type**：JKS

   **Custom Trust Keystore Pass Phrase**：*mypassword* （カスタム信頼キーパスワード）

1. 「General」の「Configuration」で「**SSL**」を選択します。
1. デフォルトでは、ID と信頼の場所にキーストアが選択されています。 選択されていない場合、キーストアに変更します。
1. 「ID」で、次の値を指定します。

   **Private Key Alias**：ads-credentials

   **Passphrase**：*mypassword*

1. 「**Release Configuration**」をクリックします。

## ホスト名の検証機能の無効化 {#disable-the-hostname-verification-feature}

1. 「Configuration」タブで、「SSL」をクリックします。
1. 「Advanced」の「Hostname Verification」リストで、「None」を選択します。

   ホスト名の検証が無効になっていない場合は、共通名（CN）にサーバーホスト名が含まれている必要があります。

1. 「Change Center」で、「Lock &amp; Edit」をクリックし、選択内容と値を変更します。
1. アプリケーションサーバーを再起動します。

