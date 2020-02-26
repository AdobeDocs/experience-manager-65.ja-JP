---
title: HTMLとしてのフォームのレンダリング
seo-title: HTMLとしてのフォームのレンダリング
description: 'null'
seo-description: 'null'
uuid: bd8edb6f-333b-4ceb-9877-618f5377f56f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 669ede46-ea55-444b-a23f-23a86e5aff8e
translation-type: tm+mt
source-git-commit: 9f3129aff8a3e389231b0fe0973794e5d34480a0

---


# HTMLとしてのフォームのレンダリング {#rendering-forms-as-html}

Formsサービスは、WebブラウザーからのHTTP要求に応答して、フォームをHTMLとしてレンダリングします。 HTML形式でフォームをレンダリングする利点は、クライアントWebブラウザーが配置されているコンピューターでAdobe Reader、Acrobat、Flash Player(フォームガイド（非推奨）用)が不要であることです。

フォームをHTMLとしてレンダリングするには、フォームデザインをXDPファイルとして保存する必要があります。 PDFファイルとして保存されたフォームデザインは、HTMLとしてレンダリングできません。 HTMLとしてレンダリングされるDesignerでフォームデザインを開発する場合は、次の条件を考慮します。

* フォームに線、ボックス、グリッドを描画するときに、オブジェクトの境界線プロパティを使用しないでください。ブラウザーによっては、 のプレビューで表示されるとおりに境界線が表示されないことがあります。また、オブジェクトが重なって表示されたり、他のオブジェクトを本来の位置から押しのけたりする場合があります。
* 線、長方形、円を使用して背景を定義できます。
* テキストを収容するために必要と思われるサイズよりも少し大きなテキストを描画します。 一部のWebブラウザーでは、テキストが見やすく表示されません。

>[!NOTE]
>
>TIFF画像を含むフォームをオブジェクトおよび `FormServiceClient``(Deprecated) renderHTMLForm``renderHTMLForm2` メソッドを使用してレンダリングする場合、Internet ExplorerまたはMozilla Firefoxブラウザーで表示されるレンダリングされたHTMLフォームにTIFF画像が表示されません。 これらのブラウザーは、TIFF画像をネイティブでサポートしません。

## HTMLページ {#html-pages}

フォームデザインがHTMLフォームとしてレンダリングされると、2番目のレベルの各サブフォームがHTMLページ（パネル）としてレンダリングされます。 サブフォームの階層はDesignerで表示できます。 ルートサブフォームに属する子サブフォーム（ルートサブフォームのデフォルト名はform1）は、パネルサブフォームです。 次の例は、フォームデザインのサブフォームを示しています。

```as3
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

フォームデザインがHTMLフォームとしてレンダリングされる場合、パネルは特定のページサイズに制限されません。 ダイナミックサブフォームがある場合は、パネルサブフォーム内に階層化する必要があります。 ダイナミックサブフォームは、HTMLページを無限に拡大できます。

フォームをHTMLフォームとしてレンダリングする場合、ページサイズ（PDFとしてレンダリングされるフォームのページ番号付けに必要）は意味を持ちません。 編集可能なレイアウトを含むフォームは、HTMLページを無制限に拡大できるので、マスターページのフッターを避けることが重要です。 マスターページ上のコンテンツ領域の下にあるフッターは、ページの境界を越えてフローするHTMLコンテンツを上書きする場合があります。

とメソッドを使用して、パネル間を明示的に移動する必 `xfa.host.pageUp` 要があ `xfa.host.pageDown` ります。 ページを変更するには、フォームをFormsサービスに送信し、Formsサービスでクライアントデバイス（通常はWebブラウザー）にフォームをレンダリングし直します。

>[!NOTE]
>
>フォームをFormsサービスに送信し、Formsサービスでフォームをクライアントデバイスにレンダリングして戻すプロセスは、サーバーへのデータのラウンドトリッピングと呼ばれます。

>[!NOTE]
>
>HTMLフォーム上の「HTMLデジタル署名」ボタンの外観をカスタマイズする場合は、fscdigsig.cssファイル（adobe-forms-ds.ear内/adobe-forms-ds.warファイル内）で次のプロパティを変更する必要があります。

**.fsc-ds-ssb**:このスタイルシートは、空白の記号フィールドの場合に適用できます。

**.fsc-ds-ssv**:このスタイルシートは、有効な記号フィールドの場合に適用できます。

**.fsc-ds-ssc**:このスタイルシートは、有効な記号フィールドが適用されるが、データが変更された場合に適用されます。

**.fsc-ds-ssi**:このスタイルシートは、無効な記号フィールドの場合に適用されます。

**.fsc-ds-popup-bg**:このスタイルシートプロパティは使用されていません。

**.fsc-ds-popup-btn**:このスタイルシートプロパティは使用されていません。

## スクリプトの実行 {#running-scripts}

フォーム作成者は、スクリプトをサーバー上で実行するか、クライアント上で実行するかを指定します。 Formsサービスは、属性を使用してクライアントとサーバーの間で配布できるフォームインテリジェンスを実行するための、分散されたイベント処理環境を作成 `runAt` します。 この属性またはフォームデザイン内でのスクリプトの作成について詳しくは、「 [Forms Designer」を参照してください](https://www.adobe.com/go/learn_aemforms_designer_63)

Formsサービスは、フォームのレンダリング中にスクリプトを実行できます。 その結果、クライアントで使用できないデータベースまたはWebサービスに接続して、フォームにデータを事前入力できます。 また、サーバー上で実行するボタンのイベン `Click` トを設定して、クライアントがサーバーに旅行データをラウンドトリップするようにすることもできます。 これにより、ユーザーがフォームを操作している間に、エンタープライズデータベースなどのサーバーリソースを必要とする可能性のあるスクリプトをクライアントが実行できます。 HTMLフォームの場合、formcalcスクリプトはサーバー上でのみ実行できます。 そのため、またはで実行するスクリプトをマークする必要が `server` ありま `both`す。

メソッドとメソッドを呼び出して、ページ（パネル）間を移動するフォームをデザ `xfa.host.pageUp` インで `xfa.host.pageDown` きます。 このスクリプトはボタンのイベントに配置さ `Click` れ、属性は `runAt` に設定されます `Both`。 選択する理由は、Adobe Reader `Both` またはAcrobat（PDFとしてレンダリングされるフォームの場合）がサーバーにアクセスせずにページを変更でき、HTMLフォームがデータをサーバーに丸めてトリッピングすることでページを変更できるようにするためです。 つまり、フォームがFormsサービスに送信され、フォームがHTMLとしてレンダリングされ、新しいページが表示されます。

スクリプト変数とフォームフィールドには、itemなどの同じ名前を付けないことをお勧めします。 Internet Explorerなどの一部のWebブラウザーでは、フォームフィールドと同じ名前の変数を初期化できず、スクリプトエラーが発生する場合があります。 フォームフィールドとスクリプト変数には、異なる名前を付けることをお勧めします。

ページナビゲーション機能とフォームスクリプトの両方を含むHTMLフォームをレンダリングする場合（例えば、フォームをレンダリングするたびにスクリプトがデータベースからフィールドデータを取得する場合）、フォームスクリプトがform:readyeventではなくform:calculateイベントに配置されていることを確認します。

form:readyイベント内のフォームスクリプトは、フォームの最初のレンダリング中に1回だけ実行され、以降のページ取得では実行されません。 これに対し、form:calculateイベントは、フォームがレンダリングされるページナビゲーションごとに実行されます。

>[!NOTE]
複数ページフォームでは、JavaScriptによってページに対して行われた変更は、別のページに移動しても保持されません。

フォームを送信する前にカスタムスクリプトを呼び出すことができます。 この機能は、使用可能なすべてのブラウザーで機能します。 ただし、この変数は、プロパティがに設定されたHTMLフォームをユーザーがレンダリングする場合にの `Output Type` み使用できま `Form Body`す。 それはその時には機能しま `Output Type` せん `Full HTML`。 この機能を設定する手順については、管理ヘルプの「フォームの設定」を参照してください。

フォームを送信する前に呼び出すコールバック関数を定義する必要があります。この関数の名前はです `_user_onsubmit`。 関数が例外をスローしないと想定されます。例外が発生した場合は無視されます。 JavaScript関数は、htmlのheadセクションに配置することをお勧めします。ただし、を含むスクリプトタグの末尾より前の任意の場所で宣言できま `xfasubset.js`す。

formserverがコンボボックスを含むXDPをレンダリングすると、コンボボックスの作成に加えて、2つの非表示テキストフィールドも作成します。 これらのテキストフィールドには、コンボボックスのデータが格納されます（一方にはオプションの表示名が格納され、もう一方にはオプションの値が格納されます）。 したがって、ユーザーがフォームを送信するたびに、コンボボックスのデータ全体が送信されます。 毎回それほど多くのデータを送信したくない場合は、それを無効にするカスタムスクリプトを作成できます。 例：コンボボックスの名前はで、サブフォ `drpOrderedByStateProv` ームヘッダーの下に含まれます。 HTML入力要素の名前は次のようになります `header[0].drpOrderedByStateProv[0]`。 ドロップダウンのデータを保存して送信する非表示フィールドの名前は、次のようになります。 `header[0].drpOrderedByStateProv_DISPLAYITEMS_[0] header[0].drpOrderedByStateProv_VALUEITEMS_[0]`

データを投稿しない場合は、次の方法でこれらの入力要素を無効にできます。 `var __CUSTOM_SCRIPTS_VERSION = 1; //enabling the feature function _user_onsubmit() { var elems = document.getElementsByName("header[0].drpOrderedByStateProv_DISPLAYITEMS_[0]"); elems[0].disabled = true; elems = document.getElementsByName("header[0].drpOrderedByStateProv_VALUEITEMS_[0]"); elems[0].disabled = true; }`

```as3
header[0].drpOrderedByStateProv_DISPLAYITEMS_[0] header[0].drpOrderedByStateProv_VALUEITEMS_[0]
```

```as3
var __CUSTOM_SCRIPTS_VERSION = 1; //enabling the feature
    function _user_onsubmit() {
    var elems = document.getElementsByName("header[0].drpOrderedByStateProv_DISPLAYITEMS_[0]");
    elems[0].disabled = true;
    elems = document.getElementsByName("header[0].drpOrderedByStateProv_VALUEITEMS_[0]");
    elems[0].disabled = true;
    }
```

## XFAサブセット {#xfa-subsets}

HTMLとしてレンダリングするフォームデザインを作成する場合は、JavaScript言語のスクリプトのXFAサブセットに制限する必要があります。

クライアント上で実行するスクリプト、またはクライアントとサーバーの両方で実行するスクリプトは、XFAサブセット内に記述する必要があります。 サーバー上で実行するスクリプトは、完全なXFAスクリプティングモデルを使用でき、FormCalcも使用できます。 JavaScriptの使用に関する詳細は、「 [Forms Designer」を参照してください](https://www.adobe.com/go/learn_aemforms_designer_63)。

クライアントでスクリプトを実行する場合、現在表示されているパネルのみがスクリプトを使用できます。例えば、パネルBが表示されている場合に、パネルAにあるフィールドに対してスクリプトを実行することはできません。 サーバーでスクリプトを実行する場合は、すべてのパネルにアクセスできます。

また、クライアント上で実行するスクリプト内でScripting Object Model(SOM)式を使用する場合は、注意が必要です。 SOM式の簡素化されたサブセットのみが、クライアントで実行されるスクリプトでサポートされます。

## イベントのタイミング {#event-timing}

XFAサブセットは、HTMLイベントにマップされるXFAイベントを定義します。 calculateイベントとvalidateイベントのタイミングでの動作には若干の違いがあります。 Webブラウザーでは、フィールドを終了するとfull calculateイベントが実行されます。 フィールド値を変更しても、calculateイベントは自動的には実行されません。 このメソッドを呼び出すことで、強制的にcalculateイベントを呼び出すことが `xfa.form.execCalculate` できます。

Webブラウザーでは、検証イベントはフィールドを終了するかフォームを送信する場合にのみ実行されます。 このメソッドを使用して、validateイベントを強制的に実行で `xfa.form.execValidate` きます。

Webブラウザー（Adobe readerやAcrobatとは異なる）に表示されるフォームは、必須フィールドのXFA nullテスト（エラーまたは警告）に準拠しています。

* nullテストでエラーが発生し、値を指定せずにフィールドを終了すると、メッセージボックスが表示され、「OK」をクリックした後でフィールドの位置が変更されます。
* nullテストによって警告が生成され、値を指定せずにフィールドを終了した場合は、「OK」または「キャンセル」をクリックするよう求められ、値を指定せずに続行するか、フィールドに戻って値を入力するかを選択できます。

nullテストについて詳しくは、「 [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)」を参照してください。

## フォームボタン {#form-buttons}

送信ボタンをクリックすると、フォームデータがFormsサービスに送信され、フォーム処理の終わりを表します。 このイベ `preSubmit` ントは、クライアントまたはサーバーで実行するように設定できます。 このイ `preSubmit` ベントは、クライアントで実行するように設定されている場合、フォーム送信の前に実行されます。 それ以外の場合は、 `preSubmit` フォームの送信中にイベントがサーバー上で実行されます。 このイベントについて詳しくは、「 `preSubmit` Forms Designer」を参 [照してください](https://www.adobe.com/go/learn_aemforms_designer_63)。

ボタンにクライアントサイドスクリプトが関連付けられていない場合、データはサーバーに送信され、サーバー上で計算が実行され、HTMLフォームが再生成されます。 ボタンにクライアントサイドのスクリプトが含まれている場合、データはサーバーに送信されず、クライアントサイドのスクリプトがWebブラウザーで実行されます。

## HTML 4.0 webブラウザー {#html-4-0-web-browser}

HTML 4.0のみをサポートするWebブラウザーは、XFAサブセットのクライアント側スクリプティングモデルをサポートできません。 HTML 4.0とMSDHTML、またはCSS2HTMLの両方で動作するフォームデザインを作成する場合、クライアントで実行するようにマークされたスクリプトが実際にサーバー上で実行されます。 例えば、HTML 4.0 webブラウザーに表示されたフォーム上のボタンをユーザーがクリックしたとします。 この場合、フォームデータはクライアントサイドスクリプトが実行されるサーバーに送信されます。

フォームロジックは、HTML 4.0のサーバーで実行され、MSDHTMLまたはCSS2HTMLのクライアントで実行されるcalculateイベントに配置することをお勧めします。

## プレゼンテーションの変更の管理 {#maintaining-presentation-changes}

HTMLページ（パネル）間を移動すると、データの状態のみが維持されます。 背景色や必須フィールドの設定などの設定は維持されません（初期設定と異なる場合）。 プレゼンテーション状態を維持するには、フィールドのプレゼンテーション状態を表すフィールド（通常は非表示）を作成する必要があります。 フィールドのイベントに、非表示のフィールド値に基づいてプレゼンテーションを変更するスクリプトを追加すると、HTMLページ（パネル）間を移動する際に、プレゼンテーションの状態を維持できます。 `Calculate`

次のスクリプトでは、の値 `fillColor` に基づいてフィールドの内容を管理しま `hiddenField`す。 このスクリプトがフィールドのイベント内にあるとし `Calculate` ます。

```as3
     If (hiddenField.rawValue == 1)
         this.fillColor = "255,0,0"
     else
         this.fillColor = "0,255,0"
```

>[!NOTE]
テーブルのセル内にネストされている場合、レンダリングされたHTMLフォームにスタティックオブジェクトが表示されません。 例えば、テーブルセル内にネストされた円と長方形は、レンダリングHTMLフォーム内に表示されません。 ただし、テーブルの外側に配置した場合は、同じスタティックオブジェクトが正しく表示されます。

## HTMLフォームへの電子署名 {#digitally-signing-html-forms}

電子署名フィールドを含むHTMLフォームが次のHTML変換のいずれかとしてレンダリングされる場合は、そのフォームに署名することはできません。

* AHTML
* HTML4
* StaticHTML
* NoScriptXHTML

ドキュメントへの電子署名について詳しくは、「ドキュメントへの電子署名と [認証」を参照してください。](/help/forms/developing/digitally-signing-certifying-documents.md)

## アクセシビリティガイドライン準拠のXHTMLフォームのレンダリング {#rendering-an-accessibility-guidelines-compliant-xhtml-form}

アクセシビリティガイドラインに準拠した完全なHTMLフォームをレンダリングできます。 つまり、フォームは完全なHTMLタグ内でレンダリングされ、HTMLフォームはbodyタグ内でレンダリングされます（完全なHTMLページではありません）。

## フォームデータの検証 {#validating-form-data}

フォームをHTMLフォームとしてレンダリングする場合は、フォームフィールドの検証ルールの使用を制限することをお勧めします。 一部の検証ルールは、HTMLフォームでサポートされていない場合があります。 例えば、HTMLフォームとしてレンダリングされるフォームデザイン内のフィールドにMM-DD-YYYYの検証パターンを適用した場合、日付が正しく入力されていても、正しく機能しません。 `Date/Time` ただし、この検証パターンは、PDFとしてレンダリングされるフォームに対して正しく機能します。

>[!NOTE]
For more information about the Forms service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## 手順の概要 {#summary-of-steps}

HTMLフォームをレンダリングするには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. フォームクライアントAPIオブジェクトを作成します。
1. HTML実行時オプションを設定します。
1. HTMLフォームをレンダリングします。
1. クライアントのWebブラウザーにフォームデータストリームを書き込みます。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

**フォームクライアントAPIオブジェクトの作成**

プログラムでデータをPDF formClient APIに読み込む前に、Form Data Integrationサービスクライアントを作成する必要があります。 サービスクライアントを作成する場合は、サービスの呼び出しに必要な接続設定を定義します。

**HTML実行時オプションの設定**

HTMLフォームのレンダリング時に、HTML実行時オプションを設定します。 例えば、HTMLフォームにツールバーを追加して、クライアントコンピューター上の添付ファイルを選択したり、HTMLフォームと共にレンダリングされる添付ファイルを取得したりできます。 デフォルトでは、HTMLツールバーは無効になっています。 HTMLフォームにツールバーを追加するには、プログラムによって実行時のオプションを設定する必要があります。 デフォルトでは、HTMLツールバーは次のボタンで構成されます。

* `Home`:アプリケーションのWebルートへのリンクを提供します。
* `Upload`:現在のフォームに添付するファイルを選択するためのユーザーインターフェイスを提供します。
* `Download`:添付ファイルを表示するユーザインターフェイスを提供します。

HTMLフォームにHTMLツールバーが表示される場合、ユーザーはフォームデータと共に送信するファイルを最大10個まで選択できます。 ファイルが送信されると、Formsサービスはファイルを取得できます。

フォームをHTMLとしてレンダリングする場合は、user-agentの値を指定できます。 user-agent値は、ブラウザーとシステムの情報を提供します。 これはオプションの値で、空の文字列値を渡すことができます。 Java APIクイックスタートを使用したHTMLフォームのレンダリングでは、ユーザーエージェントの値を取得し、それを使用してフォームをHTMLとしてレンダリングする方法を示します。

フォームデータが投稿されるHTTP URLは、Forms Service Client APIを使用してターゲットURLを設定することで指定することも、XDPフォームデザインに含まれる「送信」ボタンで指定することもできます。 ターゲットURLがフォームデザインで指定されている場合は、FormsサービスクライアントAPIを使用して値を設定しないでください。

>[!NOTE]
ツールバーを使用したHTMLフォームのレンダリングはオプションです。

>[!NOTE]
AHTMLフォームをレンダリングする場合は、フォームにツールバーを追加しないことをお勧めします。

**HTMLフォームのレンダリング**

HTMLフォームをレンダリングするには、Designerで作成し、XDPファイルとして保存するフォームデザインを指定する必要があります。 また、HTML変換タイプを選択する必要があります。 例えば、Internet Explorer 5.0以降用の動的HTMLをレンダリングするHTML変換タイプを指定できます。

HTMLフォームのレンダリングには、他のフォームタイプのレンダリングに必要なURI値などの値も必要です。

**クライアントのWebブラウザーにフォームデータストリームを書き込みます**

Formsサービスは、HTMLフォームをレンダリングすると、フォームデータストリームを返し、クライアントのWebブラウザーに書き込む必要があります。 クライアントWebブラウザーに書き込むと、HTMLフォームがユーザーに表示されます。

**関連トピック**

[Java APIを使用してフォームをHTMLとしてレンダリングする](#render-a-form-as-html-using-the-java-api)

[WebサービスAPIを使用してフォームをHTMLとしてレンダリングする](#render-a-form-as-html-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[FormsサービスAPIのクイックスタート](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[インタラクティブPDFフォームのレンダリング](/help/forms/developing/rendering-interactive-pdf-forms.md)

[カスタムツールバーを使用したHTMLフォームのレンダリング](/help/forms/developing/rendering-html-forms-custom-toolbars.md)

[フォームをレンダリングするWebアプリケーションの作成](/help/forms/developing/creating-web-applications-renders-forms.md)

## Java APIを使用してフォームをHTMLとしてレンダリングする {#render-a-form-as-html-using-the-java-api}

Forms API(Java)を使用してHTMLフォームをレンダリングします。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-forms-client.jarなどのクライアントJARファイルを含めます。

1. フォームクライアントAPIオブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `FormsServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. HTML実行時オプションの設定

   * Create an `HTMLRenderSpec` object by using its constructor.
   * ツールバーを使用してHTMLフォームをレンダリングするには、オブ `HTMLRenderSpec` ジェクトのメソッドを `setHTMLToolbar` 呼び出し、列挙値を渡 `HTMLToolbar` します。 例えば、垂直方向のHTMLツールバーを表示するには、を渡しま `HTMLToolbar.Vertical`す。
   * HTMLフォームのロケール値を設定するには、オブジェクトの `HTMLRenderSpec` メソッドを呼び出 `setLocale` し、ロケール値を指定するstring値を渡します。 （これはオプションの設定です）。
   * 完全なHTMLタグ内でHTMLフォームをレンダリングするには、オブジェクトの `HTMLRenderSpec` メソッドを呼び出 `setOutputType` して渡しま `OutputType.FullHTMLTags`す。 （これはオプションの設定です）。
   >[!NOTE]
   このオプションを選択し、AEM formsをホストするJ2EEアプリケーションサーバー以外のサーバーを参照している場合、FormsはHTMLで正常にレンダリングされません( `StandAlone` 値は、オブジェクトのメソッドに渡される `true` オブジェクトを使用して指定 `ApplicationWebRoot``ApplicationWebRoot``URLSpec``FormsServiceClient``(Deprecated) renderHTMLForm` されます)。 が、AEM formsをホ `ApplicationWebRoot` ストするサーバーの別のサーバーである場合は、管理コンソールのWebルートURIの値を、フォームのWebアプリケーションURIの値として設定する必要があります。 これは、管理コンソールにログインし、サービス/Formsをクリックし、WebルートURIをhttps://server-name:port/FormServerに設定することで実行できます。 次に、設定を保存します。

1. HTMLフォームのレンダリング

   オブジェクト `FormsServiceClient` のメソッドを `(Deprecated) renderHTMLForm` 呼び出し、次の値を渡します。

   * ファイル名の拡張子を含むフォームデザイン名を指定するstring値。 Formsアプリケーションの一部であるフォームデザインを参照する場合は、必ずなどの完全なパスを指定してくださ `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`い。
   * HTMLプ `TransformTo` リファレンスタイプを指定するenum値。 例えば、Internet Explorer 5.0以降用の動的HTMLと互換性のあるHTMLフォームをレンダリングするには、を指定します `TransformTo.MSDHTML`。
   * フォーム `com.adobe.idp.Document` とマージするデータを含むオブジェクトです。 データをマージしない場合は、空のオブジェクトを渡し `com.adobe.idp.Document` ます。
   * HTML実行 `HTMLRenderSpec` 時オプションを格納するオブジェクトです。
   * ヘッダー値を指定す `HTTP_USER_AGENT` るstring値。例えば、 `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * HTMLフォ `URLSpec` ームのレンダリングに必要なURI値を格納するオブジェクトです。
   * 添付フ `java.util.HashMap` ァイルを格納するオブジェクト。 これはオプションのパラメーターで、フォームにフ `null` ァイルを添付しないかどうかを指定できます。
   このメソ `(Deprecated) renderHTMLForm` ッドは、クライア `FormsResult` ントのWebブラウザーに書き込み可能なフォームデータストリームを含むオブジェクトを返します。

1. クライアントのWebブラウザーにフォームデータストリームを書き込みます

   * オブジェクトの `com.adobe.idp.Document` メソッドを呼び出して、オ `FormsResult` ブジェクトを作成 `getOutputContent` します。
   * メソッドを呼び出して、オブジェ `com.adobe.idp.Document` クトのコンテンツタイプを取得 `getContentType` します。
   * メソッドを呼 `javax.servlet.http.HttpServletResponse` び出し、オブジェクトのコンテンツタ `setContentType` イプを渡すことで、オブジェクトのコンテンツタイプを設定 `com.adobe.idp.Document` します。
   * オブジェクトの `javax.servlet.ServletOutputStream` メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに書き込むために使用する `javax.servlet.http.HttpServletResponse` オブジェクトを作 `getOutputStream` 成します。
   * オブジェクト `java.io.InputStream` のメソッドを呼び出して、オ `com.adobe.idp.Document` ブジェクトを作成 `getInputStream` します。
   * バイト配列を作成し、オブジェクトのメソッドを呼び出し、バイト配列を引数 `InputStream` として渡すこ `read` とで、フォームデータストリームを設定します。
   * オブジェクト `javax.servlet.ServletOutputStream` のメソッドを呼び `write` 出して、フォームデータストリームをクライアントWebブラウザーに送信します。 バイト配列をメソッドに渡し `write` ます。

**関連トピック**

[HTMLとしてのフォームのレンダリング](#rendering-forms-as-html)

[クイックスタート（SOAPモード）:Java APIを使用したHTMLフォームのレンダリング](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## WebサービスAPIを使用してフォームをHTMLとしてレンダリングする {#render-a-form-as-html-using-the-web-service-api}

Forms API（Webサービス）を使用してHTMLフォームをレンダリングします。

1. プロジェクトファイルを含める

   * FormsサービスWSDLを使用するJavaプロキシクラスを作成します。
   * クラスパスにJavaプロキシクラスを含めます。

1. フォームクライアントAPIオブジェクトの作成

   オブジェクト `FormsService` を作成し、認証値を設定します。

1. HTML実行時オプションの設定

   * Create an `HTMLRenderSpec` object by using its constructor.
   * ツールバーを使用してHTMLフォームをレンダリングするには、オブ `HTMLRenderSpec` ジェクトのメソッドを `setHTMLToolbar` 呼び出し、列挙値を渡 `HTMLToolbar` します。 例えば、垂直方向のHTMLツールバーを表示するには、を渡しま `HTMLToolbar.Vertical`す。
   * HTMLフォームのロケール値を設定するには、オブジェクトの `HTMLRenderSpec` メソッドを呼び出 `setLocale` し、ロケール値を指定するstring値を渡します。 For more information, see [AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * 完全なHTMLタグ内でHTMLフォームをレンダリングするには、オブジェクトの `HTMLRenderSpec` メソッドを呼び出 `setOutputType` して渡しま `OutputType.FullHTMLTags`す。
   >[!NOTE]
   このオプションを選択し、AEM formsをホストするJ2EEアプリケーションサーバー以外のサーバーを参照している場合、FormsはHTMLで正常にレンダリングされません( `StandAlone` 値は、オブジェクトのメソッドに渡される `true` オブジェクトを使用して指定 `ApplicationWebRoot``ApplicationWebRoot``URLSpec``FormsServiceClient``(Deprecated) renderHTMLForm` されます)。 が、AEM formsをホ `ApplicationWebRoot` ストするサーバーの別のサーバーである場合は、管理コンソールのWebルートURIの値を、フォームのWebアプリケーションURIの値として設定する必要があります。 これは、管理コンソールにログインし、サービス/Formsをクリックし、WebルートURIをhttps://server-name:port/FormServerに設定することで実行できます。 次に、設定を保存します。

1. HTMLフォームのレンダリング

   オブジェクト `FormsService` のメソッドを `(Deprecated) renderHTMLForm` 呼び出し、次の値を渡します。

   * ファイル名の拡張子を含むフォームデザイン名を指定するstring値。 Formsアプリケーションの一部であるフォームデザインを参照する場合は、必ずなどの完全なパスを指定してくださ `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`い。
   * HTMLプ `TransformTo` リファレンスタイプを指定するenum値。 例えば、Internet Explorer 5.0以降用の動的HTMLと互換性のあるHTMLフォームをレンダリングするには、を指定します `TransformTo.MSDHTML`。
   * フォーム `BLOB` とマージするデータを含むオブジェクトです。 データを結合しない場合は、を渡します `null`。 (「編集可能な [レイアウトでのフォームの自動埋め込み](/help/forms/developing/prepopulating-forms-flowable-layouts.md#prepopulating-forms-with-flowable-layouts)」を参照)。
   * HTML実行 `HTMLRenderSpec` 時オプションを格納するオブジェクトです。
   * ヘッダー値を指定す `HTTP_USER_AGENT` るstring値。例えば、 `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. この値を設定しない場合は、空の文字列を渡すことができます。
   * HTMLフォ `URLSpec` ームのレンダリングに必要なURI値を格納するオブジェクトです。 (URI値の [指定を参照](/help/forms/developing/rendering-interactive-pdf-forms.md))。
   * 添付フ `java.util.HashMap` ァイルを格納するオブジェクト。 これはオプションのパラメーターで、フォームにフ `null` ァイルを添付しないかどうかを指定できます。 (フォーム [へのファイルの添付を参照](/help/forms/developing/rendering-interactive-pdf-forms.md))。
   * メソッドに `com.adobe.idp.services.holders.BLOBHolder` よって入力される空のオブジェクトです。 このパラメーター値は、レンダリングされたフォームを保存します。
   * メソッドに `com.adobe.idp.services.holders.BLOBHolder` よって入力される空のオブジェクトです。 このパラメーターは、出力XMLデータを格納します。
   * メソッドに `javax.xml.rpc.holders.LongHolder` よって入力される空のオブジェクトです。 この引数は、フォーム内のページ数を格納します。
   * メソッドに `javax.xml.rpc.holders.StringHolder` よって入力される空のオブジェクトです。 この引数はロケールの値を格納します。
   * メソッドに `javax.xml.rpc.holders.StringHolder` よって入力される空のオブジェクトです。 この引数は、使用されるHTMLレンダリング値を格納します。
   * この操作 `com.adobe.idp.services.holders.FormsResultHolder` の結果を含む空のオブジェクトです。
   メソッド `(Deprecated) renderHTMLForm` は、最後の引 `com.adobe.idp.services.holders.FormsResultHolder` 数値として渡されたオブジェクトに、クライアントWebブラウザーに書き込む必要があるフォームデータストリームを入力します。

1. クライアントのWebブラウザーにフォームデータストリームを書き込みます

   * オブジェクト `FormResult` のデータメンバーの値を取得して、オ `com.adobe.idp.services.holders.FormsResultHolder` ブジェクトを `value` 作成します。
   * オブジェクトの `BLOB` メソッドを呼び出して、フォームデータを含むオ `FormsResult` ブジェクトを作成 `getOutputContent` します。
   * メソッドを呼び出して、オブジェ `BLOB` クトのコンテンツタイプを取得 `getContentType` します。
   * メソッドを呼 `javax.servlet.http.HttpServletResponse` び出し、オブジェクトのコンテンツタ `setContentType` イプを渡すことで、オブジェクトのコンテンツタイプを設定 `BLOB` します。
   * オブジェクトの `javax.servlet.ServletOutputStream` メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに書き込むために使用する `javax.servlet.http.HttpServletResponse` オブジェクトを作 `getOutputStream` 成します。
   * バイト配列を作成し、オブジェクトのメソッドを呼び出 `BLOB` して値を設定 `getBinaryData` します。 このタスクは、オブジェクトの内容をバ `FormsResult` イト配列に割り当てます。
   * オブジェクト `javax.servlet.http.HttpServletResponse` のメソッドを呼び `write` 出して、フォームデータストリームをクライアントWebブラウザーに送信します。 バイト配列をメソッドに渡し `write` ます。

**関連トピック**

[HTMLとしてのフォームのレンダリング](#rendering-forms-as-html)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

