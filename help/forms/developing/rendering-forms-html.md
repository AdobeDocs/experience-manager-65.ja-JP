---
title: FormsをHTMLとしてレンダリング
seo-title: FormsをHTMLとしてレンダリング
description: Formsサービスを使用して、WebブラウザーからのHTTP要求に応答してフォームをHTMLとしてレンダリングします。 Java APIおよびWebサービスAPIを使用して、フォームをHTMLとしてレンダリングできます。
seo-description: Formsサービスを使用して、WebブラウザーからのHTTP要求に応答してフォームをHTMLとしてレンダリングします。 Java APIおよびWebサービスAPIを使用して、フォームをHTMLとしてレンダリングできます。
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
source-wordcount: '4188'
ht-degree: 1%

---

# FormsをHTMLとしてレンダリング{#rendering-forms-as-html}

**このドキュメントのサンプルと例は、JEE上のAEM Forms環境に限られています。**

Formsサービスは、WebブラウザーからのHTTP要求に応じて、フォームをHTMLとしてレンダリングします。 フォームをHTMLとしてレンダリングする利点は、クライアントWebブラウザーが配置されているコンピューターにAdobe Reader、Acrobat、またはFlash Player(フォームガイド（非推奨）用)が不要であることです。

フォームをHTMLとしてレンダリングするには、フォームデザインをXDPファイルとして保存する必要があります。 PDFファイルとして保存されたフォームデザインは、HTMLとしてレンダリングできません。 HTMLとしてレンダリングされるDesignerのフォームデザインを開発する際には、次の条件を考慮してください。

* フォームに線、ボックス、グリッドを描画するときに、オブジェクトの境界線プロパティを使用しないでください。ブラウザーによっては、 のプレビューで表示されるとおりに境界線が表示されないことがあります。また、オブジェクトが重なって表示されたり、他のオブジェクトを本来の位置から押しのけたりする場合があります。
* 線、長方形および円を使用して、背景を定義できます。
* テキストを収容するために必要と思われるサイズよりも少し大きく描画します。 一部のWebブラウザーでは、読みやすくテキストが表示されません。

>[!NOTE]
>
>`FormServiceClient`オブジェクトの`(Deprecated) renderHTMLForm`および`renderHTMLForm2`メソッドを使用してTIFF画像を含むフォームをレンダリングすると、Internet ExplorerまたはMozilla Firefoxブラウザーに表示されるレンダリングされたHTMLフォームにTIFF画像が表示されません。 これらのブラウザーは、TIFF画像をネイティブでサポートしません。

## HTMLページ{#html-pages}

フォームデザインがHTMLフォームとしてレンダリングされる場合、各第2レベルサブフォームはHTMLページ（パネル）としてレンダリングされます。 Designerでサブフォームの階層を表示できます。 ルートサブフォームに属する子サブフォーム（ルートサブフォームのデフォルト名はform1）はパネルのサブフォームです。 次に、フォームデザインのサブフォームの例を示します。

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

フォームデザインをHTMLフォームとしてレンダリングする場合、パネルは特定のページサイズに制限されません。 ダイナミックサブフォームがある場合は、パネルサブフォーム内に階層化する必要があります。 動的サブフォームは、無限数のHTMLページまで拡張できます。

フォームをHTMLフォームとしてレンダリングする場合、ページサイズ（PDFとしてレンダリングされるフォームのページ番号付けに必要）は意味を持ちません。 編集可能なレイアウトを含むフォームは、無限数のHTMLページまで拡大できるので、マスターページのフッターを避けることが重要です。 マスターページのコンテンツ領域の下にあるフッターでは、フローがページ境界を超えるHTMLコンテンツを上書きする場合があります。

`xfa.host.pageUp`メソッドと`xfa.host.pageDown`メソッドを使用して、パネル間を明示的に移動する必要があります。 ページを変更するには、フォームをFormsサービスに送信し、Formsサービスでフォームをレンダリングしてクライアントデバイス（通常はWebブラウザー）に戻します。

>[!NOTE]
>
>Formsサービスにフォームを送信し、Formsサービスでフォームをレンダリングしてクライアントデバイスに戻すプロセスは、「ラウンドトリッピングデータ」と呼ばれます。

>[!NOTE]
>
>HTMLフォーム上のHTML電子署名ボタンの外観をカスタマイズする場合は、 fscdigsig.cssファイル（ adobe-forms-ds.ear / adobe-forms-ds.warファイル内）で次のプロパティを変更する必要があります。

**.fsc-ds-ssb**:このスタイルシートは、空白の記号フィールドの場合に適用されます。

**.fsc-ds-ssv**:このスタイルシートは、有効な記号フィールドの場合に適用されます。

**.fsc-ds-ssc**:このスタイルシートは、有効な記号フィールドが適用されるが、データが変更された場合に適用されます。

**.fsc-ds-ssi**:このスタイルシートは、無効な記号フィールドの場合に適用されます。

**.fsc-ds-popup-bg**:このスタイルシートのプロパティは使用されていません。

**.fsc-ds-popup-btn**:このスタイルシートのプロパティは使用されていません。

## スクリプト{#running-scripts}の実行

フォーム作成者は、スクリプトをサーバー上で実行するかクライアント上で実行するかを指定します。 Formsサービスは、`runAt`属性を使用してクライアントとサーバーの間で配布できる、フォームインテリジェンスを実行するための分散型イベント処理環境を作成します。 この属性やフォームデザイン内でのスクリプトの作成について詳しくは、[Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)を参照してください。

Formsサービスは、フォームのレンダリング中にスクリプトを実行できます。 その結果、クライアント上で使用できないデータベースやWebサービスに接続することで、フォームにデータを事前入力できます。 また、サーバー上で実行するボタンの`Click`イベントを設定し、クライアントがサーバーにトリップデータをラウンドトリップするようにすることもできます。 これにより、ユーザーがフォームを操作している間に、エンタープライズデータベースなどのサーバーリソースを必要とする可能性のあるスクリプトをクライアントが実行できます。 HTMLフォームの場合、formcalcスクリプトはサーバー上でのみ実行できます。 その結果、`server`または`both`で実行するように、これらのスクリプトにマークを付ける必要があります。

`xfa.host.pageUp`メソッドと`xfa.host.pageDown`メソッドを呼び出すことで、ページ（パネル）間を移動するフォームをデザインできます。 このスクリプトは、ボタンの`Click`イベントに配置され、`runAt`属性は`Both`に設定されます。 `Both`を選択する理由は、Adobe ReaderまたはAcrobat（PDFとしてレンダリングされるフォームの場合）がサーバーに移動せずにページを変更でき、HTMLフォームがサーバーにデータを丸めてページを変更できるようにするためです。 つまり、フォームがFormsサービスに送信され、フォームがHTMLとしてレンダリングされ、新しいページが表示されます。

スクリプト変数とフォームフィールドには、itemなどの同じ名前を付けないことをお勧めします。 Internet Explorerなどの一部のWebブラウザーでは、フォームフィールドと同じ名前の変数が初期化されず、スクリプトエラーが発生する場合があります。 フォームフィールドとスクリプト変数には、それぞれ異なる名前を付けることをお勧めします。

ページナビゲーション機能とフォームスクリプトの両方を含むHTMLフォームをレンダリングする場合（例えば、フォームがレンダリングされるたびにスクリプトがデータベースからフィールドデータを取得するとします）、フォームスクリプトがform:readyeventの代わりにform:calculateイベントに配置されます。

form:readyイベントにあるフォームスクリプトは、フォームの最初のレンダリング時に1回だけ実行され、以降のページ取得では実行されません。 これに対し、 form:calculateイベントは、フォームがレンダリングされるページナビゲーションごとに実行されます。

>[!NOTE]
複数ページフォームでは、JavaScriptによってページに加えられた変更は、別のページに移動しても保持されません。

フォームを送信する前に、カスタムスクリプトを呼び出すことができます。 この機能は、利用可能なすべてのブラウザーで動作します。 ただし、`Output Type`プロパティが`Form Body`に設定されたHTMLフォームをレンダリングする場合にのみ使用できます。 `Output Type`が`Full HTML`の場合は機能しません。 この機能を設定する手順については、管理ヘルプの「フォームの設定」を参照してください。

フォームを送信する前に呼び出すコールバック関数を定義する必要があります。関数の名前は`_user_onsubmit`です。 この関数は例外をスローしないと想定され、例外がスローされる場合は無視されます。 JavaScript関数は、htmlのheadセクションに配置することをお勧めします。ただし、`xfasubset.js`を含むスクリプトタグの終わりより前の任意の場所で宣言できます。

formserverがコンボボックスを含むXDPをレンダリングすると、コンボボックスの作成に加えて、2つの非表示テキストフィールドも作成されます。 これらのテキストフィールドには、ドロップダウンリストのデータが格納されます（一方にはオプションの表示名が格納され、もう一方にはオプションの値が格納されます）。 したがって、ユーザーがフォームを送信するたびに、ドロップダウンリストのデータ全体が送信されます。 毎回それほど多くのデータを送信したくない場合は、カスタムスクリプトを記述してそれを無効にできます。 例：ドロップダウンリストの名前は`drpOrderedByStateProv`で、サブフォームヘッダーに含まれます。 HTML入力要素の名前は`header[0].drpOrderedByStateProv[0]`になります。 ドロップダウンのデータを保存して送信する非表示フィールドの名前は、次の名前になります。`header[0].drpOrderedByStateProv_DISPLAYITEMS_[0] header[0].drpOrderedByStateProv_VALUEITEMS_[0]`

データを投稿しない場合は、次の方法でこれらの入力要素を無効にできます。`var __CUSTOM_SCRIPTS_VERSION = 1; //enabling the feature function _user_onsubmit() { var elems = document.getElementsByName("header[0].drpOrderedByStateProv_DISPLAYITEMS_[0]"); elems[0].disabled = true; elems = document.getElementsByName("header[0].drpOrderedByStateProv_VALUEITEMS_[0]"); elems[0].disabled = true; }`

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

## XFAサブセット{#xfa-subsets}

HTMLとしてレンダリングするフォームデザインを作成する場合は、JavaScript言語のスクリプトのXFAサブセットにスクリプティングを制限する必要があります。

クライアント上で実行されるスクリプト、またはクライアントとサーバーの両方で実行されるスクリプトは、XFAサブセット内で記述する必要があります。 サーバー上で実行されるスクリプトは、完全なXFAスクリプティングモデルを使用し、FormCalcも使用できます。 JavaScriptの使用について詳しくは、[Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)を参照してください。

クライアントでスクリプトを実行する場合、表示中の現在のパネルのみスクリプトを使用できます。例えば、パネルBが表示されている場合に、パネルAにあるフィールドに対してスクリプトを作成することはできません。 サーバーでスクリプトを実行する場合、すべてのパネルにアクセスできます。

また、クライアントで実行するスクリプト内でスクリプティングオブジェクトモデル(SOM)式を使用する場合は、注意が必要です。 クライアント上で実行されるスクリプトでは、SOM式の簡略化されたサブセットのみがサポートされます。

## イベントのタイミング{#event-timing}

XFAサブセットは、HTMLイベントにマッピングされるXFAイベントを定義します。 イベントの計算と検証のタイミングでの動作には、若干の違いがあります。 Webブラウザーでは、フィールドを終了すると、完全なcalculateイベントが実行されます。 「計算」イベントは、フィールド値を変更した場合には自動的には実行されません。 `xfa.form.execCalculate`メソッドを呼び出すことで、強制的にcalculateイベントを呼び出すことができます。

Webブラウザーでは、検証イベントは、フィールドを終了するかフォームを送信する場合にのみ実行されます。 `xfa.form.execValidate`メソッドを使用して、validateイベントを強制できます。

(Adobe ReaderやAcrobatとは対照的に)Webブラウザーに表示されるFormsは、必須フィールドのXFA nullテスト（エラーまたは警告）に準拠しています。

* nullテストでエラーが発生し、値を指定せずにフィールドを終了すると、メッセージボックスが表示され、「OK」をクリックした後にそのフィールドに再配置されます。
* nullテストで警告が生成され、値を指定せずにフィールドを終了した場合は、「 OK 」または「キャンセル」をクリックするよう求められ、値を指定せずに続行するか、値を入力するフィールドに戻るかを選択できます。

nullテストについて詳しくは、[Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)を参照してください。

## フォームボタン{#form-buttons}

送信ボタンをクリックすると、フォームデータがFormsサービスに送信され、フォーム処理の終了を表します。 `preSubmit`イベントは、クライアントまたはサーバー上で実行するように設定できます。 `preSubmit`イベントは、フォームがクライアント上で実行するように設定されている場合、フォーム送信の前に実行されます。 それ以外の場合は、フォームの送信中に`preSubmit`イベントがサーバーで実行されます。 `preSubmit`イベントについて詳しくは、[Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)を参照してください。

ボタンにクライアント側スクリプトが関連付けられていない場合、データがサーバーに送信され、サーバーで計算が実行され、HTMLフォームが再生成されます。 ボタンにクライアント側スクリプトが含まれている場合、データはサーバーに送信されず、クライアント側スクリプトがWebブラウザーで実行されます。

## HTML 4.0 Webブラウザー{#html-4-0-web-browser}

HTML 4.0のみをサポートするWebブラウザーは、XFAサブセットのクライアント側スクリプティングモデルをサポートできません。 HTML 4.0とMSDHTMLまたはCSS2HTMLの両方で動作するフォームデザインを作成する場合、クライアントで実行するようにマークされたスクリプトは、実際にサーバー上で実行されます。 例えば、HTML 4.0 Webブラウザーに表示されているフォーム上のボタンをユーザーがクリックするとします。 この場合、クライアント側スクリプトが実行されるサーバーにフォームデータが送信されます。

フォームロジックは、HTML 4.0のサーバーと、MSDHTMLまたはCSS2HTMLのクライアントで実行されるcalculateイベントに配置することをお勧めします。

## プレゼンテーションの変更の管理{#maintaining-presentation-changes}

HTMLページ（パネル）間を移動すると、データの状態のみが維持されます。 背景色や必須フィールド設定などの設定は維持されません（初期設定と異なる場合）。 プレゼンテーションの状態を維持するには、フィールドのプレゼンテーション状態を表すフィールド（通常は非表示）を作成する必要があります。 非表示のフィールドの値に基づいてプレゼンテーションを変更するスクリプトをフィールドの`Calculate`イベントに追加すると、HTMLページ（パネル）間を行ったり来たりする際に、プレゼンテーションの状態を保持できます。

次のスクリプトは、`hiddenField`の値に基づいてフィールドの`fillColor`を維持します。 このスクリプトがフィールドの`Calculate`イベント内にあるとします。

```java
     If (hiddenField.rawValue == 1)
         this.fillColor = "255,0,0"
     else
         this.fillColor = "0,255,0"
```

>[!NOTE]
テーブルのセル内にネストされている場合、スタティックオブジェクトはレンダリングされたHTMLフォームに表示されません。 例えば、テーブルのセル内にネストされた円や長方形は、レンダリングHTMLフォーム内に表示されません。 ただし、テーブルの外側に配置されている場合は、同じスタティックオブジェクトが正しく表示されます。

## HTMLフォームのデジタル署名{#digitally-signing-html-forms}

フォームが以下のHTML変換のいずれかとしてレンダリングされる場合、電子署名フィールドを含むHTMLフォームに署名することはできません。

* AHTML
* HTML4
* StaticHTML
* NoScriptXHTML

ドキュメントのデジタル署名については、[Digital Signing and Certifying Documents](/help/forms/developing/digitally-signing-certifying-documents.md)を参照してください。

## アクセシビリティガイドラインに準拠したXHTMLフォーム{#rendering-an-accessibility-guidelines-compliant-xhtml-form}のレンダリング

アクセシビリティガイドラインに準拠した完全なHTMLフォームをレンダリングできます。 つまり、フォームは完全なHTMLページではなくbodyタグ内でレンダリングされるのに対して、完全なHTMLタグ内でレンダリングされます。

## フォームデータの検証{#validating-form-data}

フォームをHTMLフォームとしてレンダリングする場合、フォームフィールドに対する検証ルールの使用を制限することをお勧めします。 一部の検証ルールは、HTMLフォームでサポートされない場合があります。 例えば、HTMLフォームとしてレンダリングされるフォームデザインの`Date/Time`フィールドにMM-DD-YYYYの検証パターンを適用すると、日付が正しく入力されていても、正しく機能しません。 ただし、この検証パターンは、PDFとしてレンダリングされるフォームに対して適切に機能します。

>[!NOTE]
Formsサービスについて詳しくは、『 AEM Formsのサービスリファレンス[ 』を参照してください。](https://www.adobe.com/go/learn_aemforms_services_63)

## 手順の概要{#summary-of-steps}

HTMLフォームをレンダリングするには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Forms Client APIオブジェクトを作成します。
1. HTML実行時オプションを設定します。
1. HTMLフォームをレンダリングします。
1. フォームデータストリームをクライアントWebブラウザーに書き込みます。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用する場合は、プロキシファイルを必ず含めてください。

**Forms Client APIオブジェクトの作成**

プログラムによってデータをPDF formClient APIに読み込む前に、Form Data Integrationサービスクライアントを作成する必要があります。 サービスクライアントを作成する場合、サービスを呼び出すために必要な接続設定を定義します。

**HTML実行時オプションの設定**

HTMLフォームのレンダリング時にHTML実行時オプションを設定します。 例えば、HTMLフォームにツールバーを追加して、クライアントコンピューター上の添付ファイルをユーザーが選択したり、HTMLフォームと共にレンダリングされる添付ファイルを取得したりできます。 デフォルトでは、HTMLツールバーは無効になっています。 HTMLフォームにツールバーを追加するには、実行時オプションをプログラムで設定する必要があります。 デフォルトでは、HTMLツールバーは次のボタンで構成されます。

* `Home`:アプリケーションのWebルートへのリンクを提供します。
* `Upload`:現在のフォームに添付するファイルを選択するためのユーザーインターフェイスを提供します。
* `Download`:添付ファイルを表示するユーザインタフェースを提供します。

HTMLフォームにHTMLツールバーが表示される場合、ユーザーは最大10個のファイルを選択して、フォームデータと共に送信できます。 ファイルが送信されると、Formsサービスはファイルを取得できます。

フォームをHTMLとしてレンダリングする場合、ユーザーエージェント値を指定できます。 ユーザーエージェント値は、ブラウザーとシステムの情報を提供します。 これはオプションの値で、空の文字列値を渡すことができます。 Java APIを使用したHTMLフォームのレンダリングクイックスタートでは、ユーザーエージェントの値を取得し、それを使用してフォームをHTMLとしてレンダリングする方法を示します。

FormsサービスクライアントAPIを使用してターゲットURLを設定することで、またはXDPフォームデザインに含まれる「送信」ボタンで、フォームデータが投稿されるHTTP URLを指定できます。 ターゲットURLがフォームデザインで指定されている場合は、FormsサービスクライアントAPIを使用して値を設定しないでください。

>[!NOTE]
ツールバーを使用したHTMLフォームのレンダリングはオプションです。

>[!NOTE]
AHTMLフォームをレンダリングする場合は、ツールバーをフォームに追加しないことをお勧めします。

**HTMLフォームのレンダリング**

HTMLフォームをレンダリングするには、Designerで作成し、XDPファイルとして保存するフォームデザインを指定する必要があります。 また、HTML変換タイプを選択する必要があります。 例えば、Internet Explorer 5.0以降用の動的HTMLをレンダリングするHTML変換タイプを指定できます。

HTMLフォームのレンダリングには、他のフォームタイプのレンダリングに必要なURI値などの値も必要です。

**フォームデータストリームをクライアントWebブラウザーに書き込む**

Formsサービスは、HTMLフォームをレンダリングする際に、クライアントのWebブラウザーに書き込む必要があるフォームデータストリームを返します。 クライアントのWebブラウザーに書き込まれると、HTMLフォームがユーザーに表示されます。

**関連トピック**

[Java APIを使用してフォームをHTMLとしてレンダリングする](#render-a-form-as-html-using-the-java-api)

[WebサービスAPIを使用してフォームをHTMLとしてレンダリングする](#render-a-form-as-html-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[FormsサービスAPIのクイックスタート](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[インタラクティブPDF formsのレンダリング](/help/forms/developing/rendering-interactive-pdf-forms.md)

[カスタムツールバーを使用したHTML Formsのレンダリング](/help/forms/developing/rendering-html-forms-custom-toolbars.md)

[Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

## Java API {#render-a-form-as-html-using-the-java-api}を使用してフォームをHTMLとしてレンダリングする

Forms API(Java)を使用してHTMLフォームをレンダリングします。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-forms-client.jarなどのクライアントJARファイルを含めます。

1. Forms Client APIオブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して`FormsServiceClient`オブジェクトを渡し、`ServiceClientFactory`オブジェクトを作成します。

1. HTML実行時オプションの設定

   * `HTMLRenderSpec`オブジェクトを作成するには、コンストラクタを使用します。
   * ツールバーでHTMLフォームをレンダリングするには、`HTMLRenderSpec`オブジェクトの`setHTMLToolbar`メソッドを呼び出して、`HTMLToolbar`列挙値を渡します。 例えば、垂直方向のHTMLツールバーを表示するには、`HTMLToolbar.Vertical`を渡します。
   * HTMLフォームのロケール値を設定するには、`HTMLRenderSpec`オブジェクトの`setLocale`メソッドを呼び出し、ロケール値を指定する文字列値を渡します。 （これはオプションの設定です）。
   * 完全なHTMLタグ内でHTMLフォームをレンダリングするには、`HTMLRenderSpec`オブジェクトの`setOutputType`メソッドを呼び出して`OutputType.FullHTMLTags`を渡します。 （これはオプションの設定です）。

   >[!NOTE]
   `StandAlone`オプションが`true`で、`ApplicationWebRoot`がAEM FormsをホストするJ2EEアプリケーションサーバー以外のサーバーを参照する場合（`ApplicationWebRoot`値は`FormsServiceClient`オブジェクトの`(Deprecated) renderHTMLForm`メソッドに渡される`URLSpec`オブジェクトを使用して指定）、FormsはHTMLで正常にレンダリングされません。 `ApplicationWebRoot`が、AEM Formsをホストするサーバーの別のサーバーである場合は、管理コンソールのWebルートURIの値をフォームのWebアプリケーションURI値として設定する必要があります。 これは、管理コンソールにログインして、サービス/Formsをクリックし、「 WebルートURI 」をhttps://server-name:port/FormServerに設定することで実行できます。 次に、設定を保存します。

1. HTMLフォームのレンダリング

   `FormsServiceClient`オブジェクトの`(Deprecated) renderHTMLForm`メソッドを呼び出し、次の値を渡します。

   * ファイル名拡張子を含むフォームデザイン名を指定するstring値。 Formsアプリケーションの一部であるフォームデザインを参照する場合は、必ず`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`のように完全なパスを指定してください。
   * HTML環境設定タイプを指定する`TransformTo`列挙値。 例えば、Internet Explorer 5.0以降の動的HTMLと互換性のあるHTMLフォームをレンダリングするには、`TransformTo.MSDHTML`と指定します。
   * フォームとマージするデータを含む`com.adobe.idp.Document`オブジェクト。 データを結合しない場合は、空の`com.adobe.idp.Document`オブジェクトを渡します。
   * HTML実行時オプションを格納する`HTMLRenderSpec`オブジェクト。
   * `HTTP_USER_AGENT`ヘッダー値を指定するstring値。例： `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`
   * HTMLフォームをレンダリングするために必要なURI値を格納する`URLSpec`オブジェクト。
   * 添付ファイルを格納する`java.util.HashMap`オブジェクト。 これはオプションのパラメーターで、フォームにファイルを添付しない場合は`null`を指定できます。

   `(Deprecated) renderHTMLForm`メソッドは、クライアントのWebブラウザーに書き込み可能なフォームデータストリームを含む`FormsResult`オブジェクトを返します。

1. フォームデータストリームをクライアントWebブラウザーに書き込む

   * `FormsResult`オブジェクトの`getOutputContent`メソッドを呼び出して、`com.adobe.idp.Document`オブジェクトを作成します。
   * `getContentType`メソッドを呼び出して、`com.adobe.idp.Document`オブジェクトのコンテンツタイプを取得します。
   * `setContentType`メソッドを呼び出し、`com.adobe.idp.Document`オブジェクトのコンテンツタイプを渡すことで、`javax.servlet.http.HttpServletResponse`オブジェクトのコンテンツタイプを設定します。
   * `javax.servlet.http.HttpServletResponse`オブジェクトの`getOutputStream`メソッドを呼び出して、フォームデータストリームをクライアントWebブラウザーに書き込むための`javax.servlet.ServletOutputStream`オブジェクトを作成します。
   * `com.adobe.idp.Document`オブジェクトの`getInputStream`メソッドを呼び出して、`java.io.InputStream`オブジェクトを作成します。
   * `InputStream`オブジェクトの`read`メソッドを呼び出し、バイト配列を引数として渡すことで、バイト配列を作成し、フォームデータストリームに入力します。
   * `javax.servlet.ServletOutputStream`オブジェクトの`write`メソッドを呼び出して、フォームデータストリームをクライアントWebブラウザーに送信します。 `write`メソッドにバイト配列を渡します。

**関連トピック**

[FormsをHTMLとしてレンダリング](#rendering-forms-as-html)

[クイックスタート（SOAPモード）:Java APIを使用したHTMLフォームのレンダリング](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## WebサービスAPI {#render-a-form-as-html-using-the-web-service-api}を使用してフォームをHTMLとしてレンダリングする

Forms API（Webサービス）を使用してHTMLフォームをレンダリングします。

1. プロジェクトファイルを含める

   * FormsサービスのWSDLを使用するJavaプロキシクラスを作成します。
   * Javaプロキシクラスをクラスパスに含めます。

1. Forms Client APIオブジェクトの作成

   `FormsService`オブジェクトを作成し、認証値を設定します。

1. HTML実行時オプションの設定

   * `HTMLRenderSpec`オブジェクトを作成するには、コンストラクタを使用します。
   * ツールバーでHTMLフォームをレンダリングするには、`HTMLRenderSpec`オブジェクトの`setHTMLToolbar`メソッドを呼び出して、`HTMLToolbar`列挙値を渡します。 例えば、垂直方向のHTMLツールバーを表示するには、`HTMLToolbar.Vertical`を渡します。
   * HTMLフォームのロケール値を設定するには、`HTMLRenderSpec`オブジェクトの`setLocale`メソッドを呼び出し、ロケール値を指定する文字列値を渡します。 詳しくは、「[AEM Forms APIリファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)」を参照してください。
   * 完全なHTMLタグ内でHTMLフォームをレンダリングするには、`HTMLRenderSpec`オブジェクトの`setOutputType`メソッドを呼び出して`OutputType.FullHTMLTags`を渡します。

   >[!NOTE]
   `StandAlone`オプションが`true`で、`ApplicationWebRoot`がAEM FormsをホストするJ2EEアプリケーションサーバー以外のサーバーを参照する場合（`ApplicationWebRoot`値は`FormsServiceClient`オブジェクトの`(Deprecated) renderHTMLForm`メソッドに渡される`URLSpec`オブジェクトを使用して指定）、FormsはHTMLで正常にレンダリングされません。 `ApplicationWebRoot`が、AEM Formsをホストするサーバーの別のサーバーである場合は、管理コンソールのWebルートURIの値をフォームのWebアプリケーションURI値として設定する必要があります。 これは、管理コンソールにログインして、サービス/Formsをクリックし、「 WebルートURI 」をhttps://server-name:port/FormServerに設定することで実行できます。 次に、設定を保存します。

1. HTMLフォームのレンダリング

   `FormsService`オブジェクトの`(Deprecated) renderHTMLForm`メソッドを呼び出し、次の値を渡します。

   * ファイル名拡張子を含むフォームデザイン名を指定するstring値。 Formsアプリケーションの一部であるフォームデザインを参照する場合は、必ず`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`のように完全なパスを指定してください。
   * HTML環境設定タイプを指定する`TransformTo`列挙値。 例えば、Internet Explorer 5.0以降の動的HTMLと互換性のあるHTMLフォームをレンダリングするには、`TransformTo.MSDHTML`と指定します。
   * フォームとマージするデータを含む`BLOB`オブジェクト。 データを結合しない場合は、`null`を渡します。 ([編集可能なレイアウトを使用したFormsの事前入力](/help/forms/developing/prepopulating-forms-flowable-layouts.md#prepopulating-forms-with-flowable-layouts)を参照)。
   * HTML実行時オプションを格納する`HTMLRenderSpec`オブジェクト。
   * `HTTP_USER_AGENT`ヘッダー値を指定するstring値。例： `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)` この値を設定しない場合は、空の文字列を渡すことができます。
   * HTMLフォームをレンダリングするために必要なURI値を格納する`URLSpec`オブジェクト。 （[URI値の指定](/help/forms/developing/rendering-interactive-pdf-forms.md)を参照）。
   * 添付ファイルを格納する`java.util.HashMap`オブジェクト。 これはオプションのパラメーターで、フォームにファイルを添付しない場合は`null`を指定できます。 （[フォームへのファイルの添付](/help/forms/developing/rendering-interactive-pdf-forms.md)を参照）。
   * メソッドで設定される空の`com.adobe.idp.services.holders.BLOBHolder`オブジェクト。 このパラメーター値は、レンダリングされたフォームを保存します。
   * メソッドで設定される空の`com.adobe.idp.services.holders.BLOBHolder`オブジェクト。 このパラメーターは、出力XMLデータを格納します。
   * メソッドで設定される空の`javax.xml.rpc.holders.LongHolder`オブジェクト。 この引数は、フォームのページ数を保存します。
   * メソッドで設定される空の`javax.xml.rpc.holders.StringHolder`オブジェクト。 この引数はロケール値を格納します。
   * メソッドで設定される空の`javax.xml.rpc.holders.StringHolder`オブジェクト。 この引数は、使用されるHTMLレンダリング値を格納します。
   * この操作の結果を格納する空の`com.adobe.idp.services.holders.FormsResultHolder`オブジェクト。

   `(Deprecated) renderHTMLForm`メソッドは、最後の引数値として渡される`com.adobe.idp.services.holders.FormsResultHolder`オブジェクトに、クライアントWebブラウザーに書き込む必要のあるフォームデータストリームを設定します。

1. フォームデータストリームをクライアントWebブラウザーに書き込む

   * `com.adobe.idp.services.holders.FormsResultHolder`オブジェクトの`value`データメンバーの値を取得して、`FormResult`オブジェクトを作成します。
   * `FormsResult`オブジェクトの`getOutputContent`メソッドを呼び出して、フォームデータを含む`BLOB`オブジェクトを作成します。
   * `getContentType`メソッドを呼び出して、`BLOB`オブジェクトのコンテンツタイプを取得します。
   * `setContentType`メソッドを呼び出し、`BLOB`オブジェクトのコンテンツタイプを渡すことで、`javax.servlet.http.HttpServletResponse`オブジェクトのコンテンツタイプを設定します。
   * `javax.servlet.http.HttpServletResponse`オブジェクトの`getOutputStream`メソッドを呼び出して、フォームデータストリームをクライアントWebブラウザーに書き込むための`javax.servlet.ServletOutputStream`オブジェクトを作成します。
   * バイト配列を作成し、`BLOB`オブジェクトの`getBinaryData`メソッドを呼び出してそれを設定します。 このタスクは、`FormsResult`オブジェクトの内容をバイト配列に割り当てます。
   * `javax.servlet.http.HttpServletResponse`オブジェクトの`write`メソッドを呼び出して、フォームデータストリームをクライアントWebブラウザーに送信します。 `write`メソッドにバイト配列を渡します。

**関連トピック**

[FormsをHTMLとしてレンダリング](#rendering-forms-as-html)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
