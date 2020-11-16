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
source-git-commit: 67ea825215d1ca7cc2e350ed1c128c3146de45ec
workflow-type: tm+mt
source-wordcount: '9076'
ht-degree: 2%

---


# Working with AEM Forms Repository {#working-with-aem-forms-repository}

**Repository Serviceについて**

Repositoryサービスは、リソースのストレージおよび管理サービスをAEM Formsに提供します。 When developers create an *AEM Forms* application, they can deploy the assets in the repository instead of the file system. アセットには、XML 形式、PDF 形式（Acrobat 形式を含む）、フォームのフラグメント、画像、プロファイル、ポリシー、SWF ファイル、DDX ファイル、XML スキーマ、WSDL ファイルおよびテストデータなど、任意のタイプのコラテラルが含まれます。

例えば、次のFormsアプリケーションの *Applications/FormsApplication*:

![ww_ww_formrepository](assets/ww_ww_formrepository.png)

FormsFolder内にLoan.xdpという名前のファイルがあることに注意してください。 このフォームデザインにアクセスするには、次の操作を行います（バージョンを含む）。 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.

>[!NOTE]
>
>Workbenchを使用したFormsアプリケーションの作成に関する詳細は、『 [Workbenchヘルプ](https://www.adobe.com/go/learn_aemforms_workbench_63)』を参照してください。

AEM Formsリポジトリ内のリソースへのパスは次のとおりです。

`Applications/Application-name/Application-version/Folder.../Filename`

次に、URI値の例を示します。

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

>[!NOTE]
>
>Webブラウザーを使用して、AEM Formsリポジトリを参照できます。 リポジトリを参照するには、Webブラウザーに次のURLを入力し `https://[server name]:[server port]/repository`ます。 「AEM Formsリポジトリでの作業」セクションに関連付けられているクイック開始の結果は、Webブラウザーを使用して確認できます。 例えば、コンテンツをAEM Formsリポジトリに追加すると、Webブラウザーでコンテンツを表示できます。 (See [Quick Start (SOAP mode): Writing a resource using the Java API](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api).)

リポジトリAPIは、リポジトリに情報を格納したり、リポジトリから情報を取得したりするために使用できる操作を多数提供します。 例えば、リソースのリストを取得したり、アプリケーションの処理の一部としてリソースが必要な場合にリポジトリに格納されている特定のリソースを取得したりできます。

>[!NOTE]
>
>リポジトリAPIを使用してContent Services（非推奨）とやり取りすることはできません。 Content Services（非推奨）とやり取りするには、ドキュメント管理APIを使用します。

RepositoryサービスAPIを使用して、次のタスクを実行できます。

* フォルダーの作成. 「フォルダ [の作成](aem-forms-repository.md#creating-folders)」を参照してください。
* リソースとそのプロパティを書き込みます。 「リソースの [書き込み](aem-forms-repository.md#writing-resources)」を参照してください。
* 特定のコレクション内のリストリソース、または他のリソースに関連付けられているリソース。 「 [Listing Resources](aem-forms-repository.md#listing-resources)」を参照してください。
* リソースとそのプロパティを読み取ります。 詳しくは、 [Reading Resources](aem-forms-repository.md#reading-resources)を参照してください。
* リソースとそのプロパティを更新します。 「リソース [の更新](aem-forms-repository.md#updating-resources)」を参照してください。
* 履歴、関連するリソース、プロパティなどのリソースを検索します。 「リソースの [検索](aem-forms-repository.md#searching-for-resources)」を参照してください。
* リソース間の関係を指定します。 「リソースの関係の [作成](aem-forms-repository.md#creating-resource-relationships)」を参照してください。
* リソースのロックとロック解除、アクセス制御リスト(ACL)の読み取りと書き込みなど、リソースアクセス制御を管理します。 Locking [Resources](aem-forms-repository.md#locking-resources)を参照してください。
* リソースとそのプロパティを削除します。 「リソース [の削除](aem-forms-repository.md#deleting-resources)」を参照してください。

>[!NOTE]
>
>リポジトリAPIを使用して、リソースアクセス制御の管理、リソースの検索、ECMリポジトリを使用したリソースの関係の指定を行うことはできません。

>[!NOTE]
>
>暗号化されたPDFがリポジトリに書き込まれると、自動関係抽出機能は使用できません。 それ以外の場合は、暗号化されたPDFをリポジトリに保存し、後で取得できます。 取得者は、PDFがリポジトリから取得された後に、そのPDFを復号化することを選択できます。

>[!NOTE]
>
>For more information about the Repository service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## フォルダーの作成 {#creating-folders}

フォルダー（リソースコレクション）は、オブジェクト（ファイルまたはリソース）を整理されたグループに格納するために使用します。 フォルダーには、リソースやサブフォルダーとも呼ばれるその他のフォルダーを含めることができます。 リソースは一度に1つのフォルダーにしか保存できません。

ファイルはアクセス制御リストー(ACL)をフォルダーから継承し、サブフォルダーはACLを親フォルダーから継承します。 したがって、子フォルダーを作成する前に、親フォルダーが存在している必要があります。 IDEでは、フォルダごとの操作のみが可能で、ファイルごとの操作はできません。 フォルダのバージョンを変更することはできません。また、バージョンを変更する必要はありません。フォルダーには、データ自体が含まれていません。 データを含むリソースのコンテナにすぎません。 デフォルトのACLはシステムレベルの権限です。つまり、ユーザーが特定のフォルダーに対する権限を付与するまで、ユーザーはシステムレベルの権限（読み取り、書き込み、トラバース、ACLの管理）を持つ必要があります。 ACLはIDEでのみ機能します。

>[!NOTE]
>
>For more information about the Repository service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary-of-steps}

フォルダーを作成するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. サービスクライアントを作成します。
1. フォルダーを作成します。
1. フォルダーをリポジトリに書き込みます。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを含めます。

**サービスクライアントの作成**

プログラムによってリソース収集を作成する前に、接続を確立し、秘密鍵証明書を指定する必要があります。 これは、サービスクライアントを作成することで実行されます。

**フォルダーの作成**

Repositoryサービスメソッドを呼び出して、リソースコレクションを作成し、UUID、フォルダー名、説明などの識別情報をリソースコレクションに入力します。

**フォルダーをリポジトリに書き込みます**

Repositoryサービスメソッドを呼び出して、リソースコレクションを書き込み、ターゲットフォルダーのURIを指定します。

**関連トピック**

[Java APIを使用したフォルダーの作成](aem-forms-repository.md#create-folders-using-the-java-api)

[WebサービスAPIを使用したフォルダーの作成](aem-forms-repository.md#create-folders-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Repository Service APIクイック開始](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java APIを使用したフォルダーの作成 {#create-folders-using-the-java-api}

RepositoryサービスAPI(Java)を使用してフォルダーを作成します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスにプロジェクトファイルを含めます。

1. サービスクライアントの作成

   コンストラクタを使用し、接続プロパティを含むオブジェクトを渡して、 `ResourceRepositoryClient``ServiceClientFactory` オブジェクトを作成します。

1. フォルダーの作成

   リソースコレクションを作成するには、まず `com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean` オブジェクトを作成する必要があります。

   オブジェクトの `repositoryInfomodelFactoryBean``newResourceCollection` メソッドを呼び出し、次のパラメーターを渡します。

   * リソースに割り当てる `com.adobe.repository.infomodel.Id` UUID識別子。
   * リソースに割り当てる `com.adobe.repository.infomodel.Lid` UUID識別子。
   * リソースコレクションの名前 `java.lang.String` を含む。 例： `FormsFolder`

   このメソッドは、新しいフォルダーを表す `com.adobe.repository.infomodel.bean.ResourceCollection` オブジェクトを返します。

   フォルダーの説明を設定するには、 `setDescription` メソッドを使用し、次のパラメーターを渡します。

   * リソース収集 `String` を示す。 この例では、が使用され `"test Folder"` ています。 `.`


1. フォルダーをリポジトリに書き込みます

   オブジェクトの `ResourceRepositoryClient` メソッドを呼び出し、フォルダーと `writeResource``ResourceCollection` オブジェクトのURIを渡します。 例えば、フォルダーへのURIを次の値に設定でき `/Applications/FormsApplication/1.0/`ます。

   メソッドは、新しく作成された `com.adobe.repository.infomodel.bean.Resource` オブジェクトのインスタンスを返します。 例えば、オブジェクトのメソッドを呼び出して、新しいリソースの識別子の値を取得す `com.adobe.repository.infomodel.bean.Resource` ることがで `getId` きます。

**関連トピック**

[フォルダーの作成](aem-forms-repository.md#creating-folders)

[クイック開始（SOAPモード）:Java APIを使用したフォルダーの作成](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-a-folder-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したフォルダーの作成 {#create-folders-using-the-web-service-api}

RepositoryサービスAPI（Webサービス）を使用してフォルダーを作成します。

1. プロジェクトファイルを含める

   * base64を使用してリポジトリWSDLを使用するMicrosoft .NETクライアントアセンブリを作成します。
   * Microsoft .NETクライアントアセンブリを参照します。

1. サービスクライアントの作成

   Microsoft .NETクライアントアセンブリを使用して、デフォルトのコンストラクタを呼び出して `RepositoryServiceService` オブジェクトを作成します。 ユーザー名とパスワードを含む `Credentials``System.Net.NetworkCredential` オブジェクトを使用して、プロパティを設定します。

1. フォルダーの作成

   クラスのデフォルトのコンストラクターを使用してフォルダーを作成し、次のパラメーターを `ResourceCollection` 渡します。

   * オブジェクト。クラスのデフォルトコンストラクターを呼び出して作成され、オ `Id` ブジェクトの `Id` フィールドに割り当てられるオブジェクト `Resource``id` です。
   * オブジェクト。クラスのデフォルトコンストラクターを呼び出して作成され、オ `Lid` ブジェクトの `Lid` フィールドに割り当てられるオブジェクト `Resource``lid` です。
   * リソースコレクションの名前を含む文字列。この名前は `Resource` オブジェクトの `name` フィールドに割り当てられます。 この例で使用される名前はで `"testfolder"`す。
   * リソースコレクションの説明を含む文字列。これは `Resource` オブジェクトの `description` フィールドに割り当てられます。 この例で使用される説明は、で `"test folder"`す。

1. フォルダーをリポジトリに書き込みます

   オブジェクトの `RepositoryServiceService``writeResource` メソッドを呼び出し、次のパラメーターを渡します。

   * フォルダーを作成するパスです。
   * フォルダーを表す `ResourceCollection` オブジェクトです。
   * 他の2つ `null` のパラメーターに対してを渡します。

**関連トピック**

[フォルダーの作成](aem-forms-repository.md#creating-folders)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## リソースの書き込み {#writing-resources}

リポジトリ内の特定の場所にリソースを作成できます。 自然なファイルサイズは、データベースの制限やセッションタイムアウトの影響を受けます。 デフォルトの設定では、ファイルのサイズは25 MBに制限されます。 最大ファイルサイズを増減するには、データベース設定を変更する必要があります。

リソースを書き込むことは、リポジトリにデータを格納することと同じです。 リポジトリにリソースを書き込むと、リポジトリエコシステム内のすべてのクライアントがそのリソースにアクセスできるようになります。 XMLスキーマ、XDPファイル、XSDファイルなどのリソースをリポジトリに書き込むと、そのコンテンツはMIMEタイプに基づいて解析されます。 MIMEタイプがサポートされている場合、パーサーは他のコンテンツとの暗黙の関係があるかどうかを判定します。 例えば、カスケーディングスタイルシート(CSS)に共通のCSSを参照する相対URLがある場合、共通のCSSもリポジトリに送信する必要があります。 2つのリソース間の関係は、調整不可能な30日間の保留中の関係として保存されます。 共通のCSSをリポジトリに30日以内に送信すると、関係が形成されます。

リソースを作成すると、アクセス制御リスト(ACL)は親フォルダーから継承されます。 ルートフォルダーには、最初のリソースまたはフォルダーが作成されるまで、システムレベルの権限があります。その時点で、リソースまたはフォルダーにデフォルトのACL権限が付与されます。

RepositoryサービスJava APIまたはWebサービスAPIを使用して、プログラムによってリソースを書き込むことができます。

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

プログラムでリソースを読み取る前に、接続を確立し、秘密鍵証明書を提供する必要があります。 これは、サービスクライアントを作成することで実行されます。

**リソースのターゲットフォルダーのURIを指定します**

読み取るリソースのURIを含む文字列を作成します。 構文には、次の例のようにスラッシュが含まれます。&quot;/*path*/*folder*&quot;

**リソースの作成**

Repositoryサービスメソッドを呼び出して、リソースを作成し、UUID、リソース名、説明などの識別情報をリソースに入力します。

**リソースコンテンツの指定**

Repositoryサービスメソッドを呼び出して、リソースコンテンツを作成し、そのコンテンツをリソースに格納します。

**リソースをターゲットフォルダーに書き込みます**

ターゲットフォルダーのURIを指定してリソースを書き込むには、Repositoryサービスメソッドを呼び出します。

**関連トピック**

[Java APIを使用したリソースの書き込み](aem-forms-repository.md#write-resources-using-the-java-api)

[WebサービスAPIを使用したリソースの書き込み](aem-forms-repository.md#write-resources-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Repository Service APIクイック開始](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java APIを使用したリソースの書き込み {#write-resources-using-the-java-api}

RepositoryサービスAPI(Java)を使用してリソースを書き込みます。

1. プロジェクトファイルを含める

   JavaプロジェクトのクラスパスにクライアントJARファイルを含めます。

1. サービスクライアントの作成

   コンストラクタを使用し、接続プロパティを含むオブジェクトを渡して、 `ResourceRepositoryClient``ServiceClientFactory` オブジェクトを作成します。

1. リソースのターゲットフォルダーのURIを指定します

   リソースのターゲットフォルダーのURIを指定します。 この場合、という名前のリソース `testResource` はという名前のフォルダーに保存されるので `testFolder`、フォルダーのURIは `"/testFolder"`です。 URIは `java.lang.String` オブジェクトとして保存されます。

1. リソースの作成

   リソースを作成するには、まず `com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean` オブジェクトを作成する必要があります。

   オブジェクトを作成する `RepositoryInfomodelFactoryBean` オブジェクトの `newResource` メソッドを呼び出し `com.adobe.repository.infomodel.bean.Resource` ます。 この例では、次のパラメーターが提供されます。

   * クラスのデフォルトコンストラクターを呼び出して作成される `com.adobe.repository.infomodel.Id` オブジェクト `Id` 。
   * クラスのデフォルトコンストラクターを呼び出して作成される `com.adobe.repository.infomodel.Lid` オブジェクト `Lid` 。
   * リソースのファイル名 `java.lang.String` を含む。

   リソースの説明を指定するには、 `Resource` オブジェクトの `setDescription` メソッドを呼び出し、説明を含む文字列を渡します。 この例では、説明はです `"test resource"`。

1. リソースコンテンツの指定

   リソースのコンテンツを作成するには、オブジ `RepositoryInfomodelFactoryBean` ェクトの `newResourceContent` メソッドを呼び出し、オブジ `com.adobe.repository.infomodel.bean.ResourceContent` ェクトを返します。 Add content to the `ResourceContent` object. この例では、次のタスクを行うことで実現します。

   * オブジェクトの `ResourceContent` メソッドを呼び出して、オブジ `setDataDocument``com.adobe.idp.Document` ェクトを渡す
   * オブジェクトの `ResourceContent` メソッドを呼び出して、オブジ `setSize``Document` ェクトのバイト単位でサイズを渡す

   オ追加ブジェクトのメソッドを呼び出し、オブジェクトを渡すことで、リソースに対するコンテンツを指定し `Resource``setContent``ResourceContent` ます。 For more information, see [AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. リソースをターゲットフォルダーに書き込みます

   オブジェクトの `ResourceRepositoryClient` メソッドを呼び出し、フォルダーのURIと `writeResource``Resource` オブジェクトを渡します。

**関連トピック**

[リソースの書き込み](aem-forms-repository.md#writing-resources)

[クイック開始（SOAPモード）:Java APIを使用したリソースの作成](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したリソースの書き込み {#write-resources-using-the-web-service-api}

RepositoryサービスAPI（Webサービス）を使用してリソースを書き込みます。

1. プロジェクトファイルを含める

   * base64を使用してリポジトリWSDLを使用するMicrosoft .NETクライアントアセンブリを作成します。
   * Microsoft .NETクライアントアセンブリを参照します。

1. サービスクライアントの作成

   Microsoft .NETクライアントアセンブリを使用して、デフォルトのコンストラクタを呼び出して `RepositoryServiceService` オブジェクトを作成します。 ユーザー名とパスワードを含む `Credentials``System.Net.NetworkCredential` オブジェクトを使用して、このプロパティを設定します。

1. リソースのターゲットフォルダーのURIを指定します

   リソースのターゲットフォルダーのURIを指定します。 この場合、という名前のリソース `testResource` はという名前のフォルダーに保存されるので `testFolder`、フォルダーのURIは `"/testFolder"`です。 Microsoft .NET Frameworkに準拠した言語（C#など）を使用する場合は、URIを `System.String` オブジェクトに格納します。

1. リソースの作成

   リソースを作成するには、クラスのデフォルトコンストラクターを呼び出し `Resource` ます。 この例では、次の情報が `Resource` オブジェクトに格納されます。

   * オブジェクト。クラスのデフォルトコンストラクターを呼び出して作成され、オ `com.adobe.repository.infomodel.Id` ブジェクトの `Id``Resource``id` フィールドに割り当てられます。
   * オブジェクト。クラスのデフォルトコンストラクターを呼び出して作成され、オ `com.adobe.repository.infomodel.Lid` ブジェクトの `Lid``Resource``lid` フィールドに割り当てられます。
   * リソースのファイル名を含む文字列。このファイル名は `Resource` オブジェクトの `name` フィールドに割り当てられます。 この例で使用される名前はで `"testResource"`す。
   * リソースの説明を含む文字列。このリソースは `Resource` オブジェクトの `description` フィールドに割り当てられます。 この例で使用される説明は、で `"test resource"`す。

1. リソースコンテンツの指定

   リソースのコンテンツを作成するには、クラスのデフォルトコンストラクターを呼び出し `ResourceContent` ます。 次に、 `ResourceContent` オブジェクトにコンテンツを追加します。 この例では、次のタスクを行うことで実現します。

   * ドキュメントを含む `BLOB` オブジェクトをオブジェクトの `ResourceContent` フ `dataDocument` ィールドに割り当てます。
   * オブジェクトのフィールドに `BLOB` オブジェクトのサイズをバイト単位で割り当て `ResourceContent` る `size` 。

   オ追加ブジェクトのフィールドにオブジェクトを割り当てることで、リソースに対するコンテンツを指定し `ResourceContent` ま `Resource``content` す。

1. リソースをターゲットフォルダーに書き込みます

   オブジェクトの `RepositoryServiceService` メソッドを呼び出し、フォルダーのURIと `writeResource``Resource` オブジェクトを渡します。 他の2つ `null` のパラメーターに対してを渡します。

**関連トピック**

[リソースの書き込み](aem-forms-repository.md#writing-resources)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## リソースの一覧表示 {#listing-resources}

リソースを一覧表示することで、リソースを見つけることができます。 リポジトリに対してクエリが実行され、特定のリソース収集に関連するすべてのリソースが検索されます。

リソースを整理したら、オペレーティングシステムで行うのと同じように、構造の特定のブランチを表示して、作成した構造を調べることができます。

リソースのリストは、次の関係によって機能します。リソースは、フォルダーのメンバーです。 メンバーシップは、「メンバー」のタイプの関係で表されます。 特定のフォルダー内のリソースをリストする場合、「メンバー」の関係によって特定のフォルダーに関連するリソースを照会します。 関係は方向性を持ちます。関係のメンバーには、ターゲットのメンバーであるソースがあります。 その出所は資源である。ターゲットは親フォルダーです。

>[!NOTE]
>
>For more information about the Repository service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-2}

リストリソースを作成するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. サービスクライアントを作成します。
1. フォルダーパスを指定します。
1. リソースのリストを取得します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを含めます。

**サービスクライアントの作成**

プログラムによってリソース収集を作成する前に、接続を確立し、秘密鍵証明書を指定する必要があります。 これは、サービスクライアントを作成することで実行されます。

**フォルダーパスの指定**

リソースを含むフォルダーのパスを含む文字列を作成します。 構文には、次の例のようにスラッシュが含まれます。&quot;/*path*/*folder*&quot;

**リソースのリストの取得**

ターゲットフォルダーのパスを指定して、リソースのリストを取得するには、Repositoryサービスメソッドを呼び出します。

**関連トピック**

[Java APIを使用したリストリソース](aem-forms-repository.md#list-resources-using-the-java-api)

[WebサービスAPIを使用するリストリソース](aem-forms-repository.md#list-resources-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Repository Service APIクイック開始](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java APIを使用したリストリソース {#list-resources-using-the-java-api}

RepositoryサービスAPI(Java)を使用したリストリソース：

1. プロジェクトファイルを含める

   JavaプロジェクトのクラスパスにクライアントJARファイルを含めます。

1. サービスクライアントの作成

   コンストラクタを使用し、接続プロパティを含むオブジェクトを渡して、 `ResourceRepositoryClient``ServiceClientFactory` オブジェクトを作成します。

1. フォルダーパスの指定

   照会するリソースコレクションのURIを指定します。 この場合、URIはです `"/testFolder"`。 URIは `java.lang.String` オブジェクトとして保存されます。

1. リソースのリストの取得

   オブジェクトの `ResourceRepositoryClient``listMembers` メソッドを呼び出し、フォルダーのURIを渡します。

   このメソッドは、ある種類のリソースであり、リソース収集URIをターゲットとして持つ `java.util.List` 一 `com.adobe.repository.infomodel.bean.Resource` 連の `com.adobe.repository.infomodel.bean.Relation``Relation.TYPE_MEMBER_OF` オブジェクトを返します。 この処理を繰り返し実行して、各リソース `List` を取得できます。 この例では、各リソースの名前と説明が表示されます。

**関連トピック**

[リソースの一覧](aem-forms-repository.md#listing-resources)。

[クイック開始（SOAPモード）:Java APIを使用したリソースの一覧表示](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-listing-resources-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用するリストリソース {#list-resources-using-the-web-service-api}

RepositoryサービスAPI（Webサービス）を使用したリストリソース：

1. プロジェクトファイルを含める

   * リポジトリWSDLを使用するMicrosoft .NETクライアントアセンブリを作成します。
   * Microsoft .NETクライアントアセンブリを参照します。

1. サービスクライアントの作成

   Microsoft .NETクライアントアセンブリを使用して、デフォルトのコンストラクタを呼び出して `RepositoryServiceService` オブジェクトを作成します。 ユーザー名とパスワードを含む `Credentials``System.Net.NetworkCredential` オブジェクトを使用して、このプロパティを設定します。

1. フォルダーパスの指定

   照会するフォルダーのURIを含む文字列を指定します。 この場合、URIはです `"/testFolder"`。 Microsoft .NET Frameworkに準拠している言語（C#など）を使用する場合は、URIを `System.String` オブジェクトに格納します。

1. リソースのリストの取得

   オブ `RepositoryServiceService` ジェクトの `listMembers` メソッドを呼び出し、フォルダーのURIを最初のパラメーターとして渡します。 他の2つ `null` のパラメーターに対してを渡します。

   このメソッドは、オブジェクトにキャストできるオブジェクトの配列を返し `Resource` ます。 オブジェクト配列を繰り返し処理して、関連する各リソースを取得できます。 この例では、各リソースの名前と説明が表示されます。

**関連トピック**

[リソースの一覧](aem-forms-repository.md#listing-resources)。

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## リソースの読み取り {#reading-resources}

リソースのコンテンツとメタデータを読み取るために、リポジトリ内の特定の場所からリソースを取得できます。 ワークフローは、初期化フォームによってフロントエンドされます。 プロセスには、フォームを読み取るために必要なすべての権限があります。 データ・フォームが取得され、リポジトリからコンテンツが読み取られます。 リポジトリは、コンテンツとメタデータ（リソースが存在することを知る機能）へのアクセスを許可します。

リポジトリには次の4つの権限タイプがあります。

* **traverse**:リソースをリストできます。つまり、リソースのメタデータを読み取るが、リソースの内容を読み取らない
* **read**:リソースの内容を読み取ることができます。
* **write**:リソースの内容を書き込むことができます。
* **アクセス制御リスト(ACL)**:リソースのACLを操作できます。

ユーザーがプロセスを実行できるのは、プロセスを実行する権限がある場合のみです。 IDEユーザーは、リポジトリと同期するためにtraverse権限とread権限が必要です。 実行時はシステムコンテキスト内で発生するので、ACLはデザイン時にのみ適用されます。

RepositoryサービスJava APIまたはWebサービスAPIを使用して、プログラムでリソースを読み取ることができます。

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

プログラムでリソースを読み取る前に、接続を確立し、秘密鍵証明書を提供する必要があります。 これは、サービスクライアントを作成することで実行されます。

**読み取るリソースのURIを指定します**

読み取るリソースのURIを含む文字列を作成します。 構文には、次の例のようにスラッシュが含まれます。&quot;/*path*/*resource*&quot;

**リソースの読み取り**

URIを指定してリソースを読み取るには、Repositoryサービスメソッドを呼び出します。

**関連トピック**

[Java APIを使用したリソースの読み取り](aem-forms-repository.md#read-resources-using-the-java-api)

[WebサービスAPIを使用したリソースの読み取り](aem-forms-repository.md#reading-resources-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Repository Service APIクイック開始](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java APIを使用したリソースの読み取り {#read-resources-using-the-java-api}

RepositoryサービスAPI(Java)を使用してリソースを読み取ります。

1. プロジェクトファイルを含める

   JavaプロジェクトのクラスパスにクライアントJARファイルを含めます。

1. サービスクライアントの作成

   コンストラクタを使用し、接続プロパティを含むオブジェクトを渡して、 `ResourceRepositoryClient``ServiceClientFactory` オブジェクトを作成します。

1. 読み取るリソースのURIを指定します

   取得するリソースのURIを表すstring値を指定します。 例えば、リソースの名前がtestFolderという名前のフォルダーにある *testResource* という名前の場合は、 *testFolder*&#x200B;と指定し `/testFolder/testResource`ます。

1. リソースの読み取り

   オブジェクトの `ResourceRepositoryClient``readResource` メソッドを呼び出し、リソースのURIをパラメーターとして渡します。 このメソッドは、リソースを表す `Resource` インスタンスを返します。

**関連トピック**

[リソースの読み取り](aem-forms-repository.md#reading-resources)

[クイック開始（SOAPモード）:Java APIを使用したリソースの読み取り](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-reading-a-resource-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したリソースの読み取り {#reading-resources-using-the-web-service-api}

RepositoryサービスAPI（Webサービス）を使用してリソースを読み取ります。

1. プロジェクトファイルを含める

   * リポジトリWSDLを使用するMicrosoft .NETクライアントアセンブリを作成します。 (Base64エンコーディングを使用した.NETクライアントアセンブリの [作成を参照](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding))。
   * Microsoft .NETクライアントアセンブリを参照します。 (Base64エンコーディングを使用した.NETクライアントアセンブリの [作成を参照](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding))。

1. サービスクライアントの作成

   Microsoft .NETクライアントアセンブリを使用して、デフォルトのコンストラクタを呼び出して `RepositoryServiceService` オブジェクトを作成します。 ユーザー名とパスワードを含む `Credentials``System.Net.NetworkCredential` オブジェクトを使用して、このプロパティを設定します。

1. 読み取るリソースのURIを指定します

   取得するリソースのURIを含む文字列を指定します。 この場合、という名前のリソース `testResource` はという名前のフォルダーにあるので `testFolder`、そのURIは `"/testFolder/testResource"`です。 Microsoft .NET Frameworkに準拠した言語（C#など）を使用する場合は、URIを `System.String` オブジェクトに格納します。

1. リソースの読み取り

   オブジェクトの `RepositoryServiceService``readResource` メソッドを呼び出し、リソースのURIを最初のパラメーターとして渡します。 他の2つ `null` のパラメーターに対してを渡します。

**関連トピック**

[リソースの読み取り](aem-forms-repository.md#reading-resources)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## リソースの更新 {#updating-resources}

リポジトリ内のリソースのコンテンツを取得して更新できます。 リソースを更新しても、それらのリソースのアクセス制御は、バージョン間で変更されません。 更新を実行する場合、メジャーバージョンを増分するオプションがあります。 メジャーバージョンを増分しない場合は、マイナーバージョンが自動的に更新されます。

リソースを更新すると、指定したリソース属性に基づいて新しいバージョンが作成されます。 リソースを更新する場合は、次の2つの重要なパラメータを指定します。ターゲットURIと、更新されたすべてのメタデータを含むリソースインスタンス。 特定の属性（名前など）を変更しない場合でも、その属性は渡すインスタンスで必要です。 コンテンツの解析時に作成される関係は、特定のバージョンに追加され、特に指定がない限り転送されません。

例えば、XDPファイルを更新し、そのXDPファイルに他のリソースへの参照が含まれている場合、それらの追加参照も記録されます。 form.xdpバージョン1.0に2つの外部参照があるとします。ロゴとスタイルシートを作成し、次の3つの参照を持つようにform.xdpを更新します。ロゴ、スタイルシート、スキーマファイル。 更新中、リポジトリは3つ目の関係(スキーマファイル)を保留関係テーブルに追加します。 スキーマファイルがリポジトリに存在する場合は、関係が自動的に形成されます。 ただし、form.xdpバージョン2.0がロゴを使用しなくなった場合、form.xdpバージョン2.0はロゴとの関係を持ちません。

すべての更新操作は、アトミックおよびトランザクションです。 例えば、2人のユーザーが同じリソースを読み取り、両方がバージョン1.0をバージョン2.0に更新すると、どちらかが成功し、一方が失敗すると、リポジトリの整合性が維持され、両方が成功または失敗を確認するメッセージを受け取ります。 トランザクションがコミットされない場合、データベース障害が発生した場合はロールバックされ、アプリケーションサーバーに応じてタイムアウトまたはロールバックされます。

RepositoryサービスJava APIまたはWebサービスAPIを使用して、プログラムでリソースを更新できます。

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

プログラムでリソースを読み取る前に、接続を確立し、秘密鍵証明書を提供する必要があります。 これは、サービスクライアントを作成することで実行されます。

**更新するリソースを取得します**

リソースを読み取ります。 詳しくは、「リソース [の読み取り](aem-forms-repository.md#reading-resources)」を参照してください。

**リソースの更新**

リソースに新しい情報を設定し、Repositoryサービスメソッドを呼び出して、リソースを更新します。URI、更新されたリソース、およびバージョン情報の更新方法を指定します。

**関連トピック**

[Java APIを使用したリソースの更新](aem-forms-repository.md#update-resources-using-the-java-api)

[WebサービスAPIを使用したリソースの更新](aem-forms-repository.md#update-resources-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Repository Service APIクイック開始](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java APIを使用したリソースの更新 {#update-resources-using-the-java-api}

RepositoryサービスAPI(Java)を使用してリソースを更新します。

1. プロジェクトファイルを含める

   JavaプロジェクトのクラスパスにクライアントJARファイルを含めます。

1. サービスクライアントの作成

   コンストラクタを使用し、接続プロパティを含むオブジェクトを渡して、 `ResourceRepositoryClient``ServiceClientFactory` オブジェクトを作成します。

1. 更新するリソースを取得します

   リソースを取得して読み取るリソースのURIを指定します。 この例では、リソースのURIはです `"/testFolder/testResource"`。

1. リソースの更新

   オブジェクトの `Resource` 情報を更新します。 この例では、説明を更新するには、 `Resource` オブジェクトの `setDescription` メソッドを呼び出し、新しい説明文字列をパラメーターとして渡します。

   次に、 `ServiceClientFactory` オブジェクトの `updateResource` メソッドを呼び出し、次のパラメーターを渡します。

   * リソースのURIを含む `java.lang.String` オブジェクト。
   * 更新されたリソース情報を含む `Resource` オブジェクトです。
   * メジャーバージョンを更新するか、マイナーバージョンを更新するかを示す `boolean` 値。 この例では、メジャーバージョンの値を増分す `true` ることを示す値が渡されます。

**関連トピック**

[リソースの更新](aem-forms-repository.md#updating-resources)

[クイック開始（SOAPモード）:Java APIを使用したリソースの更新](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-updating-a-resource-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したリソースの更新 {#update-resources-using-the-web-service-api}

Repository API（Webサービス）を使用してリソースを更新します。

1. プロジェクトファイルを含める

   * リポジトリWSDLを使用するMicrosoft .NETクライアントアセンブリを作成します。
   * Microsoft .NETクライアントアセンブリを参照します。

1. サービスクライアントの作成

   Microsoft .NETクライアントアセンブリを使用して、デフォルトのコンストラクタを呼び出して `RepositoryServiceService` オブジェクトを作成します。 ユーザー名とパスワードを含む `Credentials``System.Net.NetworkCredential` オブジェクトを使用して、このプロパティを設定します。

1. 更新するリソースを取得します

   取得するリソースのURIを指定し、リソースを読み取ります。 この例では、リソースのURIはです `"/testFolder/testResource"`。 詳しくは、「リソース [の読み取り](aem-forms-repository.md#reading-resources)」を参照してください。

1. リソースの更新

   オブジェクトの `Resource` 情報を更新します。 この例では、説明を更新するには、新しい値を `Resource` オブジェクトの `description` フィールドに割り当てます。

1. オブジェクトの `RepositoryServiceService``updateResource` メソッドを呼び出し、次のパラメーターを渡します。

   * リソースのURIを含む `System.String` オブジェクト。
   * 更新されたリソース情報を含む `Resource` オブジェクトです。
   * メジャーバージョンを更新するか、マイナーバージョンを更新するかを示す `boolean` 値。 この例では、メジャーバージョンの値を増分す `true` ることを示す値が渡されます。
   * 残り `null` の2つのパラメーターに対してを渡します。

**関連トピック**

[リソースの更新](aem-forms-repository.md#updating-resources)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## リソースの検索 {#searching-for-resources}

リポジトリ内のリソース（履歴、関連リソース、プロパティなど）を検索するために使用するクエリを作成できます。

関連するリソースを取得して、フォームとそのフラグメントとの依存関係を判断できます。 例えば、フォームに使用するフラグメントや外部リソースを調べることができます。 画像がある場合は、その画像がどのフォームで使用されているかを調べることもできます。 また、プロパティに基づくフィルタリングを使用して、関連するリソースを検索することもできます。 例えば、指定した名前の画像を使用するすべてのフォームを検索したり、指定した名前のフォームで使用されている画像を検索したりできます。 また、リソースプロパティを使用して検索することもできます。 例えば、「%」や「_」のワイルドカードを含む名前開始を持つすべてのフォームやリソースを検索するクエリを実行できます。 プロパティに基づく検索は関係に基づくものではないことに注意してください。このような検索は、特定のリソースに関する特定の知識があるという前提に基づいています。

**クエリ文**

*クエリには* 、条件を使用して論理的に結合された1つ以上の文が含まれます。 ス *テートメント* は、左辺オペランド、演算子、右辺オペランドで構成されます。 また、検索結果に使用する並べ替え順を指定できます。 *並べ替え順* には、SQL `ORDER BY` 句と同等の情報が含まれ、検索の基準となる属性を含む要素と、昇順または降順のどちらを使用するかを示す値で構成されます。

RepositoryサービスJava APIを使用して、プログラムによってリソースを検索できます。 現時点では、WebサービスAPIを使用してリソースを検索することはできません。

**並べ替え動作**

オブジェクトのメソッドを呼び出して、並べ替え順を指定する場合、並べ替え順は考慮されません `ResourceRepositoryClient``searchProperties` 。 例えば、属性名が `name`、、およびの3つのカスタムプロパティを持つリソースを作成するとしま `secondName``asecondName`す。 次に、属性名に並べ替え順要素を作成し、 `ascending` 値をに設定し `true`ます。

次に、 `ResourceRepositoryClient` オブジェクトの `searchProperties` メソッドを呼び出し、並べ替え順で渡します。 3つのプロパティを持つ正しいリソースが検索結果に返されます。 ただし、プロパティは属性名で並べ替えられません。 これらは、追加された順に返されます。 `name`、 `secondName`および `asecondName`。

>[!NOTE]
>
>For more information about the Repository service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-5}

リソースを検索するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. Repositoryサービスクライアントを作成します。
1. 検索するターゲットフォルダーを指定します。
1. 検索で使用する属性を指定します。
1. 検索で使用するクエリを作成します。
1. 検索結果の並べ替え順を作成します。
1. リソースを検索します。
1. 検索結果からリソースを取得します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを含めます。

**サービスクライアントの作成**

プログラムでリソースを読み取る前に、接続を確立し、秘密鍵証明書を提供する必要があります。 これは、サービスクライアントを作成することで実行されます。

**検索用のターゲットフォルダーを指定する**

検索の実行元となる基本パスを含む文字列を作成します。 構文には、次の例のようにスラッシュが含まれます。&quot;/*path*/*folder*&quot;

**検索で使用する属性を指定する**

リソースに含まれる属性に基づいて検索を行うことができます。 検索を実行する属性の値を指定します。

**検索で使用するクエリの作成**

文と条件を使用してクエリを作成します。 各文では、検索の基にする属性、使用する条件、検索で使用する属性値を指定します。

**検索結果の並べ替え順を作成する**

並べ替え順は、要素で構成されます。各要素には、検索で使用される属性の1つと、昇順または降順のどちらを使用するかを示す値が含まれます。

**リソースの検索**

フォルダー、クエリおよび並べ替え順を使用して、リソースを検索します。 さらに、検索の深さと、返される結果数の上限を示します。

**検索結果からリソースを取得**

返されたリストのリソースを繰り返し処理し、さらに処理するために情報を抽出します。

**関連トピック**

[Java APIを使用したリソースの検索](aem-forms-repository.md#search-for-resources-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Repository Service APIクイック開始](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java APIを使用したリソースの検索 {#search-for-resources-using-the-java-api}

RepositoryサービスAPI(Java)を使用してリソースを検索します。

1. プロジェクトファイルを含める

   JavaプロジェクトのクラスパスにクライアントJARファイルを含めます。

1. サービスクライアントの作成

   コンストラクタを使用し、接続プロパティを含むオブジェクトを渡して、 `ResourceRepositoryClient``ServiceClientFactory` オブジェクトを作成します。

1. 検索用のターゲットフォルダーを指定する

   検索の実行元となるベースパスのURIを指定します。 この例では、リソースのURIはです `/testFolder`。

1. 検索で使用する属性を指定する

   検索を実行する属性の値を指定します。 属性は `com.adobe.repository.infomodel.bean.Resource` オブジェクト内に存在します。 この例では、name属性に対して検索が実行されます。したがって、 `java.lang.String` オブジェクトの名前を `Resource` 含む名前が使用されます(この場合 `testResource` )。

1. 検索で使用するクエリの作成

   クエリを作成するには、クラスのデフォルトコンストラクタを呼び出して `com.adobe.repository.query.Query` オブジェクトを作成し、 `Query` クエリにステートメントを追加します。

   ステートメントを作成するには、クラスのコンストラクターを呼び出し、次のパラメーターを `com.adobe.repository.query.Query.Statement` 渡します。

   * リソース属性定数を含む左辺オペランド。 この例では、リソース名が検索の基礎として使用されるので、静的な値 `Resource.ATTRIBUTE_NAME` が使用されます。
   * 属性の検索で使用される条件を含む演算子。 演算子は、クラス内の静的定数の1つである必要があり `Query.Statement` ます。 この例では、静的な値 `Query.Statement.OPERATOR_BEGINS_WITH` が使用されます。
   * 検索を実行する属性値を含む右辺オペランド。 この例では、値を `String` 含むname属性が使用さ `"testResource"`れます。

   オブジェクトの `Query.Statement` メソッドを呼び出し、クラスに含まれる静的な値の1つを渡すことで、左辺オペランドの名前空間を指定し `setNamespace``com.adobe.repository.infomodel.bean.ResourceProperty` ます。 この例では、が使用され `ResourceProperty.RESERVED_NAMESPACE_REPOSITORY` ています。

   オ追加ブジェクトのメソッドを呼び出し、オブジェクトを渡すことで、各ステートメントをクエリに送信し `Query``addStatement``Query.Statement` ます。

1. 検索結果の並べ替え順を作成する

   検索結果で使用する並べ替え順を指定するには、クラスのデフォルトのコンストラクタを呼び出して `com.adobe.repository.query.sort.SortOrder` オブジェクトを作成し、 `SortOrder` 並べ替え順に要素を追加します。

   並べ替え順の要素を作成するには、クラスのコンストラクタの1つを呼び出し `com.adobe.repository.query.sort.SortOrder.Element` ます。 この例では、リソースの名前が検索の基礎として使用されるので、静的な値 `Resource.ATTRIBUTE_NAME` が最初のパラメーターとして使用され、昇順(値の `boolean` 値 `true`)が2番目のパラメーターとして指定されます。

   各要素追加の並べ替え順を変更するには、 `SortOrder` オブジェクトの `addSortElement` メソッドを呼び出して、オブジェクトを渡し `SortOrder.Element` ます。

1. リソースの検索

   属性プロパティに `resources` 基づいて検索するには、 `ResourceRepositoryClient` オブジェクトの `searchProperties` メソッドを呼び出し、次のパラメーターを渡します。

   * 検索を実行する基本パスを `String` 含む。 この場合、が使用 `"/testFolder"` されます。
   * 検索で使用されるクエリ。
   * 検索の深さ。 この場合、 `com.adobe.repository.infomodel.bean.ResourceCollection.DEPTH_INFINITE` は、ベースパスとそのすべてのフォルダーが使用されることを示すために使用されます。
   * ページ解除された結果セットを選択する最初の行を示す `int` 値。 この例では、を指定 `0` します。
   * 返される結果の最大数を示す `int` 値。 この例では、を指定 `10` します。
   * 検索で使用される並べ替え順。

   このメソッドは、指定された並べ替え順 `java.util.List` で一連の `Resource` オブジェクトを返します。

1. 検索結果からリソースを取得

   検索結果に含まれるリソースを取得するには、を繰り返し実行し、各オブジェクトをにキャストし `List` て情報 `Resource` を抽出します。 この例では、各リソースの名前が表示されます。

**関連トピック**

[リソースの検索](aem-forms-repository.md#searching-for-resources)

[クイック開始（SOAPモード）:Java APIを使用したリソースの検索](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## リソースの関係の作成 {#creating-resource-relationships}

リポジトリ内のリソース間の関係を指定できます。 関係には次の3種類があります。

* **依存**:リソースが他のリソースに依存する関係。つまり、関連するすべてのリソースがリポジトリ内で必要になります。
* **メンバーシップ（ファイルシステム）**:特定のフォルダー内にあるリソースの関係。
* **カスタム**:リソース間で指定する関係。 例えば、あるリソースが非推奨で、別のリソースがリポジトリに導入された場合、独自の置き換え関係を指定できます。

独自のカスタムリレーションシップを作成できます。 例えば、HTMLファイルをリポジトリに格納し、そのファイルで画像を使用する場合、カスタムの関係を指定してHTMLファイルと画像を関連付けることができます（通常はXMLファイルのみがリポジトリ定義の依存関係を使用して画像に関連付けられます）。 別の例として、ツリー構造ではなく循環グラフ構造を使用して、リポジトリの別の表示を構築する場合が考えられます。 ビューアと共に円グラフを定義して、これらの関係を横断できます。 最後に、2つのリソースが完全に異なる場合でも、1つのリソースが別のリソースを置き換えることを示すことができます。 その場合は、予約範囲外の関係タイプを定義して、これらの2つのリソース間に関係を作成できます。 アプリケーションは、関係を検出して処理できる唯一のクライアントであり、その関係を検索する際に使用できます。

RepositoryサービスJava APIまたはWebサービスAPIを使用して、プログラムによってリソース間の関係を指定できます。

>[!NOTE]
>
>For more information about the Repository service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-6}

2つのリソース間の関係を指定するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. Repositoryサービスクライアントを作成します。
1. 関連付けるリソースのURIを指定します。
1. 関係を作成します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを含めます。

**サービスクライアントの作成**

プログラムでリソースを読み取る前に、接続を確立し、秘密鍵証明書を提供する必要があります。 これは、サービスクライアントを作成することで実行されます。

**関連付けるリソースのURIを指定します**

関連付けるリソースのURIを含む文字列を作成します。 構文には、次の例のようにスラッシュが含まれます。&quot;/*path*/*resource*&quot;

**関係の作成**

Repositoryサービスメソッドを呼び出して、関係のタイプを作成および指定します。

**関連トピック**

[Java APIを使用した関係リソースの作成](aem-forms-repository.md#create-relationship-resources-using-the-java-api)

[WebサービスAPIを使用した関係リソースの作成](aem-forms-repository.md#create-relationship-resources-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Repository Service APIクイック開始](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java APIを使用した関係リソースの作成 {#create-relationship-resources-using-the-java-api}

RepositoryサービスのJava APIを使用して関係リソースを作成し、次のタスクを実行します。

1. プロジェクトファイルを含める

   JavaプロジェクトのクラスパスにクライアントJARファイルを含めます。

1. サービスクライアントの作成

   コンストラクタを使用し、接続プロパティを含むオブジェクトを渡して、 `ResourceRepositoryClient``ServiceClientFactory` オブジェクトを作成します。

1. 関連付けるリソースのURIの指定

   関連付けるリソースのURIを指定します。 この場合、リソースには名前が付けられ `testResource1` 、という名前のフォルダー `testResource2` に格納されているので、URI `testFolder`はとになり `"/testFolder/testResource1"` ま `"/testFolder/testResource2"`す。 URIはオブジェクトとして保存され `java.lang.String` ます。 この例では、リソースは最初にリポジトリに書き込まれ、そのURIが取得されます。 リソースの作成の詳細については、「リソースの [作成](aem-forms-repository.md#writing-resources)」を参照してください。

1. 関係の作成

   オブジェクトの `ResourceRepositoryClient``createRelationship` メソッドを呼び出し、次のパラメーターを渡します。

   * ソースリソースのURIです。
   * ターゲットリソースのURIです。
   * 関係のタイプ。クラス内の静的定数の1つ `com.adobe.repository.infomodel.bean.Relation` です。 この例では、値を指定して依存関係を確立し `Relation.TYPE_DEPENDANT_OF`ます。
   * 新しい先頭リソースの識別子に対して、ターゲットリソースを自動的に更新する `boolean``com.adobe.repository.infomodel.Id`かどうかを示す値。 この例では、依存関係があるので、値が指定さ `true` れています。

   また、オブジェクトのメソッドを呼び出し、次のパラメーターを渡すことで、特定のリソースに関連するリソースのリスト `ResourceRepositoryClient` を取得するこ `getRelated` ともできます。

   * 関連するリソースを取得するリソースのURIです。 この例では、ソースリソース( `"/testFolder/testResource1"`)が指定されています。
   * 指定したリソースが関係のソースリソースであるかどうかを示す `boolean` 値。 この例では、値が指定されています。こ `true` れは、この場合のみです。
   * 関係タイプ。クラス内の静的定数の1つ `Relation` です。 この例では、依存関係は、前に使用したのと同じ値を使用して指定します。 `Relation.TYPE_DEPENDANT_OF`.

   この `getRelated` メソッドは、繰り返し処理を行って各関連リソースを取得し、に含まれるオブジェクトをキャストするこ `java.util.List` とで、そのようにオブジェクト `Resource` を返 `List``Resource` します。 この例では、は返されるリソース `testResource2` のリストにあると想定されます。

**関連トピック**

[リソースの関係の作成](aem-forms-repository.md#creating-resource-relationships)

[クイック開始（SOAPモード）:Java APIを使用したリソース間の関係の作成](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-relationships-between-resources-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用した関係リソースの作成 {#create-relationship-resources-using-the-web-service-api}

Repository API（Webサービス）を使用して、次の関係リソースを作成します。

1. プロジェクトファイルを含める

   * リポジトリWSDLを使用するMicrosoft .NETクライアントアセンブリを作成します。
   * Microsoft .NETクライアントアセンブリを参照します。

1. サービスクライアントの作成

   Microsoft .NETクライアントアセンブリを使用して、デフォルトのコンストラクタを呼び出して `RepositoryServiceService` オブジェクトを作成します。 ユーザー名とパスワードを含む `Credentials``System.Net.NetworkCredential` オブジェクトを使用して、このプロパティを設定します。

1. 関連付けるリソースのURIの指定

   関連付けるリソースのURIを指定します。 この場合、リソースには名前が付けられ `testResource1` 、という名前のフォルダー `testResource2` に格納されているので、URI `testFolder`はとになり `"/testFolder/testResource1"` ま `"/testFolder/testResource2"`す。 Microsoft .NET Framework（C#など）に準拠した言語を使用する場合、URIは `System.String` オブジェクトとして保存されます。 この例では、リソースは最初にリポジトリに書き込まれ、そのURIが取得されます。 リソースの作成の詳細については、「リソースの [作成](aem-forms-repository.md#writing-resources)」を参照してください。

1. 関係の作成

   オブジェクトの `RepositoryServiceService``createRelationship` メソッドを呼び出し、次のパラメーターを渡します。

   * ソースリソースのURIです。
   * ターゲットリソースのURIです。
   * 関係のタイプ。 この例では、値を指定して依存関係を確立し `3`ます。
   * 関係タイプが指定されたかどうかを示す `boolean` 値。 この例では、値が指定さ `true` れています。
   * 新しい先頭リソースの識別子に対して、ターゲットリソースを自動的に更新する `boolean``Id`かどうかを示す値。 この例では、依存関係があるので、値が指定さ `true` れています。
   * ターゲットヘッドが指定されたかどうかを示す `boolean` 値。 この例では、値が指定さ `true` れています。
   * 最後 `null` のパラメーターに対してを渡します。

   また、オブジェクトのメソッドを呼び出し、次のパラメーターを渡すことで、特定のリソースに関連するリソースのリスト `RepositoryServiceService` を取得するこ `getRelated` ともできます。

   * 関連するリソースを取得するリソースのURIです。 この例では、ソースリソース( `"/testFolder/testResource1"`)が指定されています。
   * 指定したリソースが関係のソースリソースであるかどうかを示す `boolean` 値。 この例では、値が指定されています。こ `true` れは、この場合のみです。
   * ソースリソースが指定されたかどうかを示す `boolean` 値。 この例では、値が指定さ `true` れています。
   * 関係タイプを含む整数の配列。 この例では、以前に使用したのと同じ値を配列に使用して、依存関係を指定します。 `3`.
   * 残り `null` の2つのパラメーターに対してを渡します。

   この `getRelated``Resource` メソッドは、オブジェクトにキャストできるオブジェクトの配列を返します。この配列を使用して、関連する各リソースを取得するために繰り返し実行できます。 この例では、は返されるリソース `testResource2` のリストにあると想定されます。

**関連トピック**

[リソースの関係の作成](aem-forms-repository.md#creating-resource-relationships)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## リソースのロック {#locking-resources}

特定のユーザーが排他的に使用するため、または複数のユーザー間で共有を使用するために、リソースまたはリソースのセットをロックできます。 共有ロックは、リソースに何かが起こることを示しますが、他の誰もがそのリソースに対して行動を起こすのを妨げることはありません。 共有ロックは、シグナリングメカニズムと見なす必要があります。 排他的ロックとは、リソースをロックしたユーザーがリソースを変更することを意味し、ロックは、ユーザーがリソースにアクセスする必要がなくなり、ロックを解除するまで、他のユーザーがリソースを変更できないようにします。 リポジトリ管理者がリソースをロック解除すると、そのリソース上の排他的ロックと共有ロックがすべて自動的に削除されます。 この種のアクションは、ユーザーが使用できなくなり、リソースのロックが解除されなくなった場合に使用します。

リソースをロックすると、次の図に示すように、Workbenchの「リソース」タブに表示すると、ロックアイコンが表示されます。

![lr_lr_lockrepository](assets/lr_lr_lockrepository.png)

RepositoryサービスJava APIまたはWebサービスAPIを使用して、リソースへのアクセスをプログラムで制御できます。

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

プログラムでリソースを読み取る前に、接続を確立し、秘密鍵証明書を提供する必要があります。 これは、サービスクライアントを作成することで実行されます。

**ロックするリソースのURIを指定します**

ロックするリソースのURIを含む文字列を作成します。 構文には、次の例のようにスラッシュが含まれます。&quot;/*path*/*resource*&quot;

**リソースのロック**

Repositoryサービスメソッドを呼び出して、リソースをロックし、URI、ロックの種類、ロックの深さを指定します。

**リソースのロックを取得する**

URIを指定して、Repositoryサービスメソッドを呼び出して、リソースのロックを取得します。

**リソースのロック解除**

URIを指定してリソースのロックを解除するには、Repositoryサービスメソッドを呼び出します。

**関連トピック**

[Java APIを使用したリソースのロック](aem-forms-repository.md#lock-resources-using-the-java-api)

[WebサービスAPIを使用したリソースのロック](aem-forms-repository.md#lock-resources-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Repository Service APIクイック開始](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java APIを使用したリソースのロック {#lock-resources-using-the-java-api}

RepositoryサービスAPI(Java)を使用してリソースをロックする：

1. プロジェクトファイルを含める

   JavaプロジェクトのクラスパスにクライアントJARファイルを含めます。

1. サービスクライアントの作成

   コンストラクタを使用し、接続プロパティを含むオブジェクトを渡して、 `ResourceRepositoryClient``ServiceClientFactory` オブジェクトを作成します。

1. ロックするリソースのURIを指定します

   ロックするリソースのURIを指定します。 この場合、という名前のリソース `testResource` はという名前のフォルダーにあるので `testFolder`、そのURIは `"/testFolder/testResource"`です。 URIは `java.lang.String` オブジェクトとして保存されます。

1. リソースのロック

   オブジェクトの `ResourceRepositoryClient``lockResource` メソッドを呼び出し、次のパラメーターを渡します。

   * リソースのURI。
   * ロックの範囲。 この例では、リソースは排他的に使用するためにロックされるので、ロック範囲はに指定し `com.adobe.repository.infomodel.bean.Lock.SCOPE_EXCLUSIVE`ます。
   * ロックの深さ。 この例では、ロックは特定のリソースにのみ適用され、メンバーや子は適用されないので、ロックの深さはに指定し `Lock.DEPTH_ZERO`ます。

   >[!NOTE]
   >
   >4つのパラメーターを必要とするオーバーロードされたバージョンの `lockResource` メソッドでは、例外がスローされます。 このチュートリアルに示すように、3つのパラメータを必要とする `lockResource` メソッドを使用してください。

1. リソースのロックを取得する

   オブジェクトの `ResourceRepositoryClient``getLocks` メソッドを呼び出し、リソースのURIをパラメーターとして渡します。 繰り返し処理が可能なLockオブジェクトのリストを返します。 この例では、各Lockオブジェクトのメソッド、メソッド、およびメソッドをそれぞれ呼び出して、各オブジェクトのロック所有者、深さ、スコープ `getOwnerUserId`を印刷し `getDepth``getType` ます。

1. リソースのロック解除

   オブジェクトの `ResourceRepositoryClient``unlockResource` メソッドを呼び出し、リソースのURIをパラメーターとして渡します。 詳しくは、 [AEM FormsAPIリファレンスを参照してください](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

**関連トピック**

[リソースのロック](aem-forms-repository.md#locking-resources)

[クイック開始（SOAPモード）:Java APIを使用したリソースのロック](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-locking-a-resource-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したリソースのロック {#lock-resources-using-the-web-service-api}

RepositoryサービスAPI（Webサービス）を使用してリソースをロックするには：

1. プロジェクトファイルを含める

   * Base64を使用してリポジトリWSDLを使用するMicrosoft .NETクライアントアセンブリを作成します。
   * Microsoft .NETクライアントアセンブリを参照します。

1. サービスクライアントの作成

   Microsoft .NETクライアントアセンブリを使用して、デフォルトのコンストラクタを呼び出して `RepositoryServiceService` オブジェクトを作成します。 ユーザー名とパスワードを含む `Credentials``System.Net.NetworkCredential` オブジェクトを使用して、このプロパティを設定します。

1. ロックするリソースのURIを指定します

   ロックするリソースのURIを含む文字列を指定します。 この場合、という名前のリソース `testResource` はフォルダー内にあるので、そのURI `testFolder`は `"/testFolder/testResource"`です。 Microsoft .NET Frameworkに準拠した言語（C#など）を使用する場合は、URIを `System.String` オブジェクトに格納します。

1. リソースのロック

   オブジェクトの `RepositoryServiceService``lockResource` メソッドを呼び出し、次のパラメーターを渡します。

   * リソースのURI。
   * ロックの範囲。 この例では、リソースは排他的に使用するためにロックされるので、ロック範囲はに指定し `11`ます。
   * ロックの深さ。 この例では、ロックは特定のリソースにのみ適用され、メンバーや子は適用されないので、ロックの深さはに指定し `2`ます。
   * ロックが期限切れになるまでの秒数を示す `int` 値。 この例では、の値が使用さ `1000` れます。
   * 最後 `null` のパラメーターに対してを渡します。

1. リソースのロックを取得する

   オブジェクトの `RepositoryServiceService` メソッドを呼び出し、リソースのURIを最初のパラメーターとして渡し、2番目のパラメーター `getLocks``null` として渡します。 このメソッドは、反復可能な `object``Lock` オブジェクトを含む配列を返します。 この例では、各オブジェクトのロック所有者、深さ、範囲は、各 `Lock` オブジェクトの `ownerUserId``depth``type` フィールド、深さ、スコープにそれぞれアクセスすることで印刷されます。

1. リソースのロック解除

   オブジェクトの `RepositoryServiceService` メソッドを呼び出し、リソースのURIを最初のパラメーターとして渡し、2番目のパラメーター `unlockResource``null` として渡します。

**関連トピック**

[リソースのロック](aem-forms-repository.md#locking-resources)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## リソースの削除 {#deleting-resources}

RepositoryサービスJava API(SOAP)を使用すると、リポジトリ内の特定の場所からリソースをプログラムで削除できます。

リソースを削除する場合、削除は通常は永続的ですが、ECMリポジトリは履歴メカニズムに従ってリソースのバージョンを保存する場合があります。 したがって、リソースを削除する場合は、そのリソースが再び必要にならないことを確認することが重要です。 リソースを削除する一般的な理由としては、データベースの使用可能な領域を増やす必要があることが挙げられます。 リソースのバージョンは削除できますが、削除する場合は、そのリソースの論理識別子(LID)やパスではなく、リソースの識別子を指定する必要があります。 フォルダーを削除すると、サブフォルダーやリソースを含む、そのフォルダー内のすべての要素が自動的に削除されます。

関連するリソースは削除されません。 例えば、logo.gifファイルを使用するフォームがあり、logo.gifを削除すると、保留中の関係テーブルに関係が保存されます。 別の方法として、バージョンの非推奨の場合は、最新バージョンのオブジェクトステータスを非推奨に設定します。

ECMシステムでは、削除操作はトランザクションに対して安全ではありません。 例えば、100個のリソースを削除しようとした場合に、50個目のリソースで操作が失敗すると、最初の49個のインスタンスは削除されますが、残りは削除されません。 それ以外の場合、デフォルトの動作はrollback (non-commitment)です。

>[!NOTE]
>
>ECMリポジトリ（EMC Documentum Content ServerおよびIBM FileNet P8 Content Manager）で `com.adobe.repository.bindings.dsc.client.ResourceRepositoryClient.deleteResources()` メソッドを使用する場合、指定されたリソースの1つに対して削除が失敗した場合、トランザクションはロールバックされません。つまり、削除されたファイルは削除を取り消すことができません。

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

プログラムでリソースを読み取る前に、接続を確立し、秘密鍵証明書を提供する必要があります。 これは、サービスクライアントを作成することで実行されます。

**削除するリソースのURIを指定します**

削除するリソースのURIを含む文字列を作成します。 構文には、次の例のようにスラッシュが含まれます。&quot;/*path*/*resource*&quot; 削除するリソースがフォルダーの場合、削除は再帰的に行われます。

**リソースの削除**

URIを指定してリソースを削除するには、Repositoryサービスメソッドを呼び出します

**関連トピック**

[Java APIを使用したリソースの削除](aem-forms-repository.md#delete-resources-using-the-java-api-soap)

[WebサービスAPIを使用したリソースの削除](aem-forms-repository.md#delete-resources-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Repository Service APIクイック開始](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java API(SOAP)を使用したリソースの削除 {#delete-resources-using-the-java-api-soap}

リポジトリAPI(Java)を使用してリソースを削除します。

1. プロジェクトファイルを含める

   JavaプロジェクトのクラスパスにクライアントJARファイルを含めます。

1. サービスクライアントの作成

   コンストラクタを使用し、接続プロパティを含むオブジェクトを渡して、 `ResourceRepositoryClient``ServiceClientFactory` オブジェクトを作成します。

1. 削除するリソースのURIを指定します

   取得するリソースのURIを指定します。 この場合、testResourceToBeDeletedという名前のリソースはtestFolderという名前のフォルダーにあるので、そのURIはで `/testFolder/testResourceToBeDeleted`す。 URIは `java.lang.String` オブジェクトとして保存されます。 この例では、リソースは最初にリポジトリに書き込まれ、そのURIが取得されます。 リソースの作成の詳細については、「リソースの [作成](aem-forms-repository.md#writing-resources)」を参照してください。

1. リソースの削除

   オブジェクトの `ResourceRepositoryClient``deleteResource` メソッドを呼び出し、リソースのURIをパラメーターとして渡します。

**関連トピック**

[リソースの削除](aem-forms-repository.md#deleting-resources)

[クイック開始（SOAPモード）:Java APIを使用したリソースの検索](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したリソースの削除 {#delete-resources-using-the-web-service-api}

Repository API（Webサービス）を使用してリソースを削除します。

1. プロジェクトファイルを含める

   * Base64を使用してリポジトリWSDLを使用するMicrosoft .NETクライアントアセンブリを作成します。
   * Microsoft .NETクライアントアセンブリを参照します。

1. サービスクライアントの作成

   Microsoft .NETクライアントアセンブリを使用して、デフォルトのコンストラクタを呼び出して `RepositoryServiceService` オブジェクトを作成します。 ユーザー名とパスワードを含む `Credentials``System.Net.NetworkCredential` オブジェクトを使用して、このプロパティを設定します。

1. 削除するリソースのURIを指定します

   取得するリソースのURIを指定します。 この場合、という名前のリソース `testResourceToBeDeleted` はという名前のフォルダーにあるので `testFolder`、そのURIは `"/testFolder/testResourceToBeDeleted"`です。 この例では、リソースは最初にリポジトリに書き込まれ、そのURIが取得されます。 リソースの作成の詳細については、「リソースの [作成](aem-forms-repository.md#writing-resources)」を参照してください。

1. リソースの削除

   オブジェクトの `RepositoryServiceService` メソッドを呼び出し、リソースのURIを含む `deleteResources``System.String` 配列を最初のパラメーターとして渡します。 2番目 `null` のパラメーターに対してを渡します。

**関連トピック**

[リソースの削除](aem-forms-repository.md#deleting-resources)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
