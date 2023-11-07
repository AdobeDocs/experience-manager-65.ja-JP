---
title: ページオーサリングのカスタマイズ
description: Adobe Experience Manager(AEM) は、ページオーサリング機能をカスタマイズするための様々なメカニズムを提供します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 90594588-db8e-4d4c-a208-22c1c6ea2a2d
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1339'
ht-degree: 49%

---

# ページオーサリングのカスタマイズ{#customizing-page-authoring}

>[!CAUTION]
>
>このドキュメントでは、最新のタッチ操作対応 UI でページオーサリングをカスタマイズする方法について説明し、クラシック UI には適用されません。

Adobe Experience Manager(AEM) は、ページオーサリング機能 ( および [コンソール](/help/sites-developing/customizing-consoles-touch.md)) を作成します。

* Clientlibs

  clientlibs を使用すると、デフォルトの実装を拡張して新しい機能を実現し、標準の関数、オブジェクト、メソッドを再利用できます。 カスタマイズする際に、独自のクライアントライブラリを `/apps.` に作成できます。新しいクライアントライブラリには次の条件があります。

   * オーサリングクライアントライブラリ `cq.authoring.editor.sites.page` を使用する必要があります。
   * 適切な `cq.authoring.editor.sites.page.hook` カテゴリに含める必要があります。

* オーバーレイ

  オーバーレイはノード定義に基づいており、 `/libs`) をカスタマイズした独自の機能 ( `/apps`) をクリックします。 [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) は継承を許可しているので、オーバーレイを作成するときに、オリジナルの 1 対 1 のコピーは必要ありません。

>[!NOTE]
>
>詳しくは、 [JS ドキュメントセット](https://developer.adobe.com/experience-manager/reference-materials/6-5/jsdoc/ui-touch/editor-core/index.html).

これらは、AEMインスタンスでページオーサリング機能を拡張するための様々な方法で使用できます。 以下では、選択範囲（概要レベル）について説明します。

>[!NOTE]
>
>詳しくは、以下を参照してください。
>
>* の使用と作成 [clientlibs](/help/sites-developing/clientlibs.md).
>* の使用と作成 [overlays](/help/sites-developing/overlays.md).
>* [Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)
>* ページオーサリングに使用される構造について詳しくは、[AEM タッチ操作対応 UI の構造](/help/sites-developing/touch-ui-structure.md)を参照してください。
>


>[!CAUTION]
>
>******`/libs` パス内は一切変更しないでください。
>
>理由は、次の内容が原因です： `/libs` が上書きされる場合は、次回インスタンスをアップグレードするとき（ホットフィックスまたは機能パックを適用したときに上書きされる場合があります）。
>
>設定およびその他の変更に推奨される方法は次のとおりです。
>
>1. 必要な項目（内に存在）を再作成します。 `/libs`) （下） `/apps`
>1. `/apps` 内で変更作業をおこないます。

## 新しいレイヤー（モード）の追加 {#add-new-layer-mode}

ページを編集する際には、様々な操作が行われます [モード](/help/sites-authoring/author-environment-tools.md#page-modes) 使用可能 これらのモードは、 [レイヤー](/help/sites-developing/touch-ui-structure.md#layer). これにより、同じページコンテンツに対して、異なるタイプの機能にアクセスできます。 標準のレイヤーは、編集、プレビュー、注釈、開発者、ターゲティングです。

### レイヤーの例：ライブコピーステータス {#layer-example-live-copy-status}

標準のAEMインスタンスは MSM レイヤーを提供します。 これにより、 [マルチサイト管理](/help/sites-administering/msm.md) レイヤでハイライト表示します。

実際に表示するには、次の項目を編集します。 [We.Retail 言語コピー](/help/sites-developing/we-retail-globalized-site-structure.md) ページ（または他のライブコピーページ）を選択し、 **ライブコピーステータス** モード。

MSM レイヤーの定義（参照用）は、次のファイルにあります。

`/libs/wcm/msm/content/touch-ui/authoring/editor/js/msm.Layer.js`

### コードサンプル {#code-sample}

これは、MSM ビュー用の新しいレイヤーであるレイヤー（モード）の作成方法を示すサンプルパッケージです。

GitHub のコード

このページのコードは GitHub にあります

* [GitHub の aem-authoring-new-layer-mode プロジェクトを開きます](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode)
* プロジェクトを [ZIP ファイル](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode/archive/master.zip)としてダウンロードします

## 新しい選択カテゴリをアセットブラウザに追加 {#add-new-selection-category-to-asset-browser}

アセットブラウザーには、様々なタイプ/カテゴリ（画像やドキュメントなど）のアセットが表示されます。 このようなアセットカテゴリを使用して、アセットをフィルターすることもできます。

### コードサンプル {#code-sample-1}

`aem-authoring-extension-assetfinder-flickr` は、アセットファインダーにグループを追加する方法を示すサンプルパッケージです。 この例は、 [Flickr](https://www.flickr.com)のパブリックストリームを参照し、サイドパネルに表示します。

GitHub のコード

このページのコードは GitHub にあります

* [GitHub の aem-authoring-extension-assetfinder-flickr プロジェクトを開きます](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr)
* プロジェクトを [ZIP ファイル](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr/archive/master.zip)としてダウンロードします

## リソースのフィルタリング {#filtering-resources}

ページをオーサリングする際に、多くの場合、ユーザーはリソース（ページ、コンポーネント、アセットなど）から選択する必要があります。 これは、例えば、作成者が項目を選択する必要があるリストの形式を取ることができます。

リストを適切なサイズに保ち、使用例にも関連するように、フィルターをカスタム述語の形式で実装できます。 例えば、[`pathbrowser`](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) [Granite](/help/sites-developing/touch-ui-concepts.md#granite-ui) コンポーネントを使用してユーザーが特定のリソースへのパスを選択できるようにするには、表示されるパスを次のようにフィルタリングできます。

* [`com.day.cq.commons.predicate.AbstractNodePredicate`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/predicate/package-summary.html) インターフェイスを実装してカスタム述語を実装します。
* 述語の名前を指定し、`pathbrowser`を使用するときにその名前を参照します。

カスタム述語の作成について詳しくは、[この記事](/help/sites-developing/implementing-custom-predicate-evaluator.md)を参照してください。

>[!NOTE]
>
>`com.day.cq.commons.predicate.AbstractNodePredicate` インターフェイスの実装によるカスタム述語の実装は、クラシック UI でも機能します。
>
>詳しくは、 [このナレッジベース記事](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=ja) クラシック UI でのカスタム述語の実装例を示します。

## 新しいアクションをコンポーネントツールバーに追加 {#add-new-action-to-a-component-toolbar}

各コンポーネント（通常）には、そのコンポーネントで実行できる様々なアクションにアクセスできるツールバーがあります。

### コードサンプル {#code-sample-2}

`aem-authoring-extension-toolbar-screenshot`は、コンポーネントをレンダリングするカスタムツールバーアクションを作成する方法を示すサンプルパッケージです。

GitHub のコード

このページのコードは GitHub にあります

* [GitHub の aem-authoring-extension-toolbar-screenshot プロジェクトを開きます](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot)
* プロジェクトを [ZIP ファイル](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot/archive/master.zip)としてダウンロードします

## 新しいインプレースエディターを追加 {#add-new-in-place-editor}

### 標準インプレースエディタ {#standard-in-place-editor}

標準 AEM インストールでは、

1. `/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js`

   使用可能な各種エディターの定義を保持します。

1. エディターと、それを使用できる各リソースタイプ（コンポーネントなど）との間には、次のような接続があります。

   * `cq:inplaceEditing`

     次に例を示します。

      * `/libs/foundation/components/text/cq:editConfig`
      * `/libs/foundation/components/image/cq:editConfig`

         * プロパティ：`editorType`

           そのコンポーネントに対してインプレース編集が呼び出された場合に使用されるインラインエディターのタイプを定義します。例： `text`, `textimage`, `image`, `title`.

1. エディターの追加の設定の詳細は、 `config` 設定を含むノード `plugin` 必要なプラグイン設定の詳細を含むノード。

   画像コンポーネントの画像切り抜きプラグインの縦横比を定義する例を次に示します。画面サイズが制限されている可能性があるので、切り抜きの縦横比は全画面表示エディターに移動され、そこでのみ表示できます。

   ```xml
   <cq:inplaceEditing
           jcr:primaryType="cq:InplaceEditingConfig"
           active="{Boolean}true"
           editorType="image">
           <config jcr:primaryType="nt:unstructured">
               <plugins jcr:primaryType="nt:unstructured">
                   <crop jcr:primaryType="nt:unstructured">
                       <aspectRatios jcr:primaryType="nt:unstructured">
                           <_x0031_6-10
                               jcr:primaryType="nt:unstructured"
                               name="16 : 10"
                               ratio="0.625"/>
                       </aspectRatios>
                   </crop>
               </plugins>
           </config>
   </cq:inplaceEditing>
   ```

   >[!CAUTION]
   >
   >AEMの切り抜き率 ( `ratio` プロパティは、次のように定義されます。 **高さ/幅**. これは従来の定義である「幅/高さ」とは異なり、レガシー互換性のための設定です。`name` プロパティを明確に定義していれば、UI に表示されるので、オーサリングユーザーは違いを認識しません。

#### 新しいインプレースエディターの作成 {#creating-a-new-in-place-editor}

新しいインプレースエディターを（クライアントライブラリ内に）実装するには、次のようにします。

>[!NOTE]
>
>例として、次を参照してください。
>`/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js`

1. 実装方法：

   * `setUp`
   * `tearDown`

1. エディター（コンストラクタを含む）の登録：

   * `editor.register`

1. エディターと、エディターを使用できる各リソースタイプが（コンポーネントと同様に）関連付けられます。

#### 新しいインプレースエディターを作成するためのコードサンプル {#code-sample-for-creating-a-new-in-place-editor}

`aem-authoring-extension-inplace-editor` は、AEMでインプレースエディターを作成する方法を示すサンプルパッケージです。

GitHub のコード

このページのコードは GitHub にあります

* [GitHub の aem-authoring-extension-inplace-editor プロジェクトを開きます](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor)
* プロジェクトを [ZIP ファイル](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor/archive/master.zip)としてダウンロードします

#### 複数のインプレースエディターの設定 {#configuring-multiple-in-place-editors}

複数のインプレースエディターを含むようにコンポーネントを設定できます。 複数のインプレースエディターを設定した場合は、適切なコンテンツを選択し、適切なエディターを開くことができます。 詳しくは、[複数のインプレースエディターの設定](/help/sites-developing/multiple-inplace-editors.md)ドキュメントを参照してください。

## 新しいページアクションを追加 {#add-a-new-page-action}

新しいページアクションをページツールバーに追加するには、次のようにします。 **サイトに戻る** （コンソール）アクションを使用します。

### コードサンプル {#code-sample-3}

`aem-authoring-extension-header-backtosites` は、サイトコンソールに戻るカスタムヘッダーバーアクションを作成する方法を示すサンプルパッケージです。

GitHub のコード

このページのコードは GitHub にあります

* [GitHub の aem-authoring-extension-header-backtosites プロジェクトを開きます](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites)
* プロジェクトを [ZIP ファイル](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites/archive/master.zip)としてダウンロードします

## アクティベーションをリクエストワークフローのカスタマイズ {#customizing-the-request-for-activation-workflow}

標準のワークフロー、**アクティベーションのリクエスト**：

* コンテンツ作成者が適切なレプリケーション権限&#x200B;**を持っていない**&#x200B;が DAM-Users および作成者のメンバーシップ&#x200B;**を持っている**&#x200B;場合、適切なメニューに自動的に表示されます 。

* レプリケーション権限が削除されているので、何も表示されません。

このようなアクティベーションで動作をカスタマイズするには、 **アクティベーションのリクエスト** ワークフロー：

1.  `/apps`で **Sites** ウィザードをオーバーレイします。

   `/libs/wcm/core/content/common/managepublicationwizard`

   >[!NOTE]
   >
   >これ自体は、次の一般的なインスタンスを上書きします。
   >
   >`/libs/cq/gui/content/common/managepublicationwizard`

1. 必要に応じて、[ワークフローモデル](/help/sites-developing/workflows-models.md)および関連設定／スクリプトを更新します。
1. ユーザーがページを公開（またはレプリケート）しようとする際にこのワークフローをデフォルトのアクションとしてトリガーさせるには、すべての関連するページのすべての適切なユーザーから[`replicate`  アクション](/help/sites-administering/security.md#actions)の権限を削除します。
