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

[!DNL Adobe Experience Manager Assets]に存在するアセットをアップロードしようとすると、重複検出機能によって重複と認識されます。 重複項目の検出はデフォルトで無効になっています。この機能を有効にするには、次の手順を実行します。

1. [!DNL Experience Manager]にアクセスして&lt;a0/> Webコンソール設定ページを開きます。`https://[aem_server]:[port]/system/console/configMgr`
1. サーブレット&#x200B;**[!UICONTROL Day CQ DAM Create Asset]**&#x200B;の設定を編集します。
1. 「**[!UICONTROL 重複を検出]**」オプションを選択し、「**[!UICONTROL 保存]**」をクリックします。

   ![サーブレットで「重複項目の検出」オプションを選択](assets/chlimage_1-377.png)

   *図：サーブレットで「重複を検出」オプションを選択します。*

検出重複機能が[!DNL Assets]で有効になりました。 ユーザーが[!DNL Experience Manager]に存在するアセットをアップロードしようとすると、システムは競合がないかどうかを確認し、それを示します。 アセットは、`jcr:content/metadata/dam:sha1`に保存されているSHA-1ハッシュを使用して識別されます。つまり、ファイル名に関係なく、重複アセットが検出されます。

>[!MORELIKETHIS]
>
>* [既存のリポジトリの重複アセット（コミュニティメンバーのチュートリアル）](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)

