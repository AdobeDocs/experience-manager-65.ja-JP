---
title: AEM Content and Commerce リリースノート 2022
description: Adobe Experience Manager Content and Commerce リリースノート 2022.
exl-id: d0a66e70-c4f1-4051-8161-11f07dad0612
source-git-commit: eaffc71c23c18d26ec5cbb2bbb7524790c4826fe
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 99%

---

# コマース統合フレームワーク GitHub リリースの概要

## 必要システム構成の概要

現在使用している CIF バージョン、または今後使用する予定の CIF バージョンについては、以下の表で最小必要システム構成を確認してください。

| コンポーネント | システム要件 |
|:-------|:-----:|
| CIF アドオン | 最小：AEM 6.5.7、Adobe Commerce 2.3.5 GraphQL スキーマ |
| CIF コアコンポーネント | [システム要件](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| AEM プロジェクトアーキタイプ | [システム要件](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## リリース日：2022年9月

| コンポーネント | バージョン | 詳細 |
|:-------|:-----:|---------------------:|
| CIF アドオン | 2022.09.20.00 | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.09.20.00.zip) |
| CIF コアコンポーネント | 2.11.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.11.0) |
| CIF Venia 参照サイト | 2022.09.02 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.09.02) |

### 新機能 {#what-is-new-september}

* 作成者は、エクスペリエンスフラグメントを使用して、製品リストを動的にエンリッチメントできます（例：製品リスト間にバナーを配置）
* リストコンポーネントは、関連する製品／カテゴリーページをサポートし、関連するページを動的に表示します。
* Peregrine 12.5 コンポーネントのサポート
* 製品ティーザーおよびカルーセルでのクライアントサイドの価格読み込みのサポート

## リリース日：2022年7月

| コンポーネント | バージョン | 詳細 |
|:-------|:-----:|---------------------:|
| CIF アドオン | 2022.08.02.00 | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.08.02.00.zip) |

### 新機能 {#what-is-new-july}

* AEM ページのプロパティと製品コックピットの概要を介した、製品およびカテゴリに対する AEM ページの関連付け
  ![製品コックピットページの関連付け](/help/assets/CIF/product_cockpit_page_association.png)

## リリース日：2022年6月

| コンポーネント | バージョン | 詳細 |
|:-------|:-----:|---------------------:|
| CIF アドオン | 2022.07.05.00 | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.07.05.00.zip) |
| CIF コアコンポーネント | 2.10.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.10.0) |
| CIF Venia 参照サイト | 2022.07.04 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.07.04) |

### 新機能 {#what-is-new-june}

* 製品カタログのエンリッチメントにより、AEM ページにサポートが追加され、作成者はページと製品の関連付けを管理できるようになりました。

* CIF コアコンポーネントの様々な改善点

### バグ修正 {#bug-fixes-june}

* クライアントサイドの価格取得にログイントークンを追加

* データレイヤーのページコンポーネントが正しくありません。

## リリース日：2022年5月

| コンポーネント | バージョン | 詳細 |
|:-------|:-----:|---------------------:|
| CIF アドオン | 2022.05.31.00 | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.05.31.00.zip) |
| CIF コアコンポーネント | 2.9.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.9.0) |
| CIF Venia 参照サイト | 2022.05.30 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.05.30) |

### 新機能 {#what-is-new-may}

* よりわかりやすいシンプルな概要を示す新しい製品コックピットのプロパティページ

![製品コックピットのプロパティの概要](/help/assets/CIF/product_cockpit_properties_overview.png)

* I/O Runtime 上のサードパーティのコネクタの互換性と堅牢性の向上

* GQL クライアント設定の上書きサポートの改善（カスタムキャッシュ動作の設定など）

### バグ修正 {#bug-fixes-may}

* 複数値の製品ピッカーフィールドに、2 番目の製品と追加の製品が無効と表示されます

* 製品ピッカーがコンポーネントの背後に隠れている場合があります

## リリース日：2022年4月

| コンポーネント | バージョン | 詳細 |
|:-------|:-----:|---------------------:|
| CIF アドオン | 2022.04.28.00 | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.04.28.00.zip) |
| CIF コアコンポーネント | 2.8.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.8.0) |
| CIF Venia 参照サイト | 2022.04.28 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.04.28) |

### 新機能 {#what-is-new-april}

* 製品コックピットへのクイックアクセス：サイトエディターでワンクリックで詳細な製品情報に簡単にアクセス

  ![ウィッシュリストを有効にする](/help/assets/CIF/enable-wishlist.png)

* 追加のマーケティングコマースコンポーネントのサポート：コンポーネントを、買い物かごへの追加と、リストへの追加のコールトゥアクションを表示するように設定できます。

  ![製品コックピットへのサイトエディターショートカット](/help/assets/CIF/sites-editor-shortcut-to-cockpit.png)

## リリース日：2022年2月

| コンポーネント | バージョン | 詳細 |
|:-------|:-----:|---------------------:|
| CIF アドオン | 2022.02.24.00 | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.02.24.00.zip) |
| CIF コアコンポーネント | 2.6.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) |
| CIF Venia 参照サイト | 2022.02.24 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.02.24) |

### 新機能 {#what-is-new-march}

* ベータ版：AEM CIF Search コアコンポーネントは、Commerce LiveSearch をサポートします。
* マルチストアシナリオでの SEO 向上：PDP/PLP の URL 形式を、CIF Cloud Config プロパティを介してストアレベルで設定できるようになりました。
* 製品ピッカーは、ユーザーインターフェイスの新しいフィルターオプションを介して、ステージングされた製品をサポートします。コンテンツ担当者は、今後の製品の発売に備えて製品コンテンツ管理を準備できます
* 設定プロキシ URL の代わりに CIF Cloud Config 名を使用して、CIF 設定の管理とエラー処理を簡略化しました。
* 製品リストおよびカルーセルコンポーネントの手動カテゴリ選択。コンテンツ担当者は、カタログエクスペリエンス以外で、コンテンツページ上でこれらのコンポーネントを使用できます

## リリース日：2022年1月

| コンポーネント | バージョン | 詳細 |
|:-------|:-----:|---------------------:|
| CIF アドオン | 2022.01.20.00 | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.01.20.00.zip) |
| CIF コアコンポーネント | 2.5.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.5.0) |
| CIF Venia 参照サイト | 2022.01.27 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.01.27) |

### 新機能 {#what-is-new-january}

* myAccount コンポーネントの強化機能
* 「製品のレコメンデーション」コンポーネントで追加のページタイプ（ホームページ、買い物かご、注文確認）がサポートされるようになりました
* **ウィッシュリスト**
   * ログインした訪問者は、ウィッシュリストに製品を追加できます
   * ウィッシュリストとその製品の管理は、myAccount を使用して行えます
   * 「ウィッシュリストに追加」ボタンは、ポリシー（製品ティーザー、製品詳細など）を介して、コンポーネントレベルで有効／無効にできます
   * コアコンポーネントおよび AEM Venia ストアフロントで使用できます。

![ウィッシュリスト](/help/assets/CIF/wishlist.png)
