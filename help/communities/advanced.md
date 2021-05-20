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
role: Administrator
exl-id: d3bb6664-6c01-4bcf-840c-072fc491fc99
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 41%

---

# 高度なスコアとバッジ{#advanced-scoring-and-badges}

## 概要 {#overview}

高度なスコアを使用すると、メンバーをエキスパートとして識別するバッジを授与できます。高度なスコアでは、メンバーが作成したコンテンツの量&#x200B;*と*&#x200B;に基づいてポイントを割り当てます。一方、基本スコアでは、作成したコンテンツの量に基づいてポイントを割り当てます。

この違いは、スコアの計算に使用されるスコアエンジンによるものです。基本スコアエンジンは、単純な計算を適用します。 高度なスコアエンジンは、トピックの自然言語処理(NLP)を通じて推測される、価値のある関連性の高いコンテンツに貢献するアクティブなメンバーに報酬を与えるアダプティブなアルゴリズムです。

このスコアアルゴリズムでは、コンテンツの関連度に加え、投票や回答の割合など、メンバーのアクティビティが考慮されます。基本的なスコアには定量的に含まれますが、高度なスコアではアルゴリズム的に使用されます。

したがって、高度なスコアエンジンの分析を意味あるものにするには、十分なデータが必要です。作成されるコンテンツの量と品質に合わせてアルゴリズムが継続的に調整されるので、エキスパートになるための達成度のしきい値は、常に再評価されます。 メンバーの古い投稿の&#x200B;*decay*&#x200B;という概念もあります。 エキスパートメンバーが、事前に決めた時点でエキスパートステータスを得た主題への参加を停止すると（[スコアエンジン設定](#configurable-scoring-engine)を参照）、エキスパートとしての地位を失う可能性があります。

高度なスコアの設定方法は、基本スコアとほとんど同じです。

* 基本的なスコアと高度なスコアとバッジのルールは、同じ方法でコンテンツ](/help/communities/implementing-scoring.md#apply-rules-to-content)に[適用されます。

   * 基本的なスコアと高度なスコアとバッジのルールを同じコンテンツに適用できます。

* [コンポーネントのバッジを有](/help/communities/implementing-scoring.md#enable-badges-for-component) 効にすることは一般的です。

スコアルールおよびバッジルールの設定では、以下の点が異なります。

* 設定可能な高度なスコアエンジン
* 高度なスコアルール：

   * `scoringType` を `advanced` に設定
   * 次を必要とする `stopwords`

* 高度なバッジルール：

   * `badgingType` を `advanced` に設定
   * `badgingLevels`**を授与するエキスパートレベルの数に設定**
   * しきい値の配列とバッジのマッピングポイントの代わりに、バッジの`badgingPaths`配列が必要です。

>[!NOTE]
>
>高度なスコアおよびバッジ機能を使用するには、[エキスパートIDパッケージ](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/social/cq-social-expert-identification-pkg)をインストールします。

## 設定可能なスコアエンジン {#configurable-scoring-engine}

この高度なスコアエンジンには OSGi 設定が用意されており、パラメーターを設定して高度なスコアアルゴリズムを調整できます。

![高度なスコアエンジン](assets/advanced-scoring-engine.png)

* **スコア付けの重み**

   特定のトピックについて、スコア計算時に最も高い優先度を与える動詞を指定します。1つ以上のトピックを入力できますが、1つのトピック&#x200B;**につき**&#x200B;動詞に制限されます。 [トピックと動詞](/help/communities/implementing-scoring.md#topics-and-verbs)を参照してください。
コンマはエスケープして`topic,verb`と入力します。 以下に例を示します。
   `/social/forum/hbs/social/forum\,ADD`
デフォルトでは、Q&amp;Aとフォーラムコンポーネントの「ADD」動詞が設定されます。

* **スコア範囲**

   高度なスコアの範囲は、この値（可能な最大スコア）と0（可能な最小スコア）で定義されます。

   デフォルト値は 100 であり、スコア範囲は 0 ～ 100 となります。

* **エンティティのディケイ時間間隔**

   このパラメーターは、すべてのエンティティスコアが減衰されるまでの時間数を表します。 これは、コミュニティサイト上にある古いコンテンツをスコアに含めないようにするために必要な設定です。

   デフォルト値は 216000 時間（約 24 年）です。

* **スコア付け**
の増加率0 ～スコア範囲を指定します。この範囲を超えると、成長が遅くなり、エキスパートの数が制限されます。

   デフォルト値は 50 です。

## 高度なスコアルール {#advanced-scoring-rules}

基本スコアでは、バッジ獲得に必要な量はあらかじめ決まっています。

高度なスコアでは、システム内の上質なデータの量に基づいて、バッジ獲得に必要な量が継続的に調整されます。スコアは、ベルの曲線と同じ方法で継続的に計算されます。

メンバーがアクティブでなくなったトピックに関するエキスパートバッジを獲得した場合、時間の経過と共に減衰することでバッジが失われる可能性があります。

### scoringType {#scoringtype}

スコアルールは、スコアサブルールの集まりです。各サブルールは、それぞれ `scoringType` を宣言します。

高度なスコアエンジンを呼び出すには、`scoringType` を `advanced` に設定する必要があります。

[スコアサブルール](/help/communities/implementing-scoring.md#scoring-sub-rules)を参照してください。

![advanced-scoring-type](assets/advanced-scoring-type.png)

### ストップワーズ {#stopwords}

高度なスコアパッケージでは、ストップワードファイルを含む設定フォルダーがインストールされます。

* `/libs/settings/community/scoring/configuration/stopwords`

高度なスコアのアルゴリズムは、ストップワードファイルに含まれる単語のリストに基づいて、コンテンツ処理中に無視して構わない一般的な英単語を識別します。

このファイルが変更されることはありません。

ストップワードファイルが存在しない場合は、スコアエンジンによりエラーがスローされます。

## 高度なバッジルール  {#advanced-badging-rules}

高度なバッジルールのプロパティは、[基本バッジルールのプロパティ](/help/communities/implementing-scoring.md#badging-rules)とは異なります。

ポイントとバッジ画像を関連付ける必要はなく、許可するエキスパートの数と、授与するバッジ画像を指定するだけで十分です。

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
   <td><em>（必須）</em> badgingLevelsの数までのバッジ画像の複数値文字列。バッジ画像のパスを指定するときは、最も高いレベルのエキスパートに授与するものを最初に指定する必要があります。badgingLevels で指定された値よりもバッジの数が少ない場合、足りない部分には配列内の最終要素のバッジが使用されます。エントリ例：<br /> <code>/libs/settings/community/badging/images/expert-badge/jcr:content/expert.png</code></td>
  </tr>
  <tr>
   <td>badgingLevels</td>
   <td>Long</td>
   <td><em>（オプション）</em> 授与する専門知識のレベルを指定します。例えば、<code>expert </code>と<code>almost expert</code>（2つのバッジ）がある場合、値は2に設定する必要があります。 badgingLevelは、badgingPathプロパティにリストされるエキスパート関連のバッジ画像の数に対応している必要があります。 初期設定は 1 です。</td>
  </tr>
  <tr>
   <td>badgingType</td>
   <td>文字列</td>
   <td><em>（必須）</em> スコアエンジンを「basic」または「advanced」として識別します。「advanced」に設定すると、デフォルトは「basic」になります。</td>
  </tr>
  <tr>
   <td>scoringRules</td>
   <td>String[]</td>
   <td><em>（オプション）</em> バッジルールを、リストされたスコアルールで識別されるスコアイベントに制限する複数値文字列。<br /> エントリ例：<br /> <code>/libs/settings/community/scoring/rules/adv-comments-scoring</code><br /> デフォルトでは、制限はありません。</td>
  </tr>
 </tbody>
</table>

## このリリースに含まれるルールとバッジ {#included-rules-and-badge}

### このリリースに含まれるバッジ {#included-badge}

このベータリリースには、以下の報奨ベースのエキスパートバッジが含まれています。

* `expert`

   `/libs/settings/community/badging/images/expert-badge/jcr:content/expert.png`

![エキスパートバッジ](assets/included-badge.png)

エキスパートバッジをアクティビティの報酬として表示するには、次の点を確認します。

* `Badges` は、フォーラムやQ&amp;Aコンポーネントなどの機能に対して有効です。

* 高度なスコアルールとバッジルールは、コンポーネントが配置されているページ（または上位ページ）に適用されます

以下の基本情報を参照してください。

* [コンポーネントのバッジの有効化](/help/communities/implementing-scoring.md#enableforcomponent)
* [ルールの適用](/help/communities/implementing-scoring.md#applytopage)

### このリリースに含まれているスコアルールとサブルール {#included-scoring-rules-and-sub-rules}

ベータリリースには、[フォーラム機能](/help/communities/functions.md#forum-function)用の2つの高度なスコアルールが含まれています（それぞれフォーラム機能のフォーラムコンポーネントとコメントコンポーネント用）。

1. `/libs/settings/community/scoring/rules/adv-comments-scoring`

   * `subRules[] =
/libs/settings/community/scoring/rules/sub-rules/adv-comments-rule
/libs/settings/community/scoring/rules/sub-rules/adv-voting-rule-owner
/libs/settings/community/scoring/rules/sub-rules/adv-voting-rule`

1. `/libs/settings/community/scoring/rules/adv-forums-scoring`

   * `subRules[] =
/libs/settings/community/scoring/rules/sub-rules/adv-forums-rule
/libs/settings/community/scoring/rules/sub-rules/adv-comments-rule
/libs/settings/community/scoring/rules/sub-rules/adv-voting-rule-owner`

**備考:**

* `rules`ノードと`sub-rules`ノードの型は`cq:Page`です。

* `subRules` は、ルールのノード[] のString型の属性 `jcr:content` です。

* `sub-rules` は、様々なスコアルールで共有できます。

* `rules` は、リポジトリの場所に配置され、全員に対して読み取り権限が付与されます。

* ルール名は、場所に関係なく一意である必要があります。

### このリリースに含まれるバッジルール {#included-badging-rules}

このリリースには、[高度なフォーラムとコメントスコアルール](#included-scoring-rules-and-sub-rules)に対応する2つの高度なバッジルールが含まれています。

* `/libs/settings/community/badging/rules/adv-comments-badging`
* `/libs/settings/community/badging/rules/adv-forums-badging`

**備考:**

* `rules` ノードのタイプはcq:Pageです。
* `rules` は、リポジトリの場所に配置され、全員に対して読み取り権限が付与されます。
* ルール名は、場所に関係なく一意である必要があります。
