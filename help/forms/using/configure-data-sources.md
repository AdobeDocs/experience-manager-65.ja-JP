---
title: データソースの設定
seo-title: Configure data sources
description: ここでは、各種のデータソースを設定し、それらのデータソースを使用してフォームデータモデルを作成する方法について説明します。
seo-description: Learn how to configure different types of data sources and leverage to create form data models.
uuid: 12360c8c-b596-4f9b-837a-10a8ff5c7448
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9d78a6dc-fc9c-415b-b817-164fe6648b30
docset: aem65
feature: Form Data Model
exl-id: 7a1d9d57-66f4-4f20-91c2-ace5a71a52f2
source-git-commit: c92b5b5dd70e7a4e696d8d75282edbc88a13ba51
workflow-type: tm+mt
source-wordcount: '2010'
ht-degree: 57%

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

1. AEM Web コンソール (https://server:host/system/console/configMgr) に移動します。
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
   >    1. https://&#39;に移動します。[server]:[ポート]&#39;/system/console/crypto.
   >    1. 内 **[!UICONTROL プレーンテキスト]** フィールドで、暗号化するパスワードまたは任意の文字列を指定してをタップします。 **[!UICONTROL Protect]**.

   >    
   >    
   >    
   >暗号化されたテキストが「保護されたテキスト」フィールドに表示され、設定で指定できます。

1. プールからオブジェクトを取得するときにそのオブジェクトを検証する場合は「**[!UICONTROL Test on Borrow]**」を有効にし、プールにオブジェクトを返すときにそのオブジェクトを検証する場合は「**[!UICONTROL Test on Return]**」を有効にします。
1. 「**[!UICONTROL 検証クエリ]**」フィールドで SQL SELECT クエリを指定して、プールからの接続を検証します。このクエリでは、1 行以上の行が返される必要があります。使用しているデータベースに応じて、以下のいずれかを指定します。

   * SELECT 1 （MySQL と MS SQL）
   * SELECT 1 from dual（Oracle の場合）

1. タップ **[!UICONTROL 保存]** 設定を保存します。

## AEM ユーザープロファイルの設定 {#configure-aem-user-profile}

AEM Web コンソールでユーザープロファイルコネクター設定を使用して、AEM のユーザープロファイルを設定することができます。以下の操作を実行します。

1. AEM Web コンソール ( https://&#39; ) に移動します。[server]:[ポート]&#39;system/console/configMgr.
1. を探す **[!UICONTROL AEM Forms Data Integrations - User Profile Connector の設定]** をタップして、設定を編集モードで開きます。
1. ユーザープロファイルコネクター設定ダイアログで、ユーザープロファイルプロパティの追加、削除、更新を行うことができます。ここで指定したプロパティは、フォームデータモデルで使用することができます。次の形式を使用して、ユーザープロファイルのプロパティを指定します。

   `name=[property_name_with_location_in_user_profile],type=[property_type]`

   例：

   * `name=profile/phoneNumber,type=string`
   * `name=profile/empLocation/*/city,type=string`

   >[!NOTE]
   >
   >この **&#42;** 上記の例では、 `profile/empLocation/` CRXDE 構造のAEMユーザープロファイルのノード。 つまり、フォームデータモデルは `city` 型のプロパティ `string` 以下の任意のノードに存在する `profile/empLocation/` ノード。 ただし、指定されたプロパティが存在するノードの構造が統一されている必要があります。

1. タップ **[!UICONTROL 保存]** 設定を保存します。

## クラウドサービス設定用フォルダーの構成 {#cloud-folder}

>[!NOTE]
>
>RESTful サービス、SOAP サービス、OData サービスを設定するには、クラウドサービス用のフォルダーを設定する必要があります。

AEMのすべてのクラウドサービス設定は、 `/conf` フォルダーをAEMリポジトリに保存します。 デフォルトの場合、`conf` フォルダーには `global` フォルダーが含まれています。このフォルダーで、クラウドサービスの設定を作成することができます。ただし、このフォルダーを手動でクラウド設定用に有効にする必要があります。追加のフォルダーを `conf` フォルダー内に作成して、クラウドサービスの作成と編集を行うこともできます。

クラウドサービス設定用のフォルダーを構成するには、以下の手順を実行します。

1. **[!UICONTROL ツール／一般／設定ブラウザー]**&#x200B;に移動します。
   * 詳しくは、 [設定ブラウザー](/help/sites-administering/configurations.md) のドキュメントを参照してください。
1. 以下の手順を実行して、global フォルダーをクラウド設定用に有効にします。クラウドサービス設定用に別のフォルダーを作成する場合は、この手順をスキップしてください。

   1. **[!UICONTROL 設定ブラウザー]**&#x200B;で、「`global`」フォルダーを選択して「**[!UICONTROL プロパティ]**」をタップします。

   1. **[!UICONTROL 設定プロパティ]**&#x200B;ダイアログで、「**[!UICONTROL クラウド設定]**」を有効にします。

   1. 「**[!UICONTROL 保存して閉じる]**」をタップして設定内容を保存し、ダイアログを閉じます。

1. **[!UICONTROL 設定ブラウザー]**&#x200B;で「**[!UICONTROL 作成]**」をタップします。
1. **[!UICONTROL 設定を作成]**&#x200B;ダイアログでフォルダーのタイトルを指定し、「**[!UICONTROL クラウド設定]**」を有効にします。
1. 「**[!UICONTROL 作成]**」をタップします。これで、クラウドサービス設定が有効になったフォルダーが作成されました。

## RESTful Web サービスの設定 {#configure-restful-web-services}

RESTful Web サービスは、 [Swagger の仕様](https://swagger.io/specification/) JSON 形式または YAML 形式の Swagger 定義ファイル。 AEM クラウドサービスで RESTful Web サービスを設定するには、ファイルシステム上に Swagger ファイルが存在するか、ファイルがホストされている URL が存在していることを確認します。

RESTful サービスを設定するには、以下の手順を実行します。

1. **[!UICONTROL ツール／Cloud Services／データソース]**&#x200B;に移動します。クラウド設定の作成対象となるフォルダーをタップして選択します。

   クラウドサービス設定用フォルダーの作成方法と構成方法については、「[クラウドサービス設定用フォルダーの構成](../../forms/using/configure-data-sources.md#cloud-folder)」を参照してください。

1. 「**[!UICONTROL 作成]**」をタップして、**[!UICONTROL データソース設定を作成]**&#x200B;ウィザードを開きます。設定の名前と、必要に応じて設定のタイトルを指定し、「**[!UICONTROL サービスタイプ]**」ドロップダウンで「**[!UICONTROL RESTful サービス]**」を選択します。必要な場合は、設定のサムネール画像を選択して「**[!UICONTROL 次へ]**」をタップします。
1. 以下に示す RESTful サービスの詳細情報を指定します。

   * 「Swagger Source」ドロップダウンから「URL」または「File」を選択し、Swagger URL を Swagger 定義ファイルに指定するか、ローカルファイルシステムから Swagger ファイルをアップロードします。
   * Swagger ソースの入力に基づいて、次のフィールドに値が事前入力されます。

      * スキーム：REST API で使用される転送プロトコル。ドロップダウンリストに表示されるスキームタイプの数は、Swagger ソースで定義されているスキームによって異なります。
      * ホスト：REST API を提供するホストのドメイン名または IP アドレス。このフィールドは必須です。
      * 基本パス：すべての API パスの URL プリフィックス。これはオプションのフィールドです。\
         必要に応じて、これらのフィールドの事前入力された値を編集します。
   * RESTful サービスにアクセスするための認証の種類（「なし」、「OAuth2.0」、「基本認証」、「API キー」、「カスタム認証」、「相互認証」）を選択し、それに応じて認証の詳細を指定します。

   認証タイプとして **[!UICONTROL API キー]**&#x200B;を選択した場合は、API キーの値を指定します。API キーは、リクエストヘッダーまたはクエリパラメーターとして送信できます。「**[!UICONTROL 場所]**」ドロップダウンリストから次のオプションの 1 つを選択し、それに応じて「**[!UICONTROL パラメーター名]**」フィールドにヘッダーまたはクエリパラメーターの名前を指定します。

   次を選択した場合、 **[!UICONTROL 相互認証]** 認証タイプについては、 [RESTful Web サービスと SOAP Web サービスの証明書ベースの相互認証](#mutual-authentication).

1. 「**[!UICONTROL 作成]**」をタップして、RESTful サービス用のクラウド設定を作成します。

### パフォーマンスを最適化するためのフォームデータモデル HTTP クライアント設定 {#fdm-http-client-configuration}

[!DNL Experience Manager Forms] フォームデータモデルを使用して、データソースとして RESTful Web サービスとの統合時に、パフォーマンス最適化のための HTTP クライアント設定が含まれています。
フォームデータモデルの HTTP クライアントを設定するには、次の手順を実行します。

1. にログインします。 [!DNL Experience Manager Forms] 管理者としてのオーサーインスタンスの次の場所に移動します。 [!DNL Experience Manager] web コンソールバンドル。 デフォルトの URL は [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).

1. タップ **[!UICONTROL REST データソース用のフォームデータモデル Http クライアント設定]**.

1. 内 [!UICONTROL REST データソース用のフォームデータモデル Http クライアント設定] ダイアログ：

   * フォームデータモデルと、 **[!UICONTROL 接続の制限（合計）]** フィールドに入力します。 デフォルト値は 20 接続です。

   * 内の各ルートに対して許可される最大接続数を指定します **[!UICONTROL ルート単位の接続制限]** フィールドに入力します。 デフォルト値は 2 接続です。

   * 永続的な HTTP 接続が有効に保たれる期間を、 **[!UICONTROL 生き続ける]** フィールドに入力します。 デフォルト値は 15 秒です。

   * 期間を指定します。 [!DNL Experience Manager Forms] サーバは、 **[!UICONTROL 接続タイムアウト]** フィールドに入力します。 デフォルト値は 10 秒です。

   * 内の 2 つのデータパケットの間の無操作状態の最大期間を指定します。 **[!UICONTROL ソケットタイムアウト]** フィールドに入力します。 デフォルト値は 30 秒です。


## SOAP Web サービスの設定 {#configure-soap-web-services}

SOAP ベースの Web サービスは、[Web Services Description Language（WSDL）の仕様](https://www.w3.org/TR/wsdl)に従って記述します。AEM クラウドサービスで SOAP ベースの Web サービスを設定するには、その Web サービスの WSDL URL を確認して、以下の手順を実行します。

1. **[!UICONTROL ツール／Cloud Services／データソース]**&#x200B;に移動します。クラウド設定の作成対象となるフォルダーをタップして選択します。

   クラウドサービス設定用フォルダーの作成方法と構成方法については、「[クラウドサービス設定用フォルダーの構成](../../forms/using/configure-data-sources.md#cloud-folder)」を参照してください。

1. 「**[!UICONTROL 作成]**」をタップして、**[!UICONTROL データソース設定を作成]**&#x200B;ウィザードを開きます。設定の名前と、必要に応じて設定のタイトルを指定し、「**[!UICONTROL サービスタイプ]**」ドロップダウンで「**[!UICONTROL SOAP Web サービス]**」を選択します。必要な場合は、設定のサムネール画像を選択して「**[!UICONTROL 次へ]**」をタップします。
1. 以下に示す SOAP Web サービスの詳細情報を指定します。

   * Web サービスの WSDL URL を指定します。
   * サービスエンドポイント。WSDL で指定されているサービスエンドポイントを上書きするには、このフィールドの値を指定します。
   * SOAP サービスにアクセスするための認証の種類（「なし」、「OAuth2.0」、「基本認証」、「カスタム認証」、「X509 トークン」、「相互認証」）を選択し、認証の詳細を指定します。

      次を選択した場合、 **[!UICONTROL X509 トークン]** 認証の種類として、X509 証明書を設定します。 詳しくは、 [証明書を設定する](install-configure-document-services.md#set-up-certificates-for-reader-extension-and-encryption-service).
X509 証明書のキーストアエイリアスを **[!UICONTROL キーエイリアス]** フィールドに入力します。 認証要求が有効なままになるまでの時間（秒）を **[!UICONTROL 有効期間]** フィールドに入力します。 オプションで、メッセージの本文、タイムスタンプのヘッダー、またはその両方に署名する場合に選択します。

      次を選択した場合、 **[!UICONTROL 相互認証]** 認証タイプについては、 [RESTful Web サービスと SOAP Web サービスの証明書ベースの相互認証](#mutual-authentication).

1. 「**[!UICONTROL 作成]**」をタップして、SOAP Web サービス用のクラウド設定を作成します。

## OData サービスの設定 {#config-odata}

OData サービスは、そのサービスのルート URL によって識別されます。AEM クラウドサービスで OData サービスを設定するには、そのサービスのルート URL を確認して、以下の手順を実行します。

>[!NOTE]
>
> フォームデータモデルがサポートする [OData バージョン 4](https://www.odata.org/documentation/).
>オンライン環境またはオンプレミス環境で Microsoft Dynamics 365 を設定する詳しい手順については、「[Microsoft Dynamics OData 設定](/help/forms/using/ms-dynamics-odata-configuration.md)」を参照してください。

1. **[!UICONTROL ツール／Cloud Services／データソース]**&#x200B;に移動します。クラウド設定の作成対象となるフォルダーをタップして選択します。

   クラウドサービス設定用フォルダーの作成方法と構成方法については、「[クラウドサービス設定用フォルダーの構成](../../forms/using/configure-data-sources.md#cloud-folder)」を参照してください。

1. 「**[!UICONTROL 作成]**」をタップして、**[!UICONTROL データソース設定を作成]**&#x200B;ウィザードを開きます。設定の名前と、必要に応じて設定のタイトルを指定し、「**[!UICONTROL サービスタイプ]**」ドロップダウンで「**[!UICONTROL OData サービス]**」を選択します。必要な場合は、設定のサムネール画像を選択して「**[!UICONTROL 次へ]**」をタップします。
1. 以下に示す OData サービスの詳細情報を指定します。

   * 設定する OData サービスのルート URL を指定します。
   * OData サービスにアクセスするための認証の種類（「なし」、「OAuth2.0」、「基本認証」、「カスタム認証」）を選択し、それに応じて認証の詳細を指定します。

   >[!NOTE]
   >
   >OData エンドポイントをサービスルートとして使用して Microsoft Dynamics サービスに接続する場合は、OAuth 2.0 認証を選択する必要があります。

1. 「**作成**」をタップして、OData サービス用のクラウド設定を作成します。

## RESTful Web サービスと SOAP Web サービスの証明書ベースの相互認証 {#mutual-authentication}

フォームデータモデルの相互認証を有効にすると、フォームデータモデルが実行されているデータソースとAEMサーバーの両方が、データを共有する前に、相互の ID を認証します。 REST および SOAP ベースの接続（データソース）に対して相互認証を使用できます。 AEM Forms環境でフォームデータモデルの相互認証を設定するには、次の手順を実行します。

1. 秘密鍵（証明書）のアップロード先 [!DNL AEM Forms] サーバー。 秘密鍵をアップロードするには：
   1. にログインします。 [!DNL AEM Forms] サーバを管理者として使用する。
   1. に移動します。 **[!UICONTROL ツール]** > **[!UICONTROL セキュリティ]** > **[!UICONTROL ユーザー]**. を選択します。 `fd-cloudservice` ユーザーとタップ **[!UICONTROL プロパティ]**.
   1. を開きます。 **[!UICONTROL キーストア]** タブ、展開 **[!UICONTROL 秘密鍵をキーストアファイルから追加]** 「 」オプションを選択し、「キーストアファイル」をアップロードし、エイリアス、パスワードを指定して、 **[!UICONTROL 送信]**. 証明書がアップロードされます。  秘密鍵のエイリアスは、証明書で言及され、証明書の作成時に設定されます。
1. 信頼証明書をグローバルトラストストアにアップロードします。 証明書をアップロードするには：
   1. に移動します。 **[!UICONTROL ツール]** > **[!UICONTROL セキュリティ]** > **[!UICONTROL トラストストア]**.
   1. を展開します。 **[!UICONTROL CER ファイルから証明書を追加]** オプション、タップ **[!UICONTROL 証明書ファイルを選択]**&#x200B;をクリックし、証明書をアップロードして、 **[!UICONTROL 送信]**.
1. 設定 [SOAP](#configure-soap-web-services) または [RESTful](#configure-restful-web-services) データソースとして web サービスを選択し、 **[!UICONTROL 相互認証]** を認証タイプとして設定します。 複数の自己署名証明書を次のように設定する場合： `fd-cloudservice` ユーザーに証明書のキーエイリアス名を指定します。

## 次の手順 {#next-steps}

上記の手順により、データソースが設定されました。次に、フォームデータモデルを作成します。データソースが設定されていないフォームデータモデルが既に作成されている場合は、上記の手順で設定したデータソースにそのフォームデータモデルを関連付けます。詳しくは、「[フォームデータモデルの作成](/help/forms/using/create-form-data-models.md)」を参照してください。
