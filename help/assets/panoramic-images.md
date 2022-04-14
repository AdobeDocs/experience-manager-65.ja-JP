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
feature: Panoramic Images,Asset Management
role: User, Admin
exl-id: 4d6fbeb1-94db-4154-9e41-b76033fb4398
source-git-commit: 363e5159d290ecfbf4338f6b9793e11b613389a5
workflow-type: ht
source-wordcount: '574'
ht-degree: 100%

---

# パノラマ画像 {#panoramic-images}

ここでは、パノラマ画像ビューアを使用して球パノラマ画像をレンダリングし、室内、物件、場所、風景などをあらゆる角度から見ることができる臨場感あふれる体験を提供する方法について説明します。

[ビューアプリセットの管理](/help/assets/managing-viewer-presets.md)も参照してください。

![panoramic-image2](assets/panoramic-image2.png)

## パノラマ画像ビューアで使用するアセットのアップロード {#uploading-assets-for-use-with-the-panoramic-image-viewer}

アップロードするアセットが、パノラマ画像ビューアで使用する球体パノラマ画像として認められるためには、アセットが次のいずれかまたは両方を満たしている必要があります。

* 縦横比が 2 である。
CRXDE Lite では縦横比のデフォルト設定は 2 ですが、次で上書きできます。
   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

* キーワード `equirectangular`、または `spherical` と `panorama`、または `spherical` と `panoramic` でタグ付けされている必要があります。[タグの使用](/help/sites-authoring/tags.md)を参照してください。

縦横比とキーワードの両方の条件が、アセットの詳細ページと `Panoramic Media` WCM コンポーネントのパノラマアセットに適用されます。

パノラマ画像ビューアで使用するアセットをアップロードするには、[アセットのアップロード](/help/assets/manage-assets.md#uploading-assets)を参照してください。

## Dynamic Media Classic を設定する {#configuring-dynamic-media-classic-scene}

パノラマ画像ビューアが Adobe Experience Manager で正しく機能するには、パノラマ画像ビューアプリセットが JCR で更新されるように、ビューアプリセットを Dynamic Media Classic および Dynamic Media Classic 固有のメタデータと同期する必要があります。この同期を実行するには、次のように Dynamic Media Classic を設定します。

1. [Dynamic Media Classic デスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html?lang=ja#getting-started)を開き、アカウントにログインします。

1. ページの右上隅付近で、**[!UICONTROL 設定]**／**[!UICONTROL アプリケーション設定]**／**[!UICONTROL 公開設定]**／**[!UICONTROL Image Server]** をクリックします。
1. Image Server 公開ページの上部にある「**[!UICONTROL 公開コンテキスト]**」ドロップダウンリストで、「**[!UICONTROL 画像サービス]**」を選択します。

1. 同じ Image Server 公開ページで、「**[!UICONTROL 要求属性]**」という見出しを探します。
1. 「要求属性」の見出しの下で、「**[!UICONTROL 返信画像のサイズ制限]**」を探します。次に、関連する「幅」フィールドと「高さ」フィールドで、パノラマ画像で許容される最大画像サイズを大きくします。

   Dynamic Media Classic には、25,000,000 ピクセルという制限があります。縦横比が 2:1 の画像の最大許容サイズは 7000 x 3500 です。ただし、通常のデスクトップ画面の場合、4096 x 2048 ピクセルで十分です。

   >[!NOTE]
   >
   >許容される最大画像サイズ以内の画像のみがサポートされます。サイズ制限を超える画像をリクエストすると、403 応答が返ります。

1. 「要求属性」の見出しの下で、次の操作をおこないます。

   * 「要求難読化モード」を「**[!UICONTROL 無効]**」に設定します。
   * 「要求ロックモード」を「**[!UICONTROL 無効]**」に設定します。

   これらの設定は、Experience Manager の `Panoramic Media` WCM コンポーネントを使用するために必要です。

1. Image Server 公開ページの下部で、左側にある「**[!UICONTROL 保存]**」をクリックします。

1. 右下隅にある「**[!UICONTROL 閉じる]**」をクリックします。

### パノラマメディア WCM コンポーネントのトラブルシューティング {#troubleshooting-the-panoramic-media-wcm-component}

WCM でパノラマメディアコンポーネントに画像をドロップしたときに、コンポーネントプレースホルダーが壊れた場合、次のトラブルシューティングを行ってください。

* 403 Forbidden エラーが返る場合は、要求された画像のサイズが大きすぎることが原因である可能性があります。「[Dynamic Media Classic の設定](/help/assets/panoramic-images.md#configuring-dynamic-media-classic-scene)」の「**[!UICONTROL 返信画像のサイズ制限]**」設定を確認します。

* アセットの「無効なロック」やページに表示される「解析エラー」については、「難読化モードの要求」と「ロックモードの要求」が無効になっていることを確認します。
* キャンバスが汚染されているというエラーについては、「ルールセット定義ファイルパス」を設定し、画像アセットに対する以前の要求の CDN を無効にします。
* サポートされている制限を超えるサイズの画像を要求した後に画質が低下した場合は、**[!UICONTROL JPEG エンコード属性／画質]**&#x200B;の設定が空でないことを確認します。「**[!UICONTROL 画質]**」フィールドの一般的な設定は、`95` です。この設定は、Image Server 公開ページにあります。このページにアクセスするには、[Dynamic Media Classic の設定](/help/assets/panoramic-images.md#configuring-dynamic-media-classic-scene)を参照してください。

## パノラマ画像のプレビュー {#previewing-panoramic-images}

[アセットのプレビュー](/help/assets/previewing-assets.md)を参照してください。

## パノラマ画像の公開 {#publishing-panoramic-images}

[アセットを公開](/help/assets/publishing-dynamicmedia-assets.md)を参照してください。
