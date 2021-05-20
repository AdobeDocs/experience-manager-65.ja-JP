---
title: Apache Tikaを使用したアセットのMIMEタイプの検出
description: 'Apache Tikaを有効にして、アップロード操作中にファイル拡張子ではなくコンテンツストリームからアセットのMIMEタイプを検出するのに役立ちます。 [!DNL Experience Manager Assets] '
contentOwner: AG
role: Administrator, Architect
feature: メタデータ，開発者ツール，アセット管理
exl-id: a312466d-8d84-4c94-af85-1549afc61aed
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 11%

---

# [!DNL Apache Tika] {#detecting-mime-type-of-assets-using-apache-tika}を使用してアセットのMIMEタイプを検出する

通常、[!DNL Adobe Experience Manager Assets]は、アップロードするアセットのMIMEタイプをファイル拡張子から検出します。

[!DNL Apache Tika]を使用してアセットをアップロードする場合、[!DNL Assets]は、アップロード中に、ファイル拡張子ではなくコンテンツストリームからMIMEタイプを検出します。

この機能はデフォルトでは無効になっています。この機能を有効にするには、[!UICONTROL Configuration Manager]から&#x200B;**[!UICONTROL Day CQ DAM Mime Type]**&#x200B;サービスを設定します。

>[!NOTE]
>
>[!DNL Apache Tika]ライブラリを使用したMIMEタイプ検出は、リソースを大量に消費する操作です。

1. Configuration Manager Webコンソールを開くには、`https://[aem_server]:[port]/system/console/configMgr`にアクセスします。

1. サービスのリストで、**[!UICONTROL Day CQ DAM Mime Type Service]**&#x200B;を探し、**[!UICONTROL 「]**&#x200B;を編集」をクリックします。

1. **[!UICONTROL 「コンテンツからMIMEを検出]** 」オプションを選択して、アップロードされたアセットの解析を有効にし、ファイル拡張子を無視してMIMEタイプを判断します。 デフォルトでは、このオプションはオフになっています。

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. 「**[!UICONTROL 保存]**」をクリックして、変更を保存します。
