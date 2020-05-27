---
title: アセットとアクティビティストリームの統合
description: Experience Managerの記録機能と、特定のイベントを記録するように設定する方法について説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 51%

---


# Integrate Assets with activity stream {#integrating-assets-with-activity-stream}

Adobe Experience Manager Assetsのユーザーは、アセットの作成、アップロード、削除など、様々な操作を実行します。 ユーザーが何を実行かについて履歴を提供できるよう、これらのアクションを記録することができます。ここでは、Experience Managerの記録機能と、特定のイベントを記録するためのExperience Managerの設定方法について説明します。

## Performance considerations and default behavior {#performance-considerations-and-default-behavior}

この統合は、一括して読み込むときなどに多くの CPU およびディスク領域を消費する可能性があります。このため、アセットとアクティビティストリームの統合はデフォルトで無効になっています。

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

## アセットイベントの記録の設定 {#configuring-aem-assets-events-recording}

[Webコンソールを使用して](/help/sites-deploying/configuring-osgi.md) 、アセットイベントレコーダーのチューニングを行うことができます。 アセットイベントレコーダーを設定するには、次の手順に従います。

1. Navigate to the **[!UICONTROL Web Console]**

1. 「**[!UICONTROL 設定]**」をクリックします。

1. 「**[!UICONTROL Day CQ DAM Event Recorder]**」をダブルクリックします。

1. 「**[!UICONTROL このサービスを有効にする]**」チェックボックスをオンにします。

1. ユーザーアクティビティストリームで記録する&#x200B;**[!UICONTROL イベントタイプ]**&#x200B;のチェックボックスをチェックします。

1. 「**[!UICONTROL 保存]**」をクリックします。

## 記録済みイベントの読み取り {#reading-recorded-events}

記録されたイベントはアクティビティとして保存されます。You can read them programmatically using the [ActivityManager API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/ActivityManager.html).
