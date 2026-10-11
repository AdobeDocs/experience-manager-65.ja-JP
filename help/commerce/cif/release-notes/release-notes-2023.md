---
title: AEM Content and Commerce リリースノート 2023年
description: Adobe Experience Manager Content and Commerce リリースノート 2023年。
exl-id: 00349400-6860-4e3c-ba56-fa12afc5db1d
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 100%
---
# Commerce Integration Framework GitHub リリースの概要

## 必要システム構成の概要

現在使用している CIF バージョン、または今後使用する予定の CIF バージョンについては、以下の表で最小必要システム構成を確認してください。

| コンポーネント | システム要件 |
|:-------|:-----------------------------------------------------------------------------------------------:|
| CIF アドオン | 最小：AEM 6.5.8、Adobe Commerce 2.3.5 GraphQL スキーマ |
| CIF コアコンポーネント | [システム要件](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| AEM プロジェクトアーキタイプ | [システム要件](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## リリース日：2023年12月

| コンポーネント | バージョン | 詳細 |
|:-------|:-------:|-----------------------------------------------------------------------------------------------------------:|
| CIF コアコンポーネント | 2.12.4 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.12.4) |

### バグ修正 {#bug-fixes-december}

* ページ v3 リソースタイプに登録されている製品およびカテゴリのリダイレクトサーブレット
* CIF AEP 拡張機能のライブ検索イベントを修正

## リリース日：2023年11月

| コンポーネント | バージョン | 詳細 |
|:-------|:-------------:|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| CIF アドオン | 2023.11.23.00 | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/jp/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2023.11.23.00.zip) |
| CIF Venia 参照サイト | 2023.11.08 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2023.11.08) |

### バグ修正 {#bug-fixes-november}

* CIF 設定コンソールでの 40 件を超える設定の表示

## リリース日：2023年7月

| コンポーネント | バージョン | 詳細 |
|:-------|:-------:|--------------------------------------------------------------------------------------------------------------:|
| CIF コアコンポーネント | 2.12.2 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.12.2) |

### 新機能 {#what-is-new-july}

* `ProductList` コンポーネントの製品フィルターフック
