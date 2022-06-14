---
title: AEM Content and Commerce リリースノート 2021
description: AEM Content and Commerce リリースノート 2021
exl-id: ec47c5f8-d4dd-469f-94df-5ee28f25d696
source-git-commit: a467009851937c4a10b165a3d253c47bf990bbc5
workflow-type: tm+mt
source-wordcount: '1314'
ht-degree: 99%

---

# コマース統合フレームワーク GitHub リリースの概要

## 必要システム構成の概要

現在使用している CIF バージョン、または将来使用する予定の CIF バージョンについて、以下の表で最小必要システム構成を確認します。

| コンポーネント | システム要件 |
|:-------|:-----:|
| CIF アドオン | 最小：AEM 6.5.7、Adobe Commerce 2.3.5 GraphQL スキーマ |
| CIF コアコンポーネント | [システム要件](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| AEM プロジェクトアーキタイプ | [システム要件](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## リリース日：2021年11月

| コンポーネント | バージョン | 詳細 |
|:-------|:-----:|---------------------:|
| CIF アドオン | 2021.11.18.00 | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.11.18.00.zip) |
| CIF コアコンポーネント | 2.4.2 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.4.2) |
| CIF Venia 参照サイト | 2021.12.01 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.12.01) |

### 新機能 {#what-is-new-november}

* コマースの拡張可能な Peregrine コンポーネントに基づくマイアカウントコンポーネントを拡張しました

![拡張されたマイアカウントコンポーネント](/help/assets/CIF/extended-myAccount-components.png)

* 作成者は、追加のレコメンデーションタイプを使用してアドホックなコマース製品レコメンデーションを作成できます

* AEM ストアフロントでのギフトカードのサポート

## リリース日：2021年10月

| コンポーネント | バージョン | 詳細 |
|:-------|:-----:|---------------------:|
| CIF アドオン | 2021.10.20.02 | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.10.20.02.zip) |
| CIF コアコンポーネント | 2.4.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.4.0) |
| CIF Venia 参照サイト | 2021.11.01 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.11.01) |

### 新機能 {#what-is-new-october}

* CIF アドオンでは、新しい GraphQL API とスキーマを備えた最新の Commerce v2.4.3 をサポートしています

* 作成者は、リッチテキストエディター（RTE）を使用して、製品ページやカタログページへのリンクをテキストフィールドに追加できます。RTE ツールバーに追加された CIF アイコンをクリックすると、ピッカーが開いて、コンテキストを離れることなく製品やカテゴリをすばやく検索および選択できるようになりました。

* 既存のポップアップ買い物かごとチェックアウトは、AEM 専用の買い物かごとチェックアウトページに置き換えられました。これらのページ上のコンポーネントは、Adobe Commerce の拡張可能な Peregrine コンポーネントを使用して構築されています

* マーチャントは、Commerce のバックエンドを使用して、ナビゲーション時に特定の製品カタログカテゴリを非表示にできます。CIF ナビゲーションのコアコンポーネントは、Commerce のバックエンド設定の「メニューに含める」に従って、ナビゲーション時にカテゴリを表示／非表示にします

* カテゴリまたは商品ページが見つからない場合、AEM ストアフロント Venia は HTTP 404 エラーを返します

## リリース日：2021年9月

| コンポーネント | バージョン | 詳細 |
|:-------|:-----:|---------------------:|
| CIF アドオン | 2021.09.27 | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.09.27.zip) |
| CIF コアコンポーネント | 2.2.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.2.0) |
| CIF Venia 参照サイト | 2021.09.23 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.09.23) |

### 新機能 {#what-is-new-september}

* サイトエディターの新しい「関連するコマースコンテンツ」タブで、現在のコンテキストに関連する AEM 製品コンテンツにすばやくアクセスできるので、作成者の効率が向上します。

   ![関連するコマースコンテンツ](/help/assets/CIF/associated-commerce-content.png)

* 製品ピッカー UI の改善により、ユーザーエクスペリエンス、効率および複雑な製品カタログのサポートが向上しました。

   ![新しい製品ピッカー](/help/assets/CIF/product-picker.png)

* ナビゲーションコンポーネントの「include_in_menu」プロパティに従います

### バグ修正 {#bug-fixes-september}

* メニューキャッシュのフラッシュが正常に動作しません

* AEM CS デプロイメントステップ中と、クライアント側コンポーネントを使用していないときに、JS エラーが発生していました

* sling:configs ノードを持つフォルダー内に CIF クラウド設定を作成できません

## リリース日：2021年8月

| コンポーネント | バージョン | 詳細 |
|:-------|:-----:|---------------------:|
| CIF アドオン | 2021.09.02 | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.09.02.zip) |
| CIF コアコンポーネント | 2.1.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.1.0) |
| CIF Venia 参照サイト | 2021.08.27 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.08.27) |

### 新機能 {#what-is-new-august}

* 新しいカテゴリピッカー UI により、ユーザーエクスペリエンスと効率が向上し、複雑な製品カタログもサポートされるようになりました

   ![新しいカテゴリピッカー](/help/assets/CIF/category-picker.png)

* CIF コアコンポーネントの A11Y のサポートが向上しました

### バグ修正 {#bug-fixes-august}

* カテゴリフィルターのアコーディオンを一度開くと閉じることができません

* 製品ティーザーの「コールトゥアクションテキスト」プロパティが機能しません

* AEM CS のデプロイメント手順中に CIF JS エラーが発生します

* マッピングされた製品リスト項目の製品への生のアクセスを修正しました

## リリース日：2021年7月

| コンポーネント | バージョン | 詳細 |
|:-------|:-----:|---------------------:|
| CIF アドオン | 2021.07.21 | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.07.21.zip) |
| CIF コアコンポーネント | 2.0.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.0.0) |
| CIF Venia 参照サイト | 2021.07.22 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.07.22) |

### 新機能 {#what-is-new-july}

* CIF コアコンポーネント v2
   * PDP/PLP URL と SEO の構成の簡素化と改善
   * オーサリングモードでのステージングされた製品データの視覚的インジケーターにより、今後の変更の可視性が向上
   * コンテンツページとコマースページ用の新しいサイトマップコンポーネント

* 事前定義済みのレコメンデーションまたはオンザフライで作成されたレコメンデーションを使用した、[AEM Storefront の Adobe Sensei による Adobe Commerce Sensei](https://business.adobe.com/jp/products/magento/product-recommendations.html) 製品レコメンデーションのサポート

## リリース日：2021年6月

| コンポーネント | バージョン | 詳細 |
|:-------|:-----:|---------------------:|
| CIF アドオン | 2021.06.18 | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.06.18.zip) |
| CIF コアコンポーネント | 1.12.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.12.0) |
| CIF Venia 参照サイト | 2021.06.12 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.06.17) |

### 新機能 {#what-is-new-june}

* コンテンツフラグメントの新しい CIF 製品およびカテゴリ参照データタイプ（製品／カテゴリ選択ツール UI のサポートを含む）製品／カテゴリ選択ツール UI のサポート)
* 新しいコマースコンテンツフラグメントコアコンポーネント
* AEM バックエンドでフルテキストコマース検索をサポート
* コマースコアコンポーネントは、Adobe Commerce Sensei Recs のデータ収集をサポートします。
* カテゴリページの SEO に対応する URL の改善
* サイト／設定ごとのカスタム HTTP ヘッダーのサポート

## リリース日：2021年5月

| コンポーネント | バージョン | 詳細 |
|:-------|:-----:|---------------------:|
| CIF アドオン | 2021.05.26 | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.05.26.zip) |
| CIF コアコンポーネント | 1.11.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.11.0) |
| CIF Venia 参照サイト | 2021.05.24 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.05.24) |

### 新機能 {#what-is-new-may}

* 製品コンソールのプロパティでの関連コンテンツのページネーションのサポート

### バグ修正 {#bug-fixes-may}

* 製品プロパティの「アセット」タブにアセットサムネールが表示されない

* パンくずリストが製品コンソールのプレビューデータをリセットする

## リリース日：2021年4月

| コンポーネント | バージョン | 詳細 |
|:-------|:-----:|---------------------:|
| CIF アドオン | 2021.04.22 | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.04.22.zip) |
| CIF コアコンポーネント | 1.10.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia 参照サイト | 2021.04.22 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新機能 {#what-is-new-april}

* カテゴリ UID のサポート - カテゴリ ID に文字列を使用するシステムに対するサードパーティのコマース統合が可能になります

* PWA Studio 用 AEM 拡張機能（統合の例を含む）

* WCM ナビゲーションコアコンポーネントを拡張する新しい CIF ナビゲーションコアコンポーネント

### バグ修正 {#bug-fixes-april}

* カテゴリページのページプロパティの「コマース」タブに、ルートカテゴリフィールドが表示されなかった問題を修正しました。

## リリース日：2021年3月 {#what-is-new-march}

| GitHub | バージョン | 詳細なリリースノート |
|:-------|:-----:|---------------------:|
| CIF コネクタ | 1.9.0 | [リリースノート](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF コアコンポーネント | 1.9.0 | [リリースノート](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia 参照サイト | 2021.03.25 | [リリースノート](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新機能

* Adobe Commerce 2.4.2 のサポート

### 改善点

* コンテンツ駆動型ページでの製品詳細コンポーネントの再利用性が向上

* PDP のキャッシュ性能の改善と バックエンド呼び出しの削減

* 複数のバグ修正。

## リリース日：2021年2月

| GitHub | バージョン | 詳細なリリースノート |
|:-------|:-----:|---------------------:|
| CIF コネクタ | 1.8.0 | [リリースノート](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF コアコンポーネント | 1.8.0 | [リリースノート](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia 参照サイト | 2021.02.24 | [リリースノート](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新機能 {#what-is-new-february}

* 製品エクスペリエンス管理：エクスペリエンスフラグメントを使用して製品カタログページを個別に拡充することができます。

* 製品コンソールのプロパティを拡張して、関連するコンテンツにすばやく移動するためのアクションなど、リンクされたアセットやエクスペリエンスフラグメントを表示できるようになりました。

### 改善点  {#what-is-improved-february}

* 商品画像の URL とカテゴリ情報を使用して、クライアントサイドのデータレイヤーが強化されました。

* 複数のバグ修正。

## リリース日：2021年1月

| GitHub | バージョン | 詳細なリリースノート |
|:-------|:-----:|---------------------:|
| CIF コネクタ | 1.7.0 | [リリースノート](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF コアコンポーネント | 1.7.0 | [リリースノート](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia 参照サイト | 2021.02.02 | [リリースノート](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新機能 {#what-is-new-january}

* 製品エクスペリエンス管理：アセットおよびエクスペリエンスフラグメント用の新しい「コマース」プロパティタブが追加されました。このタブでは、アセットおよびエクスペリエンスフラグメントを商品およびカテゴリにリンクできます。 また、このタブには、リンクされたコマースオブジェクトのリアルタイムデータと、製品コンソールに詳細を表示するリンクが表示されます。

### 改善点  {#what-is-improved-january}

* 認証後にユーザーデータをアドビクライアントデータレイヤーに送信します。

* 複数のバグ修正。
