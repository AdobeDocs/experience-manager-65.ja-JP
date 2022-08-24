---
title: コミュニティサイトの基本事項
seo-title: Community Site Essentials
description: コミュニティサイトのエクスポートと削除およびカスタムサイトテンプレートの作成
seo-description: Exporting and deleting community sites and creating custom site templates
uuid: f0ec0e71-64e9-415a-b14a-939a9b1611c1
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: dc7a085e-d6de-4bc8-bd7e-6b43f8d172d2
exl-id: 1dc568cd-315c-4944-9a3e-e5d7794e5dc0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 59%

---

# コミュニティサイトの基本事項 {#community-site-essentials}

## カスタムサイトテンプレート {#custom-site-template}

カスタムサイトテンプレートは、コミュニティサイトの言語コピーごとに個別に指定できます。

この作業を行うには、以下の手順を実行します。

* カスタムテンプレートを作成します。
* 既定のサイトテンプレートパスをオーバーレイします。
* オーバーレイパスにカスタムテンプレートを追加します。
* カスタムテンプレートを指定するには、 `page-template` プロパティを `configuration` ノード。

**デフォルトのテンプレート**：

`/libs/social/console/components/hbs/sitepage/sitepage.hbs`

**オーバーレイのパスのカスタムテンプレート**：

`/apps/social/console/components/hbs/sitepage/template-name.hbs`

**プロパティ**:page-template

**種類**：string

**値**: `template-name` （拡張子なし）

**設定ノード**：

`/content/community site path/lang/configuration`

例：`/content/sites/engage/en/configuration`

>[!NOTE]
>
>オーバーレイされたパスのすべてのノードのタイプは、`Folder` である必要があります。

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

「**すべて保存**」を選択してカスタムコードをすべての AEM インスタンスにレプリケートしてください（コミュニティサイトコンテンツがコンソールから公開された時点ではカスタムコードは含まれていません）。

カスタムコードをレプリケートするには、[パッケージを作成](../../help/sites-administering/package-manager.md#creating-a-new-package)し、すべてのインスタンスにデプロイすることをお勧めします。

## コミュニティサイトの書き出し {#exporting-a-community-site}

コミュニティサイトが作成されたら、パッケージマネージャーに保存され、ダウンロードおよびアップロードできる AEM パッケージとしてそのサイトを書き出すことができます。

書き出しは、[コミュニティサイトコンソール](sites-console.md#exporting-the-site)からおこなうことができます。

UGC とカスタムコードはコミュニティサイトパッケージに含まれていないことに注意してください。

UGC を書き出すには、 [AEM Communities UGC 移行ツール](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration):GitHub で利用できるオープンソース移行ツールです。

## コミュニティサイトの削除 {#deleting-a-community-site}

AEM Communities 6.3 Service Pack 1 以降、次の場所からコミュニティサイトにカーソルを合わせると、「サイトを削除」アイコンが表示されます。 **[!UICONTROL コミュニティ]** > **[!UICONTROL サイト]** コンソール。 開発時にコミュニティサイトを削除して新規に開始したい場合は、この機能を使用できます。 コミュニティサイトを削除すると、そのサイトに関連付けられている次のアイテムが削除されます。

* [UGC](#user-generated-content)
* [ユーザーグループ](#community-user-groups)
* [Assets](#enablement-assets)
* [データベースレコード](#database-records)

### コミュニティの一意のサイト ID {#community-unique-site-id}

CRXDE を使用して、コミュニティに関連付けられている一意のサイト ID を識別するには、次の手順に従います。

* サイトの言語ルート（例： ）に移動します。 `/content/sites/*<site name>*/en/rep:policy`.

* 次を検索： `allow<#>` ノード `rep:principalName` この形式で `rep:principalName = *community-enable-nrh9h-members*`.

* サイト ID は、 `rep:principalName`

   例えば、`rep:principalName = community-enable-nrh9h-members`

   * **サイト名** = *enable*
   * **サイト ID** = *nrh9h*
   * **一意のサイト ID** = *enable-nrh9h*

### ユーザー生成コンテンツ {#user-generated-content}

Github から communities-srp-tools プロジェクトを取得します。

* [https://github.com/Adobe-Marketing-Cloud/communities-srp-tools](https://github.com/Adobe-Marketing-Cloud/communities-srp-tools)

これには、任意の SRP からすべての UGC を削除できるサーブレットが含まれています。

次の例に示すように、特定のサイトを対象としてすべての UGC を削除できます。

* `path=/content/usergenerated/asi/mongo/content/sites/engage`

この場合、（パブリッシュインスタンスで入力された）ユーザー生成コンテンツのみが削除され、（オーサーインスタンスで入力された）作成コンテンツは削除されません。したがって [シャドウノード](srp.md#shadownodes) は影響を受けません。

### コミュニティユーザーグループ {#community-user-groups}

すべてのオーサーインスタンスおよびパブリッシュインスタンスで、[セキュリティコンソール](../../help/sites-administering/security.md)から、以下に該当する[ユーザーグループ](users.md)を検索して削除します。

* プレフィックス `community`
* 続いて [一意のサイト id](#community-unique-site-id)

（例：`community-engage-x0e11-members`）。

### イネーブルメントアセット {#enablement-assets}

メインコンソールから、次の手順に従います。

* 選択 **[!UICONTROL Assets]**.
* 入力 **[!UICONTROL 選択]** モード。
* 次を使用してという名前のフォルダーを選択します。 [一意のサイト ID](#community-unique-site-id).
* 選択 **[!UICONTROL 削除]** ( 次の中から選択する必要がある場合があります： **[!UICONTROL さらに詳しく…]**) をクリックします。

### データベースレコード {#database-records}

特定のイネーブルメントコミュニティサイトの 1 つを対象として、データベースエントリを選択的に削除するためのツールはありません。

すべてのコミュニティサイトを削除する場合は、MySQL Workbench を使用して enablementdb および scormenginedb を削除します。
