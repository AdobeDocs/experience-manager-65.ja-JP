---
title: Apache Tikaを使用してアセットのMIMEタイプを検出する
description: Apache Tikaを有効にすると、Experience Manager Assetsが、アップロード操作中にファイル拡張子ではなく、コンテンツストリームからアセットのMIMEタイプを検出できるようになります。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 10%

---


# Detect MIME type of assets using Apache Tika {#detecting-mime-type-of-assets-using-apache-tika}

通常、Adobe Experience Manager Assetsは、ファイルの拡張子からアップロードするアセットのMIMEタイプを検出します。

Apache Tikaを使用してアセットをアップロードする場合、Assetsは、アップロード操作中に、ファイル拡張子ではなく、コンテンツストリームからMIMEタイプを検出します。

この機能はデフォルトでは無効になっています。To enable the feature, configure the **[!UICONTROL Day CQ DAM Mime Type]** service from [!UICONTROL Configuration Manager].

>[!NOTE]
>
>Apache Tikaライブラリを使用したMIMEタイプの検出は、リソースを大量に消費する操作です。

1. Configuration Manager Webコンソールを開くには、にアクセスし `https://[aem_server]:[port]/system/console/configMgr`ます。

1. サービスのリストから、 **[!UICONTROL Day CQ DAM Mime Type Service]** を探し、「 **[!UICONTROL 編集]**」をクリックします。

1. Select the **[!UICONTROL Detect MIME from content]** option to enable the parsing of uploaded assets to determine their MIME type while ignoring file extensions. デフォルトでは、このオプションはオフになっています。

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. 「**[!UICONTROL 保存]**」をクリックして、変更を保存します。
