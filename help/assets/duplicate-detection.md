---
title: 重複アセットの検出の有効化
description: Experience Manager で重複アセットの検出を有効にする方法について説明します。
contentOwner: AG
role: User, Admin
feature: Asset Management,Asset Reports
exl-id: a403d60e-2193-4835-8f37-4a40f2d01819
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 100%

---

# 重複アセットの検出の有効化 {#enable-detection-of-duplicate-assets}

[!DNL Adobe Experience Manager Assets] に存在するアセットをアップロードしようとすると、重複項目検出機能によって重複として識別されます。重複項目の検出はデフォルトで無効になっています。この機能を有効にするには、次の手順を実行します。

1. `https://[aem_server]:[port]/system/console/configMgr` にアクセスして、[!DNL Experience Manager] web コンソール構成ページを開きます。
1. サーブレットの **[!UICONTROL Day CQ DAM アセット作成]**&#x200B;の設定を編集します。
1. 「**[!UICONTROL 重複項目の検出]**」オプションを選択し、「**[!UICONTROL 保存]**」をクリックします。

   ![サーブレットで「重複項目の検出」オプションを選択](assets/chlimage_1-377.png)

   *サーブレットで「重複項目の検出」オプションを選択します。*

これで、重複項目検出機能が [!DNL Assets] で有効になります。[!DNL Experience Manager] に存在するアセットをアップロードしようとすると、システムが競合をチェックして表示します。`jcr:content/metadata/dam:sha1` に保存されている SHA-1 ハッシュを使用して、アセットが識別されます。つまり、重複アセットはファイル名に関係なく検出されます。

>[!MORELIKETHIS]
>
>* [既存リポジトリでの重複アセット（コミュニティメンバー提供のチュートリアル）](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)

