---
title: AEMコンテンツおよびコマースリリースノート2021
description: AEMコンテンツおよびコマースリリースノート2021
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '1324'
ht-degree: 10%

---


# Commerce統合フレームワークGitHubリリースの概要

## リリース日：2020年11月

| GitHub | バージョン | 詳細なリリースノート |
|:-------|:-----:|---------------------:|
| CIFコネクタ | 1.6.0 | [リリースノート](https://github.com/adobe/commerce-cif-connector/releases) |
| CIFコアコンポーネント | 1.6.0 | [リリースノート](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Veniaリファレンスサイト | 2020.12.01 | [リリースノート](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新機能 {#what-is-new-november}

* 特定のカテゴリページに追加されたテンプレートの継承。 この機能により、すべてのサブカテゴリで、特定のトップカテゴリ用に作成されたテンプレートを継承できるので、ビジネスユーザーの効率が向上します。

* Venia参照用ストアフロントが更新され、フッターにエクスペリエンスフラグメントが使用されるようになりました。 ビジネスユーザーは、AEMオーサリングツールを使用してページフッターを編集できます。

### 改善点{#what-is-improved-november}

* チェックアウトコンポーネントが改善され、買い物客が宛先の国を入力して、米国以外での請求/配送先住所を許可できるようになりました。

* ナビゲーションコンポーネントが拡張され、Adobeクライアントデータレイヤーがハイドレートされます。

* 複数のバグ修正。

## リリース日：2020年10月

| GitHub | バージョン | 詳細なリリースノート |
|:-------|:-----:|---------------------:|
| CIFコネクタ | 1.5.0 | [リリースノート](https://github.com/adobe/commerce-cif-connector/releases) |
| CIFコアコンポーネント | 1.5.0 | [リリースノート](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Veniaリファレンスサイト | 2020.10.27 | [リリースノート](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新機能 {#what-is-new-october}

* ビジネスユーザーがこのコンポーネントをAEMコンテンツページにドラッグ&amp;ドロップして、コマースデータを使用してコンテンツページをエンリッチメントできるようにする、新しいカテゴリカルーセルコンポーネントが追加されました。

* CIFコアコンポーネントが拡張され、コマースデータを送信することで、Adobeクライアントデータレイヤーがハイドレートされるようになりました。 Adobeクライアントデータレイヤーは、データを収集し、デジタル分析およびレポートサーバーにデータを通信するための標準化された方法です。 詳しくは、[Adobeクライアントデータレイヤー](https://github.com/adobe/adobe-client-data-layer/wiki)を参照してください。

* Magento管理UI内で設定されたSEOメタデータ（タイトル、メタ説明、メタキーワードなど）を自動的に入力するように拡張された製品の詳細ページと製品リストページ

* コマースティーザーコンポーネントのバグを修正しました。

## リリース日：2020年9月

| GitHub | バージョン | 詳細なリリースノート |
|:-------|:-----:|---------------------:|
| CIFコネクタ | 1.4.0 | [リリースノート](https://github.com/adobe/commerce-cif-connector/releases) |
| CIFコアコンポーネント | 1.4.0 | [リリースノート](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Veniaリファレンスサイト | 2020.10.2 | [リリースノート](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新機能 {#what-is-new-september}

* Magento2.4.0スキーマのクエリをサポートします。

* 買い物客が個人情報を更新できるようにする、アカウント情報機能が追加されました。

* 製品リストページと検索結果ページに実装された遅延読み込みページネーションスタイルを使用すると、開発者は、これらのコンポーネントでページネーションスタイルとして「さらに読み込む」ボタンを表示するように設定できます。

* パスワードリセットページが実装され、買い物客がアカウントのパスワードを更新/リセットできるようになりました。

* バンドルされた製品タイプのサポートを利用できます。

* 開発者は、SEOのベストプラクティスに従うように、製品カルーセル、関連製品、およびおすすめカテゴリリストコンポーネントのHTMLタグを設定できます。

* マイアカウントのバグを修正しました。

* 複数のバグ修正。

## リリース日：2020年8月

| GitHub | バージョン | 詳細なリリースノート |
|:-------|:-----:|---------------------:|
| CIFコネクタ | 1.3.0 | [リリースノート](https://github.com/adobe/commerce-cif-connector/releases) |
| CIFコアコンポーネント | 1.3.0 | [リリースノート](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Veniaリファレンスサイト | 2020.9.2 | [リリースノート](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新機能 {#what-is-new-august}

* コンテンツページとコマースページをサポートするために追加されたパンくずコンポーネント。

* ページのプロパティに「コマース」タブが追加され、ランディングページとエクスペリエンスフラグメントのCIFプロパティが表示されます。

* Searchbarコンポーネントが改善され、プレースホルダーテキストを表示するオプションがサポートされるようになりました。

* 製品および製品ティーザーコンポーネントに柔軟性を追加し、容易なカスタマイズをサポートしました。

* 製品ティーザーコンポーネントのデフォルトのCTAボタンラベルを上書きおよび設定できる柔軟性を追加しました。

* アドレス帳コンポーネントが改善され、登録済みの買い物客がチェックアウト時にアドレス帳に保存された配送先住所と請求先住所を選択できるようになりました。

* 複数のバグ修正。

## リリース日：2020年7月

| GitHub | バージョン | 詳細なリリースノート |
|:-------|:-----:|---------------------:|
| CIFコネクタ | 1.2.0 | [リリースノート](https://github.com/adobe/commerce-cif-connector/releases) |
| CIFコアコンポーネント | 1.2.0 | [リリースノート](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Veniaリファレンスサイト | 2020.8.14 | [リリースノート](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新機能 {#what-is-new-july}

* CIF Venia参照サイトはCIFアーキタイプリポジトリから抽出され、現在はスタンドアロンのGitHubリポジトリです。

* CIFアーキタイプがAEMプロジェクトアーキタイプと統合されました。 新しいプロジェクトの場合は、[AEM Project Archetype](https://github.com/adobe/aem-project-archetype)を出発点として使用します。

* サインインしたユーザーが自分のアドレスを管理できるように、アドレス帳管理が追加されました。

* CIFクラウド設定UIでは、公開/非公開アクションをサポートしています。

### 改善点{#what-is-improved-july}

* ログインコンポーネントがユーザーのドロップダウンに移動され、アクセスが容易になりました。

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

* 製品リストページと検索結果ページでの製品の並べ替えを追加し、買い物客が関連度、価格、製品名に基づいて並べ替えられるようにしました。

* カテゴリのフィルタリングをファセットとして追加し、買い物客がカテゴリに基づいてフィルタリングできるようにしました。

* ACLを直接操作するのではなく、サービスユーザーを介して/confにアクセスできるように、セキュリティ要件の一環としてサービスユーザーマッピングを追加しました。 CIFコアコンポーネントは、サービスユーザーを使用して設定にアクセスする必要があります。

### 改善点{#what-is-improved-june}

* 製品リストページと検索結果ページには、アイテムの合計数が表示されます。 買い物客が適用したフィルターで更新される項目の数。

* カテゴリクエリと製品検索クエリを組み合わせて、ファセット検索を最適化。

* ページプレビューのカテゴリ/製品ピッカーがcq:catalogPathを受け入れます。

* 複数のバグ修正。

## リリース日：2020年5月

| GitHub | バージョン | 詳細なリリースノート |
|:-------|:-----:|---------------------:|
| CIFコネクタ | 1.0.0 | [リリースノート](https://github.com/adobe/commerce-cif-connector/releases) |
| CIFコアコンポーネント | 1.0.0 | [リリースノート](https://github.com/adobe/aem-core-cif-components/releases) |
| CIFアーキタイプ | 0.11.0 | [リリースノート](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新機能 {#what-is-new-may}

* Magento2.3.5スキーマのクエリをサポートします。

* ファセット検索のサポートが検索ページと製品リストページに追加され、買い物客が製品ファセットに基づいて検索結果をフィルタリングできるようになりました。

* 新しいOSGiサービスが追加され、SEO用のPDP/PLP URLをカスタマイズできるようになりました。 詳しくは、この[ドキュメント](https://github.com/adobe/aem-core-cif-components/wiki/configuration)を参照してください。

* クラウド設定の作成時に、製品バインディングが自動的に作成されます。

### 改善点

* クラウド設定が拡張され、「フォルダーの作成」アクションが表示されるようになりました。

* 複数のバグ修正が適用されました。

## リリース日：2020年4月

| GitHub | バージョン | 詳細なリリースノート |
|:-------|:-----:|---------------------:|
| CIFコネクタ | 0.10.0 | [リリースノート](https://github.com/adobe/commerce-cif-connector/releases) |
| CIFコアコンポーネント | 0.10.0 | [リリースノート](https://github.com/adobe/aem-core-cif-components/releases) |
| CIFアーキタイプ | 0.10.0 | [リリースノート](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新機能 {#what-is-new-april}

* CIFコネクタの設定を統合および簡素化。 詳細チェックアウト[はじめに](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)または[新しいAEM CIFプロジェクト設定](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html#!AdobeDocs/commerce-cif-documentation/master/getting-started/02-new-cif-project.md)

### 改善点{#what-is-improved-april}

* 登録した買い物客をサポートするために、買い物かごとチェックアウトフローが拡張されました。

* すべてのコンポーネントで拡張国際化対応がサポートされます。

* グループ化された製品と仮想製品のサポートを利用できます。

* 関連製品、製品カルーセル、およびおすすめカテゴリのコンポーネントが改善され、オプションのタイトルがサポートされるようになりました。

* 複数のバグ修正が適用されました。

## リリース日：2020年2月

| GitHub | バージョン | 詳細なリリースノート |
|:-------|:-----:|---------------------:|
| CIFコネクタ | 0.9.0 | [リリースノート](https://github.com/adobe/commerce-cif-connector/releases) |
| CIFコアコンポーネント | 0.9.0 | [リリースノート](https://github.com/adobe/aem-core-cif-components/releases) |
| CIFアーキタイプ | 0.9.0 | [リリースノート](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新機能 {#what-is-new-february}

* Magento2.3.4スキーマのクエリをサポートします。

* カテゴリピッカーに検索のサポートが追加されました。

* 大きなカタログセットをサポートするための、カテゴリリストコンポーネントのページネーション。

### 改善点{#what-is-improved-february}

* 割引を表示するように強化された買い物かご。

* 製品詳細、製品ティーザーおよび製品リストのコンポーネントは、高度な価格情報の表示をサポートしています。

* 製品コンソールと製品ピッカーの製品検索が改善されました。

* 複数のバグ修正が適用されました。

## リリース日：2020年1月

| GitHub | バージョン | 詳細なリリースノート |
|:-------|:-----:|---------------------:|
| CIFコネクタ | 0.8.0 | [リリースノート](https://github.com/adobe/commerce-cif-connector/releases) |
| CIFコアコンポーネント | 0.8.0 | [リリースノート](https://github.com/adobe/aem-core-cif-components/releases) |
| CIFアーキタイプ | 0.7.0 | [リリースノート](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新機能 {#what-is-new-january}

* 顧客がコマースプロジェクトでXFを作成できるようにするエクスペリエンスフラグメント(XF)コンポーネントが追加されました。

* 自分のアカウントで使用可能なパスワードの変更機能。

* AEM CIFサーバー側コアコンポーネントのi18nサポート。

* 汎用の関連製品コンポーネントが使用可能です。

### 改善点{#what-is-improved-january}

* 製品ティーザーでのCTAボタンの表示をサポートします。

* おすすめカテゴリリストコンポーネントの画像を変更または選択するオプション。

* 製品リストコンポーネントでタイトル/バナーを表示/非表示にするオプション。

* 製品カルーセルコンポーネントに適用されたドラッグ&amp;ドロップ機能。

* 複数のバグ修正が適用されました。
