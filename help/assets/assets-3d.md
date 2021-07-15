---
title: Dynamic Media での 3D アセットの操作
seo-title: Dynamic Media での 3D アセットの操作
description: Dynamic Media で 3D アセットを使用する方法について説明します。
seo-description: Dynamic Media で 3D アセットを使用する方法について説明します。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: introduction
content-type: reference
feature: 3Dアセット，アセット管理
role: User, Admin
exl-id: 01c96f1e-c0e6-497d-bd7a-c0fd547a34da
source-git-commit: 471f9e99078a1e0af60024d439afd42ae77cba8c
workflow-type: tm+mt
source-wordcount: '2330'
ht-degree: 62%

---

# Dynamic Mediaでの3Dアセットの操作 {#working-with-three-d-assets-dm}

Dynamic Media を使用すると、3D アセットを、没入感のあるエクスペリエンスとしてアップロード、管理、表示および配信できます。

* 3D アセットをワンクリックで公開（ツールバーの&#x200B;**[!UICONTROL クイック公開]**&#x200B;を使用）して URL を生成。
* Adobe Dimension を使用した、高品質でインタラクティブなディメンショナルビューアプリセットで、3D アセットの表示のサポートを最適化。
* 3D メディア WCM コンポーネントによって、Adobe Experience Manager Sites ページに 3D アセットを簡単に追加可能。

Dynamic Mediaで3Dアセットを使用するために追加の設定は必要ありません。

![3D の靴](/help/assets/assets-dm/3d-dimensional-viewer-quickpublish-url-embed2.png)

<!-- See also [Dynamic Media 3D Release Notes](/help/release-notes/aem3d-release-notes.md). -->

## Dynamic Media でサポートされる 3D 形式 {#supported-three-d-file-formats-in-dm}

Dynamic Mediaは、次の3D形式をサポートしています。

[サポートされる3D形式](/help/assets/assets-formats.md)も参照してください。

| 3D ファイル拡張子 | ファイル形式 | MIME タイプ | 備考 |
|---|---|---|---|
| GLB | バイナリ GL 伝送 | model/gltf-binary | マテリアルとテクスチャを単一のアセットとして含めます。 |
| OBJ | WaveFront 3D オブジェクトファイル | application/x-tgif |  |
| STL | ステレオリソグラフィ | application/vnd.ms-pki.stl |  |
| USDZ | 汎用シーン記述 Zip アーカイブ | model/vnd.usdz+zip | *取り込みのみサポート。表示やインタラクションは利用不可。* USDZは独自の3D形式で、SafariやiOSデバイスでネイティブに表示できます。 |

## クイックスタート：Dynamic Media 内の 3D アセット {#quick-start-three-d}

次のワークフローの手順説明は、Dynamic Media - Scene7モードで3Dアセットをすばやく使い始めるのに役立つように設計されています。

>[!IMPORTANT]
>
>3Dアセットは、Dynamic Media — ハイブリッドモードではサポートされていません。

Dynamic Mediaで3DCloud Servicesを操作する前に、Experience Manager管理者がDynamic Media - Scene7モードでDynamic Mediaアセットを有効にし、設定済みであることを確認してください。

Dynamic Media - Scene7Cloud Servicesの設定の「[Dynamic Mediaモードの設定](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services)」および「[Dynamic Media - Scene7モードのトラブルシューティング](/help/assets/troubleshoot-dms7.md)」を参照してください。

1. **3D アセットのアップロード**

   * [Dynamic Mediaで使用する3Dアセットをアップロードします](/help/assets/manage-assets.md#uploading-assets)。
   * [Dynamic Media のアップロードでサポートされる 3D ファイル形式](#supported-three-d-file-formats-in-dm).

1. **3D アセットの管理**

   * 3D アセットの整理と検索

      * [デジタルアセットの整理](/help/assets/organize-assets.md#organize-digital-assets).
      * [3Dアセットの検索](/help/assets/search-assets.md)を参照してください。
      * [カスタム述語を使用して検索結果を絞り込む](/help/assets/search-assets.md#custompredicates)。
   * 3D アセットの表示

      * [3Dアセットの表示とインタラクション](#viewing-three-d-assets)を参照してください。
      * [ディメンショナルビューアプリセットを管理します](/help/assets/managing-viewer-presets.md)。
   * 3D アセットメタデータの操作

      * [デジタルアセットのメタデータの管理](/help/assets/metadata.md).
      * [メタデータスキーマ](/help/assets/metadata-schemas.md).



1. **3D アセットの公開**

   * [静的Dynamic Media 3Dアセットの公開](#publishing-three-d-assets)
   * [ディメンショナルビューアを使用した、Dynamic Media 3D アセットの代替の公開方法](#alternate-publish-methods)

## 3D アセットの表示とインタラクションについて {#viewing-three-d-assets}

この節では、3D アセットの表示およびインタラクション方法を、アセットの詳細ページ内から、または Sites の 3D メディアコンポーネント内からの 2 通り説明します。

このインタラクティブ 3D ビューアには、3D アセットをオービット、ズームおよびパンできる、インタラクティブなカメラコントロールのコレクションが含まれます。

アセットの詳細ページビューで 3D アセットを開くのにかかる時間は、いくつかの要因に依存します。要因には以下のものが含まれます。

* サーバーの帯域幅
* サーバーの待ち時間
* 画像の複雑さ

さらに、カメラをインタラクティブに操作する際に、ワークステーション、ノートパソコン、モバイルタッチデバイスなどのクライアントコンピューターの性能を考慮することも重要です。グラフィック性能に優れ、ある程度パワフルなシステムなら、インタラクティブな 3D 表示をよりスムーズで満足なものにすることができます。

>[!TIP]
>
>ディメンショナルビューアプリセットをビューアプリセットエディターで開いて、3D ファイルをアップロードせずに 3D アセット内を移動する練習ができます。ディメンショナルビューアプリセットには、操作できる組み込みの 3D アセットがあります。
>
>[ビューアプリセットの管理](/help/assets/managing-viewer-presets.md)を参照してください。

## アセットの詳細ページからの3Dアセットの表示とインタラクション {#viewing-three-d-assets-from-asset-details-page}

[ソフトウェアインターフェイスを使用したアセットのプレビュー](/help/assets/previewing-assets.md)も参照してください。

**アセットの詳細ページから 3D アセットの表示とインタラクションを行うには：**

1. 3D アセットが Experience Manager にアップロードされていることを確認します。

   [Dynamic Media](/help/assets/manage-assets.md#uploading-assets)で使用する3Dアセットのアップロードを参照してください。

1. Experience Managerの&#x200B;**[!UICONTROL ナビゲーション]**&#x200B;ページで、**[!UICONTROL アセット]**/**[!UICONTROL ファイル]**&#x200B;に移動します。
1. ページの右上隅付近にある「**[!UICONTROL 表示]**」ドロップダウンリストから「**[!UICONTROL カード表示]**」を選択します。
1. 表示する 3D アセットに移動します。
1. 3Dアセットのカードを選択します。
1. 3D アセットの詳細表示ページで、次のいずれかの操作をおこないます。

   | 表示 | 説明 | マウス操作 | タッチスクリーン操作 |
   | --- | --- | --- | --- |
   | **カメラを回転** | 3D シーンとオブジェクトの周囲でビューを周回させます。 | 左クリックしながらドラッグします。 | 1 本指で押しながらドラッグします。 |
   | **カメラをパン** | ビューを左、右、上、下にパンします。 | 右クリックしながらドラッグします。 | 2 本指で押しながらドラッグします。 |
   | **カメラをズーム** | 3D シーンの領域の内外に移動します。 | ホイールをスクロールします。 | 2 本指でピンチします。 |
   | **カメラを中心に戻す** | カメラを中心の位置に戻し、3D シーンのオブジェクトに合わせます。 | ダブルクリック. | ダブルタップ. |
   | **リセット** | ページの右下隅付近にあるリセットアイコンを選択して、視野のターゲットポイントを3Dアセットの中心に戻します。 リセットを使用しても、アセット全体を表示したり、適切な表示サイズで表示するために、カメラを近づけたり遠ざけたりできます。 |  |  |
   | **全画面表示モード** | 全画面表示モードに入るには、ページの右下隅にある全画面表示アイコンを選択します。 |  |  |

1. ページの右上隅にある「**[!UICONTROL 閉じる]**」を選択して、アセットページに戻ります。

## 3D メディアコンポーネント内の 3D アセットの表示とインタラクション {#interacting-with-asset-inside-three-d-media-component}

Web ページが&#x200B;**[!UICONTROL 編集]**&#x200B;モードの場合、3D アセットとのインタラクションは行えません。アセットをインタラクティブにするには、**[!UICONTROL プレビュー]**&#x200B;機能を使用して、3D メディアコンポーネントの機能にフルアクセスできるページエディターで Web ページを表示します。

>[!IMPORTANT]
>
>このタスクは、3D メディアコンポーネントを Web ページに追加し、3D アセットをコンポーネントに割り当てた後にのみ実行できます。詳しくは、[Web ページへの 3D メディアコンポーネントの追加](#adding-the-three-d-media-component-to-a-web-page)および [3D メディアコンポーネントへの 3D アセットの割り当て](#assigning-a-three-d-asset-to-the-component)を参照してください。

[ソフトウェアインターフェイスを使用したアセットのプレビュー](/help/assets/previewing-assets.md)も参照してください。

**3D メディアコンポーネント内の 3D アセットの表示とインタラクションを行うには：**

1. Web ページが&#x200B;**[!UICONTROL 編集]**&#x200B;モードの間に、次のいずれかの操作を行います。

   * ページの右上付近にある「**[!UICONTROL プレビュー]**」を選択して、「**[!UICONTROL プレビュー]**」モードに入ります。
   * ブラウザーのページ URL から `/editor.html` を削除します。

プレビューモードで表示された完全にインタラクティブな 3D アセット    ![3D メディアコンポーネント内に表示される 3D アセット](/help/assets/assets-dm/3d-asset-in-3d-media.png)
**[!UICONTROL プレビュー]**&#x200B;モードで表示された完全にインタラクティブな 3D アセット。

1. **[!UICONTROL プレビュー]**&#x200B;モードの間に、次のいずれかの操作を行います。

   | 表示 | 説明 | マウス操作 | タッチスクリーン操作 |
   | --- | --- | --- | --- |
   | **カメラを回転** | 3D シーンとオブジェクトの周囲でビューを周回させます。 | 左クリックしながらドラッグします。 | 1 本指で押しながらドラッグします。 |
   | **カメラをパン** | ビューを左、右、上、下にパンします。 | 右クリックしながらドラッグします。 | 2 本指で押しながらドラッグします。 |
   | **カメラをズーム** | 3D シーンの領域の内外に移動します。 | ホイールをスクロールします。 | 2 本指でピンチします。 |
   | **カメラを中心に戻す** | カメラを中心の位置に戻し、3D シーンのオブジェクトに合わせます。 | ダブルクリック. | ダブルタップ. |
   | **リセット** | ページの右下隅付近にあるリセットアイコンを選択して、視野のターゲットポイントを3Dアセットの中心に戻します。 リセットを使用しても、アセット全体を表示したり、適切な表示サイズで表示するために、カメラを近づけたり遠ざけたりできます。 |  |  |
   | **全画面表示モード** | 全画面表示モードに入るには、ページの右下隅にある全画面表示アイコンを選択します。 |  |  |

## 3D メディアコンポーネントの操作について {#working-with-three-d-media-component}

Dynamic Mediaには、Dynamic Media 3Dメディアコンポーネントが含まれており、Adobe Experience Manager Sitesで使用して、Webページ上で3Dモデルをインタラクティブに表示できます。

* [ページテンプレートへの3Dメディアコンポーネントの追加](#adding-three-d-media-component-to-page-template)
* [Webページへの3Dメディアコンポーネントの追加](#adding-the-three-d-media-component-to-a-web-page)
   * [オプション - 3D メディアコンポーネントの設定](#configuring-the-three-d-component)
* [3Dメディアコンポーネントに3Dアセットを割り当てる](#assigning-a-three-d-asset-to-the-component)

## ページテンプレートへの3Dメディアコンポーネントの追加 {#adding-three-d-media-component-to-page-template}

1. **[!UICONTROL ツール]**／**[!UICONTROL 一般]**／**[!UICONTROL テンプレート]**&#x200B;に移動します。
1. 3D コンポーネントを有効にするページテンプレートに移動し、テンプレートを選択します。
1. 「**[!UICONTROL 編集]**」を選択して、テンプレートを開きます。
1. ページの右上付近にあるドロップダウンメニューで、「**[!UICONTROL 構造]**」モードを選択します（まだアクティブでない場合）。

   ![3d-media-component-structure](/help/assets/assets-dm/3d-media-component-structure.png)

1. **[!UICONTROL レイアウトコンテナ]**&#x200B;領域の空の領域を選択して、関連するツールバーを開きます。
1. ツールバーで、**[!UICONTROL ポリシー]**&#x200B;アイコンを選択し、**[!UICONTROL ポリシーエディター]**&#x200B;を開きます。
1. 「**[!UICONTROL プロパティ]**」セクションの「**[!UICONTROL 許可されたコンポーネント]**」タブで、「**[!UICONTROL Dynamic Media]**」までスクロールし、リストを展開して、「**[!UICONTROL 3D メディア]**」をチェックします。
1. 「**[!UICONTROL 完了]**」を選択して変更を保存し、**[!UICONTROL ポリシーエディター]**&#x200B;を閉じます。

   これで、この Dynamic Media を使用するすべてのページに 3D メディアコンポーネントを配置できます。

## Webページへの3Dメディアコンポーネントの追加 {#adding-the-three-d-media-component-to-a-web-page}

Webコンテンツ管理システムとしてExperience Managerを使用する場合は、3Dメディアコンポーネントを使用してWebページに3Dアセットを追加できます。

[ページへのDynamic Mediaアセットの追加](/help/assets/adding-dynamic-media-assets-to-pages.md)も参照してください。

**Webページに3Dメディアコンポーネントを追加するには：**

1. Experience Manager Sites を開き、Dynamic Media 3D メディアコンポーネントを追加する Web ページを選択します。
1. **[!UICONTROL 編集]**（鉛筆）アイコンを選択して、ページをページエディターで開くことができます。 ページの右上付近で&#x200B;**[!UICONTROL 編集]**&#x200B;モードが選択されていることを確認します。

   ![3d-media-component-add](/help/assets/assets-dm/3d-media-component-edit.png)

1. ツールバーのサイドパネルアイコンを選択して、パネルの表示を切り替えるか、「オン」にします。

1. サイドパネルで、プラス記号アイコンを選択して、**[!UICONTROL コンポーネント]**&#x200B;リストを開きます。

   ![3d-media-component-drag-drop](/help/assets/assets-dm/3d-assets-filter.png)

1. **[!UICONTROL コンポーネント]**&#x200B;リストから、**[!UICONTROL 3D メディア]**&#x200B;コンポーネントを、3D ビューアを表示するページ上の場所にドラッグします。

これで、3D アセットをコンポーネントに割り当てる準備が整いました。

[3Dメディアコンポーネントへの3Dアセットの割り当て](#assigning-a-three-d-asset-to-the-component)を参照してください。

### オプション — 3Dメディアコンポーネントの設定 {#configuring-the-three-d-component}

1. Experience Manager Sites のページエディターで、前にページに追加した **[!UICONTROL 3D メディアビューア]**&#x200B;コンポーネントを選択します。
1. **[!UICONTROL 設定]**&#x200B;アイコン（レンチ）を選択して、コンポーネント設定ダイアログボックスを開きます。

   ![3d-media-component-config](/help/assets/assets-dm/3d-media-component-config.png)

1. 3D メディアダイアログボックスの「ビューアプリセット」ドロップダウンリストで、「**[!UICONTROL ディメンション]**」を選択して、ディメンショナルビューアプリセットをコンポーネントに割り当てます。

   ![3d-media-component-edit-config](/help/assets/assets-dm/3d-media-component-edit-config.png)

1. 右上隅のチェックマークを選択して、変更を保存します。

## 3Dメディアコンポーネントに3Dアセットを割り当てる {#assigning-a-three-d-asset-to-the-component}

Web ページに 3D メディアコンポーネントを追加した後、3D アセットを割り当てることができます。

[Webページへの3Dメディアコンポーネントの追加](#adding-the-three-d-media-component-to-a-web-page)を参照してください。

**3Dアセットを3Dメディアコンポーネントに割り当てるには：**

1. Experience Managerサイトページエディターで、**[!UICONTROL アセット]**&#x200B;アイコンを選択し、サイドパネルで&#x200B;**[!UICONTROL アセット]**&#x200B;を開きます。
1. ドロップダウンリストで、「**[!UICONTROL 3D]**」を選択して 3D アセットファイルタイプのみを表示します。
1. サイドパネルで、編集中のページに表示する 3D アセットを検索するか、スクロールして見つけます。
1. 3D アセットを Assets サイドパネルからドラッグし、前にページに追加した **[!UICONTROL 3D メディア]**&#x200B;コンポーネントにドロップします。

   ![3Dメディアコンポーネントに3Dアセットを割り当てる](/help/assets/assets-dm/3d-asset-add.png)

>[!NOTE]
>
>Web ページが Experience Manager Sites **[!UICONTROL 編集]**&#x200B;モードの場合、3D メディアコンポーネントは 3D アセットを表示しますが、アセットとのインタラクションはできません。アセットをインタラクティブにするには、**[!UICONTROL プレビュー]**&#x200B;機能を使用して、3D メディアコンポーネントの機能にフルアクセスできるページエディターで Web ページを表示します。

## 静的Dynamic Media 3Dアセットの公開 {#publishing-three-d-assets}

Dynamic Media では、Dynamic Media で&#x200B;*静的コンテンツ*&#x200B;としてサポートされる様々な 3D ファイル形式を使用できます。静的コンテンツとは、3Dアセットをアップロードして公開できるが、3Dアセットに関連付けられた&#x200B;*変数の画像*&#x200B;や画像の再編集はサポートされないことを意味します。 これは、Dynamic Media Imaging サーバーが 3D 形式を認識しないためです。したがって、Dynamic Media で 3D アセットを公開すると、インスタント URL をコピーできます。3D アセットの URL は、通常の Dynamic Media の URL 構造に従います。ただし、Dynamic Media 内の従来の画像アセットとは異なり、アセットの URL 内のパラメーターは編集できません。

[静的アセットのURLの取得](/help/assets/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-a-static-asset)も参照してください。

**[!UICONTROL カード表示]**&#x200B;で、アセット名のすぐ下、アセットが発行されたことを示す日時の左側に、小さな地球アイコンが表示されます。**[!UICONTROL リスト表示]**&#x200B;では、公開されたアセットと公開されていないアセットが「**[!UICONTROL 公開]**」列でわかります。

WCMとしてExperience Managerを使用する場合は、この公開方法を使用して、Dynamic Media 3DアセットをWebページに直接追加します。

[Dynamic Mediaアセットの公開](publishing-dynamicmedia-assets.md)も参照してください。

[ページの公開](/help/sites-authoring/publishing-pages.md)も参照してください。

**静的 Dynamic Media 3D アセットを公開するには：**

1. 3Dアセット（GLB、OBJ、またはSTLファイル形式）を開き、アセットの詳細ページで表示できるようにします。
1. ツールバーで、「**[!UICONTROL クイック公開]**」を選択します。

   ![3d-asset-quick-publish](/help/assets/assets-dm/3d-asset-quick-publish.png)

1. 「**[!UICONTROL 閉じる]**」を選択してダイアログボックスを閉じ、アセットの詳細ページに戻ります。
1. 3Dアセットのファイル名の左にあるドロップダウンリストから、「**[!UICONTROL レンディション]**」を選択します。

   ![3d-asset-renditions](/help/assets/assets-dm/3d-asset-renditions.png)

1. **[!UICONTROL 元の]**&#x200B;を選択します。 3D アセットが公開（「アクティブ化」）されると、次の 3D アセットの条件がすべて満たされた場合、「**[!UICONTROL URL]**」ボタンがページの左下隅近くに表示されます。
   * 3D アセットがサポートされている形式（GLB、OBJ、STL、USDZ）。
   * 3D アセットが Dynamic Media 画像制作システム（IPS）に取り込まれている。
   * 3D アセットが公開されている。

   ![3d-asset-url](/help/assets/assets-dm/3d-asset-url.png)

1. **[!UICONTROL URL]**&#x200B;を選択して、Webページにコピーして使用できる3Dアセットの直接実稼動URLを表示できます。

### ディメンショナルビューアを使用した、Dynamic Media 3D アセットの代替の公開方法 {#alternate-publish-methods}

Dynamic Media 3Dアセットを公開する際に、WCMとしてExperience Managerを使用&#x200B;*しない*&#x200B;場合は、次の2つの方法を使用します。

* **[!UICONTROL URL]** - サードパーティの Web コンテンツ管理システムを使用していて、ディメンショナルビューアを使用して Dynamic Media 3D アセットを Web ページにリンクする場合は、「**[!UICONTROL URL]**」を使用します。

   [WebアプリケーションへのURLのリンク](/help/assets/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset)を参照してください。

* **[!UICONTROL 埋め込み]** - Web ページに埋め込まれた Dynamic Media 3D アセットをディメンショナルビューアで表示する場合は、「**[!UICONTROL 埋め込み]**」を使用します。埋め込みコードをクリップボードにコピーして、Web ページに貼り付けることができます。**[!UICONTROL 埋め込み]**&#x200B;ダイアログボックスでは、コードの編集はできません。

   [WebページにDynamic Mediaビデオ、画像ビューア、またはディメンショナルビューアを埋め込む](/help/assets/embed-code.md#embedding-the-video-or-image-viewer-on-a-web-page)を参照してください。
