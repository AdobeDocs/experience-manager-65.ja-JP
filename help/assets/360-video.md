---
title: 360/VR ビデオ
description: Dynamic Media で 360 および VR（Virtual Reality）ビデオを操作する方法を学びます。
uuid: c21bf2c0-7acc-401f-857e-0186de86e7a1
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: aac3c850-ae84-4bff-80de-d370e150f675
docset: aem65
feature: 360 VR ビデオ
role: User, Admin
exl-id: 0c2077a7-bd16-484b-980f-4d4a1a681491
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '1054'
ht-degree: 78%

---

# 360/VR ビデオ {#vr-video}

360 度ビデオでは、すべての方向のビューが同時に記録されます。このタイプのビデオは、全方位カメラやカメラのコレクションを使用して撮影されます。フラットディスプレイでの再生中、ユーザは視野角を制御する。モバイルデバイスでの再生は、通常、組み込みのジャイロスコープ制御を使用します。

Dynamic Media - Scene7 モードには、360 ビデオアセット配信のネイティブサポートが含まれています。デフォルトでは、表示または再生するための追加設定は不要です。360 ビデオは、.mp4、.mkv、.mov といった標準のビデオ拡張子を使用して配信されます。最も一般的なコーデックは H.264 です。

この節では、360/VR ビデオビューアを操作して、部屋、物件、場所、風景、医療処置などの没入感のある視聴体験のために、エクイレクタングラー形式のビデオをレンダリングする方法について説明します。

空間オーディオは現在サポートされていません。オーディオをステレオにミックスした場合、お客様がカメラの表示角度を変更してもバランス（L/R）は変化しません。

[ビューアプリセットの管理](/help/assets/managing-viewer-presets.md)も参照してください。

## 360 ビデオの視聴 {#video-in-action}

「[Space Station 360](https://mobiletest.scene7.com/s7viewers/html5/Video360Viewer.html?asset=Viewers/space_station_360-AVS)」をタップして、ブラウザーウィンドウを開き、360 度ビデオを視聴します。ビデオ再生中にマウスポインターを新しい位置にドラッグすると、表示角度が変更されます。

![360 ビデオのサンプル](assets/6_5_360videoiss_simplified.png)
*Space Station 360（国際宇宙ステーションの 360 度ビデオ）のビデオフレーム*

## 360/VR ビデオと Adobe Premiere Pro {#vr-video-and-adobe-premiere-pro}

Adobe Premier Pro を使用すれば、360/VR シーンを表示および編集できます。例えば、シーン内にロゴやテキストを適切に配置したり、エクイレクタングラー形式のメディアに特化して設計されたエフェクトやトランジションを適用したりできます。

[360/VR ビデオの編集](https://helpx.adobe.com/jp/premiere-pro/how-to/edit-360-vr-video.html)を参照してください。

## 360 ビデオビューアで使用するアセットのアップロード {#uploading-assets-for-use-with-the-video-viewer}

Adobe Experience Managerにアップロードされた360ビデオアセットには、通常のビデオアセットと同様に、アセットページで「**マルチメディア**」というラベルが付けられます。

![6_5_360video-selecttopreview](assets/6_5_360video-selecttopreview.png)
*アップロードされた 360 ビデオアセット（カード表示）。アセットには「マルチメディア」というラベルが付けられます。*

**360ビデオビューアで使用するアセットをアップロードします。**

1. 360 ビデオアセット専用のフォルダーを作成します。
1. [フォルダーにアダプティブビデオプロファイルを適用します](/help/assets/video-profiles.md#applying-a-video-profile-to-folders)。

   360 ビデオコンテンツをレンダリングする場合、ソースビデオの解像度とレンディションのエンコード解像度に関する要件が、標準の非 360 ビデオコンテンツの場合よりも高くなります。

   Dynamic Media に付属している、既製のアダプティブビデオプロファイルを使用してもかまいません。ただしその場合、同じ設定でエンコードされた非 360 ビデオを非 360 ビデオビューアでレンダリングする場合と比べ、360 ビデオの品質のほうが低く感じられます。したがって、高品質の 360 ビデオが必要な場合は、以下の操作を行ってください。

   * 理想的には、元の360ビデオコンテンツは、次のいずれかの解像度に最適です。

      * 1080p - 1920 x 1080：フル HD または FHD 解像度と呼ばれます。
      * 2160p - 3840 x 2160(4k、UHD、またはUltraのHD解像度と呼ばれます)。 この大きなディスプレイ解像度は、ハイエンドのテレビやコンピューターモニターでよく見られます。2160pの解像度は、幅が4,000ピクセルに近いので、「4k」と呼ばれることが多いです。 つまり、そのピクセル数は 1080p の 4 倍になります。
   * より高品質のレンディションを含む[カスタムアダプティブビデオプロファイルを作成](/help/assets/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming)します。例えば、次の3つの設定を含むアダプティブビデオプロファイルを作成します。

      * width=auto; height=720; bitrate=2500 kbps
      * width=auto; height=1080; bitrate=5000 kbps
      * width=auto; height=1440; bitrate=6600 kbps
   * 360 ビデオアセット専用のフォルダー内の 360 ビデオコンテンツを処理します。

   このアプローチを使用する場合は、エンドユーザーのネットワークや CPU の要件も高くなります。

1. [フォルダーにビデオをアップロードします](/help/assets/managing-video-assets.md#upload-and-preview-video-assets)。

## 360 ビデオのデフォルト縦横比のオーバーライド  {#overriding-the-default-aspect-ratio-of-videos}

アップロードしたアセットを、360 ビデオビューアで使用する 360 ビデオにするには、アセットの縦横比が 2 である必要があります。

デフォルトでは、Experience Managerはビデオの縦横比（幅/高さ）が2.0の場合、「360」としてビデオを検出します。管理者は、次のCRXDE Liteでオプションの`s7video360AR`プロパティを設定して、デフォルトの縦横比の設定(2)を上書きできます。

* `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

   * **プロパティタイプ**  — 倍精度浮動小数点数
   * **値**  — 縦横比（デフォルトは2.0）。

このプロパティの設定が完了すると、既存のビデオと新しくアップロードされたビデオの両方で、すぐに設定が有効になります。

この縦横比は、アセットの詳細ページや[ビデオ 360 メディア WCM コンポーネント](/help/assets/adding-dynamic-media-assets-to-pages.md#dynamic-media-components)向けの 360 ビデオアセットに適用されます。

まず、360 ビデオをアップロードします。

## 360 ビデオのプレビュー {#previewing-video}

プレビューを使用すれば、360 ビデオがお客様にどのように表示されるかを確認し、ビデオが期待どおりに動作していることを確認できます。

[ビューアプリセットの編集](/help/assets/managing-viewer-presets.md#editing-viewer-presets)も参照してください。

360 ビデオの設定が完了したら、このビデオを公開できます。

[Web ページへのビデオビューアまたは画像ビューアの埋め込み](/help/assets/embed-code.md)を参照してください。[Web アプリケーションへの URL のリンク](/help/assets/linking-urls-to-yourwebapplication.md)を参照してください。インタラクティブコンテンツに相対 URL のリンク（特に Experience Manager Sites ページへのリンク）がある場合、URL ベースのリンク方法は使用できません。[ページへの Dynamic Media アセットの追加](/help/assets/adding-dynamic-media-assets-to-pages.md)を参照してください。

**360 ビデオをプレビューするには:**

1. **[!UICONTROL Assets]** で、作成した既存の 360 ビデオに移動します。360ビデオアセットをタップして、プレビューモードで開くことができます。

   ![6_5_360video-selecttopreview-1](assets/6_5_360video-selecttopreview-1.png)

   360ビデオアセットをタップして、ビデオをプレビューします。

1. プレビューページで、ページの左上隅付近にあるドロップダウンリストをタップし、「**[!UICONTROL ビューア]**」を選択します。

   ![6_5_360video-preview-viewers](assets/6_5_360video-preview-viewers.png)

   「ビューア」リストから **[!UICONTROL Video360_social]** をタップした後、次のいずれかの操作を行います。

   * 静的なシーンの表示角度を変更する場合は、ビデオ上でマウスポインタをドラッグします。
   * 再生を開始する場合は、ビデオの&#x200B;**[!UICONTROL 再生]**&#x200B;ボタンをタップします。 ビデオが再生される際に、ビデオ上でマウスポインターをドラッグして、表示角度を変更します。

   ![6_5_360video-preview-video360-social ](assets/6_5_360video-preview-video360-social.png)*360 ビデオのスクリーンショット*

   * 「ビューア」リストから **[!UICONTROL Video360VR]** をタップします。

      バーチャルリアリティ（VR）ビデオは、バーチャルリアリティヘッドセットで視聴する、没入感のあるビデオコンテンツです。通常のビデオと同様に、360 度ビデオカメラを使用してビデオを録画またはキャプチャする際、最初に VR ビデオを作成します。
   ![6_5_360video-preview-video360vr](assets/6_5_360video-preview-video360vr.png)
   *360 VR ビデオのスクリーンショット。*

1. プレビューページの右上隅付近にある「**[!UICONTROL 閉じる]**」をタップします。

## 360 ビデオの公開 {#publishing-video}

360ビデオを公開して使用できるようにします。 360 ビデオを公開すると、URL と埋め込みコードがアクティベートされます。また、スケーラブルで効率の良い配信のために CDN と統合された Dynamic Media クラウドにも、360 ビデオが公開されます。

360 ビデオの公開方法について詳しくは、[Dynamic Media アセットの公開](/help/assets/publishing-dynamicmedia-assets.md)を参照してください。[Web ページへのビデオビューアまたは画像ビューアの埋め込み](/help/assets/embed-code.md)も参照してください。[Web アプリケーションへの URL のリンク](/help/assets/linking-urls-to-yourwebapplication.md)も参照してください。インタラクティブコンテンツに相対 URL のリンク（特に Experience Manager Sites ページへのリンク）がある場合、URL ベースのリンク方法は使用できません。[ページへの Dynamic Media アセットの追加](/help/assets/adding-dynamic-media-assets-to-pages.md)も参照してください。
