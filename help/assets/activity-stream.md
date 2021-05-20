---
title: タイムライン表示のデジタルアセットのアクティビティストリーム
description: この記事では、アセットのアクティビティログをタイムラインに表示する方法について説明します。
contentOwner: AG
feature: アセット管理
role: Business Practitioner, Administrator
exl-id: 28dc0aa5-f2be-4e27-b7d8-415569b7ecd4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 69%

---

# タイムラインのアクティビティストリーム {#activity-stream-in-timeline}

この機能は、タイムラインにアセットのアクティビティログを表示します。[!DNL Adobe Experience Manager Assets]で次のアセット関連操作を実行すると、アクティビティストリーム機能によってタイムラインが更新され、アクティビティが反映されます。

アクティビティストリームでログに記録される操作は次のとおりです。

* 作成
* 削除
* ダウンロード（レンディションを含む）
* 公開
* 非公開
* 承認
* 拒否
* 移動

タイムラインに表示されるアクティビティログは、ログファイルが格納されている CRX の `/var/audit/com.day.cq.dam/content/dam` から取得されます。さらに、新しいAdobeがアップロードされたり、既存のアセットが変更されて[Experience Managerアセットリンク](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/manage-assets-using-adobe-asset-link.ug.html)または[アセットデスクトップアプリ](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html)を介して[!DNL Experience Manager]にチェックインされたりすると、タイムラインアクティビティが記録されます。

>[!NOTE]
>
>一時的なワークフローは、履歴情報が保存されないので、タイムラインに表示されません。

アクティビティストリームを表示するには、アセットに対して 1 つ以上の操作を実行して、アセットを選択してから、グローバルナビゲーションリストから&#x200B;**[!UICONTROL タイムライン]**&#x200B;を選択します。

![timeline-2](assets/timeline-2.png)

タイムラインに、アセットに対して実行した操作のアクティビティストリームが表示されます。

![activity_stream](assets/activity_stream.png)

>[!NOTE]
>
>**[!UICONTROL 公開]**&#x200B;タスクと&#x200B;**[!UICONTROL 非公開]**&#x200B;タスクのデフォルトのログ保管先は `/var/audit/com.day.cq.replication/content` です。**[!UICONTROL 移動]**&#x200B;タスクの場合は、デフォルトの保管先は `/var/audit/com.day.cq.wcm.core.page` になります。
