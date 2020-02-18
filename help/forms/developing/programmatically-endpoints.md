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
source-git-commit: 8bc99ed3817398ae358d439a5c1fcc90bbd24327

---


# エンドポイントのプログラムによる管理 {#programmatically-managing-endpoints}

**エンドポイントレジストリサービスについて**

Endpoint Registryサービスは、エンドポイントをプログラムで管理する機能を提供します。 例えば、次の種類のエンドポイントをサービスに追加できます。

* EJB
* SOAP
* 監視フォルダー
* 電子メール
* （AEM formsでは非推奨）Remoting
* タスクマネージャー

   ***注意&#x200B;**:SOAP、EJBおよび（JEE上のAEM formsでは非推奨）リモートエンドポイントは、アクティブ化された各サービスに対して自動的に作成されます。 SOAPおよびEJBエンドポイントは、すべてのサービス操作に対してSOAPおよびEJBを有効にします。*

   リモートエンドポイントを使用すると、Flexクライアントは、エンドポイントが追加されたAEM Formsサービス上の操作を呼び出すことができます。 エンドポイントと同じ名前のFlex宛先が作成され、Flexクライアントは、この宛先を指すRemoteObjectsを作成して、関連するサービスの操作を呼び出すことができます。

   電子メール、タスクマネージャーおよび監視フォルダーのエンドポイントで公開されるのは、サービスの特定の操作のみです。 これらのエンドポイントを追加するには、呼び出すメソッドを選択し、設定パラメーターを設定し、入力および出力パラメーターのマッピングを指定する、2番目の設定手順が必要です。

   TaskManagerエンドポイントは、カテゴリと呼ばれるグループに編成で *きます*。 これらのカテゴリはTaskManagerを通じてWorkspaceに公開され、エンドユーザーはTaskManagerエンドポイントを分類されたとおりに表示します。 Workspace内では、エンドユーザーはナビゲーションパネルにこれらのカテゴリを表示できます。 各カテゴリ内のエンドポイントは、Workspaceのプロセスの開始ページにプロセスカードとして表示されます。

   Endpoint Registryサービスを使用して、次のタスクを実行できます。

* EJBエンドポイントを追加します。 (「EJBエンド [ポイントの追加](programmatically-endpoints.md#adding-ejb-endpoints)」を参照)。
* SOAPエンドポイントを追加します。 (SOAPエンドポ [イントの追加を参照](programmatically-endpoints.md#adding-soap-endpoints))。
* 監視フォルダーエンドポイントの追加(監視フ [ォルダーエンドポイントの追加](programmatically-endpoints.md#adding-watched-folder-endpoints)を参照)。
* 電子メールエンドポイントの追加を参照してください。 (See [Adding Email Endpoints](programmatically-endpoints.md#adding-email-endpoints).)
* リモートエンドポイントの追加を参照してください。 (「リモートエ [ンドポイントの追加](programmatically-endpoints.md#adding-remoting-endpoints)」を参照)。
* TaskManagerエンドポイントの追加(TaskManagerエ [ンドポイントの追加](programmatically-endpoints.md#adding-taskmanager-endpoints)を参照)。
* エンドポイントの変更(エン [ドポイントの変更](programmatically-endpoints.md#modifying-endpoints)を参照)
* エンドポイントの削除(エン [ドポイントの削除](programmatically-endpoints.md#removing-endpoints)を参照)。
* エンドポイントコネクタ情報の取得(エ [ンドポイントコネクタ情報の取得を参照](programmatically-endpoints.md#retrieving-endpoint-connector-information))。

## EJBエンドポイントの追加 {#adding-ejb-endpoints}

AEM Forms Java APIを使用して、プログラムでEJBエンドポイントをサービスに追加できます。 EJBエンドポイントをサービスに追加すると、クライアントアプリケーションでEJBモードを使用してサービスを呼び出せるようになります。 つまり、AEM Formsの呼び出しに必要な接続プロパティを設定する場合は、EJBモードを選択できます。 （[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照。）

>[!NOTE]
>
>Webサービスを使用してEJBエンドポイントを追加することはできません。

>[!NOTE]
>
>通常、EJBエンドポイントはデフォルトでサービスに追加されますが、EJBエンドポイントは、プログラム的にデプロイされたプロセスや、EJBエンドポイントが削除され、再度追加する必要があるプロセスに追加できます。

### 手順の概要 {#summary-of-steps}

EJBエンドポイントをサービスに追加するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. オブジェクトを作 `EndpointRegistry Client` 成します。
1. EJBエンドポイント属性を設定します。
1. EJBエンドポイントを作成します。
1. エンドポイントを有効にします。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。 次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar（AEM FormsがJBoss Application serverにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsがJBoss Application Serverにデプロイされている場合に必要）

For information about the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**EndpointRegistry clientオブジェクトの作成**

EJBエンドポイントをプログラムで追加する前に、オブジェクトを作成する必要があ `EndpointRegistryClient` ります。

**EJBエンドポイント属性の設定**

サービスのEJBエンドポイントを作成するには、次の値を指定します。

* **コネクタ識別子**:作成するエンドポイントのタイプを指定します。 EJBエンドポイントを作成するには、を指定しま `EJB`す。
* **説明**:エンドポイントの説明を指定します。
* **名前**:エンドポイントの名前を指定します。
* **サービス識別子**:エンドポイントが属するサービスを指定します。
* **操作名**:エンドポイントを使用して呼び出される操作の名前を指定します。 EJBエンドポイントを作成する場合は、ワイルドカード文字( `*`)を指定します。 ただし、すべてのサービス操作を呼び出すのではなく、特定の操作を指定する場合は、ワイルドカード文字( `*`)を使用するのではなく、操作の名前を指定します。

**EJBエンドポイントの作成**

EJBエンドポイント属性を設定した後、サービス用のEJBエンドポイントを作成できます。

**エンドポイントの有効化**

新しいエンドポイントを作成した後、そのエンドポイントを有効にする必要があります。 エンドポイントを有効にした後は、そのエンドポイントを使用してサービスを呼び出すことができます。 エンドポイントを有効にした後、管理コンソール内でエンドポイントを表示できます。

**関連トピック**

[Java APIを使用したEJBエンドポイントの追加](programmatically-endpoints.md#adding-an-ejb-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java APIを使用したEJBエンドポイントの追加 {#adding-an-ejb-endpoint-using-the-java-api}

Java APIを使用してEJBエンドポイントを追加します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-livecycle-client.jarなどのクライアントJARファイルを含めます。 （

1. EndpointRegistry clientオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `EndpointRegistryClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. EJBエンドポイント属性を設定します。

   * コンストラクタを使用して `CreateEndpointInfo` オブジェクトを作成します。
   * コネクタ識別子の値を指定するには、オブジェクトの `CreateEndpointInfo` メソッドを呼び出 `setConnectorId` し、文字列値を渡しま `EJB`す。
   * オブジェクトのメソッドを呼び出し、エンドポ `CreateEndpointInfo` イントを説明 `setDescription` する文字列値を渡して、エンドポイントの説明を指定します。
   * オブジェクトのメソッドを呼び出し、名前を `CreateEndpointInfo` 指定するstring値 `setName` を渡して、エンドポイントの名前を指定します。
   * オブジェクトのメソッドを呼び出し、サービス名を指 `CreateEndpointInfo` 定するstring値を `setServiceId` 渡して、エンドポイントが属するサービスを指定します。
   * オブジェクトのメソッドを呼び出して呼び出 `CreateEndpointInfo` す操作を指 `setOperationName` 定し、操作名を指定するstring値を渡します。 SOAPおよびEJBエンドポイントの場合は、すべての操作を示すワイルドカ `*`ード文字()を指定します。

1. EJBエンドポイントを作成します。

   オブジェクトのメソッドを呼び出し、オ `EndpointRegistryClient` ブジェクトを渡すこ `createEndpoint` とで、エンドポイントを作 `CreateEndpointInfo` 成します。 このメソッドは、新しいEJB `Endpoint` エンドポイントを表すオブジェクトを返します。

1. エンドポイントを有効にします。

   オブジェクトのenableメソッドを呼び出し、 `EndpointRegistryClient` そのメソッドによって返されたオブジェクトを渡すこ `Endpoint` とで、エンドポイントを有効に `createEndpoint` します。

**関連トピック**

[手順の概要](programmatically-endpoints.md#summary-of-steps)

[QuickStart:Java APIを使用したEJBエンドポイントの追加](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-ejb-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## SOAPエンドポイントの追加 {#adding-soap-endpoints}

AEM Forms Java APIを使用して、プログラムによってSOAPエンドポイントをサービスに追加できます。 SOAPエンドポイントを追加すると、クライアントアプリケーションでSOAPモードを使用してサービスを呼び出せるようになります。 つまり、AEM Formsの呼び出しに必要な接続プロパティを設定する場合は、SOAPモードを選択できます。

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
* adobe-utilities.jar（AEM FormsがJBoss Application serverにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsがJBoss Application Serverにデプロイされている場合に必要）

これらのJARファイルは、SOAPエンドポイントを作成するために必要です。 ただし、SOAPエンドポイントを使用してサービスを呼び出す場合は、追加のJARファイルが必要です。 AEM Forms JARファイルについて詳しくは、「AEM Forms javaライブラリフ [ァイルを含める」を参照してください](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**EndpointRegistry clientオブジェクトの作成**

プログラムによってSOAPエンドポイントをサービスに追加するには、オブジェクトを作成する必要があ `EndpointRegistryClient` ります。

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

新しいエンドポイントを作成した後、そのエンドポイントを有効にする必要があります。 エンドポイントが有効な場合は、サービスの呼び出しに使用できます。 エンドポイントを有効にすると、管理コンソール内でエンドポイントを表示できます。

**関連トピック**

[Java APIを使用したSOAPエンドポイントの追加](programmatically-endpoints.md#add-a-soap-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java APIを使用したSOAPエンドポイントの追加 {#add-a-soap-endpoint-using-the-java-api}

Java APIを使用してSOAPエンドポイントをサービスに追加します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-livecycle-client.jarなどのクライアントJARファイルを含めます。

1. EndpointRegistry clientオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `EndpointRegistryClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. SOAPエンドポイント属性を設定します。

   * コンストラクタを使用して `CreateEndpointInfo` オブジェクトを作成します。
   * コネクタ識別子の値を指定するには、オブジェクトの `CreateEndpointInfo` メソッドを呼び出 `setConnectorId` し、文字列値を渡しま `SOAP`す。
   * オブジェクトのメソッドを呼び出し、エンドポ `CreateEndpointInfo` イントを説明 `setDescription` する文字列値を渡して、エンドポイントの説明を指定します。
   * オブジェクトのメソッドを呼び出し、名前を `CreateEndpointInfo` 指定するstring値 `setName` を渡して、エンドポイントの名前を指定します。
   * オブジェクトのメソッドを呼び出し、サービス名を指 `CreateEndpointInfo` 定するstring値を `setServiceId` 渡して、エンドポイントが属するサービスを指定します。
   * オブジェクトのメソッドを呼び出し、操作 `CreateEndpointInfo` 名を指定 `setOperationName` する文字列値を渡して、呼び出す操作を指定します。 SOAPおよびEJBエンドポイントの場合は、すべての操作を示すワイルドカ `*`ード文字()を指定します。

1. SOAPエンドポイントを作成します。

   オブジェクトのメソッドを呼び出し、オ `EndpointRegistryClient` ブジェクトを渡すこ `createEndpoint` とで、エンドポイントを作 `CreateEndpointInfo` 成します。 このメソッドは、新しいSOAP `Endpoint` エンドポイントを表すオブジェクトを返します。

1. エンドポイントを有効にします。

   オブジェクトのenableメソッドを呼び出し、 `EndpointRegistryClient` そのメソッドによって返されたオブジ `Endpoint` ェクトを渡して、エンドポイントを有効に `createEndpoint` します。

**関連トピック**

[手順の概要](programmatically-endpoints.md#summary-of-steps)

[QuickStart:Java APIを使用したSOAPエンドポイントの追加](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-soap-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 監視フォルダーエンドポイントの追加 {#adding-watched-folder-endpoints}

AEM Forms Java APIを使用して、監視フォルダーエンドポイントをプログラムでサービスに追加できます。 監視フォルダーエンドポイントを追加すると、ユーザーはファイル（PDFファイルなど）をフォルダーに配置できます。 ファイルがフォルダーに配置されると、設定済みのサービスが呼び出され、ファイルが操作されます。 サービスが指定の操作を実行した後に、変更されたファイルが指定の出力フォルダーに保存されます。監視フォルダーは、固定レートの間隔で、または毎週月曜日、水曜日、金曜日の正午など、Cronスケジュールでスキャンされるように設定されます。

プログラムによって監視フォルダーエンドポイントをサービスに追加する場合は、EncryptDocumentという短時間のみ有効なプロセスを考慮し *てくださ*&#x200B;い。 (「AEM Formsプ [ロセスについて](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes)」を参照)。

![aw_aw_encryptdocumentprocess](assets/aw_aw_encryptdocumentprocess.png)

このプロセスは、保護されていないPDFドキュメントを入力値として受け取り、保護されていないPDFドキュメントをEncryptionサービスの操作に渡 `EncryptPDFUsingPassword` します。 PDFドキュメントはパスワードで暗号化され、パスワードで暗号化されたPDFドキュメントはこのプロセスの出力値です。 入力値の名前（保護されていないPDFドキュメント）とデ `InDoc` ータタイプはです `com.adobe.idp.Document`。 出力値の名前（パスワードで暗号化されたPDFドキュメント）とデ `SecuredDoc` ータタイプはです `com.adobe.idp.Document`。

>[!NOTE]
>
>Webサービスを使用して監視フォルダーエンドポイントを追加することはできません。

### 手順の概要 {#summary_of_steps-2}

監視フォルダーエンドポイントをサービスに追加するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. オブジェクトを作 `EndpointRegistryClient` 成します。
1. 監視フォルダーエンドポイントの属性を設定します。
1. 設定値を指定します。
1. 入力パラメーター値を定義します。
1. 出力パラメーターの値を定義します。
1. 監視フォルダーエンドポイントの作成を参照してください。
1. エンドポイントを有効にします。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar（AEM FormsがJBoss Application serverにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsがJBoss Application Serverにデプロイされている場合に必要）

For information about the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**EndpointRegistry clientオブジェクトの作成**

プログラムによって監視フォルダーエンドポイントを追加するには、オブジェクトを作成する必要が `EndpointRegistryClient` あります。

**監視フォルダーエンドポイントの属性の設定**

サービスの監視フォルダーエンドポイントを作成するには、次の値を指定します。

* **コネクタ識別子**:作成するエンドポイントのタイプを指定します。 監視フォルダーエンドポイントを作成するには、を指定しま `WatchedFolder`す。
* **説明**:エンドポイントの説明を指定します。
* **名前**:エンドポイントの名前を指定します。
* **サービス識別子**:エンドポイントが属するサービスを指定します。 例えば、この節で紹介するプロセスに監視フォルダーエンドポイントを追加する（Workbenchを使用してアクティブ化した場合にプロセスがサービスになる）には、を指定しま `EncryptDocument`す。
* **操作名**:エンドポイントを使用して呼び出される操作の名前を指定します。 通常、Workbenchで作成されたプロセスから派生するサービスの監視フォルダーエンドポイントを作成する場合、操作の名前はです `invoke`。

**設定値の指定**

プログラムで監視フォルダーエンドポイントをサービスに追加する場合は、監視フォルダーエンドポイントの設定値を指定する必要があります。 これらの設定値は、管理コンソールを使用して監視フォルダーエンドポイントを追加した場合に、管理者が指定します。

次のリストは、監視フォルダーエンドポイントをプログラムでサービスに追加する場合に設定される設定値を指定します。

* **url**:監視フォルダーの場所を指定します。 クラスター環境では、この値は、クラスター内のすべてのコンピューターからアクセス可能な共有ネットワークフォルダーを指す必要があります。
* **非同期**:呼び出しの種類を非同期型または同期型として識別します。 一過性および同期型のプロセスは、同期型でのみ呼び出すことができます。デフォルト値は true です。非同期を推奨します。
* **cronExpression**:Quartzで、入力ディレクトリのポーリングをスケジュールするために使用されます。 Cron形式の設定について詳しくは、https://quartz.sourceforge.net/javadoc/org/quartz/CronTrigger.htmlを参照してく [ださい](https://quartz.sourceforge.net/javadoc/org/quartz/CronTrigger.html)。
* **purgeDuration**:これは必須の属性です。 結果フォルダー内のファイルとフォルダーは、この値より古い場合に削除されます。 この値の単位は日です。この属性は、結果フォルダーがいっぱいにならないようにするのに役立ちます。 -1 を指定すると、結果フォルダーの削除は行われません。デフォルト値は -1 です。
* **repeatInterval**:監視フォルダーをスキャンして入力を確認する間隔（秒単位）です。 ジョブ数の制限が有効になっていない限り、この値は平均ジョブの処理時間より長くする必要があります。そうしないと、システムが過負荷になる可能性があります。 デフォルト値は 5 です。
* **repeatCount**:監視フォルダーがフォルダーまたはディレクトリをスキャンする回数です。 -1 を指定すると、無限にスキャンされます。デフォルト値は -1 です。
* **throttleOn**:一度に処理できる監視フォルダーのジョブ数を制限します。 ジョブの最大数は、batchSize値によって決まります。
* **userName**:監視フォルダーからターゲットサービスを呼び出すときに使用されるユーザー名です。 この値は必須です。デフォルト値は「SuperAdmin」です。
* **domainName**:ユーザーのドメイン。 この値は必須です。デフォルト値は「DefaultDom」です。
* **batchSize**:1回のスキャンで取得されるファイルまたはフォルダーの数です。 この値を使用して、システムの過負荷を防ぎます。一度にスキャンするファイル数が多すぎると、クラッシュする可能性があります。 デフォルト値は 2 です。
* **waitTime**:フォルダーまたはファイルの作成後にスキャンを実行するまでの待機時間（ミリ秒）です。 例えば、待機時間が36,000,000ミリ秒（1時間）で、ファイルが1分前に作成された場合、このファイルは59分以上経過した後に取得されます。 この属性は、ファイルまたはフォルダーが入力フォルダーに完全にコピーされるようにする場合に役立ちます。 例えば、処理するファイルのサイズが大きく、ファイルのダウンロードに10分かかる場合は、待機時間を10&amp;ast;60 &amp;ast;1000ミリ秒に設定します。 この設定により、監視フォルダーが10分間待たない場合に、ファイルをスキャンできなくなります。 デフォルト値は 0 です。
* **excludeFilePattern**:スキャンおよび取得の対象とするファイルとフォルダーを決定するために監視フォルダーが使用するパターンです。 このパターンを含むファイルまたはフォルダーは、スキャンの対象外となります。 この設定は、入力が複数のファイルを含むフォルダーの場合に役立ちます。 フォルダーの内容は、監視フォルダーが取得する名前を持つフォルダーにコピーできます。 この手順により、フォルダーが入力フォルダーに完全にコピーされる前に監視フォルダーがフォルダーを取得して処理するのを防ぐことができます。 For example, if the excludeFilePattern value is `data*`, all files and folders that match `data*` are not picked up. This includes files and folders named `data1`, `data2`, and so on. また、このパターンにワイルドカードパターンを追加して、ファイルパターンを指定することもできます。 監視フォルダーでは、およびなどのワイルドカードパターンをサポートするように正規表現が変 `*.*` 更されま `*.pdf`す。 これらのワイルドカードパターンは、正規表現ではサポートされていません。
* **includeFilePattern**:スキャンおよび取得の対象とするフォルダーとファイルを決定するために監視フォルダーが使用するパターンです。 For example, if this value is `*`, all files and folders that match `input*` are picked up. This includes files and folders named `input1`, `input2`, and so on. デフォルト値は `*` です。この値は、すべてのファイルとフォルダーを示します。 また、このパターンにワイルドカードパターンを追加して、ファイルパターンを指定することもできます。 監視フォルダーでは、およびなどのワイルドカードパターンをサポートするように正規表現が変 `*.*` 更されま `*.pdf`す。 これらのワイルドカードパターンは、正規表現ではサポートされていません。 この値は必須です。
* **resultFolderName**:保存した結果が保存されるフォルダーです。 この場所は、絶対パスまたは相対ディレクトリパスで指定できます。 結果がこのフォルダーに表示されない場合は、失敗フォルダーを確認してください。読み取り専用ファイルは処理されず、失敗フォルダーに保存されます。デフォルト値は `result/%Y/%M/%D/` です。監視フォルダー内の結果フォルダーです。
* **preserveFolderName**:正常にスキャンおよびピックアップされた後にファイルが保存される場所。 この場所は、絶対パス、相対パス、またはNULLのディレクトリパスです。 デフォルト値は `preserve/%Y/%M/%D/` です。
* **failureFolderName**:失敗ファイルが保存されるフォルダーです。 この場所は、常に監視フォルダーからの相対パスで指定します。読み取り専用ファイルは処理されず、失敗フォルダーに保存されます。デフォルト値は `failure/%Y/%M/%D/` です。
* **preserveOnFailure**:サービスで操作の実行に失敗した場合に入力ファイルを保存します。 デフォルト値は true です。
* **overwriteDuplicateFilename**:trueに設定すると、結果フォルダーと保存用フォルダー内のファイルが上書きされます。 falseに設定した場合、名前には数値のインデックスサフィックスを持つファイルとフォルダーが使用されます。 デフォルト値は false です。

**入力パラメーター値の定義**

監視フォルダーエンドポイントを作成する場合は、入力パラメーターの値を定義する必要があります。 つまり、監視フォルダーによって呼び出される操作に渡される入力値を記述する必要があります。 例えば、このトピックで紹介したプロセスについて考えてみましょう。 この変数には、という名前の1つの入 `InDoc` 力値があり、そのデータタイプは `com.adobe.idp.Document`です。 このプロセスの監視フォルダーエンドポイントを作成する場合（プロセスがアクティブ化されると、サービスになります）、入力パラメーターの値を定義する必要があります。

監視フォルダーエンドポイントに必要な入力パラメーターの値を定義するには、次の値を指定します。

**入力パラメータ名**:入力パラメーターの名前。 入力値の名前は、プロセスに対してWorkbenchで指定されます。 入力値がサービス操作（Workbenchで作成されたプロセスではないサービス）に属する場合、入力名はcomponent.xmlファイルで指定されます。 例えば、この節で紹介するプロセスの入力パラメーターの名前はです `InDoc`。

**マッピングタイプ**:サービス操作の呼び出しに必要な入力値の設定に使用されます。 マッピングには次の2種類があります。

* `Literal`:監視フォルダーエンドポイントは、フィールドに入力された値を表示どおりに使用します。 すべての基本 Java 型がサポートされます。例えば、APIがString、long、int、Booleanなどの入力を使用する場合、文字列は適切な型に変換され、サービスが呼び出されます。
* `Variable`:入力された値は、監視フォルダーが入力を選択する際に使用するファイルパターンです。 例えば、マッピングの種類として「Variable」を選択し、入力ドキュメントがPDFファイルである必要がある場合、マッピング値 `*.pdf`として指定できます。

**マッピング値**:マッピングタイプの値を指定します。 例えば、マッピングの種類を選 `Variable` 択した場合は、ファイルパターン `*.pdf` として指定できます。

**データタイプ**:入力値のデータタイプを指定します。 例えば、この節で紹介するプロセスの入力値のデータタイプはです `com.adobe.idp.Document`。

**出力パラメーター値の定義**

監視フォルダーエンドポイントを作成する場合は、出力パラメーターの値を定義する必要があります。 つまり、監視フォルダーエンドポイントによって呼び出されるサービスから返される出力値を記述する必要があります。 例えば、このトピックで紹介したプロセスについて考えてみましょう。 この変数にはという出力値があり、 `SecuredDoc` そのデータタイプはで `com.adobe.idp.Document`す。 このプロセスの監視フォルダーエンドポイントを作成する場合（プロセスがアクティブ化されると、サービスになります）、出力パラメーターの値を定義する必要があります。

監視フォルダーエンドポイントに必要な出力パラメーターの値を定義するには、次の値を指定します。

**出力パラメータ名**:出力パラメーターの名前。 プロセス出力値の名前はWorkbenchで指定します。 出力値がサービス操作（Workbenchで作成されたプロセスではないサービス）に属する場合、出力名はcomponent.xmlファイルで指定されます。 例えば、この節で紹介するプロセスの出力パラメーターの名前はです `SecuredDoc`。

**マッピングタイプ**:サービスと操作の出力を設定するために使用します。 以下のオプションが利用できます。

* サービスが単一のオブジェクト（単一のドキュメント）を返す場合、パターンは `%F.pdf` で、ソースの宛先はsourcefilename.pdfです。 例えば、この節で紹介したプロセスは、1つのドキュメントを返します。 その結果、マッピングタイプは、 `%F.pdf` (指定したファイ `%F` ル名を使用することを意味する)と定義できます。 パターンは、 `%E` 入力ドキュメントの拡張子を指定します。
* サービスがリストを返す場合、パターン `Result\%F\`はResult\sourcefilename\source1 (output 1)およびResult\sourcefilename\source2 (output 2)です。
* サービスがマップを返す場合、パターンはResult\sourcefilename\file1 and Result\sourcefilename\file2 `Result\%F\`になり、ソースの宛先はになります。 マップに複数のオブジェクトが含まれる場合、パターンは `Result\%F.pdf` Result\sourcefilename1.pdf（出力1）、Result\sourcefilenam2.pdf（出力2）のようになります。

**データタイプ**:戻り値のデータ型を指定します。 例えば、この節で紹介するプロセスの戻り値のデータ型はです `com.adobe.idp.Document`。

**監視フォルダーエンドポイントの作成**

エンドポイントの属性、設定値を設定し、入力および出力パラメーターの値を定義した後、監視フォルダーエンドポイントを作成する必要があります。

**エンドポイントの有効化**

監視フォルダーエンドポイントを作成したら、有効にする必要があります。 エンドポイントが有効な場合は、サービスの呼び出しに使用できます。 エンドポイントを有効にした後、管理コンソール内でエンドポイントを表示できます。

**関連トピック**

[Java APIを使用した監視フォルダーエンドポイントの追加](programmatically-endpoints.md#add-a-watched-folder-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java APIを使用した監視フォルダーエンドポイントの追加 {#add-a-watched-folder-endpoint-using-the-java-api}

AEM Forms Java APIを使用して監視フォルダーエンドポイントを追加します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-livecycle-client.jarなどのクライアントJARファイルを含めます。

1. EndpointRegistry clientオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `EndpointRegistryClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. 監視フォルダーエンドポイントの属性を設定します。

   * コンストラクタを使用して `CreateEndpointInfo` オブジェクトを作成します。
   * コネクタ識別子の値を指定するには、オブジェクトの `CreateEndpointInfo` メソッドを呼び出 `setConnectorId` し、文字列値を渡しま `WatchedFolder`す。
   * オブジェクトのメソッドを呼び出し、エンドポ `CreateEndpointInfo` イントを説明 `setDescription` する文字列値を渡して、エンドポイントの説明を指定します。
   * オブジェクトのメソッドを呼び出し、名前を `CreateEndpointInfo` 指定するstring値 `setName` を渡して、エンドポイントの名前を指定します。
   * オブジェクトのメソッドを呼び出し、サービス名を指 `CreateEndpointInfo` 定するstring値を `setServiceId` 渡して、エンドポイントが属するサービスを指定します。
   * オブジェクトのメソッドを呼び出し、操作 `CreateEndpointInfo` 名を指定 `setOperationName` する文字列値を渡して、呼び出す操作を指定します。 通常、Workbenchで作成されたプロセスから生成されたサービスに対して監視フォルダーエンドポイントを作成する場合、操作の名前は「invoke」です。

1. 設定値を指定します。

   監視フォルダーエンドポイントに設定する各設定値に対して、オブジェクトのメソッドを呼び出す `CreateEndpointInfo` 必要があ `setConfigParameterAsText` ります。 例えば、設定値を設定す `url` るには、オブジェクトの `CreateEndpointInfo` メソッドを呼び `setConfigParameterAsText` 出し、次の文字列値を渡します。

   * 設定値の名前を指定するstring値。 設定値を設定す `url` る場合は、を指定しま `url`す。
   * 設定値の値を指定するstring値。 設定値を設定する `url` 場合は、監視フォルダーの場所を指定します。
   >[!NOTE]
   >
   >EncryptDocumentサービスに設定されたすべての設定値を確認するには、 [QuickStartにあるJavaコードの例を参照してください。Java APIを使用した監視フォルダーエンドポイントの追加](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)。

1. 入力パラメーター値を定義します。

   オブジェクトのメソッドを呼び出し、次 `CreateEndpointInfo` の値を渡して、入 `setInputParameterMapping` 力パラメーター値を定義します。

   * 入力パラメーターの名前を指定するstring値。 例えば、EncryptDocumentサービスの入力パラメーターの名前はです `InDoc`。
   * 入力パラメーターのデータタイプを指定するstring値。 例えば、入力パラメーターのデータタ `InDoc` イプはです `com.adobe.idp.Document`。
   * マッピングの種類を指定するstring値です。 例えば、を指定できます `variable`。
   * マッピングタイプの値を指定するstring値。 例えば、&amp;ast;.pdfをファイルパターンとして指定できます。
   >[!NOTE]
   >
   >定義する各入 `setInputParameterMapping` 力パラメーター値に対してメソッドを呼び出します。 EncryptDocumentプロセスには1つの入力パラメーターしかないので、このメソッドを1回呼び出す必要があります。

1. 出力パラメーターの値を定義します。

   オブジェクトのメソッドを呼び出し、次 `CreateEndpointInfo` の値を渡して、 `setOutputParameterMapping` 出力パラメーターの値を定義します。

   * 出力パラメーターの名前を指定するstring値。 例えば、EncryptDocumentサービスの出力パラメーターの名前はです `SecuredDoc`。
   * 出力パラメーターのデータタイプを指定するstring値。 例えば、出力パラメーターのデータタ `SecuredDoc` イプはです `com.adobe.idp.Document`。
   * マッピングの種類を指定するstring値です。 例えば、を指定できます `%F.pdf`。

1. 監視フォルダーエンドポイントの作成を参照してください。

   オブジェクトのメソッドを呼び出し、オ `EndpointRegistryClient` ブジェクトを渡すこ `createEndpoint` とで、エンドポイントを作 `CreateEndpointInfo` 成します。 このメソッドは、監視フォ `Endpoint` ルダーエンドポイントを表すオブジェクトを返します。

1. エンドポイントを有効にします。

   オブジェクトのメソッドを呼び出し、そ `EndpointRegistryClient` のメソッドによっ `enable` て返されたオ `Endpoint` ブジェクトを渡して、エンドポイントを有効 `createEndpoint` にします。

**関連トピック**

[手順の概要](programmatically-endpoints.md#summary-of-steps)

[QuickStart:Java APIを使用した監視フォルダーエンドポイントの追加](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 監視フォルダー設定値の定数ファイル {#watched-folder-configuration-values-constant-file}

クイッ [クスタート：Java APIを使用して監視フォルダーエンドポイントを追加すると](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api) 、クイックスタートをコンパイルするためにJavaプロジェクトに含める必要がある定数ファイルが使用されます。 この定数ファイルは、監視フォルダーエンドポイントを追加する際に設定する必要がある設定値を表します。 次のJavaコードは定数ファイルを表しています。

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

AEM Forms Java APIを使用して、電子メールエンドポイントをプログラムでサービスに追加できます。 電子メールエンドポイントを追加すると、1つ以上の添付ファイルを含む電子メールメッセージを指定した電子メールアカウントに送信できます。 次に、サービスの設定操作が呼び出され、ファイルが操作されます。 サービスは、指定された操作を実行した後、変更されたファイルを添付ファイルとして送信者に電子メールメッセージを送信します。

プログラムによって電子メールエンドポイントをサービスに追加する場合は、次のMyApplication\EncryptDocumentという短時間のみ有効なプロセスを考慮 *してください*。 短時間のみ有効なプロセスについて詳しくは、「AEM Formsプロ [セスについて](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes)」を参照してください。

![ae_ae_encryptdocumentprocess](assets/ae_ae_encryptdocumentprocess.png)

このプロセスは、保護されていないPDFドキュメントを入力値として受け取り、保護されていないPDFドキュメントをEncryptionサービスの操作に渡 `EncryptPDFUsingPassword` します。 このプロセスは、PDFドキュメントをパスワードで暗号化し、パスワードで暗号化されたPDFドキュメントを出力値として返します。 入力値の名前（保護されていないPDFドキュメント）とデ `InDoc` ータタイプはです `com.adobe.idp.Document`。 出力値の名前（パスワードで暗号化されたPDFドキュメント）とデ `SecuredDoc` ータタイプはです `com.adobe.idp.Document`。

>[!NOTE]
>
>Webサービスを使用して電子メールエンドポイントを追加することはできません。

### 手順の概要 {#summary_of_steps-3}

電子メールエンドポイントをサービスに追加するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. オブジェクトを作 `EndpointRegistryClient` 成します。
1. 電子メールエンドポイントの属性を設定します。
1. 設定値を指定します。
1. 入力パラメーター値を定義します。
1. 出力パラメーターの値を定義します。
1. 電子メールエンドポイントを作成します。
1. エンドポイントを有効にします。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar（AEM FormsがJBoss Application serverにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsがJBoss Application Serverにデプロイされている場合に必要）

For information about the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**EndpointRegistry clientオブジェクトの作成**

プログラムによって電子メールエンドポイントを追加する前に、オブジェクトを作成する必要が `EndpointRegistryClient` あります。

**電子メールエンドポイント属性の設定**

サービスの電子メールエンドポイントを作成するには、次の値を指定します。

* **コネクタ識別子の値**:作成するエンドポイントのタイプを指定します。 電子メールエンドポイントを作成するには、を指定しま `Email`す。
* **説明**:エンドポイントの説明を指定します。
* **名前**:エンドポイントの名前を指定します。
* **サービス識別子の値**:エンドポイントが属するサービスを指定します。 例えば、この節で紹介するプロセスに電子メールエンドポイントを追加する（Workbenchを使用してアクティブ化した場合にプロセスがサービスになる）には、を指定しま `EncryptDocument`す。
* **操作名**:エンドポイントを使用して呼び出される操作の名前を指定します。 通常、Workbenchで作成されたプロセスから派生するサービスの電子メールエンドポイントを作成する場合、操作の名前はです `invoke`。

**設定値の指定**

電子メールエンドポイントをプログラムでサービスに追加する場合は、電子メールエンドポイントの設定値を指定する必要があります。 これらの設定値は、管理コンソールを使用して電子メールエンドポイントを追加した場合に、管理者が指定します。

>[!NOTE]
>
>監視される電子メールアカウントは、電子メールエンドポイントにのみ使用される特別なアカウントです。 このアカウントは、通常のユーザーの電子メールアカウントではありません。 通常のユーザーの電子メールアカウントは、電子メールプロバイダーが使用するアカウントとして設定しないでください。電子メールプロバイダーは、メッセージの処理が完了した後でインボックスから電子メールメッセージを削除します。

電子メールエンドポイントをプログラムでサービスに追加する場合、次の設定値が設定されます。

* **cronExpression**:Cron形式を使用して電子メールをスケジュールする必要がある場合は、Cron形式。
* **repeatCount**:電子メールエンドポイントがフォルダーまたはディレクトリをスキャンする回数です。 -1 を指定すると、無限にスキャンされます。デフォルト値は -1 です。
* **repeatInterval**:受信メールの確認に使用するスキャン速度（秒）。 デフォルト値は 10 です。
* **startDelay**:スケジューラーの起動後にスキャンを待機する時間。 デフォルトの時間は0です。
* **batchSize**:受信者が最適なパフォーマンスを得るために1回のスキャンで処理する電子メールメッセージの数。 -1 を指定すると、すべての電子メールが処理されます。デフォルト値は 2 です。
* **userName**:電子メールからターゲットサービスを呼び出すときに使用されるユーザー名です。 デフォルト値は `SuperAdmin` です。
* **domainName**:必須の設定値です。 デフォルト値は `DefaultDom` です。
* **domainPattern**:プロバイダーが受け入れる受信電子メールのドメインパターンを指定します。 For example, if `adobe.com` is used, only email from adobe.com is processed, email from other domains is ignored.
* **filePattern**:プロバイダーが受け付ける受信ファイル添付パターンを指定します。 これには、特定のファイル名拡張子(&amp;ast;.dat, &amp;ast;.xml)を持つファイル、特定の名前(data)を持つファイル、名前と拡張子(&amp;ast;)に複合式を持つファイルが含まれます。[dD][aA][Tt])。 デフォルト値は `*` です。
* **recipientSuccessfulJob**:ジョブの成功を示すメッセージの送信先の電子メールアドレスです。 デフォルトでは、ジョブの正常終了メッセージは常に送信者に送信されます。`sender` と入力すると、電子メールの結果は送信者に送信されます。最大 100 人の受信者を指定できます。追加の受信者を電子メールアドレスで指定します。各受信者はコンマで区切ります。 このオプションをオフにするには、この値を空白のままにします。 場合によっては、プロセスをトリガーし、結果の電子メール通知を送信しないようにしたい場合があります。 デフォルト値は `sender` です。
* **recipientFailedJob**:ジョブの失敗を示すメッセージの送信先の電子メールアドレスです。 デフォルトでは、ジョブ失敗メッセージは常に送信者に送信されます。 `sender` と入力すると、電子メールの結果は送信者に送信されます。最大 100 人の受信者を指定できます。追加の受信者を電子メールアドレスで指定します。各受信者はコンマで区切ります。 このオプションをオフにするには、この値を空白のままにします。 デフォルト値は `sender` です。
* **inboxHost**:電子メールプロバイダーがスキャンするインボックスのホスト名またはIPアドレス。
* **inboxPort**:電子メールサーバーが使用するポート。 POP3 のデフォルト値は「110」で、IMAP のデフォルト値は「143」です。SSL が有効になっている場合は、POP3 のデフォルト値は「995」で、IMAP のデフォルト値は「993」です。
* **inboxProtocol**:電子メールエンドポイントがインボックスのスキャンに使用する電子メールプロトコルです。 またはを選択で `IMAP` きます `POP3`。 指定のプロトコルはインボックスホストメールサーバーでサポートされている必要があります。
* **inboxTimeOut**:電子メールプロバイダーがインボックスの応答を待機する時間（秒）。 デフォルト値は 60 です。
* **inboxUser**:電子メールアカウントにログインするために必要なユーザー名です。 電子メールサーバーと設定によっては、電子メールのユーザー名の部分のみ、または完全な電子メールアドレスを指定できます。
* **inboxPassword**:インボックスユーザーのパスワードです。
* **inboxSSLEnabled**:電子メールプロバイダーが結果やエラーの通知メッセージを送信する際にSSLを使用するようにするには、この値を設定します。 IMAPまたはPOP3ホストがSSLをサポートしていることを確認します。
* **smtpHost**:電子メールプロバイダーが結果およびエラーメッセージを送信するメールサーバーのホスト名です。
* **smtpPort**:SMTPポートのデフォルト値は25です。
* **smtpUser**:電子メールプロバイダーが結果およびエラーの電子メール通知を送信する際に使用するユーザーアカウントです。
* **smtpPassword**:SMTPアカウントのパスワードです。 SMTP パスワードが不要なメールサーバーもあります。
* **charSet**:電子メールプロバイダーが使用する文字セットです。 デフォルト値は `UTF-8` です。
* **smtpSSLEnabled**:電子メールプロバイダーが結果やエラーの通知メッセージを送信する際にSSLを使用するようにするには、この値を設定します。 SMTPホストがSSLをサポートしていることを確認します。
* **failedJobFolder**:SMTPメールサーバーが動作していない場合に結果を保存するディレクトリを指定します。
* **非同期**:「同期」に設定すると、すべての入力ドキュメントが処理され、単一の応答が返されます。 「asynchronous」に設定した場合、処理される入力ドキュメントごとに応答が送信されます。 例えば、このトピックで導入されたプロセス用に電子メールエンドポイントが作成され、保護されていない複数のPDFドキュメントを含む電子メールメッセージがエンドポイントのインボックスに送信されます。 すべてのPDFドキュメントがパスワードで暗号化され、エンドポイントが同期として設定されている場合は、保護されたすべてのPDFドキュメントが添付された単一の応答電子メールメッセージが送信されます。 エンドポイントが非同期として設定されている場合は、保護されたPDFドキュメントごとに別々の応答電子メールメッセージが送信されます。 各電子メールメッセージには、1つのPDFドキュメントが添付ファイルとして含まれています。 デフォルト値は「asynchronous」です。

**入力パラメーター値の定義**

電子メールエンドポイントを作成する場合は、入力パラメーターの値を定義する必要があります。 つまり、電子メールエンドポイントによって呼び出される操作に渡される入力値を記述する必要があります。 例えば、このトピックで紹介したプロセスについて考えてみましょう。 この変数には、という名前の1つの入 `InDoc` 力値があり、そのデータタイプは `com.adobe.idp.Document`です。 このプロセスの電子メールエンドポイントを作成する場合（プロセスがアクティブ化されると、サービスになります）、入力パラメーターの値を定義する必要があります。

電子メールエンドポイントに必要な入力パラメーター値を定義するには、次の値を指定します。

**入力パラメータ名**:入力パラメーターの名前。 入力値の名前は、プロセスに対してWorkbenchで指定されます。 入力値がサービス操作（Workbenchで作成されたプロセスではないFormsサービス）に属する場合、入力名はcomponent.xmlファイルで指定されます。 例えば、この節で紹介するプロセスの入力パラメーターの名前はです `InDoc`。

**マッピングタイプ**:サービス操作の呼び出しに必要な入力値の設定に使用されます。 次に、2種類のマッピングタイプを示します。

* `Literal`:電子メールエンドポイントは、フィールドに入力された値を表示どおりに使用します。 すべての基本 Java 型がサポートされます。例えば、String、long、int および Boolean などの入力が使用される API の場合、文字列は適切な型に変換され、サービスが呼び出されます。
* `Variable`:入力された値は、電子メールエンドポイントが入力の選択に使用するファイルパターンです。 例えば、マッピングの種類として「Variable」を選択し、入力ドキュメントがPDFファイルである必要がある場合、マッピング値と `*.pdf` してを指定できます。

**マッピング値**:マッピングタイプの値を指定します。 例えば、変数のマッピングタイプを選択した場合、ファイルパターンと `*.pdf` して指定できます。

**データタイプ**:入力値のデータタイプを指定します。 例えば、この節で紹介するプロセスの入力値のデータタイプはcom.adobe.idp.Documentです。

**出力パラメーター値の定義**

電子メールエンドポイントを作成する場合は、出力パラメーターの値を定義する必要があります。 つまり、電子メールエンドポイントによって呼び出されるサービスによって返される出力値を記述する必要があります。 例えば、このトピックで紹介したプロセスについて考えてみましょう。 この変数にはという出力値があり、 `SecuredDoc` そのデータタイプはで `com.adobe.idp.Document`す。 このプロセスの電子メールエンドポイントを作成する場合（プロセスがアクティブ化されると、サービスになります）、出力パラメーターの値を定義する必要があります。

電子メールエンドポイントに必要な出力パラメーター値を定義するには、次の値を指定します。

**出力パラメータ名**:出力パラメーターの名前。 プロセス出力値の名前はWorkbenchで指定します。 出力値がサービス操作（Workbenchで作成されたプロセスではないサービス）に属する場合、出力名はcomponent.xmlファイルで指定されます。 例えば、この節で紹介するプロセスの出力パラメーターの名前はです `SecuredDoc`。

**マッピングタイプ**:サービスと操作の出力を設定するために使用します。 以下のオプションが利用できます。

* サービスが単一のオブジェクト（単一のドキュメント）を返す場合、パターンは `%F.pdf` で、ソースの宛先はsourcefilename.pdfです。 例えば、この節で紹介したプロセスは、1つのドキュメントを返します。 その結果、マッピングタイプは、 `%F.pdf` (指定したファイ `%F` ル名を使用することを意味する)と定義できます。 パターンは、 `%E` 入力ドキュメントの拡張子を指定します。
* サービスがリストを返す場合、パターン `Result\%F\`はResult\sourcefilename\source1 (output 1)およびResult\sourcefilename\source2 (output 2)です。
* サービスがマップを返す場合、パターンはResult\sourcefilename\file1 and Result\sourcefilename\file2 `Result\%F\`になり、ソースの宛先はになります。 マップに複数のオブジェクトが含まれる場合、パターンは `Result\%F.pdf` Result\sourcefilename1.pdf（出力1）、Result\sourcefilenam2.pdf（出力2）のようになります。

**データタイプ**:戻り値のデータ型を指定します。 例えば、この節で紹介するプロセスの戻り値のデータ型はです `com.adobe.idp.Document`。

**電子メールエンドポイントの作成**

電子メールエンドポイントの属性と設定値を設定し、入力パラメーターと出力パラメーターの値を定義した後、電子メールエンドポイントを作成する必要があります。

**エンドポイントの有効化**

電子メールエンドポイントを作成した後、有効にする必要があります。 エンドポイントが有効な場合は、サービスの呼び出しに使用できます。 エンドポイントを有効にした後、管理コンソール内でエンドポイントを表示できます。

**関連トピック**

[Java APIを使用した電子メールエンドポイントの追加](programmatically-endpoints.md#add-an-email-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java APIを使用した電子メールエンドポイントの追加 {#add-an-email-endpoint-using-the-java-api}

Java APIを使用して電子メールエンドポイントを追加します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-livecycle-client.jarなどのクライアントJARファイルを含めます。

1. EndpointRegistry clientオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `EndpointRegistryClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. 電子メールエンドポイントの属性を設定します。

   * コンストラクタを使用して `CreateEndpointInfo` オブジェクトを作成します。
   * コネクタ識別子の値を指定するには、オブジェクトの `CreateEndpointInfo` メソッドを呼び出 `setConnectorId` し、文字列値を渡しま `Email`す。
   * オブジェクトのメソッドを呼び出し、エンドポ `CreateEndpointInfo` イントを説明 `setDescription` する文字列値を渡して、エンドポイントの説明を指定します。
   * オブジェクトのメソッドを呼び出し、名前を `CreateEndpointInfo` 指定するstring値 `setName` を渡して、エンドポイントの名前を指定します。
   * オブジェクトのメソッドを呼び出し、サービス名を指 `CreateEndpointInfo` 定するstring値を `setServiceId` 渡して、エンドポイントが属するサービスを指定します。
   * オブジェクトのメソッドを呼び出し、操作 `CreateEndpointInfo` 名を指定 `setOperationName` する文字列値を渡して、呼び出す操作を指定します。 通常、Workbenchで作成されたプロセスから派生するサービスの電子メールエンドポイントを作成する場合、操作の名前は「invoke」です。

1. 設定値を指定します。

   電子メールエンドポイントに設定する各設定値に対して、オブジェクトのメソッドを呼び出 `CreateEndpointInfo` す必要があ `setConfigParameterAsText` ります。 例えば、設定値を設定す `smtpHost` るには、オブジェクトの `CreateEndpointInfo` メソッドを呼び `setConfigParameterAsText` 出し、次の値を渡します。

   * 設定値の名前を指定するstring値。 設定値を設定す `smtpHost` る場合は、を指定しま `smtpHost`す。
   * 設定値の値を指定するstring値。 設定値を設定 `smtpHost` する場合は、SMTPサーバーの名前を指定するstring値を指定します。
   >[!NOTE]
   >
   >この節で紹介するEncryptDocumentサービスに設定されたすべての設定値を確認するには、 [QuickStartにあるJavaコードの例を参照してください。Java APIを使用した電子メールエンドポイントの追加](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-email-endpoint-using-the-java-api)。

1. 入力パラメーター値を定義します。

   オブジェクトのメソッドを呼び出し、次 `CreateEndpointInfo` の値を渡して、入 `setInputParameterMapping` 力パラメーター値を定義します。

   * 入力パラメーターの名前を指定するstring値。 例えば、EncryptDocumentサービスの入力パラメーターの名前はです `InDoc`。
   * 入力パラメーターのデータタイプを指定するstring値。 例えば、入力パラメーターのデータタ `InDoc` イプはです `com.adobe.idp.Document`。
   * マッピングの種類を指定するstring値です。 例えば、を指定できます `variable`。
   * マッピングタイプの値を指定するstring値。 例えば、&amp;ast;.pdfをファイルパターンとして指定できます。
   >[!NOTE]
   >
   >定義する各入 `setInputParameterMapping` 力パラメーター値に対してメソッドを呼び出します。 EncryptDocumentプロセスには1つの入力パラメーターしかないので、このメソッドを1回呼び出す必要があります。

1. 出力パラメーターの値を定義します。

   オブジェクトのメソッドを呼び出し、次 `CreateEndpointInfo` の値を渡して、 `setOutputParameterMapping` 出力パラメーター値を定義します。

   * 出力パラメーターの名前を指定するstring値。 例えば、EncryptDocumentサービスの出力パラメーターの名前はです `SecuredDoc`。
   * 出力パラメーターのデータタイプを指定するstring値。 例えば、出力パラメーターのデータタ `SecuredDoc` イプはです `com.adobe.idp.Document`。
   * マッピングの種類を指定するstring値です。 例えば、を指定できます `%F.pdf`。

1. 電子メールエンドポイントを作成します。

   オブジェクトのメソッドを呼び出し、オ `EndpointRegistryClient` ブジェクトを渡すこ `createEndpoint` とで、エンドポイントを作 `CreateEndpointInfo` 成します。 このメソッドは、電子メール `Endpoint` エンドポイントを表すオブジェクトを返します。

1. エンドポイントを有効にします。

   オブジェクトのメソッドを呼び出し、そ `EndpointRegistryClient` のメソッドによっ `enable` て返されたオ `Endpoint` ブジェクトを渡して、エンドポイントを有効 `createEndpoint` にします。

**関連トピック**

[手順の概要](programmatically-endpoints.md#summary-of-steps)

[QuickStart:Java APIを使用した監視フォルダーエンドポイントの追加](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 電子メール設定値の定数ファイル {#email-configuration-values-constant-file}

クイッ [クスタート：Java APIを使用して電子メールエンドポイントを追加すると](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-email-endpoint-using-the-java-api) 、クイックスタートをコンパイルするためにJavaプロジェクトに含める必要がある定数ファイルが使用されます。 この定数ファイルは、電子メールエンドポイントの追加時に設定する必要がある設定値を表します。 次のJavaコードは定数ファイルを表しています。

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

AEM Forms Java APIを使用して、プログラムによってリモートエンドポイントをサービスに追加できます。 リモートエンドポイントを追加すると、Flexアプリケーションでリモート処理を使用してサービスを呼び出せるようになります。 (『AEM Forms Remoting [を使用したAEM Formsの呼び出し（AEM Formsでは非推奨）』を参照](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting))。

プログラムによってリモートエンドポイントをサービスに追加する場合は、次のEncryptDocumentという短時間のみ有効なプロセスを考慮 *します*。

![ar_ar_encryptdocumentprocess](assets/ar_ar_encryptdocumentprocess.png)

このプロセスは、保護されていないPDFドキュメントを入力値として受け取り、保護されていないPDFドキュメントをEncryptionサービスの操作に渡 `EncryptPDFUsingPassword` します。 PDFドキュメントはパスワードで暗号化され、パスワードで暗号化されたPDFドキュメントはこのプロセスの出力値です。 入力値の名前（保護されていないPDFドキュメント）とデ `InDoc` ータタイプはです `com.adobe.idp.Document`。 出力値の名前（パスワードで暗号化されたPDFドキュメント）とデ `SecuredDoc` ータタイプはです `com.adobe.idp.Document`。

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
* adobe-utilities.jar（AEM FormsがJBoss Application serverにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsがJBoss Application Serverにデプロイされている場合に必要）

For information about the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**EndpointRegistry clientオブジェクトの作成**

プログラムによってリモートエンドポイントを追加するには、オブジェクトを作成する必要が `EndpointRegistryClient` あります。

**リモートエンドポイント属性の設定**

サービスのRemotingエンドポイントを作成するには、次の値を指定します。

* **コネクタ識別子の値**:作成するエンドポイントのタイプを指定します。 リモートエンドポイントを作成するには、を指定しま `Remoting`す。
* **説明**:エンドポイントの説明を指定します。
* **名前**:エンドポイントの名前を指定します。
* **サービス識別子の値**:エンドポイントが属するサービスを指定します。 例えば、この節で紹介するプロセスにリモートエンドポイントを追加する（Workbench内でアクティブ化されるとプロセスがサービスになる）には、を指定しま `EncryptDocument`す。
* **操作名**:エンドポイントを使用して呼び出される操作の名前を指定します。 リモートエンドポイントを作成する場合は、ワイルドカード文字(&amp;ast;)を指定します。

**リモートエンドポイントの作成**

リモートエンドポイント属性を設定した後、サービス用のリモートエンドポイントを作成できます。

**エンドポイントの有効化**

新しいエンドポイントを作成した後、そのエンドポイントを有効にする必要があります。 リモートエンドポイントが有効な場合、Flexクライアントはサービスを呼び出すことができます。

**関連トピック**

[Java APIを使用したリモートエンドポイントの追加](programmatically-endpoints.md#add-a-remoting-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java APIを使用したリモートエンドポイントの追加 {#add-a-remoting-endpoint-using-the-java-api}

Java APIを使用してリモートエンドポイントを追加します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-livecycle-client.jarなどのクライアントJARファイルを含めます。

1. EndpointRegistry clientオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `EndpointRegistryClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. リモートエンドポイントの属性を設定します。

   * コンストラクタを使用して `CreateEndpointInfo` オブジェクトを作成します。
   * コネクタ識別子の値を指定するには、オブジェクトの `CreateEndpointInfo` メソッドを呼び出 `setConnectorId` し、文字列値を渡しま `Remoting`す。
   * オブジェクトのメソッドを呼び出し、エンドポ `CreateEndpointInfo` イントを説明 `setDescription` する文字列値を渡して、エンドポイントの説明を指定します。
   * オブジェクトのメソッドを呼び出し、名前を `CreateEndpointInfo` 指定するstring値 `setName` を渡して、エンドポイントの名前を指定します。
   * オブジェクトのメソッドを呼び出し、サービス名を指 `CreateEndpointInfo` 定するstring値を `setServiceId` 渡して、エンドポイントが属するサービスを指定します。
   * オブジェクトのメソッドによって呼び出さ `CreateEndpointInfo` れる操作を指 `setOperationName` 定し、操作名を指定する文字列値を渡します。 リモートエンドポイントには、ワイルドカード文字(&amp;ast;)を指定します。

1. リモートエンドポイントの作成を参照してください。

   オブジェクトのメソッドを呼び出し、オ `EndpointRegistryClient` ブジェクトを渡すこ `createEndpoint` とで、エンドポイントを作 `CreateEndpointInfo` 成します。 このメソッドは、新しいリモ `Endpoint` ートエンドポイントを表すオブジェクトを返します。

1. エンドポイントを有効にします。

   オブジェクトのメソッドを呼び出し、そ `EndpointRegistryClient` のメソッドによっ `enable` て返されたオ `Endpoint` ブジェクトを渡して、エンドポイントを有効 `createEndpoint` にします。

**関連トピック**

[手順の概要](programmatically-endpoints.md#summary-of-steps)

[QuickStart:Java APIを使用したリモートエンドポイントの追加](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-remoting-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## TaskManagerエンドポイントの追加 {#adding-taskmanager-endpoints}

AEM Forms Java APIを使用して、プログラムによってTaskManagerエンドポイントをサービスに追加できます。 TaskManagerエンドポイントをサービスに追加すると、Workspaceユーザーがサービスを呼び出せるようになります。 つまり、Workspaceで作業しているユーザーは、対応するTaskManagerエンドポイントを持つプロセスを呼び出すことができます。

>[!NOTE]
>
>Webサービスを使用してTaskManagerエンドポイントを追加することはできません。

### 手順の概要 {#summary_of_steps-5}

TaskManagerエンドポイントをサービスに追加するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. オブジェクトを作 `EndpointRegistryClient` 成します。
1. エンドポイントのカテゴリを作成します。
1. TaskManagerエンドポイント属性を設定します。
1. TaskManagerエンドポイントを作成します。
1. エンドポイントを有効にします。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar（AEM FormsがJBoss Application serverにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsがJBoss Application Serverにデプロイされている場合に必要）

For information about the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**EndpointRegistry clientオブジェクトの作成**

プログラムによってTaskManagerエンドポイントを追加する前に、オブジェクトを作成する必要があ `EndpointRegistryClient` ります。

**エンドポイントのカテゴリの作成**

カテゴリは、Workspace内のサービスを整理するために使用されます。 つまり、Workspaceユーザーは、Workspace内のカテゴリを選択して、TaskManagerエンドポイントを持つサービスを呼び出すことができます。 TaskManagerエンドポイントを作成する場合、既存のカテゴリを参照するか、新しいカテゴリをプログラムで作成できます。

>[!NOTE]
>
>この節では、TaskManagerエンドポイントをサービスに追加する際に、新しいカテゴリを作成します。

**TaskManagerエンドポイント属性の設定**

サービスのTaskManagerエンドポイントを作成するには、次の値を指定します。

* **コネクタ識別子**:作成するエンドポイントのタイプを指定します。 TaskManagerエンドポイントを作成するには、を指定しま `TaskManagerConnector`す。
* **説明**:エンドポイントの説明を指定します。
* **名前**:エンドポイントの名前を指定します。
* **サービス識別子**:エンドポイントが属するサービスを指定します。
* **カテゴリ**:TaskManagerエンドポイントに関連付けられているカテゴリ識別子の値を指定します。
* **操作名**:通常、Workbenchで作成されたプロセスから派生するサービスに対してTaskManagerエンドポイントを作成する場合、操作の名前はです `invoke`。

**TaskManagerエンドポイントの作成**

TaskManagerエンドポイント属性を設定した後、サービスのTaskManagerエンドポイントを作成できます。

**エンドポイントの有効化**

新しいエンドポイントを作成した後、そのエンドポイントを有効にする必要があります。 エンドポイントが有効な場合、Workspace内からサービスを呼び出すために使用できます。 エンドポイントを有効にした後、管理コンソール内でエンドポイントを表示できます。

**関連トピック**

[Java APIを使用したTaskManagerエンドポイントの追加](programmatically-endpoints.md#add-a-taskmanager-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java APIを使用したTaskManagerエンドポイントの追加 {#add-a-taskmanager-endpoint-using-the-java-api}

Java APIを使用してTaskManagerエンドポイントを追加します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-livecycle-client.jarなどのクライアントJARファイルを含めます。

1. EndpointRegistry clientオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `EndpointRegistryClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. エンドポイントのカテゴリを作成します。

   * Create a `CreateEndpointCategoryInfo` object by using its constructor and passing the following values:

      * カテゴリの識別子の値を指定するstring値
      * カテゴリの説明を指定するstring値
   * オブジェクトのメソッドを呼び出し、オ `EndpointRegistryClient` ブジェクトを渡すこ `createEndpointCategory` とで、カテゴリを作成 `CreateEndpointCategoryInfo` します。 このメソッドは、新しいカ `EndpointCategory` テゴリを表すオブジェクトを返します。


1. TaskManagerエンドポイント属性を設定します。

   * コンストラクタを使用して `CreateEndpointInfo` オブジェクトを作成します。
   * コネクタ識別子の値を指定するには、オブジェクトの `CreateEndpointInfo` メソッドを呼び出 `setConnectorId` し、文字列値を渡しま `TaskManagerConnector`す。
   * オブジェクトのメソッドを呼び出し、エンドポ `CreateEndpointInfo` イントを説明 `setDescription` する文字列値を渡して、エンドポイントの説明を指定します。
   * オブジェクトのメソッドを呼び出し、名前を `CreateEndpointInfo` 指定するstring値 `setName` を渡して、エンドポイントの名前を指定します。
   * オブジェクトのメソッドを呼び出し、サービス名を指 `CreateEndpointInfo` 定するstring値を `setServiceId` 渡して、エンドポイントが属するサービスを指定します。
   * オブジェクトのメソッドを呼び出し、カテゴリ識別子の値を `CreateEndpointInfo` 指定する文字 `setCategoryId` 列値を渡すことで、エンドポイントが属するカテゴリを指定します。 オブジェクトのメ `EndpointCategory` ソッドを呼び `getId` 出して、このカテゴリの識別子の値を取得できます。
   * オブジェクトのメソッドを呼び出し、操作 `CreateEndpointInfo` 名を指定 `setOperationName` する文字列値を渡して、呼び出す操作を指定します。 通常、Workbenchで作成され `TaskManager` たプロセスから派生するサービスのエンドポイントを作成する場合、操作の名前はです `invoke`。

1. TaskManagerエンドポイントを作成します。

   オブジェクトのメソッドを呼び出し、オ `EndpointRegistryClient` ブジェクトを渡すこ `createEndpoint` とで、エンドポイントを作 `CreateEndpointInfo` 成します。 このメソッドは、新しいTaskManager `Endpoint` エンドポイントを表すオブジェクトを返します。

1. エンドポイントを有効にします。

   オブジェクトのメソッドを呼び出し、そ `EndpointRegistryClient` のメソッドによっ `enable` て返されたオ `Endpoint` ブジェクトを渡して、エンドポイントを有効 `createEndpoint` にします。

**関連トピック**

[手順の概要](programmatically-endpoints.md#summary-of-steps)

[QuickStart:Java APIを使用したTaskManagerエンドポイントの追加](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-taskmanager-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## エンドポイントの変更 {#modifying-endpoints}

AEM Forms Java APIを使用して、既存のエンドポイントをプログラムで変更できます。 エンドポイントを変更すると、エンドポイントの動作を変更できます。 例えば、監視フォルダーとして使用するフォルダーを指定する監視フォルダーエンドポイントがあるとします。 監視フォルダーエンドポイントに属する設定値をプログラムで変更すると、別のフォルダーが監視フォルダーとして機能するようになります。 監視フォルダーエンドポイントに属する設定値について詳しくは、「監視フォルダーエンドポイントの [追加」を参照してくださ](programmatically-endpoints.md#adding-watched-folder-endpoints)い。

エンドポイントの変更方法を示すために、この節では、監視フォルダーとして動作するフォルダーを変更して監視フォルダーエンドポイントを変更します。

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
* adobe-utilities.jar（AEM FormsがJBoss Application serverにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsがJBoss Application Serverにデプロイされている場合に必要）

For information about the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**EndpointRegistry clientオブジェクトの作成**

エンドポイントをプログラムで変更するには、オブジェクトを作成する必要が `EndpointRegistryClient` あります。

**変更するエンドポイントの取得**

エンドポイントを変更する前に、エンドポイントを取得する必要があります。 エンドポイントを取得するには、エンドポイントにアクセスできるユーザーとして接続する必要があります。 管理者として接続することをお勧めします。 (See [Setting connection properties](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)).

エンドポイントのリストを取得することで、エンドポイントを取得できます。 その後、削除する特定のエンドポイントを検索して、リストを繰り返し実行できます。 例えば、エンドポイントに対応するサービスとエンドポイントのタイプを決定することで、エンドポイントを特定できます。 エンドポイントを見つけたら、それを変更できます。

**新しい設定値の指定**

エンドポイントを変更する場合は、新しい設定値を指定します。 例えば、監視フォルダーエンドポイントを変更するには、変更するものだけでなく、すべての監視フォルダーエンドポイントの設定値をリセットします。 監視フォルダーエンドポイントに属する設定値について詳しくは、「監視フォルダーエンドポイントの [追加」を参照してくださ](programmatically-endpoints.md#adding-watched-folder-endpoints)い。

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

1. EndpointRegistry clientオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `EndpointRegistryClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. 変更するエンドポイントを取得します。

   * 現在のユーザー（接続プロパティで指定）がアクセスできるすべてのエンドポイントのリストを取得するには、オブジェクトのメソッドを呼び出し、フィルターとして機能するオ `EndpointRegistryClient` ブジ `getEndpoints``PagingFilter` ェクトを渡します。 値を渡すと、すべてのエ `(PagingFilter)null` ンドポイントを返すことができます。 このメソッドは、各要素が `java.util.List` オブジェクトであるオブジェクトを返 `Endpoint` します。 オブジェクトについて詳し `PagingFilter` くは、『 [AEM Forms APIリファレンス』を参照してください](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。
   * オブジェクトを繰り返し `java.util.List` 処理して、オブジェクトにエンドポイントがあるかどうかを判断します。 エンドポイントが存在する場合、各要素はインスタンス `EndPoint` です。
   * オブジェクトのメソッドを呼び出して、エンドポイントに対応するサ `EndPoint` ービスを特定 `getServiceId` します。 このメソッドは、サービス名を指定するstring値を返します。
   * オブジェクトのメソッドを呼び出して、エンドポイ `EndPoint` ントのタイプを決 `getConnectorId` 定します。 このメソッドは、エンドポイントのタイプを指定するstring値を返します。 例えば、エンドポイントが監視フォルダーエンドポイントの場合、このメソッドはを返しま `WatchedFolder`す。

1. 新しい設定値を指定します。

   * Create a `ModifyEndpointInfo` object by invoking its constructor.
   * 設定する各設定値に対して、オブジェクトの `ModifyEndpointInfo` メソッドを呼び出 `setConfigParameterAsText` します。 例えば、URL設定値を設定するには、オブジェクトのメソ `ModifyEndpointInfo` ッドを呼び出 `setConfigParameterAsText` し、次の値を渡します。

      * 設定値の名前を指定するstring値。 例えば、設定値を設定する `url` には、を指定しま `url`す。
      * 設定値の値を指定するstring値。 設定値の値を定義するには、監 `url` 視フォルダーの場所を指定します。
   * Invoke the `EndpointRegistryClient` object’s `modifyEndpoint` method and pass the `ModifyEndpointInfo` object.


**関連トピック**

[手順の概要](programmatically-endpoints.md#summary-of-steps)

[QuickStart:Java APIを使用したエンドポイントの変更](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-modifying-an-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## エンドポイントの削除 {#removing-endpoints}

AEM Forms Java APIを使用して、プログラムによってエンドポイントをサービスから削除できます。 エンドポイントを削除すると、エンドポイントで有効になっている呼び出し方法を使用してサービスを呼び出すことはできません。 例えば、サービスからSOAPエンドポイントを削除する場合、SOAPモードを使用してサービスを呼び出すことはできません。

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
* adobe-utilities.jar（AEM FormsがJBoss Application serverにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsがJBoss Application Serverにデプロイされている場合に必要）

For information about the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**EndpointRegistry clientオブジェクトの作成**

エンドポイントをプログラムで削除するには、オブジェクトを作成する必要が `EndpointRegistryClient` あります。

**削除するエンドポイントの取得**

エンドポイントを削除する前に、エンドポイントを取得する必要があります。 エンドポイントを取得するには、エンドポイントにアクセスできるユーザーとして接続する必要があります。 管理者として接続することをお勧めします。 (See [Setting connection properties](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)).

エンドポイントのリストを取得することで、エンドポイントを取得できます。 その後、削除する特定のエンドポイントを検索して、リストを繰り返し実行できます。 例えば、エンドポイントに対応するサービスとエンドポイントのタイプを決定することで、エンドポイントを特定できます。 エンドポイントを見つけたら、それを削除できます。

**エンドポイントの削除**

新しいエンドポイントを作成した後、そのエンドポイントを有効にする必要があります。 エンドポイントが有効な場合は、サービスの呼び出しに使用できます。 エンドポイントを有効にした後、管理コンソール内でエンドポイントを表示できます。

**関連トピック**

[Java APIを使用したエンドポイントの削除](programmatically-endpoints.md#removing-an-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java APIを使用したエンドポイントの削除 {#removing-an-endpoint-using-the-java-api}

Java APIを使用してエンドポイントを削除します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-livecycle-client.jarなどのクライアントJARファイルを含めます。

1. EndpointRegistry clientオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `EndpointRegistryClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. 削除するエンドポイントを取得します。

   * 現在のユーザー（接続プロパティで指定）がアクセス権を持つすべてのエンドポイントのリストを取得するには、オブジェクトのメソッドを呼び出し、フィルターとして機能するオ `EndpointRegistryClient` ブジ `getEndpoints``PagingFilter` ェクトを渡します。 すべてのエンドポイン `(PagingFilter)null` トを返すために渡すことができます。 このメソッドは、各要素が `java.util.List` オブジェクトであるオブジェクトを返 `Endpoint` します。
   * オブジェクトを繰り返し `java.util.List` 処理して、オブジェクトにエンドポイントがあるかどうかを判断します。 エンドポイントが存在する場合、各要素はインスタンス `EndPoint` です。
   * オブジェクトのメソッドを呼び出して、エンドポイントに対応するサ `EndPoint` ービスを特定 `getServiceId` します。 このメソッドは、サービス名を指定するstring値を返します。
   * オブジェクトのメソッドを呼び出して、エンドポイ `EndPoint` ントのタイプを決 `getConnectorId` 定します。 このメソッドは、エンドポイントのタイプを指定するstring値を返します。 例えば、エンドポイントがEJBエンドポイントの場合、このメソッドはを返しま `EJB`す。

1. エンドポイントを削除します。

   オブジェクトのメソッドを呼び出し、削 `EndpointRegistryClient` 除するエンドポイ `remove` ントを表すオ `EndPoint` ブジェクトを渡して、エンドポイントを削除します。

**関連トピック**

[手順の概要](programmatically-endpoints.md#summary-of-steps)

[QuickStart:Java APIを使用したエンドポイントの削除](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-removing-an-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## エンドポイントコネクタ情報の取得 {#retrieving-endpoint-connector-information}

AEM Forms APIを使用して、エンドポイントコネクタに関する情報をプログラムで取得できます。 コネクタは、エンドポイントが様々な呼び出し方法を使用してサービスを呼び出せるようにします。 例えば、監視フォルダーコネクターを使用すると、エンドポイントで監視フォルダーを使用したサービスを呼び出すことができます。 エンドポイントコネクタに関する情報をプログラムで取得することで、必要な設定値やオプションの設定値など、コネクタに関連付けられた設定値を取得できます。

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
* adobe-utilities.jar（AEM FormsがJBoss Application serverにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsがJBoss Application Serverにデプロイされている場合に必要）

AEM formsをJBoss以外のサポート対象のJ2EEアプリケーションサーバーにデプロイする場合は、adobe-utilities.jarおよびjbossall-client.jarを、AEM formsのデプロイ先のJ2EEアプリケーションサーバーに固有のJARファイルに置き換えます。 For information about the location of all AEM Forms JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**ConnectorRegistry clientオブジェクトの作成**

エンドポイントコネクタ情報をプログラムで取得するには、オブジェクトを作 `ConnectorRegistryClient` 成します。

**コネクタタイプを指定**

情報を取得するコネクタのタイプを指定します。 次のタイプのコネクタが存在します。

* **EJB**:クライアントアプリケーションがEJBモードを使用してサービスを呼び出せるようにします。
* **SOAP**:クライアントアプリケーションがSOAPモードを使用してサービスを呼び出せるようにします。
* **監視フォルダー**:監視フォルダーがサービスを呼び出せるようにします。
* **電子メール**:電子メールメッセージでサービスを呼び出せるようにします。
* **リモート**:Flexクライアントアプリケーションからサービスを呼び出せるようにします。
* **TaskManagerConnector**:WorkspaceユーザーがWorkspace内からサービスを呼び出せるようにします。

**設定値の取得**

コネクタタイプを指定した後、サポートされている設定値など、コネクタに関する情報を取得できます。 例えば、任意のコネクタについて、必要な設定値とオプションの設定値を指定できます。

**関連トピック**

[Java APIを使用したエンドポイントコネクタ情報の取得](programmatically-endpoints.md#retrieve-endpoint-connector-information-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java APIを使用したエンドポイントコネクタ情報の取得 {#retrieve-endpoint-connector-information-using-the-java-api}

Java APIを使用してエンドポイントコネクタ情報を取得します。

1. プロジェクトファイルを含めます。.

   Javaプロジェクトのクラスパスに、adobe-livecycle-client.jarなどのクライアントJARファイルを含めます。

1. ConnectorRegistry clientオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `ConnectorRegistryClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. コネクタタイプを指定します。

   コネクタタイプを指定するには、オブジ `ConnectorRegistryClient` ェクトのメソッドを `getEndpointDefinition` 呼び出し、コネクタタイプを指定する文字列値を渡します。 例えば、監視フォルダーのコネクタタイプを指定するには、文字列値を渡しま `WatchedFolder`す。 このメソッドは、コネクタ `Endpoint` の種類に対応するオブジェクトを返します。

1. 設定値を取得します。

   * オブジェクトのメソッドを呼び出して、このエンドポイント内で関連付けられ `Endpoint` ている設定値を取得 `getConfigParameters` します。 このメソッドは、オブジェクトの配列を返 `ConfigParameter` します。
   * 配列内の各要素を取得して、各設定値に関する情報を取得します。 各要素はオブジェクト `ConfigParameter` です。 例えば、オブジェクトのメソッドを呼び出して、設定値が必須か任意かを `ConfigParameter` 指定でき `isRequired` ます。 設定値が必要な場合、このメソッドはを返します `true`。

**関連トピック**

[手順の概要](programmatically-endpoints.md#summary-of-steps)

[QuickStart:Java APIを使用したエンドポイントコネクタ情報の取得](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-retrieving-endpoint-connector-information-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
