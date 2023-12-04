---
title: 「チュートリアル：AEM Forms でフォームデータモデルを作成する」
description: インタラクティブ通信用フォームデータモデルの作成
uuid: b56d3dac-be54-4812-b958-38a085686218
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e5413fb3-9d50-4f4f-9db8-7e53cd5145d5
docset: aem65
feature: Interactive Communication
exl-id: c8a6037c-46bd-4058-8314-61cb925ba5a8
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '2684'
ht-degree: 82%

---

# チュートリアル：AEM Formsでのフォームデータモデルの作成{#tutorial-create-form-data-model}

![04-create-form-data-model-main](assets/04-create-form-data-model-main.png)

これは、「[最初のインタラクティブ通信の作成](/help/forms/using/create-your-first-interactive-communication.md)」シリーズを構成するチュートリアルです。チュートリアルの使用例全体を理解、実行、デモするために、シリーズを時系列に沿って実施することをお勧めします。

## チュートリアルについて {#about-the-tutorial}

AEM Formsデータ統合モジュールを使用すると、AEMユーザープロファイル、RESTful Web サービス、SOAP ベースの Web サービス、OData サービス、リレーショナルデータベースなど、様々なバックエンドデータソースからフォームデータモデルを作成できます。 フォームデータモデル内でデータモデルオブジェクトおよびサービスを設定し、アダプティブフォームに関連付けることができます。アダプティブフォームのフィールドは、データモデルオブジェクトのプロパティに連結されます。このサービスを使用すると、アダプティブフォームに事前に入力し、送信されたフォームデータをデータモデルオブジェクトに書き込むことができます。

フォームデータの統合機能とフォームデータモデルについて詳しくは、「[AEM Forms のデータ統合機能](https://helpx.adobe.com/jp/experience-manager/6-3/forms/using/install-configure-pdf-generator.html)」を参照してください。

このチュートリアルでは、フォームデータモデルを準備、作成、設定およびインタラクティブ通信に関連付ける手順について説明します。このチュートリアルを完了すると、次の操作を実行できるようになります。

* [データベースの設定](../../forms/using/create-form-data-model0.md#step-set-up-the-database)
* [MySQL データベースをデータソースとして設定する](../../forms/using/create-form-data-model0.md#step-configure-mysql-database-as-data-source)
* [フォームデータモデルの作成](../../forms/using/create-form-data-model0.md#step-create-form-data-model)
* [フォームデータモデルを設定する](../../forms/using/create-form-data-model0.md#step-configure-form-data-model)
* [フォームデータモデルのテストを行う](../../forms/using/create-form-data-model0.md#step-test-form-data-model-and-services)

フォームデータモデルは以下に類似しています。

![フォームデータモデル](assets/form_data_model_callouts_new.png)

**A.** 設定済みのデータソース **B.** データソーススキーマ **C.** 利用可能なサービス **D.** データモデルオブジェクト **E.** 設定済みサービス

## 前提条件 {#prerequisites}

開始する前に、次の点を確認してください。

* [データベースの設定](../../forms/using/create-form-data-model0.md#step-set-up-the-database)の節にの記載に従って、MySQL データベースにサンプルデータが取り込まれていること。
* [JDBC データベースドライバーのバンドル](https://helpx.adobe.com/jp/experience-manager/6-3/help/sites-developing/jdbc.html#bundling-the-jdbc-database-driver)の説明に従って、MySQL JDBC ドライバー用の OSGi バンドルが設定されていること

## 手順 1：データベースをセットアップする {#step-set-up-the-database}

インタラクティブ通信を作成するには、データベースが不可欠です。このチュートリアルではデータベースを使用して、インタラクティブ通信のフォームデータモデルと永続性機能を表示します。顧客、請求および通話のテーブルを含むデータベースを設定します。以下の画像は、顧客テーブルのサンプルデータを示しています。

![sample_data_cust](assets/sample_data_cust.png)

以下の DDL ステートメントを使用して、データベース内に **customer** というテーブルを作成します。

```sql
CREATE TABLE `customer` (
   `mobilenum` int(11) NOT NULL,
   `name` varchar(45) NOT NULL,
   `address` varchar(45) NOT NULL,
   `alternatemobilenumber` int(11) DEFAULT NULL,
   `relationshipnumber` int(11) DEFAULT NULL,
   `customerplan` varchar(45) DEFAULT NULL,
   PRIMARY KEY (`mobilenum`),
   UNIQUE KEY `mobilenum_UNIQUE` (`mobilenum`)
 ) ENGINE=InnoDB DEFAULT CHARSET=utf8
```

以下の DDL ステートメントを使用して、データベース内に **bills** というテーブルを作成します。

```sql
CREATE TABLE `bills` (
   `billplan` varchar(45) NOT NULL,
   `latepayment` decimal(4,2) NOT NULL,
   `monthlycharges` decimal(4,2) NOT NULL,
   `billdate` date NOT NULL,
   `billperiod` varchar(45) NOT NULL,
   `prevbal` decimal(4,2) NOT NULL,
   `callcharges` decimal(4,2) NOT NULL,
   `confcallcharges` decimal(4,2) NOT NULL,
   `smscharges` decimal(4,2) NOT NULL,
   `internetcharges` decimal(4,2) NOT NULL,
   `roamingnational` decimal(4,2) NOT NULL,
   `roamingintnl` decimal(4,2) NOT NULL,
   `vas` decimal(4,2) NOT NULL,
   `discounts` decimal(4,2) NOT NULL,
   `tax` decimal(4,2) NOT NULL,
   PRIMARY KEY (`billplan`)
 ) ENGINE=InnoDB DEFAULT CHARSET=utf8
```

以下の DDL ステートメントを使用して、データベース内に **calls** というテーブルを作成します。

```sql
CREATE TABLE `calls` (
   `mobilenum` int(11) DEFAULT NULL,
   `calldate` date DEFAULT NULL,
   `calltime` varchar(45) DEFAULT NULL,
   `callnumber` int(11) DEFAULT NULL,
   `callduration` varchar(45) DEFAULT NULL,
   `callcharges` decimal(4,2) DEFAULT NULL,
   `calltype` varchar(45) DEFAULT NULL
 ) ENGINE=InnoDB DEFAULT CHARSET=utf8
```

**通話** テーブルには、通話の日付、通話の時間、通話番号、通話時間、通話料金などの詳細が含まれます。**顧客** テーブルは携帯電話番号（mobilenum）フィールドにより通話テーブルとリンクしています。**顧客**&#x200B;テーブルにリストされた各携帯電話番号ごとに、**通話**&#x200B;テーブルに複数の記録があります。例えば、**1457892541** という携帯電話番号の通話の詳細を、**通話**&#x200B;テーブルを参照することで取得できます。

**請求**&#x200B;テーブルには請求日、請求期間、月額利用料、通話料金などの請求明細が含まれます。**顧客**&#x200B;テーブルは請求プランフィールドにより&#x200B;**請求**&#x200B;テーブルとリンクしています。**顧客**&#x200B;テーブルには、各顧客と関連付けられたプランがあります。**請求**&#x200B;テーブルには、既存のすべてのプランの価格の詳細が含まれます。例えば、**Sarah** のプランの詳細を顧客テーブルから取得し&#x200B;**、**&#x200B;この情報を使って請求テーブルから価格の詳細を取得することができます&#x200B;**。**

## 手順 2：データソースとして MySQL データベースを設定する {#step-configure-mysql-database-as-data-source}

様々なタイプのデータソースを設定して、フォームデータモデルを作成できます。このチュートリアルでは、サンプルデータが設定され、入力された MySQL データベースを設定します。その他のサポート対象データソースとその設定方法について詳しくは、[AEM Forms のデータ統合機能](https://helpx.adobe.com/jp/experience-manager/6-3/forms/using/install-configure-pdf-generator.html)を参照してください。

MySQL データベースを設定するには、次の手順を実行します。

1. 以下の手順により、MySQL データベース用の JDBC ドライバーを OSGi バンドルとしてインストールします。

   1. AEM Forms のオーサーインスタンスに管理者としてログインし、AEM Web コンソールバンドルに移動します。デフォルトの URL は、[https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles) です。
   1. 選択 **インストール/更新**. 「**Upload / Install Bundles**」ダイアログが表示されます。

   1. 選択 **ファイルを選択** を参照して、MySQL JDBC ドライバー OSGi バンドルを選択します。 選択 **バンドルを開始** および **パッケージを更新**&#x200B;をクリックし、次を選択します。 **インストール** または **更新**. Oracle が提供する MySQL の JDBC ドライバーがアクティブになっていることを確認します。ドライバーがインストールされます。

1. MySQL データベースをデータソースとして設定します。

   1. AEM Web コンソール（[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)）に移動します。
   1. 「**Apache Sling Connection Pooled DataSource**」という設定を探し、「 」を選択して、設定を編集モードで開きます。
   1. 設定ダイアログで、次の詳細を指定します。

      * **データソース名：**&#x200B;任意の名前を指定できます。例えば、 **MySQL** などを指定します。

      * **データソースサービスのプロパティ名**：データソース名を含むサービスプロパティの名前を指定します。データソースインスタンスを OSGi サービスとして登録する際に指定されます。例えば、**datasource.name** です。

      * **JDBC ドライバークラス**：JDBC ドライバーの Java クラス名を指定します。MySQL データベースの場合は、**com.mysql.jdbc.Driver** と指定します。

      * **JDBC connection URI**：データベースの接続 URL を指定します。ポート 3306 とスキーマ teleca 上で稼働する MySQL データベースの場合、URL は `jdbc:mysql://'server':3306/teleca?autoReconnect=true&useUnicode=true&characterEncoding=utf-8` です。
      * **Username**：データベースのユーザー名を指定します。データベースとの接続を確立するには、JDBC ドライバーを有効にする必要があります。
      * **Password**：データベースのパスワードを指定します。データベースとの接続を確立するには、JDBC ドライバーを有効にする必要があります。
      * **Test on Borrow：** は **Test on Borrow** オプションを有効にします。

      * **Test on Return：** は **Test on Return** オプションを有効にします。

      * **検証クエリ：**&#x200B;プールからの接続を検証する SQL SELECT クエリを指定します。クエリは、1 行以上の行を返す必要があります。例：**select &#42; from customer**。

      * **Transaction Isolation**：このオプションの値を「**READ_COMMITTED**」に設定します。

   他のプロパティはデフォルトのままにします [値](https://tomcat.apache.org/tomcat-7.0-doc/jdbc-pool.html) を選択し、 **保存**.

   以下のような設定が作成されます。

   ![Apache 設定](assets/apache_configuration_new.png)

## 手順 3：フォームデータモデルを作成する {#step-create-form-data-model}

AEM Forms には、設定済みデータソースを使用して[フォームデータモデルを作成](https://helpx.adobe.com/jp/experience-manager/6-3/forms/using/data-integration.html#main-pars_header_1524967585)するための直感的なユーザーインターフェイスが用意されています。1 つのフォームデータモデル内で複数のデータソースを使用することができます。このチュートリアルのユースケースでは、MySQL をデータソースとして使用します。

フォームデータモデルを作成するには、以下の手順を実行します。

1. AEM オーサーインスタンスで、**フォーム**／**データ統合**&#x200B;に移動します。
1. 選択 **作成** > **フォームデータモデル**.
1. フォームデータモデル作成ウィザードで、フォームデータモデルの&#x200B;**名前**&#x200B;を指定します。例えば **FDM_Create_First_IC** などと指定します。「**次へ**」を選択します。
1. データソース選択画面に、すべての設定済みデータソースが一覧表示されます。選択 **MySQL** データソースと選択 **作成**.

   ![MYSQL データソース](assets/fdm_mysql_data_source_new.png)

1. 「**完了**」をクリックします。**FDM_Create_First_IC** というフォームデータモデルが作成されます。

## 手順 4：フォームデータモデルを設定する {#step-configure-form-data-model}

フォームデータモデルの設定には以下が含まれます。

* [データモデルオブジェクトとサービスの追加](#add-data-model-objects-and-services)
* [データモデルオブジェクト用の計算済み子プロパティの作成](#create-computed-child-properties-for-data-model-object)
* [データモデルオブジェクト間の関連付けの追加](#add-associations-between-data-model-objects)
* [データモデルオブジェクトプロパティの編集](#edit-data-model-object-properties)
* [データモデルオブジェクト用サービスの設定](#configure-services)

### データモデルオブジェクトとサービスの追加 {#add-data-model-objects-and-services}

1. AEM オーサーインスタンスで、**フォーム**／**データ統合**&#x200B;に移動します。デフォルトの URL は、[https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm](https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm) です。
1. 前の手順で作成した **FDM_Create_First_IC** というフォームデータモデルが表示されます。選択してを選択します。 **編集**.

   選択されたデータソース **MySQL** が&#x200B;**データソース**&#x200B;ペインに表示されます。

   ![FDM 用の MYSQL データソース](assets/mysql_fdm_new.png)

1. **MySQL** データソースツリーを展開します。**teleca** スキーマで、以下のデータモデルオブジェクトとサービスを選択します。

   * **データモデルオブジェクト**:

      * 請求
      * 通話
      * 顧客

   * **サービス：**

      * 取得
      * 更新

   選択 **選択項目を追加** 選択したデータモデルオブジェクトとサービスをフォームデータモデルに追加する場合。

   ![データモデルオブジェクトサービスを選択](assets/select_data_model_object_services_new.png)

   請求、通話および顧客のデータモデルオブジェクトは、「**モデル**」タブの右側のパネルに表示されます。取得サービスと更新サービスは、「**サービス**」タブに表示されます。

   ![データモデルオブジェクト](assets/data_model_objects_new.png)

### データモデルオブジェクト用の計算済み子プロパティの作成 {#create-computed-child-properties-for-data-model-object}

計算済みプロパティとは、ルールまたは式に基づいて値が計算されるプロパティのことです。ルールを使用して、計算済みプロパティの値を、リテラル文字列、数値、数式の計算結果、フォームデータモデル内の別のプロパティの値に設定できます。

ユースケースに基づき、以下の数式を使って&#x200B;**請求**&#x200B;データモデルオブジェクトの **usagecharges** 計算済み子プロパティを作成します。

* 利用料金 = 通話料金 + 会議通話料金 + SMS 料金 + 携帯インターネット料金 + 国内ローミング料金 + 国際ローミング料金 + VAS（これらのすべてのプロパティは bills データモデルオブジェクトに含まれます）**usagecharges** の計算済み子プロパティについて詳しくは、[インタラクティブ通信の計画](/help/forms/using/planning-interactive-communications.md)を参照してください。

請求データモデルオブジェクト用の計算済み子プロパティを作成するには、次の手順を実行します。

1. の上部にあるチェックボックスをオンにします。 **手形** 選択して選択するデータモデルオブジェクト **子プロパティを作成**.
1. **子プロパティを作成**&#x200B;パネルで、次のように操作します。

   1. 子プロパティの名前として **usagecharges** を入力します。
   1. 「**計算済み**」を有効にします。
   1. 選択 **浮動小数** をタイプとして選択し、 **完了** 子プロパティを **手形** データモデルオブジェクト。

   ![子プロパティを作成](assets/create_child_property_new.png)

1. 選択 **ルールを編集** をクリックして、ルールエディターを開きます。
1. 「**作成**」を選択します。「**Set Value**」ルールウィンドウが開きます。
1. オプション選択ドロップダウンで、「**数式**」を選択します。

   ![使用料金ルールエディター](assets/usage_charges_rule_editor_new.png)

1. 数式の最初のオブジェクトとして「**callcharges**」を選択し、2 番目のオブジェクトとして「**confcallcharges**」を選択します。演算子として「**プラス**」を選択します。数式内で「 」を選択し、「 」を選択します。 **式を拡張** 追加する **smscharges**, **インターネット料金**, **国民的な**, **roamingintnl**、および **輸管** オブジェクトを式に追加します。

   次の画像はルールエディター内の数式を示しています。

   ![使用料金ルール](assets/usage_charges_rule_all_new.png)

1. 選択 **完了**. ルールエディター内でルールが作成されます。
1. 選択 **閉じる** をクリックして、[ ルールエディタ ] ウィンドウを閉じます。

### データモデルオブジェクト間の関連付けの追加 {#add-associations-between-data-model-objects}

データモデルオブジェクトが定義されたら、オブジェクト間の関連付けを作成できます。この関連付けは、1 対 1 の場合もあれば、1 対多の場合もあります。例えば、1 人の従業員に対して複数の扶養家族を関連付けることができます。これを、1 対多の関連付けといいます。関連するデータモデルオブジェクトを接続するライン上では、「1:n」として表示されます。それに対して、特定の従業員 ID で一意の従業員名が返される場合などは、1 対 1 の関連付けになります。

データソース内の関連データモデルオブジェクトをフォームデータモデルに追加した場合、それらの関連付けは維持され、矢印の線で接続された状態で表示されます。

ユースケースに基づき、データモデルオブジェクト間で以下の関連付けを作成します。

| 関連付け | データモデルオブジェクト |
|---|---|
| 1:n | 顧客:通話（月々の請求書で、1 人の顧客と複数の通話を関連付けられます） |
| 1:1 | 顧客:請求（特定の月の請求書で、1 つの請求を 1 人の顧客と関連付けます） |

データモデルオブジェクト間で関連性を作成するには、以下の手順を実行します。

1. の上部にあるチェックボックスをオンにします。 **顧客** 選択して選択するデータモデルオブジェクト **関連付けを追加**. **関連付けを追加**&#x200B;プロパティペインが表示されます。
1. **関連付けを追加**&#x200B;パネルで、以下の操作を実行します。

   * 関連付けのタイトルを入力します。これはオプションのフィールドです。
   * 「**タイプ**」ドロップダウンリストから「**1 対多**」を選択します。

   * 「**モデルオブジェクト**」ドロップダウンリストから「**通話**」を選択します。

   * 「**サービス**」ドロップダウンリストから **get** を選択します。

   * 選択 **追加** リンクする **顧客** データモデルオブジェクトを **呼び出し** プロパティを使用するデータモデルオブジェクト。 ユースケースに基づいて、通話データモデルオブジェクトは顧客データモデルオブジェクトの携帯電話番号プロパティにリンクされている必要があります。**引数を追加**&#x200B;ダイアログボックスが開きます。

   ![関連付けを追加](assets/add_association_new.png)

1. **引数を追加**&#x200B;ダイアログボックスで、

   * 「**名前**」ドロップダウンリストから「**mobilenum**」を選択します。携帯電話プロパティは、顧客および通話データモデルオブジェクトで利用できる共通プロパティです。その結果、プロパティは顧客と通話データモデルオブジェクト間の関連付けを作成するために使用されます。顧客データモデルオブジェクトに用意された各携帯電話番号ごとに、通話テーブルに複数の記録を参照できます。

   * 引数の任意のタイトルと説明を指定します。
   * 「**連結先**」ドロップダウンリストから「**顧客**」を選択します。

   * 「**連結値**」ドロップダウンリストから「**mobilenum**」を選択します。

   * 「**追加**」を選択します。

   ![引数の関連付けを追加](assets/add_association_argument_new.png)

   mobilenum プロパティが&#x200B;**引数**&#x200B;セクションに表示されます。

   ![引数の関連付けを追加](assets/add_argument_association_new.png)

1. 選択 **完了** ：顧客と呼び出しデータモデルオブジェクトの間に 1:n の関連付けを作成します。

   顧客および通話データモデルオブジェクト間で関連付けを作成したら、顧客と通話データモデルオブジェクト間で 1:1 の関連付けを作成します。

1. の上部にあるチェックボックスをオンにします。 **顧客** 選択して選択するデータモデルオブジェクト **関連付けを追加**. **関連付けを追加**&#x200B;プロパティペインが表示されます。
1. **関連付けを追加**&#x200B;パネルで、以下の操作を実行します。

   * 関連付けのタイトルを入力します。これはオプションのフィールドです。
   * 「**タイプ**」ドロップダウンリストから「**1 対 1**」を選択します。

   * 「**モデルオブジェクト**」ドロップダウンリストから「**請求**」を選択します。

   * 「**サービス**」ドロップダウンリストから **get** を選択します。**billplan** プロパティは請求テーブルのプライマリキーであり、「**引数**」セクションにすでに用意されています。
請求および顧客データモデルオブジェクトは、それぞれbillplan（請求）および customerplan（顧客）プロパティを使ってリンクされています。これらのプロパティ間で連結を作成し、MySQL データベースに含まれるあらゆる顧客の計画の詳細を取得します。

   * 「**連結先**」ドロップダウンリストから「**顧客**」を選択します。

   * 「**連結値**」ドロップダウンリストから「**顧客プラン**」を選択します。

   * 選択 **完了** billplan プロパティと customerplan プロパティの間に連結を作成する場合。

   ![顧客請求の関連付けを追加](assets/add_association_customer_bills_new.png)

   以下の画像は、データモデルオブジェクト間の関連付けと、関連付けの作成に使用されているプロパティを示します。

   ![fdm_associations](assets/fdm_associations.gif)

### データモデルオブジェクトプロパティの編集 {#edit-data-model-object-properties}

顧客とほかのデータモデルオブジェクト間で関連付けを作成後、顧客プロパティを編集し、データモデルオブジェクトから取得されたデータに基づいてプロパティを定義します。ユースケースに基づいて、携帯電話番号は顧客データモデルオブジェクトからデータを取得するためのプロパティとして使用されます。

1. の上部にあるチェックボックスをオンにします。 **顧客** 選択して選択するデータモデルオブジェクト **プロパティを編集**. **プロパティを編集**&#x200B;ペインが開きます。
1. **顧客**&#x200B;を&#x200B;**トップレベルモデルオブジェクト**&#x200B;として指定します。
1. 「**読み取りサービス**」ドロップダウンリストで「**取得**」を選択します。
1. **引数**&#x200B;セクションで、

   * 「**連結先**」ドロップダウンリストから「**属性を要求**」を選択します。

   * **mobilenum** を連結値として指定します。

1. **書き込み**&#x200B;サービスのドロップダウンリストから「**更新**」を選択します。
1. **引数**&#x200B;セクションで、

   * **mobilenum** プロパティとして、「**連結先**」ドロップダウンリストから「**顧客**」を選択します。

   * 「**連結値**」ドロップダウンリストから「**mobilenum**」を選択します。

1. 選択 **完了** をクリックしてプロパティを保存します。

   ![サービスの設定](assets/configure_services_customer_new.png)

1. の上部にあるチェックボックスをオンにします。 **呼び出し** 選択して選択するデータモデルオブジェクト **プロパティを編集**. **プロパティを編集**&#x200B;ペインが開きます。
1. **トップレベルモデルオブジェクト**&#x200B;を、**通話**&#x200B;データモデルオブジェクトに対して無効にします。
1. 「**完了**」を選択します。

   手順 8～10 を繰り返し、**請求**&#x200B;データモデルオブジェクトのプロパティを設定します。

### サービスの設定 {#configure-services}

1. 「**サービス**」タブに移動します。
1. を選択します。 **get** サービスと選択 **プロパティを編集**. **プロパティを編集**&#x200B;ペインが開きます。
1. **プロパティを編集**&#x200B;パネルで、次の操作を行います。

   * 任意のタイトルと説明を入力します。
   * 「**出力モデルオブジェクト**」ドロップダウンリストから「**顧客**」を選択します。

   * 選択 **完了** をクリックしてプロパティを保存します。

   ![プロパティの編集](assets/edit_properties_get_details_new.png)

1. を選択します。 **更新** サービスと選択 **プロパティを編集**. **プロパティを編集**&#x200B;ペインが開きます。
1. **プロパティを編集**&#x200B;パネルで、次の操作を行います。

   * 任意のタイトルと説明を入力します。
   * 「**入力モデルオブジェクト**」ドロップダウンリストから「**顧客**」を選択します。

   * 「**完了**」を選択します。
   * 選択 **保存** フォームデータモデルを保存します。

   ![サービスプロパティを更新](assets/update_service_properties_new.png)

## 手順 5：フォームデータモデルとサービスのテストを実行する {#step-test-form-data-model-and-services}

データモデルオブジェクトとサービスをテストすることにより、フォームデータモデルが正しく設定されているかどうかを確認することができます。

テストを実行するには、以下の手順を実行します。

1. 次に移動： **モデル** タブで、 **顧客** データモデルオブジェクトを選択し、 **モデルオブジェクトのテスト**.
1. **テストフォームデータモデル**&#x200B;ウィンドウの&#x200B;**モデル / サービスを選択**&#x200B;ドロップダウンリストから&#x200B;**モデルオブジェクトを読み込み**&#x200B;を選択します。
1. Adobe Analytics の **入力** セクションで、 **mobilenum** 設定済みの MySQL データベースに存在するプロパティを選択し、 **テスト**.

   指定した mobilenum プロパティに関連付けられている顧客の詳細情報がデータベースから取得され、以下のように「出力」セクションに表示されます。ダイアログボックスを閉じます。

   ![データモデルのテストをおこなう](assets/test_data_model_new.png)

1. 「**サービス**」タブに移動します。
1. を選択します。 **get** サービスと選択 **サービスをテストします。**
1. Adobe Analytics の **入力** セクションで、 **mobilenum** 設定済みの MySQL データベースに存在するプロパティを選択し、 **テスト**.

   指定した mobilenum プロパティに関連付けられている顧客の詳細情報がデータベースから取得され、以下のように「出力」セクションに表示されます。ダイアログボックスを閉じます。

   ![サービスをテスト](assets/test_service_new.png)

### サンプルデータの編集と保存 {#edit-and-save-sample-data}

フォームデータモデルエディターでは、計算済みプロパティを含む、すべてのデータモデルオブジェクトプロパティのサンプルデータを、フォームデータモデル内で生成することができます。 各プロパティで設定されたデータタイプに基づいて、一連のランダムな値がサンプルデータとして生成されます。このサンプルデータを編集して保存することもできます。サンプルデータを再生成した場合も、編集したサンプルデータは保存されたままになります。

サンプルデータを生成、編集して保存するには、以下の手順を実行します。

1. フォームデータモデルページで、「 」を選択します。 **サンプルデータを編集**. サンプルデータが生成され、サンプルデータ編集ウィンドウに表示されます。

   ![サンプルデータを編集する](assets/edit_sample_data_new.png)

1. In **サンプルデータを編集** ウィンドウ、データを必要に応じて編集し、「 」を選択します。 **保存**. ウィンドウを閉じます。
