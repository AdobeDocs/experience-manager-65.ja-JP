---
title: フォームデータモデルの操作
seo-title: フォームデータモデルの操作
description: データ統合機能には、フォームデータモデルの設定と操作を行うためのフォームデータモデルエディターが付属しています。
seo-description: データ統合機能には、フォームデータモデルの設定と操作を行うためのフォームデータモデルエディターが付属しています。
uuid: ed78f7f7-8123-4778-9252-89924cec09d6
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c47ef627-261e-4b4b-8846-873d3d84234b
docset: aem65
translation-type: tm+mt
source-git-commit: 39ae3d8348b0c149c047c9fb3ac2eb673b610645
workflow-type: tm+mt
source-wordcount: '4162'
ht-degree: 59%

---


# フォームデータモデルの操作{#work-with-form-data-model}

![データ統合](do-not-localize/data-integeration.png)

フォームデータモデルエディターには、フォームデータモデルの編集と設定を行うための直感的なユーザーインターフェイスが用意されています。エディターを使用すると、フォームデータモデル内の関連するデータソースから、データモデルのオブジェクト、プロパティおよびサービスを追加および設定できます。 また、データソースを持っていないデータモデルオブジェクトとプロパティを作成し、後でそれらのオブジェクトとプロパティにデータソースを連結することもできます。さらに、データモデルオブジェクトのプロパティ用にサンプルデータを生成して編集し、これらのプロパティを使用してアダプティブフォームとインタラクティブ通信にデータを取り込み、プレビュー表示することもできます。フォームデータモデル内で設定したデータモデルオブジェクトとサービスのテストを実行することにより、そのフォームデータモデルがデータソースと正しく統合されているかどうかを確認することができます。

AEM Forms のデータ統合機能を初めて使用する場合や、これまでにデータソースの設定やフォームデータモデルの作成を行ったことがない場合は、以下のトピックを参照してください。

* [AEM Forms のデータ統合機能](/help/forms/using/data-integration.md)
* [データソースの設定](/help/forms/using/configure-data-sources.md)
* [フォームデータモデルを作成する](/help/forms/using/create-form-data-models.md)

ここからは、フォームデータモデルエディターを使用して各種の操作や設定を行う方法について説明します。

>[!NOTE]
>
>You must be a member of both **fdm-author** and **forms-user** groups to be able to create and work with form data model. これらのグループのメンバーになるには、AEM の管理者に依頼してください。

## データモデルオブジェクトとサービスの追加 {#add-data-model-objects-and-services}

データソースを使用してフォームデータモデルを作成した場合、フォームデータモデルエディターを使用してデータモデルのオブジェクトとサービスを追加し、そのプロパティを設定し、データモデルオブジェクト間の関連付けを構築し、フォームデータモデルとサービスをテストできます。

フォームデータモデル内の有効なデータソースを使用して、データモデルオブジェクトとサービスを追加することができます。追加したデータモデルオブジェクトは「モデル」タブに表示され、追加したサービスは「サービス」タブに表示されます。

データモデルのオブジェクトおよびサービスを追加するには：

1. AEM オーサーインスタンスにログインして&#x200B;**[!UICONTROL フォーム／データ統合]**&#x200B;に移動し、データモデルオブジェクトを追加するフォームデータモデルを開きます。
1. データソースウィンドウで、データソースを展開して、使用可能な表示データモデルのオブジェクトおよびサービスに移動します。
1. フォームデータモデルに追加するデータモデルオブジェクトとサービスを選択して、「**[!UICONTROL 選択項目を追加]**」をタップします。

   ![selected-objects](assets/selected-objects.png)

   選択されたデータモデルオブジェクトとサービス

   「モデル」タブには、フォームデータモデルに追加されたすべてのデータモデルオブジェクトのグラフィカル表現と、それらのオブジェクトのプロパティが表示されます。フォームデータモデル内の各データモデルオブジェクトは、ボックスを使用して表現されます。

   ![model-tab](assets/model-tab.png)

   追加したデータモデルオブジェクトが表示された「モデル」タブ

   >[!NOTE]
   >
   >データモデルオブジェクトのボックスを選択してドラッグすると、コンテンツ領域内にデータモデルオブジェクトを配置することができます。フォームデータモデルに追加されたデータモデルオブジェクトは、データソースペインではすべて灰色表示になっています。

   「サービス」タブには、追加されたサービスが一覧表示されます。

   ![services-tab](assets/services-tab.png)

   データモデルサービスが表示された「サービス」タブ

   >[!NOTE]
   >
   >OData サービスのメタデータドキュメントには、データモデルオブジェクトとサービスのほかに、2 つのデータモデルオブジェクト間の関連付けを定義するナビゲーションプロパティが含まれます。詳しくは、「[OData サービスのナビゲーションプロパティの操作](#navigation-properties-odata)」を参照してください。

1. 「**[!UICONTROL 保存]**」をタップして、フォームモデルオブジェクトを保存します。

   >[!NOTE]
   >
   >アダプティブフォームのルールを使用して、フォームデータモデルの「サービス」タブで設定したサービスを呼び出すことができます。設定したサービスは、ルールエディターの「サービスを起動」アクションで使用することができます。設定したサービスをアダプティブフォームルールで使用する方法については、「[ルールエディター](/help/forms/using/rule-editor.md)」で、「サービスを起動」ルールと「指定値」ルールに関する説明を参照してください。

## データモデルオブジェクトと子プロパティの作成 {#create-data-model-objects-and-child-properties}

### データモデルオブジェクトの作成 {#create-data-model-objects}

設定済みデータソースからデータモデルオブジェクトを追加することができますが、データソースを持っていないデータモデルオブジェクトやデータモデルエンティティを作成することもできます。この方法は、フォームデータモデル内でデータソースが設定されていない場合に使用すると、特に便利です。

データソースを持っていないデータモデルオブジェクトを作成するには、以下の手順を実行します。

1. AEM オーサーインスタンスにログインして&#x200B;**[!UICONTROL フォーム／データ統合]**&#x200B;に移動し、データモデルオブジェクトまたはデータモデルエンティティを作成するフォームデータモデルを開きます。
1. 「**[!UICONTROL エンティティを作成]**」をタップします。
1. フォームデータモデル作成ダイアログで、データモデルオブジェクトの名前を指定して「**[!UICONTROL 追加]**」をタップします。データモデルオブジェクトがフォームデータモデルに追加されます。新しく追加されたデータモデルオブジェクトは、データソースに連結されず、次の図に示すようなプロパティも持たないことに注意してください。

   ![new-entity](assets/new-entity.png)

次に、データソースに連結されていないデータモデルオブジェクトで、子プロパティを追加します。

### 子プロパティの追加 {#child-properties}

フォームデータモデルエディターを使用して、データモデルオブジェクト内で子プロパティを作成することができます。作成した時点では、子プロパティはデータソース内のどのプロパティにも連結されません。作成した子プロパティは、データモデルオブジェクト内の別のプロパティに後で連結することができます。

子プロパティを作成するには、以下の手順を実行します。

1. In a form data model, select a data model object and tap **[!UICONTROL Create Child Property]**.
1. **[!UICONTROL 子プロパティを作成]**&#x200B;ダイアログの「**[!UICONTROL 名前]**」フィールドと「**[!UICONTROL タイプ]**」フィールドで、子プロパティの名前とタイプを指定します。必要に応じて、子プロパティのタイトルと説明を指定することもできます。
1. 作成するプロパティが計算済みプロパティの場合は、「計算済み」を有効にします。計算済みプロパティの値は、ルールまたは式に基づいて評価されます。詳しくは、「[プロパティの編集](#edit-properties)」を参照してください。
1. データモデルオブジェクトをデータソースに連結すると、追加した子プロジェクトが親データモデルオブジェクトのプロパティに自動的に連結されます。その際、子プロパティの名前とデータタイプは変わりません。

   子プロパティをデータモデルオブジェクトのプロパティに手動で連結するには、「**[!UICONTROL 参照をバインド]**」フィールドの横に表示されている参照アイコンをタップします。**[!UICONTROL オブジェクトの選択]**&#x200B;ダイアログに、親データモデルオブジェクトのすべてのプロパティが一覧表示されます。連結するプロパティを選択して、チェックマークアイコンをタップします。子プロパティと異なるデータタイプのプロパティを選択することはできないことに注意してください。

1. 「**[!UICONTROL 完了]**」をタップして子プロパティを保存し、「**[!UICONTROL 保存]**」タップしてフォームデータモデルを保存します。これで、子プロパティがデータモデルオブジェクトに追加されました。

データモデルオブジェクトとプロパティを作成したら、フォームデータモデルに基づいて、アダプティブフォームとインタラクティブ通信を作成することができます。データソースの設定が完了した時点で、フォームデータモデルをデータソースに連結することができます。連結の設定は、関連するアダプティブフォームとインタラクティブ通信内で自動的に更新されます。For more information about creating adaptive forms and interactive communications using form data model, see [Use form data model](/help/forms/using/using-form-data-model.md).

### データモデルオブジェクトとプロパティの連結 {#bind-data-model-objects-and-properties}

When the data sources you want to integrate with the form data model are available, you can add them to the form data model as described in [Update data sources](/help/forms/using/create-form-data-models.md#update). その後、以下の手順を実行して、データソースに連結されていないデータモデルオブジェクトとプロパティを連結します。

1. フォームデータモデルで、データソースに連結するデータソースを選択します。
1. 「**[!UICONTROL プロパティを編集]**」をタップします。
1. **[!UICONTROL プロパティを編集]**&#x200B;ペインで、「**[!UICONTROL 連結]**」フィールドの横に表示されている参照アイコンをタップします。この操作により、**[!UICONTROL オブジェクトの選択]**&#x200B;ダイアログが表示されます。このダイアログには、フォームデータモデル内に追加されたデータソースが一覧表示されます。

   ![select-object](assets/select-object.png)

1. データソースツリーを展開し、連結するデータモデルオブジェクトを選択してチェックマークアイコンをタップします。
1. 「**[!UICONTROL 完了]**」をタップしてプロパティを保存し、「**[!UICONTROL 保存]**」をタップしてフォームデータモデルを保存します。これで、データモデルオブジェクトがデータソースに連結されました。データモデルオブジェクトが「連結なし」とマークされなくなったことに注意してください。

   ![bound-model-object](assets/bound-model-object.png)

## サービスの設定 {#configure-services}

データモデルオブジェクトのデータの読み取りと書き込みを行うには、以下の手順を実行して、読み取りサービスと書き込みサービスを設定します。

1. データモデルオブジェクト上部のチェックボックスを選択して「**[!UICONTROL プロパティを編集]**」をタップします。

   ![edit-properties](assets/edit-properties.png)

   データモデルオブジェクトの読み取りサービスと書き込みサービスの設定を行う「プロパティを編集」

   プロパティを編集ダイアログが表示されます。

   ![edit-properties-2](assets/edit-properties-2.png)

   プロパティを編集ダイアログ

   >[!NOTE]
   >
   >OData サービスのメタデータドキュメントには、データモデルオブジェクトとサービスのほかに、2 つのデータモデルオブジェクト間の関連付けを定義するナビゲーションプロパティが含まれます。OData サービスのデータソースをフォームデータモデルに追加すると、フォームデータモデルでデータモデルオブジェクト内のすべてのナビゲーションプロパティが有効になるサービスを使用できます。このサービスを使用して、対応するデータモデルオブジェクトのナビゲーションプロパティを読み取ることができます。
   >
   >
   >このサービスの使用について詳しくは、「[OData サービスのナビゲーションプロパティの操作](#navigation-properties-odata)」を参照してください。

1. 「**[!UICONTROL トップレベルオブジェクト]**」を切り替えて、データモデルオブジェクトを最上位のモデルオブジェクトにするかどうかを指定します。

   フォームデータモデルで設定したデータモデルオブジェクトは、そのフォームデータモデルに基づいて、アダプティブフォームのコンテンツブラウザーの「データモデルオブジェクト」タブで使用することができます。2 つのデータモデルオブジェクト間の関連付けを追加すると、「データモデルオブジェクト」タブで、関連付け先のデータモデルオブジェクトが、関連付け元のデータモデルオブジェクトの下にネストされます。ネストされたデータモデルが最上位のオブジェクトである場合は、「データモデルオブジェクト」タブにもそのデータモデルが個別に表示されます。この場合、ネストされた階層の内側と外側に 1 つずつデータモデルのエントリが表示されるため、フォームの作成者が混乱する可能性があります。関連するデータモデルオブジェクトをネストされた階層内だけで表示するには、そのデータモデルオブジェクトの「トップレベルオブジェクト」プロパティを無効にします。

1. 選択したデータモデルオブジェクトの読み取りサービスと書き込みサービスを選択します。各サービスの引数が表示されます。

   ![読み取り/書き込みサービス](assets/read-write-services.png)

   従業員データソースに対して設定されている読み取りサービスと書き込みサービス

1. Tap ![aem_6_3_edit](assets/aem_6_3_edit.png) for the read service argument to [bind the argument to a User Profile Attribute, Request Attribute, or Literal value](#bindargument) and specify the binding value.
1. 「**[!UICONTROL 完了]**」をタップして引数を保存し、もう一度「**[!UICONTROL 完了]**」をタップしてプロパティを保存します。次に、「**[!UICONTROL 保存]**」をタップしてフォームデータモデルを保存します。

### Bind Readサービスの引数 {#bindargument}

バインディング値に基づいて、Bind Readサービス引数をUserプロファイル属性、Request属性またはLiteral値に連結します。 この値が引数としてサービスに渡され、指定した値に関連付けられた詳細がデータソースから取得されます。

#### リテラル値 {#literal-value}

「 **[!UICONTROL Binding To]** 」ドロップダウンメニューから「 **[!UICONTROL Literal]** 」を選択し、「 **[!UICONTROL Binding Value]** 」フィールドに値を入力します。 値に関連付けられている詳細がデータソースから取得されます。 静的な値に関連付けられた詳細を取得するには、このオプションを使用します。

この例では、4367655678に関連付けられ **た詳細が、**`mobilenum` 引数の値としてデータソースから取得されます。 モバイル番号の引数に値を渡す場合、関連する詳細には、顧客名、顧客の住所、市区町村などのプロパティを含めることができます。

![リテラル値](assets/fdm_binding_literal_new.png)

#### ユーザープロファイルの属性 {#user-profile-attribute}

「 **[!UICONTROL 連結先]** 」ドロップダウンメニューから「 **[!UICONTROL ユーザープロファイル属性]** 」を選択し、「連 **[!UICONTROL 結値]** 」フィールドに属性名を入力します。 AEMインスタンスにログインしたユーザーの詳細は、属性名に基づいてデータソースから取得されます。

「 **[!UICONTROL 連結値]** 」フィールドで指定する属性名には、ユーザーの属性名までの完全な連結パスを含める必要があります。 次のURLを開いて、CRXDEのユーザー詳細にアクセスします。

`https://[server-name]:[port]/crx/de/index.jsp#/home/users/`

![ユーザープロファイル](assets/binding_crxde_user_profile_new.png)

この例では、 `profile.empid` ユーザーの「 **[!UICONTROL 連結値]**`grios` 」フィールドにを指定します。

![引数を編集](assets/edit_argument_user_profile_new.png)

The `id` argument takes the value of the `empid` attribute of the user profile and pass it as an argument to the Read service. ログインしたユーザーに関連付けられた従業員データモデルオブジェクトから、関連付けられたプロパティの値を読み取って返し `empid` ます。

#### 属性を要求 {#request-attribute}

request属性を使用して、データソースから関連付けられたプロパティを取得します。

1. 「 **[!UICONTROL 連結先」ドロップダウンメニューから「]** 要求属性 **[!UICONTROL 」を選択し、「]** 連結値 **** 」フィールドに属性名を入力します。

1. head.jspの [オーバーレイを作成します](../../../help/sites-developing/overlays.md) 。 オーバーレイを作成するには、CRX DEを開き、 `https://<server-name>:<port number>/crx/de/index.jsp#/libs/fd/af/components/page2/afStaticTemplatePage/head.jsp` ファイルを `https://<server-name>:<port number>/crx/de/index.jsp#/apps/fd/af/components/page2/afStaticTemplatePage/head.jsp`

   >[!NOTE]
   >
   > * 静的テンプレートを使用する場合は、head.jspを次の場所にオーバーレイします。/libs/fd/af/components/page2/afStaticTemplatePage/head.jsp
   > * 編集可能なテンプレートを使用する場合は、aftemplatedpage.jspを次の場所でオーバーレイします。/libs/fd/af/components/page2/aftemplatedpage/aftemplatedpage.jsp


1. リクエスト属性 [!DNL paramMap] に設定します。 例えば、appsフォルダーの.jspファイルに次のコードを含めます。

   ```javascript
   <%Map paraMap = new HashMap();
    paraMap.put("<request_attribute>",request.getParameter("<request_attribute>"));
    request.setAttribute("paramMap",paraMap);
   ```

   例えば、次のコードを使用して、データソースからpetidの値を取得します。


   ```javascript
   <%Map paraMap = new HashMap();
   paraMap.put("petId",request.getParameter("petId"));
   request.setAttribute("paramMap",paraMap);%>
   ```

詳細は、リクエストで指定された属性名に基づいてデータソースから取得されます。

例えば、リクエストでと同じように属性を指定 `petid=100` すると、データソースから属性値に関連付けられたプロパティが取得されます。

## 関連付けの追加 {#add-associations}

通常、データソース内のデータモデルオブジェクト間には関連付けが作成されています。この関連付けは、1 対 1 の場合もあれば、1 対多の場合もあります。例えば、1 人の従業員に対して複数の扶養家族を関連付けることができます。これを、 対多の関連付けといいます。関連するデータモデルオブジェクトを接続するライン上では、「`1:n`1:」」として表示されます。それに対して、特定の従業員 ID で一意の従業員名が返される場合などは、1 対 1 の関連付けになります。

データソース内の関連するデータモデルオブジェクトをフォームデータモデルに追加すると、関連付けは保持され、矢印で結ばれた状態で表示されます。 フォームデータモデルでは、異なる複数のデータソース間でデータモデルオブジェクト間に関連付けを追加できます。

>[!NOTE]
>
>JDBC データソース内で事前に定義されている関連付けは、フォームデータモデル内では維持されません。これらの関連付けについては、手動で作成する必要があります。

関連付けを追加するには、以下の手順を実行します。

1. データモデルオブジェクト上部のチェックボックスを選択して「**[!UICONTROL 関連付けを追加]**」をタップします。関連付けを追加ダイアログが表示されます。

   ![追加関連](assets/add-association.png)

   >[!NOTE]
   >
   >OData サービスのメタデータドキュメントには、データモデルオブジェクトとサービスのほかに、2 つのデータモデルオブジェクト間の関連付けを定義するナビゲーションプロパティが含まれます。フォームデータモデルで関連付けを追加する際に、これらのナビゲーションプロパティを使用することができます。詳しくは、「[OData サービスのナビゲーションプロパティの操作](#navigation-properties-odata)」を参照してください。

   関連付けを追加ダイアログが表示されます。

   ![add-association-2](assets/add-association-2.png)

   関連付けを追加ダイアログ

1. 関連付けを追加ペインで、以下の操作を実行します。

   * 関連付けのタイトルを入力します。
   * 関連付けのタイプを「1対1」または「1対多」から選択します。
   * 関連付けるデータモデルオブジェクトを選択します。
   * 選択したモデルオブジェクトからデータを読み取るための読み取りサービスを選択します。読み取りサービスの引数が表示されます。必要に応じて引数を編集し、関連付けるデータモデルオブジェクトのプロパティにその引数をバインドします。

   以下に示す例では、「扶養家族」データモデルオブジェクトの読み取りサービスのデフォルト引数が `dependentid` になっています。

   ![add-association-example](assets/add-association-example.png)

   「扶養家族」読み取りサービスのデフォルト引数が dependentid になっている

   ただし、この引数は、関連付けるデータモデルオブジェクト間の共通プロパティ（この例の場合は `Employeeid`）でなければなりません。Therefore, the `Employeeid` argument must be bound to the `id` property of the Employee data model object to fetch the associated dependents details from the Dependents data model object.

   ![add-association-example-2](assets/add-association-example-2.png)

   更新後の引数とバインド

   「**[!UICONTROL 完了]**」をクックして、引数を保存します。

1. 「**[!UICONTROL 完了]**」をタップして関連付けを保存し、次に「**[!UICONTROL 保存]**」をタップしてフォームデータモデルを保存します。
1. さらに関連付けを作成するには、上記の手順を繰り返します。

>[!NOTE]
>
>追加した関連付けは、入力したタイトルと、関連データモデルオブジェクトを接続する線とともに、データモデルオブジェクトのボックス内に表示されます。
>
>You can edit an association by selecting the checkbox against it and tap **[!UICONTROL Edit Association]**.

![付加結合](assets/added-association.png)

## プロパティの編集 {#properties}

フォームデータモデル内で追加されたデータモデルオブジェクトとサービスのプロパティを編集することができます。

プロパティを編集するには、以下の手順を実行します。

1. フォームデータモデル内のデータモデルオブジェクト、プロパティ、またはサービスの横に表示されているチェックボックスを選択します。
1. 「**[!UICONTROL プロパティを編集]**」をタップします。選択したモデルオブジェクト、プロパティ、またはサービスの「**[!UICONTROL プロパティを編集]**」ペインが表示されます。

   * **データモデルオブジェクト**：読み取りサービスと書き込みサービスを指定し、引数を編集します。
   * **プロパティ**：プロパティのタイプ、サブタイプ、形式を指定します。選択したプロパティをデータモデルオブジェクトのプライマリキーにするかどうかを指定することもできます。
   * **サービス**：サービスの入力モデルオブジェクト、出力タイプ、引数を指定します。Get サービスの場合は、配列を返す必要があるかどうかを指定することができます。

   ![edit-properties-service](assets/edit-properties-service.png)

   Get サービスのプロパティを編集ダイアログ

1. 「**[!UICONTROL 完了]**」をタップしてプロパティを保存し、次に「**[!UICONTROL 保存]**」をタップしてフォームデータモデルを保存します。

### 計算済みプロパティの作成 {#computed}

計算済みプロパティとは、ルールまたは式に基づいて値が計算されるプロパティのことです。ルールを使用して、計算済みプロパティの値を、リテラル文字列、数値、数式の計算結果、フォームデータモデル内の別のプロパティの値に設定することができます。

例えば、**FirstName** プロパティと **LastName** プロパティの値を組み合わせた値を持つ **FullName** プロパティを作成することができます。この作業を行うには：

1. Create a new property with the name `FullName` whose data type is String.
1. 「**[!UICONTROL 計算済み]**」を有効にし、「**[!UICONTROL 完了]**」をタップしてプロパティを作成します。

   ![計算済み](assets/computed.png)

   これにより、FullName という名前の計算済みプロパティが作成されます。このプロパティの横に、計算済みプロパティであることを表すアイコンが表示されます。

   ![computed-prop](assets/computed-prop.png)

1. 「FullName」プロパティを選択して「**[!UICONTROL ルールを編集]**」をタップします。ルールエディターウィンドウが表示されます。
1. ルールエディターウィンドウで、「**[!UICONTROL 作成]**」をタップします。「**[!UICONTROL Set Value]**」ルールウィンドウが表示されます。

   オプション選択ドロップダウンで、「**[!UICONTROL 数式]**」を選択します。「**[!UICONTROL フォームデータモデルのオブジェクト]**」オプションと「**[!UICONTROL 文字列]**」オプションを選択することもできます。

1. 数式の最初のオブジェクトとして「**[!UICONTROL FirstName]**」を選択し、2 番目のオブジェクトとして「**[!UICONTROL LastName]**」を選択します。演算子として「**[!UICONTROL プラス]**」を選択します。

   Tap **[!UICONTROL Done]** and then tap **[!UICONTROL Close]** to close the rule editor window. ルールは以下のようになります。

   ![rule](assets/rule.png)

1. フォームデータモデルで、「**[!UICONTROL 保存]**」をタップします。これで、計算済みプロパティが設定されました。

## OData サービスのナビゲーションプロパティの操作 {#work-with-navigation-properties-of-odata-services}

OData サービスでは、ナビゲーションプロパティを使用して、2 つのデータモデルオブジェクト間の関連付けが定義されます。これらのプロパティは、エンティティタイプまたは複合タイプに対して定義されます。For example, in the following extract from the metadata file of the sample [TripPin](https://www.odata.org/blog/trippin-new-odata-v4-sample-service/) OData sample services, the person entity contains three navigation properties - Friends, BestFriend, and Trips.

ナビゲーションプロパティについて詳しくは、[OData のドキュメント](https://docs.oasis-open.org/odata/odata/v4.0/errata03/os/complete/part3-csdl/odata-v4.0-errata03-os-part3-csdl-complete.html#_Toc453752536)を参照してください。

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

フォームデータモデル内で OData サービスを設定すると、そのフォームデータモデル内のサービスを経由して、エンティティコンテナ内のすべてのナビゲーションプロパティを使用できるようになります。In this example of TripPin OData service, the three navigation properties in the `Person` entity container can be read using one `GET LINK` service in the Form Data Model.

The following highlights the `GET LINK of Person /People` service in the Form Data Model, which is a combined service for the three navigation properties in the `Person` entity of the TripPin OData service.

![nav-prop-service](assets/nav-prop-service.png)

フォームデータモデルの「サービス」タブに `GET LINK` サービスを追加すると、サービス内で使用する出力モデルオブジェクトとナビゲーションプロパティを選択するための各種プロパティを編集できるようになります。For example, the following `GET LINK of Person /People` service in the following example uses Trip as the output model object and the navigation property as Trips.

![edit-prop-nav-prop](assets/edit-prop-nav-prop.png)

>[!NOTE]
>
>The values available in the **Default Value** field of the **NavigationPropertyName** argument depend on the state of the **Return array?**」トグルボタンの状態によって異なります。このボタンが有効になっている場合は、コレクションタイプのナビゲーションプロパティが表示されます。

In this example, you can also choose the output model object as Person and navigation property argument as Friends or BestFriend (depending on whether **Return array?**」ボタンが有効になっているか無効になっているかによって異なります）。

![edit-prop-nav-prop2](assets/edit-prop-nav-prop2.png)

同様に、フォームデータモデルで関連付けを追加する際に `GET LINK` サービスを選択し、サービスのナビゲーションプロパティを設定することができます。ただし、ナビゲーションプロパティを選択するには、「****&#x200B;バインディング先」フィールドが「**リテラル**」に設定されている必要があります。

![add-association-nav-prop](assets/add-association-nav-prop.png)

## サンプルデータの生成と編集 {#sample}

フォームデータモデルエディターを使用して、計算済みプロパティを含むすべてのデータモデルオブジェクトプロパティのサンプルデータを、フォームデータモデル内で生成することができます。各プロパティで設定されたデータタイプに基づいて、一連のランダムな値がサンプルデータとして生成されます。このサンプルデータを編集して保存することもできます。サンプルデータを再生成した場合も、編集したサンプルデータは保存されたままになります。

サンプルデータを生成して編集するには、以下の手順を実行します。

1. フォームデータモデルを開いて「**[!UICONTROL サンプルデータを編集]**」をタップします。サンプルデータが生成され、サンプルデータ編集ウィンドウに表示されます。

   ![サンプルデータの生成](assets/form_data_model_generate_sample_data_new.png)

1. 「**[!UICONTROL サンプルデータを編集]**」ウィンドウでデータを編集して「**[!UICONTROL 保存]**」をタップします。

次に、サンプルデータを使用し、フォームデータモデルに基づいてインタラクティブ通信にデータを取り込んでテストを実行します。詳しくは、「[フォームデータモデルの使用](/help/forms/using/using-form-data-model.md)」を参照してください。

## データモデルオブジェクトとサービスのテスト {#test-data-model-objects-and-services}

これまでの手順で設定したフォームデータモデルを使用する前に、設定したデータモデルオブジェクトとサービスが正しく動作するかどうかをテストすることをお勧めします。データモデルオブジェクトとサービスをテストするには、以下の手順を実行します。

1. フォームデータモデル内のデータモデルオブジェクトまたはサービスを選択し、「**[!UICONTROL モデルオブジェクトをテスト]**」または「**[!UICONTROL サービスをテスト]**」をタップします。

   フォームデータモデルをテストウィンドウが表示されます。

   ![test-data-model](assets/test-data-model.png)

1. 上記のウィンドウの入力ペインで、テストするデータモデルオブジェクトまたはサービスを選択します。

1. テストコードで引数の値を指定して「**[!UICONTROL テスト]**」をタップします。テストが成功すると、出力ペインに出力情報が表示されます。

   ![Test Results](assets/test_results_form_data_model_new.png)

同様の方法で、フォームデータモデル内の他のデータモデルオブジェクトやサービスをテストすることができます。

## 入力データの自動検証 {#automated-validation-of-input-data}

フォームデータモデルは、DateriBridge APIを呼び出すと同時に、入力として受け取ったデータを（フォームデータモデルで使用可能な検証基準に基づいて）検証します。 検証は、APIの呼び出しに使用されるクエリオブジェクトに設定された `ValidationOptions` フラグに基づいて行われます。

このフラグは、次のいずれかの値に設定できます。

* **FULL**:FDMは、すべての制約に基づいて検証を実行します
* **オフ**:検証なし
* **基本**:FDMは、「required」制約と「nullable」制約に基づいて検証を実行します

フ `ValidationOptions`ラグに値が設定されていない場合、 **入力データに対してBASIC** 検証が実行されます。

検証フラグを **FULLに設定する例を次に示します**。

```java
operationOptions.setValidationOptions(ValidationOptions.FULL);
```

>[!NOTE]
>
>入力データの属性に指定する値は、メタデータドキュメントの属性に定義されているデータ型と一致する必要があります。\
>値が属性に対して定義されたデータ型と一致しない場合、DateriBridge APIは `ValidationOptions` フラグの値に関係なく例外を表示します。 ログレベルがDebugに設定されている場合、エラーが **error.log** ファイルに記録されます。

フォームデータモデルは、データ型制約のリストに基づいて入力データを検証します。 入力データに対する制約のリストは、データソースによって異なる場合があります。

次の表に、データソースに基づく入力データの制約事項を示します。

<table>
 <tbody> 
  <tr> 
   <td>制約</td> 
   <td>説明</td> 
   <td>入力データソース</td> 
  </tr> 
  <tr> 
   <td>必須</td> 
   <td>trueの場合、パラメーターは入力データに含める必要があります。</td> 
   <td>Swagger、WSDLおよびデータベース</td> 
  </tr> 
  <tr> 
   <td>nullable</td> 
   <td>trueの場合、入力データでパラメーターの値をNullに設定できます。</td> 
   <td>WSDL、Odata、およびデータベース</td> 
  </tr> 
  <tr> 
   <td>maximum</td> 
   <td>数値の上限を指定します。 上限として指定した最大値は、入力データのパラメーターに割り当てることもできます。</td> 
   <td>SwaggerとWSDL</td> 
  </tr> 
  <tr> 
   <td>minimum</td> 
   <td>数値の下限を指定します。 下限として指定した最小値は、入力データのパラメーターに割り当てることもできます。</td> 
   <td>SwaggerとWSDL</td> 
  </tr> 
  <tr> 
   <td>exclusiveMaximum</td> 
   <td>数値の上限を指定します。 上限として指定する最大値を入力データのパラメーターに割り当てないでください。</td> 
   <td>SwaggerとWSDL</td> 
  </tr> 
  <tr> 
   <td>exclusiveMinimum</td> 
   <td>数値の下限を指定します。 下限として指定する最小値を入力データのパラメーターに割り当てないでください。</td> 
   <td>SwaggerとWSDL</td> 
  </tr> 
  <tr> 
   <td>minLength</td> 
   <td>文字列に含まれる文字数の下限を指定します。 下限として指定した最小値は、入力データのパラメーターに割り当てることもできます。</td> 
   <td>SwaggerとWSDL</td> 
  </tr> 
  <tr> 
   <td>maxLength</td> 
   <td>文字列に含まれる文字数の上限を指定します。 上限として指定した最大値は、入力データのパラメーターに割り当てることもできます。</td> 
   <td>Swagger、WSDL、Odataおよびデータベース</td> 
  </tr> 
  <tr> 
   <td>pattern</td> 
   <td>文字の固定シーケンスを指定します。 文字が指定したパターンに適合する場合にのみ、入力文字列が正常に検証されます。</td> 
   <td>スワガー</td> 
  </tr> 
  <tr> 
   <td>minItems</td> 
   <td>配列内の最小項目数を指定します。 下限として指定した最小値は、入力データのパラメーターに割り当てることもできます。</td> 
   <td>SwaggerとWSDL</td> 
  </tr> 
  <tr> 
   <td>maxItems</td> 
   <td>配列の最大項目数を指定します。 上限として指定した最大値は、入力データのパラメーターに割り当てることもできます。</td> 
   <td>SwaggerとWSDL</td> 
  </tr> 
  <tr> 
   <td>uniqueItems</td> 
   <td>trueの場合、配列のすべての要素は入力データ内で一意である必要があります。</td> 
   <td>スワガー</td> 
  </tr> 
  <tr> 
   <td>enum（文字列）<br /> <br /> </td> 
   <td>入力データ内のパラメーターの値を固定の文字列値のセットに制限します。 要素が1つ以上ある配列であり、各要素は一意である必要があります。</td> 
   <td>Swagger、WSDL、Odata</td> 
  </tr> 
  <tr> 
   <td>enum（数値）<br /> <br /> </td> 
   <td>入力データ内のパラメーターの値を、一定の数値のセットに制限します。 要素が1つ以上ある配列であり、各要素は一意である必要があります。</td> 
   <td>WSDL</td> 
  </tr> 
 </tbody> 
</table>

この例では、Swaggerファイルで定義されている最大制約、最小制約、必須制約に基づいて入力データが検証されます。 注文IDが存在し、その値が1 ～ 10の場合にのみ、入力データが検証条件を満たします。

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

入力データが検証条件を満たさない場合は、例外が表示されます。 ログレベルが **Debugに設定されている場合**、エラーが **error.log** ファイルに記録されます。 例：

```verilog
21.01.2019 17:26:37.411 *ERROR* com.adobe.aem.dermis.core.validation.JsonSchemaValidator {"errorCode":"AEM-FDM-001-044","errorMessage":"Input validations failed during operation execution.","violations":{"/orderId":["numeric instance is greater than the required maximum (maximum: 10, found: 16)"]}}
```

## 次の手順 {#next-steps}

これで、作業用のフォームデータモデルを、アダプティブフォームとインタラクティブ通信のワークフローで使用する準備が整いました。次の手順として、実際にこのフォームデータモデルを使用します。詳しくは、「[フォームデータモデルの使用](/help/forms/using/using-form-data-model.md)」を参照してください。
