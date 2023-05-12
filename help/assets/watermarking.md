---
title: デジタルアセットへの透かしの追加
description: 透かし処理機能を使用して、アセットにデジタル透かしを追加する方法について学びます。
contentOwner: AG
role: User, Admin
feature: Asset Management
exl-id: bc0cfb0e-3f70-4377-8831-326a7cae73bd
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 90%

---

# デジタルアセットに透かしをつける {#watermarking}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/watermark-assets.html?lang=ja) |
| AEM 6.5 | この記事 |

[!DNL Adobe Experience Manager Assets] では、アセットにデジタル透かしを追加し、ユーザーがアセットの信頼性や著作権の所有権を確認できるようにします。[!DNL Experience Manager Assets] では、PNG および JPEG ファイル上の透かしとしてテキストを使用できます。

アセットに透かしを適用できるようにするには、[!UICONTROL DAM アセットの更新] ワークフローに透かしステップを追加してください。

1. [!DNL Experience Manager] ユーザインターフェイスにアクセスし、**[!UICONTROL ツール]**／**[!UICONTROL ワークフロー]**／**[!UICONTROL モデル]**&#x200B;に移動してください。 
1. **[!UICONTROL ワークフローモデル]**&#x200B;ページで、**[!UICONTROL DAM アセットの更新]**&#x200B;ワークフローを選択し、**[!UICONTROL 編集]**&#x200B;をクリックしてください。

1. サイドパネルから、**[!UICONTROL 透かしを追加]**&#x200B;ステップを [!UICONTROL DAM アセットの更新]ワークフローにドラッグしてください。

   ![[!UICONTROL 透かしを追加]手順をドラッグして、[!UICONTROL DAM アセットの更新]ワークフローに追加](assets/add_watermark_step_aem_assets.png)

   *図：[!UICONTROL 透かしを追加]手順をドラッグして [!UICONTROL DAM アセットの更新]ワークフローに追加します。*

   >[!NOTE]
   >
   >[!UICONTROL 透かしを追加]手順は、[!UICONTROL サムネールを処理]手順の前の任意の位置に配置します。

1. を開きます。 **[!UICONTROL 透かしを追加]** ステップを使用してプロパティを表示します。
1. 内 **[!UICONTROL 引数]** 「 」タブで、各種フィールドに有効な値（テキスト、フォントタイプ、サイズ、色、位置、向きなど）を指定します。 変更を確定するには、「**[!UICONTROL 完了]**」をクリックしてください。

   ![以下に「透かしを追加」ステップの引数を指定[!DNL Assets]](assets/arguments_add_watermark_aem_assets.png)

   *図：[!DNL Assets]において「透かしを追加」ステップの引数を指定*

1. 透かしステップを追加した **[!UICONTROL DAM アセットの更新]**&#x200B;ワークフローを保存します。
1. [!DNL Assets] ユーザーインターフェイスから、サンプルアセットをアップロードします。透かしがフォントサイズやカラーなどと共に、上記手順で設定した位置に表示されます。

プログラムで、あるいは動的情報を使用して PDF ドキュメントに透かしを付ける場合は、 [Experience Manager ドキュメントサービス](/help/forms/using/overview-aem-document-services.md)の使用を検討してください。

## ヒントと制限事項 {#tips-limitations}

* テキストベースの透かしのみがサポートされます。 [!UICONTROL 透かしプロセスの追加]を作成する際には画像をアップロードできますが、画像は透かしとして使用されません。
* 透かしの使用は、PNG ファイルと JPEG ファイルのみでサポートされています。 その他のアセット形式には透かしは入りません。
