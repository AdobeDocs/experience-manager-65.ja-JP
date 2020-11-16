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
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379
workflow-type: tm+mt
source-wordcount: '2323'
ht-degree: 56%

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

JCR BOOLEAN プロパティに一致します。Only accepts the values &quot; `true`&quot; and &quot; `false`&quot;. 「`false`」では、プロパティの値が「`false`」の場合または存在しない場合に一致します。有効になっている場合のみ設定されるブール型のフラグをチェックする際に便利です。

継承される「`operation`」パラメーターには意味はありません。

ファセットの抽出に対応しています。`true` または `false` の値ごとにバケットを提供しますが、既存のプロパティに限ります。

#### プロパティ {#properties}

* **booleanproperty**&#x200B;プロパティの相対パス(例： 
`myFeatureEnabled` か `jcr:content/myFeatureEnabled` のどちらかにする必要があります。

* **プロパティをチェックする値**&quot; 
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

   最初の日付プロパティへのパス

* **property2**

   2番目の日付プロパティへのパス

* **operation**

   &quot; `=`&quot; for exact match, &quot; `!=`&quot; for unequality comparison, &quot; `>`&quot; for property1 greater than property2, &quot; `>=`&quot; for property1 greater than or equal to property2. The default value is &quot; `=`&quot;.

### daterange {#daterange}

JCR DATE プロパティと日時の間隔を照合します。This uses the ISO8601
format for dates and times ( `YYYY-MM-DDTHH:mm:ss.SSSZ`) and allows also partial representations, like `YYYY-MM-DD`. また、ミリ秒数のタイムスタンプ（UTC タイムゾーン、UNIX 時刻形式、1970 年以降）を指定することもできます。

2 つのタイムスタンプの間や、特定の日付より前または後のものを検索できるほか、両値を含めるか含めないかを選択することもできます。

ファセットの抽出に対応しています。「今日」、「今週」、「今月」、「過去 3 ヶ月」、「今年」、「前年」、「前年より前」のバケットを提供します。

フィルターには対応していません。

#### プロパティ {#properties-3}

* **property**

   relative path to a `DATE` property, for example `jcr:lastModified`

* **lowerBound**

   lower date bound to check property for, for example `2014-10-01`

* **lowerOperation**

   &quot; `>`&quot; (newer) or &quot; `>=`&quot; (at or newer), applies to the `lowerBound`. The default is &quot; `>`&quot;.

* **upperBound**

   upper bound to check property for, for example `2014-10-01T12:15:00`

* **upperOperation**

   &quot; `<`&quot; (older) or &quot; `<=`&quot; (at or older), applies to the `upperBound`. The default is &quot; `<`&quot;.

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

### group {#group}

ネストされた条件を作成できます。グループにはネストされたグループを含めることができます。querybuilder クエリのすべての要素は、暗黙的にルートグループに含まれます。ルートグループでは、`p.or` および `p.not` パラメーターを指定できます。

2 つのプロパティのいずれかを値と照合する例は次のとおりです。

```
group.p.or=true
group.1_property=jcr:title
group.1_property.value=My Page
group.2_property=navTitle
group.2_property.value=My Page
```

This is conceptually `(1_property` OR `2_property)`.

ネストされたグループの例は次のとおりです。

```
fulltext=Management
group.p.or=true
group.1_group.path=/content/geometrixx/en
group.1_group.type=cq:Page
group.2_group.path=/content/dam/geometrixx
group.2_group.type=dam:Asset
```

This searches for the term &quot;**Management**&quot; within pages in `/content/geometrixx/en` or in assets in `/content/dam/geometrixx`.

これは概念的には `fulltext AND ( (path AND type) OR (path AND type) )`。 このような OR 結合では、パフォーマンスの観点から適切なインデックスが必要です。

#### プロパティ {#properties-6}

* **p.or**

   if set to &quot; `true`&quot;, only one predicate in the group must match. デフォルトは「`false`」です。この場合は、すべてが一致する必要があります。

* **p.not**

   if set to &quot; `true`&quot;, it negates the group (defaults to &quot; `false`&quot;)

* **&lt;predicate>**

   入れ子の述語を追加します。

* **N_&lt;predicate>**

   adds multiple nested predicates of the same time, like `1_property, 2_property, ...`

### hasPermission {#haspermission}

指定された [JCR 権限](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)が現在のセッションに含まれる項目に、結果を制限します。

これはフィルターのみの述語で、検索インデックスは利用できません。ファセットの抽出には対応していません。

#### プロパティ {#properties-7}

* **hasPermission**

   comma-separated JCR privileges that the current user session must ALL have for the node in question; for example `jcr:write`, `jcr:modifyAccessControl`

### language {#language}

特定の言語の CQ ページを検索します。ページの言語プロパティと、ページパス（一般的に最上位レベルのサイト構造に言語やロケールが含まれています）の両方を検索します。

これはフィルターのみの述語で、検索インデックスは利用できません。

ファセットの抽出に対応しています。固有の言語コードごとにバケットを提供します。

#### プロパティ {#properties-8}

* **language**

   ISO language code, for example &quot; `de`&quot;

### mainasset {#mainasset}

ノードがサブアセットではなく、DAM メインアセットであるかどうかをチェックします。基本的には、DAM メインアセットは「subassets」ノード外のすべてのノードです。`dam:Asset` ノードタイプはチェックされません。To use this predicate, simply set &quot; `mainasset=true`&quot; or &quot; `mainasset=false`&quot;, there are no further properties.

これはフィルターのみの述語で、検索インデックスは利用できません。

ファセットの抽出に対応しています。メインとサブアセットの 2 つのバケットを提供します。

#### プロパティ {#properties-9}

* **mainasset**

   boolean, &quot; `true`&quot; for main assets, &quot; `false`&quot; for sub assets

### memberOf {#memberof}

特定の [sling リソースコレクション](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/resource/collection/ResourceCollection.html)のメンバーである項目を検索します。

これはフィルターのみの述語で、検索インデックスは利用できません。ファセットの抽出には対応していません。

#### プロパティ {#properties-10}

* **memberOf**

   Slingリソースコレクションのパス

### nodename {#nodename}

JCR ノード名と一致します。

ファセットの抽出に対応しています。固有のノード名（ファイル名）ごとにバケットを提供します。

#### プロパティ {#properties-11}

* **nodename**

   ワイルドカードを使用できるノード名パターン： `*` =任意または文字なし= `?` 任意の文字、 `[abc]` =角括弧内の文字のみ

### notexpired {#notexpired}

JCR DATE プロパティが現在のサーバー時間より後か同じかをチェックすることで項目を照合します。これを使用すると、日付プロパティなどの「`expiresAt`」をチェックし、まだ有効期限が切れていないプロパティ（`notexpired=true`）または既に有効期限が切れているプロパティ（`notexpired=false`）に制限できます。

フィルターには対応していません。

daterange 述語と同じように、ファセットの抽出に対応しています。

#### プロパティ {#properties-12}

* **notexpired**

    ブール値。有効期限が切れていない（日付が現在以降である）場合は「`true`」、有効期限が切れている（日付が過去である）場合は「`false`」です（必須）。

* **property**

   relative path to the `DATE` property to check (required)

### orderby {#orderby}

結果の並べ替えを有効にします。If ordering by multiple properties is required, this predicate needs to be added multiple times using the number prefix, such as `1_orderby=first`, `2_oderby=second`.

#### プロパティ {#properties-13}

* **orderby**

   either JCR property name indicated by a leading @, for example `@jcr:lastModified` or `@jcr:content/jcr:title`, or another predicate in the query, for example `2_property`, on which to sort

* **並べ替え**

   sort direction, either &quot; `desc`&quot; for descending or &quot; `asc`&quot; for ascending (default)

* **症例**

    「`ignore`」に設定すると、並べ替えで大文字と小文字が区別されなくなります（「a」が「B」の前になります）。空白または未指定の場合は、並べ替えで大文字と小文字が区別されます（「B」が「a」の前になります）。

### パス {#path}

特定のパス内を検索します。

ファセットの抽出には対応していません。

#### プロパティ {#properties-14}

* **path**

   path pattern; depending on exact, either the entire subtree will match (like appending `//*` in xpath, but note that this does not include the base path) (exact=false, default) or only an exact path matches, which can include wildcards ( `*`); if self is set, the entire subtree including the base node will be searched

* **完全一致**

   if `exact` is true/on, the exact path must match, but it can contain simple wildcards ( `*`), that match names, but not &quot; `/`&quot;; if it is false (default) all descendents are included (optional)

* **平らな**

   searches only the direct children (like appending &quot; `/*`&quot; in xpath) (only used if &#39; `exact`&#39; is not true, optional)

* **self**

    サブツリーを検索しますが、パスとして指定されたベースノードが含まれます（ワイルドカードは不可）。

### property {#property}

JCR プロパティとその値に一致します。

ファセットの抽出に対応しています。結果の固有のプロパティ値ごとにバケットを提供します。

#### プロパティ {#properties-15}

* **property**

   relative path to property, for example `jcr:title`

* **value**

    プロパティでチェックする値。JCR プロパティのタイプから文字列への変換に従います。

* **N_value**

   use `1_value`, `2_value`, ... to check for multiple values (combined with `OR` by default, with `AND` if and=true) (since 5.3)

* **および**

   set to true for combining multiple values ( `N_value`) with AND (since 5.3)

* **operation**

   &quot; `equals`&quot; for exact match (default), &quot; `unequals`&quot; for unequality comparison, &quot; `like`&quot; for using the `jcr:like` xpath function (optional), &quot; `not`&quot; for no match (eg. &quot; `not(@prop)`&quot; in xpath, value param will be ignored) or &quot; `exists`&quot; for existence check (value can be true - property must exist, the default - or false - same as &quot; `not`&quot;)

* **深さ**

   プロパティ/相対パスが存在できるワイルドカードレベルの数（例えば、node/size、node/&amp;ast;/size、node/&amp;ast;/&amp;ast;/&amp;ast;/size） `property=size depth=2`

### rangeproperty {#rangeproperty}

JCR プロパティと間隔を照合します。This applies to properties with linear types such as `LONG`, `DOUBLE` and `DECIMAL`. `DATE` に関しては、最適化された日付形式の入力情報を含む daterange 述語を参照してください。

下限と上限、またはそのいずれかを定義できます。演算（「より少ない」や「以下」など）も、下限と上限に別々に指定することができます。

ファセットの抽出には対応していません。

#### プロパティ {#properties-16}

* **property**

   プロパティの相対パス

* **lowerBound**

   ～の特性をチェックする下限

* **lowerOperation**

   &quot; `>`&quot; (default) or &quot; `>=`&quot;, applies to the `lowerValue`

* **upperBound**

   プロパティをチェックする上限

* **upperOperation**

   &quot; `<`&quot; (default) or &quot; `<=`&quot;, applies to the `lowerValue`

* **decimal**

   &quot; `true`&quot; if the checked property is of type Decimal

### relativedaterange {#relativedaterange}

`JCR DATE` プロパティと日時の間隔を照合します（現在のサーバー時間に対する時間オフセットを使用します）。You can specify `lowerBound` and `upperBound` using either a millisecond value or the bugzilla syntax `1s 2m 3h 4d 5w 6M 7y` (one second, two minutes, three hours, four days, five weeks, six months, seven years). Prefix with &quot; `-`&quot; to indicate a negative offset before the current time. `lowerBound` または `upperBound` のいずれかのみを指定する場合は、他方がデフォルトで 0（現在の時間）になります。

次に例を示します。

* `upperBound=1h` (そして `lowerBound`)次の時間には何でも選ぶ
* `lowerBound=-1d` (そして `upperBound`)過去24時間の間に何でも選択する
* `lowerBound=-6M` そして、生後6ヶ月から3ヶ月の何 `upperBound=-3M` かを選ぶ
* `lowerBound=-1500` 過去 `upperBound=5500` の1500ミリ秒から将来の5500ミリ秒の間であれば何でも選択します
* `lowerBound=1d` 明後日 `upperBound=2d` に何でも選ぶ

うるう年は考慮されず、すべての月が 30 日になる点にご注意ください。

フィルターには対応していません。

daterange 述語と同じように、ファセットの抽出に対応しています。

#### プロパティ {#properties-17}

* **upperBound**

   upper date bound in milliseconds or `1s 2m 3h 4d 5w 6M 7y` (one second, two minutes, three hours, four days, five weeks, six months, seven years) relative to current server time, use &quot;-&quot; for negative offset

* **lowerBound**

   lower date bound in milliseconds or `1s 2m 3h 4d 5w 6M 7y` (one second, two minutes, three hours, four days, five weeks, six months, seven years) relative to current server time, use &quot;-&quot; for negative offset

### root {#root}

ルート述語グループ。グループのすべての機能に対応し、グローバルクエリパラメーターを設定できます。

「root」という名前は暗黙的で、クエリでは使用されません。

#### プロパティ {#properties-18}

* **p.offset**

    結果ページの開始を表す数値（スキップする項目数）。

* **p.limit**

   ページサイズを示す数値

* **p.guessTotal**

   recommended: avoid calculating the full result total which can be costly; either a number indicating the maximum total to count up to (for example 1000, a number that gives users enough feedback on the rough size and exact numbers for smaller results) or &quot; `true`&quot; to count only up to the minimum necessary `p.offset` + `p.limit`

* **p.excerpt**

   if set to &quot; `true`&quot;, include full text excerpt in the result

* **p.hits**

    （JSON サーブレット専用）ヒットを JSON として記述する方法を、次の標準的なものの中から選択します（ResultHitWriter サービスを使用して拡張可能）。

   * **シンプル**:

      、 `path`、、、などの最小項目 `title``lastmodified``excerpt` （設定されている場合）

   * **full**:

      sling JSON rendering of the node, with `jcr:path` indicating the path of the hit: by default just lists the direct properties of the node, include a deeper tree with `p.nodedepth=N`, with 0 meaning the entire, infinite subtree; add `p.acls=true` to include the JCR permissions of the current session on the given result item (mappings: `create` = `add_node`, `modify` = `set_property`, `delete` = `remove`)

   * **選択的**:

      only properties specified in `p.properties`, which is a space separated (use &quot;+&quot; in URLs) list of relative paths; if the relative path has a depth > 1 these will be represented as child objects; the special jcr:path property includes the path of the hit

### savedquery {#savedquery}

永続的な querybuilder クエリのすべての述語を、サブグループの述語として現在のクエリに含めます。

これによって追加のクエリが実行されることはありませんが、現在のクエリが拡張されます。

Queries can be persisted programmatically using `QueryBuilder#storeQuery()`. 形式は、複数行の String プロパティか、Java プロパティ形式のテキストファイルとしてクエリを含む `nt:file` ノードにできます。

保存済みクエリの述語のファセット抽出には対応していません。

#### プロパティ {#properties-19}

* **savedquery**

   path to the saved query (String property or `nt:file` node)

### similar {#similar}

Similarity search using JCR XPath&#39;s `rep:similar()`.

フィルターには対応していません。ファセットの抽出には対応していません。

#### プロパティ {#properties-20}

* **similar** 類似ノードを検索するノードの絶対パス。

* **local** 下位ノードの相対パス、または現在のノードの場合は 
`.` 現在のノード(オプション、デフォルトは「 `.`」)

### tag {#tag}

タグタイトルのパスを指定して、タグが付けられているコンテンツを検索します。

ファセットの抽出に対応しています。現在のタグタイトルのパスを使用して固有のタグごとにバケットを提供します。

#### プロパティ {#properties-21}

* **tag**

    検索するタグタイトルのパス（「Asset Properties : Orientation / Landscape」など）。

* **N_value**

   use `1_value`, `2_value`, ... to check for multiple tags (combined with `OR` by default, with `AND` if and=true) (since 5.6)

* **property**

   property (or relative path to property) to look at (default &quot; `cq:tags`&quot;)

### tagid {#tagid}

タグ ID を指定して、タグが付けられているコンテンツを検索します。

ファセットの抽出に対応しています。現在のタグ ID を使用して固有のタグごとにバケットを提供します。

#### プロパティ {#properties-22}

* **tagid**

   tag id to look for, for example &quot; `properties:orientation/landscape`&quot;

* **N_value**

   use `1_value`, `2_value`, ... to check for multiple tagids (combined with `OR` by default, with `AND` if and=true) (since 5.6)

* **property**

   property (or relative path to property) to look at (default &quot; `cq:tags`&quot;)

### tagsearch {#tagsearch}

キーワードを指定して、タグが付けられているコンテンツを検索します。最初にタイトル内に対象のキーワードを含むタグを検索してから、それらのタグが付いている項目のみに結果を制限します。

ファセットの抽出には対応していません。

#### プロパティ {#Properties-1}

* **tagsearch**

    タグタイトル内で検索するキーワード。

* **property**

   property (or relative path to property) to look at (default &quot; `cq:tags`&quot;)

* **lang**

   to search in a certain localized tag title only (e.g. &quot; `de`&quot;)

* **all**

    （ブール値）タグのフルテキスト全体（すべてのタイトル、説明など）を検索します(takes precedence over &quot;l `ang`&quot;)

### type {#type}

特定の JCR ノードのタイプ（プライマリノードタイプまたは Mixin タイプ）に結果を制限します。そのノードタイプのサブタイプも検索します。リポジトリの検索インデックスでは、効率的に実行できるノードタイプに対応する必要があります。

ファセットの抽出に対応しています。結果の固有のタイプごとにバケットを提供します。

#### プロパティ {#Properties-2}

* **type**

   node type or mixin name to search for, for example `cq:Page`