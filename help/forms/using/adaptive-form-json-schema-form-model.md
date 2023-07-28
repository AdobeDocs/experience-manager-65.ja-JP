---
title: JSON スキーマを使用してアダプティブフォームを作成する方法。
description: JSON スキーマをフォームモデルとして使用してアダプティブフォームを作成する方法を説明します。アダプティブフォームの作成には、既存の JSON スキーマを使用できます。JSON スキーマのサンプルをさらに詳しく調べ、JSON スキーマ定義のフィールドを事前設定し、アダプティブフォームコンポーネントの許容値を制限し、サポートされていない構成を学習します。
feature: Adaptive Forms
role: User, Developer
level: Beginner, Intermediate
exl-id: 1b402aef-a319-4d32-8ada-cadc86f5c872
source-git-commit: f11bb43d914a43431cab408ca77690b6ba528a06
workflow-type: tm+mt
source-wordcount: '1861'
ht-degree: 73%

---

# JSON スキーマを使用したアダプティブフォームの作成 {#creating-adaptive-forms-using-json-schema}

<span class="preview"> Adobeでは、最新の拡張可能なデータキャプチャを使用することをお勧めします [コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja) 対象： [新しいアダプティブFormsの作成](/help/forms/using/create-an-adaptive-form-core-components.md) または [AEM SitesページへのアダプティブFormsの追加](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). これらのコンポーネントは、アダプティブFormsの作成における大幅な進歩を表し、印象的なユーザーエクスペリエンスを実現します。 この記事では、基盤コンポーネントを使用してアダプティブFormsを作成する古い方法について説明します。 </span>

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/adaptive-form-json-schema-form-model.html?lang=ja) |
| AEM 6.5 | この記事 |


## 前提条件 {#prerequisites}

フォームモデルとして JSON スキーマを使用してアダプティブフォームをオーサリングする場合、JSON スキーマの基本を理解している必要があります。この記事を読む前に、以下のコンテンツを読んでおくことをお勧めします。

* [アダプティブフォームの作成](creating-adaptive-form.md)
* [JSON スキーマ](https://json-schema.org/)

## フォームモデルとしての JSON スキーマの使用  {#using-a-json-schema-as-form-model}

[!DNL Adobe Experience Manager Forms] では、既存の JSON スキーマをフォームモデルとして使用したアダプティブフォームの作成がサポートされています。JSON スキーマは、組織内のバックエンドシステムによってデータが作成または使用される構造を表します。使用する JSON スキーマは、[v4 仕様](https://json-schema.org/draft-04/schema)に準拠している必要があります。

JSON スキーマの使用上の主な特長を以下に示します。

* JSON の構造は、アダプティブフォームのオーサリングモードの「コンテンツファインダー」タブにツリーとして表示されます。 JSON 階層からアダプティブフォームに要素をドラッグして追加することができます。
* 関連付けられたスキーマに準拠する JSON を使用して、フォームに事前入力できます。
* ユーザーが入力したデータは、送信時には関連付けられたスキーマに適合する JSON として送信されます。

JSON スキーマは、単純型要素と複合型要素で構成されています。要素には、その要素にルールを追加する属性が含まれています。これらの要素と属性がアダプティブフォームにドラッグされると、対応するアダプティブフォームコンポーネントに自動的にマッピングされます。

この JSON 要素とアダプティブフォームコンポーネントのマッピングは、次のようになります。

```json
"birthDate": {
              "type": "string",
              "format": "date",
              "pattern": "date{DD MMMM, YYYY}",
              "aem:affKeyword": [
                "DOB",
                "Date of Birth"
              ],
              "description": "Date of birth in DD MMMM, YYYY",
              "aem:afProperties": {
                "displayPictureClause": "date{DD MMMM, YYYY}",
                "displayPatternType": "date{DD MMMM, YYYY}",
                "validationPatternType": "date{DD MMMM, YYYY}",
                "validatePictureClause": "date{DD MMMM, YYYY}",
                "validatePictureClauseMessage": "Date must be in DD MMMM, YYYY format."
              }
```

<table>
 <tbody>
  <tr>
   <th><strong>JSON の要素、プロパティ、属性</strong></th>
   <th><strong>アダプティブフォームコンポーネント</strong></th>
  </tr>
  <tr>
   <td><p>enum および enumNames 制約を含む string プロパティ。</p> <p>構文</p> <p> <code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>"enum" : ["M", "F"]</code></p> <p><code>"enumNames" : ["Male", "Female"]</code></p> <p><code>}</code></p> <p> </p> </td>
   <td><p>ドロップダウンコンポーネント：</p>
    <ul>
     <li>enumNames にリストされた値はドロップボックスに表示されます。</li>
     <li>enum にリストされた値は計算に使用されます。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>format 制約を含む string プロパティ。例えば、メール、日付など。</p> <p>構文</p> <p><code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>"format" : "email"</code></p> <p><code>}</code></p> <p> </p> </td>
   <td>
    <ul>
     <li>type が string で format が email の場合、メールコンポーネントがマップされます。</li>
     <li>type が string で format が hostname の場合、検証を含むテキストボックスコンポーネントがマップされます。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>}</code></p> </td>
   <td><br /> <br /> テキストフィールド<br /> <br /> <br /> </td>
  </tr>
  <tr>
   <td>number プロパティ<br /> </td>
   <td>サブタイプが float に設定された数値フィールド<br /> </td>
  </tr>
  <tr>
   <td>integer プロパティ<br /> </td>
   <td>サブタイプが integer に設定された数値フィールド<br /> </td>
  </tr>
  <tr>
   <td>boolean プロパティ<br /> </td>
   <td>切り替え<br /> </td>
  </tr>
  <tr>
   <td>object プロパティ<br /> </td>
   <td>パネル<br /> </td>
  </tr>
  <tr>
   <td>array プロパティ</td>
   <td>minItems および maxItems にそれぞれ等しい min および max を持つ繰り返し可能なパネル。同種の配列のみがサポートされます。そのため、項目制限は、配列でなくオブジェクトである必要があります。<br /> </td>
  </tr>
 </tbody>
</table>

### 共通のスキーマプロパティ {#common-schema-properties}

アダプティブフォームは JSON スキーマで使用可能な情報を使用して、生成された各フィールドをマッピングします。具体的には、以下のようになります。

* `title` プロパティは、アダプティブフォームコンポーネントのラベルとして機能します。
* `description` プロパティは、アダプティブフォームコンポーネントの詳細な説明として設定されます。
* `default` プロパティは、アダプティブフォームフィールドの初期値として機能します。
* `maxLength` プロパティは、テキストフィールドコンポーネントの `maxlength` 属性として設定されます。
* `minimum`、`maximum`、`exclusiveMinimum` および `exclusiveMaximum` プロパティは、数値ボックスコンポーネントに使用されます。
* `DatePicker component` の範囲をサポートするために、追加の JSON スキーマプロパティ `minDate` および `maxDate` が用意されています。
* `minItems` および `maxItems` プロパティは、パネルコンポーネントに追加または削除される可能性のある項目／フィールドの数を制限するために使用されます。
* `readOnly` プロパティは、アダプティブフォームコンポーネントの `readonly` 属性を設定します。
* `required` プロパティは、アダプティブフォームフィールドを必須としてマークします。一方、パネル（タイプがオブジェクト）の場合、最終的に送信された JSON データには、そのオブジェクトに対応する空の値を持つフィールドがあります。
* `pattern` プロパティは、アダプティブフォームで検証パターン（正規表現）として設定されます。
* JSON スキーマファイルの拡張子は、.schema.json を維持する必要があります。例えば、&lt;filename>.schema.json のように指定します。

## JSON スキーマのサンプル {#sample-json-schema}

JSON スキーマの例を示します。

```json
{
 "$schema": "https://json-schema.org/draft-04/schema#",
 "definitions": {
  "employee": {
   "type": "object",
   "properties": {
    "userName": {
     "type": "string"
    },
    "dateOfBirth": {
     "type": "string",
     "format": "date"
    },
    "email": {
     "type": "string",
     "format": "email"
    },
    "language": {
     "type": "string"
    },
    "personalDetails": {
     "$ref": "#/definitions/personalDetails"
    },
    "projectDetails": {
     "$ref": "#/definitions/projectDetails"
    }
   },
   "required": [
    "userName",
    "dateOfBirth",
    "language"
   ]
  },
  "personalDetails": {
   "type": "object",
   "properties": {
    "GeneralDetails": {
     "$ref": "#/definitions/GeneralDetails"
    },
    "Family": {
     "$ref": "#/definitions/Family"
    },
    "Income": {
     "$ref": "#/definitions/Income"
    }
   }
  },
  "projectDetails": {
   "type": "array",
   "items": {
    "properties": {
     "name": {
      "type": "string"
     },
     "age": {
      "type": "number"
     },
     "projects": {
      "$ref": "#/definitions/projects"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  },
  "projects": {
   "type": "array",
   "items": {
    "properties": {
     "name": {
      "type": "string"
     },
     "age": {
      "type": "number"
     },
     "projectsAdditional": {
      "$ref": "#/definitions/projectsAdditional"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  },
  "projectsAdditional": {
   "type": "array",
   "items": {
    "properties": {
     "Additional_name": {
      "type": "string"
     },
     "Additional_areacode": {
      "type": "number"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  },
  "GeneralDetails": {
   "type": "object",
   "properties": {
    "age": {
     "type": "number"
    },
    "married": {
     "type": "boolean"
    },
    "phone": {
     "type": "number",
     "aem:afProperties": {
      "sling:resourceType": "/libs/fd/af/components/guidetelephone",
      "guideNodeClass": "guideTelephone"
     }
    },
    "address": {
     "type": "string"
    }
   }
  },
  "Family": {
   "type": "object",
   "properties": {
    "spouse": {
     "$ref": "#/definitions/spouse"
    },
    "kids": {
     "$ref": "#/definitions/kids"
    }
   }
  },
  "Income": {
   "type": "object",
   "properties": {
    "monthly": {
     "type": "number"
    },
    "yearly": {
     "type": "number"
    }
   }
  },
  "spouse": {
   "type": "object",
   "properties": {
    "name": {
     "type": "string"
    },
    "Income": {
     "$ref": "#/definitions/Income"
    }
   }
  },
  "kids": {
   "type": "array",
   "items": {
    "properties": {
     "name": {
      "type": "string"
     },
     "age": {
      "type": "number"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  }
 },
 "type": "object",
 "properties": {
  "employee": {
   "$ref": "#/definitions/employee"
  }
 }
}
```

### 再使用可能なスキーマ定義 {#reusable-schema-definitions}

定義キーを使用して、再使用可能なスキーマを識別します。再使用可能なスキーマ定義を使用して、フラグメントを作成します。これは、XSD で複合タイプを識別する場合と似ています。 定義を含む JSON スキーマのサンプルを以下に示します。

```json
{
  "$schema": "https://json-schema.org/draft-04/schema#",

  "definitions": {
    "address": {
      "type": "object",
      "properties": {
        "street_address": { "type": "string" },
        "city":           { "type": "string" },
        "state":          { "type": "string" }
      },
      "required": ["street_address", "city", "state"]
    }
  },

  "type": "object",

  "properties": {
    "billing_address": { "$ref": "#/definitions/address" },
    "shipping_address": { "$ref": "#/definitions/address" }
  }
}
```

上記の例では、各顧客が出荷先と請求先の両方の住所を持つ顧客レコードを定義します。どちらの住所も構造（都道府県、市区町村、番地など）が同じ場合は、住所が重複しないようにすることをお勧めします。また、今後変更が行われたときに、簡単にフィールドを追加したり削除したりできます。

## JSON スキーマ定義でのフィールドの事前設定 {#pre-configuring-fields-in-json-schema-definition}

**aem:afProperties** プロパティを使用して JSON スキーマのフィールドを事前構成し、カスタムのアダプティブフォームコンポーネントにマップできます。以下に例を示します。

```json
{
    "properties": {
        "sizeInMB": {
            "type": "integer",
            "minimum": 16,
            "maximum": 512,
            "aem:afProperties" : {
                 "sling:resourceType" : "/apps/fd/af/components/guideTextBox",
                 "guideNodeClass" : "guideTextBox"
             }
        }
    },
    "required": [ "sizeInMB" ],
    "additionalProperties": false
}
```

## フォームオブジェクトのスクリプトまたは式の設定  {#configure-scripts-or-expressions-for-form-objects}

JavaScript はアダプティブフォームの式言語です。 すべての式は有効な JavaScript 式で、アダプティブフォームのスクリプティングモデル API を使用します。 フォームオブジェクトを事前設定して、フォームイベントの[式を評価](adaptive-form-expressions.md)できます。

アダプティブフォームの式やスクリプトをアダプティブフォームのコンポーネント用に事前設定するには、aem:afproperties プロパティを使用します。例えば、initialize イベントがトリガーされると、次のコードは電話フィールドの値を設定し、値をログに出力します。

```json
"telephone": {
  "type": "string",
  "pattern": "/\\d{10}/",
  "aem:affKeyword": ["phone", "telephone","mobile phone", "work phone", "home phone", "telephone number", "telephone no", "phone number"],
  "description": "Telephone Number",
  "aem:afProperties" : {
    "sling:resourceType" : "fd/af/components/guidetelephone",
    "guideNodeClass" : "guideTelephone",
    "events": {
      "Initialize" : "this.value = \"1234567890\"; console.log(\"ef:gh\") "
    }
  }
}
```

フォームオブジェクトのスクリプトや式を構成するには、[forms-power-user グループ](forms-groups-privileges-tasks.md)のメンバーである必要があります。次の表に、アダプティブフォームコンポーネントでサポートされるすべてのスクリプトイベントを示します。

<table>
 <tbody>
  <tr>
   <th><strong></strong>コンポーネント \ イベント</th>
   <th>initialize <br /> </th>
   <td>Calculate</td>
   <td>視認性</td>
   <td>Validate（検証）</td>
   <td>Enabled</td>
   <td>値コミット</td>
   <td>クリック </td>
   <td>オプション</td>
  </tr>
  <tr>
   <td>テキストフィールド</td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>数値フィールド</td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>数値ステッパー</td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>ラジオボタン</td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>電話番号</td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>切り替え</td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>ボタン</td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td> </td>
  </tr>
  <tr>
   <td>チェックボックス</td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>ドロップダウン</td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>画像選択</td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>データ入力フィールド</td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>日付選択</td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>メール</td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>ファイル添付</td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>画像</td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>図面</td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>パネル</td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="はいチェックマークアイコン" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

JSON でのイベントの使用例としては、initialize イベントでフィールドを非表示にし、値コミットイベントで別のフィールドの値を設定する例があります。スクリプトイベントの式の作成について詳しくは、[アダプティブフォームの式](adaptive-form-expressions.md)を参照してください。

前述の例のサンプル JSON コードを以下に示します。

### initialize イベントでのフィールドの非表示 {#hiding-a-field-on-initialize-event}

```json
"name": {
    "type": "string",
    "aem:afProperties": {
        "events" : {
            "Initialize" : "this.visible = false;"
        }
    }
}
```

#### 値コミットイベントでの別のフィールドの値の設定 {#configure-value-of-another-field-on-value-commit-event}

```json
"Income": {
    "type": "object",
    "properties": {
        "monthly": {
            "type": "number",
            "aem:afProperties": {
                "events" : {
                    "Value Commit" : "IncomeYearly.value = this.value * 12;"
                }
            }
        },
        "yearly": {
            "type": "number",
            "aem:afProperties": {
                "name": "IncomeYearly"
            }
        }
    }
}
```

## アダプティブフォームコンポーネントで許容される値の制限 {#limit-acceptable-values-for-an-adaptive-form-component}

JSON スキーマの要素に次の制限を追加して、アダプティブフォームコンポーネントで許容される値を制限できます。

<table>
 <tbody>
  <tr>
   <td><p><strong> スキーマプロパティ</strong></p> </td>
   <td><p><strong>データタイプ</strong></p> </td>
   <td><p><strong>説明</strong></p> </td>
   <td><p><strong>コンポーネント</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>maximum</code></p> </td>
   <td><p>文字列</p> </td>
   <td><p>数値および日付の上限を指定します。デフォルトでは、最大値が含まれます。</p> </td>
   <td>
    <ul>
     <li>数値ボックス</li>
     <li>数値ステッパー<br /> </li>
     <li>日付選択</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>minimum</code></p> </td>
   <td><p>文字列</p> </td>
   <td><p>数値および日付の下限を指定します。デフォルトでは、最小値が含まれます。</p> </td>
   <td>
    <ul>
     <li>数値ボックス</li>
     <li>数値ステッパー</li>
     <li>日付選択</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMaximum</code></p> </td>
   <td><p>ブール値</p> </td>
   <td><p>true の場合、フォームのコンポーネントで指定された数値または日付は、maximum プロパティに指定された数値または日付よりも小さい値である必要があります。</p> <p>false の場合、フォームのコンポーネントで指定された数値または日付は、maximum プロパティに指定された数値または日付以下の値である必要があります。</p> </td>
   <td>
    <ul>
     <li>数値ボックス</li>
     <li>数値ステッパー</li>
     <li>日付選択</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMinimum</code></p> </td>
   <td><p>ブール値</p> </td>
   <td><p>true の場合、フォームのコンポーネントで指定された数値または日付は、minimum プロパティに指定された数値または日付よりも大きい値である必要があります。</p> <p>false の場合、フォームのコンポーネントで指定された数値または日付は、minimum プロパティに指定された数値または日付以上の値である必要があります。</p> </td>
   <td>
    <ul>
     <li>数値ボックス</li>
     <li>数値ステッパー</li>
     <li>日付選択</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>minLength</code></p> </td>
   <td><p>文字列</p> </td>
   <td><p>コンポーネントで許可される最小文字数を指定します。最小の長さは 0 以上である必要があります。</p> </td>
   <td>
    <ul>
     <li>テキストボックス</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>maxLength</code></td>
   <td>文字列</td>
   <td>コンポーネントで許可される最大文字数を指定します。最大の長さは 0 以上である必要があります。</td>
   <td>
    <ul>
     <li>テキストボックス</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>pattern</code></p> </td>
   <td><p>文字列</p> </td>
   <td><p>文字のシーケンスを指定します。文字が指定されたパターンに適合すると、コンポーネントはその文字を受け入れます。</p> <p>pattern プロパティは、対応するアダプティブフォームコンポーネントの検証パターンにマッピングされます。</p> </td>
   <td>
    <ul>
     <li>XSD スキーマにマップされるすべてのアダプティブフォームコンポーネント </li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>maxItems</code></td>
   <td>文字列</td>
   <td>配列の項目の最大数を指定します。項目の最大数は 0 以上である必要があります。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>minItems</code></td>
   <td>文字列</td>
   <td>配列の項目の最小数を指定します。項目の最小数は 0 以上である必要があります。</td>
   <td> </td>
  </tr>
 </tbody>
</table>



## スキーマ準拠データを有効にする {#enablig-schema-compliant-data}

アダプティブフォームがフォーム送信時にスキーマに準拠したデータを生成するには、次の手順を実行します。

1. Experience ManagerWeb コンソール ( ) に移動します。 `https://server:host/system/console/configMgr`.
1. 場所 **[!UICONTROL アダプティブフォームとインタラクティブ通信の Web チャネル設定]**.
1. その設定をタップして編集モードで開きます。
1. を選択します。 **[!UICONTROL スキーマ準拠データを生成]** チェックボックス。
1. 設定を保存します。

![アダプティブフォームとインタラクティブ通信の Web チャネル設定](/help/forms/using/assets/af-ic-web-channel-configuration.png)

## サポート対象外の構成  {#non-supported-constructs}

アダプティブフォームは次の JSON スキーマ構成をサポートしていません。

* Null タイプ
* any などの Union タイプ
* OneOf、AnyOf、AllOf、NOT
* 同種の配列のみがサポートされます。そのため、項目制限は、配列でなくオブジェクトである必要があります。

## よくある質問 {#frequently-asked-questions}

**繰り返し可能なサブフォーム（minOccurs 値または maxOccurs 値が 1 より大きい）では、サブフォーム（任意の複合型から生成された構造）の個々の要素をドラッグできないのはなぜですか？**

繰り返し可能なサブフォームでは、完全なサブフォームを使用する必要があります。選択した一部のフィールドのみを使用する場合は、構造全体を使用し、不要部分を削除します。

**コンテンツファインダーに長く複雑な構造があります。特定の要素を見つけるにはどうすればよいですか？**

以下の 2 つのオプションがあります。

* ツリー構造をスクロールする
* 検索ボックスを使用して、要素を検索する

**JSON スキーマファイルの拡張子は何ですか。**

JSON スキーマファイルの拡張子は、.schema.json にする必要があります。例えば、&lt;filename>.schema.json のように指定します。
