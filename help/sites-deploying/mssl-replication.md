---
title: 相互 SSL を使用したレプリケーション
seo-title: Replicating Using Mutual SSL
description: オーサーインスタンス上のレプリケーションエージェントが相互 SSL（MSSL）を使用してパブリッシュインスタンスに接続するように AEM を設定する方法について説明します。MSSL を使用して、レプリケーションエージェントとパブリッシュインスタンス上の HTTP サービスは、証明書を使用して互いに認証します。
seo-description: Learn how to configure AEM so that a replication agent on the author instance uses mutual SSL (MSSL) to connect with the publish instance. Using MSSL, the replication agent and the HTTP service on the publish instance use certificates to authenticate each other.
uuid: f4bc5e61-a58c-4fd2-9a24-b31e0c032c15
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 8bc307d9-fa5c-44c0-bff9-2d68d32a253b
feature: Configuring
exl-id: 0a8d7831-d076-45cf-835c-8063ee13d6ba
source-git-commit: b8027a8564f2dce408e7cd5b01f3b86c703c9e3a
workflow-type: ht
source-wordcount: '1392'
ht-degree: 100%

---

# 相互 SSL を使用したレプリケーション{#replicating-using-mutual-ssl}

オーサーインスタンス上のレプリケーションエージェントが相互 SSL（MSSL）を使用してパブリッシュインスタンスに接続するように AEM を設定します。MSSL を使用して、レプリケーションエージェントとパブリッシュインスタンス上の HTTP サービスは、証明書を使用して互いに認証します。

レプリケーション用の MSSL の設定には、次の手順を実行する必要があります。

1. オーサーインスタンスとパブリッシュインスタンスの秘密鍵と証明書を作成または取得します。
1. オーサーインスタンスとパブリッシュインスタンスに鍵と証明書をインストールします。

   * 作成者：作成者の秘密鍵と公開の証明書。
   * 公開：公開の秘密鍵と作成者の証明書。証明書は、レプリケーションエージェントで認証されるユーザーアカウントに関連付けられます。

1. パブリッシュインスタンスで Jetty ベースの HTTP サービスを設定します。
1. レプリケーションエージェントのトランスポートおよび SSL プロパティを設定します。

![chlimage_1-64](assets/chlimage_1-64.png)

レプリケーションを実行するユーザーアカウントを指定する必要があります。パブリッシュインスタンスに信頼済みオーサー証明書をインストールすると、その証明書がこのユーザーアカウントに関連付けられます。

## MSSL の資格情報の取得または作成 {#obtaining-or-creating-credentials-for-mssl}

オーサーインスタンスとパブリッシュインスタンスには、秘密鍵と公開証明書が必要です。

* 秘密鍵は、pkcs#12 形式または JKS 形式で含める必要があります。
* 証明書は、pkcs#12 または JKS 形式で格納されている必要があります。また、「CER」形式の証明書を Granite Truststore に追加することもできます。
* 証明書は、自己署名または認識された CA によって署名される場合があります。

### JKS 形式 {#jks-format}

JKS 形式で秘密鍵と証明書を生成します。秘密鍵は KeyStore ファイルに、証明書は TrustStore ファイルに格納されます。これらを作成するには、[Java `keytool`](https://docs.oracle.com/javase/7/docs/technotes/tools/solaris/keytool.html) を使用します。

Java `keytool` を使用して次の手順を実行し、秘密鍵と資格情報を作成します。

1. キーストアに秘密鍵と公開鍵のペアを生成します。
1. 証明書を作成または取得します。

   * 自己署名：キーストアから証明書をエクスポートします。
   * CA 署名：証明書要求を生成し、CA に送信します。

1. 証明書を TrustStore に読み込みます。

オーサーインスタンスとパブリッシュインスタンスの両方に秘密鍵と自己署名証明書を作成するには、次の手順を実行します。コマンドオプションに適宜、異なる値を使用します。

1. コマンドラインウィンドウまたはターミナルを開きます。秘密鍵と公開鍵のペアを作成するには、以下の表のオプション値を使用し、次のコマンドを入力します。

   ```shell
   keytool -genkeypair -keyalg RSA -validity 3650 -alias alias -keystore keystorename.keystore  -keypass key_password -storepass  store_password -dname "CN=Host Name, OU=Group Name, O=Company Name,L=City Name, S=State, C=Country_ Code"
   ```

   | オプション | 作成者 | 公開 |
   |---|---|---|
   | -alias | 作成者 | publish |
   | -keystore | author.keystore | publish.keystore |

1. 証明書を書き出すには、次のコマンドを入力します。以下の表に示すオプションの値を使用してください。

   ```shell
   keytool -exportcert -alias alias -file cert_file -storetype jks -keystore keystore -storepass store_password
   ```

   | オプション | 作成者 | 公開 |
   |---|---|---|
   | -alias | 作成者 | publish |
   | -file | author.cer | publish.cer |
   | -keystore | author.keystore | publish.keystore |

### pkcs#12 形式 {#pkcs-format}

pkcs#12 形式の秘密鍵と証明書を生成します。そのためには、[openSSL](https://www.openssl.org/) を使用します。次の手順を使用して、秘密鍵と証明書リクエストを生成します。証明書を取得するには、秘密鍵を使用してリクエストに署名するか（自己署名証明書）、CA にリクエストを送信します。次に、秘密鍵と証明書を格納する pkcs#12 アーカイブを生成します。

1. コマンドラインウィンドウまたはターミナルを開きます。秘密鍵を作成するには、次のコマンドを入力します。以下の表に示すオプションの値を使用してください。

   ```shell
   openssl genrsa -out keyname.key 2048
   ```

   | オプション | 作成者 | 公開 |
   |---|---|---|
   | -out | author.key | publish.key |

1. 証明書リクエストを生成するには、次のコマンドを入力します。以下の表に示すオプションの値を使用してください。

   ```shell
   openssl req -new -key keyname.key -out key_request.csr
   ```

   | オプション | 作成者 | 公開 |
   |---|---|---|
   | -key | author.key | publish.key |
   | -out | author_request.csr | publish_request.csr |

   証明書リクエストに署名するか、CA にリクエストを送信します。

1. 証明書リクエストに署名するには、次のコマンドを入力します。以下の表に示すオプションの値を使用してください。

   ```shell
   openssl x509 -req -days 3650 -in key_request.csr -signkey keyname.key -out certificate.cer
   ```

   | オプション | 作成者 | 公開 |
   |---|---|---|
   | -signkey | author.key | publish.key |
   | -in | author_request.csr | publish_request.csr |
   | -out | author.cer | publish.cer |

1. 秘密鍵と署名済みの証明書を pkcs#12 ファイルに追加するには、次のコマンドを入力します。以下の表に示すオプションの値を使用してください。

   ```shell
   openssl pkcs12 -keypbe PBE-SHA1-3DES -certpbe PBE-SHA1-3DES -export -in certificate.cer -inkey keyname.key -out pkcs12_archive.pfx -name "alias"
   ```

   | オプション | 作成者 | 公開 |
   |---|---|---|
   | -inkey | author.key | publish.key |
   | -out | author.pfx | publish.pfx |
   | -in | author.cer | publish.cer |
   | -name | 作成者 | publish |

## オーサーでの秘密鍵と TrustStore のインストール {#install-the-private-key-and-truststore-on-author}

オーサーインスタンスに次の項目をインストールします。

* オーサーインスタンスの秘密鍵。
* パブリッシュインスタンスの証明書。

次の手順を実行するには、オーサーインスタンスの管理者としてログインする必要があります。

### オーサーの秘密鍵のインストール {#install-the-author-private-key}

1. オーサーインスタンスの User Management ページを開きます。（[http://localhost:4502/libs/granite/security/content/useradmin.html](http://localhost:4502/libs/granite/security/content/useradmin.html)）
1. ユーザーアカウントのプロパティを開くには、ユーザー名をクリックまたはタップします。
1. 「アカウント設定」領域に「キーストアを作成」リンクが表示されたら、そのリンクをクリックします。パスワードを設定して、「OK」をクリックします。
1. 「アカウント設定」領域で、「キーストアを管理」をクリックします。

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. 「秘密鍵をキーストアファイルから追加」をクリックします。

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. 「キーストアファイルを選択」をクリックし、author.keystore ファイルまたは author.pfx ファイル（pkcs#12 を使用する場合）を参照して選択したら、「開く」をクリックします。
1. キーストアのエイリアスとパスワードを入力します。秘密鍵のエイリアスとパスワードを入力して、「送信」をクリックします。
1. キーストア管理ダイアログボックスを閉じます。

   ![chlimage_1-67](assets/chlimage_1-67.png)

### パブリッシュの証明書のインストール {#install-the-publish-certificate}

1. オーサーインスタンスの User Management ページを開きます。（[http://localhost:4502/libs/granite/security/content/useradmin.html](http://localhost:4502/libs/granite/security/content/useradmin.html)）
1. ユーザーアカウントのプロパティを開くには、ユーザー名をクリックまたはタップします。
1. 「アカウント設定」領域に「TrustStore を作成」リンクが表示されたら、そのリンクをクリックします。TrustStore のパスワードを作成して、「OK」をクリックします。
1. 「アカウント設定」領域で、「TrustStore を管理」をクリックします。
1. 「証明書を CER ファイルから追加」をクリックします。

   ![chlimage_1-68](assets/chlimage_1-68.png)

1. 「証明書をユーザーにマッピング」チェックボックスをオフにします。「証明書ファイルを選択」をクリックし、publish.cer を選択して、「開く」をクリックします。
1. TrustStore 管理ダイアログボックスを閉じます。

   ![chlimage_1-69](assets/chlimage_1-69.png)

## パブリッシュで秘密鍵と TrustStore をインストール {#install-private-key-and-truststore-on-publish}

パブリッシュインスタンスに次の項目をインストールします。

* パブリッシュインスタンスの秘密鍵。
* オーサーインスタンスの証明書。レプリケーションリクエストを実行するために使用するユーザーに証明書を関連付けます。

次の手順を実行するには、パブリッシュインスタンスの管理者としてログインする必要があります。

### パブリッシュの秘密鍵をインストール {#install-the-publish-private-key}

1. パブリッシュインスタンスの User Management ページを開きます。（[http://localhost:4503/libs/granite/security/content/useradmin.html](http://localhost:4503/libs/granite/security/content/useradmin.html)）
1. ユーザーアカウントのプロパティを開くには、ユーザー名をクリックまたはタップします。
1. 「アカウント設定」領域に「キーストアを作成」リンクが表示されたら、そのリンクをクリックします。パスワードを設定して、「OK」をクリックします。
1. 「アカウント設定」領域で、「キーストアを管理」をクリックします。
1. 「秘密鍵をキーストアファイルから追加」をクリックします。
1. 「キーストアファイルを選択」をクリックし、publish.keystore ファイルまたは publish.pfx ファイル（pkcs#12 を使用する場合）を探して選択し、「開く」をクリックします。
1. キーストアのエイリアスとパスワードを入力します。秘密鍵のエイリアスとパスワードを入力して、「送信」をクリックします。
1. キーストア管理ダイアログボックスを閉じます。

### オーサーの証明書をインストール {#install-the-author-certificate}

1. パブリッシュインスタンスの User Management ページを開きます。（[http://localhost:4503/libs/granite/security/content/useradmin.html](http://localhost:4503/libs/granite/security/content/useradmin.html)）
1. 「グローバルトラストストア」領域に「TrustStore を作成」リンクが表示されたら、そのリンクをクリックします。TrustStore のパスワードを作成して、「OK」をクリックします。
1. 「アカウント設定」領域で、「TrustStore を管理」をクリックします。
1. 「証明書を CER ファイルから追加」をクリックします。
1. 「証明書をユーザーにマップ」チェックボックスがオンになっていることを確認します。「証明書ファイルを選択」をクリックし、author.cer を選択して、「開く」をクリックします。
1. 「送信」をクリックして、TrustStore 管理ダイアログボックスを閉じます。

## パブリッシュでの HTTP サービスの設定 {#configure-the-http-service-on-publish}

発行インスタンスで Apache Felix Jetty ベースの HTTP サービスプロパティを設定して、発行インスタンスが Granite キーストアにアクセスする際に HTTPS を使用するようにします。サービスの PID は `org.apache.felix.http` です。

次の表は、Web コンソールを使用する場合に設定する必要のある OSGi のプロパティを示しています。

| Web コンソールでのプロパティ名 | OSGi のプロパティ名 | 値 |
|---|---|---|
| HTTPS を有効化 | org.apache.felix.https.enable | true |
| HTTPS を有効化して Granite KeyStore を使用 | org.apache.felix.https.use.granite.keystore | true |
| HTTPS ポート | org.osgi.service.http.port.secure | 8443（またはその他の必要なポート） |
| クライアント証明書 | org.apache.felix.https.clientcertificate | 「クライアント証明書が必要」 |

## オーサーでレプリケーションエージェントを設定 {#configure-the-replication-agent-on-author}

パブリッシュインスタンスへの接続時に HTTPS プロトコルを使用するように、オーサーインスタンス上のレプリケーションエージェントを設定します。レプリケーションエージェントの設定について詳しくは、[レプリケーションエージェントを設定](/help/sites-deploying/replication.md#configuring-your-replication-agents)を参照してください。

MSSL を有効にするには、次の表に示すように、「トランスポート」タブでプロパティを設定します。

<table>
 <tbody>
  <tr>
   <th>プロパティ</th>
   <th>値</th>
  </tr>
  <tr>
   <td>URI</td>
   <td><p>https://server_name:SSL_port/bin/receive?sling:authRequestLogin=1</p> <p>次に例を示します。</p> <p>http://localhost:8443/bin/receive?sling:authRequestLogin=1</p> </td>
  </tr>
  <tr>
   <td>User</td>
   <td>値なし</td>
  </tr>
  <tr>
   <td>パスワード</td>
   <td>値なし</td>
  </tr>
  <tr>
   <td>SSL</td>
   <td>クライアント認証</td>
  </tr>
 </tbody>
</table>

![chlimage_1-70](assets/chlimage_1-70.png)

レプリケーションエージェントの設定が完了したら、接続をテストして、MSSL が正しく設定されているかどうかを確認します。

```xml
29.08.2014 14:02:46 - Create new HttpClient for Default Agent
29.08.2014 14:02:46 - * HTTP Version: 1.1
29.08.2014 14:02:46 - * Using Client Auth SSL configuration *
29.08.2014 14:02:46 - adding header: Action:Test
29.08.2014 14:02:46 - adding header: Path:/content
29.08.2014 14:02:46 - adding header: Handle:/content
29.08.2014 14:02:46 - deserialize content for delivery
29.08.2014 14:02:46 - No message body: Content ReplicationContent.VOID is empty
29.08.2014 14:02:46 - Sending POST request to http://localhost:8443/bin/receive?sling:authRequestLogin=1
29.08.2014 14:02:46 - sent. Response: 200 OK
29.08.2014 14:02:46 - ------------------------------------------------
29.08.2014 14:02:46 - Sending message to localhost:8443
29.08.2014 14:02:46 - >> POST /bin/receive HTTP/1.0
29.08.2014 14:02:46 - >> Action: Test
29.08.2014 14:02:46 - >> Path: /content
29.08.2014 14:02:46 - >> Handle: /content
29.08.2014 14:02:46 - >> Referer: about:blank
29.08.2014 14:02:46 - >> Content-Length: 0
29.08.2014 14:02:46 - >> Content-Type: application/octet-stream
29.08.2014 14:02:46 - --
29.08.2014 14:02:46 - << HTTP/1.1 200 OK
29.08.2014 14:02:46 - << Connection: Keep-Alive
29.08.2014 14:02:46 - << Server: Day-Servlet-Engine/4.1.64
29.08.2014 14:02:46 - << Content-Type: text/plain;charset=utf-8
29.08.2014 14:02:46 - << Content-Length: 26
29.08.2014 14:02:46 - << Date: Fri, 29 Aug 2014 18:02:46 GMT
29.08.2014 14:02:46 - << Set-Cookie: login-token=3529326c-1500-4888-a4a3-93d299726f28%3ac8be86c6-04bb-4d18-80d6-91278e08d720_98797d969258a669%3acrx.default; Path=/; HttpOnly; Secure
29.08.2014 14:02:46 - << Set-Cookie: cq-authoring-mode=CLASSIC; Path=/; Secure
29.08.2014 14:02:46 - <<
29.08.2014 14:02:46 - << R
29.08.2014 14:02:46 - << eplicationAction TEST ok.
29.08.2014 14:02:46 - Message sent.
29.08.2014 14:02:46 - ------------------------------------------------
29.08.2014 14:02:46 - Replication (TEST) of /content successful.
Replication test succeeded
```
