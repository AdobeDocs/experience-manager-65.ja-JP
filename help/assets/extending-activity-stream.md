---
title: アクティビティ [!DNL Assets] ストリームとの統合
description: Describes the recording capabilities of [!DNL Experience Manager] and how to configure it to record specific events.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5069c2cd26e84866d72a61d36de085dadd556cdd
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 57%

---


# アクティビティストリーム [!DNL Assets] との統合 {#integrating-assets-with-activity-stream}

[!DNL Adobe Experience Manager Assets] ユーザーは、アセットの作成、アップロード、削除などの多くのアクションを実行します。ユーザーが何を実行かについて履歴を提供できるよう、これらのアクションを記録することができます。This section describes the recording capabilities of [!DNL Experience Manager] and how to configure [!DNL Experience Manager] in order to record specific events.

## Performance considerations and default behavior {#performance-considerations-and-default-behavior}

この統合は、一括して読み込むときなどに多くの CPU およびディスク領域を消費する可能性があります。For these reasons the [!DNL Assets] integration with the Activity Stream is disabled by default.

## Supported action events {#supported-action-events}

以下のイベントを記録対象として設定できます。

* ライセンス許可（ACCEPTED）
* アセットの作成（ASSET_CREATED）
* アセットの移動（ASSET_MOVED）
* アセットの削除（ASSET_REMOVED）
* ライセンス拒否（REJECTED）
* アセットのダウンロード（DOWNLOADED）
* アセットのバージョン設定（VERSIONED）
* アセットのバージョンの復元（RESTORED）
* アセットのメタデータの更新（METADATA_UPDATED）
* アセットの外部システムへの公開（PUBLISHED_EXTERNAL）
* 元のアセットの更新（ORIGINAL_UPDATED）
* アセットのレンディションの更新（RENDITION_UPDATED）
* アセットのレンディションの削除（RENDITION_REMOVED）
* サブアセットの更新（SUBASSET_UPDATED）
* サブアセットの削除（SUBASSET_REMOVED）

## [!DNL Assets] イベントの記録の設定 {#configuring-aem-assets-events-recording}

[Webコンソールを使用して](/help/sites-deploying/configuring-osgi.md) 、アセットイベントレコーダーのチューニングを行うことができます。 アセットイベントレコーダーを設定するには、次の手順に従います。

1. Navigate to the **[!UICONTROL Web Console]**

1. 「**[!UICONTROL 設定]**」をクリックします。

1. 「**[!UICONTROL Day CQ DAM Event Recorder]**」をダブルクリックします。

1. 「**[!UICONTROL このサービスを有効にする]**」チェックボックスをオンにします。

1. ユーザーアクティビティストリームで記録する&#x200B;**[!UICONTROL イベントタイプ]**&#x200B;のチェックボックスをチェックします。

1. 「**[!UICONTROL 保存]**」をクリックします。

## 記録済みイベントの読み取り {#reading-recorded-events}

記録されたイベントはアクティビティとして保存されます。You can read them programmatically using the [ActivityManager API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/ActivityManager.html).
