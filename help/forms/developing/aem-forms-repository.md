---
title: AEM Formsリポジトリの操作
seo-title: AEM Formsリポジトリの操作
description: 'null'
seo-description: 'null'
uuid: 6ead49f9-ca0d-4ee4-86a6-0a9ced6ec4f8
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d2c95881-6c02-4e34-85af-84607df54287
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Working with AEM Forms Repository {#working-with-aem-forms-repository}

**Repositoryサービスについて**

Repositoryサービスは、AEM Formsにリソースストレージと管理サービスを提供します。 When developers create an *AEM Forms* application, they can deploy the assets in the repository instead of the file system. アセットには、XML 形式、PDF 形式（Acrobat 形式を含む）、フォームのフラグメント、画像、プロファイル、ポリシー、SWF ファイル、DDX ファイル、XML スキーマ、WSDL ファイルおよびテストデータなど、任意のタイプのコラテラルが含まれます。

例えば、次のFormsアプリケーション( *Applications/FormsApplication*)を考えます。

![ww_ww_formrepository](assets/ww_ww_formrepository.png)

FormsFolder内にLoan.xdpという名前のファイルがあることに注意してください。 このフォームデザインにアクセスするには、次の完全なパス（バージョンを含む）を指定します。 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.

>[!NOTE]
>
>Workbenchを使用したFormsアプリケーションの作成について詳しくは、Workbenchヘルプを [参照してくださ](https://www.adobe.com/go/learn_aemforms_workbench_63)い。

AEM Formsリポジトリ内のリソースへのパスは次のとおりです。

`Applications/Application-name/Application-version/Folder.../Filename`

次に、URI値の例を示します。

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

>[!NOTE]
>
>AEM FormsリポジトリはWebブラウザーを使用して参照できます。 リポジトリを参照するには、Webブラウザーhttps://[server name]:[server port]/repositoryに次のURLを入力します。 「AEM Formsリポジトリでの作業」セクションに関連付けられているクイックスタート結果は、Webブラウザーを使用して確認できます。 例えば、AEM Formsリポジトリにコンテンツを追加すると、Webブラウザーでそのコンテンツを表示できます。 (See [Quick Start (SOAP mode): Writing a resource using the Java API](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api).)

リポジトリAPIは、リポジトリに情報を保存し、リポジトリから情報を取得するために使用できる多くの操作を提供します。 例えば、リソースのリストを取得したり、アプリケーションの処理の一部としてリソースが必要な場合にリポジトリに保存される特定のリソースを取得したりできます。

>[!NOTE]
>
>リポジトリAPIを使用してContent Services（非推奨）とやり取りすることはできません。 Content Services（非推奨）とやり取りするには、Document Management APIを使用します。

RepositoryサービスAPIを使用して、次のタスクを実行できます。

* フォルダーの作成. 「フォルダ [の作成」を参照してください](aem-forms-repository.md#creating-folders)。
* リソースとそのプロパティを書き込みます。 Writing [Resourcesを参照してください](aem-forms-repository.md#writing-resources)。
* 特定のコレクション内または他のリソースに関連するリソースを一覧表示します。 Listing Resourcesを参 [照してください](aem-forms-repository.md#listing-resources)。
* リソースとそのプロパティを読み取ります。 Reading Resourcesを参 [照してください](aem-forms-repository.md#reading-resources)。
* リソースとそのプロパティを更新します。 Updating [Resourcesを参照してください](aem-forms-repository.md#updating-resources)。
* 履歴、関連リソース、プロパティなどのリソースを検索します。 Searching for [Resourcesを参照してください](aem-forms-repository.md#searching-for-resources)。
* リソース間の関係を指定します。 「リソース [の関係の作成」を参照してくださ](aem-forms-repository.md#creating-resource-relationships)い。
* リソースのロックとロック解除、アクセス制御リスト(ACL)の読み取りと書き込みなど、リソースアクセス制御を管理します。 Locking [Resourcesを参照してください](aem-forms-repository.md#locking-resources)。
* リソースとそのプロパティを削除します。 Deleting [Resourcesを参照してください](aem-forms-repository.md#deleting-resources)。

>[!NOTE]
>
>リポジトリAPIを使用して、リソースアクセス制御の管理、リソースの検索、ECMリポジトリを使用したリソースの関係の指定を行うことはできません。

>[!NOTE]
>
>暗号化されたPDFがリポジトリに書き込まれると、自動関係抽出機能を使用できません。 そうしないと、暗号化されたPDFをリポジトリに保存し、後で取得できます。 取得側は、PDFがリポジトリから取得された後に、そのPDFを復号化することを選択できます。

>[!NOTE]
>
>For more information about the Repository service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## フォルダーの作成 {#creating-folders}

フォルダー（リソースコレクション）は、オブジェクト（ファイルまたはリソース）を整理されたグループに格納するために使用します。 フォルダーには、リソースやサブフォルダーとも呼ばれる他のフォルダーを含めることができます。 リソースは一度に1つのフォルダーにしか保存できません。

ファイルは、フォルダーからアクセス制御リスト(ACL)を継承し、サブフォルダーは親フォルダーからACLを継承します。 したがって、子フォルダーを作成する前に親フォルダーが存在する必要があります。 IDEでは、フォルダごとの操作のみが可能で、ファイルごとの操作はできません。 フォルダのバージョンを設定することはできません。また、バージョンを設定する必要はありません。フォルダーにはデータ自体が含まれていません。 データを含むリソースのコンテナにすぎません。 デフォルトのACLはシステムレベルの権限です。つまり、ユーザーが特定のフォルダーに対する権限を与えるまで、ユーザーはシステムレベルの権限（読み取り、書き込み、トラバース、ACLの管理）を持つ必要があります。 ACLはIDEでのみ機能します。

>[!NOTE]
>
>For more information about the Repository service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary-of-steps}

フォルダを作成するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. サービスクライアントを作成します。
1. フォルダーを作成します。
1. フォルダーをリポジトリに書き込みます。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを含めます。

**サービスクライアントの作成**

プログラムを使用してリソースコレクションを作成する前に、接続を確立し、資格情報を提供する必要があります。 これは、サービスクライアントを作成することで実現されます。

**フォルダーの作成**

Repositoryサービスメソッドを呼び出して、リソースコレクションを作成し、UUID、フォルダー名、説明などの識別情報をリソースコレクションに入力します。

**リポジトリへのフォルダーの書き込み**

Repositoryサービスメソッドを呼び出して、ターゲットフォルダーのURIを指定してリソースコレクションを書き込みます。

**関連トピック**

[Java APIを使用したフォルダーの作成](aem-forms-repository.md#create-folders-using-the-java-api)

[WebサービスAPIを使用したフォルダーの作成](aem-forms-repository.md#create-folders-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Repository Service APIクイックスタート](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java APIを使用したフォルダーの作成 {#create-folders-using-the-java-api}

RepositoryサービスAPI(Java)を使用してフォルダーを作成します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスにプロジェクトファイルを含めます。

1. サービスクライアントの作成

   コンストラク `ResourceRepositoryClient` ターを使用し、接続プロパティを含むオブジェクトを渡 `ServiceClientFactory` して、オブジェクトを作成します。

1. フォルダーの作成

   リソースコレクションを作成するには、まずオブジェクトを作成する必要が `com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean` あります。

   オブジェクト `repositoryInfomodelFactoryBean` のメソッドを `newResourceCollection` 呼び出し、次のパラメーターを渡します。

   * リソ `com.adobe.repository.infomodel.Id` ースに割り当てるUUID識別子。
   * リソ `com.adobe.repository.infomodel.Lid` ースに割り当てるUUID識別子。
   * リソ `java.lang.String` ースコレクションの名前を含む。 For example, `FormsFolder`.
   このメソッドは、新しいフォ `com.adobe.repository.infomodel.bean.ResourceCollection` ルダーを表すオブジェクトを返します。

   このメソッドを使用してフォルダーの説明を設定し、次 `setDescription` のパラメーターを渡します。

   * リソー `String` スコレクションを記述する。 この例では、 `"test Folder"` を使用します `.`


1. リポジトリへのフォルダーの書き込み

   オブジェクト `ResourceRepositoryClient` のメソッ `writeResource` ドを呼び出し、フォルダーとオブジェクトのURIを渡 `ResourceCollection` します。 例えば、フォルダーへのURIは次の値になります `/Applications/FormsApplication/1.0/`。

   このメソッドは、新しく作成されたオブジェクトのインスタンスを返 `com.adobe.repository.infomodel.bean.Resource` します。 例えば、オブジェクトのメソッドを呼び出して、新しいリソースの識別子の値を取 `com.adobe.repository.infomodel.bean.Resource` 得することがで `getId` きます。

**関連トピック**

[フォルダーの作成](aem-forms-repository.md#creating-folders)

[クイックスタート（SOAPモード）:Java APIを使用したフォルダーの作成](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-a-folder-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したフォルダーの作成 {#create-folders-using-the-web-service-api}

RepositoryサービスAPI（Webサービス）を使用してフォルダーを作成します。

1. プロジェクトファイルを含める

   * base64を使用してリポジトリWSDLを使用するMicrosoft .NETクライアントアセンブリを作成します。
   * Microsoft .NETクライアントアセンブリを参照します。

1. サービスクライアントの作成

   Microsoft .NETクライアントアセンブリを使用して、デフォルトのコンストラクタ `RepositoryServiceService` ーを呼び出してオブジェクトを作成します。 ユーザー名とパ `Credentials` スワードを含むオ `System.Net.NetworkCredential` ブジェクトを使用して、プロパティを設定します。

1. フォルダーの作成

   クラスのデフォルトのコンストラクターを使用し、次のパ `ResourceCollection` ラメーターを渡してフォルダーを作成します。

   * オブジ `Id` ェクト。クラスのデフォルトコンストラクターを呼び出して作成され、オ `Id` ブジェクトのフィールドに割 `Resource` り当てられ `id` ます。
   * オブジ `Lid` ェクト。クラスのデフォルトコンストラクターを呼び出して作成され、オ `Lid` ブジェクトのフィールドに割 `Resource` り当てられ `lid` ます。
   * オブジェクトのフィールドに割り当てられるリソースコレクションの名 `Resource` 前を含む文字 `name` 列です。 この例で使用される名前はです `"testfolder"`。
   * オブジェクトのフィールドに割り当てられるリソースコレクションの説 `Resource` 明を含む文字列 `description` です。 この例で使用される説明はです `"test folder"`。

1. リポジトリへのフォルダーの書き込み

   オブジェクト `RepositoryServiceService` のメソッドを呼 `writeResource` び出し、次のパラメーターを渡します。

   * フォルダーを作成するパス。
   * フォルダ `ResourceCollection` ーを表すオブジェクトです。
   * 他の2つ `null` のパラメーターに対して渡します。

**関連トピック**

[フォルダーの作成](aem-forms-repository.md#creating-folders)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## リソースの書き込み {#writing-resources}

リポジトリ内の特定の場所にリソースを作成できます。 自然なファイルサイズは、データベースの制限やセッションタイムアウトの影響を受けます。 デフォルトの設定では、ファイルのサイズは25 MBに制限されます。 最大ファイルサイズを増減するには、データベース設定を変更する必要があります。

リソースの書き込みは、リポジトリにデータを格納するのと同じです。 リポジトリにリソースを書き込むと、リポジトリエコシステム内のすべてのクライアントがそのリソースにアクセスできるようになります。 XMLスキーマ、XDPファイル、XSDファイルなどのリソースをリポジトリに書き込むと、MIMEタイプに基づいてコンテンツが解析されます。 MIMEタイプがサポートされている場合、パーサーは他のコンテンツとの暗黙の関係があるかどうかを判断します。 例えば、カスケーディングスタイルシート(CSS)に共通のCSSを参照する相対URLがある場合、共通のCSSもリポジトリに送信する必要があります。 2つのリソース間の関係は、30日間の非調整期間に対する保留中の関係として保存されます。 共通のCSSを30日以内にリポジトリに送信すると、関係が形成されます。

リソースを作成すると、アクセス制御リスト(ACL)は親フォルダーから継承されます。 ルートフォルダーには、最初のリソースまたはフォルダーが作成されるまで、システムレベルの権限があります。この時点で、リソースまたはフォルダーにデフォルトのACL権限が付与されます。

RepositoryサービスのJava APIまたはWebサービスのAPIを使用して、プログラムでリソースを書き込むことができます。

>[!NOTE]
>
>For more information about the Repository service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-1}

リソースを書き込むには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. Repositoryサービスクライアントを作成します。
1. 読み取るリソースのURIを指定します。
1. リソースを読み取ります。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを含めます。

**サービスクライアントの作成**

プログラムでリソースを読み取る前に、接続を確立し、資格情報を提供する必要があります。 これは、サービスクライアントを作成することで実現されます。

**リソースのターゲットフォルダーのURIを指定します**

読み取るリソースのURIを含む文字列を作成します。 この構文には、次の例のようにスラッシュが含まれます。&quot;/*path*/*folder*&quot;

**リソースの作成**

Repositoryサービスメソッドを呼び出して、リソースを作成し、UUID、リソース名、説明などの識別情報をリソースに入力します。

**リソースコンテンツの指定**

Repositoryサービスメソッドを呼び出して、リソースコンテンツを作成し、そのコンテンツをリソースに保存します。

**ターゲットフォルダーにリソースを書き込みます**

ターゲットフォルダーのURIを指定してリソースを書き込むには、Repositoryサービスメソッドを呼び出します。

**関連トピック**

[Java APIを使用したリソースの書き込み](aem-forms-repository.md#write-resources-using-the-java-api)

[WebサービスAPIを使用したリソースの書き込み](aem-forms-repository.md#write-resources-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Repository Service APIクイックスタート](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java APIを使用したリソースの書き込み {#write-resources-using-the-java-api}

RepositoryサービスAPI(Java)を使用してリソースを書き込みます。

1. プロジェクトファイルを含める

   JavaプロジェクトのクラスパスにクライアントJARファイルを含めます。

1. サービスクライアントの作成

   コンストラク `ResourceRepositoryClient` ターを使用し、接続プロパティを含むオブジェクトを渡 `ServiceClientFactory` して、オブジェクトを作成します。

1. リソースのターゲットフォルダーのURIを指定します

   リソースのターゲットフォルダーのURIを指定します。 この場合、という名前のリソースはとい `testResource` う名前のフォルダーに保存され `testFolder`るので、フォルダーのURIはとなりま `"/testFolder"`す。 URIはオブジェクトとして保存さ `java.lang.String` れます。

1. リソースの作成

   リソースを作成するには、まずオブジェクトを作成する必要があ `com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean` ります。

   オブジェクトの `RepositoryInfomodelFactoryBean` メソッドを呼び出し `newResource` ます。これにより、オブジェクトが作成 `com.adobe.repository.infomodel.bean.Resource` されます。 この例では、次のパラメーターが提供されます。

   * オブジ `com.adobe.repository.infomodel.Id` ェクト。クラスのデフォルトコンストラクターを呼び出して作成さ `Id` れます。
   * オブジ `com.adobe.repository.infomodel.Lid` ェクト。クラスのデフォルトコンストラクターを呼び出して作成さ `Lid` れます。
   * リソ `java.lang.String` ースのファイル名を含む。
   リソースの説明を指定するには、オブジェクトのメソ `Resource` ッドを呼び出 `setDescription` し、説明を含む文字列を渡します。 この例では、説明はです `"test resource"`。

1. リソースコンテンツの指定

   リソースのコンテンツを作成するには、オブジェクト `RepositoryInfomodelFactoryBean` のメソッドを呼び出 `newResourceContent` し、オブジェクトを返 `com.adobe.repository.infomodel.bean.ResourceContent` します。 Add content to the `ResourceContent` object. この例では、次のタスクを実行することで実現します。

   * オブジェクト `ResourceContent` のメソッドを呼び `setDataDocument` 出し、オブジェクトを渡 `com.adobe.idp.Document` す
   * オブジェクト `ResourceContent` のメソッドを呼 `setSize` び出して、オブジェクトのサイズをバイト単位で渡 `Document` す
   オブジェクトのメソッドを呼び出し、オブジェクト `Resource` を渡すことによ `setContent` って、コンテンツをリソースに追加 `ResourceContent` します。 For more information, see [AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. ターゲットフォルダーにリソースを書き込みます

   オブジェクト `ResourceRepositoryClient` のメソッド `writeResource` を呼び出し、フォルダーのURIとオブジェクトを渡し `Resource` ます。

**関連トピック**

[リソースの書き込み](aem-forms-repository.md#writing-resources)

[クイックスタート（SOAPモード）:Java APIを使用したリソースの書き込み](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したリソースの書き込み {#write-resources-using-the-web-service-api}

RepositoryサービスAPI（Webサービス）を使用してリソースを書き込みます。

1. プロジェクトファイルを含める

   * base64を使用してリポジトリWSDLを使用するMicrosoft .NETクライアントアセンブリを作成します。
   * Microsoft .NETクライアントアセンブリを参照します。

1. サービスクライアントの作成

   Microsoft .NETクライアントアセンブリを使用して、デフォルトのコンストラクタ `RepositoryServiceService` ーを呼び出してオブジェクトを作成します。 ユーザー名とパ `Credentials` スワードを含むオ `System.Net.NetworkCredential` ブジェクトを使用して、プロパティを設定します。

1. リソースのターゲットフォルダーのURIを指定します

   リソースのターゲットフォルダーのURIを指定します。 この場合、という名前のリソースはとい `testResource` う名前のフォルダーに保存され `testFolder`るので、フォルダーのURIはとなりま `"/testFolder"`す。 Microsoft .NET Framework（C#など）に準拠した言語を使用する場合は、URIをオブジェクトに格納し `System.String` ます。

1. リソースの作成

   リソースを作成するには、クラスのデフォルトコンストラクターを呼び出 `Resource` します。 この例では、次の情報がオブジェクトに格納され `Resource` ます。

   * オブジ `com.adobe.repository.infomodel.Id` ェクト。クラスのデフォルトコンストラクターを呼び出して作成され、オ `Id` ブジェクトのフィールドに割 `Resource` り当てられ `id` ます。
   * オブジ `com.adobe.repository.infomodel.Lid` ェクト。クラスのデフォルトコンストラクターを呼び出して作成され、オ `Lid` ブジェクトのフィールドに割 `Resource` り当てられ `lid` ます。
   * オブジェクトのフィールドに割り当てられる、リソースのファイル名を `Resource` 含む文字列 `name` です。 この例で使用される名前はです `"testResource"`。
   * オブジェクトのフィールドに割り当てられるリソースの説明を `Resource` 含む文字列 `description` です。 この例で使用される説明はです `"test resource"`。

1. リソースコンテンツの指定

   リソースのコンテンツを作成するには、クラスのデフォルトのコンストラクターを呼び出 `ResourceContent` します。 次に、オブジェクトにコンテンツを追 `ResourceContent` 加します。 この例では、次のタスクを実行することで実現します。

   * ドキュメント `BLOB` を含むオブジェクトをオブジェクトのフィー `ResourceContent` ルドに割り当て `dataDocument` ます。
   * オブジェクトのフィールドにオブ `BLOB` ジェクトのサイズをバ `ResourceContent` イト単位で割り当 `size` てます。
   オブジェクトのフィールドにオブジェクトを割り当て `ResourceContent` て、コンテンツ `Resource` をリソースに追加 `content` します。

1. ターゲットフォルダーにリソースを書き込みます

   オブジェクト `RepositoryServiceService` のメソッド `writeResource` を呼び出し、フォルダーのURIとオブジェクトを渡し `Resource` ます。 他の2つ `null` のパラメーターに対して渡します。

**関連トピック**

[リソースの書き込み](aem-forms-repository.md#writing-resources)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## リソースの一覧表示 {#listing-resources}

リソースを一覧表示することで、リソースを見つけることができます。 リポジトリに対してクエリーが実行され、特定のリソース収集に関連するすべてのリソースが検索されます。

リソースを整理したら、オペレーティングシステムと同様に、構造の特定のブランチを表示して、作成した構造を調べることができます。

リソースのリストは、次の関係によって機能します。リソースは、フォルダーのメンバーです。 メンバーシップは、「メンバー」型の関係で表されます。 特定のフォルダー内のリソースを一覧表示する場合、「メンバー」の関係によって特定のフォルダーに関連するリソースを照会します。 関係は方向性を持ちます。関係のメンバーは、ターゲットのメンバーであるソースを持ちます。 その源は資源である。ターゲットは親フォルダーです。

>[!NOTE]
>
>For more information about the Repository service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-2}

リソースを一覧表示するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. サービスクライアントを作成します。
1. フォルダーパスを指定します。
1. リソースのリストを取得します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを含めます。

**サービスクライアントの作成**

プログラムを使用してリソースコレクションを作成する前に、接続を確立し、資格情報を提供する必要があります。 これは、サービスクライアントを作成することで実現されます。

**フォルダーパスの指定**

リソースを含むフォルダーのパスを含む文字列を作成します。 この構文には、次の例のようにスラッシュが含まれます。&quot;/*path*/*folder*&quot;

**リソースのリストの取得**

ターゲットフォルダーのパスを指定してリソースのリストを取得するには、Repositoryサービスメソッドを呼び出します。

**関連トピック**

[Java APIを使用したリソースの一覧表示](aem-forms-repository.md#list-resources-using-the-java-api)

[WebサービスAPIを使用したリソースの一覧表示](aem-forms-repository.md#list-resources-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Repository Service APIクイックスタート](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java APIを使用したリソースの一覧表示 {#list-resources-using-the-java-api}

RepositoryサービスAPI(Java)を使用してリソースを一覧表示します。

1. プロジェクトファイルを含める

   JavaプロジェクトのクラスパスにクライアントJARファイルを含めます。

1. サービスクライアントの作成

   コンストラク `ResourceRepositoryClient` ターを使用し、接続プロパティを含むオブジェクトを渡 `ServiceClientFactory` して、オブジェクトを作成します。

1. フォルダーパスの指定

   照会するリソースコレクションのURIを指定します。 この場合、URIはです `"/testFolder"`。 URIはオブジェクトとして保存さ `java.lang.String` れます。

1. リソースのリストの取得

   オブジェクト `ResourceRepositoryClient` のメソッ `listMembers` ドを呼び出し、フォルダーのURIを渡します。

   このメソッドは、タイ `java.util.List` プのソ `com.adobe.repository.infomodel.bean.Resource` ースであり、ターゲットとしてリ `com.adobe.repository.infomodel.bean.Relation` ソー `Relation.TYPE_MEMBER_OF` スコレクションURIを持つオブジェクトのを返します。 これを繰り返し実行して、各リ `List` ソースを取得することができます。 この例では、各リソースの名前と説明が表示されます。

**関連トピック**

[リソースの一覧を参照してください](aem-forms-repository.md#listing-resources)。

[クイックスタート（SOAPモード）:Java APIを使用したリソースの一覧表示](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-listing-resources-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したリソースの一覧表示 {#list-resources-using-the-web-service-api}

RepositoryサービスAPI（Webサービス）を使用して、リソースを一覧表示します。

1. プロジェクトファイルを含める

   * リポジトリWSDLを使用するMicrosoft .NETクライアントアセンブリを作成します。
   * Microsoft .NETクライアントアセンブリを参照します。

1. サービスクライアントの作成

   Microsoft .NETクライアントアセンブリを使用して、デフォルトのコンストラクタ `RepositoryServiceService` ーを呼び出してオブジェクトを作成します。 ユーザー名とパ `Credentials` スワードを含むオ `System.Net.NetworkCredential` ブジェクトを使用して、プロパティを設定します。

1. フォルダーパスの指定

   照会するフォルダーのURIを含む文字列を指定します。 この場合、URIはです `"/testFolder"`。 Microsoft .NET Frameworkに準拠した言語（C#など）を使用する場合は、URIをオブジェクトに格納し `System.String` ます。

1. リソースのリストの取得

   オブジェクト `RepositoryServiceService` のメソッドを `listMembers` 呼び出し、フォルダーのURIを最初のパラメーターとして渡します。 他の2つ `null` のパラメーターに対して渡します。

   このメソッドは、オブジェクトにキャストできるオブジェクトの配列を返 `Resource` します。 オブジェクト配列を繰り返し処理して、関連する各リソースを取得できます。 この例では、各リソースの名前と説明が表示されます。

**関連トピック**

[リソースの一覧を参照してください](aem-forms-repository.md#listing-resources)。

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## リソースの読み取り {#reading-resources}

リポジトリ内の特定の場所からリソースを取得して、そのコンテンツとメタデータを読み取ることができます。 ワークフローは、初期化フォームによってフロントエンドになります。 プロセスには、フォームを読み取るために必要なすべての権限があります。 データ・フォームが取得され、リポジトリからコンテンツが読み取られます。 リポジトリは、コンテンツとメタデータへのアクセス権を付与します（リソースが存在することを知る機能）。

リポジトリには次の4つの権限タイプがあります。

* **traverse**:リソースをリストできます。つまり、リソースのメタデータを読み取るが、リソースのコンテンツは読み取らない
* **read**:リソースの内容を読み取ることができます。
* **write**:リソースコンテンツを書き込むことができます。
* **アクセス制御リスト(ACL)の管理**:リソース上のACLを操作できます。

ユーザーは、プロセスを実行する権限を持つ場合にのみプロセスを実行できます。 IDEユーザーは、リポジトリと同期するためにトラバースと読み取りの権限が必要です。 実行時はシステムコンテキスト内で発生するので、ACLはデザイン時にのみ適用されます。

RepositoryサービスのJava APIまたはWebサービスのAPIを使用して、プログラムでリソースを読み取ることができます。

>[!NOTE]
>
>For more information about the Repository service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-3}

リソースを読み取るには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. Repositoryサービスクライアントを作成します。
1. 読み取るリソースのURIを指定します。
1. リソースを読み取ります。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを含めます。

**サービスクライアントの作成**

プログラムでリソースを読み取る前に、接続を確立し、資格情報を提供する必要があります。 これは、サービスクライアントを作成することで実現されます。

**読み取るリソースのURIを指定します**

読み取るリソースのURIを含む文字列を作成します。 この構文には、次の例のようにスラッシュが含まれます。&quot;/*path*/*resource*&quot;

**リソースの読み取り**

URIを指定してリソースを読み取るには、Repositoryサービスメソッドを呼び出します。

**関連トピック**

[Java APIを使用したリソースの読み取り](aem-forms-repository.md#read-resources-using-the-java-api)

[WebサービスAPIを使用したリソースの読み取り](aem-forms-repository.md#reading-resources-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Repository Service APIクイックスタート](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java APIを使用したリソースの読み取り {#read-resources-using-the-java-api}

RepositoryサービスAPI(Java)を使用してリソースを読み取ります。

1. プロジェクトファイルを含める

   JavaプロジェクトのクラスパスにクライアントJARファイルを含めます。

1. サービスクライアントの作成

   コンストラク `ResourceRepositoryClient` ターを使用し、接続プロパティを含むオブジェクトを渡 `ServiceClientFactory` して、オブジェクトを作成します。

1. 読み取るリソースのURIを指定します

   取得するリソースのURIを表すstring値を指定します。 例えば、リソースの名前が *testFolder* (testFolder)という名前のフォルダーにあると仮定し *て*、を指定しま `/testFolder/testResource`す。

1. リソースの読み取り

   オブジェクト `ResourceRepositoryClient` のメソッドを `readResource` 呼び出し、リソースのURIをパラメーターとして渡します。 このメソッドは、リソー `Resource` スを表すインスタンスを返します。

**関連トピック**

[リソースの読み取り](aem-forms-repository.md#reading-resources)

[クイックスタート（SOAPモード）:Java APIを使用したリソースの読み取り](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-reading-a-resource-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したリソースの読み取り {#reading-resources-using-the-web-service-api}

RepositoryサービスAPI（Webサービス）を使用してリソースを読み取ります。

1. プロジェクトファイルを含める

   * リポジトリWSDLを使用するMicrosoft .NETクライアントアセンブリを作成します。 (Base64エンコ [ーディングを使用した.NETクライアントアセンブリの作成を参照](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding))。
   * Microsoft .NETクライアントアセンブリを参照します。 (Base64エンコ [ーディングを使用した.NETクライアントアセンブリの作成を参照](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding))。

1. サービスクライアントの作成

   Microsoft .NETクライアントアセンブリを使用して、デフォルトのコンストラクタ `RepositoryServiceService` ーを呼び出してオブジェクトを作成します。 ユーザー名とパ `Credentials` スワードを含むオ `System.Net.NetworkCredential` ブジェクトを使用して、プロパティを設定します。

1. 読み取るリソースのURIを指定します

   取得するリソースのURIを含む文字列を指定します。 この場合、という名前のリソースはという名 `testResource` 前のフォルダー内にあるので、 `testFolder`そのURIはです `"/testFolder/testResource"`。 Microsoft .NET Framework（C#など）に準拠した言語を使用する場合は、URIをオブジェクトに格納し `System.String` ます。

1. リソースの読み取り

   オブジェクト `RepositoryServiceService` のメソッドを `readResource` 呼び出し、リソースのURIを最初のパラメーターとして渡します。 他の2つ `null` のパラメーターに対して渡します。

**関連トピック**

[リソースの読み取り](aem-forms-repository.md#reading-resources)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## リソースの更新 {#updating-resources}

リポジトリ内のリソースのコンテンツを取得して更新できます。 リソースを更新しても、これらのリソースへのアクセス制御はバージョン間で変わりません。 更新を実行する場合、メジャーバージョンを増分するオプションがあります。 メジャーバージョンを増分しない場合は、マイナーバージョンが自動的に更新されます。

リソースを更新すると、指定したリソース属性に基づいて新しいバージョンが作成されます。 リソースを更新する場合は、次の2つの重要なパラメータを指定します。ターゲットURIと、更新されたすべてのメタデータを含むリソースインスタンス。 特定の属性（名前など）を変更しない場合でも、渡すインスタンスで属性が必要になることに注意してください。 コンテンツの解析時に作成される関係は、特定のバージョンに追加され、特に指定がない限り転送されません。

例えば、XDPファイルを更新し、そのXDPファイルに他のリソースへの参照が含まれている場合、それらの追加参照も記録されます。 form.xdpバージョン1.0に2つの外部参照があるとします。ロゴとスタイルシートを作成し、その後form.xdpを更新して、3つの参照を持つようにします。ロゴ、スタイルシート、スキーマファイル。 更新中、リポジトリは3番目の関係（スキーマファイル）を保留中の関係テーブルに追加します。 スキーマファイルがリポジトリに存在する場合は、関係が自動的に形成されます。 ただし、form.xdpバージョン2.0でロゴが使用されなくなった場合、form.xdpバージョン2.0はロゴとの関係を持ちません。

すべての更新操作は、アトミックおよびトランザクションです。 例えば、2人のユーザーが同じリソースを読み、両方でバージョン1.0をバージョン2.0に更新すると、どちらかが成功し、一方が失敗すると、リポジトリの整合性が維持され、両方が成功または失敗を確認するメッセージを受け取ります。 トランザクションがコミットされない場合は、データベース障害が発生した場合にロールバックされ、アプリケーションサーバーに応じてタイムアウトまたはロールバックされます。

RepositoryサービスのJava APIまたはWebサービスAPIを使用して、プログラムでリソースを更新できます。

>[!NOTE]
>
>For more information about the Repository service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-4}

リソースを更新するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. Repositoryサービスクライアントを作成します。
1. 更新するリソースを取得します。
1. リソースを更新します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを含めます。

**サービスクライアントの作成**

プログラムでリソースを読み取る前に、接続を確立し、資格情報を提供する必要があります。 これは、サービスクライアントを作成することで実現されます。

**更新するリソースを取得します**

リソースを読み取ります。 詳しくは、「リソースの読み取り」を [参照してください](aem-forms-repository.md#reading-resources)。

**リソースの更新**

リソースに新しい情報を設定し、Repositoryサービスメソッドを呼び出して、リソースを更新し、URI、更新されたリソース、およびバージョン情報の更新方法を指定します。

**関連トピック**

[Java APIを使用したリソースの更新](aem-forms-repository.md#update-resources-using-the-java-api)

[WebサービスAPIを使用したリソースの更新](aem-forms-repository.md#update-resources-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Repository Service APIクイックスタート](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java APIを使用したリソースの更新 {#update-resources-using-the-java-api}

RepositoryサービスAPI(Java)を使用してリソースを更新します。

1. プロジェクトファイルを含める

   JavaプロジェクトのクラスパスにクライアントJARファイルを含めます。

1. サービスクライアントの作成

   コンストラク `ResourceRepositoryClient` ターを使用し、接続プロパティを含むオブジェクトを渡 `ServiceClientFactory` して、オブジェクトを作成します。

1. 更新するリソースを取得します

   リソースを取得して読み取るリソースのURIを指定します。 この例では、リソースのURIはです `"/testFolder/testResource"`。

1. リソースの更新

   オブジェクト `Resource` の情報を更新します。 この例では、説明を更新するには、オブジェクトのメソッ `Resource` ドを呼び出 `setDescription` し、新しい説明文字列をパラメーターとして渡します。

   次に、オブジェクト `ServiceClientFactory` のメソッドを呼 `updateResource` び出し、次のパラメーターを渡します。

   * リソ `java.lang.String` ースのURIを含むオブジェクト。
   * 更新され `Resource` たリソース情報を含むオブジェクトです。
   * メジャ `boolean` ーバージョンを更新するか、マイナーバージョンを更新するかを示す値。 この例では、メジャーバージ `true` ョンの値を増分することを示す値が渡されます。

**関連トピック**

[リソースの更新](aem-forms-repository.md#updating-resources)

[クイックスタート（SOAPモード）:Java APIを使用したリソースの更新](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-updating-a-resource-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したリソースの更新 {#update-resources-using-the-web-service-api}

Repository API（Webサービス）を使用してリソースを更新します。

1. プロジェクトファイルを含める

   * リポジトリWSDLを使用するMicrosoft .NETクライアントアセンブリを作成します。
   * Microsoft .NETクライアントアセンブリを参照します。

1. サービスクライアントの作成

   Microsoft .NETクライアントアセンブリを使用して、デフォルトのコンストラクタ `RepositoryServiceService` ーを呼び出してオブジェクトを作成します。 ユーザー名とパ `Credentials` スワードを含むオ `System.Net.NetworkCredential` ブジェクトを使用して、プロパティを設定します。

1. 更新するリソースを取得します

   取得するリソースのURIを指定し、リソースを読み取ります。 この例では、リソースのURIはです `"/testFolder/testResource"`。 詳しくは、「リソースの読み取り」を [参照してください](aem-forms-repository.md#reading-resources)。

1. リソースの更新

   オブジェクト `Resource` の情報を更新します。 この例では、説明を更新するには、オブジェクトのフィールドに新しい値 `Resource` を割り当て `description` ます。

1. オブジェクト `RepositoryServiceService` のメソッドを `updateResource` 呼び出し、次のパラメーターを渡します。

   * リソ `System.String` ースのURIを含むオブジェクト。
   * 更新され `Resource` たリソース情報を含むオブジェクトです。
   * メジャ `boolean` ーバージョンを更新するか、マイナーバージョンを更新するかを示す値。 この例では、メジャーバージ `true` ョンの値を増分することを示す値が渡されます。
   * 残りの2 `null` つのパラメーターに対して渡します。

**関連トピック**

[リソースの更新](aem-forms-repository.md#updating-resources)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## リソースの検索 {#searching-for-resources}

リポジトリ内のリソース（履歴、関連リソース、プロパティなど）の検索に使用するクエリーを作成できます。

関連するリソースを取得して、フォームとそのフラグメント間の依存関係を判断できます。 例えば、フォームに使用するフラグメントや外部リソースを指定できます。 画像がある場合は、その画像を使用するフォームも確認できます。 また、プロパティに基づくフィルタリングを使用して、関連するリソースを検索することもできます。 例えば、指定した名前の画像を使用するすべてのフォームを検索したり、指定した名前のフォームで使用されている画像を検索したりできます。 また、リソースプロパティを使用して検索することもできます。 例えば、「%」や「_」のワイルドカードを含む特定の文字列で始まる名前を持つすべてのフォームまたはリソースを検索するクエリーを実行できます。 プロパティに基づく検索は関係に基づくものではないことに注意してください。このような検索は、特定のリソースに関する特定の知識を持つことを前提としています。

**クエリ文**

クエリ *ーには* 、条件と論理結合された1つ以上のステートメントが含まれます。 ステ *ートメント* は、左オペランド、演算子、右オペランドで構成されます。 また、検索結果に使用する並べ替え順を指定できます。 ソート *順は*`ORDER BY` 、SQL句と同等の情報を含み、検索の基となった属性と、昇順または降順のどちらを使用するかを示す値で構成されます。

RepositoryサービスのJava APIを使用して、プログラムでリソースを検索できます。 現時点では、WebサービスAPIを使用してリソースを検索することはできません。

**並べ替え動作**

オブジェクトのメソッドを呼び出し、並べ替え順 `ResourceRepositoryClient` 序を指定する `searchProperties` 場合、並べ替え順序は考慮されません。 例えば、属性名が、、およびの3つのカスタムプロパティを持つリソースを作成すると `name`し `secondName`ます `asecondName`。 次に、属性名にソート順要素を作成し、値をに設定 `ascending` します `true`。

次に、オブジェクト `ResourceRepositoryClient` のメソッドを呼び `searchProperties` 出し、並べ替え順で渡します。 検索は、3つのプロパティを持つ正しいリソースを返します。 ただし、プロパティは属性名で並べ替えられません。 追加された順に返されます。 `name`、 `secondName`、、 `asecondName`、

>[!NOTE]
>
>For more information about the Repository service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-5}

リソースを検索するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. Repositoryサービスクライアントを作成します。
1. 検索の対象フォルダを指定します。
1. 検索で使用する属性を指定します。
1. 検索で使用するクエリを作成します。
1. 検索結果の並べ替え順を作成します。
1. リソースを検索します。
1. 検索結果からリソースを取得します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを含めます。

**サービスクライアントの作成**

プログラムでリソースを読み取る前に、接続を確立し、資格情報を提供する必要があります。 これは、サービスクライアントを作成することで実現されます。

**検索の対象フォルダーの指定**

検索の実行元となるベースパスを含む文字列を作成します。 この構文には、次の例のようにスラッシュが含まれます。&quot;/*path*/*folder*&quot;

**検索で使用する属性を指定する**

リソースに含まれる属性を基に検索を行うことができます。 検索を実行する属性の値を指定します。

**検索で使用するクエリを作成します**

ステートメントと条件を使用してクエリーを作成します。 各文は、検索の基となる属性、使用条件、および検索で使用する属性値を指定します。

**検索結果の並べ替え順序の作成**

並べ替え順は、要素で構成され、各要素には、検索で使用される属性の1つと、昇順または降順のどちらを使用するかを示す値が含まれます。

**リソースの検索**

フォルダー、クエリー、並べ替え順を使用してリソースを検索します。 さらに、検索の深さと、返される結果数の上限を示します。

**検索結果からのリソースの取得**

返されたリソースのリストを繰り返し処理し、情報を抽出して処理します。

**関連トピック**

[Java APIを使用したリソースの検索](aem-forms-repository.md#search-for-resources-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Repository Service APIクイックスタート](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java APIを使用したリソースの検索 {#search-for-resources-using-the-java-api}

RepositoryサービスAPI(Java)を使用してリソースを検索します。

1. プロジェクトファイルを含める

   JavaプロジェクトのクラスパスにクライアントJARファイルを含めます。

1. サービスクライアントの作成

   コンストラク `ResourceRepositoryClient` ターを使用し、接続プロパティを含むオブジェクトを渡 `ServiceClientFactory` して、オブジェクトを作成します。

1. 検索の対象フォルダーの指定

   検索を実行するベースパスのURIを指定します。 この例では、リソースのURIはです `/testFolder`。

1. 検索で使用する属性を指定する

   検索を実行する属性の値を指定します。 属性はオブジェクト内に存在 `com.adobe.repository.infomodel.bean.Resource` します。 この例では、name属性に対して検索が実行されます。したがって、オ `java.lang.String` ブジェクトの名 `Resource` 前を含む名前が使用されます。この場合 `testResource` はこの名前です。

1. 検索で使用するクエリを作成します

   クエリーを作成するには、クラスのデフォル `com.adobe.repository.query.Query` トのコンストラクターを呼び出し、クエリー `Query` にステートメントを追加して、オブジェクトを作成します。

   ステートメントを作成するには、クラスのコンストラクターを呼び出 `com.adobe.repository.query.Query.Statement` し、次のパラメーターを渡します。

   * リソース属性定数を含む左の演算値。 この例では、リソースの名前が検索の基になるので、静的な値が使用さ `Resource.ATTRIBUTE_NAME` れます。
   * 属性の検索で使用される条件を含む演算子。 演算子は、クラス内の静的定数の1つである必要があ `Query.Statement` ります。 この例では、静的な値が使用さ `Query.Statement.OPERATOR_BEGINS_WITH` れています。
   * 検索を実行する属性値を含む右オペランド。 この例では、値を含むname属性 `String` が使用さ `"testResource"`れます。
   オブジェクトのメソッドを呼び出し、クラスに含まれる静 `Query.Statement` 的値の1 `setNamespace` つを渡すことで、左の演算値の名前空間を指定し `com.adobe.repository.infomodel.bean.ResourceProperty` ます。 この例では、が使 `ResourceProperty.RESERVED_NAMESPACE_REPOSITORY` 用されます。

   オブジェクトのメソッドを呼び出し、オブジェク `Query` トを渡すことによ `addStatement` って、各ステートメントをクエリに追 `Query.Statement` 加します。

1. 検索結果の並べ替え順序の作成

   検索結果で使用する並べ替え順を指定するには、クラスのデフォルトコンストラクタ `com.adobe.repository.query.sort.SortOrder` ーを呼び出してオブジェクトを作成し、 `SortOrder` 並べ替え順に要素を追加します。

   並べ替え順序の要素を作成するには、クラスのコンストラクタの1つを呼び出 `com.adobe.repository.query.sort.SortOrder.Element` します。 この例では、リソースの名前が検索の基になるので、静的な値が最初のパラメーターとして使用され、昇順(値は `Resource.ATTRIBUTE_NAME``boolean``true`)が2番目のパラメーターとして指定されます。

   オブジェクトのメソッドを呼び出し、オブジェクトを `SortOrder` 渡すことで、各 `addSortElement` 要素をソート順に追加 `SortOrder.Element` します。

1. リソースの検索

   属性プロパティに `resources` 基づいて検索するには、オブジェクトの `ResourceRepositoryClient` メソッドを呼び `searchProperties` 出し、次のパラメーターを渡します。

   * 検索 `String` を実行するベースパスを含む。 この場合は、が使用 `"/testFolder"` されます。
   * 検索で使用されるクエリ。
   * 検索の深さ。 この場合、は、ベ `com.adobe.repository.infomodel.bean.ResourceCollection.DEPTH_INFINITE` ースパスとそのすべてのフォルダーが使用されることを示すために使用されます。
   * ペー `int` ジなし結果セットを選択する最初の行を示す値。 この例では、を指定 `0` しています。
   * 返さ `int` れる結果の最大数を示す値。 この例では、を指定 `10` しています。
   * 検索で使用される並べ替え順。
   このメソッドは、指定され `java.util.List` た並べ替え順 `Resource` でオブジェクトの1つを返します。

1. 検索結果からのリソースの取得

   検索結果に含まれるリソースを取得するには、を繰り返し実行し、各オブ `List` ジェクトをにキャストして、 `Resource` 情報を抽出します。 この例では、各リソースの名前が表示されます。

**関連トピック**

[リソースの検索](aem-forms-repository.md#searching-for-resources)

[クイックスタート（SOAPモード）:Java APIを使用したリソースの検索](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## リソースの関係の作成 {#creating-resource-relationships}

リポジトリ内のリソース間の関係を指定できます。 関係には次の3種類があります。

* **依存**:リソースが他のリソースに依存する関係。つまり、すべての関連リソースがリポジトリで必要になります。
* **メンバーシップ（ファイルシステム）**:特定のフォルダー内にリソースが存在する関係。
* **カスタム**:リソース間で指定する関係。 例えば、あるリソースが非推奨で、別のリソースがリポジトリに導入された場合、独自の置き換え関係を指定できます。

独自のカスタムリレーションシップを作成できます。 例えば、HTMLファイルをリポジトリに格納し、そのファイルが画像を使用する場合、HTMLファイルと画像を関連付けるカスタム関係を指定できます（通常はXMLファイルのみがリポジトリ定義の依存関係を使用して画像に関連付けられます）。 カスタム関係の別の例として、ツリー構造ではなく、循環グラフ構造を使用してリポジトリの別のビューを作成する場合が考えられます。 ビューアと共に円グラフを定義して、これらの関係を横断できます。 最後に、2つのリソースが完全に異なる場合でも、1つのリソースが別のリソースを置き換えることを示すことができます。 その場合は、予約範囲外の関係タイプを定義し、これら2つのリソース間の関係を作成できます。 アプリケーションは、関係を検出して処理できる唯一のクライアントであり、その関係に関する検索を実行するために使用できます。

RepositoryサービスのJava APIまたはWebサービスのAPIを使用して、リソース間の関係をプログラムで指定できます。

>[!NOTE]
>
>For more information about the Repository service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-6}

2つのリソース間の関係を指定するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. Repositoryサービスクライアントを作成します。
1. 関連するリソースのURIを指定します。
1. 関係を作成します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを含めます。

**サービスクライアントの作成**

プログラムでリソースを読み取る前に、接続を確立し、資格情報を提供する必要があります。 これは、サービスクライアントを作成することで実現されます。

**関連付けるリソースのURIの指定**

関連付けるリソースのURIを含む文字列を作成します。 この構文には、次の例のようにスラッシュが含まれます。&quot;/*path*/*resource*&quot;

**関係の作成**

Repositoryサービスメソッドを呼び出して、関係のタイプを作成し指定します。

**関連トピック**

[Java APIを使用した関係リソースの作成](aem-forms-repository.md#create-relationship-resources-using-the-java-api)

[WebサービスAPIを使用して関係リソースを作成する](aem-forms-repository.md#create-relationship-resources-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Repository Service APIクイックスタート](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java APIを使用した関係リソースの作成 {#create-relationship-resources-using-the-java-api}

RepositoryサービスJava APIを使用して関係リソースを作成し、次のタスクを実行します。

1. プロジェクトファイルを含める

   JavaプロジェクトのクラスパスにクライアントJARファイルを含めます。

1. サービスクライアントの作成

   コンストラク `ResourceRepositoryClient` ターを使用し、接続プロパティを含むオブジェクトを渡 `ServiceClientFactory` して、オブジェクトを作成します。

1. 関連付けるリソースのURIの指定

   関連するリソースのURIを指定します。 この場合、リソースは名前が付けられ、という名 `testResource1` 前のフォ `testResource2` ルダーに格納されるので、URI `testFolder`はとにな `"/testFolder/testResource1"` りま `"/testFolder/testResource2"`す。 URIはオブジェクトとして保存さ `java.lang.String` れます。 この例では、リソースが最初にリポジトリに書き込まれ、そのURIが取得されます。 リソースの作成の詳細については、「リソースの作成」を参 [照してください](aem-forms-repository.md#writing-resources)。

1. 関係の作成

   オブジェクト `ResourceRepositoryClient` のメソッドを呼 `createRelationship` び出し、次のパラメーターを渡します。

   * ソースリソースのURI。
   * ターゲットリソースのURI。
   * 関係のタイプ。クラス内の静的定数の1つ `com.adobe.repository.infomodel.bean.Relation` です。 この例では、値を指定して依存関係を確立します `Relation.TYPE_DEPENDANT_OF`。
   * 新し `boolean` い先頭リソースのベース識別子に対して、対象リソースが自 `com.adobe.repository.infomodel.Id`動的に更新されるか否かを示す値。 この例では、依存関係が原因で、値が指定さ `true` れています。
   また、オブジェクトのメソッドを呼び出し、次のパラメーターを渡すことで、特定のリソースに関連 `ResourceRepositoryClient` するリソースのリ `getRelated` ストを取得することもできます。

   * 関連リソースを取得するリソースのURI。 この例では、ソースリソース( `"/testFolder/testResource1"`)が指定されています。
   * 指定さ `boolean` れたリソースが関係のソースリソースであるかどうかを示す値。 この例では、値が指定されてい `true` ます。これは、この場合です。
   * クラス内の静的定数の1つである関係タイプ `Relation` です。 この例では、前述の例と同じ値を使用して、依存関係を指定します。 `Relation.TYPE_DEPENDANT_OF`.
   このメ `getRelated` ソッドは、関連す `java.util.List` る各リ `Resource` ソースを繰り返し取得し、に含まれるオブジェクトをキャストするためのオブジェクトを返し `List``Resource` ます。 この例では、が返さ `testResource2` れるリソースのリストに含まれていると想定されます。

**関連トピック**

[リソースの関係の作成](aem-forms-repository.md#creating-resource-relationships)

[クイックスタート（SOAPモード）:Java APIを使用したリソース間の関係の作成](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-relationships-between-resources-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用して関係リソースを作成する {#create-relationship-resources-using-the-web-service-api}

Repository API（Webサービス）を使用して関係リソースを作成します。

1. プロジェクトファイルを含める

   * リポジトリWSDLを使用するMicrosoft .NETクライアントアセンブリを作成します。
   * Microsoft .NETクライアントアセンブリを参照します。

1. サービスクライアントの作成

   Microsoft .NETクライアントアセンブリを使用して、デフォルトのコンストラクタ `RepositoryServiceService` ーを呼び出してオブジェクトを作成します。 ユーザー名とパ `Credentials` スワードを含むオ `System.Net.NetworkCredential` ブジェクトを使用して、プロパティを設定します。

1. 関連付けるリソースのURIの指定

   関連するリソースのURIを指定します。 この場合、リソースは名前が付けられ、という名 `testResource1` 前のフォ `testResource2` ルダーに格納されるので、URI `testFolder`はとにな `"/testFolder/testResource1"` りま `"/testFolder/testResource2"`す。 Microsoft .NET Framework（C#など）に準拠した言語を使用する場合、URIはオブジェクトとして保存され `System.String` ます。 この例では、リソースが最初にリポジトリに書き込まれ、そのURIが取得されます。 リソースの作成の詳細については、「リソースの作成」を参 [照してください](aem-forms-repository.md#writing-resources)。

1. 関係の作成

   オブジェクト `RepositoryServiceService` のメソッドを呼 `createRelationship` び出し、次のパラメーターを渡します。

   * ソースリソースのURI。
   * ターゲットリソースのURI。
   * 関係のタイプ。 この例では、値を指定して依存関係を確立します `3`。
   * 関係 `boolean` タイプが指定されたかどうかを示す値。 この例では、値が指定さ `true` れています。
   * 新し `boolean` い先頭リソースのベース識別子に対して、対象リソースが自 `Id`動的に更新されるか否かを示す値。 この例では、依存関係が原因で、値が指定さ `true` れています。
   * ターゲ `boolean` ットヘッドが指定されたかどうかを示す値。 この例では、値が指定さ `true` れています。
   * 最後のパ `null` ラメーターに渡します。
   また、オブジェクトのメソッドを呼び出し、次のパラメーターを渡すことで、特定のリソースに関連 `RepositoryServiceService` するリソースのリ `getRelated` ストを取得することもできます。

   * 関連リソースを取得するリソースのURI。 この例では、ソースリソース( `"/testFolder/testResource1"`)が指定されています。
   * 指定さ `boolean` れたリソースが関係のソースリソースであるかどうかを示す値。 この例では、値が指定されてい `true` ます。これは、この場合です。
   * ソース `boolean` リソースが指定されたかどうかを示す値です。 この例では、値が指定さ `true` れています。
   * 関係タイプを含む整数の配列。 この例では、以前に使用したのと同じ値を配列で使用して、依存関係を指定します。 `3`.
   * 残りの2 `null` つのパラメーターに対して渡します。
   このメ `getRelated` ソッドは、オブジェクトにキャストできるオブジェクトの配列を返します。この配列を `Resource` 使用して、関連する各リソースを繰り返し取得できます。 この例では、が返さ `testResource2` れるリソースのリストに含まれていると想定されます。

**関連トピック**

[リソースの関係の作成](aem-forms-repository.md#creating-resource-relationships)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## リソースのロック {#locking-resources}

特定のユーザーが排他的に使用したり、複数のユーザー間で共有を使用したりするために、リソースまたはリソースのセットをロックできます。 共有ロックは、リソースで何かが起こることを示しますが、他のユーザーがそのリソースでアクションを実行するのを妨げることはありません。 共有ロックは、シグナリングメカニズムと見なす必要があります。 排他ロックとは、リソースをロックしたユーザーがリソースを変更することを意味し、ロックは、ユーザーがリソースにアクセスする必要がなくなり、ロックを解除するまで、他のユーザーがリソースを変更できないようにします。 リポジトリ管理者がリソースのロックを解除すると、そのリソースに対する排他的ロックと共有ロックが自動的に削除されます。 このタイプのアクションは、ユーザーが使用できなくなり、リソースのロックが解除されなくなった場合に使用されます。

リソースをロックすると、次の図に示すように、Workbenchにある「リソース」タブを表示すると、ロックアイコンが表示されます。

![lr_lr_lockrepository](assets/lr_lr_lockrepository.png)

RepositoryサービスのJava APIまたはWebサービスのAPIを使用して、リソースへのアクセスをプログラムで制御できます。

>[!NOTE]
>
>For more information about the Repository service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-7}

リソースをロックおよびロック解除するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. Repositoryサービスクライアントを作成します。
1. ロックするリソースのURIを指定します。
1. リソースをロックします。
1. リソースのロックを取得します。
1. リソースのロック解除

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを含めます。

**サービスクライアントの作成**

プログラムでリソースを読み取る前に、接続を確立し、資格情報を提供する必要があります。 これは、サービスクライアントを作成することで実現されます。

**ロックするリソースのURIを指定します**

ロックするリソースのURIを含む文字列を作成します。 この構文には、次の例のようにスラッシュが含まれます。&quot;/*path*/*resource*&quot;

**リソースのロック**

Repositoryサービスメソッドを呼び出して、リソースをロックし、URI、ロックの種類、ロックの深さを指定します。

**リソースのロックを取得します**

URIを指定してリソースのロックを取得するには、Repositoryサービスメソッドを呼び出します。

**リソースのロック解除**

URIを指定してリソースのロックを解除するには、Repositoryサービスメソッドを呼び出します。

**関連トピック**

[Java APIを使用したリソースのロック](aem-forms-repository.md#lock-resources-using-the-java-api)

[WebサービスAPIを使用したリソースのロック](aem-forms-repository.md#lock-resources-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Repository Service APIクイックスタート](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java APIを使用したリソースのロック {#lock-resources-using-the-java-api}

RepositoryサービスAPI(Java)を使用してリソースをロックします。

1. プロジェクトファイルを含める

   JavaプロジェクトのクラスパスにクライアントJARファイルを含めます。

1. サービスクライアントの作成

   コンストラク `ResourceRepositoryClient` ターを使用し、接続プロパティを含むオブジェクトを渡 `ServiceClientFactory` して、オブジェクトを作成します。

1. ロックするリソースのURIを指定します

   ロックするリソースのURIを指定します。 この場合、という名前のリソースはという名 `testResource` 前のフォルダー内にあるので、 `testFolder`そのURIはです `"/testFolder/testResource"`。 URIはオブジェクトとして保存さ `java.lang.String` れます。

1. リソースのロック

   オブジェクト `ResourceRepositoryClient` のメソッドを呼 `lockResource` び出し、次のパラメーターを渡します。

   * リソースのURI。
   * ロックスコープ。 この例では、リソースは排他的に使用するためにロックされるので、ロック範囲はに指定しま `com.adobe.repository.infomodel.bean.Lock.SCOPE_EXCLUSIVE`す。
   * ロックの深さ。 この例では、ロックは特定のリソースにのみ適用され、そのメンバーや子は適用されないので、ロックの深さは、と指定しま `Lock.DEPTH_ZERO`す。
   >[!NOTE]
   >
   >4つのパラメーターを必要とするオ `lockResource` ーバーロードされたバージョンのメソッドは、例外をスローします。 このチュートリアルで示すよ `lockResource` うに、3つのパラメータを必要とするメソッドを必ず使用してください。

1. リソースのロックを取得します

   オブジェクト `ResourceRepositoryClient` のメソッドを `getLocks` 呼び出し、リソースのURIをパラメーターとして渡します。 このメソッドは、繰り返し処理が可能なLockオブジェクトのListを返します。 この例では、各Lockオブジェクトのメソッド、メソッド、およびメソッドをそれぞれ呼び出して、各オブジェクトに対してロックの所有者、深さ、スコ `getOwnerUserId`ープ `getDepth`を印 `getType` 刷します。

1. リソースのロック解除

   オブジェクト `ResourceRepositoryClient` のメソッドを `unlockResource` 呼び出し、リソースのURIをパラメーターとして渡します。 詳しくは、『 [AEM Forms APIリファレンス』を参照してください](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

**関連トピック**

[リソースのロック](aem-forms-repository.md#locking-resources)

[クイックスタート（SOAPモード）:Java APIを使用したリソースのロック](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-locking-a-resource-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したリソースのロック {#lock-resources-using-the-web-service-api}

RepositoryサービスAPI（Webサービス）を使用してリソースをロックします。

1. プロジェクトファイルを含める

   * Base64を使用してリポジトリWSDLを使用するMicrosoft .NETクライアントアセンブリを作成します。
   * Microsoft .NETクライアントアセンブリを参照します。

1. サービスクライアントの作成

   Microsoft .NETクライアントアセンブリを使用して、デフォルトのコンストラクタ `RepositoryServiceService` ーを呼び出してオブジェクトを作成します。 ユーザー名とパ `Credentials` スワードを含むオ `System.Net.NetworkCredential` ブジェクトを使用して、プロパティを設定します。

1. ロックするリソースのURIを指定します

   ロックするリソースのURIを含む文字列を指定します。 この場合、という名前のリソースはフォ `testResource` ルダー内にあるので、 `testFolder`そのURIはです `"/testFolder/testResource"`。 Microsoft .NET Framework（C#など）に準拠した言語を使用する場合は、URIをオブジェクトに格納し `System.String` ます。

1. リソースのロック

   オブジェクト `RepositoryServiceService` のメソッドを呼 `lockResource` び出し、次のパラメーターを渡します。

   * リソースのURI。
   * ロックスコープ。 この例では、リソースは排他的に使用するためにロックされるので、ロック範囲はに指定しま `11`す。
   * ロックの深さ。 この例では、ロックは特定のリソースにのみ適用され、そのメンバーや子は適用されないので、ロックの深さは、と指定しま `2`す。
   * ロッ `int` クが期限切れになるまでの秒数を示す値。 この例では、の値が使用さ `1000` れます。
   * 最後のパ `null` ラメーターに渡します。

1. リソースのロックを取得します

   オブジェクト `RepositoryServiceService` のメソッドを `getLocks` 呼び出し、リソースのURIを最初のパラメーターと2番目のパラメー `null` ターとして渡します。 このメソッドは、繰り返し `object` が可能なオ `Lock` ブジェクトを含む配列を返します。 この例では、各オブジェクトのオーナー、深さ、およびスコープにそれぞれアクセスして、各オブジ `Lock` ェクトに対し `ownerUserId`てロ `depth`ックのオ `type` ーナー、深さ、範囲を表示します。

1. リソースのロック解除

   オブジェクト `RepositoryServiceService` のメソッドを `unlockResource` 呼び出し、リソースのURIを最初のパラメーターと2番目のパラメー `null` ターとして渡します。

**関連トピック**

[リソースのロック](aem-forms-repository.md#locking-resources)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## リソースの削除 {#deleting-resources}

RepositoryサービスJava API(SOAP)を使用して、リポジトリ内の特定の場所からリソースをプログラム的に削除できます。

リソースを削除する場合、通常は削除は永続的ですが、場合によっては、ECMリポジトリがその履歴メカニズムに従ってリソースのバージョンを保存します。 したがって、リソースを削除する場合は、そのリソースが再び必要にならないことを確認することが重要です。 リソースを削除する一般的な理由としては、データベースの空き領域を増やす必要がある場合があります。 リソースのバージョンは削除できますが、削除する場合は、その論理識別子(LID)やパスではなく、リソース識別子を指定する必要があります。 フォルダを削除すると、サブフォルダやリソースを含む、そのフォルダ内のすべての要素が自動的に削除されます。

関連するリソースは削除されません。 例えば、logo.gifファイルを使用するフォームがあり、logo.gifを削除すると、保留中の関係テーブルに関係が保存されます。 代わりに、バージョンの非推奨の場合は、最新バージョンのオブジェクトステータスを非推奨に設定します。

ECMシステムでは、削除操作はトランザクションセーフではありません。 例えば、100個のリソースを削除しようとしたが、50番目のリソースで操作が失敗した場合、最初の49個のインスタンスは削除されますが、残りは削除されません。 それ以外の場合、デフォルトの動作はrollback （非コミットメント）です。

>[!NOTE]
>
>ECMリポジトリ( `com.adobe.repository.bindings.dsc.client.ResourceRepositoryClient.deleteResources()` EMC Documentum Content serverおよびIBM fileNet P8 Content Manager)でこの方法を使用する場合、指定されたリソースの1つに対して削除が失敗した場合、削除されたファイルの削除を取り消すことはできません。

>[!NOTE]
>
>For more information about the Repository service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-8}

リソースを削除するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. Repositoryサービスクライアントを作成します。
1. 削除するリソースのURIを指定します。
1. リソースを削除します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを含めます。

**サービスクライアントの作成**

プログラムでリソースを読み取る前に、接続を確立し、資格情報を提供する必要があります。 これは、サービスクライアントを作成することで実現されます。

**削除するリソースのURIを指定します**

削除するリソースのURIを含む文字列を作成します。 この構文には、次の例のようにスラッシュが含まれます。&quot;/*path*/*resource*&quot; 削除するリソースがフォルダーの場合、削除は再帰的に実行されます。

**リソースの削除**

URIを指定してリソースを削除するには、Repositoryサービスメソッドを呼び出します。

**関連トピック**

[Java APIを使用したリソースの削除](aem-forms-repository.md#delete-resources-using-the-java-api-soap)

[WebサービスAPIを使用したリソースの削除](aem-forms-repository.md#delete-resources-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Repository Service APIクイックスタート](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java API(SOAP)を使用したリソースの削除 {#delete-resources-using-the-java-api-soap}

リポジトリAPI(Java)を使用してリソースを削除します。

1. プロジェクトファイルを含める

   JavaプロジェクトのクラスパスにクライアントJARファイルを含めます。

1. サービスクライアントの作成

   コンストラク `ResourceRepositoryClient` ターを使用し、接続プロパティを含むオブジェクトを渡 `ServiceClientFactory` して、オブジェクトを作成します。

1. 削除するリソースのURIを指定します

   取得するリソースのURIを指定します。 この場合、testResourceToBeDeletedという名前のリソースはtestFolderという名前のフォルダーにあるので、URIはです `/testFolder/testResourceToBeDeleted`。 URIはオブジェクトとして保存さ `java.lang.String` れます。 この例では、リソースが最初にリポジトリに書き込まれ、そのURIが取得されます。 リソースの作成の詳細については、「リソースの作成」を参 [照してください](aem-forms-repository.md#writing-resources)。

1. リソースの削除

   オブジェクト `ResourceRepositoryClient` のメソッドを `deleteResource` 呼び出し、リソースのURIをパラメーターとして渡します。

**関連トピック**

[リソースの削除](aem-forms-repository.md#deleting-resources)

[クイックスタート（SOAPモード）:Java APIを使用したリソースの検索](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したリソースの削除 {#delete-resources-using-the-web-service-api}

Repository API（Webサービス）を使用してリソースを削除します。

1. プロジェクトファイルを含める

   * Base64を使用してリポジトリWSDLを使用するMicrosoft .NETクライアントアセンブリを作成します。
   * Microsoft .NETクライアントアセンブリを参照します。

1. サービスクライアントの作成

   Microsoft .NETクライアントアセンブリを使用して、デフォルトのコンストラクタ `RepositoryServiceService` ーを呼び出してオブジェクトを作成します。 ユーザー名とパ `Credentials` スワードを含むオ `System.Net.NetworkCredential` ブジェクトを使用して、プロパティを設定します。

1. 削除するリソースのURIを指定します

   取得するリソースのURIを指定します。 この場合、という名前のリソースはという名 `testResourceToBeDeleted` 前のフォルダー内にあるので、 `testFolder`そのURIはです `"/testFolder/testResourceToBeDeleted"`。 この例では、リソースが最初にリポジトリに書き込まれ、そのURIが取得されます。 リソースの作成の詳細については、「リソースの作成」を参 [照してください](aem-forms-repository.md#writing-resources)。

1. リソースの削除

   オブジェクト `RepositoryServiceService` のメソッドを `deleteResources` 呼び出し、リソー `System.String` スのURIを含む配列を最初のパラメーターとして渡します。 2番目の `null` パラメーターに渡します。

**関連トピック**

[リソースの削除](aem-forms-repository.md#deleting-resources)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
