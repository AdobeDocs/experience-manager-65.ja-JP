---
title: AEMコンテンツおよびコマースリリースノート2021
description: AEMコンテンツおよびコマースリリースノート2021
exl-id: ec47c5f8-d4dd-469f-94df-5ee28f25d696
source-git-commit: b6703f519295eef728d5504360d99de69438064c
workflow-type: tm+mt
source-wordcount: '989'
ht-degree: 22%

---

# Commerce統合フレームワークGitHubリリースの概要

## システム要件の概要

現在使用しているCIFバージョン、または将来使用する予定のCIFバージョンについて、以下の表の最小必要システム構成を確認します。

**4月のリリースでは、GitHubのCIFコネクタを** Adobeソフトウェア配布 [](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)で利用できるCIFアドオンに置き換えました。アドオンに切り替えると、次のような大きなメリットが得られます。

* 新機能のほとんどは、AEM 6.5ですぐに使用できます（機能側ポートを待つ必要はありません）。
* 新しいアドオンバージョンへの容易なアップグレード
* Cloud Service準備完了

古いAEM CIFコネクタはメンテナンスモードに入り、使用しないでください。 CIFコネクタを新しいCIFアドオンに置き換えてください。 ほとんどのプロジェクトでは、単にパッケージの置き換えが可能です。

| コンポーネント | システム要件 |
|:-------|:-----:|
| CIF アドオン | 最小：AEM 6.5.7、Magento2.3.5のGraphQLスキーマ |
| CIFコアコンポーネント | [システム要件](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| AEM プロジェクトアーキタイプ | [システム要件](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## リリース日：2021年8月

| コンポーネント | バージョン | 詳細 |
|:-------|:-----:|---------------------:|
| CIF アドオン | 2021.08.20 | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.08.20.zip) |
| CIFコアコンポーネント | 2.1.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.1.0) |
| CIF Veniaリファレンスサイト | 2021.08.27 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.08.27) |

### 新機能 {#what-is-new-august}

* 新しいカテゴリピッカーUIにより、ユーザーエクスペリエンスの向上、効率の向上、複雑な製品カタログのサポートの向上を実現

   ![新しいカテゴリピッカー](/help/assets/CIF/category-picker.png)

* CIFコアコンポーネントのサポートの向A11Y

### バグの修正 {#bug-fixes-august}

* アコーディオンを開くと、カテゴリフィルタを閉じることができません

* 製品ティーザーの「コールトゥアクションテキスト」プロパティが壊れています

* AEM CSデプロイメント手順中のCIF JSエラー

* マッピングされた製品リスト項目の生の製品アクセスを修正

## リリース日：2021年7月

| コンポーネント | バージョン | 詳細 |
|:-------|:-----:|---------------------:|
| CIF アドオン | 2021.07.21 | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.07.21.zip) |
| CIFコアコンポーネント | 2.0.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.0.0) |
| CIF Veniaリファレンスサイト | 2021.07.22 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.07.22) |

### 新機能 {#what-is-new-july}

* CIFコアコンポーネントv2
   * PDP/PLP URLとSEOの構成の簡素化と改善
   * オーサリングモードでのステージングされた製品データの視覚的インジケーターにより、今後の変更の可視性が向上
   * コンテンツページとコマースページ用の新しいサイトマップコンポーネント

* 事前定義済みのレコメンデーションまたはオンザフライで作成されたレコメンデーションを使用した、AEM StorefrontのAdobe Sensei](https://business.adobe.com/products/magento/product-recommendations.html)による[AdobeコマースSensei製品レコメンデーションのサポート

## リリース日：2021年6月

| コンポーネント | バージョン | 詳細 |
|:-------|:-----:|---------------------:|
| CIF アドオン | 2021.06.18 | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.06.18.zip) |
| CIFコアコンポーネント | 1.12.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.12.0) |
| CIF Veniaリファレンスサイト | 2021.06.12 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.06.17) |

### 新機能 {#what-is-new-june}

* コンテンツフラグメント( 製品/カテゴリピッカーのUIのサポート)
* 新しいコマースコンテンツフラグメントコアコンポーネント
* AEMバックエンドでサポートされるフルテキストコマース検索
* コマースコアコンポーネントは、AdobeCommerce Sensei Recsのデータ収集をサポートします。
* カテゴリページのSEOに対応するURLの改善
* サイト/設定ごとのカスタムHTTPヘッダーのサポート

## リリース日：2021年5月

| コンポーネント | バージョン | 詳細 |
|:-------|:-----:|---------------------:|
| CIF アドオン | 2021.05.26 | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.05.26.zip) |
| CIFコアコンポーネント | 1.11.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.11.0) |
| CIF Veniaリファレンスサイト | 2021.05.24 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.05.24) |

### 新機能 {#what-is-new-may}

* 製品コンソールのプロパティでの関連コンテンツのページネーションのサポート

### バグの修正 {#bug-fixes-may}

* 製品プロパティの「アセット」タブにアセットサムネールが表示されない

* 製品コンソールのプレビューデータをリセットするパンくずリスト

## リリース日：2021年4月

| コンポーネント | バージョン | 詳細 |
|:-------|:-----:|---------------------:|
| CIF アドオン | 2021.04.22 | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.04.22.zip) |
| CIFコアコンポーネント | 1.10.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Veniaリファレンスサイト | 2021.04.22 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新機能 {#what-is-new-april}

* カテゴリUIDのサポート — カテゴリIDに文字列を使用するシステム用のサードパーティコマース統合のロックを解除します

* PWA Studio 用 AEM 拡張機能（統合の例を含む）

* WCM ナビゲーションコアコンポーネントを拡張する新しい CIF ナビゲーションコアコンポーネント

### バグの修正 {#bug-fixes-april}

* カテゴリページのページプロパティの「コマース」タブに、ルートカテゴリフィールドが表示されなかった問題を修正しました。

## リリース日：2021年3月 {#what-is-new-march}

| GitHub | バージョン | 詳細なリリースノート |
|:-------|:-----:|---------------------:|
| CIFコネクタ | 1.9.0 | [リリースノート](https://github.com/adobe/commerce-cif-connector/releases) |
| CIFコアコンポーネント | 1.9.0 | [リリースノート](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Veniaリファレンスサイト | 2021.03.25 | [リリースノート](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新機能

* Magento 2.4.2 のサポート

### 改善点

* コンテンツ駆動型ページの製品詳細コンポーネントの再利用性の向上

* キャッシュの改善とPDPのバックエンド呼び出しの削減

* 複数のバグ修正。

## リリース日：2021年2月

| GitHub | バージョン | 詳細なリリースノート |
|:-------|:-----:|---------------------:|
| CIFコネクタ | 1.8.0 | [リリースノート](https://github.com/adobe/commerce-cif-connector/releases) |
| CIFコアコンポーネント | 1.8.0 | [リリースノート](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Veniaリファレンスサイト | 2021.02.24 | [リリースノート](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新機能 {#what-is-new-february}

* 製品エクスペリエンス管理：エクスペリエンスフラグメントを使用して製品カタログページを個別に拡充することができます。

* 製品コンソールの拡張プロパティを使用して、リンクされたアセットとエクスペリエンスフラグメントを表示します。関連コンテンツにすばやく移動するアクションも含まれます。

### 改善点  {#what-is-improved-february}

* 製品画像のURLとカテゴリ情報を使用して、クライアント側のデータレイヤーを強化しました。

* 複数のバグ修正。

## リリース日：2021年1月

| GitHub | バージョン | 詳細なリリースノート |
|:-------|:-----:|---------------------:|
| CIFコネクタ | 1.7.0 | [リリースノート](https://github.com/adobe/commerce-cif-connector/releases) |
| CIFコアコンポーネント | 1.7.0 | [リリースノート](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Veniaリファレンスサイト | 2021.02.02 | [リリースノート](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新機能 {#what-is-new-january}

* 製品エクスペリエンス管理：アセットとエクスペリエンスフラグメントの新しい「コマース」プロパティタブ。 このタブでは、アセットとエクスペリエンスフラグメントを製品およびカテゴリにリンクできます。 また、「 」タブには、リンクされたコマースオブジェクトのリアルタイムデータと、製品コンソールに詳細を表示するリンクも表示されます。

### 改善点  {#what-is-improved-january}

* 認証後にユーザーデータをAdobeクライアントデータレイヤーに送信します。

* 複数のバグ修正。
