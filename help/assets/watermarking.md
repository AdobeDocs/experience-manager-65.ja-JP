---
title: デジタルアセットへの透かしの追加
description: 透かし処理機能を使用して、アセットにデジタル透かしを追加する方法について説明します。
contentOwner: AG
role: Business Practitioner, Administrator
feature: アセット管理
exl-id: bc0cfb0e-3f70-4377-8831-326a7cae73bd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 31%

---

# デジタルアセットの透かしの設定 {#watermarking}

[!DNL Adobe Experience Manager Assets] では、アセットにデジタル透かしを追加して、アセットの信頼性と著作権の所有権を確認できます。[!DNL Experience Manager Assets] では、PNG および JPEG ファイル上の透かしとしてテキストを使用できます。

アセットに透かしを適用できるようにするには、[!UICONTROL DAMアセットの更新]ワークフローに透かし処理ステップを追加します。

1. [!DNL Experience Manager]ユーザーインターフェイスにアクセスし、**[!UICONTROL ツール]** / **[!UICONTROL ワークフロー]** / **[!UICONTROL モデル]**&#x200B;に移動します。
1. **[!UICONTROL ワークフローモデル]**&#x200B;ページで、**[!UICONTROL DAMアセットの更新]**&#x200B;ワークフローを選択し、「**[!UICONTROL 編集]**」をクリックします。

1. サイドパネルから、「**[!UICONTROL 透かしを追加]**」ステップを[!UICONTROL DAMアセットの更新]ワークフローにドラッグします。

   ![「 Watermarkstepを追 [!UICONTROL 加」を] ドラッグし、「 DAMアセットの更 [!UICONTROL 新」アセットフローに] 追加します](assets/add_watermark_step_aem_assets.png)

   *図：「 Watermarkstepを追 [!UICONTROL 加」を] ドラッグし、「 DAMアセットの更 [!UICONTROL 新」アセットフローに追] 加します。*

   >[!NOTE]
   >
   >[!UICONTROL 透かしを追加]ステップを、[!UICONTROL サムネールを処理]ステップの前の任意の場所に配置します。

1. 「**[!UICONTROL 透かしを追加]**」ステップを開いて、プロパティを表示します。
1. 「**[!UICONTROL 引数]**」タブで、各種フィールド（テキスト、フォントタイプ、サイズ、カラー、位置、向きなど）に有効な値を指定します。変更を確定するには、「**[!UICONTROL 完了]**」をクリックします。

   ![ における「透かしを追加」ステップの引数の指定[!DNL Assets]](assets/arguments_add_watermark_aem_assets.png)

   *図：の透かしを追加手順で引数を指定しま [!DNL Assets]す。*

1. 透かしステップを追加した&#x200B;**[!UICONTROL DAMアセットの更新]**&#x200B;ワークフローを保存します。
1. [!DNL Assets]ユーザーインターフェイスから、サンプルアセットをアップロードします。 透かしがフォントサイズやカラーなどと共に、上記手順で設定した位置に表示されます。

プログラムによって、または動的情報を使用してPDFドキュメントに透かしを追加するには、[Experience Managerドキュメントサービス](/help/forms/using/overview-aem-document-services.md)の機能を使用することを検討してください。

## ヒントと制限事項 {#tips-limitations}

* テキストベースの透かしのみがサポートされます。 [!UICONTROL 透かしを追加処理]の作成時に画像をアップロードできる場合でも、画像は透かしとして使用されません。
* 透かしはPNGおよびJPEGファイルのみがサポートされています。 その他のアセット形式は透かしにはなりません。
