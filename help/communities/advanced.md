---
title: 高度なスコアとバッジ
description: 高度なスコアを設定して、メンバーをエキスパートとして識別するバッジの授与を許可する方法を説明します。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: d3bb6664-6c01-4bcf-840c-072fc491fc99
source-git-commit: 0a4aca939c564720f63f055e9522e56942eaa128
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 2%

---

# 高度なスコアとバッジ{#advanced-scoring-and-badges}

## 概要 {#overview}

高度なスコアでは、メンバーをエキスパートとして識別するためのバッジを授与できます。 高度なスコアリングでは、数量に基づいてポイントを割り当てます *および* メンバーが作成したコンテンツの品質。一方、基本スコアでは、作成したコンテンツの量に基づいてポイントを割り当てます。

この違いは、スコアの計算に使用されるスコアリングエンジンによるものです。 基本スコアエンジンは、単純な計算を適用します。 高度なスコアエンジンは、トピックの自然言語処理 (NLP) を通じて推測される、価値のある関連コンテンツに貢献するアクティブなメンバーに対して報酬を与えるアダプティブなアルゴリズムです。

コンテンツの関連性に加えて、スコアリングアルゴリズムは、投票や回答の割合などのメンバーアクティビティを考慮します。 基本的なスコアリングには定量的なものも含まれますが、高度なスコアリングではアルゴリズム的に使用されます。

したがって、高度なスコアエンジンでは、分析を意味のあるものにするのに十分なデータが必要です。 作成されたコンテンツのボリュームと品質にアルゴリズムが継続的に調整されるので、エキスパートになるための達成度のしきい値は、常に再評価されます。 また、 *減衰* メンバーの古い投稿の エキスパートメンバーが、事前に決定した時点で、エキスパートの地位を得た問題への参加を停止した場合 ( [スコアエンジンの設定](#configurable-scoring-engine)) エキスパートとしての地位を失う可能性があります。

高度なスコアの設定は、基本的なスコアとほぼ同じです。

* 基本的なスコアと高度なスコアおよびバッジルールは次のとおりです。 [コンテンツに適用済み](/help/communities/implementing-scoring.md#apply-rules-to-content) 同じ方法で

   * 基本スコアと高度なスコアおよびバッジルールを同じコンテンツに適用できます。

* [コンポーネントのバッジの有効化](/help/communities/implementing-scoring.md#enable-badges-for-component) は汎用です。

スコアルールとバッジルールの設定に違いは次のとおりです。

* 設定可能な高度なスコアエンジン
* 高度なスコアルール：

   * `scoringType` を `advanced` に設定
   * 次を必要とする `stopwords`

* 高度なバッジルール：

   * `badgingType` を `advanced` に設定
   * `badgingLevels` に設定 **賞に対する専門家レベルの数**
   * が必要 `badgingPaths` しきい値の代わりにバッジの配列配列のマッピングがバッジを指します。

>[!NOTE]
>
>高度なスコアおよびバッジ機能を使用するには、 [エキスパート特定パッケージ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq610%2Fsocial%2Ffeaturepack%2Fcq-social-expert-identification-pkg).

## 設定可能なスコアエンジン {#configurable-scoring-engine}

高度なスコアエンジンは、高度なスコアアルゴリズムに影響を与えるパラメーターを持つ OSGi 設定を提供します。

![advanced-scoring-engine](assets/advanced-scoring-engine.png)

* **スコア付けの重み付け**

  トピックの場合、スコアの計算時に最も優先度が高い動詞を指定します。 1 つ以上のトピックを入力できますが、次に限定されます **1 つの話題に対する 1 つの動詞**. 詳しくは、 [トピックと動詞](/help/communities/implementing-scoring.md#topics-and-verbs).
次の形式で入力 `topic,verb` コンマはエスケープされます。 次に例を示します。
  `/social/forum/hbs/social/forum\,ADD`
デフォルトでは、Q&amp;A とフォーラムコンポーネントの ADD 動詞が設定されています。

* **スコアリング範囲**

  高度なスコアの範囲は、この値（最大スコア）と 0（可能な限り低いスコア）で定義されます。

  デフォルト値は 100 なので、スコアリング範囲は 0 ～ 100 です。

* **エンティティのディケイ時間間隔**

  このパラメーターは、すべてのエンティティのスコアが低下するまでの時間数を表します。 これは、コミュニティサイトのスコアに古いコンテンツを含めなくなるために必要です。

  デフォルト値は216000時間（24 年以内）です。

* **スコア付け成長率**
この値は、0 からスコア範囲の間のスコアを指定します。この値を超えると、成長が遅くなり、エキスパートの数が制限されます。

  デフォルト値は 50 です。

## 高度なスコアルール {#advanced-scoring-rules}

基本スコアでは、バッジの獲得に必要な数がわかっています。

高度なスコアリングでは、必要な量は、システム内の品質データの量に基づいて、常に調整されます。 スコアは、ベルカーブと同様の方法で継続的に計算されます。

メンバーがアクティブでなくなったトピックに関するエキスパートバッジを獲得した場合、時間の経過と共に減衰が原因でバッジが失われる可能性があります。

### scoringType {#scoringtype}

スコア付けルールは、スコア付けサブルールのセットで、それぞれが `scoringType`.

高度なスコアエンジンを呼び出すには、 `scoringType`は次のように設定する必要があります。 `advanced`.

詳しくは、 [スコアサブルール](/help/communities/implementing-scoring.md#scoring-sub-rules).

![advanced-scoring-type](assets/advanced-scoring-type.png)

### ストップワード {#stopwords}

高度なスコアリングパッケージでは、stopwords ファイルを含む設定フォルダーがインストールされます。

* `/libs/settings/community/scoring/configuration/stopwords`

高度なスコアアルゴリズムは、ストップワードファイルに含まれる単語のリストを使用して、コンテンツの処理中に無視される一般的な英語の単語を識別します。

このファイルが変更される可能性はありません。

ストップワードファイルがない場合、高度なスコアエンジンによってエラーが発生します。

## 高度なバッジルール {#advanced-badging-rules}

高度なバッジルールのプロパティは、 [基本的なバッジルールのプロパティ](/help/communities/implementing-scoring.md#badging-rules).

ポイントをバッジ画像に関連付ける代わりに、許可されるエキスパートの数と、授与するバッジの画像を特定するだけで済みます。

![advanced-badging-rules](assets/advanced-badging-rules.png)

<table>
 <tbody>
  <tr>
   <th>プロパティ</th>
   <th>タイプ</th>
   <th>値の説明</th>
  </tr>
  <tr>
   <td>badgingPath</td>
   <td>String[]</td>
   <td><em>（必須）</em> badgingLevels の数までのバッジ画像の複数値文字列。 バッジ画像のパスを並べ替える必要があるので、最初の画像は最も高いエキスパートに与えられます。 badgingLevels で指定した数より少ないバッジがある場合、配列の最後のバッジが残りの配列を補完します。 エントリの例：<br /> <code>/libs/settings/community/badging/images/expert-badge/jcr:content/expert.png</code></td>
  </tr>
  <tr>
   <td>badgingLevels</td>
   <td>Long</td>
   <td><em>（オプション）</em> 与える専門知識のレベルを指定します。 例えば、 <code>expert </code>および <code>almost expert</code> （バッジが 2 つ）の場合、値は 2 に設定する必要があります。 badgingLevel は、badgingPath プロパティにリストされるエキスパート関連のバッジ画像の数に対応している必要があります。 初期設定は 1 です。</td>
  </tr>
  <tr>
   <td>badgingType</td>
   <td>文字列</td>
   <td><em>（必須）</em> スコアリングエンジンを「基本」または「詳細」として識別します。 "advanced"に設定し、それ以外の場合、デフォルトは"basic"です。</td>
  </tr>
  <tr>
   <td>scoringRules</td>
   <td>String[]</td>
   <td><em>（オプション）</em> リストされた 1 つ以上のスコアルールで識別されるスコアイベントにバッジルールを制限する複数値の文字列。<br /> エントリの例：<br /> <code>/libs/settings/community/scoring/rules/adv-comments-scoring</code><br /> デフォルトでは、制限はありません。</td>
  </tr>
 </tbody>
</table>

## 含まれるルールとバッジ {#included-rules-and-badge}

### 含まれるバッジ {#included-badge}

このベータリリースには、報酬ベースのエキスパートバッジが 1 つ含まれます。

* `expert`

  `/libs/settings/community/badging/images/expert-badge/jcr:content/expert.png`

![エキスパートバッジ](assets/included-badge.png)

エキスパートバッジをアクティビティへの報酬として表示するには、次の点を確認します。

* `Badges` は、フォーラムや Q&amp;A コンポーネントなどの機能に対して有効になっています。

* 高度なスコアルールとバッジルールは、コンポーネントが配置されているページ（または上位ページ）に適用されます

以下の基本情報を参照してください。

* [コンポーネントに対するバッジの有効化](/help/communities/implementing-scoring.md#enableforcomponent)
* [ルールの適用](/help/communities/implementing-scoring.md#applytopage)

### 含まれるスコアルールとサブルール {#included-scoring-rules-and-sub-rules}

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
* `subRules` は String 型の属性です`[]` 規則に従って `jcr:content` ノード。
* `sub-rules` は、様々なスコアリングルール間で共有できます。
* `rules` 全員に対する読み取り権限を持つリポジトリの場所に存在する必要があります。
* ルール名は、場所に関係なく一意である必要があります。

### 含まれるバッジルール {#included-badging-rules}

このリリースには、 [高度なフォーラムおよびコメントのスコアリングルール](#included-scoring-rules-and-sub-rules).

* `/libs/settings/community/badging/rules/adv-comments-badging`
* `/libs/settings/community/badging/rules/adv-forums-badging`

**メモ：**

* `rules` ノードのタイプは cq:Page です。
* `rules` 全員に対する読み取り権限を持つリポジトリの場所に存在する必要があります。
* ルール名は、場所に関係なく一意である必要があります。
