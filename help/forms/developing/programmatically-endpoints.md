---
title: エンドポイントのプログラム管理
seo-title: Programmatically Managing Endpoints
description: Endpoint Registry サービスを使用して、EJB エンドポイントの追加、SOAP エンドポイントの追加、監視フォルダーエンドポイントの追加、電子メールエンドポイントの追加、リモートエンドポイントの追加、Task Manager エンドポイントの追加、エンドポイントの変更、エンドポイントの削除、エンドポイントコネクタ情報の取得を行います。
seo-description: Use the Endpoint Registry service to add EJB endpoints, add SOAP endpoint, add Watched Folder endpoints, add Email endpoints, add  Remoting endpoints, add Task Manager endpoints, modify endpoints, remove endpoints, and retrieve endpoint connector information.
uuid: 5dc50946-3323-4c5d-a43b-31c1c980bd04
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 076889a7-9c9f-4b6f-a45b-67a9b3923c36
role: Developer
exl-id: b94dcca2-136b-4b7d-b5ce-544804575876
source-git-commit: 0c7dba43dad8608b4a5de271e1e44942c950fb16
workflow-type: ht
source-wordcount: '10805'
ht-degree: 100%

---

# エンドポイントのプログラム管理 {#programmatically-managing-endpoints}

**このドキュメントのサンプルと例は、JEE 環境の AEM Forms のみを対象としています。**

**Endpoint Registry サービスについて**

Endpoint Registry サービスは、エンドポイントをプログラムで管理する機能を提供します。 例えば、次の種類のエンドポイントをサービスに追加できます。

* EJB
* SOAP
* 監視フォルダー
* 電子メール
* （AEM Forms では非推奨）リモート
* タスクマネージャー

>[!NOTE]
>
>SOAP、EJB、および（JEE 上の AEM Forms では非推奨）リモートエンドポイントは、アクティブにした各サービスに対して自動的に作成されます。 SOAP および EJB エンドポイントは、すべてのサービス操作で SOAP および EJB を有効にします。

リモートエンドポイントを使用すると、Flex クライアントは、エンドポイントが追加される AEM Forms サービスで操作を呼び出すことができます。エンドポイントと同じ名前を持つ Flex の宛先が作成され、Flex クライアントは、関連するサービスの操作を呼び出すために、この宛先を指す RemoteObjects を作成できます。

電子メール、タスクマネージャー、監視フォルダーの各エンドポイントでは、サービスの特定の操作のみが公開されます。これらのエンドポイントを追加する場合は、呼び出し方法の選択、設定パラメーターの指定、入力および出力のパラメーターマッピングの指定を行うので、もう一段階の設定手順が必要になります。

TaskManager エンドポイントを&#x200B;*カテゴリ*&#x200B;というグループに整理できます。その後、これらのカテゴリは TaskManager を通じて Workspace に公開され、エンドユーザーには分類した TaskManager エンドポイントが表示されます。Workspace 内では、エンドユーザーにはナビゲーションウィンドウにこれらのカテゴリが表示されます。各カテゴリ内のエンドポイントは、Workspace の「Start Processes」ページにプロセスカードとして表示されます。

Endpoint Registry サービスを使用して、次のタスクを実行できます。

* EJB エンドポイントを追加します（[EJB エンドポイントの追加](programmatically-endpoints.md#adding-ejb-endpoints)を参照）。
* SOAP エンドポイントを追加します（[SOAP エンドポイントの追加](programmatically-endpoints.md#adding-soap-endpoints)を参照）。
* 監視フォルダーエンドポイントを追加します（[監視フォルダーエンドポイントの追加](programmatically-endpoints.md#adding-watched-folder-endpoints)を参照）。
* 電子メールエンドポイントを追加します（[電子メールエンドポイントの追加](programmatically-endpoints.md#adding-email-endpoints)を参照）。
* リモートエンドポイントを追加します（[リモートエンドポイントの追加](programmatically-endpoints.md#adding-remoting-endpoints)を参照）。
* TaskManager エンドポイントを追加します（[TaskManager エンドポイントの追加](programmatically-endpoints.md#adding-taskmanager-endpoints)を参照）。
* エンドポイントを変更します（[エンドポイントの変更](programmatically-endpoints.md#modifying-endpoints)を参照）。
* エンドポイントを削除します（[エンドポイントの削除](programmatically-endpoints.md#removing-endpoints)を参照）。
* エンドポイントコネクタ情報を取得します（[エンドポイントコネクタ情報の取得](programmatically-endpoints.md#retrieving-endpoint-connector-information)を参照）。

## EJB エンドポイントの追加 {#adding-ejb-endpoints}

EJB エンドポイントは、AEM Forms Java API を使用して、プログラムによってサービスに追加できます。EJB エンドポイントをサービスに追加すると、クライアントアプリケーションで EJB モードを使用してサービスを呼び出すことができます。つまり、AEM Forms を呼び出すために必要な接続プロパティを設定する場合は、EJB モードを選択できます（[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照）。

>[!NOTE]
>
>web サービスを使用して EJB エンドポイントを追加することはできません。

>[!NOTE]
>
>通常、EJB エンドポイントはデフォルトでサービスに追加されますが、EJB エンドポイントは、プログラムでデプロイされたプロセスや、EJB エンドポイントが削除され、再度追加される必要があるプロセスに追加できます。

### 手順の概要 {#summary-of-steps}

EJB エンドポイントをサービスに追加するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. `EndpointRegistry Client` オブジェクトを作成します。
1. EJB エンドポイント属性を設定します。
1. EJB エンドポイントを作成します。
1. エンドポイントを有効にします。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar（AEM Forms が JBoss Application Server にデプロイされている場合に必要）
* jbossall-client.jar（AEM Forms が JBoss Application Server にデプロイされている場合に必要）

これらの JAR ファイルの場所については、[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。

**EndpointRegistry Client オブジェクトを作成する**

EJB エンドポイントをプログラムで追加する前に、 `EndpointRegistryClient` オブジェクトを作成する必要があります。

**EJB エンドポイント属性を設定する**

サービスの EJB エンドポイントを作成するには、次の値を指定します。

* **コネクタ識別子**：作成するエンドポイントのタイプを指定します。EJB エンドポイントを作成するには、`EJB` を指定します。
* **説明**：エンドポイントの説明を指定します。
* **名前**：エンドポイントの名前を指定します。
* **サービス識別子**：エンドポイントが属するサービスを指定します。
* **操作名**：エンドポイントを使用して呼び出す操作の名前を指定します。EJB エンドポイントを作成する際に、ワイルドカード文字（`*`）を指定します。ただし、すべてのサービス操作を呼び出すのではなく、特定の操作を指定する場合は、ワイルドカード文字（`*`）を使用するのではなく、操作の名前を指定します。

**EJB エンドポイントを作成する**

EJB エンドポイント属性を設定した後、サービス用の EJB エンドポイントを作成できます。

**エンドポイントを有効にする**

新しいエンドポイントを作成したら、そのエンドポイントを有効にする必要があります。エンドポイントを有効にした後は、エンドポイントを使用してサービスを呼び出すことができます。エンドポイントを有効にすると、管理コンソール内で表示できます。

**関連トピック**

[Java API を使用した EJB エンドポイントの追加](programmatically-endpoints.md#adding-an-ejb-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API を使用した EJB エンドポイントの追加 {#adding-an-ejb-endpoint-using-the-java-api}

Java API を使用して EJB エンドポイントを追加します。

1. プロジェクトファイルを含めます。

   adobe-livecycle-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。（

1. EndpointRegistry クライアントオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `ServiceClientFactory` オブジェクトを渡すことによって、`EndpointRegistryClient` オブジェクトを作成します。

1. EJB エンドポイント属性を設定します。

   * コンストラクタを使用して `CreateEndpointInfo` オブジェクトを作成します。
   * `CreateEndpointInfo` オブジェクトの `setConnectorId` メソッドを呼び出し、文字列値 `EJB` を渡すことによって、コネクタ識別子の値を指定します。
   * `CreateEndpointInfo` オブジェクトの `setDescription` メソッドを呼び出し、エンドポイントを説明する文字列値を渡すことによって、エンドポイントの説明を指定します。
   * `CreateEndpointInfo` オブジェクトの `setName` メソッドを呼び出し、名前を指定する文字列値を渡すことによって、エンドポイントの名前を指定します。
   * `CreateEndpointInfo` オブジェクトの `setServiceId` メソッドを呼び出し、サービス名を指定する文字列値を渡すことによって、エンドポイントが属するサービスを指定します。
   * `CreateEndpointInfo` オブジェクトの `setOperationName` メソッドを呼び出し、操作名を指定する文字列値を渡すことによって、呼び出される操作を指定します。SOAP および EJB エンドポイントの場合は、ワイルドカード文字（`*`）を指定します。これは、すべての操作を示します。

1. EJB エンドポイントを作成します。

   `EndpointRegistryClient` オブジェクトの `createEndpoint` メソッドを呼び出し、`CreateEndpointInfo` オブジェクトを渡すことによって、エンドポイントを作成します。このメソッドは、新しい EJB エンドポイントを表す `Endpoint` オブジェクトを返します。

1. エンドポイントを有効にします。

   `EndpointRegistryClient` オブジェクトの enable メソッドを呼び出し、`createEndpoint` メソッドによって返された `Endpoint` オブジェクトを渡すことによって、エンドポイントを有効にします。

**関連トピック**

[手順の概要](programmatically-endpoints.md#summary-of-steps)

[クイックスタート：Java API を使用した EJB エンドポイントの追加](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-ejb-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## SOAP エンドポイントの追加 {#adding-soap-endpoints}

SOAP エンドポイントは、AEM Forms Java API を使用して、プログラムによってサービスに追加できます。SOAP エンドポイントを追加すると、クライアントアプリケーションで SOAP モードを使用してサービスを呼び出すことができます。つまり、AEM Forms を呼び出すために必要な接続プロパティを設定する場合、SOAP モードを選択できます。

>[!NOTE]
>
>Web サービスを使用して SOAP エンドポイントを追加することはできません。

>[!NOTE]
>
>通常、SOAP エンドポイントはデフォルトでサービスに追加されますが、SOAP エンドポイントは、プログラムでデプロイされたプロセスや、SOAP エンドポイントが削除され、再度追加される必要があるプロセスに追加できます。

### 手順の概要 {#summary_of_steps-1}

SOAP エンドポイントをサービスに追加するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. `EndpointRegistryClient` オブジェクトを作成します。
1. SOAP エンドポイント属性を設定します。
1. SOAP エンドポイントを作成します。
1. エンドポイントを有効にします。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、必ずプロキシファイルを含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar（AEM Forms が JBoss Application Server にデプロイされている場合に必要）
* jbossall-client.jar（AEM Forms が JBoss Application Server にデプロイされている場合に必要）

これらの JAR ファイルは、SOAP エンドポイントを作成するために必要です。ただし、SOAP エンドポイントを使用してサービスを呼び出す場合は、追加の JAR ファイルが必要です。AEM Forms JAR ファイルについて詳しくは、[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。

**EndpointRegistry クライアントオブジェクトの作成**

プログラムによって SOAP エンドポイントをサービスに追加するには、 `EndpointRegistryClient` オブジェクトを作成する必要があります。

**SOAP エンドポイント属性を設定する**

SOAP エンドポイントをサービスに追加するには、次の値を指定します。

* **コネクタ識別子の値**：作成するエンドポイントのタイプを指定します。SOAP エンドポイントを作成するには、`SOAP` を指定します。
* **説明**：エンドポイントの説明を指定します。
* **名前**：エンドポイントの名前を指定します。
* **サービス識別子の値**：エンドポイントが属するサービスを指定します。
* **操作名**：エンドポイントを使用して呼び出される操作の名前を指定します。SOAP エンドポイントを作成する際に、ワイルドカード文字（`*`）を指定します。ただし、すべてのサービス操作を呼び出すのではなく、特定の操作を指定する場合は、ワイルドカード文字（`*`）を使用するのではなく、操作の名前を指定します。

**SOAP エンドポイントを作成する**

SOAP エンドポイント属性を設定した後、SOAP エンドポイントを作成できます。

**エンドポイントを有効にする**

新しいエンドポイントを作成したら、そのエンドポイントを有効にする必要があります。エンドポイントが有効であれば、サービスの呼び出しに使用することができます。エンドポイントを有効にすると、管理コンソール内で表示できます。

**関連トピック**

[Java API を使用した SOAP エンドポイントの追加](programmatically-endpoints.md#add-a-soap-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API を使用した SOAP エンドポイントの追加 {#add-a-soap-endpoint-using-the-java-api}

Java API を使用して、SOAP エンドポイントをサービスに追加します。

1. プロジェクトファイルを含めます。

   adobe-livecycle-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. EndpointRegistry クライアントオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `ServiceClientFactory` オブジェクトを渡すことによって、`EndpointRegistryClient` オブジェクトを作成します。

1. SOAP エンドポイント属性を設定します。

   * コンストラクタを使用して `CreateEndpointInfo` オブジェクトを作成します。
   * `CreateEndpointInfo` オブジェクトの `setConnectorId` メソッドを呼び出し、文字列値 `SOAP` を渡すことによって、コネクタ識別子の値を指定します。
   * `CreateEndpointInfo`オブジェクトの `setDescription` メソッドを呼び出し、エンドポイントを説明する文字列値を渡すことによって、エンドポイントの説明を指定します。
   * `CreateEndpointInfo` オブジェクトの `setName` メソッドを呼び出し、名前を指定する文字列値を渡すことによって、エンドポイントの名前を指定します。
   * `CreateEndpointInfo` オブジェクトの `setServiceId` メソッドを呼び出し、サービス名を指定する文字列値を渡すことによって、エンドポイントが属するサービスを指定します。
   * `CreateEndpointInfo` オブジェクトの `setOperationName` メソッドを呼び出し、操作名を指定する文字列値を渡すことによって、呼び出される操作を指定します。SOAP および EJB エンドポイントの場合は、ワイルドカード文字（`*`）を指定します。これは、すべての操作を示します。

1. SOAP エンドポイントを作成します。

   `EndpointRegistryClient` オブジェクトの `createEndpoint` メソッドを呼び出し、`CreateEndpointInfo` オブジェクトを渡すことによって、エンドポイントを作成します。このメソッドは、新しい SOAP エンドポイントを表す `Endpoint` オブジェクトを返します。

1. エンドポイントを有効にします。

   `EndpointRegistryClient` オブジェクトの enable メソッドを呼び出し、`createEndpoint` メソッドによって返された `Endpoint` オブジェクトを渡すことによって、エンドポイントを有効にします。

**関連トピック**

[手順の概要](programmatically-endpoints.md#summary-of-steps)

[クイックスタート：Java API を使用した SOAP エンドポイントの追加](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-soap-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 監視フォルダーエンドポイントの追加 {#adding-watched-folder-endpoints}

AEM Forms Java API を使用して、プログラムによって監視フォルダーエンドポイントをサービスに追加できます。監視フォルダーエンドポイントを追加すると、ユーザーはフォルダーにファイル (PDF ファイルなど ) を配置できます。 ファイルがフォルダーに配置されると、設定済みのサービスが呼び出され、ファイルを操作します。 サービスが指定の操作を実行した後に、変更されたファイルが指定の出力フォルダーに保存されます。監視フォルダーは、毎週月曜日、水曜日、金曜日の正午など、一定の時間間隔で、または Cron スケジュールでスキャンされるように設定されています。

監視フォルダーエンドポイントをプログラムによってサービスに追加する場合は、*EncryptDocument* という名前の短時間のみ有効なプロセスを考慮してください（[AEM Formsプロセスについて](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes)を参照してください）。

![aw_aw_encryptdocumentprocess](assets/aw_aw_encryptdocumentprocess.png)

このプロセスは、セキュリティで保護されていない PDF ドキュメントを入力値として受け取り、セキュリティで保護されていない PDF ドキュメントを Encryption サービスの `EncryptPDFUsingPassword` 操作に渡します。PDF ドキュメントをパスワードで暗号化し、パスワードで暗号化された PDF ドキュメントはこのプロセスの出力値です。入力値の名前 ( 保護されていない PDF ドキュメント ) は `InDoc`、 データタイプは `com.adobe.idp.Document`です。出力値の名前 ( パスワードで暗号化された PDF ドキュメント ) は `SecuredDoc`、 データタイプは `com.adobe.idp.Document`です。

>[!NOTE]
>
>Web サービスを使用した監視フォルダーエンドポイントの追加はできません。

### 手順の概要 {#summary_of_steps-2}

監視フォルダーエンドポイントをサービスに追加するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. `EndpointRegistryClient`オブジェクトを作成します。
1. 監視フォルダーエンドポイントの属性を設定します。
1. 設定値を指定します。
1. 入力パラメーター値を定義します。
1. 出力パラメーター値を定義します。
1. 監視フォルダーエンドポイントを作成します。
1. エンドポイントを有効にします。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、必ずプロキシファイルを含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar（AEM Forms が JBoss Application Server にデプロイされている場合に必要）
* jbossall-client.jar（AEM Forms が JBoss Application Server にデプロイされている場合に必要）

これらの JAR ファイルの場所については、[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。

**EndpointRegistry Client オブジェクトの作成**

プログラムによって監視フォルダーエンドポイントを追加するには、 `EndpointRegistryClient` オブジェクトを作成する必要があります。

**監視フォルダーエンドポイントの属性を設定する**

サービスの監視フォルダーエンドポイントを作成するには、次の値を指定します。

* **コネクタ識別子**：作成するエンドポイントのタイプを指定します。監視フォルダーエンドポイントを作成するには、次を指定します。 `WatchedFolder`
* **説明**：エンドポイントの説明を指定します。
* **名前**：エンドポイントの名前を指定します。
* **サービス識別子**：エンドポイントが属するサービスを指定します。例えば、この節で説明するプロセスに監視フォルダーエンドポイントを追加する場合（Workbench を使用してアクティベートすると、プロセスはサービスになります）、 `EncryptDocument`を指定します。
* **操作名**：エンドポイントを使用して呼び出される操作の名前を指定します。通常、Workbench で作成されたプロセスから発生するサービスの監視フォルダーエンドポイントを作成する場合、操作の名前は`invoke`になります。

**設定値の指定**

プログラムによって監視フォルダーエンドポイントをサービスに追加する場合は、監視フォルダーエンドポイントの設定値を指定する必要があります。 管理コンソールを使用して監視フォルダーエンドポイントを追加した場合、これらの設定値は管理者が指定します。

次のリストでは、監視フォルダーエンドポイントをプログラムでサービスに追加する際に設定される設定値を指定します。

* **パス**：監視フォルダーの場所を指定します。クラスター環境では、クラスター内のすべてのコンピューターからアクセスできる共有ネットワークフォルダーを指定する必要があります。
* **非同期**：呼び出しを非同期型にするか同期型にするかを指定します。一次的プロセスや同期プロセスは、同期のみ呼び出すことができます。デフォルト値は true です。非同期をお勧めします。
* **cronExpression**：Quartz で、入力ディレクトリのポーリングをスケジュールするために使用されます。
* **purgeDuration**：これは必須の属性です。結果フォルダー内のファイルやフォルダがこの値よりも古い場合には、そのファイルやフォルダが削除されます。この値の単位は日です。この属性は、結果フォルダーに常に空き容量を確保しておきたい場合に役立ちます。-1 を指定すると、結果フォルダーの削除は行われません。デフォルト値は -1 です。
* **repeatInterval**：入力の有無を確認するために監視フォルダーをスキャンする間隔（秒単位）です。「ジョブ数を制限」が有効になっている場合を除き、平均的なジョブの処理にかかる時間よりも長い時間をこの値に指定する必要があります。そうしないと、システムが過負荷になるおそれがあります。デフォルト値は 5 です。
* **repeatCount**：監視フォルダーがフォルダーまたはディレクトリをスキャンする回数です。-1 を指定すると、無限にスキャンされます。デフォルト値は -1 です。
* **throttleOn**：一度に処理できる監視フォルダーのジョブ数を制限します。ジョブの最大数は、batchSize の値によって決まります。
* **userName**：監視フォルダーからターゲットサービスを呼び出すときに使用されるユーザー名です。この値は必須です。デフォルト値は「SuperAdmin」です。
* **domainName**：ユーザーのドメインです。この値は必須です。デフォルト値は「DefaultDom」です。
* **batchSize**：1 回のスキャンで取得されるファイルまたはフォルダーの数です。この値を使用して、システムが過負荷の状態になるのを防ぎます。一度にスキャンするファイル数が多すぎると、クラッシュにつながる可能性があります。デフォルト値は 2 です。
* **waitTime**：フォルダーまたはファイルを作成してからスキャンするまでに待機する時間（ミリ秒単位）です。例えば、待機時間が 36,000,000 ミリ秒（1 時間）のときにファイルが 1 分前に作成されている場合、59 分以上経過するとこのファイルが取得されます。この属性は、ファイルまたはフォルダーを入力フォルダーにコピーする処理を確実に完了するために役立ちます。例えば、処理の対象となるファイルサイズが大きく、そのファイルをダウンロードするのに 10 分かかる場合は、待機時間を 10 x 60 x 1000 ミリ秒に設定します。このように設定しておけば、監視フォルダーが 10 分間待機せずにファイルをスキャンすることを防げます。デフォルト値は 0 です。
* **excludeFilePattern**：スキャンおよび取得するファイルとフォルダーを判別する際に監視フォルダーが使用するパターンです。このパターンに当てはまるファイルまたはフォルダーは、スキャン処理の対象外となります。この設定は、複数のファイルが存在するフォルダーが入力に使用される場合に便利です。フォルダーの内容を、監視フォルダーの取得対象となる名前のフォルダーにコピーすることができます。この手順により、入力フォルダーにフォルダーを完全にコピーする前に、監視フォルダーがフォルダーを取得して処理することを回避できます。例えば、excludeFilePattern の値が `data*` であれば、`data*` に一致するファイルとフォルダーはいずれも取得されません。`data1` や `data2` などといった名前のファイルとフォルダーがこれに該当します。また、ワイルドカードパターンをパターンに追加してファイルパターンを指定することもできます。監視フォルダーでは、`*.*` や `*.pdf` などのワイルドカードパターンをサポートするよう、正規表現を変更しました。これらのワイルドカードパターンは、正規表現ではサポートされていません。
* **includeFilePattern**：スキャンおよび取得の対象となるフォルダーとファイルを判別するために監視フォルダーが使用するパターンです。例えば、この値が `*` であれば、`input*` に一致するすべてのファイルとフォルダーが取得されます。`input1` や `input2` などといった名前のファイルとフォルダーがこれに該当します。デフォルト値は `*` です。この値は、すべてのファイルとフォルダーが対象になることを示しています。また、ワイルドカードパターンをパターンに追加してファイルパターンを指定することもできます。監視フォルダーでは、`*.*` や `*.pdf` などのワイルドカードパターンに対応するよう、正規表現を変更しました。これらのワイルドカードパターンは、正規表現では対応していません。この値は必須です。
* **resultFolderName**：保存された結果を格納するフォルダーです。この場所には、絶対ディレクトリパスや相対ディレクトリパスを指定することができます。結果がこのフォルダーに表示されない場合は、失敗フォルダーを確認してください。読み取り専用ファイルは処理されず、失敗フォルダーに保存されます。デフォルト値は `result/%Y/%M/%D/` です。これは、監視フォルダー内の結果フォルダーです。
* **preserveFolderName**：スキャンとピックアップに成功した後にファイルが保存される場所です。この場所は、絶対パス、相対パス、null ディレクトリパスのいずれかを指定できます。デフォルト値は `preserve/%Y/%M/%D/` です。
* **failureFolderName**：失敗ファイルが保存されるフォルダーです。この場所は、常に監視フォルダーからの相対パスで指定します。読み取り専用ファイルは処理されず、失敗フォルダーに保存されます。デフォルト値は `failure/%Y/%M/%D/` です。
* **preserveOnFailure**：サービスで操作の実行に失敗した場合に、入力ファイルを保存します。デフォルト値は true です。
* **overwriteDuplicateFilename**：この値を True に設定すると、結果フォルダーと保存用フォルダーにあるファイルが上書きされます。false 設定すると、ファイルやフォルダーの名前に数字のインデックスサフィックスが使用されます。デフォルト値は false です。

**入力パラメーター値の定義**

監視フォルダーエンドポイントを作成する場合は、入力パラメーターの値を定義する必要があります。つまり、監視フォルダーによって呼び出される操作に渡される入力値を記述する必要があります。 例えば、このトピックで紹介するプロセスについて考えてみましょう。入力値として `InDoc` があり、データ型は `com.adobe.idp.Document` です。このプロセスの監視フォルダーエンドポイントを作成する場合（プロセスがアクティブ化されると、そのエンドポイントがサービスになります）、入力パラメーターの値を定義する必要があります。

監視フォルダーエンドポイントに必要な入力パラメーター値を定義するには、次の値を指定します。

**パラメーター名を入力**：入力パラメーターの名前。入力値の名前は、プロセスに対して Workbench で指定されます。入力値がサービス操作（Workbench で作成されたプロセスではないサービス）に属する場合、入力名は component.xml ファイルで指定されます。たとえば、このセクションで紹介するプロセスの入力パラメーターの名前は、`InDoc` です。

**マッピングタイプ**：サービス操作を呼び出すために必要な入力値を設定するために使用します。 マッピングには次の 2 つのタイプがあります。

* `Literal`：監視フォルダーでは、フィールドに入力された値が表示どおりに使用されます。すべての基本 Java 型がサポートされます。たとえば、文字列、long、int および Boolean などの入力が使用される API の場合、文字列は適切な型に変換され、サービスが呼び出されます。
* `Variable`：監視フォルダーでは、入力した値をファイルパターンとして使用して入力を取得します。例えば、マッピングの種類に「変数」を選択し、入力ドキュメントを PDF ファイルにする場合、 `*.pdf` をマッピング値として使用します。

**マッピング値**：マッピングタイプの値を指定します。例えば、`Variable` マッピングのタイプを選択した場合は、 `*.pdf` をファイルパターンとして指定できます。

**データタイプ**：入力値のデータタイプを指定します。例えば、このセクションで紹介するプロセスの入力値のデータタイプは、`com.adobe.idp.Document` です。

**出力パラメーター値の定義**

監視フォルダーエンドポイントを作成する場合は、出力パラメーターの値を定義する必要があります。つまり、監視フォルダーエンドポイントによって呼び出されるサービスが返す出力値を記述する必要があります。例えば、このトピックで紹介するプロセスについて考えてみましょう。出力値の名前が `SecuredDoc` で、データタイプが `com.adobe.idp.Document` とします。このプロセスの監視フォルダーエンドポイントを作成する場合（プロセスは、アクティブにするとサービスになります）、出力パラメーターの値を定義する必要があります。

監視フォルダーエンドポイントに必要な出力パラメーター値を定義するには、次の値を指定します。

**出力パラメーター名**：出力パラメーターの名前。プロセス出力値の名前は、Workbench で指定します。出力値がサービス操作（Workbench で作成したプロセスではないサービス）に属する場合、出力名は component.xml ファイルで指定します。例えば、このセクションで紹介するプロセスの出力パラメーターの名前は `SecuredDoc` です。

**マッピングタイプ**：サービスおよび操作の出力を設定するために使用します。以下のオプションを利用できます。

* サービスが 1 つのオブジェクト（1 つのドキュメント）を返す場合、パターンは `%F.pdf` で、ソースの宛先は sourcefilename.pdf です。例えば、このセクションで紹介したプロセスは、1 つのドキュメントを返します。そのため、マッピングタイプは `%F.pdf` と定義できます（`%F` は、指定のファイル名を使用することを意味します）。パターン `%E` は、入力ドキュメントの拡張を指定します。
* サービスがリストを返す場合、パターンは `Result\%F\` で、ソースの宛先は Result\sourcefilename\source1（出力 1）および Result\sourcefilename\source2（出力 2）です。
* サービスがマップを返す場合、パターンは `Result\%F\` で、ソースの宛先は Result\sourcefilename\file1 および Result\sourcefilename\file2 です。マップに複数のオブジェクトがある場合、パターンは `Result\%F.pdf` で、ソースの宛先は Result\sourcefilename1.pdf（出力 1）、Result\sourcefilenam2.pdf（出力 2）などです。

**データタイプ**：戻り値のデータタイプを指定します。例えば、このセクションで紹介するプロセスの戻り値のデータタイプは `com.adobe.idp.Document` です。

**監視フォルダーエンドポイントの作成**

エンドポイントの属性を設定し、設定値を指定して、さらに入力パラメーターと出力パラメーターの値を定義した後、監視フォルダーエンドポイントを作成する必要があります。

**エンドポイントを有効にする**

監視フォルダーエンドポイントを作成したら、そのエンドポイントを有効にする必要があります。エンドポイントが有効であれば、サービスの呼び出しに使用することができます。有効にしたエンドポイントは、管理コンソール内に表示されます。

**関連トピック**

[Java API を使用して監視フォルダーエンドポイントを追加する](programmatically-endpoints.md#add-a-watched-folder-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API を使用して監視フォルダーエンドポイントを追加する {#add-a-watched-folder-endpoint-using-the-java-api}

AEM Forms Java API を使用して、監視フォルダーエンドポイントを追加します。

1. プロジェクトファイルを含めます。

   adobe-livecycle-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. EndpointRegistry Client オブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して `ServiceClientFactory` オブジェクトを渡し、`EndpointRegistryClient` オブジェクトを作成します。

1. 監視フォルダーエンドポイントの属性を設定します。

   * コンストラクターを使用して `CreateEndpointInfo` オブジェクトを作成します。
   * `CreateEndpointInfo` オブジェクトの `setConnectorId` メソッドを呼び出し、文字列値 `WatchedFolder` を渡して、コネクター識別子の値を指定します。
   * `CreateEndpointInfo` オブジェクトの `setDescription` メソッドを呼び出し、エンドポイントを表す文字列値を渡すことによって、エンドポイントの説明を指定します。
   * `CreateEndpointInfo` オブジェクトの `setName` メソッドを呼び出し、名前を指定する文字列値を渡すことによって、エンドポイントの名前を指定します。
   * `CreateEndpointInfo` オブジェクトの `setServiceId` メソッドを呼び出し、サービス名を指定する文字列値を渡して、エンドポイントが属するサービスを指定します。
   * `CreateEndpointInfo` オブジェクトの `setOperationName` メソッドを呼び出し、操作名を指定する文字列値を渡して、呼び出される操作を指定します。通常、Workbench で作成されたプロセスから生成されたサービスの監視フォルダーエンドポイントを作成する場合、操作名は invoke になります。

1. 設定値を指定します。

   監視フォルダーエンドポイントに設定する設定値ごとに、`CreateEndpointInfo` オブジェクトの `setConfigParameterAsText` メソッドを呼び出す必要があります。例えば、`url` の設定値を設定するには、`CreateEndpointInfo` オブジェクトの `setConfigParameterAsText` メソッドを呼び出して、以下の文字列値を渡します。

   * 設定値の名前を指定する文字列値。`url` の設定値を設定するには、`url` を指定します。
   * 設定値の値を指定する文字列値。`url` 設定値を設定するには、監視フォルダーの場所を指定します。

   >[!NOTE]
   >
   >EncryptDocument サービスに設定されたすべての設定値を確認するには、[QuickStart：Java API を使用した監視フォルダーエンドポイントの追加](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)にある Java コードの例を参照してください。

1. 入力パラメーター値を定義します。

   `CreateEndpointInfo` オブジェクトの `setInputParameterMapping` メソッドを呼び出して入力パラメーター値を定義し、以下の値を渡します。

   * 入力パラメーターの名前を指定する文字列値。例えば、EncryptDocument サービスの入力パラメーター名は `InDoc` です。
   * 入力パラメーターのデータタイプを指定する文字列値。例えば、`InDoc` 入力パラメーターのデータタイプは `com.adobe.idp.Document` です。
   * マッピングタイプを指定する文字列値です。 例えば、`variable` を指定できます。
   * マッピングタイプの値を指定する文字列値。例えば、ファイルパターンとして、&amp;ast;.pdf を指定できます。

   >[!NOTE]
   >
   >定義する入力パラメーターの値ごとに `setInputParameterMapping` メソッドを呼び出します。 EncryptDocument プロセスには入力パラメーターが 1 つしかないので、このメソッドを 1 度呼び出す必要があります。

1. 出力パラメーター値を定義します。

   出力パラメーター値を定義するには、`CreateEndpointInfo` オブジェクトの `setOutputParameterMapping` メソッドを呼び出し、以下の値を渡します。

   * 出力パラメーターの名前を指定する文字列値。例えば、EncryptDocument サービスの出力パラメーター名は `SecuredDoc` となります。
   * 出力パラメーターのデータタイプを指定する文字列値。例えば、`SecuredDoc` 出力パラメーターのデータタイプは `com.adobe.idp.Document` となります。
   * マッピングタイプを指定する文字列値です。 例えば、`%F.pdf` を指定できます。

1. 監視フォルダーエンドポイントを作成します。

   エンドポイントを作成するには、`EndpointRegistryClient` オブジェクトの `createEndpoint` メソッドを呼び出し、`CreateEndpointInfo` オブジェクトを渡します。このメソッドは、 監視フォルダーエンドポイントを表す `Endpoint` オブジェクトを返します。

1. エンドポイントを有効にします。

   エンドポイントを有効にするには、`EndpointRegistryClient` オブジェクトの `enable` メソッドを呼び出し、`createEndpoint` メソッドから返された `Endpoint` オブジェクトを渡します。

**関連トピック**

[手順の概要](programmatically-endpoints.md#summary-of-steps)

[QuickStart：Java API を使用した監視フォルダーエンドポイントの追加](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 監視フォルダー設定値定数ファイル {#watched-folder-configuration-values-constant-file}

[クイックスタート：Java API を使用した監視フォルダーエンドポイントの追加](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)は、クイックスタートをコンパイルするために Java プロジェクトの一部である必要のある定数ファイルを使用します。 この定数ファイルは、監視フォルダーエンドポイントを追加する際に設定する必要がある設定値を表します。 次の Java コードは、定数ファイルを表しています。

```java
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

AEM Forms Java API を使用して、プログラムによって電子メールエンドポイントをサービスに追加できます。 電子メールエンドポイントを追加すると、1 つ以上の添付ファイルを含む電子メールメッセージを、指定した電子メールアカウントに送信することをユーザーに許可できます。 次に、サービス操作の設定が呼び出され、ファイルを操作します。 指定した操作を実行すると、変更されたファイルが添付ファイルとして送信者に電子メールメッセージが送信されます。

電子メールエンドポイントをプログラムでサービスに追加する場合は、*MyApplication\EncryptDocument* のような短時間のみ有効なプロセスを考慮してください。短時間のみ有効なプロセスについては、 [AEM Formsプロセスについて](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes)を参照してください。

![ae_ae_encryptdocumentprocess](assets/ae_ae_encryptdocumentprocess.png)

このプロセスは、セキュリティで保護されていない PDF ドキュメントを入力値として受け取り、セキュリティで保護されていない PDF ドキュメントを Encryption サービスの `EncryptPDFUsingPassword` 操作に渡します。 このプロセスは、PDF ドキュメントをパスワードで暗号化し、パスワードで暗号化された PDF ドキュメントを出力値として返します。 入力値の名前（保護されていない PDF ドキュメント）は `InDoc`、データタイプは `com.adobe.idp.Document` です。 出力値の名前（パスワードで暗号化された PDF ドキュメント）は `SecuredDoc`、データタイプは `com.adobe.idp.Document` です。

>[!NOTE]
>
>Web サービスを使用して電子メールエンドポイントを追加することはできません。

### 手順の概要 {#summary_of_steps-3}

電子メールエンドポイントをサービスに追加するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1.  `EndpointRegistryClient` オブジェクトを作成します。
1. 電子メールエンドポイント属性を設定します。
1. 設定値を指定します。
1. 入力パラメーター値を定義します。
1. 出力パラメーター値を定義します。
1. 電子メールエンドポイントを作成します。
1. エンドポイントを有効にします。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、必ずプロキシファイルを含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar（AEM Forms が JBoss Application Server にデプロイされている場合に必要）
* jbossall-client.jar（AEM Forms が JBoss Application Server にデプロイされている場合に必要）

これらの JAR ファイルの場所については、[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。

**EndpointRegistry Client オブジェクトの作成**

プログラム的に電子メールエンドポイントを追加する前に、 `EndpointRegistryClient` オブジェクトを作成する必要があります。

**電子メールエンドポイント属性の設定**

サービスの電子メールエンドポイントを作成するには、次の値を指定します。

* **コネクタ識別子の値**：作成するエンドポイントのタイプを指定します。 電子メールエンドポイントを作成する場合は、`Email` を指定します。
* **説明**：エンドポイントの説明を指定します。
* **名前**：エンドポイントの名前を指定します。
* **サービス識別子の値**：エンドポイントが属するサービスを指定します。例えば、このセクションで紹介するプロセスに電子メールのエンドポイントを追加する場合（プロセスは Workbench を使用してアクティベートするとサービスになります）、`EncryptDocument` を指定します。
* **操作名**：エンドポイントを使用して呼び出される操作の名前を指定します。通常、Workbench で作成したプロセスから生成されるサービスの電子メールエンドポイントを作成する場合、操作の名前は `invoke` です。

**設定値の指定**

電子メールエンドポイントをサービスにプログラム的に追加する場合は、電子メールエンドポイントの設定値を指定する必要があります。これらの設定値は、管理コンソールを使用して電子メールエンドポイントを追加する場合に、管理者が指定します。

>[!NOTE]
>
>監視対象のメールアカウントは、電子メールエンドポイントにのみ使用される専用のアカウントです。このアカウントは通常のユーザーのメールアカウントではありません。通常のユーザーのメールアカウントは、メールプロバイダーが使用するアカウントとして設定してはいけません。これはメッセージの処理が完了すると、メールプロバイダーがインボックスからメッセージを削除するためです。

電子メールエンドポイントをサービスにプログラム的に追加する際に、次の設定値が設定されます。

* **cronExpression**：Cron 形式を使用してメールをスケジュールする必要がある場合の Cron 形式です。
* **repeatCount**：電子メールエンドポイントでフォルダーまたはディレクトリをスキャンする回数です。-1 を指定すると、無限にスキャンされます。デフォルト値は -1 です。
* **repeatInterval**：受信側が受信メールの有無をチェックするために使用するスキャン頻度（秒単位）です。デフォルト値は 10 です。
* **startDelay**：スケジューラーを開始してからスキャンを実行するまでの待機時間です。デフォルトの時間は 0 です。
* **batchSize**：受信側が 1 回のスキャンで処理するメールの数です。最適なパフォーマンスのために調整します。-1 を指定すると、すべての電子メールが処理されます。デフォルト値は 2 です。
* **userName**：メールからターゲットサービスを呼び出す際に使用するユーザー名です。デフォルト値は `SuperAdmin` です。
* **domainName**：この設定値は必須です。デフォルト値は `DefaultDom` です。
* **domainPattern**：プロバイダーが受け入れる受信メールのドメインパターンを指定します。例えば、`adobe.com` を使用すると、adobe.com から受信したメールのみが処理され、それ以外のドメインからのメールは無視されます。
* **filePattern**：プロバイダーが受け入れる受信メールの添付ファイルのパターンを指定します。これには、特定のファイル拡張子を持つファイル（&amp;ast;.dat や &amp;ast;.xml）、特定の名前のファイル（data）、名前と拡張子が混在する式に一致するファイル（&amp;ast;.[dD][aA]&#39;port&#39;）が該当します。デフォルト値は `*` です。
* **recipientSuccessfulJob**：ジョブの正常終了を示すメッセージの送信先になるメールアドレスです。デフォルトでは、ジョブの正常終了を示すメッセージは常に送信者に送信されます。`sender` と入力すると、メールによる結果通知が送信者に送信されます。最大 100 人の受信者を指定できます。追加の受信者をメールアドレスで指定します。各受信者はコンマで区切ります。 このオプションをオフにするには、この値を空白のままにします。場合によっては、プロセスをトリガーしても、結果のメール通知を受信したくないことがあります。デフォルト値は `sender` です。
* **recipientFailedJob**：ジョブの失敗を示すメッセージの送信先になるメールアドレスです。デフォルトでは、ジョブの失敗を示すメッセージは常に送信者に送信されます。`sender` と入力すると、メールの結果が送信者に送信されます。最大 100 人の受信者を指定できます。追加の受信者をメールアドレスで指定します。各受信者はコンマで区切ります。 このオプションをオフにするには、この値を空白のままにします。デフォルト値は `sender` です。
* **inboxHost**：メールプロバイダーがスキャンの対象とするインボックスのホスト名または IP アドレスです。
* **inboxPort**：メールサーバーが使用するポートです。POP3 のデフォルト値は 110 で、IMAP のデフォルト値は 143 です。SSL が有効になっている場合は、POP3 のデフォルト値は 995 で、IMAP のデフォルト値は 993 です。
* **inboxProtocol**：メールエンドポイントがインボックスをスキャンするときに使用するメールプロトコルです。オプションには `IMAP` と `POP3` があります。 指定のプロトコルはインボックスホストメールサーバーでサポートされている必要があります。
* **inboxTimeOut**：メールプロバイダーがインボックスの応答を待機する時間（秒単位）です。デフォルト値は 60 です。
* **inboxUser**：メールアカウントにログインするためのユーザー名です。メールサーバーと設定によって、メールのユーザー名の部分だけを指定する場合と、完全なメールアドレスを指定する場合があります。
* **inboxPassword**：インボックスユーザーのパスワードです。
* **inboxSSLEnabled**：結果やエラーの通知メッセージを送信する際に、メールプロバイダーが SSL を使用するように強制するには、この値を設定します。 IMAP または POP3 ホストが SSL をサポートしていることを確認します。
* **smtpHost**：メールプロバイダーが結果やエラーメッセージを送信するメールサーバーのホスト名です。
* **smtpPort**：SMTP ポートのデフォルト値は 25 です。
* **smtpUser**：メールプロバイダーが結果やエラーのメール通知を送信する際に使用するユーザーアカウントです。
* **smtpPassword**：SMTP アカウントのパスワードです。SMTP パスワードが不要なメールサーバーもあります。
* **charSet**：メールプロバイダーが使用する文字セットです。 デフォルト値は `UTF-8` です。
* **smtpSSLEnabled**：結果やエラーの通知メッセージを送信する際に、メールプロバイダーが SSL を使用するように強制するには、この値を設定します。 SMTP ホストで SSL がサポートされていることを確認してください。
* **failedJobFolder**：SMTP メールサーバーが動作していない場合に結果を保存するディレクトリを指定します。
* **asynchronous**：「同期」に設定すると、すべての入力ドキュメントが処理された後に 1 回の応答が返されます。「非同期」に設定すると、1 つのドキュメントの処理が完了するたびに応答が返されます。例えば、このトピックで紹介したプロセスのメールエンドポイントが作成され、セキュリティで保護されていない複数の PDF ドキュメントを含むメールメッセージがエンドポイントのインボックスに送信されるとします。 すべての PDF ドキュメントがパスワードで暗号化され、エンドポイントが同期として設定されている場合、セキュリティで保護されたすべての PDF ドキュメントが添付された 1 つの応答メールメッセージが送信されます。 エンドポイントを非同期として設定している場合は、セキュリティで保護された PDF ドキュメントごとに個別の応答メールメッセージが送信されます。 各メールメッセージに、添付ファイルとして 1 つの PDF ドキュメントが含まれます。 デフォルト値は asynchronous（非同期）です。

**入力パラメーター値の定義**

メールエンドポイントを作成する場合、入力パラメーターの値を定義する必要があります。 つまり、メールエンドポイントによって呼び出される操作に渡される入力値を記述する必要があります。 例えば、このトピックで紹介するプロセスについて考えてみましょう。`InDoc` という名前の入力値が 1 つあり、そのデータタイプは `com.adobe.idp.Document` です。このプロセスのメールエンドポイントを作成する場合（プロセスをアクティブにするとサービスになります）、入力パラメーター値を定義する必要があります。

メールエンドポイントに必要な入力パラメーター値を定義するには、次の値を指定します。

**入力パラメーター名**：入力パラメーターの名前。 入力値の名前は、プロセスに対して Workbench で指定されます。入力値がサービス操作に属する場合（Workbench で作成されたプロセスではない Forms サービス）、入力名は component.xml ファイルで指定されます。 例えば、この節で紹介するプロセスの入力パラメーターの名前は `InDoc` です。

**マッピングタイプ**：サービス操作を呼び出すために必要な入力値の設定に使用します。 マッピングタイプには次の 2 種類があります。

* `Literal`：メールエンドポイントは、フィールドに入力した値を表示どおりに使用します。基本 Java 型がすべてサポートされます。例えば、文字列、long、int および Boolean などの入力が使用される API の場合、文字列は適切な型に変換され、サービスが呼び出されます。
* `Variable`：入力した値は、電子メールエンドポイントが入力を取得するのに使用するファイルパターンです。例えば、マッピングタイプに「変数」を選択し、入力ドキュメントを PDF ファイルにすると、マッピング値として `*.pdf` を使用します。

**マッピング値**：マッピングタイプの値を指定します。例えば、マッピングタイプに「変数」を選択した場合、ファイルパターンとして `*.pdf` を指定できます。

**データタイプ**：入力値のデータタイプを指定します。例えば、このセクションで紹介したプロセスの入力値のデータタイプは com.adobe.idp.Document です。

**出力パラメーター値の定義**

電子メールエンドポイントを作成する場合は、出力パラメーター値を定義する必要があります。つまり、電子メールエンドポイントによって呼び出されるサービスが返す出力値を記述する必要があります。例えば、このトピックで紹介するプロセスについて考えてみましょう。出力値の名前は `SecuredDoc` で、データタイプは `com.adobe.idp.Document` です。このプロセスの電子メールエンドポイントを作成する場合（プロセスは、アクティブにするとサービスになります）、出力パラメーター値を定義する必要があります。

電子メールエンドポイントに必要な出力パラメーター値を定義するには、次の値を指定します。

**出力パラメーター名**：出力パラメーターの名前。 プロセス出力値の名前は、Workbench で指定します。出力値がサービス操作（Workbench で作成したプロセスではないサービス）に属する場合、出力名は component.xml ファイルで指定します。例えば、このセクションで紹介するプロセスの出力パラメーターの名前は `SecuredDoc` です。

**マッピングタイプ**：サービスおよび操作の出力を設定するために使用します。以下のオプションが利用できます。

* サービスが 1 つのオブジェクト（1 つのドキュメント）を返す場合、パターンは `%F.pdf` で、ソースの宛先は sourcefilename.pdf です。 例えば、このセクションで紹介したプロセスは、1 つのドキュメントを返します。その結果、マッピングタイプは `%F.pdf`（`%F` は、指定されたファイル名を使用することを意味します）と定義されます。 パターン `%E` は、入力ドキュメントの拡張を指定します。
* サービスがリストを返す場合、パターンは `Result\%F\` で、ソースの宛先は Result\sourcefilename\source1（出力 1）および Result\sourcefilename\source2（出力 2）です。
* サービスがマップを返す場合、パターンは `Result\%F\` で、ソースの宛先は Result\sourcefilename\file1 および Result\sourcefilename\file2 です。 マップに複数のオブジェクトがある場合、パターンは `Result\%F.pdf` で、ソースの宛先は Result\sourcefilename1.pdf（出力 1）、Result\sourcefilenam2.pdf（出力 2）などです。

**データタイプ**：戻り値のデータタイプを指定します。例えば、このセクションで紹介するプロセスの戻り値のデータタイプは `com.adobe.idp.Document` です。

**メールエンドポイントの作成**

メールエンドポイントの属性と設定値を設定し、入力および出力パラメーターの値を定義した後、メールエンドポイントを作成する必要があります。

**エンドポイントを有効にする**

メールエンドポイントを作成したら、そのエンドポイントを有効にする必要があります。 エンドポイントが有効であれば、サービスの呼び出しに使用することができます。エンドポイントを有効にすると、管理コンソール内で表示できます。

**関連トピック**

[Java API を使用したメールエンドポイントの追加](programmatically-endpoints.md#add-an-email-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API を使用したメールエンドポイントの追加 {#add-an-email-endpoint-using-the-java-api}

Java API を使用してメールエンドポイントを追加します。

1. プロジェクトファイルを含めます。

   adobe-livecycle-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. EndpointRegistry クライアントオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して `ServiceClientFactory` オブジェクトを渡すことによって、`EndpointRegistryClient` オブジェクトを作成します。

1. 電子メールエンドポイント属性を設定します。

   * コンストラクタを使用して `CreateEndpointInfo` オブジェクトを作成します。
   * コネクタ識別子の値を指定するには、`CreateEndpointInfo` オブジェクトの `setConnectorId` メソッドを呼び出し、文字列値 `Email` を渡します。
   * エンドポイントの説明を指定するには、`CreateEndpointInfo` オブジェクトの `setDescription` メソッドを呼び出し、エンドポイントを説明する文字列値を渡します。
   * エンドポイントの名前を指定するには、`CreateEndpointInfo` オブジェクトの `setName` メソッドを呼び出し、名前を指定する文字列値を渡します。
   * エンドポイントが属するサービスを指定するには、`CreateEndpointInfo` オブジェクトの `setServiceId` メソッドを呼び出し、サービス名を指定する文字列値を渡します。
   * 呼び出す操作を指定するには、`CreateEndpointInfo` オブジェクトの `setOperationName` メソッドを呼び出し、操作名を指定する文字列値を渡します。通常、Workbench で作成されたプロセスから派生するサービスのメールエンドポイントを作成する場合、操作の名前は「呼び出し」になります。

1. 設定値を指定します。

   メールエンドポイントに設定する設定値ごとに、`CreateEndpointInfo` オブジェクトの `setConfigParameterAsText` メソッドを呼び出す必要があります。 例えば、`smtpHost` 設定値を設定するには、`CreateEndpointInfo` オブジェクトの `setConfigParameterAsText` メソッドを呼び出して、次の値を渡します。

   * 設定値の名前を指定する文字列値。`smtpHost` 設定値を設定する場合は、`smtpHost` を指定します。
   * 設定値の値を指定する文字列値。`smtpHost` 設定値を設定する場合は、SMTP サーバーの名前を指定する文字列値を指定します。

   >[!NOTE]
   >
   >このセクションで紹介する EncryptDocument サービスに設定されたすべての設定値を確認するには、Java コードの例を参照してください（[クイックスタート：Java API を使用したメールエンドポイントの追加](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-email-endpoint-using-the-java-api)）。

1. 入力パラメーター値を定義します。

   入力パラメーター値を定義するには、`CreateEndpointInfo` オブジェクトの `setInputParameterMapping` メソッドを呼び出し、次の値を渡します。

   * 入力パラメーターの名前を指定する文字列値。例えば、EncryptDocument サービスの入力パラメーターの名前は `InDoc` です。
   * 入力パラメーターのデータタイプを指定する文字列値。例えば、`InDoc` 入力パラメーターのデータタイプは `com.adobe.idp.Document` です。
   * マッピングタイプを指定する文字列値です。 例えば、`variable` を指定できます。
   * マッピングタイプの値を指定する文字列値。例えば、ファイルパターンとして、&amp;ast;.pdf を指定できます。

   >[!NOTE]
   >
   >定義する入力パラメーター値ごとに `setInputParameterMapping` メソッドを呼び出します。EncryptDocument プロセスには入力パラメーターが 1 つしかないので、このメソッドを 1 度呼び出す必要があります。

1. 出力パラメーター値を定義します。

   出力パラメーター値を定義するには、`CreateEndpointInfo` オブジェクトの `setOutputParameterMapping` メソッドを呼び出し、次の値を渡します。

   * 出力パラメーターの名前を指定する文字列値。例えば、EncryptDocument サービスの出力パラメーターの名前は `SecuredDoc` です。
   * 出力パラメーターのデータタイプを指定する文字列値。例えば、`SecuredDoc` 出力パラメーターのデータタイプは `com.adobe.idp.Document` です。
   * マッピングタイプを指定する文字列値です。 例えば、`%F.pdf` を指定できます。

1. 電子メールエンドポイントを作成します。

   エンドポイントを作成するには、`EndpointRegistryClient` オブジェクトの `createEndpoint` メソッドを呼び出し、`CreateEndpointInfo` オブジェクトを渡します。このメソッドは、メールエンドポイントを表す `Endpoint` オブジェクトを返します。

1. エンドポイントを有効にします。

   エンドポイントを有効にするには、`EndpointRegistryClient` オブジェクトの `enable` メソッドを呼び出し、`createEndpoint` メソッドによって返された `Endpoint` オブジェクトを渡します。

**関連トピック**

[手順の概要](programmatically-endpoints.md#summary-of-steps)

[QuickStart：Java API を使用した監視フォルダーエンドポイントの追加](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルの組み込み](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### メール設定値の定数ファイル {#email-configuration-values-constant-file}

「[クイックスタート：Java API を使用した電子メールエンドポイントの追加](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-email-endpoint-using-the-java-api)」では、クイックスタートをコンパイルするために Java プロジェクトの一部である必要がある定数ファイルを使用します。この定数ファイルは、電子メールエンドポイントを追加する際に設定する必要がある設定値を表します。 次の Java コードは、定数ファイルを表しています。

```java
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
>JEE 上の AEM Forms で LiveCycle Remoting API は非推奨になりました。

AEM Forms Java API を使用して、プログラムによってリモートエンドポイントをサービスに追加できます。リモートエンドポイントを追加すると、リモート処理を使用してFlexアプリケーションからサービスを呼び出すことができます。 （[（AEM Forms では廃止）AEM Forms Remoting を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)を参照してください）。

リモートエンドポイントをプログラムでサービスに追加する場合は、次の *EncryptDocument* という短時間のみ有効なプロセスを考えてみてください。

![ar_ar_encryptdocumentprocess](assets/ar_ar_encryptdocumentprocess.png)

このプロセスは、入力値として非暗号化 PDF ドキュメントを受け取り、暗号化サービスの`EncryptPDFUsingPassword`操作に非暗号化 PDF ドキュメントを渡します。PDF ドキュメントをパスワードで暗号化し、パスワードで暗号化された PDF ドキュメントはこのプロセスの出力値です。入力値（保護されていないPDFドキュメント）の名前は `InDoc`、データタイプは `com.adobe.idp.Document` です。出力値（パスワードで暗号化された PDF ドキュメント）の名前は `SecuredDoc`、データタイプは `com.adobe.idp.Document` です。

サービスにリモートエンドポイントを追加する方法を示すために、このセクションでは EncryptDocument という名前のサービスにリモートエンドポイントを追加します。

>[!NOTE]
>
>Web サービスを使用してリモートエンドポイントを追加することはできません。

### 手順の概要 {#summary_of_steps-4}

エンドポイントをサービスから削除するには、以下のタスクを実行します。

1. プロジェクトファイルを含めます。
1. `EndpointRegistryClient` オブジェクトを作成します。
1. リモートエンドポイントの属性を設定します。
1. リモートエンドポイントを作成します。
1. エンドポイントを有効にします。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、必ずプロキシファイルを含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar（AEM Forms が JBoss Application Server にデプロイされている場合に必要）
* jbossall-client.jar（AEM Forms が JBoss Application Server にデプロイされている場合に必要）

これらの JAR ファイルの場所については、[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。

**EndpointRegistry クライアントオブジェクトを作成する**

リモートエンドポイントをプログラムで追加するには、`EndpointRegistryClient` オブジェクトを作成する必要があります。

**リモートエンドポイント属性の設定**

サービスのリモートエンドポイントを作成するには、次の値を指定します。

* **コネクター識別子の値**：作成するエンドポイントのタイプを指定します。リモートエンドポイントを作成するには、`Remoting` を指定します。
* **説明**：エンドポイントの説明を指定します。
* **名前**：エンドポイントの名称を指定します。
* **サービス識別子の値**：エンドポイントが属するサービスを指定します。例えば、このセクションで紹介するプロセスにリモートエンドポイントを追加する場合（プロセスは Workbench 内で起動されるとサービスになります）、`EncryptDocument` を指定します。
* **操作名**：エンドポイントを使用して呼び出される操作の名前を指定します。リモートエンドポイントを作成する場合は、ワイルドカード文字（&amp;ast;）を指定します。

**リモートエンドポイントの作成**

リモートエンドポイント属性を設定した後、サービスのリモートエンドポイントを作成できます。

**エンドポイントを有効にする**

新しいエンドポイントを作成したら、そのエンドポイントを有効にする必要があります。リモートエンドポイントが有効な場合、Flex クライアントがサービスを呼び出すことができます。

**関連トピック**

[Java API を使用したリモートエンドポイントの追加](programmatically-endpoints.md#add-a-remoting-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API を使用したリモートエンドポイントの追加 {#add-a-remoting-endpoint-using-the-java-api}

Java API を使用してリモートエンドポイントを追加します。

1. プロジェクトファイルを含めます。

   adobe-livecycle-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. EndpointRegistry クライアントオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して `EndpointRegistryClient` オブジェクトを作成し、`ServiceClientFactory` オブジェクトを渡します。

1. リモートエンドポイントの属性を設定します。

   * コンストラクターを使用して `CreateEndpointInfo` オブジェクトを作成します。
   * `CreateEndpointInfo` オブジェクトの `setConnectorId` メソッドを呼び出し、文字列値 `Remoting` を渡すことによって、コネクタ識別子の値を指定します。
   * `CreateEndpointInfo` オブジェクトの `setDescription` メソッドを呼び出し、エンドポイントを説明する文字列値を渡すことによって、エンドポイントの説明を指定します。
   * `CreateEndpointInfo` オブジェクトの `setName` メソッドを呼び出し、名前を指定する文字列値を渡すことによって、エンドポイントの名前を指定します。
   * `CreateEndpointInfo` オブジェクトの `setServiceId` メソッドを呼び出し、サービス名を指定する文字列値を渡すことによって、エンドポイントが属するサービスを指定します。
   * `CreateEndpointInfo` オブジェクトの `setOperationName` メソッドを呼び出し、操作名を指定する文字列値を渡すことによって、操作を指定します。リモートエンドポイントの場合は、ワイルドカード文字（&amp;ast;）を指定します。

1. リモートエンドポイントを作成します。

   `EndpointRegistryClient` オブジェクトの `createEndpoint` メソッドを呼び出し、`CreateEndpointInfo` オブジェクトを渡すことによって、エンドポイントを作成します。このメソッドは、新しいリモートエンドポイントを表す `Endpoint` オブジェクトを返します。

1. エンドポイントを有効にします。

   `EndpointRegistryClient` オブジェクトの `enable` メソッドを呼び出し、`createEndpoint` メソッドによって返された `Endpoint` オブジェクトを渡すことによって、エンドポイントを有効にします。

**関連トピック**

[手順の概要](programmatically-endpoints.md#summary-of-steps)

[クイックスタート：Java API を使用してリモートエンドポイントを追加する](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-remoting-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## TaskManager エンドポイントの追加 {#adding-taskmanager-endpoints}

AEM Forms Java API を使用して、プログラムによって TaskManager エンドポイントをサービスに追加できます。TaskManager エンドポイントをサービスに追加することで、Workspace ユーザーがサービスを呼び出せるようにします。つまり、Workspace で作業しているユーザーが、対応する TaskManager エンドポイントを持つプロセスを呼び出せるようになります。

>[!NOTE]
>
>Web サービスを使用して TaskManager エンドポイントを追加することはできません。

### 手順の概要 {#summary_of_steps-5}

TaskManager エンドポイントをサービスに追加するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. `EndpointRegistryClient` オブジェクトを作成します。
1. エンドポイントのカテゴリを作成します。
1. TaskManager エンドポイント属性を設定します。
1. TaskManager エンドポイントを作成します。
1. エンドポイントを有効にします。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、必ずプロキシファイルを含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar（AEM Forms が JBoss Application Server にデプロイされている場合に必要）
* jbossall-client.jar（AEM Forms が JBoss Application Server にデプロイされている場合に必要）

これらの JAR ファイルの場所について詳しくは、[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。

**EndpointRegistry Client オブジェクトの作成**

TaskManager エンドポイントをプログラムによって追加するには、`EndpointRegistryClient` オブジェクトを事前に作成しておく必要があります。

**エンドポイントのカテゴリの作成**

カテゴリは、Workspace 内のサービスを整理するために使用されます。つまり、Workspace ユーザーは、Workspace 内のカテゴリを選択することで、TaskManager エンドポイントを持つサービスを呼び出すことができます。TaskManager エンドポイントを作成する際に、既存のカテゴリを参照するか、新しいカテゴリをプログラムで作成することができます。

>[!NOTE]
>
>このセクションでは、TaskManager エンドポイントをサービスに追加する際に、新しいカテゴリを作成します。

**TaskManager エンドポイント属性の設定**

サービスの TaskManager エンドポイントを作成するには、次の値を指定します。

* **コネクタ識別子**：作成するエンドポイントのタイプを指定します。TaskManager エンドポイントを作成するには、`TaskManagerConnector` を指定します。
* **説明**：エンドポイントの説明を指定します。
* **名前**：エンドポイントの名前を指定します。
* **サービス識別子**：エンドポイントが属するサービスを指定します。
* **カテゴリ**：TaskManager エンドポイントに関連付けられるカテゴリ識別子の値を指定します。
* **操作名**：通常、Workbench で作成されたプロセスから生成されるサービスの TaskManager エンドポイントを作成する場合、操作の名前は `invoke` です。

**TaskManager エンドポイントの作成**

TaskManager エンドポイントの属性を設定したら、サービスの TaskManager エンドポイントを作成できます。

**エンドポイントを有効にする**

新しいエンドポイントを作成したら、そのエンドポイントを有効にする必要があります。エンドポイントを有効にしたら、Workspace 内からサービスを呼び出すために使用できます。エンドポイントを有効にすると、管理コンソール内で表示できます。

**関連トピック**

[Java API を使用した TaskManager エンドポイントの追加](programmatically-endpoints.md#add-a-taskmanager-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API を使用した TaskManager エンドポイントの追加 {#add-a-taskmanager-endpoint-using-the-java-api}

Java API を使用して TaskManager エンドポイントを追加します。

1. プロジェクトファイルを含めます。

   adobe-livecycle-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. EndpointRegistry クライアントオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して `ServiceClientFactory` オブジェクトを渡すことによって、`EndpointRegistryClient` オブジェクトを作成します。

1. エンドポイントのカテゴリを作成します。

   * コンストラクターを使用して、次の文字列値を渡すことによって、`CreateEndpointCategoryInfo` オブジェクトを作成します。

      * カテゴリの識別子の値を指定する文字列値
      * カテゴリの説明を指定する文字列値
   * カテゴリを作成するには、`EndpointRegistryClient` オブジェクトの `createEndpointCategory` メソッドを呼び出し、`CreateEndpointCategoryInfo` オブジェクトを渡します。このメソッドは、新しいカテゴリを表す `EndpointCategory` オブジェクトを返します。


1. TaskManager エンドポイント属性を設定します。

   * コンストラクターを使用して `CreateEndpointInfo` オブジェクトを作成します。
   * コネクタ識別子の値を指定するには、`CreateEndpointInfo` オブジェクトの `setConnectorId` メソッドを呼び出し、文字列値 `TaskManagerConnector` を渡します。
   * エンドポイントの説明を指定するには、`CreateEndpointInfo` オブジェクトの `setDescription` メソッドを呼び出し、エンドポイントを説明する文字列値を渡します。
   * エンドポイントの名前を指定するには、`CreateEndpointInfo` オブジェクトの `setName` メソッドを呼び出し、名前を指定する文字列を渡します。
   * エンドポイントが属するサービスを指定するには、`CreateEndpointInfo` オブジェクトの `setServiceId` メソッドを呼び出し、サービス名を指定する文字列値を渡します。
   * エンドポイントが属するカテゴリを指定するには、`CreateEndpointInfo` オブジェクトの `setCategoryId` メソッドを呼び出し、カテゴリ識別子の値を指定する文字列値を渡します。`EndpointCategory` オブジェクトの `getId` メソッドを呼び出すと、このカテゴリの識別子の値を取得できます。
   * 呼び出す操作を指定するには、`CreateEndpointInfo` オブジェクトの `setOperationName` メソッドを呼び出し、操作名を指定する文字列値を渡します。通常、Workbench で作成したプロセスから派生するサービスの `TaskManager` エンドポイントで、操作の名前は `invoke` です。

1. TaskManager エンドポイントを作成します。

   エンドポイントを作成するには、`EndpointRegistryClient` オブジェクトの `createEndpoint` メソッドを呼び出し、`CreateEndpointInfo` オブジェクトを渡します。 このメソッドは、新しい TaskManager エンドポイントを表す `Endpoint` オブジェクトを返します。

1. エンドポイントを有効にします。

   エンドポイントを有効にするには、`EndpointRegistryClient` オブジェクトの `enable` メソッドを呼び出し、`createEndpoint` メソッドによって返された `Endpoint` オブジェクトを渡します。

**関連トピック**

[手順の概要](programmatically-endpoints.md#summary-of-steps)

[クイックスタート：Java API を使用した TaskManager エンドポイントの追加](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-taskmanager-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## エンドポイントの変更 {#modifying-endpoints}

AEM Forms Java API を使用して、既存のエンドポイントをプログラムで変更できます。 エンドポイントを変更すると、エンドポイントの動作を変更できます。 例えば、監視フォルダーとして使用するフォルダーを指定する監視フォルダーエンドポイントがあるとします。 監視フォルダーエンドポイントに属する設定値をプログラムで変更することで、別のフォルダーが監視フォルダーとして機能するようになります。 監視フォルダーエンドポイントに属する設定値について詳しくは、[監視フォルダーエンドポイントの追加](programmatically-endpoints.md#adding-watched-folder-endpoints)を参照してください。

このセクションでは、エンドポイントを変更する方法を示すために、監視フォルダーとして動作するフォルダーを変更して、監視フォルダーエンドポイントを変更します。

>[!NOTE]
>
>Web サービスを使用してエンドポイントを変更することはできません。

### 手順の概要 {#summary_of_steps-6}

エンドポイントを変更するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. `EndpointRegistryClient` オブジェクトを作成します。
1. エンドポイントを取得します。
1. 新しい設定値を指定します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、必ずプロキシファイルを含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar（AEM Forms が JBoss Application Server にデプロイされている場合に必要）
* jbossall-client.jar（AEM Forms が JBoss Application Server にデプロイされている場合に必要）

これらの JAR ファイルの場所については、[AEM Forms Java ライブラリファイルの組み込み](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。

**EndpointRegistry クライアントオブジェクトの作成**

エンドポイントをプログラムで変更するには、`EndpointRegistryClient` オブジェクトを作成する必要があります。

**変更するエンドポイントの取得**

エンドポイントを変更する前に、エンドポイントを取得する必要があります。 エンドポイントを取得するには、エンドポイントにアクセスできるユーザーとして接続する必要があります。 管理者として接続することをお勧めします。 （[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照）。

エンドポイントのリストを取得して、エンドポイントを取得できます。 その後、リストを繰り返し処理し、削除する特定のエンドポイントを検索できます。 例えば、エンドポイントに対応するサービスとエンドポイントのタイプを指定して、エンドポイントを特定できます。 エンドポイントを見つけたら、変更できます。

**新しい設定値を指定する**

エンドポイントを変更する場合は、新しい設定値を指定します。 例えば、監視フォルダーエンドポイントを変更するには、変更するエンドポイントだけでなく、すべての監視フォルダーエンドポイント設定値をリセットします。 監視フォルダーエンドポイントに属する設定値について詳しくは、 [監視フォルダーエンドポイントの追加](programmatically-endpoints.md#adding-watched-folder-endpoints)を参照してください。

>[!NOTE]
>
>電子メールエンドポイントに属する設定値について詳しくは、 [電子メールエンドポイントの追加](programmatically-endpoints.md#adding-email-endpoints)を参照してください。

>[!NOTE]
>
>エンドポイントによって呼び出されたサービスは変更できません。 サービスを変更しようとすると、例外が発生します。 特定のエンドポイントに関連付けられているサービスを変更するには、エンドポイントを削除し、新しく作成します。 （ [エンドポイントの削除](programmatically-endpoints.md#removing-endpoints)を参照してください）。

**関連トピック**

[Java API を使用したエンドポイントの変更](programmatically-endpoints.md#modifying-an-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API を使用したエンドポイントの変更 {#modifying-an-endpoint-using-the-java-api}

Java API を使用してエンドポイントを変更します。

1. プロジェクトファイルを含めます。

   adobe-livecycle-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. EndpointRegistry クライアントオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して `EndpointRegistryClient` オブジェクトを渡すことによって、 `ServiceClientFactory` オブジェクトを作成します。

1. 変更するエンドポイントを取得します。

   *  `EndpointRegistryClient` オブジェクトの `getEndpoints` メソッドを呼び出してフィルターとして動作する `PagingFilter` オブジェクトを渡し、現在のユーザー（接続プロパティで指定）がアクセスできるすべてのエンドポイントのリストを取得します。`(PagingFilter)null` 値を指定して、すべてのエンドポイントを返します。 このメソッドは、各要素が `Endpoint` オブジェクトである `java.util.List` オブジェクトを返します。 `PagingFilter` オブジェクトの情報は、[AEM Forms API リファレンス](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ja)を参照してください。
   * `java.util.List` オブジェクトを反復処理して、エンドポイントがあるかどうかを判断します。 エンドポイントが存在する場合、各要素は `EndPoint` インスタンスです。
   *  `EndPoint` オブジェクトの `getServiceId` メソッドを呼び出して、エンドポイントに対応するサービスを判断します。このメソッドは、サービス名を指定する文字列値を返します。
   * `EndPoint` オブジェクトの `getConnectorId` メソッドを呼び出して、エンドポイントのタイプを決定します。このメソッドは、エンドポイントのタイプを指定する文字列値を返します。 例えば、エンドポイントが監視フォルダーエンドポイントの場合、このメソッドは `WatchedFolder` を返します。

1. 新しい設定値を指定します。

   * コンストラクターを使用して `ModifyEndpointInfo` オブジェクトを作成します。
   * 設定する設定値ごとに、 `ModifyEndpointInfo` オブジェクトの `setConfigParameterAsText` メソッドを呼び出します。 例えば、URL 設定値を設定するには、`ModifyEndpointInfo` オブジェクトの `setConfigParameterAsText` メソッドを呼び出して、次の値を渡します。

      * 設定値の名前を指定する文字列値。例えば、 `url` 構成値を設定するには、`url` を指定します。
      * 設定値の値を指定する文字列値。`url` 設定値の値を定義するには、監視フォルダーの場所を指定します。
   * `EndpointRegistryClient` オブジェクトの `modifyEndpoint` メソッドを呼び出し、`ModifyEndpointInfo` オブジェクトを渡します。


**関連トピック**

[手順の概要](programmatically-endpoints.md#summary-of-steps)

[クイックスタート：Java API を使用したエンドポイントの変更](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-modifying-an-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## エンドポイントの削除 {#removing-endpoints}

AEM Forms Java API を使用して、プログラムによってエンドポイントをサービスから削除できます。 エンドポイントを削除すると、エンドポイントが有効な呼び出しメソッドを使用してもサービスを呼び出せなくなります。 例えば、サービスから SOAP エンドポイントを削除すると、SOAP モードを使用してもサービスを呼び出せません。

このセクションでは、サービスからエンドポイントを削除する方法を示すために、EJB エンドポイントを *EncryptDocument* という名前のサービスから削除します。

>[!NOTE]
>
>Web サービスを使用してエンドポイントを削除することはできません。

### 手順の概要 {#summary_of_steps-7}

エンドポイントをサービスから削除するには、以下のタスクを実行します。

1. プロジェクトファイルを含めます。
1. `EndpointRegistryClient` オブジェクトを作成します。
1. エンドポイントを取得します。
1. エンドポイントを削除します。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、必ずプロキシファイルを含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar（AEM Forms が JBoss Application Server にデプロイされている場合に必要）
* jbossall-client.jar（AEM Forms が JBoss Application Server にデプロイされている場合に必要）

これらの JAR ファイルの場所については、[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。

**EndpointRegistry クライアントオブジェクトの作成**

プログラムによってエンドポイントを削除するには、`EndpointRegistryClient` オブジェクトを作成する必要があります。

**削除するエンドポイントを取得する**

エンドポイントを削除する前に、エンドポイントを取得する必要があります。 エンドポイントを取得するには、エンドポイントにアクセスできるユーザーとして接続する必要があります。 管理者として接続することをお勧めします。 （[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照）。

エンドポイントのリストを取得して、エンドポイントを取得できます。 その後、リストを繰り返し処理し、削除する特定のエンドポイントを検索できます。 例えば、エンドポイントに対応するサービスとエンドポイントのタイプを指定して、エンドポイントを特定できます。 エンドポイントを見つけたら、そのエンドポイントを削除できます。

**エンドポイントを削除**

新しいエンドポイントを作成したら、そのエンドポイントを有効にする必要があります。エンドポイントが有効であれば、サービスの呼び出しに使用することができます。エンドポイントを有効にすると、管理コンソール内で表示できます。

**関連トピック**

[Java API を使用したエンドポイントの削除](programmatically-endpoints.md#removing-an-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API を使用したエンドポイントの削除 {#removing-an-endpoint-using-the-java-api}

Java API を使用してエンドポイントを削除します。

1. プロジェクトファイルを含めます。

   adobe-livecycle-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. EndpointRegistry クライアントオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * `EndpointRegistryClient` オブジェクトを作成するには、コンストラクターを使用して `ServiceClientFactory` オブジェクトを渡します。

1. 削除するエンドポイントを取得します。

   * `EndpointRegistryClient` オブジェクトの `getEndpoints` メソッドを呼び出してフィルターとして動作する `PagingFilter` オブジェクトを渡し、現在のユーザー（接続プロパティで指定）がアクセス権を持つすべてのエンドポイントのリストを取得します。`(PagingFilter)null` を渡して、すべてのエンドポイントを返します。このメソッドは、各要素が `Endpoint` オブジェクトである `java.util.List` オブジェクトを返します。
   * `java.util.List` オブジェクトを反復処理して、エンドポイントがあるかどうかを判断します。エンドポイントが存在する場合、各要素は `EndPoint` インスタンスです。
   * `EndPoint` オブジェクトの `getServiceId` メソッドを呼び出して、エンドポイントに対応するサービスを特定します。このメソッドは、サービス名を指定する文字列値を返します。
   * `EndPoint` オブジェクトの `getConnectorId` メソッドを呼び出して、エンドポイントのタイプを特定します。このメソッドは、エンドポイントのタイプを指定する文字列値を返します。 例えば、エンドポイントが EJB エンドポイントである場合、このメソッドは `EJB` を返します。

1. エンドポイントを削除します。

   `EndpointRegistryClient` オブジェクトの `remove` メソッドを呼び出し、削除するエンドポイントを表す `EndPoint` オブジェクトを渡すことで、エンドポイントを削除することができます。

**関連トピック**

[手順の概要](programmatically-endpoints.md#summary-of-steps)

[QuickStart：Java API を使用したエンドポイントの削除](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-removing-an-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## エンドポイントコネクタの情報を取得する {#retrieving-endpoint-connector-information}

AEM Forms APIを使用して、エンドポイントコネクターの情報をプログラムで取得することができます。コネクターを使用すると、エンドポイントで様々な呼び出し方法を用いてサービスを呼び出すことができます。例えば、監視フォルダーコネクターを使用すると、エンドポイントで監視フォルダーを使用したサービスを呼び出すことができます。エンドポイントコネクターの情報をプログラムで取得することで、どの設定値が必須で、どの設定値が任意であるかなど、コネクターに関連する設定値を取得することができます。

エンドポイントコネクターの情報を取得する方法を説明するために、ここでは監視フォルダーコネクターの情報を取得します（[監視フォルダーエンドポイントの追加](programmatically-endpoints.md#adding-watched-folder-endpoints)を参照）。

>[!NOTE]
>
>Web サービスを使用してエンドポイントの情報を取得することはできません。

>[!NOTE]
>
>このトピックでは、`ConnectorRegistryClient` APIを使用して、エンドポイントコネクターの情報を取得します（[AEM Forms API リファレンス](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ja)を参照）。

### 手順の概要 {#summary_of_steps-8}

エンドポイントコネクターの情報を取得するには、以下のタスクを実行します。

1. プロジェクトファイルを含めます。
1. `ConnectorRegistryClient` オブジェクトの作成。
1. コネクタタイプを指定します。
1. 設定値を取得します。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、必ずプロキシファイルを含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar（AEM Forms が JBoss Application Server にデプロイされている場合に必要）
* jbossall-client.jar（AEM Forms が JBoss Application Server にデプロイされている場合に必要）

AEM Forms が JBoss 以外のサポート対象の J2EE アプリケーションサーバーにデプロイされている場合は、adobe-utilities.jar ファイルと jbossall-client.jar ファイルを、AEM Forms がデプロイされている J2EE アプリケーションサーバーに固有の JAR ファイルに置き換えます。すべての AEM Forms JAR ファイルの場所については、[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。

**ConnectorRegistry クライアントオブジェクトの作成**

エンドポイントコネクタの情報をプログラムで取得するには、`ConnectorRegistryClient` オブジェクトを作成します。

**コネクタタイプを指定**

情報を取得するコネクターのタイプを指定します。以下のタイプのコネクターが存在します。

* **EJB**：クライアントアプリケーションが EJB モードを使用してサービスを呼び出せるようにします。
* **SOAP**：クライアントアプリケーションが SOAP モードを使用してサービスを呼び出せるようにします。
* **監視フォルダー**：監視フォルダーがサービスを呼び出せるようにします。
* **メール**：メールメッセージでサービスを呼び出せるようにします。
* **リモート**：Flexクライアントアプリケーションがサービスを呼び出せるようにします。
* **TaskManagerConnector**：Workspace ユーザーが Workspace でサービスを呼び出せるようにします。

**設定値の取得**

コネクタータイプを指定すると、サポートされている設定値など、コネクターに関する情報を取得することができます。例えば、任意のコネクタについて、どの設定値が必須で、どの設定値がオプションであるかを決定することができます。

**関連トピック**

[Java API を使用したエンドポイントコネクター情報の取得](programmatically-endpoints.md#retrieve-endpoint-connector-information-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API を使用したエンドポイントコネクター情報の取得 {#retrieve-endpoint-connector-information-using-the-java-api}

Java API を使用して、エンドポイントコネクターの情報を取得します。

1. プロジェクトファイルを含めます。

   adobe-livecycle-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. ConnectorRegistry クライアントオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して `ServiceClientFactory` オブジェクトを渡し、`ConnectorRegistryClient` オブジェクトを作成します。

1. コネクタタイプを指定します。

   `ConnectorRegistryClient` オブジェクトの `getEndpointDefinition` メソッドを呼び出して、コネクタータイプを指定する文字列値を渡し、コネクタータイプを指定します。例えば、監視フォルダーのコネクタータイプを指定するには、文字列値 `WatchedFolder` を渡します。このメソッドは、コネクタタイプに対応する `Endpoint` オブジェクトを返します。

1. 設定値を取得します。

   * `Endpoint` オブジェクトの `getConfigParameters` メソッドを呼び出して、このエンドポイント内で関連付けられている設定値を取得します。このメソッドは、 `ConfigParameter` オブジェクトの配列を返します。
   * 配列内の各要素を取得して、各設定値に関する情報を取得します。 各要素は `ConfigParameter` オブジェクトです。 例えば、設定値が必須かオプションかを、`ConfigParameter` オブジェクトの `isRequired` メソッドを呼び出して特定できます。設定値が必要な場合、このメソッドは `true` を返します。

**関連トピック**

[手順の概要](programmatically-endpoints.md#summary-of-steps)

[クイックスタート：Java API を使用したエンドポイントコネクタ情報の取得](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-retrieving-endpoint-connector-information-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
