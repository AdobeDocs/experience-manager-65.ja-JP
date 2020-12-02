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

1. [!DNL Assets]ユーザーインターフェイスから、翻訳サービスを適用するフォルダーを選択します。
1. ツールバーで、**[!UICONTROL プロパティ]**&#x200B;をクリックして&#x200B;**[!UICONTROL フォルダーのプロパティ]**&#x200B;ページを表示します。

   ![chlimage_1-215](assets/chlimage_1-215.png)

1. 「**[!UICONTROL Cloud Services]**」タブに移動します。
1. 「Cloud Services の設定」リストから目的の翻訳プロバイダーを選択します。例えば、Microsoft の翻訳サービスを利用する場合は、「**[!UICONTROL Microsoft Translator]**」を選択します。

   ![chlimage_1-216](assets/chlimage_1-216.png)

1. 翻訳プロバイダーのコネクタを選択します。

   ![chlimage_1-217](assets/chlimage_1-217.png)

1. ツールバーで[**[!UICONTROL 保存]**]をクリックし、[**[!UICONTROL OK]**]をクリックしてダイアログを閉じます。翻訳サービスがフォルダに適用されます。

## カスタム翻訳コネクタの適用  {#applying-custom-translation-connector}

翻訳ワークフローで使用する翻訳サービスにカスタムコネクタを適用する場合、カスタムコネクタを適用するには、まずパッケージマネージャーからコネクタをインストールします。次に、Cloud Services コンソールからコネクタを設定します。コネクタを設定すると、[翻訳サービスの適用](transition-cloud-services.md#applying-the-translation-services)で説明されている「Cloud Services」タブのコネクタのリストに表示されるようになります。カスタムコネクタを適用し、翻訳ワークフローを実行すると、翻訳プロジェクトの「**[!UICONTROL 翻訳の概要]**」タイルの「**[!UICONTROL プロバイダー]**」と「**[!UICONTROL メソッド]**」という見出しの下にコネクタの詳細が表示されます。

1. パッケージマネージャーからコネクタをインストールします。
1. [!DNL Experience Manager]ロゴをクリックし、**[!UICONTROL ツール]**/**[!UICONTROL 導入]**/**[!UICONTROL Cloud Services]**&#x200B;に移動します。
1. インストールしたコネクタを **[!UICONTROL Cloud Services]** ページの「**[!UICONTROL サードパーティのサービス]**」の下で探します。

   ![chlimage_1-218](assets/chlimage_1-218.png)

1. 「**[!UICONTROL 今すぐ設定]**」リンクをクリックして、**[!UICONTROL 設定を作成]**&#x200B;ダイアログを開きます。

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. コネクタのタイトルと名前を指定し、**[!UICONTROL 作成]**&#x200B;をクリックします。 [翻訳サービスの適用](#applying-the-translation-services)のステップ 5 で説明されている「**[!UICONTROL Cloud Services]**」タブのコネクタリストにカスタムコネクタが表示されます。
1. カスタムコネクタを適用したら、[翻訳プロジェクトの作成](translation-projects.md)で説明されている翻訳ワークフローを実行します。**[!UICONTROL プロジェクト]**&#x200B;コンソールで、翻訳プロジェクトの「**[!UICONTROL 翻訳の概要]**」タイルに表示されているコネクタの詳細を確認します。

   ![chlimage_1-220](assets/chlimage_1-220.png)
