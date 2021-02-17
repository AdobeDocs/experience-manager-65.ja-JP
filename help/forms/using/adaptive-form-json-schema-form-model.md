---
title: JSONスキーマを使用したアダプティブFormsの作成方法
description: フォームモデルとしてJSONスキーマを使用してアダプティブフォームを作成する方法を学びます。 アダプティブフォームの作成には、既存のJSONスキーマを使用できます。 JSONスキーマのサンプルを参照し、JSONスキーマ定義のフィールドを事前設定し、アダプティブフォームコンポーネントの許容値を制限し、サポートされていない構成を学びます。
feature: Adaptive Forms
role: Business Practitioner, Developers
level: Beginner, Imtermediate
translation-type: tm+mt
source-git-commit: 37ab98c9c78af452887c32101287b6d7f18d9d91
workflow-type: tm+mt
source-wordcount: '1448'
ht-degree: 61%

---


# JSON スキーマを使用したアダプティブフォームの作成 {#creating-adaptive-forms-using-json-schema}

## 前提条件 {#prerequisites}

フォームモデルとしてJSONスキーマを使用してアダプティブフォームを作成する場合は、JSONのスキーマに関する基本的な理解が必要です。 この記事を読む前に次のコンテンツを読んでおくことをお勧めします。

* [アダプティブフォームの作成](creating-adaptive-form.md)
* [JSON スキーマ](https://json-schema.org/)

## フォームモデルとしての JSON スキーマの使用   {#using-a-json-schema-as-form-model}

[!DNL Adobe Experience Manager Forms] では、既存の JSON スキーマをフォームモデルとして使用したアダプティブフォームの作成がサポートされています。JSON スキーマは、組織のバックエンドシステムによりデータの生成や消費が行われる構造を表しています。使用するJSONスキーマは、[v4仕様](https://json-schema.org/draft-04/schema)に準拠している必要があります。

JSONスキーマを使用する主な機能は次のとおりです。

* JSON の構造は、アダプティブフォームのオーサリングモードの「コンテンツファインダー」タブでツリーとして表示されます。JSON 階層からアダプティブフォームに要素をドラッグして追加できます。
* 関連付けられたスキーマに準拠する JSON を使用して、フォームに事前入力できます。
* ユーザーが入力したデータは、送信時には関連付けられたスキーマに適合する JSON として送信されます。

JSONスキーマは、単純型と複合型の要素で構成されます。 要素には、その要素にルールを追加する属性が含まれています。これらの要素や属性がアダプティブフォーム上にドラッグされると、自動的に該当するアダプティブフォームコンポーネントにマッピングされます。

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
   <td><p>enum制約とenumNames制約を含む文字列プロパティ。</p> <p>構文,</p> <p> <code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>"enum" : ["M", "F"]</code></p> <p><code>"enumNames" : ["Male", "Female"]</code></p> <p><code>}</code></p> <p> </p> </td>
   <td><p>ドロップダウンコンポーネント：</p>
    <ul>
     <li>enumNames にリストされた値はドロップボックスに表示されます。</li>
     <li>enum にリストされた値は計算に使用されます。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>フォーマット制限付きの文字列プロパティ。例えば、電子メール、日付など。</p> <p>構文,</p> <p><code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>"format" : "email"</code></p> <p><code>}</code></p> <p> </p> </td>
   <td>
    <ul>
     <li>タイプが文字列でフォーマットが電子メールのときに、電子メールのコンポーネントがマップされます。</li>
     <li>タイプが文字列でフォーマットがホスト名のときに、検証付きテキストボックスのコンポーネントがマップされます。</li>
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
   <td>minItems および maxItems にそれぞれ等しい min および max を持つ繰り返し可能なパネル。同種の配列のみがサポートされます。したがって、項目制約は配列ではなくオブジェクトでなければなりません。<br /> </td>
  </tr>
 </tbody>
</table>

### 共通のスキーマプロパティ {#common-schema-properties}

アダプティブフォームは JSON スキーマで使用可能な情報を使用して、生成された各フィールドをマッピングします。具体的には、次のことを実行します。

* `title`プロパティは、アダプティブフォームコンポーネントのラベルとして機能します。
* `description`プロパティは、アダプティブフォームコンポーネントの詳細な説明として設定されます。
* `default`プロパティは、アダプティブフォームフィールドの初期値として機能します。
* `maxLength`プロパティは、テキストフィールドコンポーネントの`maxlength`属性として設定されます。
* `minimum`、`maximum`、`exclusiveMinimum`および`exclusiveMaximum`プロパティは、数値ボックスコンポーネントに使用されます。
* `DatePicker component`の追加のJSONスキーマプロパティ`minDate`と`maxDate`の範囲をサポートするために提供されます。
* `minItems`プロパティと`maxItems`プロパティは、パネルコンポーネントに追加または削除できる項目やフィールドの数を制限するために使用します。
* `readOnly`プロパティは、アダプティブフォームコンポーネントの`readonly`属性を設定します。
* `required`プロパティはアダプティブフォームフィールドを必須としてマークしますが、パネル（typeはobject）では最終的に送信されるJSONデータには、そのオブジェクトに対応する空の値を持つフィールドがあります。
* `pattern`プロパティは、アダプティブフォームの検証パターン(正規式)として設定されます。
* JSONスキーマファイルの拡張子は。スキーマ.jsonにする必要があります。 例えば、&lt;filename>.スキーマ.jsonのように指定します。

## JSON スキーマのサンプル {#sample-json-schema}

JSONスキーマの例を示します。

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

定義キーを使用して再使用可能なスキーマを識別します。フラグメントの作成には、再利用可能なスキーマ定義が使用されます。 これは、XSD での複合型の識別と同じです。定義付きの JSON スキーマのサンプルは以下のとおりです。

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

上記の例では、それぞれの顧客が出荷先と請求先のどちらの住所もある場合の顧客レコードを定義します。どちらの住所も構造（都道府県、市区町村、番地など）が同じ場合は、住所が重複しないようにすることをお勧めします。また、今後変更が行われたときに、簡単にフィールドを追加したり削除したりできます。

## JSON スキーマ定義におけるフィールドの事前構成  {#pre-configuring-fields-in-json-schema-definition}

**aem:afProperties**&#x200B;プロパティを使用して、JSONスキーマフィールドを事前設定し、カスタムアダプティブフォームコンポーネントにマップすることができます。 以下に例を示します。

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

アダプティブフォームの式言語はJavascriptです。すべての数式は有効なJavaScriptの数式で、アダプティブフォームのスクリプトモデルAPIを使用しています。フォームイベント上の式](adaptive-form-expressions.md)を[評価するために、フォームオブジェクトを事前に設定できます。

aem:afpropertiesプロパティを使用して、アダプティブフォームコンポーネントのアダプティブフォーム式またはスクリプトを事前設定します。 例えば、initializeイベントがトリガされると、次のコードは電話フィールドの値を設定し、ログに値を出力します。

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

フォームオブジェクトのスクリプトまたは式を設定するには、[forms-power-userグループ](forms-groups-privileges-tasks.md)のメンバーである必要があります。 次の表に、アダプティブフォームコンポーネントでサポートされるすべてのスクリプトイベントを示します。

<table>
 <tbody>
  <tr>
   <th><strong></strong>コンポーネント\イベント</th>
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

JSON内でのイベントの使用例としては、初期化イベント時にフィールドを非表示にし、値コミットイベント時に別のフィールドの値を設定する例があります。 スクリプトイベント用の式の作成について詳しくは、「[アダプティブフォーム式](adaptive-form-expressions.md)」を参照してください。

前述の例のサンプルJSONコードを以下に示します。

### initializeイベント{#hiding-a-field-on-initialize-event}でフィールドを非表示にする

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

#### 値コミットイベント{#configure-value-of-another-field-on-value-commit-event}で別のフィールドの値を設定

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

JSONスキーマ要素に次の制限を追加して、アダプティブフォームコンポーネントに許容される値を制限することができます。

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
   <td><p>String</p> </td>
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
     <li>XSDスキーマにマップされているすべてのアダプティブフォームコンポーネント </li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>maxItems</code></td>
   <td>文字列</td>
   <td>配列の最大項目数を指定します。 項目の最大数は 0 以上である必要があります。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>minItems</code></td>
   <td>文字列</td>
   <td>配列内の最小項目数を指定します。 項目の最小数は 0 以上である必要があります。</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## サポート対象外の構成  {#non-supported-constructs}

アダプティブフォームは、次のJSONスキーマ構成をサポートしていません。

* Null タイプ
* any、and などの Union タイプ
* OneOf、AnyOf、AllOf、NOT
* 同種の配列のみがサポートされます。そのため、項目制限は配列でなくオブジェクトに行われる必要があります。

## よくある質問 {#frequently-asked-questions}

**繰り返し可能なサブフォーム（minOccours 値または maxOccurs 値が 1 より大きい）では、サブフォーム（任意の複合型から生成された構造）の個々の要素をドラッグできないのはなぜですか？**

繰り返し可能なサブフォームでは、完全なサブフォームを使用する必要があります。選択した一部のフィールドのみを使用する場合は、構造全体を使用し、不要部分を削除します。

**コンテンツファインダーに長く複雑な構造があります。特定の要素を見つけるにはどうすればよいですか？**

次の 2 つのオプションがあります。

* ツリー構造をスクロールします。
* 「検索」ボックスを使用して、要素を検索します。

**JSONスキーマファイルの拡張子は何ですか。**

JSONスキーマファイルの拡張子は。スキーマ.jsonにする必要があります。 例えば、&lt;filename>.スキーマ.jsonのように指定します。
