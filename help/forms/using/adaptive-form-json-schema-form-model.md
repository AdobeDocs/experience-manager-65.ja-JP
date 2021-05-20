---
title: JSONスキーマを使用してアダプティブFormsを作成する方法
description: JSONスキーマをフォームモデルとして使用してアダプティブフォームを作成する方法を説明します。 既存のJSONスキーマを使用してアダプティブフォームを作成することができます。 JSONスキーマのサンプルを使用して、より深く掘り下げ、JSONスキーマ定義のフィールドを事前設定し、アダプティブフォームコンポーネントの有効な値を制限し、サポートされていない構成要素を学びます。
feature: アダプティブフォーム
role: Business Practitioner, Developer
level: Beginner, Intermediate
exl-id: 1b402aef-a319-4d32-8ada-cadc86f5c872
source-git-commit: ad67634278088f8f953fde61a3543acdd70537dd
workflow-type: tm+mt
source-wordcount: '1450'
ht-degree: 73%

---

# JSON スキーマを使用したアダプティブフォームの作成 {#creating-adaptive-forms-using-json-schema}

## 前提条件 {#prerequisites}

JSONスキーマをフォームモデルとして使用してアダプティブフォームを作成する場合は、JSONスキーマの基本を理解しておく必要があります。 この記事を読む前に、以下のコンテンツを読んでおくことをお勧めします。

* [アダプティブフォームの作成](creating-adaptive-form.md)
* [JSON スキーマ](https://json-schema.org/)

## フォームモデルとしての JSON スキーマの使用     {#using-a-json-schema-as-form-model}

[!DNL Adobe Experience Manager Forms] では、既存の JSON スキーマをフォームモデルとして使用したアダプティブフォームの作成がサポートされています。JSON スキーマは、組織内のバックエンドシステムによってデータが作成または使用される構造を表します。使用する JSON スキーマは、[v4 仕様](https://json-schema.org/draft-04/schema)に準拠している必要があります。

JSON スキーマの使用の主な特長を以下に示します。

* JSON の構造は、アダプティブフォームのオーサリングモードの「コンテンツファインダー」タブでツリーとして表示されます。JSON 階層からアダプティブフォームに要素をドラッグして追加できます。
* 関連付けられたスキーマに準拠する JSON を使用して、フォームに事前入力できます。
* ユーザーが入力したデータは、送信時には関連付けられたスキーマに適合する JSON として送信されます。

JSON スキーマは、単純型要素と複合型要素で構成されています。要素には、その要素にルールを追加する属性が含まれています。これらの要素や属性がアダプティブフォーム上にドラッグされると、自動的に該当するアダプティブフォームコンポーネントにマッピングされます。

JSON 要素とアダプティブフォームコンポーネントのマッピングは、次のように行われます。

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
   <td><p>enum および enumNames 制約を含む string プロパティ。</p> <p>構文、</p> <p> <code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>"enum" : ["M", "F"]</code></p> <p><code>"enumNames" : ["Male", "Female"]</code></p> <p><code>}</code></p> <p> </p> </td>
   <td><p>ドロップダウンコンポーネント：</p>
    <ul>
     <li>enumNames にリストされた値はドロップボックスに表示されます。</li>
     <li>enum にリストされた値は計算に使用されます。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>format 制約を含む string プロパティ。例えば、電子メール、日付など。</p> <p>構文、</p> <p><code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>"format" : "email"</code></p> <p><code>}</code></p> <p> </p> </td>
   <td>
    <ul>
     <li>type が string で format が email の場合、電子メールコンポーネントがマップされます。</li>
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

* `title`プロパティは、アダプティブフォームコンポーネントのラベルとして機能します。
* `description`プロパティは、アダプティブフォームコンポーネントの詳細な説明として設定されます。
* `default`プロパティは、アダプティブフォームフィールドの初期値として機能します。
* `maxLength` プロパティは、テキストフィールドコンポーネントの `maxlength` 属性として設定されます。
* `minimum`、`maximum`、`exclusiveMinimum` および `exclusiveMaximum` プロパティは、数値ボックスコンポーネントに使用されます。
* `DatePicker component` の範囲をサポートするために、追加の JSON スキーマプロパティ `minDate` および `maxDate` が用意されています。
* `minItems` および `maxItems` プロパティは、パネルコンポーネントに追加または削除される可能性のある項目／フィールドの数を制限するために使用されます。
* `readOnly`プロパティは、アダプティブフォームコンポーネントの`readonly`属性を設定します。
* `required`プロパティはアダプティブフォームフィールドを必須としてマークします。一方、パネル（タイプはオブジェクト）では、最終的に送信されたJSONデータは、そのオブジェクトに対応する値が空のフィールドを持ちます。
* `pattern`プロパティは、アダプティブフォームの検証パターン（正規表現）として設定されます。
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

定義キーを使用して、再使用可能なスキーマを識別します。再使用可能なスキーマ定義を使用して、フラグメントを作成します。これは、XSD での複合型の識別と同じです。定義を含む JSON スキーマのサンプルを以下に示します。

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

## JSON スキーマ定義でのフィールドの事前設定  {#pre-configuring-fields-in-json-schema-definition}

**aem:afProperties**&#x200B;プロパティを使用して、JSONスキーマフィールドを事前設定し、カスタムのアダプティブフォームコンポーネントにマッピングすることができます。 以下に例を示します。

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

## フォームオブジェクトのスクリプトまたは式の設定{#configure-scripts-or-expressions-for-form-objects}

アダプティブフォームの式言語はJavascriptです。すべての数式は有効なJavaScriptの数式で、アダプティブフォームのスクリプトモデルAPIを使用しています。フォームイベントで式](adaptive-form-expressions.md)を評価するように、フォームオブジェクトを事前に設定することができます。[

アダプティブフォームの数式やスクリプトをアダプティブフォームのコンポーネント用に事前設定するには、 aem:afpropertiesプロパティを使用します。 例えば、 initializeイベントがトリガーされると、次のコードは電話フィールドの値を設定し、ログに値を出力します。

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

フォームオブジェクトのスクリプトや式を設定するには、[forms-power-userグループ](forms-groups-privileges-tasks.md)のメンバーである必要があります。 次の表に、アダプティブフォームコンポーネントでサポートされるすべてのスクリプトイベントを示します。

<table>
 <tbody>
  <tr>
   <th><strong></strong>Component \ Event</th>
   <th>initialize <br /> </th>
   <td>Calculate</td>
   <td>視認性</td>
   <td>Validate</td>
   <td>Enabled</td>
   <td>値コミット</td>
   <td>クリック </td>
   <td>オプション</td>
  </tr>
  <tr>
   <td>テキストフィールド</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>数値フィールド</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>数値ステッパー</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>ラジオボタン</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>電話番号</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>切り替え</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>ボタン</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
  </tr>
  <tr>
   <td>チェックボックス</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>ドロップダウン</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>画像選択</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>データ入力フィールド</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>日付選択</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>電子メール</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>添付ファイル</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>画像</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>図面</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>パネル</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

JSONでのイベントの使用例としては、initializeイベントのフィールドを非表示にし、値コミットイベントの別のフィールドの値を設定する例があります。 スクリプトイベントの式を作成する方法について詳しくは、「[アダプティブフォームの式](adaptive-form-expressions.md)」を参照してください。

前述の例のサンプルJSONコードを以下に示します。

### initializeイベント{#hiding-a-field-on-initialize-event}でのフィールドの非表示

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

#### 値コミットイベントの別のフィールドの値を設定する{#configure-value-of-another-field-on-value-commit-event}

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

JSONスキーマの要素に次の制限を追加して、アダプティブフォームコンポーネントで許容される値を制限することができます。

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
   <td><p>文字のシーケンスを指定します。文字が指定されたパターンに適合すると、コンポーネントはその文字を受け入れます。</p> <p>この pattern プロパティは、対応するアダプティブフォームコンポーネントの検証パターンにマッピされます。</p> </td>
   <td>
    <ul>
     <li>XSDスキーマにマッピングされているすべてのアダプティブフォームコンポーネント </li>
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

## サポート対象外の構成 {#non-supported-constructs}

アダプティブフォームは、次のJSONスキーマ構成をサポートしていません。

* Null タイプ
* any などの Union タイプ
* OneOf、AnyOf、AllOf、NOT
* 同種の配列のみがサポートされます。そのため、項目制限は、配列でなくオブジェクトである必要があります。

## よくある質問 {#frequently-asked-questions}

**繰り返し可能なサブフォーム（minOccours 値または maxOccurs 値が 1 より大きい）では、サブフォーム（任意の複合型から生成された構造）の個々の要素をドラッグできないのはなぜですか？**

繰り返し可能なサブフォームでは、完全なサブフォームを使用する必要があります。選択した一部のフィールドのみを使用する場合は、構造全体を使用し、不要部分を削除します。

**コンテンツファインダーに長く複雑な構造があります。特定の要素を見つけるにはどうすればよいですか？**

以下の 2 つのオプションがあります。

* ツリー構造をスクロールする
* 検索ボックスを使用して、要素を検索する

**JSON スキーマファイルの拡張子は何ですか。**

JSON スキーマファイルの拡張子は、.schema.json にする必要があります。例えば、&lt;filename>.schema.json のように指定します。
