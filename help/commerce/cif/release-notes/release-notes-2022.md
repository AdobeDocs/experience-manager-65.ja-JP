---
title: AEM Content and Commerce リリースノート 2022
description: AEM Content and Commerce リリースノート 2022
exl-id: d0a66e70-c4f1-4051-8161-11f07dad0612
source-git-commit: 1a82930d9f0aa84cea590782aba2e70ec23b41c3
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 53%

---

# コマース統合フレームワーク GitHub リリースの概要

## 必要システム構成の概要

現在使用している CIF バージョン、または将来使用する予定の CIF バージョンについて、以下の表で最小必要システム構成を確認します。

| コンポーネント | システム要件 |
|:-------|:-----:|
| CIF アドオン | 最小：AEM 6.5.7、Magento 2.3.5 GraphQL スキーマ |
| CIF コアコンポーネント | [システム要件](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| AEM プロジェクトアーキタイプ | [システム要件](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## リリース日：2022年3月

| コンポーネント | バージョン | 詳細 |
|:-------|:-----:|---------------------:|
| CIF アドオン | 2022.02.24.00 | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.02.24.00.zip) |
| CIF コアコンポーネント | 2.6.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) |
| CIF Venia 参照サイト | 2022.02.24 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.02.24) |

### 新機能 {#what-is-new-march}

* ベータ版：AEM CIF Search コアコンポーネントは、Commerce LiveSearch をサポートします。
* マルチストアシナリオでの SEO の改善：PDP/PLP の URL 形式を、CIF Cloud Config プロパティを介してストアレベルで設定できるようになりました。
* 製品ピッカーは、UI の新しいフィルターオプションを使用して、ステージングされた製品をサポートします。  これにより、コンテンツ担当者は、今後の製品の発売に備えて製品コンテンツ管理を準備できます
* 設定プロキシ URL の代わりに CIF Cloud Config 名を使用して、CIF 設定の管理とエラー処理を簡略化しました。
* 製品リストおよびカルーセルコンポーネントの手動カテゴリ選択。 これにより、コンテンツ担当者は、カタログエクスペリエンス以外で、コンテンツページ上でこれらのコンポーネントを使用できます

## リリース日：2022年1月

| コンポーネント | バージョン | 詳細 |
|:-------|:-----:|---------------------:|
| CIF アドオン | 2022.01.20.00 | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.01.20.00.zip) |
| CIF コアコンポーネント | 2.5.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.5.0) |
| CIF Venia 参照サイト | 2022.01.27 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.01.27) |

### 新機能 {#what-is-new-january}

* myAccount コンポーネントの強化
* 製品レコメンデーションコンポーネントは、追加のページタイプ（ホームページ、買い物かご、注文の確認）をサポートします。
* **ウィッシュリスト**
   * ログインした訪問者は、ウィッシュリストに製品を追加できます
   * ウィッシュリストとその製品の管理は、myAccount を通じて可能です
   * 「ウィッシュリストに追加」ボタンは、ポリシー（製品ティーザー、製品の詳細など）を介して、コンポーネントレベルで有効/無効にできます
   * コアコンポーネントおよびAEM Venia ストアフロントで使用できます。

![ウィッシュリスト](/help/assets/CIF/wishlist.png)
