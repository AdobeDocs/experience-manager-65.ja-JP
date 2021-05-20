---
title: ' [!DNL Assets] とアクティビティストリームの統合'
description: ' [!DNL Experience Manager] の記録機能と、特定のイベントを記録するように設定する方法について説明します。'
contentOwner: AG
role: Developer
feature: アセット管理
exl-id: 2a08a7c1-8be9-42d1-9983-f9c8b12ea4e8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 57%

---

# [!DNL Assets]とアクティビティストリーム{#integrating-assets-with-activity-stream}を統合します

[!DNL Adobe Experience Manager Assets] ユーザーは、アセットの作成、アップロード、削除などの多くのアクションを実行します。ユーザーが何を実行かについて履歴を提供できるよう、これらのアクションを記録することができます。この節では、[!DNL Experience Manager]の記録機能と、特定のイベントを記録するための[!DNL Experience Manager]の設定方法について説明します。

## パフォーマンスに関する考慮事項とデフォルトの動作{#performance-considerations-and-default-behavior}

この統合は、一括して読み込むときなどに多くの CPU およびディスク領域を消費する可能性があります。このため、アクティビティストリームとの[!DNL Assets]統合は、デフォルトで無効になっています。

## サポートされているアクションイベント{#supported-action-events}

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

## [!DNL Assets]イベントの{#configuring-aem-assets-events-recording}の記録の設定

[Webコンソール](/help/sites-deploying/configuring-osgi.md)から、Assetsイベントレコーダーのチューニングにアクセスできます。 Assetsイベントレコーダーを設定するには、次の手順を実行します。

1. **[!UICONTROL Webコンソール]**&#x200B;に移動します。

1. 「**[!UICONTROL 設定]**」をクリックします。

1. 「**[!UICONTROL Day CQ DAM Event Recorder]**」をダブルクリックします。

1. 「**[!UICONTROL このサービスを有効にする]**」チェックボックスをオンにします。

1. ユーザーアクティビティストリームで記録する&#x200B;**[!UICONTROL イベントタイプ]**&#x200B;のチェックボックスをチェックします。

1. 「**[!UICONTROL 保存]**」をクリックします。

## 記録されたイベントを読み取る{#reading-recorded-events}

記録されたイベントはアクティビティとして保存されます。[ActivityManager API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/ActivityManager.html)を使用して、プログラムで読み取ることができます。
