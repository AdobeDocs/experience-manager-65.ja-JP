---
title: Dynamic Media のセットアップ
description: Dynamic Media をセットアップするには、Dynamic Media を設定して、画像やビューアのプリセットを管理する必要があります。
uuid: bcd1f9ab-4201-4222-9e4a-ba82b3c7cd6c
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: 36a4a4e7-8bb2-4853-b335-cf9148be410c
role: User, Admin
exl-id: 85fa0414-354e-4530-81f9-a5659bb7f2fd
feature: Configuration
source-git-commit: 8353e6fcc76dd63a0816babbe593f474abbc4508
workflow-type: ht
source-wordcount: '260'
ht-degree: 100%

---

# Dynamic Media のセットアップ {#setting-up-dynamic-media}

[Dynamic Media ](https://business.adobe.com/products/experience-manager/assets/dynamic-media.html)では、マーチャンダイジングおよびマーケティング用のリッチなビジュアルアセットをオンデマンドで配信し、アセットを管理できます。これらのアセットは、Web、モバイルおよびソーシャルサイトでの利用に合わせて自動的に拡大縮小されます。Dynamic Media は、一連のプライマリソースアセットを使用し、パフォーマンスが最適化されスケーラビリティに優れたグローバルネットワーク経由で、複数のリッチコンテンツのバリエーションをリアルタイムで生成および配信します。

>[!NOTE]
>
>このドキュメントでは、Dynamic Media を Adobe Experience Manager に直接統合して使用する際の機能について説明します。Dynamic Media Classic を Experience Manager に統合して使用する場合は、[Dynamic Media Classic 統合ドキュメント](/help/sites-administering/scene7.md)を参照してください。
>
>Experience Manager を Dynamic Media Classic と Dynamic Media の両方に統合して使用する場合は、[両方を利用するシナリオ](/help/sites-administering/scene7.md#dual-use-scenario)を参照してください。

Dynamic Media の管理者には、次のトピックが参考になります。

* [Dynamic Media - Scene7 モードの設定](config-dms7.md) - 新規に Dynamic Media を使用する場合は、この設定を使用します。
* [Dynamic Media - ハイブリッドモードの設定](config-dynamic.md) - 既に Dynamic Media を使用していて Experience Manager をアップグレードする場合は、この設定を使用します。
* [画像プリセットの管理](managing-image-presets.md)
* [ビューアプリセットの管理](managing-viewer-presets.md)
* [Dynamic Media のトラブルシューティング - Scene7 モード](troubleshoot-dms7.md)

次のトピックも参照してください。

* [ビデオエンコーディングとビデオプロファイル](video-profiles.md)
* [イメージプロファイル](image-profiles.md)

>[!NOTE]
>
>**アップグレードする場合：**
>
>* Experience Manager を実行状態にした後にアップロードしたすべてのアセットで、Dynamic Media が自動的に有効になります（システム管理者によって明示的に無効にされた場合を除く）。アップグレードされた Experience Manager インスタンスで Dynamic Media を新たに使用する場合、Dynamic Media を使用できるようアセットを再処理する必要があります。



