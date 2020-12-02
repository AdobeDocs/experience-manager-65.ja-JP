---
title: ' [!DNL Assets] をアクティビティストリームと統合'
description: ' [!DNL Experience Manager] の記録機能と、特定のイベントを記録するように設定する方法について説明します。'
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5069c2cd26e84866d72a61d36de085dadd556cdd
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 57%

---


# [!DNL Assets]をアクティビティストリームと統合{#integrating-assets-with-activity-stream}

[!DNL Adobe Experience Manager Assets] ユーザーは、アセットの作成、アップロード、削除などの多くのアクションを実行します。ユーザーが何を実行かについて履歴を提供できるよう、これらのアクションを記録することができます。この節では、[!DNL Experience Manager]の記録機能と、特定のイベントを記録するための[!DNL Experience Manager]の設定方法について説明します。

## パフォーマンスの考慮事項とデフォルト動作{#performance-considerations-and-default-behavior}

この統合は、一括して読み込むときなどに多くの CPU およびディスク領域を消費する可能性があります。このため、[!DNL Assets]とアクティビティストリームの統合はデフォルトで無効になっています。

## サポートされるアクションイベント{#supported-action-events}

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

## [!DNL Assets]イベントの記録{#configuring-aem-assets-events-recording}の構成

[Webコンソール](/help/sites-deploying/configuring-osgi.md)は、アセットイベントレコーダーのチューニングにアクセスします。 アセットイベントレコーダーを設定するには、次の手順に従います。

1. **[!UICONTROL Webコンソール]**&#x200B;に移動します

1. 「**[!UICONTROL 設定]**」をクリックします。

1. 「**[!UICONTROL Day CQ DAM Event Recorder]**」をダブルクリックします。

1. 「**[!UICONTROL このサービスを有効にする]**」チェックボックスをオンにします。

1. ユーザーアクティビティストリームで記録する&#x200B;**[!UICONTROL イベントタイプ]**&#x200B;のチェックボックスをチェックします。

1. 「**[!UICONTROL 保存]**」をクリックします。

## 記録されたイベントを読み取りました{#reading-recorded-events}

記録されたイベントはアクティビティとして保存されます。[ActivityManager API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/ActivityManager.html)を使用して、プログラムで読み取ることができます。
