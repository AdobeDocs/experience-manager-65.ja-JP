---
title: ユーザーの管理
seo-title: ユーザーの管理
description: User Management APIを使用して、ロール、権限、プリンシパル（ユーザーまたはグループ）を管理でき、ユーザーの認証を行えるクライアントアプリケーションを作成します。
seo-description: User Management APIを使用して、ロール、権限、プリンシパル（ユーザーまたはグループ）を管理でき、ユーザーの認証を行えるクライアントアプリケーションを作成します。
uuid: 68d8a0bc-6e3d-4286-ba5c-534dcf58cb84
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 95804bff-9e6f-4807-aae4-790bd9e7cb57
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '6243'
ht-degree: 4%

---


# ユーザーの管理{#managing-users}

**User Managementについて**

User Management APIを使用して、ロール、権限、プリンシパル（ユーザーまたはグループ）を管理でき、ユーザーを認証できるクライアントアプリケーションを作成できます。 User Management APIは、次のAEM FormsAPIで構成されています。

* Directory Manager Service API
* Authentication ManagerサービスAPI
* 承認マネージャーサービスAPI

User Managementでは、ロールと権限の割り当て、削除、決定を行うことができます。 また、ドメイン、ユーザー、グループの割り当て、削除、クエリも可能です。 最後に、User Managementを使用してユーザーを認証できます。

[ユーザーの追加](users.md#adding-users)では、プログラム的にユーザーを追加する方法を理解しています。 この節では、Directory Manager Service APIを使用します。

[ユーザーの削除](users.md#deleting-users)では、ユーザーをプログラム的に削除する方法を理解しています。 この節では、Directory Manager Service APIを使用します。

[ユーザーとグループの管理](users.md#managing-users-and-groups)では、ローカルユーザーとディレクトリユーザーの違いを理解し、Java APIとWebサービスAPIを使用してユーザーとグループをプログラム的に管理する方法の例を紹介しています。 この節では、Directory Manager Service APIを使用します。

[役割と権限の管理](users.md#managing-roles-and-permissions)では、システムの役割と権限、およびそれらをプログラム的に拡張する方法について学び、JavaおよびWebサービスAPIを使用して役割と権限をプログラム的に管理する方法の例を示します。 このセクションでは、Directory Manager Service APIとAuthorization Manager Service APIの両方を使用します。

[ユーザーの認証](users.md#authenticating-users)には、Java APIとWebサービスAPIを使用してユーザーをプログラム的に認証する方法の例が示されています。 この節では、承認マネージャーサービスAPIを使用します。

**認証プロセスについて**

User Managementには組み込みの認証機能があり、独自の認証プロバイダーとの接続機能も備わっています。 User Managementは、認証要求を受け取る（例えば、ユーザーがログインを試行する）と、認証のためにユーザー情報を認証プロバイダーに渡します。 User Managementは、ユーザーの認証後、認証プロバイダーから結果を受け取ります。

次の図に、ログインを試みたエンドユーザー、User Management、認証プロバイダー間でのやり取りを示します。

![mu_mu_umuuth_process](assets/mu_mu_umauth_process.png)

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
   <td><p>ユーザーがUser Managementを呼び出すサービスにログインしようとします。 ユーザは、ユーザ名とパスワードを指定する。 </p></td>
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
   <td><p>User Managementでは、ユーザーが製品へのログインを許可するか、製品へのアクセスを拒否します。</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>サーバーのタイムゾーンがクライアントのタイムゾーンと異なる場合、WebSphere Application Serverクラスター上の.NETクライアントを使用してネイティブSOAPスタック上のAEM FormsGenerate PDFサービス用のWSDLを使用すると、次のUser Management認証エラーが発生する可能性があります。

`[com.adobe.idp.um.webservices.WSSecurityHandler] errorCode:12803 errorCodeHEX:0x3203 message:WSSecurityHandler: UM authenticate returns exception : An error was discovered processing the <wsse:Security> header. (WSSecurityEngine: Invalid timestamp The security semantics of message have expired).`

**ディレクトリ管理について**

User Managementは、LDAPディレクトリへの接続をサポートするディレクトリサービスプロバイダー(DirectoryManagerService)と共にパッケージ化されています。 組織でLDAP以外のリポジトリを使用してユーザーレコードを保存する場合は、リポジトリで機能する独自のディレクトリサービスプロバイダーを作成できます。

ディレクトリサービスプロバイダーは、User Managementの要求時にユーザーストアからレコードを取得します。 User Managementは、ユーザーレコードとグループレコードを定期的にデータベースにキャッシュし、パフォーマンスを向上させます。

ディレクトリサービスプロバイダーを使用して、User Managementデータベースをユーザーストアと同期できます。 この手順では、すべてのユーザーディレクトリ情報と、すべてのユーザーレコードおよびグループレコードが最新であることを確認します。

また、DirectoryManagerServiceでは、ドメインの作成と管理を行うことができます。 ドメインは、様々なユーザーベースを定義します。 ドメインの境界は、通常、組織の構造化方法やユーザーストアの設定方法に従って定義されます。 User Managementドメインには、認証プロバイダーやディレクトリサービスプロバイダーが使用する設定が用意されています。

User Managementがエクスポートする設定XMLでは、`Domains`の属性値を持つルートノードに、User Management用に定義された各ドメインのXML要素が含まれています。 これらの各要素には、特定のサービスプロバイダーに関連付けられたドメインの外観を定義する他の要素が含まれます。

**objectSID値について**

Active Directoryを使用する場合、`objectSID`値は複数のドメイン間で固有の属性ではないことを理解することが重要です。 この値には、オブジェクトのセキュリティ識別子が格納されます。 複数のドメイン環境（例えば、ドメインのツリー）では、`objectSID`の値が異なる場合があります。

`objectSID`の値は、あるActive Directoryドメインから別のドメインにオブジェクトを移動すると変更されます。 一部のオブジェクトは、ドメイン内のどこにも同じ`objectSID`値を持ちます。 例えば、BUILTIN\Administrators、BUILTIN\Power Usersなどのグループは、ドメインに関係なく同じ`objectSID`値を持ちます。 これらの`objectSID`値はよく知られています。

## ユーザーの追加{#adding-users}

Directory Manager Service API（JavaおよびWebサービス）を使用して、ユーザーをプログラム的にAEM Formsに追加できます。 ユーザーを追加した後、そのユーザーを、ユーザーを必要とするサービス操作の実行時に使用できます。 例えば、新しいユーザーにタスクを割り当てることができます。

### 手順{#summary-of-steps}の概要

ユーザーを追加するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. DirectoryManagerServiceクライアントを作成します。
1. ユーザー情報を定義します。
1. AEM Forms追加へのユーザー。
1. ユーザーが追加されていることを確認します。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを含めます。

**DirectoryManagerServiceクライアントの作成**

プログラムを使用してDirectory Managerサービスの操作を実行する前に、Directory Manager Service APIクライアントを作成します。

**ユーザー情報の定義**

Directory Manager Service APIを使用して新しいユーザーを追加する場合は、そのユーザーの情報を定義します。 通常、新しいユーザーを追加する場合は、次の値を定義します。

* **ドメイン名**:ユーザーが属するドメイン(例： `DefaultDom`)。
* **ユーザー識別子の値**:ユーザーの識別子の値(例： `wblue`)。
* **プリンシパルタイプ**:ユーザーのタイプ(例えば、指定でき `USER)`ます)。
* **名**:ユーザーの名前(例： `Wendy`)。
* **姓**:ユーザーの姓(例： `Blue)`)。
* **ロケール**:ユーザーのロケール情報。

**AEM Forms追加へのユーザー**

ユーザ情報を定義した後、そのユーザをAEM Formsに追加できます。 ユーザーを追加するには、`DirectoryManagerServiceClient`オブジェクトの`createLocalUser`メソッドを呼び出します。

**ユーザーが追加されたことを確認します**

ユーザーが追加されたことを確認して、問題が発生していないことを確認できます。 ユーザー識別子の値を使用して、新しいユーザーを見つけます。

**関連トピック**

[Java APIを追加使用するユーザー](users.md#add-users-using-the-java-api)

[webサービスAPI追加を使用するユーザー](users.md#add-users-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[ユーザーの削除](users.md#deleting-users)

### Java API &lt;a0/追加>を使用するユーザー{#add-users-using-the-java-api}

Directory Manager追加 Service API(Java)を使用したユーザー：

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
   * `UserImpl`オブジェクトの`setGivenName`メソッドを呼び出して、指定した名前を設定します。 ユーザーの名前を指定するstring値を渡します。 例えば、`Wendy`を指定できます。
   * `UserImpl`オブジェクトの`setFamilyName`メソッドを呼び出して、ファミリ名を設定します。 ユーザーの姓を指定するstring値を渡します。 例えば、`Blue`を指定できます。

   >[!NOTE]
   >
   >`UserImpl`オブジェクトに属するメソッドを呼び出して、他の値を設定します。 例えば、`UserImpl`オブジェクトの`setLocale`メソッドを呼び出してロケール値を設定できます。

1. AEM Forms追加へのユーザー。

   `DirectoryManagerServiceClient`オブジェクトの`createLocalUser`メソッドを呼び出し、次の値を渡します。

   * 新しいユーザーを表す`UserImpl`オブジェクト
   * ユーザーのパスワードを表すstring値です

   `createLocalUser`メソッドは、ローカルユーザー識別子の値を指定する文字列値を返します。

1. ユーザーが追加されたことを確認します。

   * コンストラクタを使用して `PrincipalSearchFilter` オブジェクトを作成します。
   * `PrincipalSearchFilter`オブジェクトの`setUserId`メソッドを呼び出して、ユーザー識別子の値を設定します。 ユーザー識別子の値を表すstring値を渡します。
   * `DirectoryManagerServiceClient`オブジェクトの`findPrincipals`メソッドを呼び出し、`PrincipalSearchFilter`オブジェクトを渡します。 このメソッドは、`java.util.List`インスタンスを返します。各要素は`User`オブジェクトです。 `java.util.List`インスタンスを繰り返し実行し、ユーザーを探します。

**関連トピック**

[手順の概要](users.md#summary-of-steps)

[クイック開始（SOAPモード）:Java APIを使用したユーザの追加](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-adding-users-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### webサービスAPI &lt;a0/追加>を使用するユーザー{#add-users-using-the-web-service-api}

Directory Manager Service API（Webサービス）追加を使用したユーザー：

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 サービス参照に次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/DirectoryManagerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. DirectoryManagerServiceクライアントを作成します。

   * `DirectoryManagerServiceClient`オブジェクトを作成するには、そのデフォルトのコンストラクタを使用します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`DirectoryManagerServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに指定するstring値を渡します（例：`http://localhost:8080/soap/services/DirectoryManagerService?blob=mtom`）。 `lc_version`属性を使用する必要はありません。 この属性は、サービス参照を作成する際に使用されます。 `?blob=mtom`を必ず指定してください。
   * `DirectoryManagerServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * AEM formsユーザー名をフィールド`DirectoryManagerServiceClient.ClientCredentials.UserName.UserName`に割り当てます。
      * 対応するパスワード値をフィールド`DirectoryManagerServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * 定数値`HttpClientCredentialType.Basic`をフィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に割り当てます。
      * 定数値`BasicHttpSecurityMode.TransportCredentialOnly`をフィールド`BasicHttpBindingSecurity.Security.Mode`に割り当てます。

1. ユーザー情報を定義します。

   * コンストラクタを使用して `UserImpl` オブジェクトを作成します。
   * `UserImpl`オブジェクトの`domainName`フィールドに文字列値を割り当てて、デメイン名を設定します。
   * プリンシパルタイプを設定するには、`UserImpl`オブジェクトの`principalType`フィールドに文字列値を割り当てます。 例えば、`USER`を指定できます。
   * `UserImpl`オブジェクトの`userid`フィールドに文字列値を割り当てて、ユーザー識別子の値を設定します。
   * `UserImpl`オブジェクトの`canonicalName`フィールドに文字列値を割り当てて、正規名の値を設定します。
   * `UserImpl`オブジェクトの`givenName`フィールドに文字列値を割り当てて、指定した名前値を設定します。
   * `UserImpl`オブジェクトの`familyName`フィールドに文字列値を割り当てて、ファミリ名の値を設定します。

1. AEM Forms追加へのユーザー。

   `DirectoryManagerServiceClient`オブジェクトの`createLocalUser`メソッドを呼び出し、次の値を渡します。

   * 新しいユーザーを表す`UserImpl`オブジェクト
   * ユーザーのパスワードを表すstring値です

   `createLocalUser`メソッドは、ローカルユーザー識別子の値を指定する文字列値を返します。

1. ユーザーが追加されたことを確認します。

   * コンストラクタを使用して `PrincipalSearchFilter` オブジェクトを作成します。
   * ユーザーのユーザー識別子の値を設定するには、ユーザー識別子の値を表すstring値を`PrincipalSearchFilter`オブジェクトの`userId`フィールドに割り当てます。
   * `DirectoryManagerServiceClient`オブジェクトの`findPrincipals`メソッドを呼び出し、`PrincipalSearchFilter`オブジェクトを渡します。 このメソッドは、`MyArrayOfUser`コレクションオブジェクトを返します。各要素は`User`オブジェクトです。 `MyArrayOfUser`コレクションを繰り返し実行し、ユーザーを探します。

**関連トピック**

[手順の概要](users.md#summary-of-steps)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## ユーザーの削除{#deleting-users}

Directory Manager Service API（JavaおよびWebサービス）を使用すると、ユーザーをAEM Formsからプログラム的に削除できます。 ユーザーを削除すると、そのユーザーは、ユーザーを必要とするサービス操作を実行するために使用できなくなります。 例えば、削除したタスクにユーザーを割り当てることはできません。

### 手順{#summary_of_steps-1}の概要

ユーザーを削除するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. DirectoryManagerServiceクライアントを作成します。
1. 削除するユーザーを指定します。
1. ユーザーをAEM Formsから削除します。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを含めます。

**DirectoryManagerServiceクライアントの作成**

プログラムでDirectory Manager Service API操作を実行する前に、Directory Managerサービスクライアントを作成します。

**削除するユーザーの指定**

ユーザーの識別子の値を使用して、削除するユーザーを指定できます。

**ユーザーをAEM Formsから削除します**

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
   * `DirectoryManagerServiceClient`オブジェクトの`findPrincipals`メソッドを呼び出し、`PrincipalSearchFilter`オブジェクトを渡します。 このメソッドは、`java.util.List`インスタンスを返します。各要素は`User`オブジェクトです。 `java.util.List`インスタンスを繰り返し実行して、削除するユーザーを探します。

1. ユーザーをAEM Formsから削除します。

   `DirectoryManagerServiceClient`オブジェクトの`deleteLocalUser`メソッドを呼び出し、`User`オブジェクトの`oid`フィールドの値を渡します。 `User`オブジェクトの`getOid`メソッドを呼び出します。 `java.util.List`インスタンスから取得した`User`オブジェクトを使用します。

**関連トピック**

[手順の概要](users.md#summary-of-steps)

[クイック開始（EJBモード）:Java APIを使用したユーザーの削除](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-deleting-users-using-the-java-api)

[クイック開始（SOAPモード）:Java APIを使用したユーザーの削除](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-deleting-users-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#delete-users-using-the-web-service-api}を使用したユーザーの削除

Directory Manager Service API（Webサービス）を使用してユーザーを削除します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-usermanager-client.jarなどのクライアントJARファイルを含めます。

1. DirectoryManagerServiceクライアントを作成します。

   * `DirectoryManagerServiceClient`オブジェクトを作成するには、そのデフォルトのコンストラクタを使用します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`DirectoryManagerServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに指定するstring値を渡します（例：`http://localhost:8080/soap/services/DirectoryManagerService?blob=mtom`）。 `lc_version`属性を使用する必要はありません。 この属性は、サービス参照を作成する際に使用されます。 必ず`blob=mtom.`を指定してください
   * `DirectoryManagerServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * AEM formsユーザー名をフィールド`DirectoryManagerServiceClient.ClientCredentials.UserName.UserName`に割り当てます。
      * 対応するパスワード値をフィールド`DirectoryManagerServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * 定数値`HttpClientCredentialType.Basic`をフィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に割り当てます。
      * 定数値`BasicHttpSecurityMode.TransportCredentialOnly`をフィールド`BasicHttpBindingSecurity.Security.Mode`に割り当てます。

1. 削除するユーザーを指定します。

   * コンストラクタを使用して `PrincipalSearchFilter` オブジェクトを作成します。
   * `PrincipalSearchFilter`オブジェクトの`userId`フィールドに文字列値を割り当てて、ユーザー識別子の値を設定します。
   * `DirectoryManagerServiceClient`オブジェクトの`findPrincipals`メソッドを呼び出し、`PrincipalSearchFilter`オブジェクトを渡します。 このメソッドは、`MyArrayOfUser`コレクションオブジェクトを返します。各要素は`User`オブジェクトです。 `MyArrayOfUser`コレクションを繰り返し実行し、ユーザーを探します。 `MyArrayOfUser`コレクションオブジェクトから取得した`User`オブジェクトは、ユーザーの削除に使用されます。

1. ユーザーをAEM Formsから削除します。

   `User`オブジェクトの`oid`フィールド値を`DirectoryManagerServiceClient`オブジェクトの`deleteLocalUser`メソッドに渡して、ユーザーを削除します。

**関連トピック**

[手順の概要](users.md#summary-of-steps)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## グループの作成 {#creating-groups}

Directory Manager Service API（JavaおよびWebサービス）を使用して、AEM Formsグループをプログラムで作成できます。 グループを作成した後、そのグループを使用して、グループを必要とするサービス操作を実行できます。 例えば、ユーザーを新しいグループに割り当てることができます。 （「[ユーザーとグループの管理](users.md#managing-users-and-groups)」を参照）。

### 手順{#summary_of_steps-2}の概要

グループを作成するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. DirectoryManagerServiceクライアントを作成します。
1. グループが存在しないことを確認します。
1. グループを作成します。
1. グループに対してアクションを実行します。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(AEM FormsがJBossにデプロイされている場合に必須)
* jbossall-client.jar(AEM FormsがJBossにデプロイされている場合に必須)

これらのJARファイルの場所について詳しくは、「[AEM FormsJavaライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)」を参照してください。

**DirectoryManagerServiceクライアントの作成**

プログラムを使用してDirectory Managerサービスの操作を実行する前に、Directory Manager Service APIクライアントを作成します。

**グループが存在するかどうかの確認**

グループを作成する場合は、そのグループが同じドメインに存在しないことを確認します。 つまり、2つのグループが同じドメイン内で同じ名前を持つことはできません。 このタスクを実行するには、検索を実行し、2つの値に基づいて検索結果をフィルタリングします。 プリンシパルタイプを`com.adobe.idp.um.api.infomodel.Principal.PRINCIPALTYPE_GROUP`に設定し、グループのみが返されるようにします。 また、ドメイン名を必ず指定してください。

**グループの作成**

グループがドメインに存在しないと判断したら、グループを作成し、次の属性を指定します。

* **共通名**:グループの名前。
* **ドメイン**:グループが追加されるドメイン。
* **説明**:グループの説明。

**グループに対するアクションの実行**

グループを作成した後、そのグループを使用してアクションを実行できます。 例えば、ユーザーをグループに追加できます。 ユーザーをグループに追加するには、ユーザーとグループの両方の固有な識別子の値を取得します。 これらの値を`addPrincipalToLocalGroup`メソッドに渡します。

**関連トピック**

[Java APIを使用したグループの作成](users.md#create-groups-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[ユーザーの追加](users.md#adding-users)

[ユーザーの削除](users.md#deleting-users)

### Java APIを使用したグループの作成{#create-groups-using-the-java-api}

Directory Manager Service API(Java)を使用してグループを作成します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-usermanager-client.jarなどのクライアントJARファイルを含めます。

1. DirectoryManagerServiceクライアントを作成します。

   コンストラクターを使用し、接続プロパティを含む`ServiceClientFactory`オブジェクトを渡して、`DirectoryManagerServiceClient`オブジェクトを作成します。

1. グループが存在するかどうかを確認します。

   * コンストラクタを使用して `PrincipalSearchFilter` オブジェクトを作成します。
   * `PrincipalSearchFilter`オブジェクトの`setPrincipalType`オブジェクトを呼び出して、プリンシパルタイプを設定します。 値`com.adobe.idp.um.api.infomodel.Principal.PRINCIPALTYPE_GROUP`を渡します。
   * `PrincipalSearchFilter`オブジェクトの`setSpecificDomainName`オブジェクトを呼び出して、ドメインを設定します。 ドメイン名を指定するstring値を渡します。
   * グループを検索するには、`DirectoryManagerServiceClient`オブジェクトの`findPrincipals`メソッドを呼び出します（プリンシパルはグループにすることができます）。 プリンシパルタイプとドメイン名を指定する`PrincipalSearchFilter`オブジェクトを渡します。 このメソッドは、`java.util.List`インスタンスを返します。各要素は`Group`インスタンスです。 各グループインスタンスは、`PrincipalSearchFilter`オブジェクトを使用して指定されたフィルターに準拠します。
   * `java.util.List`インスタンスを反復します。 各要素について、グループ名を取得します。 グループ名が新しいグループ名と等しくないことを確認します。

1. グループを作成します。

   * グループが存在しない場合は、`Group`オブジェクトの`setCommonName`メソッドを呼び出し、グループ名を指定する文字列値を渡します。
   * `Group`オブジェクトの`setDescription`メソッドを呼び出し、グループの説明を指定する文字列値を渡します。
   * `Group`オブジェクトの`setDomainName`メソッドを呼び出し、ドメイン名を指定する文字列値を渡します。
   * `DirectoryManagerServiceClient`オブジェクトの`createLocalGroup`メソッドを呼び出し、`Group`インスタンスを渡します。

   `createLocalUser`メソッドは、ローカルユーザー識別子の値を指定する文字列値を返します。

1. グループに対してアクションを実行します。

   * コンストラクタを使用して `PrincipalSearchFilter` オブジェクトを作成します。
   * `PrincipalSearchFilter`オブジェクトの`setUserId`メソッドを呼び出して、ユーザー識別子の値を設定します。 ユーザー識別子の値を表すstring値を渡します。
   * `DirectoryManagerServiceClient`オブジェクトの`findPrincipals`メソッドを呼び出し、`PrincipalSearchFilter`オブジェクトを渡します。 このメソッドは、`java.util.List`インスタンスを返します。各要素は`User`オブジェクトです。 `java.util.List`インスタンスを繰り返し実行し、ユーザーを探します。
   * &lt;a0追加/>オブジェクトの`DirectoryManagerServiceClient`メソッドを呼び出して、グループにユーザーを追加します。 `addPrincipalToLocalGroup``User`オブジェクトの`getOid`メソッドの戻り値を渡します。 `Group`オブジェクトの`getOid`メソッドの戻り値を渡します（新しいグループを表す`Group`インスタンスを使用します）。

**関連トピック**

[手順の概要](users.md#summary-of-steps)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## ユーザーとグループの管理 {#managing-users-and-groups}

このトピックでは、(Java)を使用して、ドメイン、ユーザー、グループをプログラムによって割り当て、削除、クエリする方法について説明します。

>[!NOTE]
>
>ドメインを設定する場合、グループおよびユーザーの固有な識別子を設定する必要があります。 選択する属性は、LDAP環境内で一意である必要があるだけでなく、不変である必要があり、ディレクトリ内で変更されません。 また、この属性は単純な文字列データ型である必要があります（Active Directory 2000/2003で現在許可されている唯一の例外は`"objectsid"`で、バイナリ値です）。 例えば、Novell eDirectory属性`"GUID"`は、単純な文字列データ型ではないので、機能しません。

* Active Directoryの場合は、`"objectsid"`を使用します。
* SunOneの場合は、`"nsuniqueid"`を使用します。

>[!NOTE]
>
>LDAPディレクトリの同期の進行中に複数のローカルユーザーおよびグループを作成することは、サポートされていません。 この処理を試みると、エラーが発生します。

### 手順{#summary_of_steps-3}の概要

ユーザーおよびグループを管理するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. DirectoryManagerServiceクライアントを作成します。
1. 適切なユーザー操作またはグループ操作を呼び出します。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めます。

**DirectoryManagerServiceクライアントの作成**

プログラムを使用してDirectory Managerサービスの操作を実行する前に、Directory Managerサービスクライアントを作成する必要があります。 Java APIを使用すると、`DirectoryManagerServiceClient`オブジェクトを作成することで実現できます。 WebサービスAPIを使用すると、`DirectoryManagerServiceService`オブジェクトを作成することで実現できます。

**適切なユーザー操作またはグループ操作を呼び出します**

サービスクライアントを作成したら、ユーザー管理操作またはグループ管理操作を呼び出すことができます。 サービスクライアントでは、ドメイン、ユーザー、グループの割り当て、削除、クエリが可能です。 ディレクトリプリンシパルまたはローカルプリンシパルをローカルグループに追加することは可能ですが、ローカルプリンシパルをディレクトリグループに追加することはできません。

**関連トピック**

[Java APIを使用したユーザーとグループの管理](users.md#managing-users-and-groups-using-the-java-api)

[WebサービスAPIを使用したユーザーとグループの管理](users.md#managing-users-and-groups-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[User Manager APIのクイック開始](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

### Java APIを使用したユーザーとグループの管理{#managing-users-and-groups-using-the-java-api}

(Java)を使用してユーザー、グループおよびドメインをプログラムで管理するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-usermanager-client.jarなどのクライアントJARファイルを含めます。 これらのファイルの場所については、[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。

1. DirectoryManagerServiceクライアントを作成します。

   コンストラクターを使用し、接続プロパティを含む`ServiceClientFactory`オブジェクトを渡して、`DirectoryManagerServiceClient`オブジェクトを作成します。 詳しくは、[接続プロパティの設定&#x200B;](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)*を参照してください。*

1. 適切なユーザー操作またはグループ操作を呼び出します。

   ユーザーまたはグループを検索するには、`DirectoryManagerServiceClient`オブジェクトのいずれかのメソッドを呼び出してプリンシパルを検索します（プリンシパルはユーザーまたはグループになる可能性があるため）。 次の例では、`findPrincipals`メソッドが検索フィルター（`PrincipalSearchFilter`オブジェクト）を使用して呼び出されます。

   この場合の戻り値は`Principal`オブジェクトを含む`java.util.List`なので、結果を繰り返し処理し、`Principal`オブジェクトを`User`または`Group`オブジェクトにキャストします。

   結果の`User`または`Group`オブジェクト（両方とも`Principal`インターフェイスから継承）を使用して、ワークフローで必要な情報を取得します。 例えば、ドメイン名と正規名の値を組み合わせて、プリンシパルを一意に識別します。 これらは、`Principal`オブジェクトの`getDomainName`メソッドと`getCanonicalName`メソッドをそれぞれ呼び出して取得されます。

   ローカルユーザーを削除するには、`DirectoryManagerServiceClient`オブジェクトの`deleteLocalUser`メソッドを呼び出し、ユーザーの識別子を渡します。

   ローカルグループを削除するには、`DirectoryManagerServiceClient`オブジェクトの`deleteLocalGroup`メソッドを呼び出し、グループの識別子を渡します。

**関連トピック**

[手順の概要](users.md#summary-of-steps)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#managing-users-and-groups-using-the-web-service-api}を使用したユーザーとグループの管理

Directory Manager Service API（Webサービス）を使用してユーザー、グループ、ドメインをプログラムで管理するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。

   * Directory Manager WSDLを使用するMicrosoft .NETクライアントアセンブリを作成します。 (「[Base64エンコードを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)」を参照)。
   * Microsoft .NETクライアントアセンブリを参照します。 （「[Base64エンコード](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)を使用する.NETクライアントアセンブリの作成」を参照）。

1. DirectoryManagerServiceクライアントを作成します。

   プロキシクラスのコンストラクターを使用して`DirectoryManagerServiceService`オブジェクトを作成します。

1. 適切なユーザー操作またはグループ操作を呼び出します。

   ユーザーまたはグループを検索するには、`DirectoryManagerServiceService`オブジェクトのいずれかのメソッドを呼び出してプリンシパルを検索します（プリンシパルはユーザーまたはグループになる可能性があるため）。 次の例では、`findPrincipalsWithFilter`メソッドが検索フィルター（`PrincipalSearchFilter`オブジェクト）を使用して呼び出されます。 `PrincipalSearchFilter`オブジェクトを使用する場合、ローカルプリンシパルは、`isLocal`プロパティが`true`に設定されている場合にのみ返されます。 この動作は、Java APIで発生する動作とは異なります。

   >[!NOTE]
   >
   >検索フィルターで（`PrincipalSearchFilter.resultsMax`フィールドを通して）検索結果の最大数が指定されていない場合、最大1000個の結果が返されます。 これは、Java APIを使用した場合とは異なる動作です。Java APIの結果数はデフォルトの最大数10です。 また、`findGroupMembers`などの検索方法では、検索フィルターで検索結果の最大数が指定されていない限り（例えば`GroupMembershipSearchFilter.resultsMax`フィールドを通して）結果を出すことはありません。 これは、`GenericSearchFilter`クラスから継承するすべての検索フィルターに適用されます。 詳しくは、[AEM FormsAPIリファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)を参照してください。

   この場合の戻り値は`Principal`オブジェクトを含む`object[]`なので、結果を繰り返し処理し、`Principal`オブジェクトを`User`または`Group`オブジェクトにキャストします。

   結果の`User`または`Group`オブジェクト（両方とも`Principal`インターフェイスから継承）を使用して、ワークフローで必要な情報を取得します。 例えば、ドメイン名と正規名の値を組み合わせて、プリンシパルを一意に識別します。 これらは、`Principal`オブジェクトの`domainName`フィールドと`canonicalName`フィールドをそれぞれ呼び出して取得されます。

   ローカルユーザーを削除するには、`DirectoryManagerServiceService`オブジェクトの`deleteLocalUser`メソッドを呼び出し、ユーザーの識別子を渡します。

   ローカルグループを削除するには、`DirectoryManagerServiceService`オブジェクトの`deleteLocalGroup`メソッドを呼び出し、グループの識別子を渡します。

**関連トピック**

[手順の概要](users.md#summary-of-steps)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## ロールと権限の管理{#managing-roles-and-permissions}

このトピックでは、Authorization Manager Service API (Java)を使用して、ロールと権限をプログラムによって割り当て、削除、決定する方法について説明します。

AEM Formsでは、*ロール*&#x200B;は、1つ以上のシステムレベルのリソースにアクセスするための権限のグループです。 これらの権限は、User Managementを通じて作成され、サービスコンポーネントによって適用されます。 例えば、管理者が「ポリシーセット作成者」のロールをユーザーのグループに割り当てることができます。 その後、Rights Managementは、そのロールを持つグループのユーザーに、管理コンソールからポリシーセットを作成することを許可します。

役割には2種類あります。*デフォルトの役割*&#x200B;と&#x200B;*カスタムの役割* デフォルトの役割（*システムの役割）*&#x200B;は、既にAEM Formsに常駐しています。 デフォルトのロールは、管理者が削除または変更できない場合があるので変更できません。 その後、管理者が作成したカスタムロールは、変更または削除できるので、変更できません。

ロールを使用すると、権限の管理が容易になります。 ロールがプリンシパルに割り当てられると、一連の権限がそのプリンシパルに自動的に割り当てられ、プリンシパルに関する特定のアクセス関連の決定はすべて、割り当てられた権限の全体セットに基づいて行われます。

### 手順{#summary_of_steps-4}の概要

ロールと権限を管理するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. AuthorizationManagerServiceクライアントを作成します。
1. 適切なロールまたは権限操作を呼び出します。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めます。

**AuthorizationManagerServiceクライアントの作成**

User Management AuthorizationManagerService操作をプログラムで実行する前に、AuthorizationManagerServiceクライアントを作成する必要があります。 Java APIを使用すると、`AuthorizationManagerServiceClient`オブジェクトを作成することで実現できます。

**適切なロールまたは権限操作を呼び出します**

サービスクライアントを作成したら、ロール操作または権限操作を呼び出すことができます。 サービスクライアントでは、ロールと権限の割り当て、削除、および決定を行うことができます。

**関連トピック**

[Java APIを使用したロールと権限の管理](users.md#managing-roles-and-permissions-using-the-java-api)

[WebサービスAPIを使用したロールと権限の管理](users.md#managing-roles-and-permissions-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[User Manager APIのクイック開始](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

### Java API {#managing-roles-and-permissions-using-the-java-api}を使用したロールと権限の管理

Authorization Manager Service API (Java)を使用してロールと権限を管理するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-usermanager-client.jarなどのクライアントJARファイルを含めます。

1. AuthorizationManagerServiceクライアントを作成します。

   コンストラクターを使用し、接続プロパティを含む`ServiceClientFactory`オブジェクトを渡して、`AuthorizationManagerServiceClient`オブジェクトを作成します。

1. 適切なロールまたは権限操作を呼び出します。

   プリンシパルにロールを割り当てるには、`AuthorizationManagerServiceClient`オブジェクトの`assignRole`メソッドを呼び出し、次の値を渡します。

   * ロール識別子を含む`java.lang.String`オブジェクト
   * プリンシパル識別子を含む`java.lang.String`オブジェクトの配列です。

   プリンシパルからロールを削除するには、`AuthorizationManagerServiceClient`オブジェクトの`unassignRole`メソッドを呼び出し、次の値を渡します。

   * ロール識別子を含む`java.lang.String`オブジェクト。
   * プリンシパル識別子を含む`java.lang.String`オブジェクトの配列です。


**関連トピック**

[手順の概要](users.md#summary-of-steps)

[クイック開始（SOAPモード）:Java APIを使用したロールと権限の管理](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-managing-roles-and-permissions-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#managing-roles-and-permissions-using-the-web-service-api}を使用したロールと権限の管理

Authorization Manager Service API （Webサービス）を使用して、ロールと権限を管理します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/AuthorizationManagerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. AuthorizationManagerServiceクライアントを作成します。

   * `AuthorizationManagerServiceClient`オブジェクトを作成するには、そのオブジェクトのデフォルトのコンストラクタを使用します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`AuthorizationManagerServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに指定するstring値を渡します（例：`http://localhost:8080/soap/services/AuthorizationManagerService?blob=mtom`）。 `lc_version`属性を使用する必要はありません。 この属性は、サービス参照を作成する際に使用されます。
   * `AuthorizationManagerServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * AEM formsユーザー名をフィールド`AuthorizationManagerServiceClient.ClientCredentials.UserName.UserName`に割り当てます。
      * 対応するパスワード値をフィールド`AuthorizationManagerServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * 定数値`HttpClientCredentialType.Basic`をフィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に割り当てます。
      * 定数値`BasicHttpSecurityMode.TransportCredentialOnly`をフィールド`BasicHttpBindingSecurity.Security.Mode`に割り当てます。

1. 適切なロールまたは権限操作を呼び出します。

   プリンシパルにロールを割り当てるには、`AuthorizationManagerServiceClient`オブジェクトの`assignRole`メソッドを呼び出し、次の値を渡します。

   * ロール識別子を含む`string`オブジェクト
   * プリンシパルIDを格納する`MyArrayOf_xsd_string`オブジェクト。

   プリンシパルからロールを削除するには、`AuthorizationManagerServiceService`オブジェクトの`unassignRole`メソッドを呼び出し、次の値を渡します。

   * ロール識別子を含む`string`オブジェクト。
   * プリンシパル識別子を含む`string`オブジェクトの配列です。


**関連トピック**

[手順の概要](users.md#summary-of-steps)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## ユーザーの認証{#authenticating-users}

このトピックでは、Authentication Manager Service API(Java)を使用して、クライアントアプリケーションでユーザーをプログラム的に認証する方法について説明します。

ユーザー認証は、安全なデータを格納するエンタープライズデータベースや他のエンタープライズリポジトリとのやり取りに必要な場合があります。

例えば、ユーザーがユーザー名とパスワードをWebページに入力し、値をFormsをホストするJ2EEアプリケーションサーバーに送信するシナリオを考えてみましょう。 Formsのカスタムアプリケーションは、Authentication Managerサービスでユーザーを認証できます。

認証が成功した場合、アプリケーションは、保護されたエンタープライズデータベースにアクセスします。 それ以外の場合は、許可されたユーザーではないことを示すメッセージがユーザーに送信されます。

次の図に、アプリケーションのロジックのフローを示します。

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
   <td><p>ユーザはウェブサイトにアクセスし、ユーザ名とパスワードを指定する。 この情報は、AEM FormsをホストするJ2EEアプリケーションサーバーに送信されます。</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>ユーザー資格情報はAuthentication Managerサービスで認証されます。 ユーザーの資格情報が有効な場合、ワークフローは手順3に進みます。 それ以外の場合は、許可されたユーザーではないことを示すメッセージがユーザーに送信されます。</p></td>
  </tr>
  <tr>
   <td><p>1</p></td>
   <td><p>ユーザ情報とフォームデザインは、保護された企業データベースから検索される。 </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>ユーザー情報がフォームデザインとマージされ、フォームがユーザーにレンダリングされます。 </p></td>
  </tr>
 </tbody>
</table>

### 手順{#summary_of_steps-5}の概要

プログラムによってユーザーを認証するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. AuthenticationManagerServiceクライアントを作成します。
1. 認証操作を呼び出します。
1. 必要に応じて、コンテキストを取得し、クライアントアプリケーションが認証用に別のAEM Formsサービスに転送できるようにします。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めます。

**AuthenticationManagerServiceクライアントの作成**

プログラムでユーザーを認証する前に、AuthenticationManagerServiceクライアントを作成する必要があります。 Java APIを使用する場合は、`AuthenticationManagerServiceClient`オブジェクトを作成します。

**認証操作の呼び出し**

サービスクライアントを作成したら、認証操作を呼び出すことができます。 この操作には、ユーザー名やパスワードなど、ユーザーに関する情報が必要です。 ユーザーが認証されない場合は、例外が発生します。

**認証コンテキストの取得**

ユーザーを認証すると、認証済みユーザーに基づいてコンテキストを作成できます。 その後、コンテンツを使用して別のAEM Formsサービスを呼び出すことができます。 例えば、コンテキストを使用して`EncryptionServiceClient`を作成し、PDFドキュメントをパスワードで暗号化できます。 認証されたユーザーに、AEM Formsサービスの呼び出しに必要な`Services User`というロールがあることを確認してください。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[User Manager APIのクイック開始](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

[PDFドキュメントのパスワードによる暗号化](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Java API {#authenticate-a-user-using-the-java-api}を使用したユーザー認証

Authentication Manager Service API(Java)を使用してユーザーを認証します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-usermanager-client.jarなどのクライアントJARファイルを含めます。

1. AuthenticationManagerServicesクライアントを作成します。

   コンストラクターを使用し、接続プロパティを含む`ServiceClientFactory`オブジェクトを渡して、`AuthenticationManagerServiceClient`オブジェクトを作成します。

1. 認証操作を呼び出します。

   `AuthenticationManagerServiceClient`オブジェクトの`authenticate`メソッドを呼び出し、次の値を渡します。

   * ユーザー名を含む`java.lang.String`オブジェクト。
   * ユーザーのパスワードを含むバイト配列（`byte[]`オブジェクト）。 `byte[]`オブジェクトを取得するには、`java.lang.String`オブジェクトの`getBytes`メソッドを呼び出します。

   authenticateメソッドは、認証済みユーザーに関する情報を含む`AuthResult`オブジェクトを返します。

1. 認証コンテキストを取得します。

   `ServiceClientFactory`オブジェクトの`getContext`メソッドを呼び出します。これにより、`Context`オブジェクトが返されます。

   次に、`Context`オブジェクトの`initPrincipal`メソッドを呼び出し、`AuthResult`を渡します。

### WebサービスAPI {#authenticate-a-user-using-the-web-service-api}を使用してユーザーを認証する

Authentication Manager Service API（Webサービス）を使用してユーザーを認証します。

1. プロジェクトファイルを含めます。

   * Authentication Manager WSDLを使用するMicrosoft .NETクライアント・アセンブリを作成します。 (「[Base64エンコードを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)」を参照)。
   * Microsoft .NETクライアントアセンブリを参照します。 (「[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)」の「.NETクライアントアセンブリの参照」を参照)。

1. AuthenticationManagerServiceクライアントを作成します。

   プロキシクラスのコンストラクターを使用して`AuthenticationManagerServiceService`オブジェクトを作成します。

1. 認証操作を呼び出します。

   `AuthenticationManagerServiceClient`オブジェクトの`authenticate`メソッドを呼び出し、次の値を渡します。

   * ユーザー名を含む`string`オブジェクト
   * ユーザーのパスワードを含むバイト配列（`byte[]`オブジェクト）。 次の例に示すロジックを使用して、パスワードを含む`string`オブジェクトを`byte[]`配列に変換することで、`byte[]`オブジェクトを取得できます。
   * 返される値は`AuthResult`オブジェクトで、ユーザーに関する情報の取得に使用できます。 次の例では、ユーザーの情報を取得するために、最初に`AuthResult`オブジェクトの`authenticatedUser`フィールドを取得し、次に結果の`User`オブジェクトの`canonicalName`フィールドと`domainName`フィールドを取得します。

**関連トピック**

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## プログラムによるユーザーの同期{#programmatically-synchronizing-users}

User Management APIを使用して、プログラムによってユーザーを同期できます。 ユーザーを同期すると、ユーザーリポジトリ内のユーザーデータでAEM Formsを更新します。 例えば、新しいユーザーをユーザーリポジトリに追加するとします。 同期操作を実行すると、新しいユーザーがAEM formsユーザーになります。 また、ユーザーリポジトリに存在しなくなったユーザーは、AEM Formsから削除されます。

次の図は、AEM Formsがユーザー・リポジトリと同期していることを示しています。

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
   <td><p>AEM Formsが同期操作を実行するクライアントアプリケーション要求。</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>AEM Formsが同期操作を実行します。</p></td>
  </tr>
  <tr>
   <td><p>1</p></td>
   <td><p>ユーザー情報が更新されます。</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>ユーザは、更新されたユーザ情報を表示することができる。 </p></td>
  </tr>
 </tbody>
</table>

### 手順{#summary_of_steps-6}の概要

プログラムによってユーザーを同期するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. UserManagerUtilServiceClientクライアントを作成します。
1. エンタープライズドメインを指定します。
1. 認証操作を呼び出します。
1. 同期操作が完了したかどうかを確認する

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めます。

**UserManagerUtilServiceClientclientの作成**

プログラムによってユーザーを同期する前に、`UserManagerUtilServiceClient`オブジェクトを作成する必要があります。

**エンタープライズドメインの指定**

User Management APIを使用して同期操作を実行する前に、ユーザーが属するエンタープライズドメインを指定します。 エンタープライズドメインは1つ以上指定できます。 プログラムによって同期操作を実行する前に、管理コンソールを使用してエンタープライズドメインを設定する必要があります。 （[管理ヘルプ](https://www.adobe.com/go/learn_aemforms_admin_63)を参照）。

**同期操作の呼び出し**

1つ以上のエンタープライズドメインを指定した後、同期操作を実行できます。 この操作の実行に要する時間は、ユーザーリポジトリ内のユーザーレコードの数によって異なります。

**同期操作が完了したかどうかを確認する**

プログラムで同期操作を実行した後、操作が完了したかどうかを判断できます。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[User Manager APIのクイック開始](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

[PDFドキュメントのパスワードによる暗号化](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Java API {#programmatically-synchronizing-users-using-the-java-api}を使用してプログラムによってユーザーを同期する

User Management API(Java)を使用してユーザーを同期します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-usermanager-client.jarやadobe-usermanager-util-client.jarなどのクライアントJARファイルを含めます。

1. UserManagerUtilServiceClientクライアントを作成します。

   コンストラクターを使用し、接続プロパティを含む`ServiceClientFactory`オブジェクトを渡して、`UserManagerUtilServiceClient`オブジェクトを作成します。

1. エンタープライズドメインを指定します。

   * `UserManagerUtilServiceClient`オブジェクトの`scheduleSynchronization`メソッドを呼び出して、ユーザー同期操作を開始します。
   * `HashSet`コンストラクターを使用して`java.util.Set`インスタンスを作成します。 データタイプとして`String`を必ず指定してください。 この`Java.util.Set`インスタンスは、同期操作が適用されるドメイン名を格納します。
   * 追加するドメイン名ごとに、`java.util.Set`オブジェクトのaddメソッドを呼び出し、ドメイン名を渡します。

1. 同期操作を呼び出します。

   `ServiceClientFactory`オブジェクトの`getContext`メソッドを呼び出します。これにより、`Context`オブジェクトが返されます。

   次に、`Context`オブジェクトの`initPrincipal`メソッドを呼び出し、`AuthResult`を渡します。

**関連トピック**

[プログラムによるユーザの同期](users.md#programmatically-synchronizing-users)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
