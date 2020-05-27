---
title: Adobe Experience Manager AssetsとMedia Libraryの機能を比較します。
description: Experience Manager Assetsとメディアライブラリの機能を比較し、違いを把握する。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 36%

---


# Experience Manager AssetsとExperience Manager Media Libraryの比較 {#aem-assets-vs-aem-medialibrary}

Adobe Experience Manager Assetsは、Experience Managerプラットフォームに不可欠な要素です。 このスムーズな統合は、Experience Managerの主な利点と見なされ、コンテンツ管理の一貫性とコンテンツ作成者の生産性の高さを保証します。

## よくある質問 {#frequently-asked-questions}

### What is Assets? {#what-is-aem-assets}

アセットは、Experience Managerの機能で、Webベースのリポジトリでデジタルアセット(画像、ビデオ、ドキュメントおよびオーディオクリップ)を管理できます。 アセットには、メタデータのサポート、レンディション、ファインダーおよび管理インターフェイスが含まれます。

### Experience Managerのメディアライブラリとは何ですか？ {#what-is-the-aem-media-library}

Experience Managerメディアライブラリは、Experience Manager WCMコンテンツリポジトリの中で指定された部分で、画像やその他の共有リソースが保存されます。 メディアライブラリは、WCMに基本的なデジタルアセット管理機能を提供します。

### What do I get from Assets that is not part of WCM? {#what-do-i-get-from-aem-assets-that-is-not-part-of-aem-wcm}

 Assets のお客様だけが使用できる独自の機能は次のとおりです。

* タイトル、タグ、説明以外のメタデータを抽出して編集する機能
* アセット管理者（スタートアップスクリーンから利用可能）。
* 取り込み、アセット削除、サブアセット処理、メタデータ抽出など、Digital Asset Managementに関連するすべてのワークフローステップ。
* ライブラリ `dam` を含めます。

これらの機能を使用するには、 Assets の有効なライセンスが必要です。

### Is Assets available as a separate Package? {#is-aem-assets-available-as-a-separate-package}

いいえ。インストールとデプロイを容易にするために、すべてのExperience Managerアプリケーションとアドオンは、すべての機能を含む1つのパッケージで提供されます。 これは、パッケージに含まれるすべての機能の使用権がユーザーにあることを表すわけではありません。

### デジタルアセットのメタデータを編集したいのですが、Do I need Assets? {#i-want-to-edit-metadata-of-digital-assets-do-i-need-aem-assets}

タイトル、説明およびタグ以外のメタデータを編集する場合は、 Assets のライセンスが必要です。

### Web サイトでカテゴリ述語を使用したいのですが、Do I need Assets? {#i-want-to-use-the-category-predicate-on-my-website-do-i-need-aem-assets}

はい。カテゴリ述語はアセットの一部であり、アセットライセンスが必要です。

### 画像を読み込むときに自動的にサイズ変更したいのですが、Do I need Assets? {#i-want-to-automatically-resize-images-upon-import-do-i-need-aem-assets}

いいえ。静的な画像のサイズ変更とワークフローに基づく自動変換、およびレンディション管理機能は、Experience Managerメディアライブラリの一部です。 これらの機能には、 Assets のライセンスは必要ありません。

### カスタマイズされた画像コンポーネントを使用して画像をサイズ変更したいのですが、Do I need Assets? {#i-want-to-resize-images-using-a-customized-image-component-do-i-need-aem-assets}

画像コンポーネントは WCM に含まれています。画像コンポーネント（およびアセット）が使用するグラフィックライブラリは、Experience Managerプラットフォームの一部であり、アセットのライセンスは必要ありません。

### 自分が Assets のライセンスを所持していない場合、ユーザーが Assets を使用しないようにする方法はありますか。 {#how-can-i-prevent-my-users-from-using-aem-assets-if-i-did-not-license-aem-assets}

Experience Managerから、アセットに固有のワークフロー、コンポーネント、分類、オプションおよびアセット管理者をすべて削除できます。 これにより、ライセンスを取得していないAssets機能を誤って使用するのを防ぐことができます。

### ページに画像を追加し、その画像の切り抜きやサイズ変更を実行したいのですが、Do I need Assets? {#i-want-to-add-images-to-a-page-and-want-to-crop-and-resize-these-images-do-i-need-aem-assets}

このような使用法では、 Assets を購入する必要はありません。Web サイト上で画像を使用する目的では、Media Library も使用する必要はありません。画像コンポーネントを使用すると、ページに画像を直接アップロードできるからです。

### A detailed list of features available in Assets vs Media Library {#listoffeatures}

**Experience Manager Assets**

* コレクションと Lightbox
* 高度なメタデータプロパティと管理
* Adobe Asset Link（Creative Cloud エンタープライズ版への接続）
* Experience Manager デスクトップアプリケーション
* 処理プロファイル
* [!DNL Adobe InDesign Server] 統合
* アセットテンプレートとカタログプロデューサーフレームワーク
* [!DNL Adobe Photoshop]、 [!DNL Adobe Illustrator]および [!DNL Adobe InDesign] 統合
* 多言語アセット管理
* PIM との統合
* 権限管理
* Camera RAWのサポート
* 検索ファセットの管理と設定
* 事前定義済み DAM ワークフロー（写真撮影など）
* 「インサイト」と呼ばれるアセットレポートと分析
* 3次元資産管理
* Connected Assets
* Brand Portal
* セルフサービスアクセス
* 参照、検索、ダウンロード
* コレクションとフォルダーの共有
* 管理ツールとインターフェイス
* スマートタグ付け
* ビジュアル検索

**Media Library**

* 基本的なメタデータプロパティ
* tag management
* バージョン管理
* 静的レンディション
* プロジェクト，タスク，ワークフローオーサリング
* アクティビティストリーム（タイムライン）
* クエリビルダー（API）
* Marketing Cloudの統合
* UIのカスタマイズと拡張
* コメントと注釈
