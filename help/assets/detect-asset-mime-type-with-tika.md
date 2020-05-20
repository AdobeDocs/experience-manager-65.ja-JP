---
title: Apache Tikaを使用してアセットのMIMEタイプを検出する
description: Apache Tika を使用して、AEM Assets がアセットの MIME タイプをファイル拡張子ではなくコンテンツストリームから、アップロード操作中に検出できるようにします。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 23d19d9656d61874cd00a9a2473092be0c53b8f8
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 50%

---


# Detect MIME type of assets using Apache Tika {#detecting-mime-type-of-assets-using-apache-tika}

通常、Adobe Experience Manager（AEM）Assets は、ユーザーがアップロードしたアセットの MIME タイプを、アセットのファイル拡張子から検出します。

Apache Tika を使用してアセットをアップロードすると、AEM Assets は、アセットの MIME タイプをファイル拡張子ではなくコンテンツストリームから、アップロード操作中に検出します。

この機能はデフォルトでは無効になっています。To enable the feature, configure the **[!UICONTROL Day CQ DAM Mime Type]** service from [!UICONTROL Configuration Manager].

>[!NOTE]
>
>Apache Tikaライブラリを使用したMIMEタイプの検出は、リソースを大量に消費する操作です。

1. Configuration Manager Webコンソールを開くには、にアクセスし `https://[aem_server]:[port]/system/console/configMgr`ます。

1. サービスのリストから、 **[!UICONTROL Day CQ DAM Mime Type Service]** を探し、「 **[!UICONTROL 編集]**」をクリックします。

1. Select the **[!UICONTROL Detect MIME from content]** option to enable the parsing of uploaded assets to determine their MIME type while ignoring file extensions. デフォルトでは、このオプションはオフになっています。

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. 「**[!UICONTROL 保存]**」をクリックして、変更を保存します。
