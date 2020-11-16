---
title: AEM 6 での LDAP の設定
seo-title: AEM 6 での LDAP の設定
description: AEM で LDAP を設定する方法について説明します。
seo-description: AEM で LDAP を設定する方法について説明します。
uuid: 0007def4-86f0-401d-aa37-c8d49d5acea1
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 5faf6ee5-9242-48f4-87a8-ada887a3be1e
translation-type: tm+mt
source-git-commit: 2fc35bfd93585a586cb1d4e3299261611db49ba6
workflow-type: tm+mt
source-wordcount: '1661'
ht-degree: 94%

---


# AEM 6 での LDAP の設定 {#configuring-ldap-with-aem}

LDAP（**L** ightweight **D** irectory **A** ccess **P** rotocol）は、統合されたディレクトリサービスへのアクセスに使用します。これにより、複数のアプリケーションからユーザーアカウントにアクセスできるようになるので、ユーザーアカウントの管理に必要な作業を削減できます。このような LDAP サーバーの一例として Active Directory があります。多くの場合、LDAP はシングルサインオン（ユーザーが 1 回ログインすると複数のアプリケーションにアクセスできる機能）を実現するために使用されます。

リポジトリに保存されている LDAP アカウントの詳細を使用して、LDAP サーバーとリポジトリの間でユーザーアカウントを同期できます。これにより、アカウントをリポジトリグループに割り当てて、必要な権限や特別な権限を付与することができます。

リポジトリでは LDAP 認証を使用してこれらのユーザーを認証します。認証の際は、検証用に LDAP サーバーに渡される資格情報が使用されます。この認証は、リポジトリへのアクセスを許可する前におこなう必要があります。パフォーマンスを向上させるために、検証が成功した資格情報をリポジトリでキャッシュできます。有効期限のタイムアウトを使用すると、適切な期間が経過した後に再検証がおこなわれます。

LDAP サーバーからアカウントが削除されると、検証はおこなわれないので、リポジトリへのアクセスは拒否されます。リポジトリに保存された LDAP アカウントの詳細をパージすることもできます。

このようなアカウントはユーザーに対して透過的に使用され、LDAP から作成されたユーザーアカウントやグループアカウントとリポジトリで作成されたユーザーアカウントやグループアカウントの違いはユーザーにはわかりません。

AEM 6 の LDAP のサポートには、以前のバージョンとは異なるタイプの設定が必要な新しい実装が付属します。

All LDAP configurations are now available as OSGi configurations. They can be configured via the Web Management console at:
`https://serveraddress:4502/system/console/configMgr`

LDAP と AEM を連携させるには、次の 3 つの OSGi 設定を作成する必要があります。

1. LDAP Identity Provider（IDP）
1. Sync Handler
1. External Login Module

>[!NOTE]
>
>External Login Module について詳しくは、[Oak の External Login Module - LDAP との認証および詳細（英語）](https://docs.adobe.com/content/ddc/en/gems/oak-s-external-login-module---authenticating-with-ldap-and-beyon.html#)をご覧ください。
>
>Apache DS を使用した Experience Manager の設定例については、[Apache Directory Serviceを使用するための Adobe Experience Manager 6.5 の設定](https://helpx.adobe.com/jp/experience-manager/using/configuring-aem64-apache-directory-service.html)を参照してください。

## LDAP Identity Provider の設定 {#configuring-the-ldap-identity-provider}

LDAP Identity Provider は、LDAP サーバーからのユーザーの取得方法を定義するために使用します。

このプロバイダーは、管理コンソールの **Apache Jackrabbit Oak LDAP Identity Provider** という名前の下にあります。

LDAP Identity Provider では次の設定オプションを使用できます。

<table>
 <tbody>
  <tr>
   <td><strong>LDAP Provider Name</strong></td>
   <td>この LDAP Provider 設定の名前</td>
  </tr>
  <tr>
   <td><strong>LDAP Server Hostname</strong><br /> </td>
   <td>LDAP サーバーのホスト名</td>
  </tr>
  <tr>
   <td><strong>LDAP Server Port</strong></td>
   <td>LDAP サーバーのポート</td>
  </tr>
  <tr>
   <td><strong>Use SSL</strong></td>
   <td>SSL（LDAP）接続を使用する必要があるかどうかを示します。</td>
  </tr>
  <tr>
   <td><strong>Use TLS</strong></td>
   <td>接続で TLS を開始する必要があるかどうかを示します。</td>
  </tr>
  <tr>
   <td><strong>Disable certificate checking</strong></td>
   <td>サーバー証明書の検証を無効にする必要があるかどうかを示します。</td>
  </tr>
  <tr>
   <td><strong>Bind DN</strong></td>
   <td>認証用のユーザーの DN。このオプションを空のままにすると、匿名バインドが実行されます。</td>
  </tr>
  <tr>
   <td><strong>Bind Password</strong></td>
   <td>認証用のユーザーのパスワード</td>
  </tr>
  <tr>
   <td><strong>Search timeout</strong></td>
   <td>検索がタイムアウトするまでの時間</td>
  </tr>
  <tr>
   <td><strong>Admin pool max active</strong></td>
   <td>管理接続プールの最大アクティブサイズ。</td>
  </tr>
  <tr>
   <td><strong>User pool max active</strong></td>
   <td>ユーザー接続プールの最大アクティブサイズです。</td>
  </tr>
  <tr>
   <td><strong>User base DN</strong></td>
   <td>ユーザー検索用の DN</td>
  </tr>
  <tr>
   <td><strong>User object classes</strong></td>
   <td>ユーザーエントリが格納する必要のあるオブジェクトクラスのリスト</td>
  </tr>
  <tr>
   <td><strong>User id attribute</strong></td>
   <td>ユーザー ID を格納する属性の名前</td>
  </tr>
  <tr>
   <td><strong>User extra filter</strong></td>
   <td>ユーザーの検索時に使用する追加の LDAP フィルター。最後のフィルターの形式は次のようになります。'(&amp;(&lt;idAttr&gt;=&lt;userId&gt;)(objectclass=&lt;objectclass&gt;)&lt;extraFilter&gt;)' (user.extraFilter)</td>
  </tr>
  <tr>
   <td><strong>User DN paths</strong></td>
   <td>DN を使用して中間パスの一部を計算する必要があるかどうかを制御します。</td>
  </tr>
  <tr>
   <td><strong>Group base DN</strong></td>
   <td>グループ検索用のベース DN</td>
  </tr>
  <tr>
   <td><strong>Group object classes</strong></td>
   <td>グループエントリが格納する必要のあるオブジェクトクラスのリスト</td>
  </tr>
  <tr>
   <td><strong>Group name attribute</strong></td>
   <td>グループ名を格納する属性の名前</td>
  </tr>
  <tr>
   <td><strong>Group extra filter</strong></td>
   <td>グループの検索時に使用する追加の LDAP フィルター。最後のフィルターの形式は次のようになります。'(&amp;(&lt;nameAttr&gt;=&lt;groupName&gt;)(objectclass=&lt;objectclass&gt;)&lt;extraFilter&gt;)'</td>
  </tr>
  <tr>
   <td><strong>Group DN paths</strong></td>
   <td>DN を使用して中間パスの一部を計算する必要があるかどうかを制御します。</td>
  </tr>
  <tr>
   <td><strong>Group member attribute</strong></td>
   <td>グループのメンバーを格納するグループ属性</td>
  </tr>
 </tbody>
</table>

## Sync Handler の設定 {#configuring-the-synchronization-handler}

Sync Handler は、Indentity Provider のユーザーとグループをリポジトリと同期する方法を定義します。

このハンドラーは、管理コンソールの **Apache Jackrabbit Oak Default Sync Handler** という名前の下にあります。

Sync Handler では次の設定オプションを使用できます。

<table>
 <tbody>
  <tr>
   <td><strong>Sync Handler Name</strong></td>
   <td>同期設定の名前</td>
  </tr>
  <tr>
   <td><strong>User Expiration Time</strong></td>
   <td>同期されたユーザーが期限切れになるまでの期間</td>
  </tr>
  <tr>
   <td><strong>User auto membership</strong></td>
   <td>同期されたユーザーが自動的に追加されるグループのリスト</td>
  </tr>
  <tr>
   <td><strong>User property mapping</strong></td>
   <td>外部のプロパティからのローカルのプロパティのマッピング定義のリスト</td>
  </tr>
  <tr>
   <td><strong>User Path Prefix</strong></td>
   <td>新しいユーザーの作成時に使用されるパスのプレフィックス</td>
  </tr>
  <tr>
   <td><strong>User Membership Expiration</strong></td>
   <td>メンバーシップが期限切れになるまでの時間<br /> </td>
  </tr>
  <tr>
   <td><strong>User membership nesting depth</strong></td>
   <td>メンバーシップの関係が同期される場合のグループのネストの最大の深さを返します。値 0 を指定すると、グループのメンバーシップのルックアップが事実上無効になります。値 1 を指定すると、ユーザーの直接のグループのみが追加されます。ユーザーのメンバーシップの先祖を同期する際にのみ個々のグループを同期する場合、この値は有効ではありません。</td>
  </tr>
  <tr>
   <td><strong>Group Expiration Time</strong></td>
   <td>同期されたグループが期限切れになるまでの期間</td>
  </tr>
  <tr>
   <td><strong>Group auto membership</strong></td>
   <td>同期されたグループが自動的に追加されるグループのリスト</td>
  </tr>
  <tr>
   <td><strong>Group property mapping</strong></td>
   <td>外部のプロパティからのローカルのプロパティのマッピング定義のリスト</td>
  </tr>
  <tr>
   <td><strong>Group path prefix</strong></td>
   <td>新しいグループの作成時に使用されるパスのプレフィックス</td>
  </tr>
 </tbody>
</table>

## External Login Module {#the-external-login-module}

External Login Module は、管理コンソールの **Apache Jackrabbit Oak External Login Module** の下にあります。

>[!NOTE]
>
>Apache Jackrabbit Oak External Login Module は、Java 認証・承認サービス（JAAS）の仕様を実装します。詳しくは、[Oracle 公式の Java セキュリティリファレンスガイド](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jaas/JAASRefGuide.html)を参照してください。

このモジュールは、使用する Identity Provider と Sync Handler を定義して、2 つのモジュールを効率的にバインドします。

以下の設定オプションを使用できます。

| **JAAS Ranking** | このログインモジュールのエントリのランキング（並べ替え順）を指定します。エントリは降順に並べ替えられます（ランクの高い設定が先頭になります）。 |
|---|---|
| **JAAS Control Flag** | LoginModule が REQUIRED、REQUISITE、SUFFICIENT、OPTIONAL のいずれかを指定するプロパティ。これらのフラグの意味について詳しくは、JAAS の設定ドキュメントを参照してください。 |
| **JAAS Realm** | LoginModule が登録されている領域名（またはアプリケーション名）。領域名を指定しない場合は、Felix JAAS 設定に指定されているように、LoginModule はデフォルトの領域に登録されます。 |
| **Identity Provider Name** | Identity Provider の名前 |
| **Sync Handler Name** | Sync Handler の名前 |

>[!NOTE]
>
>AEM インスタンスで複数の LDAP 設定を使用する場合は、設定ごとに Identity Provider と Sync Handler を個別に作成する必要があります。

## LDAP over SSL の設定 {#configure-ldap-over-ssl}

次の手順に従って、LDAP over SSL を使用して認証をおこなうように AEM 6 を設定できます。

1. [LDAP Identity Provider](#configuring-the-ldap-identity-provider) を設定する場合は、「**Use SSL**」チェックボックスまたは「**Use TLS**」チェックボックスをオンにします。
1. 設定に応じて Sync Handler と External Login Module を設定します。
1. 必要に応じて、Java VM に SSL 証明書をインストールします。そのためには、keytool を使用します。

   `keytool -import -alias localCA -file <certificate location> -keystore <keystore location>`

1. LDAP サーバーへの接続をテストします。

### SSL 証明書の作成 {#creating-ssl-certificates}

SSL 経由で LDAP を使用して認証をおこなうように AEM を設定する場合は、自己署名証明書を使用できます。AEM で使用する証明書の生成手順の例を次に示します。

1. SSL ライブラリがインストールされ、機能していることを確認します。この手順では、例として OpenSSL を使用します。

1. カスタマイズした OpenSSL 設定（cnf）ファイルを作成します。これは、デフォルトの**openssl.cnf **設定ファイルをコピーしてカスタマイズすることで実行できます。 On UNIX systems, it is usually located at `/usr/lib/ssl/openssl.cnf`

1. ターミナルで次のコマンドを実行して CA ルートキーを作成します。

   ```
   openssl genpkey -algorithm [public key algorithm] -out certificatefile.key -pkeyopt [public key algorithm option]
   ```

1. 次に、新しい自己署名証明書を作成します。

   `openssl req -new -x509 -days [number of days for certification] -key certificatefile.key -out root-ca.crt -config CA/openssl.cnf`

1. 新しく生成した証明書に問題がないことを確認します。

   `openssl x509 -noout -text -in root-ca.crt`

1. 証明書設定（.cnf）ファイルで指定したすべてのフォルダーが存在することを確認します。存在しない場合は、作成してください。
1. コマンドを実行してランダムシードを作成します。次に例を示します。

   `openssl rand -out private/.rand 8192`

1. 作成した .pem ファイルを .cnf ファイルで設定した場所に移動します。

1. 最後に、Java キーストアに証明書を追加します。

## デバッグログの有効化 {#enabling-debug-logging}

LDAP Identity Provider と External Login Module の両方に対してデバッグログを有効にして、接続の問題のトラブルシューティングをおこなうことができます。

デバッグログを有効にするには、次の手順をおこなう必要があります。

1. Web 管理コンソールに移動します。
1. 「Apache Sling Logging Logger Configuration」を探し、次のオプションを使用して 2 つのロガーを作成します。

* Log level：Debug
* Log File：logs/ldap.log
* Message Pattern:{0,date,dd.MM.yyyy HH:mm:ss.SSS} &amp;ast;{4}&amp;ast;{2} {3} {5}
* Logger：org.apache.jackrabbit.oak.security.authentication.ldap

* Log level：Debug
* Log File：logs/external.log
* Message Pattern:{0,date,dd.MM.yyyy HH:mm:ss.SSS} &amp;ast;{4}&amp;ast;{2} {3} {5}
* Logger：org.apache.jackrabbit.oak.spi.security.authentication.external

## グループへの関連付けに関する注意事項 {#a-word-on-group-affiliation}

LDAP で同期されたユーザーは、AEM の別のグループに含めることが可能です。同期プロセスの一部として AEM に追加される外部 LDAP グループにも含めることができますが、別に追加される、元の LDAP グループに関連するスキームに含まれないグループに含めることもできます。

ほとんどの場合は、ローカルの AEM 管理者またはその他の ID プロバイダーによって追加されるグループになります。

ユーザーが LDAP サーバー上のグループから削除されると、その変更は同期時に AEM 側にも反映されます。ただし、LDAP によって追加されなかったユーザーのその他のグループへの関連付けはそのまま維持されます。

AEM は `rep:externalId` プロパティを使用して、外部グループからのユーザーのパージを検出および処理します。このプロパティは Sync Handler によって同期されたすべてのユーザーとグループに自動的に追加されます。このプロパティには元の ID プロバイダーの情報が含まれます。

詳しくは、Apache Oak ドキュメントの [ユーザーとグループの同期（英語）](https://jackrabbit.apache.org/oak/docs/security/authentication/usersync.html)を参照してください。

## 既知の問題 {#known-issues}

LDAP over SSL を使用する場合は、Netscape のコメントオプションを指定せずに、使用する証明書が作成されていることを確認してください。このオプションが有効な場合は、SSL ハンドシェイクエラーが発生して認証が失敗します。

