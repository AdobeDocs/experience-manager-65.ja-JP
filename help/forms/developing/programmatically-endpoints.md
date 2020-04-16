---
title: エンドポイントのプログラムによる管理
seo-title: エンドポイントのプログラムによる管理
description: 'null'
seo-description: 'null'
uuid: 5dc50946-3323-4c5d-a43b-31c1c980bd04
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 076889a7-9c9f-4b6f-a45b-67a9b3923c36
translation-type: tm+mt
source-git-commit: f9389a06f9c2cd720919486765cee76257f272c3

---


# エンドポイントのプログラムによる管理 {#programmatically-managing-endpoints}

**エンドポイントレジストリサービスについて**

Endpoint Registryサービスは、エンドポイントをプログラムで管理する機能を提供します。 例えば、次の種類のエンドポイントをサービスに追加できます。

* EJB
* SOAP
* 監視フォルダー
* 電子メール
* （AEM formsでは非推奨）Remoting
* タスクマネージャ

>[!NOTE]
>
>SOAP、EJBおよび（JEE上のAEM formsでは非推奨）リモートエンドポイントは、アクティブ化された各サービスに対して自動的に作成されます。 SOAPおよびEJBエンドポイントは、すべてのサービス操作でSOAPおよびEJBを有効にします。

リモートエンドポイントを使用すると、Flexクライアントは、エンドポイントが追加されたAEM Formsサービスの操作を呼び出すことができます。 エンドポイントと同じ名前のFlex宛先が作成され、Flexクライアントは、この宛先を指すRemoteObjectsを作成して、関連するサービスの操作を呼び出すことができます。

電子メール、タスクマネージャーおよび監視フォルダーのエンドポイントは、サービスの特定の操作のみを公開します。 これらのエンドポイントを追加するには、呼び出すメソッドを選択し、設定パラメーターを設定し、入力および出力パラメーターのマッピングを指定する、2番目の設定手順が必要です。

TaskManagerエンドポイントは、エンドポイントと呼ばれるグループに整理 *カテゴリできま*&#x200B;す。 これらのカテゴリは、TaskManagerを通じてWorkspaceに公開され、エンドユーザーは、TaskManagerエンドポイントが分類されたとおりに表示されます。 Workspace内では、エンドユーザーはナビゲーションパネルにこれらのカテゴリを表示できます。 各エンドポイント内のカテゴリは、Workspaceのエンドポイントプロセスページにプロセスカードとして開始として表示されます。

Endpoint Registryサービスを使用して、次のタスクを実行できます。

* 追加EJBエンドポイント (「EJBエンド [ポイントの追加](programmatically-endpoints.md#adding-ejb-endpoints)」を参照)。
* SOAPエ追加ンドポイント (SOAPエンドポ [イントの追加を参照](programmatically-endpoints.md#adding-soap-endpoints))。
* 監視フ追加ォルダーエンドポイント(監視フォ [ルダーエンドポイントの追加](programmatically-endpoints.md#adding-watched-folder-endpoints)を参照)。
* 電子メ追加ールエンドポイント (See [Adding Email Endpoints](programmatically-endpoints.md#adding-email-endpoints).)
* エンドポ追加イントのリモート。 (「リモートエ [ンドポイントの追加](programmatically-endpoints.md#adding-remoting-endpoints)」を参照)。
* 追加TaskManagerエンドポイント(TaskManagerエンドポ [イントの追加を参照](programmatically-endpoints.md#adding-taskmanager-endpoints))。
* エンドポイントの変更(エンドポ [イントの変更](programmatically-endpoints.md#modifying-endpoints)を参照)
* エンドポイントの削除(エンドポ [イントの削除を参照](programmatically-endpoints.md#removing-endpoints))。
* エンドポイントコネクタ情報の取得(エ [ンドポイントコネクタ情報の取得](programmatically-endpoints.md#retrieving-endpoint-connector-information)を参照)。

## EJBエンドポイントの追加 {#adding-ejb-endpoints}

AEM Forms Java APIを使用して、EJBエンドポイントをプログラムでサービスに追加できます。 EJBエンドポイントをサービスに追加すると、クライアントアプリケーションでEJBモードを使用してサービスを呼び出せるようになります。 つまり、AEM Formsの呼び出しに必要な接続プロパティを設定する場合、EJBモードを選択できます。 （[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照。）

>[!NOTE]
>
>Webサービスを使用してEJBエンドポイントを追加することはできません。

>[!NOTE]
>
>通常、EJBエンドポイントはデフォルトでサービスに追加されますが、EJBエンドポイントは、プログラムによってデプロイされたプロセスや、EJBエンドポイントが削除され、再度追加する必要があるプロセスに追加できます。

### 手順の概要 {#summary-of-steps}

EJBエンドポイントをサービスに追加するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. オブジェクトを作 `EndpointRegistry Client` 成します。
1. EJBエンドポイント属性を設定します。
1. EJBエンドポイントを作成します。
1. エンドポイントを有効にします。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar（AEM FormsがJBoss Application Serverにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsがJBoss Application Serverにデプロイされている場合に必要）

For information about the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**EndpointRegistryクライアントオブジェクトの作成**

EJBエンドポイントをプログラムで追加する前に、オブジェクトを作成する必要があ `EndpointRegistryClient` ります。

**EJBエンドポイント属性の設定**

サービスのEJBエンドポイントを作成するには、次の値を指定します。

* **コネクタ識別子**:作成するエンドポイントのタイプを指定します。 EJBエンドポイントを作成するには、を指定しま `EJB`す。
* **説明**:エンドポイントの説明を指定します。
* **名前**:エンドポイントの名前を指定します。
* **サービス識別子**:エンドポイントが属するサービスを指定します。
* **操作名**:エンドポイントを使用して呼び出される操作の名前を指定します。 EJBエンドポイントを作成する場合は、ワイルドカード文字( `*`)を指定します。 ただし、すべてのサービス操作を呼び出すのではなく、特定の操作を指定する場合は、ワイルドカード文字( `*`)を使用するのではなく、操作の名前を指定します。

**EJBエンドポイントの作成**

EJBエンドポイント属性を設定した後、サービスのEJBエンドポイントを作成できます。

**エンドポイントの有効化**

新しいエンドポイントを作成したら、有効にする必要があります。 エンドポイントを有効にすると、そのエンドポイントを使用してサービスを呼び出すことができます。 エンドポイントを有効にした後、管理コンソール内で表示することができます。

**関連トピック**

[Java APIを使用したEJBエンドポイントの追加](programmatically-endpoints.md#adding-an-ejb-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java APIを使用したEJBエンドポイントの追加 {#adding-an-ejb-endpoint-using-the-java-api}

Java 追加 APIを使用したEJBエンドポイント：

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-livecycle-client.jarなどのクライアントJARファイルを含めます。 （

1. EndpointRegistry Clientオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `EndpointRegistryClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. EJBエンドポイント属性を設定します。

   * コンストラクタを使用して `CreateEndpointInfo` オブジェクトを作成します。
   * オブジェクトのメソッドを呼び出し、文 `CreateEndpointInfo` 字列値を渡 `setConnectorId` して、コネクタ識別子の値を指定しま `EJB`す。
   * オブジェクトのメソッドを呼び出し、エンドポ `CreateEndpointInfo` イントの説明を `setDescription` 記述するstring値を渡して、エンドポイントの説明を指定します。
   * オブジェクトのメソッドを呼び出し、名前 `CreateEndpointInfo` を指定する文 `setName` 字列値を渡して、エンドポイントの名前を指定します。
   * オブジェクトのメソッドを呼び出し、サービ `CreateEndpointInfo` ス名を指定 `setServiceId` する文字列値を渡して、エンドポイントが属するサービスを指定します。
   * オブジェクトのメソッドを呼び出して呼び出 `CreateEndpointInfo` す操作を指 `setOperationName` 定し、操作名を指定するstring値を渡します。 SOAPおよびEJBエンドポイントの場合は、すべての操作を示すワイルドカ `*`ード文字()を指定します。

1. EJBエンドポイントを作成します。

   オブジェクトのメソッドを呼び出し、オ `EndpointRegistryClient` ブジェクトを渡 `createEndpoint` して、エンドポイントを作成 `CreateEndpointInfo` します。 このメソッドは、新しいEJBエ `Endpoint` ンドポイントを表すオブジェクトを返します。

1. エンドポイントを有効にします。

   エンドポイントを有効にするには、オ `EndpointRegistryClient` ブジェクトのenableメソッドを呼び出し、メソッドから返さ `Endpoint` れたオブジェクトを渡 `createEndpoint` します。

**関連トピック**

[手順の概要](programmatically-endpoints.md#summary-of-steps)

[QuickStart:Java APIを使用したEJBエンドポイントの追加](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-ejb-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## SOAPエンドポイントの追加 {#adding-soap-endpoints}

AEM Forms Java APIを使用して、SOAPエンドポイントをプログラムによってサービスに追加できます。 SOAPエンドポイントを追加することで、クライアントアプリケーションがSOAPモードを使用してサービスを呼び出せるようにします。 つまり、AEM Formsの呼び出しに必要な接続プロパティを設定する場合は、SOAPモードを選択できます。

>[!NOTE]
>
>Webサービスを使用してSOAPエンドポイントを追加することはできません。

>[!NOTE]
>
>通常、SOAPエンドポイントはデフォルトでサービスに追加されますが、SOAPエンドポイントは、プログラム的にデプロイされたプロセスや、SOAPエンドポイントが削除され、再度追加する必要があるプロセスに追加できます。

### 手順の概要 {#summary_of_steps-1}

SOAPエンドポイントをサービスに追加するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. オブジェクトを作 `EndpointRegistryClient` 成します。
1. SOAPエンドポイント属性を設定します。
1. SOAPエンドポイントを作成します。
1. エンドポイントを有効にします。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar（AEM FormsがJBoss Application Serverにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsがJBoss Application Serverにデプロイされている場合に必要）

これらのJARファイルは、SOAPエンドポイントを作成するために必要です。 ただし、SOAPエンドポイントを使用してサービスを呼び出す場合は、追加のJARファイルが必要です。 AEM Forms JARファイルについて詳しくは、「AEM Forms Javaライブラリフ [ァイルのインクルード」を参照してくださ](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)い。

**EndpointRegistryクライアントオブジェクトの作成**

SOAPエンドポイントをプログラムによってサービスに追加するには、オブジェクトを作成する必要があ `EndpointRegistryClient` ります。

**SOAPエンドポイント属性の設定**

SOAPエンドポイントをサービスに追加するには、次の値を指定します。

* **コネクタ識別子の値**:作成するエンドポイントのタイプを指定します。 SOAPエンドポイントを作成するには、を指定しま `SOAP`す。
* **説明**:エンドポイントの説明を指定します。
* **名前**:エンドポイント名を指定します。
* **サービス識別子の値**:エンドポイントが属するサービスを指定します。
* **操作名**:エンドポイントを使用して呼び出される操作の名前を指定します。 SOAPエンドポイントを作成する場合は、ワイルドカード文字( `*`)を指定します。 ただし、すべてのサービス操作を呼び出すのではなく、特定の操作を指定する場合は、ワイルドカード文字( `*`)を使用するのではなく、操作の名前を指定します。

**SOAPエンドポイントの作成**

SOAPエンドポイント属性を設定した後、SOAPエンドポイントを作成できます。

**エンドポイントの有効化**

新しいエンドポイントを作成したら、有効にする必要があります。 エンドポイントが有効な場合は、サービスの呼び出しに使用できます。 エンドポイントを有効にすると、管理コンソール内で表示に表示されるようになります。

**関連トピック**

[Java APIを追加使用したSOAPエンドポイント](programmatically-endpoints.md#add-a-soap-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java APIを追加使用したSOAPエンドポイント {#add-a-soap-endpoint-using-the-java-api}

Java API追加を使用したサービスへのSOAPエンドポイント：

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-livecycle-client.jarなどのクライアントJARファイルを含めます。

1. EndpointRegistry Clientオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `EndpointRegistryClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. SOAPエンドポイント属性を設定します。

   * コンストラクタを使用して `CreateEndpointInfo` オブジェクトを作成します。
   * オブジェクトのメソッドを呼び出し、文 `CreateEndpointInfo` 字列値を渡 `setConnectorId` して、コネクタ識別子の値を指定しま `SOAP`す。
   * オブジェクトのメソッドを呼び出し、エンドポ `CreateEndpointInfo` イントの説明を `setDescription` 記述するstring値を渡して、エンドポイントの説明を指定します。
   * オブジェクトのメソッドを呼び出し、名前 `CreateEndpointInfo` を指定する文 `setName` 字列値を渡して、エンドポイントの名前を指定します。
   * オブジェクトのメソッドを呼び出し、サービ `CreateEndpointInfo` ス名を指定 `setServiceId` する文字列値を渡して、エンドポイントが属するサービスを指定します。
   * オブジェクトのメソッドを呼び出し、操 `CreateEndpointInfo` 作名を指定 `setOperationName` する文字列値を渡すことで、呼び出す操作を指定します。 SOAPおよびEJBエンドポイントの場合は、すべての操作を示すワイルドカ `*`ード文字()を指定します。

1. SOAPエンドポイントを作成します。

   オブジェクトのメソッドを呼び出し、オ `EndpointRegistryClient` ブジェクトを渡 `createEndpoint` して、エンドポイントを作成 `CreateEndpointInfo` します。 このメソッドは、新しいSOAPエ `Endpoint` ンドポイントを表すオブジェクトを返します。

1. エンドポイントを有効にします。

   オブジェクトのenableメソッドを呼び出し、 `EndpointRegistryClient` メソッドから返されたオブジェクトを渡すこ `Endpoint` とで、エンドポイントを有効に `createEndpoint` します。

**関連トピック**

[手順の概要](programmatically-endpoints.md#summary-of-steps)

[QuickStart:Java APIを使用したSOAPエンドポイントの追加](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-soap-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 監視フォルダーエンドポイントの追加 {#adding-watched-folder-endpoints}

AEM Forms Java APIを使用して、監視フォルダーエンドポイントをプログラムによってサービスに追加できます。 監視フォルダーエンドポイントを追加すると、ユーザーはファイル（PDFファイルなど）をフォルダーに配置できます。 ファイルがフォルダーに配置されると、設定済みのサービスが呼び出され、ファイルが操作されます。 サービスが指定の操作を実行した後に、変更されたファイルが指定の出力フォルダーに保存されます。監視フォルダーは、固定レートの間隔で、または毎週月曜日、水曜日、金曜日の正午などのCronスケジュールでスキャンされるように設定されます。

プログラムによって監視フォルダーエンドポイントをサービスに追加する場合は、次のEncryptDocumentという短時間のみ有効なプロセスを考慮 *します*。 (「AEM Formsプ [ロセスについて](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes)」を参照)。

![aw_aw_encryptdocumentprocess](assets/aw_aw_encryptdocumentprocess.png)

このプロセスは、保護されていないPDFドキュメントを入力値として受け取り、保護されていないPDFドキュメントをEncryptionサービスの操作に渡し `EncryptPDFUsingPassword` ます。 PDFドキュメントはパスワードで暗号化され、パスワードで暗号化されたPDFドキュメントはこのプロセスの出力値です。 入力値の名前(保護されていないPDFドキュメント)とデ `InDoc` ータタイプはです `com.adobe.idp.Document`。 出力値の名前(パスワードで暗号化されたPDFドキュメント)とデ `SecuredDoc` ータタイプはです `com.adobe.idp.Document`。

>[!NOTE]
>
>Webサービスを使用して監視フォルダーエンドポイントを追加することはできません。

### 手順の概要 {#summary_of_steps-2}

監視フォルダーエンドポイントをサービスに追加するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. オブジェクトを作 `EndpointRegistryClient` 成します。
1. 監視フォルダーエンドポイントの属性を設定します。
1. 設定値を指定します。
1. 入力パラメーターの値を定義します。
1. 出力パラメータの値を定義します。
1. 監視フォルダーエンドポイントの作成を参照してください。
1. エンドポイントを有効にします。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar（AEM FormsがJBoss Application Serverにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsがJBoss Application Serverにデプロイされている場合に必要）

For information about the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**EndpointRegistryクライアントオブジェクトの作成**

プログラムによって監視フォルダーエンドポイントを追加するには、オブジェクトを作成する必要が `EndpointRegistryClient` あります。

**監視フォルダーエンドポイントの属性の設定**

サービスの監視フォルダーエンドポイントを作成するには、次の値を指定します。

* **コネクタ識別子**:作成するエンドポイントのタイプを指定します。 監視フォルダーエンドポイントを作成するには、を指定しま `WatchedFolder`す。
* **説明**:エンドポイントの説明を指定します。
* **名前**:エンドポイントの名前を指定します。
* **サービス識別子**:エンドポイントが属するサービスを指定します。 例えば、この節で紹介するプロセス（Workbenchを使用してアクティブ化されたプロセス）に監視フォルダーエンドポイントを追加するには、を指定しま `EncryptDocument`す。
* **操作名**:エンドポイントを使用して呼び出される操作の名前を指定します。 通常、Workbenchで作成されたプロセスから生成されたサービスの監視フォルダーエンドポイントを作成する場合、操作の名前はで `invoke`す。

**設定値の指定**

監視フォルダーエンドポイントをプログラムでサービスに追加する場合は、監視フォルダーエンドポイントの設定値を指定する必要があります。 これらの設定値は、管理コンソールを使用して監視フォルダーエンドポイントを追加した場合、管理者が指定します。

次のリストは、監視フォルダーエンドポイントをプログラムでサービスに追加する際に設定される設定値を指定します。

* **url**:監視フォルダーの場所を指定します。 クラスター化環境では、この値は、クラスター内のすべてのコンピューターからアクセス可能な共有ネットワークフォルダーを指す必要があります。
* **非同期**:呼び出しの種類を非同期型または同期型として識別します。 一過性および同期型のプロセスは、同期型でのみ呼び出すことができます。デフォルト値は true です。非同期を推奨します。
* **cronExpression**:Quartzで、入力ディレクトリのポーリングをスケジュールするために使用されます。 cron式の設定について詳しくは、https://quartz.sourceforge.net/javadoc/org/quartz/CronTrigger.htmlを参照してく [ださい](https://quartz.sourceforge.net/javadoc/org/quartz/CronTrigger.html)。
* **purgeDuration**:これは必須の属性です。 結果フォルダー内のファイルとフォルダーは、この値より古い場合に削除されます。 この値の単位は日です。この属性は、結果フォルダーがいっぱいにならないようにするのに役立ちます。 -1 を指定すると、結果フォルダーの削除は行われません。デフォルト値は -1 です。
* **repeatInterval**:監視フォルダーをスキャンして入力を求める間隔（秒単位）です。 ジョブ数の制限が有効になっていない限り、この値は平均ジョブの処理時間より長くする必要があります。そうしないと、システムが過負荷になる可能性があります。 デフォルト値は 5 です。
* **repeatCount**:監視フォルダーがフォルダーまたはディレクトリをスキャンする回数です。 -1 を指定すると、無限にスキャンされます。デフォルト値は -1 です。
* **throttleOn**:任意の時点で処理できる監視フォルダーのジョブ数を制限します。 ジョブの最大数は、batchSize値によって決まります。
* **userName**:監視フォルダーからユーザーサービスを呼び出す際に使用されるターゲット名です。 この値は必須です。デフォルト値は「SuperAdmin」です。
* **domainName**:ユーザーのドメイン。 この値は必須です。デフォルト値は「DefaultDom」です。
* **batchSize**:1回のスキャンで取得されるファイルまたはフォルダーの数。 この値を使用して、システムの過負荷を防ぎます。一度にスキャンするファイル数が多すぎると、クラッシュする可能性があります。 デフォルト値は 2 です。
* **waitTime**:フォルダーまたはファイルの作成後にスキャンを実行するまでの待機時間（ミリ秒）です。 例えば、待機時間が36,000,000ミリ秒（1時間）で、ファイルが1分前に作成された場合、このファイルは59分以上経過した後に取得されます。 この属性は、ファイルまたはフォルダーが入力フォルダーに完全にコピーされるようにする場合に役立ちます。 例えば、処理するファイルのサイズが大きく、ファイルのダウンロードに10分かかる場合は、待機時間を10&amp;ast;60 &amp;ast;1000ミリ秒に設定します。 この設定により、監視フォルダーが10分間待たない場合に、ファイルをスキャンしないようにすることができます。 デフォルト値は 0 です。
* **excludeFilePattern**:スキャンおよび取得の対象とするファイルとフォルダーを決定するために監視フォルダーが使用するパターンです。 このパターンを含むファイルまたはフォルダーは、スキャンされて処理されません。 この設定は、入力が複数のファイルを含むフォルダーの場合に役立ちます。 フォルダーの内容は、監視フォルダーが取得する名前のフォルダーにコピーできます。 この手順により、フォルダーが入力フォルダーに完全にコピーされる前に、監視フォルダーがフォルダーを取得して処理するのを防ぎます。 For example, if the excludeFilePattern value is `data*`, all files and folders that match `data*` are not picked up. This includes files and folders named `data1`, `data2`, and so on. また、このパターンにワイルドカードパターンを追加して、ファイルパターンを指定できます。 監視フォルダーでは、およびなどのワイルドカード式をサポートするように正規フォルダーが `*.*` 変更されま `*.pdf`す。 これらのワイルドカードパターンは、正規式ではサポートされません。
* **includeFilePattern**:スキャンおよび取得するフォルダーとファイルを決定するために監視フォルダーが使用するパターンです。 For example, if this value is `*`, all files and folders that match `input*` are picked up. This includes files and folders named `input1`, `input2`, and so on. デフォルト値は `*` です。この値は、すべてのファイルとフォルダーを示します。 また、このパターンにワイルドカードパターンを追加して、ファイルパターンを指定できます。 監視フォルダーでは、およびなどのワイルドカード式をサポートするように正規フォルダーが `*.*` 変更されま `*.pdf`す。 これらのワイルドカードパターンは、正規式ではサポートされません。 この値は必須です。
* **resultFolderName**:保存した結果が保存されるフォルダーです。 この場所は、絶対パスまたは相対ディレクトリパスで指定できます。 結果がこのフォルダーに表示されない場合は、失敗フォルダーを確認してください。読み取り専用ファイルは処理されず、失敗フォルダーに保存されます。デフォルト値は `result/%Y/%M/%D/` です。これは、監視フォルダー内の結果フォルダーです。
* **preserveFolderName**:正常にスキャンおよび取得された後にファイルが保存される場所。 この場所は、絶対パス、相対パス、またはnullのディレクトリパスで指定できます。 デフォルト値は `preserve/%Y/%M/%D/` です。
* **failureFolderName**:失敗ファイルが保存されるフォルダーです。 この場所は、常に監視フォルダーからの相対パスで指定します。読み取り専用ファイルは処理されず、失敗フォルダーに保存されます。デフォルト値は `failure/%Y/%M/%D/` です。
* **preserveOnFailure**:サービスで操作の実行に失敗した場合に入力ファイルを保持します。 デフォルト値は true です。
* **overwriteDuplicateFilename**:trueに設定すると、結果フォルダーと保存用フォルダー内のファイルが上書きされます。 falseに設定した場合、数値のインデックスのサフィックスを持つファイルとフォルダーが名前に使用されます。 デフォルト値は false です。

**入力パラメーター値の定義**

監視フォルダーエンドポイントを作成する場合は、入力パラメーターの値を定義する必要があります。 つまり、監視フォルダーによって呼び出される操作に渡される入力値を記述する必要があります。 例えば、このトピックで紹介したプロセスについて考えてみましょう。 この変数には、という名前の入力値が1 `InDoc` つあり、そのデータタイプはで `com.adobe.idp.Document`す。 このプロセスの監視フォルダーエンドポイントを作成する場合（プロセスがアクティブ化されると、サービスになります）、入力パラメーターの値を定義する必要があります。

監視フォルダーエンドポイントに必要な入力パラメーターの値を定義するには、次の値を指定します。

**入力パラメータ名**:入力パラメータの名前。 入力値の名前は、プロセスに対してWorkbenchで指定されます。 入力値がサービス操作（Workbenchで作成されたプロセスではないサービス）に属する場合、入力名はcomponent.xmlファイルで指定されます。 例えば、この節で紹介するプロセスの入力パラメーターの名前はです `InDoc`。

**マッピングの種類**:サービス操作の呼び出しに必要な入力値の設定に使用されます。 マッピングのタイプには次の2種類があります。

* `Literal`:監視フォルダーエンドポイントは、フィールドに入力された値を表示どおりに使用します。 すべての基本 Java 型がサポートされます。例えば、APIがString、long、int、Booleanなどの入力を使用する場合、文字列は適切な型に変換され、サービスが呼び出されます。
* `Variable`:入力された値は、監視フォルダーが入力を選択する際に使用するファイルパターンです。 例えば、マッピングの種類として「Variable」を選択し、入力ドキュメントーがPDFファイルである必要がある場合、マッピング値 `*.pdf`として指定できます。

**マッピング値**:マッピングタイプの値を指定します。 例えば、マッピングの種類を選 `Variable` 択した場合、ファイルパターン `*.pdf` として指定できます。

**データタイプ**:入力値のデータタイプを指定します。 例えば、この節で紹介するプロセスの入力値のデータタイプはです `com.adobe.idp.Document`。

**出力パラメータ値の定義**

監視フォルダーエンドポイントを作成する場合は、出力パラメーターの値を定義する必要があります。 つまり、監視フォルダーエンドポイントによって呼び出されるサービスから返される出力値を記述する必要があります。 例えば、このトピックで紹介したプロセスについて考えてみましょう。 この変数には、という名前の出力値が `SecuredDoc` あり、そのデータタイプはで `com.adobe.idp.Document`す。 このプロセスの監視フォルダーエンドポイントを作成する場合（プロセスがアクティブ化されると、サービスになります）、出力パラメーターの値を定義する必要があります。

監視フォルダーエンドポイントに必要な出力パラメーターの値を定義するには、次の値を指定します。

**出力パラメータ名**:出力パラメーターの名前。 プロセス出力値の名前は、Workbenchで指定されます。 出力値がサービス操作（Workbenchで作成されたプロセスではないサービス）に属する場合、出力名はcomponent.xmlファイルで指定されます。 例えば、この節で紹介するプロセスの出力パラメーターの名前はです `SecuredDoc`。

**マッピングの種類**:サービスと操作の出力を設定するために使用します。 以下のオプションが利用できます。

* サービスが単一のオブジェクト(1つのドキュメント)を返す場合、パターンはで `%F.pdf` き、ソースの宛先はsourcefilename.pdfです。 例えば、この節で紹介したプロセスは、1つのドキュメントを返します。 その結果、マッピングタイプは、と定義できます( `%F.pdf` 指定し `%F` たファイル名を使用することを意味します)。 パターンは、 `%E` 入力拡張子を指定するドキュメントです。
* サービスがリストを返す場合、パタ `Result\%F\`ーンはResult\sourcefilename\source1 (output 1)とResult\sourcefilename\source2 (output 2)がソース宛先です。
* サービスがマップを返す場合、パターンはResult\sourcefilename\file1 and Result\sourcefilename\file2 `Result\%F\`になり、ソースの宛先はになります。 マップに複数のオブジェクトが含まれる場合、パターンは `Result\%F.pdf` Result\sourcefilename1.pdf（出力1）、Result\sourcefilenam2.pdf（出力2）のようになります。

**データタイプ**:戻り値のデータ型を指定します。 例えば、この節で紹介するプロセスの戻り値のデータ型はです `com.adobe.idp.Document`。

**監視フォルダーエンドポイントの作成**

エンドポイントの属性、設定値を設定し、入力パラメーターと出力パラメーターの値を定義した後、監視フォルダーエンドポイントを作成する必要があります。

**エンドポイントの有効化**

監視フォルダーエンドポイントを作成したら、有効にする必要があります。 エンドポイントが有効な場合は、サービスの呼び出しに使用できます。 エンドポイントを有効にした後、管理コンソール内で表示することができます。

**関連トピック**

[Java APIを使追加用した監視フォルダーエンドポイント](programmatically-endpoints.md#add-a-watched-folder-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java APIを使追加用した監視フォルダーエンドポイント {#add-a-watched-folder-endpoint-using-the-java-api}

AEM 追加 Forms Java APIを使用した監視フォルダーエンドポイント：

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-livecycle-client.jarなどのクライアントJARファイルを含めます。

1. EndpointRegistry Clientオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `EndpointRegistryClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. 監視フォルダーエンドポイントの属性を設定します。

   * コンストラクタを使用して `CreateEndpointInfo` オブジェクトを作成します。
   * オブジェクトのメソッドを呼び出し、文 `CreateEndpointInfo` 字列値を渡 `setConnectorId` して、コネクタ識別子の値を指定しま `WatchedFolder`す。
   * オブジェクトのメソッドを呼び出し、エンドポ `CreateEndpointInfo` イントの説明を `setDescription` 記述するstring値を渡して、エンドポイントの説明を指定します。
   * オブジェクトのメソッドを呼び出し、名前 `CreateEndpointInfo` を指定する文 `setName` 字列値を渡して、エンドポイントの名前を指定します。
   * オブジェクトのメソッドを呼び出し、サービ `CreateEndpointInfo` ス名を指定 `setServiceId` する文字列値を渡して、エンドポイントが属するサービスを指定します。
   * オブジェクトのメソッドを呼び出し、操 `CreateEndpointInfo` 作名を指定 `setOperationName` する文字列値を渡すことで、呼び出す操作を指定します。 通常、Workbenchで作成されたプロセスから生成されたサービスの監視フォルダーエンドポイントを作成する場合、操作の名前はinvokeです。

1. 設定値を指定します。

   監視フォルダーエンドポイントに設定する各設定値に対して、オブジェクトのメソッドを呼び出 `CreateEndpointInfo` す必要があ `setConfigParameterAsText` ります。 例えば、設定値を設定す `url` るには、オブジェクトの `CreateEndpointInfo` メソッドを呼び出 `setConfigParameterAsText` し、次の文字列値を渡します。

   * 設定値の名前を指定するstring値。 設定値を設定す `url` る際に、を指定しま `url`す。
   * 設定値の値を指定するstring値。 設定値を設定する `url` 場合は、監視フォルダーの場所を指定します。
   >[!NOTE]
   >
   >EncryptDocumentサービスに設定されたすべての設定値を確認するには、 [QuickStartにあるJavaコードの例を参照してください。Java APIを使用した監視フォルダーエンドポイントの追加](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)。

1. 入力パラメーターの値を定義します。

   オブジェクトのメソッドを呼び出し、次 `CreateEndpointInfo` の値を渡して、 `setInputParameterMapping` 入力パラメーター値を定義します。

   * 入力パラメーターの名前を指定するstring値。 例えば、EncryptDocumentサービスの入力パラメーターの名前はです `InDoc`。
   * 入力パラメーターのデータタイプを指定するstring値。 例えば、入力パラメーターのデータタ `InDoc` イプはです `com.adobe.idp.Document`。
   * マッピングの種類を指定するstring値です。 For example, you can specify `variable`.
   * マッピングタイプの値を指定するstring値。 例えば、&amp;ast;.pdfをファイルパターンとして指定できます。
   >[!NOTE]
   >
   >定義する各入 `setInputParameterMapping` 力パラメーター値のメソッドを呼び出します。 EncryptDocumentプロセスには1つの入力パラメーターしかないので、このメソッドを1回呼び出す必要があります。

1. 出力パラメータの値を定義します。

   オブジェクトのメソッドを呼び出し、次 `CreateEndpointInfo` の値を渡し `setOutputParameterMapping` て、出力パラメーター値を定義します。

   * 出力パラメーターの名前を指定するstring値。 例えば、EncryptDocumentサービスの出力パラメーターの名前はです `SecuredDoc`。
   * 出力パラメーターのデータタイプを指定するstring値。 例えば、出力パラメーターのデータタ `SecuredDoc` イプはです `com.adobe.idp.Document`。
   * マッピングの種類を指定するstring値です。 For example, you can specify `%F.pdf`.

1. 監視フォルダーエンドポイントの作成を参照してください。

   オブジェクトのメソッドを呼び出し、オ `EndpointRegistryClient` ブジェクトを渡 `createEndpoint` して、エンドポイントを作成 `CreateEndpointInfo` します。 このメソッドは、監視フォ `Endpoint` ルダーエンドポイントを表すオブジェクトを返します。

1. エンドポイントを有効にします。

   オブジェクトのメソッドを呼び出し、 `EndpointRegistryClient` メソッドによ `enable` って返されたオブジ `Endpoint` ェクトを渡して、エンドポイントを有効に `createEndpoint` します。

**関連トピック**

[手順の概要](programmatically-endpoints.md#summary-of-steps)

[QuickStart:Java APIを使用した監視フォルダーエンドポイントの追加](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 監視フォルダー設定値の定数ファイル {#watched-folder-configuration-values-constant-file}

クイッ [クスタート：Java APIを使用して監視フォルダーエンドポイントを追加すると](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api) 、クイック開始をコンパイルするためにJavaプロジェクトの一部である必要がある定数ファイルが使用されます。 この定数ファイルは、監視フォルダーエンドポイントを追加する際に設定する必要がある設定値を表します。 次のJavaコードは定数ファイルを表しています。

```as3
 /**
     * This class contains constants that can be used when setting Watched Folder
     * configuration values
     */

 public final class WatchedFolderEndpointConfigConstants {

         public static final String PROPERTY_FILEPROVIDER_URL = "url";
         public static final String PROPERTY_PROPERTY_ASYNCHRONOUS = "asynchronous";
         public static final String PROPERTY_CRON_EXPRESSION = "cronExpression";
         public static final String PROPERTY_PURGE_DURATION = "purgeDuration";
         public static final String PROPERTY_REPEAT_INTERVAL = "repeatInterval";
         public static final String PROPERTY_REPEAT_COUNT = "repeatCount";
         public static final String PROPERTY_THROTTLE = "throttleOn";
         public static final String PROPERTY_USERNAMER = "userName";
         public static final String PROPERTY_DOMAINNAME = "domainName";
         public static final String PROPERTY_FILEPROVIDER_BATCH_SIZE = "batchSize";
         public static final String PROPERTY_FILEPROVIDER_WAIT_TIME = "waitTime";
         public static final String PROPERTY_EXCLUDE_FILE_PATTERN = "excludeFilePattern";
         public static final String PROPERTY_INCLUDE_FILE_PATTERN = "excludeFilePattern";
         public static final String PROPERTY_FILEPROVIDER_RESULT_FOLDER_NAME =  "resultFolderName";
         public static final String PROPERTY_FILEPROVIDER_PRESERVE_FOLDER_NAME = "preserveFolderName";
         public static final String PROPERTY_FILEPROVIDER_FAILURE_FOLDER_NAME = "failureFolderName";
         public static final String PROPERTY_FILEPROVIDER_PRESERVE_ON_FAILURE = "preserveOnFailure";
         public static final String PROPERTY_FILEPROVIDER_OVERWRITE_DUPLICATE_FILENAME = "overwriteDuplicateFilename";
        }
```

## 電子メールエンドポイントの追加 {#adding-email-endpoints}

AEM Forms Java APIを使用して、プログラムによって電子メールエンドポイントをサービスに追加できます。 電子メールエンドポイントを追加すると、1つ以上の添付ファイルを含む電子メールメッセージを、指定した電子メールアカウントに送信できます。 次に、サービスの設定操作が呼び出され、ファイルが操作されます。 サービスは、指定された操作を実行した後、変更されたファイルを添付ファイルとして送信者に電子メールメッセージを送信します。

プログラムによって電子メールエンドポイントをサービスに追加する場合は、次のMyApplication\EncryptDocumentという短時間のみ有効なプロセスを考 *慮してください*。 短時間のみ有効なプロセスについて詳しくは、「AEM Formsプロセ [スについて」を参照してくださ](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes)い。

![ae_ae_encryptdocumentprocess](assets/ae_ae_encryptdocumentprocess.png)

このプロセスは、保護されていないPDFドキュメントを入力値として受け取り、保護されていないPDFドキュメントをEncryptionサービスの操作に渡し `EncryptPDFUsingPassword` ます。 このプロセスは、PDFドキュメントをパスワードで暗号化し、パスワードで暗号化されたPDFドキュメントを出力値として返します。 入力値の名前(保護されていないPDFドキュメント)とデ `InDoc` ータタイプはです `com.adobe.idp.Document`。 出力値の名前(パスワードで暗号化されたPDFドキュメント)とデ `SecuredDoc` ータタイプはです `com.adobe.idp.Document`。

>[!NOTE]
>
>Webサービスを使用して電子メールエンドポイントを追加することはできません。

### 手順の概要 {#summary_of_steps-3}

電子メールエンドポイントをサービスに追加するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. オブジェクトを作 `EndpointRegistryClient` 成します。
1. 電子メールエンドポイントの属性を設定します。
1. 設定値を指定します。
1. 入力パラメーターの値を定義します。
1. 出力パラメータの値を定義します。
1. 電子メールエンドポイントを作成します。
1. エンドポイントを有効にします。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar（AEM FormsがJBoss Application Serverにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsがJBoss Application Serverにデプロイされている場合に必要）

For information about the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**EndpointRegistryクライアントオブジェクトの作成**

プログラムによって電子メールエンドポイントを追加する前に、オブジェクトを作成する必要が `EndpointRegistryClient` あります。

**電子メールエンドポイント属性の設定**

サービスの電子メールエンドポイントを作成するには、次の値を指定します。

* **コネクタ識別子の値**:作成するエンドポイントのタイプを指定します。 電子メールエンドポイントを作成するには、を指定しま `Email`す。
* **説明**:エンドポイントの説明を指定します。
* **名前**:エンドポイントの名前を指定します。
* **サービス識別子の値**:エンドポイントが属するサービスを指定します。 例えば、この節で紹介するプロセス（Workbenchを使用してアクティブ化されたプロセス）に電子メールエンドポイントを追加するには、を指定しま `EncryptDocument`す。
* **操作名**:エンドポイントを使用して呼び出される操作の名前を指定します。 通常、Workbenchで作成されたプロセスから生成されたサービスの電子メールエンドポイントを作成する場合、操作の名前はで `invoke`す。

**設定値の指定**

電子メールエンドポイントをプログラムでサービスに追加する場合は、電子メールエンドポイントの設定値を指定する必要があります。 これらの設定値は、管理コンソールを使用して電子メールエンドポイントを追加した場合に、管理者が指定します。

>[!NOTE]
>
>監視される電子メールアカウントは、電子メールエンドポイントにのみ使用される特別なアカウントです。 このアカウントは、通常のユーザーの電子メールアカウントではありません。 通常のユーザーの電子メールアカウントは、電子メールプロバイダーが使用するアカウントとして設定しないでください。電子メールプロバイダーは、メッセージの処理が完了した後にインボックスから電子メールメッセージを削除します。

次の設定値は、プログラムで電子メールエンドポイントをサービスに追加する場合に設定されます。

* **cronExpression**:Cron式。Cron式を使用して電子メールをスケジュールする必要がある場合。
* **repeatCount**:電子メールエンドポイントがフォルダーまたはディレクトリをスキャンする回数。 -1 を指定すると、無限にスキャンされます。デフォルト値は -1 です。
* **repeatInterval**:受信者が受信メールの確認に使用するスキャン速度（秒）。 デフォルト値は 10 です。
* **startDelay**:スキャンが完了するまで待機する時間です。スケジューラー開始。 デフォルトの時間は0です。
* **batchSize**:受信者が最適なパフォーマンスを得るために1回のスキャンで処理する電子メールメッセージの数。 -1 を指定すると、すべての電子メールが処理されます。デフォルト値は 2 です。
* **userName**:電子メールからユーザーサービスを呼び出す際に使用されるターゲット名です。 デフォルト値は `SuperAdmin` です。
* **domainName**:必須の設定値です。 デフォルト値は `DefaultDom` です。
* **domainPattern**:プロバイダーが受け入れる受信電子メールのドメインパターンを指定します。 For example, if `adobe.com` is used, only email from adobe.com is processed, email from other domains is ignored.
* **filePattern**: Specifies the incoming file attachment patterns that the provider accepts. 特定のファイル名拡張子(&amp;ast;.dat, &amp;ast;.xml)を持つファイル、特定の名前(data)を持つファイル、名前と拡張子(&amp;ast;)に複合式を持つファイルが含まれます。[dD][aA]&#39;port&#39;)。 デフォルト値は `*` です。
* **recipientSuccessfulJob**:ジョブの成功を示すメッセージの送信先の電子メールアドレスです。 デフォルトでは、ジョブの正常終了メッセージは常に送信者に送信されます。`sender` と入力すると、電子メールの結果は送信者に送信されます。最大 100 人の受信者を指定できます。追加の受信者を指定し、それぞれをコンマで区切ります。 このオプションをオフにするには、この値を空欄にします。 In some cases, you may want to trigger a process and do not want an email notification of the result. デフォルト値は `sender` です。
* **recipientFailedJob**:ジョブの失敗を示すメッセージの送信先の電子メールアドレス。 デフォルトでは、失敗したジョブのメッセージは常に送信者に送信されます。 `sender` と入力すると、電子メールの結果は送信者に送信されます。最大 100 人の受信者を指定できます。追加の受信者を指定し、それぞれをコンマで区切ります。 このオプションをオフにするには、この値を空欄にします。 デフォルト値は `sender` です。
* **inboxHost**:電子メールプロバイダーがスキャンするインボックスのホスト名またはIPアドレス。
* **inboxPort**:電子メールサーバーが使用するポート。 POP3 のデフォルト値は「110」で、IMAP のデフォルト値は「143」です。SSL が有効になっている場合は、POP3 のデフォルト値は「995」で、IMAP のデフォルト値は「993」です。
* **inboxProtocol**:電子メールエンドポイントがインボックスのスキャンに使用する電子メールプロトコルです。 またはを選択で `IMAP` きます `POP3`。 指定のプロトコルはインボックスホストメールサーバーでサポートされている必要があります。
* **inboxTimeOut**:電子メールプロバイダーがインボックスの応答を待機するまでのタイムアウト（秒）。 デフォルト値は 60 です。
* **inboxUser**:電子メールアカウントにログインするために必要なユーザー名です。 電子メールサーバーと設定によっては、電子メールのユーザー名の部分のみ、または完全な電子メールアドレスのみを指定できます。
* **inboxPassword**:インボックスユーザーのパスワードです。
* **inboxSSLEnabled**:この値を設定すると、電子メールプロバイダーは、結果またはエラーの通知メッセージを送信する際にSSLを使用します。 IMAPまたはPOP3ホストがSSLをサポートしていることを確認します。
* **smtpHost**:電子メールプロバイダーが結果およびエラーメッセージを送信するメールサーバーのホスト名です。
* **smtpPort**:SMTPポートのデフォルト値は25です。
* **smtpUser**:電子メールプロバイダーが結果やエラーの電子メール通知を送信する際に使用するユーザーアカウントです。
* **smtpPassword**:SMTPアカウントのパスワードです。 SMTP パスワードが不要なメールサーバーもあります。
* **charSet**:電子メールプロバイダーが使用する文字セットです。 デフォルト値は `UTF-8` です。
* **smtpSSLEnabled**:この値を設定すると、電子メールプロバイダーは、結果またはエラーの通知メッセージを送信する際にSSLを使用します。 SMTPホストがSSLをサポートしていることを確認します。
* **failedJobFolder**:SMTPメールサーバーが動作していない場合に結果を保存するディレクトリを指定します。
* **非同期**:同期に設定すると、すべての入力ドキュメントが処理され、単一の応答が返されます。 「asynchronous」に設定すると、処理される入力ドキュメントごとに応答が送信されます。 例えば、このトピックで導入されたプロセス用に電子メールエンドポイントが作成され、保護されていない複数のPDFドキュメントを含む電子メールメッセージがエンドポイントのインボックスに送信されます。 すべてのPDFドキュメントがパスワードで暗号化され、エンドポイントが同期として設定されている場合は、セキュリティで保護されたすべてのPDFドキュメントが添付された単一の応答電子メールメッセージが送信されます。 エンドポイントが非同期として設定されている場合は、保護されたPDFメッセージごとに別々の応答電子メールメッセージが送信されます。ドキュメント 各電子メールメッセージには、添付ファイルとして1つのPDFドキュメントが含まれています。 デフォルト値は「asynchronous」です。

**入力パラメーター値の定義**

電子メールエンドポイントを作成する場合は、入力パラメーターの値を定義する必要があります。 つまり、電子メールエンドポイントによって呼び出される操作に渡される入力値を記述する必要があります。 例えば、このトピックで紹介したプロセスについて考えてみましょう。 この変数には、という名前の入力値が1 `InDoc` つあり、そのデータタイプはで `com.adobe.idp.Document`す。 このプロセスの電子メールエンドポイントを作成する場合（プロセスがアクティブ化されると、サービスになります）、入力パラメーターの値を定義する必要があります。

電子メールエンドポイントに必要な入力パラメーターの値を定義するには、次の値を指定します。

**入力パラメータ名**:入力パラメータの名前。 入力値の名前は、プロセスに対してWorkbenchで指定されます。 入力値がサービス操作（Workbenchで作成されたプロセスではないFormsサービス）に属する場合、入力名はcomponent.xmlファイルで指定されます。 例えば、この節で紹介するプロセスの入力パラメーターの名前はです `InDoc`。

**マッピングの種類**:サービス操作の呼び出しに必要な入力値の設定に使用されます。 次に、2種類のマッピングのタイプを示します。

* `Literal`:電子メールエンドポイントは、フィールドに入力された値を表示どおりに使用します。 すべての基本 Java 型がサポートされます。例えば、String、long、int および Boolean などの入力が使用される API の場合、文字列は適切な型に変換され、サービスが呼び出されます。
* `Variable`:入力された値は、電子メールエンドポイントが入力の選択に使用するファイルパターンです。 例えば、マッピングの種類として「Variable」を選択し、入力ドキュメントーがPDFファイルである必要がある場合、マッピング値 `*.pdf` として指定できます。

**マッピング値**:マッピングタイプの値を指定します。 例えば、変数のマッピングタイプを選択した場合、ファイルパターンと `*.pdf` して指定できます。

**データタイプ**:入力値のデータタイプを指定します。 例えば、この節で紹介するプロセスの入力値のデータタイプは、com.adobe.idp.ドキュメントです。

**出力パラメータ値の定義**

電子メールエンドポイントを作成する場合は、出力パラメーターの値を定義する必要があります。 つまり、電子メールエンドポイントによって呼び出されるサービスによって返される出力値を記述する必要があります。 例えば、このトピックで紹介したプロセスについて考えてみましょう。 この変数には、という名前の出力値が `SecuredDoc` あり、そのデータタイプはで `com.adobe.idp.Document`す。 このプロセスの電子メールエンドポイントを作成する場合（プロセスがアクティブ化されると、サービスになります）、出力パラメーターの値を定義する必要があります。

電子メールエンドポイントに必要な出力パラメーターの値を定義するには、次の値を指定します。

**出力パラメータ名**:出力パラメーターの名前。 プロセス出力値の名前は、Workbenchで指定されます。 出力値がサービス操作（Workbenchで作成されたプロセスではないサービス）に属する場合、出力名はcomponent.xmlファイルで指定されます。 例えば、この節で紹介するプロセスの出力パラメーターの名前はです `SecuredDoc`。

**マッピングの種類**:サービスと操作の出力を設定するために使用します。 以下のオプションが利用できます。

* サービスが単一のオブジェクト(1つのドキュメント)を返す場合、パターンはで `%F.pdf` き、ソースの宛先はsourcefilename.pdfです。 例えば、この節で紹介したプロセスは、1つのドキュメントを返します。 その結果、マッピングタイプは、と定義できます( `%F.pdf` 指定し `%F` たファイル名を使用することを意味します)。 パターンは、 `%E` 入力拡張子を指定するドキュメントです。
* サービスがリストを返す場合、パタ `Result\%F\`ーンはResult\sourcefilename\source1 (output 1)とResult\sourcefilename\source2 (output 2)がソース宛先です。
* サービスがマップを返す場合、パターンはResult\sourcefilename\file1 and Result\sourcefilename\file2 `Result\%F\`になり、ソースの宛先はになります。 マップに複数のオブジェクトが含まれる場合、パターンは `Result\%F.pdf` Result\sourcefilename1.pdf（出力1）、Result\sourcefilenam2.pdf（出力2）のようになります。

**データタイプ**:戻り値のデータ型を指定します。 例えば、この節で紹介するプロセスの戻り値のデータ型はです `com.adobe.idp.Document`。

**電子メールエンドポイントの作成**

電子メールエンドポイントの属性と設定値を設定し、入力および出力パラメーターの値を定義した後、電子メールエンドポイントを作成する必要があります。

**エンドポイントの有効化**

電子メールエンドポイントを作成したら、有効にする必要があります。 エンドポイントが有効な場合は、サービスの呼び出しに使用できます。 エンドポイントを有効にした後、管理コンソール内で表示することができます。

**関連トピック**

[Java APIを追加使用する電子メールエンドポイント](programmatically-endpoints.md#add-an-email-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java APIを追加使用する電子メールエンドポイント {#add-an-email-endpoint-using-the-java-api}

Java APIを追加使用した電子メールエンドポイント：

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-livecycle-client.jarなどのクライアントJARファイルを含めます。

1. EndpointRegistry Clientオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `EndpointRegistryClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. 電子メールエンドポイントの属性を設定します。

   * コンストラクタを使用して `CreateEndpointInfo` オブジェクトを作成します。
   * オブジェクトのメソッドを呼び出し、文 `CreateEndpointInfo` 字列値を渡 `setConnectorId` して、コネクタ識別子の値を指定しま `Email`す。
   * オブジェクトのメソッドを呼び出し、エンドポ `CreateEndpointInfo` イントの説明を `setDescription` 記述するstring値を渡して、エンドポイントの説明を指定します。
   * オブジェクトのメソッドを呼び出し、名前 `CreateEndpointInfo` を指定する文 `setName` 字列値を渡して、エンドポイントの名前を指定します。
   * オブジェクトのメソッドを呼び出し、サービ `CreateEndpointInfo` ス名を指定 `setServiceId` する文字列値を渡して、エンドポイントが属するサービスを指定します。
   * オブジェクトのメソッドを呼び出し、操 `CreateEndpointInfo` 作名を指定 `setOperationName` する文字列値を渡すことで、呼び出す操作を指定します。 通常、Workbenchで作成されたプロセスから生成されたサービスの電子メールエンドポイントを作成する場合、操作の名前はinvokeです。

1. 設定値を指定します。

   電子メールエンドポイントに設定する各設定値に対して、オブジェクトのメソッドを呼び出 `CreateEndpointInfo` す必要があ `setConfigParameterAsText` ります。 例えば、設定値を設定す `smtpHost` るには、オブジェクトの `CreateEndpointInfo` メソッドを呼び出 `setConfigParameterAsText` し、次の値を渡します。

   * 設定値の名前を指定するstring値。 設定値を設定す `smtpHost` る際に、を指定しま `smtpHost`す。
   * 設定値の値を指定するstring値。 設定値を設定 `smtpHost` する場合は、SMTPサーバーの名前を指定するstring値を指定します。
   >[!NOTE]
   >
   >この節で紹介するEncryptDocumentサービスの設定値をすべて確認するには、 [QuickStartにあるJavaコードの例を参照してください。Java APIを使用した電子メールエンドポイントの追加](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-email-endpoint-using-the-java-api)。

1. 入力パラメーターの値を定義します。

   オブジェクトのメソッドを呼び出し、次 `CreateEndpointInfo` の値を渡して、 `setInputParameterMapping` 入力パラメーター値を定義します。

   * 入力パラメーターの名前を指定するstring値。 例えば、EncryptDocumentサービスの入力パラメーターの名前はです `InDoc`。
   * 入力パラメーターのデータタイプを指定するstring値。 例えば、入力パラメーターのデータタ `InDoc` イプはです `com.adobe.idp.Document`。
   * マッピングの種類を指定するstring値です。 For example, you can specify `variable`.
   * マッピングタイプの値を指定するstring値。 例えば、&amp;ast;.pdfをファイルパターンとして指定できます。
   >[!NOTE]
   >
   >定義する各入 `setInputParameterMapping` 力パラメーター値のメソッドを呼び出します。 EncryptDocumentプロセスには1つの入力パラメーターしかないので、このメソッドを1回呼び出す必要があります。

1. 出力パラメータの値を定義します。

   オブジェクトのメソッドを呼び出し、次 `CreateEndpointInfo` の値を渡して、 `setOutputParameterMapping` 出力パラメーターの値を定義します。

   * 出力パラメーターの名前を指定するstring値。 例えば、EncryptDocumentサービスの出力パラメーターの名前はです `SecuredDoc`。
   * 出力パラメーターのデータタイプを指定するstring値。 例えば、出力パラメーターのデータタ `SecuredDoc` イプはです `com.adobe.idp.Document`。
   * マッピングの種類を指定するstring値です。 For example, you can specify `%F.pdf`.

1. 電子メールエンドポイントを作成します。

   オブジェクトのメソッドを呼び出し、オ `EndpointRegistryClient` ブジェクトを渡 `createEndpoint` して、エンドポイントを作成 `CreateEndpointInfo` します。 このメソッドは、電子メールエ `Endpoint` ンドポイントを表すオブジェクトを返します。

1. エンドポイントを有効にします。

   オブジェクトのメソッドを呼び出し、 `EndpointRegistryClient` メソッドによ `enable` って返されたオブジ `Endpoint` ェクトを渡して、エンドポイントを有効に `createEndpoint` します。

**関連トピック**

[手順の概要](programmatically-endpoints.md#summary-of-steps)

[QuickStart:Java APIを使用した監視フォルダーエンドポイントの追加](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 電子メール設定値の定数ファイル {#email-configuration-values-constant-file}

クイッ [クスタート：Java APIを使用して電子メールエンドポイントを追加すると](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-email-endpoint-using-the-java-api) 、クイック開始をコンパイルするためにJavaプロジェクトの一部である必要がある定数ファイルが使用されます。 この定数ファイルは、電子メールエンドポイントを追加する際に設定する必要がある設定値を表します。 次のJavaコードは定数ファイルを表しています。

```as3
 /**
     * This class contains constants that can be used when setting email endpoint
     * configuration values
     */
 public class EmailEndpointConfigConstants {

     public static final String PROPERTY_EMAILPROVIDER_CRON_EXPRESSION = "cronExpression";
     public static final String PROPERTY_EMAILPROVIDER_REPREAT_COUNT = "repeatCount";
     public static final String PROPERTY_EMAILPROVIDER_REPREAT_INTERVAL = "repeatInterval";
     public static final String PROPERTY_EMAILPROVIDER_START_DELAY = "startDelay";
     public static final String PROPERTY_EMAILPROVIDER_BATCH_SIZE = "batchSize";
     public static final String PROPERTY_EMAILPROVIDER_USERNAME = "userName";
     public static final String PROPERTY_EMAILPROVIDER_DOMAINNAME = "domainName";
     public static final String PROPERTY_EMAILPROVIDER_DOMAINPATTERN = "domainPattern";
     public static final String PROPERTY_EMAILPROVIDER_FILEPATTERN = "filePattern";
     public static final String PROPERTY_EMAILPROVIDER_RECIPIENT_SUCCESSFUL_JOB = "recipientSuccessfulJob";
     public static final String PROPERTY_EMAILPROVIDER_RECIPIENT_FAILED_JOB = "recipientFailedJob";
     public static final String PROPERTY_EMAILPROVIDER_INBOX_HOST = "inboxHost";
     public static final String PROPERTY_EMAILPROVIDER_INBOX_PORT = "inboxPort";
     public static final String PROPERTY_EMAILPROVIDER_PROTOCOL = "inboxProtocol";
     public static final String PROPERTY_EMAILPROVIDER_INBOX_TIMEOUT = "inboxTimeOut";
     public static final String PROPERTY_EMAILPROVIDER_INBOX_USER = "inboxUser";
     public static final String PROPERTY_EMAILPROVIDER_INBOX_PASSWORD = "inboxPassword";
     public static final String PROPERTY_EMAILPROVIDER_INBOX_SSL = "inboxSSLEnabled";
     public static final String PROPERTY_EMAILPROVIDER_SMTP_HOST = "smtpHost";
     public static final String PROPERTY_EMAILPROVIDER_SMTP_PORT = "smtpPort";
     public static final String PROPERTY_EMAILPROVIDER_SMTP_USER = "smtpUser";
     public static final String PROPERTY_EMAILPROVIDER_SMTP_PASSWORD = "smtpPassword";
     public static final String PROPERTY_EMAILPROVIDER_CHARSET = "charSet";
     public static final String PROPERTY_EMAILPROVIDER_SMTP_SSL = "smtpSSLEnabled";
     public static final String PROPERTY_EMAILPROVIDER_FAILED_FOLDER = "failedJobFolder";
     public static final String PROPERTY_EMAILPROVIDER_ASYNCHRONOUS = "asynchronous";
 }
```

## リモートエンドポイントの追加 {#adding-remoting-endpoints}

>[!NOTE]
>
>JEE上のAEM formsでは、LiveCycle Remoting APIが廃止されました。

AEM Forms Java APIを使用して、プログラムによってリモートエンドポイントをサービスに追加できます。 リモートエンドポイントを追加すると、Flexアプリケーションでリモート処理を使用してサービスを呼び出せるようになります。 (『AEM Forms [でのAEM Formsの呼び出し（AEM Formsでは非推奨）』を参照](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting))。

プログラムによってリモートエンドポイントをサービスに追加する場合は、次のEncryptDocumentという短時間のみ有効なプロセスを考慮 *します*。

![ar_ar_encryptdocumentprocess](assets/ar_ar_encryptdocumentprocess.png)

このプロセスは、保護されていないPDFドキュメントを入力値として受け取り、保護されていないPDFドキュメントをEncryptionサービスの操作に渡し `EncryptPDFUsingPassword` ます。 PDFドキュメントはパスワードで暗号化され、パスワードで暗号化されたPDFドキュメントはこのプロセスの出力値です。 入力値の名前(保護されていないPDFドキュメント)とデ `InDoc` ータタイプはです `com.adobe.idp.Document`。 出力値の名前(パスワードで暗号化されたPDFドキュメント)とデ `SecuredDoc` ータタイプはです `com.adobe.idp.Document`。

この節では、リモートエンドポイントをサービスに追加する方法を示すために、EncryptDocumentという名前のサービスにリモートエンドポイントを追加します。

>[!NOTE]
>
>Webサービスを使用してリモートエンドポイントを追加することはできません。

### 手順の概要 {#summary_of_steps-4}

エンドポイントをサービスから削除するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. オブジェクトを作 `EndpointRegistryClient` 成します。
1. リモートエンドポイントの属性を設定します。
1. リモートエンドポイントの作成を参照してください。
1. エンドポイントを有効にします。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar（AEM FormsがJBoss Application Serverにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsがJBoss Application Serverにデプロイされている場合に必要）

For information about the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**EndpointRegistryクライアントオブジェクトの作成**

プログラムによってリモートエンドポイントを追加するには、オブジェクトを作成する必要が `EndpointRegistryClient` あります。

**リモートエンドポイントの属性の設定**

サービスのリモートエンドポイントを作成するには、次の値を指定します。

* **コネクタ識別子の値**:作成するエンドポイントのタイプを指定します。 リモートエンドポイントを作成するには、を指定しま `Remoting`す。
* **説明**:エンドポイントの説明を指定します。
* **名前**:エンドポイントの名前を指定します。
* **サービス識別子の値**:エンドポイントが属するサービスを指定します。 例えば、この節で紹介するプロセス（Workbench内でアクティブ化されるとプロセスがサービスになる）にリモートエンドポイントを追加するには、を指定しま `EncryptDocument`す。
* **操作名**:エンドポイントを使用して呼び出される操作の名前を指定します。 リモートエンドポイントを作成する場合は、ワイルドカード文字(&amp;ast;)を指定します。

**リモートエンドポイントの作成**

リモートエンドポイント属性を設定した後、サービスのリモートエンドポイントを作成できます。

**エンドポイントの有効化**

新しいエンドポイントを作成したら、有効にする必要があります。 リモートエンドポイントが有効な場合、Flexクライアントがサービスを呼び出せるようにします。

**関連トピック**

[Java APIを追加使用したリモートエンドポイント](programmatically-endpoints.md#add-a-remoting-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java APIを追加使用したリモートエンドポイント {#add-a-remoting-endpoint-using-the-java-api}

Java 追加 APIを使用したリモートエンドポイント：

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-livecycle-client.jarなどのクライアントJARファイルを含めます。

1. EndpointRegistry Clientオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `EndpointRegistryClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. リモートエンドポイントの属性を設定します。

   * コンストラクタを使用して `CreateEndpointInfo` オブジェクトを作成します。
   * オブジェクトのメソッドを呼び出し、文 `CreateEndpointInfo` 字列値を渡 `setConnectorId` して、コネクタ識別子の値を指定しま `Remoting`す。
   * オブジェクトのメソッドを呼び出し、エンドポ `CreateEndpointInfo` イントの説明を `setDescription` 記述するstring値を渡して、エンドポイントの説明を指定します。
   * オブジェクトのメソッドを呼び出し、名前 `CreateEndpointInfo` を指定する文 `setName` 字列値を渡して、エンドポイントの名前を指定します。
   * オブジェクトのメソッドを呼び出し、サービ `CreateEndpointInfo` ス名を指定 `setServiceId` する文字列値を渡して、エンドポイントが属するサービスを指定します。
   * オブジェクトのメソッドによって呼び出 `CreateEndpointInfo` される操作を `setOperationName` 指定し、操作名を指定する文字列値を渡します。 リモートエンドポイントの場合は、ワイルドカード文字(&amp;ast;)を指定します。

1. リモートエンドポイントの作成を参照してください。

   オブジェクトのメソッドを呼び出し、オ `EndpointRegistryClient` ブジェクトを渡 `createEndpoint` して、エンドポイントを作成 `CreateEndpointInfo` します。 このメソッドは、新しいリモ `Endpoint` ートエンドポイントを表すオブジェクトを返します。

1. エンドポイントを有効にします。

   オブジェクトのメソッドを呼び出し、 `EndpointRegistryClient` メソッドによ `enable` って返されたオブジ `Endpoint` ェクトを渡して、エンドポイントを有効に `createEndpoint` します。

**関連トピック**

[手順の概要](programmatically-endpoints.md#summary-of-steps)

[QuickStart:Java APIを使用したリモートエンドポイントの追加](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-remoting-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## TaskManagerエンドポイントの追加 {#adding-taskmanager-endpoints}

AEM Forms Java APIを使用して、プログラムによってTaskManagerエンドポイントをサービスに追加できます。 TaskManagerエンドポイントをサービスに追加することで、Workspaceユーザーがサービスを呼び出せるようにします。 つまり、Workspaceで作業しているユーザーは、対応するTaskManagerエンドポイントを持つプロセスを呼び出すことができます。

>[!NOTE]
>
>Webサービスを使用してTaskManagerエンドポイントを追加することはできません。

### 手順の概要 {#summary_of_steps-5}

TaskManagerエンドポイントをサービスに追加するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. オブジェクトを作 `EndpointRegistryClient` 成します。
1. エンドポイントのカテゴリを作成します。
1. TaskManagerエンドポイントの属性を設定します。
1. TaskManagerエンドポイントを作成します。
1. エンドポイントを有効にします。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar（AEM FormsがJBoss Application Serverにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsがJBoss Application Serverにデプロイされている場合に必要）

For information about the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**EndpointRegistryクライアントオブジェクトの作成**

プログラムによってTaskManagerエンドポイントを追加する前に、オブジェクトを作成する必要があ `EndpointRegistryClient` ります。

**エンドポイントのカテゴリを作成します**

カテゴリは、Workspace内のサービスを整理するために使用されます。 つまり、Workspaceユーザーは、Workspace内でエンドポイントを選択することで、TaskManagerエンドポイントを持つサービスをカテゴリできます。 TaskManagerエンドポイントを作成する場合は、既存のエンドポイントを参照するか、新しいカテゴリをプログラムで作成することができます。カテゴリ

>[!NOTE]
>
>この節では、TaskManagerカテゴリをサービスに追加する際に、新しいエンドポイントを作成します。

**TaskManagerエンドポイント属性の設定**

サービスのTaskManagerエンドポイントを作成するには、次の値を指定します。

* **コネクタ識別子**:作成するエンドポイントのタイプを指定します。 TaskManagerエンドポイントを作成するには、を指定しま `TaskManagerConnector`す。
* **説明**:エンドポイントの説明を指定します。
* **名前**:エンドポイントの名前を指定します。
* **サービス識別子**:エンドポイントが属するサービスを指定します。
* **カテゴリ**:TaskManagerカテゴリに関連付けられているエンドポイント識別子の値を指定します。
* **操作名**:通常、Workbenchで作成されたプロセスから生成されたサービスのTaskManagerエンドポイントを作成する場合、操作の名前はです `invoke`。

**TaskManagerエンドポイントの作成**

TaskManagerエンドポイント属性を設定した後、サービスのTaskManagerエンドポイントを作成できます。

**エンドポイントの有効化**

新しいエンドポイントを作成したら、有効にする必要があります。 エンドポイントが有効な場合、Workspace内からサービスを呼び出すために使用できます。 エンドポイントを有効にした後、管理コンソール内で表示することができます。

**関連トピック**

[Java APIを追加使用するTaskManagerエンドポイント](programmatically-endpoints.md#add-a-taskmanager-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java APIを追加使用するTaskManagerエンドポイント {#add-a-taskmanager-endpoint-using-the-java-api}

Java APIを使追加用したTaskManagerエンドポイント：

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-livecycle-client.jarなどのクライアントJARファイルを含めます。

1. EndpointRegistry Clientオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `EndpointRegistryClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. エンドポイントのカテゴリを作成します。

   * Create a `CreateEndpointCategoryInfo` object by using its constructor and passing the following values:

      * カテゴリの識別子の値を指定するstring値
      * カテゴリ
   * オブジェクトのカテゴリを作成するに `EndpointRegistryClient` は、オブジェクトのメ `createEndpointCategory` ソッドを呼び出し、オブジェクトを渡 `CreateEndpointCategoryInfo` します。 このメソッドは、新しい `EndpointCategory` メソッドを表すオブジェクトを返しますカテゴリ。


1. TaskManagerエンドポイントの属性を設定します。

   * コンストラクタを使用して `CreateEndpointInfo` オブジェクトを作成します。
   * オブジェクトのメソッドを呼び出し、文 `CreateEndpointInfo` 字列値を渡 `setConnectorId` して、コネクタ識別子の値を指定しま `TaskManagerConnector`す。
   * オブジェクトのメソッドを呼び出し、エンドポ `CreateEndpointInfo` イントの説明を `setDescription` 記述するstring値を渡して、エンドポイントの説明を指定します。
   * オブジェクトのメソッドを呼び出し、名前 `CreateEndpointInfo` を指定する文 `setName` 字列値を渡して、エンドポイントの名前を指定します。
   * オブジェクトのメソッドを呼び出し、サービ `CreateEndpointInfo` ス名を指定 `setServiceId` する文字列値を渡して、エンドポイントが属するサービスを指定します。
   * オブジェクトのカテゴリを呼び出し、エンドポイ `CreateEndpointInfo` ントが属するカテゴリ `setCategoryId` を指定し、エンドポイント識別子の値を指定する文字列値を渡します。 オブジェクトのメ `EndpointCategory` ソッドを呼び `getId` 出して、このメソッドの識別子の値を取得できます。カテゴリ
   * オブジェクトのメソッドを呼び出し、操 `CreateEndpointInfo` 作名を指定 `setOperationName` する文字列値を渡すことで、呼び出す操作を指定します。 通常、Workbenchで作成されたプ `TaskManager` ロセスから派生するサービスのエンドポイントを作成する場合、操作の名前はで `invoke`す。

1. TaskManagerエンドポイントを作成します。

   オブジェクトのメソッドを呼び出し、オ `EndpointRegistryClient` ブジェクトを渡 `createEndpoint` して、エンドポイントを作成 `CreateEndpointInfo` します。 このメソッドは、新しいTaskManager `Endpoint` エンドポイントを表すオブジェクトを返します。

1. エンドポイントを有効にします。

   オブジェクトのメソッドを呼び出し、 `EndpointRegistryClient` メソッドによ `enable` って返されたオブジ `Endpoint` ェクトを渡して、エンドポイントを有効に `createEndpoint` します。

**関連トピック**

[手順の概要](programmatically-endpoints.md#summary-of-steps)

[QuickStart:Java APIを使用したTaskManagerエンドポイントの追加](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-taskmanager-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## エンドポイントの変更 {#modifying-endpoints}

AEM Forms Java APIを使用して、既存のエンドポイントをプログラムで変更できます。 エンドポイントを変更すると、エンドポイントの動作を変更できます。 例えば、監視フォルダーとして使用されるフォルダーを指定する監視フォルダーエンドポイントがあるとします。 監視フォルダーエンドポイントに属する設定値をプログラムによって変更すると、別のフォルダーが監視フォルダーとして機能します。 監視フォルダーエンドポイントに属する設定値について詳しくは、「監視フォルダーエンドポイントの追 [加」を参照してくださ](programmatically-endpoints.md#adding-watched-folder-endpoints)い。

エンドポイントの変更方法を示すために、この節では、監視フォルダーとして動作するフォルダーを変更して、監視フォルダーエンドポイントを変更します。

>[!NOTE]
>
>Webサービスを使用してエンドポイントを変更することはできません。

### 手順の概要 {#summary_of_steps-6}

エンドポイントを変更するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. オブジェクトを作 `EndpointRegistryClient` 成します。
1. エンドポイントを取得します。
1. 新しい設定値を指定します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar（AEM FormsがJBoss Application Serverにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsがJBoss Application Serverにデプロイされている場合に必要）

For information about the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**EndpointRegistryクライアントオブジェクトの作成**

エンドポイントをプログラムで変更するには、オブジェクトを作成する必要が `EndpointRegistryClient` あります。

**変更するエンドポイントの取得**

エンドポイントを変更する前に、エンドポイントを取得する必要があります。 エンドポイントを取得するには、エンドポイントにアクセスできるユーザーとして接続する必要があります。 管理者として接続することをお勧めします。 (See [Setting connection properties](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)).

エンドポイントのリストを取得できます。 その後、削除する特定のリストを検索し、エンドポイントを繰り返し処理できます。 例えば、エンドポイントに対応するサービスとエンドポイントのタイプを決定することで、エンドポイントを特定できます。 エンドポイントを見つけたら、それを変更できます。

**新しい設定値の指定**

エンドポイントを変更する場合は、新しい設定値を指定します。 例えば、監視フォルダーエンドポイントを変更するには、変更するものだけでなく、すべての監視フォルダーエンドポイントの設定値をリセットします。 監視フォルダーエンドポイントに属する設定値について詳しくは、「監視フォルダーエンドポイントの追 [加」を参照してくださ](programmatically-endpoints.md#adding-watched-folder-endpoints)い。

>[!NOTE]
>
>電子メールエンドポイントに属する設定値について詳しくは、「電子メールエンドポイントの追 [加」を参照してくださ](programmatically-endpoints.md#adding-email-endpoints)い。

>[!NOTE]
>
>エンドポイントによって呼び出されるサービスは変更できません。 サービスを変更しようとすると、例外が発生します。 特定のエンドポイントに関連付けられたサービスを変更するには、エンドポイントを削除し、新しいエンドポイントを作成します。 (エンドポイ [ントの削除を参照](programmatically-endpoints.md#removing-endpoints))。

**関連トピック**

[Java APIを使用したエンドポイントの変更](programmatically-endpoints.md#modifying-an-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java APIを使用したエンドポイントの変更 {#modifying-an-endpoint-using-the-java-api}

Java APIを使用してエンドポイントを変更します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-livecycle-client.jarなどのクライアントJARファイルを含めます。

1. EndpointRegistry Clientオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `EndpointRegistryClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. 変更するエンドポイントを取得します。

   * 現在のユーザー（接続プロパティで指定）がアクセスできるすべてのエンドポイントのリストを取得するには、オブジェクトのメソッドを呼び出し、フィルターとして `EndpointRegistryClient` 機能するオブジ `getEndpoints``PagingFilter` ェクトを渡します。 値を渡すと、すべてのエ `(PagingFilter)null` ンドポイントを返すことができます。 このメソッドは、各要素がオ `java.util.List` ブジェクトであるオブジェクトを返 `Endpoint` します。 オブジェクトについて詳し `PagingFilter` くは、『 [AEM Forms APIリファレンス』を参照してください](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。
   * オブジェクトを繰り返し `java.util.List` 処理し、オブジェクトにエンドポイントがあるかどうかを確認します。 エンドポイントが存在する場合、各要素はインスタンス `EndPoint` です。
   * オブジェクトのメソッドを呼び出して、エンドポイントに対応する `EndPoint` サービスを特定 `getServiceId` します。 このメソッドは、サービス名を指定するstring値を返します。
   * オブジェクトのメソッドを呼び出して、エンドポ `EndPoint` イントのタイプを決 `getConnectorId` 定します。 このメソッドは、エンドポイントのタイプを指定するstring値を返します。 例えば、エンドポイントが監視フォルダーエンドポイントの場合、このメソッドはを返しま `WatchedFolder`す。

1. 新しい設定値を指定します。

   * Create a `ModifyEndpointInfo` object by invoking its constructor.
   * 設定する各設定値に対して、オブジェクトの `ModifyEndpointInfo` メソッドを呼び出 `setConfigParameterAsText` します。 例えば、URL設定値を設定するには、オブジェクトのメソ `ModifyEndpointInfo` ッドを呼び出し `setConfigParameterAsText` 、次の値を渡します。

      * 設定値の名前を指定するstring値。 例えば、設定値を設定する `url` には、を指定しま `url`す。
      * 設定値の値を指定するstring値。 設定値の値を定義するには、 `url` 監視フォルダーの場所を指定します。
   * Invoke the `EndpointRegistryClient` object’s `modifyEndpoint` method and pass the `ModifyEndpointInfo` object.


**関連トピック**

[手順の概要](programmatically-endpoints.md#summary-of-steps)

[QuickStart:Java APIを使用したエンドポイントの変更](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-modifying-an-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## エンドポイントの削除 {#removing-endpoints}

AEM Forms Java APIを使用して、プログラムによってエンドポイントをサービスから削除できます。 エンドポイントを削除すると、エンドポイントで有効になっている呼び出し方法を使用してサービスを呼び出すことはできません。 例えば、サービスからSOAPエンドポイントを削除した場合、SOAPモードを使用してサービスを呼び出すことはできません。

サービスからエンドポイントを削除する方法を示すために、この節では、EncryptDocumentという名前のサービスからEJBエンドポイントを削除 *します*。

>[!NOTE]
>
>Webサービスを使用してエンドポイントを削除することはできません。

### 手順の概要 {#summary_of_steps-7}

エンドポイントをサービスから削除するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. オブジェクトを作 `EndpointRegistryClient` 成します。
1. エンドポイントを取得します。
1. エンドポイントを削除します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar（AEM FormsがJBoss Application Serverにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsがJBoss Application Serverにデプロイされている場合に必要）

For information about the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**EndpointRegistryクライアントオブジェクトの作成**

エンドポイントをプログラムによって削除するには、オブジェクトを作成する必要が `EndpointRegistryClient` あります。

**削除するエンドポイントの取得**

エンドポイントを削除する前に、エンドポイントを取得する必要があります。 エンドポイントを取得するには、エンドポイントにアクセスできるユーザーとして接続する必要があります。 管理者として接続することをお勧めします。 (See [Setting connection properties](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)).

エンドポイントのリストを取得できます。 その後、削除する特定のリストを検索し、エンドポイントを繰り返し処理できます。 例えば、エンドポイントに対応するサービスとエンドポイントのタイプを決定することで、エンドポイントを特定できます。 エンドポイントを見つけたら、それを削除できます。

**エンドポイントの削除**

新しいエンドポイントを作成したら、有効にする必要があります。 エンドポイントが有効な場合は、サービスの呼び出しに使用できます。 エンドポイントを有効にした後、管理コンソール内で表示することができます。

**関連トピック**

[Java APIを使用したエンドポイントの削除](programmatically-endpoints.md#removing-an-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java APIを使用したエンドポイントの削除 {#removing-an-endpoint-using-the-java-api}

Java APIを使用してエンドポイントを削除します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-livecycle-client.jarなどのクライアントJARファイルを含めます。

1. EndpointRegistry Clientオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `EndpointRegistryClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. 削除するエンドポイントを取得します。

   * 現在のユーザー（接続プロパティで指定）がアクセス権を持つすべてのエンドポイントのリストを取得するには、オブジェクトのメソッドを呼び出し、フィルターとして `EndpointRegistryClient` 機能するオブジ `getEndpoints``PagingFilter` ェクトを渡します。 すべてのエンドポイント `(PagingFilter)null` を返すために渡すことができます。 このメソッドは、各要素がオ `java.util.List` ブジェクトであるオブジェクトを返 `Endpoint` します。
   * オブジェクトを繰り返し `java.util.List` 処理し、オブジェクトにエンドポイントがあるかどうかを確認します。 エンドポイントが存在する場合、各要素はインスタンス `EndPoint` です。
   * オブジェクトのメソッドを呼び出して、エンドポイントに対応する `EndPoint` サービスを特定 `getServiceId` します。 このメソッドは、サービス名を指定するstring値を返します。
   * オブジェクトのメソッドを呼び出して、エンドポ `EndPoint` イントのタイプを決 `getConnectorId` 定します。 このメソッドは、エンドポイントのタイプを指定するstring値を返します。 例えば、エンドポイントがEJBエンドポイントの場合、このメソッドはを返しま `EJB`す。

1. エンドポイントを削除します。

   オブジェクトのメソッドを呼び出し、 `EndpointRegistryClient` 削除するエ `remove` ンドポイントを表すオ `EndPoint` ブジェクトを渡して、エンドポイントを削除します。

**関連トピック**

[手順の概要](programmatically-endpoints.md#summary-of-steps)

[QuickStart:Java APIを使用したエンドポイントの削除](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-removing-an-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## エンドポイントコネクタ情報の取得 {#retrieving-endpoint-connector-information}

AEM Forms APIを使用して、エンドポイントコネクタに関する情報をプログラムで取得できます。 コネクタは、エンドポイントが様々な呼び出し方法を使用してサービスを呼び出せるようにします。 例えば、監視フォルダーコネクターを使用すると、エンドポイントで監視フォルダーを使用してサービスを呼び出すことができます。 エンドポイントコネクタに関する情報をプログラムによって取得することで、必要な設定値やオプションの設定値など、コネクタに関連付けられた設定値を取得できます。

エンドポイントコネクタに関する情報を取得する方法を示すために、この節では監視フォルダーコネクタに関する情報を取得します。 (See [Adding Watched Folder Endpoints](programmatically-endpoints.md#adding-watched-folder-endpoints).)

>[!NOTE]
>
>Webサービスを使用してエンドポイントに関する情報を取得することはできません。

>[!NOTE]
>
>このトピックでは、 `ConnectorRegistryClient` APIを使用してエンドポイントコネクタに関する情報を取得します。 (『 [AEM Forms APIリファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)』を参照)。

### 手順の概要 {#summary_of_steps-8}

エンドポイントコネクタ情報を取得するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. オブジェクトを作 `ConnectorRegistryClient` 成します。
1. コネクタタイプを指定します。
1. 設定値を取得します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar（AEM FormsがJBoss Application Serverにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsがJBoss Application Serverにデプロイされている場合に必要）

AEM FormsがJBoss以外のサポート対象のJ2EEアプリケーションサーバーにデプロイされている場合は、adobe-utilities.jarおよびjbossall-client.jarを、AEM FormsがデプロイされているJ2EEアプリケーションサーバーに固有のJARファイルに置き換えます。 For information about the location of all AEM Forms JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**ConnectorRegistryクライアントオブジェクトの作成**

エンドポイントコネクタの情報をプログラムで取得するには、オブジェクトを作 `ConnectorRegistryClient` 成します。

**コネクタタイプを指定**

情報を取得するコネクタのタイプを指定します。 次のタイプのコネクタが存在します。

* **EJB**:クライアントアプリケーションがEJBモードを使用してサービスを呼び出せるようにします。
* **SOAP**:クライアントアプリケーションがSOAPモードを使用してサービスを呼び出せるようにします。
* **監視フォルダー**:監視フォルダーがサービスを呼び出せるようにします。
* **電子メール**:電子メールメッセージでサービスを呼び出せるようにします。
* **リモート**:Flexクライアントアプリケーションからサービスを呼び出せるようにします。
* **TaskManagerConnector**:WorkspaceユーザーがWorkspace内からサービスを呼び出せるようにします。

**設定値の取得**

コネクタタイプを指定すると、サポートされている設定値など、コネクタに関する情報を取得できます。 例えば、任意のコネクタの場合、どの設定値が必須で、どの設定値がオプションかを指定できます。

**関連トピック**

[Java APIを使用したエンドポイントコネクタ情報の取得](programmatically-endpoints.md#retrieve-endpoint-connector-information-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java APIを使用したエンドポイントコネクタ情報の取得 {#retrieve-endpoint-connector-information-using-the-java-api}

Java APIを使用して、エンドポイントコネクタ情報を取得します。

1. プロジェクトファイルを含めます。.

   Javaプロジェクトのクラスパスに、adobe-livecycle-client.jarなどのクライアントJARファイルを含めます。

1. ConnectorRegistry Clientオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `ConnectorRegistryClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. コネクタタイプを指定します。

   オブジェクトのメソッドを呼び出し、コ `ConnectorRegistryClient` ネクタの種 `getEndpointDefinition` 類を指定する文字列値を渡して、コネクタの種類を指定します。 例えば、監視フォルダーのコネクタタイプを指定するには、文字列値を渡しま `WatchedFolder`す。 このメソッドは、コネクタ `Endpoint` の種類に対応するオブジェクトを返します。

1. 設定値を取得します。

   * オブジェクトのメソッドを呼び出して、このエンドポイント内で関連付けら `Endpoint` れている設定値を取得 `getConfigParameters` します。 このメソッドは、オブジェクトの配列を返 `ConfigParameter` します。
   * 配列内の各要素を取得して、各設定値に関する情報を取得します。 各要素はオブジェクト `ConfigParameter` です。 例えば、オブジェクトのメソッドを呼び出して、設定値が必須か任意かを `ConfigParameter` 判断でき `isRequired` ます。 設定値が必要な場合、このメソッドはを返しま `true`す。

**関連トピック**

[手順の概要](programmatically-endpoints.md#summary-of-steps)

[QuickStart:Java APIを使用したエンドポイントコネクタ情報の取得](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-retrieving-endpoint-connector-information-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
