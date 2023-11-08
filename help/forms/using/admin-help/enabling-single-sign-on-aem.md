---
title: AEM forms でのシングルサインオンの有効化
seo-title: Enabling single sign-on in AEM forms
description: HTTP ヘッダーと SPNEGO を使用してシングルサインオン (SSO) を有効にする方法を説明します。
seo-description: Learn how to enable single sign-on (SSO) using HTTP headers and SPNEGO.
uuid: 2bc08b4f-dcbe-4a16-9025-32fc14605e13
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ee54d9d4-190d-4665-925a-9740ac65fbd5
exl-id: 89561ed0-d094-4ef7-9bc1-bde11f3c5bc3
source-git-commit: c4cd9a61a226ace2a72d60b5b7b7432de12cb873
workflow-type: tm+mt
source-wordcount: '1520'
ht-degree: 28%

---

# AEM forms でのシングルサインオンの有効化 {#enabling-single-sign-on-in-aem-forms}

AEM Forms でシングルサインオン（SSO）を有効化するには、HTTP ヘッダーと SPNEGO の 2 つの方法があります。

SSO を実装すると、AEM forms のユーザーログインページは不要になり、ユーザーが会社のポータルで既に認証済みの場合は表示されません。

AEM forms がこれらのいずれの方法を使用してもユーザーを認証できない場合、ユーザーはログインページにリダイレクトされます。

## HTTP ヘッダーを使用した SSO の有効化 {#enable-sso-using-http-headers}

ポータル設定ページを使用して、アプリケーションと、HTTP ヘッダーを介した ID の伝送をサポートする任意のアプリケーションとの間でシングルサインオン (SSO) を有効にすることができます。 SSO を実装すると、AEM forms のユーザーログインページは不要になり、ユーザーが会社のポータルで既に認証済みの場合は表示されません。

SPNEGO を使用して SSO を有効にすることもできます。 ( 詳しくは、 [SPNEGO を使用した SSO の有効化](enabling-single-sign-on-aem.md#enable-sso-using-spnego).)

1. 管理コンソールで、設定/User Management/設定/ポータル属性の設定をクリックします。
1. 「はい」を選択して SSO を有効にします。 「いいえ」を選択した場合、ページの残りの設定は使用できなくなります。
1. 必要に応じて、ページの残りのオプションを設定し、「OK」をクリックします。

   * **SSO の種類：**（必須）HTTP ヘッダーを使用して SSO を有効化するには HTTP ヘッダーを選択します。
   * **ユーザーの識別子の HTTP ヘッダー：**（必須）ログインしたユーザーの固有な識別子を値に含むヘッダーの名前です。User Management は、この値を使用して User Management データベース内のユーザーを検索します。 このヘッダーから取得された値は、LDAP ディレクトリから同期されるユーザーの一意の識別子と一致する必要があります。 ( 詳しくは、 [ユーザー設定](/help/forms/using/admin-help/adding-configuring-users.md#user-settings).)
   * **ユーザー固有の識別子ではなく、ユーザー ID に対して識別子の値をマップします：**&#x200B;ユーザー固有の識別子の値をユーザー ID にマップします。このオプションを選択するのは、ユーザー固有の識別子が、HTTP ヘッダーで簡単に伝播できないバイナリ値の場合です（例えば、Active Directory からユーザーを同期する場合は objectGUID）。
   * **ドメインの HTTP ヘッダー：**（非必須）ドメイン名を値に含むヘッダー名です。この設定は、ユーザーを一意に識別する単一の HTTP ヘッダーがない場合にのみ使用します。 この設定は、複数のドメインが存在し、一意の識別子が 1 つのドメイン内でのみ一意である場合に使用します。 この場合は、このテキストボックスでヘッダー名を指定し、「ドメインマッピング」ボックスで複数のドメインのドメインマッピングを指定します。 （[既存のドメインの編集と変換](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains)を参照）。
   * **ドメインマッピング：**（必須）複数のドメインのマッピングは、「*header value=domain name*」の形式で指定します。

     例えば、ドメインの HTTP ヘッダーが domainName で、値に domain1、domain2、domain3 を指定できる場合を考えてみましょう。 この場合、ドメインマッピングを使用して、domainName 値を User Management のドメイン名にマッピングします。 各マッピングは異なる行に配置する必要があります。

     domain1=UMdomain1

     domain2=UMdomain2

     domain3=UMdomain3

### 許可されているリファラーの設定 {#configure-allowed-referers}

許可されているリファラーを設定する手順については、 [許可されているリファラーの設定](/help/forms/using/admin-help/preventing-csrf-attacks.md#configure-allowed-referers).

## SPNEGO を使用した SSO の有効化 {#enable-sso-using-spnego}

Windows 環境で Active Directory を LDAP サーバーとして使用する場合、Simple and Protected GSSAPI Negotiation Mechanism (SPNEGO) を使用して、シングルサインオン (SSO) を有効にすることができます。 SSO が有効な場合、AEM forms のユーザーログインページは不要で、表示されません。

また、HTTP ヘッダーを使用して SSO を有効にすることもできます。 ( 詳しくは、 [HTTP ヘッダーを使用した SSO の有効化](enabling-single-sign-on-aem.md#enable-sso-using-http-headers).)

>[!NOTE]
>
>JEE での AEM Forms は複数の子ドメイン環境で Kerberos／SPNEGO を使用した SSO の設定をサポートしていません。

1. SSO を有効にするために使用するドメインを決定します。 AEM Forms Server とユーザーは、同じ Windows ドメインまたは信頼されたドメインに属している必要があります。
1. Active Directory で、AEM Forms Server を表すユーザーを作成します。 ( 詳しくは、 [ユーザーアカウントの作成](enabling-single-sign-on-aem.md#create-a-user-account).) 複数のドメインを設定して SPNEGO を使用する場合は、各ユーザーのパスワードが異なることを確認してください。 パスワードが異なる場合、SPNEGO SSO は機能しません。
1. サービスプリンシパル名をマッピングします。 ( 詳しくは、 [サービスプリンシパル名 (SPN) のマッピング](enabling-single-sign-on-aem.md#map-a-service-principal-name-spn).)
1. ドメインコントローラーを構成します。 ( 詳しくは、 [Kerberos 整合性チェックの失敗を防ぐ](enabling-single-sign-on-aem.md#prevent-kerberos-integrity-check-failures).)
1. エンタープライズドメインの追加または編集 ( [ドメインの追加](/help/forms/using/admin-help/adding-domains.md#adding-domains) または [既存のドメインの編集と変換](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains). エンタープライズドメインを作成または編集する場合は、次のタスクを実行します。

   * Active Directory 情報を含むディレクトリを追加または編集します。
   * LDAP を認証プロバイダーとして追加します。
   * 認証プロバイダーとして Kerberos を追加します。 Kerberos の [ 新規認証 ] ページまたは [ 認証の編集 ] ページに次の情報を入力します。

      * **認証プロバイダー：** Kerberos
      * **DNS IP：** AEM Forms を実行しているサーバーの DNS IP アドレス。この IP アドレスは、コマンドラインで `ipconfig/all` を実行して確認できます。
      * **KDC ホスト：**&#x200B;認証に使用する Active Directory サーバーの完全修飾ホスト名または IP アドレス。
      * **サービスユーザー：** KtPass ツールに渡されるサービスプリンシパル名（SPN）。前に挙げた例では、サービスパスワードは `HTTP/lcserver.um.lc.com` です。
      * **サービス領域：** Active Directory のドメイン名。前に挙げた例では、サービスパスワードは `UM.LC.COM.` です。
      * **サービスパスワード：**&#x200B;サービスユーザーのパスワード。前に挙げた例では、サービスパスワードは `password` です。
      * **SPNEGO を有効にする：**&#x200B;シングルサインオン（SSO）で SPNEGO を使用できるようにします。このオプションを選択します。

1. SPNEGO クライアントブラウザーを設定します。 （[SPNEGO クライアントブラウザー設定の設定](enabling-single-sign-on-aem.md#configuring-spnego-client-browser-settings)を参照）。

### ユーザーアカウントの作成 {#create-a-user-account}

1. SPNEGO で、AEM forms を表すドメインコントローラーの Active Directory にユーザーとしてサービスを登録します。 ドメインコントローラで、[ スタート ] メニュー/[ 管理ツール ]/[Active Directory ユーザーとコンピュータ ] に移動します。 [ スタート ] メニューに [ 管理ツール ] が表示されていない場合は、Campaign コントロールパネルを使用します。
1. Users フォルダーをクリックして、ユーザーのリストを表示します。
1. user フォルダーを右クリックし、 New / User を選択します。
1. [ 名/姓 ] と [ ユーザーログオン名 ] を入力し、[ 次へ ] をクリックします。 例えば、次の値を設定します。

   * **名**: umspnego
   * **ユーザーログオン名**: spnegodemo

1. パスワードを入力します。 例えば、「*password*」というパスワードを設定します。「パスワードは無期限にする」が選択されていることを確認し、その他のオプションは選択しません。
1. 「次へ」をクリックし、「完了」をクリックします。

### サービスプリンシパル名 (SPN) のマッピング {#map-a-service-principal-name-spn}

1. KtPass ユーティリティを入手します。 このユーティリティは、SPN を REALM にマッピングするために使用します。 KtPass ユーティリティは、Windows Server Tool Pack または Resource Kit の一部として入手できます。 ( 詳しくは、 [Windows Server 2003 Service Pack 1 サポートツール](https://support.microsoft.com/kb/892777).)
1. コマンドプロンプトで、次の引数を指定して `ktpass` を実行します。

   `ktpass -princ HTTP/`*host* `@`*REALM* `-mapuser`*user*

   例えば、次のようにテキストを入力します。

   `ktpass -princ HTTP/lcserver.um.lc.com@UM.LC.COM -mapuser spnegodemo`

   指定する必要がある値は、次のとおりです。

   **ホスト：** Formsサーバーの完全修飾名または一意の URL。 この例では、lcserver.um.lc.comに設定されています。

   **領域：** ドメインコントローラの Active Directory 領域です。 この例では、UM.LC.COMに設定されています。 領域は必ず大文字で入力してください。 Windows 2003 のレルムを決定するには、次の手順を実行します。

   * 「マイコンピューター」を右クリックし、「プロパティ」を選択します。
   * [ コンピュータ名 ] タブをクリックします。 「ドメイン名」の値が領域名です。

   **ユーザー：** 前のタスクで作成したユーザーアカウントのログイン名です。 この例では、spnegodemo に設定されています。

このエラーが発生した場合：

```shell
DsCrackNames returned 0x2 in the name entry for spnegodemo.
ktpass:failed getting target domain for specified user.
```

ユーザーをspnegodemo@um.lc.comに指定してみます。

```shell
ktpass -princ HTTP/lcserver.um.lc.com@UM.LC.COM -mapuser spnegodemo
```

### Kerberos 整合性チェックの失敗を防ぐ {#prevent-kerberos-integrity-check-failures}

1. ドメインコントローラで、[ スタート ] メニュー/[ 管理ツール ]/[Active Directory ユーザーとコンピュータ ] に移動します。 [ スタート ] メニューに [ 管理ツール ] が表示されていない場合は、Campaign コントロールパネルを使用します。
1. Users フォルダーをクリックして、ユーザーのリストを表示します。
1. 前のタスクで作成したユーザーアカウントを右クリックします。 この例では、ユーザーアカウントは `spnegodemo` です。
1. 「パスワードをリセット」をクリックします。
1. 前に入力したのと同じパスワードを入力し、確認します。 この例では、`password` に設定されています。
1. 「次回のログオン時にパスワードを変更する」を選択解除し、「OK」をクリックします。

### SPNEGO クライアントブラウザー設定の構成 {#configuring-spnego-client-browser-settings}

SPNEGO ベースの認証が機能するには、ユーザーアカウントを作成するドメインにクライアントコンピューターが属している必要があります。 また、SPNEGO ベースの認証を許可するようにクライアントブラウザーを設定する必要があります。 また、SPNEGO ベースの認証を必要とするサイトは、信頼できるサイトである必要があります。

https://lcserver:8080 などのコンピューター名を使用してサーバーにアクセスする場合、Internet Explorer での設定は不要です。ドット (「。」) を含まない URL を入力した場合、Internet Explorer はそのサイトをローカルイントラネットサイトとして扱います。 サイトの完全修飾名を使用している場合は、そのサイトを信頼できるサイトとして追加する必要があります。

**Internet Explorer 6.x の設定**

1. ツール/インターネットオプションに移動し、「セキュリティ」タブをクリックします。
1. 「ローカルイントラネット」アイコンをクリックし、「サイト」をクリックします。
1. 「詳細」をクリックし、「この Web サイトをゾーンに追加」ボックスに、Forms Server の URL を入力します。 例えば、`https://lcserver.um.lc.com`
1. すべてのダイアログボックスが閉じられるまで、[OK] をクリックします。
1. AEM Forms Server の URL にアクセスして、設定をテストします。 例えば、ブラウザーの URL ボックスに `https://lcserver.um.lc.com:8080/um/login?um_no_redirect=true` と入力します。

**Mozilla Firefox の設定**

1. ブラウザーの URL ボックスに `about:config` と入力します。

   about:config - Mozilla Firefox ダイアログボックスが表示されます。

1. 「フィルター」ボックスに、`negotiate`
1. 表示されたリストで、network.negotiate-auth.trusted-uri をダブルクリックし、環境に応じて、次のいずれかのコマンドを入力します。

   `.um.lc.com` - 末尾が um.lc.com のすべての URL を SPNEGO に対して許可するよう Firefox を設定します。先頭に必ずドット（「.」）を含めてください。

   `lcserver.um.lc.com` - 特定のサーバーだけに SPNEGO を許可するように Firefox が設定されます。この値をドット (「。」) で始めないでください。

1. アプリケーションにアクセスして、設定をテストします。 ターゲットアプリケーションのようこそページが表示されます。
