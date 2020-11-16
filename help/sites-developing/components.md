---
title: コンポーネント 概要
seo-title: コンポーネント
description: コンポーネントは、特定の機能を実現し、Web サイトにコンテンツを提供するためのモジュールユニットです。
seo-description: コンポーネント特定の機能を実現し、Web サイトにコンテンツを提供するためのモジュールユニットです。
uuid: fb39aeb8-8f43-4091-8083-ebfab89e6e63
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 45efff93-2fe5-4313-83a0-0e23a540da93
translation-type: tm+mt
source-git-commit: 5597fb39500ac1f85d03263bfa1e5239d35d2a2c
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 67%

---


# コンポーネントの概要{#components-overview}

このページでは、[ページオーサリングで使用される](/help/sites-authoring/default-components-foundation.md)コンポーネントなど、Adobe Experience Manager（AEM）のコンポーネントの概要を示します。

## コンポーネントとは{#what-exactly-is-a-component}

* Webサイトにコンテンツを表示するための特定の機能を実現するモジュラー型ユニット。
* 再利用可能。
* リポジトリの1つのフォルダー内に自己完結型のユニットとして開発。
* 非表示の設定ファイルを持ちません。
* 他のコンポーネントを組み込むことができます。
* AEM システム内であれば、どの場所でも実行できます。特定のコンポーネントにおいてのみ実行できるようにすることもできます。
* 標準化されたユーザーインターフェイスがあります。
* 設定可能な編集動作がある。
* Granite UIコンポーネントに基づくサブ要素を使用して構築されたダイアログボックスを使用する
* Are developed using [HTL](https://docs.adobe.com/content/help/ja-JP/experience-manager-htl/using/overview.html) (recommended) or JSP.
* デフォルトの機能を拡張するカスタマイズされたコンポーネントを作成するために開発できます。

コンポーネントはモジュールなので、次のことができます。

* ローカルインスタンスで新しいコンポーネントを開発する。
* テスト環境に展開します。
* ライブオーサリング環境にデプロイする。そこで、作成者や管理者のコンテンツの追加および設定を許可します。
* ライブパブリッシュ環境にデプロイします。この画像を使用して、Webサイトの訪問者向けにコンテンツをレンダリングします。 また、特定のコンポーネント（コミュニティ用など）がユーザーからの入力を受け入れます。

各 AEM コンポーネント：

* リソースタイプです。
* 特定の機能を完全に実現するスクリプトの集まりです。
* Can function in *isolation*, meaning either within AEM or a portal.

## AEM 内の既成のコンポーネント {#out-of-the-box-components-within-aem}

AEM には、次のような包括的な機能を提供する、](/help/sites-authoring/default-components.md)すぐに使用できる様々なコンポーネント[が付属しています。

* 段落システム ( `parsys`)
* Page ( `responsivegrid` - touch-enabled UI only)
* テキスト
* 画像（説明テキスト付き）
* ツールバー

提供される[サンプル We.Retail Web サイト](/help/sites-developing/we-retail.md)内で提供されるコンポーネントおよびそれらの使用方法は、コンポーネントの実装および使用方法の例です。コンポーネントは、すべてのソースコードと共に提供されており、そのまま使用することも、コンポーネントを変更または拡張する出発点として使用することもできます。

### コアコンポーネントおよび基盤コンポーネント {#core-components-and-foundation-components}

アドビが提供する AEM コンポーネントには 2 つのセットがあります。

* [コアコンポーネント](https://docs.adobe.com/content/help/ja-JP/experience-manager-core-components/using/introduction.html)
* [基盤コンポーネント](/help/sites-authoring/default-components-foundation.md)

**コアコンポーネント** はAEM 6.3で導入され、オファーの柔軟で豊富な機能を備えたオーサリング機能を備えています。 The [We.Retail reference site](/help/sites-developing/we-retail.md) illustrates how the core components can be used and represent the current best-practices of component development.

**基盤コンポーネント**&#x200B;は、多くのバージョンの AEM で使用でき、標準 AEM インストールでそのまま使用できます。現在もサポートされていますが、ほとんどの機能は非推奨となり、拡張されなくなり、既存のテクノロジーに基づいています。

>[!NOTE]
>
>[コアコンポーネント](https://docs.adobe.com/content/help/ja-JP/experience-manager-core-components/using/introduction.html)は、コンポーネントデザインおよび開発の現在のベストプラクティスを示し、リファレンス実装として提供されます。
>
>[AEM最新化ツール](modernization-tools.md) （英語）は、コアコンポーネントへの移行に役立ちます。

### 利用可能なコンポーネントの表示 {#viewing-available-components}

AEM インスタンスで利用可能なすべてのコンポーネントの概要を確認するには、[コンポーネントコンソール](/help/sites-authoring/default-components-console.md)を使用します。

または、CRXDE Lite を使用して、リポジトリで利用可能なすべてのコンポーネントのリストを取得することもできます。

1. In **[!UICONTROL CRXDE Lite]**, select **[!UICONTROL Tools]** from the toolbar, then **[!UICONTROL Query]**, which opens the **[!UICONTROL Query]** tab.

1. 「**[!UICONTROL クエリー]**」タブで、「`XPath`タイプ&#x200B;**[!UICONTROL 」として「]**」を選択します。

1. **[!UICONTROL クエリ]**&#x200B;入力フィールドに次の文字列を入力します。

   `//element(*, cq:Component)`

1. Click **[!UICONTROL Execute]** and the components are listed.

## その他のリソース {#further-reading}

以下のページでは、これらのコンポーネント（およびその他のコンポーネント）の開発に関する詳細を説明します。

* [AEM コンポーネント - 基本](/help/sites-developing/components-basics.md)
* [AEM コンポーネントの開発](/help/sites-developing/developing-components.md)
* [AEM コンポーネントの開発 - コードサンプル](/help/sites-developing/developing-components-samples.md)
* [複数のインプレースエディターの設定](/help/sites-developing/multiple-inplace-editors.md)
* [開発者モード](/help/sites-developing/developer-mode.md)
* [UI のテスト](/help/sites-developing/hobbes.md)
* [コンテンツフラグメント用コンポーネント](/help/sites-developing/components-content-fragments.md)
* [JSON 形式のページ情報の取得](/help/sites-developing/pageinfo.md)
* [コンポーネントの国際化](/help/sites-developing/i18n.md)
* [コアコンポーネント](https://docs.adobe.com/content/help/ja-JP/experience-manager-core-components/using/introduction.html)
* [非表示条件の使用](/help/sites-developing/hide-conditions.md)
* クラシック UI

   * [AEM コンポーネント（クラシック UI）](/help/sites-developing/developing-components-classic.md)
   * [ウィジェットの使用と拡張（クラシック UI）](/help/sites-developing/widgets.md)
   * [xtype の使用（クラシック UI）](/help/sites-developing/xtypes.md)
   * [フォームの開発（クラシック UI）](/help/sites-developing/developing-forms.md)

