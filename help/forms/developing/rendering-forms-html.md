---
title: Forms を HTML としてレンダリング
seo-title: Rendering Forms as HTML
description: Forms サービスを使用し、web ブラウザーからの HTTP リクエストに応じてフォームを HTML としてレンダリングします。 Java API および Web Service API を使用し、フォームを HTML としてレンダリングできます。
seo-description: Use the Forms service to render forms as HTML in response to an HTTP request from a web browser. You can use the Java API and Web Service API to render forms as HTML.
uuid: bd8edb6f-333b-4ceb-9877-618f5377f56f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 669ede46-ea55-444b-a23f-23a86e5aff8e
role: Developer
exl-id: e6887e45-a472-41d4-9620-c56fd5b72b4c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '4150'
ht-degree: 100%

---

# Forms を HTML としてレンダリング {#rendering-forms-as-html}

**このドキュメントのサンプルと例は、JEE 環境の AEM Forms のみを対象としています。**

Forms サービスは、web ブラウザーからの HTTP リクエストに応じて、フォームを HTML としてレンダリングします。 フォームを HTML としてレンダリングする利点の 1 つは、クライアント web ブラウザーが格納されているコンピューターに Adobe Reader、Acrobat、Flash Player（フォームガイド（非推奨）用）が必要ないことです。

フォームを HTML としてレンダリングするには、フォームデザインを XDP ファイルとして保存する必要があります。PDF ファイルとして保存されたフォームデザインは、HTML としてレンダリングできません。 Designer でフォームデザインを開発し、HTML としてレンダリングする場合は、以下の条件を考慮してください。

* フォームに線、ボックス、グリッドを描画するときに、オブジェクトの境界線プロパティを使用しないでください。ブラウザーによっては、 のプレビューで表示されるとおりに境界線が表示されないことがあります。また、オブジェクトが重なって表示されたり、他のオブジェクトを本来の位置から押しのけたりする場合があります。
* 線、長方形、円を使用して、背景を定義できます。
* テキストが収まるよう、必要と思われるサイズより少し大きめにテキストを描画します。一部の web ブラウザーでは、テキストが読みやすく表示されません。

>[!NOTE]
>
>`FormServiceClient` オブジェクトの `(Deprecated) renderHTMLForm` および `renderHTMLForm2` メソッドを使用して TIFF 画像を含むフォームをレンダリングする場合、Internet Explorer または Mozilla Firefox ブラウザーで表示されるレンダリングされたHTML フォームには TIFF 画像が表示されません。これらのブラウザーでは、TIFF 画像のネイティブサポートは提供されていません。

## HTML ページ {#html-pages}

フォームデザインが HTML フォームとしてレンダリングされる場合、各第 2 レベルサブフォームはHTML ページ（パネル）としてレンダリングされます。サブフォームの階層は Designer で表示できます。 ルートサブフォームに属する子サブフォーム（ルートサブフォームのデフォルト名は form1 です）は、パネルのサブフォームです。次に、フォームデザインのサブフォームの例を示します。

```java
     form1
         Master Pages
         PanelSubform1
             NestedDynamicSubform
                 TextEdit1
         PanelSubform2
             TextEdit1
         PanelSubform3
             TextEdit1
         PanelSubform4
             TextEdit1
```

フォームデザインが HTML フォームとしてレンダリングされる場合、パネルは特定のページサイズに制限されません。ダイナミックサブフォームがある場合は、パネルサブフォーム内にネストする必要があります。ダイナミックサブフォームは、無限数の HTML ページに拡張できます。

フォームを HTML フォームとしてレンダリングする場合、ページサイズ （PDF としてレンダリングされるフォームのページ番号付けで必須）は意味を持ちません。 編集可能なレイアウトを含むフォームは HTML ページを無限数まで拡張できるので、マスターページではフッターの使用を避けることが重要です。 マスターページのコンテンツ領域の下にフッターを配置すると、ページ境界を越えてフローする HTML コンテンツが上書きされる場合があります。

`xfa.host.pageUp` および `xfa.host.pageDown` メソッドを使用して、パネル間を明示的に移動する必要があります。ページを変更するには、フォームを Forms サービスに送信し、Forms サービスでフォームをレンダリングしてクライアントデバイス（通常は web ブラウザー）に戻す必要があります。

>[!NOTE]
>
>フォームを Forms サービスに送信し、Forms サービスでフォームをレンダリングしてクライアントデバイスに戻すプロセスは、サーバーへのラウンドトリッピングデータと呼ばれます。

>[!NOTE]
>
>HTML フォーム上の HTML のデジタル署名ボタンの外観をカスタマイズする場合は、fscdigsig.css ファイル（adobe-forms-ds.ear/adobe-forms-ds.war ファイル内）で次のプロパティを変更する必要があります。

**.fsc-ds-ssb**：このスタイルシートは、空白の記号フィールドの場合に適用されます。

**.fsc-ds-ssv**：このスタイルシートは、「有効な記号」フィールドの場合に適用されます。

**.fsc-ds-ssc**：このスタイルシートは、有効な記号フィールドでデータが変更された場合に適用されます。

**.fsc-ds-ssi**：このスタイルシートは、無効な記号フィールドの場合に適用されます。

**.fsc-ds-popup-bg**：このスタイルシートプロパティは使用されていません。

**.fsc-ds-popup-btn**：このスタイルシートプロパティは使用されていません。

## スクリプトの実行 {#running-scripts}

フォームの作成者は、スクリプトをサーバー上で実行するかクライアント上で実行するかを指定します。Forms サービスは、`runAt` 属性を使用してクライアントとサーバー間で分散できるフォームインテリジェンスを実行するための分散イベント処理環境を作成します。この属性やフォームデザイン内でのスクリプトの作成について詳しくは、[Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63_jp) を参照してください。

Forms サービスは、フォームのレンダリング中にスクリプトを実行できます。 その結果、データベースに接続するか、クライアント上で使用できない web サービスに接続することで、フォームにデータを事前入力できます。また、ボタンの `Click` イベントをサーバーで実行するように設定して、クライアントがデータをサーバーにラウンドトリップするようにすることもできます。これにより、ユーザーがフォームを操作している間に、エンタープライズデータベースなどのサーバーリソースを必要とする可能性のあるスクリプトをクライアントが実行できます。HTML フォームの場合、formcalc スクリプトはサーバー上でのみ実行できます。その結果、これらのスクリプトを `server` または `both` で実行するように指定する必要があります。

ページ（パネル）間を移動するフォームは、`xfa.host.pageUp` および `xfa.host.pageDown` メソッドを呼び出すことによって設計できます。このスクリプトはボタンの `Click` イベントに配置され、`runAt` 属性は `Both` に設定されます。`Both` を選択する理由は、（PDF としてレンダリングされるフォームの場合）Adobe Reader や Acrobat がサーバーに移動せずにページを変更でき、HTML フォームがサーバーにデータをラウンドトリップさせずにページを変更できるようにするためです。つまり、あるフォームは Forms サービスに送信され、あるフォームは新しいページを表示する HTML としてレンダリングされます。

スクリプト変数やフォームフィールドには、同じ名前（item など）を付けないことをお勧めします。 Internet Explorer などの一部の web ブラウザーでは、フォームフィールドと同じ名前の変数が初期化されず、スクリプトエラーが発生する場合があります。 フォームフィールドとスクリプト変数に異なる名前を付けることをお勧めします。

ページナビゲーション機能とフォームスクリプトの両方を含む HTML フォームをレンダリングする場合（例えば、フォームがレンダリングされるたびにスクリプトがデータベースからフィールドデータを取得するような場合）、フォームスクリプトが form:ready イベントではなく form:calculate イベント内に配置する必要があります。

form:ready イベントにあるフォームスクリプトは、フォームの最初のレンダリング時に 1 回だけ実行され、以降のページ取得時には実行されません。これに対し、 form:calculate イベントは、フォームがレンダリングされるページナビゲーションごとに実行されます。

>[!NOTE]
>複数ページフォームでは、JavaScript によってページに加えられた変更は、別のページに移動しても保持されません。

フォームを送信する前にカスタムスクリプトを呼び出すことができます。この機能は、使用可能なすべてのブラウザーで機能します。ただし、`Output Type` プロパティが `Form Body` に設定されている HTML フォームをレンダリングする場合にのみ使用できます。`Output Type` が `Full HTML` の場合には機能しません。この機能を設定する手順については、管理ヘルプの「フォームの設定」を参照してください。

フォームを送信する前に、呼び出すコールバック関数を定義する必要があります。ここで、関数の名前は `_user_onsubmit` です。この関数は例外をスローしないと想定されます。例外がスローされても無視されます。JavaScript 関数は HTML の HEAD セクションに配置することをお勧めしますが、`xfasubset.js` を含むスクリプトタグが終わる前であれば任意の場所で宣言できます。

フォームサーバーがドロップダウンリストを含む XDP をレンダリングすると、ドロップダウンリストの作成に加えて、2 つの非表示のテキストフィールドも作成されます。これらのテキストフィールドには、ドロップダウンリストのデータが格納されます（一方にはオプションの表示名が格納され、もう一方にはオプションの値が格納されます）。そのため、ユーザーがフォームを送信するたびに、ドロップダウンリストのデータ全体が送信されます。毎回それほど多くのデータを送信したくない場合は、それを無効にするカスタムスクリプトを作成できます。例：ドロップダウンリストの名前は `drpOrderedByStateProv` で、サブフォームヘッダーの下にラップされます。HTML 入力要素の名前は `header[0].drpOrderedByStateProv[0]` になります。ドロップダウンのデータを格納して送信する非表示フィールドの名前には、`header[0].drpOrderedByStateProv_DISPLAYITEMS_[0] header[0].drpOrderedByStateProv_VALUEITEMS_[0]` という名前が付けられます。

データをポストしない場合は、次の方法でこれらの入力要素を無効にできます。`var __CUSTOM_SCRIPTS_VERSION = 1; //enabling the feature function _user_onsubmit() { var elems = document.getElementsByName("header[0].drpOrderedByStateProv_DISPLAYITEMS_[0]"); elems[0].disabled = true; elems = document.getElementsByName("header[0].drpOrderedByStateProv_VALUEITEMS_[0]"); elems[0].disabled = true; }`

```java
header[0].drpOrderedByStateProv_DISPLAYITEMS_[0] header[0].drpOrderedByStateProv_VALUEITEMS_[0]
```

```java
var __CUSTOM_SCRIPTS_VERSION = 1; //enabling the feature
    function _user_onsubmit() {
    var elems = document.getElementsByName("header[0].drpOrderedByStateProv_DISPLAYITEMS_[0]");
    elems[0].disabled = true;
    elems = document.getElementsByName("header[0].drpOrderedByStateProv_VALUEITEMS_[0]");
    elems[0].disabled = true;
    }
```

## XFA サブセット {#xfa-subsets}

HTML としてレンダリングするフォームデザインを作成する場合は、JavaScript 言語のスクリプトの XFA サブセットにスクリプティングを制限する必要があります。

クライアント上で実行される、またはクライアントとサーバーの両方で実行されるスクリプトは、XFA サブセット内で記述する必要があります。サーバー上で実行されるスクリプトは、完全な XFA スクリプティングモデルを使用でき、FormCalc も使用できます。JavaScript の使用について詳しくは、 [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)を参照してください。

クライアントでスクリプトを実行する場合、表示されている現在のパネルだけがスクリプトを使用できます。例えば、パネル B が表示されているときに、パネル A にあるフィールドに対するスクリプトを記述することはできません。サーバーでスクリプトを実行すると、すべてのパネルにアクセスできます。

また、クライアントで実行するスクリプト内で Scripting Object Model（SOM）式を使用する場合は注意が必要です。クライアントで実行するスクリプトでは、簡単化された SOM 式のサブセットのみをサポートしています。

## イベントのタイミング {#event-timing}

XFA サブセットは、HTML イベントにマップされる XFA イベントを定義します。イベントの計算と検証のタイミングには、動作にわずかな違いがあります。Web ブラウザーでは、フィールドを終了すると、完全な calculate イベントが実行されます。フィールド値を変更した場合、calculate イベントは自動的には実行されません。calculate イベントを強制的に実行するには、`xfa.form.execCalculate` メソッドを呼び出します。

Web ブラウザーでは、validate イベントは、フィールドを終了するかフォームを送信する場合にのみ実行されます。validate イベントを強制的に実行するには `xfa.form.execValidate` メソッドを呼び出します。

Web ブラウザー（Adobe Reader や Acrobat とは異なり）に表示されるフォームは、必須フィールドの XFA null テスト（エラーまたは警告）に準拠しています。

* null テストでエラーが発生し、値を指定せずにフィールドを終了した場合は、メッセージボックスが表示され、「OK」をクリックした後にそのフィールドに再配置されます。
* null テストで警告が生成され、値を指定せずにフィールドを終了した場合、「OK」または「キャンセル」をクリックするように促されます。「OK」は値を指定せずに続行し、「キャンセル」は値を入力するフィールドに戻ります。

null テストについて詳しくは、[Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63) を参照してください。

## フォームボタン {#form-buttons}

「送信」ボタンをクリックすると、フォームデータが Forms サービスに送信され、フォームの処理を終了します。`preSubmit` イベントは、クライアントまたはサーバーで実行するように設定できます。`preSubmit` イベントは、フォーム送信の前に実行されます（クライアント上で実行するように設定されている場合）。それ以外の場合は、`preSubmit` イベントは、フォームの送信中にサーバーで実行されます。`preSubmit` イベントについて詳しくは、[Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63) を参照してください。

ボタンにクライアントサイドのスクリプトが関連付けられていない場合、データがサーバーに送信され、サーバー上で計算が実行されて HTML フォームが再生成されます。ボタンにクライアントサイドのスクリプトが含まれている場合、データはサーバーに送信されず、クライアント側のスクリプトが web ブラウザーで実行されます。

## HTML 4.0 web ブラウザー {#html-4-0-web-browser}

HTML 4.0 のみをサポートする web ブラウザーは、XFA サブセットのクライアントサイドスクリプティングモデルをサポートできません。 HTML 4.0 と MSDHTML または CSS2 HTML の両方で動作するフォームデザインを作成する場合、クライアントで実行するようにマークされたスクリプトは、サーバー上で実際に実行されます。 例えば、HTML 4.0 web ブラウザーで表示されているフォーム上のボタンをユーザーがクリックしたとします。 この場合、フォームデータはクライアントサイドスクリプトが実行されるサーバーに送信されます。

HTML 4.0 のサーバーと、MSDHTML または CSS2HTML 用のクライアントで実行する calculate イベントに、フォームロジックを配置することをお勧めします。

## プレゼンテーションの変更の維持 {#maintaining-presentation-changes}

HTML ページ（パネル）間を移動すると、データの状態のみが保持されます。 背景色や必須フィールド設定などの設定は維持されません（初期設定と異なる場合）。 プレゼンテーションの状態を維持するには、フィールドのプレゼンテーションの状態を表すフィールド（通常は非表示）を作成する必要があります。 非表示のフィールド値に基づいて、プレゼンテーションを変更するフィールドの `Calculate` イベントにスクリプトを追加すると、 HTML ページ（パネル）間を移動するときにプレゼンテーションの状態を維持できます。

次のスクリプトは、`hiddenField` の値に基づいてフィールドの `fillColor` を維持します。このスクリプトがフィールドの `Calculate` イベントにあるとします。

```java
     If (hiddenField.rawValue == 1)
         this.fillColor = "255,0,0"
     else
         this.fillColor = "0,255,0"
```

>[!NOTE]
>テーブルのセル内にネストされている場合、スタティックオブジェクトはレンダリングされた HTML フォームには表示されません。 例えば、テーブルのセル内にネストされた円や長方形は、レンダリングされた HTML フォーム内には表示されません。 ただし、テーブルの外側に配置されている場合は、同じスタティックオブジェクトが正しく表示されます。

## デジタル署名用 HTML フォーム {#digitally-signing-html-forms}

フォームが以下の HTML 変換のいずれかとしてレンダリングされている場合、デジタル署名フィールドを含む HTML 署名フォームには署名できません。

* AHTML
* HTML4
* StaticHTML
* NoScriptXHTML

ドキュメントのデジタル署名については、 [ドキュメントのデジタル署名と認証](/help/forms/developing/digitally-signing-certifying-documents.md)を参照してください。

## アクセシビリティガイドラインに準拠した XHTML フォームのレンダリング {#rendering-an-accessibility-guidelines-compliant-xhtml-form}

アクセシビリティガイドラインに準拠する完全な HTML フォームをレンダリングできます。 つまり、本文タグ内でレンダリングされる HTML フォームとは異なり、フォームは完全な HTML タグ内でレンダリングされます（完全な HTML ページではありません）。

## フォームデータの検証 {#validating-form-data}

フォームを HTML フォームとしてレンダリングする場合、フォームフィールドに対する検証ルールの使用を制限することをお勧めします。 一部の検証ルールは、HTML フォームでサポートされていない可能性があります。 例えば、MM-DD-YYYY という検証パターンを HTMLフォームとしてレンダリングされているフォームデザインの `Date/Time` フィールドに適用する場合、日付が正しく入力されていても、適切に機能しません。 ただし、この検証パターンは、PDF としてレンダリングされているフォームに対しては適切に機能します。

>[!NOTE]
>Forms サービスについて詳しくは、[AEM Forms のサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

## 手順の概要 {#summary-of-steps}

HTMLフォームをレンダリングするには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Forms Client API オブジェクトを作成します。
1. HTML の実行時オプションを設定します。
1. HTML フォームをレンダリングします。
1. フォームデータストリームをクライアントの Web ブラウザーに書き込みます。

**プロジェクトファイルの組み込み**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**Forms Client API オブジェクトを作成**

データをプログラムによって PDF formClient API に読み込む前に、Form Data Integration サービスクライアントを作成する必要があります。 サービスクライアントを作成する場合、サービスを呼び出すために必要な接続設定を定義します。

**HTML 実行時オプションを設定**

HTML フォームのレンダリング時に、HTML 実行時オプションを設定します。 例えば、HTML フォームにツールバーを追加すると、クライアントコンピューター上の添付ファイルを選択したり、HTML フォームでレンダリングされた添付ファイルを取得したりできます。 デフォルトでは、HTML ツールバーは無効になっています。 ツールバーを HTML フォームに追加するには、実行時オプションをプログラムによって設定する必要があります。 デフォルトでは、HTML ツールバーは次のボタンで構成されています。

* `Home`：アプリケーションの web ルートへのリンクを提供します。
* `Upload`：現在のフォームに添付するファイルを選択するためのユーザーインターフェイスを提供します。
* `Download`：添付ファイルを表示するユーザインタフェースを提供します。

HTML フォーム上に HTML ツールバーが表示されている場合、ユーザーは最大 10 個のファイルを選択して、フォームデータと共に送信することができます。 ファイルが送信されると、Forms サービスはファイルを取得することができます。

フォームを HTML としてレンダリングする際に、ユーザーエージェント値を指定することができます。ユーザーエージェント値は、ブラウザーとシステムの情報を提供します。 これはオプションの値で、空の文字列値を渡すことができます。Java API クイックスタートを使用した HTML フォームのレンダリングでは、ユーザーエージェント値を取得する方法、それを使用してフォームを HTML としてレンダリングする方法を示しています。

フォームデータの投稿先となる HTTP URL は、Forms サービスクライアント API を使用してターゲット URL を設定することで指定するか、XDP フォームデザインに含まれる「送信」ボタンで指定することもできます。ターゲット URL がフォームデザインで指定されている場合は、Forms サービスクライアント API を使用して値を設定しないでください。

>[!NOTE]
>ツールバーを含む HTML フォームのレンダリングはオプションです。

>[!NOTE]
>AHTML フォームをレンダリングする場合は、ツールバーをフォームに追加しないことをお勧めします。

**HTML フォームをレンダリング**

HTML フォームをレンダリングするには、Designer で作成され、XDP ファイルとして保存されたフォームデザインを指定する必要があります。HTML 変換タイプも選択する必要があります。たとえば、Internet Explorer 5.0 以降のダイナミック HTML をレンダリングする HTML 変換タイプを指定できます。

HTML フォームのレンダリングには、他のフォームタイプのレンダリングに必要な URI 値などの値も必要です。

**フォームデータストリームをクライアント web ブラウザーに書き込む**

Forms サービスが HTML フォームをレンダリングすると、クライアント web ブラウザーに書き込む必要があるフォームデータストリームが返されます。クライアント web ブラウザーに書き込まれると、HTML フォームがユーザーに対して表示されます。

**関連トピック**

[Java API を使用してフォームを HTML としてレンダリングする](#render-a-form-as-html-using-the-java-api)

[Web サービス API を使用してフォームを HTML としてレンダリングする](#render-a-form-as-html-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms サービス API のクイックスタート](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[インタラクティブ PDF Forms のレンダリング](/help/forms/developing/rendering-interactive-pdf-forms.md)

[カスタムツールバーを持つ HTML Forms のレンダリング](/help/forms/developing/rendering-html-forms-custom-toolbars.md)

[Forms をレンダリングする web アプリケーションの作成](/help/forms/developing/creating-web-applications-renders-forms.md)

## Java API を使用してフォームを HTML としてレンダリングする {#render-a-form-as-html-using-the-java-api}

Forms API (Java) を使用して HTML フォームをレンダリングします。

1. プロジェクトファイルを含める

   adobe-forms-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. Forms Client API オブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して `ServiceClientFactory` オブジェクトを渡すことによって、`FormsServiceClient` オブジェクトを作成します。

1. HTML 実行時オプションを設定

   * コンストラクターを使用して `HTMLRenderSpec` オブジェクトを作成します。
   * ツールバーを使用して HTML フォームをレンダリングするには、`HTMLRenderSpec` オブジェクトの `setHTMLToolbar` メソッドを呼び出して、`HTMLToolbar` enum 値を渡します。例えば、HTML ツールバーを垂直位置に表示するには、`HTMLToolbar.Vertical` を渡します。
   * HTML フォームのロケール値を設定するには、`HTMLRenderSpec` オブジェクトの `setLocale` メソッドを呼び出して、ロケール値を指定する文字列値を渡します。（これはオプション設定です）。
   * 完全な HTML タグ内で HTML フォームをレンダリングするには、`HTMLRenderSpec` オブジェクトの `setOutputType` メソッドを呼び出して、`OutputType.FullHTMLTags` を渡します。（これはオプション設定です）。

   >[!NOTE]
   >`StandAlone` オプションが `true` で、`ApplicationWebRoot` が AEM Forms をホストする J2EE アプリケーションサーバー以外を参照している場合、Forms は正常にレンダリングされません（`ApplicationWebRoot` の値は、`FormsServiceClient` オブジェクトの `(Deprecated) renderHTMLForm` メソッドに渡される `URLSpec` オブジェクトを使用して指定します）。`ApplicationWebRoot` が AEM Forms をホストするサーバーとは別のサーバーである場合、管理コンソールの web ルート URI の値を Forms の web アプリケーション URI 値として設定する必要があります。これを行うには、管理コンソールにログインして、サービス／Formsをクリックし、「 Web ルート URI 」を https://server-name:port/FormServer に設定します。次に、設定を保存します。

1. HTML フォームのレンダリング

   `FormsServiceClient` オブジェクトの `(Deprecated) renderHTMLForm` メソッドを呼び出して、次の値を渡します。

   * フォームデザイン名を指定する文字列値で、ファイル名の拡張子も含まれます。Forms アプリケーションの一部であるフォームデザインを参照する場合は、必ず次のような完全なパスを指定します。`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`
   * HTML の環境設定タイプを指定する `TransformTo` enum 値。例えば、Internet Explorer 5.0 以降の動的 HTML と互換性のある HTML フォームをレンダリングするには、`TransformTo.MSDHTML` を指定します。
   * フォームに結合するデータを含む `com.adobe.idp.Document` オブジェクト。データを結合しない場合は、空の `com.adobe.idp.Document` オブジェクトを渡します。
   * HTML の実行時オプションが保存する `HTMLRenderSpec` オブジェクト。
   * `HTTP_USER_AGENT` ヘッダー値を指定する文字列値。例：`Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`
   * HTML フォームのレンダリングに必要な URI 値を保存する `URLSpec` オブジェクト。
   * 添付ファイルを保存する `java.util.HashMap` オブジェクト。これはオプションのパラメーターで、フォームにファイルを添付しない場合に `null` を指定できます。

   `(Deprecated) renderHTMLForm` メソッドは、クライアント web ブラウザーに書き込むことができるフォームデータストリームを含む `FormsResult` オブジェクトを返します。

1. フォームデータストリームをクライアント web ブラウザーに書き込む

   * `FormsResult` オブジェクトの `getOutputContent` メソッドを呼び出して、`com.adobe.idp.Document` オブジェクトを作成します。
   * `getContentType` メソッドを呼び出して、`com.adobe.idp.Document` オブジェクトのコンテンツタイプを取得します。
   * `javax.servlet.http.HttpServletResponse` オブジェクトのコンテンツタイプを設定するには、`setContentType` メソッドを呼び出して、`com.adobe.idp.Document` オブジェクトのコンテンツタイプを渡します。
   * `javax.servlet.http.HttpServletResponse` オブジェクトの `getOutputStream` メソッドを呼び出して、フォームデータストリームをクライアント web ブラウザーに書き込むために使用される `javax.servlet.ServletOutputStream` オブジェクトを作成します。
   * `com.adobe.idp.Document` オブジェクトの `getInputStream` メソッドを呼び出すことによって `java.io.InputStream` オブジェクトを作成します。
   * `InputStream` オブジェクトの `read` メソッドを呼び出してバイト配列を引数として渡すことによって、バイト配列を作成してフォームデータストリームを入力します。
   * `javax.servlet.ServletOutputStream` オブジェクトの `write` メソッドを呼び出して、フォームデータストリームをクライアント web ブラウザーに送信します。バイト配列を `write` メソッドに渡します。

**関連トピック**

[Forms を HTML としてレンダリング](#rendering-forms-as-html)

[クイックスタート（SOAP モード）：Java API を使用した HTML フォームのレンダリング](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Web サービス API を使用してフォームを HTML としてレンダリングする {#render-a-form-as-html-using-the-web-service-api}

Forms API（web サービス）を使用して HTML フォームをレンダリングします。

1. プロジェクトファイルを含める

   * Forms Service WSDL を使用する Java プロキシクラスを作成します。
   * Java プロキシクラスをクラスパスに含めます。

1. Forms Client API オブジェクトの作成

   `FormsService` オブジェクトを作成し、認証値を設定します。

1. HTML 実行時オプションを設定

   * コンストラクターを使用して `HTMLRenderSpec` オブジェクトを作成します。
   * ツールバーを使用して HTML フォームをレンダリングするには、`HTMLRenderSpec` オブジェクトの `setHTMLToolbar` メソッドを呼び出して、`HTMLToolbar` enum 値を渡します。例えば、HTML ツールバーを垂直位置に表示するには、`HTMLToolbar.Vertical` を渡します。
   * HTML フォームのロケール値を設定するには、`HTMLRenderSpec` オブジェクトの `setLocale` メソッドを呼び出し、ロケール値を指定する文字列値を渡します。詳しくは、[AEM Forms API レファレンス](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ja)を参照してください。
   * 完全な HTML タグ内で HTML フォームをレンダリングするには、`HTMLRenderSpec` オブジェクトの `setOutputType` メソッドを呼び出して `OutputType.FullHTMLTags` を渡します。

   >[!NOTE]
   >`StandAlone` オプションが `true` で、`ApplicationWebRoot` が AEM Forms をホストする J2EE アプリケーションサーバー以外のサーバーを参照している場合、フォームは HTML で正常にレンダリングされません（`ApplicationWebRoot` 値は `FormsServiceClient` オブジェクトの `(Deprecated) renderHTMLForm` メソッドに渡される `URLSpec` オブジェクトを使用して指定されます）。`ApplicationWebRoot` が AEM Forms をホストするサーバーとは別のサーバーである場合、管理コンソールの web ルート URI の値を Forms の web アプリケーション URI 値として設定する必要があります。これを行うには、管理コンソールにログインして、サービス／Formsをクリックし、「 Web ルート URI 」を https://server-name:port/FormServer に設定します。次に、設定を保存します。

1. HTML フォームのレンダリング

   `FormsService` オブジェクトの `(Deprecated) renderHTMLForm` メソッドを呼び出して、次の値を渡します。

   * フォームデザイン名を指定する文字列値で、ファイル名の拡張子も含まれます。Forms アプリケーションの一部であるフォームデザインを参照する場合は、必ず次のような完全なパスを指定します。`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`
   * HTML の環境設定タイプを指定する `TransformTo` enum 値。例えば、Internet Explorer 5.0 以降の動的 HTML と互換性のある HTML フォームをレンダリングするには、`TransformTo.MSDHTML` を指定します。
   * フォームに結合するデータを含む `BLOB` オブジェクト。データを結合しない場合は、`null` を渡します。（[編集可能なレイアウトを使用した Forms の事前入力](/help/forms/developing/prepopulating-forms-flowable-layouts.md#prepopulating-forms-with-flowable-layouts)を参照してください）。
   * HTML の実行時オプションを格納する `HTMLRenderSpec` オブジェクト。
   * `HTTP_USER_AGENT` ヘッダー値を指定する文字列値（例：`Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`）。この値を設定しない場合は、空の文字列を渡します。
   * HTML フォームのレンダリングに必要な URI 値を格納する `URLSpec` オブジェクト。（[URI 値の指定](/help/forms/developing/rendering-interactive-pdf-forms.md)を参照してください）。
   * 添付ファイルを格納する `java.util.HashMap` オブジェクト。これはオプションのパラメーターで、フォームにファイルを添付しない場合は `null` を指定できます。（[フォームにファイルを添付する](/help/forms/developing/rendering-interactive-pdf-forms.md)を参照してください）。
   * メソッドによって設定される空の `com.adobe.idp.services.holders.BLOBHolder` オブジェクト。このパラメーター値には、レンダリングされたフォームが格納されます。
   * メソッドによって設定される空の `com.adobe.idp.services.holders.BLOBHolder` オブジェクト。このパラメーターは出力 XML データを格納します。
   * メソッドによって設定される空の `javax.xml.rpc.holders.LongHolder` オブジェクト。この引数は、フォームのページ数を保存します。
   * メソッドによって設定される空の `javax.xml.rpc.holders.StringHolder` オブジェクト。この引数はロケール値を格納します。
   * メソッドによって設定される空の `javax.xml.rpc.holders.StringHolder` オブジェクト。この引数は、使用される HTML レンダリング値を格納します。
   * この操作の結果を格納する空の `com.adobe.idp.services.holders.FormsResultHolder` オブジェクト。

   `(Deprecated) renderHTMLForm` メソッドは、最後の引数値として渡される `com.adobe.idp.services.holders.FormsResultHolder` オブジェクトに、クライアント web ブラウザーに書き込む必要のあるフォームデータストリームを入力します。

1. フォームデータストリームをクライアント web ブラウザーに書き込む

   * `com.adobe.idp.services.holders.FormsResultHolder` オブジェクトの `value` データメンバーの値を取得して、`FormResult` オブジェクトを作成します。
   * `FormsResult` オブジェクトの `getOutputContent` メソッドを呼び出して、フォームデータを含む `BLOB` オブジェクトを作成します。
   * `getContentType` メソッドを呼び出して、`BLOB` オブジェクトのコンテンツタイプを取得します。
   * `javax.servlet.http.HttpServletResponse` オブジェクトのコンテンツタイプを設定するには、`setContentType` メソッドを呼び出して、`BLOB` オブジェクトのコンテンツタイプを渡します。
   * `javax.servlet.http.HttpServletResponse` オブジェクトの `getOutputStream` メソッドを呼び出して、フォームデータストリームをクライアント web ブラウザーに書き込むために使用される `javax.servlet.ServletOutputStream` オブジェクトを作成します。
   * バイト配列を作成し、`BLOB` オブジェクトの `getBinaryData` メソッドを呼び出して入力します。このタスクは、`FormsResult` オブジェクトのコンテンツをバイト配列に割り当てます。
   * `javax.servlet.http.HttpServletResponse` オブジェクトの `write` メソッドを呼び出して、フォームデータストリームをクライアント web ブラウザーに送信します。バイト配列を `write` メソッドに渡します。

**関連トピック**

[Forms を HTML としてレンダリング](#rendering-forms-as-html)

[Base64 エンコーディングを使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
