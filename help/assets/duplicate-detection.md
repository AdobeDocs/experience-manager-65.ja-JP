---
title: 重複アセットの検出の有効化
description: Experience Managerで重複アセットを検出する方法を説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 26%

---


# 重複アセットの検出の有効化 {#enable-detection-of-duplicate-assets}

Adobe Experience Manager Assetsに存在するアセットをアップロードしようとすると、重複検出機能によって重複として識別されます。 重複項目の検出はデフォルトで無効になっています。この機能を有効にするには、次の手順を実行します。

1. にアクセスして、Experience Manager Web Console Configurationページを開き `https://[aem_server]:[port]/system/console/configMgr`ます。
1. Edit the configuration for the servlet **[!UICONTROL Day CQ DAM Create Asset]**.
1. Select the **[!UICONTROL detect duplicate]** option, and click **[!UICONTROL Save]**.

   ![サーブレットで「重複項目の検出」オプションを選択](assets/chlimage_1-377.png)

   *図： サーブレットの「重複を検出」オプションを選択*

これで、重複項目検出機能が Assets で有効になります。ユーザーがExperience Managerに存在するアセットをアップロードしようとすると、システムは競合がないかどうかを確認し、それを示します。 The assets are identified using SHA-1 hash stored at `jcr:content/metadata/dam:sha1`, which means duplicate assets are detected irrespective of the filenames.

>[!MORELIKETHIS]
>
>* [既存のリポジトリの重複アセット（コミュニティメンバーのチュートリアル）](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)

