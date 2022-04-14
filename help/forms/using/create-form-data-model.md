---
title: '"チュートリアル：フォームデータモデルの作成 "'
seo-title: Create Form Data Model Tutorial
description: フォームデータモデルの作成
seo-description: Create form data model
uuid: b9d2bb1b-90f0-44f4-b1e3-0603cdf5f5b8
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 12e6c325-ace0-4a57-8ed4-6f7ceee23099
docset: aem65
exl-id: 40bc5af6-9023-437e-95b0-f85d3df7d8aa
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '1421'
ht-degree: 100%

---

# チュートリアル：フォームデータモデルの作成 {#tutorial-create-form-data-model}

![04-create-form-data-model-main](assets/04-create-form-data-model-main.png)

これは、「[最初のアダプティブフォームを作成する](../../forms/using/create-your-first-adaptive-form.md)」シリーズを構成するチュートリアルです。チュートリアル内のユースケースを理解して実際に操作できるように、このシリーズのチュートリアルを最初から順に学習することをお勧めします。

## このチュートリアルについて {#about-the-tutorial}

AEM [!DNL Forms] のデータ統合モジュールを使用すると、AEM ユーザープロファイル、RESTful Web サービス、SOAP ベースの web サービス、OData サービス、リレーショナルデータベースなど、バックエンドの様々なデータソースを使用してフォームデータモデルを作成できます。フォームデータモデル内でデータモデルオブジェクトとサービスを設定し、そのフォームデータモデルをアダプティブフォームに関連付けることができます。アダプティブフォームのフィールドは、データモデルオブジェクトのプロパティに連結されます。フォームデータモデル内のサービスを使用して、アダプティブフォームに事前にデータを取り込み、送信されたフォームデータをデータモデルオブジェクトに書き込むことができます。

フォームデータの統合機能とフォームデータモデルについて詳しくは、「[AEM Forms のデータ統合機能](../../forms/using/data-integration.md)」を参照してください。

このチュートリアルでは、フォームデータモデルの準備、作成、設定を行い、そのフォームデータモデルをアダプティブフォームに関連付けるための手順について、順を追って説明します。このチュートリアルを完了すると、次の操作を実行できるようになります。

* [MySQL データベースをデータソースとして設定する](#config-database)
* [MySQL データソースを使用して、フォームデータモデルを作成する](#create-fdm)
* [フォームデータモデルを設定する](#config-fdm)
* [フォームデータモデルのテストを行う](#test-fdm)

フォームデータモデルは、次のように表示されます。

![form-data-model_l](assets/form-data-model_l.png)

**A.** 設定済みのデータソース **B.** データソーススキーマ **C.** 利用可能なサービス **D.** データモデルオブジェクト **E.** 設定済みサービス

## 前提条件 {#prerequisites}

作業を開始する前に、以下の条件が満たされているかどうかを確認してください。

* 「[最初のアダプティブフォームを作成する](../../forms/using/create-your-first-adaptive-form.md)」の「前提条件」セクションの記載に従って、[!DNL MySQL] データベースにサンプルデータが取り込まれていること
* 「[JDBC データベースドライバーのバンドル](/help/sites-developing/jdbc.md#bundling-the-jdbc-database-driver)」の説明に従って、[!DNL MySQL] JDBC ドライバー用の OSGi バンドルが設定されていること
* 最初のチュートリアル「[アダプティブフォームの作成](/help/forms/using/create-adaptive-form.md)」の説明に従って、アダプティブフォームが設定されていること

## 手順 1：MySQL データベースをデータソースとして設定する {#config-database}

各種のデータソースを設定して、フォームデータモデルを作成することができます。このチュートリアルでは、サンプルデータが取り込まれた MySQL データベースの設定を行います。サポートされている他のデータソースとその設定方法については、「[AEM Forms のデータ統合機能](../../forms/using/data-integration.md)」を参照してください。

[!DNL MySQL] データベースを設定するには、次の手順を実行します。

1. [!DNL MySQL] データベース用の JDBC ドライバーを OSGi バンドルとしてインストールします。

   1. AEM [!DNL Forms] のオーサーインスタンスに管理者としてログインし、AEM Web コンソールのバンドルに移動します。デフォルトの URL は、[https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles) です。

   1. 「**[!UICONTROL インストール／アップデート]**」をタップします。「[!UICONTROL バンドルのアップロード／インストール]」ダイアログが表示されます。

   1. 「**[!UICONTROL ファイルを選択]**」をタップし、[!DNL MySQL] JDBC ドライバーの OSGi バンドルを探して選択します。「**[!UICONTROL バンドルを開始]**」と「**[!UICONTROL パッケージを更新]**」を選択して「**[!UICONTROL インストールまたはアップデート]**」をタップします。[!DNL MySQL] の [!DNL Oracle Corporation's] JDBC ドライバーがアクティブになっていることを確認します。ドライバーがインストールされます。

1. [!DNL MySQL] データベースをデータソースとして設定します。

   1. AEM web コンソール（[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)）に移動します。
   1. 「**Apache Sling Connection Pooled DataSource**」という設定を探します。その設定をタップして編集モードで開きます。
   1. 設定ダイアログで、以下の詳細情報を指定します。

      * **Datasource name**：任意のデータソース名を指定します。例えば、「**WeRetailMySQL**」などを指定します。
      * **DataSource service property name**：データソース名を保管するサービスプロパティの名前を指定します。この名前は、データソースインスタンスを OSGi サービスとして登録する際に指定されます。例えば、「**datasource.name**」などを指定します。
      * **JDBC driver class**：JDBC ドライバーの Java クラス名を指定します。[!DNL MySQL] データベースの場合は、**com.mysql.jdbc.Driver**&#x200B;と指定します。
      * **JDBC connection URI**：データベースの接続 URL を指定します。ポート 3306 およびスキーマ weretail で実行される [!DNL MySQL] データベースの場合、URL は `jdbc:mysql://'server':3306/weretail?autoReconnect=true&useUnicode=true&characterEncoding=utf-8` です。
      * **Username**：データベースのユーザー名を指定します。データベースとの接続を確立するには、JDBC ドライバーを有効にする必要があります。
      * **Password**：データベースのパスワードを指定します。データベースとの接続を確立するには、JDBC ドライバーを有効にする必要があります。
      * **Test on Borrow**：「**[!UICONTROL Test on Borrow]**」オプションを有効にします。
      * **Test on Return**：「**[!UICONTROL Test on Return]**」オプションを有効にします。
      * **Validation Query**：プールからの接続状態を確認するための SQL SELECT クエリを指定します。このクエリでは、1 行以上の行が返される必要があります。例えば、「**select * from customerdetails**」などを指定します。
      * **Transaction Isolation**：このオプションの値を「**READ_COMMITTED**」に設定します。

         上記以外のプロパティはデフォルト[値](https://tomcat.apache.org/tomcat-7.0-doc/jdbc-pool.html)のままにして「**[!UICONTROL 保存]**」をタップします。

         以下のような設定が作成されます。

         ![relational-database-data-source-configuration](assets/relational-database-data-source-configuration.png)

## 手順 2：フォームデータモデルを作成する {#create-fdm}

AEM [!DNL Forms] には、設定済みデータソースから[フォームデータモデルを作成](data-integration.md)するための直感的なユーザーインターフェイスが用意されています。1 つのフォームデータモデル内で複数のデータソースを使用することができます。このユースケースでは、既に設定されている [!DNL MySQL] データソースを使用します。

フォームデータモデルを作成するには、以下の手順を実行します。

1. AEM オーサーインスタンスで、**[!UICONTROL フォーム]**／**[!UICONTROL データ統合]**&#x200B;に移動します。
1. **[!UICONTROL 作成]**／**[!UICONTROL フォームデータモデル]**&#x200B;の順にタップします。
1. フォームデータモデル作成ダイアログで、フォームデータモデルの&#x200B;**名前**&#x200B;を指定します。例えば、**customer-shipping-billing-details** などを指定します。「**[!UICONTROL 次へ]**」をタップします。
1. データソース選択画面に、すべての設定済みデータソースが一覧表示されます。「**WeRetailMySQL**」データソースを選択して「**[!UICONTROL 作成]**」をタップします。

   ![data-source-selection](assets/data-source-selection.png)

**customer-shipping-billing-details** というフォームデータモデルが作成されます。

## 手順 3：フォームデータモデルを設定する {#config-fdm}

フォームデータモデルを設定するには、以下の操作を行う必要があります。

* データモデルオブジェクトとサービスを追加する
* データモデルオブジェクト用の読み取りサービスと書き込みサービスを設定する

フォームデータモデルを設定するには、以下の手順を実行します。

1. AEM オーサーインスタンスで、**[!UICONTROL フォーム]**／**[!UICONTROL データ統合]**&#x200B;に移動します。デフォルトの URL は、[https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm](https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm) です。
1. 前の手順で作成した **customer-shipping-billing-details** というフォームデータモデルが表示されます。このフォームデータモデルを編集モードで開きます。

   前の手順で選択した **WeRetailMySQL** というデータソースが、フォームデータモデル内に設定されています。

   ![default-fdm](assets/default-fdm.png)

1. データソースツリーで WeRailMySQL データソースを展開します。**weretail**／**customerdetails** スキーマで、以下のデータモデルオブジェクトをフォームデータモデルに対して選択します。

   * **データモデルオブジェクト**：

      * id
      * name
      * shippingAddress
      * 市区町村
      * ステート
      * zipcode
   * **Services:**

      * get
      * 更新

   「**選択項目を追加**」をタップして、選択したデータモデルオブジェクトとサービスをフォームデータモデルに追加します。

   ![WeRetail スキーマ](assets/weretail_schema_new.png)

   >[!NOTE]
   >
   >JDBC データソースのデフォルトの get サービス、update サービス、insert サービスは、フォームデータモデルでそのまま使用することができます。

1. 以下の手順により、データモデルオブジェクトの読み取りサービスと書き込みサービスを設定します。

   1. 「**customerdetails**」データモデルオブジェクトを選択して「**[!UICONTROL プロパティの編集]**」をタップします。
   1. 「読み取りサービス」ドロップダウンで「**[!UICONTROL get]**」を選択します。customerdetails データモデルオブジェクトのプライマリキーである **id** 引数が自動的に追加されます。タグ ![aem_6_3_edit](assets/aem_6_3_edit.png) をタップして 、次のように引数を設定します。

      ![read-default](assets/read-default.png)

   1. 同様に、書き込みサービスとして「**[!UICONTROL update]**」を選択します。**customerdetails** オブジェクトが引数として自動的に追加されます。この引数を以下のように設定します。

      ![write-default](assets/write-default.png)

      **id** 引数を追加して以下のように設定します。

      ![id-arg](assets/id-arg.png)

   1. 「**[!UICONTROL 完了]**」をタップして、データモデルオブジェクトのプロパティを保存します。  次に「**[!UICONTROL 保存]**」をタップして、フォームデータモデルを保存します。

      **[!UICONTROL get]** サービスと **[!UICONTROL update]** サービスが、データモデルオブジェクトのデフォルトのサービスとして追加されます。

      ![data-model-object](assets/data-model-object.png)

1. 「**[!UICONTROL サービス]**」タブに移動し、**[!UICONTROL get]** サービスと **[!UICONTROL update]** サービスを設定します。

   1. **[!UICONTROL get]** サービスを選択して「**[!UICONTROL プロパティの編集]**」をタップします。プロパティダイアログが開きます。
   1. プロパティを編集ダイアログで、以下のプロパティを指定します。

      * **タイトル**：サービスのタイトルを指定します。例えば、「Retrieve Shipping Address」などを指定します。
      * **説明**：サービスの詳細な機能を示す説明を入力します。次に例を示します。

         このサービスは [!DNL MySQL] データベースから配送先住所などの顧客についての詳細を取得します

      * **出力モデルオブジェクト**：顧客データを保管するスキーマを選択します。次に例を示します。

         customerdetail スキーマ

      * **配列を返す**：「**配列を返す**」オプションを無効にします。
      * **引数**：**ID** という引数を選択します。

      「**[!UICONTROL 完了]**」をタップします。これで、顧客の詳細情報を MySQL データベースから取得するサービスが設定されました。

      ![shiping-address-retrieval](assets/shiiping-address-retrieval.png)

   1. **[!UICONTROL update]** サービスを選択して「**[!UICONTROL プロパティの編集]**」をタップします。プロパティダイアログが開きます。

   1. [!UICONTROL プロパティを編集]ダイアログで、以下を指定します。

      * **タイトル**：サービスのタイトルを指定します。例えば、「Update Shipping Address」などを指定します。
      * **説明**：サービスの詳細な機能を示す説明を入力します。次に例を示します。

         このサービスは、配送先住所とそれに関連するフィールドを MySQL データベース内で更新します

      * **入力モデルオブジェクト**：顧客データを保管するスキーマを選択します。次に例を示します。

         customerdetail スキーマ

      * **出力タイプ**：「**ブール演算式**」を選択します。

      * **引数**：**ID** という引数と **customerdetails** という引数を選択します。
      「**[!UICONTROL 完了]**」をタップします。[!DNL MySQL] データベース内の顧客の詳細情報を更新する **[!UICONTROL update]** サービスが設定されました。

      ![shiping-address-update](assets/shiiping-address-update.png)



これで、フォームデータモデル内のデータモデルオブジェクトとサービスが設定されました。次に、フォームデータモデルのテストを実行します。

## 手順 4：フォームデータモデルのテストを実行する {#test-fdm}

データモデルオブジェクトとサービスをテストすることにより、フォームデータモデルが正しく設定されているかどうかを確認することができます。

テストを実行するには、以下の手順を実行します。

1. 「**[!UICONTROL モデル]**」タブに移動し、**customerdetails** データモデルオブジェクトを選択して「**[!UICONTROL モデルオブジェクトをテスト]**」をタップします。
1. [!UICONTROL モデル／サービスのテスト]ウィンドウの「**[!UICONTROL モデル／サービスを選択]**」ドロップダウンで「**[!UICONTROL モデルオブジェクトを読み込み]**」を選択します。
1. 「**customerdetails**」セクションで、設定済み [!DNL MySQL] データベース内の **id** 引数を指定して「**[!UICONTROL テスト]**」をタップします。

   指定した id 引数に関連付けられている顧客の詳細情報がデータベースから取得され、以下のように **[!UICONTROL Output]** セクションに表示されます。

   ![test-read-model](assets/test-read-model.png)

1. 同様の手順で、書き込みモデルオブジェクトと書き込みサービスをテストします。

   以下の例では、データベース内で 7102715 という ID が設定されている住所情報が、update サービスによって正しく更新されています。

   ![test-write-model](assets/test-write-model.png)

   この状態で、7102715 という ID に対して読み取りモデルサービスのテストをもう一度実行すると、以下のように、更新後の顧客の詳細情報が画面に表示されます。

   ![read-updated](assets/read-updated.png)
