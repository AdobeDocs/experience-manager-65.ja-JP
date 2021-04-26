---
title: AEMコンテンツおよびコマースリリースノート2021
description: AEMコンテンツおよびコマースリリースノート2021
translation-type: tm+mt
source-git-commit: 2d0b52dbf85e1fbe91c09a8366744aa77f25cd73
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 15%

---

# Commerce Integration Framework GitHubリリースの概要

## システム要件の概要

現在使用しているCIFバージョンや将来使用する予定のCIFバージョンについて、次の表の最小システム要件を確認してください。

**CIFアドオンが [Adobeソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)(Software Distribution)で利用可能になりました。古いAEM CIFコネクタはメンテナンスモードに入り、使用しないでください。 新しいCIFアドオンに移行してください。**

| コンポーネント | システム要件 |
|:-------|:-----:|
| CIFアドオン | 最小：AEM 6.5.7、Magento2.3.5、GraphQLスキーマ |
| CIFコアコンポーネント | [システム要件](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| AEM プロジェクトアーキタイプ | [システム要件](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## リリース日：2021年4月

| コンポーネント | バージョン | 詳細 |
|:-------|:-----:|---------------------:|
| CIFアドオン | v2021.04.22 | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.04.22.zip) |
| CIFコアコンポーネント | 1.10.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases) |
| CIFベニアリファレンスサイト | 2021.04.22 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新機能 {#what-is-new-april}

* **CIFアドオンが [Adobeソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)(Software Distribution)で利用可能になりました。古いAEM CIFコネクタはメンテナンスモードに入り、使用しないでください。 新しいCIFアドオンに移行してください。**

* カテゴリUIDのサポート —カテゴリIDに文字列を使用するシステムのサードパーティコマース統合をロック解除します。

* AEMPWA Studio用の拡張機能（内） 例えば、統合

* WCMナビゲーションコアコンポーネントを拡張する新しいCIFナビゲーションコアコンポーネント

* AEMストアフロントのステージ済みカタログデータの視覚的なインジケーター

### バグの修正 {#bug-fixes-april}

* カテゴリページのページプロパティの「コマース」タブに、ルートカテゴリフィールドが表示されませんでした。

## リリース日：2021年3月{#what-is-new-march}

| GitHub | バージョン | 詳細なリリースノート |
|:-------|:-----:|---------------------:|
| CIFコネクタ | 1.9.0 | [リリースノート](https://github.com/adobe/commerce-cif-connector/releases) |
| CIFコアコンポーネント | 1.9.0 | [リリースノート](https://github.com/adobe/aem-core-cif-components/releases) |
| CIFベニアリファレンスサイト | 2021.03.25 | [リリースノート](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新機能

* Magento2.4.2のサポート

### 改善された点

* コンテンツ主導型ページの商品詳細コンポーネントの再利用性を向上

* PDPのキャッシュの向上とバックエンド・コールの削減

* 複数のバグ修正。

## リリース日：2021年2月

| GitHub | バージョン | 詳細なリリースノート |
|:-------|:-----:|---------------------:|
| CIFコネクタ | 1.8.0 | [リリースノート](https://github.com/adobe/commerce-cif-connector/releases) |
| CIFコアコンポーネント | 1.8.0 | [リリースノート](https://github.com/adobe/aem-core-cif-components/releases) |
| CIFベニアリファレンスサイト | 2021.02.24 | [リリースノート](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新機能 {#what-is-new-february}

* 製品エクスペリエンス管理：エクスペリエンスフラグメントを使用して、商品カタログページを個別に拡張する。

* 関連するコンテンツにすばやく移動するアクションなど、アセットとエクスペリエンスフラグメントのリンクを表示するための製品コンソールプロパティが拡張されました。

### 改善された点  {#what-is-improved-february}

* 製品画像のURLとカテゴリ情報によるクライアント側のデータレイヤーの強化

* 複数のバグ修正。

## リリース日：2021年1月

| GitHub | バージョン | 詳細なリリースノート |
|:-------|:-----:|---------------------:|
| CIFコネクタ | 1.7.0 | [リリースノート](https://github.com/adobe/commerce-cif-connector/releases) |
| CIFコアコンポーネント | 1.7.0 | [リリースノート](https://github.com/adobe/aem-core-cif-components/releases) |
| CIFベニアリファレンスサイト | 2021.02.02 | [リリースノート](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新機能 {#what-is-new-january}

* 製品エクスペリエンス管理：アセットおよびエクスペリエンスフラグメント用の新しい「コマース」プロパティタブ。 このタブを使用して、アセットとエクスペリエンスフラグメントを製品とカテゴリにリンクできます。 また、このタブには、リンクされたコマースオブジェクトのリアルタイムデータと、製品コンソールに詳細を表示するリンクも表示されます。

### 改善された点  {#what-is-improved-january}

* 認証後のユーザーデータをAdobeクライアントデータレイヤーに送信します。

* 複数のバグ修正。
