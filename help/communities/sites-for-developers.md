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
* を追加して、カスタムテンプレートを指定します。 `page-template` プロパティを `configuration` ノード。

**デフォルトのテンプレート**:

`/libs/social/console/components/hbs/sitepage/sitepage.hbs`

**オーバーレイパスのカスタムテンプレート**:

`/apps/social/console/components/hbs/sitepage/template-name.hbs`

**プロパティ**: ページテンプレート

**タイプ**：文字列

**値**: `template-name` （拡張子なし）

**設定ノード**:

`/content/community site path/lang/configuration`

例：`/content/sites/engage/en/configuration`

>[!NOTE]
>
>オーバーレイパス内のすべてのノードは、型である必要があります `Folder`.

>[!CAUTION]
>
>カスタムテンプレートに名前が付けられている場合 *sitepage.hbs*&#x200B;を選択すると、すべてのコミュニティサイトがカスタマイズされます。

### カスタムサイトテンプレートの例 {#custom-site-template-example}

例えば、 `vertical-sitepage.hbs` は、ページの左側に、バナーの下に水平方向ではなく垂直方向にメニューリンクを配置するサイトテンプレートです。

[ファイルを入手](assets/vertical-sitepage.hbs)
カスタムサイトテンプレートをオーバーレイフォルダーに配置します。

`/apps/social/console/components/hbs/sitepage/vertical-sitepage.hbs`

を追加してカスタムテンプレートを識別 `page-template` 設定ノードのプロパティ：

`/content/sites/sample/en/configuration`

![crxde-siteconfiguration](assets/crxde-siteconfiguration.png)

必ずしてください **すべて保存** すべてのAdobe Experience Manager（AEM）インスタンスにカスタムコードを複製します（コミュニティサイトのコンテンツがコンソールから公開される場合、カスタムコードは含まれません）。

カスタムコードをレプリケートする場合は、次の方法をお勧めします。 [パッケージを作成](../../help/sites-administering/package-manager.md#creating-a-new-package) すべてのインスタンスにデプロイします。

## コミュニティサイトのエクスポート {#exporting-a-community-site}

コミュニティサイトを作成したら、パッケージマネージャーに格納され、ダウンロードとアップロードに使用できるAEM パッケージとしてサイトをエクスポートできます。

これは、次から利用できます [コミュニティサイトコンソール](sites-console.md#exporting-the-site).

UGC とカスタムコードは、コミュニティサイトパッケージには含まれていません。

UGC を書き出すには、 [AEM Communities UGC Migration Tool](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration):GitHub で利用可能なオープンソース移行ツールです。

## コミュニティサイトの削除 {#deleting-a-community-site}

現在のAEM Communities 6.3 Service Pack 1 では、コミュニティサイトの上にカーソルを置くと、「サイトを削除」アイコンが表示されます。 **[!UICONTROL コミュニティ]** > **[!UICONTROL Sites]** コンソール。 開発時にコミュニティサイトを削除して新しく開始する場合は、この機能を使用できます。 コミュニティサイトを削除すると、そのサイトに関連付けられている次の項目が削除されます。

* [UGC](#user-generated-content)
* [ユーザーグループ](#community-user-groups)
* [データベースレコード](#database-records)

### コミュニティユニークサイト ID {#community-unique-site-id}

CRXDE を使用して、コミュニティサイトに関連付けられている一意のサイト ID を識別するには：

* 次のようなサイトの言語ルートに移動します `/content/sites/*<site name>*/en/rep:policy`.

* の検索 `allow<#>` を持つノード `rep:principalName` 次の形式で `rep:principalName = *community-enable-nrh9h-members*`.

* サイト ID は、の 3 番目のコンポーネントです。 `rep:principalName`

  例えば、 `rep:principalName = community-enable-nrh9h-members`

   * **サイト名** = *enable*
   * **サイト ID** = *nrh9h*
   * **ユニークサイト ID** = *enable-nrh9h*

### ユーザー作成コンテンツ {#user-generated-content}

GitHub から communities-srp-tools プロジェクトを取得します。

* [https://github.com/Adobe-Marketing-Cloud/aem-communities-srp-tools](https://github.com/Adobe-Marketing-Cloud/aem-communities-srp-tools)

これには、任意の SRP からすべての UGC を削除するサーブレットが含まれています。

すべての UGC は、例えば、次のような特定のサイトに対して削除することができます。

* `path=/content/usergenerated/asi/mongo/content/sites/engage`

これにより、ユーザー作成コンテンツ（公開時に入力）のみが削除され、作成したコンテンツ（作成者に入力）は削除されません。 したがって、 [シャドウ ノード](srp.md#shadownodes) 影響を受けません。

### コミュニティユーザーグループ {#community-user-groups}

すべてのオーサーインスタンスとパブリッシュインスタンスで、次から [セキュリティコンソール](../../help/sites-administering/security.md)を見つけて、削除します。 [ユーザーグループ](users.md) 次のとおりです。

* プレフィックスが「」の場合 `community`
* 続いて [一意のサイト id](#community-unique-site-id)

例えば、`community-engage-x0e11-members` のように指定します。
