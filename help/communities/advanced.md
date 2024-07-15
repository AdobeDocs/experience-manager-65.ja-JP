---
title: 高度なスコアとバッジ
description: メンバーをエキスパートとして識別するためのバッジを付与できるように、高度なスコアリングを設定する方法を説明します。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: d3bb6664-6c01-4bcf-840c-072fc491fc99
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1056'
ht-degree: 2%

---

# 高度なスコアとバッジ{#advanced-scoring-and-badges}

## 概要 {#overview}

高度なスコアリングでは、メンバーをエキスパートとして識別するためのバッジを付与できます。 高度なスコアリングでは、メンバーが作成したコンテンツの数量 *および* の品質に基づいてポイントが割り当てられますが、基本のスコアリングでは、作成されたコンテンツの数量に基づいてポイントが割り当てられます。

この違いは、スコアの計算に使用されるスコアリングエンジンが原因です。 基本スコアリングエンジンでは、単純な数学が適用されます。 高度なスコアリングエンジンは、トピックの自然言語処理（NLP）を通じて推定される、価値のある関連コンテンツを投稿したアクティブなメンバーを報酬とするアダプティブアルゴリズムです。

コンテンツの関連性に加えて、スコアリングアルゴリズムは、投票および回答率などのメンバーアクティビティを考慮します。 基本スコアリングではこれらが定量的に含まれますが、高度なスコアリングではアルゴリズム的に使用されます。

したがって、高度なスコアリングエンジンでは、分析を有意義なものにするために十分なデータが必要です。 作成されるコンテンツの量と品質に合わせてアルゴリズムが継続的に調整されるので、エキスパートになるための達成基準は常に再評価されます。 また、メンバーの古い投稿には *ディケイ* という概念があります。 エキスパートメンバーが、エキスパートのステータスを獲得した案件への参加を停止した場合、事前に決定された時点（[ スコアリングエンジン設定 ](#configurable-scoring-engine) を参照）で、エキスパートとしてのステータスを失う可能性があります。

詳細スコアリングの設定は、基本スコアリングとほぼ同じです：

* 基本ルールと高度なスコアおよびバッジルールは [ コンテンツに適用 ](/help/communities/implementing-scoring.md#apply-rules-to-content) 同じ方法で適用されます。

   * 基本および高度なスコアおよびバッジルールを同じコンテンツに適用できます。

* [ コンポーネントのバッジの有効化 ](/help/communities/implementing-scoring.md#enable-badges-for-component) は汎用です。

スコアルールとバッジルールの設定の違いは次のとおりです。

* 設定可能な高度なスコアリングエンジン
* 高度なスコアリング・ルール：

   * `scoringType` を `advanced` に設定
   * `stopwords` が必要

* 高度なバッジルール：

   * `badgingType` を `advanced` に設定
   * `badgingLevels` を **報奨するエキスパートレベルの数** に設定しました
   * しきい値 `badgingPaths` バッジへの配列マッピングポイントではなく、バッジの配列が必要です。

>[!NOTE]
>
>高度なスコアおよびバッジ機能を使用するには、[ エキスパート識別パッケージ ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq610%2Fsocial%2Ffeaturepack%2Fcq-social-expert-identification-pkg) をインストールします。

## 設定可能なスコアリングエンジン {#configurable-scoring-engine}

高度なスコアリングエンジンでは、高度なスコアリングアルゴリズムに影響を与えるパラメーターを含む OSGi 設定が提供されます。

![advanced-scoring-engine](assets/advanced-scoring-engine.png)

* **スコアリング・ウェイト**

  トピックの場合、スコアを計算する際に最も高い優先度を付与する動詞を指定します。 1 つ以上のトピックを入力できますが、**トピックごとに 1 つの動詞** に制限されます。 [ トピックと動詞 ](/help/communities/implementing-scoring.md#topics-and-verbs) を参照してください。
コンマをエスケープして `topic,verb` として入力します。 次に例を示します。
  `/social/forum/hbs/social/forum\,ADD`
デフォルトでは、QnA およびフォーラムコンポーネント用の ADD 動詞に設定されています。

* **スコアリング範囲**

  高度なスコアの範囲は、この値（最大スコア）と 0 （可能な限り低いスコア）で定義されます。

  デフォルト値は 100 なので、スコアリング範囲は 0～100 です。

* **エンティティの減衰時間間隔**

  このパラメーターは、すべてのエンティティスコアが表示されるまでの時間数を表します。 これは、コミュニティサイトのスコアに古いコンテンツを含めないために必要になりました。

  デフォルト値は 216000 時間（最大 24 年）です。

* **スコアリング成長率**
これは、0 のスコアリング範囲のスコアを指定します。この範囲を超えると、成長が遅くなり、エキスパートの数が制限されます。

  デフォルト値は 50 です。

## 高度なスコアルール {#advanced-scoring-rules}

基本スコアリングでは、バッジを獲得するために必要な数がわかっています。

高度なスコアリングでは、必要な量は、システム内の品質データの量に基づいて常に調整されます。 スコアは、ベルカーブと同様の方法で継続的に計算されます。

アクティブでなくなったトピックに関してエキスパートバッジを獲得したメンバーは、時間の経過と共に崩壊によってバッジを失う可能性があります。

### scoringType {#scoringtype}

スコアルールは、スコアルールのセットで、それぞれが `scoringType` を宣言します。

詳細スコアリングエンジンを呼び出すには、`scoringType` を `advanced` に設定する必要があります。

[ スコアリング・サブ・ルール ](/help/communities/implementing-scoring.md#scoring-sub-rules) を参照してください。

![advanced-scoring-type](assets/advanced-scoring-type.png)

### ストップワード {#stopwords}

高度なスコアリングパッケージでは、ストップワードファイルを含む設定フォルダーがインストールされます。

* `/libs/settings/community/scoring/configuration/stopwords`

高度なスコアリングアルゴリズムでは、ストップワードファイルに含まれる単語のリストを使用して、コンテンツ処理中に無視される一般的な英単語が識別されます。

このファイルが変更されるとは限りません。

ストップワードファイルがない場合、詳細スコアリングエンジンでエラーが発生します。

## 高度なバッジルール {#advanced-badging-rules}

詳細なバッジルールプロパティは、[ 基本のバッジルールプロパティ ](/help/communities/implementing-scoring.md#badging-rules) とは異なります。

ポイントをバッジ画像に関連付けるのではなく、許可されるエキスパートの数と付与するバッジ画像を特定するだけで済みます。

![advanced-badging-rules](assets/advanced-badging-rules.png)

<table>
 <tbody>
  <tr>
   <th>Property</th>
   <th>タイプ</th>
   <th>値の説明</th>
  </tr>
  <tr>
   <td>badgingPath</td>
   <td>String[]</td>
   <td><em> （必須） </em> バッジ画像の複数値の文字列（最大バッジレベル数）。 バッジ画像のパスは、最初のパスが最高のエキスパートに授与されるように並べ替える必要があります。 バッジ数が badgingLevels で示される数よりも少ない場合は、配列の最後のバッジが配列の残りの部分を補完します。 エントリの例：<br /> <code>/libs/settings/community/badging/images/expert-badge/jcr:content/expert.png</code></td>
  </tr>
  <tr>
   <td>バッジのレベル</td>
   <td>Long</td>
   <td><em> （任意） </em> 付与する専門知識のレベルを指定します。 例えば、<code>expert </code> と <code>almost expert</code> （2 つのバッジ）が存在する必要がある場合、値は 2 に設定する必要があります。 バッジレベルは、badgingPath プロパティにリストされているエキスパート関連のバッジ画像の数と対応する必要があります。 初期設定は 1 です。</td>
  </tr>
  <tr>
   <td>badgingType</td>
   <td>文字列</td>
   <td><em> （必須） </em> スコアリングエンジンを「基本」または「詳細」として識別します。 「詳細」に設定します。設定しない場合、デフォルトは「基本」になります。</td>
  </tr>
  <tr>
   <td>scoringRules</td>
   <td>String[]</td>
   <td><em> （任意） </em> リストされている 1 つ以上のスコアルールによって識別されるスコアリングイベントにバッジルールを制限するための複数値文字列。<br /> エントリの例：<br /> <code>/libs/settings/community/scoring/rules/adv-comments-scoring</code><br /> デフォルトは制限なしです。</td>
  </tr>
 </tbody>
</table>

## 含まれるルールとバッジ {#included-rules-and-badge}

### Included Badge {#included-badge}

このベータ版リリースには、報酬ベースのエキスパートバッジが 1 つ含まれています。

* `expert`

  `/libs/settings/community/badging/images/expert-badge/jcr:content/expert.png`

![ エキスパートバッジ ](assets/included-badge.png)

エキスパートバッジをアクティビティの報酬として表示するには、次の点を確認してください。

* フォーラムや QnA コンポーネントなど、その機能に対して `Badges` が有効になっています。

* 高度なスコアおよびバッジルールは、コンポーネントが配置されているページ（または上位）に適用されます

次の基本情報を参照してください。

* [コンポーネントのバッジの有効化](/help/communities/implementing-scoring.md#enableforcomponent)
* [ルールの適用](/help/communities/implementing-scoring.md#applytopage)

### スコアルールとサブルールを含む {#included-scoring-rules-and-sub-rules}

ベータ版リリースには、[ フォーラム機能 ](/help/communities/functions.md#forum-function) 用の 2 つの高度なスコアルール（フォーラム機能のフォーラムおよびコメント用コンポーネントのそれぞれに 1 つずつ）が含まれています。

1. `/libs/settings/community/scoring/rules/adv-comments-scoring`

   ```
   subRules[] =
   /libs/settings/community/scoring/rules/sub-rules/adv-comments-rule
   /libs/settings/community/scoring/rules/sub-rules/adv-voting-rule-owner
   /libs/settings/community/scoring/rules/sub-rules/adv-voting-rule
   ```

1. `/libs/settings/community/scoring/rules/adv-forums-scoring`

   ```
   subRules[] =
   /libs/settings/community/scoring/rules/sub-rules/adv-forums-rule
   /libs/settings/community/scoring/rules/sub-rules/adv-comments-rule
   /libs/settings/community/scoring/rules/sub-rules/adv-voting-rule-owner
   ```

**メモ：**

* `rules` ノードと `sub-rules` ノードのタイプはどちらも `cq:Page` です。
* `subRules` は、ルールの `jcr:content` ノードにある `[]` 文字列型の属性です。
* `sub-rules` は、様々なスコアルールで共有される場合があります。
* `rules` べてのユーザーに対して読み取り権限を持つリポジトリの場所に置く必要があります。
* ルール名は、場所に関係なく一意である必要があります。

### 含まれるバッジルール {#included-badging-rules}

リリースには、[ 高度なフォーラムとコメントスコアルール ](#included-scoring-rules-and-sub-rules) に対応する 2 つの高度なバッジルールが含まれています。

* `/libs/settings/community/badging/rules/adv-comments-badging`
* `/libs/settings/community/badging/rules/adv-forums-badging`

**メモ：**

* ノ `rules` ドのタイプは cq:Page です。
* `rules` べてのユーザーに対して読み取り権限を持つリポジトリの場所に置く必要があります。
* ルール名は、場所に関係なく一意である必要があります。
