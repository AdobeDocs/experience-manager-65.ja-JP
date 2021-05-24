---
title: Query Builder の述語リファレンス
seo-title: Query Builder の述語リファレンス
description: Query Builder API の詳細な述語リファレンスです。
seo-description: Query Builder API の詳細な述語リファレンスです。
uuid: af0e269e-7d52-4032-b22e-801c7b5dccfa
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
discoiquuid: 94a05894-743a-4ace-a292-bfee90ba9068
exl-id: 54b942f9-5dd9-4826-9a0a-028f2d7b8e41
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2323'
ht-degree: 62%

---

# Query Builder の述語リファレンス{#query-builder-predicate-reference}

## 一般 {#general}

* [root](#root)
* [group](#group)
* [orderby](#orderby)

## 述語 {#predicates}

* [boolproperty](/help/sites-developing/querybuilder-predicate-reference.md#boolproperty)
* [contentfragment](/help/sites-developing/querybuilder-predicate-reference.md#contentfragment)
* [dateComparison](/help/sites-developing/querybuilder-predicate-reference.md#datecomparison)
* [daterange](/help/sites-developing/querybuilder-predicate-reference.md#daterange)
* [excludepaths](/help/sites-developing/querybuilder-predicate-reference.md#excludepaths)
* [fulltext](/help/sites-developing/querybuilder-predicate-reference.md#fulltext)
* [hasPermission](/help/sites-developing/querybuilder-predicate-reference.md#haspermission)
* [language](/help/sites-developing/querybuilder-predicate-reference.md#language)
* [mainasset](/help/sites-developing/querybuilder-predicate-reference.md#mainasset)
* [memberOf](/help/sites-developing/querybuilder-predicate-reference.md#memberof)
* [nodename](/help/sites-developing/querybuilder-predicate-reference.md#nodename)
* [notexpired](/help/sites-developing/querybuilder-predicate-reference.md#notexpired)
* [path](/help/sites-developing/querybuilder-predicate-reference.md#path)
* [property](/help/sites-developing/querybuilder-predicate-reference.md#property)
* [rangeproperty](/help/sites-developing/querybuilder-predicate-reference.md#rangeproperty)
* [relativedaterange](/help/sites-developing/querybuilder-predicate-reference.md#relativedaterange)
* [savedquery](/help/sites-developing/querybuilder-predicate-reference.md#savedquery)
* [similar](/help/sites-developing/querybuilder-predicate-reference.md#similar)
* [tag](/help/sites-developing/querybuilder-predicate-reference.md#tag)
* [tagid](/help/sites-developing/querybuilder-predicate-reference.md#tagid)
* [tagsearch](/help/sites-developing/querybuilder-predicate-reference.md#tagsearch)
* [type](/help/sites-developing/querybuilder-predicate-reference.md#type)

### boolproperty {#boolproperty}

JCR BOOLEAN プロパティに一致します。値「`true`」と「`false`」のみを受け入れます。 「`false`」では、プロパティの値が「`false`」の場合または存在しない場合に一致します。有効になっている場合のみ設定されるブール型のフラグをチェックする際に便利です。

継承される「`operation`」パラメーターには意味はありません。

ファセットの抽出に対応しています。`true` または `false` の値ごとにバケットを提供しますが、既存のプロパティに限ります。

#### プロパティ {#properties}

* ****
booleanpropertyプロパティへの相対パス（例： ）。 
`myFeatureEnabled` か `jcr:content/myFeatureEnabled` のどちらかにする必要があります。

* ****
valueプロパティをチェックする値(「 
`true`&quot; または &quot; `false`&quot;

### contentfragment {#contentfragment}

結果をコンテンツフラグメントに限定します。

フィルターには対応していません。

ファセットの抽出には対応していません。

#### プロパティ {#properties-1}

* **contentfragment** 任意の値と併用してコンテンツフラグメントをチェックできます。

### dateComparison {#datecomparison}

2 つの JCR DATE プロパティを比較します。等しい、等しくない、より大きい、以上かどうかをテストできます。

これはフィルターのみの述語で、検索インデックスは利用できません。

#### プロパティ {#properties-2}

* **property1**

   1 つ目の日付プロパティのパス

* **property2**

   2 つ目の日付プロパティのパス

* **operation**

   &quot; `equals`&quot;は完全一致、&quot; `!=`&quot;は不等価比較、&quot; `greater`&quot;はproperty2より大きいプロパティ1、&quot; `>=`&quot;はproperty2以上のプロパティ1を表します。 デフォルト値は「`equals`」です。

### daterange {#daterange}

JCR DATE プロパティと日時の間隔を照合します。ISO8601 形式の日時（`YYYY-MM-DDTHH:mm:ss.SSSZ`）を使用します。`YYYY-MM-DD` などの部分表記も可能です。また、ミリ秒数のタイムスタンプ（UTC タイムゾーン、UNIX 時刻形式、1970 年以降）を指定することもできます。

2 つのタイムスタンプの間や、特定の日付より前または後のものを検索できるほか、両値を含めるか含めないかを選択することもできます。

ファセットの抽出に対応しています。「今日」、「今週」、「今月」、「過去 3 ヶ月」、「今年」、「前年」、「前年より前」のバケットを提供します。

フィルターには対応していません。

#### プロパティ {#properties-3}

* **property**

   `DATE`プロパティの相対パス（例：`jcr:lastModified`）

* **lowerBound**

    プロパティでチェックする日付の下限（`2014-10-01` など）。

* **lowerOperation**

   「 `>` 」（新しい）または「 `>=` 」（以降）は、`lowerBound`に適用されます。 デフォルトは「`>`」です。

* **upperBound**

   プロパティをチェックする上限（例：`2014-10-01T12:15:00`）

* **upperOperation**

   「 `<` 」（古い）または「 `<=` 」（古い）は、`upperBound`に適用されます。 デフォルトは「`<`」です。

* **timeZone**

    ISO-8601 の日付文字列で指定されていない場合に使用するタイムゾーンの ID。デフォルトは、システムのデフォルトのタイムゾーンです。

### excludepaths {#excludepaths}

パスが正規表現に一致するノードを結果から除外します。

これはフィルターのみの述語で、検索インデックスは利用できません。

ファセットの抽出には対応していません。

#### プロパティ {#properties-4}

* **excludepaths**

    結果のパスと照合される正規表現。一致したパスは結果から除外されます。

### fulltext {#fulltext}

フルテキストのインデックスの語句を検索します。

フィルターには対応していません。

ファセットの抽出には対応していません。

#### プロパティ {#properties-5}

* **fulltext**

   全文検索用語

* **relPath**

    プロパティまたはサブノードの検索の相対パス。このプロパティはオプションです。

### グループ {#group}

ネストされた条件を作成できます。グループにはネストされたグループを含めることができます。querybuilder クエリのすべての要素は、暗黙的にルートグループに含まれます。ルートグループでは、`p.or` および `p.not` パラメーターを指定できます。

2 つのプロパティのいずれかを値と照合する例は次のとおりです。

```
group.p.or=true
group.1_property=jcr:title
group.1_property.value=My Page
group.2_property=navTitle
group.2_property.value=My Page
```

これは概念上は `(1_property` OR `2_property)` になります。

ネストされたグループの例は次のとおりです。

```
fulltext=Management
group.p.or=true
group.1_group.path=/content/geometrixx/en
group.1_group.type=cq:Page
group.2_group.path=/content/dam/geometrixx
group.2_group.type=dam:Asset
```

これにより、`/content/geometrixx/en`のページ内または`/content/dam/geometrixx`のアセット内で「**管理**」という用語が検索されます。

これは概念上は `fulltext AND ( (path AND type) OR (path AND type) )` になります。このような OR 結合では、パフォーマンスの観点から適切なインデックスが必要です。

#### プロパティ {#properties-6}

* **p.or**

   「 `true` 」に設定した場合、グループ内の1つの述語のみが一致する必要があります。 デフォルトは「`false`」です。この場合は、すべてが一致する必要があります。

* **p.not**

   「 `true` 」に設定すると、グループを無効にします（デフォルトは「 `false` 」）。

* **&lt;predicate>**

   ネストされた述語を追加します

* **N_&lt;predicate>**

   `1_property, 2_property, ...`のように、ネストされた複数の述語を同時に追加します。

### hasPermission {#haspermission}

指定された [JCR 権限](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)が現在のセッションに含まれる項目に、結果を制限します。

これはフィルターのみの述語で、検索インデックスは利用できません。ファセットの抽出には対応していません。

#### プロパティ {#properties-7}

* **hasPermission**

   現在のユーザーセッションが対象のノードに対してすべて持つ必要がある、コンマ区切りのJCR権限。例： `jcr:write`、`jcr:modifyAccessControl`

### 言語 {#language}

特定の言語の CQ ページを検索します。ページの言語プロパティと、ページパス（一般的に最上位レベルのサイト構造に言語やロケールが含まれています）の両方を検索します。

これはフィルターのみの述語で、検索インデックスは利用できません。

ファセットの抽出に対応しています。固有の言語コードごとにバケットを提供します。

#### プロパティ {#properties-8}

* **language**

   ISO言語コード（例：「 `de` 」）

### mainasset {#mainasset}

ノードがサブアセットではなく、DAM メインアセットであるかどうかをチェックします。基本的には、DAM メインアセットは「subassets」ノード外のすべてのノードです。`dam:Asset` ノードタイプはチェックされません。この述語を使用するには、「 `mainasset=true` 」または「 `mainasset=false` 」を設定します。それ以上のプロパティはありません。

これはフィルターのみの述語で、検索インデックスは利用できません。

ファセットの抽出に対応しています。メインとサブアセットの 2 つのバケットを提供します。

#### プロパティ {#properties-9}

* **mainasset**

   ブール値。メインアセットの場合は「 `true` 」、サブアセットの場合は「 `false` 」

### memberOf {#memberof}

特定の [sling リソースコレクション](https://helpx.adobe.com/jp/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/resource/collection/ResourceCollection.html)のメンバーである項目を検索します。

これはフィルターのみの述語で、検索インデックスは利用できません。ファセットの抽出には対応していません。

#### プロパティ {#properties-10}

* **memberOf**

   Sling リソースコレクションのパス

### ノデナム {#nodename}

JCR ノード名と一致します。

ファセットの抽出に対応しています。固有のノード名（ファイル名）ごとにバケットを提供します。

#### プロパティ {#properties-11}

* **nodename**

   ワイルドカードを使用できるノード名パターン：`*` は 0 個以上の任意の文字、`?` は任意の文字、`[abc]` は角括弧内の文字のみ

### notextired {#notexpired}

JCR DATE プロパティが現在のサーバー時間より後か同じかをチェックすることで項目を照合します。これを使用すると、日付プロパティなどの「`expiresAt`」をチェックし、まだ有効期限が切れていないプロパティ（`notexpired=true`）または既に有効期限が切れているプロパティ（`notexpired=false`）に制限できます。

フィルターには対応していません。

daterange 述語と同じように、ファセットの抽出に対応しています。

#### プロパティ {#properties-12}

* **notexpired**

    ブール値。有効期限が切れていない（日付が現在以降である）場合は「`true`」、有効期限が切れている（日付が過去である）場合は「`false`」です（必須）。

* **プロパティ**

   確認する`DATE`プロパティの相対パス（必須）

### orderby {#orderby}

結果の並べ替えを有効にします。複数のプロパティ別に並べ替える必要がある場合は、`1_orderby=first`、`2_oderby=second` などの数字のプレフィックスを使用して、この述語を複数回追加する必要があります。

#### プロパティ {#properties-13}

* **orderby**

   並べ替えの基準となる、先頭が @ の JCR プロパティ名（例：`@jcr:lastModified`、`@jcr:content/jcr:title`）またはクエリ内の別の述語（例：`2_property`）

* **並べ替え**

   並べ替えの方向。降順の場合は「 `desc` 」、昇順の場合は「 `asc` 」（デフォルト）

* **ケース**

    「`ignore`」に設定すると、並べ替えで大文字と小文字が区別されなくなります（「a」が「B」の前になります）。空白または未指定の場合は、並べ替えで大文字と小文字が区別されます（「B」が「a」の前になります）。

### パス {#path}

特定のパス内を検索します。

ファセットの抽出には対応していません。

#### プロパティ {#properties-14}

* **path**

   パスパターン；厳密に応じて、サブツリー全体が一致します（xpathに`//*`を追加する場合など）。ただし、これはベースパスを含まない(exact=false、default)か、ワイルドカード( `*`)を含む完全なパスの一致のみです。selfが設定されている場合、ベースノードを含むサブツリー全体が検索されます

* **厳密**

   `exact`がtrue/onの場合、パスは完全に一致する必要がありますが、名前に一致する単純なワイルドカード(`*`)を含めることができますが、「`/`」は含めません。false（デフォルト）の場合、すべての子が含まれます（オプション）。

* **平らな**

   直接の子のみを検索します（xpathに「 `/*` 」を付加する場合など）（「 `exact` 」がtrueでない場合にのみ使用されます。オプション）

* **self**

    サブツリーを検索しますが、パスとして指定されたベースノードが含まれます（ワイルドカードは不可）。

### プロパティ {#property}

JCR プロパティとその値に一致します。

ファセットの抽出に対応しています。結果の固有のプロパティ値ごとにバケットを提供します。

#### プロパティ {#properties-15}

* **プロパティ**

   プロパティへの相対パス（例：`jcr:title`）

* **value**

   プロパティでチェックする値。JCR プロパティタイプから文字列への変換に従います

* **N_value**

   `1_value`、`2_value`、...を使用して、複数の値をチェックします（デフォルトで`OR`と組み合わされ、and=trueの場合は`AND`と組み合わされます）（5.3以降）。

* **および**

   複数の値(`N_value`)とANDを組み合わせる場合は、trueに設定します（5.3以降）。

* **操作**

   &quot;`equals`&quot;は完全一致（デフォルト）、&quot; `unequals`&quot;は不等価比較、&quot; `like`&quot;は`jcr:like` xpath関数（オプション）を使用し、&quot; `not`&quot;は一致しない(例： xpathの「`not(@prop)`」、値パラメーターは無視されます)、または「`exists`」（値はtrue、プロパティは存在する必要があり、デフォルトはfalse、「`not`」と同じ）

* **深さ**

   プロパティ/相対パスが存在できるワイルドカードレベルの数（例えば、`property=size depth=2`は、node/size、node/amp;ast;/sizeおよびnode/&amp;ast;/&amp;ast;ast;/amp;ast;/size）をチェックします。

### rangeproperty {#rangeproperty}

JCR プロパティと間隔を照合します。`LONG`、`DOUBLE`、`DECIMAL` などの線形タイプのプロパティに適用されます。`DATE` に関しては、最適化された日付形式の入力情報を含む daterange 述語を参照してください。

下限と上限、またはそのいずれかを定義できます。演算（「より少ない」や「以下」など）も、下限と上限に別々に指定することができます。

ファセットの抽出には対応していません。

#### プロパティ {#properties-16}

* **プロパティ**

   プロパティの相対パス

* **lowerBound**

   プロパティをチェックする下限

* **lowerOperation**

   &quot; `>`&quot; （デフォルト）または&quot; `>=`&quot; （`lowerValue`に適用）

* **upperBound**

   プロパティをチェックする上限

* **upperOperation**

   &quot; `<`&quot; （デフォルト）または&quot; `<=`&quot; （`lowerValue`に適用）

* **decimal**

   チェックされたプロパティのタイプがDecimalの場合は&quot; `true`&quot;

### relativedaterange {#relativedaterange}

`JCR DATE` プロパティと日時の間隔を照合します（現在のサーバー時間に対する時間オフセットを使用します）。`lowerBound`と`upperBound`は、ミリ秒値またはbugzilla構文`1s 2m 3h 4d 5w 6M 7y`（1秒、2分、3時間、4日、5週間、6ヶ月、7年）を使用して指定できます。 現在の時刻より前の負のオフセットを示す「`-`」というプレフィックス。 `lowerBound` または `upperBound` のいずれかのみを指定する場合は、他方がデフォルトで 0（現在の時間）になります。

次に例を示します。

* `upperBound=1h` (そしてい `lowerBound`いえ)次の1時間には何も選択しません
* `lowerBound=-1d` (およびいいえ `upperBound`)過去24時間以内に選択された項目は何でもかまいません
* `lowerBound=-6M` そして `upperBound=-3M` 生後6ヶ月から3ヶ月の何かを選ぶ
* `lowerBound=-1500` 過去 `upperBound=5500` の1500ミリ秒から将来の5500ミリ秒の間のものを選択します。
* `lowerBound=1d` 明後 `upperBound=2d` 日何かを選ぶだろう

うるう年は考慮されず、すべての月が 30 日になる点にご注意ください。

フィルターには対応していません。

daterange 述語と同じように、ファセットの抽出に対応しています。

#### プロパティ {#properties-17}

* **upperBound**

   現在のサーバー時間の上限（ミリ秒、2分、3時間、4日、5週間、6か月、7年）をミリ秒単位または`1s 2m 3h 4d 5w 6M 7y`（1秒、2分、3時間、4日、5週間、6ヶ月、7年）で、負のオフセットは「 — 」を使用します。

* **lowerBound**

   現在のサーバー時間の下限（ミリ秒、2分、3時間、4日、5週間、6ヶ月、7年）を示す日付（ミリ秒）または`1s 2m 3h 4d 5w 6M 7y`（1秒、2分、3時間、4日、5週、6ヶ月、7年）。負のオフセットは「 — 」を使用します

### root {#root}

ルート述語グループ。グループのすべての機能に対応し、グローバルクエリパラメーターを設定できます。

「root」という名前は暗黙的で、クエリでは使用されません。

#### プロパティ {#properties-18}

* **p.offset**

    結果ページの開始を表す数値（スキップする項目数）。

* **p.limit**

   ページのサイズを表す数値

* **p.guessTotal**

   推奨：コストのかかる結果の全体を計算しないようにします。カウントする最大合計を示す数値（例えば、1000、小さい結果を得るのに十分な大きさと正確な数をユーザーに提供する数）または「`true`」で、最小限必要な`p.offset` + `p.limit`までカウントします。

* **p.excerpt**

   「 `true` 」に設定した場合は、完全なテキストの抜粋を結果に含めます

* **p.hits**

    （JSON サーブレット専用）ヒットを JSON として記述する方法を、次の標準的なものの中から選択します（ResultHitWriter サービスを使用して拡張可能）。

   * **シンプル**:

      `path`、`title`、`lastmodified`、`excerpt`（設定されている場合）など、最小の項目

   * **full**:

      ノードのsling JSONレンダリング（`jcr:path`はヒットのパスを示します）。デフォルトでは、ノードの直接のプロパティのリストのみが表示され、`p.nodedepth=N`で深いツリーを含めます。0は無限のサブツリー全体を意味します。`p.acls=true`を追加して、指定された結果項目に対する現在のセッションのJCR権限を含めます(マッピング：`create` = `add_node`、`modify` = `set_property`、`delete` = `remove`)

   * **選択的**:

      `p.properties`で指定されたプロパティのみ。相対パスのリストをスペースで区切ります（URLでは「+」を使用）。相対パスの深さが1を超える場合は、子オブジェクトとして表されます。特別なjcr:pathプロパティには、ヒットのパスが含まれます。

### savedquery {#savedquery}

永続的な querybuilder クエリのすべての述語を、サブグループの述語として現在のクエリに含めます。

これによって追加のクエリが実行されるわけではなく、現在のクエリが拡張されます。

クエリは `QueryBuilder#storeQuery()` を使用してプログラムで永続化できます。形式は、複数行の String プロパティか、Java プロパティ形式のテキストファイルとしてクエリを含む `nt:file` ノードにできます。

保存済みクエリの述語のファセット抽出には対応していません。

#### プロパティ {#properties-19}

* **savedquery**

   保存されたクエリのパス（Stringプロパティまたは`nt:file`ノード）

### 類似 {#similar}

JCR XPathの`rep:similar()`を使用した類似性検索。

フィルターには対応していません。ファセットの抽出には対応していません。

#### プロパティ {#properties-20}

* **similar** 類似ノードを検索するノードの絶対パス。

* **local** 下位ノードの相対パス、または現在のノードの場合は 
`.` 現在のノード(オプション、デフォルトは「  `.`」)

### タグ {#tag}

タグタイトルのパスを指定して、タグが付けられているコンテンツを検索します。

ファセットの抽出に対応しています。現在のタグタイトルのパスを使用して固有のタグごとにバケットを提供します。

#### プロパティ {#properties-21}

* **tag**

    検索するタグタイトルのパス（「Asset Properties : Orientation / Landscape」など）。

* **N_value**

   `1_value`、`2_value`、...を使用して、複数のタグ（デフォルトでは`OR`と組み合わされ、and=trueの場合は`AND`と組み合わされている）をチェックします（5.6以降）。

* **プロパティ**

   参照するプロパティ（またはプロパティの相対パス）（デフォルトは「`cq:tags`」）

### tagid {#tagid}

タグ ID を指定して、タグが付けられているコンテンツを検索します。

ファセットの抽出に対応しています。現在のタグ ID を使用して固有のタグごとにバケットを提供します。

#### プロパティ {#properties-22}

* **tagid**

   探すタグID（例：「 `properties:orientation/landscape` 」）。

* **N_value**

   `1_value`、`2_value`、...を使用して、複数のタグidをチェックします（デフォルトで`OR`と組み合わされ、and=trueの場合は`AND`と組み合わされます）（5.6以降）。

* **プロパティ**

   参照するプロパティ（またはプロパティの相対パス）（デフォルトは「`cq:tags`」）

### tagsearch {#tagsearch}

キーワードを指定して、タグが付けられているコンテンツを検索します。最初にタイトル内に対象のキーワードを含むタグを検索してから、それらのタグが付いている項目のみに結果を制限します。

ファセットの抽出には対応していません。

#### プロパティ {#Properties-1}

* **tagsearch**

   タグタイトル内で検索するキーワード

* **プロパティ**

   参照するプロパティ（またはプロパティの相対パス）（デフォルトは「`cq:tags`」）

* **lang**

   特定のローカライズされたタグタイトルのみを検索する場合(例：&quot; `de`&quot;)

* **all**

    （ブール値）タグのフルテキスト全体（すべてのタイトル、説明など）を検索します（「l `ang`」よりも優先）

### type {#type}

特定の JCR ノードのタイプ（プライマリノードタイプまたは Mixin タイプ）に結果を制限します。そのノードタイプのサブタイプも検索します。リポジトリーの検索インデックスでは、効率的に実行できるノードタイプに対応する必要があります。

ファセットの抽出に対応しています。結果の固有のタイプごとにバケットを提供します。

#### プロパティ {#Properties-2}

* **type**

   検索するノードタイプまたはmixin名（例：`cq:Page`）
