---
title: 高度なスコアとバッジ
seo-title: Advanced Scoring and Badges
description: 高度なスコアの設定
seo-description: Setting up advanced scoring
uuid: 48caca57-43d3-4f2f-adf3-257428ba54d5
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: eb3d5c37-8097-46de-8c4f-804ea723f1c5
docset: aem65
role: Admin
exl-id: d3bb6664-6c01-4bcf-840c-072fc491fc99
source-git-commit: 07f8a9f629122102d30676926b225d57e542147d
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 39%

---

# 高度なスコアとバッジ{#advanced-scoring-and-badges}

## 概要 {#overview}

高度なスコアを使用すると、メンバーをエキスパートとして識別するバッジを授与できます。高度なスコアリングでは、数量に基づいてポイントを割り当てます *および* メンバーが作成したコンテンツの品質。一方、基本スコアでは、作成したコンテンツの量に基づいてポイントを割り当てます。

この違いは、スコアの計算に使用されるスコアエンジンによるものです。基本スコアエンジンは、単純な計算を適用します。 高度なスコアエンジンは、トピックの自然言語処理 (NLP) を通じて推測される、価値のある関連コンテンツに貢献するアクティブなメンバーに対して報酬を与えるアダプティブなアルゴリズムです。

このスコアアルゴリズムでは、コンテンツの関連度に加え、投票や回答の割合など、メンバーのアクティビティが考慮されます。基本的なスコアリングには定量的なものも含まれますが、高度なスコアリングではアルゴリズム的に使用されます。

したがって、高度なスコアエンジンの分析を意味あるものにするには、十分なデータが必要です。作成されるコンテンツの量と品質に応じてアルゴリズムが継続的に調整されるので、エキスパートになるための達成度のしきい値は、常に再評価されます。 また、 *減衰* メンバーの古い投稿の エキスパートメンバーが、事前に決定した時点で、エキスパートの地位を得た問題への参加を停止した場合 ( [スコアエンジンの設定](#configurable-scoring-engine)) エキスパートとしての地位を失う可能性があります。

高度なスコアの設定方法は、基本スコアとほとんど同じです。

* 基本的なスコアと高度なスコアおよびバッジルールは次のとおりです。 [コンテンツに適用済み](/help/communities/implementing-scoring.md#apply-rules-to-content) 同じように

   * 基本スコアと高度なスコアおよびバッジルールを同じコンテンツに適用できます。

* [コンポーネントのバッジの有効化](/help/communities/implementing-scoring.md#enable-badges-for-component) は汎用です。

スコアルールおよびバッジルールの設定では、以下の点が異なります。

* 設定可能な高度なスコアエンジン
* 高度なスコアルール：

   * `scoringType` を `advanced` に設定
   * 次を必要とする `stopwords`

* 高度なバッジルール：

   * `badgingType` を `advanced` に設定
   * `badgingLevels`**を授与するエキスパートレベルの数に設定**
   * 必要 `badgingPaths` しきい値の代わりにバッジの配列配列配列マッピングポイントとバッジ。

>[!NOTE]
>
>高度なスコアおよびバッジ機能を使用するには、 [エキスパート特定パッケージ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq610%2Fsocial%2Ffeaturepack%2Fcq-social-expert-identification-pkg).

## 設定可能なスコアエンジン {#configurable-scoring-engine}

この高度なスコアエンジンには OSGi 設定が用意されており、パラメーターを設定して高度なスコアアルゴリズムを調整できます。

![advanced-scoring-engine](assets/advanced-scoring-engine.png)

* **スコア付けの重み付け**

   特定のトピックについて、スコア計算時に最も高い優先度を与える動詞を指定します。1 つ以上のトピックを入力できますが、次に限定されます **1 つの話題に対する 1 つの動詞**. 詳しくは、 [トピックと動詞](/help/communities/implementing-scoring.md#topics-and-verbs).
次の形式で入力 `topic,verb` コンマはエスケープされます。 次に例を示します。
   `/social/forum/hbs/social/forum\,ADD`
デフォルトでは、Q&amp;A とフォーラムコンポーネントの ADD 動詞が設定されています。

* **スコアリング範囲**

   高度なスコアの範囲は、この値（可能な最大スコア）と 0（可能な最小スコア）で定義されます。

   デフォルト値は 100 であり、スコア範囲は 0 ～ 100 となります。

* **エンティティの減衰時間間隔**

   このパラメーターは、すべてのエンティティのスコアが低下するまでの時間数を表します。 これは、コミュニティサイト上にある古いコンテンツをスコアに含めないようにするために必要な設定です。

   デフォルト値は 216000 時間（約 24 年）です。

* **スコア付け成長率**
この値は、0 からスコア範囲の間のスコアを指定します。この値を超えると、成長が遅くなり、エキスパートの数が制限されます。

   デフォルト値は 50 です。

## 高度なスコアルール {#advanced-scoring-rules}

基本スコアでは、バッジ獲得に必要な量はあらかじめ決まっています。

高度なスコアでは、システム内の上質なデータの量に基づいて、バッジ獲得に必要な量が継続的に調整されます。スコアは、ベルカーブと同様の方法で継続的に計算されます。

メンバーがアクティブでなくなったトピックに関するエキスパートバッジを獲得した場合、時間の経過と共に減衰が原因でバッジが失われる可能性があります。

### scoringType {#scoringtype}

スコアルールは、スコアサブルールの集まりです。各サブルールは、それぞれ `scoringType` を宣言します。

高度なスコアエンジンを呼び出すには、`scoringType` を `advanced` に設定する必要があります。

[スコアサブルール](/help/communities/implementing-scoring.md#scoring-sub-rules)を参照してください。

![advanced-scoring-type](assets/advanced-scoring-type.png)

### ストップワード {#stopwords}

高度なスコアパッケージでは、ストップワードファイルを含む設定フォルダーがインストールされます。

* `/libs/settings/community/scoring/configuration/stopwords`

高度なスコアのアルゴリズムは、ストップワードファイルに含まれる単語のリストに基づいて、コンテンツ処理中に無視して構わない一般的な英単語を識別します。

このファイルが変更されることはありません。

ストップワードファイルが存在しない場合は、スコアエンジンによりエラーがスローされます。

## 高度なバッジルール {#advanced-badging-rules}

高度なバッジルールのプロパティは、[基本バッジルールのプロパティ](/help/communities/implementing-scoring.md#badging-rules)とは異なります。

ポイントとバッジ画像を関連付ける必要はなく、許可するエキスパートの数と、授与するバッジ画像を指定するだけで十分です。

![advanced-badging-rules](assets/advanced-badging-rules.png)

<table>
 <tbody>
  <tr>
   <th>プロパティ</th>
   <th>タイプ</th>
   <th>値 説明</th>
  </tr>
  <tr>
   <td>badgingPath</td>
   <td>String[]</td>
   <td><em>（必須）</em> badgingLevels の数までのバッジ画像の複数値文字列。 バッジ画像のパスを指定するときは、最も高いレベルのエキスパートに授与するものを最初に指定する必要があります。badgingLevels で指定された値よりもバッジの数が少ない場合、足りない部分には配列内の最終要素のバッジが使用されます。エントリの例：<br /> <code>/libs/settings/community/badging/images/expert-badge/jcr:content/expert.png</code></td>
  </tr>
  <tr>
   <td>badgingLevels</td>
   <td>Long</td>
   <td><em>（オプション）</em> 与える専門知識のレベルを指定します。 例えば、 <code>expert </code>および <code>almost expert</code> （バッジが 2 つ）の場合、値は 2 に設定する必要があります。 badgingLevel は、badgingPath プロパティにリストされるエキスパート関連のバッジ画像の数に対応している必要があります。 初期設定は 1 です。</td>
  </tr>
  <tr>
   <td>badgingType</td>
   <td>String</td>
   <td><em>（必須）</em> スコアリングエンジンを「基本」または「詳細」として識別します。 "advanced"に設定し、それ以外の場合、デフォルトは"basic"です。</td>
  </tr>
  <tr>
   <td>scoringRules</td>
   <td>String[]</td>
   <td><em>（オプション）</em> リストに表示されるスコアルールで識別されるスコアイベントにバッジルールを制限する複数値の文字列。<br /> エントリの例：<br /> <code>/libs/settings/community/scoring/rules/adv-comments-scoring</code><br /> デフォルトでは、制限はありません。</td>
  </tr>
 </tbody>
</table>

## このリリースに含まれるルールとバッジ {#included-rules-and-badge}

### このリリースに含まれるバッジ {#included-badge}

このベータリリースには、以下の報奨ベースのエキスパートバッジが含まれています。

* `expert`

   `/libs/settings/community/badging/images/expert-badge/jcr:content/expert.png`

![エキスパートバッジ](assets/included-badge.png)

エキスパートバッジをアクティビティへの報酬として表示するには、次の点を確認します。

* `Badges` は、フォーラムや Q&amp;A コンポーネントなどの機能に対して有効になっています。

* 高度なスコアルールとバッジルールは、コンポーネントが配置されているページ（または上位ページ）に適用されます

以下の基本情報を参照してください。

* [コンポーネントのバッジの有効化](/help/communities/implementing-scoring.md#enableforcomponent)
* [ルールの適用](/help/communities/implementing-scoring.md#applytopage)

### このリリースに含まれているスコアルールとサブルール {#included-scoring-rules-and-sub-rules}

ベータリリースには、 [フォーラム機能](/help/communities/functions.md#forum-function) （フォーラム機能のフォーラムおよびコメントコンポーネントごとに 1 つずつ）:

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

* 両方 `rules` および `sub-rules` ノードはタイプです `cq:Page`.
* `subRules` は String 型の属性です`[]` 規則の `jcr:content` ノード。
* `sub-rules` は、様々なスコアリングルール間で共有できます。
* `rules` はリポジトリの場所に配置し、全員に対して読み取り権限を付与する必要があります。
* ルール名は、場所に関係なく一意である必要があります。

### このリリースに含まれるバッジルール {#included-badging-rules}

このリリースには、 [高度なフォーラムおよびコメントのスコアリングルール](#included-scoring-rules-and-sub-rules).

* `/libs/settings/community/badging/rules/adv-comments-badging`
* `/libs/settings/community/badging/rules/adv-forums-badging`

**メモ：**

* `rules` ノードのタイプは cq:Page です。
* `rules` はリポジトリの場所に配置し、全員に対して読み取り権限を付与する必要があります。
* ルール名は、場所に関係なく一意である必要があります。
