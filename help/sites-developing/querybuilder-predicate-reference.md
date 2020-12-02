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
* [グループ](#group)
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

### boolproperty  {#boolproperty}

JCR BOOLEAN プロパティに一致します。「 `true` 」と「 `false` 」の値のみを受け入れます。 「`false`」では、プロパティの値が「`false`」の場合または存在しない場合に一致します。有効になっている場合のみ設定されるブール型のフラグをチェックする際に便利です。

継承される「`operation`」パラメーターには意味はありません。

ファセットの抽出に対応しています。`true` または `false` の値ごとにバケットを提供しますが、既存のプロパティに限ります。

#### プロパティ {#properties}

* **例えば、**
booleanpropertyプロパティの相対パス 
`myFeatureEnabled` か `jcr:content/myFeatureEnabled` のどちらかにする必要があります。

* **プロパティをチェックする**
値&quot; 
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

   &quot;完全一致の場合は&quot; `=`&quot;、不等価比較の場合は&quot; `!=`&quot;、property2より大きいプロパティ1の場合は&quot; `>`&quot;、property2より大きいか等しいプロパティ1の場合は&quot; `>=`&quot;です。 デフォルト値は「`=`」です。

### daterange {#daterange}

JCR DATE プロパティと日時の間隔を照合します。これはISO8601
日付と時間の形式(`YYYY-MM-DDTHH:mm:ss.SSSZ`)を指定し、`YYYY-MM-DD`のように部分的な表現も許可します。 また、ミリ秒数のタイムスタンプ（UTC タイムゾーン、UNIX 時刻形式、1970 年以降）を指定することもできます。

2 つのタイムスタンプの間や、特定の日付より前または後のものを検索できるほか、両値を含めるか含めないかを選択することもできます。

ファセットの抽出に対応しています。「今日」、「今週」、「今月」、「過去 3 ヶ月」、「今年」、「前年」、「前年より前」のバケットを提供します。

フィルターには対応していません。

#### プロパティ {#properties-3}

* **プロパティ**

   `DATE`プロパティの相対パス（例：`jcr:lastModified`）

* **lowerBound**

   `2014-10-01`

* **lowerOperation**

   &quot; `>`&quot; （新しい）または&quot; `>=`&quot; （以降）は、`lowerBound`に適用されます。 デフォルトは「`>`」です。

* **upperBound**

   `2014-10-01T12:15:00`のように、プロパティをチェックする上限

* **upperOperation**

   &quot; `<`&quot; （古い）または&quot; `<=`&quot; （古い）は、`upperBound`に適用されます。 デフォルトは「`<`」です。

* **timeZone**

    ISO-8601 の日付文字列で指定されていない場合に使用するタイムゾーンの ID。デフォルトは、システムのデフォルトのタイムゾーンです。

### excludepaths  {#excludepaths}

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

これは概念的には`(1_property` OR `2_property)`です。

ネストされたグループの例は次のとおりです。

```
fulltext=Management
group.p.or=true
group.1_group.path=/content/geometrixx/en
group.1_group.type=cq:Page
group.2_group.path=/content/dam/geometrixx
group.2_group.type=dam:Asset
```

これは、`/content/geometrixx/en`のページ内または`/content/dam/geometrixx`のアセット内で、「**管理**」という語を検索します。

これは概念的に`fulltext AND ( (path AND type) OR (path AND type) )`です。 このような OR 結合では、パフォーマンスの観点から適切なインデックスが必要です。

#### プロパティ {#properties-6}

* **p.or**

   &quot; `true`&quot;に設定した場合、グループ内の1つの述語のみが一致する必要があります。 デフォルトは「`false`」です。この場合は、すべてが一致する必要があります。

* **p.not**

   &quot; `true`&quot;に設定した場合、グループを無効にします（デフォルトは&quot; `false`&quot;）

* **&lt;predicate>**

   入れ子の述語を追加します。

* **N_&lt;predicate>**

   `1_property, 2_property, ...`のように、ネストされた複数の述語を同時に追加します。

### hasPermission {#haspermission}

指定された [JCR 権限](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)が現在のセッションに含まれる項目に、結果を制限します。

これはフィルターのみの述語で、検索インデックスは利用できません。ファセットの抽出には対応していません。

#### プロパティ {#properties-7}

* **hasPermission**

   現在のユーザーセッションが、問題のノードに対してすべてのセッションで持つ必要があるJCRのコンマ区切り権限。例：`jcr:write`, `jcr:modifyAccessControl`

### language {#language}

特定の言語の CQ ページを検索します。ページの言語プロパティと、ページパス（一般的に最上位レベルのサイト構造に言語やロケールが含まれています）の両方を検索します。

これはフィルターのみの述語で、検索インデックスは利用できません。

ファセットの抽出に対応しています。固有の言語コードごとにバケットを提供します。

#### プロパティ {#properties-8}

* **language**

   ISO言語コード（例：`de`）

### mainasset {#mainasset}

ノードがサブアセットではなく、DAM メインアセットであるかどうかをチェックします。基本的には、DAM メインアセットは「subassets」ノード外のすべてのノードです。`dam:Asset` ノードタイプはチェックされません。この述語を使用するには、&quot; `mainasset=true`&quot;または&quot; `mainasset=false`&quot;を設定します。これ以上のプロパティはありません。

これはフィルターのみの述語で、検索インデックスは利用できません。

ファセットの抽出に対応しています。メインとサブアセットの 2 つのバケットを提供します。

#### プロパティ {#properties-9}

* **mainasset**

   ブール値。メインアセットは&quot; `true`&quot;、サブアセットは&quot; `false`&quot;

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

* **ノデナム**

   ワイルドカードを使用できるノード名パターン：`*` =任意または文字なし、`?` =任意の文字、`[abc]` =角括弧内の文字のみ

### notexpired {#notexpired}

JCR DATE プロパティが現在のサーバー時間より後か同じかをチェックすることで項目を照合します。これを使用すると、日付プロパティなどの「`expiresAt`」をチェックし、まだ有効期限が切れていないプロパティ（`notexpired=true`）または既に有効期限が切れているプロパティ（`notexpired=false`）に制限できます。

フィルターには対応していません。

daterange 述語と同じように、ファセットの抽出に対応しています。

#### プロパティ {#properties-12}

* **notexpired**

    ブール値。有効期限が切れていない（日付が現在以降である）場合は「`true`」、有効期限が切れている（日付が過去である）場合は「`false`」です（必須）。

* **プロパティ**

   確認する`DATE`プロパティの相対パス（必須）

### orderby {#orderby}

結果の並べ替えを有効にします。複数のプロパティで順序付けが必要な場合は、`1_orderby=first`、`2_oderby=second`のように、数値のプレフィックスを使用して、この述語を複数回追加する必要があります。

#### プロパティ {#properties-13}

* **orderby**

   `@jcr:lastModified`や`@jcr:content/jcr:title`などの先頭に@が付いたJCRプロパティ名か、クエリ内の別の述語（例：`2_property`）で並べ替えの対象となる

* **並べ替え**

   並べ替え方向（降順は&quot; `desc`&quot;、昇順は&quot; `asc`&quot;）

* **症例**

    「`ignore`」に設定すると、並べ替えで大文字と小文字が区別されなくなります（「a」が「B」の前になります）。空白または未指定の場合は、並べ替えで大文字と小文字が区別されます（「B」が「a」の前になります）。

### パス {#path}

特定のパス内を検索します。

ファセットの抽出には対応していません。

#### プロパティ {#properties-14}

* **path**

   パスパターン；完全一致に応じて、サブツリー全体が（xpathに`//*`を付加するのと同じですが、これはベースパスを含まないことに注意してください）(exact=false、default)、または完全一致のみに一致し、ワイルドカード(`*`)を含めることができます。selfが設定されている場合、ベースノードを含むサブツリー全体が検索されます

* **完全一致**

   `exact`がtrue/onの場合は、完全なパスは一致する必要がありますが、一致する名前を含む単純なワイルドカード(`*`)を含めることはできますが、&quot; `/`&quot;；は含めません。false（デフォルト）の場合、すべての子孫が含まれます（オプション）。

* **平らな**

   （xpathに「 `/*` 」を付加する場合など）直接の子のみを検索します（「 `exact` 」がtrueでない場合にのみ使用します。オプション）

* **self**

    サブツリーを検索しますが、パスとして指定されたベースノードが含まれます（ワイルドカードは不可）。

### property {#property}

JCR プロパティとその値に一致します。

ファセットの抽出に対応しています。結果の固有のプロパティ値ごとにバケットを提供します。

#### プロパティ {#properties-15}

* **プロパティ**

   プロパティの相対パス（例：`jcr:title`）

* **value**

    プロパティでチェックする値。JCR プロパティのタイプから文字列への変換に従います。

* **N_value**

   `1_value`、`2_value`、...を使用して、複数の値（デフォルトで`OR`と組み合わされ、ifと=true）をチェックします（5.3以降）。`AND`

* **および**

   複数の値(`N_value`)とANDを組み合わせる場合はtrueに設定（5.3以降）

* **operation**

   完全一致（デフォルト）の場合は&quot; `equals`&quot;、不等価比較の場合は&quot; `unequals`&quot;、`jcr:like` xpath関数（オプション）の場合は&quot; `like`&quot;、一致しない場合は&quot; `not`&quot; xpathの&quot; `not(@prop)`&quot;、value paramは無視されます)、または&quot; `exists`&quot; （値はtrueの場合があります。プロパティは存在する必要があり、デフォルト値はfalseの場合は&quot; `not`&quot;と同じ）

* **深さ**

   プロパティ/相対パスが存在できるワイルドカードレベルの数（例えば、`property=size depth=2`はnode/size、node/amp;ast;/size、node/&amp;ast;/&amp;ast;/size）をチェックします

### rangeproperty {#rangeproperty}

JCR プロパティと間隔を照合します。これは、`LONG`、`DOUBLE`、`DECIMAL`などの線形型を持つプロパティに適用されます。 `DATE` に関しては、最適化された日付形式の入力情報を含む daterange 述語を参照してください。

下限と上限、またはそのいずれかを定義できます。演算（「より少ない」や「以下」など）も、下限と上限に別々に指定することができます。

ファセットの抽出には対応していません。

#### プロパティ {#properties-16}

* **プロパティ**

   プロパティの相対パス

* **lowerBound**

   ～の特性をチェックする下限

* **lowerOperation**

   &quot; `>`&quot;（デフォルト）または&quot; `>=`&quot;が`lowerValue`に適用されます

* **upperBound**

   プロパティをチェックする上限

* **upperOperation**

   &quot; `<`&quot;（デフォルト）または&quot; `<=`&quot;が`lowerValue`に適用されます

* **decimal**

   &quot; `true`&quot;チェック済みプロパティのタイプが10進の場合

### relativedaterange {#relativedaterange}

`JCR DATE` プロパティと日時の間隔を照合します（現在のサーバー時間に対する時間オフセットを使用します）。ミリ秒値またはbugzilla構文`1s 2m 3h 4d 5w 6M 7y` （1秒、2分、3時間、4日、5週間、6か月、7年）を使用して`lowerBound`と`upperBound`を指定できます。 現在時間より前の負のオフセットを示す場合は、「 `-` 」というプリフィックスを付けます。 `lowerBound` または `upperBound` のいずれかのみを指定する場合は、他方がデフォルトで 0（現在の時間）になります。

次に例を示します。

* `upperBound=1h` (そして `lowerBound`)次の時間には何でも選ぶ
* `lowerBound=-1d` (そして `upperBound`)過去24時間の間に何でも選択する
* `lowerBound=-6M` 6ヶ月 `upperBound=-3M` から3ヶ月の歳月は何でも選ぶ
* `lowerBound=-1500` また、過去1500ミリ秒から将来5500ミリ秒の間の値を `upperBound=5500` 選択する必要があります。
* `lowerBound=1d` 明後日 `upperBound=2d` には何でも選ぶ

うるう年は考慮されず、すべての月が 30 日になる点にご注意ください。

フィルターには対応していません。

daterange 述語と同じように、ファセットの抽出に対応しています。

#### プロパティ {#properties-17}

* **upperBound**

   ミリ秒または`1s 2m 3h 4d 5w 6M 7y`（1秒、2分、3時間、4日、5週間、6か月、7年）の上限のサーバー時間、負のオフセットには「 — 」を使用します

* **lowerBound**

   現在のサーバー時間に対する下限の日付（ミリ秒、2分、3時間、4日、5週間、6か月、7年）。負のオフセットには「 — 」を使用します`1s 2m 3h 4d 5w 6M 7y`

### root {#root}

ルート述語グループ。グループのすべての機能に対応し、グローバルクエリパラメーターを設定できます。

「root」という名前は暗黙的で、クエリでは使用されません。

#### プロパティ {#properties-18}

* **p.offset**

    結果ページの開始を表す数値（スキップする項目数）。

* **p.limit**

   ページサイズを示す数値

* **p.guessTotal**

   推奨：コストのかかる結果の総計を計算しないようにする。最大カウント総数を示す数値（1000など、粗いサイズで十分なフィードバックを与え、小さい結果を求める正確な数値）または「`true`」（最小限必要な値までカウント） + `p.limit``p.offset`

* **p.excerpt**

   &quot; `true`&quot;に設定した場合、結果に全文の抜粋を含めます。

* **p.hits**

    （JSON サーブレット専用）ヒットを JSON として記述する方法を、次の標準的なものの中から選択します（ResultHitWriter サービスを使用して拡張可能）。

   * **シンプル**:

      `path`、`title`、`lastmodified`、`excerpt`（設定されている場合）など、最小の項目

   * **full**:

      ノードのsling JSONレンダリングで、ヒットのパスを示す`jcr:path`が付きます。デフォルトでは、リストの直接のプロパティだけがノードのより深いツリーを含めます。`p.nodedepth=N`は、0は無限のサブツリー全体を意味します。`p.acls=true`を追加して、指定した結果アイテムに対する現在のセッションのJCR権限を含めます(マッピング：`create` = `add_node`、`modify` = `set_property`、`delete` = `remove`)

   * **選択的**:

      `p.properties`に指定されたプロパティのみ。相対パスのスペース区切り（URLでは「+」を使用）リスト。相対パスの深さが1より大きい場合、これらは子オブジェクトとして表されます。特殊なjcr:pathプロパティには、ヒットのパスが含まれます。

### savedquery {#savedquery}

永続的な querybuilder クエリのすべての述語を、サブグループの述語として現在のクエリに含めます。

これによって追加のクエリが実行されることはありませんが、現在のクエリが拡張されます。

クエリは、`QueryBuilder#storeQuery()`を使用してプログラムで保持できます。 形式は、複数行の String プロパティか、Java プロパティ形式のテキストファイルとしてクエリを含む `nt:file` ノードにできます。

保存済みクエリの述語のファセット抽出には対応していません。

#### プロパティ {#properties-19}

* **savedquery**

   保存されたクエリーへのパス（Stringプロパティまたは`nt:file`ノード）

### similar {#similar}

JCR XPathの`rep:similar()`を使用した類似性検索。

フィルターには対応していません。ファセットの抽出には対応していません。

#### プロパティ {#properties-20}

* **similar** 類似ノードを検索するノードの絶対パス。

* **local** 下位ノードの相対パス、または現在のノードの場合は 
`.` 現在のノード(オプション、デフォルトは「  `.`」)

### tag {#tag}

タグタイトルのパスを指定して、タグが付けられているコンテンツを検索します。

ファセットの抽出に対応しています。現在のタグタイトルのパスを使用して固有のタグごとにバケットを提供します。

#### プロパティ {#properties-21}

* **タグ**

    検索するタグタイトルのパス（「Asset Properties : Orientation / Landscape」など）。

* **N_value**

   `1_value`、`2_value`、...を使用して、複数のタグ（デフォルトで`OR`と組み合わされ、ifと=true）をチェックします（5.6以降）`AND`

* **プロパティ**

   参照するプロパティ（またはプロパティの相対パス）（デフォルトは「`cq:tags`」）

### tagid {#tagid}

タグ ID を指定して、タグが付けられているコンテンツを検索します。

ファセットの抽出に対応しています。現在のタグ ID を使用して固有のタグごとにバケットを提供します。

#### プロパティ {#properties-22}

* **tagid**

   検索するタグID（例：&quot; `properties:orientation/landscape`&quot;）

* **N_value**

   `1_value`、`2_value`、...を使用して、複数のタグidをチェックします（デフォルトでは`OR`と組み合わされ、ifと=true）（5.6以降）。`AND`

* **プロパティ**

   参照するプロパティ（またはプロパティの相対パス）（デフォルトは「`cq:tags`」）

### tagsearch {#tagsearch}

キーワードを指定して、タグが付けられているコンテンツを検索します。最初にタイトル内に対象のキーワードを含むタグを検索してから、それらのタグが付いている項目のみに結果を制限します。

ファセットの抽出には対応していません。

#### プロパティ {#Properties-1}

* **tagsearch**

    タグタイトル内で検索するキーワード。

* **プロパティ**

   参照するプロパティ（またはプロパティの相対パス）（デフォルトは「`cq:tags`」）

* **lang**

   特定のローカライズされたタグタイトルのみを検索する場合(例：&quot; `de`&quot;)

* **all**

    （ブール値）タグのフルテキスト全体（すべてのタイトル、説明など）を検索します（「l `ang`」より優先）

### type {#type}

特定の JCR ノードのタイプ（プライマリノードタイプまたは Mixin タイプ）に結果を制限します。そのノードタイプのサブタイプも検索します。リポジトリの検索インデックスでは、効率的に実行できるノードタイプに対応する必要があります。

ファセットの抽出に対応しています。結果の固有のタイプごとにバケットを提供します。

#### プロパティ {#Properties-2}

* **type**

   検索するノードタイプまたはmixin名（例：`cq:Page`）