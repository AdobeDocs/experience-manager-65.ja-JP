---
title: Apache Tika を使用したアセットの MIME タイプの検出
description: Apache Tikaを有効にして、[!DNL Experience Manager Assets]がファイル拡張子ではなく、アップロード操作中にコンテンツストリームからアセットのMIME タイプを検出できるようにします。
contentOwner: AG
role: Admin, Developer
feature: Metadata,Developer Tools,Asset Management
exl-id: a312466d-8d84-4c94-af85-1549afc61aed
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: f2d27a5f-0d67-4d85-8a24-86a8d8a3574b
    internal-label: Developer tools
  - id: 7d2b2ec8-499c-5434-9ffd-9218cd71f683
    internal-label: Asset Management
  - id: ac365bec-0634-4744-9473-c42f47320593
    internal-label: Asset management and governance
subfeature_v2:
  - id: ed6971a3-2c12-4fd2-81f4-ff329c416250
    internal-label: Metadata
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 85%
---
# [!DNL Apache Tika] を使用したアセットの MIME タイプの検出 {#detecting-mime-type-of-assets-using-apache-tika}

通常、[!DNL Adobe Experience Manager Assets] はアップロードするアセットの MIME タイプをファイル拡張子から検出します。

[!DNL Apache Tika] を使用してアセットをアップロードすると、[!DNL Assets] はアセットの MIME タイプをファイル拡張子ではなくコンテンツストリームから、アップロード操作中に検出します。

この機能はデフォルトでは無効になっています。 この機能を有効にするには、[!UICONTROL Configuration Manager] で **[!UICONTROL Day CQ DAM Mime タイプ]**&#x200B;サービスを設定してください。

>[!NOTE]
>
>[!DNL Apache Tika] ライブラリを使用した MIME タイプ検出は、リソースを集中的に消費する操作です。

1. Configuration Manager web コンソールを開くには、 `https://[aem_server]:[port]/system/console/configMgr` にアクセスしてください。

1. サービスのリストから、**[!UICONTROL Day CQ DAM Mime タイプサービス]**&#x200B;をクリックしてから、「 **[!UICONTROL 編集]**」をクリックしてください。

1. アップロードされたアセットの解析を有効にし、ファイルの拡張子を無視して MIME タイプを検出するには、「**[!UICONTROL コンテンツから MIME タイプを検出]**」オプションを選択してください。 デフォルトでは、このオプションはオフになっています。

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. 「**[!UICONTROL 保存]**」をクリックして、変更を保存します。
