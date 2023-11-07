---
title: Forms の開発（クラシック UI）
seo-title: Developing Forms (Classic UI)
description: Adobe Experience Managerクラシック UI 用のフォームを開発する方法を説明します。
seo-description: Learn how to develop forms
uuid: 33859f29-edc5-4bd5-a634-35549f3b5ccf
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 6ee3bd3b-51d1-462f-b12e-3cbe24898b85
docset: aem65
exl-id: f43e9491-aa8f-40af-9800-123695142559
source-git-commit: fc2f26a69c208947c14e8c6036825bb217901481
workflow-type: tm+mt
source-wordcount: '1946'
ht-degree: 52%

---

# Forms の開発（クラシック UI）{#developing-forms-classic-ui}

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

必要に応じて、[スクリプトを使用して](#developing-scripts-for-use-with-forms)機能を拡張できます。

>[!NOTE]
>
>このドキュメントでは、 [基盤コンポーネント](/help/sites-authoring/default-components-foundation.md) （クラシック UI）を参照してください。 Adobeは、新しい [コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja) および [条件を非表示](/help/sites-developing/hide-conditions.md) タッチ操作対応 UI でのフォーム開発用。

## フォーム値のプリロード {#preloading-form-values}

フォーム開始コンポーネントは、 **読み込みパス**：リポジトリ内のノードを指すオプションのパス。

読み込みパスは、定義済みの値をフォーム上の複数のフィールドに読み込むために使用されるノードプロパティへのパスです。

これは、リポジトリ内のノードへのパスを指定するオプションのフィールドです。 このノードにフィールド名と一致するプロパティがある場合、フォーム上の該当フィールドには、これらのプロパティの値が事前に読み込まれます。一致が存在しない場合、フィールドにはデフォルト値が使用されます。


>[!NOTE]
>
>A [フォームアクション](#developing-your-own-form-actions) また、初期値の読み込み元となるリソースを設定することもできます。 これには、`init.jsp` 内で `FormsHelper#setFormLoadResource` を使用します。
>
>設定されていない場合にのみ、作成者がフォームコンポーネントで設定したパスからフォームに入力します。

### 複数の値を持つフォームフィールドのプリロード {#preloading-form-fields-with-multiple-values}

様々なフォームフィールドにも **項目読み込みパス**&#x200B;リポジトリ内のノードを指すオプションのパス。

The **項目読み込みパス** は、定義済みの値をフォーム上の特定のフィールドに読み込むために使用されるノードプロパティのパスです。例えば、 [ドロップダウンリスト](/help/sites-authoring/default-components-foundation.md#dropdown-list), [チェックボックスグループ](/help/sites-authoring/default-components-foundation.md#checkbox-group) または [ラジオグループ](/help/sites-authoring/default-components-foundation.md#radio-group).

#### 例 — 複数の値を含むドロップダウンリストのプリロード {#example-preloading-a-dropdown-list-with-multiple-values}

コンボボックスは、選択する値の範囲で設定できます。

The **項目読み込みパス** を使用して、リポジトリ内のフォルダーからリストにアクセスし、これらをフィールドにプリロードできます。

1. Sling フォルダー ( `sling:Folder`など ) が含まれます。 `/etc/designs/<myDesign>/formlistvalues`

1. 新しいプロパティを追加します ( 例： `myList`) 型の複数値文字列 ( `String[]`) をクリックして、ドロップダウン項目のリストを含めます。 コンテンツはスクリプト（JSP スクリプトやシェルスクリプトの curl など）を使用してインポートすることもできます。

1. 「**項目読み込みパス**」フィールドにフルパスを使用します。
例：`/etc/designs/geometrixx/formlistvalues/myList`

`String[]` 内の値が次のような形式の場合

* `AL=Alabama`
* `AK=Alaska`
* などなど

次のリストが生成されます。

* `<option value="AL">Alabama</option>`
* `<option value="AK">Alaska</option>`

この機能は、例えば、多言語設定で適切に使用できます。

### 独自のフォームアクションの作成 {#developing-your-own-form-actions}

フォームにはアクションが必要です。アクションは、フォームがユーザーデータと共に送信されたときに実行される操作を定義します。

標準のAEMインストールでは、様々なアクションが提供されます。これらは次の場所に表示されます。

`/libs/foundation/components/form/actions`

および&#x200B;**フォーム**&#x200B;コンポーネントの&#x200B;**アクションタイプ**&#x200B;リストで確認できます。

![chlimage_1-8](assets/chlimage_1-8.png)

この節では、このリストに含める独自のフォームアクションを作成する方法について説明します。

`/apps` に独自のアクションを追加するには、次の手順を実行します。

1. `sling:Folder` タイプのノードを作成します。実装するアクションを反映した名前を指定してください。

   次に例を示します。

   `/apps/myProject/components/customFormAction`

1. このノードで、次のプロパティを定義し、**すべて保存**&#x200B;をクリックして、変更を保存してください。

   * `sling:resourceType` - `foundation/components/form/action` に設定 

   * `componentGroup` - `.hidden` として定義

   * オプション：

      * `jcr:title` - 選択したタイトルを指定します。これは、ドロップダウン選択リストに表示されます。設定されていない場合は、ノード名が表示されます

      * `jcr:description` - 任意の説明を入力します

1. フォルダー内に、ダイアログノードを作成します。

   1. アクションを選択した後で作成者がフォームダイアログを編集できるように、フィールドを追加します。

1. フォルダーで、次のいずれかを作成します。

   1. ポストスクリプト。
スクリプトの名前は `post.POST.<extension>`例： `post.POST.jsp`
フォームを処理するためにフォームが送信されると、post スクリプトが呼び出されます。このスクリプトには、フォームから到着したデータを処理するコードが含まれています `POST`.

   1. フォームが送信されたときに呼び出される転送スクリプトを追加します。
スクリプトの名前は `forward.<extension`>（例： ） `forward.jsp`
このスクリプトは、パスを定義できます。 現在の要求が、指定されたパスに転送されます。

   必要な呼び出しは、`FormsHelper#setForwardPath`（2 つのバリアント）です。通常は、何らかの検証（ロジック）を実行して、ターゲットパスを見つけ、そのパスに転送し、デフォルトの Sling POST サーブレットで JCR への実際の保存を実行できるようにしてください。

   また、フォームアクションと `forward.jsp` が「グルー」コードとしてのみ動作するような場合には、別のサーブレットで実際の処理を実行することもできます。その例として、`/libs/foundation/components/form/actions/mail` にあるメールアクションでは、メールサーブレットが配置されている `<currentpath>.mail.html` に詳細を転送します。

   まとめると、次のようになります。

   * `post.POST.jsp` は、アクション自体によって完全に実行される小さな操作に便利です。
   * `forward.jsp` は、委任のみが必要な場合に便利です。

   スクリプトは次の順序で実行されます。

   * フォームのレンダリング時（`GET`）：

      1. `init.jsp`
      1. すべてのフィールドの制約に対して：`clientvalidation.jsp`
      1. フォームの validationRT：`clientvalidation.jsp`
      1. 設定されている場合は、読み込みリソースを介してフォームが読み込まれます
      1. `<form></form>`の内部レンダリング時に`addfields.jsp`

   * フォームの処理時（`POST`）：

      1. `init.jsp`
      1. すべてのフィールドの制約に対して：`servervalidation.jsp`
      1. フォームの validationRT：`servervalidation.jsp`
      1. `forward.jsp`
      1. 転送パスが設定されていた場合（`FormsHelper.setForwardPath`）、リクエストを転送し、その後、`cleanup.jsp` を呼び出します

      1. 転送パスを設定しなかった場合は、`post.POST.jsp` を呼び出します（ここで終了し、`cleanup.jsp` は呼び出しません）

1. 再び必要に応じてフォルダーに以下を追加します。

   1. フィールドを追加するためのスクリプト。
スクリプトの名前は `addfields.<extension>`例： `addfields.jsp`
An `addfields` スクリプトは、フォーム開始のHTMLが記述された直後に呼び出されます。 これにより、カスタム入力フィールドなどの HTML をフォーム内に追加するアクションを実行できます。

   1. 初期化スクリプト。
スクリプトの名前は `init.<extension>`例： `init.jsp`
このスクリプトは、フォームがレンダリングされると呼び出されます。 このスクリプトを使用して、アクションの詳細を初期化できます。

   1. クリーンアップスクリプト。
スクリプトの名前は `cleanup.<extension>`例： `cleanup.jsp`
このスクリプトを使用してクリーンアップを実行できます。

1. 以下を使用します。 **Forms** parsys 内のコンポーネント。 The **アクションタイプ** ドロップダウンに新しいアクションが含まれます。

   >[!NOTE]
   >
   >製品に含まれるデフォルトのアクションを表示するには：
   >
   >
   >`/libs/foundation/components/form/actions`

### 独自のフォーム制約の作成 {#developing-your-own-form-constraints}

制約は次の 2 つのレベルで適用できます。

* の場合 [個々のフィールド（以下の手順を参照）](#constraints-for-individual-fields)
* As [フォームグローバル検証](#form-global-constraints)

#### 個々のフィールドの制約 {#constraints-for-individual-fields}

（`/apps` に）個々のフィールドの独自の制約を追加するには、次の手順を実行します。

1. `sling:Folder` タイプのノードを作成します。実装する制約を反映した名前を指定します。

   次に例を示します。

   `/apps/myProject/components/customFormConstraint`

1. このノードで、次のプロパティを定義し、「**すべて保存**」をクリックして、変更を保存します。

   * `sling:resourceType` - `foundation/components/form/constraint` に設定

   * `constraintMessage`  — フォームが送信されたときに、制約に従ってフィールドが有効でない場合に表示される、カスタマイズされたメッセージ

   * 省略可能：

      * `jcr:title` - 選択したタイトルを指定します。これは選択リストに表示されます。設定されていない場合は、ノード名が表示されます
      * `hint` - ユーザーに向けたフィールドの使用方法に関する追加情報

1. このフォルダー内には、少なくとも次のどちらかのスクリプトが必要です。

   * クライアント検証スクリプト：スクリプトの名前は次のとおりです。 `clientvalidation.<extension>`例： `clientvalidation.jsp`
これは、フォームフィールドがレンダリングされると呼び出されます。 このスクリプトを使用すると、クライアントでフィールドを検証するクライアント JavaScript を作成できます。

   * サーバー検証スクリプト：スクリプトの名前は次のとおりです。 `servervalidation.<extension>`例： `servervalidation.jsp`
これは、フォームが送信されると呼び出されます。 この変数は、送信後にサーバー上のフィールドを検証するために使用できます。

>[!NOTE]
>
>サンプル制約は、次の場所に表示されます。
>
>`/libs/foundation/components/form/constraints`

#### フォームグローバル制約 {#form-global-constraints}

フォームグローバル検証は、開始フォームコンポーネントでリソースタイプを設定することで指定します（`validationRT`）。次に例を示します。

`apps/myProject/components/form/validation`

その後、以下を定義できます。

* `clientvalidation.jsp` - フィールドのクライアント検証スクリプトの後に挿入されます。
* `servervalidation.jsp` - `POST` 時の個々のフィールドのサーバー検証後に呼び出されます。

### フォームコンポーネントの表示と非表示 {#showing-and-hiding-form-components}

フォーム内の他のフィールドの値に応じて、フォームのコンポーネントの表示と非表示を切り替えるようにフォームを設定できます。

特定の条件下でのみフィールドが必要とされる場合、フォームフィールドの表示を変更することは役立ちます。例えば、フィードバックフォームで、製品情報を電子メールで顧客に送信したいかどうかを尋ねる質問が発生した場合です。 「はい」を選択すると、顧客が電子メールアドレスを入力できるテキストフィールドが表示されます。

フォームコンポーネントを表示または非表示にする条件を指定するには、**表示 / 非表示のルールを編集**&#x200B;ダイアログボックスを使用します。

![showhider](assets/showhideeditor.png)

ダイアログボックスの上部にあるフィールドを使用して、次の情報を指定します。

* コンポーネントを非表示にするか表示するかの条件を指定するかどうか。
* コンポーネントを表示または非表示にするために、条件のいずれかまたはすべてが true である必要があるかどうか。

これらのフィールドの下に、1 つ以上の条件が表示されます。 条件は、（同じフォーム上の）別のフォームコンポーネントの値と値を比較します。 フィールドの実際の値が条件を満たした場合に、条件が真と評価されます。条件には以下の情報が含まれます。

* テストするフォームフィールドのタイトル。
* 演算子。
* フィールド値に対する値が比較されます。

例えば、タイトル `Receive email notifications?`* * を持つラジオグループコンポーネントは `Yes` および `No` ラジオボタンを含みます。「`Email Address`」というタイトルのテキストフィールドコンポーネントは、次の条件を使用しているので、「`Yes`」を選択した場合に表示されます。

![showhidecondition](assets/showhidecondition.png)

JavaScript では、条件は要素名プロパティの値を使用してフィールドを参照します。 前述の例では、ラジオグループコンポーネントの要素名プロパティは「`contact`」です。次のコードは、この例と同等の JavaScript コードです。

`((contact == "Yes"))`

**フォームコンポーネントを表示または非表示にするには：**

1. 特定のフォームコンポーネントを編集します。

1. 選択 **表示/非表示** 開く **表示/非表示のルールを編集** ダイアログ：

   * 最初のドロップダウンリストで、次のいずれかを選択します。 **表示** または **非表示** を使用して、コンポーネントの表示と非表示を条件で指定します。

   * 上部の行の末尾にあるドロップダウンリストで、次の項目を選択します。

      * **すべて**  — コンポーネントを表示または非表示にするすべての条件が true である必要がある場合
      * **任意** - 1 つ以上の条件のみが true に設定されている場合に、コンポーネントの表示/非表示を切り替えます。

   * 条件行（デフォルトで表示されます）で、コンポーネント、演算子を選択し、値を指定します。
   * 必要に応じて、「 」をクリックしてさらに条件を追加します。 **条件を追加**.

   次に例を示します。

   ![chlimage_1-9](assets/chlimage_1-9.png)

1. 「**OK**」をクリックして、定義を保存します。

1. 定義を保存した後、 **ルールを編集** の横にリンクが表示されます **表示/非表示** オプションを使用して、フォームコンポーネントのプロパティに追加します。 このリンクをクリックして、 **表示/非表示のルールを編集** 変更を加えるダイアログボックス

   クリック **OK** をクリックして、すべての変更を保存します。

   ![chlimage_1-10](assets/chlimage_1-10.png)

   >[!CAUTION]
   >
   >表示／非表示の定義の効果は、以下で確認およびテストできます。
   >
   >* オーサー環境の&#x200B;**プレビュー**&#x200B;モード（最初にプレビューに切り替えるときに、ページをリロードする必要があります）
   >
   >* パブリッシュ環境で

#### 壊れたコンポーネント参照の処理 {#handling-broken-component-references}

表示／非表示の条件では、要素名プロパティの値を使用して、フォーム内の他のコンポーネントを参照します。いずれかの条件で、削除されたコンポーネントまたは要素名プロパティが変更されたコンポーネントを参照している場合、表示／非表示の設定は無効になります。その場合は、手動で条件を更新する必要があります。更新しないと、フォームの読み込み時にエラーが発生します。

表示／非表示の設定が無効な場合、その設定は JavaScript コードとしてのみ提供されます。コードを編集して、問題を修正します。そのコードでは、コンポーネントを参照するために元々使用していた要素名プロパティを使用しています。

### Forms で使用するスクリプトの作成 {#developing-scripts-for-use-with-forms}

スクリプトを記述する際に使用できる API 要素について詳しくは、[フォームに関連する javadoc](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/foundation/forms/package-summary.html) を参照してください。

これは、フォームが送信される前にサービスを呼び出し、呼び出しに失敗した場合にサービスをキャンセルするなどのアクションに使用できます。

* 検証リソースタイプを定義します。
* 検証用のスクリプトを含めます。

   * JSP で、web サービスを呼び出し、エラーメッセージを含む `com.day.cq.wcm.foundation.forms.ValidationInfo` オブジェクトを作成します。エラーが発生した場合、フォームデータはポストされません。
