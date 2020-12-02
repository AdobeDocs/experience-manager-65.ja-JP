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


# AEM Formsリポジトリの操作{#working-with-aem-forms-repository}

**Repository Serviceについて**

Repositoryサービスは、リソースのストレージおよび管理サービスをAEM Formsに提供します。 開発者は、*AEM Forms*&#x200B;アプリケーションを作成するときに、ファイルシステムではなく、リポジトリにアセットをデプロイできます。 アセットには、XML 形式、PDF 形式（Acrobat 形式を含む）、フォームのフラグメント、画像、プロファイル、ポリシー、SWF ファイル、DDX ファイル、XML スキーマ、WSDL ファイルおよびテストデータなど、任意のタイプのコラテラルが含まれます。

例えば、次のFormsアプリケーション&#x200B;*Applications/FormsApplication*&#x200B;を考えてみましょう。

![ww_ww_formrepository](assets/ww_ww_formrepository.png)

FormsFolder内にLoan.xdpという名前のファイルがあることに注意してください。 このフォームデザインにアクセスするには、次の操作を行います（バージョンを含む）。`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.

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
>Webブラウザーを使用して、AEM Formsリポジトリを参照できます。 リポジトリを参照するには、Webブラウザー`https://[server name]:[server port]/repository`に次のURLを入力します。 「AEM Formsリポジトリでの作業」セクションに関連付けられているクイック開始の結果は、Webブラウザーを使用して確認できます。 例えば、コンテンツをAEM Formsリポジトリに追加すると、Webブラウザーでコンテンツを表示できます。 ([クイック開始（SOAPモード）を参照):Java API](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)を使用したリソースの書き込み)。

リポジトリAPIは、リポジトリに情報を格納したり、リポジトリから情報を取得したりするために使用できる操作を多数提供します。 例えば、リソースのリストを取得したり、アプリケーションの処理の一部としてリソースが必要な場合にリポジトリに格納されている特定のリソースを取得したりできます。

>[!NOTE]
>
>リポジトリAPIを使用してContent Services（非推奨）とやり取りすることはできません。 Content Services（非推奨）とやり取りするには、ドキュメント管理APIを使用します。

RepositoryサービスAPIを使用して、次のタスクを実行できます。

* フォルダーの作成. 「[フォルダーの作成](aem-forms-repository.md#creating-folders)」を参照してください。
* リソースとそのプロパティを書き込みます。 [リソースの書き込み](aem-forms-repository.md#writing-resources)を参照してください。
* 特定のコレクション内のリストリソース、または他のリソースに関連付けられているリソース。 [リソースの一覧表示](aem-forms-repository.md#listing-resources)を参照してください。
* リソースとそのプロパティを読み取ります。 [リソースの読み取り](aem-forms-repository.md#reading-resources)を参照してください。
* リソースとそのプロパティを更新します。 「[リソースの更新](aem-forms-repository.md#updating-resources)」を参照してください。
* 履歴、関連するリソース、プロパティなどのリソースを検索します。 [リソースの検索](aem-forms-repository.md#searching-for-resources)を参照してください。
* リソース間の関係を指定します。 「[リソースの関係の作成](aem-forms-repository.md#creating-resource-relationships)」を参照してください。
* リソースのロックとロック解除、アクセス制御リスト(ACL)の読み取りと書き込みなど、リソースアクセス制御を管理します。 [リソースのロック](aem-forms-repository.md#locking-resources)を参照してください。
* リソースとそのプロパティを削除します。 「[リソースの削除](aem-forms-repository.md#deleting-resources)」を参照してください。

>[!NOTE]
>
>リポジトリAPIを使用して、リソースアクセス制御の管理、リソースの検索、ECMリポジトリを使用したリソースの関係の指定を行うことはできません。

>[!NOTE]
>
>暗号化されたPDFがリポジトリに書き込まれると、自動関係抽出機能は使用できません。 それ以外の場合は、暗号化されたPDFをリポジトリに保存し、後で取得できます。 取得者は、PDFがリポジトリから取得された後に、そのPDFを復号化することを選択できます。

>[!NOTE]
>
>Repositoryサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

## フォルダーの作成 {#creating-folders}

フォルダー（リソースコレクション）は、オブジェクト（ファイルまたはリソース）を整理されたグループに格納するために使用します。 フォルダーには、リソースやサブフォルダーとも呼ばれるその他のフォルダーを含めることができます。 リソースは一度に1つのフォルダーにしか保存できません。

ファイルはアクセス制御リストー(ACL)をフォルダーから継承し、サブフォルダーはACLを親フォルダーから継承します。 したがって、子フォルダーを作成する前に、親フォルダーが存在している必要があります。 IDEでは、フォルダごとの操作のみが可能で、ファイルごとの操作はできません。 フォルダのバージョンを変更することはできません。また、バージョンを変更する必要はありません。フォルダーには、データ自体が含まれていません。 データを含むリソースのコンテナにすぎません。 デフォルトのACLはシステムレベルの権限です。つまり、ユーザーが特定のフォルダーに対する権限を付与するまで、ユーザーはシステムレベルの権限（読み取り、書き込み、トラバース、ACLの管理）を持つ必要があります。 ACLはIDEでのみ機能します。

>[!NOTE]
>
>Repositoryサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順{#summary-of-steps}の概要

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

### Java APIを使用したフォルダーの作成{#create-folders-using-the-java-api}

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
   * リソースコレクションの名前を含む`java.lang.String`。 例： `FormsFolder`

   このメソッドは、新しいフォルダーを表す`com.adobe.repository.infomodel.bean.ResourceCollection`オブジェクトを返します。

   `setDescription`メソッドを使用してフォルダーの説明を設定し、次のパラメーターを渡します。

   * リソース収集を記述する`String`。 この例では、`"test Folder"`が`.`として使用されています。


1. フォルダーをリポジトリに書き込みます

   `ResourceRepositoryClient`オブジェクトの`writeResource`メソッドを呼び出し、フォルダーと`ResourceCollection`オブジェクトのURIを渡します。 例えば、フォルダーへのURIは次の値`/Applications/FormsApplication/1.0/`にすることができます。

   メソッドは、新しく作成された`com.adobe.repository.infomodel.bean.Resource`オブジェクトのインスタンスを返します。 例えば、`com.adobe.repository.infomodel.bean.Resource`オブジェクトの`getId`メソッドを呼び出すことで、新しいリソースの識別子の値を取得できます。

**関連トピック**

[フォルダーの作成](aem-forms-repository.md#creating-folders)

[クイック開始（SOAPモード）:Java APIを使用したフォルダーの作成](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-a-folder-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#create-folders-using-the-web-service-api}を使用したフォルダーの作成

RepositoryサービスAPI（Webサービス）を使用してフォルダーを作成します。

1. プロジェクトファイルを含める

   * base64を使用してリポジトリWSDLを使用するMicrosoft .NETクライアントアセンブリを作成します。
   * Microsoft .NETクライアントアセンブリを参照します。

1. サービスクライアントの作成

   Microsoft .NETクライアントアセンブリを使用して、`RepositoryServiceService`オブジェクトを作成します。その場合は、デフォルトのコンストラクタを呼び出します。 ユーザー名とパスワードを含む`System.Net.NetworkCredential`オブジェクトを使用して、`Credentials`プロパティを設定します。

1. フォルダーの作成

   `ResourceCollection`クラスのデフォルトのコンストラクターを使用してフォルダーを作成し、次のパラメーターを渡します。

   * `Id`オブジェクト。`Id`クラスのデフォルトのコンストラクターを呼び出して作成され、`Resource`オブジェクトの`id`フィールドに割り当てられます。
   * `Lid`オブジェクト。`Lid`クラスのデフォルトのコンストラクターを呼び出して作成され、`Resource`オブジェクトの`lid`フィールドに割り当てられます。
   * リソースコレクションの名前を含む文字列。この名前は`Resource`オブジェクトの`name`フィールドに割り当てられます。 この例で使用される名前は`"testfolder"`です。
   * リソースコレクションの説明を含む文字列。これは`Resource`オブジェクトの`description`フィールドに割り当てられます。 この例で使用される説明は`"test folder"`です。

1. フォルダーをリポジトリに書き込みます

   `RepositoryServiceService`オブジェクトの`writeResource`メソッドを呼び出し、次のパラメーターを渡します。

   * フォルダーを作成するパスです。
   * フォルダーを表す`ResourceCollection`オブジェクトです。
   * 他の2つのパラメーターに対して`null`を渡します。

**関連トピック**

[フォルダーの作成](aem-forms-repository.md#creating-folders)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## リソースの書き込み{#writing-resources}

リポジトリ内の特定の場所にリソースを作成できます。 自然なファイルサイズは、データベースの制限やセッションタイムアウトの影響を受けます。 デフォルトの設定では、ファイルのサイズは25 MBに制限されます。 最大ファイルサイズを増減するには、データベース設定を変更する必要があります。

リソースを書き込むことは、リポジトリにデータを格納することと同じです。 リポジトリにリソースを書き込むと、リポジトリエコシステム内のすべてのクライアントがそのリソースにアクセスできるようになります。 XMLスキーマ、XDPファイル、XSDファイルなどのリソースをリポジトリに書き込むと、そのコンテンツはMIMEタイプに基づいて解析されます。 MIMEタイプがサポートされている場合、パーサーは他のコンテンツとの暗黙の関係があるかどうかを判定します。 例えば、カスケーディングスタイルシート(CSS)に共通のCSSを参照する相対URLがある場合、共通のCSSもリポジトリに送信する必要があります。 2つのリソース間の関係は、調整不可能な30日間の保留中の関係として保存されます。 共通のCSSをリポジトリに30日以内に送信すると、関係が形成されます。

リソースを作成すると、アクセス制御リスト(ACL)は親フォルダーから継承されます。 ルートフォルダーには、最初のリソースまたはフォルダーが作成されるまで、システムレベルの権限があります。その時点で、リソースまたはフォルダーにデフォルトのACL権限が付与されます。

RepositoryサービスJava APIまたはWebサービスAPIを使用して、プログラムによってリソースを書き込むことができます。

>[!NOTE]
>
>Repositoryサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順{#summary_of_steps-1}の概要

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

読み取るリソースのURIを含む文字列を作成します。 構文には、次の例のようにスラッシュが含まれます。&quot;/*パス*/*フォルダー*&quot;

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

### Java API {#write-resources-using-the-java-api}を使用したリソースの書き込み

RepositoryサービスAPI(Java)を使用してリソースを書き込みます。

1. プロジェクトファイルを含める

   JavaプロジェクトのクラスパスにクライアントJARファイルを含めます。

1. サービスクライアントの作成

   コンストラクターを使用し、接続プロパティを含む`ServiceClientFactory`オブジェクトを渡して、`ResourceRepositoryClient`オブジェクトを作成します。

1. リソースのターゲットフォルダーのURIを指定します

   リソースのターゲットフォルダーのURIを指定します。 この場合、`testResource`という名前のリソースは`testFolder`という名前のフォルダーに保存されるので、フォルダーのURIは`"/testFolder"`です。 URIは`java.lang.String`オブジェクトとして保存されます。

1. リソースの作成

   リソースを作成するには、まず`com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean`オブジェクトを作成する必要があります。

   `RepositoryInfomodelFactoryBean`オブジェクトの`newResource`メソッドを呼び出します。これにより`com.adobe.repository.infomodel.bean.Resource`オブジェクトが作成されます。 この例では、次のパラメーターが提供されます。

   * `com.adobe.repository.infomodel.Id`オブジェクト。`Id`クラスのデフォルトのコンストラクターを呼び出して作成します。
   * `com.adobe.repository.infomodel.Lid`オブジェクト。`Lid`クラスのデフォルトのコンストラクターを呼び出して作成します。
   * リソースのファイル名を含む`java.lang.String`。

   リソースの説明を指定するには、`Resource`オブジェクトの`setDescription`メソッドを呼び出し、説明を含む文字列を渡します。 この例では、説明は`"test resource"`です。

1. リソースコンテンツの指定

   リソースのコンテンツを作成するには、`RepositoryInfomodelFactoryBean`オブジェクトの`newResourceContent`メソッドを呼び出します。このメソッドは、`com.adobe.repository.infomodel.bean.ResourceContent`オブジェクトを返します。 &lt;a0追加/>オブジェクトの内容。 `ResourceContent`この例では、次のタスクを行うことで実現します。

   * `ResourceContent`オブジェクトの`setDataDocument`メソッドを呼び出して`com.adobe.idp.Document`オブジェクトを渡す
   * `ResourceContent`オブジェクトの`setSize`メソッドを呼び出して、`Document`オブジェクトのバイト数でサイズを渡す

   追加`Resource`オブジェクトの`setContent`メソッドを呼び出し、`ResourceContent`オブジェクトを渡すことで、リソースの内容を指定します。 詳しくは、[AEM FormsAPIリファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)を参照してください。

1. リソースをターゲットフォルダーに書き込みます

   `ResourceRepositoryClient`オブジェクトの`writeResource`メソッドを呼び出し、フォルダーのURIと`Resource`オブジェクトを渡します。

**関連トピック**

[リソースの書き込み](aem-forms-repository.md#writing-resources)

[クイック開始（SOAPモード）:Java APIを使用したリソースの作成](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#write-resources-using-the-web-service-api}を使用したリソースの書き込み

RepositoryサービスAPI（Webサービス）を使用してリソースを書き込みます。

1. プロジェクトファイルを含める

   * base64を使用してリポジトリWSDLを使用するMicrosoft .NETクライアントアセンブリを作成します。
   * Microsoft .NETクライアントアセンブリを参照します。

1. サービスクライアントの作成

   Microsoft .NETクライアントアセンブリを使用して、`RepositoryServiceService`オブジェクトを作成します。その場合は、デフォルトのコンストラクタを呼び出します。 ユーザー名とパスワードを含む`System.Net.NetworkCredential`オブジェクトを使用して、`Credentials`プロパティを設定します。

1. リソースのターゲットフォルダーのURIを指定します

   リソースのターゲットフォルダーのURIを指定します。 この場合、`testResource`という名前のリソースは`testFolder`という名前のフォルダーに保存されるので、フォルダーのURIは`"/testFolder"`です。 Microsoft .NET Frameworkに準拠した言語（C#など）を使用する場合は、URIを`System.String`オブジェクトに格納します。

1. リソースの作成

   リソースを作成するには、`Resource`クラスのデフォルトのコンストラクタを呼び出します。 この例では、次の情報が`Resource`オブジェクトに格納されます。

   * `com.adobe.repository.infomodel.Id`オブジェクト。`Id`クラスのデフォルトのコンストラクターを呼び出して作成され、`Resource`オブジェクトの`id`フィールドに割り当てられます。
   * `com.adobe.repository.infomodel.Lid`オブジェクト。`Lid`クラスのデフォルトのコンストラクターを呼び出して作成され、`Resource`オブジェクトの`lid`フィールドに割り当てられます。
   * リソースのファイル名を含む文字列。このファイル名は`Resource`オブジェクトの`name`フィールドに割り当てられます。 この例で使用される名前は`"testResource"`です。
   * リソースの説明を含む文字列です。このリソースは`Resource`オブジェクトの`description`フィールドに割り当てられます。 この例で使用される説明は`"test resource"`です。

1. リソースコンテンツの指定

   リソースのコンテンツを作成するには、`ResourceContent`クラスのデフォルトコンストラクターを呼び出します。 次に、`ResourceContent`オブジェクトにコンテンツを追加します。 この例では、次のタスクを行うことで実現します。

   * ドキュメントを含む`BLOB`オブジェクトを`ResourceContent`オブジェクトの`dataDocument`フィールドに割り当てます。
   * `BLOB`オブジェクトの`ResourceContent`フィールドに`size`オブジェクトのサイズをバイト単位で割り当てます。

   追加`ResourceContent`オブジェクトを`Resource`オブジェクトの`content`フィールドに割り当てることで、リソースの内容を指定します。

1. リソースをターゲットフォルダーに書き込みます

   `RepositoryServiceService`オブジェクトの`writeResource`メソッドを呼び出し、フォルダーのURIと`Resource`オブジェクトを渡します。 他の2つのパラメーターに対して`null`を渡します。

**関連トピック**

[リソースの書き込み](aem-forms-repository.md#writing-resources)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## リソースのリスト{#listing-resources}

リソースを一覧表示することで、リソースを見つけることができます。 リポジトリに対してクエリが実行され、特定のリソース収集に関連するすべてのリソースが検索されます。

リソースを整理したら、オペレーティングシステムで行うのと同じように、構造の特定のブランチを表示して、作成した構造を調べることができます。

リソースのリストは、次の関係によって機能します。リソースは、フォルダーのメンバーです。 メンバーシップは、「メンバー」のタイプの関係で表されます。 特定のフォルダー内のリソースをリストする場合、「メンバー」の関係によって特定のフォルダーに関連するリソースを照会します。 関係は方向性を持ちます。関係のメンバーには、ターゲットのメンバーであるソースがあります。 その出所は資源である。ターゲットは親フォルダーです。

>[!NOTE]
>
>Repositoryサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順{#summary_of_steps-2}の概要

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

リソースを含むフォルダーのパスを含む文字列を作成します。 構文には、次の例のようにスラッシュが含まれます。&quot;/*パス*/*フォルダー*&quot;

**リソースのリストの取得**

ターゲットフォルダーのパスを指定して、リソースのリストを取得するには、Repositoryサービスメソッドを呼び出します。

**関連トピック**

[Java APIを使用したリストリソース](aem-forms-repository.md#list-resources-using-the-java-api)

[WebサービスAPIを使用するリストリソース](aem-forms-repository.md#list-resources-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Repository Service APIクイック開始](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java APIを使用したリストリソース{#list-resources-using-the-java-api}

RepositoryサービスAPI(Java)を使用したリストリソース：

1. プロジェクトファイルを含める

   JavaプロジェクトのクラスパスにクライアントJARファイルを含めます。

1. サービスクライアントの作成

   コンストラクターを使用し、接続プロパティを含む`ServiceClientFactory`オブジェクトを渡して、`ResourceRepositoryClient`オブジェクトを作成します。

1. フォルダーパスの指定

   照会するリソースコレクションのURIを指定します。 この場合、URIは`"/testFolder"`です。 URIは`java.lang.String`オブジェクトとして保存されます。

1. リソースのリストの取得

   `ResourceRepositoryClient`オブジェクトの`listMembers`メソッドを呼び出し、フォルダーのURIを渡します。

   このメソッドは、`Relation.TYPE_MEMBER_OF`型の`com.adobe.repository.infomodel.bean.Relation`のソースであり、ターゲットとしてリソース収集URIを持つ`com.adobe.repository.infomodel.bean.Resource`オブジェクトの`java.util.List`を返します。 この`List`を繰り返し実行して、各リソースを取得できます。 この例では、各リソースの名前と説明が表示されます。

**関連トピック**

[リソースの一覧](aem-forms-repository.md#listing-resources)。

[クイック開始（SOAPモード）:Java APIを使用したリソースの一覧表示](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-listing-resources-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#list-resources-using-the-web-service-api}を使用したリストリソース

RepositoryサービスAPI（Webサービス）を使用したリストリソース：

1. プロジェクトファイルを含める

   * リポジトリWSDLを使用するMicrosoft .NETクライアントアセンブリを作成します。
   * Microsoft .NETクライアントアセンブリを参照します。

1. サービスクライアントの作成

   Microsoft .NETクライアントアセンブリを使用して、`RepositoryServiceService`オブジェクトを作成します。その場合は、デフォルトのコンストラクタを呼び出します。 ユーザー名とパスワードを含む`System.Net.NetworkCredential`オブジェクトを使用して、`Credentials`プロパティを設定します。

1. フォルダーパスの指定

   照会するフォルダーのURIを含む文字列を指定します。 この場合、URIは`"/testFolder"`です。 Microsoft .NET Frameworkに準拠している言語（C#など）を使用する場合は、URIを`System.String`オブジェクトに格納します。

1. リソースのリストの取得

   `RepositoryServiceService`オブジェクトの`listMembers`メソッドを呼び出し、フォルダーのURIを最初のパラメーターとして渡します。 他の2つのパラメーターに対して`null`を渡します。

   このメソッドは、`Resource`オブジェクトにキャストできるオブジェクトの配列を返します。 オブジェクト配列を繰り返し処理して、関連する各リソースを取得できます。 この例では、各リソースの名前と説明が表示されます。

**関連トピック**

[リソースの一覧](aem-forms-repository.md#listing-resources)。

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## リソースを読み取り中{#reading-resources}

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
>Repositoryサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順{#summary_of_steps-3}の概要

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

読み取るリソースのURIを含む文字列を作成します。 構文には、次の例のようにスラッシュが含まれます。&quot;/*パス*/*リソース*&quot;

**リソースの読み取り**

URIを指定してリソースを読み取るには、Repositoryサービスメソッドを呼び出します。

**関連トピック**

[Java APIを使用したリソースの読み取り](aem-forms-repository.md#read-resources-using-the-java-api)

[WebサービスAPIを使用したリソースの読み取り](aem-forms-repository.md#reading-resources-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Repository Service APIクイック開始](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java API {#read-resources-using-the-java-api}を使用してリソースを読み取ります

RepositoryサービスAPI(Java)を使用してリソースを読み取ります。

1. プロジェクトファイルを含める

   JavaプロジェクトのクラスパスにクライアントJARファイルを含めます。

1. サービスクライアントの作成

   コンストラクターを使用し、接続プロパティを含む`ServiceClientFactory`オブジェクトを渡して、`ResourceRepositoryClient`オブジェクトを作成します。

1. 読み取るリソースのURIを指定します

   取得するリソースのURIを表すstring値を指定します。 例えば、リソースの名前が&#x200B;*testResource*&#x200B;で、*testFolder*&#x200B;という名前のフォルダーにあると仮定し、`/testFolder/testResource`を指定します。

1. リソースの読み取り

   `ResourceRepositoryClient`オブジェクトの`readResource`メソッドを呼び出し、リソースのURIをパラメーターとして渡します。 このメソッドは、リソースを表す`Resource`インスタンスを返します。

**関連トピック**

[リソースの読み取り](aem-forms-repository.md#reading-resources)

[クイック開始（SOAPモード）:Java APIを使用したリソースの読み取り](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-reading-a-resource-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#reading-resources-using-the-web-service-api}を使用してリソースを読み取ります

RepositoryサービスAPI（Webサービス）を使用してリソースを読み取ります。

1. プロジェクトファイルを含める

   * リポジトリWSDLを使用するMicrosoft .NETクライアントアセンブリを作成します。 （「[Base64エンコード](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)を使用する.NETクライアントアセンブリの作成」を参照）。
   * Microsoft .NETクライアントアセンブリを参照します。 （「[Base64エンコード](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)を使用する.NETクライアントアセンブリの作成」を参照）。

1. サービスクライアントの作成

   Microsoft .NETクライアントアセンブリを使用して、`RepositoryServiceService`オブジェクトを作成します。その場合は、デフォルトのコンストラクタを呼び出します。 ユーザー名とパスワードを含む`System.Net.NetworkCredential`オブジェクトを使用して、`Credentials`プロパティを設定します。

1. 読み取るリソースのURIを指定します

   取得するリソースのURIを含む文字列を指定します。 この場合、`testResource`という名前のリソースは`testFolder`という名前のフォルダーにあるので、そのURIは`"/testFolder/testResource"`です。 Microsoft .NET Frameworkに準拠した言語（C#など）を使用する場合は、URIを`System.String`オブジェクトに格納します。

1. リソースの読み取り

   `RepositoryServiceService`オブジェクトの`readResource`メソッドを呼び出し、リソースのURIを最初のパラメーターとして渡します。 他の2つのパラメーターに対して`null`を渡します。

**関連トピック**

[リソースの読み取り](aem-forms-repository.md#reading-resources)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## リソースの更新{#updating-resources}

リポジトリ内のリソースのコンテンツを取得して更新できます。 リソースを更新しても、それらのリソースのアクセス制御は、バージョン間で変更されません。 更新を実行する場合、メジャーバージョンを増分するオプションがあります。 メジャーバージョンを増分しない場合は、マイナーバージョンが自動的に更新されます。

リソースを更新すると、指定したリソース属性に基づいて新しいバージョンが作成されます。 リソースを更新する場合は、次の2つの重要なパラメータを指定します。ターゲットURIと、更新されたすべてのメタデータを含むリソースインスタンス。 特定の属性（名前など）を変更しない場合でも、その属性は渡すインスタンスで必要です。 コンテンツの解析時に作成される関係は、特定のバージョンに追加され、特に指定がない限り転送されません。

例えば、XDPファイルを更新し、そのXDPファイルに他のリソースへの参照が含まれている場合、それらの追加参照も記録されます。 form.xdpバージョン1.0に2つの外部参照があるとします。ロゴとスタイルシートを作成し、次の3つの参照を持つようにform.xdpを更新します。ロゴ、スタイルシート、スキーマファイル。 更新中、リポジトリは3つ目の関係(スキーマファイル)を保留関係テーブルに追加します。 スキーマファイルがリポジトリに存在する場合は、関係が自動的に形成されます。 ただし、form.xdpバージョン2.0がロゴを使用しなくなった場合、form.xdpバージョン2.0はロゴとの関係を持ちません。

すべての更新操作は、アトミックおよびトランザクションです。 例えば、2人のユーザーが同じリソースを読み取り、両方がバージョン1.0をバージョン2.0に更新すると、どちらかが成功し、一方が失敗すると、リポジトリの整合性が維持され、両方が成功または失敗を確認するメッセージを受け取ります。 トランザクションがコミットされない場合、データベース障害が発生した場合はロールバックされ、アプリケーションサーバーに応じてタイムアウトまたはロールバックされます。

RepositoryサービスJava APIまたはWebサービスAPIを使用して、プログラムでリソースを更新できます。

>[!NOTE]
>
>Repositoryサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順{#summary_of_steps-4}の概要

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

リソースを読み取ります。 詳しくは、[リソースの読み取り](aem-forms-repository.md#reading-resources)を参照してください。

**リソースの更新**

リソースに新しい情報を設定し、Repositoryサービスメソッドを呼び出して、リソースを更新します。URI、更新されたリソース、およびバージョン情報の更新方法を指定します。

**関連トピック**

[Java APIを使用したリソースの更新](aem-forms-repository.md#update-resources-using-the-java-api)

[WebサービスAPIを使用したリソースの更新](aem-forms-repository.md#update-resources-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Repository Service APIクイック開始](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java API {#update-resources-using-the-java-api}を使用したリソースの更新

RepositoryサービスAPI(Java)を使用してリソースを更新します。

1. プロジェクトファイルを含める

   JavaプロジェクトのクラスパスにクライアントJARファイルを含めます。

1. サービスクライアントの作成

   コンストラクターを使用し、接続プロパティを含む`ServiceClientFactory`オブジェクトを渡して、`ResourceRepositoryClient`オブジェクトを作成します。

1. 更新するリソースを取得します

   リソースを取得して読み取るリソースのURIを指定します。 この例では、リソースのURIは`"/testFolder/testResource"`です。

1. リソースの更新

   `Resource`オブジェクトの情報を更新します。 この例では、説明を更新するには、`Resource`オブジェクトの`setDescription`メソッドを呼び出し、新しい説明文字列をパラメーターとして渡します。

   次に、`ServiceClientFactory`オブジェクトの`updateResource`メソッドを呼び出し、次のパラメーターを渡します。

   * リソースのURIを含む`java.lang.String`オブジェクト。
   * 更新されたリソース情報を含む`Resource`オブジェクトです。
   * メジャーバージョンとマイナーバージョンのどちらを更新するかを示す`boolean`値。 この例では、メジャーバージョンの値が増分されることを示す値`true`が渡されます。

**関連トピック**

[リソースの更新](aem-forms-repository.md#updating-resources)

[クイック開始（SOAPモード）:Java APIを使用したリソースの更新](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-updating-a-resource-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#update-resources-using-the-web-service-api}を使用してリソースを更新する

Repository API（Webサービス）を使用してリソースを更新します。

1. プロジェクトファイルを含める

   * リポジトリWSDLを使用するMicrosoft .NETクライアントアセンブリを作成します。
   * Microsoft .NETクライアントアセンブリを参照します。

1. サービスクライアントの作成

   Microsoft .NETクライアントアセンブリを使用して、`RepositoryServiceService`オブジェクトを作成します。その場合は、デフォルトのコンストラクタを呼び出します。 ユーザー名とパスワードを含む`System.Net.NetworkCredential`オブジェクトを使用して、`Credentials`プロパティを設定します。

1. 更新するリソースを取得します

   取得するリソースのURIを指定し、リソースを読み取ります。 この例では、リソースのURIは`"/testFolder/testResource"`です。 詳しくは、[リソースの読み取り](aem-forms-repository.md#reading-resources)を参照してください。

1. リソースの更新

   `Resource`オブジェクトの情報を更新します。 この例では、説明を更新するには、`Resource`オブジェクトの`description`フィールドに新しい値を割り当てます。

1. `RepositoryServiceService`オブジェクトの`updateResource`メソッドを呼び出し、次のパラメーターを渡します。

   * リソースのURIを含む`System.String`オブジェクト。
   * 更新されたリソース情報を含む`Resource`オブジェクトです。
   * メジャーバージョンとマイナーバージョンのどちらを更新するかを示す`boolean`値。 この例では、メジャーバージョンの値が増分されることを示す値`true`が渡されます。
   * 残りの2つのパラメーターに`null`を渡します。

**関連トピック**

[リソースの更新](aem-forms-repository.md#updating-resources)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## リソースの検索{#searching-for-resources}

リポジトリ内のリソース（履歴、関連リソース、プロパティなど）を検索するために使用するクエリを作成できます。

関連するリソースを取得して、フォームとそのフラグメントとの依存関係を判断できます。 例えば、フォームに使用するフラグメントや外部リソースを調べることができます。 画像がある場合は、その画像がどのフォームで使用されているかを調べることもできます。 また、プロパティに基づくフィルタリングを使用して、関連するリソースを検索することもできます。 例えば、指定した名前の画像を使用するすべてのフォームを検索したり、指定した名前のフォームで使用されている画像を検索したりできます。 また、リソースプロパティを使用して検索することもできます。 例えば、「%」や「_」のワイルドカードを含む名前開始を持つすべてのフォームやリソースを検索するクエリを実行できます。 プロパティに基づく検索は関係に基づくものではないことに注意してください。このような検索は、特定のリソースに関する特定の知識があるという前提に基づいています。

**クエリ文**

*クエリ*&#x200B;には、条件を論理的に結合した1つ以上のステートメントが含まれます。 *ステートメント*&#x200B;は、左辺の演算値、演算子、右辺の演算値で構成されます。 また、検索結果に使用する並べ替え順を指定できます。 *並べ替え順*&#x200B;は、SQL `ORDER BY`句と同等の情報を含み、検索の基となる属性を含む要素と、昇順または降順を使用するかどうかを示す値で構成されます。

RepositoryサービスJava APIを使用して、プログラムによってリソースを検索できます。 現時点では、WebサービスAPIを使用してリソースを検索することはできません。

**並べ替え動作**

`ResourceRepositoryClient`オブジェクトの`searchProperties`メソッドを呼び出して、並べ替え順を指定する場合、並べ替え順は考慮されません。 例えば、属性名が`name`、`secondName`、`asecondName`の3つのカスタムプロパティを持つリソースを作成するとします。 次に、属性名にソート順要素を作成し、`ascending`値を`true`に設定します。

次に、`ResourceRepositoryClient`オブジェクトの`searchProperties`メソッドを呼び出し、並べ替え順で渡します。 3つのプロパティを持つ正しいリソースが検索結果に返されます。 ただし、プロパティは属性名で並べ替えられません。 これらは、追加された順に返されます。`name`、`secondName`、`asecondName`。

>[!NOTE]
>
>Repositoryサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順{#summary_of_steps-5}の概要

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

検索の実行元となる基本パスを含む文字列を作成します。 構文には、次の例のようにスラッシュが含まれます。&quot;/*パス*/*フォルダー*&quot;

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

### Java API {#search-for-resources-using-the-java-api}を使用したリソースの検索

RepositoryサービスAPI(Java)を使用してリソースを検索します。

1. プロジェクトファイルを含める

   JavaプロジェクトのクラスパスにクライアントJARファイルを含めます。

1. サービスクライアントの作成

   コンストラクターを使用し、接続プロパティを含む`ServiceClientFactory`オブジェクトを渡して、`ResourceRepositoryClient`オブジェクトを作成します。

1. 検索用のターゲットフォルダーを指定する

   検索の実行元となるベースパスのURIを指定します。 この例では、リソースのURIは`/testFolder`です。

1. 検索で使用する属性を指定する

   検索を実行する属性の値を指定します。 属性は`com.adobe.repository.infomodel.bean.Resource`オブジェクト内に存在します。 この例では、name属性に対して検索が実行されます。したがって、`Resource`オブジェクトの名前を含む`java.lang.String`が使用されます。この場合は`testResource`です。

1. 検索で使用するクエリの作成

   クエリを作成するには、`Query`クラスのデフォルトのコンストラクターを呼び出して`com.adobe.repository.query.Query`オブジェクトを作成し、クエリにステートメントを追加します。

   ステートメントを作成するには、`com.adobe.repository.query.Query.Statement`クラスのコンストラクターを呼び出し、次のパラメーターを渡します。

   * リソース属性定数を含む左辺オペランド。 この例では、リソース名が検索の基礎として使用されるので、静的な値`Resource.ATTRIBUTE_NAME`が使用されます。
   * 属性の検索で使用される条件を含む演算子。 演算子は、`Query.Statement`クラスの静的定数の1つである必要があります。 この例では、静的な値`Query.Statement.OPERATOR_BEGINS_WITH`が使用されます。
   * 検索を実行する属性値を含む右辺オペランド。 この例では、name属性（`"testResource"`という値を含む`String`）が使用されます。

   `Query.Statement`オブジェクトの`setNamespace`メソッドを呼び出し、`com.adobe.repository.infomodel.bean.ResourceProperty`クラスに含まれる静的な値の1つを渡して、左辺の演算値の名前空間を指定します。 この例では、`ResourceProperty.RESERVED_NAMESPACE_REPOSITORY`が使用されます。

   &lt;a0追加/>オブジェクトの`Query`メソッドを呼び出し、`addStatement`オブジェクトを渡すことで、各ステートメントをクエリに送信します。`Query.Statement`

1. 検索結果の並べ替え順を作成する

   検索結果で使用する並べ替え順を指定するには、`SortOrder`クラスのデフォルトのコンストラクタを呼び出して`com.adobe.repository.query.sort.SortOrder`オブジェクトを作成し、要素を並べ替え順に追加します。

   並べ替え順の要素を作成するには、`com.adobe.repository.query.sort.SortOrder.Element`クラスのコンストラクタの1つを呼び出します。 この例では、リソースの名前が検索の基礎として使用されるので、静的な値`Resource.ATTRIBUTE_NAME`が最初のパラメーターとして使用され、昇順の順序（`boolean`値`true`）が2番目のパラメーターとして指定されます。

   &lt;a0/追加>オブジェクトの`SortOrder`メソッドを呼び出し、`addSortElement`オブジェクトを渡すことで、各要素を並べ替え順に指定します。`SortOrder.Element`

1. リソースの検索

   属性プロパティに基づいて`resources`を検索するには、`ResourceRepositoryClient`オブジェクトの`searchProperties`メソッドを呼び出し、次のパラメーターを渡します。

   * 検索を実行する基本パスを含む`String`。 この場合は`"/testFolder"`が使用されます。
   * 検索で使用されるクエリ。
   * 検索の深さ。 この場合、`com.adobe.repository.infomodel.bean.ResourceCollection.DEPTH_INFINITE`は、ベースパスとそのすべてのフォルダーが使用されることを示します。
   * ページ解除された結果セットを選択する最初の行を示す`int`値。 この例では、`0`が指定されています。
   * 返される結果の最大数を示す`int`値。 この例では、`10`が指定されています。
   * 検索で使用される並べ替え順。

   このメソッドは、指定された並べ替え順で`Resource`オブジェクトの`java.util.List`を返します。

1. 検索結果からリソースを取得

   検索結果に含まれるリソースを取得するには、`List`を繰り返し処理し、各オブジェクトを`Resource`にキャストして情報を抽出します。 この例では、各リソースの名前が表示されます。

**関連トピック**

[リソースの検索](aem-forms-repository.md#searching-for-resources)

[クイック開始（SOAPモード）:Java APIを使用したリソースの検索](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## リソースの関係の作成{#creating-resource-relationships}

リポジトリ内のリソース間の関係を指定できます。 関係には次の3種類があります。

* **依存**:リソースが他のリソースに依存する関係。つまり、関連するすべてのリソースがリポジトリ内で必要になります。
* **メンバーシップ（ファイルシステム）**:特定のフォルダー内にあるリソースの関係。
* **カスタム**:リソース間で指定する関係。例えば、あるリソースが非推奨で、別のリソースがリポジトリに導入された場合、独自の置き換え関係を指定できます。

独自のカスタムリレーションシップを作成できます。 例えば、HTMLファイルをリポジトリに格納し、そのファイルで画像を使用する場合、カスタムの関係を指定してHTMLファイルと画像を関連付けることができます（通常はXMLファイルのみがリポジトリ定義の依存関係を使用して画像に関連付けられます）。 別の例として、ツリー構造ではなく循環グラフ構造を使用して、リポジトリの別の表示を構築する場合が考えられます。 ビューアと共に円グラフを定義して、これらの関係を横断できます。 最後に、2つのリソースが完全に異なる場合でも、1つのリソースが別のリソースを置き換えることを示すことができます。 その場合は、予約範囲外の関係タイプを定義して、これらの2つのリソース間に関係を作成できます。 アプリケーションは、関係を検出して処理できる唯一のクライアントであり、その関係を検索する際に使用できます。

RepositoryサービスJava APIまたはWebサービスAPIを使用して、プログラムによってリソース間の関係を指定できます。

>[!NOTE]
>
>Repositoryサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順{#summary_of_steps-6}の概要

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

関連付けるリソースのURIを含む文字列を作成します。 構文には、次の例のようにスラッシュが含まれます。&quot;/*パス*/*リソース*&quot;

**関係の作成**

Repositoryサービスメソッドを呼び出して、関係のタイプを作成および指定します。

**関連トピック**

[Java APIを使用した関係リソースの作成](aem-forms-repository.md#create-relationship-resources-using-the-java-api)

[WebサービスAPIを使用した関係リソースの作成](aem-forms-repository.md#create-relationship-resources-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Repository Service APIクイック開始](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java API {#create-relationship-resources-using-the-java-api}を使用したリレーションシップリソースの作成

RepositoryサービスのJava APIを使用して関係リソースを作成し、次のタスクを実行します。

1. プロジェクトファイルを含める

   JavaプロジェクトのクラスパスにクライアントJARファイルを含めます。

1. サービスクライアントの作成

   コンストラクターを使用し、接続プロパティを含む`ServiceClientFactory`オブジェクトを渡して、`ResourceRepositoryClient`オブジェクトを作成します。

1. 関連付けるリソースのURIを指定します

   関連付けるリソースのURIを指定します。 この場合、リソースの名前は`testResource1`と`testResource2`で、`testFolder`という名前のフォルダーにあるので、リソースのURIは`"/testFolder/testResource1"`と`"/testFolder/testResource2"`です。 URIは`java.lang.String`オブジェクトとして保存されます。 この例では、リソースは最初にリポジトリに書き込まれ、そのURIが取得されます。 リソースの書き込みについて詳しくは、[リソースの書き込み](aem-forms-repository.md#writing-resources)を参照してください。

1. 関係の作成

   `ResourceRepositoryClient`オブジェクトの`createRelationship`メソッドを呼び出し、次のパラメーターを渡します。

   * ソースリソースのURIです。
   * ターゲットリソースのURIです。
   * 関係のタイプ。`com.adobe.repository.infomodel.bean.Relation`クラスの静的定数の1つです。 この例では、`Relation.TYPE_DEPENDANT_OF`値を指定して依存関係を確立します。
   * ターゲットリソースが新しいヘッドリソースの`com.adobe.repository.infomodel.Id`ベースの識別子に自動的に更新されるかどうかを示す`boolean`値。 この例では、依存関係があるので、`true`の値が指定されています。

   また、`ResourceRepositoryClient`オブジェクトの`getRelated`メソッドを呼び出し、次のパラメーターを渡すことで、特定のリソースに関連するリソースのリストを取得できます。

   * 関連するリソースを取得するリソースのURIです。 この例では、ソースリソース(`"/testFolder/testResource1"`)が指定されています。
   * 指定したリソースが関係のソースリソースであるかどうかを示す`boolean`値。 この例では、`true`という値が指定されています。これは、この場合です。
   * 関係タイプ。`Relation`クラスの静的定数の1つです。 この例では、依存関係は、前に使用したのと同じ値を使用して指定します。`Relation.TYPE_DEPENDANT_OF`.

   `getRelated`メソッドは、`Resource`オブジェクトの`java.util.List`を返します。このメソッドを使用して、`List`に含まれるオブジェクトを`Resource`にキャストし、関連する各リソースを取得できます。 この例では、返されるリソースのリストに`testResource2`が必要です。

**関連トピック**

[リソースの関係の作成](aem-forms-repository.md#creating-resource-relationships)

[クイック開始（SOAPモード）:Java APIを使用したリソース間の関係の作成](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-relationships-between-resources-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#create-relationship-resources-using-the-web-service-api}を使用してリレーションシップリソースを作成する

Repository API（Webサービス）を使用して、次の関係リソースを作成します。

1. プロジェクトファイルを含める

   * リポジトリWSDLを使用するMicrosoft .NETクライアントアセンブリを作成します。
   * Microsoft .NETクライアントアセンブリを参照します。

1. サービスクライアントの作成

   Microsoft .NETクライアントアセンブリを使用して、`RepositoryServiceService`オブジェクトを作成します。その場合は、デフォルトのコンストラクタを呼び出します。 ユーザー名とパスワードを含む`System.Net.NetworkCredential`オブジェクトを使用して、`Credentials`プロパティを設定します。

1. 関連付けるリソースのURIを指定します

   関連付けるリソースのURIを指定します。 この場合、リソースの名前は`testResource1`と`testResource2`で、`testFolder`という名前のフォルダーにあるので、リソースのURIは`"/testFolder/testResource1"`と`"/testFolder/testResource2"`です。 Microsoft .NET Frameworkに準拠する言語（C#など）を使用する場合、URIは`System.String`オブジェクトとして保存されます。 この例では、リソースは最初にリポジトリに書き込まれ、そのURIが取得されます。 リソースの書き込みについて詳しくは、[リソースの書き込み](aem-forms-repository.md#writing-resources)を参照してください。

1. 関係の作成

   `RepositoryServiceService`オブジェクトの`createRelationship`メソッドを呼び出し、次のパラメーターを渡します。

   * ソースリソースのURIです。
   * ターゲットリソースのURIです。
   * 関係のタイプ。 この例では、`3`値を指定して依存関係を確立します。
   * 関係タイプが指定されたかどうかを示す`boolean`値。 この例では、値`true`が指定されています。
   * ターゲットリソースが新しいヘッドリソースの`Id`ベースの識別子に自動的に更新されるかどうかを示す`boolean`値。 この例では、依存関係があるので、`true`の値が指定されています。
   * ターゲットヘッドが指定されたかどうかを示す`boolean`値。 この例では、値`true`が指定されています。
   * 最後のパラメーターに`null`を渡します。

   また、`RepositoryServiceService`オブジェクトの`getRelated`メソッドを呼び出し、次のパラメーターを渡すことで、特定のリソースに関連するリソースのリストを取得できます。

   * 関連するリソースを取得するリソースのURIです。 この例では、ソースリソース(`"/testFolder/testResource1"`)が指定されています。
   * 指定したリソースが関係のソースリソースであるかどうかを示す`boolean`値。 この例では、`true`という値が指定されています。これは、この場合です。
   * ソースリソースが指定されたかどうかを示す`boolean`値。 この例では、値`true`が指定されています。
   * 関係タイプを含む整数の配列。 この例では、以前に使用したのと同じ値を配列に使用して、依存関係を指定します。`3`.
   * 残りの2つのパラメーターに`null`を渡します。

   `getRelated`メソッドは、`Resource`オブジェクトにキャストできるオブジェクトの配列を返します。この配列を介して、関連する各リソースを取得するために反復できます。 この例では、返されるリソースのリストに`testResource2`が必要です。

**関連トピック**

[リソースの関係の作成](aem-forms-repository.md#creating-resource-relationships)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## リソースのロック{#locking-resources}

特定のユーザーが排他的に使用するため、または複数のユーザー間で共有を使用するために、リソースまたはリソースのセットをロックできます。 共有ロックは、リソースに何かが起こることを示しますが、他の誰もがそのリソースに対して行動を起こすのを妨げることはありません。 共有ロックは、シグナリングメカニズムと見なす必要があります。 排他的ロックとは、リソースをロックしたユーザーがリソースを変更することを意味し、ロックは、ユーザーがリソースにアクセスする必要がなくなり、ロックを解除するまで、他のユーザーがリソースを変更できないようにします。 リポジトリ管理者がリソースをロック解除すると、そのリソース上の排他的ロックと共有ロックがすべて自動的に削除されます。 この種のアクションは、ユーザーが使用できなくなり、リソースのロックが解除されなくなった場合に使用します。

リソースをロックすると、次の図に示すように、Workbenchの「リソース」タブに表示すると、ロックアイコンが表示されます。

![lr_lr_lockrepository](assets/lr_lr_lockrepository.png)

RepositoryサービスJava APIまたはWebサービスAPIを使用して、リソースへのアクセスをプログラムで制御できます。

>[!NOTE]
>
>Repositoryサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順{#summary_of_steps-7}の概要

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

ロックするリソースのURIを含む文字列を作成します。 構文には、次の例のようにスラッシュが含まれます。&quot;/*パス*/*リソース*&quot;

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

### Java APIを使用したリソースのロック{#lock-resources-using-the-java-api}

RepositoryサービスAPI(Java)を使用してリソースをロックする：

1. プロジェクトファイルを含める

   JavaプロジェクトのクラスパスにクライアントJARファイルを含めます。

1. サービスクライアントの作成

   コンストラクターを使用し、接続プロパティを含む`ServiceClientFactory`オブジェクトを渡して、`ResourceRepositoryClient`オブジェクトを作成します。

1. ロックするリソースのURIを指定します

   ロックするリソースのURIを指定します。 この場合、`testResource`という名前のリソースは`testFolder`という名前のフォルダーにあるので、そのURIは`"/testFolder/testResource"`です。 URIは`java.lang.String`オブジェクトとして保存されます。

1. リソースのロック

   `ResourceRepositoryClient`オブジェクトの`lockResource`メソッドを呼び出し、次のパラメーターを渡します。

   * リソースのURI。
   * ロックの範囲。 この例では、リソースは排他的に使用するためにロックされるので、ロック範囲は`com.adobe.repository.infomodel.bean.Lock.SCOPE_EXCLUSIVE`に指定されます。
   * ロックの深さ。 この例では、ロックは特定のリソースにのみ適用され、メンバーや子は適用されないので、ロックの深さは`Lock.DEPTH_ZERO`に指定されます。

   >[!NOTE]
   >
   >4つのパラメーターが必要な`lockResource`メソッドのオーバーロードされたバージョンでは、例外がスローされます。 このチュートリアルに示すように、3つのパラメーターを必要とする`lockResource`メソッドを使用してください。

1. リソースのロックを取得する

   `ResourceRepositoryClient`オブジェクトの`getLocks`メソッドを呼び出し、リソースのURIをパラメーターとして渡します。 繰り返し処理が可能なLockオブジェクトのリストを返します。 この例では、各Lockオブジェクトの`getOwnerUserId`、`getDepth`、`getType`メソッドをそれぞれ呼び出して、各オブジェクトのロック所有者、深さ、範囲を印刷します。

1. リソースのロック解除

   `ResourceRepositoryClient`オブジェクトの`unlockResource`メソッドを呼び出し、リソースのURIをパラメーターとして渡します。 詳しくは、[AEM FormsAPIリファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)を参照してください。

**関連トピック**

[リソースのロック](aem-forms-repository.md#locking-resources)

[クイック開始（SOAPモード）:Java APIを使用したリソースのロック](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-locking-a-resource-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#lock-resources-using-the-web-service-api}を使用してリソースをロックする

RepositoryサービスAPI（Webサービス）を使用してリソースをロックするには：

1. プロジェクトファイルを含める

   * Base64を使用してリポジトリWSDLを使用するMicrosoft .NETクライアントアセンブリを作成します。
   * Microsoft .NETクライアントアセンブリを参照します。

1. サービスクライアントの作成

   Microsoft .NETクライアントアセンブリを使用して、`RepositoryServiceService`オブジェクトを作成します。その場合は、デフォルトのコンストラクタを呼び出します。 ユーザー名とパスワードを含む`System.Net.NetworkCredential`オブジェクトを使用して、`Credentials`プロパティを設定します。

1. ロックするリソースのURIを指定します

   ロックするリソースのURIを含む文字列を指定します。 この場合、`testResource`という名前のリソースはフォルダー`testFolder`内にあるので、そのURIは`"/testFolder/testResource"`です。 Microsoft .NET Frameworkに準拠した言語（C#など）を使用する場合は、URIを`System.String`オブジェクトに格納します。

1. リソースのロック

   `RepositoryServiceService`オブジェクトの`lockResource`メソッドを呼び出し、次のパラメーターを渡します。

   * リソースのURI。
   * ロックの範囲。 この例では、リソースは排他的に使用するためにロックされるので、ロック範囲は`11`に指定されます。
   * ロックの深さ。 この例では、ロックは特定のリソースにのみ適用され、メンバーや子は適用されないので、ロックの深さは`2`に指定されます。
   * ロックが切れるまでの秒数を示す`int`値。 この例では、`1000`の値が使用されます。
   * 最後のパラメーターに`null`を渡します。

1. リソースのロックを取得する

   `RepositoryServiceService`オブジェクトの`getLocks`メソッドを呼び出し、リソースのURIを最初のパラメーターとして渡し、2番目のパラメーターとして`null`を渡します。 このメソッドは、`Lock`オブジェクトを含む`object`配列を返します。この配列を使用して反復を行うことができます。 この例では、各`Lock`オブジェクトの`ownerUserId`、`depth`、`type`フィールドにそれぞれアクセスすることで、各オブジェクトに対してロックの所有者、深さ、範囲が印刷されます。

1. リソースのロック解除

   `RepositoryServiceService`オブジェクトの`unlockResource`メソッドを呼び出し、リソースのURIを最初のパラメーターとして渡し、2番目のパラメーターとして`null`を渡します。

**関連トピック**

[リソースのロック](aem-forms-repository.md#locking-resources)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## リソースの削除{#deleting-resources}

RepositoryサービスJava API(SOAP)を使用すると、リポジトリ内の特定の場所からリソースをプログラムで削除できます。

リソースを削除する場合、削除は通常は永続的ですが、ECMリポジトリは履歴メカニズムに従ってリソースのバージョンを保存する場合があります。 したがって、リソースを削除する場合は、そのリソースが再び必要にならないことを確認することが重要です。 リソースを削除する一般的な理由としては、データベースの使用可能な領域を増やす必要がある場合があります。 リソースのバージョンは削除できますが、削除する場合は、そのリソースの論理識別子(LID)やパスではなく、リソースの識別子を指定する必要があります。 フォルダーを削除すると、サブフォルダーやリソースを含む、そのフォルダー内のすべての要素が自動的に削除されます。

関連するリソースは削除されません。 例えば、logo.gifファイルを使用するフォームがあり、logo.gifを削除すると、保留中の関係テーブルに関係が保存されます。 別の方法として、バージョンの非推奨の場合は、最新バージョンのオブジェクトステータスを非推奨に設定します。

ECMシステムでは、削除操作はトランザクションに対して安全ではありません。 例えば、100個のリソースを削除しようとした場合に、50個目のリソースで操作が失敗すると、最初の49個のインスタンスは削除されますが、残りは削除されません。 それ以外の場合、デフォルトの動作はrollback (non-commitment)です。

>[!NOTE]
>
>ECMリポジトリ（EMC Documentum Content ServerおよびIBM FileNet P8 Content Manager）で`com.adobe.repository.bindings.dsc.client.ResourceRepositoryClient.deleteResources()`メソッドを使用する場合、指定されたリソースの1つに対して削除が失敗した場合、削除されたファイルの削除を取り消すことはできません。

>[!NOTE]
>
>Repositoryサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順{#summary_of_steps-8}の概要

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

削除するリソースのURIを含む文字列を作成します。 構文には、次の例のようにスラッシュが含まれます。&quot;/*パス*/*リソース*&quot; 削除するリソースがフォルダーの場合、削除は再帰的に行われます。

**リソースの削除**

URIを指定してリソースを削除するには、Repositoryサービスメソッドを呼び出します

**関連トピック**

[Java APIを使用したリソースの削除](aem-forms-repository.md#delete-resources-using-the-java-api-soap)

[WebサービスAPIを使用したリソースの削除](aem-forms-repository.md#delete-resources-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Repository Service APIクイック開始](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java API(SOAP) {#delete-resources-using-the-java-api-soap}を使用したリソースの削除

リポジトリAPI(Java)を使用してリソースを削除します。

1. プロジェクトファイルを含める

   JavaプロジェクトのクラスパスにクライアントJARファイルを含めます。

1. サービスクライアントの作成

   コンストラクターを使用し、接続プロパティを含む`ServiceClientFactory`オブジェクトを渡して、`ResourceRepositoryClient`オブジェクトを作成します。

1. 削除するリソースのURIを指定します

   取得するリソースのURIを指定します。 この場合、testResourceToBeDeletedという名前のリソースはtestFolderという名前のフォルダーにあるので、そのURIは`/testFolder/testResourceToBeDeleted`です。 URIは`java.lang.String`オブジェクトとして保存されます。 この例では、リソースは最初にリポジトリに書き込まれ、そのURIが取得されます。 リソースの書き込みについて詳しくは、[リソースの書き込み](aem-forms-repository.md#writing-resources)を参照してください。

1. リソースの削除

   `ResourceRepositoryClient`オブジェクトの`deleteResource`メソッドを呼び出し、リソースのURIをパラメーターとして渡します。

**関連トピック**

[リソースの削除](aem-forms-repository.md#deleting-resources)

[クイック開始（SOAPモード）:Java APIを使用したリソースの検索](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#delete-resources-using-the-web-service-api}を使用したリソースの削除

Repository API（Webサービス）を使用してリソースを削除します。

1. プロジェクトファイルを含める

   * Base64を使用してリポジトリWSDLを使用するMicrosoft .NETクライアントアセンブリを作成します。
   * Microsoft .NETクライアントアセンブリを参照します。

1. サービスクライアントの作成

   Microsoft .NETクライアントアセンブリを使用して、`RepositoryServiceService`オブジェクトを作成します。その場合は、デフォルトのコンストラクタを呼び出します。 ユーザー名とパスワードを含む`System.Net.NetworkCredential`オブジェクトを使用して、`Credentials`プロパティを設定します。

1. 削除するリソースのURIを指定します

   取得するリソースのURIを指定します。 この場合、`testResourceToBeDeleted`という名前のリソースは`testFolder`という名前のフォルダーにあるので、そのURIは`"/testFolder/testResourceToBeDeleted"`です。 この例では、リソースは最初にリポジトリに書き込まれ、そのURIが取得されます。 リソースの書き込みについて詳しくは、[リソースの書き込み](aem-forms-repository.md#writing-resources)を参照してください。

1. リソースの削除

   `RepositoryServiceService`オブジェクトの`deleteResources`メソッドを呼び出し、リソースのURIを最初のパラメーターとして含む`System.String`配列を渡します。 2番目のパラメーターに`null`を渡します。

**関連トピック**

[リソースの削除](aem-forms-repository.md#deleting-resources)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
