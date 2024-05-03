---
title: "チュートリアル：フォームデータモデルの作成 "
description: MySQL をデータソースとして設定する方法、フォームデータモデル（FDM）を作成して設定する方法、MySQL を AEM Forms 用にテストする方法について説明します。
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.3/FORMS
docset: aem65
exl-id: 40bc5af6-9023-437e-95b0-f85d3df7d8aa
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1533'
ht-degree: 100%

---

# チュートリアル：フォームデータモデルの作成 {#tutorial-create-form-data-model}

![04-create-form-data-model-main](assets/04-create-form-data-model-main.png)

これは、[最初のアダプティブフォームを作成する](../../forms/using/create-your-first-adaptive-form.md)シリーズを構成するチュートリアルです。チュートリアル内のユースケースを理解して実際に操作できるように、このシリーズのチュートリアルを最初から順に学習することをお勧めします。

## チュートリアルについて {#about-the-tutorial}

AEM [!DNL Forms] のデータ統合モジュールを使用すると、AEM ユーザープロファイル、RESTful web サービス、SOAP ベースの web サービス、OData サービス、リレーショナルデータベースなど、バックエンドの様々なデータソースからフォームデータモデルを作成できます。フォームデータモデル内でデータモデルオブジェクトおよびサービスを設定し、アダプティブフォームに関連付けることができます。アダプティブフォームのフィールドは、データモデルオブジェクトのプロパティに連結されます。このサービスを使用すると、アダプティブフォームに事前に入力し、送信されたフォームデータをデータモデルオブジェクトに書き込むことができます。

フォームデータの統合機能とフォームデータモデルについて詳しくは、「[AEM Forms のデータ統合機能](../../forms/using/data-integration.md)」を参照してください。

このチュートリアルでは、フォームデータモデルの準備、作成、設定およびアダプティブフォームとの関連付けの手順について説明します。このチュートリアルを完了すると、次の操作を実行できるようになります。

* [MySQL データベースをデータソースとして設定する](#config-database)
* [MySQL データソースを使用して、フォームデータモデルを作成する](#create-fdm)
* [フォームデータモデルを設定する](#config-fdm)
* [フォームデータモデルのテストを行う](#test-fdm)

フォームデータモデルは、次のように表示されます。

![form-data-model_l](assets/form-data-model_l.png)

**A.** 設定済みのデータソース **B.** データソーススキーマ **C.** 利用可能なサービス **D.** データモデルオブジェクト **E.** 設定済みサービス

## 前提条件 {#prerequisites}

開始する前に、次の点を確認してください。

* 「[最初のアダプティブフォームを作成する](../../forms/using/create-your-first-adaptive-form.md)」の「前提条件」セクションの記載に従って、[!DNL MySQL] データベースにサンプルデータが取り込まれていること
* 「[JDBC データベースドライバーのバンドル](/help/sites-developing/jdbc.md#bundling-the-jdbc-database-driver)」の説明に従って、[!DNL MySQL] JDBC ドライバー用の OSGi バンドルが設定されていること
* 最初のチュートリアル「[アダプティブフォームの作成](/help/forms/using/create-adaptive-form.md)」の説明に従って、アダプティブフォームが設定されていること

## 手順 1：MySQL データベースをデータソースとして設定する {#config-database}

様々なタイプのデータソースを設定して、フォームデータモデルを作成できます。このチュートリアルでは、サンプルデータが取り込まれた MySQL データベースを設定します。その他のサポート対象データソースとその設定方法について詳しくは、[AEM Forms データ統合](../../forms/using/data-integration.md)を参照してください。

[!DNL MySQL] データベースを設定するには、次の手順を実行します。

1. [!DNL MySQL] データベース用の JDBC ドライバーを OSGi バンドルとしてインストールします。

   1. [!DNL MySQL] JDBC ドライバー OSGi バンドルを `http://www.java2s.com/ref/jar/download-orgosgiservicejdbc100jar-file.html` からダウンロードします。<!-- This URL is an insecure link but using https is not possible -->
   1. AEM [!DNL Forms] のオーサーインスタンスに管理者としてログインし、AEM Web コンソールのバンドルに移動します。デフォルトの URL は、[https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles) です。

   1. 「**[!UICONTROL Install/Update]**」を選択します。「[!UICONTROL Upload / Install Bundles]」ダイアログが表示されます。

   1. 「**[!UICONTROL Choose File]**」を選択し、[!DNL MySQL] JDBC ドライバーの OSGi バンドルを探して選択します。「**[!UICONTROL Start Bundle]**」と「**[!UICONTROL Refresh Packages]**」を選択して「**[!UICONTROL Install or Update]**」を選択します。[!DNL MySQL] の [!DNL Oracle Corporation's] JDBC ドライバーがアクティブになっていることを確認します。ドライバーがインストールされます。

1. [!DNL MySQL] データベースをデータソースとして設定します。

   1. AEM web コンソール（[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)）に移動します。
   1. 「**Apache Sling Connection Pooled DataSource**」という設定を探し、その設定を選択して編集モードで開きます。
   1. 設定ダイアログで、次の詳細を指定します。

      * **データソース名：**&#x200B;任意の名前を指定できます。例えば、「**WeRetailMySQL**」などを指定します。
      * **DataSource サービスのプロパティ名**：DataSource 名を含むサービスプロパティの名前を指定します。データソースインスタンスを OSGi サービスとして登録する際に指定されます。例えば、**datasource.name** です。
      * **JDBC ドライバークラス**：JDBC ドライバーの Java™ クラス名を指定します。[!DNL MySQL] データベースの場合は、**com.mysql.jdbc.Driver**&#x200B;と指定します。
      * **JDBC connection URI**：データベースの接続 URL を指定します。ポート 3306 およびスキーマ `weretail` で実行される [!DNL MySQL] データベースの場合、URL は `jdbc:mysql://'server':3306/weretail?autoReconnect=true&useUnicode=true&characterEncoding=utf-8` です。

      >[!NOTE]
      >
      > [!DNL MySQL] データベースがファイアウォールの内側にある場合、データベースホスト名はパブリック DNS ではありません。データベースの IP アドレスを AEM ホストマシンの */etc/hosts* ファイルに追加する必要があります。

      * **Username**：データベースのユーザー名を指定します。データベースとの接続を確立するには、JDBC ドライバーを有効にする必要があります。
      * **Password**：データベースのパスワードを指定します。データベースとの接続を確立するには、JDBC ドライバーを有効にする必要があります。

      >[!NOTE]
      >
      >AEM Forms は、[!DNL MySQL] の NT 認証をサポートしていません。[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr) で AEM web コンソールに移動し、「Apache Sling Connection Pooled Datasource」を検索します。「JDBC 接続 URI」プロパティでは、「integratedSecurity」の値を False に設定し、作成したユーザー名とパスワードを使用して [!DNL MySQL] データベースに接続します。

      * **Test on Borrow：** は **[!UICONTROL Test on Borrow]** オプションを有効にします。
      * **Test on Return：** は **[!UICONTROL Test on Return]** オプションを有効にします。
      * **検証クエリ：**&#x200B;プールからの接続を検証する SQL SELECT クエリを指定します。クエリは、1 行以上の行を返す必要があります。例えば、**customerdetails から &#42; を選択します**。
      * **Transaction Isolation**：このオプションの値を「**READ_COMMITTED**」に設定します。

        上記以外のプロパティはデフォルト[値](https://tomcat.apache.org/tomcat-7.0-doc/jdbc-pool.html)のままにして「**[!UICONTROL Save]**」を選択します。

        以下のような設定が作成されます。

        ![relational-database-data-source-configuration](assets/relational-database-data-source-configuration.png)

## 手順 2：フォームデータモデルを作成する {#create-fdm}

AEM [!DNL Forms] には、設定済みデータソースから[フォームデータモデルを作成](data-integration.md)するための直感的なユーザーインターフェイスが用意されています。1 つのフォームデータモデル内で複数のデータソースを使用することができます。このユースケースでは、既に設定されている [!DNL MySQL] データソースを使用できます。

フォームデータモデルを作成するには、以下の手順を実行します。

1. AEM オーサーインスタンスで、**[!UICONTROL フォーム]**／**[!UICONTROL データ統合]**&#x200B;に移動します。
1. 「**[!UICONTROL 作成]**／**[!UICONTROL フォームデータモデル]**」を選択します。
1. フォームデータモデル作成ダイアログで、フォームデータモデルの&#x200B;**名前**&#x200B;を指定します。例えば、**customer-shipping-billing-details** などを指定します。「**[!UICONTROL 次へ]**」を選択します。
1. データソース選択画面に、すべての設定済みデータソースが一覧表示されます。「**WeRetailMySQL**」データソースを選択して「**[!UICONTROL 作成]**」を選択します。

   ![data-source-selection](assets/data-source-selection.png)

**customer-shipping-billing-details** というフォームデータモデルが作成されます。

## 手順 3：フォームデータモデルを設定する {#config-fdm}

フォームデータモデルを設定するには、次の操作を行います。

* データモデルオブジェクトとサービスを追加する
* データモデルオブジェクトの読み取りサービスと書き込みサービスの設定

フォームデータモデルを設定するには、次の手順に従います。

1. AEM オーサーインスタンスで、**[!UICONTROL フォーム]**／**[!UICONTROL データ統合]**&#x200B;に移動します。デフォルトの URL は、[https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm](https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm) です。
1. 前の手順で作成した **customer-shipping-billing-details** というフォームデータモデルが表示されます。編集モードで開きます。

   選択したデータソース **WeRetailMySQL** がフォームデータモデルで設定されます。

   ![default-fdm](assets/default-fdm.png)

1. データソースツリーで WeRailMySQL データソースを展開します。**weretail**／**customerdetails** スキーマで、以下のデータモデルオブジェクトをフォームデータモデルに対して選択します。

   * **データモデルオブジェクト**：

      * id
      * name
      * shippingAddress
      * 市区町村
      * ステート
      * 郵便番号

   * **サービス：**

      * 取得
      * 更新

   「**選択項目を追加**」を選択して、フォームデータモデルに対して選択したデータモデルオブジェクトおよびサービスを追加します。

   ![WeRetail スキーマ](assets/weretail_schema_new.png)

   >[!NOTE]
   >
   >JDBC データソースのデフォルトの get サービス、update サービス、insert サービスは、フォームデータモデルでそのまま使用することができます。

1. データモデルオブジェクトに読み取りサービスおよび書き込みサービスを設定します。

   1. **customerdetails** データモデルオブジェクトを選択して、「**[!UICONTROL プロパティを編集]**」を選択します。
   1. 「読み取りサービス」ドロップダウンで「**[!UICONTROL get]**」を選択します。customerdetails データモデルオブジェクトのプライマリキーである **id** 引数が自動的に追加されます。タグ ![aem_6_3_edit](assets/aem_6_3_edit.png) を選択して、次のように引数を設定します。

      ![read-default](assets/read-default.png)

   1. 同様に、書き込みサービスとして「**[!UICONTROL 更新]**」を選択します。**customerdetails** オブジェクトが引数として自動的に追加されます。引数は次のように設定されます。

      ![write-default](assets/write-default.png)

      **id** 引数を追加して以下のように設定します。

      ![id-arg](assets/id-arg.png)

   1. 「**[!UICONTROL 完了]**」を選択して、データモデルオブジェクトのプロパティを保存します。  次に「**[!UICONTROL 保存]**」を選択して、フォームデータモデルを保存します。

      **[!UICONTROL get]** サービスと **[!UICONTROL update]** サービスが、データモデルオブジェクトのデフォルトのサービスとして追加されます。

      ![data-model-object](assets/data-model-object.png)

1. 「**[!UICONTROL サービス]**」タブに移動し、**[!UICONTROL get]** サービスと **[!UICONTROL update]** サービスを設定します。

   1. **[!UICONTROL get]** サービスを選択して「**[!UICONTROL プロパティの編集]**」を選択します。プロパティダイアログが開きます。
   1. プロパティを編集ダイアログで、以下のプロパティを指定します。

      * **タイトル**：サービスのタイトルを指定します。例：配送先住所を取得します。
      * **説明**：サービスの詳細な機能を含む説明を指定します。例：

        このサービスは [!DNL MySQL] データベースから配送先住所などの顧客についての詳細を取得します

      * **出力モデルオブジェクト**：顧客データを保管するスキーマを選択します。例：

        customerdetail スキーマ

      * **配列を返す**：「**配列を返す**」オプションを無効にします。
      * **引数**：**ID** という引数を選択します。

      「**[!UICONTROL 完了]**」を選択します。これで、顧客の詳細情報を MySQL データベースから取得するサービスが設定されました。

      ![shiping-address-retrieval](assets/shiiping-address-retrieval.png)

   1. **[!UICONTROL update]** サービスを選択して「**[!UICONTROL プロパティの編集]**」を選択します。プロパティダイアログが開きます。

   1. [!UICONTROL プロパティを編集]ダイアログで、以下を指定します。

      * **タイトル**：サービスのタイトルを指定します。例えば、「配送先住所を更新」などです。
      * **説明**：サービスの詳細な機能を含む説明を指定します。例：

        このサービスは、配送先住所とそれに関連するフィールドを MySQL データベース内で更新します

      * **入力モデルオブジェクト**：顧客データを保管するスキーマを選択します。例：

        customerdetail スキーマ

      * **出力タイプ**：「**ブール演算式**」を選択します。

      * **引数**：**ID** という引数と **customerdetails** という引数を選択します。

      「**[!UICONTROL 完了]**」を選択します。[!DNL MySQL] データベース内の顧客の詳細情報を更新する **[!UICONTROL update]** サービスが設定されました。

      ![shiping-address-update](assets/shiiping-address-update.png)

フォームデータモデル内のデータモデルオブジェクトとサービスが設定されています。これで、フォームデータモデルをテストできます。

## 手順 4：フォームデータモデルをテストする {#test-fdm}

データモデルオブジェクトとサービスをテストすることにより、フォームデータモデルが正しく設定されているかどうかを確認することができます。

テストを実行するには、以下の手順を実行します。

1. 「**[!UICONTROL モデル]**」タブに移動し、**customerdetails** データモデルオブジェクトを選択し、「**[!UICONTROL モデルオブジェクトをテスト]**」を選択します。
1. [!UICONTROL モデル／サービスのテスト]ウィンドウの「**[!UICONTROL モデル／サービスを選択]**」ドロップダウンで「**[!UICONTROL モデルオブジェクトを読み込み]**」を選択します。
1. 「**customerdetails**」セクションで、設定済み [!DNL MySQL] データベース内の **id** 引数を指定して「**[!UICONTROL テスト]**」を選択します。

   指定した id 引数に関連付けられている顧客の詳細情報がデータベースから取得され、以下のように **[!UICONTROL Output]** セクションに表示されます。

   ![test-read-model](assets/test-read-model.png)

1. 同様に、書き込みモデルオブジェクトおよびサービスをテストできます。

   次の例では、更新サービスは、データベース内の ID 7102715 のアドレスの詳細を正常に更新します。

   ![test-write-model](assets/test-write-model.png)

   この状態で、7102715 という ID に対して読み取りモデルサービスのテストをもう一度実行すると、以下のように、更新後の顧客の詳細情報が画面に表示されます。

   ![read-updated](assets/read-updated.png)


>[!NOTE]
>
> アダプティブフォームのフォームデータモデルを使用して SharePoint リスト設定を作成および使用し、データや生成済みレコードのドキュメントを SharePoint リストに保存できます。手順について詳しくは、[Microsoft® SharePoint リストへアダプティブフォームを接続](/help/forms/using/configuring-submit-actions.md#create-a-sharepoint-list-configuration)を参照してください。