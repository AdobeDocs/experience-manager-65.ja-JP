---
title: AEMコンテンツおよびコマースリリースノート2021
description: AEMコンテンツおよびコマースリリースノート2021
translation-type: tm+mt
source-git-commit: c859aa89e481e852302e9cda0adf2acc04d68a55
workflow-type: tm+mt
source-wordcount: '1323'
ht-degree: 11%

---


# Commerce Integration Framework GitHubリリースの概要

## リリース日：2020年11月

| GitHub | バージョン | 詳細なリリースノート |
|:-------|:-----:|---------------------:|
| CIFコネクタ | 1.6.0 | [リリースノート](https://github.com/adobe/commerce-cif-connector/releases) |
| CIFコアコンポーネント | 1.6.0 | [リリースノート](https://github.com/adobe/aem-core-cif-components/releases) |
| CIFベニアリファレンスサイト | 2020.12.01 | [リリースノート](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新機能 {#what-is-new-november}

* 特定のカテゴリページに追加されたテンプレートの継承。 この機能により、特定の最上位カテゴリ用に作成されたテンプレートをすべてのサブカテゴリが継承できるので、ビジネスユーザーの効率が向上します。

* フッターにエクスペリエンスフラグメントを使用するように、ベニアリファレンスストアフロントが更新されました。 ビジネスユーザーは、AEMオーサリングツールを使用してページフッターを編集できます。

### 改善された点  {#what-is-improved-november}

* チェックアウトコンポーネントが改善され、買い物客が行き先の国に入る機能が改善され、米国外の請求先/配送先住所を許可できるようになりました。

* Adobeクライアントデータレイヤーをハイドレート化するために拡張されたナビゲーションコンポーネント。

* 複数のバグ修正。

## リリース日：2020年10月

| GitHub | バージョン | 詳細なリリースノート |
|:-------|:-----:|---------------------:|
| CIFコネクタ | 1.5.0 | [リリースノート](https://github.com/adobe/commerce-cif-connector/releases) |
| CIFコアコンポーネント | 1.5.0 | [リリースノート](https://github.com/adobe/aem-core-cif-components/releases) |
| CIFベニアリファレンスサイト | 2020.10.27 | [リリースノート](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新機能 {#what-is-new-october}

* ビジネスユーザーがAEMコンテンツページにこのコンポーネントをドラッグ&amp;ドロップして、コマースデータを使用してコンテンツページを強化できるようにする新しいカテゴリカルーセルコンポーネントが追加されました。

* コマースデータを送信して、AdobeクライアントデータレイヤーをハイドレートするようにCIFコアコンポーネントを拡張しました。 Adobeクライアントデータレイヤーは、データを収集し、デジタル解析およびレポートサーバーにデータを通信するための標準化された方法です。 詳しくは、[Adobeクライアントデータレイヤー](https://github.com/adobe/adobe-client-data-layer/wiki)を参照してください。

* Magento管理UIから設定されたSEOメタデータ(タイトル、メタ説明、メタリストなど)を自動的に埋め込むために拡張された製品の詳細ページと製品のキーワードページ

* コマースティーザーコンポーネントのバグが修正されました。

## リリース日：2020年9月

| GitHub | バージョン | 詳細なリリースノート |
|:-------|:-----:|---------------------:|
| CIFコネクタ | 1.4.0 | [リリースノート](https://github.com/adobe/commerce-cif-connector/releases) |
| CIFコアコンポーネント | 1.4.0 | [リリースノート](https://github.com/adobe/aem-core-cif-components/releases) |
| CIFベニアリファレンスサイト | 2020.10.2 | [リリースノート](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新機能 {#what-is-new-september}

* Magento2.4.0スキーマのクエリをサポートします。

* 買い物客が個人情報を更新できるようにするためのアカウント情報機能が追加されました。

* 開発者が製品リストページと検索結果ページに対して実装されたページネーションスタイルを遅延読み込みすることで、開発者はこれらのコンポーネントを設定して、ページネーションスタイルとして「もっと読み込む」ボタンを表示できます。

* 買い物客がアカウントのパスワードを更新/リセットできるように、パスワードリセットページが実装されました。

* バンドルされた製品タイプのサポートを利用できます。

* 開発者は、商品カルーセル、関連商品、および重点カテゴリリストコンポーネントのHTMLタグを設定して、SEOのベストプラクティスに従うことができます。

* マイアカウントのバグが修正されました。

* 複数のバグ修正。

## リリース日：2020年8月

| GitHub | バージョン | 詳細なリリースノート |
|:-------|:-----:|---------------------:|
| CIFコネクタ | 1.3.0 | [リリースノート](https://github.com/adobe/commerce-cif-connector/releases) |
| CIFコアコンポーネント | 1.3.0 | [リリースノート](https://github.com/adobe/aem-core-cif-components/releases) |
| CIFベニアリファレンスサイト | 2020.9.2 | [リリースノート](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新機能 {#what-is-new-august}

* コンテンツおよびコマースページをサポートするために追加された階層リンクコンポーネント。

* ページプロパティに追加された「コマース」タブで、ランディングページフラグメントとエクスペリエンスフラグメント用のCIFプロパティを公開できます。

* Searchbarコンポーネントが改善され、プレースホルダーテキストを表示するオプションがサポートされるようになりました。

* 製品および製品のTeaserコンポーネントに柔軟性を追加し、容易なカスタマイズをサポート。

* 製品ティーザーコンポーネントのデフォルトのCTAボタンラベルを上書きおよび設定する柔軟性を追加。

* アドレス帳コンポーネントが改善され、登録済み買い物客がチェックアウト時にアドレス帳に保存された配送先と請求先の住所を選択できるようになりました。

* 複数のバグ修正。

## リリース日：2020年7月

| GitHub | バージョン | 詳細なリリースノート |
|:-------|:-----:|---------------------:|
| CIFコネクタ | 1.2.0 | [リリースノート](https://github.com/adobe/commerce-cif-connector/releases) |
| CIFコアコンポーネント | 1.2.0 | [リリースノート](https://github.com/adobe/aem-core-cif-components/releases) |
| CIFベニアリファレンスサイト | 2020.8.14 | [リリースノート](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新機能 {#what-is-new-july}

* CIFベニアリファレンスサイトはCIFアーキタイプリポジトリから抽出され、スタンドアロンのGitHubリポジトリになりました。

* CIFアーキタイプがAEMプロジェクトアーキタイプと統合されました。 新しいプロジェクトの場合は、[AEMプロジェクトアーキタイプ](https://github.com/adobe/aem-project-archetype)を起点として使用します。

* サインインしたユーザーが自分のアドレスを管理できるようにアドレス帳の管理が追加されました。

* CIF Cloud Configuration UIでは、公開/非公開アクションがサポートされています。

### 改善された点  {#what-is-improved-july}

* ログインコンポーネントは、ユーザーのドロップダウンに移動され、容易にアクセスできるようになりました。

* aem-core-cif-react-componentsパッケージを簡略化しました。

* 複数のバグ修正。

## リリース日：2020年6月

| GitHub | バージョン | 詳細なリリースノート |
|:-------|:-----:|---------------------:|
| CIFコネクタ | 1.1.0 | [リリースノート](https://github.com/adobe/commerce-cif-connector/releases) |
| CIFコアコンポーネント | 1.1.1 | [リリースノート](https://github.com/adobe/aem-core-cif-components/releases) |
| CIFアーキタイプ | 0.11.0 | [リリースノート](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新機能 {#what-is-new-june}

これは、Adobe Experience ManagerでサポートされるCIFコアコンポーネントの最初のバージョンです。

* 商品リストページと検索結果ページに商品の並べ替えを追加し、買い物客が関連性、価格、商品名に基づいて並べ替えられるようにしました。

* 買い物客がカテゴリに基づいてフィルタリングできるファセットとして、カテゴリのフィルタリングを追加しました。

* ACLを直接操作するのではなく、サービスユーザーを介した/confへのアクセスを確保するセキュリティ要件の一部として、サービスユーザーマッピングを追加しました。 CIFコアコンポーネントは、設定にアクセスする際にサービスユーザーを使用する必要があるようになりました。

### 改善された点  {#what-is-improved-june}

* 製品のリストページと検索結果ページには、項目の合計数が表示されます。 買い物客が適用したフィルターの場合に更新される項目数。

* カテゴリクエリと商品検索クエリを組み合わせて最適化されたファセット検索。

* ページプレビューのカテゴリ/製品の選択にcq:catalogPathが使用されます。

* 複数のバグ修正。

## リリース日：2020年5月

| GitHub | バージョン | 詳細なリリースノート |
|:-------|:-----:|---------------------:|
| CIFコネクタ | 1.0.0 | [リリースノート](https://github.com/adobe/commerce-cif-connector/releases) |
| CIFコアコンポーネント | 1.0.0 | [リリースノート](https://github.com/adobe/aem-core-cif-components/releases) |
| CIFアーキタイプ | 0.11.0 | [リリースノート](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新機能 {#what-is-new-may}

* Magento2.3.5スキーマのクエリをサポートします。

* 検索ページと製品リストページにファセット検索のサポートが追加され、買い物客が製品ファセットに基づいて検索結果をフィルターできるようになりました。

* 新しいOSGiサービスが追加され、SEO用のPDP/PLP URLをカスタマイズできるようになりました。 詳しくは、[ドキュメント](https://github.com/adobe/aem-core-cif-components/wiki/configuration)を参照してください。

* 製品バインディングは、クラウド設定の作成時に自動的に作成されます。

### 改善された点

* 「フォルダーの作成」アクションを表示するように、クラウド設定が拡張されました。

* 複数のバグ修正が適用されました。

## リリース日：2020年4月

| GitHub | バージョン | 詳細なリリースノート |
|:-------|:-----:|---------------------:|
| CIFコネクタ | 0.10.0 | [リリースノート](https://github.com/adobe/commerce-cif-connector/releases) |
| CIFコアコンポーネント | 0.10.0 | [リリースノート](https://github.com/adobe/aem-core-cif-components/releases) |
| CIFアーキタイプ | 0.10.0 | [リリースノート](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新機能 {#what-is-new-april}

* CIF Connectorの統合およびシンプル化された設定です。 詳細は、チェックアウト[はじめに](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)または[新しいAEM CIFプロジェクトのセットアップ](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html#!AdobeDocs/commerce-cif-documentation/master/getting-started/02-new-cif-project.md)を参照してください。

### 改善された点  {#what-is-improved-april}

* 登録買い物かごやチェックアウトのフローが拡張され、登録買い物客をサポートします。

* すべてのコンポーネントに対して拡張国際化対応をサポート。

* グループ化された製品と仮想製品のサポートを利用できます。

* 関連製品、製品カルーセル、および特集カテゴリのコンポーネントが強化され、オプションのタイトルがサポートされるようになりました。

* 複数のバグ修正が適用されました。

## リリース日：2020年2月

| GitHub | バージョン | 詳細なリリースノート |
|:-------|:-----:|---------------------:|
| CIFコネクタ | 0.9.0 | [リリースノート](https://github.com/adobe/commerce-cif-connector/releases) |
| CIFコアコンポーネント | 0.9.0 | [リリースノート](https://github.com/adobe/aem-core-cif-components/releases) |
| CIFアーキタイプ | 0.9.0 | [リリースノート](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新機能 {#what-is-new-february}

* Magento2.3.4のスキーマのクエリをサポートします。

* カテゴリ選択での検索のサポートを追加しました。

* 大きなカタログセットをサポートする、カテゴリリストコンポーネントでのページネーション。

### 改善された点  {#what-is-improved-february}

* 買い物かごが強化され、割引が表示されるようになりました。

* 製品詳細、製品ティーザーおよび製品リストのコンポーネントは、高度な価格情報の表示をサポートしています。

* 製品コンソールと製品選択での製品検索が改善されました。

* 複数のバグ修正が適用されました。

## リリース日：2020年1月

| GitHub | バージョン | 詳細なリリースノート |
|:-------|:-----:|---------------------:|
| CIFコネクタ | 0.8.0 | [リリースノート](https://github.com/adobe/commerce-cif-connector/releases) |
| CIFコアコンポーネント | 0.8.0 | [リリースノート](https://github.com/adobe/aem-core-cif-components/releases) |
| CIFアーキタイプ | 0.7.0 | [リリースノート](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新機能 {#what-is-new-january}

* 顧客がコマースプロジェクトでXFを作成できるようにするために、エクスペリエンスフラグメント(XF)コンポーネントが追加されました。

* 自分のアカウントで使用できるパスワードの変更機能。

* i18nはAEM CIFサーバー側のコアコンポーネントをサポートします。

* 汎用関連製品コンポーネントが使用可能です。

### 改善された点  {#what-is-improved-january}

* 製品テーザーでCTAボタンを表示できるようになりました。

* 重点カテゴリリストコンポーネント内の画像を変更/選択するオプションです。

* 製品のリストコンポーネントでタイトル/バナーを非表示/表示するオプションです。

* 製品カルーセルコンポーネントに適用したドラッグ&amp;ドロップ機能

* 複数のバグ修正が適用されました。
