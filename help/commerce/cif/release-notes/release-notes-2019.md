---
title: AEMコンテンツおよびコマースリリースノート2021
description: AEMコンテンツおよびコマースリリースノート2021
translation-type: tm+mt
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '973'
ht-degree: 8%

---

# Commerce Integration Framework GitHubリリースの概要

## リリース日：2019年11月

| GitHub | バージョン | 詳細なリリースノート |
|:-------|:-----:|---------------------:|
| CIFコネクタ | 0.7.1 | [リリースノート](https://github.com/adobe/commerce-cif-connector/releases) |
| CIFコアコンポーネント | 0.6.0 | [リリースノート](https://github.com/adobe/aem-core-cif-components/releases) |
| CIFアーキタイプ | 0.6.2 | [リリースノート](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新機能 {#what-is-new-november}

* 作成者は、サイトエディターの新しい「製品/カテゴリとの表示」オプションを使用して、製品詳細および製品リストページを製品/カテゴリとプレビューできます。

* 作成者は、製品SKU別にアセットにタグを付けたり、SKU別に製品固有のアセットを検索したりできます。

* 買い物追加かごに追加されたクーポンのサポートを削除します。

* AEM Venia店頭にBraintree支払いサポートが追加されました。

### 改善点{#what-is-improved-november}

* マルチストア設定で指定したMagentoストアの表示を考慮するようにカテゴリ/製品の選択機能が強化されました。

* npmパッケージとして利用できるリアクトベースのコンポーネント。 これにより、開発者は、既存のコンポーネントをカスタマイズしたり、新しいReactベースのコンポーネントを開発したりするために、新しいReactプロジェクトの依存関係としてReact Componentsパッケージを使用できます。

* GraphQLクエリのカスタマイズがシンプルになりました。 これにより、開発者は少ないコードでCIFコアコンポーネントをカスタマイズできます。

## リリース日：2019年10月

| GitHub | バージョン | 詳細なリリースノート |
|:-------|:-----:|---------------------:|
| CIFコネクタ | 0.6.0 | [リリースノート](https://github.com/adobe/commerce-cif-connector/releases) |
| CIFコアコンポーネント | 0.5.0 | [リリースノート](https://github.com/adobe/aem-core-cif-components/releases) |
| CIFアーキタイプ | 0.5.0 | [リリースノート](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新機能 {#what-is-new-october}

* 商品詳細ページと商品リストページの承認可能なテンプレート。 作成者は、新しいテンプレートを作成し、製品リストと製品の詳細コンポーネントをこれらのテンプレートにドラッグ&amp;ドロップできるようになりました。 他のコンポーネントを追加するだけでなく、作成者はこれらのテンプレートのレイアウトも変更できるようになり、マーケティングとコマースのコンテンツを組み合わせた驚くべきエクスペリエンスを無制限に作成できます。

* 作成者にとって使いやすいCIFコアコンポーネントはすべて、[AEMスタイルシステム](https://helpx.adobe.com/jp/experience-manager/6-5/sites/authoring/using/style-system.html)をサポートするように拡張されました。 製品リストコンポーネントのスタイルの例が提供されています。

* アカウント管理に対して、クライアント側のコンポーネントをリアクトベースにします。 このリリースでは、次の機能がサポートされています。サインイン、パスワードを忘れた場合、およびアカウントを作成する。

### 改善点{#what-is-improved-october}

* 製品の詳細と製品のリストコンポーネントが強化され、ダミーデータが表示され、これらのコンポーネントがテンプレート/ページに配置されたときにレイアウトのプレビューを作成者に示すようになりました。

* MinicartおよびCheckoutコンポーネントが、拡張性を向上させるためにReactフックを使用するようになりました。

## リリース日：2019年9月

| GitHub | バージョン | 詳細なリリースノート |
|:-------|:-----:|---------------------:|
| CIFコネクタ | 0.5.0 | [リリースノート](https://github.com/adobe/commerce-cif-connector/releases) |
| CIFコアコンポーネント | 0.4.0 | [リリースノート](https://github.com/adobe/aem-core-cif-components/releases) |
| CIFアーキタイプ | 0.4.0 | [リリースノート](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新機能 {#what-is-new-september}

* 複数テンプレート機能を使用して、特定の商品詳細ページまたは商品リストページを作成できます。 作成者は、カスタム商品詳細ページや商品リストページを簡単に作成して、商品またはカテゴリ選択を使用してカスタムページを特定の商品またはカテゴリに割り当てることができます。

* マルチカタログ連結を使用して、作成者がAEM製品コンソールで複数のカタログを連結できるようにします。 また、連結を作成した後に、カタログ連結プロパティを編集し、表示することもできます。

* GraphQLを使用して、クライアント側のチェックアウトとミニカートに対応し、基本的な買い物ジャーニーを完全にサポート。

* チェックアウトコンポーネントには、住所フォーム、支払いの選択、配送方法の選択が含まれます。

### 改善点{#what-is-improved-september}

* Product TeaserおよびProduct Carouselコンポーネントは、製品のバリエーションをサポートしています。

## リリース日：2019年8月

| GitHub | バージョン | 詳細なリリースノート |
|:-------|:-----:|---------------------:|
| CIFコネクタ | 0.4.0 | [リリースノート](https://github.com/adobe/commerce-cif-connector/releases) |
| CIFコアコンポーネント | 0.3.0 | [リリースノート](https://github.com/adobe/aem-core-cif-components/releases) |
| CIFアーキタイプ | 0.3.0 | [リリースノート](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新機能 {#what-is-new-august}

* CIFアーキタイプにCIFコネクタを埋め込むと、開発者の柔軟性が向上しました。

* CIFコンポーネントは、開発者が選択したCSSスタイルを適用できるように、「ベニア」固有のCSSスタイルから切り離されています。

* マルチストア/サイト機能。複数のAEMサイト構造でCIFコアコンポーネントを使用でき、基盤となるGraphQLクライアント実装で異なるMagentoストア/ストア表示に接続できるようにします。

* GraphQLキャッシュは、HTTPGETを介した特定のGraphQLクエリに対して有効になり、応答時間を短縮します。

* AEM製品コンソールで有効になっている製品説明表示。

* Commerce Teaserは、WCM Teaserコンポーネントを拡張して、作成者がCTAフィールドを製品詳細ページまたは製品リストページに追加することも可能にしています。

* 作成者がAEMページに配置して、AEMページ、製品の詳細ページ、製品のリストページまたは外部リンクにリンクできるボタンです。

### 改善点{#what-is-improved-august}

* Magentoストア設定をOSGiからAEM製品コンソールに移動し、統合の設定をより作成者にわかりやすくしました。

## リリース日：2019年7月

| GitHub | バージョン | 詳細なリリースノート |
|:-------|:-----:|---------------------:|
| CIFコネクタ | 0.3.0 | [リリースノート](https://github.com/adobe/commerce-cif-connector/releases) |
| CIFコアコンポーネント | 0.2.0 | [リリースノート](https://github.com/adobe/aem-core-cif-components/releases) |
| CIFアーキタイプ | 0.2.0 | [リリースノート](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新機能 {#what-is-new-july}

* 開発者に対して次のいくつかのデプロイメントオプションを提供する最初のCIFアーキタイプ。1. AEM Veniaストアフロント2をデプロイします。 新しいプロジェクト用の足場3を配置します。 既存のプロジェクトでCIF要素を使用する

* カテゴリやサブカテゴリ間のナビゲーションをサポートするマルチレベルのカタログナビゲーション。

* カテゴリページのページネーションによるUX向けの改善。

* 動的属性のレンダリングをサポートするために、製品の詳細および製品のリストコンポーネントの価格属性のクライアント側レンダリング。

* サーバー側の製品カルーセル。特集製品のリストをカルーセル形式で表示します。

* AEMページにカテゴリのリストを表示するためのサーバ側の特集カテゴリリスト。

### 改善点{#what-is-improved-july}

* Magento2.3.2のサポートおよび製品のプロパティに関するバグ修正は、製品コンソールに表示されます。

## リリース日：2019年6月

| GitHub | バージョン | 詳細なリリースノート |
|:-------|:-----:|---------------------:|
| CIFコネクタ | 0.2.0 | [リリースノート](https://github.com/adobe/commerce-cif-connector/releases) |
| CIFコアコンポーネント | 0.1.0 | [リリースノート](https://github.com/adobe/aem-core-cif-components/releases) |

### 新機能 {#what-is-new-june}

* AEM B2CストアフロントにモバイルファーストベニアのCSSスタイル、ランディングページ、製品とカテゴリページを介した動的なカタログナビゲーション、製品検索ページ、買い物かご機能を搭載。商取引を開始し、業務を迅速化します。

* CIF Connectorおよびオーサリングツール(製品コンソール、カテゴリ選択、製品選択)を使用して、作成者がAEMでコマースコンテンツを持つエクスペリエンスを作成できるようにします。

* Magento2.3.1と互換性のあるCIFコアコンポーネントの最初のバージョン：
   * 製品の詳細
   * 製品リスト
   * Product Teaser
   * ナビゲーション
   * 製品の検索
   * 買い物かご(REST)

