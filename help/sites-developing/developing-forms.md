---
title: フォームの作成（クラシック UI）
seo-title: フォームの作成（クラシック UI）
description: フォームの作成方法について説明します
seo-description: フォームの作成方法について説明します
uuid: 33859f29-edc5-4bd5-a634-35549f3b5ccf
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 6ee3bd3b-51d1-462f-b12e-3cbe24898b85
docset: aem65
exl-id: f43e9491-aa8f-40af-9800-123695142559
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1952'
ht-degree: 76%

---

# フォームの作成（クラシック UI）{#developing-forms-classic-ui}

フォームの基本的な構造は次のとおりです。

* フォーム開始
* フォームエレメント
* フォーム終了

これらはすべて、標準の AEM インストールで利用できるデフォルトの一連の[フォームコンポーネント](/help/sites-authoring/default-components.md#form)を使用して実現されます。

フォームで使用する[新しいコンポーネントを開発する](/help/sites-developing/developing-components-samples.md)ほかに、次のこともできます。

* [フォームに値をプリロードする](#preloading-form-values)
* [（特定の）フィールドに複数値をプリロードする](#preloading-form-fields-with-multiple-values)
* [新しいアクションを作成する](#developing-your-own-form-actions)
* [新しい制約を作成する](#developing-your-own-form-constraints)
* [特定のフォームフィールドを表示または非表示にする](#showing-and-hiding-form-components)

必要に応じて、[スクリプトを使用して](#developing-scripts-for-use-with-forms)、機能を拡張できます。

>[!NOTE]
>
>このドキュメントでは、クラシック UI の[基盤コンポーネント](/help/sites-authoring/default-components-foundation.md)を使用したフォームの作成に重点を置いて説明します。アドビでは、タッチ操作対応 UI でのフォーム作成に新しい[コアコンポーネント](https://docs.adobe.com/content/help/ja/experience-manager-core-components/using/introduction.html)と[非表示の条件](/help/sites-developing/hide-conditions.md)を使用することをお勧めします。

## フォーム値のプリロード  {#preloading-form-values}

フォーム開始コンポーネントには、**読み込み元パス**（リポジトリ内のノードを指すオプションのパス）を指定するフィールドがあります。

読み込み元パスとは、定義済みの値をフォーム上の複数のフィールドに読み込むために使用するノードプロパティのパスです。

これは、リポジトリ内のノードへのパスを指定するオプションのフィールドです。このノードに、フィールド名と一致するプロパティがある場合、フォーム上の適切なフィールドがそのプロパティの値が設定された状態でプリロードされます。一致が存在しない場合、フィールドにはデフォルト値が使用されます。

>[!NOTE]
>
>[フォームアクション](#developing-your-own-form-actions)で初期値の読み込み元となるリソースを設定することもできます。これは、`init.jsp`内の`FormsHelper#setFormLoadResource`を使用して行います。
>
>設定されていない場合にのみ、作成者がフォーム開始コンポーネントに設定したパスからフォームに値が読み込まれます。

### フォームフィールドへの複数値のプリロード  {#preloading-form-fields-with-multiple-values}

様々なフォームフィールドには、**項目読み込みパス**（リポジトリ内のノードを指すオプションのパス）もあります。

**項目読み込みパス**&#x200B;とは、定義済みの値をフォーム上の特定のフィールド（[ドロップダウンリスト](/help/sites-authoring/default-components-foundation.md#dropdown-list)、[チェックボックスグループ](/help/sites-authoring/default-components-foundation.md#checkbox-group)、[ラジオグループ](/help/sites-authoring/default-components-foundation.md#radio-group)など）に読み込むために使用するノードプロパティのパスです。

#### 例 - ドロップダウンリストへの複数値のプリロード {#example-preloading-a-dropdown-list-with-multiple-values}

ドロップダウンリストは、選択肢の値を提供するように設定できます。

「**項目読み込みパス**」を使用すると、リポジトリ内のフォルダーからリストにアクセスし、リストの値をフィールドにプリロードできます。

1. 新しいslingフォルダー(`sling:Folder`)を作成します。
例： `/etc/designs/<myDesign>/formlistvalues`

1. 複数値の文字列(`String[]`)型の新しいプロパティ（例えば、`myList`）を追加して、ドロップダウン項目のリストを含めます。 コンテンツはスクリプト（JSP スクリプトやシェルスクリプトの curl など）を使用してインポートすることもできます。

1. **Items Load Path**フィールドでフルパスを使用します。
例： `/etc/designs/geometrixx/formlistvalues/myList`

`String[]`内の値が次のような形式の場合は、

* `AL=Alabama`
* `AK=Alaska`
* *等。*

次のリストが生成されます。

* `<option value="AL">Alabama</option>`
* `<option value="AK">Alaska</option>`

この機能は、多言語設定などに適しています。

### 独自のフォームアクションの作成  {#developing-your-own-form-actions}

フォームにはアクションが必要です。アクションでは、ユーザーデータが入力されたフォームが送信されたときに実行する操作を定義します。

標準の AEM インストールに用意されている一連のアクションは、

`/libs/foundation/components/form/actions`

および&#x200B;**フォーム**&#x200B;コンポーネントの「**アクションタイプ**」リストで確認できます。

![chlimage_1-8](assets/chlimage_1-8.png)

この節では、このリストに含める独自のフォームアクションを作成する方法について説明します。

`/apps`の下に独自のアクションを追加するには、次の手順を実行します。

1. `sling:Folder`型のノードを作成します。実装するアクションを反映する名前を指定します。

   次に例を示します。

   `/apps/myProject/components/customFormAction`

1. このノードで、次のプロパティを定義し、「**すべて保存**」をクリックして、変更を保存します。

   * `sling:resourceType`  — 次のように設定します。  `foundation/components/form/action`

   * `componentGroup`  — 次のように定義します。  `.hidden`

   * 省略可能：

      * `jcr:title` ：選択したタイトルを指定します。これは、ドロップダウン選択リストに表示されます。設定されていない場合は、ノード名が表示されます

      * `jcr:description`  — 選択した説明を入力します

1. フォルダーにダイアログノードを作成します。

   1. アクションを選択したら、作成者がフォームダイアログを編集できるようにフィールドを追加します。

1. フォルダーに次のどちらかを作成します。

   1. ポストスクリプト。スクリプトの名前は`post.POST.<extension>`です。例：`post.POST.jsp`
フォームを処理するためにフォームが送信されると、postスクリプトが呼び出されます。このスクリプトには、フォームから到着したデータを処理するコードが含まれます 
`POST`

   1. フォームが送信されたときに呼び出される転送スクリプトを追加します。スクリプトの名前は`forward.<extension`です。例：`forward.jsp`
このスクリプトはパスを定義できます。 現在の要求が、指定されたパスに転送されます。
   必要な呼び出しは`FormsHelper#setForwardPath` （2つのバリアント）です。 通常は、何らかの検証（ロジック）を実行して、ターゲットパスを見つけ、そのパスに転送し、デフォルトの Sling POST サーブレットで JCR への実際の保存を実行できるようにします。

   また、フォームアクションと `forward.jsp` が「グルー」コードとしてのみ動作するような場合には、別のサーブレットで実際の処理を実行することもできます。例えば、`/libs/foundation/components/form/actions/mail`のメールアクションは、メールサーブレットが配置されている`<currentpath>.mail.html`に詳細を転送します。

   まとめると、次のようになります。

   * `post.POST.jsp` は、アクション自体によって完全に実行される小さな操作に便利です。
   * `forward.jsp` は、委任のみが必要な場合に便利です。

   スクリプトは次の順序で実行されます。

   * フォームのレンダリング時(`GET`):

      1. `init.jsp`
      1. すべてのフィールドの制約に対して、次の操作を行います。`clientvalidation.jsp`
      1. フォームのvalidationRT:`clientvalidation.jsp`
      1. 設定されている場合は、読み込みリソースを介してフォームが読み込まれます
      1. `addfields.jsp` レンダリングの中で  `<form></form>`
   * フォーム`POST`の処理時：

      1. `init.jsp`
      1. すべてのフィールドの制約に対して、次の操作を行います。`servervalidation.jsp`
      1. フォームのvalidationRT:`servervalidation.jsp`
      1. `forward.jsp`
      1. 転送パスが設定されていた場合（`FormsHelper.setForwardPath`）、要求を転送し、その後、`cleanup.jsp` を呼び出します

      1. 転送パスが設定されていなかった場合、`post.POST.jsp` を呼び出します（ここで終了し、`cleanup.jsp` は呼び出されません）




1. 必要に応じて、再びフォルダーに以下を追加します。

   1. フィールドを追加するためのスクリプト。スクリプトの名前は`addfields.<extension>`です。例：`addfields.jsp`
addfieldsスクリプトは、フォーム開始のHTMLが書き込まれた直後に呼び出されます。 これにより、カスタム入力フィールドなどの HTML をフォーム内に追加するアクションを実行できます。

   1. 初期化スクリプト。スクリプトの名前は`init.<extension>`です。例：`init.jsp`
このスクリプトは、フォームがレンダリングされると呼び出されます。 これを使用して、アクションの詳細を初期化できます。&quot;

   1. クリーンアップスクリプト。スクリプトの名前は`cleanup.<extension>`です。例：`cleanup.jsp`
このスクリプトを使用してクリーンアップを実行できます。

1. parsys でこの&#x200B;**フォーム**&#x200B;コンポーネントを使用します。これで「**アクションタイプ**」ドロップダウンに新しいアクションが含まれるようになります。

   >[!NOTE]
   >
   >製品に用意されているデフォルトのアクションは、以下で確認できます。
   >
   >
   >`/libs/foundation/components/form/actions`

### 独自のフォーム制約の作成 {#developing-your-own-form-constraints}

制約は、次の 2 つのレベルで課すことができます。

* [個々のフィールド（次の手順を参照してください）](#constraints-for-individual-fields)
* [フォームグローバル検証](#form-global-constraints)

#### 個々のフィールドの制約  {#constraints-for-individual-fields}

個々のフィールド（`/apps`の下）に独自の制約を追加するには、次の手順を実行します。

1. `sling:Folder`型のノードを作成します。実装する制約を反映する名前を指定します。

   次に例を示します。

   `/apps/myProject/components/customFormConstraint`

1. このノードで、次のプロパティを定義し、「**すべて保存**」をクリックして、変更を保存します。

   * `sling:resourceType`  — に設定  `foundation/components/form/constraint`

   * `constraintMessage` - フォームの送信時に、制約に照らしてフィールドが無効な場合に表示されるカスタマイズされたメッセージ

   * 省略可能：

      * `jcr:title` ：選択したタイトルを指定します。これは選択リストに表示されます。設定されていない場合は、ノード名が表示されます
      * `hint` - ユーザーに向けたフィールドの使用方法に関する追加情報

1. このフォルダー内には、少なくとも次のどちらかのスクリプトが必要です。

   * クライアント検証スクリプト：
スクリプトの名前は`clientvalidation.<extension>`です。例：`clientvalidation.jsp`
これは、フォームフィールドがレンダリングされると呼び出されます。 このスクリプトを使用すると、クライアントでフィールドを検証するクライアント JavaScript を作成できます。

   * サーバー検証スクリプト：
スクリプトの名前は`servervalidation.<extension>`です。例：`servervalidation.jsp`
これは、フォームの送信時に呼び出されます。 このスクリプトを使用すると、フォームの送信後にサーバーでフィールドを検証できます。

>[!NOTE]
>
>サンプルの制約は、以下で確認できます。
>
>`/libs/foundation/components/form/constraints`

#### フォームグローバル制約 {#form-global-constraints}

フォームグローバル検証は、開始フォームコンポーネントでリソースタイプを設定することで指定します（`validationRT`）。次に例を示します。

`apps/myProject/components/form/validation`

その後、以下を定義できます。

* a `clientvalidation.jsp` — フィールドのクライアント検証スクリプトの後に挿入されます
* と`servervalidation.jsp` - `POST`での個々のフィールドサーバーの検証後にも呼び出されます。

### フォームコンポーネントの表示と非表示 {#showing-and-hiding-form-components}

フォーム内の他のフィールドの値に応じてフォームコンポーネントの表示と非表示が切り替わるようにフォームを設定できます。

フォームフィールドの表示の変更は、フィールドが特定の条件のみで必要となる場合に便利です。例えば、フィードバックフォームで、顧客に電子メールで製品情報を送信してよいかを尋ねて、顧客が「はい」を選択すると、顧客が電子メールアドレスを入力できるテキストフィールドが表示されるような場合です。

フォームコンポーネントを表示または非表示にする条件を指定するには、**表示 / 非表示のルールを編集**&#x200B;ダイアログボックスを使用します。

![showhider](assets/showhideeditor.png)

ダイアログボックスの最上部にあるフィールドを使用して、次の情報を指定します。

* コンポーネントの表示または非表示に関する条件を指定するかどうか
* コンポーネントを表示または非表示にするのは、条件のいずれかが満たされた場合か、すべてが満たされた場合か

1 つ以上の条件がこれらのフィールドの下に表示されます。条件では、ある値に対して、同じフォーム上の別のフォームコンポーネントの値が比較されます。フィールドの実際の値が条件を満たした場合に、条件が真と評価されます。条件には以下の情報が含まれます。

* 評価するフォームフィールドのタイトル。
* 演算子
* フィールドの値と比較する値

例えば、タイトルが`Receive email notifications?`* *のラジオグループコンポーネントには、`Yes`と`No`のラジオボタンが含まれます。 「`Email Address`」というタイトルのテキストフィールドコンポーネントは、次の条件を使用しているので、「`Yes`」が選択された場合に表示されます。

![showhidecondition](assets/showhidecondition.png)

JavaScript の場合、条件にはエレメント名プロパティの値を使用して、フィールドを参照します。前の例では、ラジオグループコンポーネントのエレメント名プロパティは`contact`です。 次のコードは、前の例と同等の JavaScript コードです。

`((contact == "Yes"))`

**フォームコンポーネントを表示または非表示にするには：**

1. 特定のフォームコンポーネントを編集します。

1. 「**表示 / 非表示**」を選択して、**表示 / 非表示のルールを編集**&#x200B;ダイアログを開きます。

   * 最初のドロップダウンリストで、「**表示**」または「**非表示**」を選択して、条件に応じてコンポーネントを表示するか、非表示にするかを指定します。

   * 一番上の行の末尾にあるドロップダウンリストで、次のどちらかを選択します。

      * **すべて** - すべての条件を満たした場合に、コンポーネントが表示または非表示になります。
      * **いずれか** - 1 つでも条件を満たした場合に、コンポーネントが表示または非表示になります。
   * 条件行で（デフォルトとして 1 つだけ表示されます）、コンポーネントと演算子を選択し、値を指定します。
   * 必要に応じて、「**条件を追加**」をクリックして、条件を追加します。

   次に例を示します。

   ![chlimage_1-9](assets/chlimage_1-9.png)

1. 「**OK**」をクリックして、定義を保存します。

1. 定義を保存すると、フォームコンポーネントプロパティの「**表示 / 非表示**」オプションの横に「**ルールを編集**」リンクが表示されます。そのリンクをクリックすると、**表示 / 非表示のルールを編集**&#x200B;ダイアログボックスが開いて、変更できます。

   「**OK**」をクリックして、すべての変更を保存します。

   ![chlimage_1-10](assets/chlimage_1-10.png)

   >[!CAUTION]
   >
   >表示／非表示の定義の効果は、以下で確認およびテストできます。
   >
   >
   >
   >    * 作成環境の&#x200B;**プレビュー**&#x200B;モード（最初にプレビューに切り替えるときに、ページをリロードする必要があります）
      >
      >    
   * パブリッシュ環境


#### 壊れたコンポーネント参照の処理  {#handling-broken-component-references}

表示／非表示の条件では、エレメント名プロパティの値を使用して、フォーム内の他のコンポーネントを参照します。表示/非表示の設定は、削除されたコンポーネントや、要素名プロパティが変更されたコンポーネントを参照する条件がある場合に無効になります。 その場合は、手動で条件を更新する必要があります。更新しないと、フォームの読み込み時にエラーが発生します。

表示/非表示の設定が無効な場合、設定はJavaScriptコードとしてのみ提供されます。 コードを編集して、問題を修正します。そのコードでは、コンポーネントを参照するために元々使用していたエレメント名プロパティを使用しています。

### フォームで使用するスクリプトの作成 {#developing-scripts-for-use-with-forms}

スクリプトを記述する際に使用できる API エレメントについて詳しくは、[フォームに関連する javadoc](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/foundation/forms/package-summary.html) を参照してください。

これは、フォームが送信される前にサービスを呼び出し、呼び出しに失敗した場合にサービスをキャンセルするなどのアクションに使用できます。

* 検証リソースタイプを定義します。
* 検証用のスクリプトを含めます。

   * JSP で、Web サービスを呼び出し、エラーメッセージを含む `com.day.cq.wcm.foundation.forms.ValidationInfo` オブジェクトを作成します。エラーが発生した場合、フォームデータはポストされません。
