---
title: Dynamic Media のセットアップ
description: ダイナミックメディアを設定するには、ダイナミックメディアを設定し、画像とビューアのプリセットを管理する必要があります。
uuid: bcd1f9ab-4201-4222-9e4a-ba82b3c7cd6c
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: 36a4a4e7-8bb2-4853-b335-cf9148be410c
translation-type: tm+mt
source-git-commit: 10dae6e9f49e93d2f4923cee754c1d23d9d4b25e
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 65%

---


# Dynamic Media のセットアップ  {#setting-up-dynamic-media}

[Dynamic Media ](https://www.adobe.com/solutions/web-experience-management/dynamic-media.html)では、マーチャンダイジングおよびマーケティング用のリッチなビジュアルアセットをオンデマンドで配信し、アセットを管理できます。これらのアセットは、Web、モバイルおよびソーシャルサイトでの利用に合わせて自動的に拡大縮小されます。Dynamic Media は、一連のプライマリソースアセットを使用し、パフォーマンスが最適化されスケーラビリティに優れたグローバルネットワーク経由で、複数のリッチコンテンツのバリエーションをリアルタイムで生成および配信します。

>[!NOTE]
>
>このドキュメントは、AEM に直接統合された Dynamic Media の機能について説明します。AEMに統合されたダイナミックメディアクラシックを使用している場合は、[ダイナミックメディアクラシック統合ドキュメント](/help/sites-administering/scene7.md)を参照してください。
>
>ダイナミックメディアと統合されたAEMを使用したい場合は、[デュアル使用シナリオ](/help/sites-administering/scene7.md#dual-use-scenario)を参照してください。

Dynamic Media の管理者には、次のトピックが参考になります。

* [ダイナミックメディア —Scene7モードの設定](config-dms7.md)  — この設定は、ダイナミックメディアを初めてお使いの場合に使用します。
* [ダイナミックメディアハイブリッドモードの設定](config-dynamic.md)  — 既存のダイナミックメディアユーザーアップグレードAEMの場合は、この設定を使用します。
* [画像プリセットの管理](managing-image-presets.md)
* [ビューアプリセットの管理](managing-viewer-presets.md)
* [Dynamic Media - Scene7 モードのトラブルシューティング](troubleshoot-dms7.md)

次のトピックも参照してください。

* [ビデオエンコーディングとビデオプロファイル](video-profiles.md)
* [イメージプロファイル](image-profiles.md)

>[!NOTE]
>
>**アップグレードする場合：**
>
>* AEM を実行状態にした後にアップロードしたすべてのアセットで、Dynamic Media が自動的に有効になります（システム管理者によって明示的に無効にされた場合を除く）。アップグレードされた AEM インスタンスで Dynamic Media を新たに使用する場合、Dynamic Media を使用できるようアセットを再処理する必要が生じる場合があります。