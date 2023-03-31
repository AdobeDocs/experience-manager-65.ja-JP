---
title: コミュニティサイトの基本事項
seo-title: Community Site Essentials
description: コミュニティサイトの書き出しと削除、およびカスタムサイトテンプレートの作成
seo-description: Exporting and deleting community sites and creating custom site templates
uuid: f0ec0e71-64e9-415a-b14a-939a9b1611c1
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: dc7a085e-d6de-4bc8-bd7e-6b43f8d172d2
exl-id: 1dc568cd-315c-4944-9a3e-e5d7794e5dc0
source-git-commit: cc0574ae22758d095a3ca6b91f0ceae4a8691f0e
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 3%

---

# コミュニティサイトの基本事項 {#community-site-essentials}

## カスタムサイトテンプレート {#custom-site-template}

カスタムサイトテンプレートは、コミュニティサイトの各言語コピーに対して個別に指定できます。

この作業を行うには、以下の手順を実行します。

* カスタムテンプレートを作成します。
* 既定のサイトテンプレートパスをオーバーレイします。
* オーバーレイパスにカスタムテンプレートを追加します。
* カスタムテンプレートを指定するには、 `page-template` プロパティを `configuration` ノード。

**デフォルトのテンプレート**:

`/libs/social/console/components/hbs/sitepage/sitepage.hbs`

**オーバーレイパスのカスタムテンプレート**:

`/apps/social/console/components/hbs/sitepage/template-name.hbs`

**プロパティ**:page-template

**タイプ**:文字列

**値**: `template-name` （拡張子なし）

**設定ノード**:

`/content/community site path/lang/configuration`

例：`/content/sites/engage/en/configuration`

>[!NOTE]
>
>オーバーレイされたパス内のすべてのノードは、タイプのみである必要があります `Folder`.

>[!CAUTION]
>
>カスタムテンプレートに *sitepage.hbs*&#x200B;に設定すると、すべてのコミュニティサイトがカスタマイズされます。

### カスタムサイトテンプレートの例 {#custom-site-template-example}

例えば、 `vertical-sitepage.hbs` は、バナーの下に水平方向ではなく、ページの左側から垂直方向にメニューリンクを配置するサイトテンプレートです。

[ダウンロード](assets/vertical-sitepage.hbs)
オーバーレイフォルダーにカスタムサイトテンプレートを配置します。

`/apps/social/console/components/hbs/sitepage/vertical-sitepage.hbs`

カスタムテンプレートを指定するには、 `page-template` プロパティを設定ノードに設定します。

`/content/sites/sample/en/configuration`

![crxde-siteconfiguration](assets/crxde-siteconfiguration.png)

必ず **すべて保存** すべてのAEMインスタンスにカスタムコードをレプリケートします（コミュニティサイトコンテンツをコンソールから公開する際に、カスタムコードは含まれません）。

カスタムコードをレプリケートする場合の推奨方法は、次のとおりです。 [パッケージの作成](../../help/sites-administering/package-manager.md#creating-a-new-package) すべてのインスタンスにデプロイします。

## コミュニティサイトを書き出す {#exporting-a-community-site}

コミュニティサイトを作成したら、そのサイトをパッケージマネージャーに保存されたAEMパッケージとして書き出し、ダウンロードおよびアップロードできます。

これは、 [コミュニティサイトコンソール](sites-console.md#exporting-the-site).

UGC とカスタムコードはコミュニティサイトパッケージに含まれていません。

UGC を書き出すには、 [AEM Communities UGC 移行ツール](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration):GitHub で利用できるオープンソース移行ツールです。

## コミュニティサイトの削除 {#deleting-a-community-site}

AEM Communities 6.3 Service Pack 1 以降、次の場所からコミュニティサイトにカーソルを合わせると、「サイトを削除」アイコンが表示されます。 **[!UICONTROL コミュニティ]** > **[!UICONTROL サイト]** コンソール。 開発時にコミュニティサイトを削除して新規に開始したい場合は、この機能を使用できます。 コミュニティサイトを削除すると、そのサイトに関連付けられている次の項目が削除されます。

* [UGC](#user-generated-content)
* [ユーザーグループ](#community-user-groups)
* [データベースレコード](#database-records)

### コミュニティの一意のサイト ID {#community-unique-site-id}

CRXDE を使用して、コミュニティサイトに関連付けられた一意のサイト ID を識別するには、次の手順を実行します。

* サイトの言語ルート（例： ）に移動します。 `/content/sites/*<site name>*/en/rep:policy`.

* 次を検索： `allow<#>` ノード `rep:principalName` この形式で `rep:principalName = *community-enable-nrh9h-members*`.

* サイト ID は、 `rep:principalName`

   例えば、 `rep:principalName = community-enable-nrh9h-members`

   * **サイト名** = *有効*
   * **サイト ID** = *nrh9h*
   * **一意のサイト ID** = *enable-nrh9h*

### ユーザー生成コンテンツ {#user-generated-content}

Github から communities-srp-tools プロジェクトを取得します。

* [https://github.com/Adobe-Marketing-Cloud/communities-srp-tools](https://github.com/Adobe-Marketing-Cloud/communities-srp-tools)

SRP からすべての UGC を削除するサーブレットが含まれます。

すべての UGC は、次のように、特定のサイトで削除できます。

* `path=/content/usergenerated/asi/mongo/content/sites/engage`

これにより、ユーザー生成コンテンツ（パブリッシュ時に入力）は削除され、オーサリングコンテンツ（オーサー時に入力）は削除されません。 したがって [シャドウノード](srp.md#shadownodes) は影響を受けません。

### コミュニティユーザーグループ {#community-user-groups}

すべてのオーサーインスタンスとパブリッシュインスタンスで、 [セキュリティコンソール](../../help/sites-administering/security.md)を探し、 [ユーザーグループ](users.md) 次のようになります。

* プレフィックス `community`
* 続いて [一意のサイト id](#community-unique-site-id)

例：`community-engage-x0e11-members`
