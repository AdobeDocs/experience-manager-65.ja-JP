---
title: Query Builder の述語リファレンス
description: Query Builder API の完全な述語リファレンスです。
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
exl-id: 54b942f9-5dd9-4826-9a0a-028f2d7b8e41
source-git-commit: 1ef5593495b4bf22d2635492a360168bccc1725d
workflow-type: tm+mt
source-wordcount: '2343'
ht-degree: 28%

---

# Query Builder の述語リファレンス{#query-builder-predicate-reference}

>[!CAUTION]
>
>このページの情報は網羅的ではありません。
>
>詳しくは、Query Builder Debugger コンソールで、**使用可能な述語**&#x200B;のリストを参照してください。例：
>* [http://localhost:4502/libs/cq/search/content/querydebug.html](http://localhost:4502/libs/cq/search/content/querydebug.html)
>
>例：
>
>* [http://localhost:4502/system/console/services?filter=%28component.factory%3Dcom.day.cq.search.eval.PredicateEvaluator%2F*%29](http://localhost:4502/system/console/services?filter=%28component.factory%3Dcom.day.cq.search.eval.PredicateEvaluator%2F*%29)

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

JCR ブール型プロパティに一致します。 受け入れられる値は「`true`」と「`false`」のみです。&quot; `false`&quot;、プロパティの値が&quot; `false`」またはまったく存在しない場合は「 有効なときだけ設定されるブール型のフラグをチェックする際に便利です。

継承される「`operation`」パラメーターには意味はありません。

ファセットの抽出に対応しています。各 `true` または `false` 値のみを取得します。ただし、既存のプロパティの場合のみ。

#### プロパティ {#properties}

* **boolproperty**
プロパティへの相対パス（例： ） `myFeatureEnabled` または `jcr:content/myFeatureEnabled`.

* **値**
プロパティを確認する値 (「」) `true`&quot;または&quot; `false`&quot;.

### contentfragment {#contentfragment}

結果をコンテンツフラグメントに制限します。

フィルタリングをサポートしていません。

ファセットの抽出はサポートされていません。

#### プロパティ {#properties-1}

* **contentfragment** 
任意の値と併用してコンテンツフラグメントをチェックできます。

### dateComparison {#datecomparison}

2 つの JCR DATE プロパティを比較します。 等しい、等しくない、より大きいか等しいかをテストできます。

これはフィルターのみの述語で、検索インデックスを使用できません。

#### プロパティ {#properties-2}

* **property1**

  最初の日付プロパティへのパス。

* **property2**

  2 つ目の日付プロパティへのパス。

* **operation**

  完全一致の場合は「`equals`」、不等号比較の場合は「`!=`」、プロパティ 1 がプロパティ 2 より大きい場合は「`greater`」、プロパティ 1 がプロパティ 2 以上の場合は「`>=`」となります。デフォルト値は「`equals`」です。

### daterange {#daterange}

JCR DATE プロパティと日時間隔を照合します。 ISO8601 形式の日時（`YYYY-MM-DDTHH:mm:ss.SSSZ`）を使用します。`YYYY-MM-DD` などの部分表記も可能です。また、タイムスタンプは、1970 以降のミリ秒数 (UTC タイムゾーン (UNIX®時刻形式 ) で指定することもできます。

2 つのタイムスタンプの間や、特定の日付より前または後のものを検索できるほか、両値を含めるか含めないかを選択することもできます。

ファセットの抽出に対応しています。「今日」、「今週」、「今月」、「過去 3 ヶ月」、「今年」、「昨年」、「昨年より前」のバケットを提供します。

フィルタリングをサポートしていません。

#### プロパティ {#properties-3}

* **property**

  の相対パス `DATE` プロパティ。例： `jcr:lastModified`.

* **lowerBound**

  プロパティを確認する日付の下限（例： ） `2014-10-01`.

* **lowerOperation**

  「`>`」（より後）または 「`>=`」（以降）が `lowerBound` に適用されます。デフォルトは「`>`」です。

* **upperBound**

  プロパティを確認する上限（例： ） `2014-10-01T12:15:00`.

* **upperOperation**

  「`<`」（より前）または 「`<=`」（以前）が `upperBound` に適用されます。デフォルトは「`<`」です。

* **timeZone**

   ISO-8601 の日付文字列で指定されていない場合に使用するタイムゾーンの ID。デフォルトは、システムのデフォルトタイムゾーンです。

### excludepaths {#excludepaths}

パスが正規表現と一致するノードを結果から除外します。

これはフィルターのみの述語で、検索インデックスを使用できません。

ファセットの抽出はサポートされていません。

#### プロパティ {#properties-4}

* **excludepaths**

  結果のパスと一致する正規表現（一致するパスを結果から除く）。

### fulltext {#fulltext}

フルテキストインデックス内の用語を検索します。

フィルタリングをサポートしていません。

ファセットの抽出はサポートされていません。

#### プロパティ {#properties-5}

* **fulltext**

  全文検索用語。

* **relPath**

  プロパティまたはサブノード内の検索の相対パス。 このプロパティはオプションです。

### group {#group}

ネストされた条件を作成できます。 グループにはネストされたグループを含めることができます。Query Builder クエリ内のすべては、ルートグループ内で暗黙的に存在し、 `p.or` および `p.not` パラメーターも同様に使用します。

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

これは概念上は `fulltext AND ( (path AND type) OR (path AND type) )` になります。このような OR 結合は、パフォーマンスを向上させるために適切なインデックスが必要です。

#### プロパティ {#properties-6}

* **p.or**

  &quot; `true`」（グループ内の 1 つの述語のみが一致する必要があります） デフォルトは「`false`」です。この場合は、すべてが一致する必要があります。

* **p.not**

  &quot; `true`&quot;、グループを否定します ( デフォルトは&quot; `false`&quot;) です。

* **&lt;predicate>**

  ネストされた述語を追加します。

* **N_&lt;predicate>**

  同時にネストされた複数の述語を追加します。例： `1_property, 2_property, ...`.

### hasPermission {#haspermission}

指定された [JCR 権限](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)が現在のセッションに含まれる項目に、結果を制限します。

これはフィルターのみの述語で、検索インデックスを使用できません。 ファセットの抽出には対応していません。

#### プロパティ {#properties-7}

* **hasPermission**

  現在のユーザーセッションには、問題のノードが含まれている必要がある、コンマ区切りの JCR 権限。 例： `jcr:write`, `jcr:modifyAccessControl`.

### language {#language}

特定の言語で CQ ページを検索します。 これは、ページ言語プロパティと、多くの場合、トップレベルのサイト構造に言語やロケールを含むページパスの両方を確認します。

これはフィルターのみの述語で、検索インデックスを使用できません。

ファセットの抽出に対応しています。一意の言語コードごとにグループを提供します。

#### プロパティ {#properties-8}

* **language**

  ISO 言語コード（例：「`de`」）

### mainasset {#mainasset}

ノードがサブアセットではなく DAM のメインアセットであるかどうかを確認します。 これは基本的に、「サブアセット」ノード内にないすべてのノードです。 これは、 `dam:Asset` ノードタイプ。 この述語を使用するには、 `mainasset=true`&quot;または&quot; `mainasset=false`「、これ以上のプロパティはありません。

これはフィルターのみの述語で、検索インデックスを使用できません。

ファセットの抽出に対応しています。メインアセットとサブアセットの 2 つのバケットを提供します。

#### プロパティ {#properties-9}

* **mainasset**

  ブール値、「 `true`」（メインアセットの場合） `false`」 （サブアセット用）

### memberOf {#memberof}

特定の項目のメンバーである項目を検索します [sling リソースコレクション](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/resource/collection/ResourceCollection.html).

これはフィルターのみの述語で、検索インデックスを使用できません。 ファセットの抽出はサポートされていません。

#### プロパティ {#properties-10}

* **memberOf**

  Sling リソースコレクションのパス。

### nodename {#nodename}

JCR ノード名に一致します。

ファセットの抽出に対応しています。一意のノード名（ファイル名）ごとにグループを提供します。

#### プロパティ {#properties-11}

* **nodename**

  ワイルドカードを使用できるノード名パターン： `*` =文字のいずれか、または文字なし `?` =任意の文字 `[abc]` =括弧内の文字のみ。

### notexpired {#notexpired}

JCR DATE プロパティが現在のサーバー時刻以上かどうかをチェックして項目を照合します。 これを使用すると、日付プロパティなどの「`expiresAt`」をチェックし、まだ有効期限が切れていないプロパティ（`notexpired=true`）または既に有効期限が切れているプロパティ（`notexpired=false`）に制限できます。

フィルタリングをサポートしていません。

daterange 述語と同じ方法でファセットの抽出をサポートします。

#### プロパティ {#properties-12}

* **notexpired**

  ブール値、「 `true`」 ( まだ期限切れではありません（日付が未来かそれと等しい）の場合、「 `false`」 ( 期限切れ（過去の日付） （必須）の場合 )

* **property**

  の相対パス `DATE` 確認するプロパティ（必須）。

### orderby {#orderby}

結果を並べ替えることを許可します。 複数のプロパティによる並べ替えが必要な場合は、数値のプレフィックスを使用して、この述語を複数回追加する必要があります ( 例： `1_orderby=first`, `2_oderby=second`.

#### プロパティ {#properties-13}

* **orderby**

  先頭に@が付く JCR プロパティ名（例： ） `@jcr:lastModified` または `@jcr:content/jcr:title`またはクエリ内の別の述語（例： ） `2_property`：並べ替える基準となる。

* **並べ替え**

  「 `desc`「 」（降順）または「 `asc`」を追加します（デフォルト）。

* **case**

  次に設定した場合： `ignore`の場合、並べ替えでは大文字と小文字が区別されません。つまり、「a」が「B」の前にあることを意味します。空の場合または除外された場合、並べ替えでは大文字と小文字が区別されます。つまり、「B」は「a」の前になります。

### path {#path}

特定のパス内を検索します。

ファセットの抽出はサポートされていません。

#### プロパティ {#properties-14}

* **path**

  パスのパターン；完全一致に応じて、サブツリー全体が一致する ( `//*` xpath ではベースパスは含まれません (exact=false、default)。または完全一致パスのみが一致します。この場合、ワイルドカード ( `*`);self が設定されている場合は、ベースノードを含むサブツリー全体が検索されます。

* **exact**

  If `exact` が true/on の場合、パスは完全に一致する必要がありますが、単純なワイルドカード ( `*`)、名前に一致するが、&quot;に一致しない `/`&quot;;false（デフォルト）の場合、すべての子孫が含まれます（オプション）。

* **flat**

  直接の子のみを検索します (「 `/*`」 （xpath 内）(&#39; `exact`「 」は true ではありません（オプション）。

* **self**

  サブツリーを検索しますが、パスとして指定されたベースノードが含まれます（ワイルドカードは使用できません）。

### property {#property}

JCR プロパティとその値が一致します。

ファセットの抽出に対応しています。結果の一意のプロパティ値ごとにグループを提供します。

#### プロパティ {#properties-15}

* **property**

  プロパティへの相対パス（例： ） `jcr:title`.

* **value**

  プロパティを確認する値。では、JCR プロパティタイプに従って文字列を変換します。

* **N_value**

  用途 `1_value`, `2_value`、...複数の値をチェックします ( `OR` デフォルトでは、 `AND` and=true の場合は（5.3 以降）。

* **および**

  複数の値を組み合わせる場合は true に設定します ( `N_value`) と AND （ 5.3 以降）

* **operation**

  &quot;`equals`&quot;完全一致の場合（デフォルト）、&quot; `unequals`&quot;非等価の比較のために&quot; `like`」を `jcr:like` xpath 関数（オプション）, &quot; `not`」の場合は「`not(@prop)`&quot; xpath では、値のパラメーターは無視されます ) または&quot; `exists`&quot;存在を確認する場合 ( 値は true、プロパティは存在する必要があります。デフォルト (false) は&quot; `not`&quot;) です。

* **depth**

  プロパティや相対パスが存在できるワイルドカードレベルの数 ( 例： `property=size depth=2` node/size、node/&amp;ast;/size および node/&amp;ast;/&amp;ast;/size) をチェックします。

### rangeproperty {#rangeproperty}

JCR プロパティと間隔を照合します。 これは、次のような線形タイプのプロパティに適用されます。 `LONG`, `DOUBLE`、および `DECIMAL`. の場合 `DATE`を参照してください。最適化された日付形式の入力を持つ daterange 述語を参照してください。

下限と上限、またはそのうち 1 つのみを定義できます。 また、下限と上限に対して、操作（例えば、「より小さい」または「より小さいか等しい」）を個別に指定することもできます。

ファセットの抽出はサポートされていません。

#### プロパティ {#properties-16}

* **property**

  プロパティの相対パス。

* **lowerBound**

  プロパティを確認する下限。

* **lowerOperation**

  「`>`」（デフォルト）または「`>=`」が、`lowerValue` に適用されます

* **upperBound**

  プロパティを確認する上限です。

* **upperOperation**

  「`<`」（デフォルト）または「`<=`」が、`lowerValue` に適用されます

* **decimal**

  チェックされたプロパティのタイプが Decimal の場合は「`true`」

### relativedaterange {#relativedaterange}

`JCR DATE` プロパティと日時の間隔を照合します（現在のサーバー時間に対する時間オフセットを使用します）。ミリ秒値または Bugzilla 構文 `1s 2m 3h 4d 5w 6M 7y`（それぞれ 1 秒、2 分、3 時間、4 日、5 週間、6 か月、7 年）を使用して、`lowerBound` と `upperBound` を指定できます。先頭に「`-`」を付けると、オフセットが現在の時間より前のマイナスであることを意味します。次のみを指定した場合、 `lowerBound` または `upperBound`の場合は、もう 1 つのデフォルト値は 0 で、現在の時刻を表します。

次に例を示します。

* `upperBound=1h` を指定（`lowerBound` を指定しない）：次の 1 時間以内の時刻を選択
* `lowerBound=-1d` を指定（`upperBound` を指定しない）：過去 24 時間以内の時刻を選択
* `lowerBound=-6M` および `upperBound=-3M` を指定：6 か月前から 3 か月前までを選択
* `lowerBound=-1500` および `upperBound=5500` を指定：1500 ミリ秒前から 5500 ミリ秒後の間で選択
* `lowerBound=1d` および `upperBound=2d` を指定：明後日の時刻を選択

うるう年は考慮されず、すべての月が 30 日です。

フィルタリングをサポートしていません。

daterange 述語と同じ方法でファセットの抽出をサポートします。

#### プロパティ {#properties-17}

* **upperBound**

  日付の上限（ミリ秒）または `1s 2m 3h 4d 5w 6M 7y` （1 秒、2 分、3 時間、4 日、5 週間、6 ヶ月、7 年）現在のサーバー時間を基準にした相対的な値。負のオフセットは「 — 」を使用します。

* **lowerBound**

  日付の下限（ミリ秒）または `1s 2m 3h 4d 5w 6M 7y` （1 秒、2 分、3 時間、4 日、5 週間、6 ヶ月、7 年）現在のサーバー時間を基準にした相対的な値。負のオフセットは「 — 」を使用します。

### root {#root}

ルート述語グループ。 グループのすべての機能をサポートし、グローバルクエリパラメーターを設定できます。

「root」という名前は暗黙的で、クエリでは使用されません。

#### プロパティ {#properties-18}

* **p.offset**

  結果ページの開始（スキップする項目数）を示す数値。

* **p.limit**

  ページサイズを示す数値。

* **p.guessTotal**

  推奨：コストのかかる結果の全体を計算するのを避ける。最大数を示す数（例：1000、大まかなサイズと小さい結果を得るための正確な数でユーザーに十分なフィードバックを提供する数）または「 `true`」をクリックして、必要最小限の値までカウントします。 `p.offset` + `p.limit`.

* **p.excerpt**

  &quot; `true`「、結果に全文の抜粋を含める。

* **p.hits**

   （JSON サーブレット専用）ヒットを JSON として記述する方法を、次の標準的なものの中から選択します（ResultHitWriter サービスを使用して拡張可能）。

   * **simple**：

     のような最小項目 `path`, `title`, `lastmodified`, `excerpt` （設定されている場合）

   * **full**：

     ノードの Sling JSON レンダリング（を使用） `jcr:path` ヒットのパスを示します。デフォルトでは、ノードの直接プロパティのリストのみが表示され、 `p.nodedepth=N`（0 は全体を意味し、無限サブツリーを意味する）追加 `p.acls=true` 指定した結果項目に対する現在のセッションの JCR 権限を含めるには ( マッピング： `create` = `add_node`, `modify` = `set_property`, `delete` = `remove`) をクリックします。

   * **selective**：

     で指定されたプロパティのみ `p.properties`：スペースで区切られた（URL で「+」を使用）相対パスのリスト。相対パスの深さが 1 を超える場合は、これらは子オブジェクトとして表されます。特別な jcr:path プロパティには、ヒットのパスが含まれます

### savedquery {#savedquery}

永続化された Query Builder クエリのすべての述語を、サブグループの述語として現在のクエリに含めます。

追加のクエリは実行されず、現在のクエリを拡張します。

クエリは `QueryBuilder#storeQuery()` を使用してプログラムで永続化できます。複数行の文字列プロパティまたは `nt:file` クエリをテキストファイルとして Java™プロパティ形式で含むノード。

保存済みクエリの述語のファセット抽出には対応していません。

#### プロパティ {#properties-19}

* **savedquery**

  保存されたクエリのパス (String プロパティまたは `nt:file` ノード ) で使用できます。

### similar {#similar}

JCR XPath の `rep:similar()` を使用した類似性検索。

フィルタリングをサポートしていません。 ファセットの抽出はサポートされていません。

#### プロパティ {#properties-20}

* **類似**
類似のノードを検索するノードへの絶対パス。

* **ローカル**
下位ノードへの相対パス、または `.` 現在のノード ( オプション、デフォルトは&quot; `.`&quot;) です。

### tag {#tag}

タグタイトルのパスを指定して、1 つ以上のタグが付いたコンテンツを検索します。

ファセットの抽出に対応しています。現在のタグタイトルパスを使用して、一意のタグごとにバケットを提供します。

#### プロパティ {#properties-21}

* **tag**

  検索するタグタイトルのパス（「アセットのプロパティ」など）。向き/横向き»。

* **N_value**

  用途 `1_value`, `2_value`、...複数のタグ ( `OR` デフォルトでは、 `AND` and=true の場合は（5.6 以降）。

* **property**

  参照するプロパティ（またはプロパティへの相対パス） ( デフォルト&quot; `cq:tags`&quot;)

### tagid {#tagid}

タグ ID を指定して、1 つ以上のタグが付いたコンテンツを検索します。

ファセットの抽出に対応しています。現在のタグ ID を使用して、一意のタグごとにバケットを提供します。

#### プロパティ {#properties-22}

* **tagid**

  タグ ID（例： ） `properties:orientation/landscape`&quot;.

* **N_value**

  用途 `1_value`, `2_value`、...複数のタグ ID ( `OR` デフォルトでは、 `AND` and=true の場合は（5.6 以降）。

* **property**

  参照するプロパティ（またはプロパティへの相対パス） ( デフォルト&quot; `cq:tags`&quot;) です。

### tagsearch {#tagsearch}

キーワードを指定して、1 つ以上のタグが付いたコンテンツを検索します。 これにより、まずこれらのキーワードをタイトルに含むタグを検索し、結果をこれらのタグが付けられた項目のみに制限します。

ファセットの抽出はサポートされていません。

#### プロパティ {#Properties-1}

* **tagsearch**

  タグタイトルで検索するキーワード。

* **property**

  参照するプロパティ（またはプロパティへの相対パス）（デフォルト） `cq:tags`) をクリックします。

* **lang**

  特定のローカライズされたタグタイトルのみを検索するには ( 例： `de`) をクリックします。

* **all**

  （ブール値）タグのフルテキスト全体、つまり、すべてのタイトルや説明などを検索します ( `ang`&quot;) です。

### type {#type}

結果を特定の JCR ノードタイプ（プライマリノードタイプまたは Mixin タイプの両方）に制限します。 また、そのノードタイプのサブタイプも検索します。 リポジトリ検索インデックスでは、効率的に実行するために、ノードタイプをカバーする必要があります。

ファセットの抽出に対応しています。結果の一意のタイプごとにグループを提供します。

#### プロパティ {#Properties-2}

* **type**

  検索するノードタイプまたは mixin 名（例： ） `cq:Page`.
