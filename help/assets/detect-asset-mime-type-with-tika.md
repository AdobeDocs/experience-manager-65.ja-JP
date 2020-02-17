---
title: Apache Tikaを使用してアセットのMIMEタイプを検出する
description: Apache Tika を使用して、AEM Assets がアセットの MIME タイプをファイル拡張子ではなくコンテンツストリームから、アップロード操作中に検出できるようにします。
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Detect MIME type of assets using Apache Tika {#detecting-mime-type-of-assets-using-apache-tika}

通常、Adobe Experience Manager（AEM）Assets は、ユーザーがアップロードしたアセットの MIME タイプを、アセットのファイル拡張子から検出します。

Apache Tika を使用してアセットをアップロードすると、AEM Assets は、アセットの MIME タイプをファイル拡張子ではなくコンテンツストリームから、アップロード操作中に検出します。

この機能はデフォルトでは無効になっています。To enable the feature, configure the **[!UICONTROL Day CQ DAM Mime Type]** service from [!UICONTROL Configuration Manager].

>[!NOTE]
>
>Apache Tikaライブラリを使用したMIMEタイプの検出は、リソースを大量に消費する操作です。

1. Configuration Manager webコンソールを開くには、にアクセスしま `https://[aem_server]:[port]/system/console/configMgr`す。
1. From the list of services, locate **[!UICONTROL Day CQ DAM Mime Type Service]** and tap **[!UICONTROL Edit]** beside it to open it in Edit mode.

1. Select the **[!UICONTROL Detect MIME from content]** option to enable the parsing of uploaded assets to determine their MIME type while ignoring file extensions. デフォルトでは、このオプションはオフになっています。

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. Click/tap **[!UICONTROL Save]** to save the changes.
