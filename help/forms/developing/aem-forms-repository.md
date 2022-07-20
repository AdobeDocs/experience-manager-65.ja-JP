---
title: AEM Forms リポジトリの操作
seo-title: Working with AEM Forms Repository
description: AEM Forms リポジトリを管理して、Java API や web サービス API によるフォルダー作成や、リソースの書き込み、リスト化、読み取り、更新および検索をおこないます。さらに、リソースの関係の作成方法や、リソースのロックと削除の方法についても説明します。
seo-description: Manage AEM Forms repository to create folders, write, list, read, update resources, and search resources using the Java API and Web Service API. In addition, learn how to create resource relationships, lock and delete resources.
uuid: 6ead49f9-ca0d-4ee4-86a6-0a9ced6ec4f8
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d2c95881-6c02-4e34-85af-84607df54287
role: Developer
exl-id: a07e51ca-fea0-4719-8071-1b7e805de2ae
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '9117'
ht-degree: 100%

---

# AEM Forms リポジトリの操作 {#working-with-aem-forms-repository}

**このドキュメントのサンプルと例は、JEE 環境の AEM Forms のみを対象としています。**

**リポジトリサービスについて**

リポジトリサービスは、リソースを保存および管理するためのサービスを AEM Forms に提供します。開発者が *AEM Forms* アプリケーションを作成したら、アセットをファイルシステムではなくリポジトリにデプロイできます。アセットには、XML フォーム、PDF フォーム（Acrobat フォームを含む）、フォームのフラグメント、画像、プロファイル、ポリシー、SWF ファイル、DDX ファイル、XML スキーマ、WSDL ファイルおよびテストデータなど、任意のタイプの販促物が該当します。

例えば、次に示す *Applications/FormsApplication* という名前の Forms アプリケーションを考えてみましょう。

![ww_ww_formrepository](assets/ww_ww_formrepository.png)

FormsFolder に Loan.xdp という名前のファイルがあることを確認してください。このフォームデザインにアクセスするには、完全パス（バージョンを含む）である `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp` を指定します。

>[!NOTE]
>
>Workbench を使用して Forms アプリケーションを作成する方法について詳しくは、[Workbench ヘルプ](https://www.adobe.com/go/learn_aemforms_workbench_63_jp)を参照してください。

AEM Forms リポジトリにあるリソースへのパスは次のとおりです。

`Applications/Application-name/Application-version/Folder.../Filename`

URI 値の一例を以下に示します。

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

>[!NOTE]
>
>Web ブラウザーを使用して AEM Forms リポジトリを参照できます。リポジトリを参照するには、web ブラウザーに URL `https://[server name]:[server port]/repository` を入力します。Web ブラウザーを使用して、「AEM Forms リポジトリの操作」セクションに関連するクイックスタートの結果を確認できます。例えば、AEM Forms リポジトリにコンテンツを追加したら、そのコンテンツを web ブラウザーで表示できます（詳しくは、[クイックスタート（SOAP モード）：Java API を使用したリソースの書き込み](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)を参照してください）。

リポジトリ API には、リポジトリへの情報の保存や取得に使用できる多数の操作が用意されています。例えば、リソースのリストを取得したり、アプリケーションの処理の一環としてリソースが必要な場合にリポジトリに保存されている特定のリソースを取得したりできます。

>[!NOTE]
>
>リポジトリ API は、コンテンツサービス（非推奨）の操作には使用できません。コンテンツサービス（非推奨）を操作するには、Document Management API を使用します。

リポジトリサービス API を使用すると、次のタスクを実行できます。

* フォルダーの作成。詳しくは、[フォルダーの作成](aem-forms-repository.md#creating-folders)を参照してください。
* リソースとそのプロパティの書き込み。詳しくは、[リソースの書き込み](aem-forms-repository.md#writing-resources)を参照してください。
* 特定のコレクション内のリソースまたは他のリソースに関連するリソースのリスト化。詳しくは、[リソースのリスト化](aem-forms-repository.md#listing-resources)を参照してください。
* リソースとそのプロパティの読み取り。詳しくは、[リソースの読み取り](aem-forms-repository.md#reading-resources)を参照してください。
* リソースとそのプロパティの更新。詳しくは、[リソースの更新](aem-forms-repository.md#updating-resources)を参照してください。
* リソースの検索。履歴、関連リソース、プロパティなども指定できます。詳しくは、[リソースの検索](aem-forms-repository.md#searching-for-resources)を参照してください。
* リソース間の関係の指定。詳しくは、[リソースの関係の作成](aem-forms-repository.md#creating-resource-relationships)を参照してください。
* リソースアクセス制御の管理。具体的には、リソースのロックとロック解除や、アクセス制御リスト（ACL）の読み取りと書き込みなどです。詳しくは、[リソースのロック](aem-forms-repository.md#locking-resources)を参照してください。
* リソースとそのプロパティの削除。詳しくは、[リソースの削除](aem-forms-repository.md#deleting-resources)を参照してください。

>[!NOTE]
>
>Repository API では、ECM リポジトリを使用して、リソースアクセス制御の管理、リソースの検索、リソースの関係の指定を行うことはできません。

>[!NOTE]
>
>暗号化された PDF をリポジトリに書き込んだ場合は、自動関係抽出機能は使用できません。ただし、暗号化された PDF をリポジトリに保存し、後で取得することは可能です。取得側は、リポジトリから取得した後に PDF を復号できます。

>[!NOTE]
>
>リポジトリサービスについて詳しくは、[AEM Forms サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

## フォルダーの作成 {#creating-folders}

フォルダー（リソースコレクション）は、整理されたグループにオブジェクト（ファイルまたはリソース）を保存するために使用します。フォルダーには、リソースと他のフォルダー（サブフォルダーとも呼ばれます）を含めることができます。リソースは一度に 1 つのフォルダーにのみ保存できます。

ファイルはフォルダーからアクセス制御リスト (ACL) を継承し、サブフォルダーは親フォルダーから ACL を継承します。したがって、子フォルダーを作成するには、親フォルダーが存在する必要があります。IDE では、ファイル単位ではなく、フォルダー単位でのみやり取りできます。フォルダーのバージョンを設定することはできず、また設定する必要もありません。1 つのフォルダーには、データ自体は含まれていません。データを含むリソースのコンテナにすぎません。デフォルトの ACL はシステムレベルの権限です。すなわち、特定のフォルダに対する権限が付与されるまで、ユーザーはシステムレベルの権限（読み取り、書き込み、トラバース、ACL の管理）を持つ必要があります。ACL は IDE でのみ機能します。

>[!NOTE]
>
>リポジトリサービスについて詳しくは、 [AEM Forms サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary-of-steps}

フォルダーを作成するには、以下の手順に従います。

1. プロジェクトファイルを含めます。
1. サービスクライアントを作成します。
1. フォルダーを作成します。
1. フォルダーをリポジトリに書き込みます。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを含めます。

**サービスクライアントを作成**

プログラムによってリソースコレクションを作成する前に、接続を確立し、資格情報を入力する必要があります。これは、サービスクライアントを作成することで実行されます。

**フォルダーを作成**

リポジトリサービスメソッドを呼び出して、リソースコレクションを作成し、UUID、フォルダー名、説明などの識別情報をリソースコレクションに入力します。

**フォルダーをリポジトリに書き込む**

リポジトリサービスメソッドを呼び出して、ターゲットフォルダーの URI を指定し、リソースコレクションを書き込みます。

**関連トピック**

[Java API を使用してフォルダーを作成](aem-forms-repository.md#create-folders-using-the-java-api)

[Web サービス API を使用してフォルダーを作成](aem-forms-repository.md#create-folders-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Repository サービス API クイックスタート](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java API を使用してフォルダーを作成 {#create-folders-using-the-java-api}

リポジトリサービス API（Java）を使用してフォルダーを作成します。

1. プロジェクトファイルを含める

   Java プロジェクトのクラスパスにプロジェクトファイルを含めます。

1. サービスクライアントの作成

   コンストラクターを使用し、 `ServiceClientFactory` 接続プロパティを含むオブジェクトを渡して、`ResourceRepositoryClient` オブジェクトを作成します。

1. フォルダーを作成

   リソースコレクションを作成するには、まず `com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean` オブジェクトを作成する必要があります。

   `repositoryInfomodelFactoryBean` オブジェクトの `newResourceCollection` メソッドを呼び出し、次のパラメーターに渡します。

   * `com.adobe.repository.infomodel.Id` リソースに割り当てる UUID 識別情報。
   * `com.adobe.repository.infomodel.Lid` リソースに割り当てる UUID 識別情報。
   * `java.lang.String` リソースコレクションの名前を含む。例えば、`FormsFolder`のようになります。

   このメソッドは、 `com.adobe.repository.infomodel.bean.ResourceCollection` 新規フォルダーを表すオブジェクトを返します。

   フォルダーの説明を設定するには、 `setDescription` メソッドを使用して、次のパラメーターを渡します。

   * リソースのコレクションを説明する`String`。この例では、 `"test Folder"` が使用されています `.`


1. フォルダーをリポジトリに書き込む

   `ResourceRepositoryClient` オブジェクトの `writeResource` メソッドを呼び出して、フォルダーの URI と `ResourceCollection` オブジェクトに渡します。例えば、フォルダーの URI は次の値になります `/Applications/FormsApplication/1.0/`。

   メソッドは、新しく作成された `com.adobe.repository.infomodel.bean.Resource` オブジェクトのインスタンスを返します。例えば、`com.adobe.repository.infomodel.bean.Resource` オブジェクトの `getId` メソッドを呼び出して、新しいリソースの識別情報の値を取得することができます。

**関連トピック**

[フォルダーの作成](aem-forms-repository.md#creating-folders)

[クイックスタート（SOAP モード）：Java API を使用したフォルダーの作成](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-a-folder-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用してフォルダーを作成 {#create-folders-using-the-web-service-api}

リポジトリサービス API（web サービス）を使用してフォルダーを作成します。

1. プロジェクトファイルを含める

   * base64 を使用して、Repository WSDL を使用する Microsoft .NET クライアントアセンブリを作成します。
   * Microsoft .NET クライアントアセンブリを参照します。

1. サービスクライアントの作成

   Microsoft .NET クライアントアセンブリを使用して、デフォルトのコンストラクターを呼び出すことで `RepositoryServiceService` オブジェクトを作成します。ユーザー名とパスワードを含む `System.Net.NetworkCredential` オブジェクトを使用して `Credentials` プロパティを設定します。

1. フォルダーを作成

   `ResourceCollection` クラスのデフォルトのコンストラクターを使用し、次のパラメーターを渡すことで、フォルダーを作成します。

   * `Id` クラスのデフォルトのコンストラクターを呼び出し、`Resource` オブジェクトの `id` フィールドに割り当てることによって作成される `Id` オブジェクト。
   * `Lid` クラスのデフォルトのコンストラクターを呼び出し、`Resource` オブジェクトの `lid` フィールドに割り当てることによって作成される `Lid` オブジェクト。
   * `Resource` オブジェクトの `name` フィールドに割り当てられる、リソースコレクションの名前を含む文字列。この例で使用される名前は `"testfolder"` です。
   * `Resource` オブジェクトの `description` フィールドに割り当てられる、リソースコレクションの説明を含む文字列。この例で使用される説明は `"test folder"` です。

1. フォルダーをリポジトリに書き込む

   `RepositoryServiceService` オブジェクトの `writeResource` メソッドを呼び出し、以下のパラメーターを渡します。

   * フォルダーを作成するパス。
   * フォルダーを表す `ResourceCollection` オブジェクト。
   * 他の 2 つのパラメーターには `null` を渡します。

**関連トピック**

[フォルダーの作成](aem-forms-repository.md#creating-folders)

[Base64 エンコーディングを使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## リソースの書き込み {#writing-resources}

リポジトリ内の特定の場所にリソースを作成できます。未加工のファイルサイズによっては、データベース制限やセッションタイムアウトの影響を受けることがあります。デフォルトの設定では、ファイルのサイズは 25 MB に制限されます。最大ファイルサイズを増減するには、データベース設定を変更する必要があります。

リソースの書き込みは、リポジトリにデータを格納することと同じです。リソースをリポジトリに書き込むと、リポジトリエコシステム内のすべてのクライアントがそのリソースにアクセスできるようになります。XML スキーマ、XDP ファイル、XSD ファイルなどのリソースをリポジトリに書き込むと、そのコンテンツは MIME タイプにもとづいて解析されます。MIME タイプがサポートされている場合、パーサーは他のコンテンツとの暗黙の関係があるかどうかを判断します。例えば、カスケーディングスタイルシート（CSS）に共通の CSS を参照する相対 URL がある場合、その共通の CSS もリポジトリに送信する必要があります。2 つのリソース間の関係は、保留関係として 30 日間（調整不可）保存されます。30 日以内にリポジトリに共通の CSS を送信すると、関係が形成されます。

リソースを作成すると、アクセス制御リスト（ACL）が親フォルダーから継承されます。ルートフォルダーには、最初のリソースまたはフォルダーを作成するまでは、システムレベルの権限が割り当てられています。リソースまたはフォルダーを初めて作成した時点で、それらにデフォルトの ACL 権限が付与されます。

Repository サービス Java API または web サービス API を使用して、プログラムによってリソースを書き込むことができます。

>[!NOTE]
>
>Repository サービスについて詳しくは、[AEM Forms のサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary_of_steps-1}

リソースを書き込むには、以下の手順に従います。

1. プロジェクトファイルを含めます。
1. リポジトリサービスクライアントを作成します。
1. 読み取るリソースの URI を指定します。
1. リソースを読み取ります。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを含めます。

**サービスクライアントの作成**

プログラムによってリソースを読み取る前に、接続を確立し、資格情報を指定する必要があります。これは、サービスクライアントを作成することで実行されます。

**リソースに対するターゲットフォルダーの URI の指定**

読み取るリソースの URI を含む文字列を作成します。構文には、「/*path*/*folder*」のようにフォワードスラッシュが含まれます。

**リソースの作成**

Repository サービスメソッドを呼び出してリソースを作成し、UUID、リソース名、説明などの識別情報をリソースに設定します。

**リソースコンテンツの指定**

Repository サービスメソッドを呼び出してリソースコンテンツを作成し、そのコンテンツをリソースに保存します。

**ターゲットフォルダーへのリソースの書き込み**

Repository サービスメソッドを呼び出し、ターゲットフォルダーの URI を指定してリソースを書き込みます。

**関連トピック**

[Java API を使用したリソースの書き込み](aem-forms-repository.md#write-resources-using-the-java-api)

[Web サービス API を使用したリソースの書き込み](aem-forms-repository.md#write-resources-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Repository サービス API クイックスタート](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java API を使用したリソースの書き込み {#write-resources-using-the-java-api}

Repository サービス API（Java）を使用してリソースを書き込みます。

1. プロジェクトファイルを含める

   クライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. サービスクライアントの作成

   `ResourceRepositoryClient` オブジェクトを作成するには、コンストラクターを使用して、接続プロパティを含む `ServiceClientFactory` オブジェクトを渡します。

1. リソースに対するターゲットフォルダーの URI の指定

   リソースのターゲットフォルダーの URI を指定します。この場合、`testResource` という名前のリソースが `testFolder` という名前のフォルダーに保存されるので、そのフォルダーの URI は `"/testFolder"` となります。URI は `java.lang.String` オブジェクトとして保存されます。

1. リソースを作成

   リソースを作成するには、まず `com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean` オブジェクトを作成する必要があります。

   `com.adobe.repository.infomodel.bean.Resource` オブジェクトを作成する `RepositoryInfomodelFactoryBean` オブジェクトの `newResource` メソッドを呼び出します。この例では、以下のパラメーターが提供されます。

   * `Id` クラス用のデフォルトコンストラクターを呼び出して作成される `com.adobe.repository.infomodel.Id` オブジェクト。
   *  `Lid` クラス用のデフォルトコンストラクターを呼び出して作成される `com.adobe.repository.infomodel.Lid` オブジェクト。
   * `java.lang.String` はリソースのファイル名を含みます。

   リソースの説明を指定するには、`Resource` オブジェクトの `setDescription` メソッドを呼び出して、説明を含む文字列を渡します。この例では、説明は `"test resource"` です。

1. リソースコンテンツを指定

   リソースのコンテンツを作成するには、`RepositoryInfomodelFactoryBean` オブジェクトの `newResourceContent` メソッドを呼び出します。このメソッドは `com.adobe.repository.infomodel.bean.ResourceContent` オブジェクトを返します。`ResourceContent` オブジェクトにコンテンツを追加します。この例では、次のタスクを実行して実現されます。

   * `ResourceContent` オブジェクトの `setDataDocument` メソッドを呼び出して `com.adobe.idp.Document` オブジェクトを渡す
   * `ResourceContent` オブジェクトの `setSize` メソッドを呼び出して、`Document` オブジェクトをバイト単位で渡す

   `Resource` オブジェクトの `setContent` メソッドを呼び出して `ResourceContent` オブジェクをに渡すことで、コンテンツをリソースに追加します。詳しくは、[AEM Forms API リファレンス](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ja)を参照してください。

1. ターゲットフォルダにリソースを書き込む

   `ResourceRepositoryClient` オブジェクトの `writeResource` メソッドを呼び出して、フォルダーの URI と `Resource` オブジェクトに渡します。

**関連トピック**

[リソースの書き込み](aem-forms-repository.md#writing-resources)

[クイックスタート（SOAP モード）：Java API を使用したリソースの書き込み](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用したリソースの書き込み {#write-resources-using-the-web-service-api}

リポジトリーサービス API（web サービス）を使用してリソースを書き込みます。

1. プロジェクトファイルを含める

   * base64 を使用して、Repository WSDL を使用する Microsoft .NET クライアントアセンブリを作成します。
   * Microsoft .NET クライアントアセンブリを参照します。

1. サービスクライアントの作成

   Microsoft .NET クライアントアセンブリを使用して、デフォルトのコンストラクターを呼び出し、`RepositoryServiceService` オブジェクトを作成します。ユーザー名とパスワードを含む `System.Net.NetworkCredential` オブジェクトを使用して、`Credentials` プロパティを設定します。

1. リソースに対するターゲットフォルダーの URI の指定

   リソースのターゲットフォルダーの URI を指定します。この場合、 `testResource` と名付けたリソースは、 `testFolder` と名付けたフォルダーに保存されるため、フォルダーの URI は `"/testFolder"` になります。Microsoft .NET Framework に準拠している言語（例：C#）を使用する場合、URI を `System.String` オブジェクトに保存します。

1. リソースを作成

   リソースを作成するには、 `Resource` クラスのデフォルトのコンストラクターを呼び出します 。この例では、次の情報が `Resource` オブジェクトに保存されています：

   * `com.adobe.repository.infomodel.Id` オブジェクト。 `Id` クラス用のデフォルトのコンストラクターを呼び出し、`Resource` オブジェクトの `id` フィールドに割り当てられると作成される。
   * `com.adobe.repository.infomodel.Lid` オブジェクト。 `Lid` クラス用のデフォルトのコンストラクターを呼び出し、`Resource` オブジェクトの `lid` フィールドに割り当てられると作成される。
   * `Resource` オブジェクトの `name` フィールドに割り当てられた、リソースのファイル名を含む文字列。この例で使用される名前は、 `"testResource"` です。
   * `Resource` オブジェクトの `description` フィールドに割り当てられた、リソースの説明を含む文字列。この例で使用される説明は `"test resource"` です。

1. リソースコンテンツを指定

   リソースのコンテンツを作成するには、 `ResourceContent` クラス用のデフォルトのコンストラクターを呼び出します。次に、 `ResourceContent` オブジェクトにコンテンツを追加します。この例では、次のタスクを実行して実現されます。

   * `BLOB` ドキュメントを含むオブジェクトを `ResourceContent` オブジェクトの `dataDocument` フィールドに割り当てます。
   * `BLOB` オブジェクトのサイズ（バイト単位）を `ResourceContent` オブジェクトの `size` フィールドに割り当てます。

   `ResourceContent` オブジェクトを `Resource` オブジェクトの `content` フィールドに割り当てて、コンテンツをリソースに追加します。

1. ターゲットフォルダにリソースを書き込む

   `RepositoryServiceService` オブジェクトの `writeResource` メソッドを呼び出して、フォルダーの URI と `Resource` オブジェクトを渡します。他の 2 つのパラメータに対して `null` を渡します。

**関連トピック**

[リソースの書き込み](aem-forms-repository.md#writing-resources)

[Base64 エンコーディングを使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## リソースのリスト {#listing-resources}

リソースを一覧表示することで、リソースを見つけることができます。リポジトリに対してクエリが実行され、特定のリソースコレクションに関連するすべてのリソースが検索されます。

リソースを整理したら、オペレーティングシステムでおこなうように、構造の特定のブランチを表示して、作成した構造を検査できます。

リソースのリストは、次の関係によって機能します。リソースは、フォルダーのメンバーです。メンバーシップは、「…のメンバー」タイプの関係で表されます。特定のフォルダー内のリソースをリストする場合、「…のメンバー」の関係によって特定のフォルダーに関連するリソースをクエリします。関係は方向性を持ちます。関係のメンバーには、ターゲットのメンバーであるソースがあります。ソースはリソースです。ターゲットは親フォルダーです。

>[!NOTE]
>
>リポジトリサービスに関する詳細は、 [AEM Forms サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary_of_steps-2}

リソースをリストに追加するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. サービスクライアントを作成します。
1. フォルダーパスを指定します。
1. リソースのリストを取得します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを含めます。

**サービスクライアントを作成**

プログラムによってリソースコレクションを作成する前に、接続を確立し、資格情報を入力する必要があります。これは、サービスクライアントを作成することで実行されます。

**フォルダーパスを指定**

リソースを含むフォルダーのパスを含む文字列を作成します。構文には、次の例のようにスラッシュが含まれます。「/*パス*/*フォルダー*」。

**リソースのリストを取得**

Repository サービスメソッドを呼び出し、ターゲットフォルダーのパスを指定して、リソースのリストを取得します。

**関連トピック**

[Java API を使用したリソースのリスト化](aem-forms-repository.md#list-resources-using-the-java-api)

[Web サービス API を使用したリソースのリスト化](aem-forms-repository.md#list-resources-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Repository サービス API クイックスタート](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java API を使用したリソースのリスト化 {#list-resources-using-the-java-api}

Repository サービス API（Java）を使用してリソースをリスト化します。

1. プロジェクトファイルを含める

   クライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. サービスクライアントの作成

   `ResourceRepositoryClient` オブジェクトを作成するには、コンストラクターを使用して、接続プロパティを含む `ServiceClientFactory` オブジェクトを渡します。

1. フォルダーパスの指定

   クエリを実行するリソースコレクションの URI を指定します。この場合、URI は `"/testFolder"` となります。URI は `java.lang.String` オブジェクトとして保存されます。

1. リソースのリストの取得

   `ResourceRepositoryClient` オブジェクトの `listMembers` メソッドを呼び出して、フォルダーの URI を渡します。

   このメソッドは、`com.adobe.repository.infomodel.bean.Resource` オブジェクト（`Relation.TYPE_MEMBER_OF` タイプの `com.adobe.repository.infomodel.bean.Relation` であり、ターゲットとしてリソースコレクション URI を持つ）の `java.util.List` を返します。この `List` を反復処理して各リソースを取得できます。この例では、各リソースの名前と説明が表示されます。

**関連トピック**

[リソースのリスト化](aem-forms-repository.md#listing-resources)

[クイックスタート（SOAP モード）：Java API を使用したリソースのリスト化](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-listing-resources-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用したリソースのリスト化 {#list-resources-using-the-web-service-api}

Repository サービス API（web サービス）を使用してリソースをリスト化します。

1. プロジェクトファイルを含める

   * リポジトリ WSDL を使用する Microsoft .NET クライアントアセンブリを作成します。
   * Microsoft .NET クライアントアセンブリを参照します。

1. サービスクライアントの作成

   Microsoft .NET クライアントアセンブリを使用して、デフォルトのコンストラクターを呼び出し、`RepositoryServiceService` オブジェクトを作成します。ユーザー名とパスワードを含む `System.Net.NetworkCredential` オブジェクトを使用して、`Credentials` プロパティを設定します。

1. フォルダーパスの指定

   クエリを実行するフォルダーの URI を含む文字列を指定します。この場合、URI は `"/testFolder"` です。Microsoft .NET Framework に準拠している言語（C# など）を使用する場合、URI を `System.String` オブジェクトに保存します。

1. リソースのリストを取得

   `RepositoryServiceService` オブジェクトの `listMembers` メソッドを呼び出して、フォルダーの URI を最初のパラメーターとして渡します。他の 2 つのパラメータに対して `null` を渡します。

   メソッドは、`Resource` オブジェクトにキャスト可能なオブジェクトの配列を返します。オブジェクト配列を反復処理して、関連する各リソースを取得できます。この例では、各リソースの名前と説明が表示されます。

**関連トピック**

[リソースのリスト化](aem-forms-repository.md#listing-resources)

[Base64 エンコーディングを使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## リソースの読み取り {#reading-resources}

リポジトリ内の特定の場所からリソースを取得して、そのコンテンツとメタデータを読み取ることができます。ワークフローは、初期化フォームによってフロントエンドで実行されます。プロセスには、フォームを読み取るために必要なすべての権限があります。システムがデータフォームを取得し、リポジトリからコンテンツを読み取ります。リポジトリは、コンテンツとメタデータへのアクセスを許可します（リソースが存在することを知る機能）。

リポジトリには、以下の 4 つの権限タイプがあります。

* **トラバース**：リソースをリスト化できます。リソースのメタデータを読み取りますが、リソースのコンテンツを読み取ることはできません
* **読み取り**：リソースのコンテンツを読み取ることができます
* **書き込み**：リソースのコンテンツに書き込むことができます
* **アクセス制御リスト（ACL）の管理**：リソース上の ACL を操作できます

ユーザーは、プロセスを実行する権限を持っている場合にのみ、プロセスを実行できます。IDE ユーザーは、リポジトリと同期するには、トラバース権限と読み取り権限が必要です。ランタイムはシステムコンテキスト内で発生するので、ACL は設計時にのみ適用されます。

Repository サービス Java API または web サービス API を使用して、プログラムによってリソースを読み取ることができます。

>[!NOTE]
>
>Repository サービスについて詳しくは、[AEM Forms サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary_of_steps-3}

リソースを読み取るには、以下の手順に従います。

1. プロジェクトファイルを含めます。
1. リポジトリサービスクライアントを作成します。
1. 読み取るリソースの URI を指定します。
1. リソースを読み取ります。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを含めます。

**サービスクライアントの作成**

プログラムによってリソースを読み取る前に、接続を確立し、資格情報を指定する必要があります。これは、サービスクライアントを作成することで実行されます。

**読み取るリソースの URI の指定**

読み取るリソースの URI を含む文字列を作成します。構文には、「/*path*/*resource*」のようにフォワードスラッシュが含まれます。

**リソースを読み込む**

レポジトリサービスメソッドを呼び出し、URI を指定してリソースを読み込みます。

**関連トピック**

[Java API を使用してリソースを読み取る](aem-forms-repository.md#read-resources-using-the-java-api)

[Web サービス API を使用したリソースの読み込み](aem-forms-repository.md#reading-resources-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Repository サービス API クイックスタート](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java API を使用してリソースを読み込む {#read-resources-using-the-java-api}

リポジトリサービス API（Java）を使用してリソースを読み込みます。

1. プロジェクトファイルを含める

   クライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. サービスクライアントの作成

   コンストラクターを使用して、接続プロパティを含む `ServiceClientFactory` オブジェクトを渡すことにより、`ResourceRepositoryClient` オブジェクトを作成します。

1. 読み込むリソースの URI を指定

   取得するリソースの URI を表す文字列値を指定します。例えば、リソースの名前が *testResource* で、*testFolder* という名前のフォルダーに保存されているとすると、`/testFolder/testResource` を指定します。

1. リソースを読み込む

   `ResourceRepositoryClient` オブジェクトの `readResource` メソッドを呼び出し、リソースの URI をパラメーターとして渡します。このメソッドは、リソースを表す `Resource` インスタンスを返します。

**関連トピック**

[リソースの読み取り](aem-forms-repository.md#reading-resources)

[クイックスタート（SOAP モード）：Java API を使用したリソースの読み込み](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-reading-a-resource-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用したリソースの読み込み {#reading-resources-using-the-web-service-api}

リポジトリサービス API（web サービス）を使用してリソースを読み込みます。

1. プロジェクトファイルを含める

   * リポジトリ WSDL を使用する Microsoft .NET クライアントアセンブリを作成します。（[Base64 エンコーディングを使用する .NET クライアントアセンブリの作成](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)を参照。）
   * Microsoft .NET クライアントアセンブリを参照します（[Base64 エンコーディングを使用する .NET クライアントアセンブリの作成](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)を参照。）

1. サービスクライアントの作成

   Microsoft .NET クライアントアセンブリを使用して、デフォルトのコンストラクターを呼び出し、`RepositoryServiceService` オブジェクトを作成します。ユーザー名とパスワードを含む `System.Net.NetworkCredential` オブジェクトを使用して、`Credentials` プロパティを設定します。

1. 読み込むリソースの URI を指定

   取得するリソースの URI を含む文字列を指定します。この場合、`testResource` という名前のリソースが、`testFolder` という名前のフォルダーにあるため、その URI は `"/testFolder/testResource"` になります。Microsoft .NET Framework に準拠している言語（例：C#）を使用する場合、URI を `System.String` オブジェクトに格納します。

1. リソースを読み込む

   `RepositoryServiceService` オブジェクトの `readResource` メソッドを呼び出し、リソースの URI を最初のパラメーターとして渡します。他の 2 つのパラメーターには `null` を渡します。

**関連トピック**

[リソースの読み取り](aem-forms-repository.md#reading-resources)

[Base64 エンコーディングを使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## リソースのアップデート {#updating-resources}

リポジトリ内のリソースのコンテンツを取得および更新できます。リソースを更新しても、それらのリソースへのアクセス制御は、バージョン間で変更されません。アップデートを実行する際に、メジャーバージョンを増分するオプションがあります。メジャーバージョンの増分を選択しない場合、マイナーバージョンは自動的にアップデートされます。

リソースをアップデートすると、指定したリソースの属性に基づいて新しいバージョンが作成されます。リソースをアップデートする際には、次の 2 つの重要なパラメータを指定します。ターゲット URI と、更新されたすべてのメタデータを含むリソースインスタンスです。特定の属性（名前など）を変更しない場合、その属性は渡すインスタンスで依然として必須であることに注意してください。コンテンツの解析時に作成される関係は、特定のバージョンに追加され、指定がない限り繰り越されません。

例えば、XDP ファイルを更新し、そのファイルにその他のリソースへの参照が含まれている場合、それらの追加参照も記録されます。form.xdp バージョン 1.0 に 2 つの外部参照（ロゴとスタイルシート）があり、その後 form.xdp を更新して、3 つの参照（ロゴ、スタイルシートおよびスキーマファイル）が含まれるようにしたとします。更新中、リポジトリは 3 つ目の関係（スキーマファイルへ）を保留中の関係テーブルに追加します。スキーマファイルがリポジトリに存在すると、関係は自動的に形成されます。ただし、form.xdp バージョン 2.0 でロゴが使用されなくなった場合、form.xdp バージョン 2.0 はロゴとの関係がなくなります。

すべての更新操作はアトミックでトランザクションです。例えば、2 人のユーザーが同じリソースを読み込み、両方のユーザーがバージョン 1.0 をバージョン 2.0 に更新しようとした場合、一方が成功し、他方が失敗すると、リポジトリの整合性が維持され、両方のユーザーに成功または失敗を確認するメッセージが表示されます。トランザクションがコミットされない時、データベース障害が発生した場合にロールバックされ、アプリケーションサーバーに応じてタイムアウトまたはロールバックされます。

リポジトリサービス Java API または web サービス API を使用して、プログラムでリソースを更新できます。

>[!NOTE]
>
>リポジトリサービスについて詳しくは、[AEM Forms のサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary_of_steps-4}

リソースを更新するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. リポジトリサービスクライアントを作成します。
1. 更新するリソースを取得します。
1. リソースを更新します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを含めます。

**サービスクライアントの作成**

プログラムによってリソースを読み取る前に、接続を確立し、資格情報を指定する必要があります。これは、サービスクライアントを作成することで実行されます。

**アップデートするリソースを取得する**

リソースを読み取ります。詳しくは、[リソースの読み取り](aem-forms-repository.md#reading-resources)を参照してください。

**リソースをアップデート**

リソースに新しい情報を設定し、リポジトリサービスメソッドを呼び出して、リソースをアップデートし、URI、アップデートされたリソース、およびバージョン情報のアップデート方法を指定します。

**関連トピック**

[Java API を使用したリソースのアップデート](aem-forms-repository.md#update-resources-using-the-java-api)

[Web サービス API を使用したリソースのアップデート](aem-forms-repository.md#update-resources-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Repository サービス API クイックスタート](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java API を使用したリソースのアップデート {#update-resources-using-the-java-api}

リポジトリサービス API（Java）を使用してリソースをアップデートします。

1. プロジェクトファイルを含める

   クライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. サービスクライアントの作成

   コンストラクターを使用し、接続プロパティを含む `ServiceClientFactory` オブジェクトを渡すことにより、`ResourceRepositoryClient` オブジェクトを作成します。

1. アップデートするリソースを取得する

   リソースを取得および読み取るリソースの URI を指定します。この例では、リソースの URI は `"/testFolder/testResource"` です。

1. リソースをアップデート

   `Resource` オブジェクトの情報をアップデートします。この例では、説明をアップデートするには、 `Resource` オブジェクトの `setDescription` メソッドを呼び出して新しい説明文字列をパラメーターとして渡します。

   次に、`ServiceClientFactory` オブジェクトの `updateResource` メソッドを呼び出して、次のパラメーターを渡します。

   * リソースの URI を含む `java.lang.String` オブジェクト。
   * アップデートされたリソース情報を含む `Resource` オブジェクト。
   * メジャーバージョンとマイナーバージョンのどちらをアップデートするかを示す `boolean` 値。この例では、値は `true` を渡して、メジャーバージョンの増分を示します。

**関連トピック**

[リソースのアップデート](aem-forms-repository.md#updating-resources)

[クイックスタート（SOAP モード）：Java API を使用したリソースの書き込み](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-updating-a-resource-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用したリソースのアップデート {#update-resources-using-the-web-service-api}

Repository API（web サービス）を使用してリソースをアップデートします。

1. プロジェクトファイルを含める

   * リポジトリ WSDL を使用する Microsoft .NET クライアントアセンブリを作成します。
   * Microsoft .NET クライアントアセンブリを参照します。

1. サービスクライアントの作成

   Microsoft .NET クライアントアセンブリを使用して、デフォルトのコンストラクターを呼び出し、`RepositoryServiceService` オブジェクトを作成します。ユーザー名とパスワードを含む `System.Net.NetworkCredential` オブジェクトを使用して、その `Credentials` プロパティを設定します。

1. アップデートするリソースを取得する

   取得するリソースの URI を指定し、リソースを読み取ります。この例では、リソースの URI は `"/testFolder/testResource"` です。詳しくは、 [リソースの読み取り](aem-forms-repository.md#reading-resources)を参照してください。

1. リソースをアップデート

   `Resource` オブジェクトの情報をアップデートします。この例では、説明をアップデートするために、新しい値を `Resource` オブジェクトの `description` フィールドに割り当てます。

1. `RepositoryServiceService` オブジェクトの `updateResource` メソッドを呼び出して、次のパラメーターを渡します。

   * リソースの URI を含む `System.String` オブジェクト。
   * アップデートされたリソース情報を含む `Resource` オブジェクト。
   * メジャーバージョンとマイナーバージョンのどちらをアップデートするかを示す `boolean` 値。この例では、`true` の値が渡されて、メジャーバージョンを増加する必要があることを示します。
   * 残りの 2 つのパラメータに対して `null` を渡します。

**関連トピック**

[リソースのアップデート](aem-forms-repository.md#updating-resources)

[Base64 エンコーディングを使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## リソースの検索 {#searching-for-resources}

リポジトリ内のリソース（履歴、関連リソース、プロパティなど）を検索するために使用するクエリを作成できます。

関連リソースを取得して、フォームとそのフラグメント間の依存関係を判断できます。例えば、フォームがある場合、使用するフラグメントや外部リソースを決定できます。画像がある場合は、その画像がどのフォームで使用されているかも確認できます。また、プロパティに基づくフィルタリングを使用して、関連リソースを検索することもできます。例えば、指定した名前の画像を使用するすべてのフォームを検索したり、指定した名前のフォームで使用されている画像を検索できます。また、リソースプロパティを使用して検索することもできます。例えば、クエリを実行して、名前が指定の文字列で始まるすべてのフォームやリソースを検索することができ、文字列にはワイルドカード「%」や「_」を含めることができます。プロパティに基づく検索は、関係に基づくものではないことに注意してください。このような検索は、あるリソースに関する特定の知識を持っていることを前提としています。

**クエリステートメント**

*クエリ*&#x200B;には、条件で論理的に結合される 1 つ以上のステートメントが含まれます。*ステートメント*&#x200B;は、左オペランド、演算子、右オペランドで構成されます。また、検索結果に使用する並べ替え順を指定できます。この&#x200B;*並べ替え順*&#x200B;には、SQL の `ORDER BY` 句と同等の情報が含まれ、検索の基となった属性と、昇順または降順を使用するかどうかを示す値を含む要素で構成されます。

レポジトリサービス Java API を使用して、プログラムでリソースを検索できます。現時点では、web サービス API を使用してリソースを検索することはできません。

**並べ替え動作**

並べ替え順序は、`ResourceRepositoryClient` オブジェクトの `searchProperties` メソッドを呼び出す際や並べ替え順を指定する際に考慮されません。例えば、属性名が `name`、`secondName` および `asecondName` の 3 つのカスタムプロパティを持つリソースを作成するとします。次に、属性名に並べ替え順の要素を作成し、`ascending` の値を `true` に設定します。

次に、 `ResourceRepositoryClient` オブジェクトの `searchProperties` メソッドを呼び出して、並べ替え順を渡します。検索を実行すると、適切なリソースと 3 つのプロパティが返されます。ただし、プロパティは属性名でソートされていません。`name`、`secondName` および `asecondName` のように、追加された順序で返されます。

>[!NOTE]
>
>レポジトリサービスについて詳しくは、[ AEM Forms サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary_of_steps-5}

リソースを検索するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. リポジトリサービスクライアントを作成します。
1. 検索のターゲットフォルダーを指定します。
1. 検索で使用する属性を指定します。
1. 検索で使用するクエリを作成します。
1. 検索結果の並べ替え順を作成します。
1. リソースを検索します。
1. 検索結果からリソースを取得します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを含めます。

**サービスクライアントの作成**

プログラムによってリソースを読み取る前に、接続を確立し、資格情報を指定する必要があります。これは、サービスクライアントを作成することで実行されます。

**検索のターゲットフォルダーを指定**

検索の実行元となるベースパスを含む文字列を作成します。構文には、「/*path*/*folder*」のようにフォワードスラッシュが含まれます。

**検索に使用する属性を指定**

リソース内に含まれる属性に基づいて検索を実行できます。検索を実行する属性の値を指定します。

**検索で使用するクエリを作成**

ステートメントと条件を使用してクエリを作成します。各ステートメントは、検索のベースとなる属性、使用する条件、検索で使用する属性値を指定します。

**検索結果の並べ替え順を作成**

並べ替え順は、要素で構成され、各要素には、検索で使用される属性の 1 つと、昇順または降順を使用するかどうかを示す値が含まれます。

**リソースの検索**

フォルダー、クエリ、並べ替え順を使用してリソースを検索します。また、検索の深度と、返される結果の数の上限を指定します。

**検索結果からリソースを取得**

返されたリソースのリストを繰り返し処理し、さらに処理するために情報を抽出します。

**関連トピック**

[Java API を使用したリソースの検索](aem-forms-repository.md#search-for-resources-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Repository サービス API クイックスタート](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java API を使用したリソースの検索 {#search-for-resources-using-the-java-api}

Repository service API（Java）を使用してリソースを検索します。

1. プロジェクトファイルを含める

   クライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. サービスクライアントの作成

   コンストラクターを使用して、接続プロパティを含む `ServiceClientFactory` オブジェクトを渡すことによって、`ResourceRepositoryClient` オブジェクトを作成します。

1. 検索のターゲットフォルダーの指定

   検索を実行するベースパスの URI を指定します。この例では、リソースの URI は `/testFolder` です。

1. 検索に使用する属性の指定

   検索を実行する属性の値を指定します。属性は `com.adobe.repository.infomodel.bean.Resource` オブジェクト内に存在します。この例では、検索は name 属性に対して実行されます。したがって、`Resource` オブジェクトの名前を含む `java.lang.String` が使用されます（この場合は `testResource`）。

1. 検索で使用するクエリの作成

   クエリを作成するには、`Query` クラスのデフォルトコンストラクターを呼び出して `com.adobe.repository.query.Query` オブジェクトを作成し、クエリに文を追加します。

   文を作成するには、`com.adobe.repository.query.Query.Statement` クラスのコンストラクタ―を呼び出して、以下のパラメーターを渡します。

   * リソース属性定数を含む左オペランド。この例では、リソースの名前が検索の基礎として使用されるので、静的な値 `Resource.ATTRIBUTE_NAME` が使用されます。
   * 属性の検索で使用される条件を含む演算子。演算子は、`Query.Statement` クラスの静的定数のいずれかである必要があります。この例では、静的な値 `Query.Statement.OPERATOR_BEGINS_WITH` が使用されます。
   * 検索を実行する属性値が含まれる右オペランド。この例では、name 属性（`"testResource"` 値を含む `String`）が使用されます。

   `Query.Statement` オブジェクトの `setNamespace` メソッドを呼び出し、`com.adobe.repository.infomodel.bean.ResourceProperty` クラスに含まれる静的値の 1 つを渡すことにより、左側のオペランドの名前空間を指定します。この例では、`ResourceProperty.RESERVED_NAMESPACE_REPOSITORY` が使用されます。

   `Query` オブジェクトの `addStatement` メソッドを呼び出し、`Query.Statement` オブジェクトを渡すことにより、各文をクエリに追加します。

1. 検索結果の並べ替え順の作成

   検索結果で使用される並び替え順を指定するには、`SortOrder` クラスのデフォルトコンストラクターを呼び出して `com.adobe.repository.query.sort.SortOrder` オブジェクトを作成し、並び替え順に要素を追加します。

   並べ替え順の要素を作成するには、`com.adobe.repository.query.sort.SortOrder.Element` クラスのコンストラクターのいずれかを呼び出します。この例では、リソースの名前が検索の基礎として使用されるので、静的な値 `Resource.ATTRIBUTE_NAME` は最初のパラメーターとして使用され、昇順（`true` の `boolean` 値）が 2 番目のパラメーターとして指定されます。

   並べ替え順に各要素を追加するには、`SortOrder` オブジェクトの `addSortElement` メソッドを呼び出して `SortOrder.Element` オブジェクトを渡します。

1. リソースの検索

   属性プロパティにもとづいて `resources` を検索するには、`ResourceRepositoryClient` オブジェクトの `searchProperties` メソッドを呼び出して以下のパラメーターを渡します。

   * 検索を実行するベースパスを含む `String`。この場合、`"/testFolder"` が使用されます。
   * 検索で使用されるクエリ。
   * 検索の深度。この場合、`com.adobe.repository.infomodel.bean.ResourceCollection.DEPTH_INFINITE` は、ベースパスとそのすべてのフォルダーを使用することを示すために使用されます。
   * 非ページ化結果セットを選択する最初の行を示す `int` 値。この例では、`0` が指定されています。
   * 返される結果の最大数を示す `int` 値。この例では、`10` が指定されています。
   * 検索で使用される並べ替え順です。

   このメソッドは、`Resource` オブジェクトの `java.util.List` を指定した並べ替え順に返します。

1. 検索結果からのリソースの取得

   検索結果に含まれるリソースを取得するには、`List` を反復処理して各オブジェクトを `Resource` にキャストし、情報を抽出します。この例では、各リソースの名前が表示されます。

**関連トピック**

[リソースの検索](aem-forms-repository.md#searching-for-resources)

[クイックスタート（SOAP モード）：Java API を使用したリソースの検索](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## リソースの関係の作成 {#creating-resource-relationships}

リポジトリ内のリソース間の関係を指定できます。関係には、以下の 3 種類があります。

* **依存性**：リソースが他のリソースに依存する関係。関連するすべてのリソースがリポジトリ内で必要であることを意味します。
* **メンバーシップ（ファイルシステム）**：あるリソースが、特定のフォルダー内に配置されている関係。
* **カスタム**：リソース間で指定する関係。例えば、あるリソースが非推奨になり、別のリソースがリポジトリに導入された場合、独自の代替関係を指定できます。

独自のカスタム関係を作成します。例えば、HTML ファイルをリポジトリに格納し、そのファイルが画像を使用する場合、カスタムの関係を指定して HTML ファイルと画像を関連付けることができます（通常、リポジトリ定義の依存関係を使用して画像に関連付けられるのは XML ファイルのみです）。別のカスタム関係の例として、ツリー構造ではなく循環グラフ構造を使用して、リポジトリの別のビューを構築する場合があります。ビューアーと共に円グラフを定義して、これらの関係をトラバースすることができます。最後に、2 つのリソースが完全に異なる場合でも、1 つのリソースが別のリソースを置き換えることを示すことができます。この場合、予約範囲外の関係タイプを定義して、これら 2 つのリソース間の関係を作成できます。アプリケーションは、関係を検出して処理できる唯一のクライアントであり、その関係の検索を実行するために使用できます。

Repository サービス Java API または web サービス API を使用して、プログラムによってリソース間の関係を指定できます。

>[!NOTE]
>
>Repository サービスについて詳しくは、[AEM Forms サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary_of_steps-6}

2 つのリソース間の関係を指定するには、以下の手順に従います。

1. プロジェクトファイルを含めます。
1. リポジトリサービスクライアントを作成します。
1. 関連付けるリソースの URI を指定します。
1. 関係を作成します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを含めます。

**サービスクライアントの作成**

プログラムによってリソースを読み取る前に、接続を確立し、資格情報を指定する必要があります。これは、サービスクライアントを作成することで実行されます。

**関連付けるリソースの URI の指定**

関連付けるリソースの URI を含む文字列を作成します。構文には、「/*path*/*resource*」のようにフォワードスラッシュが含まれます。

**関係の作成**

Repository サービスメソッドを呼び出して、関係のタイプを作成し、指定します。

**関連トピック**

[Java API を使用した関係リソースの作成](aem-forms-repository.md#create-relationship-resources-using-the-java-api)

[Web サービス API を使用した関係リソースの作成](aem-forms-repository.md#create-relationship-resources-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Repository サービス API クイックスタート](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java API を使用した関係リソースの作成 {#create-relationship-resources-using-the-java-api}

Repository サービス Java API を使用して関係リソースを作成し、以下のタスクを実行します。

1. プロジェクトファイルを含める

   クライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. サービスクライアントの作成

   `ResourceRepositoryClient` オブジェクトを作成するには、コンストラクターを使用して、接続プロパティを含む `ServiceClientFactory` オブジェクトを渡します。

1. 関連付けるリソースの URI の指定

   関連付けるリソースの URI を指定します。この場合、リソースの名前が `testResource1` および `testResource2` で、`testFolder` という名前のフォルダーに配置されているので、URI は `"/testFolder/testResource1"` および `"/testFolder/testResource2"` となります。URI は `java.lang.String` オブジェクトとして格納されます。この例では、リソースは最初にリポジトリに書き込まれ、URI が取得されます。リソースの書き込みについて詳しくは、[リソースの書き込み](aem-forms-repository.md#writing-resources)を参照してください。

1. 関係の作成

   `ResourceRepositoryClient` オブジェクトの `createRelationship` メソッドを呼び出して、次のパラメーターを渡します。

   * ソースリソースの URI。
   * ターゲットリソースの URI。
   * 関係のタイプで、`com.adobe.repository.infomodel.bean.Relation` クラスの静的定数値の 1 つです。この例では、`Relation.TYPE_DEPENDANT_OF` 値を指定することで依存関係が成立します。
   * `boolean` 値は、新しいヘッドリソースの `com.adobe.repository.infomodel.Id` ベースの識別情報にターゲットリソースを自動的に更新するかどうかを示す値です。この例では、依存関係により、`true` 値が指定されています。

   また、特定のリソースに関連するリソースのリストを取得するには、`ResourceRepositoryClient` オブジェクトの `getRelated` メソッドを呼び出して、以下のパラメーターを渡します。

   * 関連リソースを取得するリソースの URI です。この例では、ソースリソース（`"/testFolder/testResource1"`）が指定されています。
   * 指定したリソースが関係のソースリソースであるかどうかを示す `boolean` 値。この例では、このようになっているため、`true` 値が指定されています。
   * 関係タイプは、`Relation` クラスの静的定数値の 1 つです。この例では、以前と同じく `Relation.TYPE_DEPENDANT_OF` 値を使用して依存関係を指定します。

   `getRelated` メソッドは、`Resource` オブジェクトの `java.util.List` を返します。これを繰り返し処理して各関連リソースを取得することができ、`List` に含まれるオブジェクトを `Resource` にキャストします。この例では、`testResource2` は、返されたリソースのリストに含まれると想定されます。

**関連トピック**

[リソースの関係の作成](aem-forms-repository.md#creating-resource-relationships)

[クイックスタート（SOAP モード）：Java API を使用したリソース間の関係の作成](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-relationships-between-resources-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用した関係リソースの作成 {#create-relationship-resources-using-the-web-service-api}

リポジトリ API（web サービス）を使用して関係リソースを作成します。

1. プロジェクトファイルを含める

   * リポジトリ WSDL を使用する Microsoft .NET クライアントアセンブリを作成します。
   * Microsoft .NET クライアントアセンブリを参照します。

1. サービスクライアントの作成

   Microsoft .NET クライアントアセンブリを使用して、デフォルトのコンストラクターを呼び出し、`RepositoryServiceService` オブジェクトを作成します。ユーザー名とパスワードを含む `System.Net.NetworkCredential` オブジェクトを使用して、`Credentials` プロパティを設定します。

1. 関連付けるリソースの URI の指定

   関連付けるリソースの URI を指定します。この場合、リソースの名前が `testResource1` および `testResource2` で、`testFolder` という名前のフォルダーに配置されているので、URI は `"/testFolder/testResource1"` および `"/testFolder/testResource2"` となります。Microsoft .NET Framework に準拠している言語（C# など）を使用する場合、URI は `System.String` オブジェクトとして保存されます。この例では、リソースは最初にリポジトリに書き込まれ、URI が取得されます。リソースの書き込みについて詳しくは、[リソースの書き込み](aem-forms-repository.md#writing-resources)を参照してください。

1. 関係の作成

   `RepositoryServiceService` オブジェクトの `createRelationship` メソッドを呼び出して、次のパラメーターを渡します。

   * ソースリソースの URI。
   * ターゲットリソースの URI。
   * 関係のタイプ。この例では、値 `3` を指定することで依存関係が成立します。
   * 関係タイプが指定されたかどうかを示す `boolean` 値。この例では、値 `true` が指定されています。
   * ターゲットリソースが新しいヘッドリソースの `Id` ベースの識別子に自動的に更新されるかどうかを示す `boolean` 値。この例では、依存関係が成り立っているため、値 `true` が指定されています。
   * ターゲットヘッドが指定されたかどうかを示す `boolean` 値。この例では、値 `true` が指定されています。
   * 最後のパラメーターとして `null` を渡します。

   また、`RepositoryServiceService` オブジェクトの `getRelated` メソッドを呼び出し、次のパラメーターを渡すことで、特定のリソースに関連するリソースのリストを取得できます。

   * 関連リソースを取得するリソースの URI です。この例では、ソースリソース（`"/testFolder/testResource1"`）が指定されています。
   * 指定したリソースが関係のソースリソースであるかどうかを示す `boolean` 値。この例では、ソースリソースであるため、値 `true` が指定されています。
   * ソースリソースが指定されたかどうかを示す `boolean` 値。この例では、値 `true` が指定されています。
   * 関係タイプを格納する整数の配列。この例では、以前と同じ値を配列で使用して依存関係が指定されているので `3` が指定されています。
   * 残りの 2 つのパラメーターには `null` を渡します。

   `getRelated` メソッドは、オブジェクトの配列を返します。この配列は `Resource` オブジェクトにキャストでき、このオブジェクトを介し各関連リソースを繰り返し取得できます。この例では、返されるリソースリストに `testResource2` があると想定されます。

**関連トピック**

[リソースの関係の作成](aem-forms-repository.md#creating-resource-relationships)

[Base64 エンコーディングを使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## リソースのロック {#locking-resources}

特定のユーザーが排他的に使用できるように、または複数のユーザー間で共有して使用できるように、リソースまたはリソースのセットをロックできます。共有ロックは、リソースに対して何らかの処理が行われることを示すものですが、他のユーザーもそのリソースに操作を行うことができます。共有ロックは、他のユーザーにサインを示すメカニズムと考えることができます。排他的ロックとは、リソースをロックしたユーザーがリソースに変更を加えようとしていることを意味し、ロックをすることで、そのユーザーがリソースにアクセスする必要がなくなりロックを解除するまでは、他のユーザーがリソースを変更できなくなります。リポジトリ管理者がリソースのロックを解除すると、そのリソースに対するすべての排他的なロックと共有ロックが自動的に削除されます。このタイプのアクションは、登録解除されたユーザーがリソースのロックを解除しなかった場合に使用します。

リソースがロックされていると、次の図に示すように、Workbench の「リソース」タブを表示したときにロックアイコンが表示されます。

![lr_lr_lockrepository](assets/lr_lr_lockrepository.png)

Repository サービス Java API または web サービス API を使用して、リソースへのアクセスをプログラムで制御できます。

>[!NOTE]
>
>Repository サービスについて詳しくは、[AEM Forms のサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary_of_steps-7}

リソースのロックやロック解除を行うには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. リポジトリサービスクライアントを作成します。
1. ロックするリソースの URI を指定します。
1. リソースをロックします。
1. リソースのロックを取得します。
1. リソースのロックの解除

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを含めます。

**サービスクライアントの作成**

プログラムによってリソースを読み取る前に、接続を確立し、資格情報を指定する必要があります。これは、サービスクライアントを作成することで実行されます。

**ロックするリソースの URI の指定**

ロックするリソースの URI を含む文字列を作成します。構文には、「/*path*/*resource*」のようにフォワードスラッシュが含まれます。

**リソースのロック**

Repository サービスメソッドを呼び出し、URI、ロックのタイプ、ロックの深度を指定して、リソースをロックします。

**リソースのロックの取得**

Repository サービスメソッドを呼び出し URI を指定して、リソースのロックを取得します。

**リソースのロックの解除**

Repository サービスメソッドを呼び出し URI を指定して、リソースのロックを解除します。

**関連トピック**

[Java API を使用したリソースのロック](aem-forms-repository.md#lock-resources-using-the-java-api)

[Web サービス API を使用したリソースのロック](aem-forms-repository.md#lock-resources-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Repository サービス API クイックスタート](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java API を使用したリソースのロック {#lock-resources-using-the-java-api}

Repository サービス API（Java）を使用してリソースをロックします。

1. プロジェクトファイルを含める

   クライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. サービスクライアントの作成

   `ResourceRepositoryClient` オブジェクトを作成するには、コンストラクターを使用して、接続プロパティを含む `ServiceClientFactory` オブジェクトを渡します。

1. ロックするリソースの URI の指定

   ロックするリソースの URI を指定します。この場合、`testResource` という名前のリソースが、`testFolder` という名前のフォルダーにあるため、その URI は `"/testFolder/testResource"` となります。URI は `java.lang.String` オブジェクトとして保存されます。

1. リソースのロック

   `ResourceRepositoryClient` オブジェクトの `lockResource` メソッドを呼び出して、以下のパラメーターを渡します。

   * リソースの URI です。
   * ロックの範囲。この例では、リソースは排他的に使用するためにロックされるので、ロックの範囲は `com.adobe.repository.infomodel.bean.Lock.SCOPE_EXCLUSIVE` のように指定されます。
   * ロックの深度。この例では、ロックは特定のリソースにのみ適用され、メンバーや子には適用されないので、ロックの深度は `Lock.DEPTH_ZERO` になります。

   >[!NOTE]
   >
   >4 つのパラメーターを必要とする、オーバーロードされたバージョンの `lockResource` メソッドでは、例外がスローされます。このチュートリアルに示す 3 つのパラメーターを必要とする `lockResource` メソッドを、必ず使用してください。

1. リソースのロックを取得

   `ResourceRepositoryClient` オブジェクトの `getLocks` メソッドを呼び出し、リソースの URI をパラメーターとして渡します。メソッドは、反復可能な Lock オブジェクトのリストを返します。この例では、個々の Lock オブジェクトの `getOwnerUserId`、`getDepth`、および `getType` メソッドをそれぞれ呼び出すことにより、所有者、深度、範囲が個々のオブジェクトのために印刷されます。

1. リソースのロックの解除

   `ResourceRepositoryClient` オブジェクトの `unlockResource` メソッドを呼び出し、リソースの URI をパラメーターとして渡します。詳しくは、[AEM Forms API リファレンス](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ja)を参照してください。

**関連トピック**

[リソースのロック](aem-forms-repository.md#locking-resources)

[クイックスタート（SOAP モード）：Java API を使用したリソースのロック](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-locking-a-resource-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用したリソースのロック {#lock-resources-using-the-web-service-api}

Repository サービス API（web サービス）を使用してリソースをロックします。

1. プロジェクトファイルを含める

   * リポジトリ WSDL を使用する Microsoft .NET クライアントアセンブリを、Base64 を使用して作成します。
   * Microsoft .NET クライアントアセンブリを参照します。

1. サービスクライアントの作成

   Microsoft .NET クライアントアセンブリを使用して、デフォルトのコンストラクターを呼び出し、`RepositoryServiceService` オブジェクトを作成します。ユーザー名とパスワードを含む `System.Net.NetworkCredential` オブジェクトを使用して、`Credentials` プロパティを設定します。

1. ロックするリソースの URI の指定

   ロックするリソースの URI を含む文字列を指定します。この場合、`testResource` という名前のリソースが `testFolder` フォルダーにあるため、その URI は `"/testFolder/testResource"` となります。Microsoft .NET Framework に準拠している言語（C# など）を使用する場合、URI は `System.String` オブジェクトに保存されます。

1. リソースのロック

   `RepositoryServiceService` オブジェクトの `lockResource` メソッドを呼び出して、以下のパラメーターを渡します。

   * リソースの URI です。
   * ロックの範囲。この例では、リソースは排他的に使用するためにロックされるので、ロックの範囲は `11` のように指定されます。
   * ロックの深度。この例では、ロックは特定のリソースにのみ適用され、メンバーや子には適用されないので、ロックの深度は `2` になります。
   * ロックの有効期限が切れるまでの秒数を示す `int` 値。この例では、`1000` の値が使用されます。
   * 最後のパラメーターに `null` を渡します。

1. リソースのロックの取得

   `RepositoryServiceService` オブジェクトの `getLocks` メソッドを呼び出し、リソースの URI を最初のパラメーターとして渡し、2 つ目のパラメーターに `null` を渡します。メソッドは、繰り返し可能な `Lock` オブジェクトを含む `object` 配列を返します。この例では、各 `Lock` オブジェクトの `ownerUserId`、`depth` および `type` フィールドにアクセスすると、各オブジェクトに対するロックの所有者、深度、範囲が印刷されます。

1. リソースのロックの解除

   `RepositoryServiceService` オブジェクトの `unlockResource` メソッドを呼び出し、リソースの URI を最初のパラメーターとして渡し、2 つ目のパラメーターに `null` を渡します。

**関連トピック**

[リソースのロック](aem-forms-repository.md#locking-resources)

[Base64 エンコーディングを使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## リソースの削除 {#deleting-resources}

Repository サービス Java API（SOAP）を使用して、リポジトリ内の特定の場所からリソースをプログラムで削除できます。

リソースを削除する場合、削除は通常は永続的ですが、ECM リポジトリの履歴メカニズムに従ってリソースのバージョンを保存する場合もあります。したがって、リソースを削除する場合は、そのリソースが再び必要にならないようにすることが重要です。リソースを削除する一般的な理由として、データベースの使用可能な領域を増やすことが挙げられます。リソースのバージョンは削除できますが、削除する場合は、論理識別子（LID）やパスではなく、リソース識別子を指定する必要があります。フォルダーを削除すると、サブフォルダーやリソースを含め、そのフォルダー内のすべてが自動的に削除されます。

関連リソースは削除されません。例えば、logo.gif ファイルを使用するフォームがあり、logo.gif を削除した場合、関係は保留中の関係テーブルに保存されます。別の方法として、バージョンの廃止については、最新バージョンのオブジェクトステータスを「非推奨」に設定します。

削除操作は、ECM システムではトランザクションセーフではありません。例えば、100 個のリソースを削除しようとして、50 番目のリソースで操作が失敗した場合、最初の 49 個のインスタンスは削除されますが、残りは削除されません。それ以外の場合、デフォルトの動作はロールバック（非コミットメント）です。

>[!NOTE]
>
>ECM リポジトリ（EMC Documentum Content Server および IBM FileNet P8 Content Manager）で `com.adobe.repository.bindings.dsc.client.ResourceRepositoryClient.deleteResources()` メソッドを使用する場合、指定したリソースの削除に失敗するとトランザクションがロールバックされず、削除されたファイルを元に戻せなくなります。

>[!NOTE]
>
>リポジトリサービスの詳細については、[AEM Forms のサービスレファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary_of_steps-8}

リソースを削除するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. リポジトリサービスクライアントを作成します。
1. 削除するリソースの URI を指定します。
1. リソースを削除します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを含めます。

**サービスクライアントの作成**

プログラムによってリソースを読み取る前に、接続を確立し、資格情報を指定する必要があります。これは、サービスクライアントを作成することで実行されます。

**削除するリソースの URI を指定**

削除するリソースの URI を含む文字列を作成します。構文には、次のようにフォワードスラッシュが含まれます。「/*パス*／*リソース*」。削除するリソースがフォルダーの場合、削除は繰り返し実行されます。

**リソースを削除**

URI を指定してリソースを削除するには、レポジトリサービスメソッドを呼び出します。

**関連トピック**

[Java API を使用したリソースの削除](aem-forms-repository.md#delete-resources-using-the-java-api-soap)

[Web サービス API を使用したリソースの削除](aem-forms-repository.md#delete-resources-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Repository サービス API クイックスタート](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java API（SOAP）を使用したリソースの削除 {#delete-resources-using-the-java-api-soap}

リポジトリ API（Java）を使用してリソースを削除します。

1. プロジェクトファイルを含める

   クライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. サービスクライアントの作成

   コンストラクターを使用して、接続プロパティを含む`ServiceClientFactory`オブジェクトを渡すことにより、`ResourceRepositoryClient`オブジェクトを作成します。

1. 削除するリソースの URI の指定

   取得するリソースの URI を指定します。この場合、testResourceToBeDeleted というリソースは testFolder というフォルダーにあるので、そのURIは `/testFolder/testResourceToBeDeleted` となります。URI は `java.lang.String` オブジェクトとして格納されます。この例では、リソースはまずリポジトリに書き込まれ、それから URI が取得されます。リソースの書き込みについて詳しくは、[リソースの書き込み](aem-forms-repository.md#writing-resources)を参照してください。

1. リソースの削除

   `ResourceRepositoryClient`オブジェクトの`deleteResource`メソッドを呼び出し、リソースの URI をパラメーターとして渡してください。

**関連トピック**

[リソースの削除](aem-forms-repository.md#deleting-resources)

[クイックスタート（SOAP モード）：Java API を使用したリソースの検索](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用したリソースの削除 {#delete-resources-using-the-web-service-api}

リポジトリ API（web サービス）を使用してリソースを削除します。

1. プロジェクトファイルを含める

   * リポジトリ WSDL を使用する Microsoft .NET クライアントアセンブリを、Base64 を使用して作成します。
   * Microsoft .NET クライアントアセンブリを参照します。

1. サービスクライアントの作成

   Microsoft .NET クライアントアセンブリを使用して、デフォルトのコンストラクターを呼び出し、`RepositoryServiceService` オブジェクトを作成します。ユーザー名とパスワードを含む`System.Net.NetworkCredential`オブジェクトを使用して、`Credentials` プロパティを設定します。

1. 削除するリソースの URI の指定

   取得するリソースの URI を指定します。この場合、`testResourceToBeDeleted` という名前のリソースが `testFolder` という名前のフォルダーにあるので、その URI は `"/testFolder/testResourceToBeDeleted"` です。この例では、リソースはまずリポジトリに書き込まれ、それから URI が取得されます。リソースの書き込みについて詳しくは、[リソースの書き込み](aem-forms-repository.md#writing-resources)を参照してください。

1. リソースの削除

   `RepositoryServiceService`オブジェクトの`deleteResources` メソッドを呼び出し、リソースの URI を含む`System.String`配列を最初のパラメーターとして渡してください。2 番目のパラメーターには `null` を渡します。

**関連トピック**

[リソースの削除](aem-forms-repository.md#deleting-resources)

[Base64 エンコーディングを使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
