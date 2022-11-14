---
title: コミュニティのスコアとバッジ
seo-title: Communities Scoring and Badges
description: AEM Communities のスコアとバッジを使用すると、コミュニティメンバーを識別して報奨を与えることができます
seo-description: AEM Communities scoring and badges lets you identify and reward community members
uuid: d73683df-a413-4b3c-869c-67568bfdfcf6
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ea033bb9-cb92-4c93-855f-8c902999378c
docset: aem65
tagskeywords: scoring, badging, badges, gamification
role: Admin
exl-id: 4aa857f7-d111-4548-8f03-f6d6c27acf51
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '2868'
ht-degree: 53%

---

# コミュニティのスコアとバッジ {#communities-scoring-and-badges}

## 概要 {#overview}

AEM Communities のスコアおよびバッジ機能を使用すると、コミュニティメンバーを分類して報奨を与えることができます。

スコアとバッジの主な要素を以下に示します。

* [バッジを割り当て](#assign-and-revoke-badges) コミュニティ内のメンバーの役割を特定する。

* [バッジの基本的な授与](#enable-scoring) メンバーの参加を促すために、メンバーに送信します（作成されたコンテンツの数）。

* [バッジの高度な授与](/help/communities/advanced.md) メンバーをエキスパートとして識別する（作成されたコンテンツの質）。

**注意** バッジの授与は [デフォルトでは有効になっていません](/help/communities/implementing-scoring.md#main-pars-text-237875536).

>[!CAUTION]
>
>CRXDE Lite で表示される実装の構造は、UI が使用可能になると変化する場合があります。

## バッジ {#badges}

バッジはコミュニティ内でのメンバーの役割または地位を表すためのもので、メンバーの名前の下に配置されます。バッジは、画像として、または名前として表示できます。 画像として表示される場合、この名前はアクセシビリティのための代替テキストとして含まれます。

デフォルトでは、バッジは次の場所のリポジトリに配置されます。

* `/libs/settings/community/badging/images`

別の場所に格納する場合は、バッジに誰でもアクセスできるようにする必要があります。

UGC 内では、割り当てられたバッジと、ルールに従って獲得されたバッジが区別されます。現在は、割り当てられたバッジがテキストとして表示され、獲得したバッジが画像として表示されます。

### バッジ管理 UI {#badge-management-ui}

コミュニティ [バッジコンソール](/help/communities/badges.md) は、獲得（与えられる）時やコミュニティで特定の役割を担う（割り当てられる）時に、メンバーに対して表示できるカスタムバッジを追加する機能を提供します。

### 割り当てられたバッジ {#assigned-badges}

役割ベースのバッジは、管理者がコミュニティメンバーに対し、各メンバーのコミュニティ内での役割に基づいて割り当てるものです。

割り当てられた（および待ち受けの）バッジは、選択した [SRP](/help/communities/srp.md) およびは直接アクセスできません。 GUI が使用できるようになるまで、ロールベースのバッジを割り当てる唯一の方法は、コードまたは cURL を使用して割り当てることです。 cURL の手順については、「 [バッジの割り当てと取り消し](#assign-and-revoke-badges).

このリリースには、以下の 3 つの役割ベースのバッジが含まれています。

* **モデレーター**

   `/libs/settings/community/badging/images/moderator/jcr:content/moderator.png`

* **グループマネージャー**

   `/libs/settings/community/badging/images/group-manager/jcr:content/group-manager.png`

* **特権を持つ人**

   `/libs/settings/community/badging/images/privileged-member/jcr:content/privileged-member.png`

   ![割り当てられたバッジ](assets/assigned-badges.png)

### 授与されたバッジ {#awarded-badges}

報奨ベースのバッジは、スコアサービスがコミュニティ内でのメンバーのアクティビティを一定のルールで評価し、その結果としてメンバーに付与されるものです。

アクティビティに対する報奨としてバッジを表示するには、以下の 2 つの設定をする必要があります。

* バッジは必ず設定します [有効](#enableforcomponent) フィーチャコンポーネント用。
* スコアルールとバッジルールは次の条件を満たす必要があります [適用](#applytopage) を、コンポーネントが配置されているページ（または上位ページ）に追加します。

このリリースには、以下の 3 つの報奨ベースのバッジが含まれています。

* **金**

   `/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png`

* **銀**

   `/libs/settings/community/badging/images/silver-badge/jcr:content/silver.png`

* **青銅**

   `/libs/settings/community/badging/images/bronze-badge/jcr:content/bronze.png`

   ![授与されたバッジ](assets/awarded-badges.png)

>[!NOTE]
>
>不適切な投稿としてフラグが付けられた場合に、その投稿にマイナスのポイントを割り当て、スコアの値に反映させるようなスコアルールを設定できます。ただし、バッジを獲得すると、スコアリングポイントの削減やスコアリングルールの変更により、バッジは自動的に削除されません。
>
>授与されたバッジは、割り当てられたバッジと同じ方法で取り消すことができます。詳しくは、 [バッジの割り当てと取り消し](#assign-and-revoke-badges) 」セクションに入力します。 今後の改善には、メンバーのバッジを管理する UI が含まれます。

### カスタムバッジ {#custom-badges}

カスタムバッジは、 [バッジコンソール](/help/communities/badges.md) バッジルールで割り当てるか指定します。

バッジコンソールからインストールすると、カスタムバッジは自動的にパブリッシュ環境にレプリケートされます。

## スコアの有効化 {#enable-scoring}

スコアはデフォルトで有効になっていません。スコア付けとバッジの授与を設定して有効にする基本的な手順は次のとおりです。

* ポイント獲得のルールを指定する ([スコア付けルール](#scoring-rules)) をクリックします。
* スコア付けルールごとに累積されたポイントに対して、 [バッジ](#badges) ([バッジルール](#badging-rules)) をクリックします。

* [スコアルールとバッジルールをコミュニティサイトに適用する](#apply-rules-to-content).
* [コミュニティ機能のバッジを有効にする](#enable-badges-for-component).

詳しくは、 [クイックテスト](#quick-test) セクションを開き、フォーラムとコメントのデフォルトのスコアルールとバッジルールを使用して、コミュニティサイトのスコアを有効にします。

### コンテンツに対するルールの適用 {#apply-rules-to-content}

スコアとバッジを有効にするには、プロパティを追加します `scoringRules` および `badgingRules` を、サイトのコンテンツツリー内の任意のノードに追加します。

サイトが公開済みの場合は、すべてのルールを適用してコンポーネントを有効にした後に、サイトを再公開します。

バッジを有効にしたコンポーネントには、現在のノードまたはその上位ノードのルールが適用されます。

ノードのタイプがの場合 `cq:Page` （推奨）次に、CRXDE|Lite を使用して、プロパティをそのに追加します。 `jcr:content` ノード。

| **プロパティ** | **タイプ** | **説明** |
|---|---|---|
| badgingRules | String | [バッジルール](#badging-rules)の配列リスト |
| scoringRules | 文字列 | [スコアルール](#scoring-rules)の配列リスト |

>[!NOTE]
>
>スコアルールがバッジ授与に影響を与えていないように見える場合は、スコアルールがバッジルールの scoringRules でブロックされていないかを確認してください。「 [バッジルール](#badging-rules).

### コンポーネントに対するバッジの有効化 {#enable-badges-for-component}

スコアルールとバッジルールは、[オーサリングモード](/help/communities/author-communities.md)でコンポーネント設定を編集してバッジを有効にしたコンポーネントのインスタンスに対してのみ有効です。

コンポーネントインスタンスでバッジを表示するかどうかは、ブール型プロパティの `allowBadges` で指定できます。これは、 [コンポーネント編集ダイアログ](/help/communities/author-communities.md) フォーラム、Q&amp;A、コメントコンポーネントの場合は、「 」というラベルの付いたチェックボックスを使用します。 **バッジを表示**.

#### 例：フォーラムコンポーネントインスタンスの allowBadges {#example-allowbadges-for-forum-component-instance}

![enable-badges-component](assets/enable-badges-component.png)

>[!NOTE]
>
>フォーラム、Q&amp;A およびコメントで見つかった HBS コードを例として使用すると、どのコンポーネントもバッジを表示するようにオーバーレイすることができます。

## スコアルール {#scoring-rules}

スコアルールは、バッジを授与するためのスコア計算の基礎となるものです。

ごく簡単に言うと、スコアルールは、1 つ以上のサブルールから成るリストです。バッジが有効な場合に適用するルールを識別するために、スコアルールがコミュニティサイトのコンテンツに適用されます。

スコアルールは継承されますが、付加的ではありません。次に例を示します。

* page2 にスコアルール 2 が含まれ、その上位ページ 1 にスコアルール 1 が含まれる場合。
* page2 コンポーネントのアクションは、rule1 と rule2 の両方を呼び出します。
* 両方のルールに同じに適用可能なサブルールが含まれる場合 `topic/verb`:

   * スコアに影響を与えるのは、rule2 のサブルールのみです。
   * 両方のサブルールのスコアは、一緒に追加されません。

1 つ以上のスコアルールが存在するときは、ルールごとに分けてスコアが管理されます。

スコア付けルールは、 `cq:Page` プロパティを含む `jcr:content` 定義するサブルールのリストを指定するノード。

スコアは SRP に格納されます。

>[!NOTE]
>
>ベストプラクティスは、各スコアルールに一意の名前を付けることです。
>
>スコアルールの名前はグローバルレベルで一意にする必要があり、末尾を同じ名前にしてはなりません。
>
>例 *not* 手順：
>
>/libs/settings/community/scoring/rules/site1/forums-scoring
>/libs/settings/community/scoring/rules/site2/forums-scoring

### スコアサブルール {#scoring-sub-rules}

スコアサブルールには、コミュニティへの参加状況を表す値を詳細に設定するプロパティが含まれています。

それぞれのスコアサブルールでは、以下を指定します。：

* 追跡されているアクティビティは何ですか？
* 関連する特定のコミュニティ機能は何ですか？
* 与えられるポイントは何点ですか？

デフォルトではアクションを実行したメンバーにポイントが付与されますが、サブルールでコンテンツの所有者にポイントを付与するよう設定することも可能です（`forOwner`）。

各サブルールには、1 つ以上のスコアルールを含めることができます。

通常、サブルールの名前は、 *件名* , *object* および *動詞*. 次に例を示します。

* member-comment-create
* member-receive-vote

サブルールは、タイプのノードです `cq:Page` プロパティを含む `jcr:content`ノード [動詞とトピック](#topics-and-verbs) .

<table>
 <tbody>
  <tr>
   <th>プロパティ</th>
   <th>タイプ</th>
   <th> 値 説明</th>
  </tr>
  <tr>
   <td><i><code>VERB</code></i></td>
   <td>Long</td>
   <td>
    <ul>
     <li>必須です。動詞はイベントアクションに対応します。</li>
     <li>少なくとも 1 つの動詞プロパティが必要です。</li>
     <li>動詞はすべて大文字で入力する必要があります。</li>
     <li>複数の動詞プロパティを設定できますが、重複はできません。</li>
     <li>値はこのイベントに適用するスコアです。</li>
     <li>値は正でも負でも構いません。</li>
     <li>このリリースでサポートされている動詞のリストは、 <a href="#topics-and-verbs">トピックと動詞</a> セクション</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>topics</code></td>
   <td>文字列</td>
   <td>
    <ul>
     <li>オプションです。サブルールを、イベントトピックで識別されるコミュニティコンポーネントのみに制限します。</li>
     <li>指定する場合は、イベントトピックの複数値文字列を指定します。</li>
     <li>このリリースのトピックのリストは、 <a href="#topics-and-verbs">トピックと動詞</a> セクション</li>
     <li>デフォルトでは、動詞に関連するすべてのトピックに適用されます。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>forOwner</code></td>
   <td>ブール値</td>
   <td>
    <ul>
     <li>オプションです。メンバーが自分の所有するコンテンツを操作している場合は関係ありません。</li>
     <li>true の場合は、操作されたコンテンツの所有者にスコアが適用されます。</li>
     <li>false の場合は、操作をおこなうメンバーにスコアが適用されます。</li>
     <li>デフォルトは false です。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>scoringType</code></td>
   <td>文字列</td>
   <td>
    <ul>
     <li>オプションです。スコアエンジンを指定します。</li>
     <li>「basic」の場合は、量に基づくスコアエンジンが使用されます。
      <ul>
       <li>このリリースに含まれています。</li>
      </ul> </li>
     <li>「advanced」の場合は、質と量に基づくスコアエンジンが使用されます。
      <ul>
       <li><a href="/help/communities/advanced.md">追加パッケージ</a>が必要です。</li>
      </ul> </li>
     <li>デフォルトは「basic」です。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### このリリースに含まれているスコアルールとサブルール {#included-scoring-rules-and-sub-rules}

このリリースには、 [フォーラム機能](/help/communities/functions.md#forum-function) （フォーラム機能の「フォーラム」および「コメント」コンポーネント用にそれぞれ 1 つずつ）:

1. /libs/settings/community/scoring/rules/comments-scoring

   * subRules[] = /libs/settings/community/scoring/rules/sub-rules/member-comment-create /libs/settings/community/scoring/rules/sub-rules/member-receive-vote /libs/settings/community/scoring/rules/sub-moderated/member-is

1. /libs/settings/community/scoring/rules/forums-scoring

   * subRules[] = /libs/settings/community/scoring/rules/sub-rules/member-forum-create /libs/settings/community/scoring/rules/sub-rules/member-receive-vote /libs/settings/community/scoring/rules/sub-moderated/member-soter

**メモ：**

* 両方 `rules` および `sub-rules` ノードのタイプは cq:Page です。

* `subRules` は String 型の属性です[] 規則の `jcr:content` ノード。

* `sub-rules` は、様々なスコアリングルール間で共有できます。
* `rules` はリポジトリの場所に配置し、全員に対して読み取り権限を付与する必要があります。

   * ルール名は、場所に関係なく一意である必要があります。

### カスタムスコアルールのアクティベート {#activating-custom-scoring-rules}

オーサー環境でスコアルールやサブルールに対して行った変更や追加は、パブリッシュ環境にインストールする必要があります。

## バッジルール {#badging-rules}

バッジルールでは、以下を指定することで、スコアルールをバッジにリンクします。

* スコア付けルール
* 特定のバッジの待機に必要なスコア

バッジルールは `cq:Page` タイプのノードであり、その `jcr:content` ノードのプロパティで、スコアルールをスコアおよびバッジと関連付けます。

バッジルールは必須の `thresholds` プロパティから成り、このプロパティには、バッジに対応付けるスコアの順序付きリストを指定します。スコアは小さい値から順に並べる必要があります。次に例を示します。

* `1|/libs/settings/community/badging/images/bronze-badge/jcr:content/bronze.png`

   * 1 ポイントの獲得に対して、ブロンズバッジが待機されます。

* `60|/libs/settings/community/badging/images/silver-badge/jcr:content/silver.png`

   * シルバーバッジは、60 ポイントが累積したときに授与されます。

* `80|/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png`

   * 80 ポイントが累積すると、ゴールドバッジが表示されます。

バッジルールは、ポイントの累積方法を決定するスコアルールと組み合わせて使用されます。「 [コンテンツへのルールの適用](#apply-rules-to-content).

バッジルールの `scoringRules` プロパティは、そのバッジルールに組み合わせ可能なスコアルールを制限します。

>[!NOTE]
>
>ベストプラクティスは、各 AEM サイトに固有のバッジ画像を作成することです。

![badging-rule-configuration](assets/badging-rule-configuration.png)

<table>
 <tbody>
  <tr>
   <th>プロパティ</th>
   <th>タイプ</th>
   <th>値 説明</th>
  </tr>
  <tr>
   <td>thresholds</td>
   <td>文字列</td>
   <td>（必須）「number|path」という形式の複数値文字列<em></em>
    <ul>
     <li>number = スコア</li>
     <li>| = 縦線の文字（U+007C）</li>
     <li>path = バッジ画像リソースへのフルパス</li>
    </ul> 文字列は、値が増加し、数値とパスの間に空白が表示されないように、並べ替える必要があります。<br /> エントリの例：<br /> <code>80|/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png</code></td>
  </tr>
  <tr>
   <td>badgingType</td>
   <td>文字列</td>
   <td><em>（オプション）</em> スコアリングエンジンを「基本」または「詳細」として識別します。 高度なスコアエンジンが必要な場合は、 <a href="/help/communities/advanced.md">高度なスコアとバッジ</a>. デフォルトは「basic」です。</td>
  </tr>
  <tr>
   <td>scoringRules</td>
   <td>文字列</td>
   <td>(<em>オプション</em>) バッジルールを、スコアルールで識別されるスコアイベントに制限する複数値の文字列</td>
  </tr>
 </tbody>
</table>

### このリリースに含まれるバッジルール {#included-badging-rules}

このリリースには、[フォーラムとコメントのスコアルール](#includedscoringrules)に対応する 2 つのバッジルールが含まれています。

* `/libs/settings/community/badging/rules/comments-badging`

* `/libs/settings/community/badging/rules/forums-badging`

**メモ：**

* `rules` ノードのタイプは cq:Page です。
* `rules` はリポジトリの場所に配置し、全員に対して読み取り権限を付与する必要があります。

   * ルール名は、場所に関係なく一意である必要があります。

### カスタムバッジルールのアクティベート {#activating-custom-badging-rules}

オーサー環境でバッジルールまたはバッジ画像の変更や追加をおこなった場合は、それをパブリッシュ環境でインストールする必要があります。

## バッジの割り当てと取り消し {#assign-and-revoke-badges}

メンバーへのバッジの割り当ては、[メンバーコンソール](/help/communities/members.md#badges-tab)を使用するか、プログラムで cURL コマンドを使用して、おこなうことができます。

以下の cURL コマンドは、バッジの割り当てと取り消しの HTTP リクエストで必要とされる要素を示しています。基本的な形式は以下のとおりです。

cURL -i -XPOST-H *ヘッダー* -u *サインイン* -F *操作* -F *バッジ* *member-profile-url*

*ヘッダー* =サーバーに渡すカスタムヘッダー（必須）

*サインイン* = administrator-id:password 例：admin:admin

*操作* = &quot;:operation=social:assignBadge&quot; OR &quot;:operation=social:deleteBadge&quot;

*バッジ* = &quot;badgeContentPath=*badge-image-file*&quot;

*badge-image-file* =リポジトリ内のバッジ画像ファイルの場所 ( 例：/libs/settings/community/badging/images/moderator/jcr:content/moderator.png

*member-profile-url* =パブリッシュ時のメンバーのプロファイルのエンドポイント（例： ）https://&lt;server>:&lt;port>/home/users/community/riley/profile.social.json

>[!NOTE]
>
>この *member-profile-url*:
>
>* オーサーインスタンスを参照する場合、 [トンネルサービス](/help/communities/users.md#tunnel-service) が有効になっている。
>* わかりにくく、ランダムな名前である可能性があります。詳しくは、 [セキュリティチェックリスト](/help/sites-administering/security-checklist.md#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path) 許可可能 ID に関する情報です。


### 例： {#examples}

#### モデレーターバッジの割り当て {#assign-a-moderator-badge}

```shell
curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:assignBadge" -F "badgeContentPath=/libs/settings/community/badging/images/moderator/jcr:content/moderator.png" /home/users/community/updcs9DndLEI74DB9zsB/profile.social.json
```

#### 割り当て済みのシルバーバッジの取り消し {#revoke-an-assigned-silver-badge}

```shell
curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:deleteBadge" -F "badgeContentPath=/libs/settings/community/badging/images/silver/jcr:content/silver.png" /home/users/community/updcs9DndLEI74DB9zsB/profile.social.json
```

>[!NOTE]
>
>cURL を使用したバッジの割り当てと取り消しは、どのバッジ画像でも機能します。ただし、獲得されたバッジではなく割り当てられたバッジの場合は、割り当てられたバッジとしてマークされ、相応に処理されます。

## カスタムコンポーネント用のスコアとバッジ {#scoring-and-badges-for-custom-components}

カスタムコンポーネント用に作成されたイベントトピックを動詞と関連付けることで、カスタムコンポーネント用のスコアルールとバッジルールを作成できます。

## トピックと動詞 {#topics-and-verbs}

メンバーがコミュニティ機能を操作すると、通知やスコアなどの非同期リスナーを呼び出すイベントが送信されます。

コンポーネントの SocialEvent インスタンスは、イベントを `actions` それは `topic`. SocialEvent には、 `verb` アクションに関連付けられている。 ここに *n-1* ～間の関係 `actions` および `verbs`.

配信されるコミュニティコンポーネントについて、次の表で次の内容を説明します `verbs` それぞれに定義 `topic` ～で使用できる [スコアサブルール](#scoring-sub-rules).

>[!NOTE]
>
>コンポーネントインスタンスでバッジを表示するかどうかは、新しいブール型プロパティの `allowBadges` で指定できます。更新時に設定可能になります [コンポーネント編集ダイアログ](/help/communities/author-communities.md) ラベル付きのチェックボックスを通じて **バッジを表示**.

**[カレンダーコンポーネント](/help/communities/calendar.md)** SocialEvent `topic`=  = com/adobe/cq/social/calendar

| **動詞** | **説明** |
|---|---|
| POST | メンバーがカレンダーイベントを作成する |
| 追加 | メンバーがカレンダーイベントについてコメントする |
| UPDATE | メンバーのカレンダーイベントまたはコメントが編集される |
| 削除 | メンバーのカレンダーイベントまたはコメントが削除される |

**[コメントコンポーネント](/help/communities/comments.md)** SocialEvent `topic`=  = com/adobe/cq/social/comment

| **動詞** | **説明** |
|---|---|
| POST | メンバーがコメントを作成する |
| 追加 | メンバーがコメントに返信する |
| 更新 | メンバーのコメントが編集される |
| 削除 | メンバーのコメントが削除される |

**[ファイルライブラリコンポーネント](/help/communities/file-library.md)** SocialEvent `topic`=  = com/adobe/cq/social/fileLibrary

| **動詞** | **説明** |
|---|---|
| POST | メンバーがフォルダーを作成する |
| ATTACH | メンバーがファイルをアップロードする |
| 更新 | メンバーがフォルダーまたはファイルを更新する |
| 削除 | メンバーがフォルダーまたはファイルを削除する |

**[フォーラムコンポーネント](/help/communities/forum.md)** SocialEvent `topic`=  = com/adobe/cq/social/forum

| **動詞** | **説明** |
|---|---|
| POST | メンバーがフォーラムトピックを作成する |
| 追加 | メンバーがフォーラムトピックに返信する |
| 更新 | メンバーのフォーラムトピックまたは返信が編集される |
| 削除 | メンバーのフォーラムトピックまたは返信が削除される |

**[ジャーナルコンポーネント](/help/communities/blog-feature.md)** SocialEvent `topic`=  = com/adobe/cq/social/journal

| **動詞** | **説明** |
|---|---|
| POST | メンバーがブログ記事を作成する |
| 追加 | メンバーがブログ記事にコメントする |
| 更新 | メンバーのブログ記事またはコメントが編集される |
| 削除 | メンバーのブログ記事またはコメントが削除される |

**[Q&amp;A コンポーネント](/help/communities/working-with-qna.md)** SocialEvent `topic` = com/adobe/cq/social/qna

| **動詞** | **説明** |
|---|---|
| POST | メンバーが Q&amp;A の質問を作成する |
| 追加 | メンバーが Q&amp;A の回答を作成する |
| 更新 | メンバーの Q&amp;A の質問または回答が編集される |
| SELECT | メンバーの回答が選択される |
| UNSELECT | メンバーの回答の選択が解除される |
| 削除 | メンバーの Q&amp;A の質問または回答が削除される |

**[レビューコンポーネント](/help/communities/reviews.md)** SocialEvent `topic`=  = com/adobe/cq/social/review

| **動詞** | **説明** |
|---|---|
| POST | メンバーがレビューを作成する |
| 更新 | メンバーのレビューが編集される |
| 削除 | メンバーのレビューが削除される |

**[評価コンポーネント](/help/communities/rating.md)**
SocialEvent `topic`= com/adobe/cq/social/tally/rating

| **動詞** | **説明** |
|---|---|
| ADD RATING | メンバーのコンテンツの評価が上がった |
| REMOVE RATING | メンバーのコンテンツの評価が下がった |

**[投票コンポーネント](/help/communities/voting.md)**
SocialEvent `topic`= com/adobe/cq/social/tally/voting

| **動詞** | **説明** |
|---|---|
| ADD VOTING | メンバーのコンテンツに賛成票が投じられた |
| REMOVE VOTING | メンバーのコンテンツに反対票が投じられた |

**モデレート対応コンポーネント** SocialEvent `topic`=  = com/adobe/cq/social/moderation

| **動詞** | **説明** |
|---|---|
| DENY | メンバーのコンテンツが拒否される |
| FLAG-AS-INAPPROPRIATE | メンバーのコンテンツにフラグが付けられる |
| UNFLAG-AS-INAPPROPRIATE | メンバーのコンテンツのフラグが解除される |
| ACCEPT | メンバーのコンテンツがモデレーターにより承認される |
| CLOSE | メンバーがコメントの編集と返信を閉じる |
| OPEN | メンバーがコメントを再度開く |

### カスタムコンポーネントイベント {#custom-component-events}

カスタムコンポーネントの場合、 SocialEvent がインスタンス化され、コンポーネントのイベントが `actions` それは `topic`.

スコアリングをサポートするには、 SocialEvent でメソッドを上書きする必要があります `getVerb()` 適切な `verb` が返される `action`. この `verb` アクションに対して返されるのは、一般的に使用される ( `POST`) またはコンポーネント専用の ( 例えば `ADD RATING`) をクリックします。 ここに *n-1* ～間の関係 `actions` および `verbs`.

## トラブルシューティング {#troubleshooting}

### バッジが表示されない {#badges-are-not-appearing}

スコアルールとバッジルールが Web サイトのコンテンツに適用されていて、どのアクティビティに対してもバッジが表示されない場合は、そのコンポーネントのインスタンスに対してバッジが有効になっていることを確認します。

詳しくは、 [コンポーネントのバッジを有効にする](#enable-badges-for-component).

### スコアルールが反映されない {#scoring-rule-has-no-effect}

スコアルールとバッジルールを Web サイトのコンテンツに適用したのに、バッジが一部のアクションにしか授与されない場合は、バッジルールの適用先のスコアルールが制限されていないかを確認してください。

詳しくは、 `scoringRules` プロパティ [バッジルール](#badging-rules).

### 大文字と小文字のタイプミス {#case-sensitive-typo}

ほとんどのプロパティや値（特に動詞）では、大文字と小文字が区別されます。スコアサブルールで使用する場合、動詞はすべて大文字にする必要があります。

この機能が予想どおり動作しない場合は、データが正しく入力されているかを確認してください。

## クイックテスト {#quick-test}

[Getting Started Tutorial](/help/communities/getting-started.md)（engage）サイトを使用すると、スコアとバッジを簡単に試すことができます。

* 作成者のCRXDE Liteにアクセスします。
* ベースページを参照します。

   * /content/sites/engage/en/jcr:content

* badgingRules プロパティを追加します。

   * **名前**：`badgingRules`
   * **型**：`String`
   * 選択 **複数**
   * 選択 **追加**
   * `/libs/settings/community/badging/rules/forums-badging` と入力します。
   * 選択 **+**
   * `/libs/settings/community/badging/rules/comments-badging` と入力します。
   * 「**OK**」を選択します。

* scoringRules プロパティを追加します。

   * **名前**：`scoringRules`
   * **型**：`String`
   * 選択 **複数**
   * 選択 **追加**
   * `/libs/settings/community/scoring/rules/forums-scoring` と入力します。
   * 選択 **+**
   * `/libs/settings/community/scoring/rules/comments-scoring` と入力します。
   * 「**OK**」を選択します。

* **すべて保存** を選択します。

![test-scoring-badging](assets/test-scoring-badging.png)

次に、フォーラムおよびコメントコンポーネントでバッジを表示できるようにします。

* 再びCRXDE Lite。
* フォーラムコンポーネントを参照

   * `/content/sites/engage/en/forum/jcr:content/content/primary/forum`

* 必要に応じて、allowBadges ブール型プロパティを追加し、true に設定する。

   * **名前**：`allowBadges`
   * **型**：`Boolean`
   * **値**：`true`

![test-forum-component](assets/test-forum-component.png)

次に、コミュニティサイトを[再公開](/help/communities/sites-console.md#publishing-the-site)します。

最後に、

* パブリッシュインスタンス上のコンポーネントを参照します。
* コミュニティメンバーとしてログインします ( 例：weston.mccall@dodgit.com / password) で確認できます。
* 新しいフォーラムトピックを投稿します。
* バッジを表示するには、ページを更新する必要があります。

   * ログアウトし、別のコミュニティメンバーとしてログインします ( 例：aaron.mcdonald@mailinator.com/password) を参照してください。

* フォーラムを選択します。

フォーラムトピックを投稿したコミュニティメンバーを見ると、ブロンズバッジが表示されているはずです。これは、最初のフォーラムバッジルールの最初のしきい値のスコアが 1 であるからです。

![気取った](assets/bronzebadge.png)

## 追加情報 {#additional-information}

詳しくは、 [スコアとバッジの基本事項](/help/communities/configure-scoring.md) 開発者向けのページ

高度なスコアエンジンについて詳しくは、 [高度なスコアとバッジ](/help/communities/advanced.md).

設定可能なリーダーボード [コンポーネント](/help/communities/enabling-leaderboard.md) および [関数](/help/communities/functions.md#leaderboard-function) は、コミュニティサイトでのメンバーとそのスコアの表示を簡素化します。
