---
title: データソースの設定
seo-title: データソースの設定
description: ここでは、各種のデータソースを設定し、それらのデータソースを使用してフォームデータモデルを作成する方法について説明します。
seo-description: ここでは、各種のデータソースを設定し、それらのデータソースを使用してフォームデータモデルを作成する方法について説明します。
uuid: 12360c8c-b596-4f9b-837a-10a8ff5c7448
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9d78a6dc-fc9c-415b-b817-164fe6648b30
docset: aem65
feature: フォームデータモデル
exl-id: 7a1d9d57-66f4-4f20-91c2-ace5a71a52f2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2023'
ht-degree: 58%

---

# データソースの設定{#configure-data-sources}

![](do-not-localize/data-integeration.png)

AEM Forms のデータ統合機能により、複数の異なるデータソースを設定して接続することができます。以下のタイプがサポートされています。これらのタイプは、すぐに使用することができます。ただし、これらの機能を少しカスタマイズするだけで、他のデータソースを統合することもできます。

* リレーショナルデータベース - MySQL、Microsoft SQL Server、IBM DB2、Oracle RDBMS
* AEM ユーザープロファイル
* RESTful Web サービス
* SOAP ベース Web サービス
* OData サービス

データ統合では、すぐに使用できる認証タイプとして、OAuth2.0 認証、基本認証、API キー認証がサポートされています。また、Web サービスにアクセスするためのカスタムの認証タイプを実装することもできます。RESTful サービス、SOAP ベースサービス、OData サービスは AEM クラウドサービスで設定し、リレーショナルデータベース用の JDBC と AEM ユーザープロファイル用のコネクターは、AEM Web コンソールで設定します。

## リレーショナルデータベースの設定 {#configure-relational-database}

AEM Web Console Configuration を使用してリレーショナルデータベースを設定することができます。以下の操作を実行します。

1. AEM Webコンソール(https://server:host/system/console/configMgr)に移動します。
1. 「**[!UICONTROL Apache Sling Connection Pooled DataSource]**」という設定を探し、その設定をタップして編集モードで開きます。
1. 設定ダイアログで、設定するデータベースの詳細を指定します。例えば、以下のような詳細を指定します。

   * データソースの名前
   * データソース名が保管されるデータソースサービスプロパティ
   * JDBC ドライバーの Java クラス名
   * JDBC 接続 URI
   * JDBC ドライバーとの接続を確立するためのユーザー名とパスワード

   >[!NOTE]
   >
   >データソースを設定する前に、パスワードなどの機密情報を必ず暗号化してください。暗号化するには、以下の手順を実行します。
   >
   >    
   >    
   >    1. https://&#39;[server]:[port]&#39;/system/console/cryptoに移動します。
   >    1. 「**[!UICONTROL プレーンテキスト]**」フィールドで、暗号化するパスワードまたは任意の文字列を指定して、「**[!UICONTROL Protect]**」をタップします。

   >    
   >    
   >    
   >暗号化されたテキストが「保護されたテキスト」フィールドに表示され、設定で指定できます。

1. プールからオブジェクトを取得するときにそのオブジェクトを検証する場合は「**[!UICONTROL Test on Borrow]**」を有効にし、プールにオブジェクトを返すときにそのオブジェクトを検証する場合は「**[!UICONTROL Test on Return]**」を有効にします。
1. 「**[!UICONTROL 検証クエリ]**」フィールドで SQL SELECT クエリを指定して、プールからの接続を検証します。このクエリでは、1 行以上の行が返される必要があります。使用しているデータベースに応じて、以下のいずれかを指定します。

   * SELECT 1 （MySQLとMS SQL）
   * SELECT 1 from dual（Oracle の場合）

1. 「**[!UICONTROL 保存]**」をタップして設定を保存します。

## AEM ユーザープロファイルの設定 {#configure-aem-user-profile}

AEM Web コンソールでユーザープロファイルコネクター設定を使用して、AEM のユーザープロファイルを設定することができます。以下の操作を実行します。

1. AEM Webコンソール(https://&#39;[server]:[port]&#39;system/console/configMgr)に移動します。
1. **[!UICONTROL AEM Forms Data Integrations - User Profile Connector Configuration]**&#x200B;を探し、をタップして設定を編集モードで開きます。
1. ユーザープロファイルコネクター設定ダイアログで、ユーザープロファイルプロパティの追加、削除、更新を行うことができます。ここで指定したプロパティは、フォームデータモデルで使用することができます。次の形式を使用して、ユーザープロファイルのプロパティを指定します。

   `name=[property_name_with_location_in_user_profile],type=[property_type]`

   例：

   * `name=profile/phoneNumber,type=string`
   * `name=profile/empLocation/*/city,type=string`

   >[!NOTE]
   >
   >上記の例の&#x200B;*****&#x200B;は、CRXDE構造のAEMユーザープロファイルの`profile/empLocation/`ノードの下のすべてのノードを表します。 つまり、フォームデータモデルは、`profile/empLocation/`ノードの下の任意のノードに存在するタイプ`string`の`city`プロパティにアクセスできます。 ただし、指定されたプロパティが存在するノードの構造が統一されている必要があります。

1. 「**[!UICONTROL 保存]**」をタップして設定を保存します。

## クラウドサービス設定用フォルダーの構成 {#cloud-folder}

>[!NOTE]
RESTful サービス、SOAP サービス、OData サービスを設定するには、クラウドサービス用のフォルダーを設定する必要があります。

AEM内のすべてのクラウドサービス設定は、AEMリポジトリの`/conf`フォルダーに統合されます。 デフォルトの場合、`conf` フォルダーには `global` フォルダーが含まれています。このフォルダーで、クラウドサービスの設定を作成することができます。ただし、このフォルダーを手動でクラウド設定用に有効にする必要があります。追加のフォルダーを `conf` フォルダー内に作成して、クラウドサービスの作成と編集を行うこともできます。

クラウドサービス設定用のフォルダーを構成するには、以下の手順を実行します。

1. **[!UICONTROL ツール／一般／設定ブラウザー]**&#x200B;に移動します。
   * 詳しくは、[設定ブラウザー](/help/sites-administering/configurations.md)のドキュメントを参照してください。
1. 以下の手順を実行して、global フォルダーをクラウド設定用に有効にします。クラウドサービス設定用に別のフォルダーを作成する場合は、この手順をスキップしてください。

   1. **[!UICONTROL 設定ブラウザー]**&#x200B;で、「`global`」フォルダーを選択して「**[!UICONTROL プロパティ]**」をタップします。

   1. **[!UICONTROL 設定プロパティ]**&#x200B;ダイアログで、「**[!UICONTROL クラウド設定]**」を有効にします。

   1. 「**[!UICONTROL 保存して閉じる]**」をタップして設定内容を保存し、ダイアログを閉じます。

1. **[!UICONTROL 設定ブラウザー]**&#x200B;で「**[!UICONTROL 作成]**」をタップします。
1. **[!UICONTROL 設定を作成]**&#x200B;ダイアログでフォルダーのタイトルを指定し、「**[!UICONTROL クラウド設定]**」を有効にします。
1. 「**[!UICONTROL 作成]**」をタップします。これで、クラウドサービス設定が有効になったフォルダーが作成されました。

## RESTful Web サービスの設定 {#configure-restful-web-services}

RESTful Webサービスは、Swagger定義ファイルのJSON形式またはYAML形式の[Swagger仕様](https://swagger.io/specification/)を使用して記述できます。 AEMクラウドサービスでRESTful Webサービスを設定するには、ファイルシステム上にSwaggerファイルが存在するか、ファイルがホストされているURLが存在することを確認します。

RESTful サービスを設定するには、以下の手順を実行します。

1. **[!UICONTROL ツール／Cloud Services／データソース]**&#x200B;に移動します。クラウド設定の作成対象となるフォルダーをタップして選択します。

   クラウドサービス設定用フォルダーの作成方法と構成方法については、「[クラウドサービス設定用フォルダーの構成](../../forms/using/configure-data-sources.md#cloud-folder)」を参照してください。

1. 「**[!UICONTROL 作成]**」をタップして、**[!UICONTROL データソース設定を作成]**&#x200B;ウィザードを開きます。設定の名前と、必要に応じて設定のタイトルを指定し、「**[!UICONTROL サービスタイプ]**」ドロップダウンで「**[!UICONTROL RESTful サービス]**」を選択します。必要な場合は、設定のサムネイル画像を選択して「**[!UICONTROL 次へ]**」をタップします。
1. 以下に示す RESTful サービスの詳細情報を指定します。

   * 「Swagger Source」ドロップダウンから「URL」または「File」を選択し、Swagger URLをSwagger定義ファイルに指定するか、ローカルファイルシステムからSwaggerファイルをアップロードします。
   * Swaggerソースの入力に基づいて、次のフィールドに値が事前入力されます。

      * スキーム：REST API で使用される転送プロトコル。ドロップダウンリストに表示されるスキームタイプの数は、Swaggerソースで定義されているスキームによって異なります。
      * ホスト：REST API を提供するホストのドメイン名または IP アドレス。このフィールドは必須です。
      * 基本パス：すべての API パスの URL プリフィックス。これはオプションのフィールドです。\
         必要に応じて、これらのフィールドの事前入力された値を編集します。
   * RESTfulサービスにアクセスするための認証タイプ（なし、OAuth2.0、基本認証、APIキー、カスタム認証、相互認証）を選択し、それに応じて認証の詳細を指定します。

   認証タイプとして **[!UICONTROL API キー]**&#x200B;を選択した場合は、API キーの値を指定します。API キーは、リクエストヘッダーまたはクエリパラメーターとして送信できます。「**[!UICONTROL 場所]**」ドロップダウンリストから次のオプションの 1 つを選択し、それに応じて「**[!UICONTROL パラメーター名]**」フィールドにヘッダーまたはクエリパラメーターの名前を指定します。

   認証の種類として&#x200B;**[!UICONTROL 相互認証]**&#x200B;を選択した場合は、[RESTfulおよびSOAP Webサービスの証明書ベースの相互認証](#mutual-authentication)を参照してください。

1. 「**[!UICONTROL 作成]**」をタップして、RESTful サービス用のクラウド設定を作成します。

### パフォーマンスを最適化するためのフォームデータモデルHTTPクライアント設定{#fdm-http-client-configuration}

[!DNL Experience Manager Forms] フォームデータモデルを使用して、データソースとしてRESTful Webサービスとの統合時に、パフォーマンス最適化のためのHTTPクライアント設定が含まれている。次の手順を実行して、フォームデータモデルのHTTPクライアントを設定します。

1. [!DNL Experience Manager Forms]オーサーインスタンスに管理者としてログインし、[!DNL Experience Manager] Webコンソールバンドルに移動します。 デフォルトのURLは[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)です。

1. 「**[!UICONTROL フォームデータモデルのHTTPクライアント設定（RESTデータソース用）]**」をタップします。

1. [!UICONTROL Form Data Model Http Client Configuration for REST data source]ダイアログで、次の操作を実行します。

   * 「**[!UICONTROL Connection limit in total]**」フィールドで、フォームデータモデルとRESTful Webサービス間の許可される接続の最大数を指定します。 デフォルト値は20接続です。

   * **[!UICONTROL Connection limit on per route basis]**&#x200B;フィールドに、各ルートに許可される接続の最大数を指定します。 デフォルト値は2接続です。

   * **[!UICONTROL キープアライブ]**&#x200B;フィールドに、永続的なHTTP接続を維持する期間を指定します。 デフォルト値は 15 秒です。

   * **[!UICONTROL 「接続タイムアウト]**」フィールドに、[!DNL Experience Manager Forms]サーバーが接続確立を待機する時間を指定します。 デフォルト値は 10 秒です。

   * **[!UICONTROL Socket timeout]**&#x200B;フィールドで、2つのデータパケットの間に無操作状態が続く最大時間を指定します。 デフォルト値は 30 秒です。


## SOAP Web サービスの設定 {#configure-soap-web-services}

SOAP ベースの Web サービスは、[Web Services Description Language（WSDL）の仕様](https://www.w3.org/TR/wsdl)に従って記述します。AEM クラウドサービスで SOAP ベースの Web サービスを設定するには、その Web サービスの WSDL URL を確認して、以下の手順を実行します。

1. **[!UICONTROL ツール／Cloud Services／データソース]**&#x200B;に移動します。クラウド設定の作成対象となるフォルダーをタップして選択します。

   クラウドサービス設定用フォルダーの作成方法と構成方法については、「[クラウドサービス設定用フォルダーの構成](../../forms/using/configure-data-sources.md#cloud-folder)」を参照してください。

1. 「**[!UICONTROL 作成]**」をタップして、**[!UICONTROL データソース設定を作成]**&#x200B;ウィザードを開きます。設定の名前と、必要に応じて設定のタイトルを指定し、「**[!UICONTROL サービスタイプ]**」ドロップダウンで「**[!UICONTROL SOAP Web サービス]**」を選択します。必要な場合は、設定のサムネイル画像を選択して「**[!UICONTROL 次へ]**」をタップします。
1. 以下に示す SOAP Web サービスの詳細情報を指定します。

   * Web サービスの WSDL URL を指定します。
   * サービスエンドポイント。WSDL で指定されているサービスエンドポイントを上書きするには、このフィールドの値を指定します。
   * SOAPサービスにアクセスするための認証の種類（「なし」、「OAuth2.0」、「基本認証」、「カスタム認証」、「X509トークン」、「相互認証」）を選択し、認証の詳細を指定します。

      認証の種類として&#x200B;**[!UICONTROL X509トークン]**&#x200B;を選択した場合は、X509証明書を設定します。 詳しくは、「[証明書の設定](install-configure-document-services.md#set-up-certificates-for-reader-extension-and-encryption-service)」を参照してください。
**[!UICONTROL Key Alias]**&#x200B;フィールドにX509証明書のキーストアエイリアスを指定します。 **[!UICONTROL 有効期間]**&#x200B;フィールドで、認証リクエストが有効なままになるまでの時間を秒単位で指定します。 オプションで、メッセージの本文、タイムスタンプのヘッダー、またはその両方に署名する場合に選択します。

      認証の種類として&#x200B;**[!UICONTROL 相互認証]**&#x200B;を選択した場合は、[RESTfulおよびSOAP Webサービスの証明書ベースの相互認証](#mutual-authentication)を参照してください。

1. 「**[!UICONTROL 作成]**」をタップして、SOAP Web サービス用のクラウド設定を作成します。

## OData サービスの設定 {#config-odata}

OData サービスは、そのサービスのルート URL によって識別されます。AEM クラウドサービスで OData サービスを設定するには、そのサービスのルート URL を確認して、以下の手順を実行します。

>[!NOTE]
オンライン環境またはオンプレミス環境で Microsoft Dynamics 365 を設定する詳しい手順については、「[Microsoft Dynamics OData 設定](/help/forms/using/ms-dynamics-odata-configuration.md)」を参照してください。

1. **[!UICONTROL ツール／Cloud Services／データソース]**&#x200B;に移動します。クラウド設定の作成対象となるフォルダーをタップして選択します。

   クラウドサービス設定用フォルダーの作成方法と構成方法については、「[クラウドサービス設定用フォルダーの構成](../../forms/using/configure-data-sources.md#cloud-folder)」を参照してください。

1. 「**[!UICONTROL 作成]**」をタップして、**[!UICONTROL データソース設定を作成]**&#x200B;ウィザードを開きます。設定の名前と、必要に応じて設定のタイトルを指定し、「**[!UICONTROL サービスタイプ]**」ドロップダウンで「**[!UICONTROL OData サービス]**」を選択します。必要な場合は、設定のサムネイル画像を選択して「**[!UICONTROL 次へ]**」をタップします。
1. 以下に示す OData サービスの詳細情報を指定します。

   * 設定する OData サービスのルート URL を指定します。
   * ODataサービスにアクセスするための認証の種類（「なし」、「OAuth2.0」、「基本認証」、「カスタム認証」）を選択し、それに応じて認証の詳細を指定します。

   >[!NOTE]
   OData エンドポイントをサービスルートとして使用して Microsoft Dynamics サービスに接続する場合は、OAuth 2.0 認証を選択する必要があります。

1. 「**作成**」をタップして、OData サービス用のクラウド設定を作成します。

## RESTful WebサービスとSOAP Webサービスの証明書ベースの相互認証{#mutual-authentication}

フォームデータモデルの相互認証を有効にすると、フォームデータモデルを実行するデータソースとAEMサーバーの両方が、データを共有する前に、相互のIDを認証します。 RESTおよびSOAPベースの接続（データソース）に対して相互認証を使用できます。 AEM Forms環境でフォームデータモデルの相互認証を設定するには、次の手順を実行します。

1. 秘密鍵（証明書）を[!DNL AEM Forms]サーバーにアップロードします。 秘密鍵をアップロードするには：
   1. [!DNL AEM Forms]サーバーに管理者としてログインします。
   1. **[!UICONTROL ツール]** > **[!UICONTROL セキュリティ]** > **[!UICONTROL ユーザー]**&#x200B;に移動します。 `fd-cloudservice`ユーザーを選択し、「**[!UICONTROL プロパティ]**」をタップします。
   1. 「**[!UICONTROL キーストア]**」タブを開き、「**[!UICONTROL 秘密鍵をキーストアファイルから追加]**」オプションを展開して、キーストアファイルをアップロードし、エイリアスとパスワードを指定して、「**[!UICONTROL 送信]**」をタップします。 証明書がアップロードされます。  秘密鍵のエイリアスは、証明書で言及され、証明書の作成時に設定されます。
1. 信頼証明書をグローバルTrust Storeにアップロードします。 証明書をアップロードするには：
   1. **[!UICONTROL ツール]** > **[!UICONTROL セキュリティ]** > **[!UICONTROL Trust Store]**&#x200B;に移動します。
   1. 「**[!UICONTROL CERファイルから証明書を追加]**」オプションを展開し、「**[!UICONTROL 証明書ファイル]**」をタップし、証明書をアップロードして、「**[!UICONTROL 送信]**」をタップします。
1. [SOAP](#configure-soap-web-services)または[RESTful](#configure-restful-web-services) Webサービスをデータソースとして設定し、認証の種類として&#x200B;**[!UICONTROL 相互認証]**&#x200B;を選択します。 `fd-cloudservice`ユーザーに対して複数の自己署名証明書を設定する場合は、証明書のキーエイリアス名を指定します。

## 次の手順 {#next-steps}

上記の手順により、データソースが設定されました。次に、フォームデータモデルを作成します。データソースが設定されていないフォームデータモデルが既に作成されている場合は、上記の手順で設定したデータソースにそのフォームデータモデルを関連付けます。詳しくは、「[フォームデータモデルの作成](/help/forms/using/create-form-data-models.md)」を参照してください。
