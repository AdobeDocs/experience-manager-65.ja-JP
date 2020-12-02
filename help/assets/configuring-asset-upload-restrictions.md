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


# アセットのアップロード制限を設定{#configuring-asset-upload-restrictions}

[!DNL Adobe Experience Manager Assets]を設定して、ユーザーがアップロードできるアセットの種類を制限できます。 意図しない形式や悪意のあるファイルを誤ってアップロードするのを防ぐのに役立ちます。 `Day CQ DAM Asset Upload Restriction` サービスを使用すると、ユーザーがアップロードできるファイルの種類を制御できます。デフォルトでは、[!DNL Assets]は、すべてのMIMEタイプのアセットのアップロードをユーザーに許可します。 ただし、アップロードを特定の MIME タイプのファイルのみに制限するようにサービスを設定できます。

1. Configuration Manager の Web コンソールを開きます。`https://[aem_server]:[port]/system/console/configMgr` にアクセスします。
1. **[!UICONTROL Day CQ DAM Asset Upload Restriction]** サービスを編集モードで開きます。デフォルトでは、「**Allow all MIME**」オプションがオンになっており、すべての MIME タイプのファイルのアップロードが許可されます。

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. 特定のMIMEタイプのファイルのみをアップロードするようにユーザーに制限するには、「**[!UICONTROL すべてのMIMEを許可]**」オプションの選択を解除し、正規式を使用して「**[!UICONTROL 許可されるアセットのMIME(regex)]**」フィールドに許可されるMIMEタイプを指定します。

   ![chlimage_1-379](assets/chlimage_1-379.png)

1. 「**[!UICONTROL 保存]**」をクリックして、変更を保存します。許可する MIME タイプに MIME 文字列を指定した場合、これらのフィールドに設定した MIME 文字列と一致しないすべての MIME タイプのアセットでは、アップロード操作が失敗します。
