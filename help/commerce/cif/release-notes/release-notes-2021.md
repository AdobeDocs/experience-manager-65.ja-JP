---
title: AEMコンテンツおよびコマースリリースノート2021
description: AEMコンテンツおよびコマースリリースノート2021
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 14%

---

# Commerce統合フレームワークGitHubリリースの概要

## システム要件の概要

現在使用しているCIFバージョン、または将来使用する予定のCIFバージョンについて、以下の表の最小必要システム構成を確認します。

**CIFアドオンが [Adobeソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)から利用できるようになりました。古いAEM CIFコネクタはメンテナンスモードに入り、使用しないでください。 新しいCIFアドオンに移行してください。**

| コンポーネント | システム要件 |
|:-------|:-----:|
| CIFアドオン | 最小：AEM 6.5.7、Magento2.3.5のGraphQLスキーマ |
| CIFコアコンポーネント | [システム要件](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| AEM プロジェクトアーキタイプ | [システム要件](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## リリース日：2021年4月

| コンポーネント | バージョン | 詳細 |
|:-------|:-----:|---------------------:|
| CIFアドオン | 2021.04.22 | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.04.22.zip) |
| CIFコアコンポーネント | 1.10.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Veniaリファレンスサイト | 2021.04.22 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新機能 {#what-is-new-april}

* カテゴリUIDのサポート — カテゴリIDに文字列を使用するシステム用のサードパーティコマース統合のロックを解除します

* AEM extension forPWA Studio（を含む） 統合の例

* WCMナビゲーションコアコンポーネントを拡張する新しいCIFナビゲーションコアコンポーネント

* AEMストアフロントのステージング済みカタログデータの視覚的インジケーター

### バグの修正 {#bug-fixes-april}

* カテゴリページのページプロパティの「コマース」タブに、ルートカテゴリフィールドが表示されなかった問題を修正しました。

## リリース日：2021年3月{#what-is-new-march}

| GitHub | バージョン | 詳細なリリースノート |
|:-------|:-----:|---------------------:|
| CIFコネクタ | 1.9.0 | [リリースノート](https://github.com/adobe/commerce-cif-connector/releases) |
| CIFコアコンポーネント | 1.9.0 | [リリースノート](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Veniaリファレンスサイト | 2021.03.25 | [リリースノート](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新機能

* Magento2.4.2のサポート

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

* 製品エクスペリエンス管理：エクスペリエンスフラグメントを使用して、製品カタログページを個別に強化する。

* 製品コンソールの拡張プロパティを使用して、リンクされたアセットとエクスペリエンスフラグメントを表示します。関連コンテンツにすばやく移動するアクションも含まれます。

### 改善点{#what-is-improved-february}

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

### 改善点{#what-is-improved-january}

* 認証後にユーザーデータをAdobeクライアントデータレイヤーに送信します。

* 複数のバグ修正。
