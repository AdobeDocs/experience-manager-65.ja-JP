---
title: We.Retail 参照実装
description: We.Retail は、AEMを使用したオンラインプレゼンスの設定で推奨される方法を示す、参照実装のテクノロジープレビューです
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 504c61c7-dcd3-412c-9239-d24a2b78e4b9
source-git-commit: f7b24617dec77c6907798b1615debdc2329c9d80
workflow-type: tm+mt
source-wordcount: '759'
ht-degree: 37%

---

# We.Retail 参照実装{#we-retail-reference-implementation}

## 概要 {#introduction}

We.Retail は、Adobe Experience Managerでオンラインプレゼンスを設定する推奨方法を示す参照実装およびサンプルコンテンツです。

We.Retail では、HTL、レスポンシブレイアウト、編集可能なテンプレート、コアコンポーネントなど、最新のAdobe Experience Manager(AEM) テクノロジーが使用されます。

これは小売業界を示していますが、サイトの設定方法は任意の業種に適用でき、商品カタログと買い物かごの機能のみが小売に固有です。

## 機能 {#features}

AEMの標準的な参照実装として、We.Retail はAEMの最も強力な機能の一部を示します。

| **機能** | **説明** | **興味が？** |
|---|---|---|
| [グローバル化されたサイト構造](/help/sites-administering/tc-bp.md) | We.Retail には、国固有のサイトにライブコピーされる言語マスターが含まれます。 | [やってみて！](/help/sites-developing/we-retail-globalized-site-structure.md) |
| [レスポンシブレイアウト](/help/sites-authoring/responsive-layout.md) | すべてのページには、画面やデバイスのサイズに動的に適応するレスポンシブレイアウトが備わっています。 | [やってみて！](/help/sites-developing/we-retail-responsive-layout.md) |
| [編集可能なテンプレート](/help/sites-developing/page-templates-editable.md) | すべてのページは編集可能なテンプレートに基づいているので、開発者以外のユーザーがテンプレートを調整およびカスタマイズできます。 | [やってみて！](/help/sites-developing/we-retail-editable-templates.md) |
| [HTML テンプレート言語](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=ja) | すべてのコンポーネントは HTL に基づいています |  |
| [e コマース機能](/help/commerce/cif-classic/developing/ecommerce.md) | 商品カタログを機能させる |  |
| [コミュニティサイト](/help/communities/overview.md) | 訪問者によるコミュニティディスカッションへの参加、ブログの読み取りなどの許可 |  |
| [コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja) | すべてのコンポーネントは新しいコアコンポーネントに基づいており、より使いやすく、ユーザーがすぐに使用できる形で設定可能です | [やってみて！](/help/sites-developing/we-retail-core-components.md) |
| [コンテンツフラグメント](/help/assets/content-fragments/content-fragments.md) | 「 We.Retail エクスペリエンス」の節では、コンテンツフラグメントを使用してコンテンツを再利用する方法を示します。 | [試してみる](/help/sites-developing/we-retail-content-fragments.md) |
| [エクスペリエンスフラグメント](/help/sites-authoring/experience-fragments.md) | エクスペリエンスフラグメントは、ページ内で参照できるコンテンツおよびレイアウトを含む 1 つ以上のコンポーネントのグループです。 | [試してみる](/help/sites-developing/we-retail-experience-fragments.md) |

## はじめに {#getting-started}

We.Retail は、AEMサンプルコンテンツとして配信されます。 使用するには、単純に [通常どおりにAEMを起動します](/help/sites-deploying/deploy.md#getting-started)を設定する場合は、サンプルコンテンツが無効になっていないことを確認します。

>[!CAUTION]
>
>実稼動インスタンスに We.Retail をインストールしないでください。 実稼動インスタンスは、で開始する必要があります `nosamplecontent` [実行モード](/help/sites-deploying/configure-runmodes.md).

>[!CAUTION]
>
>We.Retail は最新の AEM テクノロジーに基づいているので、[クラシック UI のオーサリング](/help/sites-classic-ui-authoring/home.md)には対応していません。

### 最新バージョン {#latest-version}

We.Retail は AEM リリースと共に配布されますが、リリース後にコンテンツおよびその機能が更新される可能性があります。そのため、[GitHub から最新リリースをダウンロード](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases)した後、AEM インスタンスにパッケージとして[アップロード](/help/sites-administering/package-manager.md#uploading-packages-from-your-file-system)して[インストール](/help/sites-administering/package-manager.md#installing-packages)することができます。

### 最初の手順 {#first-steps}

1. AEMが開始（または We.Retail がインストール）されると、サイト **We.Retail** は、 [サイトコンソール](/help/sites-authoring/basic-handling.md#global-navigation).
1. 例えば、次のページを開くと、 [付録](#appendix) 以下：

   `https://<server name>:<port number>/editor.html/content/we-retail/language-masters/en.html`

## We.Retail および Geometrixx {#we-retail-geometrixx}

Geometrixxとその多くの転身は、AEMの以前のバージョンでサンプルコンテンツとして機能していました。 バージョン 6.3 以降、 We.Retail はAEMで提供されるサンプルコンテンツであり、新しい標準的な参照実装として機能します。

We.Retail は、技術的により堅牢で、最新のAEMテクノロジーを活用して、より柔軟で拡張性を高めると同時に、製品の最新の機能も示します。

### 機能の比較 {#feature-comparison}

次の表は、We.Retail でGeometrixxと比較して使用できる主な機能の概要を示しています。

* **利用可能** は、機能の例がサンプルコンテンツに含まれていることを意味します。
* **利用不可** は、機能の例がサンプルコンテンツでは使用できないことを意味しますが、機能自体が使用できないとは限りません。

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
| カルーセルビューア、ダウンロード、グラフコンポーネント | 使用不可 | 使用可 |
| 列の制御 | レイアウトコンテナに置き換えられる | 使用可 |
| Forms | 使用不可 | 使用可 |
| Campaign | メールのサンプルはない | 使用可 |

>[!NOTE]
>
>このリストは完成を目指していますが、すべてを網羅したものとは考えないでください。

## コントリビューション {#contribute}

We.Retail はオープンソースプロジェクトとしてリリースされ、最新バージョンのソースコードを GitHub からダウンロードできます。

GitHub のコード

このページのコードは GitHub にあります。

* [GitHub の aem-sample-we-retail プロジェクトを開きます](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail)
* プロジェクトを [ZIP ファイル](https://codeload.github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/zip/refs/heads/master)としてダウンロードします

最新のリリースは、インストール可能なパッケージとして[直接ダウンロード](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases/tag/we.retail.reactor-4.0.0)することもできます。

問題が発生した場合は、 [GitHub の問題](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/issues).

自由にフォークするか、[プルリクエスト](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/pulls)によって貢献してください。

## プレビュー {#preview}

We.Retail ようこそページのプレビュー：

![screencapture-localhost-4502-editor-html-content-we-retail-us-en-html-2018-08-17-14_33_32](assets/screencapture-localhost-4502-editor-html-content-we-retail-us-en-html-2018-08-17-14_33_32.png)
