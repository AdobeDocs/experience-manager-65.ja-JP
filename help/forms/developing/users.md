---
title: ユーザーの管理
seo-title: Managing Users
description: User Management API を使用して、役割、権限、プリンシパル（ユーザーまたはグループ）を管理し、ユーザーを認証できるクライアントアプリケーションを作成してください。
seo-description: Use the User Management API to create client applications that can manage roles, permissions, and principals (which can be users or groups), as well as authenticate users.
uuid: 68d8a0bc-6e3d-4286-ba5c-534dcf58cb84
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 95804bff-9e6f-4807-aae4-790bd9e7cb57
role: Developer
exl-id: d7c5bb84-a988-4b2e-a587-f4e5b50fea58
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '6228'
ht-degree: 99%

---

# ユーザーの管理 {#managing-users}

**このドキュメントのサンプルと例は、JEE 環境の AEM Forms のみを対象としています。**

**User Management について**

User Management API を使用して、役割、権限、プリンシパル（ユーザーまたはグループ）を管理し、ユーザーを認証できるクライアントアプリケーションを作成できます。User Management API は、次の AEM Forms API で構成されています。

* Directory Manager Service API
* Authentication Manager Service API
* Authorization Manager Service API

User Management では、役割および権限の割り当て、削除、決定が可能です。また、ドメイン、ユーザー、グループの割り当て、削除、問い合わせも可能です。最後に、User Management を使用してユーザーを認証できます。

[ユーザーの追加](users.md#adding-users)では、プログラムによってユーザーを追加する方法を説明します。この節では、Directory Manager Service API を使用します。

[ユーザーの削除](users.md#deleting-users)では、ユーザーをプログラムで削除する方法を説明します。この節では、Directory Manager Service API を使用します。

[ユーザーとグループの管理](users.md#managing-users-and-groups)では、ローカルユーザーとディレクトリユーザーの違いを理解し、Java および web サービス API を使用してユーザーとグループをプログラムで管理する方法の例を確認できます。この節では、Directory Manager Service API を使用します。

[役割と権限の管理](users.md#managing-roles-and-permissions)では、システムの役割と権限、およびそれらを拡張するためにプログラムで実行できる操作について学び、Java および web サービス API を使用して役割と権限をプログラムで管理する方法の例を確認します。この節では、Directory Manager Service API と Authorization Manager Service API の両方を使用します。

[ユーザーの認証](users.md#authenticating-users)では、Java および web サービス API を使用してプログラムによってユーザーを認証する方法の例が表示されます。この節では、Authorization Manager Service API を使用します。

**認証プロセスについて**

User Management には、組み込みの認証機能が用意されており、独自の認証プロバイダーと接続する機能も備えています。User Management は、認証リクエストを受け取ると（ユーザーがログインを試みるなど）、認証プロバイダーにユーザー情報を渡して認証を行います。User Management は、ユーザーの認証後に認証プロバイダーから結果を受け取ります。

次の図は、ログインを試みるエンドユーザー、User Management、および認証プロバイダー間のやり取りを示しています。

![mu_mu_umauth_process](assets/mu_mu_umauth_process.png)

次の表に、認証プロセスの各ステップを示します。

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
   <td><p>ユーザーが User Management を呼び出すサービスにログインしようとします。ユーザーはユーザー名とパスワードを指定します。 </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>User Management は、ユーザー名とパスワード、および設定情報を認証プロバイダーに送信します。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>認証プロバイダは、ユーザストアに接続し、ユーザを認証します。</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>認証プロバイダーが結果を User Management に返します。</p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>User Management は、ユーザーを製品にログインさせるか、製品へのアクセスを拒否するかのどちらかをします。</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>サーバーのタイムゾーンがクライアントのタイムゾーンと異なる場合、WebSphere Application Server クラスター上の .NET クライアントを使用してネイティブの SOAP スタック上で AEM Forms Generate PDF サービスの WSDL を使用すると、次の User Management 認証エラーが発生する場合があります。

`[com.adobe.idp.um.webservices.WSSecurityHandler] errorCode:12803 errorCodeHEX:0x3203 message:WSSecurityHandler: UM authenticate returns exception : An error was discovered processing the <wsse:Security> header. (WSSecurityEngine: Invalid timestamp The security semantics of message have expired).`

**ディレクトリ管理について**

User Management は、LDAP ディレクトリへの接続をサポートするディレクトリサービスプロバイダ (DirectoryManagerService) と併せてパッケージ化されます。組織で LDAP 以外のリポジトリを使用してユーザーレコードを保存する場合、リポジトリーで使用する独自のディレクトリサービスプロバイダーを作成できます。

ディレクトリサービスプロバイダーは、User Management のリクエスト時に、ユーザーストアからレコードを取得します。User Management は、パフォーマンスを向上させるために、ユーザーおよびグループのレコードをデータベースに定期的にキャッシュします。

ディレクトリサービスプロバイダーを使用して、User Management データベースとユーザーストアを同期できます。このステップでは、すべてのユーザーディレクトリ情報と、すべてのユーザーレコードとグループレコードが最新の状態に保たれます。

また、DirectoryManagerService では、ドメインを作成および管理する機能を提供します。ドメインは、異なるユーザーベースを定義します。ドメインの境界は、通常、組織の構造やユーザーストアの設定方法に従って定義されます。User Management ドメインは、認証プロバイダーおよびディレクトリサービスプロバイダーが使用する設定を提供します。

User Management が書き出す設定 XML で、属性値が `Domains` のルートノードには、User Management 用に定義された各ドメインの XML 要素が含まれます。これらの各要素には、特定のサービスプロバイダーに関連付けられたドメインの側面を定義する他の要素が含まれます。

**objectSID の値について**

Active Directory を使用する場合、 `objectSID` の値は、複数のドメインで一意の属性ではありません。この値は、オブジェクトのセキュリティ識別情報を格納しています。複数ドメイン環境（ドメインのツリーなど）では、 `objectSID` の値は異なる場合があります。

`objectSID` 値は、ある Active Directory ドメインから別のドメインにオブジェクトが移動された場合に変更されます。オブジェクトによっては、ドメイン内のどこにいても同じ`objectSID`値を持つものがあります。例えば、BUILTIN\Administrators、BUILTIN\Power Users などのグループは、ドメインに関係なく同じ `objectSID` 値を持ちます。これらの `objectSID` 値はよく知られています。

## ユーザーの追加 {#adding-users}

Directory Manager Service API（Java および web サービス）を使用すると、ユーザーをプログラムで AEM Forms に追加できます。ユーザーを追加した後、ユーザーを必要とするサービス操作を実行する際に、そのユーザーを使用できます。例えば、新しいユーザーにタスクを割り当てることができます。

### 手順の概要 {#summary-of-steps}

ユーザーを追加するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. DirectoryManagerService クライアントを作成します。
1. ユーザー情報を定義します。
1. AEM Forms にユーザーを追加します。
1. ユーザーが追加されていることを確認します。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを含めます。

**DirectoryManagerService クライアントの作成**

Directory Manager サービスの操作をプログラムで実行する前に、Directory Manager Service API クライアントを作成します。

**ユーザー情報の定義**

Directory Manager Service API を使用して新しいユーザーを追加する場合は、そのユーザーの情報を定義してください。通常、新しいユーザーを追加する場合、次の値を定義します。

* **ドメイン名**：ユーザーが属するドメイン（例：`DefaultDom`）。
* **ユーザー識別情報の値**：ユーザーの識別情報の値（例： `wblue`）。
* **プリンシパルタイプ**：ユーザーのタイプ（例：`USER)`）。
* **名**：ユーザーの名（例：`Wendy`）。
* **姓**：ユーザーの姓（例：`Blue)`）
* **ロケール**：ユーザーのロケール情報。

**AEM Forms へのユーザーの追加**

ユーザー情報を定義した後、そのユーザーを AEM Forms に追加できます。ユーザーを追加するには、`DirectoryManagerServiceClient` オブジェクトの `createLocalUser` メソッドを呼び出してください。

**ユーザーが追加されたことを確認**

ユーザーが追加されたことを確認することにより、問題が発生しなかったことを確認できます。ユーザー識別情報の値を使用して、新しいユーザーを見つけます。

**関連トピック**

[Java API を使用してユーザーを追加する](users.md#add-users-using-the-java-api)

[Web サービス API を使用してユーザーを追加する](users.md#add-users-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[ユーザーの削除](users.md#deleting-users)

### Java API を使用してユーザーを追加する {#add-users-using-the-java-api}

Directory Manager Service API（Java）を使用してユーザーを追加します。

1. プロジェクトファイルを含めます。

   adobe-livecycle-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. DirectoryManagerServices クライアントを作成します。

   コンストラクターを使用して接続プロパティを含む `ServiceClientFactory` オブジェクトを渡すことによって、`DirectoryManagerServiceClient` オブジェクトを作成します。 

1. ユーザー情報を定義します。

   * コンストラクターを使用して `UserImpl` オブジェクトを作成します。
   * `UserImpl` オブジェクトの `setDomainName` メソッドを呼び出して、ドメイン名を設定します。ドメイン名を指定する文字列値を渡します。
   * `UserImpl` オブジェクトの `setPrincipalType` メソッドを呼び出して、プリンシパルタイプを設定します。ユーザーのタイプを指定する文字列値を渡します。例えば、`USER` を指定できます。
   * `UserImpl` オブジェクトの `setUserid` メソッドを呼び出して、ユーザー識別子の値を設定します。ユーザー識別子の値を指定する文字列値を渡します。例えば、`wblue` を指定できます。
   * `UserImpl` オブジェクトの `setCanonicalName` メソッドを呼び出して、正規名を設定します。ユーザーの正規名を指定する文字列値を渡します。例えば、`wblue` を指定できます。
   * `UserImpl` オブジェクトの `setGivenName` メソッドを呼び出して、名前を設定します。ユーザーの名前を指定する文字列値を渡します。例えば、`Wendy` を指定できます。
   * `UserImpl` オブジェクトの `setFamilyName` メソッドを呼び出して、姓を設定します。ユーザーの姓を指定する文字列値を渡します。例えば、`Blue` を指定できます。

   >[!NOTE]
   >
   >`UserImpl` オブジェクトに属するメソッドを呼び出して他の値を設定します。例えば、 `UserImpl` オブジェクトの `setLocale` メソッドを呼び出して、ロケール値を設定できます。

1. ユーザーを AEM Forms に追加します。

   `DirectoryManagerServiceClient` オブジェクトの `createLocalUser` メソッドを呼び出して、以下の値を渡します。

   * 新しいユーザーを表す `UserImpl` オブジェクト
   * ユーザーのパスワードを表す文字列値

   この `createLocalUser` メソッドは、ローカルユーザー ID の値を指定する文字列値を返します。

1. ユーザーが追加されたことを確認します。

   * コンストラクタを使用して `PrincipalSearchFilter` オブジェクトを作成します。
   * `PrincipalSearchFilter` オブジェクトの `setUserId` メソッドを呼び出して、ユーザー識別子の値を設定します。ユーザー ID の値を表す文字列値を渡します。
   * `DirectoryManagerServiceClient` オブジェクトの `findPrincipals` メソッドを呼び出し、`PrincipalSearchFilter` オブジェクトを渡します。このメソッドは、 `java.util.List` インスタンス（各要素は `User` オブジェクト）を返します。`java.util.List` インスタンスを繰り返し、ユーザーを特定します。

**関連トピック**

[手順の概要](users.md#summary-of-steps)

[クイックスタート（SOAP モード）：Java API を使用したユーザーの追加](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-adding-users-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用してユーザーを追加する {#add-users-using-the-web-service-api}

Directory Manager サービス API（web サービス）を使用してユーザーを追加します。

1. プロジェクトファイルを含めます。

   MTOM を使用する Microsoft .NET プロジェクトを作成します。サービス参照に WSDL 定義 `http://localhost:8080/soap/services/DirectoryManagerService?WSDL&lc_version=9.0.1` を使用していることを確認してください。

   >[!NOTE]
   >
   >`localhost` を、AEM Forms をホストするサーバーの IP アドレスで置換します。

1. DirectoryManagerService クライアントを作成します。

   * デフォルトのコンストラクターを使用して `DirectoryManagerServiceClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して`DirectoryManagerServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を 指定する文字列値を AEM Forms サービスに渡します（例：`http://localhost:8080/soap/services/DirectoryManagerService?blob=mtom`）。`lc_version` 属性を使用する必要はありません。この属性は、サービス参照を作成する際に使用されます。`?blob=mtom` を指定するようにしてください。
   * `DirectoryManagerServiceClient.Endpoint.Binding` フィールドの値を取得して、`System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` フィールドを `WSMessageEncoding.Mtom` に設定します。この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `DirectoryManagerServiceClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms ユーザー名を割り当てます。
      * 対応するパスワード値を `DirectoryManagerServiceClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` を`BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに割り当てます。
      * 定数値 `BasicHttpSecurityMode.TransportCredentialOnly` をフィールド `BasicHttpBindingSecurity.Security.Mode` に割り当てます。

1. ユーザー情報を定義します。

   * コンストラクターを使用して `UserImpl` オブジェクトを作成します。
   * デフォルト名を設定するには、`UserImpl` オブジェクトの `domainName` フィールドに文字列値を割り当てます。
   * プリンシパルタイプを設定するには、`UserImpl` オブジェクトの `principalType` フィールドに文字列値を割り当てます。例えば、`USER` を指定できます。
   * ユーザー ID の値を設定するには、`UserImpl` オブジェクトの `userid` フィールドに文字列値を割り当てます。
   * 正規名の値を設定するには、`UserImpl` オブジェクトの `canonicalName` フィールドに文字列値を割り当てます。
   * 指定された名前の値を設定するには、`UserImpl` オブジェクトの `givenName` フィールドに文字列値を割り当てます。
   * 姓の値を設定するには、`UserImpl` オブジェクトの `familyName` フィールドに文字列値を割り当てます。

1. AEM Forms にユーザーを追加します。

   `DirectoryManagerServiceClient` オブジェクトの `createLocalUser` メソッドを呼び出して、以下の値を渡します。

   * 新しいユーザーを表す `UserImpl` オブジェクト
   * ユーザーのパスワードを表す文字列値

   この `createLocalUser` メソッドは、ローカルユーザー ID の値を指定する文字列値を返します。

1. ユーザーが追加されたことを確認します。

   * コンストラクターを使用して `PrincipalSearchFilter` オブジェクトを作成します。
   * ユーザー ID の値を設定するには、`PrincipalSearchFilter` オブジェクトの `userId` フィールドにユーザー ID の値を表す文字列値を割り当てます。
   * `DirectoryManagerServiceClient` オブジェクトの `findPrincipals` メソッドを呼び出し、`PrincipalSearchFilter` オブジェクトを渡します。このメソッドは、`MyArrayOfUser` コレクションオブジェクト（各要素は `User` オブジェクト）を返します。`MyArrayOfUser` コレクションを反復処理して、ユーザーを特定します。

**関連トピック**

[手順の概要](users.md#summary-of-steps)

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## ユーザーの削除 {#deleting-users}

Directory Manager Service API（Java および web サービス）を使用して、AEM Forms からユーザーをプログラムで削除できます。ユーザーを削除すると、そのユーザーはユーザーを必要とするサービス操作を実行できなくなります。例えば、削除されたユーザーにタスクを割り当てることはできません。

### 手順の概要 {#summary_of_steps-1}

ユーザーを削除するには、以下の手順に従います。

1. プロジェクトファイルを含めます。
1. DirectoryManagerService クライアントを作成します。
1. 削除するユーザーを指定します。
1. AEM Forms からユーザーを削除します。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを含めます。

**DirectoryManagerService クライアントの作成**

Directory Manager Service API 操作をプログラムで実行する前に、Directory Manager サービスクライアントを作成します。

**削除するユーザーの指定**

ユーザー ID の値を使用して、削除するユーザーを指定できます。

**AEM Forms からのユーザーの削除**

ユーザーを削除するには、`DirectoryManagerServiceClient` オブジェクトの `deleteLocalUser` メソッドを呼び出します。

**関連トピック**

[Java API を使用したユーザーの削除](users.md#delete-users-using-the-java-api)

[Web サービス API を使用したユーザーの削除](users.md#delete-users-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[ユーザーの追加](users.md#adding-users)

### Java API を使用したユーザーの削除 {#delete-users-using-the-java-api}

Directory Manager Service API（Java）を使用してユーザーを削除します。

1. プロジェクトファイルを含めます。

   adobe-livecycle-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. DirectoryManagerService クライアントを作成します。

   コンストラクタを使用し、接続プロパティを含む `ServiceClientFactory` オブジェクトを渡すことで、`DirectoryManagerServiceClient` オブジェクトを作成します。

1. 削除するユーザーを指定します。

   * コンストラクタを使用して `PrincipalSearchFilter` オブジェクトを作成します。
   * `PrincipalSearchFilter` オブジェクトの `setUserId` メソッドを呼び出して、ユーザー識別子の値を設定します。ユーザー ID の値を表す文字列値を渡します。
   * `DirectoryManagerServiceClient` オブジェクトの `findPrincipals` メソッドを呼び出し、`PrincipalSearchFilter` オブジェクトを渡します。このメソッドは、`java.util.List` インスタンスを返します。このインスタンスの各要素は `User` オブジェクトです。`java.util.List` インスタンスを繰り返し、削除するユーザーを特定します。

1. AEM Forms からユーザーを削除します。

   `DirectoryManagerServiceClient` オブジェクトの `deleteLocalUser` メソッドを呼び出して、`User` オブジェクトの `oid` フィールドの値を渡します。`User` オブジェクトの `getOid` メソッドを呼び出します。`java.util.List` インスタンスから取得した `User` オブジェクトを使用します。

**関連トピック**

[手順の概要](users.md#summary-of-steps)

[クイックスタート（EJB モード）：Java API を使用したユーザーの削除](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-deleting-users-using-the-java-api)

[クイックスタート（SOAP モード）：Java API を使用したユーザーの削除](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-deleting-users-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用したユーザーの削除 {#delete-users-using-the-web-service-api}

Directory Manager Service API（web サービス）を使用してユーザーを削除します。

1. プロジェクトファイルを含めます。

   adobe-livecycle-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. DirectoryManagerService クライアントを作成します。

   * デフォルトのコンストラクターを使用して `DirectoryManagerServiceClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して`DirectoryManagerServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を 指定する文字列値を AEM Forms サービスに渡します（例：`http://localhost:8080/soap/services/DirectoryManagerService?blob=mtom`）。`lc_version` 属性を使用する必要はありません。この属性は、サービス参照を作成する際に使用されます。`blob=mtom.` を指定してください
   * `DirectoryManagerServiceClient.Endpoint.Binding` フィールドの値を取得して、`System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` フィールドを `WSMessageEncoding.Mtom` に設定します。この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `DirectoryManagerServiceClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms ユーザー名を割り当てます。
      * 対応するパスワード値を `DirectoryManagerServiceClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` を`BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに割り当てます。
      * 定数値 `BasicHttpSecurityMode.TransportCredentialOnly` をフィールド `BasicHttpBindingSecurity.Security.Mode` に割り当てます。

1. 削除するユーザーを指定します。

   * コンストラクターを使用して `PrincipalSearchFilter` オブジェクトを作成します。
   * ユーザー ID の値を設定するには、`PrincipalSearchFilter` オブジェクトの `userId` フィールドに文字列値を入力します。
   * `DirectoryManagerServiceClient` オブジェクトの `findPrincipals` メソッドを呼び出し、`PrincipalSearchFilter` オブジェクトを渡します。このメソッドは、`MyArrayOfUser` コレクションオブジェクト（各要素は `User` オブジェクト）を返します。`MyArrayOfUser` コレクションを反復処理して、ユーザーを特定します。`MyArrayOfUser` コレクションオブジェクトから取得した `User` オブジェクトは、ユーザーの削除に使用されます。

1. AEM Forms からユーザーを削除します。

   ユーザーを削除するには、`User` オブジェクトの `oid` フィールド値を `DirectoryManagerServiceClient` オブジェクトの `deleteLocalUser` メソッドに渡します。

**関連トピック**

[手順の概要](users.md#summary-of-steps)

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## グループの作成 {#creating-groups}

Directory Manager Service API（Java および web サービス）を使用して、プログラムによって AEM Forms グループを作成できます。グループを作成したらそのグループを使用して、グループを必要とするサービス操作を実行できます。例えば、ユーザーを新規グループに割り当てることができます（[ユーザーとグループの管理](users.md#managing-users-and-groups)を参照）。

### 手順の概要 {#summary_of_steps-2}

グループを作成するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. DirectoryManagerService クライアントを作成します。
1. グループが存在しないことを確認します。
1. グループを作成します。
1. グループでアクションを実行します。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar（AEM Forms を JBoss にデプロイする場合に必要）
* jbossall-client.jar（AEM Forms が JBoss にデプロイされている場合に必要）

これらのファイルの場所については、[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。

**DirectoryManagerService クライアントの作成**

Directory Manager サービスの操作をプログラムで実行する前に、Directory Manager Service API クライアントを作成します。

**グループが存在するかどうかを判断する**

グループを作成する場合は、そのグループが同じドメインに存在しないことを確認します。つまり、2 つのグループが同じドメイン内で同じ名前を持つことはできません。このタスクを実行するには、検索を実行し、2 つの値に基づいて検索結果をフィルタリングします。プリンシパルタイプを `com.adobe.idp.um.api.infomodel.Principal.PRINCIPALTYPE_GROUP` に設定して、グループのみが返されるようにします。また、ドメイン名を必ず指定してください。

**グループの作成**

ドメインにグループが存在しないと判断したら、グループを作成し、次の属性を指定します。

* **CommonName**：グループの名前。
* **ドメイン**：グループを追加するドメイン。
* **説明**：グループの説明

**グループでのアクションの実行**

グループを作成した後、そのグループを使用してアクションを実行できます。例えば、グループにユーザーを追加できます。グループにユーザーを追加するには、ユーザーとグループの両方で一意の ID 値を取得します。これらの値を `addPrincipalToLocalGroup` メソッドに渡します。

**関連トピック**

[Java API を使用したグループの作成](users.md#create-groups-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[ユーザーの追加](users.md#adding-users)

[ユーザーの削除](users.md#deleting-users)

### Java API を使用したグループの作成 {#create-groups-using-the-java-api}

Directory Manager Service API（Java）を使用してグループを作成します。

1. プロジェクトファイルを含めます。

   adobe-livecycle-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. DirectoryManagerService クライアントを作成します。

   コンストラクターを使用して接続プロパティを含む `ServiceClientFactory` オブジェクトを渡して、`DirectoryManagerServiceClient` オブジェクトを作成します。

1. グループが存在するかどうかを確認します。

   * コンストラクターを使用して `PrincipalSearchFilter` オブジェクトを作成します。
   * `PrincipalSearchFilter` オブジェクトの `setPrincipalType` オブジェクトを呼び出して、プリンシパルタイプを設定します。値 `com.adobe.idp.um.api.infomodel.Principal.PRINCIPALTYPE_GROUP` を渡します。
   * `PrincipalSearchFilter` オブジェクトの `setSpecificDomainName` オブジェクトを呼び出してドメインを設定します。ドメイン名を指定する文字列値を渡します。
   * グループを検索するには、`DirectoryManagerServiceClient` オブジェクトの `findPrincipals` メソッド（プリンシパルはグループにすることができます）を呼び出します。プリンシパルタイプとドメイン名を指定する `PrincipalSearchFilter` オブジェクトを渡します。このメソッドは、各要素が `Group` インスタンスである `java.util.List` インスタンスを返します。各グループインスタンスは、`PrincipalSearchFilter` オブジェクトを使用して指定されたフィルターに準拠しています。
   * `java.util.List` インスタンスを反復処理します。各要素について、グループ名を取得します。グループ名が新しいグループ名と等しくないことを確認します。

1. グループを作成します。

   * グループが存在しない場合は、`Group` オブジェクトの `setCommonName` メソッドを呼び出して、グループ名を指定する文字列値を渡します。
   * `Group` オブジェクトの `setDescription` メソッドを呼び出して、グループの説明を指定する文字列値を渡します。
   * `Group` オブジェクトの `setDomainName` メソッドを呼び出して、ドメイン名を指定する文字列値を渡します。
   * `DirectoryManagerServiceClient` オブジェクトの `createLocalGroup` メソッドを呼び出して、`Group` インスタンスを渡します。

   `createLocalUser` メソッドは、ローカルユーザー ID の値を指定する文字列値を返します。

1. グループでアクションを実行します。

   * コンストラクターを使用して `PrincipalSearchFilter` オブジェクトを作成します。
   * `PrincipalSearchFilter` オブジェクトの `setUserId` メソッドを呼び出して、ユーザー識別子の値を設定します。ユーザー ID の値を表す文字列値を渡します。
   * `DirectoryManagerServiceClient` オブジェクトの `findPrincipals` メソッドを呼び出し、`PrincipalSearchFilter` オブジェクトを渡します。このメソッドは、 `java.util.List` インスタンス（各要素は `User` オブジェクト）を返します。`java.util.List` インスタンスを反復処理して、ユーザーを特定します。
   * `DirectoryManagerServiceClient` オブジェクトの `addPrincipalToLocalGroup` メソッドを呼び出して、グループにユーザーを追加します。`User` オブジェクトの `getOid` メソッドの戻り値を渡します。`Group` オブジェクトの `getOid` メソッドの戻り値を渡します（新しいグループを表す `Group` インスタンスを使用）。

**関連項目**

[手順の概要](users.md#summary-of-steps)

[AEM Forms Java ライブラリファイルの組み込み](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## ユーザーとグループの管理 {#managing-users-and-groups}

このトピックでは、（Java）を使用して、ドメイン、ユーザー、グループをプログラムで割り当て、削除およびクエリする方法について説明します。

>[!NOTE]
>
>ドメインを設定する際は、グループとユーザーに一意の識別子を設定する必要があります。選択する属性は、LDAP 環境内で一意である必要があるだけでなく、不変である必要があり、ディレクトリ内では変更されません。この属性は、単純な文字列データタイプである必要があります（現在、Active Directory 2000／2003で許可されている唯一の例外は `"objectsid"` です。これはバイナリ値です）。例えば、Novell eDirectory 属性 `"GUID"` は単純な文字列データタイプではないので、機能しません。

* Active Directory の場合は、`"objectsid"` を使用します。
* SunOne の場合は、`"nsuniqueid"` を使用します。

>[!NOTE]
>
>LDAP ディレクトリ同期を実行中に複数のローカルユーザーおよびグループを作成することはできません。この処理を試みると、エラーが発生します。

### 手順の概要 {#summary_of_steps-3}

ユーザーとグループを管理するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. DirectoryManagerService クライアントを作成します。
1. 適切なユーザーまたはグループの操作を呼び出します。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めるようにします。

**DirectoryManagerService クライアントの作成**

Directory Manager サービスの操作をプログラムで実行する前に、Directory Manager サービスクライアントを作成する必要があります。Java API では、これは `DirectoryManagerServiceClient` オブジェクトを作成することによって実現できます。Web サービス API では、これは `DirectoryManagerServiceService` オブジェクトを作成することによって実現できます。

**適切なユーザーまたはグループの操作を呼び出す**

サービスクライアントを作成したら、ユーザーまたはグループの管理操作を呼び出すことができます。サービスクライアントでは、ドメイン、ユーザー、グループの割り当て、削除、問い合わせを行うことができます。ディレクトリプリンシパルまたはローカルプリンシパルをローカルグループに追加することは可能ですが、ローカルプリンシパルをディレクトリグループに追加することはできません。

**関連項目**

[Java API を使用したユーザーとグループの管理](users.md#managing-users-and-groups-using-the-java-api)

[Web サービス API を使用したユーザーとグループの管理](users.md#managing-users-and-groups-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[User Manager API クイックスタート](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

### Java API を使用したユーザーとグループの管理 {#managing-users-and-groups-using-the-java-api}

（Java）を使用してユーザー、グループ、ドメインをプログラムで管理するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。

   adobe-livecycle-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。これらのファイルの場所については、[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。

1. DirectoryManagerService クライアントを作成します。

   コンストラクターを使用して、接続プロパティを含む `ServiceClientFactory` オブジェクトを渡すことによって、`DirectoryManagerServiceClient` オブジェクトを作成します。詳しくは、[接続プロパティの設定&#x200B;](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)*を参照してください。*

1. 適切なユーザーまたはグループの操作を呼び出します。

   ユーザーまたはグループを検索するには、プリンシパルを検索する `DirectoryManagerServiceClient` オブジェクトのメソッドのいずれかを呼び出します（プリンシパルはユーザーまたはグループにすることができるためです）。次の例では、`findPrincipals` メソッドは、検索フィルター（`PrincipalSearchFilter` オブジェクト）を使用して呼び出されています。

   この場合の戻り値は `Principal` オブジェクトを含む `java.util.List` であるため、結果を反復処理し、`Principal`オブジェクトを `User` オブジェクトまたは `Group` オブジェクトにキャストします。

   結果の `User` オブジェクトまたは `Group` オブジェクト（両方とも `Principal` インターフェイスから継承）を使用して、ワークフローで必要な情報を取得します。例えば、ドメイン名と正規名の値を組み合わせて、プリンシパルを一意に識別します。これらはそれぞれ `Principal` オブジェクトの `getDomainName` メソッドおよび `getCanonicalName` メソッドを呼び出して取得されます。

   ローカルユーザーを削除するには、`DirectoryManagerServiceClient` オブジェクトの `deleteLocalUser` メソッドを呼び出してユーザーの識別情報を渡します。

   ローカルグループを削除するには、 `DirectoryManagerServiceClient` オブジェクトの `deleteLocalGroup` メソッドを呼び出してグループの識別情報を渡します。

**関連項目**

[手順の概要](users.md#summary-of-steps)

[AEM Forms Java ライブラリファイルの組み込み](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用したユーザーとグループの管理 {#managing-users-and-groups-using-the-web-service-api}

Directory Manager Service API（web サービス）を使用してユーザー、グループ、ドメインをプログラムで管理するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。

   * Directory Manager WSDL を使用するMicrosoft .NET クライアントアセンブリを作成します（[Base64 エンコーディングを使用したAEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)を参照してください）。
   * Microsoft .NET クライアントアセンブリを参照します（[Base64 エンコーディングを使用する .NET クライアントアセンブリの作成](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)を参照してください）。

1. DirectoryManagerService クライアントを作成します。

   プロキシクラスのコンストラクターを使用して、`DirectoryManagerServiceService` オブジェクトを作成します。

1. 適切なユーザーまたはグループの操作を呼び出します。

   ユーザーまたはグループを検索するには、プリンシパルを検索する `DirectoryManagerServiceService` オブジェクトのメソッドのいずれかを呼び出します（プリンシパルはユーザーまたはグループにすることができるためです）。次の例では、`findPrincipalsWithFilter` メソッドは、検索フィルター（`PrincipalSearchFilter` オブジェクト）を使用して呼び出されます。`PrincipalSearchFilter` オブジェクトを使用する場合、ローカルプリンシパルは、`isLocal` プロパティが `true` に設定されている場合のみに返されます。この動作は、Java API で発生する動作とは異なります。

   >[!NOTE]
   >
   >検索フィルターで結果の最大数が `PrincipalSearchFilter.resultsMax` フィールドを介して指定されていない場合、最大 1000 個の結果が返されます。これは、Java API を使用して発生する動作とは異なります。Java API では、結果の数はデフォルトで最大 10 個です。また、`findGroupMembers` などの検索メソッドでは、検索フィルターで（たとえば、`GroupMembershipSearchFilter.resultsMax` フィールドで）結果の最大数が指定されていない場合、結果は得られません。これは、`GenericSearchFilter` クラスから継承されるすべての検索フィルターに適用されます。詳しくは、「[AEM Forms API リフェレンス](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ja)」を参照してください。

   この場合の戻り値は `Principal` オブジェクトを含む `object[]` であるため、結果を反復処理して `Principal` オブジェクトを `User` または `Group` オブジェクトにキャストします。

   結果の `User` オブジェクトまたは `Group` オブジェクト（両方とも `Principal` インターフェイス から継承）を使用して、ワークフローで必要な情報を取得します。例えば、ドメイン名と正規名の値を組み合わせて、プリンシパルを一意に識別します。これらはそれぞれ、`Principal` オブジェクトの `domainName` フィールドおよび `canonicalName` フィールドを呼び出すことによって設定されます。

   ローカルユーザーを削除するには、`DirectoryManagerServiceService` オブジェクトの `deleteLocalUser` メソッドを呼び出してユーザーの識別情報を渡します。

   ローカルグループを削除するには、 `DirectoryManagerServiceService` オブジェクトの `deleteLocalGroup` メソッドを呼び出してグループの識別情報を渡します。

**関連項目**

[手順の概要](users.md#summary-of-steps)

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 役割と権限の管理 {#managing-roles-and-permissions}

このトピックでは、Authorization Manager Service API（Java）を使用して、役割と権限をプログラムで割り当て、削除、決定する方法について説明します。

AEM Forms では、*役割*&#x200B;とは、1 つまたは複数のシステムレベルのリソースにアクセスするための権限のグループです。これらの権限はユーザー管理を通じて作成され、サービスコンポーネントによって適用されます。例えば、管理者は「ポリシーセット作成者」の役割をユーザーのグループに割り当てることができます。Rights Management は、その役割を持つグループのユーザーに対し、管理コンソールを通じてポリシーセットを作成することを許可します。

役割には、*デフォルトロール*&#x200B;および&#x200B;*カスタムロール*&#x200B;の 2 つのタイプがあります。デフォルトロール（*システムロール*）は既に AEM Forms に存在します。デフォルトロールは管理者が削除または変更できないと想定するものであり、不変です。カスタムロールは管理者が作成するものであり、作成後、変更または削除できるので、可変です。

役割を使用すると、権限の管理が容易になります。役割がプリンシパルに割り当てられると、そのプリンシパルに一連の権限が自動的に割り当てられ、プリンシパルに関する特定のアクセス関連の決定はすべて、割り当てられた権限の全体セットに基づいて行われます。

### 手順の概要 {#summary_of_steps-4}

役割と権限を管理するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. AuthorizationManagerService クライアントを作成します。
1. 適切な役割または権限の操作を呼び出します。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めるようにします。

**AuthorizationManagerService クライアントの作成**

User Management AuthorizationManagerService 操作をプログラムで実行する前に、AuthorizationManagerService クライアントを作成する必要があります。Java API では、これは `AuthorizationManagerServiceClient` オブジェクトを作成することによって実現できます。

**適切な役割または権限の操作を呼び出す**

サービスクライアントを作成したら、役割または権限の操作を呼び出すことができます。サービスクライアントを使用すると、役割と権限の割り当て、削除、決定を行うことができます。

**関連項目**

[Java API を使用した役割と権限の管理](users.md#managing-roles-and-permissions-using-the-java-api)

[Web サービス API を使用した役割と権限の管理](users.md#managing-roles-and-permissions-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[User Manager API クイックスタート](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

### Java API を使用した役割と権限の管理 {#managing-roles-and-permissions-using-the-java-api}

Authorization Manager Service API（Java）を使用して役割と権限を管理するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。

   adobe-livecycle-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. AuthorizationManagerService クライアントを作成します。

   コンストラクターを使用し、接続プロパティを含む `ServiceClientFactory` オブジェクトを渡すことにより、`AuthorizationManagerServiceClient` オブジェクトを作成します。

1. 適切な役割または権限の操作を呼び出します。

   プリンシパルに役割を割り当てるには、`AuthorizationManagerServiceClient` オブジェクトの `assignRole` メソッドを呼び出して、次の値を渡します。

   * 役割識別情報を含む `java.lang.String` オブジェクト
   * プリンシパル識別情報を含む `java.lang.String` オブジェクトの配列。

   プリンシパルから役割を削除するには、`AuthorizationManagerServiceClient` オブジェクトの `unassignRole` メソッドを呼び出して、次の値を渡します。

   * 役割識別情報を含む `java.lang.String` オブジェクト。
   * プリンシパル識別情報を含む `java.lang.String` オブジェクトの配列。


**関連項目**

[手順の概要](users.md#summary-of-steps)

[クイックスタート（SOAP モード）：Java API を使用した役割と権限の管理](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-managing-roles-and-permissions-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用した役割と権限の管理 {#managing-roles-and-permissions-using-the-web-service-api}

Authorization Manager Service API（Web サービス）を使用して、役割と権限を管理します。

1. プロジェクトファイルを含めます。

   MTOM を使用する Microsoft .NET プロジェクトを作成します。WSDL 定義 `http://localhost:8080/soap/services/AuthorizationManagerService?WSDL&lc_version=9.0.1` を使用するようにします。

   >[!NOTE]
   >
   >`localhost` を、AEM Forms をホストするサーバーの IP アドレスと置き換えます。

1. AuthorizationManagerService クライアントを作成します。

   * デフォルトのコンストラクターを使用して `AuthorizationManagerServiceClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して、`AuthorizationManagerServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を指定する文字列値を AEM Forms サービスに渡します（例：`http://localhost:8080/soap/services/AuthorizationManagerService?blob=mtom`）。`lc_version` 属性を使用する必要はありません。この属性は、サービス参照を作成する際に使用されます。
   * `AuthorizationManagerServiceClient.Endpoint.Binding` フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` フィールドを `WSMessageEncoding.Mtom` に設定します。この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `AuthorizationManagerServiceClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms ユーザー名を割り当てます。
      * 対応するパスワード値を `AuthorizationManagerServiceClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` を`BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに割り当てます。
      * 定数値 `BasicHttpSecurityMode.TransportCredentialOnly` を `BasicHttpBindingSecurity.Security.Mode` フィールドに割り当てます。

1. 適切な役割または権限の操作を呼び出します。

   プリンシパルに役割を割り当てるには、`AuthorizationManagerServiceClient` オブジェクトの `assignRole` メソッドを呼び出して、次の値を渡します。

   * 役割識別情報を含む `string` オブジェクト
   * プリンシパル識別情報を含む `MyArrayOf_xsd_string` オブジェクト

   プリンシパルから役割を削除するには、`AuthorizationManagerServiceService` オブジェクトの `unassignRole` メソッドを呼び出して、以下の値を渡します。

   * 役割識別情報を含む `string` オブジェクト。
   * プリンシパル識別情報を含む `string` オブジェクトの配列。


**関連項目**

[手順の概要](users.md#summary-of-steps)

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## ユーザーの認証 {#authenticating-users}

このトピックでは、Authentication Manager Service API（Java）を使用して、クライアントアプリケーションがユーザーをプログラムで認証する方法について説明します。

ユーザー認証は、安全なデータを格納するエンタープライズデータベースやその他のエンタープライズリポジトリとやり取りする際に必要になる場合があります。

例えば、ユーザーが web ページにユーザー名とパスワードを入力し、Forms をホストする J2EE アプリケーションサーバーにそれらの値を送信するシナリオを考えてみます。Forms のカスタムアプリケーションでは、Authentication Manager サービスを使用してユーザーを認証できます。

認証が成功した場合、アプリケーションは保護されたエンタープライズデータベースにアクセスします。そうでない場合は、ユーザーが承認されていないことを示すメッセージがユーザーに送信されます。

次の図に、アプリケーションのロジック・フローを示します。

![au_au_umauth_process](assets/au_au_umauth_process.png)

以下の表に、この図の手順を示します。

<table>
 <thead>
  <tr>
   <th><p>手順</p></th>
   <th><p>説明</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>ユーザーが web サイトにアクセスし、ユーザー名とパスワードを指定します。この情報は、AEM Forms をホストする J2EE アプリケーションサーバーに送信されます。</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>ユーザーの認証情報は、Authentication Manager サービスで認証されます。ユーザーの認証情報が有効な場合、ワークフローは手順 3 に進みます。そうでない場合は、ユーザーが承認されていないことを示すメッセージがユーザーに送信されます。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>ユーザー情報とフォームデザインは、保護されたエンタープライズデータベースから取得されます。 </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>ユーザー情報がフォームデザインと統合され、ユーザーに対してフォームが処理されます。 </p></td>
  </tr>
 </tbody>
</table>

### 手順の概要 {#summary_of_steps-5}

プログラムによるユーザーの認証を行うには、以下の手順を実行します。

1. プロジェクトファイルを含めます。
1. AuthenticationManagerService クライアントを作成します。
1. 認証操作を呼び出します。
1. 必要に応じて、コンテキストを取得し、クライアントアプリケーションが認証用に別の AEM Forms サービスに転送できるようにします。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めるようにします。

**AuthenticationManagerService クライアントの作成**

ユーザーをプログラムで認証する前に、AuthenticationManagerService クライアントを作成する必要があります。Java API を使用する場合、`AuthenticationManagerServiceClient` オブジェクトを作成します。

**認証操作の呼び出し**

サービスクライアントを作成すると、認証操作を呼び出すことができます。この操作には、ユーザー名やパスワードなど、ユーザーに関する情報が必要です。ユーザーが認証しない場合、例外がスローされます。

**認証コンテキストの取得**

ユーザーを認証すると、認証済みユーザーにもとづいてコンテキストを作成できます。その後、コンテンツを使用して別の AEM Forms サービスを呼び出すことができます。例えば、コンテキストを使用して `EncryptionServiceClient` を作成し、パスワードを使用して PDF ドキュメントを暗号化します。認証されたユーザーが、AEM Forms サービスを呼び出すために必要な `Services User` という名前の役割を持っていることを確認します。

**関連トピック**

[AEM Forms Java ライブラリファイルの組み込み](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[User Manager API クイックスタート](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

[パスワードを使用した PDF ドキュメントの暗号化](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Java API を使用したユーザーの認証 {#authenticate-a-user-using-the-java-api}

Authentication Manager Service API（Java）を使用してユーザーを認証します。

1. プロジェクトファイルを含めます。

   adobe-livecycle-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. AuthenticationManagerServices クライアントを作成します。

   `AuthenticationManagerServiceClient` オブジェクトを作成するには、コンストラクターを使用し、接続プロパティを含む `ServiceClientFactory` オブジェクトを渡します。

1. 認証操作を呼び出します。

   `AuthenticationManagerServiceClient` オブジェクトの `authenticate` メソッドを呼び出して、次の値を渡します。

   * ユーザーの名前を含む `java.lang.String` オブジェクト。
   * ユーザーのパスワードを含むバイト配列（`byte[]` オブジェクト）。`java.lang.String` オブジェクトの `getBytes` メソッドを呼び出すと、`byte[]` オブジェクトを取得できます。

   認証メソッドが、認証済みユーザーに関する情報を含む `AuthResult` オブジェクトを返します。

1. 認証コンテキストを取得します。

   `ServiceClientFactory` オブジェクトの `getContext` メソッドを呼び出すことで、`Context` オブジェクトが返されます。

   次に、`Context` オブジェクトの `initPrincipal` メソッドを呼び出して、`AuthResult` を渡します。

### Web サービス API を使用したユーザーの認証 {#authenticate-a-user-using-the-web-service-api}

Authentication Manager Service API（web サービス）を使用してユーザーを認証します。

1. プロジェクトファイルを含めます。

   * Authentication Manager WSDL を使用する Microsoft .NET クライアントアセンブリを作成します（[Base64 エンコーディングを使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)を参照してください）。
   * Microsoft .NET クライアントアセンブリを参照します( [Base64 エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).)

1. AuthenticationManagerService クライアントを作成します。

   プロキシクラスのコントラクターを使用して、`AuthenticationManagerServiceService` オブジェクトを作成します。

1. 認証操作を呼び出します。

   `AuthenticationManagerServiceClient` オブジェクトの `authenticate` メソッドを呼び出して、次の値を渡します。

   * ユーザーの名前を含む `string` オブジェクト
   * ユーザーのパスワードを含むバイト配列（`byte[]` オブジェクト）。以下の例に示すロジックを使用して、パスワードを含む `string` オブジェクトを `byte[]` 配列に変換することによって、`byte[]` オブジェクトを取得できます。
   * 戻り値は `AuthResult` オブジェクトです。このオブジェクトは、ユーザーに関する情報を取得するために使用できます。以下の例では、ユーザーの情報は、最初に `AuthResult` オブジェクトの `authenticatedUser` フィールドを取得し、続いてその結果の `User` オブジェクトの `canonicalName` フィールドおよび `domainName` フィールドを取得することによって取得されます。

**関連項目**

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## プログラムによるユーザーの同期 {#programmatically-synchronizing-users}

User Management API を使用して、プログラムによってユーザーを同期できます。ユーザーを同期する際、ユーザーリポジトリ内にあるユーザーデータで AEM Forms を更新します。例えば、新しいユーザーをユーザーリポジトリに追加するとします。同期操作を実行すると、新しいユーザーが AEM forms ユーザーになります。また、ユーザーリポジトリ内のユーザーは AEM Forms から削除されます。

次の図は、AEM Forms がユーザーリポジトリと同期する様子を示しています。

![ps_ps_umauth_sync](assets/ps_ps_umauth_sync.png)

以下の表に、この図の手順を示します。

<table>
 <thead>
  <tr>
   <th><p>手順</p></th>
   <th><p>説明</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>クライアントアプリケーションが、同期操作を実行するように AEM Forms に要求します。</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>AEM Forms が同期操作を実行します。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>ユーザー情報が更新されます。</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>ユーザーは、更新されたユーザー情報を表示することができます。 </p></td>
  </tr>
 </tbody>
</table>

### 手順の概要 {#summary_of_steps-6}

プログラムによってユーザーを同期するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. UserManagerUtilServiceClient クライアントを作成します。
1. エンタープライズドメインを指定します。
1. 認証操作を呼び出します。
1. 同期処理が完了したかどうかを確認します

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めるようにします。

**UserManagerUtilServiceClientclient の作成**

プログラムによるユーザーの同期を行う前に、`UserManagerUtilServiceClient` オブジェクトを作成する必要があります。

**エンタープライズドメインを指定**

User Management API を使用して同期操作を実行する前に、ユーザーが属するエンタープライズドメインを指定します。1 つまたは複数のエンタープライズドメインを指定できます。プログラムによって同期処理を実行する前に、管理コンソールを使用してエンタープライズドメインを設定する必要があります（[管理ヘルプ](https://www.adobe.com/go/learn_aemforms_admin_63_jp)を参照）。

**同期処理の呼び出し**

1 つ以上のエンタープライズドメインを指定した後、同期処理を実行できます。この処理の実行に要する時間は、ユーザーリポジトリ内にあるユーザーレコードの数によって異なります。

**同期処理が完了したかどうかを確認する**

プログラムによって同期処理を実行した後、処理が完了したかどうかを確認できます。

**関連トピック**

[AEM Forms Java ライブラリファイルの組み込み](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[User Manager API クイックスタート](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

[パスワードを使用した PDF ドキュメントの暗号化](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Java API を使用したプログラムによるユーザーの同期 {#programmatically-synchronizing-users-using-the-java-api}

User Management API（Java）を使用してユーザーを同期します。

1. プロジェクトファイルを含めます。

   Java プロジェクトのクラスパスに、adobe-usermanager-client.jar や adobe-usermanager-util-client.jar などのクライアント JAR ファイルを含めます。

1. UserManagerUtilServiceClient クライアントを作成します。

   コンストラクターを使用し、接続プロパティを含む `ServiceClientFactory` オブジェクトを渡して、`UserManagerUtilServiceClient` オブジェクトを作成します。

1. エンタープライズドメインを指定します。

   * `UserManagerUtilServiceClient` オブジェクトの `scheduleSynchronization` メソッドを呼び出して、ユーザー同期処理を開始します。
   * `HashSet` コンストラクターを使用して `java.util.Set` インスタンスを作成します。`String` をデータタイプとして設定したことを確認してください。この `Java.util.Set` インスタンスは、同期操作が適用されるドメイン名を格納します。
   * 追加するドメイン名ごとに、`java.util.Set` オブジェクトの add メソッドを参照し、ドメイン名を渡します。

1. 同期操作を呼び出します。

   `ServiceClientFactory` オブジェクトの `getContext` メソッドを呼び出し、`Context` オブジェクトを返します。

   `Context` オブジェクトの `initPrincipal` メソッドを呼び出し、`AuthResult` を渡します。

**関連トピック**

[プログラムによるユーザーの同期](users.md#programmatically-synchronizing-users)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
