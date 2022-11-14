---
title: アセットのアップロード制限を設定する
description: ユーザーがアップロードできるアセット（ファイル）のタイプを制限する
contentOwner: AG
role: Developer, Admin, Architect
feature: Asset Management,Upload
exl-id: 0e009b9a-54c4-4715-98ee-0207839f90f6
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 100%

---

# アセットのアップロード制限を設定する {#configuring-asset-upload-restrictions}

[!DNL Adobe Experience Manager Assets] の設定で、ユーザーがアップロードできるアセット（ファイル）のタイプを制限できます。これにより、望ましくない形式や悪意のあるファイルが誤ってアップロードされるのを防ぐことができます。 `Day CQ DAM Asset Upload Restriction` サービスを使用すると、ユーザーがアップロードできるファイルの種類を制御できます。デフォルトでは、[!DNL Assets] ではすべての MIME タイプのアセットをアップロードできます。ただし、アップロードを特定の MIME タイプのファイルのみに制限するようにサービスを設定できます。

1. Configuration Manager の Web コンソールを開きます。`https://[aem_server]:[port]/system/console/configMgr` にアクセスします。
1. **[!UICONTROL Day CQ DAM Asset Upload Restriction]** サービスを編集モードで開きます。デフォルトでは、「**Allow all MIME**」オプションがオンになっており、すべての MIME タイプのファイルのアップロードが許可されます。

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. ユーザーがアップロードできるファイルを特定の MIME タイプのみに制限するには、「**[!UICONTROL すべての MIME を許可]**」オプションをオフにして、「**[!UICONTROL 許可されたアセットの MIME（regex）]**」フィールドに許可する MIME タイプを正規表現を使用して指定します。

   ![chlimage_1-379](assets/chlimage_1-379.png)

1. 「**[!UICONTROL 保存]**」をクリックして、変更を保存します。許可する MIME タイプに MIME 文字列を指定した場合、これらのフィールドに設定した MIME 文字列と一致しないすべての MIME タイプのアセットでは、アップロード操作が失敗します。
