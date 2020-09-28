---
title: Compareおよび [!DNL Assets] Media Libraryの機能
description: CompareとMedia Libraryの各ソリューショ [!DNL Experience Manager Assets] ンの違いを理解しています。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5069c2cd26e84866d72a61d36de085dadd556cdd
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 22%

---


# [!DNL Experience Manager Assets] 対 [!DNL Experience Manager] 応メディアライブラリ {#aem-assets-vs-aem-medialibrary}

[!DNL Adobe Experience Manager Assets] はプラットフォームの不可欠な部 [!DNL Experience Manager] 分です。 This smooth integration is seen as a major advantage of [!DNL Experience Manager] and ensures consistency in content management and high productivity for content authors.

## よくある質問 {#frequently-asked-questions}

### What is [!DNL Assets]? {#what-is-aem-assets}

[!DNL Assets] は、ユーザー [!DNL Experience Manager] がwebベースのリポジトリでデジタルアセット(画像、ビデオ、ドキュメント、オーディオクリップ)を管理できる機能です。 [!DNL Assets] には、メタデータのサポート、レンディション、ファインダー、管理インターフェイスが含まれます。

### What is the [!DNL Experience Manager] Media Library? {#what-is-the-aem-media-library}

The [!DNL Experience Manager] Media Library is a designated part of the [!DNL Experience Manager] WCM content repository where images and other shared resources are stored. メディアライブラリは、WCMに基本的なデジタルアセット管理機能を提供します。

### What do I get from [!DNL Assets] that is not part of WCM? {#what-do-i-get-from-aem-assets-that-is-not-part-of-aem-wcm}

Unique features that are only available to customers of [!DNL Assets] are:

* タイトル、タグ、説明以外のメタデータを抽出して編集する機能
* スタートアップスクリーンから [!DNL Assets] 使用できる管理者。
* 取り込み、アセット削除、サブアセット処理、メタデータ抽出など、Digital Asset Managementに関連するすべてのワークフローステップ。
* ライブラリ `dam` を含めます。

Using these features requires a valid license of [!DNL Assets].

### Is [!DNL Assets] available as a separate Package? {#is-aem-assets-available-as-a-separate-package}

いいえ。To ease installation and deployment, all [!DNL Experience Manager] applications and add-ons are delivered in one single package with all functionality included. これは、パッケージに含まれるすべての機能の使用権がユーザーにあることを表すわけではありません。

### デジタルアセットのメタデータを編集したいのですが、Do I need [!DNL Assets]? {#i-want-to-edit-metadata-of-digital-assets-do-i-need-aem-assets}

If you are planning to edit metadata other than title, description and tags, it is required to license [!DNL Assets].

### Web サイトでカテゴリ述語を使用したいのですが、Do I need [!DNL Assets]? {#i-want-to-use-the-category-predicate-on-my-website-do-i-need-aem-assets}

はい、カテゴリ述語はの一部であり、 [!DNL Assets][!DNL Assets] ライセンスが必要です。

### 画像を読み込むときに自動的にサイズ変更したいのですが、Do I need [!DNL Assets]? {#i-want-to-automatically-resize-images-upon-import-do-i-need-aem-assets}

いいえ。Resizing and automatic workflow-driven transformation of static images as well as the ability to manage renditions are part of [!DNL Experience Manager] Media Library. These features do not require an [!DNL Assets] license.

### カスタマイズされた画像コンポーネントを使用して画像をサイズ変更したいのですが、Do I need [!DNL Assets]? {#i-want-to-resize-images-using-a-customized-image-component-do-i-need-aem-assets}

画像コンポーネントは WCM に含まれています。The graphics library that is being used by the image component (but also by [!DNL Assets]) is part of the [!DNL Experience Manager] platform and does not require an [!DNL Assets] license.

### How can I prevent my users from using [!DNL Assets] if I did not license [!DNL Assets]? {#how-can-i-prevent-my-users-from-using-aem-assets-if-i-did-not-license-aem-assets}

You can remove all [!DNL Assets]-specific workflows, components, taxonomies, options and the [!DNL Assets] admin from [!DNL Experience Manager]. Doing so prevents your users from accidentally using [!DNL Assets] features that you did not license.

### ページに画像を追加し、その画像の切り抜きやサイズ変更を実行したいのですが、Do I need Assets? {#i-want-to-add-images-to-a-page-and-want-to-crop-and-resize-these-images-do-i-need-aem-assets}

For this use case it is not required to buy [!DNL Assets], even the use of the Media Library is not required to use images on a website as the smart image component allows uploading images directly into the page.

### A detailed list of features available in [!DNL Assets] vs Media Library {#listoffeatures}

**Experience Manager Assets**

* コレクションと Lightbox
* 高度なメタデータプロパティと管理
* Adobe Asset Link（Creative Cloud エンタープライズ版への接続）
* [!DNL Experience Manager] デスクトップアプリ
* 処理プロファイル
* [!DNL Adobe InDesign Server] 統合
* アセットテンプレートとカタログプロデューサーフレームワーク
* [!DNL Adobe Photoshop]、 [!DNL Adobe Illustrator]および [!DNL Adobe InDesign] 統合
* 多言語アセット管理
* PIM との統合
* 権限管理
* Camera Raw支持
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
* Marketing Cloud統合
* UIのカスタマイズと拡張
* コメントと注釈
