---
title: 3D アセットのプレビュー
description: Dynamic Media の 3D アセットのプレビュー方法について
contentOwner: Rick Brough
docset: aem65
feature: 3D アセット
role: Business Practitioner
exl-id: fdebbc2b-c04d-4cdd-b7c2-8e9a2a854e79
source-git-commit: 666bc5d943af371726708cb2ef157a9b3f07eb8e
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 61%

---

# Adobe Experience Manager{#previewing-3d-assets-aem}での3Dアセットのプレビュー

Adobe Experience Manager では、オーサリングプロセスの一環として、3D アセットのアップロード、配信、インタラクティブプレビューをサポートしています。

インタラクティブ3Dビューアは、Assetの詳細ページから使用できます。Experience Manager このビューアには、3D アセットをオービット、ズームおよびパンできるインタラクティブなカメラコントロールのコレクションが含まれます。

<!-- See also [Working with 3D assets in Dynamic Media](/help/assets/assets-3d.md). -->

## Experience Manager{#supported-3d-previewing-assets}の3Dプレビューでサポートされる形式

インタラクティブ 3D プレビューでは、次のファイル形式をサポートしています。

| 3D ファイル拡張子 | ファイル形式 | MIME タイプ | 備考 |
|---|---|---|---|
| GLB | バイナリ GL 伝送 | model/gltf-binary |  |
| GLTF | GL 伝送形式 | model/gltf+json | 下記の&#x200B;**備考**&#x200B;を参照。 |
| OBJ | WaveFront 3D オブジェクトファイル | application/x-tgif |  |
| STL | ステレオリソグラフィ | application/vnd.ms-pki.stl |  |
| DN | Adobe Dimension | model/x-adobe-dn | 取り込みのみサポート。プレビューは使用できません。 |
| USDZ | 汎用シーン記述 Zip アーカイブ | model/vnd.usdz+zip | 取り込みのみサポート。プレビューは使用できません。 |

>[!NOTE]
>
>gLTFモデルのプレビューでマテリアルがレンダリングされない場合は、次のように、マテリアルの名前が適切に、モデルと同じルートフォルダ内の`textures`フォルダに設定されていることを確認します。

    Asset（フォルダー）
    model.gltf
    model.bin
    textures（フォルダー）
    material_0_baseColor.jpeg
    material_0_normal.jpeg

## Experience Manager{#performance-3d-previewing-assets}で3Dアセットをプレビューする際のパフォーマンスに関する考慮事項

アセットの詳細表示ページで 3D アセットを開くときにかかる時間は、帯域幅、画像の複雑さ、サーバーの待ち時間など、いくつかの要因によって異なります。

さらに、カメラをインタラクティブに操作する際に、ワークステーション、ノートパソコン、モバイルタッチデバイスなどのクライアントコンピューターの性能を考慮することも重要です。グラフィック性能に優れ、ある程度パワフルなシステムなら、インタラクティブな 3D 表示をよりスムーズで満足なものにすることができます。

**3Dアセットをプレビューするには、Experience Manager:**

1. 3D アセットが Experience Manager にアップロードされていることを確認します。詳しくは、[3D プレビューでサポートされるファイル形式](#supported-3d-previewing-assets)と[アセットのアップロード](/help/assets/manage-assets.md#uploading-assets)を参照してください。
1. Experience Managerの&#x200B;**[!UICONTROL ナビゲーション]**&#x200B;ページで、**[!UICONTROL アセット/ファイルをタップします。]**

   ![ナビゲーションページ](/help/assets/assets-dm/navigation-assets.png)

1. ページの右上隅付近にある「表示」ドロップダウンリストで「**[!UICONTROL カード表示]**」をタップし、プレビューする 3D アセットに移動します。

   ![3D カードの選択](/help/assets/assets-dm/3d-card-select.png)
   _カード表示で、プレビューする 3D アセットのカードをタップ_

1. 3Dアセットのカードをタップします。

   ![インタラクティブ 3D プレビュー](/help/assets/assets-dm/3d-preview.png)
   _アセット詳細表示ページでの 3D アセットのインタラクティブプレビュー_
1. 3D アセットのアセット詳細表示ページで、次のいずれかの操作をおこないます。

   | 表示 | 説明 | マウス操作 | タッチスクリーンアクション |
   | --- | --- | --- | --- |
   | **カメラを回す** | 3D シーンとオブジェクトの周囲でビューを周回させます。 | 左クリックしながらドラッグします。 | 1本指で押しながらドラッグします。 |
   | **カメラをパン** | ビューを左右上下にパンします。 | 右クリックしながらドラッグします。 | 2本指で押しながらドラッグします。 |
   | **カメラをズーム** | 3Dシーンの領域の内外を移動します。 | ホイールをスクロールします。 | 2本指でピンチ。 |
   | **カメラ視野の中心を変更** | 3Dシーン内のオブジェクト上の1点をカメラの中心に戻します。 | ダブルクリック. | ダブルタップ. |
   | **リセット** | ページの右下隅付近にあるリセットアイコンをタップして、視野のターゲットポイントを3Dアセットの中心に戻します。 リセットを使用しても、アセット全体を表示したり、適切な表示サイズで表示するために、カメラを近づけたり遠ざけたりできます。 |  |  |
   | **全画面表示モード** | 全画面表示モードに入るには、ページの右下隅にある全画面表示アイコンをタップします。 |  |  |

1. 作業が完了したら、ページの右上隅付近にある「**[!UICONTROL 閉じる」をタップします。]**
