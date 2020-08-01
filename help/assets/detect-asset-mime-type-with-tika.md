---
title: Apache Tikaを使用してアセットのMIMEタイプを検出する
description: Enable Apache Tika to help [!DNL Experience Manager Assets] detect the MIME type of assets from the content stream during the upload operation instead of the file extension.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 11%

---


# 次を使用してアセットのMIMEタイプを検出する [!DNL Apache Tika] {#detecting-mime-type-of-assets-using-apache-tika}

通常、は、ファイルの拡張子からアップロードするアセットのMIMEタイプを [!DNL Adobe Experience Manager Assets] 検出します。

If you use [!DNL Apache Tika] to upload assets, [!DNL Assets] detects their MIME type from the content stream during the upload operation instead of the file extension.

この機能はデフォルトでは無効になっています。To enable the feature, configure the **[!UICONTROL Day CQ DAM Mime Type]** service from [!UICONTROL Configuration Manager].

>[!NOTE]
>
>MIME type detection using the [!DNL Apache Tika] library is a resource-intensive operation.

1. Configuration Manager Webコンソールを開くには、にアクセスし `https://[aem_server]:[port]/system/console/configMgr`ます。

1. サービスのリストから、 **[!UICONTROL Day CQ DAM Mime Type Service]** を探し、「 **[!UICONTROL 編集]**」をクリックします。

1. Select the **[!UICONTROL Detect MIME from content]** option to enable the parsing of uploaded assets to determine their MIME type while ignoring file extensions. デフォルトでは、このオプションはオフになっています。

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. 「**[!UICONTROL 保存]**」をクリックして、変更を保存します。
