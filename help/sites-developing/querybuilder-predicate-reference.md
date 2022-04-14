---
title: Query Builder の述語リファレンス
seo-title: Query Builder Predicate Reference
description: Query Builder API の詳細な述語リファレンスです。
seo-description: Complete predicate reference for the Query Builder API.
uuid: af0e269e-7d52-4032-b22e-801c7b5dccfa
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
discoiquuid: 94a05894-743a-4ace-a292-bfee90ba9068
exl-id: 54b942f9-5dd9-4826-9a0a-028f2d7b8e41
source-git-commit: 2bae11eafb875f01602c39c0dba00a888e11391a
workflow-type: ht
source-wordcount: '2310'
ht-degree: 100%

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

JCR BOOLEAN プロパティに一致します。受け入れられる値は「`true`」と「`false`」のみです。`false` の場合、プロパティの値が `false` であるか、値がないときに該当します。有効なときだけ設定されるブール型のフラグをチェックする際に便利です。

継承される「`operation`」パラメーターには意味はありません。

ファセットの抽出に対応しています。`true` または `false` の値ごとにバケットを提供しますが、既存のプロパティに限ります。

#### プロパティ {#properties}

* **boolproperty**
プロパティへの相対パス。例： 
`myFeatureEnabled` または `jcr:content/myFeatureEnabled`

* **value**
次のプロパティをチェックするための値 
「`true`」または「`false`」に対して検査する値

### contentfragment {#contentfragment}

結果をコンテンツフラグメントに限定します。

フィルターには対応していません。

ファセットの抽出には対応していません。

#### プロパティ {#properties-1}

* **contentfragment** 
任意の値と併用してコンテンツフラグメントをチェックできます。

### dateComparison {#datecomparison}

2 つの JCR DATE プロパティを比較します。等しい、等しくない、より大きい、以上かどうかをテストできます。

これはフィルターのみの述語で、検索インデックスは利用できません。

#### プロパティ {#properties-2}

* **property1**

   1 つ目の日付プロパティのパス

* **property2**

   2 つ目の日付プロパティのパス

* **operation**

   完全一致の場合は「`equals`」、不等号比較の場合は「`!=`」、プロパティ 1 がプロパティ 2 より大きい場合は「`greater`」、プロパティ 1 がプロパティ 2 以上の場合は「`>=`」となります。デフォルト値は「`equals`」です。

### daterange {#daterange}

JCR DATE プロパティと日時の間隔を照合します。ISO8601 形式の日時（`YYYY-MM-DDTHH:mm:ss.SSSZ`）を使用します。`YYYY-MM-DD` などの部分表記も可能です。また、ミリ秒数のタイムスタンプ（UTC タイムゾーン、UNIX 時刻形式、1970 年以降）を指定することもできます。

2 つのタイムスタンプの間や、特定の日付より前または後のものを検索できるほか、両値を含めるか含めないかを選択することもできます。

ファセットの抽出に対応しています。「今日」、「今週」、「今月」、「過去 3 ヶ月」、「今年」、「前年」、「前年より前」のバケットを提供します。

フィルターには対応していません。

#### プロパティ {#properties-3}

* **property**

   `DATE` プロパティの相対パス（例：`jcr:lastModified`）

* **lowerBound**

    プロパティでチェックする日付の下限（`2014-10-01` など）。

* **lowerOperation**

   「`>`」（より後）または 「`>=`」（以降）が `lowerBound` に適用されます。デフォルトは「`>`」です。

* **upperBound**

   プロパティでチェックする日付の上限（例：`2014-10-01T12:15:00`）

* **upperOperation**

   「`<`」（より前）または 「`<=`」（以前）が `upperBound` に適用されます。デフォルトは「`<`」です。

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

   フルテキストの検索語句

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

この例では、`/content/geometrixx/en` のページ内または `/content/dam/geometrixx` のアセット内で「**管理**」という語句を検索します。

これは概念上は `fulltext AND ( (path AND type) OR (path AND type) )` になります。このような OR 結合では、パフォーマンスの観点から適切なインデックスが必要です。

#### プロパティ {#properties-6}

* **p.or**

   「`true`」に設定した場合は、一致する必要があるのはグループ内の 1 つの述語のみになります。デフォルトは「`false`」です。この場合は、すべてが一致する必要があります。

* **p.not**

   「`true`」に設定されている場合は、グループを否定します（デフォルトは「`false`」）

* **&lt;predicate>**

   ネストされた述語を追加します

* **N_&lt;predicate>**

   `1_property, 2_property, ...` など、同じ時刻の複数のネストされた述語をまとめて追加します。

### hasPermission {#haspermission}

指定された [JCR 権限](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)が現在のセッションに含まれる項目に、結果を制限します。

これはフィルターのみの述語で、検索インデックスは利用できません。ファセットの抽出には対応していません。

#### プロパティ {#properties-7}

* **hasPermission**

   該当のノードに対して現在のユーザーセッションがすべて持っている必要がある JCR 権限のコンマ区切りリスト（例：`jcr:write`、`jcr:modifyAccessControl`）

### language {#language}

特定の言語の CQ ページを検索します。ページの言語プロパティと、ページパス（一般的に最上位レベルのサイト構造に言語やロケールが含まれています）の両方を検索します。

これはフィルターのみの述語で、検索インデックスは利用できません。

ファセットの抽出に対応しています。固有の言語コードごとにバケットを提供します。

#### プロパティ {#properties-8}

* **language**

   ISO 言語コード（例：「`de`」）

### mainasset {#mainasset}

ノードがサブアセットではなく、DAM メインアセットであるかどうかをチェックします。基本的には、DAM メインアセットは「subassets」ノード外のすべてのノードです。`dam:Asset` ノードタイプはチェックされません。この述語を使用するには、「`mainasset=true`」または「`mainasset=false`」を設定します。それ以外のプロパティはありません。

これはフィルターのみの述語で、検索インデックスは利用できません。

ファセットの抽出に対応しています。メインとサブアセットの 2 つのバケットを提供します。

#### プロパティ {#properties-9}

* **mainasset**

   ブール値。メインアセットの場合は「`true`」、サブアセットの場合は「`false`」です

### memberOf {#memberof}

特定の [sling リソースコレクション](https://helpx.adobe.com/jp/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/resource/collection/ResourceCollection.html)のメンバーである項目を検索します。

これはフィルターのみの述語で、検索インデックスは利用できません。ファセットの抽出には対応していません。

#### プロパティ {#properties-10}

* **memberOf**

   Sling リソースコレクションのパス

### nodename {#nodename}

JCR ノード名と一致します。

ファセットの抽出に対応しています。固有のノード名（ファイル名）ごとにバケットを提供します。

#### プロパティ {#properties-11}

* **nodename**

   ワイルドカードを使用できるノード名パターン：`*` は 0 個以上の任意の文字、`?` は任意の文字、`[abc]` は角括弧内の文字のみ

### notexpired {#notexpired}

JCR DATE プロパティが現在のサーバー時間より後か同じかをチェックすることで項目を照合します。これを使用すると、日付プロパティなどの「`expiresAt`」をチェックし、まだ有効期限が切れていないプロパティ（`notexpired=true`）または既に有効期限が切れているプロパティ（`notexpired=false`）に制限できます。

フィルターには対応していません。

daterange 述語と同じように、ファセットの抽出に対応しています。

#### プロパティ {#properties-12}

* **notexpired**

    ブール値。有効期限が切れていない（日付が現在以降である）場合は「`true`」、有効期限が切れている（日付が過去である）場合は「`false`」です（必須）。

* **property**

   チェックする `DATE` プロパティの相対パス（必須）

### orderby {#orderby}

結果の並べ替えを有効にします。複数のプロパティ別に並べ替える必要がある場合は、`1_orderby=first`、`2_oderby=second` などの数字のプレフィックスを使用して、この述語を複数回追加する必要があります。

#### プロパティ {#properties-13}

* **orderby**

   並べ替えの基準となる、先頭が @ の JCR プロパティ名（例：`@jcr:lastModified`、`@jcr:content/jcr:title`）またはクエリ内の別の述語（例：`2_property`）

* **並べ替え**

   並べ替えの方向。降順の場合は「`desc`」、昇順の場合は「`asc`」（デフォルト）です

* **case**

    「`ignore`」に設定すると、並べ替えで大文字と小文字が区別されなくなります（「a」が「B」の前になります）。空白または未指定の場合は、並べ替えで大文字と小文字が区別されます（「B」が「a」の前になります）。

### path {#path}

特定のパス内を検索します。

ファセットの抽出には対応していません。

#### プロパティ {#properties-14}

* **path**

    パスのパターン。exact に応じて、サブツリー全体が一致するか（xpath で `//*` を追加した場合と同様です。ただし、ベースパスは含まれません。デフォルトの exact=false の場合）、正確なパスのみが一致します（ワイルドカード `*` を使用できます）。self が設定されている場合は、ベースノードを含むサブツリー全体が検索されます。

* **exact**

   `exact` が true または on の場合は、正確なパスが一致する必要があります。ただし、名前に一致する簡単なワイルドカード（`*`）を含めることもできます（「`/`」は不可）。false（デフォルト）の場合は、すべての下位要素が含まれます（オプション）。

* **flat**

    直属の子要素（xpath で「`/*`」を追加した場合と同様です）のみを検索します（『`exact`』が true ではない場合のみ使用されます。オプション）。

* **self**

    サブツリーを検索しますが、パスとして指定されたベースノードが含まれます（ワイルドカードは不可）。

### property {#property}

JCR プロパティとその値に一致します。

ファセットの抽出に対応しています。結果に含まれる固有のプロパティ値ごとにバケットを提供します。

#### プロパティ {#properties-15}

* **property**

   プロパティの相対パス（例：`jcr:title`）

* **value**

   プロパティでチェックする値。JCR プロパティタイプから文字列への変換に従います

* **N_value**

   `1_value`や`2_value`などを使用し、複数の値をチェックします。（デフォルトでは `OR` と結合され、and=true の場合は `AND` と結合されます）（5.3 以降）

* **および**

    複数の値（`N_value`）を AND で結合する場合は、true に設定します（5.3 以降）

* **operation**

   完全一致の場合は「`equals`」（デフォルト）、不等比較の場合は「`unequals`」、`jcr:like` xpath 関数を使用する場合は「`like`」（オプション）、一致なしの場合は「`not`」（例えば、xpath の「`not(@prop)`」では、値のパラメーターが無視されます）、存在するかどうかをチェックする場合は「`exists`」（値は、プロパティが必ず存在すること意味するデフォルトの true と、「`not`」と同義の false）です

* **depth**

   その下にプロパティや相対パスが存在できるワイルドカードレベルの数（例： `property=size depth=2` node/size、node/*/size および node/*/*/size をチェックします）

### rangeproperty {#rangeproperty}

JCR プロパティと間隔を照合します。`LONG`、`DOUBLE` および `DECIMAL` などの線形タイプのプロパティに適用されます。`DATE` に関しては、最適化された日付形式の入力情報を含む daterange 述語を参照してください。

下限と上限、またはそのいずれかを定義できます。演算（「より少ない」や「以下」など）も、下限と上限に別々に指定することができます。

ファセットの抽出には対応していません。

#### プロパティ {#properties-16}

* **property**

   プロパティの相対パス

* **lowerBound**

   プロパティでチェックする下限

* **lowerOperation**

   「`>`」（デフォルト）または「`>=`」が、`lowerValue` に適用されます

* **upperBound**

    プロパティでチェックする上限

* **upperOperation**

   「`<`」（デフォルト）または「`<=`」が、`lowerValue` に適用されます

* **decimal**

   チェックされたプロパティのタイプが Decimal の場合は「`true`」

### relativedaterange {#relativedaterange}

`JCR DATE` プロパティと日時の間隔を照合します（現在のサーバー時間に対する時間オフセットを使用します）。ミリ秒値または Bugzilla 構文 `1s 2m 3h 4d 5w 6M 7y`（それぞれ 1 秒、2 分、3 時間、4 日、5 週間、6 か月、7 年）を使用して、`lowerBound` と `upperBound` を指定できます。先頭に「`-`」を付けると、オフセットが現在の時間より前のマイナスであることを意味します。`lowerBound` または `upperBound` のいずれかのみを指定する場合は、他方がデフォルトで 0（現在の時間）になります。

次に例を示します。

* `upperBound=1h` を指定（`lowerBound` を指定しない）：次の 1 時間以内の時刻を選択
* `lowerBound=-1d` を指定（`upperBound` を指定しない）：過去 24 時間以内の時刻を選択
* `lowerBound=-6M` および `upperBound=-3M` を指定：6 か月前から 3 か月前までを選択
* `lowerBound=-1500` および `upperBound=5500` を指定：1500 ミリ秒前から 5500 ミリ秒後の間で選択
* `lowerBound=1d` および `upperBound=2d` を指定：明後日の時刻を選択

うるう年は考慮されず、すべての月が 30 日になる点にご注意ください。

フィルターには対応していません。

daterange 述語と同じように、ファセットの抽出に対応しています。

#### プロパティ {#properties-17}

* **upperBound**

   現在のサーバー時間を基準とした日付の上限。ミリ秒単位または `1s 2m 3h 4d 5w 6M 7y`（それぞれ 1 秒、2 分、3 時間、4 日、5 週間、6 か月、7 年）で指定します。オフセットがマイナスの場合は「-」を使用します

* **lowerBound**

   現在のサーバー時間を基準とした日付の下限。ミリ秒単位または `1s 2m 3h 4d 5w 6M 7y`（それぞれ 1 秒、2 分、3 時間、4 日、5 週間、6 か月、7 年）で指定します。オフセットがマイナスの場合は「-」を使用します。

### root {#root}

ルート述語グループ。グループのすべての機能に対応し、グローバルクエリパラメーターを設定できます。

「root」という名前は暗黙的で、クエリでは使用されません。

#### プロパティ {#properties-18}

* **p.offset**

    結果ページの開始を表す数値（スキップする項目数）。

* **p.limit**

   ページのサイズを表す数値

* **p.guessTotal**

   推奨：負荷が大きくなる場合があるので、結果をすべて計算することは避けるようにしてください。カウントする最大数（1000 など、大まかなサイズに関する十分なフィードバックが得られ、結果が比較的少数の場合は正確な量がわかる数値）、または最低限必要な数値（`p.offset` + `p.limit`）までをカウントする場合は「`true`」。

* **p.excerpt**

   「`true`」に設定した場合は、完全なテキストの抜粋が結果に含まれます

* **p.hits**

    （JSON サーブレット専用）ヒットを JSON として記述する方法を、次の標準的なものの中から選択します（ResultHitWriter サービスを使用して拡張可能）。

   * **simple**：

      `path`、`title`、`lastmodified`、`excerpt`（設定されている場合）などの最小限の項目

   * **full**：

      ノードの Sling JSON レンダリング。`jcr:path` はヒットのパスを示します。デフォルトではノードの直属のプロパティのみをリストし、`p.nodedepth=N` で指定された深さのツリーが含まれます（0 は無制限のサブツリー全体を表します）。`p.acls=true` を追加すると、特定の結果項目の現在のセッションの JCR 権限が含まれます（マッピング：`create` = `add_node`、`modify` = `set_property`、`delete` = `remove`）

   * **selective**：

      `p.properties` で指定されたプロパティのみ。相対パスのスペース区切り（URL では「+」を使用）のリストになります。相対パスの深さが 1 より大きい場合は、子オブジェクトとして表現されます。特殊な jcr:path プロパティにはヒットのパスが含まれます。

### savedquery {#savedquery}

永続的な querybuilder クエリのすべての述語を、サブグループの述語として現在のクエリに含めます。

これによって追加のクエリが実行されるわけではなく、現在のクエリが拡張されます。

クエリは `QueryBuilder#storeQuery()` を使用してプログラムで永続化できます。形式は、複数行の文字列プロパティか、Java プロパティ形式のテキストファイルとしてクエリを含む `nt:file` ノードにできます。

保存済みクエリの述語のファセット抽出には対応していません。

#### プロパティ {#properties-19}

* **savedquery**

   保存済みクエリのパス（文字列プロパティまたは `nt:file` ノード）

### similar {#similar}

JCR XPath の `rep:similar()` を使用した類似性検索。

フィルターには対応していません。ファセットの抽出には対応していません。

#### プロパティ {#properties-20}

* **similar** 
類似ノードを検索するノードの絶対パス。

* **local** 
下位ノードの相対パス、または 
現在のノードの場合は `.`（オプション。デフォルトは「`.`」）

### tag {#tag}

タグタイトルのパスを指定して、タグが付けられているコンテンツを検索します。

ファセットの抽出に対応しています。現在のタグタイトルのパスを使用して固有のタグごとにバケットを提供します。

#### プロパティ {#properties-21}

* **tag**

   検索するタグタイトルのパス（「Asset Properties : Orientation / Landscape」など）。

* **N_value**

   `1_value`、`2_value`、...を使用して、複数のタグをチェックします（デフォルトでは `OR` と組み合わせ、and=true の場合は `AND` と組み合わされます）（5.6 以降）

* **property**

   検索するプロパティ（またはプロパティへの相対パス）（デフォルトは「`cq:tags`」）

### tagid {#tagid}

タグ ID を指定して、タグが付けられているコンテンツを検索します。

ファセットの抽出に対応しています。現在のタグ ID を使用して、一意のタグごとにバケットを提供します。

#### プロパティ {#properties-22}

* **tagid**

   検索するタグ ID（例：「`properties:orientation/landscape`」）

* **N_value**

   `1_value`、`2_value`、...を使用して、複数の tagid をチェックします（デフォルトでは `OR` と組み合わせ、and=true の場合は `AND` と組み合わされます）（5.6 以降）

* **property**

   検索するプロパティ（またはプロパティへの相対パス）（デフォルトは「`cq:tags`」）

### tagsearch {#tagsearch}

キーワードを指定して、タグが付けられているコンテンツを検索します。最初にタイトル内に対象のキーワードを含むタグを検索してから、それらのタグが付いている項目のみに結果を制限します。

ファセットの抽出には対応していません。

#### プロパティ {#Properties-1}

* **tagsearch**

   タグタイトルで検索するキーワード

* **property**

   検索するプロパティ（またはプロパティへの相対パス）（デフォルトは「`cq:tags`」）

* **lang**

   特定の言語にローカライズされたタグタイトルのみを対象に検索します（例：「`de`」）

* **all**

    （ブール値）タグのフルテキスト全体（すべてのタイトル、説明など）を検索します（「l `ang`」より優先されます）

### type {#type}

特定の JCR ノードのタイプ（プライマリノードタイプまたは Mixin タイプ）に結果を制限します。そのノードタイプのサブタイプも検索します。リポジトリーの検索インデックスでは、効率的に実行するために、ノードタイプに対応している必要があります。

ファセットの抽出に対応しています。結果の固有のタイプごとにバケットを提供します。

#### プロパティ {#Properties-2}

* **type**

   検索するノードタイプまたは Mixin 名（例：`cq:Page`）
