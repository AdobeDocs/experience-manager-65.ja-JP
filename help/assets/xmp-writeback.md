---
title: レンディションへの XMP の書き戻し
description: XMP の書き戻し機能を使用して、アセットのメタデータの変更を、そのアセットのすべてのレンディションまたは特定のレンディションに反映させる方法を学習します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# レンディションへの XMP の書き戻し {#xmp-writeback-to-renditions}

Adobe Experience Manager（AEM）Assets のこの XMP の書き戻し機能は、アセットメタデータの変更をアセットのレンディションにレプリケートします。

AEM Assets内から、またはアセットのアップロード中に、アセットのメタデータを変更すると、変更は最初にCrx-Deのアセットノード内に保存されます。

XMPの書き戻し機能は、アセットのすべてのレンディションまたは特定のレンディションにメタデータの変更を反映します。

Consider a scenario where you modify the Title property of the asset titled `Classic Leather` to `Nylon`.

![メタデータ](assets/metadata.png)

この場合、AEM Assets ではこの「**タイトル**」プロパティへの変更が、アセット階層に格納されたアセットメタデータ用の `dc:title` パラメーターに保存されます。

![metadata_stored](assets/metadata_stored.png)

ただし、AEM Assets では、メタデータの変更はアセットのレンディションに自動的に反映されません。

XMPの書き戻し機能を使用すると、メタデータの変更をアセットのすべてのレンディションまたは特定のレンディションに反映できます。 ただし、変更はアセット階層の metadata ノード以下には保存されません。代わりに、この機能によって、レンディションのバイナリファイル内に変更内容が埋め込まれます。

## XMP の書き戻しの有効化 {#enabling-xmp-writeback}

To enable the metadata changes to be propagated to the renditions of the asset when uploading it, modify the **Adobe CQ DAM Rendition Maker** configuration in Configuration Manager.

1. Configuration Managerを開くには、にアクセスしま `https://[aem_server]:[port]/system/console/configMgr`す。
1. Open the **Adobe CQ DAM Rendition Maker** configuration.
1. Select the **Propagate XMP** option, and then save the changes.

   ![chlimage_1-135](assets/chlimage_1-346.png)

## 特定のレンディションに対する XMP の書き戻しの有効化 {#enabling-xmp-writeback-for-specific-renditions}

XMP の書き戻し機能によって、選択されたレンディションにメタデータの変更が反映されるようにするには、これらのレンディションを DAM メタデータ書き戻しワークフローの「XMP の書き戻しプロセスワークフロー」ステップに指定します。デフォルトでは、このステップには元のレンディションが設定されています。

XMP の書き戻し機能でメタデータをレンディションサムネール 140.100.png および 319.319.png に反映するには、次の手順を実行します。

1. Tap/click the AEM logo, and then navigate to **Tools** > **Workflow** > **Models**.
1. From the Models page, open the **DAM Metadata Writeback** workflow model.
1. In the **DAM Metadata Writeback** properties page, open the **XMP Writeback Process** step.
1. In the Step Properties dialog box, tap/click the **Process** tab.
1. In the **Arguments** box, add `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`, andd then tap/click **OK**.

   ![step_properties](assets/step_properties.png)

1. 変更内容を保存します。
1. To regenerate the pyramid TIF renditions for Dynamic Media images with the new attributes, add the **Dynamic Media Process Image Assets** step to the DAM Metadata Writeback workflow.

   PTIFF レンディションは、Dynamic Media ハイブリッド実装でのみ、ローカルで作成および格納されます。

1. ワークフローを保存します。

メタデータの変更は、アセットのレンディションレンディションthumbnail.140.100.pngおよびthumbnail.319.319.pngに反映され、他のレンディションレンディションレンディションには反映されません。

>[!NOTE]
>
>For XMP writeback issues in 64 bit Linux, see [How to enable XMP write-back on 64-bit RedHat Linux](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html).
>
>For more information about supported platforms, see [XMP metadata write-back prerequisites](/help/sites-deploying/technical-requirements.md#requirements-for-aem-assets-xmp-metadata-write-back).

## XMP メタデータのフィルタリング {#filtering-xmp-metadata}

AEM Assetsは、アセットバイナリから読み取られ、アセットの取り込み時にJCRに保存されるXMPメタデータのプロパティ/ノードのブラックリストフィルターとホワイトリストフィルターの両方をサポートしています。

ブラックリストフィルターは、除外するよう指定されたプロパティを除く、すべての XMP メタデータプロパティを読み込みます。ただし、膨大な量の XMP メタデータ（例えば、10,000 個のプロパティを持つ 1,000 個のノード）を含む INDD ファイルなどのアセットタイプの場合、フィルタリングするノードの名前が必ずしも事前にわかるわけではありません。ブラックリストフィルターで、大量の XMP メタデータを含む膨大な量のアセットを読み込むと、監視キューの遅滞など、安定性に関する問題が、AEM インスタンス／クラスターで発生する可能性があります。

この問題は、XMP メタデータのホワイトリストフィルターで解決できます。このフィルターは、読み込む XMP プロパティを定義するので、そこに定義されていない XMP プロパティや不明な XMP プロパティは無視されます。これらのプロパティをいくつかブラックリストフィルターに追加することで、後方互換性を確保できます。

>[!NOTE]
>
>フィルタリングは、アセットバイナリの XMP ソースから派生したプロパティに対してのみ機能します。EXIF 形式や IPTC 形式などの XMP 以外のソースから派生したプロパティについては、フィルタリングは機能しません。例えば、アセットの作成日は、`CreateDate` という名前のプロパティに EXIF TIFF 形式で格納されています。AEM では、この値を `exif:DateTimeOriginal`.という名前のメタデータフィールドに格納します。この場合は XMP 以外のソースなので、このプロパティにはフィルタリングは機能しません。

1. Configuration Managerを開くには、にアクセスしま `https://[aem_server]:[port]/system/console/configMgr`す。
1. Open the **Adobe CQ DAM XmpFilter** configuration.
1. To apply whitelist filtering, select **Apply Whitelist to XMP Properties**, and specify the properties to be imported in the **Whitelisted XML Names for XMP filtering** box.

   ![chlimage_1-136](assets/chlimage_1-347.png)

1. To filter out blacklisted XMP properties after applying whitelist filtering, specify them in the **Blacklisted XML Names for XMP filtering** box.

   >[!NOTE]
   >
   >「**Apply Blacklist to XMP Properties**」チェックボックスは、デフォルトでオンになっています。つまり、ブラックリストフィルターは、デフォルトで有効になっています。To disable blacklist filtering, unselect the **Apply Blacklist to XMP Properties** option.

1. 変更内容を保存します。
