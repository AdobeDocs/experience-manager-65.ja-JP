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
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7

---


# データソースの設定{#configure-data-sources}

![](do-not-localize/data-integeration.png)

AEM Forms のデータ統合機能により、複数の異なるデータソースを設定して接続することができます。以下のタイプがサポートされています。これらのタイプは、すぐに使用することができます。ただし、これらの機能を少しカスタマイズするだけで、他のデータソースを統合することもできます。

* リレーショナルデータベース - MySQL、Microsoft SQL Server、IBM DB2、Oracle RDBMS
* AEM ユーザープロファイル
* RESTful Web サービス
* SOAP ベース Web サービス
* OData サービス

データ統合では、OAuth2.0、基本認証、APIキーの認証タイプがすぐに使用でき、Webサービスにアクセスするためのカスタム認証を実装できます。 RESTful サービス、SOAP ベースサービス、OData サービスは AEM クラウドサービスで設定し、リレーショナルデータベース用の JDBC と AEM ユーザープロファイル用のコネクターは、AEM Web コンソールで設定します。

## リレーショナルデータベースの設定 {#configure-relational-database}

AEM Web Console Configuration を使用してリレーショナルデータベースを設定することができます。以下の操作を実行してください。

1. AEM Webコンソール(https://server:host/system/console/configMgr)に移動します。
1. 「**[!UICONTROL Apache Sling Connection Pooled DataSource]**」という設定を探し、その設定をタップして編集モードで開きます。
1. 設定ダイアログで、設定するデータベースの詳細を指定します。例えば、以下のような詳細を指定します。

   * データソースの名前
   * データソース名が保管されるデータソースサービスプロパティ
   * JDBC ドライバーの Java クラス名
   * JDBC 接続 URI
   * JDBC ドライバーとの接続を確立するためのユーザー名とパスワード
   >[!NOTE] {graybox=&quot;true&quot;}
   >
   >データソースを設定する前に、パスワードなどの機密情報を必ず暗号化してください。暗号化するには、以下の手順を実行します。
   >
   >    
   >    
   >    1. Go to https://&#39;[server]:[port]&#39;/system/console/crypto.
   >    1. 「**[!UICONTROL プレーンテキスト]**」フィールドに暗号化する文字列（パスワードなど）を入力して「**[!UICONTROL 保護]**」をクリックします。
   >    
   >    
   >    
   >暗号化されたテキストは、設定で指定できる「保護されたテキスト」フィールドに表示されます。

1. プールからオブジェクトを取得するときにそのオブジェクトを検証する場合は「**[!UICONTROL Test on Borrow]**」を有効にし、プールにオブジェクトを返すときにそのオブジェクトを検証する場合は「**[!UICONTROL Test on Return]**」を有効にします。
1. 「**[!UICONTROL 検証クエリ]**」フィールドで SQL SELECT クエリを指定して、プールからの接続を検証します。このクエリでは、1 行以上の行が返される必要があります。使用しているデータベースに応じて、以下のいずれかを指定します。

   * SELECT 1 （MySQLおよびMS SQL）
   * SELECT 1 from dual（Oracle の場合）

1. Tap **[!UICONTROL Save]** to save the configuration.

## AEM ユーザープロファイルの設定 {#configure-aem-user-profile}

AEM Web コンソールでユーザープロファイルコネクター設定を使用して、AEM のユーザープロファイルを設定することができます。以下の操作を実行してください。

1. Go to AEM web console at https://&#39;[server]:[port]&#39;system/console/configMgr.
1. Look for **[!UICONTROL AEM Forms Data Integrations - User Profile Connector Configuration]** and tap to open the configuration in edit mode.
1. ユーザープロファイルコネクター設定ダイアログで、ユーザープロファイルプロパティの追加、削除、更新を行うことができます。ここで指定したプロパティは、フォームデータモデルで使用することができます。次の形式を使用して、ユーザープロファイルのプロパティを指定します。

   `name=[property_name_with_location_in_user_profile],type=[property_type]`

   例：

   * `name=profile/phoneNumber,type=string`
   * `name=profile/empLocation/*/city,type=string`
   >[!NOTE] {graybox=&quot;true&quot;}
   >
   >The ***** in the above example denotes all nodes under the `profile/empLocation/` node in AEM user profile in CRXDE structure. It means that the form data model can access the `city` property of type `string` present in any node under the `profile/empLocation/` node. ただし、指定されたプロパティが存在するノードの構造が統一されている必要があります。

1. Tap **[!UICONTROL Save]** to save the configuration.

## クラウドサービス設定用フォルダーの構成 {#cloud-folder}

>[!NOTE]
RESTful、SOAPおよびODataサービス用のクラウドサービスを設定するには、クラウドサービスフォルダーの設定が必要です。

All cloud service configurations in AEM are consolidated in the `/conf` folder in AEM repository. デフォルトの場合、`conf` フォルダーには `global` フォルダーが含まれています。このフォルダーで、クラウドサービスの設定を作成することができます。ただし、このフォルダーを手動でクラウド設定用に有効にする必要があります。追加のフォルダーを `conf` フォルダー内に作成して、クラウドサービスの作成と編集を行うこともできます。

クラウドサービス設定用のフォルダーを構成するには、以下の手順を実行します。

1. Go to **[!UICONTROL Tools > General > Configuration Browser]**.
1. 以下の手順を実行して、global フォルダーをクラウド設定用に有効にします。クラウドサービス設定用に別のフォルダーを作成する場合は、この手順をスキップしてください。

   1. **[!UICONTROL 設定ブラウザー]**&#x200B;で、「`global`」フォルダーを選択して「**[!UICONTROL プロパティ]**」をタップします。

   1. **[!UICONTROL 設定プロパティ]**&#x200B;ダイアログで、「**[!UICONTROL クラウド設定]**」を有効にします。

   1. 「**[!UICONTROL 保存して閉じる]**」をタップして設定内容を保存し、ダイアログを閉じます。

1. **[!UICONTROL 設定ブラウザー]**&#x200B;で「**[!UICONTROL 作成]**」をタップします。
1. **[!UICONTROL 設定を作成]**&#x200B;ダイアログでフォルダーのタイトルを指定し、「**[!UICONTROL クラウド設定]**」を有効にします。
1. Tap **[!UICONTROL Create]** to create the folder enabled for cloud service configurations.

## RESTful Web サービスの設定 {#configure-restful-web-services}

RESTful web service can be described using [Swagger specifications](https://swagger.io/specification/) in JSON or YAML format in a Swagger definition file. AEMクラウドサービスでRESTful Webサービスを設定するには、ファイルシステムにSwaggerファイルが存在するか、ファイルがホストされているURLが存在することを確認します。

RESTful サービスを設定するには、以下の手順を実行します。

1. **[!UICONTROL ツール／クラウドサービス／データソース]**&#x200B;に移動します。クラウド設定を作成するフォルダーをタップして選択します。

   See [Configure folder for cloud service configurations](../../forms/using/configure-data-sources.md#cloud-folder) for information about creating and configuring a folder for cloud service configurations.

1. Tap **[!UICONTROL Create]** to open the **[!UICONTROL Create Data Source Configuration wizard]**. 設定の名前と、必要に応じて設定のタイトルを指定し、「**[!UICONTROL サービスタイプ]**」ドロップダウンで「**[!UICONTROL RESTful サービス]**」を選択します。必要な場合は、設定のサムネイル画像を選択して「**[!UICONTROL 次へ]**」をタップします。
1. 以下に示す RESTful サービスの詳細情報を指定します。

   * 「Swaggerソース」ドロップダウンから「URL」または「ファイル」を選択し、それに応じてSwagger URLをSwagger定義ファイルに指定するか、ローカルファイルシステムからSwaggerファイルをアップロードします。
   * Swaggerソースの入力に基づいて、次のフィールドに値が事前入力されます。

      * スキーム：REST APIで使用される転送プロトコルです。 ドロップダウンリストに表示されるスキームの種類の数は、Swaggerソースで定義されているスキームによって異なります。
      * ホスト：REST APIを提供するホストのドメイン名またはIPアドレス。 このフィールドは必須です。
      * ベースパス：すべてのAPIパスのURLプレフィックス。 これはオプションのフィールドです。\
         必要に応じて、これらのフィールドの事前入力値を編集します。
   * 認証タイプの選択 — なし、OAuth2.0、基本認証、APIキー、またはカスタム認証 — を使用してRESTfulサービスにアクセスし、認証の詳細を指定します。
   認証タイプとして **[!UICONTROL APIキー]** を選択する場合は、APIキーの値を指定します。 APIキーは、リクエストヘッダーまたはパラメーターとしてクエリできます。 「場所」ドロップダウンリストから **[!UICONTROL 、次のいずれかのオプションを選択し、「クエリ名」フィールドにヘッダーの名前またはパラメーターのパラ]** メーターを指定します **** 。

1. 「**[!UICONTROL 作成]**」をタップして、RESTful サービス用のクラウド設定を作成します。

## SOAP Web サービスの設定 {#configure-soap-web-services}

SOAP ベースの Web サービスは、[Web Services Description Language（WSDL）の仕様](https://www.w3.org/TR/wsdl)に従って記述します。AEM クラウドサービスで SOAP ベースの Web サービスを設定するには、その Web サービスの WSDL URL を確認して、以下の手順を実行します。

1. **[!UICONTROL ツール／クラウドサービス／データソース]**&#x200B;に移動します。クラウド設定を作成するフォルダーをタップして選択します。

   See [Configure folder for cloud service configurations](../../forms/using/configure-data-sources.md#cloud-folder) for information about creating and configuring a folder for cloud service configurations.

1. Tap **[!UICONTROL Create]** to open the **[!UICONTROL Create Data Source Configuration wizard]**. 設定の名前と、必要に応じて設定のタイトルを指定し、「**[!UICONTROL サービスタイプ]**」ドロップダウンで「**[!UICONTROL SOAP Web サービス]**」を選択します。必要な場合は、設定のサムネイル画像を選択して「**[!UICONTROL 次へ]**」をタップします。
1. 以下に示す SOAP Web サービスの詳細情報を指定します。

   * Web サービスの WSDL URL を指定します。
   * サービスエンドポイント. WSDLで指定されているサービスエンドポイントを上書きするには、このフィールドの値を指定します。
   * 認証タイプの選択 — なし、OAuth2.0、基本認証、またはカスタム認証 — SOAPサービスにアクセスし、認証の詳細を指定します。

1. 「**[!UICONTROL 作成]**」をタップして、SOAP Web サービス用のクラウド設定を作成します。

## OData サービスの設定 {#config-odata}

OData サービスは、そのサービスのルート URL によって識別されます。AEM クラウドサービスで OData サービスを設定するには、そのサービスのルート URL を確認して、以下の手順を実行します。

>[!NOTE]
オンライン環境またはオンプレミス環境で Microsoft Dynamics 365 を設定する詳しい手順については、「[Microsoft Dynamics OData 設定](/help/forms/using/ms-dynamics-odata-configuration.md)」を参照してください。

1. **[!UICONTROL ツール／クラウドサービス／データソース]**&#x200B;に移動します。クラウド設定を作成するフォルダーをタップして選択します。

   See [Configure folder for cloud service configurations](../../forms/using/configure-data-sources.md#cloud-folder) for information about creating and configuring a folder for cloud service configurations.

1. Tap **[!UICONTROL Create]** to open the **[!UICONTROL Create Data Source Configuration wizard]**. 設定の名前と、必要に応じて設定のタイトルを指定し、「**[!UICONTROL サービスタイプ]**」ドロップダウンで「**[!UICONTROL OData サービス]**」を選択します。必要な場合は、設定のサムネイル画像を選択して「**[!UICONTROL 次へ]**」をタップします。
1. 以下に示す OData サービスの詳細情報を指定します。

   * 設定する OData サービスのルート URL を指定します。
   * 認証タイプの選択 — なし、OAuth2.0、基本認証、またはカスタム認証 — を使用してODataサービスにアクセスし、それに従って認証の詳細を提供します。
   >[!NOTE]
   OData エンドポイントをサービスルートとして使用して Microsoft Dynamics サービスに接続する場合は、OAuth 2.0 認証を選択する必要があります。

1. Tap **Create** to create the cloud configuration for the OData service.

## 次の手順 {#next-steps}

上記の手順により、データソースが設定されました。次に、フォームデータモデルを作成します。データソースが設定されていないフォームデータモデルが既に作成されている場合は、上記の手順で設定したデータソースにそのフォームデータモデルを関連付けます。See [Create form data model](/help/forms/using/create-form-data-models.md) for details.
