---
title: 重複アセットの検出の有効化
description: Experience Manager内の重複アセットを検出できるようにする方法を説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 22%

---


# 重複アセットの検出の有効化 {#enable-detection-of-duplicate-assets}

If you attempt to upload an asset that exists in [!DNL Adobe Experience Manager Assets], the duplicate detection feature identifies it as duplicate. 重複項目の検出はデフォルトで無効になっています。この機能を有効にするには、次の手順を実行します。

1. にアクセスして、 [!DNL Experience Manager] Webコンソール設定ページを開き `https://[aem_server]:[port]/system/console/configMgr`ます。
1. Edit the configuration for the servlet **[!UICONTROL Day CQ DAM Create Asset]**.
1. Select the **[!UICONTROL detect duplicate]** option, and click **[!UICONTROL Save]**.

   ![サーブレットで「重複項目の検出」オプションを選択](assets/chlimage_1-377.png)

   *図：サーブレットで「重複を検出」オプションを選択します。*

The detect duplicate feature is now enabled in [!DNL Assets]. When a user attempts to upload an asset that exists in [!DNL Experience Manager], the system checks for conflict and indicates it. The assets are identified using SHA-1 hash stored at `jcr:content/metadata/dam:sha1`, which means duplicate assets are detected irrespective of the filenames.

>[!MORELIKETHIS]
>
>* [既存のリポジトリの重複アセット（コミュニティメンバーのチュートリアル）](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)

