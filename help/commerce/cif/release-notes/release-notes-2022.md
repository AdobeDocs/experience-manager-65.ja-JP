---
title: AEM Content and Commerce リリースノート 2022
description: AEM Content and Commerce リリースノート 2022
exl-id: ec47c5f8-d4dd-469f-94df-5ee28f25d696
source-git-commit: 26df21270e8c586ba21b9bf3e9fc5003facbaade
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 67%

---

# コマース統合フレームワーク GitHub リリースの概要

## 必要システム構成の概要

現在使用している CIF バージョン、または将来使用する予定の CIF バージョンについて、以下の表で最小必要システム構成を確認します。

| コンポーネント | システム要件 |
|:-------|:-----:|
| CIF アドオン | 最小：AEM 6.5.7、Magento 2.3.5 GraphQL スキーマ |
| CIF コアコンポーネント | [システム要件](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| AEM プロジェクトアーキタイプ | [システム要件](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

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

