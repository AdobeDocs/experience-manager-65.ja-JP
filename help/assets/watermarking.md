---
title: デジタルアセットへの透かしの追加
description: 透かし処理機能を使用して、アセットにデジタル透かしを追加する方法について学びます。
contentOwner: AG
role: User, Admin
feature: Asset Management
exl-id: bc0cfb0e-3f70-4377-8831-326a7cae73bd
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 100%

---

# デジタルアセットに透かしをつける {#watermarking}

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

1. 「**[!UICONTROL 透かしを追加]**」ステップを開いて、プロパティを表示します。
1. 「**[!UICONTROL 引数]**」タブで、各種フィールド（テキスト、フォントタイプ、サイズ、カラー、位置、向きなど）に有効な値を指定します。変更を確定するには、「**[!UICONTROL 完了]**」をクリックしてください。

   ![以下に「透かしを追加」ステップの引数を指定[!DNL Assets]](assets/arguments_add_watermark_aem_assets.png)

   *図：[!DNL Assets]において「透かしを追加」ステップの引数を指定*

1. 透かしステップを追加した **[!UICONTROL DAM アセットの更新]**&#x200B;ワークフローを保存します。
1. [!DNL Assets] ユーザーインターフェイスから、サンプルアセットをアップロードします。透かしがフォントサイズやカラーなどと共に、上記手順で設定した位置に表示されます。

プログラムで、あるいは動的情報を使用して PDF ドキュメントに透かしを付ける場合は、 [Experience Manager ドキュメントサービス](/help/forms/using/overview-aem-document-services.md)の使用を検討してください。

## ヒントと制限事項 {#tips-limitations}

* テキストベースの透かしのみがサポートされます。 [!UICONTROL 透かしプロセスの追加]を作成する際には画像をアップロードできますが、画像は透かしとして使用されません。
* 透かしの使用は、PNG ファイルと JPEG ファイルのみでサポートされています。 その他のアセット形式には透かしは入りません。
