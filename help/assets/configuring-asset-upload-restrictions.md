---
title: アセットのアップロード制限の設定
description: 'ユーザーがアップロードできるアセット（ファイル）の種類を制限する '
contentOwner: AG
translation-type: tm+mt
source-git-commit: 23d19d9656d61874cd00a9a2473092be0c53b8f8
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 55%

---


# アセットのアップロード制限の設定 {#configuring-asset-upload-restrictions}

You can configure [!DNL Adobe Experience Manager Assets] to restrict the type of assets that users can upload. 意図しない形式や悪意のあるファイルを誤ってアップロードするのを防ぐのに役立ちます。 `Day CQ DAM Asset Upload Restriction` サービスを使用すると、ユーザーがアップロードできるファイルの種類を制御できます。By default, [!DNL Assets] allows users to upload assets of all MIME types. ただし、アップロードを特定の MIME タイプのファイルのみに制限するようにサービスを設定できます。

1. Configuration Manager の Web コンソールを開きます。`https://[aem_server]:[port]/system/console/configMgr` にアクセスします。
1. **[!UICONTROL Day CQ DAM Asset Upload Restriction]** サービスを編集モードで開きます。デフォルトでは、「**Allow all MIME**」オプションがオンになっており、すべての MIME タイプのファイルのアップロードが許可されます。

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. To restrict users to upload files of certain MIME types only, unselect the **[!UICONTROL Allow all MIME]** option and specify allowed MIME types in the **[!UICONTROL Allowed Asset MIMEs (regex)]** fields using regular expressions.

   ![chlimage_1-379](assets/chlimage_1-379.png)

1. 「**[!UICONTROL 保存]**」をクリックして、変更を保存します。許可する MIME タイプに MIME 文字列を指定した場合、これらのフィールドに設定した MIME 文字列と一致しないすべての MIME タイプのアセットでは、アップロード操作が失敗します。
