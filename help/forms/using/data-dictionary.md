---
title: データディクショナリ
description: Correspondence Management のデータ辞書を使用すると、顧客対応で使用する入力としてバックエンドのデータをレターに統合できます。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
docset: aem65
feature: Correspondence Management
exl-id: aaed75e6-8849-46a8-b986-896ad729adda
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '3842'
ht-degree: 24%

---

# データディクショナリ{#data-dictionary}

## はじめに {#introduction}

ビジネスユーザーは、データディクショナリを使用することで、基になるデータモデルの技術的な詳細を知ることなく、バックエンドデータソースの情報を使用できます。 データディクショナリは、データディクショナリ要素 (DDE) で構成されます。 これらのデータ要素を使用して、顧客通信で使用するための入力としてバックエンドデータをレターに統合します。

データディクショナリは、基盤となるデータ構造とその関連属性を記述するメタデータを独立して表したものです。 データディクショナリは、ビジネス語彙を使用して作成されます。 基になる 1 つ以上のデータモデルにマッピングできます。

データディクショナリは、単純要素、複合要素、コレクション要素の 3 種類の要素で構成されています。 単純 DDE は、文字列、数値、日付、Boolean 値などのプリミティブ要素で、市区町村名などの情報を保持します。 複合 DDE には、他の DDE が含まれます。この DDE は、プリミティブ、複合、コレクションのいずれかのタイプにすることができます。 例として、郵便番号、国、都道府県、市町村、地名、番地で構成される住所が挙げられます。コレクションは、類似した単純 DDE または複合 DDE のリストです。 例えば、複数の場所を持つ顧客や、請求先と配送先の住所が異なる顧客などです。

Correspondence Management は、データディクショナリの構造に従って保存されたバックエンド、顧客、または受信者固有のデータを使用して、様々な顧客向けの通信を作成します。 例えば、「{First Name} 様」や「Mr. {姓}様」などの名前を使用できます。

通常、ビジネスユーザーは、XSD（XML スキーマ）や Java クラスなどのメタデータ表現に関する知識は必要ありません。 ただし、通常はソリューションを構築するために、これらのデータ構造や属性へのアクセスが必要となります。

### データディクショナリのワークフロー {#data-dictionary-workflow}

1. 作成者 [データディクショナリを作成します。](#createdatadictionary) スキーマをアップロードするか、または最初からアップロードする。
1. 作成者はデータディクショナリに基づいてレターとインタラクティブ通信を作成し、レターとインタラクティブ通信のデータディクショナリ要素を必要な箇所に関連付けます。
1. 作成者はサンプルデータの XML ファイルをダウンロードできます。これはデータディクショナリのスキーマに基づいたものです。作成者はサンプルデータの XML ファイルを編集できます。これはテストデータとしてデータディクショナリに関連付けることができます。レターのプレビューでも同様の操作が可能です。
1. [レターのプレビュー](../../forms/using/create-letter.md#p-types-of-linkage-available-for-each-of-the-fields-p)時に、作成者はデータが入ったレターをプレビューすることを選択できます（カスタムプレビュー）。作成者が提供したデータが入力された状態でレターが開きます。通信を作成するインターフェイスが開きます。このレターをプレビューしているエージェントは、レターのコンテンツ、データ、および添付ファイルを変更して最終的なレターを送信できます。レターの作成について詳しくは、[通信の作成](../../forms/using/create-letter.md)を参照してください。

## 前提条件 {#prerequisite}

[互換パッケージ](compatibility-package.md)をインストールし、「**フォーム**」ページで「**データディクショナリ**」オプションを表示します。

## データディクショナリの作成 {#createdatadictionary}

データディクショナリの作成にはデータディクショナリエディターを使用します。または、XSD スキーマファイルをアップロードして、そのファイルに基づくデータディクショナリを作成することもできます。 その後、フィールドを含む必要な情報をさらに追加して、データディクショナリを拡張できます。 データディクショナリの作成方法に関係なく、ビジネスプロセスの所有者は、バックエンドシステムに関する知識を必要としません。 ビジネスプロセスの所有者は、プロセスのドメインオブジェクトとその定義に関する知識のみ必要です。

>[!NOTE]
>
>類似の要素を必要とする複数のレターに対して、共通のデータディクショナリを作成できます。 ただし、要素数が多い大きなデータディクショナリを使用すると、データディクショナリを使用してレターやドキュメントフラグメントなどの要素を読み込む際に、パフォーマンスの問題が発生する可能性があります。 パフォーマンスの問題が発生した場合は、異なるレターに対して別々のデータ辞書を作成するようにしてください。

1. 選択 **Forms** > **データディクショナリ**.
1. 選択 **データ辞書を作成**.
1. プロパティ画面で以下を追加します。

   * **タイトル：**（オプション）データディクショナリのタイトルを入力します。タイトルは一意である必要はなく、特殊文字や英語以外の文字を含めることができます。 レターやその他のドキュメントフラグメントは、サムネールやアセットプロパティなど、タイトル（使用可能な場合）と共に参照されます。 データディクショナリは、タイトルではなく名前で参照されます。
   * **名前：** データディクショナリの一意の名前。 「名前」フィールドに入力できるのは、英語の文字、数字、ハイフンのみです。「名前」フィールドは「タイトル」フィールドに基づいて自動的に入力され、「タイトル」フィールドに入力された特殊文字、スペース、数字および英語以外の文字はハイフンに置き換えられます。 「タイトル」フィールドの値は「名前」フィールドに自動的にコピーされますが、値を編集することもできます。

   * **説明**：（オプション）データディクショナリの説明。
   * **タグ**：（オプション）カスタムタグを作成するには、テキストフィールドに値を入力して Enter を押します。タグのテキストフィールドの下にタグが表示されます。このテキストを保存すると、新しく追加されたタグも作成されます。
   * **拡張プロパティ**: （オプション） Select **フィールドを追加** データディクショナリのメタデータ属性を指定します。 [ プロパティ名 ] 列に、一意のプロパティ名を入力します。 「値」列に、プロパティに関連付ける値を入力します。

   ![ドイツ語で指定されたデータディクショナリプロパティ](do-not-localize/1_ddproperties.png)

1. （オプション）データディクショナリの XSD スキーマ定義をアップロードするには、データディクショナリの構造ウィンドウで、 **XML スキーマをアップロード**. XSD ファイルを参照して選択し、選択します。 **開く**. アップロードされた XML スキーマに基づいてデータ辞書が作成されます。 データディクショナリ内の要素の表示名や説明を調整する必要があります。 これを行うには、要素の名前をタップして選択し、右側のペインのフィールドで説明、表示名、およびその他の詳細を編集します。

   計算済み DD 要素について詳しくは、「[計算済みデータディクショナリ要素](#computedddelements)」を参照してください。

   >[!NOTE]
   >
   >ユーザーインターフェイスを使用して、スキーマファイルのアップロードをスキップし、最初からデータディクショナリを作成することができます。 これをおこなうには、この手順をスキップし、次の手順に進みます。

1. 「**次へ**」を選択します。
1. プロパティを追加画面で、データディクショナリに要素を追加します。 また、データディクショナリの基本構造を取得するためにスキーマをアップロードした場合は、要素を追加または削除し、その詳細を編集できます。

   要素の右側にある 3 つのドットを選択し、データディクショナリの構造に要素を追加できます。

   ![1_2_createanelement](assets/1_2_createanelement.png)

   「複合要素」、「コレクション要素」、または「プリミティブ要素」を選択します。

   * 複合 DDE には、他の DDE が含まれます。この DDE は、プリミティブ、複合、コレクションのいずれかのタイプにすることができます。 例として、郵便番号、国、都道府県、市町村、地名、番地で構成される住所が挙げられます。
   * プリミティブ DDE は、文字列、数値、日付、ブール値などの要素であり、都市名などの情報を保持します。
   * コレクションは、類似した単純 DDE または複合 DDE のリストです。 例えば、複数の場所を持つ顧客や、請求先と配送先の住所が異なる顧客などです。

   次に、データディクショナリの作成に関するルールを示します。

   * 複合タイプのみが、データディクショナリ内のトップレベル DDE として使用できます。
   * 名前、参照名および要素タイプは、データディクショナリと DDE において必須のフィールドです。
   * 参照名は一意である必要があります。
   * 親 DDE（複合）には、同じ名前の 2 つの子を指定できません。
   * 列挙型には、プリミティブな String 型のみが含まれます。

   複合要素、コレクション要素、プリミティブ要素について、およびデータディクショナリ要素の操作について詳しくは、[データディクショナリ要素の XML スキーマへのマッピング](#mappingddetoschema)を参照してください。

   データディクショナリにおける検証について詳しくは、[データディクショナリエディターの検証](#ddvalidations)を参照してください。

   ![2_addddpropertiesbasic](assets/2_addddpropertiesbasic.png)

1. （オプション）要素を選択後に、「詳細設定」タブでプロパティ（属性）を追加できます。また、 **フィールドを追加** DD 要素のプロパティを拡張します。

   ![3_addddpropertiesadvanced](assets/3_addddpropertiesadvanced.png)

1. （オプション）要素の右側の 3 つのドットをタップして「**削除**」を選択すると、要素を削除できます。

   ![4_deleteelement](assets/4_deleteelement.png)

   >[!NOTE]
   >
   >子ノードを持つ複合要素またはコレクション要素を削除すると、その子ノードも削除されます。

1. （オプション）データディクショナリの構造ウィンドウの、フィールドと変数のリストパネルで要素を選択します。 要素に関連付けられた必要な属性を変更または追加します。
1. 「**保存**」を選択します。

### 1 つ以上のデータディクショナリのコピーを作成します {#create-copies-of-one-or-more-data-dictionary}

既存のデータディクショナリに類似したプロパティと要素を持つ 1 つ以上のデータディクショナリをすばやく作成するには、それらをコピーして貼り付けます。

1. データディクショナリのリストから、適切なデータディクショナリを選択します。 UI に「コピー」アイコンが表示されます。
1. 「コピー」を選択します。 UI に貼り付けアイコンが表示されます。
1. 「貼り付け」を選択します。 貼り付けダイアログが表示されます。新しいデータディクショナリに名前とタイトルが自動的に割り当てられます。
1. 必要に応じて、データディクショナリのコピーを保存するタイトルと名前を編集します。
1. 「貼り付け」を選択します。 データディクショナリのコピーが作成されます。これで、新しく作成されたデータディクショナリで必要な変更を行うことができます。

## データディクショナリ要素を参照するドキュメントフラグメントまたは文書を確認する {#see-the-document-fragments-or-documents-that-refer-to-a-data-dictionary-element}

データディクショナリの編集中または表示中に、データディクショナリ内のどの要素がどのテキスト、条件、レター、およびインタラクティブ通信で参照されているかを確認できます。

1. データディクショナリを編集するには、次のいずれかの操作を行います。

   * データディクショナリにカーソルを合わせ、「編集」を選択します。
   * データディクショナリを選択し、ヘッダーで「編集」を選択します。
   * データディクショナリにカーソルを合わせ、「選択」を選択します。 次に、ヘッダーで「編集」を選択します。

   または、データディクショナリを選択して表示します。

1. データディクショナリで、単純な要素を選択して選択します。 複合要素とコレクション要素には参照がありません。

   要素の基本プロパティ、詳細プロパティと共に「貸したコンテンツ」も表示されます。

1. 「貸したコンテンツ」を選択します。

   「貸したコンテンツ」タブには、テキスト、条件、レター、インタラクティブ通信といった内容が表示されます。 これらの見出しのそれぞれには、選択した要素への参照数も表示されます。

1. 要素を参照するアセットの名前を確認するには、見出しを選択します。

   ![lentcontent](assets/lentcontent.png)

1. 別の要素の貸したコンテンツを表示するには、要素を選択します。
1. 要素を参照するアセットを表示するには、その名前を選択します。 アセット、レター、またはインタラクティブ通信がブラウザーに表示されます。

## テストデータの操作 {#working-with-test-data}

1. データディクショナリページで、を選択します。 **選択**.
1. テストデータをダウンロードするデータディクショナリを選択し、「 」を選択します。 **サンプル XML データをダウンロード**.
1. 選択 **OK** （アラートメッセージ内） XML ファイルがダウンロードされます。
1. XML ファイルを Notepad または別の XML エディターで開きます。 XML ファイルは、データディクショナリと要素内のプレースホルダー文字列と同じ構造を持っています。 レターをテストするデータで、プレースホルダー文字列を置き換えます。

   ```xml
   <?xml version="1.0" encoding="UTF-8" standalone="no"?>
   <Company>
   <Name>string</Name>
   <Type>string</Type>
   <HeadOfficeAddress>
   <Street>string</Street>
   <City>string</City>
   <State>string</State>
   <Zip>string</Zip>
   </HeadOfficeAddress>
   <SalesOfficeAddress>
   <Street>string</Street>
   <City>string</City>
   <State>string</State>
   <Zip>string</Zip>
   </SalesOfficeAddress>
   <HeadCount>1.0</HeadCount>
   <CEO>
   <PersonName>
   <FirstName>string</FirstName>
   <MiddleName>string</MiddleName>
   <LastName>string</LastName>
   </PersonName>
   <DOB>string</DOB>
   <CurrAddress>
   <Street>string</Street>
   <City>string</City>
   <State>string</State>
   <Zip>string</Zip>
   </CurrAddress>
   <DOJ>14-04-1973</DOJ>
   <Phone>1.0</Phone>
   </CEO>
   </Company>
   ```

   >[!NOTE]
   >
   >この例では、XML がコレクション要素に 3 つの値のスペースを作成しますが、値の数は必要に応じて増減できます。

1. データエントリの作成後は、テストデータを含むレターをプレビューする際にこの XML ファイルを使用できます。

   DD（DD を選択し、テストデータをアップロードを選択し、この XML ファイルをアップロード）でこのテストデータを追加できます。このため、レターを通常（カスタムではない）プレビューする場合、この XML データはレターで使用されます。 「カスタム」を選択して、この XML をアップロードすることもできます。

## サンプル {#samples}

以下のコードサンプルは、データディクショナリの実装の詳細を示しています。

### データディクショナリにアップロードできるサンプルスキーマ {#sample-schema-that-can-be-uploaded-to-the-data-dictionary}

```xml
<?xml version="1.0" encoding="utf-8"?>
<xs:schema xmlns="DCT" targetNamespace="DCT" xmlns:xs="https://www.w3.org/2001/XMLSchema"
  elementFormDefault="qualified" attributeFormDefault="unqualified">
  <xs:element name="Company">
    <xs:complexType>
      <xs:sequence>
        <xs:element name="Name" type="xs:string"/>
        <xs:element name="Type" type="xs:anySimpleType"/>
        <xs:element name="HeadOfficeAddress" type="Address"/>
        <xs:element name="SalesOfficeAddress" type="Address" minOccurs="0"/>
        <xs:element name="HeadCount" type="xs:integer"/>
        <xs:element name="CEO" type="Employee"/>
        <xs:element name="Workers" type="Employee" maxOccurs="unbounded"/>
      </xs:sequence>
    </xs:complexType>
  </xs:element>
  <xs:complexType name="Employee">
    <xs:complexContent>
      <xs:extension  base="Person">
        <xs:sequence>
          <xs:element name="CurrAddress" type="Address"/>
          <xs:element name="DOJ" type="xs:date"/>
          <xs:element name="Phone" type="xs:integer"/>
        </xs:sequence>
      </xs:extension>
    </xs:complexContent>
  </xs:complexType>
  <xs:complexType name="Person">
    <xs:sequence>
      <xs:element name="PersonName" type="Name"/>
      <xs:element name="DOB" type="xs:dateTime"/>
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="Name">
    <xs:sequence>
      <xs:element name="FirstName" type="xs:string"/>
      <xs:element name="MiddleName" type="xs:string"/>
      <xs:element name="LastName" type="xs:string"/>
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="Address">
    <xs:sequence>
      <xs:element name="Street" type="xs:string"/>
      <xs:element name="City" type="xs:string"/>
      <xs:element name="State" type="xs:string"/>
      <xs:element name="Zip" type="xs:string"/>
    </xs:sequence>
  </xs:complexType>
</xs:schema>
```

## DDE に関連付けられた共通属性 {#common-attributes-associated-with-a-dde}

次の表に、DDE に関連付けられる共通属性の詳細を示します。

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>タイプ</strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td>名前</td>
   <td>文字列</td>
   <td>必須。<br /> DDE の名前。 一意である必要があります。</td>
  </tr>
  <tr>
   <td>参照<br /> 名前</td>
   <td>文字列</td>
   <td>必須。データディクショナリの階層や構造の変更に依存しない DDE への参照を可能にする、DDE の一意の参照名。 テキストモジュールは、この名前を使用してマッピングされます</td>
  </tr>
  <tr>
   <td>displayname</td>
   <td>文字列</td>
   <td>DDE のわかりやすい名前（オプション）。</td>
  </tr>
  <tr>
   <td>説明</td>
   <td>文字列</td>
   <td>DDE の説明。</td>
  </tr>
  <tr>
   <td>elementType</td>
   <td>文字列</td>
   <td>必須。DDE のタイプ：STRING、NUMBER、DATE、Boolean、COMPOSITE、COLLECTION。</td>
  </tr>
  <tr>
   <td>elementSubType</td>
   <td>文字列</td>
   <td>DDE のサブタイプ： ENUM。 STRING および NUMBER elementType に対してのみ使用できます。</td>
  </tr>
  <tr>
   <td>キー</td>
   <td>ブール値</td>
   <td>DDE がキー要素かどうかを示すブール型 ( Boolean ) フィールド。</td>
  </tr>
  <tr>
   <td>計算済み</td>
   <td>ブール値</td>
   <td>DDE が計算されたかどうかを示すブール型 ( Boolean ) フィールド。 計算済み DDE 値は、他の DDE 値の関数です。 デフォルトでは、JSP 式をサポートしています。</td>
  </tr>
  <tr>
   <td>式</td>
   <td>文字列</td>
   <td>「計算済み」DDE の式。 デフォルトで提供される式評価サービスは、JSP EL 式をサポートします。 式サービスは、カスタム実装で置き換えることができます。</td>
  </tr>
  <tr>
   <td>valueSet</td>
   <td>リスト</td>
   <td>Enum タイプの DDE に使用できる値のセット。 例えば、アカウントタイプには（保存、現在）値のみを含めることができます。</td>
  </tr>
  <tr>
   <td>extendedProperties</td>
   <td>オブジェクト</td>
   <td>DDE に追加されたカスタムプロパティのマップ（ユーザーインターフェイス固有の情報またはその他の情報）。</td>
  </tr>
  <tr>
   <td>必須</td>
   <td>ブール値</td>
   <td>このフラグは、データディクショナリに対応するインスタンスデータのソースに、この特定の DDE の値が含まれている必要があることを示します。</td>
  </tr>
  <tr>
   <td>連結</td>
   <td>BindingElement</td>
   <td>要素の XML バインディングまたは Java バインディング。</td>
  </tr>
 </tbody>
</table>

### 計算済みデータディクショナリ要素 {#computedddelements}

データディクショナリには、計算済み要素を含めることもできます。 計算済みデータディクショナリ要素は、常に式に関連付けられます。 この式は、実行時にデータディクショナリ要素の値を取得するために評価されます。 計算済み DDE 値は、他の DDE 値またはリテラルの関数です。 デフォルトでは、JSP 式言語 (EL) 式がサポートされています。 EL 式は${ } 文字を使用し、有効な式にはリテラル、演算子、変数（データディクショナリ要素の参照）、関数呼び出しを含めることができます。 式内でデータディクショナリ要素を参照する際には、DDE の参照名が使用されます。 参照名は、データディクショナリ内のすべてのデータディクショナリ要素に対して一意です。

計算済み DDE PersonFullName は、$などの EL 連結式に関連付けることができます。{PersonFirstName} ${PersonLastName}.

## XSD とデータディクショナリの間のデータタイプマッピング {#data-type-mapping-between-xsd-and-data-dictionary-br}

XSD を書き出すには、特定のデータマッピングが必要です。詳しくは、次の表を参照してください。 DDI 列は、DDI で使用可能な DDE 値のタイプを示します。

<table>
 <tbody>
  <tr>
   <td>XSD <br /> </td>
   <td><p>データディクショナリ <br /> </p> </td>
   <td>DDI（インスタンス値のデータタイプ）<br /> </p> </td>
  </tr>
  <tr>
   <td><p>xs:element （タイプ — 複合タイプ）<br /> </p> </td>
   <td>DDE（タイプ — 複合）<br /> </p> </td>
   <td>java.util.Map<br /> </td>
  </tr>
  <tr>
   <td><p>xs:element ( maxOccurs &gt; 1)<br /> </p> </td>
   <td>DDE（タイプ — COLLECTION — ）<br /> DDE ノードは、親 COLLECTION ノードから情報を取り込む COLLECTION DDE の横に作成されます。 単純データ型と複合データ型の両方のコレクションに対して同じが作成されます。 複合タイプのコレクションがある場合は常に、データディクショナリツリーは、タイプ情報を取得するために作成された DDE の子に含まれる構成フィールドをキャプチャします。<br /> - DDE（コレクション）<br /> - DDE（情報タイプの複合）<br /> - DDE(STRING) フィールド 1<br /> - DDE(STRING) field2<br /> <br /> </p> </td>
   <td>java.util.List<br /> </td>
  </tr>
  <tr>
   <td>属性（タイプ - xs:id）<br /> </p> </td>
   <td>DDE（タイプ - 文字列）<br /> </td>
   <td>java.lang.String<br /> </td>
  </tr>
  <tr>
   <td>xs:attribute /xs:element（タイプ — xs:string）</p> </td>
   <td>DDE（タイプ - 文字列）<br /> </td>
   <td>java.lang.String<br /> </td>
  </tr>
  <tr>
   <td>xs:attribute /xs:element（タイプ - xs:boolean）<br /> </td>
   <td>DDE（タイプ - ブール値）<br /> </td>
   <td>java.lang.Boolean<br /> </td>
  </tr>
  <tr>
   <td>xs:attribute／xs:element（タイプ - xs:date） </td>
   <td>DDE（タイプ - 日付） </td>
   <td>java.lang.String</td>
  </tr>
  <tr>
   <td>xs:attribute／xs:element（タイプ - xs:integer） </td>
   <td>DDE（タイプ - 数値） </td>
   <td>java.lang.Double</td>
  </tr>
  <tr>
   <td>xs:attribute /xs:element（タイプ — xs:long）</td>
   <td>DDE（タイプ - 数値） </td>
   <td>java.lang.Double</td>
  </tr>
  <tr>
   <td>xs:attribute /xs:element（タイプ — xs:double）</td>
   <td>DDE（タイプ - 数値） </td>
   <td>java.lang.Double</td>
  </tr>
  <tr>
   <td>列挙型と baseType の要素 — xs:string</td>
   <td>次の DDE<br /> type - STRING<br /> サブタイプ — ENUM<br /> valueSet - ENUM に使用できる値<br /> </td>
   <td>java.lang.String</td>
  </tr>
 </tbody>
</table>

## データディクショナリからサンプルデータファイルをダウンロードします。 {#download-a-sample-data-file-from-a-data-dictionary}

データディクショナリを作成したら、XML サンプルデータファイルをダウンロードすると、テキストのエントリを作成できます。

1. データディクショナリページで、を選択します。 **選択** 次に、データディクショナリを選択して選択します。
1. 「**サンプル XML データのダウンロード**」を選択します。
1. 選択 **OK** （アラートメッセージ内）

   Correspondence Management は、選択したデータ辞書の構造に基づいて XML ファイルを作成し、そのファイルを、という名前でコンピューターにダウンロードします。 &lt;data-dictionary-name>-SampleData これにより、このファイルを XML エディターまたはテキストエディターで編集することで、[レターの作成](../../forms/using/create-letter.md)の際にデータエントリを作成することができるようになります。

## メタデータの国際化対応 {#internationalization-of-meta-data}

同じレターを異なる言語で顧客に送信する場合は、データディクショナリとデータディクショナリ要素の表示名、説明、および列挙値のセットをローカライズできます。

### データディクショナリのローカライズ {#localize-data-dictionary}

1. データディクショナリページで、を選択します。 **選択** 次に、データディクショナリを選択して選択します。
1. 選択 **ローカリゼーションデータをダウンロード**.
1. 選択 **OK** をクリックします。 Correspondence Management が DataDictionary-&lt;DDname>.zip のという名前の zip ファイルをお使いのコンピューターにダウンロードします。
1. Zip ファイルには.properties ファイルが含まれています。 このファイルは、ダウンロードしたデータディクショナリを定義します。 プロパティファイルの内容は次のようになります。

   ```ini
   #Wed May 20 16:06:23 BST 2015
   DataDictionary.EmployeeDD.description=
   DataDictionary.EmployeeDD.displayName=EmployeeDataDictionary
   DataDictionaryElement.name.description=
   DataDictionaryElement.name.displayName=name
   DataDictionaryElement.person.description=
   DataDictionaryElement.person.displayName=person
   ```

   プロパティファイルの構造は、説明とデータディクショナリの表示名、およびデータディクショナリ内の各データディクショナリ要素に対して 1 行ずつを定義します。 さらに、プロパティファイルでは、各データディクショナリ要素に設定された列挙値の 1 行を定義します。 データディクショナリと同様に、対応するプロパティファイルに複数のデータディクショナリ要素の定義を含めることができます。 また、このファイルには、1 つ以上の列挙値セットの定義を含めることができます。

1. 別のロケールの.properties ファイルを更新するには、ファイルの表示名と説明の値を更新します。 ローカライズする各言語用に、さらにファイルのインスタンスを作成します。 サポートする言語はフランス語、ドイツ語、日本語、英語のみです。

1. 更新したプロパティファイルを、それぞれ次の名前で保存します。

   _fr_FR.properties French

   _de_DE.properties German

   _ja_JA.properties Japanese

   _en_EN.properties English

1. .properties ファイル（または複数のロケール用のファイル）を 1 つの .zip ファイルにアーカイブします。

1. データディクショナリページで、**詳細**／**ローカリゼーションデータのアップロード**&#x200B;を選択し、ローカライズ済みのプロパティファイルを含む zip ファイルを選択します。
1. ローカリゼーションの変更を表示するには、ブラウザーのロケールを変更します。

## データ辞書の検証 {#ddvalidations}

データディクショナリの作成または更新時に、データディクショナリエディターは次の検証を強制します。

* 複合タイプのみが、データディクショナリのトップレベル要素として使用できます。
* 複合要素とコレクション要素は、リーフレベルでは使用できません。 プリミティブ (String、Date、Number、Boolean) 要素のみがリーフレベルで使用できます。 この検証では、子 DDE を持たない複合要素とコレクション要素が存在しないことを確認します。
* XSD ファイルをアップロードしてデータディクショナリを作成する際、データディクショナリエディターでは、データディクショナリを作成するための最上位要素（複数存在する場合）の入力を求められます。
* データディクショナリに必要なパラメータは、この名前だけです。
* 親 DDE（複合）に同じ名前の 2 つの子を指定することはできません
* DDE が必須のパラメーターでない場合にのみ、計算済みとしてマークされていることを確認します。 必須要素は計算できず、計算済み要素は必須ではありません。 また、コレクション要素と複合要素は計算要素にできません。
* DDE が必要とマークされていることを確認します（DDE が計算されていない場合のみ）。 また、コレクションのタイプ（コレクション要素の唯一の子）を示す「collectionElement」ではないことを確認します。
* データディクショナリまたは DDE の extendedProperties では、空のキーや重複キーは使用できません。
* 拡張プロパティのキーや値内でコロン (:) や縦棒 (|) を使用しないでください。 これらの禁止文字の使用に関する検証は行われません。

データディクショナリレベルでの検証

* データ辞書名は null にできません。
* データディクショナリ名には、英数字のみを含める必要があります。
* データディクショナリの子要素のリストは、null または空にできません。
* データディクショナリには、複数のトップレベルのデータディクショナリ要素を含めることはできません。
* 複合タイプのみが、データディクショナリのトップレベル要素として使用できます。

データディクショナリ要素レベルでの検証。

* すべての DDE 名を null にすることはできません。また、スペースを含めることはできません。
* すべての DDE は、要素タイプ「not null/non null」を持つ必要があります。
* すべての DDE 参照名を NULL にすることはできません。
* すべての DDE 参照名は一意である必要があります。
* すべての DDE 参照には、英数字およびアンダースコア「_」しか使用できません。
* すべての DDE 表示名には、英数字およびアンダースコア「_」しか使用できません。
* 複合要素とコレクション要素は、リーフレベルでは使用できません。 プリミティブ (String、Date、Number、Boolean) 要素のみがリーフレベルで使用できます。 この検証では、子 DDE を持たない複合要素とコレクション要素が存在しないことを確認します。
* 複合親 DDE には、同じ名前の 2 つの子要素を指定できません。
* ENUM サブタイプは、String 要素と Number 要素にのみ使用されます。
* コレクション要素と複合要素は計算できません。
* DDE は、計算済みと必須の両方を指定することはできません。
* 計算済み DDE には有効な式を含める必要があります。
* 計算済み DDE に XML バインディングを含めることはできません。
* コレクション DDE のタイプを示す DDE は、計算済みまたは必須の要素として指定できません。
* サブタイプ ENUM の DDE には、null または空の値セットを含めることはできません。
* コレクション DDE の XML バインディングは、属性にマッピングできません。
* XML バインディング構文は、有効である必要があります（@が 1 つだけ表示され、@は属性名の後にのみ使用できます）。

## データ辞書要素の XML スキーマへのマッピング {#mappingddetoschema}

データディクショナリは、XML スキーマから作成することも、データディクショナリのユーザーインターフェイスを使用して構築することもできます。 データディクショナリ内のすべてのデータディクショナリ要素 (DDE) には、DDE の XML バインディングを XML スキーマ内の要素に格納する XML バインディングフィールドがあります。 各 DDE のバインディングは、親 DDE に対する相対パスです。

データディクショナリの実装の詳細を示すサンプルモデルとコードサンプルについて以下に示します。

## 単純な（プリミティブ）要素のマッピング {#mapping-simple-primitive-elements}

プリミティブ DDE は、本質的にアトミックなフィールドまたは属性を表します。 複合型（複合 DDE）または繰り返し要素（コレクション DDE）の範囲外で定義されたプリミティブ DDE は、XML スキーマ内の任意の場所に格納できます。 プリミティブ DDE に対応するデータの場所は、その親 DDE のマッピングに依存しません。 プリミティブ DDE は、XML バインディングフィールドのマッピング情報を使用してその値を判断し、マッピングは次のいずれかに変換されます。

* 属性
* 要素
* テキストコンテキスト
* なし（無視された DDE） 

次の例は、単純なスキーマを示しています。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema xmlns:xs="https://www.w3.org/2001/XMLSchema">
  <xs:element name='age' type='integer'/>
  <xs:element name='price' type='decimal'/>
</xs:schema>
```

| **データディクショナリ要素** | **デフォルトの XML バインディング** |
|---|---|
| 年齢 | /age |
| 価格 | /price |

### 複合要素のマッピング {#mapping-composite-elements}

複合要素のバインディングはサポートされていません。バインディングが指定されている場合は無視されます。 プリミティブタイプの構成要素となるすべての子 DDE のバインディングは、絶対バインディングである必要があります。 複合 DDE の子要素に対して絶対マッピングを許可すると、XPath バインディングの点でより柔軟に指定できます。 複合 DDE を XML スキーマ内の複合型要素にマッピングすると、その子要素のバインディングの範囲が制限されます。

以下の例は、メモ（note）のスキーマを示しています。

```xml
<xs:element name="note">
    <xs:complexType>
        <xs:sequence>
            <xs:element name="to" type="xs:string"/>
            <xs:element name="from" type="xs:string"/>
            <xs:element name="heading" type="xs:string"/>
            <xs:element name="body" type="xs:string"/>
        </xs:sequence>
    </xs:complexType>
</xs:element>
```

<table>
 <tbody>
  <tr>
   <td><strong>データディクショナリ要素</strong></td>
   <td><strong>デフォルトの XML バインディング</strong></td>
  </tr>
  <tr>
   <td>注意</td>
   <td>empty(null)<br /> </td>
  </tr>
  <tr>
   <td>コピー先：</td>
   <td>/note/to</td>
  </tr>
  <tr>
   <td>コピー元：</td>
   <td>/note/from</td>
  </tr>
  <tr>
   <td>見出し</td>
   <td>/note/heading</td>
  </tr>
  <tr>
   <td>本文</td>
   <td>/note/body</td>
  </tr>
 </tbody>
</table>

### コレクション要素のマッピング {#mapping-collection-elements}

コレクション要素は、基数が 1 を超える別のコレクション要素にのみマッピングされます。 コレクション DDE の子 DDE には、親の XML バインディングに対する相対（ローカル）XML バインディングが含まれます。 コレクション要素の子 DDE は親のカーディナリティと同じカーディナリティを持つ必要があるので、カーディナリティの制約を確実にするために、子 DDE が繰り返さない XML スキーマ要素を指さないように、相対バインディングを必須にします。 以下の例では、「TokenID」の基数は、親コレクション DDE の「Tokens」と同じである必要があります。

コレクション DDE を XML スキーマ要素にマッピングする場合：

* コレクション要素に対応する DDE のバインディングは、絶対 XPath である必要があります。

* コレクション要素のタイプを表す DDE には、バインディングを指定しません。 指定した場合、バインディングは無視されます。

* コレクション要素のすべての子 DDE のバインディングは、親コレクション要素の相対パスである必要があります。

以下の XML スキーマは、名前が Tokens で maxOccurs 属性が「unbounded」の要素を宣言しています。したがって、Tokens はコレクション要素です。

```xml
<?xml version="1.0" encoding="utf-8"?>
<Root>
  <Tokens>
    <TokenID>string</TokenID>
    <TokenText>
      <TextHeading>string</TextHeading>
      <TextBody>string</TextBody>
    </TokenText>
  </Tokens>
  <Tokens>
    <TokenID>string</TokenID>
    <TokenText>
      <TextHeading>string</TextHeading>
      <TextBody>string</TextBody>
    </TokenText>
  </Tokens>
  <Tokens>
    <TokenID>string</TokenID>
    <TokenText>
      <TextHeading>string</TextHeading>
      <TextBody>string</TextBody>
    </TokenText>
  </Tokens>
</Root>
```

このサンプルに関連付けられる Token.xsd は次のようになります。

```xml
<xs:element name="Root">
  <xs:complexType>
    <xs:sequence>
      <xs:element name="Tokens" type="TokenType" maxOccurs="unbounded"/>
    </xs:sequence>
  </xs:complexType>
</xs:element>

<xs:complexType name="TokenType">
  <xs:sequence>
    <xs:element name="TokenID" type="xs:string"/>
    <xs:element name="TokenText">
      <xs:complexType>
        <xs:sequence>
          <xs:element name="TextHeading" type="xs:string"/>
          <xs:element name="TextBody" type="xs:string"/>
        </xs:sequence>
      </xs:complexType>
    </xs:element>
  </xs:sequence>
</xs:complexType>
```

| **データディクショナリ要素** | **デフォルトの XML バインディング** |
|---|---|
| ルート | empty(null) |
| トークン | /Root/Tokens |
| 複合 | empty(null) |
| TokenID | TokenID |
| TokenText | empty(null) |
| TokenHeading | TokenText/TextHeading |
| TokenBody | TokenText/TextBody |
