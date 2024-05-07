---
title: ' [!DNL Assets]  とアクティビティストリームの統合'
description: ' [!DNL Experience Manager]  の記録機能と、特定のイベントを記録するための設定方法について説明します。'
contentOwner: AG
role: Developer
feature: Asset Management
exl-id: 2a08a7c1-8be9-42d1-9983-f9c8b12ea4e8
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: ht
source-wordcount: '243'
ht-degree: 100%

---

# [!DNL Assets] とアクティビティストリームの統合 {#integrating-assets-with-activity-stream}

[!DNL Adobe Experience Manager Assets] ユーザーは、アセットの作成、アップロード、削除などの多くのアクションを実行します。ユーザーが実行した操作の履歴を提供できるよう、これらのアクションを記録できます。この節では、[!DNL Experience Manager] の記録機能と、特定のイベントを記録するための [!DNL Experience Manager] の設定方法について説明します。

## パフォーマンスに関する考慮事項とデフォルトの動作 {#performance-considerations-and-default-behavior}

この統合は、一括して読み込む際などに多くの CPU およびディスク領域を消費する可能性があります。これらの理由から、[!DNL Assets] とアクティビティストリームの統合はデフォルトで無効になっています。

## サポートしているアクションイベント {#supported-action-events}

次のイベントを記録するように設定できます。

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

## [!DNL Assets] イベント記録の設定 {#configuring-aem-assets-events-recording}

[Web コンソール](/help/sites-deploying/configuring-osgi.md)から、Assets Event Recorder のチューニングにアクセスできます。Assets Event Recorder を設定するには、次の手順を実行します。

1. **[!UICONTROL Web コンソール]**&#x200B;に移動します。

1. 「**[!UICONTROL 設定]**」をクリックします。

1. 「**[!UICONTROL Day CQ DAM Event Recorder]**」をダブルクリックします。

1. 「**[!UICONTROL このサービスを有効にする]**」チェックボックスをオンにします。

1. ユーザーアクティビティストリームに記録する&#x200B;**[!UICONTROL イベントタイプ]**&#x200B;のチェックボックスをオンにします。

1. 「**[!UICONTROL 保存]**」をクリックします。

## 記録されたイベントの読み取り {#reading-recorded-events}

記録されたイベントはアクティビティとして保存されます。[ActivityManager API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/granite/activitystreams/ActivityManager.html) を使用すると、プログラムで読み取ることができます。
