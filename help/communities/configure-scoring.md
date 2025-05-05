---
title: スコアおよびバッジの基本事項
description: Adobe Experience Manager Communities のスコアおよびバッジ機能でコミュニティメンバーが識別され、報酬が与えられる仕組みについて説明します。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 470a382a-2aa7-449e-bf48-b5a804c5b114
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 2%

---

# スコアおよびバッジの基本事項 {#scoring-and-badges-essentials}

AEM Communitiesのスコアとバッジ機能は、コミュニティメンバーを特定して報酬を付与します。

この機能のセットアップについて詳しくは、こちらを参照してください。

* [コミュニティのスコアとバッジ](/help/communities/implementing-scoring.md)

このページには、その他の技術的な詳細が含まれています。

* 画像またはテキストとしてバッジを [ 表示 ](#displaying-badges) する方法
* 広範な [ デバッグログ ](#debug-log-for-scoring-and-badging) を有効にする方法
* スコアおよびバッジに関連する [UGC にアクセス ](#ugc-for-scoring-and-badging) 方法

>[!CAUTION]
>
>CRXDE Liteに表示される実装構造は変更される場合があります。

## バッジの表示 {#displaying-badges}

バッジをテキストまたは画像のどちらで表示するかは、HBS テンプレートでクライアント側で制御されます。

例えば、`/libs/social/forum/components/hbs/topic/list-item.hbs` で `this.isAssigned` を検索します。

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

true の場合、`isAssigned` はバッジが役割に割り当てられたことを示し、バッジはテキストで表示されます。

false の場合、バッジ `isAssigned` 獲得したスコアに対して授与され、そのバッジは画像として表示される必要があることを示します。

この動作への変更は、カスタマイズされたスクリプト（オーバーライドまたはオーバーレイ）で行う必要があります。 [ クライアントサイドのカスタマイズ ](/help/communities/client-customize.md) を参照してください。

## スコアリングおよびバッジのデバッグログ {#debug-log-for-scoring-and-badging}

スコアリングとバッジのデバッグに役立つように、カスタムログファイルを設定できます。 機能に問題が発生した場合、このログファイルの内容がカスタマーサポートに提供されることがあります。

手順について詳しくは、[ カスタムログファイルの作成 ](/help/sites-deploying/monitoring-and-maintaining.md#create-a-custom-log-file) を参照してください。

slinglog ファイルをすばやく設定するには：

1. **Adobe Experience Manager Web コンソールログのサポート** にアクセスします。例：

   * https://localhost:4502/system/console/slinglog

1. **新しいロガーを追加** を選択します

   1. **ログレベル** の `DEBUG` を選択

   1. **ログファイル** の名前を入力します。例：

      * logs/scoring-debug.log

   1. **Logger** （クラス）エントリを 2 つ入力します（`+` のアイコンを使用）

      * `com.adobe.cq.social.scoring`
      * `com.adobe.cq.social.badging`

   1. 「**保存**」を選択します

![debug-scoring-log](assets/debug-scoring-log.png)

ログエントリを確認するには：

* Web コンソールから

   * **ステータス** メニューで
   * 「**ログファイル**」を選択します。
   * `scoring-debug` のようなログファイル名を検索します。

* サーバーのローカルディスク上

   * ログファイルは、&lt;*server-install-dir*>/crx-quickstart/logs/&lt;*log-file-name*>.log にあります。

   * 例えば、`.../crx-quickstart/logs/scoring-debug.log` のように指定します。

![scoring-log](assets/scoring-log.png)

## スコアおよびバッジ用 UGC {#ugc-for-scoring-and-badging}

選択された SRP が JSRP または MSRP であり、ASRP ではない場合、スコアおよびバッジに関連する UGC を表示できます。 （これらの用語に詳しくない場合は、[ コミュニティコンテンツストレージ ](/help/communities/working-with-srp.md) および [ ストレージリソースプロバイダーの概要 ](/help/communities/srp.md) を参照してください。）

UGC は [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) を使用して簡単にアクセスできるので、スコアリングデータとバッジデータへのアクセスに関する説明では JSRP が使用されます。

**オーサー環境における JSRP**：オーサー環境で実験を行うと、UGC がオーサー環境からのみ表示されるようになります。

**パブリッシュ環境での JSRP**：同様に、パブリッシュ環境でテストする場合は、パブリッシュインスタンスに対する管理者権限を持つCRXDE Liteにアクセスする必要があります。 パブリッシュインスタンスが [ 実稼動モード ](/help/sites-administering/production-ready.md) （nosamplecontent 実行モード）で実行されている場合は、[CRXDE Liteを有効にする ](/help/sites-administering/enabling-crxde-lite.md) 必要があります。

JSRP 上の UGC のベースの場所は `/content/usergenerated/asi/jcr/` です。

### スコアおよびバッジ API {#scoring-and-badging-apis}

次の API を使用できます。

* [com.adobe.cq.social.scoring.api、6.3](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ja)
* [com.adobe.cq.social.badging.api - 6.3](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ja)

インストールされた機能パックの最新の Javadocs は、開発者がAdobeリポジトリから使用できます。 [ コミュニティでの Maven の使用：Javadocs](/help/communities/maven.md#javadocs) を参照してください。

**リポジトリ内の UGC の場所と形式は、警告なく変更される場合があります**。

### 設定例 {#example-setup}

リポジトリデータのスクリーンショットは、2 つの異なるAEM サイトでフォーラムのスコアとバッジを設定することで取得できます。

1. AEM サイト *一意の ID を持つ* （ウィザードを使用して作成されたコミュニティサイト） :

   * [ はじめる前に ](/help/communities/getting-started.md) のチュートリアルで作成したはじめる前に（engage）サイトを使用します。
   * フォーラムページのノードを見つけます

     `/content/sites/engage/en/forum/jcr:content`

   * スコアリングプロパティとバッジプロパティの追加

   ```
   scoringRules = [/libs/settings/community/scoring/rules/comments-scoring,
   /libs/settings/community/scoring/rules/forums-scoring]
   ```

   ```
   badgingRules =[/libs/settings/community/badging/rules/comments-scoring,
   /libs/settings/community/badging/rules/forums-scoring]
   ```

   * フォーラムコンポーネントのノードを見つけます

     `/content/sites/engage/en/forum/jcr:content/content/primary/forum`
（`sling:resourceType = social/forum/components/hbs/forum`）

   * バッジを表示するには、プロパティを追加します

     `allowBadges = true`

   * ユーザーがログインし、フォーラムトピックを作成すると、ブロンズバッジが付与されます

1. AEM サイト *一意の ID なし* :

   * [ コミュニティコンポーネントガイド ](/help/communities/components-guide.md) の使用
   * フォーラムページのノードを見つけます

     `/content/community-components/en/forum/jcr:content`

   * スコアリングプロパティとバッジプロパティの追加

   ```
   scoringRules = [/libs/settings/community/scoring/rules/comments-scoring,
   /libs/settings/community/scoring/rules/forums-scoring]
   ```

   ```
   badgingRules =[/libs/settings/community/badging/rules/comments-badging,
   /libs/settings/community/badging/rules/forums-badging]
   ```

   * フォーラムコンポーネントのノードを見つけます

     `/content/community-components/en/forum/jcr:content/content/forum`
（`sling:resourceType = social/forum/components/hbs/forum`）

   * バッジを表示するには、プロパティを追加します

     `allowBadges = true`

   * ユーザーがログインし、フォーラムトピックを作成すると、ブロンズバッジが付与されます

1. cURL を使用すると、ユーザーにモデレータバッジが割り当てられる。

   ```shell
   curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:assignBadge" -F "badgeContentPath=/libs/settings/community/badging/images/moderator/jcr:content/moderator.png" https://localhost:4503/home/users/community/w271OOup2Z4DjnOQrviv/profile.social.json
   ```

   ユーザーが 2 つのブロンズバッジを獲得し、モデレーターバッジを獲得すると、フォーラムへのエントリが次のように表示されます。

   ![ 調整者 ](assets/moderator.png)

>[!NOTE]
>
>この例は、次のベストプラクティスには従っていません。
>
>* スコアルール名は、グローバルに一意である必要があります。また、末尾に同じ名前を付けることはできません。
>
>  実行する *ない* の例：
>
>  /libs/settings/community/scoring/rules/site1/forums-scoring
>  /libs/settings/community/scoring/rules/site2/forums-scoring
>
>* 様々なAEM サイト用の一意のバッジ画像の作成

### スコアリング UGC へのアクセス {#access-scoring-ugc}

[API](#scoring-and-badging-apis) の使用をお勧めします。

調査のために、例えば JSRP を使用する場合、スコアを含むベースフォルダーはです

* `/content/usergenerated/asi/jcr/scoring`

`scoring` の子ノードはスコアリング・ルール名です。 したがって、サーバー上のスコアルール名はグローバルに一意であることがベストプラクティスです。

Geometrixxエンゲージメントサイトの場合、ユーザーとそのスコアは、スコアリングルール名、コミュニティサイトのサイト ID （`engage-ba81p`）、一意の ID、ユーザー ID で構成されるパスに格納されます。

* `.../scoring/forums-scoring/engage-ba81p/6d179715c0e93cb2b20886aa0434ca9b5a540401/riley`

コミュニティコンポーネントガイドサイトの場合、ユーザーとそのスコアは、スコアルール名、デフォルト ID （`default-site`）、一意の ID、ユーザー ID で構成されるパス内にあります。

* `.../scoring/forums-scoring/default-site/b27a17cb4910a9b69fe81fb1b492ba672d2c086e/riley`

スコアはプロパティ `scoreValue_tl` に格納されます。このプロパティは、値を含むことのみ、または atomicCounter を間接的に参照することができます。

![access-scoring-ugc](assets/access-scoring-ugc.png)

### アクセスバッジ UGC {#access-badging-ugc}

[API](#scoring-and-badging-apis) の使用をお勧めします。

調査のために、例えば JSRP を使用すると、割り当てられた、または付与されたバッジに関する情報を含むベースフォルダーは次のようになります

* `/content/usergenerated/asi/jcr`

&#x200B;+ ユーザーのプロファイルのパス。末尾には次のようなバッジフォルダーが付きます。

* `/home/users/community/w271OOup2Z4DjnOQrviv/profile/badges`

#### Awished badge {#awarded-badge}

![awdified-badging-ugc](assets/access-badging-ugc.png)

#### 割り当て済みバッジ {#assigned-badge}

![assigned-badge](assets/assigned-badge.png)

## 追加情報 {#additional-information}

点に基づいてメンバーをソートしたリストを表示するには、次の手順に従います。

* コミュニティサイトまたはグループテンプレートに含める [ リーダーボード関数 ](/help/communities/functions.md#leaderboard-function)。
* [ リーダーボードコンポーネント ](/help/communities/enabling-leaderboard.md)：リーダーボード関数の注目のコンポーネントで、ページオーサリング用。
