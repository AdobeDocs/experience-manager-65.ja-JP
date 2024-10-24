---
title: AEM Content and Commerce リリースノート 2024年
description: Adobe Experience Manager Content and Commerce リリースノート 2024年。
exl-id: 372e6a46-72bb-4db4-ad01-534ca723ae58
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 1788e5f77d4c46a548710361e9e5dae3c6daab28
workflow-type: ht
source-wordcount: '221'
ht-degree: 100%

---

# コマース統合フレームワーク GitHub リリースの概要

## 必要システム構成の概要

現在使用している CIF バージョン、または今後使用する予定の CIF バージョンについては、以下の表で最小必要システム構成を確認してください。

| コンポーネント | システム要件 |
|:-------|:-----------------------------------------------------------------------------------------------:|
| CIF アドオン | 最小：AEM 6.5.18、Adobe Commerce 2.3.5 GraphQL スキーマ |
| CIF コアコンポーネント | [システム要件](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| AEM プロジェクトアーキタイプ | [システム要件](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## リリース日：2024年10月

| コンポーネント | バージョン | 詳細 |
|:-------|:-------:|-----------------------------------------------------------------------------------------------------------:|
| CIF コアコンポーネント | 2.15.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.15.0) |

### バグ修正 {#bug-fixes-October}

* コア CIF コンポーネントで正しく動作するように UI テストを修正しました。
* カテゴリ URL 形式がクラウドインスタンスで期待どおりに機能しない問題を解決しました。

## リリース日：2024年9月

| コンポーネント | バージョン | 詳細 |
|:-------|:-------:|-----------------------------------------------------------------------------------------------------------:|
| CIF コアコンポーネント | 2.14.2 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.14.2) |

### 機能改善 {#improvements-September}

* カテゴリ制限をカスタマイズ可能にします。

### バグ修正 {#bug-fixes-September}

* Commerce のフィールドが、Assets メタデータスキーマエディターと適切に統合されていない。
* カルーセル製品のマルチフィールドでのドラッグ＆ドロップの問題。
* カルーセルカテゴリのマルチフィールドでのドラッグ＆ドロップの問題。
* カテゴリと製品のエディターページのページ情報のメニューで、オンクリックが機能しない。
* 注文確認ページに注文番号が表示されない。

## リリース日：2024年1月

| コンポーネント | バージョン | 詳細 |
|:-------|:-------:|-----------------------------------------------------------------------------------------------------------:|
| CIF コアコンポーネント | 2.12.6 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.12.6) |

### バグ修正 {#bug-fixes-january}

* 製品コレクションコンポーネントの「買い物かごに追加」ボタンと「ウィッシュリストに追加」ボタンを修正
