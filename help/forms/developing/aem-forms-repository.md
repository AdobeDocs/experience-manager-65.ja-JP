---
title: AEM Formsリポジトリの操作
seo-title: AEM Formsリポジトリの操作
description: AEM Formsリポジトリを管理し、Java APIとWebサービスAPIを使用して、フォルダーの作成、書き込み、リスト、読み取り、更新および検索をおこないます。 さらに、リソースの関係の作成、リソースのロックと削除の方法についても説明します。
seo-description: Java APIとWebサービスAPIを使用して、AEM Formsリポジトリを管理し、フォルダーの作成、書き込み、リスト、読み取り、リソースの更新、およびリソースの検索をおこないます。 さらに、リソースの関係の作成、リソースのロックと削除の方法についても説明します。
uuid: 6ead49f9-ca0d-4ee4-86a6-0a9ced6ec4f8
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d2c95881-6c02-4e34-85af-84607df54287
role: Developer
exl-id: a07e51ca-fea0-4719-8071-1b7e805de2ae
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '9157'
ht-degree: 2%

---

# AEM Formsリポジトリの操作{#working-with-aem-forms-repository}

**このドキュメントのサンプルと例は、JEE上のAEM Forms環境に限られています。**

**Repositoryサービスについて**

Repositoryサービスは、リソースストレージと管理サービスをAEM Formsに提供します。 開発者が&#x200B;*AEM Forms*&#x200B;アプリケーションを作成すると、ファイルシステムではなくリポジトリにアセットをデプロイできます。 アセットには、XML 形式、PDF 形式（Acrobat 形式を含む）、フォームのフラグメント、画像、プロファイル、ポリシー、SWF ファイル、DDX ファイル、XML スキーマ、WSDL ファイルおよびテストデータなど、任意のタイプのコラテラルが含まれます。

例えば、次のFormsアプリケーションの名前が&#x200B;*Applications/FormsApplication*&#x200B;であるとします。

![ww_ww_formrepository](assets/ww_ww_formrepository.png)

FormsFolder内にLoan.xdpという名前のファイルが存在することに注意してください。 このフォームデザインにアクセスするには、完全パス（バージョンを含む）を指定します。`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.

>[!NOTE]
>
>Workbenchを使用したFormsアプリケーションの作成について詳しくは、[Workbenchヘルプ](https://www.adobe.com/go/learn_aemforms_workbench_63)を参照してください。

AEM Formsリポジトリ内のリソースへのパスは次のとおりです。

`Applications/Application-name/Application-version/Folder.../Filename`

次に、URI値の例を示します。

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

>[!NOTE]
>
>Webブラウザーを使用してAEM Formsリポジトリを参照できます。 リポジトリを参照するには、Webブラウザーに次のURLを入力します`https://[server name]:[server port]/repository`。 Webブラウザーを使用して、「 AEM Formsリポジトリの操作」セクションに関連するクイックスタートの結果を確認できます。 例えば、AEM Formsリポジトリにコンテンツを追加すると、そのコンテンツをWebブラウザーで表示できます。 ([クイックスタート（SOAPモード）を参照):Java API](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)を使用したリソースの書き込み)。

リポジトリAPIは、リポジトリから情報を保存および取得するために使用できる操作を多数提供します。 例えば、リソースのリストを取得したり、アプリケーションの処理の一環としてリソースが必要な場合にリポジトリに保存されている特定のリソースを取得したりできます。

>[!NOTE]
>
>リポジトリAPIは、Content Services（非推奨）とのやり取りには使用できません。 Content Services（非推奨）とやり取りするには、Document Management APIを使用します。

RepositoryサービスAPIを使用すると、次のタスクを実行できます。

* フォルダーの作成. [フォルダーの作成](aem-forms-repository.md#creating-folders)を参照してください。
* リソースとそのプロパティを書き込みます。 [リソースの書き込み](aem-forms-repository.md#writing-resources)を参照してください。
* 特定のコレクション内または他のリソースに関連するリソースのリスト。 [リソースのリスト](aem-forms-repository.md#listing-resources)を参照してください。
* リソースとそのプロパティを読み取ります。 [リソースの読み取り](aem-forms-repository.md#reading-resources)を参照してください。
* リソースとそのプロパティを更新します。 [リソースの更新](aem-forms-repository.md#updating-resources)を参照してください。
* 履歴、関連リソース、プロパティなどのリソースを検索します。 [リソースの検索](aem-forms-repository.md#searching-for-resources)を参照してください。
* リソース間の関係を指定します。 [リソースの関係の作成](aem-forms-repository.md#creating-resource-relationships)を参照してください。
* リソースのロックとロック解除、アクセス制御リスト(ACL)の読み取りと書き込みを含む、リソースアクセス制御の管理。 [リソースのロック](aem-forms-repository.md#locking-resources)を参照してください。
* リソースとそのプロパティを削除します。 [リソースの削除](aem-forms-repository.md#deleting-resources)を参照してください。

>[!NOTE]
>
>リポジトリAPIを使用する場合、ECMリポジトリを使用して、リソースアクセス制御の管理、リソースの検索、リソースの関係の指定を行うことはできません。

>[!NOTE]
>
>暗号化されたPDFがリポジトリに書き込まれると、自動関係抽出機能は使用できません。 そうしないと、暗号化されたPDFをリポジトリに保存し、後で取得できます。 PDFをリポジトリから取得した後で、そのPDFを復号化することもできます。

>[!NOTE]
>
>Repositoryサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

## フォルダーの作成 {#creating-folders}

フォルダー（リソースコレクション）は、オブジェクト（ファイルまたはリソース）を整理されたグループに格納するために使用されます。 フォルダーには、リソースやその他のフォルダー（サブフォルダーとも呼ばれます）を含めることができます。 リソースは一度に1つのフォルダーにしか保存できません。

ファイルはフォルダーからアクセス制御リスト(ACL)を継承し、サブフォルダーは親フォルダーからACLを継承します。 したがって、子フォルダーを作成するには、親フォルダーが存在する必要があります。 IDEでは、ファイル単位ではなく、フォルダー単位でのみ操作できます。 フォルダーのバージョンを設定することはできず、必要ありません。フォルダーには、データ自体は含まれません。 データを含むリソースのコンテナにすぎません。 デフォルトのACLはシステムレベルの権限です。つまり、ユーザーが特定のフォルダーに対する権限を付与されるまで、システムレベルの権限（読み取り、書き込み、トラバース、ACLの管理）が必要です。 ACLはIDEでのみ機能します。

>[!NOTE]
>
>Repositoryサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順の概要{#summary-of-steps}

フォルダーを作成するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. サービスクライアントを作成します。
1. フォルダーを作成します。
1. フォルダーをリポジトリに書き込みます。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを含めます。

**サービスクライアントの作成**

プログラムによってリソース収集を作成する前に、接続を確立し、資格情報を指定する必要があります。 これは、サービスクライアントを作成することで実現されます。

**フォルダーの作成**

Repositoryサービスメソッドを呼び出して、リソースコレクションを作成し、UUID、フォルダー名、説明などの識別情報をリソースコレクションに設定します。

**フォルダーをリポジトリに書き込みます。**

Repositoryサービスメソッドを呼び出して、ターゲットフォルダーのURIを指定してリソースコレクションを書き込みます。

**関連トピック**

[Java APIを使用したフォルダーの作成](aem-forms-repository.md#create-folders-using-the-java-api)

[WebサービスAPIを使用したフォルダーの作成](aem-forms-repository.md#create-folders-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[リポジトリサービスAPIのクイックスタート](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java API {#create-folders-using-the-java-api}を使用したフォルダーの作成

RepositoryサービスAPI(Java)を使用してフォルダーを作成します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスにプロジェクトファイルを含めます。

1. サービスクライアントの作成

   コンストラクターを使用し、接続プロパティを含む`ServiceClientFactory`オブジェクトを渡して、`ResourceRepositoryClient`オブジェクトを作成します。

1. フォルダーの作成

   リソースコレクションを作成するには、まず`com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean`オブジェクトを作成する必要があります。

   `repositoryInfomodelFactoryBean`オブジェクトの`newResourceCollection`メソッドを呼び出し、次のパラメーターを渡します。

   * リソースに割り当てる`com.adobe.repository.infomodel.Id` UUID識別子。
   * リソースに割り当てる`com.adobe.repository.infomodel.Lid` UUID識別子。
   * リソースコレクションの名前を含む`java.lang.String`。 （例：`FormsFolder`）。

   このメソッドは、新しいフォルダーを表す`com.adobe.repository.infomodel.bean.ResourceCollection`オブジェクトを返します。

   `setDescription`メソッドを使用してフォルダーの説明を設定し、次のパラメーターを渡します。

   * リソースの収集を表す`String`。 この例では、`"test Folder"`が`.`として使用されます。


1. フォルダーをリポジトリに書き込みます。

   `ResourceRepositoryClient`オブジェクトの`writeResource`メソッドを呼び出して、フォルダーと`ResourceCollection`オブジェクトのURIを渡します。 例えば、フォルダーへのURIは`/Applications/FormsApplication/1.0/`のようになります。

   メソッドは、新しく作成された`com.adobe.repository.infomodel.bean.Resource`オブジェクトのインスタンスを返します。 例えば、`com.adobe.repository.infomodel.bean.Resource`オブジェクトの`getId`メソッドを呼び出すことで、新しいリソースの識別子の値を取得できます。

**関連トピック**

[フォルダーの作成](aem-forms-repository.md#creating-folders)

[クイックスタート（SOAPモード）:Java APIを使用したフォルダーの作成](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-a-folder-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したフォルダーの作成{#create-folders-using-the-web-service-api}

RepositoryサービスAPI（Webサービス）を使用してフォルダーを作成します。

1. プロジェクトファイルを含める

   * base64を使用してリポジトリWSDLを使用するMicrosoft .NETクライアントアセンブリを作成します。
   * Microsoft .NETクライアントアセンブリを参照します。

1. サービスクライアントの作成

   Microsoft .NETクライアントアセンブリを使用して、デフォルトのコンストラクタを呼び出して`RepositoryServiceService`オブジェクトを作成します。 ユーザー名とパスワードを含む`System.Net.NetworkCredential`オブジェクトを使用して、 `Credentials`プロパティを設定します。

1. フォルダーの作成

   `ResourceCollection`クラスのデフォルトのコンストラクターを使用してフォルダーを作成し、次のパラメーターを渡します。

   * `Id`オブジェクト。`Id`クラスのデフォルトのコンストラクターを呼び出し、`Resource`オブジェクトの`id`フィールドに割り当てることで作成されます。
   * `Lid`オブジェクト。`Lid`クラスのデフォルトのコンストラクターを呼び出し、`Resource`オブジェクトの`lid`フィールドに割り当てることで作成されます。
   * リソースコレクションの名前を含む文字列。この名前は、`Resource`オブジェクトの`name`フィールドに割り当てられます。 この例で使用される名前は`"testfolder"`です。
   * リソースコレクションの説明を含む文字列。この情報は、`Resource`オブジェクトの`description`フィールドに割り当てられます。 この例では、`"test folder"`と説明します。

1. フォルダーをリポジトリに書き込みます。

   `RepositoryServiceService`オブジェクトの`writeResource`メソッドを呼び出し、次のパラメーターを渡します。

   * フォルダーを作成するパス。
   * フォルダーを表す`ResourceCollection`オブジェクト。
   * 他の2つのパラメーターには`null`を渡します。

**関連トピック**

[フォルダーの作成](aem-forms-repository.md#creating-folders)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## リソースの書き込み{#writing-resources}

リポジトリ内の特定の場所にリソースを作成できます。 自然なファイルサイズは、データベースの制限やセッションタイムアウトの影響を受けます。 デフォルトの設定では、ファイルのサイズは25 MBに制限されます。 最大ファイルサイズを増減するには、データベース設定を変更する必要があります。

リソースの書き込みは、リポジトリにデータを保存することと同じです。 リソースをリポジトリに書き込むと、リポジトリエコシステム内のすべてのクライアントがリソースにアクセスできるようになります。 XMLスキーマ、XDPファイル、XSDファイルなどのリソースをリポジトリに書き込むと、その内容はMIMEタイプに基づいて解析されます。 MIMEタイプがサポートされている場合、パーサーは他のコンテンツとの暗黙の関係があるかどうかを判断します。 例えば、カスケーディングスタイルシート(CSS)に共通のCSSを参照する相対URLがある場合、共通のCSSもリポジトリに送信する必要があります。 2つのリソース間の関係は、30日間の非調整期間の保留中の関係として保存されます。 共通のCSSを30日以内にリポジトリに送信すると、関係が形成されます。

リソースを作成すると、アクセス制御リスト(ACL)が親フォルダーから継承されます。 ルートフォルダーには、初期リソースまたはフォルダーが作成されるまで、システムレベルの権限があり、その時点でリソースまたはフォルダーにデフォルトのACL権限が付与されます。

RepositoryサービスJava APIまたはWebサービスAPIを使用して、プログラムでリソースを書き込むことができます。

>[!NOTE]
>
>Repositoryサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順の概要{#summary_of_steps-1}

リソースを書き込むには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. Repositoryサービスクライアントを作成します。
1. 読み取るリソースのURIを指定します。
1. リソースを読み取ります。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを含めます。

**サービスクライアントの作成**

プログラムによってリソースを読み取る前に、接続を確立し、資格情報を指定する必要があります。 これは、サービスクライアントを作成することで実現されます。

**リソースのターゲットフォルダーのURIを指定します**

読み取るリソースのURIを含む文字列を作成します。 構文には、次のようにスラッシュが含まれます。&quot;/*path*/*folder*&quot;

**リソースの作成**

Repositoryサービスメソッドを呼び出してリソースを作成し、UUID、リソース名、説明などの識別情報をリソースに設定します。

**リソースコンテンツの指定**

Repositoryサービスメソッドを呼び出して、リソースコンテンツを作成し、そのコンテンツをリソースに格納します。

**ターゲットフォルダーにリソースを書き込む**

Repositoryサービスメソッドを呼び出して、ターゲットフォルダーのURIを指定してリソースを書き込みます。

**関連トピック**

[Java APIを使用したリソースの書き込み](aem-forms-repository.md#write-resources-using-the-java-api)

[WebサービスAPIを使用したリソースの書き込み](aem-forms-repository.md#write-resources-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[リポジトリサービスAPIのクイックスタート](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java API {#write-resources-using-the-java-api}を使用してリソースを書き込みます。

RepositoryサービスAPI(Java)を使用してリソースを書き込みます。

1. プロジェクトファイルを含める

   クライアントJARファイルをJavaプロジェクトのクラスパスに含めます。

1. サービスクライアントの作成

   コンストラクターを使用し、接続プロパティを含む`ServiceClientFactory`オブジェクトを渡して、`ResourceRepositoryClient`オブジェクトを作成します。

1. リソースのターゲットフォルダーのURIを指定します

   リソースのターゲットフォルダーのURIを指定します。 この場合、`testResource`という名前のリソースは`testFolder`という名前のフォルダーに保存されるので、フォルダーのURIは`"/testFolder"`になります。 URIは`java.lang.String`オブジェクトとして保存されます。

1. リソースの作成

   リソースを作成するには、まず`com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean`オブジェクトを作成する必要があります。

   `RepositoryInfomodelFactoryBean`オブジェクトの`newResource`メソッドを呼び出し、`com.adobe.repository.infomodel.bean.Resource`オブジェクトを作成します。 この例では、次のパラメーターが指定されます。

   * `com.adobe.repository.infomodel.Id`オブジェクト。`Id`クラスのデフォルトのコンストラクターを呼び出すことで作成されます。
   * `com.adobe.repository.infomodel.Lid`オブジェクト。`Lid`クラスのデフォルトのコンストラクターを呼び出すことで作成されます。
   * リソースのファイル名を含む`java.lang.String`。

   リソースの説明を指定するには、`Resource`オブジェクトの`setDescription`メソッドを呼び出して、説明を含む文字列を渡します。 この例では、説明は`"test resource"`です。

1. リソースコンテンツの指定

   リソースのコンテンツを作成するには、`RepositoryInfomodelFactoryBean`オブジェクトの`newResourceContent`メソッドを呼び出します。このメソッドは、`com.adobe.repository.infomodel.bean.ResourceContent`オブジェクトを返します。 `ResourceContent`オブジェクトにコンテンツを追加します。 この例では、次のタスクを実行します。

   * `ResourceContent`オブジェクトの`setDataDocument`メソッドを呼び出し、`com.adobe.idp.Document`オブジェクトを渡す
   * `ResourceContent`オブジェクトの`setSize`メソッドを呼び出し、`Document`オブジェクトのバイト数でサイズを渡す

   `Resource`オブジェクトの`setContent`メソッドを呼び出し、`ResourceContent`オブジェクトを渡すことで、コンテンツをリソースに追加します。 詳しくは、「[AEM Forms APIリファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)」を参照してください。

1. ターゲットフォルダーにリソースを書き込む

   `ResourceRepositoryClient`オブジェクトの`writeResource`メソッドを呼び出し、フォルダーのURIと`Resource`オブジェクトを渡します。

**関連トピック**

[リソースの書き込み](aem-forms-repository.md#writing-resources)

[クイックスタート（SOAPモード）:Java APIを使用したリソースの書き込み](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#write-resources-using-the-web-service-api}を使用してリソースを書き込みます。

RepositoryサービスAPI（Webサービス）を使用してリソースを書き込みます。

1. プロジェクトファイルを含める

   * base64を使用してリポジトリWSDLを使用するMicrosoft .NETクライアントアセンブリを作成します。
   * Microsoft .NETクライアントアセンブリを参照します。

1. サービスクライアントの作成

   Microsoft .NETクライアントアセンブリを使用して、デフォルトのコンストラクタを呼び出して`RepositoryServiceService`オブジェクトを作成します。 ユーザー名とパスワードを含む`System.Net.NetworkCredential`オブジェクトを使用して、 `Credentials`プロパティを設定します。

1. リソースのターゲットフォルダーのURIを指定します

   リソースのターゲットフォルダーのURIを指定します。 この場合、`testResource`という名前のリソースは`testFolder`という名前のフォルダーに保存されるので、フォルダーのURIは`"/testFolder"`になります。 Microsoft .NET Frameworkに準拠している言語（C#など）を使用する場合は、URIを`System.String`オブジェクトに格納します。

1. リソースの作成

   リソースを作成するには、`Resource`クラスのデフォルトのコンストラクターを呼び出します。 この例では、次の情報が`Resource`オブジェクトに格納されます。

   * `com.adobe.repository.infomodel.Id`オブジェクト。`Id`クラスのデフォルトのコンストラクターを呼び出し、`Resource`オブジェクトの`id`フィールドに割り当てることで作成されます。
   * `com.adobe.repository.infomodel.Lid`オブジェクト。`Lid`クラスのデフォルトのコンストラクターを呼び出し、`Resource`オブジェクトの`lid`フィールドに割り当てることで作成されます。
   * リソースのファイル名を含む文字列。このファイル名は、`Resource`オブジェクトの`name`フィールドに割り当てられます。 この例で使用される名前は`"testResource"`です。
   * リソースの説明を含む文字列。この文字列は、`Resource`オブジェクトの`description`フィールドに割り当てられます。 この例では、`"test resource"`と説明します。

1. リソースコンテンツの指定

   リソースのコンテンツを作成するには、`ResourceContent`クラスのデフォルトのコンストラクターを呼び出します。 次に、`ResourceContent`オブジェクトにコンテンツを追加します。 この例では、次のタスクを実行します。

   * ドキュメントを含む`BLOB`オブジェクトを`ResourceContent`オブジェクトの`dataDocument`フィールドに割り当てます。
   * `BLOB`オブジェクトのサイズを`ResourceContent`オブジェクトの`size`フィールドに割り当てます。

   `ResourceContent`オブジェクトを`Resource`オブジェクトの`content`フィールドに割り当てて、コンテンツをリソースに追加します。

1. ターゲットフォルダーにリソースを書き込む

   `RepositoryServiceService`オブジェクトの`writeResource`メソッドを呼び出し、フォルダーのURIと`Resource`オブジェクトを渡します。 他の2つのパラメーターには`null`を渡します。

**関連トピック**

[リソースの書き込み](aem-forms-repository.md#writing-resources)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## リソースのリスト{#listing-resources}

リソースを一覧表示すると、リソースを見つけることができます。 リポジトリに対してクエリが実行され、特定のリソースコレクションに関連するすべてのリソースが検索されます。

リソースを整理したら、オペレーティングシステムでおこなうのと同じように、構造の特定のブランチを表示して、作成した構造を調べることができます。

リストリソースは、次の関係によって機能します。リソースは、フォルダーのメンバーです。 メンバーシップは、「メンバー」タイプの関係で表されます。 特定のフォルダー内のリソースをリストすると、「メンバー」の関係によって特定のフォルダーに関連するリソースを照会します。 関係は方向性を持ちます。関係のメンバーには、ターゲットのメンバーであるソースがあります。 ソースはリソースです。ターゲットは親フォルダーです。

>[!NOTE]
>
>Repositoryサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順の概要{#summary_of_steps-2}

リソースを一覧表示するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. サービスクライアントを作成します。
1. フォルダーパスを指定します。
1. リソースのリストを取得します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを含めます。

**サービスクライアントの作成**

プログラムによってリソース収集を作成する前に、接続を確立し、資格情報を指定する必要があります。 これは、サービスクライアントを作成することで実現されます。

**フォルダーパスの指定**

リソースを含むフォルダーのパスを含む文字列を作成します。 構文には、次のようにスラッシュが含まれます。&quot;/*path*/*folder*&quot;

**リソースのリストの取得**

Repositoryサービスメソッドを呼び出して、ターゲットフォルダーのパスを指定してリソースのリストを取得します。

**関連トピック**

[Java APIを使用したリソースのリスト](aem-forms-repository.md#list-resources-using-the-java-api)

[WebサービスAPIを使用したリソースのリスト](aem-forms-repository.md#list-resources-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[リポジトリサービスAPIのクイックスタート](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java API {#list-resources-using-the-java-api}を使用したリソースのリスト

RepositoryサービスAPI(Java)を使用してリソースをリストします。

1. プロジェクトファイルを含める

   クライアントJARファイルをJavaプロジェクトのクラスパスに含めます。

1. サービスクライアントの作成

   コンストラクターを使用し、接続プロパティを含む`ServiceClientFactory`オブジェクトを渡して、`ResourceRepositoryClient`オブジェクトを作成します。

1. フォルダーパスの指定

   問い合わせるリソースコレクションのURIを指定します。 この場合、URIは`"/testFolder"`です。 URIは`java.lang.String`オブジェクトとして保存されます。

1. リソースのリストの取得

   `ResourceRepositoryClient`オブジェクトの`listMembers`メソッドを呼び出して、フォルダーのURIを渡します。

   このメソッドは、`Relation.TYPE_MEMBER_OF`型の`com.adobe.repository.infomodel.bean.Relation`のソースであり、リソース収集URIをターゲットとする`java.util.List`オブジェクトの`com.adobe.repository.infomodel.bean.Resource`を返します。 この`List`を繰り返し処理して、各リソースを取得できます。 この例では、各リソースの名前と説明が表示されます。

**関連トピック**

[リソースのリスト](aem-forms-repository.md#listing-resources)を参照してください。

[クイックスタート（SOAPモード）:Java APIを使用したリソースの一覧](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-listing-resources-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#list-resources-using-the-web-service-api}を使用してリソースをリストします

RepositoryサービスAPI（Webサービス）を使用してリソースをリストします。

1. プロジェクトファイルを含める

   * リポジトリWSDLを使用するMicrosoft .NETクライアントアセンブリを作成します。
   * Microsoft .NETクライアントアセンブリを参照します。

1. サービスクライアントの作成

   Microsoft .NETクライアントアセンブリを使用して、デフォルトのコンストラクタを呼び出して`RepositoryServiceService`オブジェクトを作成します。 ユーザー名とパスワードを含む`System.Net.NetworkCredential`オブジェクトを使用して、 `Credentials`プロパティを設定します。

1. フォルダーパスの指定

   問い合わせるフォルダーのURIを含む文字列を指定します。 この場合、URIは`"/testFolder"`です。 Microsoft .NET Frameworkに準拠している言語（C#など）を使用する場合は、URIを`System.String`オブジェクトに格納します。

1. リソースのリストの取得

   `RepositoryServiceService`オブジェクトの`listMembers`メソッドを呼び出し、最初のパラメーターとしてフォルダーのURIを渡します。 他の2つのパラメーターには`null`を渡します。

   このメソッドは、`Resource`オブジェクトにキャストできるオブジェクトの配列を返します。 オブジェクト配列を繰り返し処理して、関連する各リソースを取得できます。 この例では、各リソースの名前と説明が表示されます。

**関連トピック**

[リソースのリスト](aem-forms-repository.md#listing-resources)を参照してください。

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## リソースの読み取り{#reading-resources}

リポジトリ内の特定の場所からリソースを取得して、そのコンテンツとメタデータを読み取ることができます。 ワークフローは、初期化フォームによってフロントエンドされます。 プロセスには、フォームを読み取るために必要なすべての権限があります。 システムはデータ・フォームを取得し、リポジトリからコンテンツを読み取ります。 リポジトリは、コンテンツとメタデータへのアクセス（リソースが存在することを知る機能）を許可します。

リポジトリには次の4つの権限タイプがあります。

* **traverse**:では、リソースのリストを表示できます。つまり、リソースのメタデータを読み取るが、リソースの内容を読み取らない
* **読み取り**:リソースコンテンツを読み取ることができます。
* **書き込み**:リソースコンテンツの書き込みが可能
* **アクセス制御リスト(ACL)の管理**:を使用すると、リソースのACLを操作できます。

ユーザーは、プロセスを実行する権限を持つ場合にのみプロセスを実行できます。 IDEユーザーは、リポジトリと同期するには、トラバースおよび読み取り権限が必要です。 実行時はシステムコンテキスト内で発生するので、ACLはデザイン時にのみ適用されます。

RepositoryサービスJava APIまたはWebサービスAPIを使用して、プログラムでリソースを読み取ることができます。

>[!NOTE]
>
>Repositoryサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順の概要{#summary_of_steps-3}

リソースを読み取るには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. Repositoryサービスクライアントを作成します。
1. 読み取るリソースのURIを指定します。
1. リソースを読み取ります。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを含めます。

**サービスクライアントの作成**

プログラムによってリソースを読み取る前に、接続を確立し、資格情報を指定する必要があります。 これは、サービスクライアントを作成することで実現されます。

**読み取るリソースのURIを指定します**

読み取るリソースのURIを含む文字列を作成します。 構文には、次のようにスラッシュが含まれます。&quot;/*path*/*resource*&quot;

**リソースの読み取り**

Repositoryサービスメソッドを呼び出して、URIを指定してリソースを読み取ります。

**関連トピック**

[Java APIを使用したリソースの読み取り](aem-forms-repository.md#read-resources-using-the-java-api)

[WebサービスAPIを使用したリソースの読み取り](aem-forms-repository.md#reading-resources-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[リポジトリサービスAPIのクイックスタート](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java API {#read-resources-using-the-java-api}を使用してリソースを読み取ります

RepositoryサービスAPI(Java)を使用してリソースを読み取ります。

1. プロジェクトファイルを含める

   クライアントJARファイルをJavaプロジェクトのクラスパスに含めます。

1. サービスクライアントの作成

   コンストラクターを使用し、接続プロパティを含む`ServiceClientFactory`オブジェクトを渡して、`ResourceRepositoryClient`オブジェクトを作成します。

1. 読み取るリソースのURIを指定します

   取得するリソースのURIを表すstring値を指定します。 例えば、リソースの名前が&#x200B;*testResource*（*testFolder*&#x200B;にある）と仮定して、`/testFolder/testResource`と指定します。

1. リソースの読み取り

   `ResourceRepositoryClient`オブジェクトの`readResource`メソッドを呼び出し、リソースのURIをパラメーターとして渡します。 このメソッドは、リソースを表す`Resource`インスタンスを返します。

**関連トピック**

[リソースの読み取り](aem-forms-repository.md#reading-resources)

[クイックスタート（SOAPモード）:Java APIを使用したリソースの読み取り](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-reading-a-resource-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#reading-resources-using-the-web-service-api}を使用してリソースを読み取る

RepositoryサービスAPI（Webサービス）を使用してリソースを読み取ります。

1. プロジェクトファイルを含める

   * リポジトリWSDLを使用するMicrosoft .NETクライアントアセンブリを作成します。 （[Base64エンコード](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)を使用する.NETクライアントアセンブリの作成を参照）。
   * Microsoft .NETクライアントアセンブリを参照します。 （[Base64エンコード](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)を使用する.NETクライアントアセンブリの作成を参照）。

1. サービスクライアントの作成

   Microsoft .NETクライアントアセンブリを使用して、デフォルトのコンストラクタを呼び出して`RepositoryServiceService`オブジェクトを作成します。 ユーザー名とパスワードを含む`System.Net.NetworkCredential`オブジェクトを使用して、 `Credentials`プロパティを設定します。

1. 読み取るリソースのURIを指定します

   取得するリソースのURIを含む文字列を指定します。 この場合、`testResource`という名前のリソースは`testFolder`という名前のフォルダーにあるので、URIは`"/testFolder/testResource"`になります。 Microsoft .NET Frameworkに準拠している言語（C#など）を使用する場合は、URIを`System.String`オブジェクトに格納します。

1. リソースの読み取り

   `RepositoryServiceService`オブジェクトの`readResource`メソッドを呼び出し、リソースのURIを最初のパラメーターとして渡します。 他の2つのパラメーターには`null`を渡します。

**関連トピック**

[リソースの読み取り](aem-forms-repository.md#reading-resources)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## リソース{#updating-resources}を更新中

リポジトリ内のリソースのコンテンツを取得して更新できます。 リソースを更新する場合、それらのリソースへのアクセス制御は、バージョン間で変更されません。 更新を実行する場合、メジャーバージョンを増分するオプションがあります。 メジャーバージョンを増分しない場合、マイナーバージョンが自動的に更新されます。

リソースを更新すると、指定したリソース属性に基づいて新しいバージョンが作成されます。 リソースを更新する際には、次の2つの重要なパラメータを指定します。ターゲットURIと、更新されたすべてのメタデータを含むリソースインスタンス。 特定の属性（名前など）を変更しない場合、渡すインスタンスでも属性が必要です。 コンテンツの解析時に作成される関係は、特定のバージョンに追加され、特に指定のない限り転送されません。

例えば、更新したXDPファイルに他のリソースへの参照が含まれている場合は、その他の参照も記録されます。 form.xdpバージョン1.0に2つの外部参照があるとします。ロゴとスタイルシートを追加し、その後form.xdpを更新して、3つの参照が含まれるようにします。ロゴ、スタイルシートおよびスキーマファイル。 更新中、リポジトリは3番目の関係（スキーマファイル）を保留中の関係テーブルに追加します。 スキーマファイルがリポジトリに存在すると、関係が自動的に形成されます。 ただし、form.xdpバージョン2.0でロゴが使用されなくなった場合、form.xdpバージョン2.0はロゴとの関係を持ちません。

すべての更新操作はアトミックおよびトランザクションです。 例えば、2人のユーザーが同じリソースを読み、両方のユーザーがバージョン1.0をバージョン2.0に更新した場合、いずれかが成功し、一方が失敗し、リポジトリの整合性が維持され、両方が成功または失敗を確認するメッセージを受け取ります。 トランザクションがコミットされない場合、データベース障害が発生した場合にロールバックされ、アプリケーション・サーバに応じてタイムアウトまたはロールバックされます。

RepositoryサービスJava APIまたはWebサービスAPIを使用して、プログラムでリソースを更新できます。

>[!NOTE]
>
>Repositoryサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順の概要{#summary_of_steps-4}

リソースを更新するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. Repositoryサービスクライアントを作成します。
1. 更新するリソースを取得します。
1. リソースを更新します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを含めます。

**サービスクライアントの作成**

プログラムによってリソースを読み取る前に、接続を確立し、資格情報を指定する必要があります。 これは、サービスクライアントを作成することで実現されます。

**更新するリソースの取得**

リソースを読み取ります。 詳しくは、[リソース](aem-forms-repository.md#reading-resources)の読み取りを参照してください。

**リソースの更新**

リソースに新しい情報を設定し、Repositoryサービスメソッドを呼び出して、リソースを更新し、URI、更新されたリソース、およびバージョン情報の更新方法を指定します。

**関連トピック**

[Java APIを使用したリソースの更新](aem-forms-repository.md#update-resources-using-the-java-api)

[WebサービスAPIを使用したリソースの更新](aem-forms-repository.md#update-resources-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[リポジトリサービスAPIのクイックスタート](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java API {#update-resources-using-the-java-api}を使用してリソースを更新する

RepositoryサービスAPI(Java)を使用してリソースを更新します。

1. プロジェクトファイルを含める

   クライアントJARファイルをJavaプロジェクトのクラスパスに含めます。

1. サービスクライアントの作成

   コンストラクターを使用し、接続プロパティを含む`ServiceClientFactory`オブジェクトを渡して、`ResourceRepositoryClient`オブジェクトを作成します。

1. 更新するリソースの取得

   リソースを取得して読み取るリソースのURIを指定します。 この例では、リソースのURIは`"/testFolder/testResource"`です。

1. リソースの更新

   `Resource`オブジェクトの情報を更新します。 この例では、説明を更新するには、`Resource`オブジェクトの`setDescription`メソッドを呼び出し、新しい説明文字列をパラメーターとして渡します。

   次に、`ServiceClientFactory`オブジェクトの`updateResource`メソッドを呼び出し、次のパラメーターを渡します。

   * リソースのURIを含む`java.lang.String`オブジェクト。
   * 更新されたリソース情報を含む`Resource`オブジェクト。
   * メジャーバージョンとマイナーバージョンのどちらを更新するかを示す`boolean`値。 この例では、メジャーバージョンの値を増分することを示す値`true`が渡されます。

**関連トピック**

[リソースの更新](aem-forms-repository.md#updating-resources)

[クイックスタート（SOAPモード）:Java APIを使用したリソースの更新](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-updating-a-resource-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#update-resources-using-the-web-service-api}を使用してリソースを更新する

Repository API（Webサービス）を使用してリソースを更新します。

1. プロジェクトファイルを含める

   * リポジトリWSDLを使用するMicrosoft .NETクライアントアセンブリを作成します。
   * Microsoft .NETクライアントアセンブリを参照します。

1. サービスクライアントの作成

   Microsoft .NETクライアントアセンブリを使用して、デフォルトのコンストラクタを呼び出して`RepositoryServiceService`オブジェクトを作成します。 ユーザー名とパスワードを含む`System.Net.NetworkCredential`オブジェクトを使用して、 `Credentials`プロパティを設定します。

1. 更新するリソースの取得

   取得するリソースのURIを指定し、リソースを読み取ります。 この例では、リソースのURIは`"/testFolder/testResource"`です。 詳しくは、[リソース](aem-forms-repository.md#reading-resources)の読み取りを参照してください。

1. リソースの更新

   `Resource`オブジェクトの情報を更新します。 この例では、説明を更新するために、`Resource`オブジェクトの`description`フィールドに新しい値を割り当てます。

1. `RepositoryServiceService`オブジェクトの`updateResource`メソッドを呼び出し、次のパラメーターを渡します。

   * リソースのURIを含む`System.String`オブジェクト。
   * 更新されたリソース情報を含む`Resource`オブジェクト。
   * メジャーバージョンとマイナーバージョンのどちらを更新するかを示す`boolean`値。 この例では、メジャーバージョンの値を増分することを示す値`true`が渡されます。
   * 残りの2つのパラメーターに`null`を渡します。

**関連トピック**

[リソースの更新](aem-forms-repository.md#updating-resources)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## リソースの検索{#searching-for-resources}

リポジトリ内のリソース（履歴、関連リソース、プロパティなど）の検索に使用するクエリを作成できます。

関連リソースを取得して、フォームとそのフラグメントの間の依存関係を判断できます。 例えば、フォームがある場合、フォームで使用するフラグメントや外部リソースを決定できます。 画像がある場合は、その画像がどのフォームで使用されているかも確認できます。 また、プロパティに基づくフィルタリングを使用して、関連リソースを検索することもできます。 例えば、指定した名前の画像を使用するすべてのフォームを検索したり、指定した名前のフォームで使用されている画像を検索したりできます。 また、リソースプロパティを使用して検索することもできます。 例えば、クエリを実行して、名前が「%」や「_」のワイルドカードを含む特定の文字列で始まるすべてのフォームやリソースを検索できます。 プロパティに基づく検索は、関係に基づくものではありません。このような検索は、特定のリソースに関する特定の知識があることを前提としています。

**クエリステートメント**

*クエリ*&#x200B;には、条件を論理的に結合した1つ以上のステートメントが含まれます。 *文*&#x200B;は、左オペランド、演算子、右オペランドで構成されます。 さらに、検索結果に使用する並べ替え順を指定できます。 *並べ替え順*&#x200B;は、SQLの`ORDER BY`句に相当する情報を含み、検索の基となる属性を含む要素と、昇順または降順のどちらを使用するかを示す値で構成されます。

RepositoryサービスJava APIを使用して、プログラムでリソースを検索できます。 現時点では、WebサービスAPIを使用してリソースを検索することはできません。

**並べ替え動作**

`ResourceRepositoryClient`オブジェクトの`searchProperties`メソッドを呼び出し、並べ替え順を指定する場合、並べ替え順は考慮されません。 例えば、属性名が`name`、`secondName`、`asecondName`の3つのカスタムプロパティを持つリソースを作成するとします。 次に、属性名に並べ替え順の要素を作成し、`ascending`値を`true`に設定します。

次に、`ResourceRepositoryClient`オブジェクトの`searchProperties`メソッドを呼び出し、並べ替え順を渡します。 検索を実行すると、適切なリソースと3つのプロパティが返されます。 ただし、プロパティは属性名で並べ替えられません。 追加された順序で返されます。`name`、`secondName`、および`asecondName`。

>[!NOTE]
>
>Repositoryサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順の概要{#summary_of_steps-5}

リソースを検索するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. Repositoryサービスクライアントを作成します。
1. 検索の対象フォルダーを指定します。
1. 検索で使用する属性を指定します。
1. 検索で使用するクエリを作成します。
1. 検索結果の並べ替え順を作成します。
1. リソースを検索します。
1. 検索結果からリソースを取得します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを含めます。

**サービスクライアントの作成**

プログラムによってリソースを読み取る前に、接続を確立し、資格情報を指定する必要があります。 これは、サービスクライアントを作成することで実現されます。

**検索の対象フォルダーの指定**

検索の実行元となるベースパスを含む文字列を作成します。 構文には、次のようにスラッシュが含まれます。&quot;/*path*/*folder*&quot;

**検索で使用する属性の指定**

リソースに含まれる属性に基づいて検索を行うことができます。 検索の対象となる属性の値を指定します。

**検索で使用するクエリの作成**

文と条件を使用してクエリを作成します。 各文は、検索のベースとなる属性、使用する条件、検索で使用する属性値を指定します。

**検索結果の並べ替え順の作成**

並べ替え順は、要素で構成され、各要素には、検索で使用される属性の1つと、昇順または降順のどちらを使用するかを示す値が含まれます。

**リソースの検索**

フォルダー、クエリ、並べ替え順を使用して、リソースを検索します。 さらに、検索の深さと、返される結果の数の上限を指定します。

**検索結果からのリソースの取得**

返されたリソースのリストを繰り返し処理し、さらに処理するために情報を抽出します。

**関連トピック**

[Java APIを使用したリソースの検索](aem-forms-repository.md#search-for-resources-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[リポジトリサービスAPIのクイックスタート](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java API {#search-for-resources-using-the-java-api}を使用したリソースの検索

RepositoryサービスAPI(Java)を使用してリソースを検索します。

1. プロジェクトファイルを含める

   クライアントJARファイルをJavaプロジェクトのクラスパスに含めます。

1. サービスクライアントの作成

   コンストラクターを使用し、接続プロパティを含む`ServiceClientFactory`オブジェクトを渡して、`ResourceRepositoryClient`オブジェクトを作成します。

1. 検索の対象フォルダーの指定

   検索を実行するベースパスのURIを指定します。 この例では、リソースのURIは`/testFolder`です。

1. 検索で使用する属性の指定

   検索の対象となる属性の値を指定します。 属性は`com.adobe.repository.infomodel.bean.Resource`オブジェクト内に存在します。 この例では、検索はname属性に対して実行されます。したがって、`Resource`オブジェクトの名前を含む`java.lang.String`が使用されます。この場合は`testResource`です。

1. 検索で使用するクエリの作成

   クエリを作成するには、`Query`クラスのデフォルトのコンストラクターを呼び出し、クエリにステートメントを追加して、`com.adobe.repository.query.Query`オブジェクトを作成します。

   文を作成するには、`com.adobe.repository.query.Query.Statement`クラスのコンストラクターを呼び出し、次のパラメーターを渡します。

   * リソース属性定数を含む左オペランド。 この例では、リソースの名前が検索の基礎として使用されるので、静的な値`Resource.ATTRIBUTE_NAME`が使用されます。
   * 属性の検索に使用される条件を含む演算子。 演算子は、`Query.Statement`クラスの静的定数の1つである必要があります。 この例では、静的な値`Query.Statement.OPERATOR_BEGINS_WITH`が使用されます。
   * 検索を実行する属性値を含む右オペランド。 この例では、name属性（値`"testResource"`を含む`String`）が使用されます。

   `Query.Statement`オブジェクトの`setNamespace`メソッドを呼び出し、`com.adobe.repository.infomodel.bean.ResourceProperty`クラスに含まれる静的値の1つを渡すことで、左のオペランドの名前空間を指定します。 この例では、`ResourceProperty.RESERVED_NAMESPACE_REPOSITORY`が使用されます。

   `Query`オブジェクトの`addStatement`メソッドを呼び出し、`Query.Statement`オブジェクトを渡すことで、各文をクエリに追加します。

1. 検索結果の並べ替え順の作成

   検索結果で使用される並べ替え順を指定するには、`SortOrder`クラスのデフォルトのコンストラクターを呼び出し、並べ替え順に要素を追加して、`com.adobe.repository.query.sort.SortOrder`オブジェクトを作成します。

   並べ替え順の要素を作成するには、`com.adobe.repository.query.sort.SortOrder.Element`クラスのコンストラクタの1つを呼び出します。 この例では、リソースの名前が検索の基礎として使用されるので、静的な値`Resource.ATTRIBUTE_NAME`が最初のパラメーターとして使用され、昇順の値（`boolean`値`true`）が2番目のパラメーターとして指定されます。

   `SortOrder`オブジェクトの`addSortElement`メソッドを呼び出し、`SortOrder.Element`オブジェクトを渡すことで、各要素を並べ替え順に追加します。

1. リソースの検索

   属性プロパティに基づいて`resources`を検索するには、`ResourceRepositoryClient`オブジェクトの`searchProperties`メソッドを呼び出して、次のパラメーターを渡します。

   * 検索を実行するベースパスを含む`String`。 この場合は`"/testFolder"`が使用されます。
   * 検索で使用されるクエリ。
   * 検索の深さ。 この場合、`com.adobe.repository.infomodel.bean.ResourceCollection.DEPTH_INFINITE`は、ベースパスとそのすべてのフォルダーが使用されることを示します。
   * ページ化されていない結果セットを選択する最初の行を示す`int`値。 この例では、`0`が指定されています。
   * 返される結果の最大数を示す`int`値。 この例では、`10`が指定されています。
   * 検索で使用される並べ替え順。

   このメソッドは、指定した並べ替え順で`Resource`オブジェクトの`java.util.List`を返します。

1. 検索結果からのリソースの取得

   検索結果に含まれるリソースを取得するには、`List`を繰り返し処理し、各オブジェクトを`Resource`にキャストして情報を抽出します。 この例では、各リソースの名前が表示されます。

**関連トピック**

[リソースの検索](aem-forms-repository.md#searching-for-resources)

[クイックスタート（SOAPモード）:Java APIを使用したリソースの検索](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## リソースの関係の作成{#creating-resource-relationships}

リポジトリ内のリソース間の関係を指定できます。 関係には次の3種類があります。

* **依存関係**:リソースが他のリソースに依存する関係。つまり、リポジトリ内のすべての関連リソースが必要です。
* **メンバーシップ（ファイルシステム）**:リソースが特定のフォルダー内に存在する関係。
* **カスタム**:リソース間で指定する関係。例えば、あるリソースが非推奨になり、別のリソースがリポジトリに導入された場合は、独自の置換関係を指定できます。

独自のカスタムの関係を作成できます。 例えば、HTMLファイルをリポジトリに格納し、画像を使用する場合、カスタム関係を指定してHTMLファイルと画像を関連付けることができます（通常、XMLファイルのみがリポジトリ定義の依存関係を使用して画像に関連付けられます）。 カスタム関係のもう1つの例は、ツリー構造ではなく循環グラフ構造を使用してリポジトリの別のビューを作成する場合です。 ビューアと共に円グラフを定義して、これらの関係をトラバースできます。 最後に、2つのリソースが完全に異なる場合でも、1つのリソースが別のリソースを置き換えることを示すことができます。 その場合、予約範囲外の関係タイプを定義して、これら2つのリソース間の関係を作成できます。 アプリケーションは、関係を検出して処理できる唯一のクライアントであり、その関係を検索するために使用できます。

RepositoryサービスJava APIまたはWebサービスAPIを使用して、プログラムでリソース間の関係を指定できます。

>[!NOTE]
>
>Repositoryサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順の概要{#summary_of_steps-6}

2つのリソース間の関係を指定するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. Repositoryサービスクライアントを作成します。
1. 関連付けるリソースのURIを指定します。
1. 関係を作成します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを含めます。

**サービスクライアントの作成**

プログラムによってリソースを読み取る前に、接続を確立し、資格情報を指定する必要があります。 これは、サービスクライアントを作成することで実現されます。

**関連付けるリソースのURIの指定**

関連付けるリソースのURIを含む文字列を作成します。 構文には、次のようにスラッシュが含まれます。&quot;/*path*/*resource*&quot;

**関係の作成**

Repositoryサービスメソッドを呼び出して、関係のタイプを作成および指定します。

**関連トピック**

[Java APIを使用した関係リソースの作成](aem-forms-repository.md#create-relationship-resources-using-the-java-api)

[WebサービスAPIを使用した関係リソースの作成](aem-forms-repository.md#create-relationship-resources-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[リポジトリサービスAPIのクイックスタート](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java API {#create-relationship-resources-using-the-java-api}を使用して関係リソースを作成します

RepositoryサービスJava APIを使用して関係リソースを作成し、次のタスクを実行します。

1. プロジェクトファイルを含める

   クライアントJARファイルをJavaプロジェクトのクラスパスに含めます。

1. サービスクライアントの作成

   コンストラクターを使用し、接続プロパティを含む`ServiceClientFactory`オブジェクトを渡して、`ResourceRepositoryClient`オブジェクトを作成します。

1. 関連付けるリソースのURIの指定

   関連付けるリソースのURIを指定します。 この場合、リソースの名前は`testResource1`および`testResource2`で、`testFolder`というフォルダーに配置されているので、URIは`"/testFolder/testResource1"`および`"/testFolder/testResource2"`になります。 URIは`java.lang.String`オブジェクトとして保存されます。 この例では、リソースは最初にリポジトリに書き込まれ、URIが取得されます。 リソースの書き込みについて詳しくは、[リソースの書き込み](aem-forms-repository.md#writing-resources)を参照してください。

1. 関係の作成

   `ResourceRepositoryClient`オブジェクトの`createRelationship`メソッドを呼び出し、次のパラメーターを渡します。

   * ソースリソースのURI。
   * ターゲットリソースのURI。
   * `com.adobe.repository.infomodel.bean.Relation`クラスの静的定数の1つである関係のタイプ。 この例では、`Relation.TYPE_DEPENDANT_OF`という値を指定して依存関係を確立します。
   * ターゲットリソースを新しいヘッドリソースの`com.adobe.repository.infomodel.Id`ベースの識別子に自動的に更新するかどうかを示す`boolean`値。 この例では、依存関係が原因で、値`true`が指定されています。

   `ResourceRepositoryClient`オブジェクトの`getRelated`メソッドを呼び出し、次のパラメーターを渡すことで、特定のリソースに関連するリソースのリストを取得することもできます。

   * 関連リソースを取得するリソースのURI。 この例では、ソースリソース(`"/testFolder/testResource1"`)が指定されています。
   * 指定したリソースが関係のソースリソースであるかどうかを示す`boolean`値。 この例では、値`true`が指定されています。これは、この場合です。
   * `Relation`クラスの静的定数の1つである関係タイプ。 この例では、以前に使用したのと同じ値を使用して依存関係を指定します。`Relation.TYPE_DEPENDANT_OF`.

   `getRelated`メソッドは、`Resource`オブジェクトの`java.util.List`を返します。このメソッドを使用して、関連する各リソースを繰り返し取得し、`List`に含まれるオブジェクトを`Resource`にキャストします。 この例では、返されるリソースのリストに`testResource2`が含まれている必要があります。

**関連トピック**

[リソースの関係の作成](aem-forms-repository.md#creating-resource-relationships)

[クイックスタート（SOAPモード）:Java APIを使用したリソース間の関係の作成](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-relationships-between-resources-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#create-relationship-resources-using-the-web-service-api}を使用して関係リソースを作成します

Repository API（Webサービス）を使用して関係リソースを作成します。

1. プロジェクトファイルを含める

   * リポジトリWSDLを使用するMicrosoft .NETクライアントアセンブリを作成します。
   * Microsoft .NETクライアントアセンブリを参照します。

1. サービスクライアントの作成

   Microsoft .NETクライアントアセンブリを使用して、デフォルトのコンストラクタを呼び出して`RepositoryServiceService`オブジェクトを作成します。 ユーザー名とパスワードを含む`System.Net.NetworkCredential`オブジェクトを使用して、 `Credentials`プロパティを設定します。

1. 関連付けるリソースのURIの指定

   関連付けるリソースのURIを指定します。 この場合、リソースの名前は`testResource1`および`testResource2`で、`testFolder`というフォルダーに配置されているので、URIは`"/testFolder/testResource1"`および`"/testFolder/testResource2"`になります。 Microsoft .NET Frameworkに準拠した言語（C#など）を使用する場合、URIは`System.String`オブジェクトとして保存されます。 この例では、リソースは最初にリポジトリに書き込まれ、URIが取得されます。 リソースの書き込みについて詳しくは、[リソースの書き込み](aem-forms-repository.md#writing-resources)を参照してください。

1. 関係の作成

   `RepositoryServiceService`オブジェクトの`createRelationship`メソッドを呼び出し、次のパラメーターを渡します。

   * ソースリソースのURI。
   * ターゲットリソースのURI。
   * 関係のタイプ。 この例では、`3`という値を指定して依存関係を確立します。
   * 関係タイプが指定されたかどうかを示す`boolean`値。 この例では、値`true`が指定されています。
   * ターゲットリソースを新しいヘッドリソースの`Id`ベースの識別子に自動的に更新するかどうかを示す`boolean`値。 この例では、依存関係が原因で、値`true`が指定されています。
   * ターゲットヘッドが指定されたかどうかを示す`boolean`値。 この例では、値`true`が指定されています。
   * 最後のパラメーターに`null`を渡します。

   `RepositoryServiceService`オブジェクトの`getRelated`メソッドを呼び出し、次のパラメーターを渡すことで、特定のリソースに関連するリソースのリストを取得することもできます。

   * 関連リソースを取得するリソースのURI。 この例では、ソースリソース(`"/testFolder/testResource1"`)が指定されています。
   * 指定したリソースが関係のソースリソースであるかどうかを示す`boolean`値。 この例では、値`true`が指定されています。これは、この場合です。
   * ソースリソースが指定されたかどうかを示す`boolean`値。 この例では、値`true`が指定されています。
   * 関係タイプを含む整数の配列。 この例では、以前に使用したのと同じ値を配列に使用して依存関係を指定します。`3`.
   * 残りの2つのパラメーターに`null`を渡します。

   `getRelated`メソッドは、`Resource`オブジェクトにキャストできるオブジェクトの配列を返します。この配列を使用して、関連する各リソースを繰り返し取得できます。 この例では、返されるリソースのリストに`testResource2`が含まれている必要があります。

**関連トピック**

[リソースの関係の作成](aem-forms-repository.md#creating-resource-relationships)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## リソースのロック{#locking-resources}

特定のユーザーが排他的に使用するリソースまたはリソースのセットをロックしたり、複数のユーザー間で共有を使用したりできます。 共有ロックは、リソースで何かが起こることを示しますが、他のユーザーがそのリソースでアクションを実行するのを妨げることはありません。 共有ロックは、シグナリングメカニズムと見なす必要があります。 排他的ロックとは、リソースをロックしたユーザーがリソースを変更することを意味し、ロックは、ユーザーがリソースにアクセスする必要がなくなり、ロックを解除するまで、他のユーザーがリソースを変更できないようにします。 リポジトリ管理者がリソースのロックを解除すると、そのリソースに対する排他的ロックと共有ロックがすべて自動的に削除されます。 このタイプのアクションは、ユーザーが使用できなくなり、リソースのロックが解除されていない場合に使用します。

リソースがロックされている場合、次の図に示すように、Workbenchの「リソース」タブを表示すると、ロックアイコンが表示されます。

![lr_lr_lockrepository](assets/lr_lr_lockrepository.png)

RepositoryサービスJava APIまたはWebサービスAPIを使用して、リソースへのアクセスをプログラムで制御できます。

>[!NOTE]
>
>Repositoryサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順の概要{#summary_of_steps-7}

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

プログラムによってリソースを読み取る前に、接続を確立し、資格情報を指定する必要があります。 これは、サービスクライアントを作成することで実現されます。

**ロックするリソースのURIの指定**

ロックするリソースのURIを含む文字列を作成します。 構文には、次のようにスラッシュが含まれます。&quot;/*path*/*resource*&quot;

**リソースのロック**

Repositoryサービスメソッドを呼び出して、リソースをロックし、URI、ロックのタイプおよびロックの深さを指定します。

**リソースのロックの取得**

Repositoryサービスメソッドを呼び出して、URIを指定してリソースのロックを取得します。

**リソースのロック解除**

Repositoryサービスメソッドを呼び出して、URIを指定して、リソースのロックを解除します。

**関連トピック**

[Java APIを使用したリソースのロック](aem-forms-repository.md#lock-resources-using-the-java-api)

[WebサービスAPIを使用したリソースのロック](aem-forms-repository.md#lock-resources-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[リポジトリサービスAPIのクイックスタート](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java API {#lock-resources-using-the-java-api}を使用してリソースをロックする

RepositoryサービスAPI(Java)を使用してリソースをロックするには：

1. プロジェクトファイルを含める

   クライアントJARファイルをJavaプロジェクトのクラスパスに含めます。

1. サービスクライアントの作成

   コンストラクターを使用し、接続プロパティを含む`ServiceClientFactory`オブジェクトを渡して、`ResourceRepositoryClient`オブジェクトを作成します。

1. ロックするリソースのURIの指定

   ロックするリソースのURIを指定します。 この場合、`testResource`という名前のリソースは`testFolder`という名前のフォルダーにあるので、URIは`"/testFolder/testResource"`になります。 URIは`java.lang.String`オブジェクトとして保存されます。

1. リソースのロック

   `ResourceRepositoryClient`オブジェクトの`lockResource`メソッドを呼び出し、次のパラメーターを渡します。

   * リソースのURI。
   * ロックの範囲。 この例では、リソースは排他的に使用するためにロックされるので、ロック範囲は`com.adobe.repository.infomodel.bean.Lock.SCOPE_EXCLUSIVE`と指定します。
   * ロックの深さ。 この例では、ロックは特定のリソースにのみ適用され、メンバーや子には適用されないので、ロックの深さは`Lock.DEPTH_ZERO`と指定します。

   >[!NOTE]
   >
   >4つのパラメーターを必要とするオーバーロードされたバージョンの`lockResource`メソッドでは、例外がスローされます。 このチュートリアルに示すように、3つのパラメーターを必要とする`lockResource`メソッドを使用してください。

1. リソースのロックの取得

   `ResourceRepositoryClient`オブジェクトの`getLocks`メソッドを呼び出し、リソースのURIをパラメーターとして渡します。 メソッドは、繰り返し処理できるList of Lockオブジェクトを返します。 この例では、各Lockオブジェクトの`getOwnerUserId`、`getDepth`、`getType`メソッドを呼び出して、各オブジェクトに対してロックの所有者、深さ、範囲を印刷します。

1. リソースのロック解除

   `ResourceRepositoryClient`オブジェクトの`unlockResource`メソッドを呼び出し、リソースのURIをパラメーターとして渡します。 詳しくは、「[AEM Forms APIリファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)」を参照してください。

**関連トピック**

[リソースのロック](aem-forms-repository.md#locking-resources)

[クイックスタート（SOAPモード）:Java APIを使用したリソースのロック](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-locking-a-resource-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#lock-resources-using-the-web-service-api}を使用してリソースをロックする

RepositoryサービスAPI（Webサービス）を使用してリソースをロックします。

1. プロジェクトファイルを含める

   * Base64を使用してリポジトリWSDLを使用するMicrosoft .NETクライアントアセンブリを作成します。
   * Microsoft .NETクライアントアセンブリを参照します。

1. サービスクライアントの作成

   Microsoft .NETクライアントアセンブリを使用して、デフォルトのコンストラクタを呼び出して`RepositoryServiceService`オブジェクトを作成します。 ユーザー名とパスワードを含む`System.Net.NetworkCredential`オブジェクトを使用して、 `Credentials`プロパティを設定します。

1. ロックするリソースのURIの指定

   ロックするリソースのURIを含む文字列を指定します。 この場合、`testResource`という名前のリソースはフォルダー`testFolder`内にあるので、URIは`"/testFolder/testResource"`になります。 Microsoft .NET Frameworkに準拠している言語（C#など）を使用する場合は、URIを`System.String`オブジェクトに格納します。

1. リソースのロック

   `RepositoryServiceService`オブジェクトの`lockResource`メソッドを呼び出し、次のパラメーターを渡します。

   * リソースのURI。
   * ロックの範囲。 この例では、リソースは排他的に使用するためにロックされるので、ロック範囲は`11`と指定します。
   * ロックの深さ。 この例では、ロックは特定のリソースにのみ適用され、メンバーや子には適用されないので、ロックの深さは`2`と指定します。
   * ロックが期限切れになるまでの秒数を示す`int`値。 この例では、`1000`の値が使用されます。
   * 最後のパラメーターに`null`を渡します。

1. リソースのロックの取得

   `RepositoryServiceService`オブジェクトの`getLocks`メソッドを呼び出し、リソースのURIを最初のパラメーターとして渡し、2番目のパラメーターに`null`を渡します。 メソッドは、繰り返し処理が可能な`Lock`オブジェクトを含む`object`配列を返します。 この例では、各`Lock`オブジェクトの`ownerUserId`、`depth`、`type`フィールドにそれぞれアクセスして、各オブジェクトに対してロックの所有者、深さ、範囲を印刷します。

1. リソースのロック解除

   `RepositoryServiceService`オブジェクトの`unlockResource`メソッドを呼び出し、リソースのURIを最初のパラメーターとして渡し、2番目のパラメーターに`null`を渡します。

**関連トピック**

[リソースのロック](aem-forms-repository.md#locking-resources)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## リソース{#deleting-resources}の削除

RepositoryサービスJava API(SOAP)を使用すると、リポジトリ内の特定の場所からプログラムでリソースを削除できます。

リソースを削除する場合、削除は通常は永続的ですが、ECMリポジトリの履歴メカニズムに従ってリソースのバージョンを保存する場合もあります。 したがって、リソースを削除する場合は、そのリソースを再び必要としないようにすることが重要です。 リソースを削除する一般的な理由には、データベースの空き領域を増やす必要がある場合などがあります。 リソースのバージョンは削除できますが、削除する場合は、論理識別子(LID)やパスではなく、リソース識別子を指定する必要があります。 フォルダーを削除すると、サブフォルダーやリソースを含むそのフォルダー内のすべての要素が自動的に削除されます。

関連リソースは削除されません。 例えば、logo.gifファイルを使用するフォームがあり、logo.gifを削除すると、保留中の関係テーブルに関係が保存されます。 別の方法として、バージョンの非推奨については、最新バージョンのオブジェクトステータスを非推奨に設定します。

ECMシステムでは、削除操作はトランザクションセーフではありません。 例えば、100個のリソースを削除しようとし、その操作が50番目のリソースで失敗した場合、最初の49個のインスタンスは削除されますが、残りは削除されません。 それ以外の場合、デフォルトの動作はロールバック（非コミットメント）です。

>[!NOTE]
>
>ECMリポジトリ（EMC Documentum Content ServerおよびIBM FileNet P8 Content Manager）で`com.adobe.repository.bindings.dsc.client.ResourceRepositoryClient.deleteResources()`メソッドを使用する場合、指定されたリソースの削除が失敗した場合、削除されたファイルの削除を取り消すことはできません。

>[!NOTE]
>
>Repositoryサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順の概要{#summary_of_steps-8}

リソースを削除するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. Repositoryサービスクライアントを作成します。
1. 削除するリソースのURIを指定します。
1. リソースを削除します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを含めます。

**サービスクライアントの作成**

プログラムによってリソースを読み取る前に、接続を確立し、資格情報を指定する必要があります。 これは、サービスクライアントを作成することで実現されます。

**削除するリソースのURIを指定します**

削除するリソースのURIを含む文字列を作成します。 構文には、次のようにスラッシュが含まれます。&quot;/*path*/*resource*&quot; 削除するリソースがフォルダーの場合、削除は繰り返し実行されます。

**リソースの削除**

Repositoryサービスメソッドを呼び出して、URIを指定してリソースを削除します。

**関連トピック**

[Java APIを使用したリソースの削除](aem-forms-repository.md#delete-resources-using-the-java-api-soap)

[WebサービスAPIを使用したリソースの削除](aem-forms-repository.md#delete-resources-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[リポジトリサービスAPIのクイックスタート](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java API(SOAP) {#delete-resources-using-the-java-api-soap}を使用してリソースを削除する

リポジトリAPI(Java)を使用してリソースを削除します。

1. プロジェクトファイルを含める

   クライアントJARファイルをJavaプロジェクトのクラスパスに含めます。

1. サービスクライアントの作成

   コンストラクターを使用し、接続プロパティを含む`ServiceClientFactory`オブジェクトを渡して、`ResourceRepositoryClient`オブジェクトを作成します。

1. 削除するリソースのURIを指定します

   取得するリソースのURIを指定します。 この場合、testResourceToBeDeletedという名前のリソースはtestFolderという名前のフォルダー内にあるので、URIは`/testFolder/testResourceToBeDeleted`になります。 URIは`java.lang.String`オブジェクトとして保存されます。 この例では、リソースは最初にリポジトリに書き込まれ、そのURIが取得されます。 リソースの書き込みについて詳しくは、[リソースの書き込み](aem-forms-repository.md#writing-resources)を参照してください。

1. リソースの削除

   `ResourceRepositoryClient`オブジェクトの`deleteResource`メソッドを呼び出し、リソースのURIをパラメーターとして渡します。

**関連トピック**

[リソースの削除](aem-forms-repository.md#deleting-resources)

[クイックスタート（SOAPモード）:Java APIを使用したリソースの検索](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#delete-resources-using-the-web-service-api}を使用してリソースを削除する

Repository API（Webサービス）を使用してリソースを削除します。

1. プロジェクトファイルを含める

   * Base64を使用してリポジトリWSDLを使用するMicrosoft .NETクライアントアセンブリを作成します。
   * Microsoft .NETクライアントアセンブリを参照します。

1. サービスクライアントの作成

   Microsoft .NETクライアントアセンブリを使用して、デフォルトのコンストラクタを呼び出して`RepositoryServiceService`オブジェクトを作成します。 ユーザー名とパスワードを含む`System.Net.NetworkCredential`オブジェクトを使用して、 `Credentials`プロパティを設定します。

1. 削除するリソースのURIを指定します

   取得するリソースのURIを指定します。 この場合、`testResourceToBeDeleted`という名前のリソースは`testFolder`という名前のフォルダーにあるので、URIは`"/testFolder/testResourceToBeDeleted"`になります。 この例では、リソースは最初にリポジトリに書き込まれ、そのURIが取得されます。 リソースの書き込みについて詳しくは、[リソースの書き込み](aem-forms-repository.md#writing-resources)を参照してください。

1. リソースの削除

   `RepositoryServiceService`オブジェクトの`deleteResources`メソッドを呼び出し、リソースのURIを含む`System.String`配列を最初のパラメーターとして渡します。 2番目のパラメーターに`null`を渡します。

**関連トピック**

[リソースの削除](aem-forms-repository.md#deleting-resources)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
