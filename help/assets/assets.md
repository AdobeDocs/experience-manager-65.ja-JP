---
title: 概要 [!DNL Adobe Experience Manager Assets]。
description: デジタルアセット管理、その使用例、 [!DNL Adobe Experience Manager Asset] およびオファーについて説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0d5b3a442756e95c15cb01c4117a83b761dc8367
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 35%

---


# DAMソリュ [!DNL Adobe Experience Manager Assets] ーションについて {#administering-assets}

[!DNL Assets] は、プラットフォームに不可欠なツールで、企業がデジタルアセットを管理および配信できるようにするDigital Asset Management(DAM)ツールです。 [!DNL Experience Manager] 画像、ビデオ、ドキュメント、オーディオクリップ、3Dファイル、リッチメディアなど、Web上で使用したり、印刷したり、デジタル配信用に様々な種類のデジタルアセットを管理、保存、アクセスできます。

## What is Digital Asset Management? {#what-is-digital-asset-management}

[!DNL Assets]AEM は、組織の主要なデジタルアセットを、企業全体で共有および配布する機能を提供します。組織のユーザーは、画像、グラフィック、オーディオ、ビデオおよびドキュメントなどのデジタルアセットを、Web インターフェイス（または CIFS や WebDAV フォルダー）を使用して格納、管理したり、これらのデジタルアセットにアクセスしたりできます。

[!DNL Assets] の機能 [!DNL Experience Manager] を使用すると、次のことができます。

* 様々なファイル形式の画像、ドキュメント、オーディオファイルおよびビデオファイルを追加および共有する。
* タグ、ライトボックス、星（お気に入り）でアセットをグループ化して、アセットを管理します。 アセットに注釈を追加する。
* ファイル名、ドキュメントのフルテキスト、日付、ドキュメントタイプおよびタグに基づいてアセットを検索する。
* アセットのメタデータ情報を追加または編集する。メタデータは、関連するアセットと共に、自動的にバージョン管理されます。アセットのメタデータの読み込みまたは書き出しができます。
* 拡大縮小や画像フィルターの追加など、画像編集機能を実行する。WebDAV または CIFS フォルダーを使用して、複数のデジタルアセットを同時に読み込んだり、書き出したりする。
* ワークフローおよび通知を使用して、アセットのセットに関する結合処理とダウンロードを許可し、アセットへのアクセス権を管理する。

### [!DNL Experience Manager Assets] は、 [!DNL Experience Manager Sites] {#aem-assets-fully-integrated-in-cq-wcm}

[!DNL Assets] すべての用途に対して完全に統合 [!DNL Sites] され、シームレスに機能します。 例えば、Webページの作成時に、 [!DNL Sites] 作成者はコンテンツファインダーでデジタルアセットを検索して使用できます。 のユーザーインターフェイス [!DNL Assets] は、のユーザーインターフェイスと同じで [!DNL Sites]す。 詳しくは、「サイト [の概要](/help/sites-authoring/page-authoring.md) 」を参照してください。

基本的なユーザインターフェイスは、のインターフェイスと同じで [!DNL Sites]す。 詳しくは、「サイト [の概要](/help/sites-authoring/page-authoring.md) 」を参照してください。

### Digital Asset Management versus image component {#digital-asset-management-versus-image-component}

画像をDAMリポジトリに配置するか、画像コンポーネントを使用するかを決定する際は、画像のライフサイクルを考慮します。

* 画像のライフサイクルがページと同じ場合は、画像コンポーネントを使用します。
* If the image has a separate life cycle, for example, if you use the image twice or outside WCM, use [!DNL Assets].

## What are digital assets? {#what-are-digital-assets}

アセットとは、複数のレンディションを持つことができ、サブアセット（例えば、photoshopファイルのレイヤー、PowerPointファイルのスライド、PDFのページ、ZIP内のファイル）を持つことができるデジタルドキュメント、画像、ビデオまたはオーディオ（またはその一部）です。

アセットは、基本的にバイナリ、メタデータ、レンディション、サブアセットを組み合わせたものです。詳しくは、[DAM パフォーマンスガイド](/help/sites-deploying/assets-performance-sizing.md)を参照してください。

>[!CAUTION]
>
>Uploading and/or editing a large volume of assets (particularly images) can impact the performance of your [!DNL Experience Manager] instance.

### [!DNL Experience Manager Assets] 用語 {#aem-assets-terminology}

When working with digital assets in [!DNL Experience Manager], you need to understand the following terminology:

* **コレクション**: 物理的な場所（フォルダー）、共通のプロパティ（保存された検索フォルダー）またはユーザー選択（ライトボックスのフォルダー）に基づくアセットのコレクションです。

* **メタデータ**[!DNL Assets] はメタデータを持つ。 例えば、作成者、有効期限、DRM情報(Digital Rights Management)などがあります。 メタデータは、アクセスが制御されます。[!DNL Assets] では、追加設定なしに、次の共通の各種メタデータスキーマがサポートされます。

   * Dublin Core：作成者、説明、日付、件名などが含まれます。
   * IPTC：イベント、モデル、場所などが含まれます。
   * WCM: ページプロパティ、 [!UICONTROL オン時間] 、 [!UICONTROL オフ時間]などを含みます。

* **タグ付け**: [!DNL Assets] は、タグ付けと分類が可能です。 詳しくは、アセットの [編成を参照してください](/help/assets/organize-assets.md)。

* **レンディション**: レンディションとは、アセットのバイナリ表現です。 [!DNL Assets] 常に主要な表現（アップロードされたファイルの表現）を持ちます。 アセットは、例えば、カスタマイズされたワークフロー手順によって作成された、またはアセットがアップロードされた際に作成された、任意の数の追加の表現を持つことができます。レンディションには、様々なサイズや解像度のものがあります。また、透かしが追加されていたり、その他の変更された特徴を持つものもあります。

* **バージョン**: バージョン管理では、特定の時点でのデジタルアセットのスナップショットが作成されます。 これにより、以前のバージョンにアセットを復元できます。See [versioning in Assets](managing-assets-touch-ui.md#asset-versioning).

* **サブアセット**: サブアセットとは、ファイル内のレイヤーやPDFファイル内のページなど、アセットを構成するアセ [!DNL Adobe Photoshop] ットのことです。 In [!DNL Assets], you can manage sub-assets as you would assets.

### How to work with assets {#how-to-work-with-assets}

アセットまたはコレクションに対してアクションを実行します。アクションでは、アセット、コレクションおよびレンディションを作成したり変更したりできます。アセットに対して実行する基本的な操作の多く(アップロード、削除、更新、サブアセットの保存 — 事前設定済みのワークフローをトリガー)。 These are automatically turned on in [!DNL Assets] and are described in detail in [!DNL Assets] media handlers.

次の事前設定済みワークフローで実行できるタスクです。

* アセットをリポジトリに保存または削除します。
* アセットのメタデータを抽出し、保存します。 個々のメタデータ項目はXMPとして保存されます。
* アセットのレンディションとサムネールを生成する、 必要に応じて、自動サイズ変更や切り抜きを含めます。
* 必要に応じてアセットをトランスコードします。 例えば、モバイルおよびWebでの使用に使用するビデオは、24フレーム/秒でトランスコードされ、30フレーム/秒のビデオをダウンロードします。 モバイルおよびWebでの使用に使用するオーディオは128 Kbpsでトランスコードされ、192 Kbpsでのダウンロード用のオーディオです。

また、ワークフローを手動で適用することもできます。デフォルトワークフローのリストについては、[ Assets メディアハンドラー](/help/assets/media-handlers.md)を参照してください。

## [!DNL Experience Manager Assets] および [!DNL MediaLibrary] {#cq-dam-vs-cq-medialibrary}

相違点について詳しくは、 [アセットとMediaLibrary](/help/assets/medialibrary.md) （英語のみ）を参照してください。
