---
title: FormsをHTMLとしてレンダリング
seo-title: FormsをHTMLとしてレンダリング
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
source-git-commit: c74d9e86727f2deda62b8d1eb105b28ef4b6d184
workflow-type: tm+mt
source-wordcount: '4108'
ht-degree: 1%

---


# FormsをHTMLとしてレンダリング{#rendering-forms-as-html}

Formsサービスは、WebブラウザーからのHTTP要求に応じてフォームをHTMLとしてレンダリングします。 HTML形式でフォームをレンダリングする利点は、クライアントWebブラウザーが配置されているコンピューターでは、Adobe Reader、Acrobat、Flash Player(フォームガイド（非推奨）用)が不要であることです。

フォームをHTMLとしてレンダリングするには、フォームデザインをXDPファイルとして保存する必要があります。 PDFファイルとして保存されたフォームデザインは、HTMLとしてレンダリングできません。 HTMLとしてレンダリングされるフォームデザインをDesignerで開発する場合は、次の条件を考慮します。

* フォームに線、ボックス、グリッドを描画するときに、オブジェクトの境界線プロパティを使用しないでください。ブラウザーによっては、 のプレビューで表示されるとおりに境界線が表示されないことがあります。また、オブジェクトが重なって表示されたり、他のオブジェクトを本来の位置から押しのけたりする場合があります。
* 線、長方形および円を使用して、背景を定義できます。
* テキストを収容するのに必要と思われる大きさよりも少し大きめにテキストを描画します。 Webブラウザーによっては、テキストが見やすく表示されない場合があります。

>[!NOTE]
>
>`FormServiceClient`オブジェクトの`(Deprecated) renderHTMLForm`メソッドと`renderHTMLForm2`メソッドを使用してTIFF画像を含むフォームをレンダリングすると、Internet ExplorerまたはMozilla Firefoxブラウザーに表示されるレンダリングされたHTMLフォームでTIFF画像が表示されません。 これらのブラウザーは、TIFF画像をネイティブでサポートしません。

## HTMLページ{#html-pages}

フォームデザインがHTMLフォームとしてレンダリングされると、2番目のレベルの各サブフォームがHTMLページ（パネル）としてレンダリングされます。 Designerでサブフォームの階層を表示できます。 ルートサブフォームに属する子サブフォーム（ルートサブフォームのデフォルト名はform1）がパネルサブフォームです。 次の例は、フォームデザインのサブフォームを示しています。

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

フォームデザインがHTMLフォームとしてレンダリングされる場合、パネルは特定のページサイズに制限されません。 ダイナミックサブフォームがある場合は、パネルサブフォーム内に階層化する必要があります。 ダイナミックサブフォームは、HTMLページを無限に拡大できます。

フォームをHTMLフォームとしてレンダリングする場合、ページサイズ（PDFとしてレンダリングされるフォームのページ番号付けに必要）は意味を持ちません。 編集可能なレイアウトを含むフォームはHTMLページを無限に多く含めることができるので、マスターページのフッターには挿入しないようにすることが重要です。 マスターページのコンテンツ領域の下にフッターがあると、ページの境界を越えてフローするHTMLコンテンツが上書きされる場合があります。

`xfa.host.pageUp`メソッドと`xfa.host.pageDown`メソッドを使用して、パネル間を明示的に移動する必要があります。 ページを変更するには、フォームをFormsサービスに送信し、Formsサービスでフォームをレンダリングしてクライアントデバイス（通常はWebブラウザー）に戻します。

>[!NOTE]
>
>フォームをFormsサービスに送信し、その後、Formsサービスがフォームをレンダリングしてクライアントデバイスに戻すプロセスを、サーバーへのラウンドトリッピングデータと呼びます。

>[!NOTE]
>
>HTMLフォーム上の「HTMLデジタル署名」ボタンの外観をカスタマイズする場合は、fscdigsig.cssファイル（adobe-forms-ds.ear/adobe-forms-ds.warファイル内）で次のプロパティを変更する必要があります。

**.fsc-ds-ssb**:このスタイルシートは、空白の記号フィールドの場合に適用されます。

**.fsc-ds-ssv**:このスタイルシートは、有効な署名フィールドの場合に適用されます。

**.fsc-ds-ssc**:このスタイルシートは、有効な署名フィールドがあるがデータが変更された場合に適用されます。

**.fsc-ds-ssi**:このスタイルシートは、無効な記号フィールドが含まれる場合に適用されます。

**.fsc-ds-popup-bg**:このスタイルシートプロパティは使用されていません。

**.fsc-ds-popup-btn**:このスタイルシートプロパティは使用されていません。

## スクリプト{#running-scripts}を実行中

フォーム作成者は、スクリプトをサーバー上で実行するか、クライアント上で実行するかを指定します。 Formsサービスは、フォームインテリジェンスを実行する分散イベント処理環境を作成します。このインテリジェンスは、`runAt`属性を使用して、クライアントとサーバーの間で配布できます。 この属性やフォームデザイン内でのスクリプトの作成について詳しくは、「[Formsデザイナ](https://www.adobe.com/go/learn_aemforms_designer_63)」を参照してください。

Formsサービスは、フォームのレンダリング中にスクリプトを実行できます。 その結果、クライアントで使用できないデータベースまたはWebサービスに接続して、フォームにデータを自動埋め込むことができます。 また、サーバー上で実行するボタンの`Click`イベントを設定して、クライアントがサーバーに旅行データを丸めるようにすることもできます。 これにより、ユーザーがフォームを操作している間に、エンタープライズデータベースなどのサーバーリソースを必要とする可能性のあるスクリプトをクライアントが実行できます。 HTMLフォームの場合、formcalcスクリプトはサーバー上でのみ実行できます。 その結果、`server`または`both`で実行するようにこれらのスクリプトにマークを付ける必要があります。

`xfa.host.pageUp`メソッドと`xfa.host.pageDown`メソッドを呼び出すと、ページ（パネル）間を移動するフォームをデザインできます。 このスクリプトはボタンの`Click`イベントに配置され、`runAt`属性は`Both`に設定されます。 `Both`を選択した理由は、（PDFとしてレンダリングされるフォームの）Adobe ReaderやAcrobatがサーバーに行かなくてもページを変更でき、HTMLフォームがサーバーにデータを丸めてページを変更できるようにすることです。 つまり、フォームがFormsサービスに送信され、フォームがHTMLとしてレンダリングされ、新しいページが表示されます。

スクリプト変数とフォームフィールドには、itemなどの同じ名前を付けないことをお勧めします。 Internet Explorerなど、一部のWebブラウザーでは、フォームフィールドと同じ名前の変数が初期化されず、スクリプトエラーが発生する場合があります。 フォームフィールドとスクリプト変数には異なる名前を付けることをお勧めします。

ページナビゲーション機能とフォームスクリプトの両方を含むHTMLフォームをレンダリングする場合（例えば、フォームをレンダリングするたびにスクリプトがデータベースからフィールドデータを取得するとします）、フォームスクリプトがform:readyeventではなくform:calculateイベントに配置されていることを確認します。

form:readyイベントにあるフォームスクリプトは、フォームの最初のレンダリング時に1回だけ実行され、以降のページ取得時には実行されません。 これに対し、form:calculateイベントは、フォームがレンダリングされるページナビゲーションごとに実行されます。

>[!NOTE]
複数ページのフォームでは、JavaScriptによってページに加えられた変更は、別のページに移動した場合にも保持されません。

フォームを送信する前にカスタムスクリプトを呼び出すことができます。 この機能は、利用可能なすべてのブラウザーで動作します。 ただし、`Output Type`プロパティが`Form Body`に設定されたHTMLフォームをレンダリングする場合にのみ使用できます。 `Output Type`が`Full HTML`の場合は動作しません。 この機能を設定する手順については、管理ヘルプの「フォームの設定」を参照してください。

フォームを送信する前に呼び出すコールバック関数を定義する必要があります。関数名は`_user_onsubmit`です。 関数が例外をスローしないと想定します。例外が発生した場合は無視されます。 JavaScript関数は、htmlのheadセクションに配置することをお勧めします。ただし、`xfasubset.js`を含むスクリプトタグの末尾より前の任意の場所で宣言できます。

formserverは、ドロップダウンリストを含むXDPをレンダリングするときに、ドロップダウンリストの作成に加えて、2つの非表示テキストフィールドを作成します。 これらのテキストフィールドには、ドロップダウンリストのデータが格納されます（一方にはオプションの表示名が格納され、もう一方にはオプションの値が格納されます）。 したがって、ユーザーがフォームを送信するたびに、ドロップダウンリストのデータ全体が送信されます。 毎回それほど多くのデータを送信したくない場合は、それを無効にするカスタムスクリプトを作成できます。 次に例を示します。ドロップダウンリストの名前は`drpOrderedByStateProv`で、サブフォームヘッダーの下に含まれます。 HTML入力要素の名前は`header[0].drpOrderedByStateProv[0]`になります。 ドロップダウンのデータを保存して送信する非表示フィールドの名前には、次の名前が付けられます。`header[0].drpOrderedByStateProv_DISPLAYITEMS_[0] header[0].drpOrderedByStateProv_VALUEITEMS_[0]`

データを投稿したくない場合は、これらの入力要素を次のように無効にできます。`var __CUSTOM_SCRIPTS_VERSION = 1; //enabling the feature function _user_onsubmit() { var elems = document.getElementsByName("header[0].drpOrderedByStateProv_DISPLAYITEMS_[0]"); elems[0].disabled = true; elems = document.getElementsByName("header[0].drpOrderedByStateProv_VALUEITEMS_[0]"); elems[0].disabled = true; }`

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

HTMLとしてレンダリングするフォームデザインを作成する場合、JavaScript言語のスクリプトのXFAサブセットに制限する必要があります。

クライアント上で実行するスクリプト、またはクライアントとサーバーの両方で実行するスクリプトは、XFAサブセット内で記述する必要があります。 サーバー上で実行するスクリプトは、完全なXFAスクリプティングモデルを使用でき、FormCalcも使用できます。 JavaScriptの使用について詳しくは、[Formsデザイナ](https://www.adobe.com/go/learn_aemforms_designer_63)を参照してください。

クライアントでスクリプトを実行する場合、現在表示されているパネルのみがスクリプトを使用できます。例えば、パネルBが表示されている場合に、パネルAにあるフィールドに対してスクリプトを作成することはできません。 サーバーでスクリプトを実行する場合は、すべてのパネルにアクセスできます。

また、クライアント上で実行するスクリプト内でスクリプティングオブジェクトモデル(SOM)式を使用する場合は、注意が必要です。 クライアントで実行されるスクリプトでは、SOM式の簡素化されたサブセットのみがサポートされます。

## イベントのタイミング{#event-timing}

XFAサブセットは、HTMLイベントにマップされるXFAイベントを定義します。 イベントの計算と検証のタイミングに関しては、動作に若干の違いがあります。 Webブラウザーでは、フィールドを終了すると完全な計算イベントが実行されます。 フィールドの値を変更しても、計算イベントは自動的には実行されません。 `xfa.form.execCalculate`メソッドを呼び出すと、強制的にcalculateイベントを実行できます。

Webブラウザーでは、フィールドを終了するかフォームを送信する場合にのみ、検証イベントが実行されます。 `xfa.form.execValidate`メソッドを使用して、検証イベントを強制的に実行できます。

(Adobe ReaderやAcrobatとは対照的に)Webブラウザーに表示されるFormsは、必須フィールドのXFAのnullテスト（エラーまたは警告）に準拠しています。

* nullテストによってエラーが発生し、値を指定せずにフィールドを終了すると、メッセージボックスが表示され、「OK」をクリックした後にフィールドに移動されます。
* Nullテストを実行すると警告が表示され、値を指定せずにフィールドを終了した場合は、[OK]または[キャンセル]をクリックするように求められ、値を指定せずに続行するか、フィールドに戻って値を入力するかを選択できます。

nullテストについて詳しくは、[Formsデザイナー](https://www.adobe.com/go/learn_aemforms_designer_63)を参照してください。

## フォームボタン{#form-buttons}

送信ボタンをクリックすると、フォームデータがFormsサービスに送信され、フォーム処理の終了を表します。 `preSubmit`イベントは、クライアントまたはサーバーで実行するように設定できます。 `preSubmit`イベントは、フォーム送信の前に実行されます（クライアント上で実行するように設定されている場合）。 それ以外の場合は、フォームの送信中に`preSubmit`イベントがサーバー上で実行されます。 `preSubmit`イベントについて詳しくは、[Formsデザイナ](https://www.adobe.com/go/learn_aemforms_designer_63)を参照してください。

ボタンにクライアントサイドのスクリプトが関連付けられていない場合、データはサーバーに送信され、サーバーで計算が実行され、HTMLフォームが再生成されます。 ボタンにクライアントサイドのスクリプトが含まれている場合、データはサーバーに送信されず、クライアントサイドのスクリプトがWebブラウザーで実行されます。

## HTML 4.0 Webブラウザー{#html-4-0-web-browser}

HTML 4.0のみをサポートするWebブラウザーは、XFAサブセットのクライアント側スクリプティングモデルをサポートできません。 HTML 4.0とMSDHTML、またはCSS2HTMLの両方で動作するフォームデザインを作成する場合、クライアントで実行するようにマークされたスクリプトは、実際にサーバー上で実行されます。 例えば、ユーザーがHTML 4.0 Webブラウザーに表示されているフォーム上のボタンをクリックしたとします。 この場合、フォームデータはクライアントサイドスクリプトが実行されるサーバーに送信されます。

フォームロジックはcalculateイベントに配置することをお勧めします。これはHTML 4.0のサーバーで実行し、MSDHTMLまたはCSS2HTMLのクライアントで実行します。

## プレゼンテーションの変更の管理{#maintaining-presentation-changes}

HTMLページ（パネル）間を移動すると、データの状態のみが維持されます。 背景色や必須フィールドの設定などの設定は維持されません（初期設定と異なる場合）。 プレゼンテーション状態を維持するには、フィールドのプレゼンテーション状態を表すフィールド（通常は非表示）を作成する必要があります。 フィールドの`Calculate`イベントに、非表示のフィールド値に基づいて表示を変更するスクリプトを追加すると、HTMLページ（パネル）間を移動する際に表示状態を保持できます。

次のスクリプトでは、`hiddenField`の値に基づいてフィールドの`fillColor`を維持します。 このスクリプトがフィールドの`Calculate`イベントー内にあるとします。

```java
     If (hiddenField.rawValue == 1)
         this.fillColor = "255,0,0"
     else
         this.fillColor = "0,255,0"
```

>[!NOTE]
テーブルのセル内にネストされている場合、レンダリングされたHTMLフォームにスタティックオブジェクトは表示されません。 例えば、テーブルセル内にネストされた円や長方形は、レンダリングHTMLフォーム内に表示されません。 ただし、テーブルの外側に配置した場合は、これらの同じスタティックオブジェクトが正しく表示されます。

## HTMLフォームへのデジタル署名{#digitally-signing-html-forms}

電子署名フィールドを含むHTMLフォームを、次のHTML変換のいずれかとしてレンダリングする場合は、このフォームに署名することはできません。

* AHTML
* HTML4
* StaticHTML
* NoScriptXHTML

ドキュメントのデジタル署名について詳しくは、[デジタル署名と認証ドキュメント](/help/forms/developing/digitally-signing-certifying-documents.md)を参照してください

## アクセシビリティガイドラインに準拠したXHTMLフォーム{#rendering-an-accessibility-guidelines-compliant-xhtml-form}のレンダリング

アクセシビリティガイドラインに準拠した完全なHTMLフォームをレンダリングできます。 つまり、フォームは完全なHTMLタグ内でレンダリングされ、HTMLフォームはbodyタグ内（完全なHTMLページではありません）でレンダリングされます。

## フォームデータを検証中{#validating-form-data}

フォームをHTMLフォームとしてレンダリングする場合は、フォームフィールドの検証ルールの使用を制限することをお勧めします。 一部の検証ルールは、HTMLフォームでサポートされていない場合があります。 例えば、HTMLフォームとしてレンダリングされるフォームデザイン内の`Date/Time`フィールドにMM-DD-YYYYの検証パターンを適用した場合、日付が正しく入力されていても、正しく機能しません。 ただし、この検証パターンは、PDFとしてレンダリングされたフォームで正しく機能します。

>[!NOTE]
Formsサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

## 手順{#summary-of-steps}の概要

HTMLフォームをレンダリングするには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. FormsクライアントAPIオブジェクトを作成します。
1. HTML実行時オプションを設定します。
1. HTMLフォームをレンダリングする。
1. フォームデータストリームをクライアントのWebブラウザーに書き込みます。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めてください。

**FormsクライアントAPIオブジェクトの作成**

プログラムでデータをPDF formClient APIに読み込む前に、Form Data Integrationサービスクライアントを作成する必要があります。 サービスクライアントを作成する場合、サービスの呼び出しに必要な接続設定を定義します。

**HTML実行時オプションの設定**

HTMLフォームをレンダリングする場合は、HTML実行時オプションを設定します。 例えば、HTMLフォームにツールバーを追加して、クライアントコンピューター上の添付ファイルを選択したり、HTMLフォームと共にレンダリングされる添付ファイルを取得したりできます。 デフォルトでは、HTMLツールバーは無効です。 HTMLフォームにツールバーを追加するには、実行時のオプションをプログラムで設定する必要があります。 デフォルトでは、HTMLツールバーは次のボタンで構成されます。

* `Home`:アプリケーションのWebルートへのリンクを提供します。
* `Upload`:現在のフォームに添付するファイルを選択するためのユーザーインターフェイスです。
* `Download`:添付ファイルを表示するユーザーインターフェイスを提供します。

HTMLフォームにHTMLツールバーが表示される場合、ユーザーは最大10個のファイルを選択して、フォームデータと共に送信できます。 ファイルが送信されると、Formsサービスはファイルを取得できます。

フォームをHTMLとしてレンダリングする場合、ユーザーエージェントの値を指定できます。 user-agent値は、ブラウザーとシステムの情報を提供します。 これはオプションの値で、空の文字列値を渡すことができます。 Java APIを使用したHTMLフォームのレンダリングクイック開始では、ユーザーエージェントの値を取得し、それを使用してフォームをHTMLとしてレンダリングする方法を示しています。

フォームデータが投稿されるHTTP URLは、FormsサービスクライアントAPIを使用してターゲットURLを設定することで指定できます。また、XDPフォームデザインに含まれる「送信」ボタンで指定することもできます。 フォームデザインでターゲットURLが指定されている場合は、FormsサービスクライアントAPIを使用して値を設定しないでください。

>[!NOTE]
ツールバーを使用したHTMLフォームのレンダリングはオプションです。

>[!NOTE]
AHTMLフォームをレンダリングする場合は、ツールバーをフォームに追加しないことをお勧めします。

**HTMLフォームのレンダリング**

HTMLフォームをレンダリングするには、Designerで作成し、XDPファイルとして保存するフォームデザインを指定する必要があります。 また、HTML変換タイプを選択する必要もあります。 例えば、Internet Explorer 5.0以降用の動的HTMLをレンダリングするHTML変換タイプを指定できます。

HTMLフォームのレンダリングには、他のフォームタイプのレンダリングに必要なURI値などの値も必要です。

**フォームデータストリームをクライアントのWebブラウザーに書き込みます**

Formsサービスは、HTMLフォームをレンダリングすると、フォームデータストリームを返します。このストリームは、クライアントのWebブラウザーに書き込む必要があります。 クライアントのWebブラウザーに書き込むと、HTMLフォームがユーザーに表示されます。

**関連トピック**

[Java APIを使用してフォームをHTMLとしてレンダリングする](#render-a-form-as-html-using-the-java-api)

[WebサービスAPIを使用してフォームをHTMLとしてレンダリングする](#render-a-form-as-html-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[FormsサービスAPIクイック開始](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[インタラクティブPDF formsのレンダリング](/help/forms/developing/rendering-interactive-pdf-forms.md)

[カスタムツールバーでのHTMLFormsのレンダリング](/help/forms/developing/rendering-html-forms-custom-toolbars.md)

[FormsをレンダリングするWeb アプリケーションの作成](/help/forms/developing/creating-web-applications-renders-forms.md)

## Java API {#render-a-form-as-html-using-the-java-api}を使用してフォームをHTMLとしてレンダリングする

FormsAPI(Java)を使用してHTMLフォームをレンダリングする：

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-forms-client.jarなどのクライアントJARファイルを含めます。

1. FormsクライアントAPIオブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用し、`FormsServiceClient`オブジェクトを渡して、`ServiceClientFactory`オブジェクトを作成します。

1. HTML実行時オプションの設定

   * コンストラクターを使用して`HTMLRenderSpec`オブジェクトを作成します。
   * ツールバーを含むHTMLフォームをレンダリングするには、`HTMLRenderSpec`オブジェクトの`setHTMLToolbar`メソッドを呼び出し、`HTMLToolbar`列挙値を渡します。 例えば、垂直方向のHTMLツールバーを表示するには、`HTMLToolbar.Vertical`を渡します。
   * HTMLフォームのロケール値を設定するには、`HTMLRenderSpec`オブジェクトの`setLocale`メソッドを呼び出し、ロケール値を指定する文字列値を渡します。 （これはオプションの設定です）。
   * 完全なHTMLタグ内にHTMLフォームをレンダリングするには、`HTMLRenderSpec`オブジェクトの`setOutputType`メソッドを呼び出し、`OutputType.FullHTMLTags`を渡します。 （これはオプションの設定です）。

   >[!NOTE]
   `StandAlone`オプションが`true`で、`ApplicationWebRoot`がAEM FormsをホストするJ2EEアプリケーションサーバー以外のサーバーを参照している場合、FormsはHTMLで正常にレンダリングされません（`ApplicationWebRoot`値は、`FormsServiceClient`オブジェクトの`(Deprecated) renderHTMLForm`メソッドに渡される`URLSpec`オブジェクトを使用して指定されます）。 `ApplicationWebRoot`がホストサーバーの別のサーバーである場合は、管理コンソールのWebルートURIの値をフォームのWebアプリケーションのURI値として設定する必要があります。 これを行うには、管理コンソールにログインし、サービス/Formsをクリックし、WebルートURIをhttps://server-name:port/FormServerに設定します。 次に、設定を保存します。

1. HTMLフォームのレンダリング

   `FormsServiceClient`オブジェクトの`(Deprecated) renderHTMLForm`メソッドを呼び出し、次の値を渡します。

   * ファイル名拡張子を含むフォームデザイン名を指定するstring値。 Formsアプリケーションの一部であるフォームデザインを参照する場合は、`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`など、完全なパスを必ず指定してください。
   * HTML環境設定の種類を指定する`TransformTo`列挙値。 例えば、Internet Explorer 5.0以降用の動的HTMLと互換性のあるHTMLフォームをレンダリングするには、`TransformTo.MSDHTML`を指定します。
   * フォームとマージするデータを含む`com.adobe.idp.Document`オブジェクト。 データをマージしない場合は、空の`com.adobe.idp.Document`オブジェクトを渡します。
   * HTML実行時オプションを格納する`HTMLRenderSpec`オブジェクト。
   * `HTTP_USER_AGENT`ヘッダー値を指定するstring値。例：`Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`
   * HTMLフォームのレンダリングに必要なURI値を格納する`URLSpec`オブジェクト。
   * 添付ファイルを格納する`java.util.HashMap`オブジェクト。 これはオプションのパラメーターです。フォームにファイルを添付しない場合は、`null`を指定できます。

   `(Deprecated) renderHTMLForm`メソッドは、クライアントのWebブラウザーに書き込み可能なフォームデータストリームを含む`FormsResult`オブジェクトを返します。

1. フォームデータストリームをクライアントのWebブラウザーに書き込みます

   * `FormsResult`オブジェクト&#39;s `getOutputContent`メソッドを呼び出して、`com.adobe.idp.Document`オブジェクトを作成します。
   * `getContentType`メソッドを呼び出して、`com.adobe.idp.Document`オブジェクトのコンテンツタイプを取得します。
   * `javax.servlet.http.HttpServletResponse`オブジェクトのコンテンツタイプを設定するには、`setContentType`メソッドを呼び出し、`com.adobe.idp.Document`オブジェクトのコンテンツタイプを渡します。
   * `javax.servlet.http.HttpServletResponse`オブジェクトの`getOutputStream`メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに書き込むために使用する`javax.servlet.ServletOutputStream`オブジェクトを作成します。
   * `com.adobe.idp.Document`オブジェクトの`getInputStream`メソッドを呼び出して、`java.io.InputStream`オブジェクトを作成します。
   * バイト配列を作成し、`InputStream`オブジェクトの`read`メソッドを呼び出して、バイト配列を引数として渡すことで、フォームデータストリームを設定します。
   * `javax.servlet.ServletOutputStream`オブジェクトの`write`メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに送信します。 バイト配列を`write`メソッドに渡します。

**関連トピック**

[FormsをHTMLとしてレンダリング](#rendering-forms-as-html)

[クイック開始（SOAPモード）:Java APIを使用したHTMLフォームのレンダリング](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## WebサービスAPI {#render-a-form-as-html-using-the-web-service-api}を使用してフォームをHTMLとしてレンダリングする

FormsAPI（Webサービス）を使用してHTMLフォームをレンダリングします。

1. プロジェクトファイルを含める

   * FormsサービスのWSDLを使用するJavaプロキシクラスを作成します。
   * クラスパスにJavaプロキシクラスを含めます。

1. FormsクライアントAPIオブジェクトの作成

   `FormsService`オブジェクトを作成し、認証値を設定します。

1. HTML実行時オプションの設定

   * コンストラクターを使用して`HTMLRenderSpec`オブジェクトを作成します。
   * ツールバーを含むHTMLフォームをレンダリングするには、`HTMLRenderSpec`オブジェクトの`setHTMLToolbar`メソッドを呼び出し、`HTMLToolbar`列挙値を渡します。 例えば、垂直方向のHTMLツールバーを表示するには、`HTMLToolbar.Vertical`を渡します。
   * HTMLフォームのロケール値を設定するには、`HTMLRenderSpec`オブジェクトの`setLocale`メソッドを呼び出し、ロケール値を指定する文字列値を渡します。 詳しくは、[AEM FormsAPIリファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)を参照してください。
   * 完全なHTMLタグ内にHTMLフォームをレンダリングするには、`HTMLRenderSpec`オブジェクトの`setOutputType`メソッドを呼び出し、`OutputType.FullHTMLTags`を渡します。

   >[!NOTE]
   `StandAlone`オプションが`true`で、`ApplicationWebRoot`がAEM FormsをホストするJ2EEアプリケーションサーバー以外のサーバーを参照している場合、FormsはHTMLで正常にレンダリングされません（`ApplicationWebRoot`値は、`FormsServiceClient`オブジェクトの`(Deprecated) renderHTMLForm`メソッドに渡される`URLSpec`オブジェクトを使用して指定されます）。 `ApplicationWebRoot`がホストサーバーの別のサーバーである場合は、管理コンソールのWebルートURIの値をフォームのWebアプリケーションのURI値として設定する必要があります。 これを行うには、管理コンソールにログインし、サービス/Formsをクリックし、WebルートURIをhttps://server-name:port/FormServerに設定します。 次に、設定を保存します。

1. HTMLフォームのレンダリング

   `FormsService`オブジェクトの`(Deprecated) renderHTMLForm`メソッドを呼び出し、次の値を渡します。

   * ファイル名拡張子を含むフォームデザイン名を指定するstring値。 Formsアプリケーションの一部であるフォームデザインを参照する場合は、`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`など、完全なパスを必ず指定してください。
   * HTML環境設定の種類を指定する`TransformTo`列挙値。 例えば、Internet Explorer 5.0以降用の動的HTMLと互換性のあるHTMLフォームをレンダリングするには、`TransformTo.MSDHTML`を指定します。
   * フォームとマージするデータを含む`BLOB`オブジェクト。 データを結合したくない場合は、`null`を渡します。 (「[編集可能なレイアウトでFormsを自動埋め込む](/help/forms/developing/prepopulating-forms-flowable-layouts.md#prepopulating-forms-with-flowable-layouts)」を参照)。
   * HTML実行時オプションを格納する`HTMLRenderSpec`オブジェクト。
   * `HTTP_USER_AGENT`ヘッダー値を指定するstring値。例：`Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)` この値を設定したくない場合は、空の文字列を渡すことができます。
   * HTMLフォームのレンダリングに必要なURI値を格納する`URLSpec`オブジェクト。 （[URI値の指定](/help/forms/developing/rendering-interactive-pdf-forms.md)を参照）。
   * 添付ファイルを格納する`java.util.HashMap`オブジェクト。 これはオプションのパラメーターです。フォームにファイルを添付しない場合は、`null`を指定できます。 （[フォームへのファイルの添付](/help/forms/developing/rendering-interactive-pdf-forms.md)を参照）。
   * メソッドによって入力される空の`com.adobe.idp.services.holders.BLOBHolder`オブジェクト。 このパラメーター値は、レンダリングされたフォームを保存します。
   * メソッドによって入力される空の`com.adobe.idp.services.holders.BLOBHolder`オブジェクト。 このパラメーターは、出力XMLデータを格納します。
   * メソッドによって入力される空の`javax.xml.rpc.holders.LongHolder`オブジェクト。 この引数は、フォームのページ数を格納します。
   * メソッドによって入力される空の`javax.xml.rpc.holders.StringHolder`オブジェクト。 この引数はロケールの値を格納します。
   * メソッドによって入力される空の`javax.xml.rpc.holders.StringHolder`オブジェクト。 この引数は、使用されるHTMLレンダリング値を格納します。
   * この操作の結果を含む空の`com.adobe.idp.services.holders.FormsResultHolder`オブジェクトです。

   `(Deprecated) renderHTMLForm`メソッドは、最後の引数値として渡される`com.adobe.idp.services.holders.FormsResultHolder`オブジェクトに、クライアントWebブラウザーに書き込む必要のあるフォームデータストリームを入力します。

1. フォームデータストリームをクライアントのWebブラウザーに書き込みます

   * `com.adobe.idp.services.holders.FormsResultHolder`オブジェクトの`value`データメンバの値を取得して、`FormResult`オブジェクトを作成します。
   * `FormsResult`オブジェクトの`getOutputContent`メソッドを呼び出して、フォームデータを含む`BLOB`オブジェクトを作成します。
   * `getContentType`メソッドを呼び出して、`BLOB`オブジェクトのコンテンツタイプを取得します。
   * `javax.servlet.http.HttpServletResponse`オブジェクトのコンテンツタイプを設定するには、`setContentType`メソッドを呼び出し、`BLOB`オブジェクトのコンテンツタイプを渡します。
   * `javax.servlet.http.HttpServletResponse`オブジェクトの`getOutputStream`メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに書き込むために使用する`javax.servlet.ServletOutputStream`オブジェクトを作成します。
   * バイト配列を作成し、`BLOB`オブジェクトの`getBinaryData`メソッドを呼び出して値を設定します。 このタスクは、`FormsResult`オブジェクトの内容をバイト配列に割り当てます。
   * `javax.servlet.http.HttpServletResponse`オブジェクトの`write`メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに送信します。 バイト配列を`write`メソッドに渡します。

**関連トピック**

[FormsをHTMLとしてレンダリング](#rendering-forms-as-html)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

