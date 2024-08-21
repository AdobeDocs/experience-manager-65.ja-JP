---
title: AEM forms でのシングルサインオンの有効化
description: HTTP ヘッダーと SPNEGO を使用してシングルサインオン（SSO）を有効化する方法について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 89561ed0-d094-4ef7-9bc1-bde11f3c5bc3
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Security
role: User, Developer
source-git-commit: c941de0b069b5bea9edb822eca0ebbb5483ae9ed
workflow-type: tm+mt
source-wordcount: '1704'
ht-degree: 84%

---

# AEM forms でのシングルサインオンの有効化 {#enabling-single-sign-on-in-aem-forms}

AEM フォームでシングルサインオン（SSO）を有効化するには、HTTP ヘッダーと SPNEGO の 2 つの方法があります。

SSO を使用すると、ユーザーが会社のポータルで既に認証されている場合、AEM Forms ユーザーのログインページは不要になり、ログインページは表示されません。

AEM Forms で前述のいずれの方法を使用してもユーザーが認証されない場合、ユーザーはログインページにリダイレクトされます。

* [HTTP ヘッダーの使用による SSO の有効化](#enable-sso-using-http-headers)
* [SPNEGO を使用した SSO を有効化](#enable-sso-using-spnego)
* [ユーザーとグループへの役割の割り当て](#assign-roles-to-users-groups)

## HTTP ヘッダーの使用による SSO の有効化 {#enable-sso-using-http-headers}

ポータル設定ページを使用すると、アプリケーションと、HTTP ヘッダー経由での ID の転送をサポートする任意のアプリケーションとの間で、シングルサインオン（SSO）を有効にすることができます。 SSO を使用すると、ユーザーが会社のポータルで既に認証されている場合、AEM Forms ユーザーのログインページは不要になり、ログインページは表示されません。

また、SPNEGO を使用して SSO を有効化することもできます（[SPNEGO を使用した SSO の有効化](enabling-single-sign-on-aem.md#enable-sso-using-spnego)を参照。）

1. 管理コンソールで、設定/User Management/設定/ポータル属性の設定をクリックしてください。
1. 「はい」を選択して SSO を有効化します。「いいえ」を選択した場合、ページの残りの設定が使用できなくなります。
1. 必要に応じて、ページの残りの設定を調整し、「OK」をクリックします。

   * **SSO の種類：**（必須）HTTP ヘッダーを使用して SSO を有効化するには HTTP ヘッダーを選択します。
   * **ユーザーの識別子の HTTP ヘッダー：**（必須）ログインしたユーザーの固有な識別子を値に含むヘッダーの名前です。User Management は、この値を使用して User Management データベースからユーザーを検索します。このヘッダーから取得される値は、LDAP ディレクトリから同期されるユーザーの固有な識別子と一致する必要があります（[ユーザー設定](/help/forms/using/admin-help/adding-configuring-users.md#user-settings)を参照）。
   * **ユーザー固有の識別子ではなく、ユーザー ID に対して識別子の値をマップします：**&#x200B;ユーザー固有の識別子の値をユーザー ID にマップします。このオプションを選択するのは、ユーザー固有の識別子が、HTTP ヘッダーで簡単に伝播できないバイナリ値の場合です（例えば、Active Directory からユーザーを同期する場合は objectGUID）。
   * **ドメインの HTTP ヘッダー：**（非必須）ドメイン名を値に含むヘッダー名です。この設定は、ユーザーを一意に識別する単一の HTTP ヘッダーが存在しない場合にのみ使用します。この設定は、複数のドメインが存在し、固有な識別子がそのドメイン内でのみ一意である場合に使用します。この場合、このテキストボックスでヘッダー名を指定し、「ドメインマッピング」ボックスに複数のドメインのドメインマッピングを指定します（[既存のドメインの編集と変換](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains)を参照）。
   * **ドメインマッピング：**（必須）複数のドメインのマッピングは、「*header value=domain name*」の形式で指定します。

     例えば、ドメインの HTTP ヘッダーが domainName で、その値に domain1、domain2 または domain3 を使用できる状況を考えます。この場合は、ドメインマッピングを使用して domainName の値を User Management のドメイン名にマップします。各マッピングは、異なる行で指定する必要があります。

     domain1=UMdomain1

     domain2=UMdomain2

     domain3=UMdomain3

### 許可されているリファラーの設定 {#configure-allowed-referers}

許可されているリファラーの設定手順については、[許可されているリファラーの設定](/help/forms/using/admin-help/preventing-csrf-attacks.md#configure-allowed-referers)を参照してください。

### ユーザーとグループへの役割の割り当て

をクリックして、「ユーザーとグループへの役割の割り当て [ の手順を確認し ](/help/forms/using/admin-help/enabling-single-sign-on-aem.md#assign-roles-to-users-and-groups-assign-roles-to-users-groups) す。

## SPNEGO を使用した SSO を有効化 {#enable-sso-using-spnego}

Windows 環境で LDAP サーバーに Active Directory を使用している場合は、Simple and Protected GSSAPI Negotiation Mechanism（SPNEGO）を使用してシングルサインオン（SSO）を有効化することができます。SSO が有効になっている場合、AEM Forms のユーザーログインページは必要とされず、表示されません。

また、HTTP ヘッダーを使用して SSO を有効化することもできます（[HTTP ヘッダーの使用による SSO の有効化](enabling-single-sign-on-aem.md#enable-sso-using-http-headers)を参照）。

>[!NOTE]
>
>JEE 上のAEM Formsでは、複数の子ドメイン環境で Kerberos/SPNEGO を使用した SSO の設定をサポートしていません。

1. SSO を有効化するために使用するドメインを決定します。AEM Forms サーバーとユーザーは、同じ Windows ドメインまたは信頼されたドメインの一部である必要があります。
1. Active Directory に、AEM Forms サーバーを表すユーザーを作成します（[ユーザーアカウントの作成](enabling-single-sign-on-aem.md#create-a-user-account)を参照）。複数のドメインで SPNEGO を使用するように設定している場合、これらの各ユーザーのパスワードが異なっていることを確認してください。パスワードが同じ場合、SPNEGO SSO は機能しません。
1. サービスプリンシパル名をマップします（[サービスプリンシパル名（SPN）のマッピング](enabling-single-sign-on-aem.md#map-a-service-principal-name-spn)を参照）。
1. ドメインコントローラーを設定します（[Kerberos 整合性チェックの失敗の回避](enabling-single-sign-on-aem.md#prevent-kerberos-integrity-check-failures)を参照）。
1. [ドメインの追加](/help/forms/using/admin-help/adding-domains.md#adding-domains)または[既存のドメインの編集と変換](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains)で説明されているとおりに、エンタープライズドメインを追加または編集します。エンタープライズドメインを作成または編集するときは、次のタスクを実行する必要があります。

   * Active Directory の情報を含むディレクトリを追加または編集します。
   * 認証プロバイダーとして LDAP を追加します。
   * 認証プロバイダーとして Kerberos を追加します。Kerberos の新規認証ページまたは認証を編集ページに、以下の情報を入力します。

      * **認証プロバイダー：** Kerberos
      * **DNS IP：** AEM Forms を実行しているサーバーの DNS IP アドレス。この IP アドレスは、コマンドラインで `ipconfig/all` を実行して確認できます。
      * **KDC ホスト：**&#x200B;認証に使用する Active Directory サーバーの完全修飾ホスト名または IP アドレス。
      * **サービスユーザー：** KtPass ツールに渡されるサービスプリンシパル名（SPN）。前に挙げた例では、サービスパスワードは `HTTP/lcserver.um.lc.com` です。
      * **サービス領域：** Active Directory のドメイン名。前に挙げた例では、サービスパスワードは `UM.LC.COM.` です。
      * **サービスパスワード：**&#x200B;サービスユーザーのパスワード。前に挙げた例では、サービスパスワードは `password` です。
      * **SPNEGO を有効にする：**&#x200B;シングルサインオン（SSO）で SPNEGO を使用できるようにします。このオプションを選択します。

1. SPNEGO クライアントブラウザー設定を設定します（[SPNEGO クライアントブラウザー設定の設定](enabling-single-sign-on-aem.md#configuring-spnego-client-browser-settings)を参照）。

### ユーザーアカウントを作成 {#create-a-user-account}

1. SPNEGO の場合、AEM Forms となるドメインコントローラー上にある Active Directory 内のユーザーとしてサービスを登録します。そのドメインコントローラーで、スタートメニュー／管理ツール／Active Directory ユーザーとコンピューターに移動します。「管理ツール」がスタートメニューにない場合は、コントロールパネルを使用します。
1. Users フォルダーをクリックして、ユーザーのリストを表示します。
1. Users フォルダーを右クリックし、新規作成／ユーザーを選択します。
1. 「姓」、「名」および「ユーザーログオン名」を入力し、「次へ」をクリックします。例えば、次の値を設定します。

   * **名**：umspnego
   * **ユーザーログオン名**：spnegodemo

1. パスワードを入力します。例えば、「*password*」というパスワードを設定します。「パスワードを無期限にする」を選択し、それ以外のオプションは選択しません。
1. 「次へ」をクリックし、「完了」をクリックします。

### サービスプリンシパル名（SPN）のマッピング {#map-a-service-principal-name-spn}

1. KtPass ユーティリティを入手します。このユーティリティは、SPN を REALM にマップする場合に使用します。KtPass ユーティリティは、Windows Server ツールパックまたはリソースキットの一部として入手できます（[Windows Server 2003 Service Pack 1 のサポートツール](https://support.microsoft.com/kb/892777)を参照）。
1. コマンドプロンプトで、次の引数を指定して `ktpass` を実行します。

   `ktpass -princ HTTP/`*host* `@`*REALM* `-mapuser`*user*

   例えば、次のようにテキストを入力します。

   `ktpass -princ HTTP/lcserver.um.lc.com@UM.LC.COM -mapuser spnegodemo`

   指定する値は、次のとおりです。

   **host：** Forms サーバーの完全修飾名または一意の URL です。この例では、lcserver.um.lc.com に設定しています。

   **REALM：**&#x200B;ドメインコントローラーの Active Directory 領域です。この例では、UM.LC.COM に設定しています。領域は大文字で入力してください。Windows 2003 の領域を決めるには、次の手順を実行します。

   * 「マイコンピューター」を右クリックし、「プロパティ」を選択します。
   * 「コンピューター名」タブをクリックします。「ドメイン名」の値が領域名です。

   **user：**&#x200B;前のタスクで作成したユーザーアカウントのログイン名です。この例では、spnegodemo に設定しています。

次のようなエラーが発生することがあります。

```shell
DsCrackNames returned 0x2 in the name entry for spnegodemo.
ktpass:failed getting target domain for specified user.
```

この場合、次のようにユーザーを spnegodemo@um.lc.com に指定してください。

```shell
ktpass -princ HTTP/lcserver.um.lc.com@UM.LC.COM -mapuser spnegodemo
```

### Kerberos 整合性チェックの失敗の回避 {#prevent-kerberos-integrity-check-failures}

1. そのドメインコントローラーで、スタートメニュー／管理ツール／Active Directory ユーザーとコンピューターに移動します。「管理ツール」がスタートメニューにない場合は、コントロールパネルを使用します。
1. Users フォルダーをクリックして、ユーザーのリストを表示します。
1. 前のタスクで作成したユーザーアカウントを右クリックします。この例では、ユーザーアカウントは `spnegodemo` です。
1. 「パスワードのリセット」をクリックします。
1. 以前に入力したものと同じパスワードを入力し、確認します。この例では、`password` に設定されています。
1. 「ユーザーは次回ログオン時にパスワード変更が必要」を選択解除し、「OK」をクリックします。

### SPNEGO クライアントブラウザー設定の設定 {#configuring-spnego-client-browser-settings}

SPNEGO ベースの認証を機能させるには、ユーザーアカウントを作成しているドメインにクライアントコンピューターが含まれている必要があります。また、SPNEGO ベースの認証を許可するようにクライアントブラウザーを設定する必要があります。また、SPNEGO ベースの認証を必要とするサイトは、信頼できるサイトである必要があります。

https://lcserver:8080 などのコンピューター名を使用してサーバーにアクセスする場合、Internet Explorer での設定は不要です。入力した URL にドット（「.」）が含まれていない場合は、Internet Explorer はそのサイトをローカルなイントラネットサイトとして扱います。サイトに完全修飾名を使用している場合は、サイトを信頼できるサイトとして追加する必要があります。

**Internet Explorer 6.x の設定**

1. ツール／インターネットオプションに移動し、「セキュリティ」タブをクリックします。
1. ローカルなイントラネットのアイコンをクリックし、「サイト」をクリックします。
1. 「詳細設定」をクリックし、「次の web サイトをゾーンに追加する」ボックスに、Forms サーバーの URL を入力します。例えば、`https://lcserver.um.lc.com`
1. ダイアログボックスがすべて閉じるまで、各ダイアログボックスで「OK」をクリックします。
1. AEM Forms サーバーの URL にアクセスして、設定をテストします。例えば、ブラウザーの URL ボックスに `https://lcserver.um.lc.com:8080/um/login?um_no_redirect=true` と入力します。

**Mozilla Firefox の設定**

1. ブラウザーの URL ボックスに `about:config` と入力します。

   about:config - Mozilla Firefox ダイアログボックスが表示されます。

1. 「フィルター」ボックスに、`negotiate`
1. 表示されたリストで、network.negotiate-auth.trusted-uri をダブルクリックし、環境に応じて、次のいずれかのコマンドを入力します。

   `.um.lc.com` - 末尾が um.lc.com のすべての URL を SPNEGO に対して許可するよう Firefox を設定します。先頭に必ずドット（「.」）を含めてください。

   `lcserver.um.lc.com` - 特定のサーバーだけに SPNEGO を許可するように Firefox が設定されます。ドット（「.」）から始めないでください。

1. アプリケーションにアクセスして、設定をテストします。ターゲットアプリケーションのようこそページが表示されます。

をクリックして、「ユーザーとグループへの役割の割り当て [ の手順を確認し ](/help/forms/using/admin-help/enabling-single-sign-on-aem.md#assign-roles-to-users-and-groups-assign-roles-to-users-groups) す。

## ユーザーとグループへの役割の割り当て {#assign-roles-to-users-groups}

1. JEE 上のAEM Forms環境にログインします。
1. 管理コンソールで、設定/User Management/ドメインの管理をクリックします。
1. ドメイン設定（例：LDAP）を選択し、クリックします。 ディレクトリに、作成されたすべてのユーザーとグループが表示されます。 必要に応じて、新しいユーザーまたはグループを作成できます。
   ![ ドメイン管理ページ ](/help/forms/using/assets/domain-mgmt-page.png)
1. [ 認証 ] をクリックします。新しいページで、LDAP などの認証プロバイダを選択します。
1. 「Domain Management」ページに移動し、「LDAP」を選択して「**Syn Now**」をクリックし、AEMアクセス用にディレクトリを構成した認証スキームと同期させます。
   ![LDAP の同期 ](/help/forms/using/assets/sync-ldap.png)
1. User Management に移動し、「ユーザーとグループ」をクリックします。
1. 次の画像に示すように、ユーザーまたはグループを名前で検索します。
   ![ ユーザーグループを検索 ](/help/forms/using/assets/search-user-group.png)
1. 必要に応じて、役割をユーザーまたはグループに割り当てます。
   ![ ユーザーロールの割り当て ](/help/forms/using/assets/user-role-assign.png)

