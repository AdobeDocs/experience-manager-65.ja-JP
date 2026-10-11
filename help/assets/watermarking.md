---
title: デジタルアセットへの透かしの追加
description: 透かし処理機能を使用して、アセットにデジタル透かしを追加する方法について学びます。
contentOwner: AG
role: User, Admin
feature: Asset Management
exl-id: bc0cfb0e-3f70-4377-8831-326a7cae73bd
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
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 100%
---
# デジタルアセットに透かしをつける {#watermarking}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/watermark-assets.html?lang=ja) |
| AEM 6.5 | この記事 |

[!DNL Adobe Experience Manager Assets] ではアセットにデジタル透かしを追加することができ、ユーザーがアセットの信頼性や著作権の所有権を確認できるようになります。 [!DNL Experience Manager Assets] では、PNG および JPEG ファイル上の透かしとしてテキストを使用できます。

アセットに透かしを適用できるようにするには、[!UICONTROL DAM アセットの更新] ワークフローに透かしステップを追加してください。

1. [!DNL Experience Manager] ユーザーインターフェイスにアクセスし、**[!UICONTROL ツール]**／**[!UICONTROL ワークフロー]**／**[!UICONTROL モデル]**&#x200B;に移動してください。
1. **[!UICONTROL ワークフローモデル]**&#x200B;ページで、**[!UICONTROL DAM アセットの更新]**&#x200B;ワークフローを選択し、**[!UICONTROL 編集]**&#x200B;をクリックしてください。

1. サイドパネルから、**[!UICONTROL 透かしを追加]**&#x200B;ステップを [!UICONTROL DAM アセットの更新]ワークフローにドラッグしてください。

   ![[!UICONTROL 透かしを追加]手順をドラッグして、[!UICONTROL DAM アセットの更新]ワークフローに追加](assets/add_watermark_step_aem_assets.png)

   *図：[!UICONTROL 透かしを追加]手順をドラッグして [!UICONTROL DAM アセットの更新]ワークフローに追加します。*

   >[!NOTE]
   >
   >[!UICONTROL 透かしを追加]手順は、[!UICONTROL サムネールを処理]手順の前の任意の位置に配置します。

1. 「**[!UICONTROL 透かしを追加]**」ステップを開いて、プロパティを表示します。
1. 「**[!UICONTROL 引数]**」タブで、各種フィールド（テキスト、フォントタイプ、サイズ、カラー、位置、向きなど）に有効な値を指定します。 変更を確定するには、「**[!UICONTROL 完了]**」をクリックしてください。

   ![以下に「透かしを追加」ステップの引数を指定[!DNL Assets]](assets/arguments_add_watermark_aem_assets.png)

   *図：[!DNL Assets]において「透かしを追加」ステップの引数を指定*

1. 透かしステップを追加した **[!UICONTROL DAM アセットの更新]**&#x200B;ワークフローを保存します。
1. [!DNL Assets] ユーザーインターフェイスから、サンプルアセットをアップロードします。 透かしが、上記手順で設定した位置に、指定したフォントサイズやカラーなどの設定で表示されます。

プログラムで、あるいは動的情報を使用して PDF ドキュメントに透かしを付ける場合は、 [Experience Manager ドキュメントサービス](/help/forms/using/overview-aem-document-services.md)の使用を検討してください。

## ヒントと制限事項 {#tips-limitations}

* テキストベースの透かしのみがサポートされます。 [!UICONTROL 透かしプロセスの追加]を作成する際には画像をアップロードできますが、画像は透かしとして使用されません。
* 透かしを適用できるのは、PNG ファイルと JPEG ファイルのみです。 その他のアセット形式には透かしは入りません。
