---
title: AEM 6 での LDAP の設定
description: AEMで LDAP を設定する方法を説明します。
uuid: 0007def4-86f0-401d-aa37-c8d49d5acea1
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 5faf6ee5-9242-48f4-87a8-ada887a3be1e
exl-id: 2ebca4fb-20f7-499c-96a0-4018eaeddc1a
source-git-commit: 768576e300b655962adc3e1db20fc5ec06a5ba6c
workflow-type: tm+mt
source-wordcount: '1625'
ht-degree: 36%

---

# AEM 6 での LDAP の設定 {#configuring-ldap-with-aem}

LDAP ( **L**&#x200B;明るさ **D**&#x200B;ディレクトリ **A**&#x200B;アクセス **P** rotocol) は、一元化されたディレクトリサービスへのアクセスに使用されます。 複数のアプリケーションからアクセスできるので、ユーザーアカウントの管理に必要な作業を軽減できます。 そのような LDAP サーバの 1 つが Active Directory です。 多くの場合、LDAP はシングルサインオン（ユーザーが 1 回ログインすると複数のアプリケーションにアクセスできる機能）を実現するために使用されます。

リポジトリに保存されている LDAP アカウントの詳細を使用して、LDAP サーバーとリポジトリの間でユーザーアカウントを同期できます。この機能を使用すると、必要な権限と権限を割り当てるために、アカウントをリポジトリグループに割り当てることができます。

リポジトリでは、LDAP 認証を使用してこれらのユーザーを認証します。認証の際は、検証用に LDAP サーバーに渡される認証情報が使用されます。この認証は、リポジトリへのアクセスを許可する前に行う必要があります。パフォーマンスを向上させるために、検証が成功した認証情報をリポジトリでキャッシュできます。有効期限のタイムアウトを使用すると、適切な期間が経過した後に再検証が実行されます。

LDAP サーバーからアカウントが削除されると、検証は許可されなくなり、リポジトリへのアクセスが拒否されます。 リポジトリに保存された LDAP アカウントの詳細もパージできます。

このようなアカウントの使用は、ユーザーに対して透過的です。 つまり、LDAP から作成されたユーザーアカウントとグループアカウント、およびリポジトリ内でのみ作成されたアカウントの違いは見られません。

AEM 6 では、LDAP のサポートに、以前のバージョンとは異なるタイプの設定が必要な新しい実装が付属しています。

すべての LDAP 設定を OSGi 設定として使用できるようになりました。これらは、以下の web 管理コンソールを使用して設定できます。
`https://serveraddress:4502/system/console/configMgr`

AEMで LDAP を使用するには、次の 3 つの OSGi 設定を作成する必要があります。

1. LDAP Identity Provider（IDP）
1. 同期ハンドラー。
1. 外部ログインモジュール。

>[!NOTE]
>
>External Login Module について詳しくは、[Oak の External Login Module - LDAP との認証および詳細（英語）](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2015/aem-oak-external-login-module-authenticating-with-ldap-and-beyond.html?lang=en)をご覧ください。
>
>Apache DS を使用した Experience Manager の設定例については、[Apache Directory Service を使用するための Adobe Experience Manager 6.5 の設定](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/configuring-adobe-experience-manager-6-to-use-apache-directory/m-p/183805)を参照してください。

## LDAP Identity Provider の設定 {#configuring-the-ldap-identity-provider}

LDAP Identity Provider は、LDAP サーバーからのユーザーの取得方法を定義するために使用します。

このプロバイダーは、管理コンソールの **Apache Jackrabbit Oak LDAP Identity Provider** という名前の下にあります。

LDAP Identity Provider では、以下の設定オプションを使用できます。

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
   <td>認証用のユーザーの DN。 このフィールドを空のままにすると、匿名バインドが実行されます。</td>
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
   <td>管理接続プールの最大アクティブサイズ</td>
  </tr>
  <tr>
   <td><strong>User pool max active</strong></td>
   <td>ユーザー接続プールの最大アクティブサイズ</td>
  </tr>
  <tr>
   <td><strong>User base DN</strong></td>
   <td>ユーザー検索用の DN</td>
  </tr>
  <tr>
   <td><strong>User object classes</strong></td>
   <td>ユーザーエントリに含める必要があるオブジェクトクラスのリスト。</td>
  </tr>
  <tr>
   <td><strong>User id attribute</strong></td>
   <td>ユーザー ID を格納する属性の名前</td>
  </tr>
  <tr>
   <td><strong>User extra filter</strong></td>
   <td>ユーザーの検索時に使用する追加の LDAP フィルター。 最終フィルターは次のようにフォーマットされます。'(&amp;(&lt;idattr&gt;=&lt;userid&gt;)(objectclass=&lt;objectclass&gt;)&lt;extrafilter&gt;)' (user.extraFilter)</td>
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
   <td>グループの検索時に使用する追加の LDAP フィルタ。 最終フィルターの形式は次のようになります。'(&amp;(&lt;nameattr&gt;=&lt;groupname&gt;)(objectclass=&lt;objectclass&gt;)&lt;extrafilter&gt;)'</td>
  </tr>
  <tr>
   <td><strong>Group DN paths</strong></td>
   <td>DN を使用して中間パスの一部を計算する必要があるかどうかを制御します。</td>
  </tr>
  <tr>
   <td><strong>Group member attribute</strong></td>
   <td>グループの 1 つ以上のメンバーを含む Group 属性。</td>
  </tr>
 </tbody>
</table>

## 同期ハンドラーの設定 {#configuring-the-synchronization-handler}

同期ハンドラーは、ID プロバイダーのユーザーおよびグループをリポジトリと同期する方法を定義します。

これは、 **Apache Jackrabbit Oak デフォルト同期ハンドラー** 管理コンソールでの名前。

Sync Handler では、以下の設定オプションを使用できます。

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
   <td>同期されたユーザーが自動的に追加されるグループのリスト。</td>
  </tr>
  <tr>
   <td><strong>User property mapping</strong></td>
   <td>外部プロパティからのローカルプロパティのリストマッピング定義。</td>
  </tr>
  <tr>
   <td><strong>User Path Prefix</strong></td>
   <td>ユーザーの作成時に使用されるパスプレフィックス。</td>
  </tr>
  <tr>
   <td><strong>User Membership Expiration</strong></td>
   <td>メンバーシップが期限切れになるまでの時間<br /> </td>
  </tr>
  <tr>
   <td><strong>User membership nesting depth</strong></td>
   <td>メンバーシップ関係が同期された場合のグループのネストの最大深さを返します。 値 0 を指定すると、グループメンバーシップの参照が事実上無効になります。 値 1 は、ユーザーの直接グループのみを追加します。 ユーザーのメンバーシップの祖先を同期する場合にのみ、個々のグループを同期する場合、この値は無効です。</td>
  </tr>
  <tr>
   <td><strong>Group Expiration Time</strong></td>
   <td>同期されたグループが期限切れになるまでの期間</td>
  </tr>
  <tr>
   <td><strong>Group auto membership</strong></td>
   <td>同期されたグループが自動的に追加されるグループのリスト。</td>
  </tr>
  <tr>
   <td><strong>Group property mapping</strong></td>
   <td>外部プロパティからのローカルプロパティのリストマッピング定義。</td>
  </tr>
  <tr>
   <td><strong>Group path prefix</strong></td>
   <td>グループの作成時に使用されるパスのプレフィックス。</td>
  </tr>
 </tbody>
</table>

## 外部ログインモジュール {#the-external-login-module}

外部ログインモジュールは、 **Apache Jackrabbit Oak 外部ログインモジュール** をクリックします。

>[!NOTE]
>
>Apache Jackrabbit Oak External Login Module は、Java™ Authentication and Authorization Servi(JAAS) の仕様を実装しています。 詳しくは、 [公式OracleJava™セキュリティリファレンスガイド](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jaas/JAASRefGuide.html) を参照してください。

使用する ID プロバイダーと同期ハンドラーを定義し、2 つのモジュールを効果的にバインドします。

以下の設定オプションを使用できます。

| **JAAS Ranking** | このログインモジュールエントリのランキング（つまり、並べ替え順）を指定する。 エントリは降順で並べ替えられます（つまり、ランクの高い設定値が先になります）。 |
|---|---|
| **JAAS 制御フラグ** | LoginModule が REQUIRED、REQUISITE、SUFFICIENT、または OPTIONAL のどれであるかを指定するプロパティです。 これらのフラグの意味について詳しくは、 JAAS の設定に関するドキュメントを参照してください。 |
| **JAAS Realm** | LoginModule が登録される領域名（またはアプリケーション名）。 領域名を指定しない場合、LoginModule は Felix JAAS 設定で設定されたデフォルトの領域に登録されます。 |
| **ID プロバイダー名** | ID プロバイダーの名前。 |
| **Sync Handler Name** | 同期ハンドラーの名前。 |

>[!NOTE]
AEMインスタンスと複数の LDAP 設定を持つ予定がある場合は、各設定に対して個別の ID プロバイダーと同期ハンドラーを作成する必要があります。

## LDAP over SSL の設定 {#configure-ldap-over-ssl}

AEM 6 は、次の手順に従って、SSL 経由で LDAP で認証するように設定できます。

1. 次を確認します。 **SSL を使用** または **TLS を使用** 設定時のチェックボックス [LDAP ID プロバイダー](#configuring-the-ldap-identity-provider).
1. 設定に従って、同期ハンドラーと外部ログインモジュールを設定します。
1. 必要に応じて、Java™ VM に SSL 証明書をインストールします。 このインストールは、keytool を使用して実行できます。

   `keytool -import -alias localCA -file <certificate location> -keystore <keystore location>`

1. LDAP サーバーへの接続をテストします。

### SSL 証明書の作成 {#creating-ssl-certificates}

SSL を介して LDAP で認証するようにAEMを設定する場合は、自己署名証明書を使用できます。 次に、AEMで使用する証明書を生成する作業手順の例を示します。

1. SSL ライブラリがインストールされ、機能していることを確認します。 この手順では、例として OpenSSL を使用します。

1. カスタマイズした OpenSSL 設定（cnf）ファイルを作成します。この設定は、デフォルトの**openssl.cnf **設定ファイルをコピーし、カスタマイズすることで行うことができます。 UNIX®システムでは、 `/usr/lib/ssl/openssl.cnf`

1. ターミナルで以下のコマンドを実行して CA ルートキーを作成します。

   ```
   openssl genpkey -algorithm [public key algorithm] -out certificatefile.key -pkeyopt [public key algorithm option]
   ```

1. 次に、自己署名証明書を作成します。

   `openssl req -new -x509 -days [number of days for certification] -key certificatefile.key -out root-ca.crt -config CA/openssl.cnf`

1. すべてが正しく動作していることを確認するには、新しく生成された証明書を調べます。

   `openssl x509 -noout -text -in root-ca.crt`

1. 証明書設定 (.cnf) ファイルで指定されたすべてのフォルダが存在することを確認します。 そうでない場合は、作成します。
1. を実行して、ランダムなシードを作成します。次に例を示します。

   `openssl rand -out private/.rand 8192`

1. 作成した .pem ファイルを .cnf ファイルで設定した場所に移動します。

1. 最後に、Java™キーストアに証明書を追加します。

## デバッグログの有効化 {#enabling-debug-logging}

LDAP ID プロバイダーと外部ログインモジュールの両方でデバッグログを有効にして、接続の問題をトラブルシューティングできます。

デバッグログを有効にするには、次の操作を行う必要があります。

1. Web 管理コンソールに移動します。
1. 「Apache Sling Logging Logger Configuration」を検索し、次のオプションを使用して 2 つのロガーを作成します。

* ログレベル：デバッグ
* ログファイルlogs/ldap.log
* メッセージパターン： {0,date,dd.MM.yyyy HH:mm:ss.SSS} &amp;ast;{4}&amp;ast; {2} {3} {5}
* ロガー：org.apache.jackrabbit.oak.security.authentication.ldap

* ログレベル：デバッグ
* ログファイル：logs/external.log
* メッセージパターン： {0,date,dd.MM.yyyy HH:mm:ss.SSS} &amp;ast;{4}&amp;ast; {2} {3} {5}
* Logger：org.apache.jackrabbit.oak.spi.security.authentication.external

## グループの所属に関する言葉 {#a-word-on-group-affiliation}

LDAP を通じて同期されたユーザーは、AEMの別のグループに属することができます。 これらのグループは、同期プロセスの一環としてAEMに追加される外部 LDAP グループにすることができます。 ただし、別々に追加され、元の LDAP グループ所属スキームに含まれていないグループを指定することもできます。

通常、これらのグループは、ローカルのAEM管理者または他の ID プロバイダーによって追加されます。

ユーザーが LDAP サーバー上のグループから削除されると、同期時にAEM側に変更が反映されます。 ただし、LDAP によって追加されなかったユーザーのその他のグループ関連はすべてそのまま残ります。

AEMは、 `rep:externalId` プロパティ。 このプロパティは Sync Handler によって同期されたすべてのユーザーとグループに自動的に追加されます。このプロパティには元の ID プロバイダーの情報が含まれます。

次の Apache Oak ドキュメントを参照してください。 [ユーザーとグループの同期](https://jackrabbit.apache.org/oak/docs/security/authentication/usersync.html).

## 既知の問題 {#known-issues}

LDAP over SSL を使用する予定がある場合は、使用する証明書が Netscape のコメントオプションを使用せずに作成されていることを確認します。 このオプションが有効な場合、SSL ハンドシェイクエラーで認証が失敗します。
