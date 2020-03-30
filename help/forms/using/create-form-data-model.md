---
title: '"チュートリアル：フォームデータモデルの作成 "'
seo-title: フォームデータモデルの作成チュートリアル
description: フォームデータモデルの作成
seo-description: フォームデータモデルの作成
uuid: b9d2bb1b-90f0-44f4-b1e3-0603cdf5f5b8
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 12e6c325-ace0-4a57-8ed4-6f7ceee23099
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# チュートリアル：フォームデータモデルの作成 {#tutorial-create-form-data-model}

![04-create-form-data-model-main](assets/04-create-form-data-model-main.png)

これは、「[最初のアダプティブフォームを作成する](../../forms/using/create-your-first-adaptive-form.md)」シリーズを構成するチュートリアルです。チュートリアル内のユースケースを理解して実際に操作できるように、このシリーズのチュートリアルを最初から順に学習することをお勧めします。

## このチュートリアルについて {#about-the-tutorial}

AEM Formsデータ統合モジュールを使用すると、AEMユーザープロファイル、RESTful Webサービス、SOAPベースのWebサービス、ODataサービス、リレーショナルデータベースなど、異なるバックエンドデータソースからフォームデータモデルを作成できます。 フォームデータモデル内でデータモデルオブジェクトとサービスを設定し、そのフォームデータモデルをアダプティブフォームに関連付けることができます。アダプティブフォームのフィールドは、データモデルオブジェクトのプロパティに連結されます。フォームデータモデル内のサービスを使用して、アダプティブフォームに事前にデータを取り込み、送信されたフォームデータをデータモデルオブジェクトに書き込むことができます。

フォームデータの統合機能とフォームデータモデルについて詳しくは、「[AEM Forms のデータ統合機能](../../forms/using/data-integration.md)」を参照してください。

このチュートリアルでは、フォームデータモデルの準備、作成、設定を行い、そのフォームデータモデルをアダプティブフォームに関連付けるための手順について、順を追って説明します。このチュートリアルを完了すると、次の操作を実行できるようになります。

* [MySQL データベースをデータソースとして設定する](#config-database)
* [MySQLデータベースを使用したフォームデータモデルの作成](#create-fdm)
* [フォームデータモデルを設定する](#config-fdm)
* [フォームデータモデルのテストを行う](#test-fdm)

フォームデータモデルは、以下のように表示されます。

![form-data-model_l](assets/form-data-model_l.png)

**A.** 設定済みのデータソ **ースB。** データソースのスキーマ **C.** 利用可能なサー **ビスD.** データモデルのオブジェ **クトE.** 設定済みのサービス

## 前提条件 {#prerequisites}

作業を開始する前に、以下の条件が満たされているかどうかを確認してください。

* 「[最初のアダプティブフォームを作成する](../../forms/using/create-your-first-adaptive-form.md)」の「前提条件」セクションの記載に従って、MySQL データベースにサンプルデータが取り込まれていること
* OSGi bundle for MySQL JDBC driver as explained in [Bundling the JDBC Database Driver](/help/sites-developing/jdbc.md#bundling-the-jdbc-database-driver)
* Adaptive form as explained in the first tutorial [Create an adaptive form](/help/forms/using/create-adaptive-form.md)

## 手順 1：MySQL データベースをデータソースとして設定する {#config-database}

各種のデータソースを設定して、フォームデータモデルを作成することができます。このチュートリアルでは、サンプルデータが取り込まれた MySQL データベースの設定を行います。サポートされている他のデータソースとその設定方法については、「[AEM Forms のデータ統合機能](../../forms/using/data-integration.md)」を参照してください。

MySQL データベースを設定するには、以下の手順を実行します。

1. MySQLデータベース用のJDBCドライバーをOSGiバンドルとしてインストールします。

   1. AEM Forms のオーサーインスタンスに管理者としてログインし、AEM Web コンソールバンドルに移動します。The default URL is [https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles).

   1. Tap **Install/Update**. 「**Upload / Install Bundles**」ダイアログが表示されます。

   1. 「**Choose File**」をタップし、MySQL JDBC ドライバーの OSGi バンドルを探して選択します。Select **Start Bundle** and **Refresh Packages**, and tap **Install or Update**. Oracle が提供する MySQL の JDBC ドライバーがアクティブになっていることを確認します。このドライバーは、既にインストールされています。

1. 以下の手順により、MySQL データベースをデータソースとして設定します。

   1. Go to AEM web console at [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
   1. 「**Apache Sling Connection Pooled DataSource**」という設定を探し、その設定をタップして編集モードで開きます。
   1. 設定ダイアログで、以下の詳細情報を指定します。

      * **Datasource name**：任意のデータソース名を指定します。For example, specify **WeRetailMySQL**.
      * **DataSource service property name**：データソース名を保管するサービスプロパティの名前を指定します。この名前は、データソースインスタンスを OSGi サービスとして登録する際に指定されます。例えば、「**datasource.name**」などを指定します。
      * **JDBC driver class**：JDBC ドライバーの Java クラス名を指定します。For MySQL database, specify **com.mysql.jdbc.Driver**.
      * **JDBC connection URI**：データベースの接続 URL を指定します。For MySQL database running on port 3306 and schema weretail, the URL is: `jdbc:mysql://'server':3306/weretail?autoReconnect=true&useUnicode=true&characterEncoding=utf-8`
      * **Username**：データベースのユーザー名を指定します。データベースとの接続を確立するには、JDBC ドライバーを有効にする必要があります。
      * **Password**：データベースのパスワードを指定します。データベースとの接続を確立するには、JDBC ドライバーを有効にする必要があります。
      * **借用時のテスト：** [借用時にテ **スト]オプションを有効** にします。
      * **リターン時のテスト：** 「リターン時にテ **スト」オプションを有効** にします。
      * **Validation Query**：プールからの接続状態を確認するための SQL SELECT クエリを指定します。このクエリでは、1 行以上の行が返される必要があります。例えば、「**select * from customerdetails**」などを指定します。
      * **Transaction Isolation**：このオプションの値を「**READ_COMMITTED**」に設定します。
      Leave other properties with default [values](https://tomcat.apache.org/tomcat-7.0-doc/jdbc-pool.html) and tap **Save**.
   以下のような設定が作成されます。

   ![relational-database-data-source-configuration](assets/relational-database-data-source-configuration.png)

## 手順 2：フォームデータモデルを作成する {#create-fdm}

AEM Forms には、設定済みデータソースを使用して[フォームデータモデルを作成](../../forms/using/data-integration.md#main-pars-header-1524967585)するための直感的なユーザーインターフェイスが用意されています。1 つのフォームデータモデル内で複数のデータソースを使用することができます。このユースケースでは、既に設定されている MySQL データソースを使用します。

フォームデータモデルを作成するには、以下の手順を実行します。

1. In AEM author instance, navigate to **Forms** > **Data Integrations**.
1. Tap **Create** > **Form Data Model**.
1. フォームデータモデル作成ダイアログで、フォームデータモデルの&#x200B;**名前**&#x200B;を指定します。例えば、「**customer-shipping-billing-details**」などを指定します。「**次へ**」をタップします。
1. データソース選択画面に、すべての設定済みデータソースが一覧表示されます。Select **WeRetailMySQL** data source and tap **Create**.

   ![データソースの選択](assets/data-source-selection.png)

The **customer-shipping-billing-details** form data model is created.

## 手順 3：フォームデータモデルを設定する {#config-fdm}

フォームデータモデルを設定するには、以下の操作を行う必要があります。

* データモデルのオブジェクトおよびサービスの追加
* データモデルオブジェクト用の読み取りサービスと書き込みサービスを設定する

フォームデータモデルを設定するには、以下の手順を実行します。

1. On AEM author instance, navigate to **Forms** > **Data Integrations**. The default URL is [https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm](https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm).
1. The **customer-shipping-billing-details** form data model you created earlier is listed here. このフォームデータモデルを編集モードで開きます。

   前の手順で選択した **WeRetailMySQL** というデータソースが、フォームデータモデル内に設定されています。

   ![デフォルトFDM](assets/default-fdm.png)

1. データソースツリーで WeRailMySQL データソースを展開します。Select the following data model objects and services from **weretail** > **customerdetails** schema to form data model:

   * **データモデルオブジェクト**:

      * id
      * name
      * shippingAddress
      * 市区町村
      * state
      * zipcode
   * **Services:**

      * get
      * 更新
   「**選択項目を追加**」をタップして、選択したデータモデルオブジェクトとサービスをフォームデータモデルに追加します。

   ![WeRetailスキーマ](assets/weretail_schema_new.png)

   >[!NOTE]
   >
   >JDBCデータソースのデフォルトのget、updateおよびinsertサービスは、フォームデータモデルと共に、そのまま使用できます。

1. 以下の手順により、データモデルオブジェクトの読み取りサービスと書き込みサービスを設定します。

   1. 「**customerdetails**」データモデルオブジェクトを選択して「**プロパティの編集**」をタップします。
   1. 「読み取りサービス」ドロップダウンで「**get**」を選択します。**id引数は** 、customerdetailsデータモデルオブジェクトの主キーです。 aem_6_3 ![_editをタップし](assets/aem_6_3_edit.png) 、次のように引数を設定します。

      ![読み取りデフォルト](assets/read-default.png)

   1. 同様に、書き込みサービスとして「**update**」を選択します。**customerdetails** オブジェクトが引数として自動的に追加されます。この引数を以下のように設定します。

      ![書き込みデフォルト](assets/write-default.png)

      **id** 引数を追加して以下のように設定します。

      ![id-arg](assets/id-arg.png)

   1. 「**完了**」をタップして、データモデルオブジェクトのプロパティを保存します。Then, tap **Save** to save the form data model.

      **get** サービスと **update** サービスが、データモデルオブジェクトのデフォルトのサービスとして追加されます。

      ![data-model-object](assets/data-model-object.png)

1. 「**サービス**」タブに移動し、**get** サービスと **update** サービスを設定します。

   1. Select the **get** service and tap **Edit Properties**. プロパティダイアログが開きます。
   1. プロパティを編集ダイアログで、以下のプロパティを指定します。

      * **タイトル**：サービスのタイトルを指定します。例えば、「Retrieve Shipping Address」などを指定します。
      * **説明**：サービスの詳細な機能を示す説明を入力します。次に例を示します。

         このサービスは、MySQLデータベースから配送先住所とその他の顧客の詳細を取得します

      * **出力モデルオブジェクト**：顧客データを保管するスキーマを選択します。次に例を示します。

         顧客詳細スキーマ

      * **配列を返す**：「**配列を返す**」オプションを無効にします。
      * **引数**：**ID** という引数を選択します。
      「**Done**」をタップします。これで、顧客の詳細情報を MySQL データベースから取得するサービスが設定されました。

      ![シピングアドレス検索](assets/shiiping-address-retrieval.png)

   1. Select the **update** service and tap **Edit Properties**. プロパティダイアログが開きます。

   1. プロパティを編集ダイアログで、以下のプロパティを指定します。

      * **タイトル**：サービスのタイトルを指定します。例えば、「Update Shipping Address」などを指定します。
      * **説明**：サービスの詳細な機能を示す説明を入力します。次に例を示します。

         このサービスは、MySQLデータベースの配送先住所と関連フィールドを更新します

      * **入力モデルオブジェクト**：顧客データを保管するスキーマを選択します。次に例を示します。

         顧客詳細スキーマ

      * **出力タイプ**：「**ブール演算式**」を選択します。

      * **引数**：**ID** という引数と **customerdetails** という引数を選択します。
      「**Done**」をタップします。これで、MySQL データベース内の顧客の詳細情報を更新する **update** サービスが設定されました。

      ![shiping-address-update](assets/shiiping-address-update.png)



これで、フォームデータモデル内のデータモデルオブジェクトとサービスが設定されました。次に、フォームデータモデルのテストを実行します。

## 手順 4：フォームデータモデルのテストを実行する {#test-fdm}

データモデルのオブジェクトおよびサービスをテストして、フォームデータモデルが正しく設定されていることを確認できます。

テストを実行するには、以下の手順を実行します。

1. 「**モデル**」タブに移動し、**customerdetails** データモデルオブジェクトを選択して「**モデルオブジェクトをテスト**」をタップします。
1. 「**モデル / サービスのテスト**」ウィンドウの「**モデル / サービスを選択**」ドロップダウンで「**モデルオブジェクトを読み込み**」を選択します。
1. 「**customerdetails**」セクションで、設定済み MySQL データベース内の **id** 引数を指定して「**テスト**」をタップします。

   指定した id 引数に関連付けられている顧客の詳細情報がデータベースから取得され、以下のように「**出力**」セクションに表示されます。

   ![test-read-model](assets/test-read-model.png)

1. 同様の手順で、書き込みモデルオブジェクトと書き込みサービスをテストします。

   以下の例では、データベース内で 7102715 という ID が設定されている住所情報が、update サービスによって正しく更新されています。

   ![テスト・ライト・モデル](assets/test-write-model.png)

   この状態で、7102715 という ID に対して読み取りモデルサービスのテストをもう一度実行すると、以下のように、更新後の顧客情報が画面に表示されます。

   ![読み取り更新された](assets/read-updated.png)
