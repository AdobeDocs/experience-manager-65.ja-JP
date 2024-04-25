---
title: コミュニティのスコアとバッジ
description: AEM Communitiesのスコアとバッジを使用すると、コミュニティメンバーを識別して報酬を付与できます
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
tagskeywords: scoring, badging, badges, gamification
role: Admin
exl-id: 4aa857f7-d111-4548-8f03-f6d6c27acf51
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '2856'
ht-degree: 3%

---

# コミュニティのスコアとバッジ {#communities-scoring-and-badges}

## 概要 {#overview}

AEM Communitiesのスコアおよびバッジ機能を使用すると、コミュニティメンバーを特定して報酬を付与できます。

スコアとバッジの主な側面は次のとおりです。

* [バッジを割り当て](#assign-and-revoke-badges) コミュニティにおけるメンバーの役割を識別する。

* [バッジの基本的な授与](#enable-scoring) メンバーに参加を促す場合（作成されるコンテンツの量）。

* [バッジの事前授与](/help/communities/advanced.md) メンバーをエキスパートとして特定します（作成されたコンテンツの品質）。

**注意** バッジの授与は [デフォルトでは有効になっていません](/help/communities/implementing-scoring.md#main-pars-text-237875536).

>[!CAUTION]
>
>CRXDE Liteに表示される実装構造は、UI が使用可能になると変更される場合があります。

## バッジ {#badges}

バッジはメンバーの名前の下に配置され、メンバーの役割またはコミュニティ内での地位を示します。 バッジは、画像または名前として表示できます。 画像として表示される場合、名前はアクセシビリティの代替テキストとして含まれます。

デフォルトでは、バッジは次の場所にあるリポジトリに格納されます。

* `/libs/settings/community/badging/images`

別の場所に保存されている場合は、すべてのユーザーがアクセス可能な状態で読み取る必要があります。

バッジは、ルールに従って割り当てられたか、獲得したかに応じて、UGC で区別されます。 現在、割り当てられたバッジはテキストとして表示され、獲得したバッジは画像として表示されます。

### バッジ管理 UI {#badge-management-ui}

コミュニティ [バッジコンソール](/help/communities/badges.md) メンバーが獲得（授与）した場合や、コミュニティで特定の役割を担った（割り当てられた）場合に表示できるカスタムバッジを追加できます。

### 割り当て済みバッジ {#assigned-badges}

役割ベースのバッジは、コミュニティ内の役割に基づいて、管理者がコミュニティメンバーに割り当てます。

割り当てられた（および付与された）バッジは、選択されたに保存されます [SRP](/help/communities/srp.md) とに直接アクセスすることはできません。 GUI が使用可能になるまで、役割ベースのバッジを割り当てる唯一の手段は、コードまたは cURL を使用することです。 cURL の手順については、というタイトルの節を参照してください。 [バッジの割り当てと失効](#assign-and-revoke-badges).

リリースには、役割ベースのバッジが 3 つ含まれています。

* **調整者**
  `/libs/settings/community/badging/images/moderator/jcr:content/moderator.png`

* **グループ管理者**
  `/libs/settings/community/badging/images/group-manager/jcr:content/group-manager.png`

* **特権メンバー**
  `/libs/settings/community/badging/images/privileged-member/jcr:content/privileged-member.png`

  ![assigned-badges](assets/assigned-badges.png)

### 審査済みバッジ {#awarded-badges}

報酬ベースのバッジは、コミュニティ内のメンバーのアクティビティに適用されるルールに基づいて、スコアリングサービスによってコミュニティメンバーに付与されます。

アクティビティの報酬としてバッジが表示されるようにするには、次の 2 つの処理を行う必要があります。

* バッジはでなければなりません [enabled](#enableforcomponent) 機能コンポーネントの場合。
* スコアおよびバッジルールは次の条件を満たす必要があります [適用日時](#applytopage) コンポーネントが配置されているページ（または上位）に移動します。

リリースには、報酬ベースのバッジが 3 つ含まれています。

* **ゴールド**
  `/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png`

* **シルバー**
  `/libs/settings/community/badging/images/silver-badge/jcr:content/silver.png`

* **ブロンズ**
  `/libs/settings/community/badging/images/bronze-badge/jcr:content/bronze.png`

  ![授与されたバッジ](assets/awarded-badges.png)

>[!NOTE]
>
>スコア ルールは、不適切とフラグ付けされた投稿に負のポイントを割り当てるように設定され、スコア値に影響を与える場合があります。 ただし、バッジを獲得しても、スコアポイントの減少やスコアルールの変更が原因で、自動的に削除されることはありません。
>
>授与されたバッジは、割り当てられたバッジと同じ方法で取り消すことができます。 を参照してください。 [バッジの割り当てと失効](#assign-and-revoke-badges) セクション。 今後の機能強化には、メンバーのバッジを管理する UI が含まれる予定です。

### カスタムバッジ {#custom-badges}

カスタムバッジは、 [バッジコンソール](/help/communities/badges.md) また、バッジルールに割り当てまたは指定します。

バッジコンソールからインストールすると、カスタムバッジがパブリッシュ環境に自動的に複製されます。

## スコアリングを有効にする {#enable-scoring}

スコアリングは、デフォルトでは有効になっていません。 バッジのスコアリングと授与を設定して有効にするための基本的な手順は次のとおりです。

* ポイントを獲得するためのルールを識別する（[スコアルール](#scoring-rules)）に設定します。
* スコアリング・ルールごとに累積されるポイントの割当て [バッジ](#badges) （[バッジルール](#badging-rules)）に設定します。

* [コミュニティサイトへのスコアおよびバッジルールの適用](#apply-rules-to-content).
* [コミュニティ機能のバッジを有効にする](#enable-badges-for-component).

を参照してください。 [クイックテスト](#quick-test) フォーラムとコメントのデフォルトのスコアおよびバッジルールを使用してコミュニティサイトのスコアリングを有効にする節です。

### コンテンツへのルールの適用 {#apply-rules-to-content}

スコアおよびバッジを有効にするには、以下のプロパティを追加します `scoringRules` および `badgingRules` をサイトのコンテンツツリー内の任意のノードに追加します。

サイトが既に公開されている場合は、すべてのルールを適用してコンポーネントを有効にした後、サイトを再公開します。

バッジが有効になっているコンポーネントに適用されるルールは、現在のノードまたはその上位のノードのルールです。

ノードのタイプがの場合 `cq:Page` （推奨） CRXDE|Lite を使用して、のプロパティをに追加します `jcr:content` ノード。

| **プロパティ** | **タイプ** | **説明** |
|---|---|---|
| badgingrules | 文字列 | の配列リスト [バッジルール](#badging-rules) |
| scoringRules | 文字列 | の配列リスト [スコアルール](#scoring-rules) |

>[!NOTE]
>
>スコアルールがバッジの獲得に影響を与えていないようであれば、そのスコアルールがバッジルールの scoringRules プロパティによってブロックされていないことを確認してください。 というタイトルのセクションを参照してください。 [バッジルール](#badging-rules).

### コンポーネントのバッジを有効にする {#enable-badges-for-component}

スコアおよびバッディングルールは、でコンポーネント設定を編集することでバッジを有効にしているコンポーネントのインスタンスに対してのみ有効になります [オーサリングモード](/help/communities/author-communities.md).

ブール値プロパティ、 `allowBadges`、コンポーネントインスタンスのバッジの表示を有効または無効にします。 で設定できます [コンポーネント編集ダイアログ](/help/communities/author-communities.md) というラベルの付いたチェックボックスを使用したフォーラム、QnA、コメントのコンポーネント **バッジを表示**.

#### 例：フォーラムコンポーネントインスタンスの allowBadges {#example-allowbadges-for-forum-component-instance}

![enable-badges-component](assets/enable-badges-component.png)

>[!NOTE]
>
>フォーラム、QnA およびコメントにある HBS コードを例として使用して、任意のコンポーネントをオーバーレイしてバッジを表示できます。

## スコアルール {#scoring-rules}

スコアルールは、バッジを付与するためのスコアリングの基礎です。

各スコアルールは、1 つ以上のサブルールのリストです。 スコアルールは、バッジが有効な場合に適用するルールを識別するために、コミュニティサイトのコンテンツに適用されます。

スコアルールは継承されますが、加算はできません。 次に例を示します。

* page2 にスコアリング・ルール 2 が含まれ、その上位 page1 にスコアリング・ルール 1 が含まれる場合。
* page2 コンポーネントに対するアクションは、rule1 と rule2 の両方を呼び出します。
* 両方のルールに、同じルールに適用可能なサブルールが含まれる場合 `topic/verb`:

   * ルール 2 のサブルールのみがスコアに影響します。
   * 両方のサブルールのスコアは追加されません。

複数のスコアルールがある場合、スコアはルールごとに別々に維持されます。

スコアルールは、タイプのノードです `cq:Page` プロパティが設定されたアセット `jcr:content` サブルールを定義するサブルールのリストを指定するノード。

スコアは SRP に保存されます。

>[!NOTE]
>
>ベストプラクティス：各スコアルールに一意の名前を付けます。
>
>スコアルール名は、グローバルに一意である必要があります。また、末尾に同じ名前を付けることはできません。
>
>例えば、 *ではない* 手順は次のとおりです。
>
>/libs/settings/community/scoring/rules/site1/forums-scoring
>/libs/settings/community/scoring/rules/site2/forums-scoring

### スコアリングサブルール {#scoring-sub-rules}

スコアリングサブルールには、コミュニティに参加するための値の詳細を示すプロパティが含まれています。

各スコアリング・サブルールは、次の項目を識別します。

* 追跡されているアクティビティは何ですか？
* 関与するコミュニティ機能の具体的な種類
* 何点が付与されますか？

デフォルトでは、サブルールでコンテンツの所有者にポイントの付与が指定されていない限り、アクションを実行したメンバーにポイントが付与されます（ `forOwner`）に設定します。

各サブルールは、1 つ以上のスコアルールに含めることができます。

サブルールの名前は、通常、 *件名*, *オブジェクト*、および *動詞*. 次に例を示します。

* member-comment-create
* 会員が投票する

サブルールはタイプのノードです `cq:Page` プロパティが設定されたアセット `jcr:content`を指定するノード [動詞とトピック](#topics-and-verbs) .

<table>
 <tbody>
  <tr>
   <th>Property</th>
   <th>タイプ</th>
   <th> 値の説明</th>
  </tr>
  <tr>
   <td><i><code>VERB</code></i></td>
   <td>Long</td>
   <td>
    <ul>
     <li>必須。動詞はイベント アクションに対応します</li>
     <li>少なくとも 1 つの動詞プロパティが必要です</li>
     <li>動詞はすべて大文字で入力する必要があります</li>
     <li>複数の動詞プロパティを指定できますが、重複はありません</li>
     <li>値は、このイベントに適用するスコアです</li>
     <li>正または負の値を指定できます</li>
     <li>このリリースでサポートされている動詞のリストは <a href="#topics-and-verbs">トピックと動詞</a> セクション</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>topics</code></td>
   <td>文字列</td>
   <td>
    <ul>
     <li>オプション。サブルールを、イベントのトピックで識別されるコミュニティコンポーネントに制限します。</li>
     <li>指定された場合：値はイベントトピックの複数値文字列です</li>
     <li>このリリースのトピックのリストは、 <a href="#topics-and-verbs">トピックと動詞</a> セクション</li>
     <li>既定では、動詞に関連付けられたすべてのトピックに適用されます</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>forOwner</code></td>
   <td>ブーリアン</td>
   <td>
    <ul>
     <li>オプション。メンバーが所有するコンテンツに対してアクションを実行する場合は関係なし</li>
     <li>true の場合、アクションの対象となるコンテンツの所有者にスコアを適用</li>
     <li>false の場合、アクションを実行するメンバーにスコアを適用します</li>
     <li>デフォルトは false です</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>scoringType</code></td>
   <td>文字列</td>
   <td>
    <ul>
     <li>オプション。スコアリングエンジンを識別します</li>
     <li>「基本」の場合、数量に基づくスコアリング・エンジンを指定します
      <ul>
       <li>このリリースに含まれる</li>
      </ul> </li>
     <li>「詳細」の場合、品質と数量に基づいてスコアリング・エンジンを指定します
      <ul>
       <li>が必要 <a href="/help/communities/advanced.md">追加パッケージ</a></li>
      </ul> </li>
     <li>デフォルトは「basic」です</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### スコアルールとサブルールを含む {#included-scoring-rules-and-sub-rules}

リリースには、次の 2 つのスコアルールが含まれています [フォーラム機能](/help/communities/functions.md#forum-function) （フォーラム機能のフォーラム コンポーネントとコメント コンポーネントごとに 1 つ）。

1. /libs/settings/community/scoring/rules/comments-scoring

   * subRules[] = /libs/settings/community/scoring/rules/sub-rules/member-comment-create /libs/settings/community/scoring/rules/sub-rules/member-receive-vote /libs/settings/community/scoring/rules/sub-rules/member-give-vote /libs/settings/community/scoring/rules/sub-rules/member-is-moderated

1. /libs/settings/community/scoring/rules/forums-scoring

   * subRules[] = /libs/settings/community/scoring/rules/sub-rules/member-forum-create /libs/settings/community/scoring/rules/sub-rules/member-receive-vote /libs/settings/community/scoring/rules/sub-rules/member-give-vote /libs/settings/community/scoring/rules/sub-rules/member-is-moderated

**メモ：**

* 両方 `rules` および `sub-rules` ノードのタイプは cq:Page です。

* `subRules` は、文字列型の属性です[] 規則に従って `jcr:content` ノード。

* `sub-rules` 様々なスコアルールで共有できます。
* `rules` は、すべてのユーザーに対して読み取り権限を持つリポジトリの場所にある必要があります。

   * ルール名は、場所に関係なく一意である必要があります。

### カスタムスコアルールの有効化 {#activating-custom-scoring-rules}

オーサー環境で行われたスコアルールまたはサブルールに対する変更や追加は、パブリッシュ環境にインストールする必要があります。

## バッジルール {#badging-rules}

バッジルールは、次のように指定して、スコアルールをバッジにリンクします。

* スコアルール
* 特定のバッジを授与されるために必要なスコア

バッジルールは、タイプのノードです `cq:Page` プロパティが設定されたアセット `jcr:content` スコアルールをスコアおよびバッジに関連付けるノード。

バッジのルールは必須で構成されています `thresholds` バッジにマッピングされたスコアの順序付きリストであるプロパティ。 スコアは、値を増やして並べ替える必要があります。 次に例を示します。

* `1|/libs/settings/community/badging/images/bronze-badge/jcr:content/bronze.png`

   * ブロンズバッジは 1 点獲得で獲得できます。

* `60|/libs/settings/community/badging/images/silver-badge/jcr:content/silver.png`

   * シルバーバッジは 60 ポイント貯まると付与されます。

* `80|/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png`

   * 80 ポイントがたまったらゴールドバッジが付与されます。

バッジルールは、ポイントの蓄積方法を決定するスコアルールとペアになっています。 というタイトルのセクションを参照してください。 [コンテンツへのルールの適用](#apply-rules-to-content).

この `scoringRules` バッジルールのプロパティは、その特定のバッジルールとペアにできるスコアルールを制限するだけです。

>[!NOTE]
>
>ベストプラクティス：各AEM サイトに固有のバッジ画像を作成します。

![badging-rule-configuration](assets/badging-rule-configuration.png)

<table>
 <tbody>
  <tr>
   <th>Property</th>
   <th>タイプ</th>
   <th>値の説明</th>
  </tr>
  <tr>
   <td>しきい値</td>
   <td>文字列</td>
   <td><em>（必須）</em> 'number|path'形式の複数値文字列
    <ul>
     <li>数値= スコア</li>
     <li>| =縦線の文字（U+007C）</li>
     <li>path = バッジ画像リソースのフルパス</li>
    </ul> 文字列は、数値が値で増加し、数値とパスの間に空白が表示されないように順序付ける必要があります。<br /> エントリの例：<br /> <code>80|/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png</code></td>
  </tr>
  <tr>
   <td>badgingType</td>
   <td>文字列</td>
   <td><em>（オプション）</em> スコアリングエンジンを「基本」または「詳細」として識別します。 高度なスコアリング・エンジンが必要な場合は、を参照してください <a href="/help/communities/advanced.md">高度なスコアとバッジ</a>. デフォルトは「basic」です。</td>
  </tr>
  <tr>
   <td>scoringRules</td>
   <td>文字列</td>
   <td>（<em>optional</em>）スコアルールで識別されるスコアリングイベントにバッジルールを制限するための複数値文字列</td>
  </tr>
 </tbody>
</table>

### 含まれるバッジルール {#included-badging-rules}

リリースには、に対応する 2 つのバッジルールが含まれています [フォーラムとコメントのスコアルール](#includedscoringrules).

* `/libs/settings/community/badging/rules/comments-badging`

* `/libs/settings/community/badging/rules/forums-badging`

**メモ：**

* `rules` ノードのタイプは cq:Page です。
* `rules` は、すべてのユーザーに対して読み取り権限を持つリポジトリの場所にある必要があります。

   * ルール名は、場所に関係なく一意である必要があります。

### カスタムバッジルールのアクティブ化 {#activating-custom-badging-rules}

オーサー環境で行われたバッジルールまたは画像の変更や追加は、すべてパブリッシュ環境にインストールする必要があります。

## バッジの割り当てと取り消し {#assign-and-revoke-badges}

バッジは、次のいずれかを使用してメンバーに割り当てることができます [メンバーコンソール](/help/communities/members.md#badges-tab) または、cURL コマンドをプログラムで使用した場合も同様です。

次の cURL コマンドは、バッジの割り当てと取り消しに関する HTTP リクエストに必要な操作を示しています。 基本的な形式は次のとおりです。

cURL -i -X POST -H *ヘッダー* -u *サインイン* -F *操作* -F *バッジ* *member-profile-url*

*ヘッダー* = &quot;Accept:application/json&quot; カスタムヘッダーをサーバーに渡す（必須）

*サインイン* =管理者 id：パスワード（例：admin:admin）

*操作* = &quot;:operation=social:assignBadge&quot;または&quot;:operation=social:deleteBadge&quot;

*バッジ* = &quot;badgeContentPath=*badge-image-file*“

*badge-image-file* =リポジトリ内のバッジ画像ファイルの場所（例：/libs/settings/community/badging/images/moderator/jcr:content/moderator.png）

*member-profile-url* =公開時のメンバーのプロファイルのエンドポイント（例：https://）&lt;server>:&lt;port>/home/users/community/riley/profile.social.json

>[!NOTE]
>
>この *member-profile-url*:
>
>* 次の場合は、オーサーインスタンスを参照できます [トンネルサービス](/help/communities/users.md#tunnel-service) が有効になっています。
>* 不明瞭でランダムな名前である可能性があります。を参照してください。 [セキュリティチェックリスト](/help/sites-administering/security-checklist.md#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path) 認証可能な ID に関する。

### 例： {#examples}

#### モデレータバッジを割り当てる {#assign-a-moderator-badge}

```shell
curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:assignBadge" -F "badgeContentPath=/libs/settings/community/badging/images/moderator/jcr:content/moderator.png" /home/users/community/updcs9DndLEI74DB9zsB/profile.social.json
```

#### 割り当てられたシルバーバッジの取り消し {#revoke-an-assigned-silver-badge}

```shell
curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:deleteBadge" -F "badgeContentPath=/libs/settings/community/badging/images/silver/jcr:content/silver.png" /home/users/community/updcs9DndLEI74DB9zsB/profile.social.json
```

>[!NOTE]
>
>cURL を使用したバッジの割り当てと取り消しは、どのバッジ画像にも機能しますが、獲得ではなく割り当てられると、割り当てられたバッジとしてマークされ、それに応じて処理されます。

## カスタムコンポーネントのスコアとバッジ {#scoring-and-badges-for-custom-components}

コンポーネント用に作成したイベントトピックを動詞に関連付けることで、カスタムコンポーネントのスコアおよびバッジルールを作成できます。

## トピックと動詞 {#topics-and-verbs}

メンバーがコミュニティの機能を操作すると、通知やスコアリングなどの非同期リスナーをトリガーにできるイベントが送信されます。

コンポーネントの SocialEvent インスタンスは、イベントをとして記録します `actions` ～に起こる `topic`. SocialEvent には、 `verb` アクションに関連付けられます。 次のものがあります *n-1* ～間の関係 `actions` および `verbs`.

提供されるコミュニティコンポーネントについて、次の表で説明します `verbs` それぞれに定義済み `topic` ～で利用できる [スコアリングサブルール](#scoring-sub-rules).

>[!NOTE]
>
>新規ブール値プロパティ、 `allowBadges`、コンポーネントインスタンスのバッジの表示を有効または無効にします。 更新後はで設定可能です [コンポーネント編集ダイアログ](/help/communities/author-communities.md) というラベルの付いたチェックボックスを使用 **バッジを表示**.

**[カレンダーコンポーネント](/help/communities/calendar.md)**
SocialEvent `topic`= com/adobe/cq/social/calendar

| **動詞** | **説明** |
|---|---|
| POST | メンバーがカレンダーイベントを作成します |
| 追加 | カレンダーイベントに対するメンバーコメント |
| 更新 | メンバーのカレンダーイベントまたはコメントが編集されたとき |
| 削除 | メンバーのカレンダーイベントまたはコメントが削除されました |

**[コメントコンポーネント](/help/communities/comments.md)**
SocialEvent `topic`= com/adobe/cq/social/comment

| **動詞** | **説明** |
|---|---|
| POST | メンバーがコメントを作成 |
| 追加 | メンバーのコメントへの返信 |
| 更新 | メンバーのコメントが編集されました |
| 削除 | メンバーのコメントが削除されました |

**[ファイルライブラリコンポーネント](/help/communities/file-library.md)**
SocialEvent `topic`= com/adobe/cq/social/fileLibrary

| **動詞** | **説明** |
|---|---|
| POST | メンバーがフォルダーを作成します |
| 添付 | メンバーがファイルをアップロードする |
| 更新 | メンバーによるフォルダーまたはファイルの更新 |
| 削除 | メンバーがフォルダーまたはファイルを削除します |

**[フォーラムコンポーネント](/help/communities/forum.md)**
SocialEvent `topic`= com/adobe/cq/social/forum

| **動詞** | **説明** |
|---|---|
| POST | メンバーがフォーラムトピックを作成 |
| 追加 | フォーラムトピックに対するメンバーの返信 |
| 更新 | メンバーのフォーラムトピックまたは返信が編集された |
| 削除 | メンバーのフォーラムトピックまたは返信が削除されました |

**[ジャーナルコンポーネント](/help/communities/blog-feature.md)**
SocialEvent `topic`= com/adobe/cq/social/journal

| **動詞** | **説明** |
|---|---|
| POST | メンバーがブログ記事を作成します |
| 追加 | ブログ記事に対するメンバーコメント |
| 更新 | メンバーのブログ記事またはコメントが編集されました |
| 削除 | メンバーのブログ記事またはコメントが削除されました |

**[QnA コンポーネント](/help/communities/working-with-qna.md)**
SocialEvent `topic` = com/adobe/cq/social/qna

| **動詞** | **説明** |
|---|---|
| POST | メンバーが QnA 質問を作成します |
| 追加 | メンバーが QnA 回答を作成 |
| 更新 | メンバーの QnA 質問または回答が編集されました |
| を選択 | メンバーの回答が選択されました |
| 選択解除 | メンバーの回答は選択解除されています |
| 削除 | メンバーの QnA の質問または回答が削除されました |

**[レビューコンポーネント](/help/communities/reviews.md)**
SocialEvent `topic`= com/adobe/cq/social/review

| **動詞** | **説明** |
|---|---|
| POST | メンバーがレビューを作成 |
| 更新 | メンバーのレビューが編集されました |
| 削除 | メンバーのレビューが削除されました |

**[評価コンポーネント](/help/communities/rating.md)**
SocialEvent `topic`= com/adobe/cq/social/tally/rating

| **動詞** | **説明** |
|---|---|
| 評価を追加 | メンバーのコンテンツが評価されました |
| 評価を削除 | メンバーのコンテンツが評価から外されました |

**[投票コンポーネント](/help/communities/voting.md)**
SocialEvent `topic`= com/adobe/cq/social/tally/voting

| **動詞** | **説明** |
|---|---|
| 投票を追加 | メンバーのコンテンツが投票でアップしました |
| 投票を削除 | メンバーのコンテンツが投票で落選されました |

**モデレートが有効なコンポーネント**
SocialEvent `topic`= com/adobe/cq/social/moderation

| **動詞** | **説明** |
|---|---|
| 拒否 | メンバーのコンテンツが拒否されました |
| 不相応な旗 | メンバーのコンテンツにフラグが付けられる |
| 不適切なものとして旗を振らない | メンバーのコンテンツのフラグが解除されました |
| 承諾 | メンバーのコンテンツはモデレーターによって承認されます |
| 閉じる | メンバーがコメントを閉じて編集と返信を行う |
| を開く | メンバーがコメントを再度開く |

### カスタムコンポーネントイベント {#custom-component-events}

カスタムコンポーネントの場合、SocialEvent がインスタンス化されて、コンポーネントのイベントが次のように記録されます `actions` ～に起こる `topic`.

スコアリングをサポートするには、SocialEvent がメソッドを上書きする必要があります `getVerb()` 適切なように `verb` は、それぞれの `action`. この `verb` アクションに対して返されるものには、一般的に使用されるもの（例えば `POST`）またはコンポーネントに特化したもの（例： `ADD RATING`）に設定します。 次のものがあります *n-1* ～間の関係 `actions` および `verbs`.

## トラブルシューティング {#troubleshooting}

### バッジが表示されない {#badges-are-not-appearing}

Web サイトのコンテンツにスコアおよびバッジルールが適用されていて、アクティビティに対してバッジが付与されていない場合は、そのコンポーネントのインスタンスに対してバッジが有効になっていることを確認してください。

参照： [コンポーネントのバッジを有効にする](#enable-badges-for-component).

### スコアルールが無効 {#scoring-rule-has-no-effect}

Web サイトのコンテンツにスコアルールとバッジルールが適用されていて、一部のアクションにのみバッジが付与され、他のアクションには付与されない場合は、バッジルールが適用対象のスコアルールを制限していないことを確認します。

を参照してください。 `scoringRules` のプロパティ [バッジルール](#badging-rules).

### 大文字と小文字を区別するタイプミス {#case-sensitive-typo}

ほとんどのプロパティと値、特に動詞では、大文字と小文字が区別されます。 スコアリング サブルールで使用する場合、動詞はすべて大文字である必要があります。

機能が期待どおりに動作しない場合は、データが正しく入力されていることを確認します。

## クイックテスト {#quick-test}

を使用してスコアリングとバッジをすばやく試すことができます [入門チュートリアル](/help/communities/getting-started.md) （engage） サイト :

* オーサー環境のCRXDE Liteにアクセスします。
* ベースページを参照します。

   * /content/sites/engage/en/jcr:content

* badgingrules プロパティを追加します。

   * **名前**：`badgingRules`
   * **型**：`String`
   * を選択 **マルチ**
   * を選択 **追加**
   * `/libs/settings/community/badging/rules/forums-badging` と入力します。
   * を選択 **+**
   * `/libs/settings/community/badging/rules/comments-badging` と入力します。
   * 「**OK**」を選択します。

* scoringRules プロパティを追加します。

   * **名前**：`scoringRules`
   * **型**：`String`
   * を選択 **マルチ**
   * を選択 **追加**
   * `/libs/settings/community/scoring/rules/forums-scoring` と入力します。
   * を選択 **+**
   * `/libs/settings/community/scoring/rules/comments-scoring` と入力します。
   * 「**OK**」を選択します。

* 「**すべて保存**」を選択します。

![test-scoring-badging](assets/test-scoring-badging.png)

次に、フォーラムおよびコメントのコンポーネントで、バッジを表示できることを確認します。

* もう一度CRXDE Liteを使用します。
* フォーラムコンポーネントを参照します

   * `/content/sites/engage/en/forum/jcr:content/content/primary/forum`

* 必要に応じて、ブール値プロパティ allowBadges を追加し、そのプロパティが true であることを確認します。

   * **名前**：`allowBadges`
   * **型**：`Boolean`
   * **値**：`true`

![test-forum-component](assets/test-forum-component.png)

次に、 [再公開](/help/communities/sites-console.md#publishing-the-site) コミュニティサイト。

最後に

* パブリッシュインスタンスでコンポーネントを参照します。
* コミュニティメンバーとしてログインします（例：weston.mccall@dodgit.com/パスワード）。
* 新しいフォーラムトピックを投稿します。
* バッジを表示するには、ページを更新する必要があります。

   * 別のコミュニティメンバーとしてログアウトしてログインします（例：aaron.mcdonald@mailinator.com/password）。

* フォーラムを選択します。

最初のフォーラムバッジルールの最初のしきい値が 1 のスコアなので、これにより、コミュニティメンバーにはフォーラム投稿に表示されるブロンズバッジが与えられます。

![bronzebadge](assets/bronzebadge.png)

## 追加情報 {#additional-information}

詳しくは、 [スコアおよびバッジの基本事項](/help/communities/configure-scoring.md) 開発者向けのページです。

高度スコアリング・エンジンの詳細は、次を参照してください： [高度なスコアとバッジ](/help/communities/advanced.md).

設定可能なリーダーボード [component](/help/communities/enabling-leaderboard.md) および [関数](/help/communities/functions.md#leaderboard-function) コミュニティサイトでのメンバーとそのスコアの表示を簡素化します。
