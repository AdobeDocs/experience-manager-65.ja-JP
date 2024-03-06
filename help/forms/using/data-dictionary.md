---
title: データディクショナリ
description: Correspondence Management のデータディクショナリを使用すると、バックエンドのデータを入力としてレターに統合し、顧客対応に使用することができます。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
docset: aem65
feature: Correspondence Management
exl-id: aaed75e6-8849-46a8-b986-896ad729adda
source-git-commit: 9d497413d0ca72f22712581cf7eda1413eb8d643
workflow-type: tm+mt
source-wordcount: '3842'
ht-degree: 89%

---

# データディクショナリ{#data-dictionary}

## はじめに {#introduction}

ビジネスユーザーはデータディクショナリを介すことで、バックエンドデータソースの情報を使用できます。基礎となるデータモデルの技術的な詳細情報を把握する必要はありません。データディクショナリは、複数のデータディクショナリ要素（DDE）で構成されます。これらのデータ要素を使用して、バックエンドデータを（顧客対応に使用する入力として）レターに統合します。

データディクショナリは、基礎となるデータ構造とその関連する属性を説明するメタデータの独立した表現です。データディクショナリはビジネス用語を使用して作成されます。また、基礎となるデータモデルの 1 つまたは複数にマッピングできます。

データディクショナリは、単純要素、複合要素、コレクション要素という 3 種類の要素から構成されます。単純 DDE は、都市名などの情報を保持する文字列、数値、日付、ブーリアン値などのプリミティブ要素です。複合 DDE は他の DDE を含むものであり、そのタイプはプリミティブ、複合、コレクションのいずれでもかまいません。例として、郵便番号、国、都道府県、市町村、地名、番地で構成される住所が挙げられます。コレクションは、同類の単純 DDE または複合 DDE のリストです。例として、複数の住所や、請求先と出荷先の住所が異なる顧客が挙げられます。

Correspondence Management は、バックエンド、顧客、または受信者に固有のデータを使用して、異なる顧客向けの通信を作成します。それらの固有のデータは、データディクショナリの構造に従って格納されています。例えば、ドキュメントの作成時に「{First Name} さん」、「{姓}様」などの名前を使用できます。

ビジネスユーザーは一般的に、XSD（xml スキーマ）、Java クラスなどの、メタデータ表現に関する知識を必要としません。ただし、通常はソリューションを構築するために、これらのデータ構造や属性へのアクセスが必要となります。

### データディクショナリのワークフロー {#data-dictionary-workflow}

1. 作成者が[データディクショナリを作成](#createdatadictionary)します。作成には、スキーマを読み込むか、または新規に作成します。
1. 作成者はデータディクショナリに基づいてレターとインタラクティブ通信を作成し、レターとインタラクティブ通信のデータディクショナリ要素を必要な箇所に関連付けます。
1. 作成者はサンプルデータの XML ファイルをダウンロードできます。これはデータディクショナリのスキーマに基づいたものです。作成者はサンプルデータの XML ファイルを編集できます。これはテストデータとしてデータディクショナリに関連付けることができます。レターのプレビューでも同様の操作が可能です。
1. [レターのプレビュー](../../forms/using/create-letter.md#p-types-of-linkage-available-for-each-of-the-fields-p)時に、作成者はデータが入ったレターをプレビューすることを選択できます（カスタムプレビュー）。作成者が提供したデータが入力された状態でレターが開きます。通信を作成するインターフェイスが開きます。このレターをプレビューしているエージェントは、レターのコンテンツ、データ、および添付ファイルを変更して最終的なレターを送信できます。レターの作成について詳しくは、[通信の作成](../../forms/using/create-letter.md)を参照してください。

## 前提条件 {#prerequisite}

[互換パッケージ](compatibility-package.md)をインストールし、「**フォーム**」ページで「**データディクショナリ**」オプションを表示します。

## データディクショナリを作成 {#createdatadictionary}

データディクショナリの作成にはデータディクショナリエディターを使用します。または、XSD スキーマファイルをアップロードしてデータディクショナリを作成することができます。後からフィールドなどの必須の情報をさらに追加して、このデータディクショナリを拡張できます。データディクショナリの作成方法を問わず、ビジネスプロセスの所有者にはバックエンドシステムに関する知識は必要がありません。ビジネスプロセスの所有者に必要とされるのは、プロセスのドメインオブジェクトとその宛先に関する知識だけです。

>[!NOTE]
>
>類似した要素を必要とするレターが複数存在する場合は、共通データディクショナリを作成することができます。ただし、要素数が多い大きなデータディクショナリを使用すると、データディクショナリを使用してレターやドキュメントフラグメントなどの要素を読み込む際に、パフォーマンスの問題が発生する可能性があります。 パフォーマンスに関する問題が発生した場合は、レターごとに個別のデータディクショナリを作成してください。

1. **フォーム**／**データディクショナリ**&#x200B;を選択します。
1. 選択 **データ辞書を作成**.
1. プロパティ画面で以下を追加します。

   * **タイトル：**（オプション）データディクショナリのタイトルを入力します。タイトルは一意である必要はなく、特殊文字や英語以外の文字を含めることもできます。レターなどのドキュメントフラグメントは、タイトル（利用可能な場合）を用いて参照されます。タイトルは、サムネールやアセットプロパティなどで使用されます。データディクショナリは、名前ではなく、タイトルで参照されます。
   * **名前**：データディクショナリの一意の名前。「名前」フィールドに入力できるのは、英語の文字、数字、ハイフンのみです。「名前」フィールドは、タイトルフィールドに基づいて自動的に入力されます。「タイトル」フィールドに入力された特殊文字、スペース、および英数字以外の文字はハイフンに置き換えられます。「タイトル」フィールドの値は「名前」フィールドに自動的にコピーされますが、値を編集することもできます。

   * **説明**：（オプション）データディクショナリの説明。
   * **タグ**：（オプション）カスタムタグを作成するには、テキストフィールドに値を入力して Enter を押します。タグのテキストフィールドの下にタグが表示されます。このテキストを保存すると、新しく追加されたタグも作成されます。
   * **拡張プロパティ**: （オプション） Select **フィールドを追加** データディクショナリのメタデータ属性を指定します。 「プロパティ名」列に、固有のプロパティ名を入力します。「値」列に、プロパティに関連付ける値を入力します。

   ![ドイツ語で指定されたデータディクショナリプロパティ](do-not-localize/1_ddproperties.png)

1. （オプション）データディクショナリの XSD スキーマ定義をアップロードするには、データディクショナリの構造ウィンドウで、 **XML スキーマをアップロード**. XSD ファイルを参照して選択し、選択します。 **開く**. データディクショナリは、アップロードされた XML スキーマに基づいて作成されます。データディクショナリで要素の表示名や説明を調整する必要があります。これを行うには、要素の名前をタップして選択し、右側のペインのフィールドで説明、表示名、およびその他の詳細を編集します。

   計算済み DD 要素について詳しくは、「[計算済みデータディクショナリ要素](#computedddelements)」を参照してください。

   >[!NOTE]
   >
   >ユーザーインターフェイスを使用することで、スキーマファイルのアップロードをスキップして、新規でデータディクショナリを構築することもできます。新規で構築するには、この手順をスキップし次の手順に進みます。

1. 「**次へ**」を選択します。
1. プロパティを追加画面でデータディクショナリに要素を追加します。また、データディクショナリの基本構造を取得するためにスキーマをアップロードすることで、要素の追加や削除、詳細の編集を行うことができます。

   要素の右側にある 3 つのドットを選択し、データディクショナリの構造に要素を追加できます。

   ![1_2_createanelement](assets/1_2_createanelement.png)

   「複合要素」、「コレクション要素」または「プリミティブ要素」を選択します。

   * 複合 DDE は他の DDE を含むものであり、そのタイプはプリミティブ、複合、コレクションのいずれでも構いません。例として、郵便番号、国、都道府県、市町村、地名、番地で構成される住所が挙げられます。
   * プリミティブ DDE は、文字列、数値、日付、ブール値などの要素であり、都市名などの情報を保持します。
   * コレクションは、同類の単純 DDE または複合 DDE のリストです。例として、複数の住所や、請求先と出荷先の住所が異なる顧客が挙げられます。

   次に、データディクショナリの作成ルールを示します。

   * データディクショナリ内のトップレベル DDE として使用できるのは、複合タイプのみです。
   * 名前、参照名および要素タイプは、データディクショナリと DDE において必須のフィールドです。
   * 参照名は一意にする必要があります。
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

1. （オプション）データディクショナリの構造ペインの要素を選択し、フィールドと変数リストパネルで、要素に関連する必要な属性を変更または追加します。要素に関連付けられた必要な属性を変更または追加します。
1. 「**保存**」を選択します。

### 1 つ以上のデータディクショナリのコピーを作成 {#create-copies-of-one-or-more-data-dictionary}

既存のデータディクショナリをコピーしてペーストすることにより、そのデータディクショナリに類似するプロパティやコンテンツを持つ 1 つ以上のデータディクショナリをすばやく作成することができます。

1. データディクショナリのリストで、目的のデータディクショナリを選択します。UI に「コピー」アイコンが表示されます。
1. 「コピー」を選択します。 UI にペーストアイコンが表示されます。
1. 「貼り付け」を選択します。 貼り付けダイアログが表示されます。システムにより、新しいデータディクショナリに名前とタイトルが自動的に割り当てられます。
1. 必要に応じて、データディクショナリのコピーを保存するタイトルと名前を編集します。
1. 「貼り付け」を選択します。 データディクショナリのコピーが作成されます。これで、新しく作成されたデータディクショナリで必要な変更を行うことができます。

## データディクショナリ要素を参照するドキュメントフラグメントまたは文書を確認する {#see-the-document-fragments-or-documents-that-refer-to-a-data-dictionary-element}

データディクショナリの編集中または表示中は、データディクショナリ内のどの要素が、どのテキスト、条件、レター、インタラクティブ通信に参照されているか確認できます。

1. データディクショナリを編集するには、次のいずれかの操作を行います。

   * データディクショナリにカーソルを合わせ、「編集」を選択します。
   * データディクショナリを選択し、ヘッダーで「編集」を選択します。
   * データディクショナリにカーソルを合わせ、「選択」を選択します。 次に、ヘッダーで「編集」を選択します。

   または、データディクショナリを選択して表示します。

1. データディクショナリで、単純な要素を選択して選択します。 複合要素とコレクション要素には参照がありません。

   要素の基本プロパティ、詳細プロパティと共に「貸したコンテンツ」も表示されます。

1. 「貸したコンテンツ」を選択します。

   「貸したコンテンツ」タブでは、テキスト、条件、レター、インタラクティブ通信が表示されます。それぞれの見出しには、選択した要素の参照数も表示されます。

1. 要素を参照するアセットの名前を確認するには、見出しを選択します。

   ![lentcontent](assets/lentcontent.png)

1. 別の要素の貸したコンテンツを表示するには、要素を選択します。
1. 要素を参照するアセットを表示するには、その名前を選択します。 アセット、レターまたはインタラクティブ通信がブラウザーに表示されます。

## テストデータの操作 {#working-with-test-data}

1. データディクショナリページで、を選択します。 **選択**.
1. テストデータをダウンロードするデータディクショナリを選択し、「 」を選択します。 **サンプル XML データをダウンロード**.
1. 選択 **OK** （アラートメッセージ内） XML ファイルがダウンロードされます。
1. XML ファイルを Notepad その他の XML エディターで開きます。XML ファイルは、データディクショナリおよび要素内のプレースホルダー文字列と同じ構造を持っています。レターのテストに使うデータでプレースホルダー文字列を置き換えます。

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

データディクショナリ実装の詳細コードサンプルを以下に示します。

### データディクショナリにアップロード可能なサンプルスキーマ {#sample-schema-that-can-be-uploaded-to-the-data-dictionary}

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

## DDE に関連付けられる共通属性 {#common-attributes-associated-with-a-dde}

DDE に関連付けられる共通属性について、以下の表に示します。

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
   <td>必須。<br />DDE の名前。一意である必要があります。</td>
  </tr>
  <tr>
   <td>参照<br />名</td>
   <td>文字列</td>
   <td>必須。データディクショナリの階層や構造の変更に左右されない、DDE への参照を可能にする DDE の一意の参照名です。テキストモジュールは、この名前を使用してマッピングされます。</td>
  </tr>
  <tr>
   <td>displayname</td>
   <td>文字列</td>
   <td>ユーザーにわかりやすい DDE の名前（オプション）。</td>
  </tr>
  <tr>
   <td>説明</td>
   <td>文字列</td>
   <td>DDE の説明。</td>
  </tr>
  <tr>
   <td>elementType</td>
   <td>文字列</td>
   <td>必須。DDE のタイプ：文字列、数値、日付、ブール値、複合、コレクションのいずれかです。</td>
  </tr>
  <tr>
   <td>elementSubType</td>
   <td>文字列</td>
   <td>DDE のサブタイプ：列挙型。elementType が文字列および数値の場合のみ使用できます。</td>
  </tr>
  <tr>
   <td>キー</td>
   <td>ブール値</td>
   <td>DDE がキー要素かどうかを示すブール値フィールド。</td>
  </tr>
  <tr>
   <td>計算済み</td>
   <td>ブール値</td>
   <td>DDE が計算済みかどうかを示すブール値フィールド。計算済み DDE の値は、他の DDE 値の関数です。デフォルトでは、JSP 式をサポートしています。</td>
  </tr>
  <tr>
   <td>式</td>
   <td>文字列</td>
   <td>「計算済み」DDE の式。デフォルトで提供される式評価サービスは、JSP EL 式をサポートします。式サービスは、カスタム実装に置き換えることができます。</td>
  </tr>
  <tr>
   <td>valueSet</td>
   <td>リスト</td>
   <td>列挙型 DDE に使用できる値のセット。例えば、アカウントタイプには（Saving, Current）値のみを設定できます。</td>
  </tr>
  <tr>
   <td>extendedProperties</td>
   <td>オブジェクト</td>
   <td>DDE に追加されたカスタムプロパティ（ユーザーインターフェイス固有の情報やその他の情報）のマップ。</td>
  </tr>
  <tr>
   <td>必須</td>
   <td>ブール値</td>
   <td>このフラグは、データディクショナリに対応するインスタンスデータのソースに、この特定の DDE の値が含まれている必要があることを示します。</td>
  </tr>
  <tr>
   <td>バインディング</td>
   <td>BindingElement</td>
   <td>要素の XML バインディングまたは Java バインディング。</td>
  </tr>
 </tbody>
</table>

### 計算済みデータディクショナリ要素 {#computedddelements}

データディクショナリには、計算済み要素を含めることもできます。計算済みデータディクショナリ要素は、常に式と関連付けられます。実行時にこの式が評価され、データディクショナリ要素の値が取得されます。計算済み DDE 値は、他の DDE 値またはリテラルによる関数です。デフォルトでは、JSP 式言語（EL）の式がサポートされます。EL 式は ${ } の文字を使用します。有効な式にはリテラル、演算子、変数（データディクショナリ要素の参照）および関数呼び出しを含めることができます。式においてデータディクショナリ要素を参照する際は、DDE の参照名を使用します。あるデータディクショナリに含まれるすべてのデータディクショナリ要素は、それぞれ一意の参照名によって特定されます。

計算済み DDE PersonFullName は、${PersonFirstName} ${PersonLastName} などの EL 連結式に関連付けることができます。

## XSD とデータディクショナリの間のデータタイプマッピング {#data-type-mapping-between-xsd-and-data-dictionary-br}

XSD を書き出すには、固有のデータマッピングが必要になります。これについては、次の表に示します。DDI 列は、DDI で利用できる DDE 値のタイプを示します。

<table>
 <tbody>
  <tr>
   <td>XSD <br /> </td>
   <td><p>データディクショナリ <br /> </p> </td>
   <td>DDI（インスタンス値のデータ型）<br /> </p> </td>
  </tr>
  <tr>
   <td><p>xs:element（タイプ - 複合タイプ）<br /> </p> </td>
   <td>DDE（タイプ - 複合）<br /> </p> </td>
   <td>java.util.Map<br /> </td>
  </tr>
  <tr>
   <td><p>xs:element（maxOccurs &gt; 1）<br /> </p> </td>
   <td>DDE（タイプ - コレクション）<br />DDE ノードは、親コレクションノードから情報を取り込むコレクション DDE の次に作成されます。単純データタイプと複合データタイプの両方のコレクション向けに、同じものが作成されます。複合タイプのコレクションがある場合は常に、データディクショナリツリーは、タイプ情報を取り込むために作成された DDE の子に、以下の構成要素フィールドを取り込みます。<br /> - DDE（コレクション）<br /> - DDE（タイプ情報：複合）<br /> - DDE（文字列）field1<br /> - DDE（文字列）field2<br /> <br /> </p> </td>
   <td>java.util.List<br /> </td>
  </tr>
  <tr>
   <td>属性（タイプ - xs:id）<br /> </p> </td>
   <td>DDE（タイプ - 文字列）<br /> </td>
   <td>java.lang.String<br /> </td>
  </tr>
  <tr>
   <td>xs:attribute /xs:element（タイプ - xs:string）</p> </td>
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
   <td>xs:attribute /xs:element（タイプ - xs:long）</td>
   <td>DDE（タイプ - 数値） </td>
   <td>java.lang.Double</td>
  </tr>
  <tr>
   <td>xs:attribute /xs:element（タイプ - xs:double）</td>
   <td>DDE（タイプ - 数値） </td>
   <td>java.lang.Double</td>
  </tr>
  <tr>
   <td>列挙型と baseType の要素 - xs:string</td>
   <td>以下の DDE<br /> タイプ - 文字列<br /> サブタイプ - 列挙型<br /> valueSet - 列挙型に使用できる値<br /> </td>
   <td>java.lang.String</td>
  </tr>
 </tbody>
</table>

## データディクショナリからサンプルデータファイルをダウンロード {#download-a-sample-data-file-from-a-data-dictionary}

データディクショナリを作成したら、XML サンプルデータファイルをダウンロードすると、テキストのエントリを作成できます。

1. データディクショナリページで、を選択します。 **選択** 次に、データディクショナリを選択して選択します。
1. 「**サンプル XML データのダウンロード**」を選択します。
1. 選択 **OK** （アラートメッセージ内）

   Correspondence Management は、選択されたデータディクショナリの構造に基づいて XML ファイルを作成し、&lt;data-dictionary-name>-SampleData の名称でコンピューターにダウンロードします。これにより、このファイルを XML エディターまたはテキストエディターで編集することで、[レターの作成](../../forms/using/create-letter.md)の際にデータエントリを作成することができるようになります。

## メタデータの国際化 {#internationalization-of-meta-data}

同じレターを異なる言語で顧客へ送信する場合、データディクショナリとデータディクショナリ要素の表示名、説明、および列挙値のセットをローカライズすることができます。

### データディクショナリのローカライズ {#localize-data-dictionary}

1. データディクショナリページで、を選択します。 **選択** 次に、データディクショナリを選択して選択します。
1. 選択 **ローカリゼーションデータをダウンロード**.
1. 選択 **OK** をクリックします。 Correspondence Management が DataDictionary-&lt;DDname>.zip のという名前の zip ファイルをお使いのコンピューターにダウンロードします。
1. Zip ファイルには .properties ファイルが含まれています。このファイルは、ダウンロードされたデータディクショナリを定義します。プロパティファイルのコンテンツは以下のようになります。

   ```ini
   #Wed May 20 16:06:23 BST 2015
   DataDictionary.EmployeeDD.description=
   DataDictionary.EmployeeDD.displayName=EmployeeDataDictionary
   DataDictionaryElement.name.description=
   DataDictionaryElement.name.displayName=name
   DataDictionaryElement.person.description=
   DataDictionaryElement.person.displayName=person
   ```

   プロパティファイルの構造は、データディクショナリの説明と表示名、およびデータディクショナリ内のデータディクショナリの各要素をそれぞれ 1 行で定義します。さらに、プロパティファイルは各データディクショナリ要素の列挙値セットを 1 行で定義します。データディクショナリと同様に、対応するプロパティファイルは複数のデータディクショナリ要素の定義を持つことができます。さらに、このファイルには 1 つ以上の列挙値セットの定義を含めることができます。

1. 別のロケールの .properties ファイルをアップデートするには、ファイルの表示名と説明の値をアップデートします。ローカライズする各言語でファイルのインスタンスをさらに作成します。サポートする言語はフランス語、ドイツ語、日本語、英語のみです。

1. 更新したプロパティファイルを、それぞれ次の名前で保存します。

   _fr_FR.properties French

   _de_DE.properties German

   _ja_JA.properties Japanese

   _en_EN.properties English

1. .properties ファイル（または複数のロケール用のファイル）を 1 つの .zip ファイルにアーカイブします。

1. データディクショナリページで、**詳細**／**ローカリゼーションデータのアップロード**&#x200B;を選択し、ローカライズ済みのプロパティファイルを含む zip ファイルを選択します。
1. ローカリゼーションの変更を表示するには、ブラウザーのロケールを変更します。

## データディクショナリの検証 {#ddvalidations}

データディクショナリの作成または更新時に、データディクショナリエディターは以下の検証を強制的に行います。

* 複合タイプのみを、データディクショナリのトップレベル要素として使用できます。
* リーフレベルでは、複合要素とコレクション要素を使用できません。リーフレベルでは、プリミティブ（文字列、日付、数値、ブーリアン）要素のみが許可されます。この検証では、子 DDE なしの複合要素やコレクション要素が存在しないことが確認されます。
* データディクショナリを作成するために XSD ファイルをアップロードする際、データディクショナリエディターは、データディクショナリを作成するための最上位要素（複数存在する場合）を要求します。
* データディクショナリに必要なパラメーターは、この名前だけです。
* 親 DDE（複合）には、同じ名前の 2 つの子を指定できません
* DDE が必須のパラメーターでない場合にのみ、DDE が計算済みとしてマークされていることを確認します。必須の要素の計算はできず、計算済みの要素を必須にすることもできません。また、コレクション要素と複合要素は計算済み要素にはできません。
* DDE が計算済みではない場合のみ、DDE が必須としてマークされていることを確認します。また、コレクションのタイプ（コレクション要素の唯一の子）を示す「collectionElement」ではないことを確認します。
* データディクショナリまたは DDE の extendedProperties では、空のキーや重複するキーは許可されません。
* 拡張プロパティのキーまたは値の内部でコロン（：）や縦棒（|）を使用しないでください。これらの禁止文字の使用について検証は行われません。

データディクショナリレベルで適用される検証

* データディクショナリ名は null にできません。
* データディクショナリ名には、英数字のみを使用する必要があります。
* データディクショナリの子要素のリストは、null や空にできません。
* データディクショナリに複数のトップレベルのデータディクショナリ要素を含めることはできません。
* 複合タイプのみを、データディクショナリのトップレベル要素として使用できます。

データディクショナリ要素レベルで適用される検証

* どの DDE 名も null にできません。またスペースを含めることはできません。
* すべての DDE の要素タイプを「not null／non null」にする必要があります。
* すべての DDE 参照名を null にすることはできません。
* すべての DDE 参照名は、一意である必要があります。
* すべての DDE 参照には、英数字およびアンダースコア「_」しか使用できません。
* すべての DDE 表示名には、英数字およびアンダースコア「_」しか使用できません。
* リーフレベルでは、複合要素とコレクション要素を使用できません。リーフレベルでは、プリミティブ（文字列、日付、数値、ブーリアン）要素のみが許可されます。この検証では、子 DDE なしの複合要素やコレクション要素が存在しないことが確認されます。
* 複合親 DDE（複合）は、同じ名前の子を 2 つ持つことはできません。
* ENUM サブタイプは、文字列および数値要素にのみ使用します。
* コレクション要素および複合要素は計算できません。
* DDE は、計算と必須の両方を行うことはできません。
* 計算済み DDE には有効な式を含める必要があります。
* 計算済み DDE に XML バインディングは指定できません。
* コレクション DDE のタイプを示す DDE は、計算済みまたは必須の要素として指定できません。
* サブタイプが列挙型の DDE は、値セットを null または空にすることはできません。
* コレクション DDE の XML バインディングで、属性へのマッピングはできません。
* XML バインディング構文は、有効なものである必要があります（@ を 1 つだけ使用する、@ は属性名の前にのみ使用するなど）。

## データディクショナリ要素の XML スキーマへのマッピング {#mappingddetoschema}

データディクショナリは XML スキーマから作成することも、データディクショナリユーザーインターフェイスを使用して作成することもできます。データディクショナリ内のすべてのデータディクショナリ要素（DDE）には XML バインディングフィールドがあり、DDE のバインディングを XML スキーマの要素に格納できます。各 DDE のバインディングは、親 DDE に対する相対パスにします。

データディクショナリの実装の詳細を示すサンプルモデルとコードサンプルについて以下に示します。

## 単純な（プリミティブ）要素のマッピング {#mapping-simple-primitive-elements}

プリミティブ DDE とは、本来アトミックなフィールドまたは属性を表します。複合タイプ（複合 DDE）または繰り返し要素（コレクション DDE）以外で定義されたプリミティブ DDE は、XML スキーマ内のどの場所にも格納できます。プリミティブ DDE に対応するデータの場所は、その親 DDE のマッピングには依存しません。プリミティブ DDE は、XML バインディングフィールドのマッピング情報を使用して値を特定します。マッピングは次のいずれかに解釈されます。

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
| age | /age |
| price | /price |

### 複合要素のマッピング {#mapping-composite-elements}

複合要素ではバインディングがサポートされていません。バインディングが提供されても無視されます。プリミティブタイプの構成要素であるすべての子 DDE のバインディングは、絶対パスである必要があります。複合 DDE の子要素に対して絶対マッピングが使用できるので、XPath バインディングの観点で柔軟性が高くなります。複合 DDE を XML スキーマの複合タイプ要素にマッピングすると、その子要素のバインディングの範囲が制限されます。

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
   <td>note</td>
   <td>空（ヌル）<br /> </td>
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
   <td>heading</td>
   <td>/note/heading</td>
  </tr>
  <tr>
   <td>本文</td>
   <td>/note/body</td>
  </tr>
 </tbody>
</table>

### コレクション要素のマッピング {#mapping-collection-elements}

コレクション要素は、基数が 1 より大きい別のコレクション要素にのみマッピングされます。コレクション DDE の子 DDE には、親の XML バインディングに対する相対（ローカル）XML バインディングが含まれます。コレクション要素の子 DDE は親と同じ基数を持つ必要があるので、基数の制約を守るために相対バインディングを必須とし、子 DDE が繰り返しなしの XML スキーマ要素を指さないようにする必要があります。以下の例では、「TokenID」の基数は、親コレクション DDE の「Tokens」と同じである必要があります。

コレクション DDE を XML スキーマ要素にマッピングする場合：

* コレクション要素に対応する DDE のバインディングは、絶対 XPath である必要があります。

* コレクション要素のタイプを表す DDE には、バインディングを指定しません。指定しても、バインディングは無視されます。

* コレクション要素のすべての子 DDE のバインディングは、親コレクション要素の相対パスである必要があります。

以下の XML スキーマは、名前が Tokens で maxOccurs 属性が「unbounded」の要素を宣言しています。つまり、Tokens はコレクション要素です。

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
| Root | 空（ヌル） |
| Tokens | /Root/Tokens |
| Composite | 空（ヌル） |
| TokenID | TokenID |
| TokenText | 空（ヌル） |
| TokenHeading | TokenText/TextHeading |
| TokenBody | TokenText/TextBody |
