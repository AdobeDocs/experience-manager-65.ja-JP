---
title: レスポンシブサイト用に最適化された画像の配信
description: レスポンシブコード機能を使用して最適化された画像を配信する方法
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
feature: Asset Management
role: User, Admin
exl-id: 753d806f-5f44-4d73-a3a3-a2a0fc3e154b
source-git-commit: 04050f31742c926b45235595f6318929d3767bd8
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 96%

---

# レスポンシブサイト用に最適化された画像の配信 {#delivering-optimized-images-for-a-responsive-site}

レスポンシブサービング用のコードを Web 開発者と共有する場合は、レスポンシブコード機能を使用します。レスポンシブ（**[!UICONTROL RESS]**）コードをクリップボードにコピーして、Web 開発者と共有することができます。

この機能は、Web サイトがサードパーティの WCM で稼動する場合に有効です。ただし、Web サイトが Adobe Experience Manager で稼動する場合は、オフサイトの画像サーバーが画像をレンダリングして Web ページに提供します。

[Web ページへのビデオビューアの埋め込み](embed-code.md)も参照してください。

[Web アプリケーションへの URL のリンク](linking-urls-to-yourwebapplication.md)も参照してください。

**レスポンシブサイトに最適化された画像を配信するには：**

1. レスポンシブコードを提供する画像の場所に移動して、ドロップダウンメニューで「**[!UICONTROL レンディション]**」を選択します。

   ![chlimage_1-408](assets/chlimage_1-408.png)

1. レスポンシブ画像プリセットを選択します。「**[!UICONTROL URL]**」ボタンと「**[!UICONTROL RESS]**」ボタンが表示されます。

   ![chlimage_1-409](assets/chlimage_1-208.png)

   >[!NOTE]
   >
   >「**[!UICONTROL URL]**」ボタンまたは「**[!UICONTROL RESS]**」ボタンを使用可能にするには、選択したアセット&#x200B;*と*&#x200B;選択した画像プリセットまたはビューアプリセットを公開する必要があります。
   >
   >Dynamic Media - ハイブリッドモードでは、画像プリセットを手動で公開する必要があります。Dynamic Media - Scene7 モードでは、画像プリセットが自動的に公開されます。

1. 「**[!UICONTROL RESS]**」を選択します。

   ![chlimage_1-410](assets/chlimage_1-410.png)

1. **[!UICONTROL レスポンシブ画像を埋め込み]**&#x200B;ダイアログボックスで、レスポンシブコードテキストを選択してコピーし Web サイトに貼り付けて、レスポンシブアセットにアクセスします。
1. 埋め込みコード内でデフォルトのブレークポイントを編集して、コード内で直接、レスポンシブ web サイトのブレークポイントに合わせます。また、異なるページのブレークポイントで、異なる解像度の画像が配信されることをテストします。

## HTTP/2 を使用して Dynamic Media アセットを配信する {#using-http-to-delivery-your-dynamic-media-assets}

HTTP/2 は、ブラウザーとサーバーの通信方法を改善する、新しく更新された web プロトコルです。情報の転送を高速化し、必要な処理能力を削減します。Dynamic Media アセットの配信は HTTP/2 を使用して行うことができ、応答時間と読み込み時間を短縮できます。

Dynamic Media アカウントでの HTTP/2 の使用方法について詳しくは、[コンテンツの HTTP/2 配信](http2.md)を参照してください。
