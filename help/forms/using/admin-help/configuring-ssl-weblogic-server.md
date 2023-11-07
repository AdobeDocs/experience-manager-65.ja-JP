---
title: WebLogic Server 用の SSL の設定
seo-title: Configuring SSL for WebLogic Server
description: WebLogic Server で使用する SSL 秘密鍵証明書を作成する方法と、WebLogic Server 用の SSL を設定する方法について説明します。
seo-description: Learn how to create an SSL credential for use on WebLogic server and how to configure SSL for WebLogic Server.
uuid: 8ee979fd-2615-451b-a607-4f73ecfed4f9
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 968c2574-ec9a-45ca-9c64-66f4caeec285
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1047'
ht-degree: 33%

---


# WebLogic Server 用の SSL の設定 {#configuring-ssl-for-weblogic-server}

WebLogic Server で SSL を設定するには、認証用の SSL 秘密鍵証明書が必要です。 Java keytool を使用して、次のタスクを実行し、秘密鍵証明書を作成できます。

* 公開鍵と秘密鍵のペアを作成し、単一要素の証明書チェーンとして保存されている X.509 v1 自己署名証明書で公開鍵を囲み、証明書チェーンと秘密鍵を新しいキーストアに保存します。 このキーストアは、アプリケーションサーバーのカスタム ID キーストアです。
* 証明書を抽出し、新しいキーストアに挿入します。 このキーストアは、アプリケーションサーバーのカスタム信頼キーストアです。

次に、作成したカスタム ID キーストアとカスタム信頼キーストアを使用するように WebLogic を設定します。 また、キーストアファイルの作成に使用する識別名に WebLogic をホストするコンピューターの名前が含まれていなかったので、WebLogic のホスト名の検証機能を無効にします。

## WebLogic Server で使用する SSL 秘密鍵証明書の作成 {#creating-an-ssl-credential-for-use-on-weblogic-server}

keytool コマンドは通常、Java jre/bin ディレクトリにあり、次の表に示すオプションとオプションの値を含める必要があります。

<table>
 <thead>
  <tr>
   <th><p>Keytool オプション</p></th>
   <th><p>説明</p></th>
   <th><p>オプションの値</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>-alias</p></td>
   <td><p>キーストアのエイリアス。</p></td>
   <td>
    <ul>
     <li><p>カスタム ID キーストア： <code>ads-credentials</code></p></li>
     <li><p>カスタム Trust キーストア： <code>bedrock</code></p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-keyalg</p></td>
   <td><p>キーペアの生成に使用するアルゴリズム。</p></td>
   <td><p>RSA</p><p>会社のポリシーに応じて、異なるアルゴリズムを使用できます。</p></td>
  </tr>
  <tr>
   <td><p>-keystore</p></td>
   <td><p>キーストアファイルの場所と名前。</p><p>場所には、ファイルの絶対パスを含めることができます。 または、keytool コマンドを入力したコマンドプロンプトの現在のディレクトリを基準にした相対パスを指定できます。</p></td>
   <td>
    <ul>
     <li><p>カスタム ID キーストア：<code>[</code><i>appserverdomain<code>]</code></i><code>/adobe/</code><i>[サーバー名]</i><code>/ads-ssl.jks</code></p></li>
     <li><p>カスタム Trust キーストア：<code>[</code><i>appserverdomain<code>]</code></i><code>/adobe/</code><i>[サーバー名]</i><code>/ads-ca.jks</code></p></li>
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
   <td><p>3650</p><p>会社のポリシーに応じて、異なる値を使用できます。</p></td>
  </tr>
  <tr>
   <td><p>-storepass</p></td>
   <td><p>キーストアの内容を保護するパスワード。 </p></td>
   <td>
    <ul>
     <li><p>カスタム ID キーストア：キーストアのパスワードは、管理コンソールの Trust Store コンポーネントに指定された SSL 秘密鍵証明書のパスワードと一致している必要があります。</p></li>
     <li><p>カスタム信頼キーストア：カスタム ID キーストアに使用したのと同じパスワードを使用します。</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-keypass</p></td>
   <td><p>キーペアの秘密鍵を保護するパスワード。</p></td>
   <td><p><code>-storepass</code> オプションと同じパスワードを使用します。キーのパスワードは 6 文字以上にする必要があります。</p></td>
  </tr>
  <tr>
   <td><p>-dname</p></td>
   <td><p>キーストアを所有する人を識別する識別名。</p></td>
   <td><p><code>"CN=</code><code>[User name]</code><code>,OU=</code><code>[Group Name]</code><code>, O=</code><code>[Company Name]</code><code>, L=</code><code>[City Name]</code><code>, S=</code><code>[State or province]</code><code>, C=</code><code>[Country Code]</code><code>"</code></p>
    <ul>
     <li><p><code><i>[User name]</i></code> はキーストアを所有しているユーザーの識別名です。</p></li>
     <li><p><code><i>[Group Name]</i></code> はキーストアの所有者が所属している会社グループの識別名です。</p></li>
     <li><p><code><i>[Company Name]</i></code> は所属する組織の名前です。</p></li>
     <li><p><code><i>[City Name]</i></code> は組織の所在地の市区町村です。</p></li>
     <li><p><code><i>[State or province]</i></code> は組織の所在地の都道府県です。</p></li>
     <li><p><code><i>[Country Code]</i></code> は組織の所在国を示す 2 文字のコードです。</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

keytool コマンドの使用方法の詳細については、JDK のマニュアルに含まれている keytool.html ファイルを参照してください。

## カスタム ID および信頼キーストアの作成 {#create-the-custom-identity-and-trust-keystores}

1. コマンドプロンプトで、*[appserverdomain]*/adobe/*[server name]* に移動します。
1. 以下のコマンドを入力します。

   `[JAVA_HOME]/bin/keytool -genkey -v -alias ads-credentials -keyalg RSA -keystore "ads-credentials.jks" -validity 3650 -storepass store_password -keypass key_password -dname "CN=Hostname, OU=Group Name, O=Company Name, L=City Name, S=State,C=Country Code`

   >[!NOTE]
   >
   >`[JAVA_HOME]`*は JDK がインストールされているディレクトリに、イタリックのテキストは自分の環境に対応する値に置き換えます。*

   次に例を示します。

   ```java
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -genkey -v -alias ads-credentials -keyalg RSA -keystore "ads-credentials.jks" -validity 3650 -storepass P@ssw0rd -keypass P@ssw0rd -dname "CN=wasnode01, OU=LC, O=Adobe, L=Noida, S=UP,C=91
   ```

   「ads-credentials.jks」という名前のカスタム ID キーストアファイルが [appserverdomain]/adobe/[server name] ディレクトリに作成されます。

1. 次のコマンドを入力して、ads-credentials キーストアから証明書を抽出します。

   [JAVA_HOME]`/bin/keytool -export -v -alias ads-credentials`

   `-file "ads-ca.cer" -keystore "ads-credentials.jks"`

   `-storepass` `*store*`*_**パスワード**

   >[!NOTE]
   >
   >`[JAVA_HOME]` は、JDK がインストールされているディレクトリに、`store`*_* `password`* は、カスタム ID キーストアのパスワードに置き換えます*。

   次に例を示します。

   ```java
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -export -v -alias ads-credentials -file "ads-ca.cer" -keystore "ads-credentials.jks" -storepass P@ssw0rd
   ```

   「ads-ca.cer」という名前の証明書ファイルが、[appserverdomain]/adobe/[*server name*] ディレクトリに作成されます。

1. ads-ca.cer ファイルを、アプリケーションサーバーとの安全な通信を必要とするすべてのホストコンピューターにコピーします。
1. 次のコマンドを入力して、証明書を新しいキーストアファイル（カスタム信頼キーストア）に挿入します。

   [JAVA_HOME] `/bin/keytool -import -v -noprompt -alias bedrock -file "ads-ca.cer" -keystore "ads-ca.jks" -storepass store_password -keypass key_password`

   >[!NOTE]
   >
   >`[JAVA_HOME]` は JDK がインストールされているディレクトリに、 `store`*_* `password` と `key`*_* `password` *は使用しているパスワードに置き換えます。*

   次に例を示します。

   ```java
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -import -v -noprompt -alias bedrock -file "ads-ca.cer" -keystore "ads-ca.jks" -storepass Password1 -keypass Password1
   ```

「‘ads-ca.jks」という名前のカスタム Trust キーストアファイルが、[appserverdomain]/adobe/&#39;server&#39; ディレクトリに作成されます。

作成したカスタム ID キーストアとカスタム信頼キーストアを使用するように WebLogic を設定します。 また、キーストアファイルの作成に使用する識別名に WebLogic Server をホストするコンピューターの名前が含まれていないので、WebLogic のホスト名の検証機能を無効にします。

## SSL を使用する WebLogic の設定 {#configure-weblogic-to-use-ssl}

1. Web ブラウザーの URL 行に`https://`*[ホスト名&#x200B;]*`:7001/console` を入力して、WebLogic サーバー管理コンソールを起動します。
1. 「Environment」下の「Domain Configurations」で **Servers／&#39;server&#39;／Configuration／General** を選択します。
1. 「一般」の「設定」で、次の点を確認します。 **リスンポート有効** および **SSL リッスンポートが有効になっています** が選択されている。 有効になっていない場合は、次の操作を行います。

   1. 「Change Center」で、「**Lock &amp; Edit**」をクリックし、選択内容と値を変更します。
   1. 次を確認します。 **リスンポート有効** および **SSL リッスンポートが有効になっています** チェックボックス。

1. このサーバーが管理対象サーバーの場合は、Listen Port を未使用のポート値（8001 など）に変更し、SSL Listen Port を未使用のポート値（8002 など）に変更します。 スタンドアロンサーバーでは、デフォルトの SSL ポートは 7002 です。
1. クリック **リリース設定**.
1. 「Environment」下の「Domain Configurations」で **Servers／[*Managed Server*]／Configuration／General** をクリックします。
1. 「General」の「Configuration」で「**Keystores**」を選択します。
1. 「Change Center」で、「**Lock &amp; Edit**」をクリックし、選択内容と値を変更します。
1. クリック **変更** キーストアリストをドロップダウンリストとして取得し、「 」を選択します。 **カスタム Id とカスタム信頼**.
1. 「ID」で、次の値を指定します。

   **Custom Identity Keystore**：*[appserverdomain]*/adobe/*[server name]*/ads-credentials.jks。ここで、*[appserverdomain]* は実際のパス、*[server name]* はアプリケーションサーバーの名前です。

   **カスタム ID キーストアタイプ**: JKS

   **カスタム ID キーストアのパスフレーズ**: *mypassword* （カスタム ID キーストアのパスワード）

1. 「信頼」で、次の値を指定します。

   **Custom Trust Keystore ファイル名**：`*[appserverdomain]*/adobe/*'server'*/ads-ca.jks` ここで、`*[appserverdomain]*` は実際のパスです。

   **カスタム信頼キーストアの種類**: JKS

   **カスタム信頼キーストアのパスフレーズ**: *mypassword* （カスタム信頼キーのパスワード）

1. 「一般」の「設定」で、「 **SSL**.
1. デフォルトでは、ID と信頼の場所にキーストアが選択されています。そうでない場合は、キーストアに変更します。
1. 「ID」で、次の値を指定します。

   **秘密鍵のエイリアス**: ads-credentials

   **パスフレーズ**: *mypassword*

1. クリック **リリース設定**.

## ホスト名の検証機能を無効にします。 {#disable-the-hostname-verification-feature}

1. 「設定」タブで、「SSL」をクリックします。
1. 「詳細」で、「ホスト名の検証」リストから「なし」を選択します。

   ホスト名の検証が無効になっていない場合、共通名 (CN) にサーバのホスト名が含まれている必要があります。

1. [Change Center] で、[Lock &amp; Edit] をクリックして、選択内容と値を変更します。
1. アプリケーションサーバーを再起動します。

