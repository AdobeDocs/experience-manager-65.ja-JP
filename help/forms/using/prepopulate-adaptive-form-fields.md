---
title: アダプティブフォームのフィールドの事前入力
seo-title: アダプティブフォームのフィールドの事前入力
description: 既存データを使用して、アダプティブフォームのフィールドを事前入力します。
seo-description: アダプティブフォームを使って、ユーザーは、ソーシャルプロファイルにログインすることによって、事前にフォームの基本情報を入力することができます。この記事は、これを達成する方法について説明します。
uuid: 574de83a-7b5b-4a1f-ad37-b9717e5c14f1
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 7139a0e6-0e37-477c-9e0b-aa356991d040
docset: aem65
translation-type: tm+mt
source-git-commit: 726163106ddb80600eaa7cc09b1a2e9b035a223e

---


# アダプティブフォームのフィールドの事前入力{#prefill-adaptive-form-fields}

## 概要 {#introduction}

既存データを使用して、アダプティブフォームのフィールドを事前入力することができます。ユーザーがフォームを開くと、これらのフィールドの値は事前入力されています。アダプティブフォームにデータを事前入力するには、アダプティブフォームの事前入力データ構造に合った形式を使用して、事前入力 XML または JSON としてユーザーデータを作成します。

## Structure of prefill data {#the-prefill-structure}

アダプティブフォームには、連結されたフィールドと連結されていないフィールドが混在している場合があります。Bound fields are fields which are dragged from the Content Finder tab and contain non-empty `bindRef` property value in the field edit dialog. Unbound fields are dragged directly from the component browser of Sidekick and have an empty `bindRef` value.

アダプティブフォームの連結されたフィールドと連結されていないフィールドの両方を事前入力できます。事前入力データには afBoundData セクションと afUnBoundData セクションが含まれており、アダプティブフォームの連結されたフィールドと連結されていないフィールドの両方を事前入力できます。`afBoundData` セクションには連結されたフィールドとパネルの事前入力データが含まれています。このデータは関連するフォームモデルスキーマに準拠している必要があります。

* [XFA フォームテンプレート](../../forms/using/prepopulate-adaptive-form-fields.md)を使用しているアダプティブフォームの場合は、XFA テンプレートのデータスキーマに準拠している事前入力 XML を使用します。
* [XML スキーマ](#xml-schema-af)を使用しているアダプティブフォームの場合は、XML スキーマ構造に準拠している事前入力 XML を使用します。
* [JSON スキーマ](#json-schema-based-adaptive-forms)を使用しているアダプティブフォームの場合は、JSON スキーマに準拠している事前入力 JSON を使用します。
* FDM スキーマを使用しているアダプティブフォームの場合は、FDM スキーマに準拠している事前入力 JSON を使用します。
* [フォームモデルのない](#adaptive-form-with-no-form-model)アダプティブフォームの場合、連結されたデータはありません。すべてのフィールドは、連結されていないフィールドであり、連結されていないXMLを使用して事前入力されています。

### 事前入力 XML 構造のサンプル {#sample-prefill-xml-structure}

```xml
<?xml version="1.0" encoding="UTF-8"?>
<afData>
  <afBoundData>
     <employeeData>
        .
     </employeeData>
  </afBoundData>

  <afUnboundData>
    <data>
      <textbox>Hello World</textbox>
         .
         .
      <numericbox>12</numericbox>
         . 
         .              
    </data>
  </afUnboundData>
</afData>
```

### 事前入力 JSON 構造のサンプル {#sample-prefill-json-structure}

```
{
   "afBoundData": {
      "employeeData": { }
   },
   "afUnboundData": {
      "data": {
         "textbox": "Hello World",
         "numericbox": "12"
      }
   }
}
```

同じ bindref を持つ連結されているフィールド、または同じ名前を持つ連結されていないフィールドの場合、XML タグまたは JSON オブジェクトで指定したデータがすべてのフィールドに入力されます。For example, two fields in a form are mapped to the name `textbox` in the prefill data. ランタイム時、最初のテキストボックスに「A」が含まれる場合、この「A」が 2 番目のテキストボックスに自動的に挿入されます。このリンクは、アダプティブフォームフィールドのライブリンクと呼ばれます。

### XFAフォームテンプレートを使用したアダプティブフォーム {#xfa-based-af}

XFAベースのアダプティブフォームの事前入力XMLと送信済みXMLの構造は、次のとおりです。

* **事前入力 XML 構造**：XFA ベースのアダプティブフォームのための事前入力 XML は、XFA フォームテンプレートのデータスキーマに準拠していなければなりません。To prefill unbound fields, wrap the prefill XML structure into `/afData/afBoundData` tag.

* **送信済み XML 構造**：事前入力 XML が使用されていない場合、送信済み XML の `afData` wrapper タグには、連結されたフィールドと連結されていないフィールドの両方のデータが含まれます。事前入力 XML が使用された場合、送信済み XML は、事前入力 XML と同じ構造をしています。事前入力 XML が `afData` のルートタグで開始する場合、出力 XML もまた同じフォーマットとなります。事前入力 XML に `afData/afBoundData` のラッパーが無く、直接 `employeeData` のようなスキーマルートタグから開始する場合は、送信済み XML もまた `employeeData` タグから開始します。

Prefill-Submit-Data-ContentPackage.zip

[事前入力データと送](assets/prefill-submit-data-contentpackage.zip)信データを含むGet File Sample

### XMLスキーマベースのアダプティブフォーム{#xml-schema-af}

XML スキーマをベースとするアダプティブフォームの事前入力 XML と送信済み XML の構造は次のとおりです。

* **事前入力 XML 構造**：事前入力 XML は、関連する XML スキーマに準拠していなければなりません。連結されていないフィールドを事前入力するには、事前入力 XML 構造を /afData/afBoundData タグにラップします。
* **送信されたXML構造**:事前入力XMLが使用されていない場合、送信されたXMLには、wrapperタグ内の連結されたフィールドと連結されていないフィールドの両方のデータ `afData` が含まれます。 事前入力 XML が使用された場合、送信済み XML は、事前入力 XML と同じ構造をしています。事前入力 XML が `afData` のルートタグで開始する場合、出力 XML もまた同じフォーマットとなります。事前入力 XML に `afData/afBoundData` のラッパーが無く、直接 `employeeData` のようなスキーマルートタグから開始する場合は、送信済み XML もまた `employeeData` タグから開始します。

```xml
<?xml version="1.0" encoding="utf-8" ?> 
<xs:schema targetNamespace="https://adobe.com/sample.xsd"
            xmlns="https://adobe.com/sample.xsd"
            xmlns:xs="https://www.w3.org/2001/XMLSchema">
 
    <xs:element name="sample" type="SampleType"/>
         
    <xs:complexType name="SampleType">
        <xs:sequence>
            <xs:element name="noOfProjectsAssigned" type="xs:string"/>
        </xs:sequence>
    </xs:complexType>
</xs:schema>
```

XML スキーマをモデルとするフィールドの場合、以下の XML のサンプルに示すように、`afBoundData` タグのデータは事前入力されます。これは、1 つ以上の連結されていないテキストフィールドでアダプティブフォームを事前入力する場合に使用できます。

```xml
<?xml version="1.0" encoding="UTF-8"?><afData>
  <afUnboundData>
    <data>
      <textbox>Ignorance is bliss :) </textbox>
    </data>
  </afUnboundData>
  <afBoundData>
    <data>
      <noOfProjectsAssigned>twelve</noOfProjectsAssigned>
    </data>
  </afBoundData>
</afData>
```

>[!NOTE]
>
>連結されているパネル（サイドキックまたは「データソース」タブからコンポーネントをドラッグして作成された、空ではない `bindRef` が含まれているパネル）では、連結されていないフィールドを使用しないことをお勧めします。これらの連結していないフィールドのデーターの損失を招くことがあります。また、フィールド名は、特に連結していないフィールドについては、フォーム間で一意のフィールド名を設定することをお勧めします。

#### afData および afBoundData ラッパーがない場合の例 {#an-example-without-afdata-and-afbounddata-wrapper}

```xml
<?xml version="1.0" encoding="UTF-8"?><config>
 <assignmentDetails descriptionOfAssignment="Some Science Project" durationOfAssignment="34" financeRelatedProject="1" name="Lisa" numberOfMentees="1"/>
 <assignmentDetails descriptionOfAssignment="Kidding, right?" durationOfAssignment="4" financeRelatedProject="1" name="House" numberOfMentees="3"/>
</config>
```

### JSON スキーマベースのアダプティブフォーム {#json-schema-based-adaptive-forms}

JSON スキーマをベースとするアダプティブフォームの場合、事前入力 JSON と送信済み JSON の構造は次のようになります。詳しくは、「[JSON スキーマを使ったアダプティブフォームの作成](../../forms/using/adaptive-form-json-schema-form-model.md)」を参照してください。

* **事前入力 JSON スキーマ**：事前入力 JSON は、関連する JSON スキーマに準拠していなければなりません。また、連結されていないフィールドも事前入力する場合は、オプションで/afData/afBoundDataオブジェクトに含めることができます。
* **送信されたJSON構造**:事前入力JSONが使用されない場合、送信されたJSONには、afDataのラッパータグ内の連結されたフィールドと連結されていないフィールドの両方のデータが含まれます。 事前入力JSONを使用する場合、送信されたJSONの構造は事前入力JSONと同じです。 JSON開始にafDataルートオブジェクトを事前入力する場合、出力JSONの形式は同じです。 事前入力JSONにafData/afBoundDataラッパーがなく、代わりにuserなどのスキーマルートオブジェクトから直接開始した場合、送信されたJSONもユーザーオブジェクトと開始します。

```
{
    "id": "https://some.site.somewhere/entry-schema#",
    "$schema": "https://json-schema.org/draft-04/schema#",
    "type": "object",
    "properties": {
        "address": {
            "type": "object",
            "properties": { 
    "name": {
     "type": "string"
    },
    "age": {
     "type": "integer"
}}}}}
```

JSON スキーマモデルを使用するフィールドの場合、以下の JSON のサンプルに示すように、afBoundedData オブジェクトのデータは事前入力されます。これは、1 つ以上の連結されていないテキストフィールドでアダプティブフォームを事前入力する場合に使用できます。Below is an example of data with `afData/afBoundData` wrapper:

```
{
  "afData": {
    "afUnboundData": {
      "data": { "textbox": "Ignorance is bliss :) " }
    },
    "afBoundData": {
      "data": { {
   "user": {
    "address": {
     "city": "Noida",
     "country": "India"
}}}}}}}
```

Below is an example without `afData/afBoundData` wrapper:

```
{
 "user": {
  "address": {
   "city": "Noida",
   "country": "India"
}}}
```

>[!NOTE]
>
>連結されているパネル（サイドキックまたは「データソース」タブからコンポーネントをドラッグして作成された、空ではない bindRef が含まれているパネル）では、連結されていないフィールドを使用することは&#x200B;**お勧めしません**。連結されていないフィールドで、データ損失が発生する可能性があるためです。特に連結していないフィールドについては、フォーム間で一意のフィールド名を設定することをお勧めします。

### フォームモデルのないアダプティブフォーム {#adaptive-form-with-no-form-model}

For adaptive forms with no form model, the data for all the fields is under the `<data>` tag of `<afUnboundData> tag`.

また、次のことを控えておいてください：

各種フィールドに送信されたユーザーデータのためのXMLタグは、フィールド名を使用して生成されます。したがって、一意のフィールド名を設定する必要があります。

```xml
<?xml version="1.0" encoding="UTF-8"?><afData>
  <afUnboundData>
    <data>
      <radiobutton>2</radiobutton>
      <repeatable_panel_no_form_model>
        <numericbox>12</numericbox>
      </repeatable_panel_no_form_model>
      <repeatable_panel_no_form_model>
        <numericbox>21</numericbox>
      </repeatable_panel_no_form_model>
      <checkbox>2</checkbox>
      <textbox>Nopes</textbox>
    </data>
  </afUnboundData>
  <afBoundData/>
</afData>
```

## Configuration Manager を使用した事前入力サービスの設定 {#configuring-prefill-service-using-configuration-manager}

事前入力サービスを有効にするには、AEM Webコンソールの設定で「Default Prefill Service Configuration」を指定します。 次の手順を使用して、事前入力サービスを設定します。

>[!NOTE]
>
>事前サービスの設定は、アダプティブフォーム、HTML5 フォーム、HTML5 フォームセットに適用することができます。

1. Open **[!UICONTROL Adobe Experience Manager Web Console Configuration]** by using the URL:\
   https://&lt;サーバー>:&lt;ポート>/system/console/configMgr
1. Search and open **[!UICONTROL Default Prefill Service Configuration]**.

   ![事前入力の設定](assets/prefill_config_new.png)

1. データの場所または正規表現を「**Data files locations**」に入力します。有効なデータファイルの場所の例は次のとおりです。

   * file:///C:/Users/public/Document/Prefill/*
   * https://localhost:8000/somesamplexmlfile.xml
   >[!NOTE]
   >
   >デフォルトでは、すべてのタイプのアダプティブフォーム（XSD、XDP、JSON、FDM、およびフォームモデルベースではない）のcrxファイルを通じて事前入力が許可されます。 事前入力は JSON ファイルおよび XML ファイルでのみ許可されます。

1. 事前入力サービスがフォームに対して設定されました。

   >[!NOTE]
   >
   >crx プロトコルは、事前入力済みデータのセキュリティを管理するので、デフォルトで許可されています。汎用的な正規表現を使用して他のプロトコル経由で事前入力すると、脆弱性が発生する可能性があります。データを保護するため、設定では安全性の高い URL を指定してください。

## 繰り返し可能なパネルの例外的なケース {#the-curious-case-of-repeatable-panels}

連結された（フォームスキーマ）フィールドや連結されていないフィールドは通常、同じアダプティブフォームに作成されます。ただし、連結が繰り返し可能な場合は、次のような例外があります。

* XFA フォームテンプレート、または XSD、JSON、FDM の各スキーマを使用したアダプティブフォームでは、連結されていない繰り返し可能なパネルはサポートされません。
* 連結された繰り返し可能なパネル内で、連結されていないフィールドを使用しないでください。

>[!NOTE]
>
>連結されていないフィールドにエンドユーザーが入力したデータ上で、連結されているフィールドと連結されていないフィールドが重複する場合は、これらのフィールドを混在させないようにします。可能な場合は、スキーマまたは XFA フォームテンプレートを変更し、連結されていないフィールドのエントリを追加します。これにより、フィールドが連結されて、そのデータを送信済みデータの他のフィールドのデータと同様に使用できます。

## ユーザーデータの事前入力でサポートされるプロトコル {#supported-protocols-for-prefilling-user-data}

以下のプロトコルを使用し、有効な正規表現で設定した場合、事前入力データフォーマットのユーザーデータをアダプティブフォームに事前入力できます。

### crx:// プロトコル {#the-crx-protocol}

```xml
https://localhost:4502/content/forms/af/xml.html?wcmmode=disabled&dataRef=crx:///tmp/fd/af/myassets/sample.xml
```

特定のノードには、`jcr:data` と呼ばれるプロパティがあり、データを保持していなければなりません。

### The file:// protocol  {#the-file-protocol-nbsp}

```xml
https://localhost:4502/content/forms/af/someAF.html?wcmmode=disabled&dataRef=file:///C:/Users/form-user/Downloads/somesamplexml.xml
```

参照元ファイルは、同じサーバー上になければなりません。

### https://プロトコル {#the-http-protocol}

```xml
https://localhost:4502/content/forms/af/xml.html?wcmmode=disabled&dataRef=https://localhost:8000/somesamplexmlfile.xml
```

### service:// プロトコル {#the-service-protocol}

```xml
https://localhost:4502/content/forms/af/abc.html?wcmmode=disabled&dataRef=service://[SERVICE_NAME]/[IDENTIFIER]
```

* SERVICE_NAME は OSGI 事前入力サービスの名前を参照します。「[事前入力サービスの作成と実行](../../forms/using/prepopulate-adaptive-form-fields.md#create-and-run-a-prefill-service)」を参照してください。
* IDENTIFIER は、事前入力データを取得するために OSGI 事前入力サービスが必要とするメタデータを参照します。ログイン済みユーザーの識別子は、使用できるメタデータの一例です。

>[!NOTE]
>
>認証パラメータの引き渡しはサポートされていません。

### slingRequestでのデータ属性の設定 {#setting-data-attribute-in-slingrequest}

You can also set the `data` attribute in `slingRequest`, where the `data` attribute is a string containing XML or JSON, as shown in the sample code below (Example is for XML):

```java
<%
           String dataXML="<afData>" +
                            "<afUnboundData>" +
                                "<data>" +
                                    "<first_name>"+ "Tyler" + "</first_name>" +
                                    "<last_name>"+ "Durden " + "</last_name>" +
                                    "<gender>"+ "Male" + "</gender>" +
                                    "<location>"+ "Texas" + "</location>" +
                                    "</data>" +
                            "</afUnboundData>" +
                        "</afData>";
        slingRequest.setAttribute("data", dataXML);
%>
```

すべてのデータが含まれている単純な XML または JSON 文字列を記述して、slingRequest に設定できます。これは、slingRequest data属性を設定するページに含むすべてのコンポーネントのレンダラ― JSP で、簡単にできます。

例えば、特定のタイプのヘッダーを使用して、特定のデザインのページを作成するとします。To achieve this, you can write your own `header.jsp`, which you can include in your page component and set the `data` attribute.

例えば、Facebook、Twitter、LinkedIn などのソーシャルアカウントを使用して、ログイン時にデータを事前入力するとします。この場合、`header.jsp`ユーザーアカウントからデータを取得し、データパラメーターを設定するに単純なJSPを含めることができます。

prefill-page component.zip

[ページコンポー](assets/prefill-page-component.zip)ネント内のFileSample prefill.jspの取得

## AEM Forms カスタム事前入力サービス {#aem-forms-custom-prefill-service}

事前定義されたソースからデータを頻繁に読み取る必要がある場合は、カスタム事前入力サービスを使用できます。事前入力サービスでは、定義済みデータソースからデータを読み取り、事前入力データファイルの内容を、アダプティブフォームのフィールドに事前入力します。事前入力データをアダプティブフォームと永続的に関連付ける場合にも役立ちます。

### 事前入力サービスの作成と実行 {#create-and-run-a-prefill-service}

事前入力サービスは OSGi サービスで、OSGi バンドルを使用してパッケージ化します。OSGi バンドルを作成し、アップロードし、AEM Forms バンドルにインストールします。バンドルの作成を開始する前に、以下を行います。

* [AEM Forms Client SDK をダウンロードします](https://helpx.adobe.com/jp/aem-forms/kb/aem-forms-releases.html)
* [ボイラープレートパッケージをダウンロードします](../../forms/using/prepopulate-adaptive-form-fields.md#main-pars-download-section-711716493)

* データ（事前入力データ）ファイルを crx-repository に配置します。ファイルは crx-repository の \contents フォルダー内の任意の場所に配置できます。

[ファイルを入手](assets/prefill-sumbit-xmlsandcontentpackage.zip)

#### 事前入力サービスの作成 {#create-a-prefill-service}

ボイラープレートパッケージ（サンプルの事前入力サービスパッケージ）には、AEM Forms 事前入力サービスのサンプル実装が含まれています。ボイラープレートパッケージをコードエディターで開きます。例えば、ボイラープレートプロジェクトを Eclipse で開いて編集します。ボイラープレートパッケージをコードエディターで開いたら、以下の手順でサービスを作成します。

1. src\main\java\com\adobe\test\Prefill.java ファイルを開いて編集します。
1. コードで、以下の値を設定します。

   * `nodePath:` crx-repositoryの場所を指すnode path変数には、データ（事前入力）ファイルのパスが含まれます。 例：/content/prefilldata.xml
   * `label:` labelパラメーターは、サービスの表示名を指定します。 例：Default Prefill Service

1. Save and close the `Prefill.java` file.
1. Add the `AEM Forms Client SDK` package to the build path of the boilerplate project.
1. プロジェクトをコンパイルし、バンドルの .jar を作成します。

#### 事前入力サービスを起動し、使用します {#start-and-use-the-prefill-service}

事前入力サービスを起動するには、JAR ファイルを AEM Forms Web Console にアップロードし、サービスをアクティブ化します。サービスはアダプティブフォームエディターに表示されるようになります。事前入力サービスをアダプティブフォームに関連付けるには：

1. アダプティブフォームをフォームエディターで開き、フォームコンテナのプロパティパネルを開きます。
1. プロパティコンソールで、AEM Form コンテナ／基本／事前入力サービスに移動します。
1. Default Prefill Service を選択し、「**[!UICONTROL 保存]**」をクリックします。サービスはフォームに関連付けられます。

