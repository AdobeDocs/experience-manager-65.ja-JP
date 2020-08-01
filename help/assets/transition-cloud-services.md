---
title: フォルダーへの翻訳クラウドサービスの適用
description: フォルダーへの翻訳クラウドサービスの適用
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 73%

---


# フォルダーへの翻訳クラウドサービスの適用 {#applying-translation-cloud-services-to-folders}

[!DNL Adobe Experience Manager] 任意の翻訳プロバイダーからクラウドベースの翻訳サービスを利用して、必要に応じてアセットが翻訳されていることを確認できます。

翻訳クラウドサービスをアセットフォルダーに直接適用できるので、翻訳ワークフローの間もずっとアセットを利用できます。

## 翻訳サービスの適用 {#applying-the-translation-services}

翻訳クラウドサービスをアセットフォルダーに直接適用すると、翻訳ワークフローの作成または変更時に翻訳サービスを設定する必要がなくなります。

1. From the [!DNL Assets] user interface, select the folder to which you want to apply translation services.
1. From the toolbar, click **[!UICONTROL Properties]** to display the **[!UICONTROL Folder Properties]** page.

   ![chlimage_1-215](assets/chlimage_1-215.png)

1. 「**[!UICONTROL Cloud Services]**」タブに移動します。
1. 「Cloud Services の設定」リストから目的の翻訳プロバイダーを選択します。例えば、Microsoft の翻訳サービスを利用する場合は、「**[!UICONTROL Microsoft Translator]**」を選択します。

   ![chlimage_1-216](assets/chlimage_1-216.png)

1. 翻訳プロバイダーのコネクタを選択します。

   ![chlimage_1-217](assets/chlimage_1-217.png)

1. From the toolbar, click **[!UICONTROL Save]**, and then click **[!UICONTROL OK]** to close the dialog.The translation service is applied to the folder.

## カスタム翻訳コネクタの適用  {#applying-custom-translation-connector}

翻訳ワークフローで使用する翻訳サービスにカスタムコネクタを適用する場合、カスタムコネクタを適用するには、まずパッケージマネージャーからコネクタをインストールします。次に、Cloud Services コンソールからコネクタを設定します。コネクタを設定すると、[翻訳サービスの適用](transition-cloud-services.md#applying-the-translation-services)で説明されている「Cloud Services」タブのコネクタのリストに表示されるようになります。カスタムコネクタを適用し、翻訳ワークフローを実行すると、翻訳プロジェクトの「**[!UICONTROL 翻訳の概要]**」タイルの「**[!UICONTROL プロバイダー]**」と「**[!UICONTROL メソッド]**」という見出しの下にコネクタの詳細が表示されます。

1. パッケージマネージャーからコネクタをインストールします。
1. Click the [!DNL Experience Manager] logo, and navigate to **[!UICONTROL Tools]** > **[!UICONTROL Deployment]** > **[!UICONTROL Cloud Services]**.
1. インストールしたコネクタを **[!UICONTROL Cloud Services]** ページの「**[!UICONTROL サードパーティのサービス]**」の下で探します。

   ![chlimage_1-218](assets/chlimage_1-218.png)

1. Click the **[!UICONTROL Configure now]** link to open the **[!UICONTROL Create Configuration]** dialog.

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. Specify a title and a name for the connector, and then click **[!UICONTROL Create]**. [翻訳サービスの適用](#applying-the-translation-services)のステップ 5 で説明されている「**[!UICONTROL Cloud Services]**」タブのコネクタリストにカスタムコネクタが表示されます。
1. カスタムコネクタを適用したら、[翻訳プロジェクトの作成](translation-projects.md)で説明されている翻訳ワークフローを実行します。**[!UICONTROL プロジェクト]**&#x200B;コンソールで、翻訳プロジェクトの「**[!UICONTROL 翻訳の概要]**」タイルに表示されているコネクタの詳細を確認します。

   ![chlimage_1-220](assets/chlimage_1-220.png)
