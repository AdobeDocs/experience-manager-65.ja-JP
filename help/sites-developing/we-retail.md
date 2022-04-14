---
title: We.Retail 参照実装
seo-title: We.Retail Reference Implementation
description: We.Retail は参照実装の技術プレビューであり、AEM を使用したオンラインプレゼンスをセットアップする際に推奨される方法を示しています
seo-description: We.Retail is a technology preview of a reference implementation that illustrates the recommended way of setting up an online presence with AEM
uuid: d8833192-b592-4812-bf9b-bd882e8ee7f0
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: f50150af-deff-4c29-bfe0-1cfc67b29d51
exl-id: 504c61c7-dcd3-412c-9239-d24a2b78e4b9
source-git-commit: 1cef6f87fa66fd78d439c23e6ac907f9531b8fd6
workflow-type: ht
source-wordcount: '754'
ht-degree: 100%

---

# We.Retail 参照実装{#we-retail-reference-implementation}

## 概要 {#introduction}

We.Retail は、Adobe Experience Manager を使用したオンラインプレゼンスの設定で推奨される方法を示す参照実装兼サンプルコンテンツです。

We.Retail では、HTL、レスポンシブレイアウト、編集可能テンプレート、コアコンポーネントなどの最新の AEM テクノロジーが使用されています。

これは小売業界について示していますが、サイトの設定方法は任意の業界に適用できます。製品カタログおよび買い物かご機能のみが小売特有です。

## 機能 {#features}

We.Retail は、AEM の標準的な参照実装として、AEM の最も強力な機能のいくつかを示します。

| **機能** | **説明** | **興味がある場合** |
|---|---|---|
| [グローバル化されたサイト構造](/help/sites-administering/tc-bp.md) | We.Retail には、国固有の Web サイトにライブコピーできる言語マスターが含まれています。 | [試してみる](/help/sites-developing/we-retail-globalized-site-structure.md) |
| [レスポンシブレイアウト](/help/sites-authoring/responsive-layout.md) | すべてのページには、画面やデバイスのサイズに動的に適応するレスポンシブレイアウトが採用されています。 | [試してみる](/help/sites-developing/we-retail-responsive-layout.md) |
| [編集可能テンプレート](/help/sites-developing/page-templates-editable.md) | すべてのページが編集可能テンプレートに基づいており、開発者以外のユーザーがテンプレートを変更したり、カスタマイズしたりできます。 | [試してみる](/help/sites-developing/we-retail-editable-templates.md) |
| [HTML テンプレート言語](https://docs.adobe.com/content/help/ja-JP/experience-manager-htl/using/overview.html) | すべてのコンポーネントが HTL に基づいています。 |  |
| [e コマース機能](/help/commerce/cif-classic/developing/ecommerce.md) | 製品カタログを特徴としています。 |  |
| [コミュニティサイト](/help/communities/overview.md) | 訪問者がコミュニティでのディスカッションに参加したりブログを読んだりできるようにします。 |  |
| [コアコンポーネント](https://docs.adobe.com/content/help/ja-JP/experience-manager-core-components/using/introduction.html) | すべてのコンポーネントが新しいコアコンポーネントに基づいており、使いやすく、設定変更も手早くおこなえます。 | [試してみる](/help/sites-developing/we-retail-core-components.md) |
| [コンテンツフラグメント](/help/assets/content-fragments/content-fragments.md) | We.Retail エクスペリエンスのセクションは、コンテンツフラグメントによってコンテンツを再利用する方法を示します。 | [試してみる](/help/sites-developing/we-retail-content-fragments.md) |
| [エクスペリエンスフラグメント](/help/sites-authoring/experience-fragments.md) | エクスペリエンスフラグメントは、ページ内で参照できるコンテンツおよびレイアウトを含む 1 つ以上のコンポーネントのグループです。 | [試してみる](/help/sites-developing/we-retail-experience-fragments.md) |

## はじめに {#getting-started}

We.Retail は AEM のサンプルコンテンツとして提供されています。使用するには、[通常どおりに AEM を起動する](/help/sites-deploying/deploy.md#getting-started)だけです。このとき、サンプルコンテンツが無効になっていないことを確認してください。

>[!CAUTION]
>
>We.Retail は、実稼動インスタンスにインストールしないでください。実稼動インスタンスは、`nosamplecontent` [実行モード](/help/sites-deploying/configure-runmodes.md)で開始する必要があります。

>[!CAUTION]
>
>We.Retail は最新の AEM テクノロジーに基づいているので、[クラシック UI のオーサリング](/help/sites-classic-ui-authoring/home.md)には対応していません。

### 最新バージョン {#latest-version}

We.Retail は AEM リリースと共に配布されますが、リリース後にコンテンツおよびその機能が更新される可能性があります。そのため、[GitHub から最新リリースをダウンロード](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases)した後、AEM インスタンスにパッケージとして[アップロード](/help/sites-administering/package-manager.md#uploading-packages-from-your-file-system)して[インストール](/help/sites-administering/package-manager.md#installing-packages)することができます。

### 最初の手順 {#first-steps}

1. AEM が起動したら、**We.Retail** サイトは[サイトコンソール](/help/sites-authoring/basic-handling.md#global-navigation)で利用できるようになります（We.Retail がインストールされている場合）。
1. 例えば、次のページを開くことができ、そのページは後述の[付録](#appendix)のように表示されます。

   `https://<server name>:<port number>/editor.html/content/we-retail/language-masters/en.html`

## We.Retail および Geometrixx {#we-retail-geometrixx}

以前のバージョンの AEM では、サンプルコンテンツとして Geometrixx とその多くの実例が提供されてきました。バージョン 6.3 以降では、We.Retail が AEM で提供されるサンプルコンテンツになり、新しい標準の参照実装となります。

We.Retail には、最新の AEM テクノロジーが搭載されています。製品の最新機能を見ると、技術的な堅牢性や、柔軟性、スケーラビリティの向上が明らかです。

### 機能の比較 {#feature-comparison}

次の表では、We.Retail で利用できる主な機能の概要を Geometrixx と比較して示します。

* **使用可能**&#x200B;は、サンプルコンテンツに機能の例が含まれていることを意味します。
* **使用不可**&#x200B;は、サンプルコンテンツに機能の例が含まれていないことを意味します。ただし、機能自体を使用できないという意味ではありません。

| **機能** | **We.Retail** | **Geometrixx** |
|---|---|---|
| グローバル化されたサイト構造 | 国固有のサイトにライブコピーされた言語マスター | 使用不可 |
| コンテンツフラグメント | 使用可 | 使用不可 |
| エクスペリエンスフラグメント | 使用可 | 使用不可 |
| レスポンシブレイアウト | すべてのページ | Geometrixx Media のみ |
| 編集可能なテンプレート | すべてのページ | 使用不可 |
| HTL | すべてのコンポーネント | 限定的 |
| ターゲット設定 | すべてのページ | Geometrixx Outdoors のみ |
| Screens | 使用可 | 使用不可 |
| モバイル | 使用不可 | 使用可 |
| 原稿 | 使用不可 | 使用可 |
| カルーセル、ダウンロード、グラフのコンポーネント | 使用不可 | 使用可 |
| 列の制御 | レイアウトコンテナに置き換えられる | 使用可 |
| Forms | 使用不可 | 使用可 |
| Campaign | 電子メールのサンプルはない | 使用可 |

>[!NOTE]
>
>このリストは、完全を期していますが、あらゆる機能を網羅しているわけではありません。

## コントリビューション {#contribute}

We.Retail はオープンソースプロジェクトとしてリリースされています。最新バージョンのソースコードは GitHub からダウンロードできます。

GitHub のコード

このページのコードは GitHub にあります

* [GitHub の aem-sample-we-retail プロジェクトを開きます](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail)
* プロジェクトを [ZIP ファイル](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/archive/master.zip)としてダウンロードします

最新のリリースは、インストール可能なパッケージとして[直接ダウンロード](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases/latest)することもできます。

問題が発生した場合は、[GitHub の Issues](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/issues) に記入してください。

自由にフォークするか、[プルリクエスト](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/pulls)によって貢献してください。

## プレビュー {#preview}

We.Retail ようこそページのプレビュー：

![screencapture-localhost-4502-editor-html-content-we-retail-us-en-html-2018-08-17-14_33_32](assets/screencapture-localhost-4502-editor-html-content-we-retail-us-en-html-2018-08-17-14_33_32.png)
