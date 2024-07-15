---
title: タイムライン表示でのデジタルアセットのアクティビティストリーム
description: この記事では、アセットのアクティビティログをタイムラインに表示する方法について説明します。
contentOwner: AG
feature: Asset Management
role: User, Admin
exl-id: 28dc0aa5-f2be-4e27-b7d8-415569b7ecd4
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 100%

---

# タイムラインのアクティビティストリーム {#activity-stream-in-timeline}

この機能は、タイムラインにアセットのアクティビティログを表示します。[!DNL Adobe Experience Manager Assets] で以下のアセット関連操作を実行すると、アクティビティストリーム機能により、タイムラインが更新され、そのアクティビティが反映されます。

アクティビティストリームでログに記録される操作は次のとおりです。

* 作成
* 削除
* ダウンロード（レンディションを含む）
* 公開
* 非公開
* 承認
* 非承認
* 移動

タイムラインに表示されるアクティビティログは、ログファイルが格納されている CRX の `/var/audit/com.day.cq.dam/content/dam` から取得されます。また、[Adobe Asset Link](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/manage-assets-using-adobe-asset-link.ug.html) または [Experience Manager デスクトップアプリケーション](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html?lang=ja) により、新しいアセットがアップロードされたり、既存のアセットが変更されて [!DNL Experience Manager] にチェックインされたりすると、タイムラインアクティビティがログに記録されます。

>[!NOTE]
>
>一時的なワークフローは、履歴情報が保存されないので、タイムラインに表示されません。

アクティビティストリームを表示するには、アセットに対して 1 つ以上の操作を実行して、アセットを選択してから、グローバルナビゲーションリストから&#x200B;**[!UICONTROL タイムライン]**&#x200B;を選択します。

![timeline-2](assets/timeline-2.png)

タイムラインに、アセットに対して実行した操作のアクティビティストリームが表示されます。

![activity_stream](assets/activity_stream.png)

>[!NOTE]
>
>「**[!UICONTROL 公開]**」および「**[!UICONTROL 非公開]**」タスクのデフォルトのログ保存場所は、`/var/audit/com.day.cq.replication/content` です。**[!UICONTROL 移動]**&#x200B;タスクの場合、デフォルトの場所は `/var/audit/com.day.cq.wcm.core.page` です。
