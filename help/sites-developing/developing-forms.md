---
title: Forms の開発（クラシック UI）
seo-title: Developing Forms (Classic UI)
description: フォームの作成方法について説明します
seo-description: Learn how to develop forms
uuid: 33859f29-edc5-4bd5-a634-35549f3b5ccf
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 6ee3bd3b-51d1-462f-b12e-3cbe24898b85
docset: aem65
exl-id: f43e9491-aa8f-40af-9800-123695142559
source-git-commit: 4df14f837569997c3e4da8161ac2b099c39d89a6
workflow-type: tm+mt
source-wordcount: '1942'
ht-degree: 97%

---

# Forms の開発（クラシック UI）{#developing-forms-classic-ui}

フォームの基本的な構造は次のとおりです。

* フォーム開始
* フォームエレメント
* フォーム終了

これらはすべて、一連のデフォルトで実現されます [フォームコンポーネント](/help/sites-authoring/default-components.md#form)：標準のAEMインストールで使用できます。

フォームで使用する[新しいコンポーネントを開発する](/help/sites-developing/developing-components-samples.md)ほかに、次のこともできます。

* [フォームに値をプリロードする](#preloading-form-values)
* [（特定の）フィールドに複数値をプリロードする](#preloading-form-fields-with-multiple-values)
* [新しいアクションを作成する](#developing-your-own-form-actions)
* [新しい制約を作成する](#developing-your-own-form-constraints)
* [特定のフォームフィールドを表示または非表示にする](#showing-and-hiding-form-components)

必要に応じて、[スクリプトを使用して](#developing-scripts-for-use-with-forms)機能を拡張できます。

>[!NOTE]
>
>このドキュメントでは、クラシック UI の[基盤コンポーネント](/help/sites-authoring/default-components-foundation.md)を使用したフォームの作成に重点を置いて説明します。アドビでは、タッチ操作対応 UI でのフォーム作成に新しい[コアコンポーネント](https://docs.adobe.com/content/help/ja-JP/experience-manager-core-components/using/introduction.html)と[非表示の条件](/help/sites-developing/hide-conditions.md)を使用することをお勧めします。

## フォーム値のプリロード {#preloading-form-values}

フォーム開始コンポーネントには、**読み込み元パス**（リポジトリ内のノードを指すオプションのパス）を指定するフィールドがあります。

読み込み元パスとは、定義済みの値をフォーム上の複数のフィールドに読み込むために使用するノードプロパティのパスです。

これは、リポジトリ内のノードへのパスを指定するオプションのフィールドです。このノードに、フィールド名と一致するプロパティがある場合、フォーム上の適切なフィールドがそのプロパティの値が設定された状態でプリロードされます。一致が存在しない場合、フィールドにはデフォルト値が使用されます。


>[!NOTE]
>
>[フォームアクション](#developing-your-own-form-actions)で初期値の読み込み元となるリソースを設定することもできます。これには、`init.jsp` 内で `FormsHelper#setFormLoadResource` を使用します。
>
>設定されていない場合にのみ、作成者がフォーム開始コンポーネントに設定したパスからフォームに値が読み込まれます。

### フォームフィールドへの複数値のプリロード {#preloading-form-fields-with-multiple-values}

様々なフォームフィールドには、**項目読み込みパス**（リポジトリ内のノードを指すオプションのパス）もあります。

**項目読み込みパス**&#x200B;とは、定義済みの値をフォーム上の特定のフィールド（[ドロップダウンリスト](/help/sites-authoring/default-components-foundation.md#dropdown-list)、[チェックボックスグループ](/help/sites-authoring/default-components-foundation.md#checkbox-group)、[ラジオグループ](/help/sites-authoring/default-components-foundation.md#radio-group)など）に読み込むために使用するノードプロパティのパスです。

#### 例 - ドロップダウンリストへの複数値のプリロード {#example-preloading-a-dropdown-list-with-multiple-values}

ドロップダウンリストは、選択肢の値を提供するように設定できます。

「**項目読み込みパス**」を使用すると、リポジトリ内のフォルダーからリストにアクセスし、リストの値をフィールドにプリロードできます。

1. 新しい sling フォルダー（`sling:Folder`）を作成する
例：`/etc/designs/<myDesign>/formlistvalues`

1. ドロップダウンアイテムのリストを格納する複数値文字列タイプ（`String[]`）の新しいプロパティ（`myList` など）を追加します。コンテンツはスクリプト（JSP スクリプトやシェルスクリプトの curl など）を使用してインポートすることもできます。

1. 「**項目読み込みパス**」フィールドにフルパスを使用します。
例：`/etc/designs/geometrixx/formlistvalues/myList`

`String[]` 内の値が次のような形式の場合

* `AL=Alabama`
* `AK=Alaska`
* 等。

次のリストが生成されます。

* `<option value="AL">Alabama</option>`
* `<option value="AK">Alaska</option>`

この機能は、多言語設定などに適しています。

### 独自のフォームアクションの作成 {#developing-your-own-form-actions}

フォームにはアクションが必要です。アクションでは、ユーザーデータが入力されたフォームが送信されたときに実行する操作を定義します。

標準の AEM インストールに用意されている一連のアクションは、

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

      * `jcr:title` - 選択したタイトルを指定します。これは、ドロップダウン選択リストに表示されます。 設定されていない場合は、ノード名が表示されます

      * `jcr:description` - 任意の説明を入力します

1. フォルダーにダイアログノードを作成します。

   1. アクションを選択したら、作成者がフォームダイアログを編集できるようにフィールドを追加します。

1. フォルダーに次のどちらかを作成します。

   1. ポストスクリプト。
スクリプトの名前は `post.POST.<extension>` にします（例：`post.POST.jsp`）
ポストスクリプトは、フォームが処理のために送信されたときに呼び出されます。フォーム  
`POST`から受け取ったデータを処理するコードを含めます。

   1. フォームが送信されたときに呼び出される転送スクリプトを追加します。
スクリプトの名前は `forward.<extension`（例：`forward.jsp`）にします
このスクリプトでは、パスを定義できます。現在の要求が、指定されたパスに転送されます。
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
An 
`addfields` スクリプトは、フォーム開始のHTMLが記述された直後に呼び出されます。 これにより、カスタム入力フィールドなどの HTML をフォーム内に追加するアクションを実行できます。

   1. 初期化スクリプト。
スクリプトの名前は `init.<extension>` にします（例：`init.jsp`）
このスクリプトは、フォームのレンダリング時に呼び出されます。このスクリプトを使用して、アクションの詳細を初期化できます。

   1. クリーンアップスクリプト。
スクリプトの名前は `cleanup.<extension>` にします（例：`cleanup.jsp`）
このスクリプトを使用して、クリーンアップを実行できます。

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

#### 個々のフィールドの制約 {#constraints-for-individual-fields}

（`/apps` に）個々のフィールドの独自の制約を追加するには、次の手順を実行します。

1. `sling:Folder` タイプのノードを作成します。実装する制約を反映した名前を指定します。

   次に例を示します。

   `/apps/myProject/components/customFormConstraint`

1. このノードで、次のプロパティを定義し、「**すべて保存**」をクリックして、変更を保存します。

   * `sling:resourceType` - `foundation/components/form/constraint` に設定

   * `constraintMessage` - フォームの送信時に、制約に照らしてフィールドが無効な場合に表示されるカスタマイズされたメッセージ

   * 省略可能：

      * `jcr:title` - 選択したタイトルを指定します。これは選択リストに表示されます。 設定されていない場合は、ノード名が表示されます
      * `hint` - ユーザーに向けたフィールドの使用方法に関する追加情報

1. このフォルダー内には、少なくとも次のどちらかのスクリプトが必要です。

   * クライアント検証スクリプト：
スクリプトの名前は `clientvalidation.<extension>` です（例： `clientvalidation.jsp`）
これは、フォームフィールドをレンダリングすると呼び出されます。 このスクリプトを使用すると、クライアントでフィールドを検証するクライアント JavaScript を作成できます。

   * サーバー検証スクリプト：
スクリプトの名前は `servervalidation.<extension>` です（例： `servervalidation.jsp`）
これは、フォームを送信すると呼び出されます。 このスクリプトを使用すると、フォームの送信後にサーバーでフィールドを検証できます。

>[!NOTE]
>
>サンプルの制約は、以下で確認できます。
>
>`/libs/foundation/components/form/constraints`

#### フォームグローバル制約 {#form-global-constraints}

フォームグローバル検証は、開始フォームコンポーネントでリソースタイプを設定することで指定します（`validationRT`）。次に例を示します。

`apps/myProject/components/form/validation`

その後、以下を定義できます。

* `clientvalidation.jsp` - フィールドのクライアント検証スクリプトの後に挿入されます。
* `servervalidation.jsp` - `POST` 時の個々のフィールドのサーバー検証後に呼び出されます。

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

例えば、タイトル `Receive email notifications?`* *を持つラジオグループコンポーネントは `Yes` および `No` ラジオボタンを含みます。 「`Email Address`」というタイトルのテキストフィールドコンポーネントは、次の条件を使用しているので、「`Yes`」を選択した場合に表示されます。

![showhidecondition](assets/showhidecondition.png)

JavaScript の場合、条件にはエレメント名プロパティの値を使用して、フィールドを参照します。前述の例では、ラジオグループコンポーネントのエレメント名プロパティは「`contact`」です。次のコードは、前の例と同等の JavaScript コードです。

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
   >* オーサー環境の&#x200B;**プレビュー**&#x200B;モード（最初にプレビューに切り替えるときに、ページをリロードする必要があります）
   >
   >* パブリッシュ環境


#### 壊れたコンポーネント参照の処理 {#handling-broken-component-references}

表示／非表示の条件では、エレメント名プロパティの値を使用して、フォーム内の他のコンポーネントを参照します。いずれかの条件で、削除されたコンポーネントまたはエレメント名プロパティが変更されたコンポーネントを参照している場合、表示／非表示の設定は無効になります。その場合は、手動で条件を更新する必要があります。更新しないと、フォームの読み込み時にエラーが発生します。

表示／非表示の設定が無効な場合、その設定は JavaScript コードとしてのみ提供されます。コードを編集して、問題を修正します。そのコードでは、コンポーネントを参照するために元々使用していたエレメント名プロパティを使用しています。

### Forms で使用するスクリプトの作成 {#developing-scripts-for-use-with-forms}

スクリプトを記述する際に使用できる API エレメントについて詳しくは、[フォームに関連する javadoc](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/foundation/forms/package-summary.html) を参照してください。

これは、フォームが送信される前にサービスを呼び出し、呼び出しに失敗した場合にサービスをキャンセルするなどのアクションに使用できます。

* 検証リソースタイプを定義します。
* 検証用のスクリプトを含めます。

   * JSP で、web サービスを呼び出し、エラーメッセージを含む `com.day.cq.wcm.foundation.forms.ValidationInfo` オブジェクトを作成します。エラーが発生した場合、フォームデータはポストされません。
