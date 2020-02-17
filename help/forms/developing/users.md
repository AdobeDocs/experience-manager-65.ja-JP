---
title: ユーザーの管理
seo-title: ユーザーの管理
description: 'null'
seo-description: 'null'
uuid: 68d8a0bc-6e3d-4286-ba5c-534dcf58cb84
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 95804bff-9e6f-4807-aae4-790bd9e7cb57
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# ユーザーの管理 {#managing-users}

**User Managementについて**

User Management APIを使用して、ロール、権限、プリンシパル（ユーザーまたはグループ）を管理でき、ユーザーを認証できるクライアントアプリケーションを作成できます。 User Management APIは、次のAEM Forms APIで構成されています。

* Directory ManagerサービスAPI
* Authentication ManagerサービスAPI
* 承認マネージャーサービスAPI

User Managementでは、ロールと権限の割り当て、削除、決定を行うことができます。 また、ドメイン、ユーザー、グループの割り当て、削除、およびクエリを行うこともできます。 最後に、User Managementを使用してユーザーを認証できます。

「ユーザ [ーの追加](users.md#adding-users) 」では、プログラムによるユーザーの追加方法を理解します。 この節では、Directory Manager Service APIを使用します。

「ユーザ [ーの削除](users.md#deleting-users) 」では、ユーザーをプログラム的に削除する方法を理解します。 この節では、Directory Manager Service APIを使用します。

「ユー [ザーとグループの管理](users.md#managing-users-and-groups) 」では、ローカルユーザーとディレクトリユーザーの違いを理解し、JavaおよびWebサービスAPIを使用してユーザーとグループをプログラム的に管理する方法の例を確認します。 この節では、Directory Manager Service APIを使用します。

「ロー [ルと権限の管理](users.md#managing-roles-and-permissions) 」では、システムの役割と権限について、およびそれらをプログラム的に拡張する方法と、JavaおよびWebサービスAPIを使用して役割と権限をプログラム的に管理する方法の例を示します。 この節では、Directory Manager Service APIとAuthorization Manager Service APIの両方を使用します。

「ユー [ザの認証](users.md#authenticating-users) 」には、Java APIとWebサービスAPIを使用してユーザをプログラム的に認証する方法の例が示されています。 このセクションでは、Authorization Manager Service APIを使用します。

**認証プロセスについて**

User Managementには、組み込みの認証機能と、独自の認証プロバイダーとの接続機能が用意されています。 User Managementは、認証要求を受け取ると（例えば、ユーザーがログインを試みると）、認証プロバイダーにユーザー情報を渡して認証を受けます。 User Managementは、ユーザーの認証後、認証プロバイダーから結果を受け取ります。

次の図は、ログインを試みたエンドユーザー、User Management、および認証プロバイダー間でのやり取りを示しています。

![mu_mu_uauth_process](assets/mu_mu_umauth_process.png)

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
   <td><p>User Managementでは、ユーザーが製品にログインするか、製品へのアクセスを拒否します。</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>サーバーのタイムゾーンがクライアントのタイムゾーンと異なる場合、WebSphere Application serverクラスター上の.NETクライアントを使用して、ネイティブSOAPスタック上のAEM Forms Generate PDFサービス用のWSDLを使用すると、次のUser Management認証エラーが発生する可能性があります。

`[com.adobe.idp.um.webservices.WSSecurityHandler] errorCode:12803 errorCodeHEX:0x3203 message:WSSecurityHandler: UM authenticate returns exception : An error was discovered processing the <wsse:Security> header. (WSSecurityEngine: Invalid timestamp The security semantics of message have expired).`

**ディレクトリ管理について**

User Managementは、LDAPディレクトリへの接続をサポートするディレクトリサービスプロバイダー(DirectoryManagerService)でパッケージ化されています。 組織でLDAP以外のリポジトリを使用してユーザーレコードを保存する場合は、リポジトリで動作する独自のディレクトリサービスプロバイダーを作成できます。

ディレクトリサービスプロバイダーは、User Managementの要求に応じてユーザーストアからレコードを取得します。 User Managementは、パフォーマンスを向上させるために、ユーザーレコードとグループレコードを定期的にデータベースにキャッシュします。

ディレクトリサービスプロバイダーを使用して、User Managementデータベースをユーザーストアと同期できます。 この手順により、すべてのユーザーディレクトリ情報と、すべてのユーザーレコードおよびグループレコードが最新の状態になります。

また、DirectoryManagerServiceはドメインの作成と管理を行う機能も提供します。 ドメインは、様々なユーザーベースを定義します。 ドメインの境界は、通常、組織の構造やユーザーストアの設定方法に従って定義されます。 User Managementドメインは、認証プロバイダーおよびディレクトリサービスプロバイダーが使用する設定を提供します。

User Managementが書き出す設定XMLでは、の属性値を持つルートノードに、User Management用に定義された各ドメ `Domains` インのXML要素が含まれています。 これらの各要素には、特定のサービスプロバイダーに関連付けられたドメインの外観を定義する他の要素が含まれています。

**objectSID値について**

Active Directoryを使用する場合、値が複数のドメイン間で一意の属性で `objectSID` はないことを理解することが重要です。 この値は、オブジェクトのセキュリティ識別子を格納します。 複数のドメイン環境（例えば、ドメインのツリー）では、値が異な `objectSID` る場合があります。

値は、 `objectSID` あるActive Directoryドメインから別のドメインにオブジェクトを移動した場合に変更されます。 一部のオブジェクトは、ドメイ `objectSID` ン内のどこでも同じ値を持ちます。 例えば、BUILTIN\Administrators、BUILTIN\Power usersなどのグループは、ドメインに関係なく同じ値 `objectSID` を持ちます。 これら `objectSID` の値はよく知られています。

## Adding Users {#adding-users}

Directory Manager Service API（JavaおよびWebサービス）を使用して、AEM Formsにプログラム的にユーザーを追加できます。 ユーザーを追加した後、そのユーザーを使用して、ユーザーを必要とするサービス操作を実行できます。 例えば、新しいユーザーにタスクを割り当てることができます。

### 手順の概要 {#summary-of-steps}

ユーザーを追加するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. DirectoryManagerServiceクライアントを作成します。
1. ユーザー情報を定義します。
1. AEM Formsにユーザーを追加します。
1. ユーザーが追加されていることを確認します。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを含めます。

**DirectoryManagerServiceクライアントの作成**

プログラムでDirectory Managerサービス操作を実行する前に、Directory Manager Service APIクライアントを作成します。

**ユーザー情報の定義**

Directory Manager Service APIを使用して新しいユーザーを追加する場合は、そのユーザーの情報を定義します。 通常、新しいユーザーを追加する場合は、次の値を定義します。

* **ドメイン名**:ユーザーが属するドメイン(例： `DefaultDom`)。
* **ユーザー識別子の値**:ユーザーの識別子の値(例： `wblue`)。
* **プリンシパルタイプ**:ユーザーのタイプ(例えば、 `USER)`.
* **名**:ユーザーの特定の名前(例： `Wendy`)。
* **姓**:ユーザーの姓(例： `Blue)`.
* **ロケール**:ユーザーのロケール情報。

**AEM Formsへのユーザーの追加**

ユーザー情報を定義した後、そのユーザーをAEM Formsに追加できます。 ユーザーを追加するには、オブジェクトの `DirectoryManagerServiceClient` メソッドを呼び出 `createLocalUser` します。

**ユーザーが追加されたことの確認**

ユーザーが追加されたことを確認して、問題が発生していないことを確認できます。 ユーザー識別子の値を使用して、新しいユーザーを検索します。

**関連トピック**

[Java APIを使用したユーザーの追加](users.md#add-users-using-the-java-api)

[WebサービスAPIを使用したユーザーの追加](users.md#add-users-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[ユーザーの削除](users.md#deleting-users)

### Java APIを使用したユーザーの追加 {#add-users-using-the-java-api}

Directory Manager Service API(Java)を使用してユーザーを追加します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-usermanager-client.jarなどのクライアントJARファイルを含めます。

1. DirectoryManagerServicesクライアントを作成します。

   コンストラク `DirectoryManagerServiceClient` ターを使用し、接続プロパティを含むオブジェクトを渡 `ServiceClientFactory` して、オブジェクトを作成します。

1. ユーザー情報を定義します。

   * コンストラクタを使用して `UserImpl` オブジェクトを作成します。
   * オブジェクトのメソッドを呼び出して、デ `UserImpl` メイン名を設定 `setDomainName` します。 ドメイン名を指定するstring値を渡します。
   * オブジェクトのメソッドを呼び出して、プ `UserImpl` リンシパルタイプを設 `setPrincipalType` 定します。 ユーザーのタイプを指定するstring値を渡します。 例えば、を指定できます `USER`。
   * オブジェクトのメソッドを呼び出して、ユー `UserImpl` ザー識別子の値を設 `setUserid` 定します。 ユーザー識別子の値を指定するstring値を渡します。 例えば、を指定できます `wblue`。
   * オブジェクトのメソッドを呼び出して、正 `UserImpl` 規名を設定 `setCanonicalName` します。 ユーザーの正規名を指定するstring値を渡します。 例えば、を指定できます `wblue`。
   * オブジェクトのメソッドを呼び出して、 `UserImpl` 指定した名前を設 `setGivenName` 定します。 ユーザーの名前を指定するstring値を渡します。 例えば、を指定できます `Wendy`。
   * オブジェクトのメソッドを呼び出して、フ `UserImpl` ァミリ名を設定 `setFamilyName` します。 ユーザーの姓を指定するstring値を渡します。 例えば、を指定できます `Blue`。
   >[!NOTE]
   >
   >オブジェクトに属するメソッドを呼び出し `UserImpl` て、他の値を設定します。 例えば、オブジェクトのメソッドを呼び出してロケール値 `UserImpl` を設定でき `setLocale` ます。

1. AEM Formsにユーザーを追加します。

   オブジェクト `DirectoryManagerServiceClient` のメソッドを `createLocalUser` 呼び出し、次の値を渡します。

   * 新しい `UserImpl` ユーザーを表すオブジェクトです
   * ユーザーのパスワードを表すstring値です
   このメ `createLocalUser` ソッドは、ローカルユーザー識別子の値を指定するstring値を返します。

1. ユーザーが追加されたことを確認します。

   * コンストラクタを使用して `PrincipalSearchFilter` オブジェクトを作成します。
   * オブジェクトのメソッドを呼び出して、ユー `PrincipalSearchFilter` ザー識別子の値を設 `setUserId` 定します。 ユーザー識別子の値を表すstring値を渡します。
   * Invoke the `DirectoryManagerServiceClient` object’s `findPrincipals` method and pass the `PrincipalSearchFilter` object. このメソッドは、各要素 `java.util.List` がオブジェクトであるインスタンスを返 `User` します。 インスタンスを繰り `java.util.List` 返し実行し、ユーザーを検索します。

**関連トピック**

[手順の概要](users.md#summary-of-steps)

[クイックスタート（SOAPモード）:Java APIを使用したユーザの追加](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-adding-users-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したユーザーの追加 {#add-users-using-the-web-service-api}

Directory Manager Service API（Webサービス）を使用してユーザーを追加します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 サービス参照に次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/DirectoryManagerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. DirectoryManagerServiceクライアントを作成します。

   * Create a `DirectoryManagerServiceClient` object by using its default constructor.
   * Create a `DirectoryManagerServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/DirectoryManagerService?blob=mtom`)に渡すstring値。 属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます。 必ず指定しま `?blob=mtom`す。
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `DirectoryManagerServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当てま `DirectoryManagerServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `DirectoryManagerServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. ユーザー情報を定義します。

   * コンストラクタを使用して `UserImpl` オブジェクトを作成します。
   * オブジェクトのフィールドに文字列値を割り当てて、デ `UserImpl` メイン名を設定 `domainName` します。
   * オブジェクトのフィールドに文字列値を割り当てて、プリンシパル `UserImpl` タイプを設定 `principalType` します。 例えば、を指定できます `USER`。
   * オブジェクトのフィールドに文字列値を割り当てて、ユー `UserImpl` ザー識別子の値を設 `userid` 定します。
   * オブジェクトのフィールドに文字列値を割り当てて、正規名 `UserImpl` の値を設定し `canonicalName` ます。
   * オブジェクトのフィールドに文字列値を割り当てて、指定し `UserImpl` た名前値を設定 `givenName` します。
   * オブジェクトのフィールドに文字列値を割り当てて、ファミリ名 `UserImpl` の値を設定 `familyName` します。

1. AEM Formsにユーザーを追加します。

   オブジェクト `DirectoryManagerServiceClient` のメソッドを `createLocalUser` 呼び出し、次の値を渡します。

   * 新しい `UserImpl` ユーザーを表すオブジェクトです
   * ユーザーのパスワードを表すstring値です
   このメ `createLocalUser` ソッドは、ローカルユーザー識別子の値を指定するstring値を返します。

1. ユーザーが追加されたことを確認します。

   * コンストラクタを使用して `PrincipalSearchFilter` オブジェクトを作成します。
   * ユーザーのユーザー識別子の値を設定するには、ユーザー識別子の値を表すstring値をオブジェクトのフィー `PrincipalSearchFilter` ルドに割り当 `userId` てます。
   * Invoke the `DirectoryManagerServiceClient` object’s `findPrincipals` method and pass the `PrincipalSearchFilter` object. このメソッドは、各要素が `MyArrayOfUser` オブジェクトであるコレクションオブジェクトを返 `User` します。 コレクションを繰り返し `MyArrayOfUser` 実行し、ユーザーを検索します。

**関連トピック**

[手順の概要](users.md#summary-of-steps)

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## ユーザーの削除 {#deleting-users}

Directory Manager Service API（JavaおよびWebサービス）を使用して、AEM Formsからユーザーをプログラム的に削除できます。 ユーザーを削除すると、そのユーザーは、ユーザーを必要とするサービス操作を実行するために使用できなくなります。 例えば、削除したユーザーにタスクを割り当てることはできません。

### 手順の概要 {#summary_of_steps-1}

ユーザーを削除するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. DirectoryManagerServiceクライアントを作成します。
1. 削除するユーザーを指定します。
1. AEM Formsからユーザーを削除します。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを含めます。

**DirectoryManagerServiceクライアントの作成**

プログラムでDirectory Manager Service API操作を実行する前に、Directory Managerサービスクライアントを作成します。

**削除するユーザーの指定**

ユーザーの識別子の値を使用して、削除するユーザーを指定できます。

**AEM Formsからのユーザーの削除**

ユーザーを削除するには、オブジェクトの `DirectoryManagerServiceClient` メソッドを呼び出 `deleteLocalUser` します。

**関連トピック**

[Java APIを使用したユーザーの削除](users.md#delete-users-using-the-java-api)

[WebサービスAPIを使用したユーザーの削除](users.md#delete-users-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[ユーザーの追加](users.md#adding-users)

### Java APIを使用したユーザーの削除 {#delete-users-using-the-java-api}

Directory Manager Service API(Java)を使用してユーザーを削除します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-usermanager-client.jarなどのクライアントJARファイルを含めます。

1. DirectoryManagerServiceクライアントを作成します。

   コンストラク `DirectoryManagerServiceClient` ターを使用し、接続プロパティを含むオブジェクトを渡 `ServiceClientFactory` して、オブジェクトを作成します。

1. 削除するユーザーを指定します。

   * コンストラクタを使用して `PrincipalSearchFilter` オブジェクトを作成します。
   * オブジェクトのメソッドを呼び出して、ユー `PrincipalSearchFilter` ザー識別子の値を設 `setUserId` 定します。 ユーザー識別子の値を表すstring値を渡します。
   * Invoke the `DirectoryManagerServiceClient` object’s `findPrincipals` method and pass the `PrincipalSearchFilter` object. このメソッドは、各要素 `java.util.List` がオブジェクトであるインスタンスを返 `User` します。 インスタンスを繰 `java.util.List` り返し処理して、削除するユーザーを検索します。

1. AEM Formsからユーザーを削除します。

   オブジェクト `DirectoryManagerServiceClient` のメソッドを `deleteLocalUser` 呼び出し、オブジェクトのフィー `User` ルドの値を渡 `oid` します。 オブジェクト `User` のメソッドを呼び出 `getOid` します。 インスタンスか `User` ら取得したオブジェクトを使 `java.util.List` 用します。

**関連トピック**

[手順の概要](users.md#summary-of-steps)

[クイックスタート（EJBモード）:Java APIを使用したユーザの削除](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-deleting-users-using-the-java-api)

[クイックスタート（SOAPモード）:Java APIを使用したユーザの削除](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-deleting-users-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したユーザーの削除 {#delete-users-using-the-web-service-api}

Directory Manager Service API（Webサービス）を使用してユーザーを削除します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-usermanager-client.jarなどのクライアントJARファイルを含めます。

1. DirectoryManagerServiceクライアントを作成します。

   * Create a `DirectoryManagerServiceClient` object by using its default constructor.
   * Create a `DirectoryManagerServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/DirectoryManagerService?blob=mtom`)に渡すstring値。 属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます。 必ず `blob=mtom.`
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `DirectoryManagerServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当てま `DirectoryManagerServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `DirectoryManagerServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. 削除するユーザーを指定します。

   * コンストラクタを使用して `PrincipalSearchFilter` オブジェクトを作成します。
   * オブジェクトのフィールドに文字列値を割り当てて、ユー `PrincipalSearchFilter` ザー識別子の値を設 `userId` 定します。
   * Invoke the `DirectoryManagerServiceClient` object’s `findPrincipals` method and pass the `PrincipalSearchFilter` object. このメソッドは、各要素が `MyArrayOfUser` オブジェクトであるコレクションオブジェクトを返 `User` します。 コレクションを繰り返し `MyArrayOfUser` 実行し、ユーザーを検索します。 コレクション `User` オブジェクトから取得さ `MyArrayOfUser` れたオブジェクトは、ユーザーの削除に使用されます。

1. AEM Formsからユーザーを削除します。

   オブジェクトのフィールド値を `User` オブジェクトのメ `oid` ソッドに渡して、 `DirectoryManagerServiceClient` ユーザーを削 `deleteLocalUser` 除します。

**関連トピック**

[手順の概要](users.md#summary-of-steps)

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## グループの作成 {#creating-groups}

Directory Manager Service API（JavaおよびWebサービス）を使用して、AEM Formsグループをプログラム的に作成できます。 グループを作成した後、そのグループを使用して、グループを必要とするサービス操作を実行できます。 例えば、新しいグループにユーザーを割り当てることができます。 (「ユーザ [ーとグループの管理](users.md#managing-users-and-groups)」を参照)。

### 手順の概要 {#summary_of_steps-2}

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
* adobe-utilities.jar（AEM FormsがJBossにデプロイされている場合に必須）
* jbossall-client.jar（AEM FormsがJBossにデプロイされている場合は必須）

For information about the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**DirectoryManagerServiceクライアントの作成**

プログラムでDirectory Managerサービス操作を実行する前に、Directory Manager Service APIクライアントを作成します。

**グループが存在するかどうかの確認**

グループを作成する場合は、そのグループが同じドメインに存在しないことを確認します。 つまり、2つのグループが同じドメイン内で同じ名前を持つことはできません。 このタスクを実行するには、検索を実行し、2つの値に基づいて検索結果をフィルタリングします。 プリンシパルタイプをに設定して、 `com.adobe.idp.um.api.infomodel.Principal.PRINCIPALTYPE_GROUP` グループのみが返されるようにします。 また、ドメイン名を必ず指定してください。

**グループの作成**

グループがドメインに存在しないと判断したら、グループを作成し、次の属性を指定します。

* **共通名**:グループの名前。
* **ドメイン**:グループが追加されるドメイン。
* **説明**:グループの説明。

**グループに対するアクションの実行**

グループを作成した後、そのグループを使用してアクションを実行できます。 例えば、ユーザーをグループに追加できます。 ユーザーをグループに追加するには、ユーザーとグループの両方の一意の識別子の値を取得します。 これらの値をメソッドに渡 `addPrincipalToLocalGroup` します。

**関連トピック**

[Java APIを使用したグループの作成](users.md#create-groups-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[ユーザーの追加](users.md#adding-users)

[ユーザーの削除](users.md#deleting-users)

### Java APIを使用したグループの作成 {#create-groups-using-the-java-api}

Directory Manager Service API(Java)を使用してグループを作成します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-usermanager-client.jarなどのクライアントJARファイルを含めます。

1. DirectoryManagerServiceクライアントを作成します。

   コンストラク `DirectoryManagerServiceClient` ターを使用し、接続プロパティを含むオブジェクトを渡 `ServiceClientFactory` して、オブジェクトを作成します。

1. グループが存在するかどうかを確認します。

   * コンストラクタを使用して `PrincipalSearchFilter` オブジェクトを作成します。
   * オブジェクトのオブジェクトを呼び出して、プ `PrincipalSearchFilter` リンシパルタイプを設 `setPrincipalType` 定します。 値を渡します `com.adobe.idp.um.api.infomodel.Principal.PRINCIPALTYPE_GROUP`。
   * オブジェクトのオブジェクトを呼び出し `PrincipalSearchFilter` て、ドメインを設 `setSpecificDomainName` 定します。 ドメイン名を指定するstring値を渡します。
   * グループを検索するには、オブジェクトの `DirectoryManagerServiceClient` メソッドを呼び出し `findPrincipals` ます（プリンシパルはグループにすることができます）。 プリンシパル `PrincipalSearchFilter` の種類とドメイン名を指定するオブジェクトを渡します。 このメソッドは、各要素 `java.util.List` がインスタンスであるインスタンスを返 `Group` します。 各グループインスタンスは、オブジェクトを使用して指定されたフィルタに準拠 `PrincipalSearchFilter` します。
   * インスタンスを繰り返 `java.util.List` し処理します。 各要素に対して、グループ名を取得します。 グループ名が新しいグループ名と等しくないことを確認します。

1. グループを作成します。

   * グループが存在しない場合は、オブジェクトの `Group` メソッドを呼び出 `setCommonName` し、グループ名を指定するstring値を渡します。
   * オブジェクト `Group` のメソッドを `setDescription` 呼び出し、グループの説明を指定するstring値を渡します。
   * オブジェクト `Group` のメソッドを `setDomainName` 呼び出し、ドメイン名を指定するstring値を渡します。
   * Invoke the `DirectoryManagerServiceClient` object’s `createLocalGroup` method and pass the `Group` instance.
   このメ `createLocalUser` ソッドは、ローカルユーザー識別子の値を指定するstring値を返します。

1. グループに対してアクションを実行します。

   * コンストラクタを使用して `PrincipalSearchFilter` オブジェクトを作成します。
   * オブジェクトのメソッドを呼び出して、ユー `PrincipalSearchFilter` ザー識別子の値を設 `setUserId` 定します。 ユーザー識別子の値を表すstring値を渡します。
   * Invoke the `DirectoryManagerServiceClient` object’s `findPrincipals` method and pass the `PrincipalSearchFilter` object. このメソッドは、各要素 `java.util.List` がオブジェクトであるインスタンスを返 `User` します。 インスタンスを繰り `java.util.List` 返し実行し、ユーザーを検索します。
   * オブジェクトのメソッドを呼び出して、ユーザーを `DirectoryManagerServiceClient` グループに追加 `addPrincipalToLocalGroup` します。 オブジェクトのメソッドの `User` 戻り値を渡し `getOid` ます。 オブジェクトのメソッドの戻 `Group` り値を渡しま `getOid` す(新しいグ `Group` ループを表すインスタンスを使用)。

**関連トピック**

[手順の概要](users.md#summary-of-steps)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## ユーザーとグループの管理 {#managing-users-and-groups}

このトピックでは、(Java)を使用して、ドメイン、ユーザーおよびグループをプログラムによって割り当て、削除、およびクエリする方法について説明します。

>[!NOTE]
>
>ドメインを設定する場合は、グループとユーザーの一意の識別子を設定する必要があります。 選択する属性は、LDAP環境内で一意である必要があるだけでなく、不変である必要があり、ディレクトリ内で変更されることはありません。 また、この属性は単純な文字列データ型である必要があります(Active Directory 2000/2003では、現在唯一の例外はバイナリ `"objectsid"`値であるためです)。 例えば、Novell eDirectory属 `"GUID"`性は単純な文字列データ型ではないので、機能しません。

* Active Directoryの場合は、を使用しま `"objectsid"`す。
* SunOneの場合は、を使用しま `"nsuniqueid"`す。

>[!NOTE]
>
>LDAPディレクトリ同期の進行中に複数のローカルユーザーおよびグループを作成することはサポートされていません。 この処理を試みると、エラーが発生します。

### 手順の概要 {#summary_of_steps-3}

ユーザーとグループを管理するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. DirectoryManagerServiceクライアントを作成します。
1. 適切なユーザー操作またはグループ操作を呼び出します。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

**DirectoryManagerServiceクライアントの作成**

Directory Managerサービス操作をプログラムで実行する前に、Directory Managerサービスクライアントを作成する必要があります。 Java APIを使用すると、オブジェクトを作成することで実現で `DirectoryManagerServiceClient` きます。 WebサービスAPIを使用すると、オブジェクトを作成することで実現で `DirectoryManagerServiceService` きます。

**適切なユーザー操作またはグループ操作の呼び出し**

サービスクライアントを作成したら、ユーザー管理操作またはグループ管理操作を呼び出すことができます。 サービスクライアントでは、ドメイン、ユーザー、グループの割り当て、削除、およびクエリを実行できます。 ディレクトリプリンシパルまたはローカルプリンシパルをローカルグループに追加することは可能ですが、ローカルプリンシパルをディレクトリグループに追加することはできません。

**関連トピック**

[Java APIを使用したユーザーとグループの管理](users.md#managing-users-and-groups-using-the-java-api)

[WebサービスAPIを使用したユーザーとグループの管理](users.md#managing-users-and-groups-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[User Manager APIクイックスタート](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

### Java APIを使用したユーザーとグループの管理 {#managing-users-and-groups-using-the-java-api}

(Java)を使用してユーザー、グループおよびドメインをプログラムで管理するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-usermanager-client.jarなどのクライアントJARファイルを含めます。 これらのファイルの場所については、[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。

1. DirectoryManagerServiceクライアントを作成します。

   コンストラク `DirectoryManagerServiceClient` ターを使用し、接続プロパティを含むオブジェクトを渡 `ServiceClientFactory` して、オブジェクトを作成します。 詳しくは、接続プロパティ [の設定を参照してくださ](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)*い。*

1. 適切なユーザー操作またはグループ操作を呼び出します。

   ユーザーまたはグループを検索するには、オブジェクトのプリンシパルを検索す `DirectoryManagerServiceClient` るメソッドの1つを呼び出します（プリンシパルはユーザーまたはグループにすることができます）。 次の例では、メソッドは検索 `findPrincipals` フィルター（オブジェクト）を使用して呼び出 `PrincipalSearchFilter` されます。

   この場合の戻り値は含まれるオブジェクトなので、 `java.util.List` 結果を繰り返 `Principal` し処理し、またはのいずれかのオブジ `Principal` ェクトにキャ `User` ストし `Group` ます。

   (両方ともインタ `User` ーフェイ `Group` スから継承する)結果またはオブジェ `Principal` クトを使用して、ワークフローで必要な情報を取得します。 例えば、ドメイン名と正規名の値を組み合わせて、プリンシパルを一意に識別します。 これらは、オブジェクトのメソッドと `Principal` メソッドをそれぞれ呼 `getDomainName` び出して `getCanonicalName` 取得されます。

   ローカルユーザーを削除するには、オブジェクト `DirectoryManagerServiceClient` のメソッドを呼び `deleteLocalUser` 出し、ユーザーのIDを渡します。

   ローカルグループを削除するには、オブジェクト `DirectoryManagerServiceClient` のメソッドを呼 `deleteLocalGroup` び出し、グループの識別子を渡します。

**関連トピック**

[手順の概要](users.md#summary-of-steps)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したユーザーとグループの管理 {#managing-users-and-groups-using-the-web-service-api}

Directory Manager Service API（Webサービス）を使用してユーザー、グループおよびドメインをプログラムで管理するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。

   * Directory Manager WSDLを使用するMicrosoft .NETクライアントアセンブリを作成します。 (「Base64エンコ [ーディングを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)」を参照)。
   * Microsoft .NETクライアントアセンブリを参照します。 (Base64エンコ [ーディングを使用した.NETクライアントアセンブリの作成を参照](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding))。

1. DirectoryManagerServiceクライアントを作成します。

   プロキシクラ `DirectoryManagerServiceService` スのコンストラクターを使用してオブジェクトを作成します。

1. 適切なユーザー操作またはグループ操作を呼び出します。

   ユーザーまたはグループを検索するには、オブジェクトのプリンシパルを検索す `DirectoryManagerServiceService` るメソッドの1つを呼び出します（プリンシパルはユーザーまたはグループにすることができます）。 次の例では、メソッドは検索 `findPrincipalsWithFilter` フィルター（オブジェクト）を使用して呼び出 `PrincipalSearchFilter` されます。 オブジェクトを使 `PrincipalSearchFilter` 用する場合、ローカルプリンシパルは、プロパティがに設定さ `isLocal` れている場合にのみ返されま `true`す。 この動作は、Java APIで発生する動作とは異なります。

   >[!NOTE]
   >
   >検索フィルターで検索結果の最大数が指定されていない場合は(フィー `PrincipalSearchFilter.resultsMax` ルドを通して)、最大1,000件の結果が返されます。 これは、Java APIを使用した場合と異なる動作です。Java APIの結果はデフォルトの最大数で10件です。 また、検索フィルターで検索結果の最大数が指定されていない限り（例えば、フィールドを通して）、などの検索方法を使用しても結果は得られ `findGroupMembers``GroupMembershipSearchFilter.resultsMax` ません。 これは、クラスから継承するすべての検索フィルターに適用さ `GenericSearchFilter` れます。 For more information, see [AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

   この場合の戻り値は含まれるオブジェクトなの `object[]` で、結 `Principal` 果を繰り返し処理し、オブジェクトをまた `Principal` はにキャ `User` ストし `Group` ます。

   (両方ともインタ `User` ーフェイ `Group` スから継承する)結果またはオブジェ `Principal` クトを使用して、ワークフローで必要な情報を取得します。 例えば、ドメイン名と正規名の値を組み合わせて、プリンシパルを一意に識別します。 これらは、オブジェクトのフィールドを呼 `Principal` び出すことによ `domainName` って取 `canonicalName` 得されます。

   ローカルユーザーを削除するには、オブジェクト `DirectoryManagerServiceService` のメソッドを呼び `deleteLocalUser` 出し、ユーザーのIDを渡します。

   ローカルグループを削除するには、オブジェクト `DirectoryManagerServiceService` のメソッドを呼 `deleteLocalGroup` び出し、グループの識別子を渡します。

**関連トピック**

[手順の概要](users.md#summary-of-steps)

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## ロールと権限の管理 {#managing-roles-and-permissions}

このトピックでは、Authorization Manager Service API (Java)を使用して、役割と権限をプログラム的に割り当て、削除、決定する方法について説明します。

AEM Formsでは、ロールは ** 1つ以上のシステムレベルのリソースにアクセスするための権限のグループです。 これらの権限は、User Managementを通じて作成され、サービスコンポーネントによって適用されます。 例えば、管理者が「ポリシーセット作成者」の役割をユーザーのグループに割り当てることができます。 その後、Rights Managementは、そのロールを持つグループのユーザーに対して、管理コンソールからポリシーセットを作成することを許可します。

役割には2種類あります。デフォ *ルトの役割* とカ *スタム役割*。 デフォルトのロ&#x200B;*ール（システムロール）* は、AEM Formsに既に常駐しています。 デフォルトのロールは管理者が削除または変更できないので、不変であると想定されます。 管理者が作成したカスタムロールは、その後変更または削除する場合があるので、変更できます。

役割を使用すると、権限の管理が容易になります。 ロールがプリンシパルに割り当てられると、そのプリンシパルに一連の権限が自動的に割り当てられ、プリンシパルに関する特定のアクセス関連のすべての決定は、割り当てられた権限のセット全体に基づいて行われます。

### 手順の概要 {#summary_of_steps-4}

ロールと権限を管理するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. AuthorizationManagerServiceクライアントを作成します。
1. 適切なロール操作または権限操作を呼び出します。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

**AuthorizationManagerServiceクライアントの作成**

User Management AuthorizationManagerService操作をプログラムで実行する前に、AuthorizationManagerServiceクライアントを作成する必要があります。 Java APIを使用すると、オブジェクトを作成することで実現で `AuthorizationManagerServiceClient` きます。

**適切なロール操作または権限操作を呼び出します**

サービスクライアントを作成したら、ロール操作または権限操作を呼び出すことができます。 サービスクライアントでは、ロールと権限を割り当て、削除、決定できます。

**関連トピック**

[Java APIを使用したロールと権限の管理](users.md#managing-roles-and-permissions-using-the-java-api)

[WebサービスAPIを使用したロールと権限の管理](users.md#managing-roles-and-permissions-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[User Manager APIクイックスタート](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

### Java APIを使用したロールと権限の管理 {#managing-roles-and-permissions-using-the-java-api}

Authorization Manager Service API (Java)を使用してロールと権限を管理するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-usermanager-client.jarなどのクライアントJARファイルを含めます。

1. AuthorizationManagerServiceクライアントを作成します。

   コンストラク `AuthorizationManagerServiceClient` ターを使用し、接続プロパティを含むオブジェクトを `ServiceClientFactory` 渡して、オブジェクトを作成します。

1. 適切なロール操作または権限操作を呼び出します。

   プリンシパルにロールを割り当てるには、オブジェクトの `AuthorizationManagerServiceClient` メソッドを呼び出 `assignRole` し、次の値を渡します。

   * ロール `java.lang.String` 識別子を含むオブジェクト
   * プリンシパルIDを `java.lang.String` 含むオブジェクトの配列です。
   プリンシパルからロールを削除するには、オブジェクトの `AuthorizationManagerServiceClient` メソッドを呼び出 `unassignRole` し、次の値を渡します。

   * ロール `java.lang.String` 識別子を含むオブジェクトです。
   * プリンシパルIDを `java.lang.String` 含むオブジェクトの配列です。


**関連トピック**

[手順の概要](users.md#summary-of-steps)

[クイックスタート（SOAPモード）:Java APIを使用したロールと権限の管理](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-managing-roles-and-permissions-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したロールと権限の管理 {#managing-roles-and-permissions-using-the-web-service-api}

Authorization Manager Service API （Webサービス）を使用して、役割と権限を管理します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/AuthorizationManagerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. AuthorizationManagerServiceクライアントを作成します。

   * デフォルトのコンス `AuthorizationManagerServiceClient` トラクターを使用して、オブジェクトを作成します。
   * コンストラクタ `AuthorizationManagerServiceClient.Endpoint.Address` ーを使用してオブジェクトを作 `System.ServiceModel.EndpointAddress` 成します。 WSDLを指定するstring値をAEM Formsサービスに渡します(例 `http://localhost:8080/soap/services/AuthorizationManagerService?blob=mtom`:)。属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます。
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `AuthorizationManagerServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当てま `AuthorizationManagerServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `AuthorizationManagerServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. 適切なロール操作または権限操作を呼び出します。

   プリンシパルにロールを割り当てるには、オブジェクトの `AuthorizationManagerServiceClient` メソッドを呼び出 `assignRole` し、次の値を渡します。

   * ロール `string` 識別子を含むオブジェクト
   * プリンシパル `MyArrayOf_xsd_string` 識別子を含むオブジェクトです。
   プリンシパルからロールを削除するには、オブジェクトの `AuthorizationManagerServiceService` メソッドを呼び出 `unassignRole` し、次の値を渡します。

   * ロール `string` 識別子を含むオブジェクトです。
   * プリンシパルIDを `string` 含むオブジェクトの配列です。


**関連トピック**

[手順の概要](users.md#summary-of-steps)

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## ユーザーの認証 {#authenticating-users}

このトピックでは、Authentication Manager Service API(Java)を使用して、クライアントアプリケーションでユーザーをプログラム的に認証する方法について説明します。

ユーザー認証は、セキュリティで保護されたデータを保存するエンタープライズデータベースや他のエンタープライズリポジトリとやり取りする際に必要になる場合があります。

例えば、ユーザーがWebページにユーザー名とパスワードを入力し、FormsをホストするJ2EEアプリケーションサーバーに値を送信するシナリオを考えてみましょう。 Formsカスタムアプリケーションは、Authentication Managerサービスを使用してユーザーを認証できます。

認証が成功した場合、アプリケーションは保護されたエンタープライズデータベースにアクセスします。 それ以外の場合は、そのユーザーが許可されたユーザーではないことを示すメッセージがユーザーに送信されます。

次の図に、アプリケーションのロジックフローを示します。

![au_au_uauth_process](assets/au_au_umauth_process.png)

次の表に、この図の手順を示します。

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
   <td><p>ユーザはウェブサイトにアクセスし、ユーザ名とパスワードを指定する。 この情報は、AEM formsをホストするJ2EEアプリケーションサーバーに送信されます。</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>ユーザー資格情報はAuthentication Managerサービスで認証されます。 ユーザーの資格情報が有効な場合、ワークフローは手順3に進みます。 それ以外の場合は、そのユーザーが許可されたユーザーではないことを示すメッセージがユーザーに送信されます。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>ユーザー情報とフォームデザインは、セキュリティで保護されたエンタープライズデータベースから取得されます。 </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>ユーザー情報がフォームデザインとマージされ、フォームがユーザーにレンダリングされます。 </p></td>
  </tr>
 </tbody>
</table>

### 手順の概要 {#summary_of_steps-5}

プログラムでユーザーを認証するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. AuthenticationManagerServiceクライアントを作成します。
1. 認証操作を呼び出します。
1. 必要に応じて、コンテキストを取得し、クライアントアプリケーションが認証用に別のAEM Formsサービスに転送できるようにします。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

**AuthenticationManagerServiceクライアントの作成**

プログラムでユーザーを認証する前に、AuthenticationManagerServiceクライアントを作成する必要があります。 Java APIを使用する場合は、オブジェクトを作成 `AuthenticationManagerServiceClient` します。

**認証操作の呼び出し**

サービスクライアントを作成したら、認証操作を呼び出すことができます。 この操作には、ユーザーの名前やパスワードなど、ユーザーに関する情報が必要です。 ユーザーが認証されない場合は、例外がスローされます。

**認証コンテキストの取得**

ユーザーを認証したら、認証済みユーザーに基づいてコンテキストを作成できます。 その後、コンテンツを使用して別のAEM Formsサービスを呼び出すことができます。 例えば、コンテキストを使用して、PDFドキュメントを作成し、パ `EncryptionServiceClient` スワードを使用して暗号化することができます。 認証済みのユーザーに、AEM Formsサービスの呼び出しに必要なロ `Services User` ールの名前が付いていることを確認します。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[User Manager APIクイックスタート](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

[PDFドキュメントのパスワードによる暗号化](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Java APIを使用したユーザーの認証 {#authenticate-a-user-using-the-java-api}

Authentication Manager Service API(Java)を使用してユーザーを認証します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-usermanager-client.jarなどのクライアントJARファイルを含めます。

1. AuthenticationManagerServicesクライアントを作成します。

   コンストラク `AuthenticationManagerServiceClient` ターを使用し、接続プロパティを含むオブジェクトを `ServiceClientFactory` 渡して、オブジェクトを作成します。

1. 認証操作を呼び出します。

   オブジェクト `AuthenticationManagerServiceClient` のメソッドを `authenticate` 呼び出し、次の値を渡します。

   * ユー `java.lang.String` ザーの名前を含むオブジェクトです。
   * ユーザーのパスワードを `byte[]` 含むバイト配列（オブジェクト）。 オブジェクトのメソッドを呼 `byte[]` び出して、このオブジ `java.lang.String` ェクトを取得で `getBytes` きます。
   authenticateメソッドは、認証済みユ `AuthResult` ーザーに関する情報を含むオブジェクトを返します。

1. 認証コンテキストを取得します。

   オブジェクト `ServiceClientFactory` のメソッドを呼び `getContext` 出します。このメソッドはオブジェクトを返 `Context` します。

   次に、オブジェクト `Context` のメソッドを呼 `initPrincipal` び出して、を渡しま `AuthResult`す。

### WebサービスAPIを使用したユーザーの認証 {#authenticate-a-user-using-the-web-service-api}

Authentication Manager Service API（Webサービス）を使用してユーザーを認証します。

1. プロジェクトファイルを含めます。

   * Authentication Manager WSDLを使用するMicrosoft .NETクライアント・アセンブリを作成します。 (「Base64エンコ [ーディングを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)」を参照)。
   * Microsoft .NETクライアントアセンブリを参照します。 (『Base64エンコーディングを使用したAEM Formsの呼び出し』の「.NET [クライアントアセンブリの参照](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)」を参照)。

1. AuthenticationManagerServiceクライアントを作成します。

   プロキシクラ `AuthenticationManagerServiceService` スのコンストラクターを使用してオブジェクトを作成します。

1. 認証操作を呼び出します。

   オブジェクト `AuthenticationManagerServiceClient` のメソッドを `authenticate` 呼び出し、次の値を渡します。

   * ユー `string` ザー名を含むオブジェクト
   * ユーザーのパスワードを `byte[]` 含むバイト配列（オブジェクト）。 次の例に示すロジッ `byte[]` クを使用して、パスワ `string` ードを含むオブジェクトを配 `byte[]` 列に変換することで、オブジェクトを取得できます。
   * 戻り値はオブジェクトにな `AuthResult` り、ユーザーに関する情報を取得するために使用できます。 以下の例では、ユーザーの情報を取得するには、最初にオブジェクトのフィールドを取得し、次に結果のオ `AuthResult` ブジェク `authenticatedUser` トのフィールドを取 `User` 得し `canonicalName` ます `domainName` 。

**関連トピック**

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## プログラムによるユーザーの同期 {#programmatically-synchronizing-users}

User Management APIを使用して、プログラムによってユーザーを同期できます。 ユーザーを同期すると、AEM Formsはユーザーリポジトリ内のユーザーデータで更新されます。 例えば、新しいユーザーをユーザーリポジトリに追加するとします。 同期操作を実行すると、新しいユーザーがAEM formsユーザーになります。 また、ユーザーリポジトリに存在しなくなったユーザーはAEM Formsから削除されます。

次の図に、AEM Formsがユーザーリポジトリと同期していることを示します。

![ps_ps_uauth_sync](assets/ps_ps_umauth_sync.png)

次の表に、この図の手順を示します。

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
   <td><p>クライアントアプリケーションが、AEM Formsが同期操作を実行するように要求します。</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>AEM formsは同期操作を実行します。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>ユーザー情報が更新されました。</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>ユーザは、更新されたユーザ情報を表示できる。 </p></td>
  </tr>
 </tbody>
</table>

### 手順の概要 {#summary_of_steps-6}

プログラムによってユーザーを同期するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. UserManagerUtilServiceClientクライアントを作成します。
1. エンタープライズドメインを指定します。
1. 認証操作を呼び出します。
1. 同期操作が完了したかどうかの判断

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

**UserManagerUtilServiceClientclientの作成**

プログラムによってユーザーを同期する前に、オブジェクトを作成する必要があ `UserManagerUtilServiceClient` ります。

**エンタープライズドメインの指定**

User Management APIを使用して同期操作を実行する前に、ユーザーが属するエンタープライズドメインを指定します。 1つ以上のエンタープライズドメインを指定できます。 プログラムによって同期操作を実行する前に、管理コンソールを使用してエンタープライズドメインを設定する必要があります。 (See [administration help](https://www.adobe.com/go/learn_aemforms_admin_63).)

**同期操作の呼び出し**

1つ以上のエンタープライズドメインを指定した後で、同期操作を実行できます。 この操作の実行にかかる時間は、ユーザーリポジトリ内のユーザーレコードの数によって異なります。

**同期操作が完了したかどうかの判断**

プログラムで同期操作を実行した後、操作が完了したかどうかを判断できます。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[User Manager APIクイックスタート](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

[PDFドキュメントのパスワードによる暗号化](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Java APIを使用したプログラムによるユーザーの同期 {#programmatically-synchronizing-users-using-the-java-api}

User Management API(Java)を使用してユーザーを同期します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-usermanager-client.jarやadobe-usermanager-util-client.jarなどのクライアントJARファイルを含めます。

1. UserManagerUtilServiceClientクライアントを作成します。

   コンストラク `UserManagerUtilServiceClient` ターを使用し、接続プロパティを含むオブジェクトを渡 `ServiceClientFactory` して、オブジェクトを作成します。

1. エンタープライズドメインを指定します。

   * オブジェクト `UserManagerUtilServiceClient` のメソッドを呼 `scheduleSynchronization` び出して、ユーザー同期操作を開始します。
   * コンストラクタ `java.util.Set` ーを使用してインスタンスを作 `HashSet` 成します。 データタイプとして指定し `String` ていることを確認します。 このイ `Java.util.Set` ンスタンスは、同期操作が適用されるドメイン名を格納します。
   * 追加するドメイン名ごとに、オブジェクトの `java.util.Set` addメソッドを呼び出し、ドメイン名を渡します。

1. 同期操作を呼び出します。

   オブジェクト `ServiceClientFactory` のメソッドを呼び `getContext` 出します。このメソッドはオブジェクトを返 `Context` します。

   次に、オブジェクト `Context` のメソッドを呼 `initPrincipal` び出して、を渡しま `AuthResult`す。

**関連トピック**

[プログラムによるユーザーの同期](users.md#programmatically-synchronizing-users)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
