---
title: Web ページへの Dynamic Media ビデオビューアまたは画像ビューアの埋め込み
description: Web ページに Dynamic Media ビデオまたは画像を埋め込む方法を説明します。
uuid: 6f786521-eb6c-4c80-8c15-9bf97b56818f
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 4ae76d8a-208f-4099-9f17-a94df424685e
feature: ビューア
role: 営業者、管理者
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 91%

---


# Web ページへの Dynamic Media ビデオ、画像ビューア、またはディメンショナルビューアの埋め込み {#embedding-the-video-or-image-viewer-on-a-web-page}

Web ページに埋め込んでビデオを再生したりアセットを表示したりする場合は、**[!UICONTROL 埋め込みコード]**&#x200B;機能を使用します。埋め込みコードをクリップボードにコピーして、Web ページに貼り付けることができます。**[!UICONTROL 埋め込みコード]**&#x200B;ダイアログボックスでは、コードの編集はできません。

AEM を WCM として使用&#x200B;_していない_&#x200B;場合に限り、URL の埋め込みを実行します。AEM を WCM として使用している場合は、[ページに直接アセットを追加](adding-dynamic-media-assets-to-pages.md)します。

[Web アプリケーションへの URL のリンク](linking-urls-to-yourwebapplication.md)を参照してください。

[レスポンシブサイト用に最適化された画像の配信](responsive-site.md)を参照してください。

>[!NOTE]
>
>埋め込みコードは、選択したアセットを公開するまではコピーできません。また、ビューアプリセットまたは画像プリセットを公開する必要もあります。
>
>[アセットの公開](publishing-dynamicmedia-assets.md)を参照してください。
>
>[ビューアプリセットの公開](managing-viewer-presets.md#publishing-viewer-presets)を参照してください。
>
>[画像プリセットの公開](managing-image-presets.md#publishing-image-presets)を参照してください。

**Dynamic Media ビデオビューアまたは画像ビューアを Web ページに埋め込むには**

1. 埋め込みコードをコピーする&#x200B;*公開済み*&#x200B;のビデオまたは画像アセットに移動します。

   埋め込みコードを使用するには、その&#x200B;*前に*&#x200B;アセットを&#x200B;*公開*&#x200B;しておく必要があります。また、ビューアプリセットまたは画像プリセットを公開する必要もあります。

   [アセットの公開](publishing-dynamicmedia-assets.md)を参照してください。

   [ビューアプリセットの公開](managing-viewer-presets.md#publishing-viewer-presets)を参照してください。

   [画像プリセットの公開](managing-image-presets.md#publishing-image-presets)を参照してください。

1. 左側のレールで、ドロップダウンメニューを選択し、「**[!UICONTROL ビューア」をタップします。]**
1. 左側のレールで、ビューアプリセット名をタップします。ビューアプリセットがアセットに適用されます。
1. 「**[!UICONTROL 埋め込み」をタップします。]**
1. **[!UICONTROL 埋め込みコード]**&#x200B;ダイアログボックスで、コード全体をクリップボードにコピーし、**[!UICONTROL 閉じるをタップします。]**
1. 埋め込みコードを Web ページに貼り付けます。

## HTTP/2 を使用した Dynamic Media アセットの配信 {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2 は、ブラウザーとサーバーの交信を強化する、新しく更新された Web プロトコルです。このプロトコルを使用すれば、情報の伝送を高速化し、必要な処理能力を抑えることができます。HTTP/2 上で Dynamic Media アセットの配信が可能になり、応答時間と読み込み時間が短縮されました。

Dynamic Media アカウントでの HTTP/2 の使用方法について詳しくは、[コンテンツの HTTP/2 配信](http2.md)を参照してください。
