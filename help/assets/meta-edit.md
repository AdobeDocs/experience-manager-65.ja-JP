---
title: メタデータの編集と追加
description: '[!DNL Adobe Experience Manager Assets]のアセットメタデータについて、アセットのメタデータを編集する様々な方法を説明します。'
contentOwner: AG
translation-type: tm+mt
source-git-commit: 90f9c0b60d4b0878f56eefea838154bb7627066d

---


# メタデータの編集と追加 {#how-to-edit-or-add-metadata}

メタデータは、検索可能なアセットに関する追加情報です。画像をアップロードすると自動的に抽出されます。既存のメタデータを編集したり、新しいメタデータプロパティを既存のフィールドに追加（例えば、メタデータフィールドが空白の場合など）したりすることができます。

Because organizations need controlled and reliable metadata vocabularies, [!DNL Experience Manager Assets] does not allow for ad-hoc adding of new metadata properties. 作成者は、アセットの新しいメタデータフィールドを追加することはできませんが、開発者は追加できます。See [create new metadata property for assets](meta-edit.md#editing-metadata-schema).

## Edit metadata for an asset {#editing-metadata-for-an-asset}

メタデータを編集するには、次の手順に従います。

1. 次のいずれかの操作をおこないます。

   * インターフェイス [!DNL Assets] から、アセットを選択し、ツールバーの「 **[!UICONTROL 表示のプロパティ]** 」をクリックします。
   * アセットのサムネールから、「**[!UICONTROL プロパティを表示]**」クイックアクションを選択します。
   * From the asset page, click **[!UICONTROL View Properties]** ![chlimage_1-168](assets/chlimage_1-168.png) from the toolbar.
   アセットページに、アセットのメタデータがすべて表示されます。メタデータは、アセットがExperience Managerにアップロード（取り込み）されると抽出されます。

   ![アセットのプロパティを選択して表示メタデータ](assets/asset-metadata.png)

   *図：アセットのプロパティページでメタデータを編集または追加します。*

1. Make edits to the metadata under the various tabs, as required, and when completed, click **[!UICONTROL Save]** from the toolbar to save your changes. Click **[!UICONTROL Close]** to return to the Assets web interface.

   >[!NOTE]
   >
   >テキストフィールドが空の場合、現在設定されているメタデータはありません。フィールドに値を入力して保存すると、そのメタデータプロパティを追加できます。

アセットのメタデータへの変更内容は、XMP データの一部として元のバイナリに書き戻されます。これは、Experience Managerメタデータの書き戻しワークフローを通じて行われます。 既存のプロパティ（`dc:title` など）への変更は上書きされ、新しく作成されたプロパティ（`cq:tags` などのカスタムプロパティを含む）はスキーマとともに追加されます。

XMP write-back is supported and enabled for the platforms and file formats described in [technical requirements.](/help/sites-deploying/technical-requirements.md)

## Edit metadata schema {#editing-metadata-schema}

For details on how to edit metadata schema, see [Edit metadata schema forms](metadata-schemas.md#edit-metadata-schema-forms).

## Experience Managerでのカスタム名前空間の登録 {#registering-a-custom-namespace-within-aem}

Experience Manager内で独自の名前空間を追加できます。 cq、jcr、sling など事前に定義された名前空間があるように、リポジトリメタデータと xml 処理用の名前空間を設定できます。

1. Go to the node type administration page `https:[aem_server]:[port]/crx/explorer/nodetypes/index.jsp`.
1. Click **[!UICONTROL Namespaces]** at the top of the page. ウィンドウに名前空間管理ページが表示されます。

1. To add a namespace, click **[!UICONTROL New]** at the bottom.
1. Specify a custom namespace in the XML namespace convention (Specify the id in the form of a URI and an associated prefix for the id), and click **[!UICONTROL Save]**.
