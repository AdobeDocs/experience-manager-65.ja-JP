---
title: コミュニティサイトの基本事項
description: コミュニティサイトの書き出しと削除およびカスタムサイトテンプレートの作成
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 1dc568cd-315c-4944-9a3e-e5d7794e5dc0
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 3%

---

# コミュニティサイトの基本事項 {#community-site-essentials}

## カスタムサイトテンプレート {#custom-site-template}

カスタムサイトテンプレートは、コミュニティサイトの言語コピーごとに個別に指定できます。

この作業を行うには、以下の手順を実行します。

* カスタムテンプレートを作成します。
* デフォルトのサイトテンプレートパスをオーバーレイします。
* オーバーレイパスにカスタムテンプレートを追加します。
* `configuration` ノードに `page-template` プロパティを追加して、カスタムテンプレートを指定します。

**デフォルトのテンプレート**:

`/libs/social/console/components/hbs/sitepage/sitepage.hbs`

**オーバーレイパスのカスタムテンプレート**:

`/apps/social/console/components/hbs/sitepage/template-name.hbs`

**プロパティ**:page-template

**タイプ**：文字列

**値**:`template-name` （拡張子なし）

**設定ノード**:

`/content/community site path/lang/configuration`

例：`/content/sites/engage/en/configuration`

>[!NOTE]
>
>オーバーレイパス内のすべてのノードは、タイプ `Folder` である必要があります。

>[!CAUTION]
>
>*sitepage.hbs* という名前をカスタムテンプレートに付けると、すべてのコミュニティサイトがカスタマイズされます。

### カスタムサイトテンプレートの例 {#custom-site-template-example}

例えば、`vertical-sitepage.hbs` は、ページの左側を水平方向に下にするのではなく、垂直方向に下にメニューリンクを配置するサイトテンプレートです。

[ ファイルを入手 ](assets/vertical-sitepage.hbs)
カスタムサイトテンプレートをオーバーレイフォルダーに配置します。

`/apps/social/console/components/hbs/sitepage/vertical-sitepage.hbs`

設定ノードに `page-template` プロパティを追加して、カスタムテンプレートを識別します。

`/content/sites/sample/en/configuration`

![crxde-siteconfiguration](assets/crxde-siteconfiguration.png)

**すべて保存** してすべてのAdobe Experience Manager（AEM）インスタンスにカスタムコードをレプリケートしてください（コミュニティサイトのコンテンツがコンソールから公開される場合、カスタムコードは含まれません）。

カスタムコードをレプリケートする場合は、[ パッケージを作成 ](../../help/sites-administering/package-manager.md#creating-a-new-package) してすべてのインスタンスにデプロイすることをお勧めします。

## コミュニティサイトのエクスポート {#exporting-a-community-site}

コミュニティサイトを作成したら、パッケージマネージャーに格納され、ダウンロードとアップロードに使用できるAEM パッケージとしてサイトをエクスポートできます。

これは、[Communities サイトコンソール ](sites-console.md#exporting-the-site) から利用できます。

UGC とカスタムコードは、コミュニティサイトパッケージには含まれていません。

UGC を書き出すには、GitHub で利用可能なオープンソースの移行ツールである {0[&#128279;](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration)AEM Communities UGC Migration Tool} を使用します。

## コミュニティサイトの削除 {#deleting-a-community-site}

AEM Communities 6.3 Service Pack 1 の時点では、（Communities **/**&#x200B;[!UICONTROL &#x200B; Sites &#x200B;]&#x200B;**コンソールでコミュニティサイトの上にマウスポインターを置くと、「サイトを削除** アイコンが表示されます。 開発時にコミュニティサイトを削除して新しく開始する場合は、この機能を使用できます。 コミュニティサイトを削除すると、そのサイトに関連付けられている次の項目が削除されます。

* [UGC](#user-generated-content)
* [ユーザーグループ](#community-user-groups)
* [データベースレコード](#database-records)

### コミュニティユニークサイト ID {#community-unique-site-id}

CRXDE を使用して、コミュニティサイトに関連付けられている一意のサイト ID を識別するには：

* サイトの言語ルート（`/content/sites/*<site name>*/en/rep:policy` など）に移動します。

* この形式の `rep:principalName = *community-enable-nrh9h-members*` で `rep:principalName` を持つ `allow<#>` ノードを検索します。

* サイト ID は、`rep:principalName` の 3 番目のコンポーネントです

  例えば、次の場合：`rep:principalName = community-enable-nrh9h-members`

   * **サイト名** = *有効*
   * **サイト ID** = *nrh9h*
   * **unique site ID** = *enable-nrh9h*

### ユーザー作成コンテンツ {#user-generated-content}

GitHub から communities-srp-tools プロジェクトを取得します。

* [https://github.com/Adobe-Marketing-Cloud/aem-communities-srp-tools](https://github.com/Adobe-Marketing-Cloud/aem-communities-srp-tools)

これには、任意の SRP からすべての UGC を削除するサーブレットが含まれています。

すべての UGC は、例えば、次のような特定のサイトに対して削除することができます。

* `path=/content/usergenerated/asi/mongo/content/sites/engage`

これにより、ユーザー作成コンテンツ（公開時に入力）のみが削除され、作成したコンテンツ（作成者に入力）は削除されません。 したがって、[ シャドウノード ](srp.md#shadownodes) は影響を受けません。

### コミュニティユーザーグループ {#community-user-groups}

すべてのオーサーインスタンスおよびパブリッシュインスタンスで、[ セキュリティコンソール ](../../help/sites-administering/security.md) から、以下に該当する [ ユーザーグループ ](users.md) を見つけて削除します。

* 先頭に `community` が付いています
* &#x200B;+ [ 一意のサイト ID](#community-unique-site-id)

例えば、`community-engage-x0e11-members` のように指定します。
