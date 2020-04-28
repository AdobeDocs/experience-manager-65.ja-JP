---
title: レンディションへの XMP の書き戻し
description: XMP の書き戻し機能を使用して、アセットのメタデータの変更を、そのアセットのすべてのレンディションまたは特定のレンディションに反映させる方法を学習します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 33ab9845f7800c80a6beb5db06f3fadf582122d0

---


# レンディションへの XMP の書き戻し {#xmp-writeback-to-renditions}

Adobe Experience Manager（AEM）Assets のこの XMP の書き戻し機能は、アセットメタデータの変更をアセットのレンディションにレプリケートします。

AEM Assets内から、またはアセットのアップロード中に、アセットのメタデータを変更すると、変更はCrx-Deのアセットノード内に最初に保存されます。

XMPの書き戻し機能は、アセットのすべてのレンディションまたは特定のレンディションにメタデータの変更を反映します。

「`Classic Leather`」というタイトルのアセットの「タイトル」プロパティを「`Nylon`」に変更するシナリオについて考えます。

![メタデータ](assets/metadata.png)

この場合、AEM Assets ではこの「**タイトル**」プロパティへの変更が、アセット階層に格納されたアセットメタデータ用の `dc:title` パラメーターに保存されます。

![metadata_stored](assets/metadata_stored.png)

ただし、AEM Assets では、メタデータの変更はアセットのレンディションに自動的に反映されません。

XMPの書き戻し機能を使用すると、メタデータの変更をアセットのすべてのレンディションまたは特定のレンディションに反映できます。 ただし、変更はアセット階層の metadata ノード以下には保存されません。代わりに、この機能によって、レンディションのバイナリファイル内に変更内容が埋め込まれます。

## XMP の書き戻しの有効化 {#enabling-xmp-writeback}

アセットのアップロード時にメタデータの変更をアセットのレンディションに反映させるには、設定マネージャーで「**Adobe CQ DAM Rendition Maker**」の設定を変更します。

1. Configuration Manager を開くには、`https://[aem_server]:[port]/system/console/configMgr` にアクセスします。
1. 「**Adobe CQ DAM Rendition Maker**」設定を開きます。
1. 「**Propagate XMP**」オプションを選択し、変更を保存します。

   ![chlimage_1-135](assets/chlimage_1-346.png)

## 特定のレンディションに対する XMP の書き戻しの有効化 {#enabling-xmp-writeback-for-specific-renditions}

XMP の書き戻し機能によって、選択されたレンディションにメタデータの変更が反映されるようにするには、これらのレンディションを DAM メタデータ書き戻しワークフローの「XMP の書き戻しプロセスワークフロー」ステップに指定します。デフォルトでは、このステップには元のレンディションが設定されています。

XMP の書き戻し機能でメタデータをレンディションサムネール 140.100.png および 319.319.png に反映するには、次の手順を実行します。

1. AEM のロゴをタップまたはクリックし、**ツール**／**ワークフロー**／**モデル**&#x200B;に移動します。
1. モデルページで、「**DAM メタデータの書き戻し**」ワークフローモデルを開きます。
1. **DAM メタデータの書き戻し**&#x200B;ページで、「**XMP の書き戻しプロセス**」ステップを開きます。
1. ステップのプロパティダイアログボックスで、「**プロセス**」タブをタップまたはクリックします。
1. In the **Arguments** box, add `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`, andd then tap/click **OK**.

   ![step_properties](assets/step_properties.png)

1. 変更内容を保存します。
1. To regenerate the pyramid TIF renditions for Dynamic Media images with the new attributes, add the **Dynamic Media Process Image Assets** step to the DAM Metadata Writeback workflow.

   PTIFF レンディションは、Dynamic Media Hybrid 実装でのみ、ローカルで作成および格納されます。

1. ワークフローを保存します。

メタデータの変更がアセットのレンディション thumbnail.140.100.png と thumbnail.319.319.png のみに反映され、他のレンディションには反映されなくなります。

>[!NOTE]
>
>For XMP writeback issues in 64 bit Linux, see [How to enable XMP write-back on 64-bit RedHat Linux](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html).
>
>For more information about supported platforms, see [XMP metadata write-back prerequisites](/help/sites-deploying/technical-requirements.md#requirements-for-aem-assets-xmp-metadata-write-back).

## XMP メタデータのフィルタリング {#filtering-xmp-metadata}

AEM Assets は、アセットの取得時にアセットバイナリから読み取られて JCR に保存される XMP メタデータのプロパティ／ノードのブラックリストフィルターとホワイトリストフィルターの両方をサポートしています。

ブラックリストフィルターは、除外するよう指定されたプロパティを除く、すべての XMP メタデータプロパティを読み込みます。ただし、膨大な量の XMP メタデータ（例えば、10,000 個のプロパティを持つ 1,000 個のノード）を含む INDD ファイルなどのアセットタイプの場合、フィルタリングするノードの名前が必ずしも事前にわかるわけではありません。ブラックリストフィルターで、大量の XMP メタデータを含む膨大な量のアセットを読み込むと、監視キューの遅滞など、安定性に関する問題が、AEM インスタンス／クラスターで発生する可能性があります。

この問題は、XMP メタデータのホワイトリストフィルターで解決できます。このフィルターは、読み込む XMP プロパティを定義するので、そこに定義されていない XMP プロパティや不明な XMP プロパティは無視されます。これらのプロパティをいくつかブラックリストフィルターに追加することで、後方互換性を確保できます。

>[!NOTE]
>
>フィルタリングは、アセットバイナリの XMP ソースから派生したプロパティに対してのみ機能します。EXIF 形式や IPTC 形式などの XMP 以外のソースから派生したプロパティについては、フィルタリングは機能しません。例えば、アセットの作成日は、`CreateDate` という名前のプロパティに EXIF TIFF 形式で格納されています。AEM stores this value in a metadata field named `exif:DateTimeOriginal`. この場合は XMP 以外のソースなので、このプロパティにはフィルタリングは機能しません。

1. Configuration Manager を開くには、`https://[aem_server]:[port]/system/console/configMgr` にアクセスします。
1. 「**Adobe CQ DAM XmpFilter**」設定を開きます。
1. ホワイトリストフィルターを適用するには、「**Apply Whitelist to XMP Properties**」を選択し、「**Whitelisted XML Names for XMP filtering**」ボックスで読み込むプロパティを指定します。

   ![chlimage_1-136](assets/chlimage_1-347.png)

1. ホワイトリストフィルターを適用した後、ブラックリストに登録された XMP プロパティを除外するには、それらのプロパティを「**Blacklisted XML Names for XMP filtering**」ボックスに指定します。

   >[!NOTE]
   >
   >「**Apply Blacklist to XMP Properties**」チェックボックスは、デフォルトでオンになっています。つまり、ブラックリストフィルターは、デフォルトで有効になっています。ブラックリストフィルターを無効にするには、「**Apply Blacklist to XMP Properties**」オプションをオフにします。

1. 変更内容を保存します。
