---
title: "チュートリアル：フォームデータモデルの作成 "
description: MySQL を データソース として設定する方法、フォームデータモデル(FDM)を作成して設定する方法、MySQL を AEM Forms 用にテストする方法を学びます。
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.3/FORMS
docset: aem65
exl-id: 40bc5af6-9023-437e-95b0-f85d3df7d8aa
source-git-commit: 4158315c28412bb9498c7d49d21b3f4d72681fc6
workflow-type: tm+mt
source-wordcount: '1533'
ht-degree: 74%

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

様々なタイプのデータソースを設定して、フォームデータモデルを作成できます。このチュートリアルでは、構成してサンプルデータを設定した MySQL データベースを構成します。 その他のサポート対象データソースとその設定方法について詳しくは、[AEM Forms データ統合](../../forms/using/data-integration.md)を参照してください。

[!DNL MySQL] データベースを設定するには、次の手順を実行します。

1. [!DNL MySQL] データベース用の JDBC ドライバーを OSGi バンドルとしてインストールします。

   1. [!DNL MySQL] JDBC ドライバー OSGi バンドルを `http://www.java2s.com/ref/jar/download-orgosgiservicejdbc100jar-file.html` からダウンロードします。<!-- This URL is an insecure link but using https is not possible -->
   1. AEM [!DNL Forms] のオーサーインスタンスに管理者としてログインし、AEM Web コンソールのバンドルに移動します。デフォルトの URL は、[https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles) です。

   1. 選択 **[!UICONTROL インストール/更新]**. 「[!UICONTROL Upload / Install Bundles]」ダイアログが表示されます。

   1. 「ファイル&#x200B;]**を選択」を選択して、**[!UICONTROL  JDBC ドライバーの OSGi バンドルを参照し、[!DNL MySQL]選択します。「開始バンドルおよび更新パッケージ&#x200B;]**」を選択し**[!UICONTROL 、「インストール」または「更新&#x200B;]**」を選択します**[!UICONTROL 。****[!DNL MySQL] の [!DNL Oracle Corporation's] JDBC ドライバーがアクティブになっていることを確認します。ドライバーがインストールされます。

1. [!DNL MySQL] データベースをデータソースとして設定します。

   1. AEM web コンソール（[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)）に移動します。
   1. 「**Apache Sling Connection Pooled DataSource**」という設定を探し、オンにすると、編集モードで設定が開きます。
   1. 設定ダイアログで、次の詳細を指定します。

      * **データソース名：**&#x200B;任意の名前を指定できます。例えば、「**WeRetailMySQL**」などを指定します。
      * **DataSource サービスのプロパティ名**：DataSource 名を含むサービスプロパティの名前を指定します。データソースインスタンスを OSGi サービスとして登録する際に指定されます。例えば、**datasource.name** です。
      * **JDBC ドライバークラス**:JDBC ドライバーの Java™クラス名を指定します。 [!DNL MySQL] データベースの場合は、**com.mysql.jdbc.Driver**&#x200B;と指定します。
      * **JDBC connection URI**：データベースの接続 URL を指定します。ポート 3306 および スキーマ `weretail`で実行されているデータベースの場合[!DNL MySQL]、URLは次のようになります。`jdbc:mysql://'server':3306/weretail?autoReconnect=true&useUnicode=true&characterEncoding=utf-8`

      >[!NOTE]
      >
      > [!DNL MySQL] データベースがファイアウォールの内側にある場合、データベースホスト名はパブリック DNS ではありません。データベースの IP アドレスをAEM ホストマシンの */etc/hosts* ファイルに追加する必要があります。

      * **Username**：データベースのユーザー名を指定します。データベースとの接続を確立するには、JDBC ドライバーを有効にする必要があります。
      * **Password**：データベースのパスワードを指定します。データベースとの接続を確立するには、JDBC ドライバーを有効にする必要があります。

      >[!NOTE]
      >
      >AEM Forms は、[!DNL MySQL] の NT 認証をサポートしていません。Web コンソールAEM [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr) に移動し、「Apache Sling 接続 Pooled Datasource」検索します。 「JDBC接続URI」プロパティは、「integratedSecurity」の値をFalseに設定し、作成したユーザー名とパスワードを使用してデータベースに接続します [!DNL MySQL] 。

      * **Test on Borrow：** は **[!UICONTROL Test on Borrow]** オプションを有効にします。
      * **Test on Return：** は **[!UICONTROL Test on Return]** オプションを有効にします。
      * **検証クエリ：**&#x200B;プールからの接続を検証する SQL SELECT クエリを指定します。クエリは、1 行以上の行を返す必要があります。例えば、**customerdetails から &#42; を選択します**。
      * **Transaction Isolation**：このオプションの値を「**READ_COMMITTED**」に設定します。

        他のプロパティはデフォルト値[](https://tomcat.apache.org/tomcat-7.0-doc/jdbc-pool.html)のままにして、「保存&#x200B;]**」を選択します**[!UICONTROL 。

        以下のような設定が作成されます。

        ![relational-database-data-source-configuration](assets/relational-database-data-source-configuration.png)

## 手順 2：フォームデータモデルを作成する {#create-fdm}

AEM [!DNL Forms] には、設定済みデータソースから[フォームデータモデルを作成](data-integration.md)するための直感的なユーザーインターフェイスが用意されています。1 つのフォームデータモデル内で複数のデータソースを使用することができます。この使用例では、設定済みの [!DNL MySQL] データソースを使用できます。

フォームデータモデルを作成するには、以下の手順を実行します。

1. AEM オーサーインスタンスで、**[!UICONTROL フォーム]**／**[!UICONTROL データ統合]**&#x200B;に移動します。
1. 作成&#x200B;]**>**[!UICONTROL &#x200B;フォーム データモデル&#x200B;]**を選択します**[!UICONTROL 。
1. フォームデータモデル作成ダイアログで、フォームデータモデルの&#x200B;**名前**&#x200B;を指定します。例えば、**customer-shipping-billing-details** などを指定します。「**[!UICONTROL 次へ]**」を選択します。
1. データソース選択画面に、すべての設定済みデータソースが一覧表示されます。選択 **WeRetailMySQL** データソースと選択 **[!UICONTROL 作成]**.

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

1. データソースツリーで WeRailMySQL データソースを展開します。データモデルを形成できるように、weretail > customerdetails **スキーマから**&#x200B;次のデータモデルオブジェクトとサービス&#x200B;**を選択します。**

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

   選択した **データモデルオブジェクトとサービスをフォームデータモデルに追加するには、「追加選択済み** 」を選択します。

   ![WeRetail スキーマ](assets/weretail_schema_new.png)

   >[!NOTE]
   >
   >JDBC データソースのデフォルトの get サービス、update サービス、insert サービスは、フォームデータモデルでそのまま使用することができます。

1. データモデルオブジェクトに読み取りサービスおよび書き込みサービスを設定します。

   1. を選択します。 **customerdetails** データモデルオブジェクトを選択し、 **[!UICONTROL プロパティを編集]**.
   1. 「読み取りサービス」ドロップダウンで「**[!UICONTROL get]**」を選択します。customerdetails データモデルオブジェクトのプライマリキーである **id** 引数が自動的に追加されます。![aem_6_3_editを選択し、](assets/aem_6_3_edit.png)次のように引数を設定します。

      ![read-default](assets/read-default.png)

   1. 同様に、書き込みサービスとして「**[!UICONTROL 更新]**」を選択します。**customerdetails** オブジェクトが引数として自動的に追加されます。引数は次のように設定されます。

      ![write-default](assets/write-default.png)

      **id** 引数を追加して以下のように設定します。

      ![id-arg](assets/id-arg.png)

   1. データモデルオブジェクトのプロパティを保存する完了&#x200B;]**を選択します**[!UICONTROL 。次に、 **[!UICONTROL 保存]** フォームデータモデルを保存します。

      **[!UICONTROL get]** サービスと **[!UICONTROL update]** サービスが、データモデルオブジェクトのデフォルトのサービスとして追加されます。

      ![data-model-object](assets/data-model-object.png)

1. 「**[!UICONTROL サービス]**」タブに移動し、**[!UICONTROL get]** サービスと **[!UICONTROL update]** サービスを設定します。

   1. Get ]**サービスを選択し、「**[!UICONTROL &#x200B;編集 プロパティ&#x200B;]**」を選択します**[!UICONTROL 。プロパティダイアログが開きます。
   1. プロパティを編集ダイアログで、以下のプロパティを指定します。

      * **タイトル**：サービスのタイトルを指定します。例：配送先住所を取得します。
      * **説明**：サービスの詳細な機能を含む説明を指定します。例：

        このサービスは、データベースから [!DNL MySQL] 配送先住所およびその他の顧客の詳細を取得します

      * **出力モデルオブジェクト**：顧客データを保管するスキーマを選択します。例：

        customerdetail スキーマ

      * **配列を返す**：「**配列を返す**」オプションを無効にします。
      * **引数**：**ID** という引数を選択します。

      「**[!UICONTROL 完了]**」を選択します。これで、顧客の詳細情報を MySQL データベースから取得するサービスが設定されました。

      ![shiping-address-retrieval](assets/shiiping-address-retrieval.png)

   1. 更新&#x200B;]**サービスを選択し、[**[!UICONTROL &#x200B;編集 プロパティ&#x200B;]**] を選択します**[!UICONTROL 。プロパティダイアログが開きます。

   1. [!UICONTROL プロパティを編集]ダイアログで、以下を指定します。

      * **タイトル**：サービスのタイトルを指定します。例えば、「配送先住所を更新」などです。
      * **説明**：サービスの詳細な機能を含む説明を指定します。例：

        このサービスは、配送先住所とそれに関連するフィールドを MySQL データベース内で更新します

      * **入力モデルオブジェクト**：顧客データを保管するスキーマを選択します。例：

        customerdetail スキーマ

      * **出力タイプ**：「**ブール演算式**」を選択します。

      * **引数:引数**&#x200B;名 **、ID** および **顧客詳細**&#x200B;を選択します。

      「**[!UICONTROL 完了]**」を選択します。[!DNL MySQL] データベース内の顧客の詳細情報を更新する **[!UICONTROL update]** サービスが設定されました。

      ![shiping-address-update](assets/shiiping-address-update.png)

フォームデータモデル内のデータモデルオブジェクトとサービスが設定されています。これで、フォームデータモデルをテストできます。

## 手順 4：フォームデータモデルをテストする {#test-fdm}

データモデルオブジェクトとサービスをテストすることにより、フォームデータモデルが正しく設定されているかどうかを確認することができます。

テストを実行するには、以下の手順を実行します。

1. **[!UICONTROL モデル]**&#x200B;タブに移動し、customerdetails **データモデルオブジェクトを選択して**、「モデルオブジェクト&#x200B;]**テストを選択します**[!UICONTROL 。
1. [!UICONTROL モデル／サービスのテスト]ウィンドウの「**[!UICONTROL モデル／サービスを選択]**」ドロップダウンで「**[!UICONTROL モデルオブジェクトを読み込み]**」を選択します。
1. customerdetails **セクションで、構成済みの[!DNL MySQL]データベースに存在する id** 引数の値&#x200B;**を指定し、[テスト]**] を選択します&#x200B;**[!UICONTROL 。**

   指定した id 引数に関連付けられている顧客の詳細情報がデータベースから取得され、以下のように **[!UICONTROL Output]** セクションに表示されます。

   ![test-read-model](assets/test-read-model.png)

1. 同様に、書き込みモデルオブジェクトおよびサービスをテストできます。

   次の例では、更新サービスは、データベース内の ID 7102715 のアドレスの詳細を正常に更新します。

   ![test-write-model](assets/test-write-model.png)

   これで、id 7107215 に対してモデルの読み取りサービスを再度テストすると、次に示すように、更新された顧客の詳細がフェッチされて表示されます。

   ![read-updated](assets/read-updated.png)


>[!NOTE]
>
> アダプティブ フォームで フォーム データ モデルを使用して SharePoint リスト構成を作成および使用し、データまたは生成されたレコードのドキュメントを SharePoint リストに保存できます。 詳細な手順については、「アダプティブフォームを Microsoft® SharePoint リスト](/help/forms/using/configuring-submit-actions.md#create-a-sharepoint-list-configuration)に接続する」を参照してください[。