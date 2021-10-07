---
title: AEMコンテンツおよびコマースリリースノート 2021
description: AEMコンテンツおよびコマースリリースノート 2021
exl-id: ec47c5f8-d4dd-469f-94df-5ee28f25d696
source-git-commit: a401955e4b163a8062a498ea897d4a3d95ae0208
workflow-type: tm+mt
source-wordcount: '1135'
ht-degree: 22%

---

# Commerce 統合フレームワーク GitHub リリースの概要

## システム要件の概要

現在使用している CIF バージョンまたは将来使用する予定の CIF バージョンについて、次の表の最小必要システム構成を確認します。

**4 月のリリースでは、GitHub の CIF コネクタを** Adobeソフトウェア配布 [で利用できる CIF アドオンに置き換えまし](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)た。アドオンに切り替えると、次のようなプロジェクトに大きなメリットがもたらされます。

* 新機能のほとんどは、AEM 6.5 ですぐに利用できます（機能側ポートを待つ必要はありません）
* 新しいアドオンバージョンへの容易なアップグレード
* Cloud Service準備完了

古いAEM CIF コネクタはメンテナンスモードに入り、使用しないでください。 CIF コネクタを新しい CIF アドオンに置き換えてください。 ほとんどのプロジェクトでは、単にパッケージの交換が可能です。

| コンポーネント | システム要件 |
|:-------|:-----:|
| CIF アドオン | 最小：AEM 6.5.7、Magento2.3.5 GraphQL スキーマ |
| CIF コアコンポーネント | [システム要件](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| AEM プロジェクトアーキタイプ | [システム要件](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## リリース日：2021 年 9 月

| コンポーネント | バージョン | 詳細 |
|:-------|:-----:|---------------------:|
| CIF アドオン | 2021.09.27 | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.09.27.zip) |
| CIF コアコンポーネント | 2.2.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.2.0) |
| CIF Venia リファレンスサイト | 2021.09.23 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.09.23) |

### 新機能 {#what-is-new-september}

* サイトエディターの新しい「関連するコマースコンテンツ」タブでは、現在のコンテキストの関連するAEM製品コンテンツにすばやくアクセスできるので、作成者の効率が向上します。

   ![関連するコマースコンテンツ](/help/assets/CIF/associated-commerce-content.png)

* 製品ピッカーの UI が改善され、ユーザーエクスペリエンスが向上し、効率が向上し、複雑な製品カタログのサポートが向上

   ![新しい製品ピッカー](/help/assets/CIF/product-picker.png)

* ナビゲーションコンポーネントで「include_in_menu」プロパティを適用する

### バグの修正 {#bug-fixes-september}

* メニューキャッシュのフラッシュが期待どおりに機能しない

* AEM CS のデプロイメント手順中およびクライアント側コンポーネントを使用していない場合の JS エラー

* sling:configs ノードを持つフォルダー内に CIF クラウド設定を作成できない

## リリース日：2021 年 8 月

| コンポーネント | バージョン | 詳細 |
|:-------|:-----:|---------------------:|
| CIF アドオン | 2021.09.02 | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.09.02.zip) |
| CIF コアコンポーネント | 2.1.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.1.0) |
| CIF Venia リファレンスサイト | 2021.08.27 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.08.27) |

### 新機能 {#what-is-new-august}

* 新しいカテゴリピッカー UI により、ユーザーエクスペリエンスの向上、効率の向上、複雑な製品カタログのサポートの向上を実現

   ![新しいカテゴリピッカー](/help/assets/CIF/category-picker.png)

* CIF コアコンポーネントのサポートの向A11Y

### バグの修正 {#bug-fixes-august}

* アコーディオンを開いた後、カテゴリフィルタを閉じることはできません

* 製品ティーザーの「コールトゥアクションテキスト」プロパティが壊れています

* AEM CS デプロイメント手順中の CIF JS エラー

* マッピングされた製品リスト項目の生の製品アクセスを修正

## リリース日：2021 年 7 月

| コンポーネント | バージョン | 詳細 |
|:-------|:-----:|---------------------:|
| CIF アドオン | 2021.07.21 | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.07.21.zip) |
| CIF コアコンポーネント | 2.0.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.0.0) |
| CIF Venia リファレンスサイト | 2021.07.22 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.07.22) |

### 新機能 {#what-is-new-july}

* CIF コアコンポーネント v2
   * PDP/PLP URL と SEO の構成を簡素化し、改善
   * オーサリングモードでの段階別製品データの視覚的インジケーターにより、今後の変更の可視性が向上
   * コンテンツページとコマースページ用の新しいサイトマップコンポーネント

* 事前定義済みまたはオンザフライで作成されたレコメンデーションを使用した、AEMストアフロントのAdobe Sensei](https://business.adobe.com/products/magento/product-recommendations.html) による [Adobe Commerce Sensei製品レコメンデーションのサポート

## リリース日：2021 年 6 月

| コンポーネント | バージョン | 詳細 |
|:-------|:-----:|---------------------:|
| CIF アドオン | 2021.06.18 | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.06.18.zip) |
| CIF コアコンポーネント | 1.12.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.12.0) |
| CIF Venia リファレンスサイト | 2021.06.12 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.06.17) |

### 新機能 {#what-is-new-june}

* コンテンツフラグメント ( 製品/カテゴリピッカー UI のサポート )
* 新しいコマースコンテンツフラグメントコアコンポーネント
* AEMバックエンドでサポートされるフルテキストコマース検索
* Commerce コアコンポーネントは、Adobe Commerce Sensei Recs のデータ収集をサポートします。
* カテゴリページの SEO 対応 URL の改善
* サイト/設定ごとのカスタム HTTP ヘッダーのサポート

## リリース日：2021 年 5 月

| コンポーネント | バージョン | 詳細 |
|:-------|:-----:|---------------------:|
| CIF アドオン | 2021.05.26 | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.05.26.zip) |
| CIF コアコンポーネント | 1.11.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.11.0) |
| CIF Venia リファレンスサイト | 2021.05.24 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.05.24) |

### 新機能 {#what-is-new-may}

* 製品コンソールのプロパティで関連するコンテンツのページネーションをサポート

### バグの修正 {#bug-fixes-may}

* 製品プロパティの「アセット」タブにアセットのサムネールが表示されない

* 製品コンソールのプレビューデータをリセットするパンくず

## リリース日：2021 年 4 月

| コンポーネント | バージョン | 詳細 |
|:-------|:-----:|---------------------:|
| CIF アドオン | 2021.04.22 | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.04.22.zip) |
| CIF コアコンポーネント | 1.10.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia リファレンスサイト | 2021.04.22 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新機能 {#what-is-new-april}

* カテゴリ UID のサポート — カテゴリ ID に文字列を使用するシステム用のサードパーティコマース統合をロック解除します

* PWA Studio 用 AEM 拡張機能（統合の例を含む）

* WCM ナビゲーションコアコンポーネントを拡張する新しい CIF ナビゲーションコアコンポーネント

### バグの修正 {#bug-fixes-april}

* カテゴリページのページプロパティの「コマース」タブに、ルートカテゴリフィールドが表示されなかった問題を修正しました。

## リリース日：2021 年 3 月 {#what-is-new-march}

| GitHub | バージョン | 詳細なリリースノート |
|:-------|:-----:|---------------------:|
| CIF コネクタ | 1.9.0 | [リリースノート](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF コアコンポーネント | 1.9.0 | [リリースノート](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia リファレンスサイト | 2021.03.25 | [リリースノート](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新機能

* Magento 2.4.2 のサポート

### 改善点

* コンテンツ駆動型のページでの製品詳細コンポーネントの再利用性の向上

* キャッシュの向上と PDP のバックエンド呼び出しの削減

* 複数のバグ修正。

## リリース日：2021 年 2 月

| GitHub | バージョン | 詳細なリリースノート |
|:-------|:-----:|---------------------:|
| CIF コネクタ | 1.8.0 | [リリースノート](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF コアコンポーネント | 1.8.0 | [リリースノート](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia リファレンスサイト | 2021.02.24 | [リリースノート](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新機能 {#what-is-new-february}

* 製品エクスペリエンス管理：エクスペリエンスフラグメントを使用して製品カタログページを個別に拡充することができます。

* 製品コンソールの拡張プロパティを使用して、リンクされたアセットとエクスペリエンスフラグメントを表示できます。これには、関連するコンテンツにすばやく移動するアクションが含まれます。

### 改善点  {#what-is-improved-february}

* 製品画像の URL とカテゴリ情報により、クライアント側のデータレイヤーが強化されました。

* 複数のバグ修正。

## リリース日：2021 年 1 月

| GitHub | バージョン | 詳細なリリースノート |
|:-------|:-----:|---------------------:|
| CIF コネクタ | 1.7.0 | [リリースノート](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF コアコンポーネント | 1.7.0 | [リリースノート](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia リファレンスサイト | 2021.02.02 | [リリースノート](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新機能 {#what-is-new-january}

* 製品エクスペリエンス管理：アセットとエクスペリエンスフラグメントの新しい「コマース」プロパティタブ。 このタブでは、アセットとエクスペリエンスフラグメントを製品およびカテゴリにリンクできます。 また、「 」タブには、リンクされたコマースオブジェクトのリアルタイムデータと、製品コンソールに詳細を表示するリンクも表示されます。

### 改善点  {#what-is-improved-january}

* 認証後にユーザーデータをAdobeクライアントデータレイヤーに送信します。

* 複数のバグ修正。
