---
title: レンディションへの XMP の書き戻し
description: XMP の書き戻し機能を使用して、アセットのメタデータの変更を、そのアセットのすべてのレンディションまたは特定のレンディションに反映させる方法を学習します。
contentOwner: AG
role: User, Admin
feature: Metadata
exl-id: 82148ae5-37e9-4fc5-ada9-db3d91b29c33
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: ht
source-wordcount: '784'
ht-degree: 100%

---

# レンディションへの XMP の書き戻し {#xmp-writeback-to-renditions}

[!DNL Adobe Experience Manager Assets] の XMP の書き戻し機能では、メタデータの変更内容を元のアセットのレンディションに複製します。 アセット内からアセットのメタデータを変更すると、またはアセットをアップロードすると、変更内容はまずアセット階層のメタデータノードに保存されます。

XMP の書き戻し機能によって、メタデータの変更が、アセットのすべてのレンディションまたは特定のレンディションに反映されます。この機能は、`jcr` 名前空間を使用するメタデータプロパティのみを書き戻します。つまり、`dc:title` という名前のプロパティは書き戻されますが、`mytitle` という名前のプロパティは書き戻されません。

「`Classic Leather`」というタイトルのアセットの「[!UICONTROL タイトル]」プロパティを「`Nylon`」に変更するシナリオについて考えます。

![メタデータ](assets/metadata.png)

この場合、[!DNL Experience Manager Assets] ではこの「**[!UICONTROL タイトル]**」プロパティへの変更が、アセット階層に格納されたアセットメタデータ用の `dc:title` パラメーターに保存されます。

![metadata_stored](assets/metadata_stored.png)

ただし、[!DNL Experience Manager Assets] では、メタデータの変更はアセットのレンディションに自動的に反映されません。[XMP の書き戻しを有効にする方法](#enable-xmp-writeback)を参照してください。

## XMP の書き戻しを有効にする {#enable-xmp-writeback}

アセットのアップロード時にメタデータの変更をアセットのレンディションに反映させるには、設定マネージャーで「**[!UICONTROL Adobe CQ DAM Rendition Maker]**」の設定を変更します。

1. Configuration Manager を開くには、`https://[aem_server]:[port]/system/console/configMgr` にアクセスします。
1. 「**[!UICONTROL Adobe CQ DAM Rendition Maker]**」設定を開きます。
1. 「**[!UICONTROL Propagate XMP]**」オプションを選択し、変更を保存します。

   ![chlimage_1-135](assets/chlimage_1-346.png)

## 特定のレンディションに対する XMP の書き戻しの有効化 {#enabling-xmp-writeback-for-specific-renditions}

XMP の書き戻し機能によって、選択されたレンディションにメタデータの変更が反映されるようにするには、これらのレンディションを [!UICONTROL DAM メタデータ書き戻し]ワークフローの「XMP の書き戻しプロセス」ワークフロー手順に指定します。デフォルトでは、このステップには元のレンディションが設定されています。

XMP の書き戻し機能でメタデータをレンディションサムネール 140.100.png および 319.319.png に反映するには、次の手順を実行します。

1. Experience Manager インターフェイスで、**[!UICONTROL ツール]**／**[!UICONTROL ワークフロー]**／**[!UICONTROL モデル]**&#x200B;に移動します。
1. モデルページで、「**[!UICONTROL DAM メタデータの書き戻し]**」ワークフローモデルを開きます。
1. **[!UICONTROL DAM メタデータの書き戻し]**&#x200B;ページで、「**[!UICONTROL XMP の書き戻しプロセス]**」ステップを開きます。
1. [!UICONTROL 手順のプロパティ]ダイアログボックスで、「**[!UICONTROL プロセス]**」タブをクリックします。
1. 「**引数**」ボックスに「`rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`」を追加し、「**[!UICONTROL OK]**」をクリックします。

   ![step_properties](assets/step_properties.png)

1. 変更内容を保存します。
1. 新しい属性で [!DNL Dynamic Media] 画像のピラミッド TIFF レンディションを再生成するには、「**[!UICONTROL Dynamic Media プロセスの画像アセット]**」手順を「[!UICONTROL DAM メタデータ書き戻し]」ワークフローに追加します。

   PTIFF レンディションは、Dynamic Media Hybrid 実装でのみ、ローカルで作成および格納されます。

1. ワークフローを保存します。

メタデータの変更がアセットのレンディション thumbnail.140.100.png と thumbnail.319.319.png のみに反映され、他のレンディションには反映されなくなります。

>[!NOTE]
>
>64 ビット Linux での XMP の書き戻しに関する問題については、[64 ビット RedHat Linux で XMP の書き戻しを有効にする方法](https://helpx.adobe.com/jp/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html)を参照してください。
>
>サポートしているプラットフォームについては、[XMP メタデータの書き戻しの前提条件](/help/sites-deploying/technical-requirements.md#requirements-for-aem-assets-xmp-metadata-write-back)を参照してください。

## XMP メタデータのフィルタリング {#filtering-xmp-metadata}

[!DNL Experience Manager Assets] では、アセットの取り込み時にアセットバイナリから読み取られて JCR に保存される XMP メタデータに対して、ブロックリストと許可リストの両方で、プロパティやノードのフィルタリングをサポートしています。

ブロックリストを使用したフィルターは、除外するよう指定されたプロパティを除く、すべての XMP メタデータプロパティを読み込みます。ただし、膨大な量の XMP メタデータ（例えば、10,000 個のプロパティを持つ 1,000 個のノード）を含む INDD ファイルなどのアセットタイプの場合、フィルタリングするノードの名前が必ずしも事前にわかるわけではありません。ブロックリストを使用したフィルタリングで、大量の XMP メタデータを含む膨大な量のアセットをインポートできるようにすると、監視キューの遅滞など、安定性に関する問題が [!DNL Experience Manager] デプロイメントで発生する可能性があります。

許可リストを使用した XMP メタデータのフィルタリングでは、インポートする XMP プロパティを定義できるので、この問題を解決できます。許可リストに定義されていない XMP プロパティや不明な XMP プロパティは無視されます。下位互換性を確保するために、ブロックリストを使用するフィルターにこれらのプロパティの一部を追加できます。

>[!NOTE]
>
>フィルタリングは、アセットバイナリの XMP ソースから派生したプロパティに対してのみ機能します。EXIF 形式や IPTC 形式などの XMP 以外のソースから派生したプロパティについては、フィルタリングは機能しません。例えば、アセットの作成日は、`CreateDate` という名前のプロパティに EXIF TIFF 形式で格納されています。Experience Manager は、この値を `exif:DateTimeOriginal` という名前のメタデータフィールドに格納します。この場合は XMP 以外のソースなので、このプロパティにはフィルタリングは機能しません。

1. Configuration Manager を開くには、`https://[aem_server]:[port]/system/console/configMgr` にアクセスします。
1. 「**[!UICONTROL Adobe CQ DAM XmpFilter]**」設定を開きます。
1. 許可リストを使用したフィルタリングを適用するには、「**[!UICONTROL Apply Allowlist to XMP Properties]**」を選択し、インポートするプロパティを「**[!UICONTROL Allowed XML Names for XMP filtering]**」ボックスで指定します。

   ![chlimage_1-136](assets/chlimage_1-347.png)

1. 許可リストでフィルターを適用した後で、ブロックされた XMP プロパティをフィルターで除外するには、それらのプロパティを「**[!UICONTROL XMP フィルタリングでブロックされた XML 名]** 」ボックスで指定します。

   >[!NOTE]
   >
   >「**[!UICONTROL Apply Blocklist to XMP Properties]**」チェックボックスは、デフォルトでオンになっています。つまり、ブロックリストを使用したフィルタリングは、デフォルトで有効になっています。こうしたフィルタリングを無効にするには、「 **[!UICONTROL XMP プロパティにブロックリストを適用]** 」オプションの選択をキャンセルします。

1. 変更を保存します。
