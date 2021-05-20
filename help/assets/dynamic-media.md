---
title: Dynamic Media の操作
description: Dynamic Media を使用して、Web、モバイルおよびソーシャルサイトで使用するためにアセットを配信する方法を学習します。
uuid: 4dc0f436-d20e-4e8b-aeff-5515380fa44d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: introduction
content-type: reference
discoiquuid: a8063d43-923a-42ac-9a16-0c7fadd8f73f
role: Business Practitioner, Administrator
exl-id: f8a80b22-b1a6-475f-b3f1-b2f47822f21d
feature: コラボレーション、アセット管理
source-git-commit: c9aec973faf4caef741961d92a6f258646aeddb7
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 90%

---

# Dynamic Media の操作 {#working-with-dynamic-media}

[Dynamic Media ](https://www.adobe.com/solutions/web-experience-management/dynamic-media.html)は、マーチャンダイジングおよびマーケティング用のリッチなビジュアルアセットをオンデマンドで配信するもので、これらのアセットは、Web、モバイルおよびソーシャルサイトでの利用に合わせて自動的に拡大縮小されます。Dynamic Media は、一連のプライマリソースアセットを使用し、パフォーマンスが最適化されスケーラビリティに優れたグローバルネットワーク経由で、複数のリッチコンテンツのバリエーションをリアルタイムで生成および配信します。

Dynamic Media は、ズーム、360 度スピン、ビデオなどのインタラクティブな閲覧エクスペリエンスを提供します。Dynamic Media は Adobe Experience Manager デジタルアセット管理（AEM Assets）ソリューションのワークフローを独自に取り込むことで、デジタルキャンペーン管理プロセスを簡易化し、効率化します。

>[!NOTE]
>
>[Adobe Experience Manager および Dynamic Media の操作](https://helpx.adobe.com/jp/experience-manager/using/aem_dynamic_media.html)にコミュニティの記事があります。

## Dynamic Media の機能  {#what-you-can-do-with-dynamic-media}

Dynamic Media では、公開前のアセットを管理できます。一般的なアセットの操作方法については、[デジタルアセットの操作](manage-assets.md)で詳しく説明しています。一般的なトピックには、アセットのアップロード、ダウンロード、編集および公開、プロパティの表示と編集、アセットの検索が含まれます。

Dynamic Media 限定の機能は次のとおりです。

* [カルーセルバナー](carousel-banners.md)
* [画像セット](image-sets.md)
* [インタラクティブ画像](interactive-images.md)
* [インタラクティブビデオ](interactive-videos.md)
* [混在メディアセット](mixed-media-sets.md)
* [パノラマ画像](panoramic-images.md)

* [スピンセット](spin-sets.md)
* [ビデオ](video.md)
* [Dynamic Media アセットの配信](delivering-dynamic-media-assets.md)
* [アセットの管理](managing-assets.md)
* [クイックビューを使用したカスタムポップアップの作成](custom-pop-ups.md)

[Dynamic Media の設定](administering-dynamic-media.md)も参照してください。

>[!NOTE]
>
>Dynamic Mediaの使用とDynamic Media ClassicとAEMの統合の違いについては、[Dynamic Media ClassicとDynamic Media](/help/sites-administering/scene7.md#aem-scene-integration-versus-dynamic-media)の統合を参照してください。

## Dynamic Media が有効な場合と無効な場合の比較 {#dynamic-media-on-versus-dynamic-media-off}

Dynamic Media が有効（オン）になっているかどうかは、次の特徴から判断できます。

* アセットのダウンロードやプレビューで動的レンディションを使用できる。
* 画像セット、スピンセット、混在メディアセットを使用できる。
* PTIFF レンディションが作成されている。

Dynamic Media [が有効](config-dynamic.md#enabling-dynamic-media)の場合、画像アセットをクリックしたときのアセットの表示は異なります。 Dynamic Media では、オンデマンドの HTML5 ビューアが使用されます。

### 動的レンディション {#dynamic-renditions}

「**[!UICONTROL 動的]**」の下にある画像プリセットやビューアプリセットなどの動的レンディションは、Dynamic Media が有効な場合に使用できます。

![chlimage_1-358](assets/chlimage_1-358.png)

### 画像セット、スピンセット、混在メディアセット {#image-sets-spins-sets-mixed-media-sets}

画像セット、スピンセットおよび混在メディアセットは、Dynamic Media が有効な場合に使用できます。

![chlimage_1-359](assets/chlimage_1-359.png)

### PTIFF レンディション {#ptiff-renditions}

Dynamic Media 対応のアセットには `pyramid.tiffs` が含まれています。

![chlimage_1-360](assets/chlimage_1-360.png)

### アセットのビューの変化 {#asset-views-change}

Dynamic Media を有効にすると、「`+`」ボタンをクリックしてズームインし、「`-`」ボタンをクリックしてズームアウトすることができます。クリックまたはタップして、特定の領域にズームインすることもできます。元に戻すアイコンをクリックすると元のバージョンに戻ります。また、斜めの矢印をクリックすると、画像を全画面表示にすることができます。Dynamic Media を有効にした場合の画面は次のようになります。

![chlimage_1-361](assets/chlimage_1-361.png)

Dynamic Media を無効にした場合は、次のようにズームイン、ズームアウトおよび元のサイズに戻す操作が可能です。

![chlimage_1-362](assets/chlimage_1-362.png)
