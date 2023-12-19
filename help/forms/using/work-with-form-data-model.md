---
title: フォームデータモデルの操作
description: データ統合機能には、フォームデータモデルの設定と操作を行うためのフォームデータモデルエディターが付属しています。
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Form Data Model
exl-id: 16b76265-9ec4-4993-9ac0-b7aef1b1e5f1
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '4159'
ht-degree: 89%

---

# フォームデータモデルの操作{#work-with-form-data-model}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/create-form-data-models.html?lang=ja) |
| AEM 6.5 | この記事 |

![data-integration](do-not-localize/data-integeration.png)

フォームデータモデルエディターには、フォームデータモデルの編集と設定を行うための直感的なユーザーインターフェイスとツールが用意されています。このエディターを使用すると、フォームデータモデル内の関連データソースからデータモデルのオブジェクト、プロパティ、サービスの追加と設定を行うことができます。また、データソースを持っていないデータモデルオブジェクトとプロパティを作成し、後でそれらのオブジェクトとプロパティにデータソースを連結することもできます。さらに、データモデルオブジェクトのプロパティ用にサンプルデータを生成して編集し、これらのプロパティを使用してアダプティブフォームにデータを取り込み、プレビュー表示することもできます。フォームデータモデル内で設定したデータモデルのオブジェクトとサービスをテストすることにより、そのフォームデータモデルがデータソースと正しく統合されているかどうかを確認できます。

Forms のデータ統合機能を初めて使用する場合や、これまでにデータソースの設定やフォームデータモデルの作成を行ったことがない場合は、以下のトピックを参照してください。

* [AEM Forms のデータ統合](/help/forms/using/data-integration.md)
* [データソースの設定](/help/forms/using/configure-data-sources.md)
* [フォームデータモデルの作成](/help/forms/using/create-form-data-models.md)

フォームデータモデルエディターを使用して実行できる様々なタスクや設定について、詳しくはこちらをご覧ください。

>[!NOTE]
>
>フォームデータモデルの作成と操作を行うには、**fdm-author** グループと **forms-user** グループの両方のメンバーである必要があります。これらのグループのメンバーになるには、AEM の管理者に依頼してください。

## データモデルオブジェクトとサービスを追加 {#add-data-model-objects-and-services}

データソースを持つフォームデータモデルが既に作成されている場合は、フォームデータモデルエディターを使用して、データモデルオブジェクトとサービスの追加、各種プロパティの設定、データモデルオブジェクト間の関連付けの定義、フォームデータモデルとサービスのテストをおこなうことができます。

フォームデータモデル内の使用可能なデータソースから、データモデルのオブジェクトとサービスを追加できます。 追加したデータモデルオブジェクトは「モデル」タブに表示され、追加したサービスは「サービス」タブに表示されます。

データモデルオブジェクトとサービスを追加するには、以下の手順を実行します。

1. AEM オーサーインスタンスにログインして&#x200B;**[!UICONTROL フォーム／データ統合]**&#x200B;に移動し、データモデルオブジェクトを追加するフォームデータモデルを開きます。
1. データソースペインでデータソースを展開して、使用可能なデータモデルオブジェクトとサービスを表示します。
1. フォームデータモデルに追加するデータモデルオブジェクトとサービスを選択し、「 」を選択します。 **[!UICONTROL 選択項目を追加]**.

   ![selected-objects](assets/selected-objects.png)

   選択されたデータモデルオブジェクトとサービス

   >[!NOTE]
   >
   > Forms データモデルにリレーショナルデータベースの予約済みキーワードであるオブジェクトが含まれている場合、データの追加、更新または取得に関する問題が発生する可能性があります。そのため、そのようなオブジェクトはフォームデータモデルで使用しないようにしてください。

   「モデル」タブには、フォームデータモデルに追加されたすべてのデータモデルオブジェクトのグラフィカル表現と、それらのオブジェクトのプロパティが表示されます。フォームデータモデル内の各データモデルオブジェクトは、ボックスを使用して表現されます。

   ![model-tab](assets/model-tab.png)

   追加したデータモデルオブジェクトが表示された「モデル」タブ

   >[!NOTE]
   >
   >データモデルオブジェクトのボックスを選択してドラッグすると、コンテンツ領域内にデータモデルオブジェクトを配置できます。フォームデータモデルに追加されたデータモデルオブジェクトは、データソースペイン内ではすべてグレーアウトされます。

   「サービス」タブには、追加されたサービスが一覧表示されます。

   ![services-tab](assets/services-tab.png)

   データモデルサービスが表示された「サービス」タブ

   >[!NOTE]
   >
   >OData サービスのメタデータドキュメントには、データモデルオブジェクトとサービスのほかに、2 つのデータモデルオブジェクト間の関連付けを定義するナビゲーションプロパティが含まれます。詳しくは、[OData サービスのナビゲーションプロパティの操作](#work-with-navigation-properties-of-odata-services)を参照してください。

1. 選択 **[!UICONTROL 保存]** フォームモデルオブジェクトを保存します。

   >[!NOTE]
   >
   >アダプティブフォームのルールを使用すると、フォームデータモデルの「サービス」タブで設定したサービスを呼び出せます。設定したサービスは、ルールエディターの「サービスを起動」アクションで使用できます。設定したサービスをアダプティブフォームルールで使用する方法について詳しくは、[ルールエディター](/help/forms/using/rule-editor.md)でサービスの起動とルールの値の設定を参照してください。

## データモデルオブジェクトと子プロパティの作成 {#create-data-model-objects-and-child-properties}

### データモデルオブジェクトの作成 {#create-data-model-objects}

設定済みのデータソースからデータモデルオブジェクトを追加できますが、データソースのないデータモデルオブジェクトやデータモデルエンティティを作成することもできます。フォームデータモデルでデータソースを設定していない場合は特に便利です。

データソースを使用せずにデータモデルオブジェクトを作成するには：

1. AEM オーサーインスタンスにログインして&#x200B;**[!UICONTROL フォーム／データ統合]**&#x200B;に移動し、データモデルオブジェクトまたはデータモデルエンティティを作成するフォームデータモデルを開きます。
1. 選択 **[!UICONTROL エンティティを作成]**.
1. [ データモデルを作成 ] ダイアログで、データモデルオブジェクトの名前を指定し、を選択します。 **[!UICONTROL 追加]**. データモデルオブジェクトがフォームデータモデルに追加されます。以下の図に示すように、新しく追加されたデータモデルオブジェクトは、データソースには連結されません。また、プロパティも設定されません。

   ![new-entity](assets/new-entity.png)

次に、バインドされていないデータモデルオブジェクトに子プロパティを追加できます。

### 子プロパティの追加 {#child-properties}

フォームデータモデルエディターを使用すると、データモデルオブジェクトで子プロパティを作成できます。作成時のプロパティは、データソース内のどのプロパティにもバインドされません。後で、データモデルオブジェクトを含む別のプロパティにこの子プロパティをバインドできます。

子プロパティを作成するには、以下の手順を実行します。

1. フォームデータモデルで、データモデルオブジェクトを選択し、「 」を選択します。 **[!UICONTROL 子プロパティを作成]**.
1. **[!UICONTROL 子プロパティを作成]**&#x200B;ダイアログで、 プロパティの名前とデータタイプをそれぞれ&#x200B;**[!UICONTROL 名前]**&#x200B;フィールドと&#x200B;**[!UICONTROL タイプ]**&#x200B;フィールドに指定します。必要に応じて、プロパティのタイトルと説明を指定できます。
1. プロパティが計算済みの場合は、「計算済み」を有効にします。計算済みプロパティの値は、ルールまたは式に基づいて評価されます。詳しくは、[プロパティの編集](#edit-properties)を参照してください。
1. データモデルオブジェクトがデータソースにバインドされている場合、追加された子プロパティは、同じ名前とデータタイプを持つ親データモデルオブジェクトのプロパティに自動的にバインドされます。

   子プロパティをデータモデルオブジェクトプロパティに手動で連結するには、 **[!UICONTROL バインド参照]** フィールドに入力します。 **[!UICONTROL オブジェクトの選択]**&#x200B;ダイアログには、親データモデルオブジェクトのすべてのプロパティが一覧表示されます。バインドするプロパティを選択し、チェックマークアイコンを選択します。 なお、子プロパティと同じデータタイプのプロパティしか選択できません。

1. 選択 **[!UICONTROL 完了]** 子プロパティを保存し、「 **[!UICONTROL 保存]** フォームデータモデルを保存するには… これで、子プロパティがデータモデルオブジェクトに追加されました。

データモデルオブジェクトとプロパティを作成したら、続いて、アダプティブフォームとインタラクティブ通信をそのフォームデータモデルに基づいて作成できます。データソースの設定が完了した時点で、フォームデータモデルをデータソースにバインドできます。連結の設定は、関連するアダプティブフォームとインタラクティブ通信内で自動的に更新されます。フォームデータモデルを使用してアダプティブフォームとインタラクティブ通信を作成する方法については、[フォームデータモデルの使用](/help/forms/using/using-form-data-model.md)を参照してください。

### データモデルオブジェクトとプロパティの連結 {#bind-data-model-objects-and-properties}

フォームデータモデルに統合するデータソースが使用可能な状態になったら、[データソースの更新](/help/forms/using/create-form-data-models.md#update)に記載されている説明に従い、データソースをフォームデータモデルに追加することができます。次に、バインドされていないデータモデルオブジェクトとプロパティを以下の手順でバインドします。

1. フォームデータモデルで、データソースへのバインドの対象となるバインドされていないデータソースを選択します。
1. 「**[!UICONTROL プロパティを編集]**」を選択します。
1. Adobe Analytics の **[!UICONTROL プロパティを編集]** ウィンドウで、 **[!UICONTROL 連結]** フィールドに入力します。 フォームデータモデルに追加されたデータソースを一覧表示する&#x200B;**[!UICONTROL オブジェクトを選択]**&#x200B;ダイアログが開きます。

   ![select-object](assets/select-object.png)

1. データソースツリーを展開し、バインドするデータモデルオブジェクトを選択して、チェックマークアイコンを選択します。
1. 選択 **[!UICONTROL 完了]** プロパティを保存し、「 」を選択します。 **[!UICONTROL 保存]** フォームデータモデルを保存します。 これで、データモデルオブジェクトがデータソースにバインドされました。これ以降は、データモデルオブジェクトに「連結されていない」というテキストが表示されることはありません。

   ![bound-model-object](assets/bound-model-object.png)

## サービスの設定 {#configure-services}

データモデルオブジェクトのデータの読み取りと書き込みを行うには、以下の手順を実行して、読み取りサービスと書き込みサービスを設定します。

1. データモデルオブジェクトの上部にあるチェックボックスを選択して、「 」を選択します。 **[!UICONTROL プロパティを編集]**.

   ![edit-properties](assets/edit-properties.png)

   データモデルオブジェクトの読み取りサービスと書き込みサービスの設定を行う「プロパティを編集」

   プロパティ編集ダイアログが表示されます。

   ![edit-properties-2](assets/edit-properties-2.png)

   プロパティを編集ダイアログ

   >[!NOTE]
   >
   >OData サービスのメタデータドキュメントには、データモデルオブジェクトとサービスのほかに、2 つのデータモデルオブジェクト間の関連付けを定義するナビゲーションプロパティが含まれます。OData サービスのデータソースをフォームデータモデルに追加すると、データモデルオブジェクト内のすべてのナビゲーションプロパティに対し、フォームデータモデルでサービスを使用できます。このサービスを使用して、対応するデータモデルオブジェクトのナビゲーションプロパティを読み取ることができます。
   >
   >
   >このサービスの使用について詳しくは、「[OData サービスのナビゲーションプロパティの操作](#work-with-navigation-properties-of-odata-services)」を参照してください。

1. **[!UICONTROL トップレベルオブジェクト]**&#x200B;を切り替えて、データモデルオブジェクトを最上位のモデルオブジェクトにするかどうかを指定します。

   フォームデータモデルで設定したデータモデルオブジェクトは、そのフォームデータモデルに基づくアダプティブフォームのコンテンツブラウザーの「データモデルオブジェクト」タブで使用できるようになります。2 つのデータモデルオブジェクト間の関連付けを追加すると、「データモデルオブジェクト」タブで、関連付け先のデータモデルオブジェクトが、関連付け元のデータモデルオブジェクトの下にネストされます。ネストされたデータモデルが最上位のオブジェクトである場合は、「データモデルオブジェクト」タブにもそのデータモデルが個別に表示されます。そのため、ネストされた階層の内側と外側に 1 つずつデータモデルのエントリが表示されるので、フォームの作成者が混乱する可能性があります。関連するデータモデルオブジェクトをネストされた階層内だけで表示するには、そのデータモデルオブジェクトの「トップレベルオブジェクト」プロパティを無効にします。

1. 選択したデータモデルオブジェクトの読み取りサービスと書き込みサービスを選択します。サービスの引数が表示されます。

   ![read-write-services](assets/read-write-services.png)

   従業員データソースに対して設定されている読み取りサービスと書き込みサービス

1. 選択 ![aem_6_3_edit](assets/aem_6_3_edit.png) 読み取りサービスの引数を [引数をユーザープロファイル属性、要求属性、またはリテラル値にバインドする](#bindargument) 連結値を指定します。
1. 選択 **[!UICONTROL 完了]** 議論を保存する **[!UICONTROL 完了]** プロパティを保存し、 **[!UICONTROL 保存]** フォームデータモデルを保存します。

### バインド読み取りサービスの引数 {#bindargument}

連結値に基づいて、バインド読み取りサービスの引数をユーザープロファイル属性、リクエスト属性またはリテラル値に連結します。この値が引数としてサービスに渡され、指定した値に関連付けられた詳細がデータソースから取得されます。

#### リテラル値 {#literal-value}

**[!UICONTROL 連結先]**&#x200B;ドロップダウンメニューから「**[!UICONTROL リテラル]**」を選択し、「**[!UICONTROL 連結値]**」フィールドに値を入力します。値に関連付けられている詳細がデータソースから取得されます。静的な値に関連付けられた詳細を取得するには、このオプションを使用します。

この例では、**4367655678** に関連付けられた詳細が、`mobilenum` 引数の値としてデータソースから取得されます。モバイル番号の引数に値を渡す場合、関連する詳細には、顧客名、顧客の住所、市区町村などのプロパティを含めることができます。

![リテラル値](assets/fdm_binding_literal_new.png)

#### ユーザープロファイルの属性 {#user-profile-attribute}

**[!UICONTROL 連結先]**&#x200B;ドロップダウンメニューから「**[!UICONTROL ユーザープロファイル属性]**」を選択し、「**[!UICONTROL 連結値]**」フィールドに属性名を入力します。AEM インスタンスにログインしたユーザーの詳細は、属性名に基づいてデータソースから取得されます。

属性名が **[!UICONTROL 連結値]** フィールドには、ユーザーの属性名まで完全なバインディングパスを含める必要があります。 以下の URL を開いて、CRXDE のユーザー詳細にアクセスします。

`https://[server-name]:[port]/crx/de/index.jsp#/home/users/`

![ユーザープロファイル](assets/binding_crxde_user_profile_new.png)

この例では、`grios` ユーザーの「**[!UICONTROL 連結値]**」フィールドに `profile.empid` を指定します。

![引数を編集](assets/edit_argument_user_profile_new.png)

`id` 引数を使用してユーザープロファイルの `empid` 属性の値を取得し、それを引数として読み取りサービスに渡しています。ログインしたユーザーに関連付けられた `empid` の従業員データモデルオブジェクトから、関連付けられたプロパティの値を読み取って返します。

#### リクエスト属性 {#request-attribute}

リクエスト属性を使用して、データソースから関連付けられたプロパティを取得します。

1. **[!UICONTROL 連結先]**&#x200B;ドロップダウンメニューから「**[!UICONTROL リクエスト属性]**」を選択し、「**[!UICONTROL 連結値]**」フィールドに属性名を入力します。

1. head.jsp の[オーバーレイ](../../../help/sites-developing/overlays.md)を作成します。オーバーレイを作成するには、CRX DEを開き、`https://<server-name>:<port number>/crx/de/index.jsp#/libs/fd/af/components/page2/afStaticTemplatePage/head.jsp` ファイルを `https://<server-name>:<port number>/crx/de/index.jsp#/apps/fd/af/components/page2/afStaticTemplatePage/head.jsp` にコピーします

   >[!NOTE]
   >
   >* 静的テンプレートを使用する場合は、head.jsp を以下の場所にオーバーレイします。
   >  `/libs/fd/af/components/page2/afStaticTemplatePage/head.jsp`
   >* 編集可能なテンプレートを使用する場合は、aftemplatedpage.jsp を以下の場所でオーバーレイします。
   >  `/libs/fd/af/components/page2/aftemplatedpage/aftemplatedpage.jsp`

1. リクエスト属性に [!DNL paramMap] を設定します。例えば、apps フォルダーの .jsp ファイルに以下のコードを含めます。

   ```javascript
   <%Map paraMap = new HashMap();
    paraMap.put("<request_attribute>",request.getParameter("<request_attribute>"));
    request.setAttribute("paramMap",paraMap);
   ```

   例えば、以下のコードを使用して、データソースから petid の値を取得します。


   ```javascript
   <%Map paraMap = new HashMap();
   paraMap.put("petId",request.getParameter("petId"));
   request.setAttribute("paramMap",paraMap);%>
   ```

詳細は、リクエストで指定された属性名に基づいてデータソースから取得されます。

例えば、リクエストで属性を `petid=100` と指定すると、属性値に関連付けられたプロパティがデータソースから取得されます。

## 関連付けの追加 {#add-associations}

通常、データソース内のデータモデルオブジェクト間には関連付けが構築されています。この関連付けは、1 対 1 の場合もあれば、1 対多の場合もあります。例えば、1 人の従業員に対して複数の扶養家族を関連付けることができます。これを、1 対多の関連付けといいます。関連するデータモデルオブジェクトを接続するライン上では、「`1:n`」として表示されます。それに対して、特定の従業員 ID で一意の従業員名が返される場合などは、1 対 1 の関連付けになります。

データソース内の関連データモデルオブジェクトをフォームデータモデルに追加した場合、それらの関連付けは維持され、矢印の線で接続された状態で表示されます。フォームデータモデル内の異なる複数のデータソース全体で、データモデルオブジェクト間に関連付けを作成できます。

>[!NOTE]
>
>JDBC データソースの事前定義済みの関連付けは、フォームデータモデルでは保持されません。手動で作成します。

関連付けを追加するには：

1. データモデルオブジェクトの上部にあるチェックボックスを選択して、「 」を選択します。 **[!UICONTROL 関連付けを追加]**. 関連付けを追加ダイアログが表示されます。

   ![add-association](assets/add-association.png)

   >[!NOTE]
   >
   >OData サービスのメタデータドキュメントには、データモデルオブジェクトとサービスのほかに、2 つのデータモデルオブジェクト間の関連付けを定義するナビゲーションプロパティが含まれます。フォームデータモデルで関連付けを追加する際に、これらのナビゲーションプロパティを使用できます。詳しくは、[OData サービスのナビゲーションプロパティの操作](#work-with-navigation-properties-of-odata-services)を参照してください。

   関連付けを追加ダイアログが表示されます。

   ![add-association-2](assets/add-association-2.png)

   関連付けを追加ダイアログ

1. 関連付けを追加ペインで、以下の操作を実行します。

   * 関連付けのタイトルを入力します。
   * 関連付けのタイプ（「1 対 1」または「1 対多」）を選択します。
   * 関連付けるデータモデルオブジェクトを選択します。
   * 選択したモデルオブジェクトからデータを読み取るための読み取りサービスを選択します。読み取りサービスの引数が表示されます。必要に応じて引数を編集し、関連付けるデータモデルオブジェクトのプロパティにその引数をバインドします。

   以下に示す例では、「扶養家族」データモデルオブジェクトの読み取りサービスのデフォルト引数が `dependentid` になっています。

   ![add-association-example](assets/add-association-example.png)

   「扶養家族」読み取りサービスのデフォルト引数が dependentid になっている

   ただし、この引数は、関連付けるデータモデルオブジェクト間の共通プロパティ（この例の場合は `Employeeid`）でなければなりません。そのため、`Employeeid` 引数を「従業員」データモデルオブジェクトの `id` プロパティにバインドして、関連付けられている扶養家族の詳細情報を「扶養家族」データモデルオブジェクトから取得する必要があります。

   ![add-association-example-2](assets/add-association-example-2.png)

   更新後の引数とバインディング

   選択 **[!UICONTROL 完了]** をクリックして、引数を保存します。

1. 選択 **[!UICONTROL 完了]** 関連付けを保存し、 **[!UICONTROL 保存]** フォームデータモデルを保存します。
1. 必要に応じて上記の手順を繰り返し、さらに関連付けを作成します。

>[!NOTE]
>
>追加した関連付けは、入力したタイトルと、関連データモデルオブジェクトを接続する線とともに、データモデルオブジェクトのボックス内に表示されます。
>
>関連付けを編集するには、その関連付けのチェックボックスをオンにして、「 」を選択します **[!UICONTROL 関連付けを編集]**.

![added-association](assets/added-association.png)

## プロパティの編集 {#properties}

フォームデータモデル内で追加されたデータモデルオブジェクト、それらのプロパティおよびサービスのプロパティを編集できます。

プロパティを編集するには：

1. フォームデータモデル内のデータモデルオブジェクト、プロパティまたはサービスの横に表示されているチェックボックスを選択します。
1. 選択 **[!UICONTROL プロパティを編集]**. 選択したモデルオブジェクト、プロパティまたはサービスの&#x200B;**[!UICONTROL プロパティを編集]**&#x200B;ペインが開きます。

   * **データモデルオブジェクト**：読み取りサービスと書き込みサービスを指定し、引数を編集します。
   * **プロパティ**：プロパティのタイプ、サブタイプ、形式を指定します。選択したプロパティをデータモデルオブジェクトのプライマリキーにするかどうかを指定することもできます。
   * **サービス**：サービスの入力モデルオブジェクト、出力タイプおよび引数を指定します。Get サービスの場合は、配列を返すようにするかどうかを指定できます。

   ![edit-properties-service](assets/edit-properties-service.png)

   Get サービスのプロパティを編集ダイアログ

1. 選択 **[!UICONTROL 完了]** プロパティを保存してから **[!UICONTROL 保存]** フォームデータモデルを保存します。

### 計算済みプロパティを作成 {#computed}

計算済みプロパティとは、ルールまたは式に基づいて値が計算されるプロパティのことです。ルールを使用して、計算済みプロパティの値を、リテラル文字列、数値、数式の計算結果、フォームデータモデル内の別のプロパティの値に設定できます。

例えば、既存の **FirstName** プロパティと **LastName** プロパティの値を組み合わせた値を持つ **FullName** という計算済みプロパティを作成することができます。そのためには、以下の手順を実行します。

1. という名前でプロパティを作成します。 `FullName` のデータタイプは String です。
1. 有効にする **[!UICONTROL 計算済み]** を選択し、 **[!UICONTROL 完了]** をクリックしてプロパティを作成します。

   ![計算済み](assets/computed.png)

   FullName という計算済みプロパティが作成されます。このプロパティの横に、計算済みプロパティであることを表すアイコンが表示されます。

   ![computed-prop](assets/computed-prop.png)

1. FullName プロパティを選択し、「 」を選択します。 **[!UICONTROL ルールを編集]**. ルールエディターウィンドウが表示されます。
1. ルールエディターウィンドウで、「 」を選択します。 **[!UICONTROL 作成]**. 「**[!UICONTROL Set Value]**」ルールウィンドウが開きます。

   オプション選択ドロップダウンで、「**[!UICONTROL 数式]**」を選択します。「**[!UICONTROL フォームデータモデルのオブジェクト]**」オプションや「**[!UICONTROL 文字列]**」オプションを選択することもできます。

1. 数式の最初のオブジェクトとして「**[!UICONTROL FirstName]**」を選択し、2 番目のオブジェクトとして「**[!UICONTROL LastName]**」を選択します。演算子として「**[!UICONTROL プラス]**」を選択します。

   選択 **[!UICONTROL 完了]** 次に、「 **[!UICONTROL 閉じる]** をクリックして、ルールエディターウィンドウを閉じます。 ルールは以下のようになります。

   ![ルール](assets/rule.png)

1. フォームデータモデルで、 **[!UICONTROL 保存]**. これで、計算済みプロパティが設定されました。

## OData サービスのナビゲーションプロパティを操作 {#work-with-navigation-properties-of-odata-services}

OData サービスでは、ナビゲーションプロパティを使用して、2 つのデータモデルオブジェクト間の関連付けが定義されます。これらのプロパティは、エンティティタイプまたは複合タイプで定義されます。例えば、サンプルの [TripPin](https://www.odata.org/blog/trippin-new-odata-v4-sample-service/) OData サービスのメタデータファイルから抽出した以下のコードの場合、Friends、BestFriend、Trips という 3 つのナビゲーションプロパティが Person エンティティに含まれています。

ナビゲーションプロパティについて詳しくは、「[OData のドキュメント](https://docs.oasis-open.org/odata/odata/v4.0/errata03/os/complete/part3-csdl/odata-v4.0-errata03-os-part3-csdl-complete.html#_Toc453752536)」を参照してください。

```xml
<edmx:Edmx xmlns:edmx="https://docs.oasis-open.org/odata/ns/edmx" Version="4.0">
<script/>
<edmx:DataServices>
<Schema xmlns="https://docs.oasis-open.org/odata/ns/edm" Namespace="Microsoft.OData.Service.Sample.TrippinInMemory.Models">
<EntityType Name="Person">
<Key>
<PropertyRef Name="UserName"/>
</Key>
<Property Name="UserName" Type="Edm.String" Nullable="false"/>
<Property Name="FirstName" Type="Edm.String" Nullable="false"/>
<Property Name="LastName" Type="Edm.String"/>
<Property Name="MiddleName" Type="Edm.String"/>
<Property Name="Gender" Type="Microsoft.OData.Service.Sample.TrippinInMemory.Models.PersonGender" Nullable="false"/>
<Property Name="Age" Type="Edm.Int64"/>
<Property Name="Emails" Type="Collection(Edm.String)"/>
<Property Name="AddressInfo" Type="Collection(Microsoft.OData.Service.Sample.TrippinInMemory.Models.Location)"/>
<Property Name="HomeAddress" Type="Microsoft.OData.Service.Sample.TrippinInMemory.Models.Location"/>
<Property Name="FavoriteFeature" Type="Microsoft.OData.Service.Sample.TrippinInMemory.Models.Feature" Nullable="false"/>
<Property Name="Features" Type="Collection(Microsoft.OData.Service.Sample.TrippinInMemory.Models.Feature)" Nullable="false"/>
<NavigationProperty Name="Friends" Type="Collection(Microsoft.OData.Service.Sample.TrippinInMemory.Models.Person)"/>
<NavigationProperty Name="BestFriend" Type="Microsoft.OData.Service.Sample.TrippinInMemory.Models.Person"/>
<NavigationProperty Name="Trips" Type="Collection(Microsoft.OData.Service.Sample.TrippinInMemory.Models.Trip)"/>
</EntityType>
```

フォームデータモデル内で OData サービスを設定すると、そのフォームデータモデル内のサービスを経由して、エンティティコンテナ内のすべてのナビゲーションプロパティを使用できるようになります。このサンプルの TripPin OData サービスでは、フォームデータモデル内の `GET LINK` サービスを使用して、`Person` エンティティコンテナに含まれている 3 つのナビゲーションプロパティを読み取ることができます。

以下の図では、フォームデータモデル内の `GET LINK of Person /People` サービスがハイライト表示されています。これは、TripPin OData サービスの `Person` エンティティに含まれている 3 つのナビゲーションプロパティを組み合わせたサービスです。

![nav-prop-service](assets/nav-prop-service.png)

フォームデータモデルの「サービス」タブに `GET LINK` サービスを追加すると、サービス内で使用する出力モデルオブジェクトとナビゲーションプロパティを選択するための各種プロパティを編集できるようになります。例えば、以下の `GET LINK of Person /People` サービスでは、出力モデルオブジェクトとして「Trip」を使用し、ナビゲーションプロパティとして「Trips」を使用しています。

![edit-prop-nav-prop](assets/edit-prop-nav-prop.png)

>[!NOTE]
>
>**NavigationPropertyName** 引数の「**デフォルト値**」フィールドで指定できる値は、「**配列を返しますか？**」トグルボタンの状態によって異なります。このボタンが有効になっている場合は、コレクションタイプのナビゲーションプロパティが表示されます。

この例では、出力モデルオブジェクトとして「Person」を選択し、ナビゲーションプロパティの引数として「Friends」または「BestFriend」を選択することもできます（どちらを選択するかは、「**配列を返しますか？**」ボタンが有効になっているか無効になっているかによって異なります）。

![edit-prop-nav-prop2](assets/edit-prop-nav-prop2.png)

同様に、フォームデータモデルで関連付けを追加する際に `GET LINK` サービスを選択し、サービスのナビゲーションプロパティを設定できます。ただし、ナビゲーションプロパティを選択するには、**[!UICONTROL 連結先]**&#x200B;ドロップダウンメニューで「**リテラル**」に設定されている必要があります。

![add-association-nav-prop](assets/add-association-nav-prop.png)

## サンプルデータの生成と編集 {#sample}

フォームデータモデルエディターを使用して、計算済みプロパティを含むすべてのデータモデルオブジェクトプロパティのサンプルデータを、フォームデータモデル内で生成できます。各プロパティで設定されたデータタイプに基づいて、一連のランダムな値がサンプルデータとして生成されます。このサンプルデータを編集して保存することもできます。サンプルデータを再生成した場合も、編集したサンプルデータは保存されたままになります。

サンプルデータを生成して編集するには、以下の手順を実行します。

1. フォームデータモデルを開き、「 」を選択します。 **[!UICONTROL サンプルデータを編集]**. サンプルデータが生成され、サンプルデータ編集ウィンドウに表示されます。

   ![サンプルデータの生成](assets/form_data_model_generate_sample_data_new.png)

1. In **[!UICONTROL サンプルデータを編集]** ウィンドウ、データを必要に応じて編集し、「 」を選択します。 **[!UICONTROL 保存]**.

次に、サンプルデータを使用し、フォームデータモデルに基づいてインタラクティブ通信にデータを取り込んでテストを実行します。詳しくは、[フォームデータモデルの使用](/help/forms/using/using-form-data-model.md)を参照してください。

## データモデルオブジェクトとサービスのテスト {#test-data-model-objects-and-services}

これまでの手順で設定したフォームデータモデルを使用する前に、設定したデータモデルオブジェクトとサービスが正しく動作するかどうかをテストすることをお勧めします。データモデルオブジェクトとサービスをテストするには、以下の手順を実行します。

1. フォームデータモデル内のデータモデルオブジェクトまたはサービスを選択し、「 」を選択します。 **[!UICONTROL モデルオブジェクトのテスト]** または **[!UICONTROL サービスをテスト]**、それぞれ。

   フォームデータモデルをテストウィンドウが表示されます。

   ![test-data-model](assets/test-data-model.png)

1. フォームデータモデルをテストウィンドウの入力ペインで、テストするデータモデルオブジェクトまたはサービスを選択します。

1. テストコードで引数の値を指定し、「 」を選択します。 **[!UICONTROL テスト]**. テストが成功すると、出力ペインに出力情報が返されます。

   ![テストの結果](assets/test_results_form_data_model_new.png)

同様の方法で、フォームデータモデル内の他のデータモデルオブジェクトやサービスをテストできます。

## 入力データの自動検証 {#automated-validation-of-input-data}

フォームデータモデルは、DermisBridge API を呼び出す際に入力として受け取ったデータを（フォームデータモデルで使用可能な検証条件に基づいて）検証します。検証は、API の呼び出しに使用されるクエリオブジェクトに設定された `ValidationOptions` フラグに基づいて行われます。

このフラグは、以下のいずれかの値に設定できます。

* **完全**：FDM は、すべての制約に基づいて検証を実行します
* **オフ**：検証なし
* **基本**：FDM は、「required」制約および「nullable」制約に基づいて検証を実行します

`ValidationOptions`フラグに値が設定されていない場合、入力データに対して&#x200B;**基本**&#x200B;検証が実行されます。

以下に、検証フラグを&#x200B;**完全**&#x200B;に設定する例を示します。

```java
operationOptions.setValidationOptions(ValidationOptions.FULL);
```

>[!NOTE]
>
>入力データの属性に指定する値は、メタデータドキュメントの属性に定義されているデータタイプと一致する必要があります。\
>値が属性に対して定義されたデータタイプと一致しない場合、DermisBridge API は `ValidationOptions` フラグの値に関係なく例外を表示します。ログレベルが「デバッグ」に設定されている場合は、**error.log** ファイルにエラーが記録されます。

フォームデータモデルは、データタイプ制約のリストに基づいて入力データを検証します。入力データに対する制約のリストは、データソースによって異なる場合があります。

以下の表に、データソースに基づく入力データの制約事項を示します。

<table>
 <tbody> 
  <tr> 
   <td>制約</td> 
   <td>説明</td> 
   <td>入力データソース</td> 
  </tr> 
  <tr> 
   <td>required</td> 
   <td>true の場合、パラメーターを入力データに含める必要があります。</td> 
   <td>Swagger、WSDL およびデータベース</td> 
  </tr> 
  <tr> 
   <td>nullable</td> 
   <td>true の場合、入力データでパラメーターの値を Null に設定できます。</td> 
   <td>WSDL、Odata およびデータベース</td> 
  </tr> 
  <tr> 
   <td>maximum</td> 
   <td>数値の上限を指定します。また、上限として指定した最大値も入力データのパラメーターに割り当てることができます。</td> 
   <td>Swagger および WSDL</td> 
  </tr> 
  <tr> 
   <td>minimum</td> 
   <td>数値の下限を指定します。また、下限として指定した最小値も入力データのパラメーターに割り当てることができます。</td> 
   <td>Swagger および WSDL</td> 
  </tr> 
  <tr> 
   <td>exclusiveMaximum</td> 
   <td>数値の上限を指定します。上限として指定した最大値を入力データのパラメーターに割り当てないでください。</td> 
   <td>Swagger および WSDL</td> 
  </tr> 
  <tr> 
   <td>exclusiveMinimum</td> 
   <td>数値の下限を指定します。下限として指定した最小値を入力データのパラメーターに割り当てないでください。</td> 
   <td>Swagger および WSDL</td> 
  </tr> 
  <tr> 
   <td>minLength</td> 
   <td>文字列に含まれる文字数の下限を指定します。また、下限として指定した最小値も入力データのパラメーターに割り当てることができます。</td> 
   <td>Swagger および WSDL</td> 
  </tr> 
  <tr> 
   <td>maxLength</td> 
   <td>文字列に含まれる文字数の上限を指定します。また、上限として指定した最大値も入力データのパラメーターに割り当てることができます。</td> 
   <td>Swagger、WSDL、Odata およびデータベース</td> 
  </tr> 
  <tr> 
   <td>pattern</td> 
   <td>文字の固定シーケンスを指定します。文字が指定したパターンに適合する場合にのみ、入力文字列が正常に検証されます。</td> 
   <td>Swagger</td> 
  </tr> 
  <tr> 
   <td>minItems</td> 
   <td>配列の項目の最小数を指定します。また、下限として指定した最小値も入力データのパラメーターに割り当てることができます。</td> 
   <td>Swagger および WSDL</td> 
  </tr> 
  <tr> 
   <td>maxItems</td> 
   <td>配列の項目の最大数を指定します。また、上限として指定した最大値も入力データのパラメーターに割り当てることができます。</td> 
   <td>Swagger および WSDL</td> 
  </tr> 
  <tr> 
   <td>uniqueItems</td> 
   <td>true の場合、配列のすべての要素は入力データ内で一意である必要があります。</td> 
   <td>Swagger</td> 
  </tr> 
  <tr> 
   <td>enum（文字列）<br /> <br /> </td> 
   <td>入力データ内のパラメーターの値を固定の文字列の値のセットに制限します。1 つ以上の要素がある配列であり、各要素は一意である必要があります。</td> 
   <td>Swagger、WSDL および Odata</td> 
  </tr> 
  <tr> 
   <td>enum （数値）<br /> <br /> </td> 
   <td>入力データ内のパラメーターの値を、一定の数値のセットに制限します。1 つ以上の要素がある配列であり、各要素は一意である必要があります。</td> 
   <td>WSDL</td> 
  </tr> 
 </tbody> 
</table>

この例では、Swagger ファイルで定義されている最大制約、最小制約、必須制約に基づいて入力データが検証されます。注文 ID が存在し、その値が 1 ～ 10 の場合にのみ、入力データは検証条件を満たします。

```json
   parameters: [
   {
   name: "orderId",
   in: "path",
   description: "ID of pet that needs to be fetched",
   required: true,
   type: "integer",
   maximum: 10,
   minimum: 1,
   format: "int64"
   }
   ]
```

入力データが検証条件を満たさない場合は、例外が表示されます。ログレベルが「**デバッグ**」に設定されている場合は、**error.log** ファイルにエラーが記録されます。例：

```verilog
21.01.2019 17:26:37.411 *ERROR* com.adobe.aem.dermis.core.validation.JsonSchemaValidator {"errorCode":"AEM-FDM-001-044","errorMessage":"Input validations failed during operation execution.","violations":{"/orderId":["numeric instance is greater than the required maximum (maximum: 10, found: 16)"]}}
```

## 次の手順 {#next-steps}

これで、作業用のフォームデータモデルを、アダプティブフォームとインタラクティブ通信のワークフローで使用する準備が整いました。次の手順として、実際にこのフォームデータモデルを使用します。詳しくは、[フォームデータモデルの使用](/help/forms/using/using-form-data-model.md)を参照してください。
