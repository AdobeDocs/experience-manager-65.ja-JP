---
title: ユーザーの管理
seo-title: ユーザーの管理
description: User Management APIを使用して、役割、権限、プリンシパル（ユーザーまたはグループ）を管理し、ユーザーを認証できるクライアントアプリケーションを作成します。
seo-description: User Management APIを使用して、役割、権限、プリンシパル（ユーザーまたはグループ）を管理し、ユーザーを認証できるクライアントアプリケーションを作成します。
uuid: 68d8a0bc-6e3d-4286-ba5c-534dcf58cb84
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 95804bff-9e6f-4807-aae4-790bd9e7cb57
role: Developer
exl-id: d7c5bb84-a988-4b2e-a587-f4e5b50fea58
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '6257'
ht-degree: 4%

---

# ユーザーの管理{#managing-users}

**このドキュメントのサンプルと例は、JEE上のAEM Forms環境に限られています。**

**User Managementについて**

User Management APIを使用して、役割、権限、プリンシパル（ユーザーまたはグループ）を管理し、ユーザーを認証できるクライアントアプリケーションを作成できます。 User Management APIは、次のAEM Forms APIで構成されています。

* ディレクトリマネージャーサービスAPI
* Authentication ManagerサービスAPI
* Authorization ManagerサービスAPI

User Managementでは、役割と権限の割り当て、削除および決定が可能です。 また、ドメイン、ユーザー、グループの割り当て、削除、照会も可能です。 最後に、User Managementを使用してユーザーを認証できます。

[ユーザー](users.md#adding-users)の追加では、プログラムによるユーザーの追加方法を理解します。 この節では、ディレクトリマネージャーサービスAPIを使用します。

[ユーザーの削除](users.md#deleting-users)では、プログラムによるユーザーの削除方法を理解します。 この節では、ディレクトリマネージャーサービスAPIを使用します。

[ユーザーとグループの管理](users.md#managing-users-and-groups)では、ローカルユーザーとディレクトリユーザーの違いを理解し、JavaとWebサービスAPIを使用してユーザーとグループをプログラムで管理する方法の例を示します。 この節では、ディレクトリマネージャーサービスAPIを使用します。

[役割と権限の管理](users.md#managing-roles-and-permissions)では、システムの役割と権限、およびそれらを拡張するためにプログラムで実行できる操作について学び、JavaおよびWebサービスAPIを使用して役割と権限をプログラムで管理する方法の例を示します。 この節では、Directory Manager Service APIとAuthorization Manager Service APIの両方を使用します。

[ユーザーの認証](users.md#authenticating-users)では、JavaおよびWebサービスAPIを使用してユーザーをプログラムで認証する方法の例を示します。 この節では、Authorization ManagerサービスAPIを使用します。

**認証プロセスについて**

User Managementには、組み込みの認証機能が備わっており、独自の認証プロバイダーに接続する機能も備わっています。 User Managementは、認証要求を受け取ると（例えば、ユーザーがログインを試みると）、ユーザー情報を認証プロバイダーに渡して認証します。 User Managementは、ユーザーの認証後に認証プロバイダーから結果を受け取ります。

次の図は、ログインを試みるエンドユーザー、User Management、認証プロバイダー間のやり取りを示しています。

![mu_mu_umauth_process](assets/mu_mu_umauth_process.png)

次の表に、認証プロセスの各手順を示します。

<table>
 <thead>
  <tr>
   <th><p>ステップ</p></th>
   <th><p>説明</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>ユーザーが、User Managementを呼び出すサービスにログインしようとします。 ユーザは、ユーザ名とパスワードを指定する。 </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>User Managementは、ユーザー名とパスワード、および設定情報を認証プロバイダーに送信します。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>認証プロバイダは、ユーザストアに接続し、ユーザを認証する。</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>認証プロバイダーは、結果をUser Managementに返します。</p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>User Managementは、ユーザーに対し、製品へのアクセスをログインまたは拒否します。</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>サーバーのタイムゾーンがクライアントのタイムゾーンと異なる場合、WebSphere Application Serverクラスター上の.NETクライアントを使用して、ネイティブSOAPスタック上でAEM Forms Generate PDFサービスのWSDLを使用すると、次のUser Management認証エラーが発生する可能性があります。

`[com.adobe.idp.um.webservices.WSSecurityHandler] errorCode:12803 errorCodeHEX:0x3203 message:WSSecurityHandler: UM authenticate returns exception : An error was discovered processing the <wsse:Security> header. (WSSecurityEngine: Invalid timestamp The security semantics of message have expired).`

**ディレクトリ管理について**

User Managementは、LDAPディレクトリへの接続をサポートするディレクトリサービスプロバイダー(DirectoryManagerService)でパッケージ化されています。 組織でLDAP以外のリポジトリを使用してユーザーレコードを保存する場合、リポジトリで使用する独自のディレクトリサービスプロバイダーを作成できます。

ディレクトリサービスプロバイダーは、User Managementの要求時にユーザーストアからレコードを取得します。 User Managementは、データベース内のユーザーレコードとグループレコードを定期的にキャッシュし、パフォーマンスを向上させます。

ディレクトリサービスプロバイダーを使用して、User Managementデータベースをユーザーストアと同期できます。 この手順では、すべてのユーザーディレクトリ情報と、すべてのユーザーレコードとグループレコードが最新の状態に保たれます。

また、 DirectoryManagerServiceはドメインを作成および管理する機能を提供します。 ドメインは、異なるユーザーベースを定義します。 ドメインの境界は、通常、組織の構造やユーザーストアの設定に従って定義されます。 User Managementドメインは、認証プロバイダーおよびディレクトリサービスプロバイダーが使用する設定を提供します。

User Managementが書き出す設定XMLでは、属性値`Domains`が設定されたルートノードに、User Management用に定義された各ドメインのXML要素が含まれます。 これらの各要素には、特定のサービスプロバイダーに関連付けられたドメインの側面を定義する他の要素が含まれます。

**objectSIDの値について**

Active Directoryを使用する場合、`objectSID`値は複数のドメイン間で一意の属性ではないことを理解することが重要です。 この値は、オブジェクトのセキュリティ識別子を格納します。 複数のドメイン環境（例えば、ドメインのツリー）では、`objectSID`の値が異なる場合があります。

`objectSID`の値は、あるActive Directoryドメインから別のドメインにオブジェクトが移動された場合に変更されます。 一部のオブジェクトは、ドメイン内の任意の場所に同じ`objectSID`値を持ちます。 例えば、BUILTIN\Administrators、BUILTIN\Power Usersなどのグループは、ドメインに関係なく同じ`objectSID`値を持ちます。 これらの`objectSID`値はよく知られています。

## ユーザー{#adding-users}の追加

Directory Manager Service API（JavaおよびWebサービス）を使用して、ユーザーをAEM Formsにプログラムで追加できます。 ユーザーを追加した後は、ユーザーを必要とするサービス操作を実行する際に、そのユーザーを使用できます。 例えば、新しいユーザーにタスクを割り当てることができます。

### 手順の概要{#summary-of-steps}

ユーザーを追加するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. DirectoryManagerServiceクライアントを作成します。
1. ユーザー情報を定義します。
1. ユーザーをAEM Formsに追加します。
1. ユーザーが追加されていることを確認します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを含めます。

**DirectoryManagerServiceクライアントの作成**

プログラムによってDirectory Managerサービス操作を実行する前に、Directory Manager Service APIクライアントを作成します。

**ユーザー情報の定義**

Directory ManagerサービスAPIを使用して新しいユーザーを追加する場合は、そのユーザーの情報を定義します。 通常、新しいユーザーを追加する場合、次の値を定義します。

* **ドメイン名**:ユーザーが属するドメイン(例： `DefaultDom`)。
* **ユーザー識別子の値**:ユーザーの識別子の値(例： `wblue`)。
* **プリンシパルタイプ**:ユーザーのタイプ(例えば、を指定できま `USER)`す)。
* **名**:ユーザーの特定の名前(例： `Wendy`)。
* **姓**:ユーザーの姓(例：  `Blue)`)。
* **ロケール**:ユーザーのロケール情報。

**AEM Formsへのユーザーの追加**

ユーザー情報を定義したら、そのユーザーをAEM Formsに追加できます。 ユーザーを追加するには、`DirectoryManagerServiceClient`オブジェクトの`createLocalUser`メソッドを呼び出します。

**ユーザーが追加されたことを確認します。**

ユーザーが追加されたことを確認して、問題が発生していないことを確認できます。 ユーザー識別子の値を使用して、新しいユーザーを見つけます。

**関連トピック**

[Java APIを使用したユーザーの追加](users.md#add-users-using-the-java-api)

[WebサービスAPIを使用したユーザーの追加](users.md#add-users-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[ユーザーの削除](users.md#deleting-users)

### Java APIを使用したユーザーの追加{#add-users-using-the-java-api}

Directory Manager Service API(Java)を使用してユーザーを追加します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-usermanager-client.jarなどのクライアントJARファイルを含めます。

1. DirectoryManagerServicesクライアントを作成します。

   コンストラクターを使用し、接続プロパティを含む`ServiceClientFactory`オブジェクトを渡して、`DirectoryManagerServiceClient`オブジェクトを作成します。

1. ユーザー情報を定義します。

   * コンストラクタを使用して `UserImpl` オブジェクトを作成します。
   * `UserImpl`オブジェクトの`setDomainName`メソッドを呼び出して、デメイン名を設定します。 ドメイン名を指定するstring値を渡します。
   * `UserImpl`オブジェクトの`setPrincipalType`メソッドを呼び出して、プリンシパルタイプを設定します。 ユーザーのタイプを指定するstring値を渡します。 例えば、`USER`を指定できます。
   * `UserImpl`オブジェクトの`setUserid`メソッドを呼び出して、ユーザー識別子の値を設定します。 ユーザー識別子の値を指定するstring値を渡します。 例えば、`wblue`を指定できます。
   * `UserImpl`オブジェクトの`setCanonicalName`メソッドを呼び出して、正規名を設定します。 ユーザーの正規名を指定するstring値を渡します。 例えば、`wblue`を指定できます。
   * `UserImpl`オブジェクトの`setGivenName`メソッドを呼び出して、指定された名前を設定します。 ユーザーの名前を指定するstring値を渡します。 例えば、`Wendy`を指定できます。
   * `UserImpl`オブジェクトの`setFamilyName`メソッドを呼び出して、ファミリ名を設定します。 ユーザーの姓を指定するstring値を渡します。 例えば、`Blue`を指定できます。

   >[!NOTE]
   >
   >`UserImpl`オブジェクトに属するメソッドを呼び出して、他の値を設定します。 例えば、 `UserImpl`オブジェクトの`setLocale`メソッドを呼び出してロケール値を設定できます。

1. ユーザーをAEM Formsに追加します。

   `DirectoryManagerServiceClient`オブジェクトの`createLocalUser`メソッドを呼び出し、次の値を渡します。

   * 新しいユーザーを表す`UserImpl`オブジェクト
   * ユーザーのパスワードを表すstring値です

   `createLocalUser`メソッドは、ローカルユーザー識別子の値を指定する文字列値を返します。

1. ユーザーが追加されたことを確認します。

   * コンストラクタを使用して `PrincipalSearchFilter` オブジェクトを作成します。
   * `PrincipalSearchFilter`オブジェクトの`setUserId`メソッドを呼び出して、ユーザー識別子の値を設定します。 ユーザー識別子の値を表すstring値を渡します。
   * `DirectoryManagerServiceClient`オブジェクトの`findPrincipals`メソッドを呼び出して、`PrincipalSearchFilter`オブジェクトを渡します。 このメソッドは、`java.util.List`インスタンスを返します。各要素は`User`オブジェクトです。 `java.util.List`インスタンスを繰り返し処理して、ユーザーを見つけます。

**関連トピック**

[手順の概要](users.md#summary-of-steps)

[クイックスタート（SOAPモード）:Java APIを使用したユーザーの追加](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-adding-users-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#add-users-using-the-web-service-api}を使用してユーザーを追加する

Directory Manager Service API（Webサービス）を使用してユーザーを追加します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 サービス参照に次のWSDL定義を使用していることを確認してください。`http://localhost:8080/soap/services/DirectoryManagerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. DirectoryManagerServiceクライアントを作成します。

   * デフォルトのコンストラクターを使用して`DirectoryManagerServiceClient`オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`DirectoryManagerServiceClient.Endpoint.Address`オブジェクトを作成します。 AEM FormsサービスにWSDLを指定するstring値を渡します（例：`http://localhost:8080/soap/services/DirectoryManagerService?blob=mtom`）。 `lc_version`属性を使用する必要はありません。 この属性は、サービス参照を作成する際に使用されます。 必ず`?blob=mtom`を指定してください。
   * `DirectoryManagerServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値は、MTOMが使用されるようにします。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールド`DirectoryManagerServiceClient.ClientCredentials.UserName.UserName`にAEM formsユーザー名を割り当てます。
      * 対応するパスワード値をフィールド`DirectoryManagerServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * フィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に定数値`HttpClientCredentialType.Basic`を割り当てます。
      * フィールド`BasicHttpBindingSecurity.Security.Mode`に定数値`BasicHttpSecurityMode.TransportCredentialOnly`を割り当てます。

1. ユーザー情報を定義します。

   * コンストラクタを使用して `UserImpl` オブジェクトを作成します。
   * `UserImpl`オブジェクトの`domainName`フィールドに文字列値を割り当てて、デメイン名を設定します。
   * `UserImpl`オブジェクトの`principalType`フィールドに文字列値を割り当てて、プリンシパルタイプを設定します。 例えば、`USER`を指定できます。
   * `UserImpl`オブジェクトの`userid`フィールドに文字列値を割り当てて、ユーザー識別子の値を設定します。
   * `UserImpl`オブジェクトの`canonicalName`フィールドに文字列値を割り当てて、正規名の値を設定します。
   * `UserImpl`オブジェクトの`givenName`フィールドに文字列値を割り当てて、指定された名前値を設定します。
   * `UserImpl`オブジェクトの`familyName`フィールドに文字列値を割り当てて、ファミリ名の値を設定します。

1. ユーザーをAEM Formsに追加します。

   `DirectoryManagerServiceClient`オブジェクトの`createLocalUser`メソッドを呼び出し、次の値を渡します。

   * 新しいユーザーを表す`UserImpl`オブジェクト
   * ユーザーのパスワードを表すstring値です

   `createLocalUser`メソッドは、ローカルユーザー識別子の値を指定する文字列値を返します。

1. ユーザーが追加されたことを確認します。

   * コンストラクタを使用して `PrincipalSearchFilter` オブジェクトを作成します。
   * ユーザーのユーザー識別子の値を設定するには、ユーザー識別子の値を表す文字列値を`PrincipalSearchFilter`オブジェクトの`userId`フィールドに割り当てます。
   * `DirectoryManagerServiceClient`オブジェクトの`findPrincipals`メソッドを呼び出して、`PrincipalSearchFilter`オブジェクトを渡します。 このメソッドは、`MyArrayOfUser`コレクションオブジェクトを返します。各要素は`User`オブジェクトです。 `MyArrayOfUser`コレクションを繰り返し処理して、ユーザーを見つけます。

**関連トピック**

[手順の概要](users.md#summary-of-steps)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## ユーザーの削除{#deleting-users}

Directory Manager Service API（JavaおよびWebサービス）を使用して、AEM Formsからユーザーをプログラムで削除できます。 ユーザーを削除すると、そのユーザーは、ユーザーを必要とするサービス操作を実行できなくなります。 例えば、削除されたユーザーにタスクを割り当てることはできません。

### 手順の概要{#summary_of_steps-1}

ユーザーを削除するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. DirectoryManagerServiceクライアントを作成します。
1. 削除するユーザーを指定します。
1. AEM Formsからユーザーを削除します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを含めます。

**DirectoryManagerServiceクライアントの作成**

Directory Manager Service API操作をプログラムで実行する前に、Directory Managerサービスクライアントを作成します。

**削除するユーザーの指定**

ユーザーの識別子の値を使用して、削除するユーザーを指定できます。

**AEM Formsからのユーザーの削除**

ユーザーを削除するには、`DirectoryManagerServiceClient`オブジェクトの`deleteLocalUser`メソッドを呼び出します。

**関連トピック**

[Java APIを使用したユーザーの削除](users.md#delete-users-using-the-java-api)

[WebサービスAPIを使用したユーザーの削除](users.md#delete-users-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[ユーザーの追加](users.md#adding-users)

### Java APIを使用したユーザーの削除{#delete-users-using-the-java-api}

Directory Manager Service API(Java)を使用してユーザーを削除します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-usermanager-client.jarなどのクライアントJARファイルを含めます。

1. DirectoryManagerServiceクライアントを作成します。

   コンストラクターを使用し、接続プロパティを含む`ServiceClientFactory`オブジェクトを渡して、`DirectoryManagerServiceClient`オブジェクトを作成します。

1. 削除するユーザーを指定します。

   * コンストラクタを使用して `PrincipalSearchFilter` オブジェクトを作成します。
   * `PrincipalSearchFilter`オブジェクトの`setUserId`メソッドを呼び出して、ユーザー識別子の値を設定します。 ユーザー識別子の値を表すstring値を渡します。
   * `DirectoryManagerServiceClient`オブジェクトの`findPrincipals`メソッドを呼び出して、`PrincipalSearchFilter`オブジェクトを渡します。 このメソッドは、`java.util.List`インスタンスを返します。各要素は`User`オブジェクトです。 `java.util.List`インスタンスを繰り返し処理して、削除するユーザーを見つけます。

1. AEM Formsからユーザーを削除します。

   `DirectoryManagerServiceClient`オブジェクトの`deleteLocalUser`メソッドを呼び出し、`User`オブジェクトの`oid`フィールドの値を渡します。 `User`オブジェクトの`getOid`メソッドを呼び出します。 `java.util.List`インスタンスから取得した`User`オブジェクトを使用します。

**関連トピック**

[手順の概要](users.md#summary-of-steps)

[クイックスタート（EJBモード）:Java APIを使用したユーザーの削除](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-deleting-users-using-the-java-api)

[クイックスタート（SOAPモード）:Java APIを使用したユーザーの削除](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-deleting-users-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#delete-users-using-the-web-service-api}を使用したユーザーの削除

Directory Manager Service API（Webサービス）を使用してユーザーを削除します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-usermanager-client.jarなどのクライアントJARファイルを含めます。

1. DirectoryManagerServiceクライアントを作成します。

   * デフォルトのコンストラクターを使用して`DirectoryManagerServiceClient`オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`DirectoryManagerServiceClient.Endpoint.Address`オブジェクトを作成します。 AEM FormsサービスにWSDLを指定するstring値を渡します（例：`http://localhost:8080/soap/services/DirectoryManagerService?blob=mtom`）。 `lc_version`属性を使用する必要はありません。 この属性は、サービス参照を作成する際に使用されます。 必ず`blob=mtom.`を指定してください
   * `DirectoryManagerServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値は、MTOMが使用されるようにします。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールド`DirectoryManagerServiceClient.ClientCredentials.UserName.UserName`にAEM formsユーザー名を割り当てます。
      * 対応するパスワード値をフィールド`DirectoryManagerServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * フィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に定数値`HttpClientCredentialType.Basic`を割り当てます。
      * フィールド`BasicHttpBindingSecurity.Security.Mode`に定数値`BasicHttpSecurityMode.TransportCredentialOnly`を割り当てます。

1. 削除するユーザーを指定します。

   * コンストラクタを使用して `PrincipalSearchFilter` オブジェクトを作成します。
   * `PrincipalSearchFilter`オブジェクトの`userId`フィールドに文字列値を割り当てて、ユーザー識別子の値を設定します。
   * `DirectoryManagerServiceClient`オブジェクトの`findPrincipals`メソッドを呼び出して、`PrincipalSearchFilter`オブジェクトを渡します。 このメソッドは、`MyArrayOfUser`コレクションオブジェクトを返します。各要素は`User`オブジェクトです。 `MyArrayOfUser`コレクションを繰り返し処理して、ユーザーを見つけます。 `MyArrayOfUser`コレクションオブジェクトから取得した`User`オブジェクトを使用して、ユーザーが削除されます。

1. AEM Formsからユーザーを削除します。

   `User`オブジェクトの`oid`フィールド値を`DirectoryManagerServiceClient`オブジェクトの`deleteLocalUser`メソッドに渡して、ユーザーを削除します。

**関連トピック**

[手順の概要](users.md#summary-of-steps)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## グループの作成 {#creating-groups}

Directory Manager Service API（JavaおよびWebサービス）を使用して、AEM Formsグループをプログラムで作成できます。 グループを作成した後、そのグループを使用して、グループを必要とするサービス操作を実行できます。 例えば、ユーザーを新しいグループに割り当てることができます。 （[ユーザーとグループの管理](users.md#managing-users-and-groups)を参照）。

### 手順の概要{#summary_of_steps-2}

グループを作成するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. DirectoryManagerServiceクライアントを作成します。
1. グループが存在しないことを確認します。
1. グループを作成します。
1. グループでアクションを実行します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(AEM FormsがJBossにデプロイされている場合に必須)
* jbossall-client.jar(AEM FormsがJBossにデプロイされている場合に必須)

これらのJARファイルの場所について詳しくは、「[AEM Forms Javaライブラリファイル](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を含める」を参照してください。

**DirectoryManagerServiceクライアントの作成**

プログラムによってDirectory Managerサービス操作を実行する前に、Directory Manager Service APIクライアントを作成します。

**グループが存在するかどうかを確認する**

グループを作成する場合は、そのグループが同じドメインに存在しないことを確認します。 つまり、2つのグループが同じドメイン内で同じ名前を持つことはできません。 このタスクを実行するには、検索を実行し、2つの値に基づいて検索結果をフィルタリングします。 プリンシパルタイプを`com.adobe.idp.um.api.infomodel.Principal.PRINCIPALTYPE_GROUP`に設定して、グループのみが返されるようにします。 また、ドメイン名を必ず指定してください。

**グループの作成**

グループがドメインに存在しないと判断したら、グループを作成し、次の属性を指定します。

* **共通名**:グループの名前。
* **ドメイン**:グループを追加するドメイン。
* **説明**:グループの説明。

**グループでのアクションの実行**

グループを作成した後、そのグループを使用してアクションを実行できます。 例えば、ユーザーをグループに追加できます。 ユーザーをグループに追加するには、ユーザーとグループの両方の一意の識別子の値を取得します。 これらの値を`addPrincipalToLocalGroup`メソッドに渡します。

**関連トピック**

[Java APIを使用したグループの作成](users.md#create-groups-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[ユーザーの追加](users.md#adding-users)

[ユーザーの削除](users.md#deleting-users)

### Java API {#create-groups-using-the-java-api}を使用したグループの作成

Directory ManagerサービスAPI(Java)を使用してグループを作成します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-usermanager-client.jarなどのクライアントJARファイルを含めます。

1. DirectoryManagerServiceクライアントを作成します。

   コンストラクターを使用し、接続プロパティを含む`ServiceClientFactory`オブジェクトを渡して、`DirectoryManagerServiceClient`オブジェクトを作成します。

1. グループが存在するかどうかを確認します。

   * コンストラクタを使用して `PrincipalSearchFilter` オブジェクトを作成します。
   * `PrincipalSearchFilter`オブジェクトの`setPrincipalType`オブジェクトを呼び出して、プリンシパルタイプを設定します。 値`com.adobe.idp.um.api.infomodel.Principal.PRINCIPALTYPE_GROUP`を渡します。
   * `PrincipalSearchFilter`オブジェクトの`setSpecificDomainName`オブジェクトを呼び出して、ドメインを設定します。 ドメイン名を指定するstring値を渡します。
   * グループを検索するには、`DirectoryManagerServiceClient`オブジェクトの`findPrincipals`メソッドを呼び出します（プリンシパルはグループにすることができます）。 プリンシパルタイプとドメイン名を指定する`PrincipalSearchFilter`オブジェクトを渡します。 このメソッドは、`java.util.List`インスタンスを返します。各要素は、`Group`インスタンスです。 各グループインスタンスは、`PrincipalSearchFilter`オブジェクトを使用して指定されたフィルターに準拠します。
   * `java.util.List`インスタンスを繰り返し処理します。 各要素について、グループ名を取得します。 グループ名が新しいグループ名と等しくないようにしてください。

1. グループを作成します。

   * グループが存在しない場合は、`Group`オブジェクトの`setCommonName`メソッドを呼び出し、グループ名を指定する文字列値を渡します。
   * `Group`オブジェクトの`setDescription`メソッドを呼び出し、グループの説明を指定する文字列値を渡します。
   * `Group`オブジェクトの`setDomainName`メソッドを呼び出し、ドメイン名を指定する文字列値を渡します。
   * `DirectoryManagerServiceClient`オブジェクトの`createLocalGroup`メソッドを呼び出して、`Group`インスタンスを渡します。

   `createLocalUser`メソッドは、ローカルユーザー識別子の値を指定する文字列値を返します。

1. グループでアクションを実行します。

   * コンストラクタを使用して `PrincipalSearchFilter` オブジェクトを作成します。
   * `PrincipalSearchFilter`オブジェクトの`setUserId`メソッドを呼び出して、ユーザー識別子の値を設定します。 ユーザー識別子の値を表すstring値を渡します。
   * `DirectoryManagerServiceClient`オブジェクトの`findPrincipals`メソッドを呼び出して、`PrincipalSearchFilter`オブジェクトを渡します。 このメソッドは、`java.util.List`インスタンスを返します。各要素は`User`オブジェクトです。 `java.util.List`インスタンスを繰り返し処理して、ユーザーを見つけます。
   * `DirectoryManagerServiceClient`オブジェクトの`addPrincipalToLocalGroup`メソッドを呼び出して、ユーザーをグループに追加します。 `User`オブジェクトの`getOid`メソッドの戻り値を渡します。 `Group`オブジェクトの`getOid`メソッドの戻り値を渡します（新しいグループを表す`Group`インスタンスを使用します）。

**関連トピック**

[手順の概要](users.md#summary-of-steps)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## ユーザーとグループの管理 {#managing-users-and-groups}

このトピックでは、 (Java)を使用して、ドメイン、ユーザー、グループの割り当て、削除、クエリをプログラムで実行する方法について説明します。

>[!NOTE]
>
>ドメインを設定する場合、グループとユーザーの一意の識別子を設定する必要があります。 選択する属性は、LDAP環境内で一意である必要があるだけでなく、不変である必要があり、ディレクトリ内では変更されません。 この属性は、単純な文字列データ型である必要もあります(Active Directory 2000/2003で現在許可されている唯一の例外は、バイナリ値である`"objectsid"`です)。 例えば、Novell eDirectory属性`"GUID"`は、単純な文字列データ型ではないので、機能しません。

* Active Directoryの場合は、`"objectsid"`を使用します。
* SunOneの場合は、`"nsuniqueid"`を使用します。

>[!NOTE]
>
>LDAPディレクトリの同期中に複数のローカルユーザーおよびグループを作成することは、サポートされていません。 この処理を試みると、エラーが発生します。

### 手順の概要{#summary_of_steps-3}

ユーザーとグループを管理するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. DirectoryManagerServiceクライアントを作成します。
1. 適切なユーザー操作またはグループ操作を呼び出します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用する場合は、プロキシファイルを必ず含めてください。

**DirectoryManagerServiceクライアントの作成**

Directory Managerサービス操作をプログラムで実行する前に、Directory Managerサービスクライアントを作成する必要があります。 Java APIを使用すると、`DirectoryManagerServiceClient`オブジェクトを作成してこれを実現できます。 WebサービスAPIを使用すると、`DirectoryManagerServiceService`オブジェクトを作成してこれを実現できます。

**適切なユーザー操作またはグループ操作を呼び出す**

サービスクライアントを作成したら、ユーザーまたはグループの管理操作を呼び出すことができます。 サービスクライアントでは、ドメイン、ユーザー、グループの割り当て、削除、およびクエリを実行できます。 ディレクトリプリンシパルまたはローカルプリンシパルをローカルグループに追加することは可能ですが、ローカルプリンシパルをディレクトリグループに追加することはできません。

**関連トピック**

[Java APIを使用したユーザーとグループの管理](users.md#managing-users-and-groups-using-the-java-api)

[WebサービスAPIを使用したユーザーとグループの管理](users.md#managing-users-and-groups-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[User Manager APIクイックスタート](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

### Java APIを使用したユーザーとグループの管理{#managing-users-and-groups-using-the-java-api}

(Java)を使用してユーザー、グループ、ドメインをプログラムで管理するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-usermanager-client.jarなどのクライアントJARファイルを含めます。 これらのファイルの場所については、[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。

1. DirectoryManagerServiceクライアントを作成します。

   コンストラクターを使用し、接続プロパティを含む`ServiceClientFactory`オブジェクトを渡して、`DirectoryManagerServiceClient`オブジェクトを作成します。 詳しくは、[接続プロパティの設定&#x200B;](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)*.*&#x200B;を参照してください。

1. 適切なユーザー操作またはグループ操作を呼び出します。

   ユーザーまたはグループを検索するには、`DirectoryManagerServiceClient`オブジェクトのメソッドの1つを呼び出してプリンシパルを検索します（プリンシパルはユーザーまたはグループになる可能性があるため）。 次の例では、`findPrincipals`メソッドは検索フィルター（`PrincipalSearchFilter`オブジェクト）を使用して呼び出されます。

   この場合の戻り値は`Principal`オブジェクトを含む`java.util.List`なので、結果を繰り返し処理し、`Principal`オブジェクトを`User`または`Group`オブジェクトにキャストします。

   結果の`User`または`Group`オブジェクト（両方とも`Principal`インターフェイスから継承）を使用して、ワークフローで必要な情報を取得します。 例えば、ドメイン名と正規名の値を組み合わせて、プリンシパルを一意に識別します。 これらは、 `Principal`オブジェクトの`getDomainName`メソッドと`getCanonicalName`メソッドをそれぞれ呼び出して取得されます。

   ローカルユーザーを削除するには、`DirectoryManagerServiceClient`オブジェクトの`deleteLocalUser`メソッドを呼び出して、ユーザーの識別子を渡します。

   ローカルグループを削除するには、`DirectoryManagerServiceClient`オブジェクトの`deleteLocalGroup`メソッドを呼び出して、グループの識別子を渡します。

**関連トピック**

[手順の概要](users.md#summary-of-steps)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#managing-users-and-groups-using-the-web-service-api}を使用したユーザーとグループの管理

Directory Manager Service API（Webサービス）を使用してユーザー、グループ、ドメインをプログラムで管理するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。

   * Directory Manager WSDLを使用するMicrosoft .NETクライアントアセンブリを作成します。 ([Base64エンコーディング](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)を使用したAEM Formsの呼び出しを参照)。
   * Microsoft .NETクライアントアセンブリを参照します。 （[Base64エンコード](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)を使用する.NETクライアントアセンブリの作成を参照）。

1. DirectoryManagerServiceクライアントを作成します。

   プロキシクラスのコンストラクターを使用して`DirectoryManagerServiceService`オブジェクトを作成します。

1. 適切なユーザー操作またはグループ操作を呼び出します。

   ユーザーまたはグループを検索するには、`DirectoryManagerServiceService`オブジェクトのメソッドの1つを呼び出してプリンシパルを検索します（プリンシパルはユーザーまたはグループになる可能性があるため）。 次の例では、`findPrincipalsWithFilter`メソッドは検索フィルター（`PrincipalSearchFilter`オブジェクト）を使用して呼び出されます。 `PrincipalSearchFilter`オブジェクトを使用する場合、ローカルプリンシパルは`isLocal`プロパティが`true`に設定されている場合にのみ返されます。 この動作は、Java APIでおこなわれる動作とは異なります。

   >[!NOTE]
   >
   >検索フィルターで検索結果の最大数が指定されていない場合（`PrincipalSearchFilter.resultsMax`フィールドを使用）、最大1,000件の結果が返されます。 これは、Java APIを使用して行われる動作とは異なります。Java APIの結果はデフォルトで10個です。 また、`findGroupMembers`などの検索方法では、検索フィルターで検索結果の最大数が指定されていない限り（例えば、`GroupMembershipSearchFilter.resultsMax`フィールドを使用して）結果が得られません。 これは、`GenericSearchFilter`クラスから継承するすべての検索フィルターに適用されます。 詳しくは、「[AEM Forms APIリファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)」を参照してください。

   この場合の戻り値は`Principal`オブジェクトを含む`object[]`なので、結果を繰り返し処理し、`Principal`オブジェクトを`User`または`Group`オブジェクトにキャストします。

   結果の`User`または`Group`オブジェクト（両方とも`Principal`インターフェイスから継承）を使用して、ワークフローで必要な情報を取得します。 例えば、ドメイン名と正規名の値を組み合わせて、プリンシパルを一意に識別します。 これらは、 `Principal`オブジェクトの`domainName`フィールドと`canonicalName`フィールドをそれぞれ呼び出して取得されます。

   ローカルユーザーを削除するには、`DirectoryManagerServiceService`オブジェクトの`deleteLocalUser`メソッドを呼び出して、ユーザーの識別子を渡します。

   ローカルグループを削除するには、`DirectoryManagerServiceService`オブジェクトの`deleteLocalGroup`メソッドを呼び出して、グループの識別子を渡します。

**関連トピック**

[手順の概要](users.md#summary-of-steps)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 役割と権限の管理{#managing-roles-and-permissions}

このトピックでは、Authorization Manager Service API(Java)を使用して、役割と権限をプログラムで割り当て、削除、決定する方法について説明します。

AEM Formsでは、*役割*&#x200B;は、1つ以上のシステムレベルリソースにアクセスするための権限のグループです。 これらの権限はユーザー管理を通じて作成され、サービスコンポーネントによって適用されます。 例えば、管理者は「ポリシーセット作成者」の役割をユーザーのグループに割り当てることができます。 Rights Managementは、その役割を持つグループのユーザーに、管理コンソールを使用してポリシーセットを作成することを許可します。

役割には、次の2つのタイプがあります。*デフォルトの役割*&#x200B;と&#x200B;*カスタムの役割*。 デフォルトの役割（*システムの役割）*&#x200B;は、既にAEM Formsに存在します。 デフォルトの役割は、管理者が削除または変更できない場合があり、変更できないと想定されます。 このため、管理者が作成したカスタムロールは、その後変更または削除できます。

役割を使用すると、権限の管理が容易になります。 役割がプリンシパルに割り当てられると、一連の権限が自動的にそのプリンシパルに割り当てられ、プリンシパルに関する特定のアクセス関連の決定はすべて、割り当てられた権限の全体セットに基づきます。

### 手順の概要{#summary_of_steps-4}

役割と権限を管理するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. AuthorizationManagerServiceクライアントを作成します。
1. 適切な役割または権限操作を呼び出します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用する場合は、プロキシファイルを必ず含めてください。

**AuthorizationManagerServiceクライアントの作成**

User Management AuthorizationManagerService操作をプログラムで実行する前に、AuthorizationManagerServiceクライアントを作成する必要があります。 Java APIを使用すると、`AuthorizationManagerServiceClient`オブジェクトを作成してこれを実現できます。

**適切なロールまたは権限操作を呼び出す**

サービスクライアントを作成したら、ロール操作または権限操作を呼び出すことができます。 サービスクライアントでは、役割と権限の割り当て、削除、決定をおこなうことができます。

**関連トピック**

[Java APIを使用した役割と権限の管理](users.md#managing-roles-and-permissions-using-the-java-api)

[WebサービスAPIを使用した役割と権限の管理](users.md#managing-roles-and-permissions-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[User Manager APIクイックスタート](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

### Java API {#managing-roles-and-permissions-using-the-java-api}を使用した役割と権限の管理

Authorization ManagerサービスAPI(Java)を使用して役割と権限を管理するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-usermanager-client.jarなどのクライアントJARファイルを含めます。

1. AuthorizationManagerServiceクライアントを作成します。

   コンストラクターを使用し、接続プロパティを含む`ServiceClientFactory`オブジェクトを渡して、`AuthorizationManagerServiceClient`オブジェクトを作成します。

1. 適切な役割または権限操作を呼び出します。

   プリンシパルにロールを割り当てるには、`AuthorizationManagerServiceClient`オブジェクトの`assignRole`メソッドを呼び出し、次の値を渡します。

   * ロール識別子を含む`java.lang.String`オブジェクト
   * 主識別子を含む`java.lang.String`オブジェクトの配列。

   プリンシパルからロールを削除するには、`AuthorizationManagerServiceClient`オブジェクトの`unassignRole`メソッドを呼び出し、次の値を渡します。

   * ロール識別子を含む`java.lang.String`オブジェクト。
   * 主識別子を含む`java.lang.String`オブジェクトの配列。


**関連トピック**

[手順の概要](users.md#summary-of-steps)

[クイックスタート（SOAPモード）:Java APIを使用した役割と権限の管理](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-managing-roles-and-permissions-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#managing-roles-and-permissions-using-the-web-service-api}を使用した役割と権限の管理

承認マネージャーサービスAPI（Webサービス）を使用して、役割と権限を管理します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/AuthorizationManagerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. AuthorizationManagerServiceクライアントを作成します。

   * デフォルトのコンストラクターを使用して`AuthorizationManagerServiceClient`オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`AuthorizationManagerServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに渡す文字列値（例：`http://localhost:8080/soap/services/AuthorizationManagerService?blob=mtom`）を渡します。 `lc_version`属性を使用する必要はありません。 この属性は、サービス参照を作成する際に使用されます。
   * `AuthorizationManagerServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値は、MTOMが使用されるようにします。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールド`AuthorizationManagerServiceClient.ClientCredentials.UserName.UserName`にAEM formsユーザー名を割り当てます。
      * 対応するパスワード値をフィールド`AuthorizationManagerServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * フィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に定数値`HttpClientCredentialType.Basic`を割り当てます。
      * フィールド`BasicHttpBindingSecurity.Security.Mode`に定数値`BasicHttpSecurityMode.TransportCredentialOnly`を割り当てます。

1. 適切な役割または権限操作を呼び出します。

   プリンシパルにロールを割り当てるには、`AuthorizationManagerServiceClient`オブジェクトの`assignRole`メソッドを呼び出し、次の値を渡します。

   * ロール識別子を含む`string`オブジェクト
   * 主識別子を含む`MyArrayOf_xsd_string`オブジェクト。

   プリンシパルからロールを削除するには、`AuthorizationManagerServiceService`オブジェクトの`unassignRole`メソッドを呼び出し、次の値を渡します。

   * ロール識別子を含む`string`オブジェクト。
   * 主識別子を含む`string`オブジェクトの配列。


**関連トピック**

[手順の概要](users.md#summary-of-steps)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## ユーザーの認証{#authenticating-users}

このトピックでは、Authentication Manager Service API(Java)を使用して、クライアント・アプリケーションがユーザーをプログラムで認証する方法について説明します。

ユーザー認証は、安全なデータを格納するエンタープライズデータベースやその他のエンタープライズリポジトリとのやり取りに必要な場合があります。

例えば、ユーザーがWebページにユーザー名とパスワードを入力し、FormsをホストするJ2EEアプリケーションサーバーに値を送信するシナリオを考えてみます。 Formsのカスタムアプリケーションは、Authentication Managerサービスを使用してユーザーを認証できます。

認証が成功した場合、アプリケーションは保護されたエンタープライズデータベースにアクセスします。 それ以外の場合は、ユーザが許可されたユーザでないことを示すメッセージがユーザに送信される。

次の図に、アプリケーションのロジック・フローを示します。

![au_au_umauth_process](assets/au_au_umauth_process.png)

次の表に、この図の手順を示します

<table>
 <thead>
  <tr>
   <th><p>ステップ</p></th>
   <th><p>説明</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>ユーザは、Wfcサイトにアクセスし、ユーザ名とパスワードを指定する。 この情報は、AEM FormsをホストするJ2EEアプリケーションサーバーに送信されます。</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>ユーザー資格情報はAuthentication Managerサービスで認証されます。 ユーザーの資格情報が有効な場合、ワークフローは手順3に進みます。 それ以外の場合は、ユーザが許可されたユーザでないことを示すメッセージがユーザに送信される。</p></td>
  </tr>
  <tr>
   <td><p>1</p></td>
   <td><p>ユーザー情報とフォームデザインは、セキュリティで保護されたエンタープライズデータベースから取得される。 </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>ユーザー情報がフォームデザインとマージされ、フォームがユーザーにレンダリングされます。 </p></td>
  </tr>
 </tbody>
</table>

### 手順の概要{#summary_of_steps-5}

プログラムによってユーザーを認証するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. AuthenticationManagerServiceクライアントを作成します。
1. 認証操作を呼び出します。
1. 必要に応じて、コンテキストを取得し、クライアントアプリケーションが認証用に別のAEM Formsサービスに転送できるようにします。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用する場合は、プロキシファイルを必ず含めてください。

**AuthenticationManagerServiceクライアントの作成**

プログラムによるユーザーの認証を行う前に、AuthenticationManagerServiceクライアントを作成する必要があります。 Java APIを使用する場合は、`AuthenticationManagerServiceClient`オブジェクトを作成します。

**認証操作を呼び出す**

サービスクライアントを作成したら、認証操作を呼び出すことができます。 この操作には、ユーザーの名前やパスワードなど、ユーザーに関する情報が必要です。 ユーザーが認証されない場合は、例外が発生します。

**認証コンテキストの取得**

ユーザーを認証したら、認証済みユーザーに基づいてコンテキストを作成できます。 その後、コンテンツを使用して別のAEM Formsサービスを呼び出すことができます。 例えば、コンテキストを使用して`EncryptionServiceClient`を作成し、PDFドキュメントをパスワードで暗号化できます。 認証されたユーザーに、AEM Formsサービスを呼び出すために必要な`Services User`という役割があることを確認します。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[User Manager APIクイックスタート](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

[PDFドキュメントのパスワードによる暗号化](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Java API {#authenticate-a-user-using-the-java-api}を使用してユーザーを認証します

Authentication ManagerサービスAPI(Java)を使用してユーザーを認証します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-usermanager-client.jarなどのクライアントJARファイルを含めます。

1. AuthenticationManagerServicesクライアントを作成します。

   コンストラクターを使用し、接続プロパティを含む`ServiceClientFactory`オブジェクトを渡して、`AuthenticationManagerServiceClient`オブジェクトを作成します。

1. 認証操作を呼び出します。

   `AuthenticationManagerServiceClient`オブジェクトの`authenticate`メソッドを呼び出し、次の値を渡します。

   * ユーザー名を含む`java.lang.String`オブジェクト。
   * ユーザーのパスワードを含むバイト配列（`byte[]`オブジェクト）。 `byte[]`オブジェクトは、`java.lang.String`オブジェクトの`getBytes`メソッドを呼び出して取得できます。

   authenticateメソッドは、`AuthResult`オブジェクトを返します。このオブジェクトには、認証済みユーザーに関する情報が含まれています。

1. 認証コンテキストを取得します。

   `ServiceClientFactory`オブジェクトの`getContext`メソッドを呼び出して、`Context`オブジェクトを返します。

   次に、`Context`オブジェクトの`initPrincipal`メソッドを呼び出し、`AuthResult`を渡します。

### WebサービスAPI {#authenticate-a-user-using-the-web-service-api}を使用してユーザーを認証します。

Authentication Manager Service API（Webサービス）を使用してユーザーを認証します。

1. プロジェクトファイルを含めます。

   * Authentication Manager WSDLを使用するMicrosoft .NETクライアント・アセンブリを作成します。 ([Base64エンコーディング](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)を使用したAEM Formsの呼び出しを参照)。
   * Microsoft .NETクライアントアセンブリを参照します。 ([Base64エンコード](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)を使用したAEM Formsの呼び出しの「.NETクライアントアセンブリの参照」を参照)。

1. AuthenticationManagerServiceクライアントを作成します。

   プロキシクラスのコンストラクターを使用して`AuthenticationManagerServiceService`オブジェクトを作成します。

1. 認証操作を呼び出します。

   `AuthenticationManagerServiceClient`オブジェクトの`authenticate`メソッドを呼び出し、次の値を渡します。

   * ユーザー名を含む`string`オブジェクト
   * ユーザーのパスワードを含むバイト配列（`byte[]`オブジェクト）。 次の例に示すロジックを使用して、パスワードを含む`string`オブジェクトを`byte[]`配列に変換することで、`byte[]`オブジェクトを取得できます。
   * 返される値は`AuthResult`オブジェクトで、ユーザーに関する情報を取得するために使用できます。 次の例では、ユーザーの情報を取得するために、まず`AuthResult`オブジェクトの`authenticatedUser`フィールドを取得し、次に結果の`User`オブジェクトの`canonicalName`フィールドと`domainName`フィールドを取得します。

**関連トピック**

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## プログラムによるユーザーの同期{#programmatically-synchronizing-users}

User Management APIを使用して、プログラムでユーザーを同期できます。 ユーザーを同期する際、AEM Formsをユーザーリポジトリ内のユーザーデータに更新します。 例えば、新しいユーザーをユーザーリポジトリに追加するとします。 同期操作を実行すると、新しいユーザーがAEM formsユーザーになります。 また、ユーザーリポジトリに存在しないユーザーはAEM Formsから削除されます。

次の図に、AEM Formsとユーザーリポジトリの同期を示します。

![ps_ps_umauth_sync](assets/ps_ps_umauth_sync.png)

次の表に、この図の手順を示します

<table>
 <thead>
  <tr>
   <th><p>ステップ</p></th>
   <th><p>説明</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>クライアントアプリケーションは、AEM Formsが同期操作を実行するように要求します。</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>AEM Formsは同期操作を実行します。</p></td>
  </tr>
  <tr>
   <td><p>1</p></td>
   <td><p>ユーザー情報が更新されました。</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>ユーザは、更新されたユーザ情報を見ることができる。 </p></td>
  </tr>
 </tbody>
</table>

### 手順の概要{#summary_of_steps-6}

プログラムによってユーザーを同期するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. UserManagerUtilServiceClientクライアントを作成します。
1. エンタープライズドメインを指定します。
1. 認証操作を呼び出します。
1. 同期操作が完了したかどうかを確認する

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用する場合は、プロキシファイルを必ず含めてください。

**UserManagerUtilServiceClientclientの作成**

プログラムによってユーザーを同期する前に、`UserManagerUtilServiceClient`オブジェクトを作成する必要があります。

**エンタープライズドメインの指定**

User Management APIを使用して同期操作を実行する前に、ユーザーが属するエンタープライズドメインを指定します。 1つまたは複数のエンタープライズドメインを指定できます。 プログラムによって同期操作を実行する前に、管理コンソールを使用してエンタープライズドメインを設定する必要があります。 （[管理ヘルプ](https://www.adobe.com/go/learn_aemforms_admin_63)を参照）。

**同期操作の呼び出し**

1つ以上のエンタープライズドメインを指定した後、同期操作を実行できます。 この操作の実行に要する時間は、ユーザーリポジトリ内にあるユーザーレコードの数によって異なります。

**同期操作が完了したかどうかを確認する**

プログラムで同期操作を実行した後、操作が完了したかどうかを判断できます。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[User Manager APIクイックスタート](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

[PDFドキュメントのパスワードによる暗号化](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Java API {#programmatically-synchronizing-users-using-the-java-api}を使用したプログラムによるユーザーの同期

User Management API(Java)を使用してユーザーを同期します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-usermanager-client.jarやadobe-usermanager-util-client.jarなどのクライアントJARファイルを含めます。

1. UserManagerUtilServiceClientクライアントを作成します。

   コンストラクターを使用し、接続プロパティを含む`ServiceClientFactory`オブジェクトを渡して、`UserManagerUtilServiceClient`オブジェクトを作成します。

1. エンタープライズドメインを指定します。

   * `UserManagerUtilServiceClient`オブジェクトの`scheduleSynchronization`メソッドを呼び出して、ユーザー同期操作を開始します。
   * `HashSet`コンストラクターを使用して`java.util.Set`インスタンスを作成します。 必ず`String`をデータ型として指定してください。 この`Java.util.Set`インスタンスは、同期操作が適用されるドメイン名を保存します。
   * 追加するドメイン名ごとに、`java.util.Set`オブジェクトのaddメソッドを呼び出し、ドメイン名を渡します。

1. 同期操作を呼び出します。

   `ServiceClientFactory`オブジェクトの`getContext`メソッドを呼び出して、`Context`オブジェクトを返します。

   次に、`Context`オブジェクトの`initPrincipal`メソッドを呼び出し、`AuthResult`を渡します。

**関連トピック**

[プログラムによるユーザーの同期](users.md#programmatically-synchronizing-users)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
