---
title: コミュニティコンテンツのモデレート
seo-title: Moderating Community Content
description: モデレートの概念とアクション
seo-description: Moderation concepts and actions
uuid: 5c991d3a-0037-4d78-8f91-bb62e44441fa
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 6866d209-5789-4ef9-bc3c-d644d4fb4b1c
docset: aem65
role: Admin
exl-id: 22276580-e6bc-41c5-9ac3-e8f291f676b7
source-git-commit: 812b9f3af3ad04343e648a8d07d53f8442978b82
workflow-type: tm+mt
source-wordcount: '1516'
ht-degree: 56%

---

# コミュニティコンテンツのモデレート {#moderating-community-content}

## 概要 {#overview}

コミュニティコンテンツは、ユーザー生成コンテンツ（UGC）とも呼ばれ、メンバー（サインインした訪問者）がパブリッシュ環境で以下のいずれかのコミュニティコンポーネントを操作してコンテンツを投稿したときに作成されます。

* [ブログ](/help/communities/blog-feature.md):メンバーはブログ記事またはコメントを投稿します。
* [カレンダー](/help/communities/calendar.md):メンバーはカレンダーイベントまたはコメントを投稿します。
* [コメント](/help/communities/comments.md):メンバーはコメントを投稿したり、コメントに返信したりします。

* [フォーラム](/help/communities/forum.md):メンバーは、新しいトピックを投稿したり、トピックに返信したりします。
* [アイディエーション](/help/communities/ideation-feature.md):メンバーはアイデアまたはコメントを投稿します。
* [Q&amp;A](/help/communities/working-with-qna.md):メンバーが質問を作成したり、質問に回答したりします。
* [レビュー](/help/communities/reviews.md):メンバーは、項目を評価する際にコメントを投稿します。

UGC のモデレートは、肯定的な投稿を見分けるだけでなく、否定的な投稿（スパムや暴言など）を制限するためにも役立ちます。UGC は、次の複数の環境からモデレートできます。

* [コミュニティコンテンツストレージ](working-with-srp.md)

* [一括モデレートコンソール](moderation.md)

   モデレートコンソールには、管理者がアクセスでき、 [コミュニティモデレーター](/help/communities/users.md) パブリック環境の場合と、オーサー環境の管理者の場合が考えられます。 これは、コミュニティコンテンツが [共通店](/help/communities/working-with-srp.md).

* [コンテキスト内モデレート](in-context.md)

   パブリッシュ環境でのモデレートは、管理者およびコミュニティモデレーターが、コンテンツが投稿されたページで直接実行できます。

## モデレートアクション {#moderation-actions}

投稿コンテンツ（UGC）に対して実行できるアクションは、ユーザーの種類と環境によって異なります。次の表では、次の用語を使用して、ユーザー ID に応じた様々な役割を説明します。

* `Admin`

   次のメンバーに属するユーザー [community-administrators](users.md) グループ化します。

* `Moderator`

   のメンバー [コミュニティモデレーター](users.md#publishenvironmentusersandgroups) グループ（次を含む） [モデレーター権限](in-context.md#moderatorpermissions)) をクリックします。

* `Creator`

   コンテンツを投稿したユーザー。

* `Member`

   特別な権限を持たないサインイン済みユーザー。

* `Visitor`

   匿名ユーザー。

<table>
 <tbody>
  <tr>
   <td> </td>
   <td><strong>管理者</strong></td>
   <td><strong>モデレーター</strong></td>
   <td><strong>作成者</strong></td>
   <td><strong>メンバー</strong></td>
   <td><strong>訪問者</strong></td>
   <td><strong>発生する<br />イベント</strong></td>
   <td><strong>事前モデレート</strong></td>
  </tr>
  <tr>
   <td><strong>編集／<br />削除</strong></td>
   <td>X</td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>切り取り</strong></td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>拒否</strong></td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td>X</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>閉じる／<br />再度開く</strong></td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td>X</td>
   <td>X<br /> </td>
  </tr>
  <tr>
   <td><strong>フラグ／<br />フラグ解除</strong></td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td>X</td>
   <td> </td>
   <td>X</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>アクセス設定</strong></td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td>X</td>
   <td>X</td>
  </tr>
 </tbody>
</table>

### 編集／削除 {#edit-delete}

投稿後、作成者、管理者またはコミュニティモデレーターは、投稿を編集または削除できます。

UGC を削除すると、リポジトリから消去され、復元できなくなります。

### 切り取り {#cut}

管理者またはコミュニティモデレーターは、1 つ以上のフォーラムトピックまたは Q&amp;A の質問を、ある場所から別の場所に移動できます。同じメンバーが両方のサイトでモデレート権限を持っている場合、1 つのコミュニティサイトから別のコミュニティサイトに移動することも含まれます。

切り取りのアクションを選択すると、コンテンツはクリップボードにコピーされます。複数の投稿をコピーし、グループとして新しい場所に移動できます。

![cutugc](assets/cutugc.png)

![putbackug](assets/putbackugc.png)

別の場所で、クリップボードにコンテンツが存在するときには、新しい投稿の横に「貼り付け」ボタンと貼り付けられる投稿数が表示されます。「貼り付け」ボタンには、貼り付けの代わりにクリップボードをクリアするオプションが含まれています。

![pasteugc](assets/pasteugc.png)

![pasteugc1](assets/pasteugc1.png)

### 拒否 {#deny}

モデレーターは、公開済みのサイトで特定の UGC の表示を禁止できます。管理者およびコミュニティモデレーターは、投稿を引き続き利用でき、スパムとして注釈が付けられます。

### 閉じる／再度開く {#close-reopen}

閉じるのアクションは、会話（フォーラムトピックまたは最初のコメント）のスレッド全体に作用し、後続のすべての投稿または返信も含まれます。

閉じるを実行すると、返信がそれ以上できなくなり、さらにモデレートアクションもできなくなります。

何か操作を実行するには、トピックまたはコメントを再度開く必要があります。

閉じる／再度開くのアクションは、管理者またはコミュニティモデレーターが実行できます。

### フラグ／フラグ解除 {#flag-unflag}

フラグ設定は、サインインしたメンバー（コンテンツの作成者を除く）が投稿のコンテンツに問題があることを示す手段です。フラグが設定されると、フラグ解除アイコンが表示され、同じメンバーがコンテンツのフラグを解除できます。

コンテキスト内モデレートは、設定によりメンバーが投稿にフラグを付けた理由を選択可能にできます。選択可能なフラグの理由のリストは、カスタム理由を入力できるかどうかなどを設定できます。 フラグの理由は UGC と共に保存されますが、その理由によって特定のアクションが呼び出されることはありません。通知のフラグ数だけをトリガーします。 フラグ付きのコンテンツには注釈が付けられ、モデレーターが操作できるようになります。

すべてのフラグと、フラグを付けた人、フラグの理由はシステムで追跡され、しきい値に達するとイベントが送信されます。UGC がコミュニティモデレーターによって許可されている場合、これらのフラグはアーカイブされます。 許可およびアーカイブの後にフラグが設定された場合は、以前のフラグ設定はなかったものとして、後のフラグがアーカイブされます。

### 許可 {#allow}

許可のアクションは、フラグが設定された UGC や、拒否された UGC、事前モデレートシステムで承認されなかった UGC に対するオプションです。許可アクションは、存在するフラグ付きまたは拒否/スパムのステータスをクリアし、フラグ付きのデータをアーカイブします。

## 一般的なモデレートの概念 {#common-moderation-concepts}

### 事前モデレート {#premoderation}

UGC の事前モデレートがおこなわれる場合、投稿は、モデレートアクションで承認されるまでは公開サイトに表示されません。の作成時 [コミュニティサイト](/help/communities/sites-console.md)、 [コンテンツを事前にモデレート](sites-console.md#moderation) サイト全体の事前モデレートを有効にします。 コンポーネントをページに配置すると、モデレートをサポートするコンポーネントは、編集ダイアログの設定を使用して、事前モデレート用に設定できます。

* [コメント](comments.md) および [レビュー](reviews.md)
in **[!UICONTROL ユーザーモデレート]** > **[!UICONTROL モデレート前]**.

* [フォーラム](/help/communities/forum.md), [理想化](/help/communities/ideation-feature.md), [Q&amp;A](/help/communities/working-with-qna.md)、および [カレンダー](/help/communities/calendar.md)
in **[!UICONTROL 設定]** > **[!UICONTROL モデレート]**.

### スパム検出 {#spam-detection}

スパム検出は、送信済みのユーザー生成コンテンツの中から、好ましくないコンテンツをスパムとしてマーキングして除外する自動モデレート機能です。 ユーザーがスパムとしてマークすることで、送信されたコンテンツの望ましくない部分を送信しました。 有効にすると、事前に設定されたスパムワードの集まりに基づいて、ユーザーが生成したコンテンツがスパムかどうかを識別します。 デフォルトのスパムワードは次の場所にあります。

`/libs/settings/community/sites/moderation/spamdetector-conf/profiles/spam_words.txt`

ただし、デフォルトのスパムワードをカスタマイズまたは拡張するには、[overlay](/help/communities/overlay-comments.md) を使用して、デフォルトのスパムワードの構造に従って /apps ディレクトリ内にスパムワードを作成します。

スパムワードを含むユーザー生成投稿（ブログやフォーラム、コメントなど、あらゆるコンテンツタイプの投稿）には、「この投稿はスパムとして分類されました」というテキストが表示されます。 スパムワードを含む（ブログ、フォーラム、コメントなど、すべてのコンテンツタイプの）ユーザー生成投稿は、投稿の上に「この投稿はスパムとして分類されました」というテキストでマークされます。

モデレーターは、このような投稿を表示して同じようにマーキングし、サイトへの表示を許可または拒否できます。これらの投稿に対するモデレートアクションは、コンテキスト内でおこなうことも、一括モデレート UI でおこなうこともできます。

![スパム検出](assets/spamdetection.png)

スパム検出エンジンを有効にするには、次の手順に従います。

1. 開く [Web コンソール](https://localhost:4502/system/console/configMgr)に移動して、 `/system/console/configMgr`.

1. **AEM Communities Auto Moderation** 設定を見つけて編集します。
1. を **[!UICONTROL SpamProcess]** エントリ。

![間抜け](assets/spamprocess.png)

>[!NOTE]
>
>スパム検出は英語ロケールにのみ実装されます。

### 好感度 {#sentiment}

好感度は、投稿（UGC）内に存在する肯定的および否定的なキーワード（[ウォッチワード](#configuringwatchwords)）の数に基づいて計算されます。

好感度分析では、あらかじめ設定した一連のルールが使用され、UGC の好感度が計算されます。デフォルトのルールは次の場所にあります。 `/libs/cq/workflow/components/workflow/social/sentiments/rules.`

ルールにより生成される値は、1（すべて否定的、肯定的な言葉なし）～ 10（すべて肯定的、否定的な言葉なし）です。値 5 は中立の好感度を表し、これがデフォルトになります。

/libs コンポーネントで定義されているルールを以下に示します。

* ルール 1:肯定の単語と少なくとも 1 つの否定の単語がない場合は、値を 1 に設定します。
* ルール 2：否定的な言葉が 1 つもなく、肯定的な言葉が少なくとも 1 つある場合は、値を 10 に設定.
* ルール 3:肯定的な単語よりも否定的な単語が多い場合は、値を 3 に設定します。
* ルール 4:否定的な単語よりも肯定的な単語が多い場合は、値を 8 に設定します。

ルールを上書きまたは追加するには、デフォルトのルールの構造に従って、/apps ディレクトリに一連のルールを作成します。好感度設定を編集してルールの場所を指定します。

分析が完了すると、好感度が UGC と共に保存されます。

[一括モデレートコンソール](/help/communities/moderation.md)では、肯定的、否定的または中立のいずれかの好感度で UGC をフィルタリングして表示できます。

#### ウォッチワード {#watchwords}

AEM communities は、 *ウォッチワード分析装置* ～を評価する過程の一歩として [好感度](#sentiment). ウォッチワードによって提供されるセンチメント値の貢献度は、投稿されたコンテンツで使用される否定的なウォッチワードと肯定的なウォッチワード、および禁止されているワードが比較された結果です。

#### 好感度とウォッチワードの設定 {#configure-sentiment-and-watchwords}

好感度のルールと同様に、肯定的および否定的なウォッチワードのリストをカスタマイズできます。

ウォッチワードのデフォルトのリストは、リポジトリ内のノードのプロパティとして、デフォルトと同様に入力できます。また、単語のリストを使用して OSGi サービス `sentimentprocess.name` を設定することで、デフォルトを上書きしても入力できます。

この **sentimentprocess.name** また、センチメントルールのカスタムセットの場所を参照するように変更することもできます。

好感度とウォッチワードを設定するには：

*  管理者として、 のオーサーインスタンスにログインします。
* 開く [Web コンソール](https://localhost:4502/system/console/configMgr).
* 場所 `sentimentprocess.name`.
* 編集モードで開く設定を選択します。

![感傷的処理](assets/sentimentprocess.png)

* **肯定的なウォッチワード**

   デフォルトを上書きするための、肯定的な好感度に影響を与える単語のコンマ区切りリストです。デフォルトは空のリストです。

* **否定的なウォッチワード**

   デフォルトを上書きするための、否定的な好感度に影響を与える単語のコンマ区切りリストです。デフォルトは空のリストです。

* **ウォッチワードノードへの明示的なパス**

   デフォルトを含むノードのリポジトリの場所 `positive` および `negative` デフォルトの監視ワードを指定するプロパティです。 デフォルトは `/libs/settings/community/watchwords/default` です。

* **好感度ルール**

   肯定的および否定的ウォッチワードに基づいて好感度を計算するルールのリポジトリの場所です。デフォルトはです。 `/libs/cq/workflow/components/workflow/social/sentiments/rules` （ただし、関連するワークフローはなくなりました）。

次に、デフォルトのウォッチワードのカスタムエントリの例を示します。 `Explicit Path to Watchwords Node` が `/libs/settings/community/watchwords/default`.

![crxde](assets/crxde.png)

### モデレーター権限 {#moderator-permissions}

以下の権限は、同じリソースに割り当てられた場合、まとめて「 `moderator permissions`:

* `Read`
* `Modify`
* `Create`
* `Delete`
* `Replicate`
