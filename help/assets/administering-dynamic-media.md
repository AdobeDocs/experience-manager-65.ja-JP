---
title: Dynamic Media の設定
description: Dynamic Media をセットアップするには、Dynamic Media を設定して、画像やビューアのプリセットを管理する必要があります
uuid: bcd1f9ab-4201-4222-9e4a-ba82b3c7cd6c
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: 36a4a4e7-8bb2-4853-b335-cf9148be410c
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# Dynamic Media の設定 {#setting-up-dynamic-media}

[Dynamic Media ](https://www.adobe.com/solutions/web-experience-management/dynamic-media.html)では、マーチャンダイジングおよびマーケティング用のリッチなビジュアルアセットをオンデマンドで配信し、アセットを管理できます。これらのアセットは、Web、モバイルおよびソーシャルサイトでの利用に合わせて自動的に拡大縮小されます。Dynamic Media は、一連のマスターアセットを使用し、パフォーマンスが最適化されスケーラビリティに優れたグローバルネットワーク経由で、複数のリッチコンテンツのバリエーションをリアルタイムで生成および配信します。

>[!NOTE]
>
>このドキュメントは、AEM に直接統合された Dynamic Media の機能について説明します。If you are using Dynamic Media Classic (previously called Scene7) integrated into AEM, see [Dynamic Media Classic integration documentation](/help/sites-administering/scene7.md).
>
>See [Dual Use Scenario](/help/sites-administering/scene7.md#dual-use-scenario) for times when you may want to use AEM integrated with Dynamic Media Classic along with Dynamic Media.

Dynamic Media の管理者には、次のトピックが参考になります。

* [ダイナミックメディア —Scene7モードの設定](config-dms7.md) — Dynamic mediaを初めて使用する場合は、この設定を使用します。
* [ダイナミックメディアハイブリッドモードの設定](config-dynamic.md) — 既存のダイナミックメディアユーザーがAEMをアップグレードする場合は、この設定を使用します。
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
>* AEMの起動と実行が完了すると、アップロードしたアセットはすべて、ダイナミックメディアを自動的に有効になります（システム管理者が明示的に無効にしていない限り）。 アップグレードしたAEMのインスタンスを使用し、ダイナミックメディアに初めてアクセスする場合は、アセットをダイナミックメディア対応にするには、アセットの再処理が必要になる場合があります。