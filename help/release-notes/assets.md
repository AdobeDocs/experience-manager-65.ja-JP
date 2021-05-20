---
title: ' [!DNL Adobe Experience Manager Assets] 6.5のリリースノート。'
description: ' [!DNL Adobe Experience Manager] 6.5 [!DNL Assets]の新機能と機能強化。'
exl-id: 6d9c9f09-ea42-43fb-98f7-12ce82d308bf
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '897'
ht-degree: 43%

---

# [!DNL Adobe Experience Manager Assets] リリースノート  {#aem-assets-release-notes}

[!DNL Adobe Experience Manager] 6.5 [!DNL Assets]リリースの主な機能と主な特徴を次に示します。

## [!DNL Adobe Creative Cloud]およびクリエイティブワークフロー{#integration-with-adobe-creative-cloud-and-creative-workflows}との統合

[!DNL Adobe Experience Manager] では、様々な方法で と連携し、クリエイティブチームとマーケティングチームが密接に共同作業するワークフローでアセットを共有できます。[!DNL Adobe Creative Cloud][!DNL Experience Manager] 6.5 では連携を引き続き改善し効率化して、より多くのチャンスを明らかにし、既存の手段の無駄も省きます。

コンテンツベロシティの使用例を最もサポートするために活用できる[!DNL Experience Manager] 6.5の具体的な機能と統合について説明します。

### Adobe Asset Link {#aal}

[!DNL Adobe Asset Link] は、コンテンツ作成プロセスにおけるクリエイティブとマーケターのコラボレーションを強化します。クリエイティブは、[!DNL Experience Manager Assets]に保存されたコンテンツに、最もなじみのあるアプリを残さずにアクセスできます。 クリエイティブは、[!DNL Adobe Photoshop]、[!DNL Adobe Illustrator]および[!DNL Adobe InDesign]アプリのアプリ内パネルを使用して、アセットをシームレスに参照、検索、チェックアウトおよびチェックインできます。

[!DNL Adobe Asset Link] は、エンタープライズ向け [Creative Cloudの](https://www.adobe.com/jp/creativecloud/business/enterprise.html) 一部です。[!DNL Experience Manager]デプロイメントの必要な設定など、詳細については、「[Adobeアセットリンク](https://helpx.adobe.com/jp/enterprise/using/adobe-asset-link.html)」を参照してください。

![Adobe Photoshopでのアセットの検索](assets/asset_search_photoshop.png)

### [!DNL Adobe Stock] 統合 {#stock}

[!DNL Adobe Stock]エンタープライズプランを[!DNL Experience Manager Assets]内で使用して、ライセンスが必要なアセットをクリエイティブプロジェクトやマーケティングプロジェクトで幅広く利用できるようにします。 [!DNL Experience Manager]の強力なDAM機能を使用して、Experience Managerに保存されている[!DNL Adobe Stock]アセットの検索、プレビュー、ライセンスの取得をすばやくおこなうことができます。

[!DNL Adobe Stock] サービスは、あらゆるクリエイティブプロジェクトに使用できる、適切にキュレーションされ、著作権使用料が不要で質の高い何百万点もの写真、ベクター、イラスト、ビデオ、テンプレートおよび 3D アセットを提供します。

詳しくは、[Experience ManagerアセットでのAdobe Stockアセットの使用](/help/assets/aem-assets-adobe-stock.md)を参照してください。

![Adobe Stockの画像とライセンスのExperience Manager](assets/stock_image_preview_license_options.png)

*図：内から [!DNL Adobe Stock] 画像とライセンスをプレビューしま [!DNL Experience Manager Assets]す。*

![Experience Managerでのライセンス済みAdobe Stock画像の検索とフィルタリング](assets/aem-search-filters2.jpg)

*図：で、ライセンス画像を検索してフィ [!DNL Adobe Stock] ルタリングし [!DNL Experience Manager]ます。*

### [!DNL Adobe InDesign] {#dynamic-references-in-indesign}の動的参照

[!DNL Experience Manager Assets] ファイルで [!DNL Adobe InDesign] は動的に使用されます。参照元のアセットがリポジトリ内に移動すると、参照が自動的に更新されます。 詳しくは、[複合アセットの管理方法](/help/assets/managing-linked-subassets.md)を参照してください。

## Brand Portal の機能 {#brand-portal-capabilities}

[!DNL Experience Manager Assets Brand Portal] では、承認済みアセットを容易に取得、効果的に制御し、それらのアセットを様々なデバイスをまたいで外部のベンダー／代理店、および内部のビジネスユーザーへと安全に配布できます。アセットの共有を効率化し、アセットの市場投入時間を短縮し、コンプライアンスに違反した使用や不正アクセスのリスクをなくすことができます。

詳細については、](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html?lang=ja#introduction)AEM Assets Brand Portal の新機能[を参照してください。

## Connected Assets {#connectedassets}

大規模企業では、Web サイトの作成に必要なインフラストラクチャを分散させることができます。しかし、Web サイトの作成機能と必要なデジタルアセットが、分断させた状態で別々の場所に存在する場合があります。

[!DNL Experience Manager Sites] は Web ページの作成機能を備え、 は Web サイトに必要なアセットを提供するデジタルアセット管理（DAM）システムです。[!DNL Experience Manager Assets][!DNL Experience Manager] では、[!DNL Sites] と [!DNL Assets] の統合により、上記の使用事例をサポートできるようになりました。[Connected Assets機能の設定方法と使用方法](/help/assets/use-assets-across-connected-assets-instances.md)を参照してください。

![別のデプロイメントのペ [!DNL Experience Manager] ージ上のデプロイメ [!DNL Sites] ントからのアセットの [!DNL Experience Manager] ドラッグ](assets/connected-assets-drag-and-drop-only.gif)

*図：別のデプロイメントのペ [!DNL Experience Manager] ージ上のデプロイメ [!DNL Sites] ントからアセットをドラッ [!DNL Experience Manager] グします。*

## Dynamic Media {#dynamic-media}

[!DNL Dynamic Media] では、リッチメディアのオーサリングと配信が強化され、没入感のあ [!DNL Experience Manager Assets] るパーソナライズされた最先端のエクスペリエンスを推進します。単一の高品質のマスターアセットをアップロードし、アドビの高度なクラウドレンダリングとビューアを使用することで、任意のレンディションの組み合わせをその場で配信して、組織のメディア戦略をサポートできます。

新しい[!DNL Dynamic Media]機能の詳細については、[Dynamic Mediaリリースノート](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/release-notes/s7rn2017.html)を参照してください。

### 360ビデオサポート{#video-support}

最先端のビューアを使用して、デスクトップ、モバイル、VRヘッドセットにVRエクスペリエンスを提供し、360ビデオファイルを[!DNL Experience Manager]で直接管理します。 詳しくは、[360 ビデオ の使用](/help/assets/360-video.md)を参照してください。

### カスタムビデオサムネール{#custom-video-thumbnails}

DAM に保存されているビデオそのものまたは他のコンテンツのフレームを使用して、ビデオアセットのサムネールをカスタマイズできるようになりました。詳しくは、[ビデオのサムネールについて](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-scene-mode)を参照してください。

### アクセシビリティの強化 {#accessibility-enhancements}

[!DNL Dynamic Media] ビューアで、Ariaサポート、スクリーンリーダー、代替テキストなどのアクセシビリティ機能が強化されました。詳細については、[Dynamic Media ビューアのリリースノート](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/home.html?lang=ja)を参照してください。

## 検索エクスペリエンスの強化  {#experience-enhancement-for-searching}

[!DNL Experience Manager] 6.5以降では、マーケターは検索結果ページから目的のアセットをすばやく見つけることができます。検索フィルターのアセット数は、検索フィルターを適用する前でも更新されます。フィルターに対するアセット数を確認すると、検索結果を効率的にナビゲートすることができます。詳しくは、「[Experience Manager](../assets/search-assets.md)でのアセットの検索」を参照してください。

![検索ファセットで検索結果をフィルタリングしない場合のアセット数の表示](/help/assets/assets/asset_search_results_in_facets_filters.png)

*図：検索ファセットで検索結果をフィルタリングしない場合のアセット数の確認*

## 使いやすさの向上 {#usability-enhancement}

フォルダー内または検索結果から読み込まれたすべてのアセットを一度に選択できるようになりました。 複数のアセットをすばやく管理するのに役立ちます。チェックボックスをオンにすると、[!DNL Experience Manager]インターフェイスに表示されるアセットだけでなく、シナリオに合うすべてのアセット（検索結果など）が選択されます。

![「すべて選択」オプションを使用して、読み込まれたすべてのアセットを1回のクリックで選択します。](assets/select-all-in-aem-assets.gif)

*図：「すべて選択」オプションを使用して、読み込まれたすべてのアセットを1回のクリックで選択します。*

## メタデータの機能強化 {#metadata-enhancements}

[!DNL Assets] では、フォルダープロパティページに表示されるレイアウトおよびメタデータを定義する、アセットフォルダーのメタデータスキーマを作成できます。既存のフォルダーまたは新規作成するフォルダーにフォルダーメタデータスキーマを割り当てることができるようになりました。詳しくは、](/help/assets/metadata-config.md#folder-metadata-schema)フォルダーメタデータスキーマ[を参照してください。

カスケードメタデータを指定すると、選択肢をフォームに手動で入力するのではなく、実行時に JSON ファイルから読み込むことができます。詳しくは、[カスケードメタデータ](/help/assets/metadata-schemas.md#cascading-metadata)を参照してください。

## レポート機能の強化 {#reporting-enhancements}

ダウンロードしたレポートに、コンテンツフラグメントとリンク共有が含まれるようになりました。 詳しくは、[AEM Assets レポート](/help/assets/asset-reports.md)を参照してください。
