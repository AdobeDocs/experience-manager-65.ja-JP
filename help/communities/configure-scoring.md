---
title: スコアおよびバッジの基本事項
description: Adobe Experience Manager Communities のスコア付け機能とバッジ機能でコミュニティメンバーを特定し、報酬を与える方法について説明します。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 470a382a-2aa7-449e-bf48-b5a804c5b114
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '946'
ht-degree: 3%

---

# スコアおよびバッジの基本事項 {#scoring-and-badges-essentials}

AEM Communitiesのスコアとバッジ機能は、コミュニティメンバーを特定し、報酬を与えます。

この機能の設定の詳細については、を参照してください。

* [コミュニティのスコアとバッジ](/help/communities/implementing-scoring.md)

このページには、その他の技術的詳細が含まれています。

* 方法 [バッジを表示](#displaying-badges) 画像またはテキストのいずれか
* 拡張を有効にする方法 [デバッグログ](#debug-log-for-scoring-and-badging)
* 方法 [UGC にアクセス](#ugc-for-scoring-and-badging) スコアとバッジに関連する

>[!CAUTION]
>
>実装で表示される実装構造は、CRXDE Liteで変更される場合があります。

## バッジの表示 {#displaying-badges}

バッジをテキストまたは画像として表示するかどうかは、HBS テンプレートのクライアント側で制御します。

例えば、「 `this.isAssigned` in `/libs/social/forum/components/hbs/topic/list-item.hbs`:

```
{{#each author.badges}}

  {{#if this.isAssigned}}

    <div class="scf-badge-text">

      {{this.title}}

    </div>

  {{/if}}

{{/each}}

{{#each author.badges}}

  {{#unless this.isAssigned}}

    <img class="scf-badge-image" alt="{{this.title}}" title="{{this.title}}" src="{{this.imageUrl}}" />

  {{/unless}}

{{/each}}
```

true の場合、 `isAssigned` は、バッジが役割に割り当てられ、バッジがテキストとして表示されることを示します。

false の場合、 `isAssigned` 獲得スコアに対してバッジが付与され、バッジが画像として表示されることを示します。

この動作に対する変更は、カスタマイズしたスクリプト（上書きまたはオーバーレイ）で行う必要があります。 詳しくは、 [クライアント側のカスタマイズ](/help/communities/client-customize.md).

## スコアおよびバッジのデバッグログ {#debug-log-for-scoring-and-badging}

スコアとバッジのデバッグに役立つように、カスタムログファイルを設定できます。 この機能で問題が発生した場合は、このログファイルの内容をカスタマーサポートに提供できます。

詳しい手順については、 [カスタムログファイルの作成](/help/sites-deploying/monitoring-and-maintaining.md#create-a-custom-log-file).

slinglog ファイルを簡単にセットアップするには：

1. 次にアクセス： **Adobe Experience Manager Web コンソールログのサポート**&#x200B;例：

   * https://localhost:4502/system/console/slinglog

1. 選択 **新しいロガーを追加**

   1. 選択 `DEBUG` 対象： **ログレベル**

   1. 名前を入力 **ログファイル**&#x200B;例：

      * logs/scoring-debug.log

   1. 2 つを入力 **ロガー** クラスエントリ ( `+` アイコン )

      * `com.adobe.cq.social.scoring`
      * `com.adobe.cq.social.badging`

   1. 「**保存**」を選択します

![debug-scoring-log](assets/debug-scoring-log.png)

ログエントリを表示するには：

* Web コンソールから

   * の下 **ステータス** メニュー
   * 選択 **ログファイル**
   * ログファイル名を検索します（例： ）。 `scoring-debug`

* サーバーのローカルディスク上

   * ログファイルの場所は &lt; です。*server-install-dir*>/crx-quickstart/logs/&lt;*log-file-name*>.log

   * 例：`.../crx-quickstart/logs/scoring-debug.log`

![scoring-log](assets/scoring-log.png)

## スコアおよびバッジの UGC {#ugc-for-scoring-and-badging}

選択した SRP が JSRP または MSRP で、ASRP ではない場合、スコアとバッジに関連する UGC を表示できます。 ( これらの用語に詳しくない場合は、 [コミュニティコンテンツストレージ](/help/communities/working-with-srp.md) および [ストレージリソースプロバイダの概要](/help/communities/srp.md).)

スコアおよびバッジのデータにアクセスするための説明には JSRP が使用されます。JSRP は、 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

**オーサー環境の JSRP**：オーサー環境で実験を行うと、オーサー環境からのみ表示される UGC が生成されます。

**公開時の JSRP**：同様に、パブリッシュ環境でテストする場合は、パブリッシュインスタンス上の管理者権限を持つCRXDE Liteにアクセスする必要があります。 パブリッシュインスタンスがで実行されている場合、 [実稼動モード](/help/sites-administering/production-ready.md) （nosamplecontent 実行モード）、 [「有効」CRXDE Lite](/help/sites-administering/enabling-crxde-lite.md).

JSRP 上の UGC の基本的な場所は次のとおりです。 `/content/usergenerated/asi/jcr/`.

### スコアとバッジの API {#scoring-and-badging-apis}

次の API を使用できます。

* [com.adobe.cq.social.scoring.api(6.3)](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ja)
* [com.adobe.cq.social.badging.api（6.3 の場合）](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ja)

開発者は、インストールされた機能パックの最新の Javadoc を、Adobeリポジトリから入手できます。 詳しくは、 [コミュニティでの Maven の使用：Javadocs](/help/communities/maven.md#javadocs).

**リポジトリ内の UGC の場所と形式は、警告なしで変更される場合があります**.

### 設定例 {#example-setup}

リポジトリデータのスクリーンショットは、2 つの異なるAEMサイト上のフォーラムに対してスコアとバッジを設定することに基づいています。

1. AEMサイト *次を使用* 一意の id（ウィザードを使用して作成されたコミュニティサイト）:

   * 使用の手引きのチュートリアル (engage) サイトを使用して、 [はじめにのチュートリアル](/help/communities/getting-started.md)
   * フォーラムページノードを見つけます。

     `/content/sites/engage/en/forum/jcr:content`

   * スコアおよびバッジのプロパティの追加

   ```
   scoringRules = [/libs/settings/community/scoring/rules/comments-scoring,
   /libs/settings/community/scoring/rules/forums-scoring]
   ```

   ```
   badgingRules =[/libs/settings/community/badging/rules/comments-scoring,
   /libs/settings/community/badging/rules/forums-scoring]
   ```

   * フォーラムコンポーネントノードを探します。

     `/content/sites/engage/en/forum/jcr:content/content/primary/forum`
( `sling:resourceType = social/forum/components/hbs/forum`)

   * バッジを表示するには、プロパティを追加します

     `allowBadges = true`

   * ユーザーがサインインし、フォーラムトピックを作成し、ブロンズバッジを受け取ります。

1. AEMサイト *なし* 一意の id :

   * の使用 [コミュニティコンポーネントガイド](/help/communities/components-guide.md)
   * フォーラムページノードを見つけます。

     `/content/community-components/en/forum/jcr:content`

   * スコアおよびバッジのプロパティの追加

   ```
   scoringRules = [/libs/settings/community/scoring/rules/comments-scoring,
   /libs/settings/community/scoring/rules/forums-scoring]
   ```

   ```
   badgingRules =[/libs/settings/community/badging/rules/comments-badging,
   /libs/settings/community/badging/rules/forums-badging]
   ```

   * フォーラムコンポーネントノードを探します。

     `/content/community-components/en/forum/jcr:content/content/forum`
( `sling:resourceType = social/forum/components/hbs/forum`)

   * バッジを表示するには、プロパティを追加します

     `allowBadges = true`

   * ユーザーがサインインし、フォーラムトピックを作成し、ブロンズバッジを受け取ります。

1. cURL を使用してモデレーターバッジが割り当てられます。

   ```shell
   curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:assignBadge" -F "badgeContentPath=/libs/settings/community/badging/images/moderator/jcr:content/moderator.png" https://localhost:4503/home/users/community/w271OOup2Z4DjnOQrviv/profile.social.json
   ```

   ユーザーが 2 つのブロンズバッジを獲得し、モデレーターバッジを受け取ると、ユーザーは次のようにフォーラムエントリと共に表示されます。

   ![モデレーター](assets/moderator.png)

>[!NOTE]
>
>この例では、次のベストプラクティスには従っていません。
>
>* スコア付けルール名は、グローバルに一意である必要があります。同じ名前で終わらないでください。
>
>  例 *not* 手順：
>
>  /libs/settings/community/scoring/rules/site1/forums-scoring
>  /libs/settings/community/scoring/rules/site2/forums-scoring
>
>* 様々なAEMサイト用の一意のバッジ画像の作成

### スコアリング UGC にアクセス {#access-scoring-ugc}

の使用 [API](#scoring-and-badging-apis) をお勧めします。

調査のために、例で JSRP を使用すると、スコアを含む基本フォルダーがになります。

* `/content/usergenerated/asi/jcr/scoring`

の子ノード `scoring` は、スコアリングルールの名前です。 したがって、サーバー上のスコア付けルール名はグローバルに一意になることがベストプラクティスとなります。

Geometrixxエンゲージサイト、ユーザーおよびそのスコアは、スコア付けルール名、コミュニティサイトのサイト ID( `engage-ba81p`)、一意の id、およびユーザーの id:

* `.../scoring/forums-scoring/engage-ba81p/6d179715c0e93cb2b20886aa0434ca9b5a540401/riley`

コミュニティコンポーネントガイドサイトのユーザーとそのスコアは、スコア付けルール名とデフォルト ID( `default-site`)、一意の id、およびユーザーの id:

* `.../scoring/forums-scoring/default-site/b27a17cb4910a9b69fe81fb1b492ba672d2c086e/riley`

スコアはプロパティに保存されます。 `scoreValue_tl` この関数は、値を含む場合も、atomicCounter を間接的に参照する場合もあります。

![access-scoring-ugc](assets/access-scoring-ugc.png)

### バッジ UGC へのアクセス {#access-badging-ugc}

の使用 [API](#scoring-and-badging-apis) をお勧めします。

例では、JSRP を使用して、割り当てられたバッジや与えられたバッジに関する情報を格納する基本フォルダーを調べます。

* `/content/usergenerated/asi/jcr`

ユーザーのプロファイルのパスが続き、次のようなバッジフォルダーで終わります。

* `/home/users/community/w271OOup2Z4DjnOQrviv/profile/badges`

#### 授与されたバッジ {#awarded-badge}

![与えられた badging-ugc](assets/access-badging-ugc.png)

#### 割り当て済みバッジ {#assigned-badge}

![割り当て済みバッジ](assets/assigned-badge.png)

## 追加情報 {#additional-information}

ポイントに基づいてメンバーのソート済リストを表示する手順は、次のとおりです。

* [リーダーボード機能](/help/communities/functions.md#leaderboard-function) コミュニティサイトまたはグループテンプレートに含める。
* [リーダーボードコンポーネント](/help/communities/enabling-leaderboard.md)（ページオーサリング用のリーダーボード機能の主なコンポーネント）。
