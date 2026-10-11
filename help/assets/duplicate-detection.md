---
title: 重複アセットの検出の有効化
description: Experience Manager で重複アセットの検出を有効にする方法について説明します。
contentOwner: AG
role: User, Admin
feature: Asset Management,Asset Reports
exl-id: a403d60e-2193-4835-8f37-4a40f2d01819
hide: true
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: 7d2b2ec8-499c-5434-9ffd-9218cd71f683
    internal-label: Asset Management
  - id: ac365bec-0634-4744-9473-c42f47320593
    internal-label: Asset management and governance
subfeature_v2:
  - id: c29e3a96-cd2b-4e21-b382-a8279aa04553
    internal-label: Asset reports
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 100%
---
# 重複アセットの検出の有効化 {#enable-detection-of-duplicate-assets}

[!DNL Adobe Experience Manager Assets] に存在するアセットをアップロードしようとすると、重複項目検出機能によって重複として識別されます。 重複項目の検出はデフォルトで無効になっています。 この機能を有効にするには、次の手順を実行します。

1. `https://[aem_server]:[port]/system/console/configMgr` にアクセスして、[!DNL Experience Manager] web コンソール構成ページを開きます。
1. サーブレットの **[!UICONTROL Day CQ DAM アセット作成]**&#x200B;の設定を編集します。
1. 「**[!UICONTROL 重複項目の検出]**」オプションを選択し、「**[!UICONTROL 保存]**」をクリックします。

   ![サーブレットで「重複項目の検出」オプションを選択](assets/chlimage_1-377.png)

   *サーブレットで「重複項目の検出」オプションを選択します。*

これで、重複項目検出機能が [!DNL Assets] で有効になります。 [!DNL Experience Manager] に存在するアセットをアップロードしようとすると、システムが競合をチェックして表示します。 `jcr:content/metadata/dam:sha1` に保存されている SHA-1 ハッシュを使用して、アセットが識別されます。つまり、重複アセットはファイル名に関係なく検出されます。

>[!MORELIKETHIS]
>
>* [既存リポジトリでの重複アセット（コミュニティメンバー提供のチュートリアル）](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)
>* [AEM as a Cloud Service の重複アセットを検出](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/detect-duplicate-assets.html?lang=ja)
