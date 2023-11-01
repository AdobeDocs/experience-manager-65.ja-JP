---
title: コンソールのカスタマイズ
seo-title: Customizing the Consoles
description: AEMには、オーサーインスタンスのコンソールをカスタマイズできる様々なメカニズムが用意されています。
seo-description: AEM provides various mechanisms to enable you to customize the consoles of your authoring instance
uuid: 8ecce9ff-5907-41e1-af3b-a8646352d633
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 61a4e196-bd53-4ef0-816b-c14401462457
docset: aem65
exl-id: 6e67f2b3-78b9-45f2-b496-61776b9fd9cc
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '667'
ht-degree: 50%

---

# コンソールのカスタマイズ {#customizing-the-consoles}

>[!CAUTION]
>
>このドキュメントでは、最新のタッチ操作対応 UI でコンソールをカスタマイズする方法について説明します。クラシック UI には適用されません。

AEMは、コンソール ( および [ページオーサリング機能](/help/sites-developing/customizing-page-authoring-touch.md)) を作成します。

* clientlibs Clientlibs を使用すると、デフォルトの実装を拡張して新しい機能を実現し、標準の関数、オブジェクト、メソッドを再利用できます。 カスタマイズするときに、独自の clientlib を `/apps.` に作成して、カスタムコンポーネントに必要なコードを保持するといった操作が可能です。

* オーバーレイオーバーレイはノード定義に基づいており、標準の機能 ( `/libs`) をカスタマイズした独自の機能 ( `/apps`) をクリックします。 Sling Resource Merger は継承を許可しているので、オーバーレイを作成するときに、オリジナルの 1 対 1 のコピーは必要ありません。

これらは、AEMコンソールを拡張するための様々な方法で使用できます。 一部については、以降で（大まかに）説明します。

>[!NOTE]
>
>詳しくは、次のセクションを参照してください。
>
>* の使用と作成 [clientlibs](/help/sites-developing/clientlibs.md).
>* の使用と作成 [overlays](/help/sites-developing/overlays.md).
>* [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)
>


>[!CAUTION]
>
>`/libs` パス内の設定は&#x200B;***一切***&#x200B;変更しないでください。
>
>`/libs` コンテンツは、インスタンスを次回アップグレードするとき（場合によってはホットフィックスまたは機能パックを適用したとき）に上書きされるからです。
>
>設定およびその他の変更に推奨される方法は次のとおりです。
>
>1. 必要な項目（`/libs`内に存在）を、`/apps`の下で再作成します。
>
>1. `/apps` 内で変更作業をおこないます。
>

例えば、`/libs` 構造内の以下の場所をオーバーレイできます。

* コンソール（Granite UI ページに基づくすべてのコンソール）。次に例を示します。

   * `/libs/wcm/core/content`

>[!NOTE]
>
>ヒントおよびツールについて詳しくは、ナレッジベースの記事「[Troubleshooting AEM TouchUI issues](https://helpx.adobe.com/jp/experience-manager/kb/troubleshooting-aem-touchui-issues.html)」を参照してください。

## コンソールのデフォルト表示のカスタマイズ {#customizing-the-default-view-for-a-console}

コンソールのデフォルトの表示（列、カード、リスト）をカスタマイズできます。

1. ビューの順序を変更するには、次の場所から必要なエントリをオーバーレイします。

   `/libs/wcm/core/content/sites/jcr:content/views`

   先頭のエントリがデフォルトになります。

   使用可能なノードは、使用可能な表示オプションに関連付けられます。

   * `column`
   * `card`
   * `list`

1. 例えば、リスト用のオーバーレイで、

   `/apps/wcm/core/content/sites/jcr:content/views/list`

   次のプロパティを定義します。

   * **名前**：`sling:orderBefore`
   * **型**：`String`
   * **値**: `column`

### ツールバーに新しいアクションを追加する {#add-new-action-to-the-toolbar}

1. 独自のコンポーネントを構築し、対応するカスタムアクション用のクライアントライブラリを含めることができます。 例えば、 **twitterに昇格** アクション：

   `/apps/wcm/core/clientlibs/sites/js/twitter.js`

   このアクションを独自コンソールのツールバー項目に関連付けることができます。

   `/apps/<yourProject>/admin/ext/launches`

   選択モードの例：

   `content/jcr:content/body/content/header/items/selection/items/twitter`

### 特定のグループにツールバーアクションを制限する {#restrict-a-toolbar-action-to-a-specific-group}

1. カスタムのレンダリング条件を使用して、標準のアクションをオーバーレイし、レンダリング前に満たす必要のある特定の条件を課すことができます。

   例えば、グループに従ってレンダリング条件を制御するコンポーネントを作成します。

   `/apps/myapp/components/renderconditions/group`

1. これをサイトコンソールの「サイトを作成」アクションに適用するには、

   `/libs/wcm/core/content/sites`

   オーバーレイを作成します。

   `/apps/wcm/core/content/sites`

1. このアクションのレンダリング条件を追加します。

   `jcr:content/body/content/header/items/default/items/create/items/createsite/rendercondition`

   このノードのプロパティを使用して、特定のアクションを実行できる `groups`（`administrators` など）を定義できます。

### リスト表示で列のカスタマイズ {#customizing-columns-in-the-list-view}

>[!NOTE]
>
>この機能は、テキストフィールドの列に対して最適化されています。その他のデータタイプに対しては、`/apps` の `cq/gui/components/siteadmin/admin/listview/columns/analyticscolumnrenderer` をオーバーレイできます。

リスト表示の列をカスタマイズするには：

1. 使用可能な列のリストをオーバーレイします。

   * ノードの場合：

     ```
            /apps/wcm/core/content/common/availablecolumns
     ```

   * 新しい列を追加、または既存の列を削除します。

   詳しくは、[オーバーレイ（および Sling Resource Merger）の使用](/help/sites-developing/overlays.md)を参照してください。

1. 省略可能：

   * 追加データを挿入する場合は、以下を持つ [PageInforProvider](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageInfoProvider.html) を記述する必要があります。
     `pageInfoProviderType` property.

   例えば、以下の GitHub から添付されたクラス/バンドルを参照してください。

1. これで、リスト表示の列コンフィギュレーターで列を選択できるようになりました。

### リソースのフィルタリング {#filtering-resources}

コンソールを使用する場合、一般的な使用例は、リソース（ページ、コンポーネント、アセットなど）から選択する必要がある場合です。 これは、例えば、作成者が項目を選択する必要があるリストの形式をとることができます。

リストを適切なサイズに保ち、使用例にも関連するように、フィルターをカスタム述語の形式で実装できます。 詳しくは、 [この記事](/help/sites-developing/customizing-page-authoring-touch.md#filtering-resources) 」を参照してください。
