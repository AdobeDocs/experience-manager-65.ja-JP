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
exl-id: 40bc5af6-9023-437e-95b0-f85d3df7d8aa
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1430'
ht-degree: 66%

---

# チュートリアル：フォームデータモデルの作成 {#tutorial-create-form-data-model}

![04-create-form-data-model-main](assets/04-create-form-data-model-main.png)

これは、「[最初のアダプティブフォームを作成する](../../forms/using/create-your-first-adaptive-form.md)」シリーズを構成するチュートリアルです。チュートリアル内のユースケースを理解して実際に操作できるように、このシリーズのチュートリアルを最初から順に学習することをお勧めします。

## このチュートリアルについて  {#about-the-tutorial}

AEM [!DNL Forms]データ統合モジュールを使用すると、AEMユーザープロファイル、RESTful Webサービス、SOAPベースのWebサービス、ODataサービス、リレーショナルデータベースなど、様々なバックエンドデータソースからフォームデータモデルを作成できます。 フォームデータモデル内でデータモデルオブジェクトとサービスを設定し、そのフォームデータモデルをアダプティブフォームに関連付けることができます。アダプティブフォームのフィールドは、データモデルオブジェクトのプロパティに連結されます。フォームデータモデル内のサービスを使用して、アダプティブフォームに事前にデータを取り込み、送信されたフォームデータをデータモデルオブジェクトに書き込むことができます。

フォームデータの統合機能とフォームデータモデルについて詳しくは、「[AEM Forms のデータ統合機能](../../forms/using/data-integration.md)」を参照してください。

このチュートリアルでは、フォームデータモデルの準備、作成、設定を行い、そのフォームデータモデルをアダプティブフォームに関連付けるための手順について、順を追って説明します。このチュートリアルを完了すると、次の操作を実行できるようになります。

* [MySQL データベースをデータソースとして設定する](#config-database)
* [MySQLデータベースを使用してフォームデータモデルを作成する](#create-fdm)
* [フォームデータモデルを設定する](#config-fdm)
* [フォームデータモデルのテストを行う](#test-fdm)

フォームデータモデルは、以下のように表示されます。

![form-data-model_l](assets/form-data-model_l.png)

**A.** 設定済みデータソー **スB.** データソーススキーマ **C.** 使用可能なサービス **D.** データモデルオブジェクト **E.** 設定済みサービス

## 前提条件 {#prerequisites}

作業を開始する前に、以下の条件が満たされているかどうかを確認してください。

* [!DNL MySQL]「[最初のアダプティブフォームを作成する](../../forms/using/create-your-first-adaptive-form.md)」の「前提条件」セクションの記載に従って、 データベースにサンプルデータが取り込まれていること
* [JDBCデータベースドライバのバンドル](/help/sites-developing/jdbc.md#bundling-the-jdbc-database-driver)で説明されている[!DNL MySQL] JDBCドライバ用のOSGiバンドル
* 最初のチュートリアル「[アダプティブフォームの作成](/help/forms/using/create-adaptive-form.md)」で説明されているアダプティブフォーム

## 手順 1：MySQL データベースをデータソースとして設定する {#config-database}

各種のデータソースを設定して、フォームデータモデルを作成することができます。このチュートリアルでは、サンプルデータが取り込まれた MySQL データベースの設定を行います。サポートされている他のデータソースとその設定方法については、「[AEM Forms のデータ統合機能](../../forms/using/data-integration.md)」を参照してください。

[!DNL MySQL]データベースを設定するには、次の手順を実行します。

1. [!DNL MySQL]データベース用のJDBCドライバーをOSGiバンドルとしてインストールします。

   1. AEM [!DNL Forms]オーサーインスタンスに管理者としてログインし、AEM Webコンソールバンドルに移動します。 デフォルトのURLは[https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles)です。

   1. **[!UICONTROL 「インストール/更新]**」をタップします。 「[!UICONTROL Upload / Install Bundles]」ダイアログが表示されます。

   1. 「**[!UICONTROL Choose File]**」をタップし、 JDBC ドライバーの OSGi バンドルを探して選択します。[!DNL MySQL]「**[!UICONTROL Start Bundle]**」と「**[!UICONTROL Refresh Packages]**」を選択し、「**[!UICONTROL Install or Update]**」をタップします。 [!DNL MySQL]の[!DNL Oracle Corporation's] JDBCドライバーがアクティブであることを確認します。 このドライバーは、既にインストールされています。

1. [!DNL MySQL]データベースをデータソースとして設定します。

   1. AEM Webコンソール([https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr))に移動します。
   1. 「**Apache Sling Connection Pooled DataSource**」という設定を探し、その設定をタップして編集モードで開きます。
   1. 設定ダイアログで、以下の詳細情報を指定します。

      * **Datasource name**：任意のデータソース名を指定します。例えば、**WeRetailMySQL**&#x200B;を指定します。
      * **DataSource service property name**：データソース名を保管するサービスプロパティの名前を指定します。この名前は、データソースインスタンスを OSGi サービスとして登録する際に指定されます。例えば、「**datasource.name**」などを指定します。
      * **JDBC driver class**：JDBC ドライバーの Java クラス名を指定します。[!DNL MySQL]データベースの場合は、**com.mysql.jdbc.Driver**&#x200B;を指定します。
      * **JDBC connection URI**：データベースの接続 URL を指定します。ポート3306およびスキーマweretailで実行される[!DNL MySQL]データベースの場合、URLは次のようになります。`jdbc:mysql://'server':3306/weretail?autoReconnect=true&useUnicode=true&characterEncoding=utf-8`
      * **Username**：データベースのユーザー名を指定します。データベースとの接続を確立するには、JDBC ドライバーを有効にする必要があります。
      * **Password**：データベースのパスワードを指定します。データベースとの接続を確立するには、JDBC ドライバーを有効にする必要があります。
      * **借入テスト：** 「借入テスト」オプシ **[!UICONTROL ョンを有効]** にします。
      * **Test on Return:** 「Test on Return」オプショ **[!UICONTROL ンを有効に]** します。
      * **Validation Query**：プールからの接続状態を確認するための SQL SELECT クエリを指定します。このクエリでは、1 行以上の行が返される必要があります。例えば、「**select * from customerdetails**」などを指定します。
      * **Transaction Isolation**：このオプションの値を「**READ_COMMITTED**」に設定します。

         他のプロパティはデフォルトの[値](https://tomcat.apache.org/tomcat-7.0-doc/jdbc-pool.html)のままにし、「**[!UICONTROL 保存]**」をタップします。

         以下のような設定が作成されます。

         ![relational-database-data-source-configuration](assets/relational-database-data-source-configuration.png)

## 手順 2：フォームデータモデルを作成する {#create-fdm}

AEM [!DNL Forms]は、設定済みのデータソースからフォームデータモデル](data-integration.md)を作成するための直感的なユーザーインターフェイスを提供します。 [1 つのフォームデータモデル内で複数のデータソースを使用することができます。このユースケースでは、設定済みの[!DNL MySQL]データソースを使用します。

フォームデータモデルを作成するには、以下の手順を実行します。

1. AEM オーサーインスタンスで、**[!UICONTROL フォーム]**／**[!UICONTROL データ統合]**&#x200B;に移動します。
1. **[!UICONTROL 作成]**／**[!UICONTROL フォームデータモデル]**&#x200B;の順にタップします。
1. フォームデータモデル作成ダイアログで、フォームデータモデルの&#x200B;**名前**&#x200B;を指定します。例えば、「**customer-shipping-billing-details**」などを指定します。「**[!UICONTROL 次へ]**」をタップします。
1. データソース選択画面に、すべての設定済みデータソースが一覧表示されます。**WeRetailMySQL**&#x200B;データソースを選択して「**[!UICONTROL 作成]**」をタップします。

   ![data-source-selection](assets/data-source-selection.png)

**customer-shipping-billing-details**&#x200B;フォームデータモデルが作成されます。

## 手順 3：フォームデータモデルを設定する {#config-fdm}

フォームデータモデルを設定するには、以下の操作を行う必要があります。

* データモデルオブジェクトとサービスの追加
* データモデルオブジェクト用の読み取りサービスと書き込みサービスを設定する

フォームデータモデルを設定するには、以下の手順を実行します。

1. AEMオーサーインスタンスで、**[!UICONTROL Forms]** / **[!UICONTROL データ統合]**&#x200B;に移動します。 デフォルトのURLは[https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm](https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm)です。
1. 先ほど作成した&#x200B;**customer-shipping-billing-details**&#x200B;フォームデータモデルがここに表示されます。 このフォームデータモデルを編集モードで開きます。

   前の手順で選択した **WeRetailMySQL** というデータソースが、フォームデータモデル内に設定されています。

   ![default-fdm](assets/default-fdm.png)

1. データソースツリーで WeRailMySQL データソースを展開します。データモデルを形成するには、 **weretail** > **customerdetails**&#x200B;スキーマから次のデータモデルオブジェクトとサービスを選択します。

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
   >JDBCデータソースのデフォルトのget、update、insertサービスは、フォームデータモデルと共に標準で提供されています。

1. 以下の手順により、データモデルオブジェクトの読み取りサービスと書き込みサービスを設定します。

   1. 「**customerdetails**」データモデルオブジェクトを選択して「**[!UICONTROL プロパティの編集]**」をタップします。
   1. 「読み取りサービス」ドロップダウンで「**[!UICONTROL get]**」を選択します。**id**&#x200B;引数（ customerdetailsデータモデルオブジェクトのプライマリキー）が自動的に追加されます。 ![aem_6_3_edit](assets/aem_6_3_edit.png)をタップし、引数を次のように設定します。

      ![read-default](assets/read-default.png)

   1. 同様に、書き込みサービスとして「**[!UICONTROL update]**」を選択します。**customerdetails** オブジェクトが引数として自動的に追加されます。この引数を以下のように設定します。

      ![write-default](assets/write-default.png)

      **id** 引数を追加して以下のように設定します。

      ![id-arg](assets/id-arg.png)

   1. 「**[!UICONTROL 完了]**」をタップして、データモデルオブジェクトのプロパティを保存します。次に、「**[!UICONTROL 保存]**」をタップして、フォームデータモデルを保存します。

      **[!UICONTROL get]** サービスと **[!UICONTROL update]** サービスが、データモデルオブジェクトのデフォルトのサービスとして追加されます。

      ![data-model-object](assets/data-model-object.png)

1. 「**[!UICONTROL サービス]**」タブに移動し、**[!UICONTROL get]** サービスと **[!UICONTROL update]** サービスを設定します。

   1. **[!UICONTROL get]**&#x200B;サービスを選択し、「**[!UICONTROL プロパティを編集]**」をタップします。 プロパティダイアログが開きます。
   1. プロパティを編集ダイアログで、以下のプロパティを指定します。

      * **タイトル**：サービスのタイトルを指定します。例えば、「Retrieve Shipping Address」などを指定します。
      * **説明**：サービスの詳細な機能を示す説明を入力します。以下に例を示します。

         このサービスは、[!DNL MySQL]データベースから配送先住所とその他の顧客の詳細を取得します

      * **出力モデルオブジェクト**：顧客データを保管するスキーマを選択します。以下に例を示します。

         customerdetailスキーマ

      * **配列を返す**：「**配列を返す**」オプションを無効にします。
      * **引数**：**ID** という引数を選択します。

      「**[!UICONTROL 完了]**」をタップします。これで、顧客の詳細情報を MySQL データベースから取得するサービスが設定されました。

      ![shiping-address-retrieval](assets/shiiping-address-retrieval.png)

   1. **[!UICONTROL update]**&#x200B;サービスを選択し、「**[!UICONTROL プロパティを編集]**」をタップします。 プロパティダイアログが開きます。

   1. [!UICONTROL プロパティを編集]ダイアログで、次の情報を指定します。

      * **タイトル**：サービスのタイトルを指定します。例えば、「Update Shipping Address」などを指定します。
      * **説明**：サービスの詳細な機能を示す説明を入力します。以下に例を示します。

         このサービスは、MySQLデータベースの配送先住所と関連するフィールドを更新します

      * **入力モデルオブジェクト**：顧客データを保管するスキーマを選択します。以下に例を示します。

         customerdetailスキーマ

      * **出力タイプ**：「**ブール演算式**」を選択します。

      * **引数**：**ID** という引数と **customerdetails** という引数を選択します。
      「**[!UICONTROL 完了]**」をタップします。これで、 データベース内の顧客の詳細情報を更新する **[!UICONTROL update]** サービスが設定されました。[!DNL MySQL]

      ![shiping-address-update](assets/shiiping-address-update.png)



これで、フォームデータモデル内のデータモデルオブジェクトとサービスが設定されました。次に、フォームデータモデルのテストを実行します。

## 手順 4：フォームデータモデルのテストを実行する  {#test-fdm}

データモデルオブジェクトとサービスをテストして、フォームデータモデルが正しく設定されていることを確認できます。

テストを実行するには、以下の手順を実行します。

1. 「**[!UICONTROL モデル]**」タブに移動し、**customerdetails** データモデルオブジェクトを選択して「**[!UICONTROL モデルオブジェクトをテスト]**」をタップします。
1. 「[!UICONTROL モデル / サービスのテスト]」ウィンドウの「**[!UICONTROL モデル / サービスを選択]**」ドロップダウンで「**[!UICONTROL モデルオブジェクトを読み込み]**」を選択します。
1. **customerdetails**&#x200B;セクションで、設定した[!DNL MySQL]データベースに存在する&#x200B;**id**&#x200B;引数の値を指定し、**[!UICONTROL Test]**&#x200B;をタップします。

   指定した id 引数に関連付けられている顧客の詳細情報がデータベースから取得され、以下のように「**[!UICONTROL 出力]**」セクションに表示されます。

   ![test-read-model](assets/test-read-model.png)

1. 同様の手順で、書き込みモデルオブジェクトと書き込みサービスをテストします。

   以下の例では、データベース内で 7102715 という ID が設定されている住所情報が、update サービスによって正しく更新されています。

   ![test-write-model](assets/test-write-model.png)

   この状態で、7102715 という ID に対して読み取りモデルサービスのテストをもう一度実行すると、以下のように、更新後の顧客情報が画面に表示されます。

   ![読み取り更新済み](assets/read-updated.png)
