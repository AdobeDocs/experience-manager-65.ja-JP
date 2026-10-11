---
title: アセットのアップロード制限を設定する
description: ユーザーがアップロードできるアセット（ファイル）のタイプを制限する
contentOwner: AG
role: Developer, Admin
feature: Asset Management,Upload
exl-id: 0e009b9a-54c4-4715-98ee-0207839f90f6
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: 7d2b2ec8-499c-5434-9ffd-9218cd71f683
    internal-label: Asset Management
  - id: cda65036-5305-4f01-89da-9b3506ae8c50
    internal-label: Administration
subfeature_v2:
  - id: f1dc0c96-022d-4003-afbe-47bd40173c4a
    internal-label: Upload assets
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 84%
---
# アセットのアップロード制限を設定する {#configuring-asset-upload-restrictions}

[!DNL Adobe Experience Manager Assets] の設定で、ユーザーがアップロードできるアセット（ファイル）のタイプを制限できます。 これにより、望ましくない形式や悪意のあるファイルが誤ってアップロードされるのを防ぐことができます。 `Day CQ DAM Asset Upload Restriction` サービスを使用すると、ユーザーがアップロードできるファイルの種類を制御できます。 デフォルトでは、[!DNL Assets] ではすべての MIME タイプのアセットをアップロードできます。 ただし、アップロードを特定の MIME タイプのファイルのみに制限するようにサービスを設定できます。

1. Configuration Manager の Web コンソールを開きます。 `https://[aem_server]:[port]/system/console/configMgr` にアクセスします。
1. **[!UICONTROL Day CQ DAM Asset Upload Restriction]** サービスを編集モードで開きます。 デフォルトでは、「**Allow all MIME**」オプションがオンになっており、すべての MIME タイプのファイルのアップロードが許可されます。

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. ユーザーがアップロードできるファイルを特定の MIME タイプのみに制限するには、「**[!UICONTROL すべての MIME を許可]**」オプションをオフにして、「**[!UICONTROL 許可されたアセットの MIME（regex）]**」フィールドに許可する MIME タイプを正規表現を使用して指定します。

   ![chlimage_1-379](assets/chlimage_1-379.png)

1. 「**[!UICONTROL 保存]**」をクリックして、変更を保存します。 許可されたMIME タイプにMIME文字列を指定すると、これらのフィールドで設定されたMIME文字列と一致しないMIME タイプを持つアセットのアップロード操作が失敗します。
