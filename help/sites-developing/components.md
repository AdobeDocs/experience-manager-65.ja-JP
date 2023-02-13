---
title: コンポーネントの概要
seo-title: Components
description: コンポーネントは、特定の機能を実現し、Web サイトにコンテンツを提供するためのモジュールユニットです。
seo-description: Components are modular units which realize specific functionality to present your content on your website
uuid: fb39aeb8-8f43-4091-8083-ebfab89e6e63
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 45efff93-2fe5-4313-83a0-0e23a540da93
exl-id: 9e30c969-2692-4380-943a-b022ee900ce8
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: ht
source-wordcount: '590'
ht-degree: 100%

---

# コンポーネントの概要{#components-overview}

このページでは、[ページオーサリングで使用される](/help/sites-authoring/default-components-foundation.md)コンポーネントなど、Adobe Experience Manager（AEM）のコンポーネントの概要を示します。

## コンポーネントとは {#what-exactly-is-a-component}

* 特定の機能を実現し、Web サイトにコンテンツを提供するためのモジュールユニットです。
* 再利用可能です。
* リポジトリーの 1 つのフォルダー内の自己完結型ユニットとして開発されます。
* 非表示の設定ファイルを持ちません。
* 他のコンポーネントを組み込むことができます。
* AEM システム内であれば、どの場所でも実行できます。特定のコンポーネントにおいてのみ実行できるようにすることもできます。
* 標準化されたユーザーインターフェイスがあります。
* 設定可能な編集動作があります。
* Granite UI コンポーネントに基づくサブ要素を使用して構築されたダイアログボックスを使用します。
* [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=ja)（推奨）または JSP を使用して作成できます。
* デフォルトの機能を拡張するカスタマイズされたコンポーネントを作成するために開発できます。

コンポーネントはモジュールなので、次のことができます。

* ローカルインスタンスで新しいコンポーネントを開発する。
* テスト環境にデプロイします。
* ライブオーサリング環境にデプロイし、そこで、作成者や管理者のコンテンツの追加および設定を許可します。
* ライブパブリッシュ環境にデプロイします。Web サイトへの訪問者用にコンテンツをレンダリングするために使用します。また、特定のコンポーネント（コミュニティ用など）がユーザーからの入力を受け入れます。

各 AEM コンポーネント：

* リソースタイプです。
* 特定の機能を完全に実現するスクリプトのコレクションです。
* *単独で*（AEM 内またはポータル内で）機能できます。

## AEM 内の既成のコンポーネント {#out-of-the-box-components-within-aem}

AEM には、次のような包括的な機能を提供する、](/help/sites-authoring/default-components.md)すぐに使用できる様々なコンポーネント[が付属しています。

* 段落システム ( `parsys`)
* ページ（`responsivegrid` - タッチ操作対応 UI のみ）
* テキスト
* 画像（説明テキスト付き）
* ツールバー

提供される[サンプル We.Retail Web サイト](/help/sites-developing/we-retail.md)内で提供されるコンポーネントおよびそれらの使用方法は、コンポーネントの実装および使用方法の例です。コンポーネントは、すべてのソースコードと共に提供されており、そのまま使用することも、コンポーネントを変更または拡張する出発点として使用することもできます。

### コアコンポーネントおよび基盤コンポーネント {#core-components-and-foundation-components}

アドビが提供する AEM コンポーネントには 2 つのセットがあります。

* [コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja)
* [基盤コンポーネント](/help/sites-authoring/default-components-foundation.md)

**コアコンポーネント**&#x200B;は、AEM 6.3 で導入され、柔軟で豊富なオーサリング機能を提供します。[We.Retail 参照サイト](/help/sites-developing/we-retail.md)では、コアコンポーネントがどのように使用できるかや、コンポーネント開発の現在のベストプラクティスについて説明しています。

**基盤コンポーネント**&#x200B;は、多くのバージョンの AEM で使用でき、標準 AEM インストールでそのまま使用できます。引き続きサポートされていますが、従来のテクノロジーに基づいており、多くの機能が非推奨になっているほか、今後は機能強化が行われません。

>[!NOTE]
>
>[コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja)は、コンポーネントデザインおよび開発の現在のベストプラクティスを示し、リファレンス実装として提供されます。
>
>[AEM 最新化ツール](modernization-tools.md)が、コアコンポーネントへの移行に役立ちます。

### 利用可能なコンポーネントの表示 {#viewing-available-components}

AEM インスタンスで利用可能なすべてのコンポーネントの概要を確認するには、[コンポーネントコンソール](/help/sites-authoring/default-components-console.md)を使用します。

または、CRXDE Lite を使用して、リポジトリで利用可能なすべてのコンポーネントのリストを取得することもできます。

1. **[!UICONTROL CRXDE Lite]** で、ツールバーから「**[!UICONTROL ツール]**」を選択し、「**[!UICONTROL クエリ]**」を選択して、「**[!UICONTROL クエリ]**」タブを開きます。

1. 「**[!UICONTROL クエリ]**」タブで、「**[!UICONTROL タイプ]**」として「`XPath`」を選択します。

1. 「**[!UICONTROL クエリ]**」入力フィールドに次の文字列を入力します。

   `//element(*, cq:Component)`

1. 「**[!UICONTROL 実行]**」をクリックするとコンポーネントがリストされます。

## その他のリソース {#further-reading}

上述のコンポーネント（およびその他のコンポーネント）の開発について詳しくは、以下のページを参照してください。

* [AEM コンポーネント - 基本](/help/sites-developing/components-basics.md)
* [AEM コンポーネントの開発](/help/sites-developing/developing-components.md)
* [AEM コンポーネントの開発 - コードサンプル](/help/sites-developing/developing-components-samples.md)
* [複数のインプレースエディターの設定](/help/sites-developing/multiple-inplace-editors.md)
* [開発者モード](/help/sites-developing/developer-mode.md)
* [UI のテスト](/help/sites-developing/hobbes.md)
* [コンテンツフラグメント用コンポーネント](/help/sites-developing/components-content-fragments.md)
* [JSON 形式のページ情報の取得](/help/sites-developing/pageinfo.md)
* [コンポーネントの国際化](/help/sites-developing/i18n.md)
* [コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja)
* [非表示条件の使用](/help/sites-developing/hide-conditions.md)
* クラシック UI

   * [AEM コンポーネント（クラシック UI）](/help/sites-developing/developing-components-classic.md)
   * [ウィジェットの使用および拡張（クラシック UI）](/help/sites-developing/widgets.md)
   * [xtype の使用（クラシック UI）](/help/sites-developing/xtypes.md)
   * [フォームの作成（クラシック UI）](/help/sites-developing/developing-forms.md)
