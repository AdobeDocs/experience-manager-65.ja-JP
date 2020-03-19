---
title: 高度なスコアとバッジ
seo-title: 高度なスコアとバッジ
description: 高度なスコアの設定
seo-description: 高度なスコアの設定
uuid: 48caca57-43d3-4f2f-adf3-257428ba54d5
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: eb3d5c37-8097-46de-8c4f-804ea723f1c5
docset: aem65
translation-type: tm+mt
source-git-commit: 974d58efa560b90234d5121a11bdb445c7bf94cf

---


# 高度なスコアとバッジ{#advanced-scoring-and-badges}

## 概要 {#overview}

高度なスコアを使用すると、メンバーをエキスパートとして識別するバッジを授与できます。Advanced scoring assigns points based on the quantity *and* quality of content created by a member, whereas basic scoring assigns points simply based on the quantity of content created.

この違いは、スコアの計算に使用されるスコアエンジンによるものです。基本スコアリングエンジンは、単純な計算を適用します。 アドバンススコアリングエンジンは、トピックの自然言語処理(NLP)を通じて導き出される、価値の高い関連コンテンツに貢献するアクティブなメンバーに報酬を与えるアダプティブアルゴリズムです。

このスコアアルゴリズムでは、コンテンツの関連度に加え、投票や回答の割合など、メンバーのアクティビティが考慮されます。基本スコアには定量的なものも含まれますが、高度なスコアではアルゴリズム的に使用されます。

したがって、高度なスコアエンジンの分析を意味あるものにするには、十分なデータが必要です。エキスパートになるための達成のしきい値は、作成されたコンテンツの量と品質にアルゴリズムが継続的に調整されるので、常に再評価されます。 There is also a concept of *decay* of a member&#39;s older posts. If an expert member stops participating in the subject matter where they gained expert status, at some pre-determined point (see [scoring engine configuration](#configurable-scoring-engine)) they could lose their status as an expert.

高度なスコアの設定方法は、基本スコアとほとんど同じです。

* Basic and advanced scoring and badging rules are [applied to content](/help/communities/implementing-scoring.md#apply-rules-to-content) in the same manner

   * 基本および高度なスコアおよびバッジルールを同じコンテンツに適用できます。

* [コンポーネントのバッジの有効化](/help/communities/implementing-scoring.md#enable-badges-for-component) ：汎用

スコアルールおよびバッジルールの設定では、以下の点が異なります。

* 設定可能な高度なスコアリングエンジン
* 高度なスコアリングルール：

   * `scoringType` 設定 `advanced`
   * 必須 `stopwords`

* 詳細なバッジルール：

   * `badgingType` 設定 `advanced`
   * `badgingLevels`**を授与するエキスパートレベルの数に設定**
   * requires `badgingPaths` array of badges instead of thresholds array mapping points to badges

>[!NOTE]
>
>高度なスコアおよびバッジ機能を使用するには、エキスパートIDパッ [ケージをインストールしま](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/social/cq-social-expert-identification-pkg)す。

## 設定可能なスコアエンジン {#configurable-scoring-engine}

この高度なスコアエンジンには OSGi 設定が用意されており、パラメーターを設定して高度なスコアアルゴリズムを調整できます。

![chlimage_1-139](assets/chlimage_1-139.png)

* **スコアリングの重み**

   特定のトピックについて、スコア計算時に最も高い優先度を与える動詞を指定します。One or more topics may be entered, but limited to **one verb per topic**. See [Topics and Verbs](/help/communities/implementing-scoring.md#topics-and-verbs).
コンマはエスケープさ `topic,verb` れたとおりに入力されます。 次に例を示します。
   `/social/forum/hbs/social/forum\,ADD`
デフォルトは、QnAおよびフォーラムコンポーネントのADD動詞に設定されます。

* **スコアリング範囲**

   高度なスコアの範囲は、この値（可能な最大スコア）と0（可能な最小スコア）で定義されます。

   デフォルト値は 100 であり、スコア範囲は 0 ～ 100 となります。

* **エンティティの減衰時間間隔**

   このパラメーターは、すべてのエンティティスコアがディケードされる時間数を表します。 これは、コミュニティサイト上にある古いコンテンツをスコアに含めないようにするために必要な設定です。

   デフォルト値は 216000 時間（約 24 年）です。

* **スコアの増加率**:0からスコアの範囲でスコアを指定します。この範囲を超えると、成長速度が遅くなり、エキスパートの数が制限されます。

   デフォルト値は 50 です。

## 高度なスコアルール {#advanced-scoring-rules}

基本スコアでは、バッジ獲得に必要な量はあらかじめ決まっています。

高度なスコアでは、システム内の上質なデータの量に基づいて、バッジ獲得に必要な量が継続的に調整されます。スコアリングは、ベル曲線と同様の方法で連続的に計算されます。

メンバーが、アクティブでなくなったトピックに関するエキスパートバッジを得た場合、時間の経過と共に減少するためにバッジを失う可能性があります。

### scoringType {#scoringtype}

スコアルールは、スコアサブルールの集まりです。各サブルールは、それぞれ `scoringType` を宣言します。

高度なスコアエンジンを呼び出すには、`scoringType` を `advanced` に設定する必要があります。

[スコアサブルール](/help/communities/implementing-scoring.md#scoring-sub-rules)を参照してください。

![chlimage_1-140](assets/chlimage_1-140.png)

### Stopwords {#stopwords}

高度なスコアパッケージでは、ストップワードファイルを含む設定フォルダーがインストールされます。

* `/etc/community/scoring/configuration/stopwords`

高度なスコアのアルゴリズムは、ストップワードファイルに含まれる単語のリストに基づいて、コンテンツ処理中に無視して構わない一般的な英単語を識別します。

このファイルが変更されることはありません。

ストップワードファイルが存在しない場合は、スコアエンジンによりエラーがスローされます。

## 高度なバッジルール {#advanced-badging-rules}

高度なバッジルールのプロパティは、[基本バッジルールのプロパティ](/help/communities/implementing-scoring.md#badging-rules)とは異なります。

ポイントとバッジ画像を関連付ける必要はなく、許可するエキスパートの数と、授与するバッジ画像を指定するだけで十分です。

![chlimage_1-141](assets/chlimage_1-141.png)

<table>
 <tbody>
  <tr>
   <th>プロパティ</th>
   <th>タイプ</th>
   <th>値 説明</th>
  </tr>
  <tr>
   <td>badgingPath</td>
   <td>文字列[]</td>
   <td><em>（必須）</em> 、badgingLevelsの数までのバッジ画像の複数値の文字列。 バッジ画像のパスを指定するときは、最も高いレベルのエキスパートに授与するものを最初に指定する必要があります。badgingLevels で指定された値よりもバッジの数が少ない場合、足りない部分には配列内の最終要素のバッジが使用されます。エントリの例：<br /> <code>/etc/community/badging/images/expert-badge/jcr:content/expert.png</code></td>
  </tr>
  <tr>
   <td>badgingLevels</td>
   <td>Long</td>
   <td><em>（オプション）</em> 、認定する専門知識のレベルを指定します。 For example, if there should be an <code>expert </code>and an <code>almost expert</code> (two badges), then the value should be set to 2. badgingLevelは、badgingPathプロパティに対してリストされたエキスパート関連のバッジ画像の数に対応する必要があります。 初期設定は 1 です。</td>
  </tr>
  <tr>
   <td>badgingType</td>
   <td>文字列</td>
   <td><em>（必須）</em> 「基本」または「詳細」としてスコアリングエンジンを識別します。 「advanced」に設定すると、デフォルトは「basic」になります。</td>
  </tr>
  <tr>
   <td>scoringRules</td>
   <td>文字列[]</td>
   <td><em>（オプション）</em> 、リストに表示されたスコアリングルールで識別されるスコアリングイベントにバッジルールを制限する複数値の文字列。<br /> エントリの例：<br /> 初期設 <code>/etc/community/scoring/rules/adv-comments-scoring</code><br /> 定では、制限はありません。</td>
  </tr>
 </tbody>
</table>

## このリリースに含まれるルールとバッジ {#included-rules-and-badge}

### このリリースに含まれるバッジ {#included-badge}

このベータリリースには、以下の報奨ベースのエキスパートバッジが含まれています。

* `expert`

   `/etc/community/badging/images/expert-badge/jcr:content/expert.png`

![chlimage_1-142](assets/chlimage_1-142.png)

エキスパートバッジがアクティビティの報酬として表示されるようにするには、次の点を確認します。

* `Badges` が有効になっているかどうかを確認します。

* 高度なスコアリングとバッジルールは、コンポーネントが配置されるページ（または上位）に適用されます

次の基本情報を参照してください。

* [コンポーネントのバッジの有効化](/help/communities/implementing-scoring.md#enableforcomponent)
* [ルールの適用](/help/communities/implementing-scoring.md#applytopage)

### このリリースに含まれているスコアルールとサブルール {#included-scoring-rules-and-sub-rules}

Included in the beta release are two advanced scoring rules for the [forum function](/help/communities/functions.md#forum-function) (one each for the forum and comments components of the forum feature):

1. `/etc/community/scoring/rules/adv-comments-scoring`

   * `subRules[] =
/etc/community/scoring/rules/sub-rules/adv-comments-rule
/etc/community/scoring/rules/sub-rules/adv-voting-rule-owner
/etc/community/scoring/rules/sub-rules/adv-voting-rule`

1. `/etc/community/scoring/rules/adv-forums-scoring`

   * `subRules[] =
/etc/community/scoring/rules/sub-rules/adv-forums-rule
/etc/community/scoring/rules/sub-rules/adv-comments-rule
/etc/community/scoring/rules/sub-rules/adv-voting-rule-owner`

**注意：**

* Both `rules`and `sub-rules` nodes are of type `cq:Page`

* `subRules`は、ルールのノード上のString[] 型の属性で `jcr:content` す

* `sub-rules` は、複数のスコアルール間で共有できます。

* `rules` は、リポジトリ内の誰でも読み取れる場所に配置する必要があります。

   * ルール名は場所に関係なく一意である必要があります

### このリリースに含まれるバッジルール {#included-badging-rules}

Included in the release are two advanced badging rules that correspond to the [advanced forums and comments scoring rules](#included-scoring-rules-and-sub-rules).

* `/etc/community/badging/rules/adv-comments-badging`
* `/etc/community/badging/rules/adv-forums-badging`

**注意：**

* `rules` のノードは、cq:Page タイプです。
* `rules` は、リポジトリ内の誰でも読み取れる場所に配置する必要があります。

   * ルール名は場所に関係なく一意である必要があります

