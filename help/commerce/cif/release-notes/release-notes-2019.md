---
title: AEM Content and Commerce リリースノート 2019
description: Adobe Experience Manager Content and Commerce リリースノート 2019。
exl-id: 7e61a75d-6b35-46ee-b88a-444c10b2708f
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: ht
source-wordcount: '946'
ht-degree: 100%

---

# コマース統合フレームワーク GitHub リリースの概要

## リリース日：2019年11月

| GitHub | バージョン | 詳細なリリースノート |
|:-------|:-----:|---------------------:|
| CIF コネクタ | 0.7.1 | [リリースノート](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF コアコンポーネント | 0.6.0 | [リリースノート](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF アーキタイプ | 0.6.2 | [リリースノート](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新機能 {#what-is-new-november}

* 作成者は、サイトエディターの新しい「製品 / カテゴリで表示」オプションを使用して、製品の詳細ページや製品の一覧ページを製品／カテゴリでプレビューできます。

* 作成者は、製品 SKU 別にアセットをタグ付けし、SKU で製品固有のアセットを検索できます。

* 買い物かごにクーポンサポートを追加または削除します。

* Braintree 支払いのサポートが AEM Venia ストアフロントに追加されました。

### 改善点 {#what-is-improved-november}

* カテゴリ／製品ピッカーは、マルチストア設定で指定された Adobe Commerce ストア表示に従って機能が強化されました。

* React ベースのコンポーネントは、npm パッケージとして入手可能です。これにより、開発者は、React コンポーネントパッケージを新しい React プロジェクトの依存関係として使用することで、既存のコンポーネントをカスタマイズしたり、新しい React ベースのコンポーネントを開発したりできます。

* GraphQL クエリのカスタマイズが簡単になりました。これにより、開発者はより少ないコードで CIF コアコンポーネントをカスタマイズできます。

## リリース日：2019年10月

| GitHub | バージョン | 詳細なリリースノート |
|:-------|:-----:|---------------------:|
| CIF コネクタ | 0.6.0 | [リリースノート](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF コアコンポーネント | 0.5.0 | [リリースノート](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF アーキタイプ | 0.5.0 | [リリースノート](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新機能 {#what-is-new-october}

* 製品の詳細ページおよび製品リストページの完全にオーサリング可能なテンプレート。作成者は、テンプレートを作成し、これらのテンプレートに製品リストや製品詳細のコンポーネントをドラッグ＆ドロップできるようになりました。作成者は、他のコンポーネントを追加するだけでなく、これらのテンプレートのレイアウトも変更できるようになり、マーケティングとコマースコンテンツを組み合わせて、優れたエクスペリエンスを無制限に作成できます。

* 作成者にとって使いやすい CIF コアコンポーネントがすべて強化され、 [AEM のスタイルシステム](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/siteandpage/style-system.html?lang=ja)をサポートするようになりました。製品リストコンポーネントのスタイルの例が提供されています。

* アカウント管理用の React ベースのクライアントサイドコンポーネント。このリリースでは、「サインイン」、「パスワードを忘れた場合」および「アカウントを作成」の各機能がサポートされています。

### 改善点 {#what-is-improved-october}

* 製品詳細および製品リストのコンポーネントが強化され、ダミーデータを表示して、作成者がテンプレートやページに配置されたときのレイアウトのプレビューを確認できるようになりました。

* ミニ買い物かごコンポーネントとチェックアウトコンポーネントで、React フックが使用されるようになり、拡張性が向上しました。

## リリース日：2019年9月

| GitHub | バージョン | 詳細なリリースノート |
|:-------|:-----:|---------------------:|
| CIF コネクタ | 0.5.0 | [リリースノート](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF コアコンポーネント | 0.4.0 | [リリースノート](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF アーキタイプ | 0.4.0 | [リリースノート](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新機能 {#what-is-new-september}

* マルチテンプレート機能を使用すると、作成者は特定の製品詳細ページまたは製品リストページをエンリッチメントできます。作成者は、カスタムの製品詳細ページや製品リストページを簡単に作成し、製品やカテゴリのピッカーを使用して、カスタムページを特定の製品やカテゴリに割り当てることができます。

* マルチカタログバインディングを使用すると、作成者は AEM 製品コンソールで複数のカタログをバインドできます。作成者は、バインディングを作成した後で、カタログバインディングプロパティを編集および表示することもできます。

* GraphQL を使用した React ベースのクライアントサイドのチェックアウトとミニ買い物かごで、完全な基本的ショッピングジャーニーをサポートします。

* チェックアウトコンポーネントには、住所フォーム、支払いの選択、発送方法の選択が含まれます。

### 改善点 {#what-is-improved-september}

* 製品ティーザーおよび製品カルーセルコンポーネントは、製品のバリアントをサポートしています。

## リリース日：2019年8月

| GitHub | バージョン | 詳細なリリースノート |
|:-------|:-----:|---------------------:|
| CIF コネクタ | 0.4.0 | [リリースノート](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF コアコンポーネント | 0.3.0 | [リリースノート](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF アーキタイプ | 0.3.0 | [リリースノート](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新機能 {#what-is-new-august}

* CIF アーキタイプへの CIF コネクタの埋め込みがオプションになり、開発者にとっての柔軟性が高まります。

* CIF コンポーネントは、「Venia」固有の CSS スタイル設定から切り離されているので、開発者は選択した CSS スタイル設定を適用できます。

* マルチストア／マルチサイト機能により、複数の AEM サイト構造で CIF コアコンポーネントを使用でき、基盤となる GraphQL クライアント実装が様々な Adobe Commerce ストア／ストア表示に接続できるようになります。

* HTTP GET を使用した特定の GraphQL クエリに対して GraphQL キャッシュが有効になり、応答時間が短縮されます。

* 製品説明表示が AEM 製品コンソールで有効になりました。

* コマースティーザーは WCM ティーザーコンポーネントを拡張したもので、これを使用して作成者が CTA フィールドを製品の詳細ページや製品リストページに追加することもできます。

* 作成者が AEM ページに配置して、AEM ページ、製品の詳細ページ、製品のリストページ、外部リンクのいずれかにリンクできるボタンです。

### 改善点 {#what-is-improved-august}

* Adobe Commerce ストアの設定が OSGi から AEM 製品コンソールに移動され、統合の設定を作成者が容易に行えるようになりました。

## リリース日：2019年7月

| GitHub | バージョン | 詳細なリリースノート |
|:-------|:-----:|---------------------:|
| CIF コネクタ | 0.3.0 | [リリースノート](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF コアコンポーネント | 0.2.0 | [リリースノート](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF アーキタイプ | 0.2.0 | [リリースノート](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新機能 {#what-is-new-july}

* 最初の CIF アーキタイプは、開発者に次のデプロイメントオプションを提供します。1. AEM Venia ストアフロントをデプロイする 2. 新しいプロジェクトの基礎モードをデプロイする 3. 既存のプロジェクトの CIF 要素を使用する

* カテゴリやサブカテゴリ間の移動をサポートするマルチレベルのカタログナビゲーション。

* カテゴリページでのページネーションで UX が向上しました。

* 製品詳細および製品リストのコンポーネントで価格の属性をクライアントサイドでレンダリングでき、属性の動的なレンダリングをサポートします。

* サーバーサイドの製品カルーセルにより、おすすめ製品のリストをカルーセルスタイルで表示できます。

* サーバーサイドのおすすめカテゴリリストで、AEM ページにカテゴリのリストを表示できます。

### 改善点 {#what-is-improved-july}

* Adobe Commerce 2.3.2 がサポートされ、製品コンソールでの製品プロパティ表示に関するバグが修正されました。

## リリース日：2019年6月

| GitHub | バージョン | 詳細なリリースノート |
|:-------|:-----:|---------------------:|
| CIF コネクタ | 0.2.0 | [リリースノート](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF コアコンポーネント | 0.1.0 | [リリースノート](https://github.com/adobe/aem-core-cif-components/releases) |

### 新機能 {#what-is-new-june}

* AEM B2C ストアフロントに、モバイルファーストの Venia CSS スタイル、ランディングページ、製品とカテゴリページを介した動的なカタログナビゲーション、製品検索ページ、買い物かご機能が追加され、コマースプロジェクトをすばやく開始し推進できるようになりました。

* CIF コネクタおよびオーサリングツール（製品コンソール、製品ピッカー、カテゴリピッカー）を使用して、作成者がコマースコンテンツを使用して AEM でエクスペリエンスを作成できるようになりました。

* Adobe Commerce 2.3.1 と互換性のある CIF コアコンポーネントの最初のバージョン：
   * 製品の詳細
   * 製品リスト
   * 製品ティーザー
   * ナビゲーション
   * 製品検索
   * 買い物かご（REST）
