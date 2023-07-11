---
title: ' [!DNL Assets]  とアクティビティストリームの統合'
description: ' [!DNL Experience Manager]  の記録機能と、特定のイベントを記録するための設定方法について説明します。'
contentOwner: AG
role: Developer
feature: Asset Management
exl-id: 2a08a7c1-8be9-42d1-9983-f9c8b12ea4e8
source-git-commit: 1ef5593495b4bf22d2635492a360168bccc1725d
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 30%

---

# [!DNL Assets] とアクティビティストリームの統合 {#integrating-assets-with-activity-stream}

[!DNL Adobe Experience Manager Assets] ユーザーは、アセットの作成、アップロード、削除など、様々な操作を実行します。 これらのアクションを記録して、ユーザーがおこなった操作の履歴を提供できます。 この節では、 [!DNL Experience Manager] および設定方法 [!DNL Experience Manager] を使用して特定のイベントを記録します。

## パフォーマンスに関する考慮事項とデフォルトの動作 {#performance-considerations-and-default-behavior}

この統合は、例えば、一括インポートの場合に、CPU とディスク容量を消費する可能性があります。 こうした理由から、 [!DNL Assets] アクティビティストリームとの統合は、デフォルトで無効になっています。

## サポートしているアクションイベント {#supported-action-events}

次のイベントを記録するように設定できます。

* 使用許諾済み（許可済み）
* 作成されたアセット (ASSET_CREATED)
* 移動されたアセット (ASSET_MOVED)
* 削除されたアセット (ASSET_REMOVED)
* ライセンス拒否（却下）
* ダウンロードされたアセット（ダウンロード済み）
* バージョン管理されたアセット（バージョン管理）
* 復元されたアセットのバージョン (RESTORED)
* 更新されたアセットメタデータ (METADATA_UPDATED)
* 外部システムに公開されたアセット (PUBLISHED_EXTERNAL)
* アセットのオリジナルの更新 (ORIGINAL_UPDATED)
* 更新されたアセットレンディション (RENDITION_UPDATED)
* 削除されたアセットのレンディション (RENDITION_REMOVED)
* 更新されたサブアセット (SUBASSET_UPDATED)
* 削除されたサブアセット (SUBASSET_REMOVED)

## [!DNL Assets] イベント記録の設定 {#configuring-aem-assets-events-recording}

[Web コンソール](/help/sites-deploying/configuring-osgi.md)から、Assets Event Recorder のチューニングにアクセスできます。Assets Event Recorder を設定するには、次の手順を実行します。

1. **[!UICONTROL Web コンソール]**&#x200B;に移動します。

1. クリック **[!UICONTROL 設定]**.

1. ダブルクリック **[!UICONTROL Day CQ DAM Event Recorder]**.

1. チェック **[!UICONTROL このサービスを有効にする]**.

1. 確認する **[!UICONTROL イベントタイプ]** ユーザーアクティビティストリームに記録する

1. 「**[!UICONTROL 保存]**」をクリックします。

## 記録されたイベントの読み取り {#reading-recorded-events}

記録されたイベントはアクティビティとして保存されます。[ActivityManager API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/granite/activitystreams/ActivityManager.html) を使用すると、プログラムで読み取ることができます。
