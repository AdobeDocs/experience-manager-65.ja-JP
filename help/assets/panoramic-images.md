---
title: パノラマ画像
description: Dynamic Media でのパノラマ画像の使用方法を学習します。
uuid: ced3e5bd-93c8-4d5f-a397-1380d4d0a5e7
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: 632a9074-b747-49a1-a57d-1f42bba1f4e9
docset: aem65
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# Panoramic images{#panoramic-images}

ここでは、パノラマ画像ビューアを使用して球パノラマ画像をレンダリングし、室内、物件、場所、風景などをあらゆる角度から見ることができる臨場感あふれる体験を提供する方法について説明します。

[ビューアプリセットの管理](/help/assets/managing-viewer-presets.md)も参照してください。

![panoramic-image2](assets/panoramic-image2.png)

## パノラマ画像ビューアで使用するアセットのアップロード {#uploading-assets-for-use-with-the-panoramic-image-viewer}

アップロードするアセットが、パノラマ画像ビューアで使用する球パノラマ画像として適格となるには、アセットが以下の一方または両方の条件を満たしている必要があります。

* 縦横比が 2 である必要があります。CRXDE liteのデフォルトの縦横比設定である2は、次の場所で上書きできます。
   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

* Tagged with the keywords `equirectangular`, or `spherical`and `panorama`, or `spherical` and `panoramic`. [タグの使用](/help/sites-authoring/tags.md)を参照してください。

Both the aspect ratio and keyword criteria apply to panoramic assets for the asset details page and the `Panoramic Media` WCM component.

パノラマ画像ビューアで使用するアセットをアップロードするには、[アセットのアップロード](/help/assets/managing-assets-touch-ui.md#uploading-assets)を参照してください。

## Dynamic Media Classic（Scene7）の設定 {#configuring-dynamic-media-classic-scene}

パノラマ画像ビューアが AEM 内で正しく機能するには、パノラマ画像ビューアプリセットが JCR で更新されるように、ビューアプリセットを Dynamic Media Classic（Scene7）および Dynamic Media Classic（Scene7）固有のメタデータと同期する必要があります。そのためには、Dynamic Media Classic（Scene7）を次のように設定します。

1. 各会社アカウントの [Dynamic Media Classic（Scene7）のインスタンスにログイン](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html)します。

1. ページの右上隅付近で、**[!UICONTROL 設定／アプリケーション設定／公開設定／Image Server]** をクリックします。
1. Image Server 公開ページの上部にある「**[!UICONTROL 公開コンテキスト]**」ドロップダウンリストで、「**[!UICONTROL 画像サービング]**」を選択します。

1. 同じ Image Server 公開ページで、「**[!UICONTROL 要求属性]**」という見出しを探します。
1. 「要求属性」の見出しの下で、「**[!UICONTROL 返信画像のサイズ制限]**」を探します。次に、関連する「幅」と「高さ」フィールドで、パノラマ画像に使用できる最大画像サイズを大きくします。

   Dynamic Media Classic（Scene7）には、25,000,000 ピクセルという制限があります。縦横比が2:1の画像の最大許容サイズは7000 x 3500です。 ただし、通常のデスクトップ画面の場合、4096 x 2048 ピクセルで十分です。

   >[!NOTE]
   >
   >許容される最大画像サイズ以内の画像のみがサポートされます。サイズ制限を超える画像を要求すると、403 応答が生成されます。

1. 「要求属性」の見出しの下で、次の操作をおこないます。

   * 「要求難読化モード」を「**[!UICONTROL 無効]**」に設定します。
   * 「要求ロックモード」を「**[!UICONTROL 無効]**」に設定します。
   These settings are necessary for using the `Panoramic Media` WCM component in AEM.

1. Image Server 公開ページの下部で、左側にある「**[!UICONTROL 保存]**」をクリックします。

1. 右下隅にある「**[!UICONTROL 閉じる]**」をクリックします。

### パノラマメディア WCM コンポーネントのトラブルシューティング {#troubleshooting-the-panoramic-media-wcm-component}

WCM でパノラマメディアコンポーネントに画像をドロップしたときに、コンポーネントプレースホルダーが壊れた場合、以下のトラブルシューティングをおこなってください。

* 403 Forbidden エラーが発生する場合は、要求された画像のサイズが大きすぎることが原因となっている可能性があります。[Dynamic Media Classic（Scene7）の設定](/help/assets/panoramic-images.md#configuring%20dynamic%20media%20classic%20(scene7))でおこなった「**[!UICONTROL 返信画像のサイズ制限]**」の設定を確認します。

* アセットの「無効なロック」やページに表示される「解析エラー」については、「要求難読化モード」と「要求ロックモード」が無効になっていることを確認します。
* キャンバスが汚染されているというエラーについては、ルールセット定義ファイルのパスを設定し、画像アセットについて以前の要求の CDN を無効にします。
* サポートされている制限を超えるサイズの画像を要求した後に画質が大幅に低下した場合は、**[!UICONTROL JPEG エンコード属性／画質]**&#x200B;の設定が空でないことを確認します。A typical setting for the **[!UICONTROL Quality]** field is `95`. この設定は、Image Server 公開ページにあります。To access the page, see [Configuring Dynamic Media Classic (Scene7)](/help/assets/panoramic-images.md#configuring%20dynamic%20media%20classic%20(scene7)).

## パノラマ画像のプレビュー {#previewing-panoramic-images}

詳しくは、[アセットのプレビュー](/help/assets/previewing-assets.md)を参照してください。

## パノラマ画像の公開 {#publishing-panoramic-images}

[アセットの公開](/help/assets/publishing-dynamicmedia-assets.md)を参照してください。
