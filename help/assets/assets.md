---
title: ' [!DNL Adobe Experience Manager Assets]の紹介'
description: デジタルアセット管理、その使用例、 [!DNL Adobe Experience Manager Asset] オファーについて説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: b851bfb2758db60e960afd4720d04202934c18bc
workflow-type: tm+mt
source-wordcount: '874'
ht-degree: 33%

---


# [!DNL Adobe Experience Manager Assets]をDAMソリューションとして{#administering-assets}

[!DNL Assets] は、プラットフ [!DNL Experience Manager] ォームに不可欠なDAM(Digital Asset Management)ツールで、デジタルアセットの管理と配布を企業に対して可能にします。画像、ビデオ、ドキュメント、オーディオクリップ、3Dファイル、リッチメディアなど、Web上で使用したり、印刷したり、デジタル配信用に様々な種類のデジタルアセットを管理、保存、アクセスできます。

## Digital Asset Managementとは{#what-is-digital-asset-management}

[!DNL Assets]AEM は、組織の主要なデジタルアセットを、企業全体で共有および配布する機能を提供します。組織のユーザーは、画像、グラフィック、オーディオ、ビデオおよびドキュメントなどのデジタルアセットを、Web インターフェイス（または CIFS や WebDAV フォルダー）を使用して格納、管理したり、これらのデジタルアセットにアクセスしたりできます。

[!DNL Assets] の機能 [!DNL Experience Manager] を使用すると、次のことができます。

* 様々なファイル形式の画像、ドキュメント、オーディオファイルおよびビデオファイルを追加および共有する。
* タグ、ライトボックス、星（お気に入り）でアセットをグループ化して、アセットを管理します。 アセットに注釈を追加する。
* ファイル名、ドキュメントのフルテキスト、日付、ドキュメントタイプおよびタグに基づいてアセットを検索する。
* アセットのメタデータ情報を追加または編集する。メタデータは、関連するアセットと共に、自動的にバージョン管理されます。アセットのメタデータの読み込みまたは書き出しができます。
* 拡大縮小や画像フィルターの追加など、画像編集機能を実行する。WebDAV または CIFS フォルダーを使用して、複数のデジタルアセットを同時に読み込んだり、書き出したりする。
* ワークフローおよび通知を使用して、アセットのセットに関する結合処理とダウンロードを許可し、アセットへのアクセス権を管理する。

### [!DNL Experience Manager Assets] は、  [!DNL Experience Manager Sites] {#aem-assets-fully-integrated-in-cq-wcm}

[!DNL Assets] すべての用途に対して完全に統合 [!DNL Sites] され、シームレスに機能します。例えば、Webページの作成時に、[!DNL Sites]作成者はコンテンツファインダーでデジタルアセットを検索して使用できます。 [!DNL Assets]のユーザーインターフェイスは、[!DNL Sites]と同じです。 詳しくは、[サイトの概要](/help/sites-authoring/page-authoring.md)を参照してください。

基本的なユーザーインターフェイスは、[!DNL Sites]と同じです。 詳しくは、[サイトの概要](/help/sites-authoring/page-authoring.md)を参照してください。

### デジタルアセット管理と画像コンポーネント{#digital-asset-management-versus-image-component}

画像をDAMリポジトリに配置するか、画像コンポーネントを使用するかを決定する際は、画像のライフサイクルを考慮します。

* 画像とページのライフサイクルが同じ場合は、画像コンポーネントを使用します。
* イメージに別々のライフサイクルがある場合（例えば、WCMの外部で2回イメージを使用する場合）、[!DNL Assets]を使用します。

## デジタルアセットとは{#what-are-digital-assets}

アセットは、複数のレンディションを持つことができ、サブアセット（例えば、photoshopファイルのレイヤー、PowerPointファイルのスライド、PDFのページ、ZIP内のファイル）を持つことができるデジタルドキュメント、画像、ビデオまたはオーディオ（またはその一部）です。

アセットは、基本的にバイナリ、メタデータ、レンディション、サブアセットを組み合わせたものです。詳しくは、[DAM パフォーマンスガイド](/help/sites-deploying/assets-performance-sizing.md)を参照してください。

>[!CAUTION]
>
>大量のアセット（特に画像）をアップロードまたは編集すると、[!DNL Experience Manager]展開のパフォーマンスに影響を与える可能性があります。

### [!DNL Experience Manager Assets] 用語  {#aem-assets-terminology}

[!DNL Experience Manager]でデジタルアセットを操作する場合は、次の用語を理解する必要があります。

* **コレクション**:物理的な場所（フォルダー）、共通のプロパティ（保存された検索フォルダー）またはユーザー選択（ライトボックスフォルダー）に基づく、アセットのコレクションです。

* **Metadatahave metadata;** [!DNL Assets] 例えば、作成者、有効期限、DRM情報(Digital Rights Management)などがあります。メタデータは、アクセスが制御されます。[!DNL Assets] では、追加設定なしに、次の共通の各種メタデータスキーマがサポートされます。

   * Dublin Core：作成者、説明、日付、件名などが含まれます。
   * IPTC：イベント、モデル、場所などが含まれます。
   * WCM:ページのプロパティ、[!UICONTROL On Time]、[!UICONTROL Off Time]などを含みます。

* **タグ付け**: [!DNL Assets] は、タグ付けと分類が可能です。[アセットの整理](/help/assets/organize-assets.md)を参照してください。

* **レンディション**:レンディションとは、アセットのバイナリ表現です。[!DNL Assets] 常に主要な表現（アップロードされたファイルの表現）を持ちます。アセットは、例えば、カスタマイズされたワークフロー手順によって作成された、またはアセットがアップロードされた際に作成された、任意の数の追加の表現を持つことができます。レンディションには、様々なサイズや解像度のものがあります。また、透かしが追加されていたり、その他の変更された特徴を持つものもあります。

* **バージョン**:バージョン管理では、特定の時点でのデジタルアセットのスナップショットが作成されます。これにより、以前のバージョンにアセットを復元できます。 [!DNL Assets]](manage-assets.md#asset-versioning)の[バージョン管理を参照してください。

* **サブアセット**:サブアセットとは、例えば、 [!DNL Adobe Photoshop] ファイル内のレイヤーやPDFファイル内のページなど、アセットを構成するアセットです。[!DNL Assets]では、サブアセットをアセットと同じように管理できます。

### デジタルアセットの操作方法{#how-to-work-with-assets}

アセットまたはコレクションに対してアクションを実行します。アクションでは、アセット、コレクションおよびレンディションを作成したり変更したりできます。アセットに対して実行する基本的な操作の多く(アップロード、削除、更新、保存、サブアセット —トリガーの事前設定済みワークフロー)。 これらは[!DNL Assets]で自動的にオンになり、[!DNL Assets]メディアハンドラーで詳しく説明されます。

次の事前設定済みワークフローで実行できるタスクです。

* アセットをリポジトリに保存または削除します。
* アセットのメタデータを抽出し、保存します。個々のメタデータ項目はXMPとして保存されます。
* アセットのレンディションとサムネールを生成する、必要に応じて、自動サイズ変更や切り抜きを含めます。
* 必要に応じてアセットをトランスコードします。例えば、モバイルおよびWebでの使用に使用するビデオは、24フレーム/秒でトランスコードされ、30フレーム/秒のビデオをダウンロードします。モバイルおよびWebでの使用に使用するオーディオは128 Kbpsでトランスコードされ、192 Kbpsでのダウンロード用のオーディオです。

また、ワークフローを手動で適用することもできます。デフォルトワークフローのリストについては、[ Assets メディアハンドラー](media-handlers.md)を参照してください。

## [!DNL Experience Manager Assets] および [!DNL Media Library] {#cq-dam-vs-cq-medialibrary}

相違点については、[アセットとメディアライブラリ](medialibrary.md)を参照してください。

>[!MORELIKETHIS]
>
>* [ビデオの紹介 — 最新のDAMとしてのExperience Managerアセット](https://www.youtube.com/watch?v=PBwQqZgC-yo)
>* [メタデータの概念について](/help/assets/metadata-concepts.md)

