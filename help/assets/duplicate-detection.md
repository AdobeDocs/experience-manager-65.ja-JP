---
title: 重複アセットの検出の有効化
description: 重複アセットの検出を有効にする方法をExperience Managerします。
contentOwner: AG
role: Business Practitioner, Administrator
feature: アセット管理、アセットレポート
exl-id: a403d60e-2193-4835-8f37-4a40f2d01819
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 21%

---

# 重複アセットの検出の有効化 {#enable-detection-of-duplicate-assets}

[!DNL Adobe Experience Manager Assets]に存在するアセットをアップロードしようとすると、重複の検出機能によって重複と見なされます。 重複項目の検出はデフォルトで無効になっています。この機能を有効にするには、次の手順を実行します。

1. `https://[aem_server]:[port]/system/console/configMgr`にアクセスして、[!DNL Experience Manager] Webコンソール設定ページを開きます。
1. サーブレット&#x200B;**[!UICONTROL Day CQ DAM Create Asset]**&#x200B;の設定を編集します。
1. 「**[!UICONTROL 重複を検出]**」オプションを選択し、「**[!UICONTROL 保存]**」をクリックします。

   ![サーブレットで「重複項目の検出」オプションを選択](assets/chlimage_1-377.png)

   *図：サーブレットで「重複を検出」オプションを選択します。*

重複の検出機能が[!DNL Assets]で有効になりました。 ユーザーが[!DNL Experience Manager]に存在するアセットをアップロードしようとすると、競合がないかどうかがチェックされ、その旨が示されます。 アセットは、`jcr:content/metadata/dam:sha1`に保存されているSHA-1ハッシュを使用して識別されます。つまり、重複するアセットは、ファイル名に関係なく検出されます。

>[!MORELIKETHIS]
>
>* [既存のリポジトリ内のアセットの複製（コミュニティメンバーのチュートリアル）](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)

