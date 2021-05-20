---
title: アセットのアップロード制限の設定
description: 'ユーザーがアップロードできるアセット（ファイル）のタイプを制限する '
contentOwner: AG
role: Developer, Administrator, Architect
feature: アセット管理，アップロード
exl-id: 0e009b9a-54c4-4715-98ee-0207839f90f6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 54%

---

# アセットのアップロード制限の設定{#configuring-asset-upload-restrictions}

[!DNL Adobe Experience Manager Assets]を設定して、ユーザーがアップロードできるアセットのタイプを制限できます。 これにより、意図しない形式や悪意のあるファイルが誤ってアップロードされるのを防ぐことができます。 `Day CQ DAM Asset Upload Restriction` サービスを使用すると、ユーザーがアップロードできるファイルの種類を制御できます。デフォルトでは、[!DNL Assets]を使用すると、すべてのMIMEタイプのアセットのアップロードが許可されます。 ただし、アップロードを特定の MIME タイプのファイルのみに制限するようにサービスを設定できます。

1. Configuration Manager の Web コンソールを開きます。`https://[aem_server]:[port]/system/console/configMgr` にアクセスします。
1. **[!UICONTROL Day CQ DAM Asset Upload Restriction]** サービスを編集モードで開きます。デフォルトでは、「**Allow all MIME**」オプションがオンになっており、すべての MIME タイプのファイルのアップロードが許可されます。

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. アップロードを特定のMIMEタイプのファイルのみに制限するには、「**[!UICONTROL Allow all MIME]**」オプションをオフにし、「**[!UICONTROL Allowed Asset MIMEs (regex)]**」フィールドに許可するMIMEタイプを正規表現を使用して指定します。

   ![chlimage_1-379](assets/chlimage_1-379.png)

1. 「**[!UICONTROL 保存]**」をクリックして、変更を保存します。許可する MIME タイプに MIME 文字列を指定した場合、これらのフィールドに設定した MIME 文字列と一致しないすべての MIME タイプのアセットでは、アップロード操作が失敗します。
