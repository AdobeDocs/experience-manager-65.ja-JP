---
title: レンディションへの XMP の書き戻し
description: XMP の書き戻し機能を使用して、アセットのメタデータの変更を、そのアセットのすべてのレンディションまたは特定のレンディションに反映させる方法を学習します。
contentOwner: AG
role: Business Practitioner, Administrator
feature: メタデータ
exl-id: 82148ae5-37e9-4fc5-ada9-db3d91b29c33
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 57%

---

# レンディションへの XMP の書き戻し {#xmp-writeback-to-renditions}

[!DNL Adobe Experience Manager Assets]のこのXMPの書き戻し機能は、メタデータの変更を元のアセットのレンディションにレプリケートします。 アセット内から、またはアセットをアップロードする際に、アセットのメタデータを変更すると、その変更は最初にアセット階層のメタデータノードに保存されます。

XMP の書き戻し機能によって、メタデータの変更が、アセットのすべてのレンディションまたは特定のレンディションに反映されます。この機能は、`jcr`名前空間を使用するメタデータプロパティ（`dc:title`という名前のプロパティは書き戻されますが、`mytitle`という名前のプロパティは書き戻されません）のみを書き戻します。

「`Classic Leather`」というタイトルのアセットの「[!UICONTROL タイトル]」プロパティを「`Nylon`」に変更するシナリオについて考えます。

![メタデータ](assets/metadata.png)

この場合、[!DNL Experience Manager Assets]は、 **[!UICONTROL Title]**&#x200B;プロパティへの変更を、アセット階層に格納されたアセットメタデータ用の`dc:title`パラメーターに保存します。

![metadata_stored](assets/metadata_stored.png)

ただし、[!DNL Experience Manager Assets]は、メタデータの変更をアセットのレンディションに自動的に反映しません。 [XMPの書き戻しを有効にする方法](#enable-xmp-writeback)を参照してください。

## XMPの書き戻し{#enable-xmp-writeback}を有効にする

アセットのアップロード時にメタデータの変更をアセットのレンディションに反映させるには、設定マネージャーで「**[!UICONTROL Adobe CQ DAM Rendition Maker]**」の設定を変更します。

1. Configuration Manager を開くには、`https://[aem_server]:[port]/system/console/configMgr` にアクセスします。
1. 「**[!UICONTROL Adobe CQ DAM Rendition Maker]**」設定を開きます。
1. 「**[!UICONTROL Propagate XMP]**」オプションを選択し、変更を保存します。

   ![chlimage_1-135](assets/chlimage_1-346.png)

## 特定のレンディションに対する XMP の書き戻しの有効化 {#enabling-xmp-writeback-for-specific-renditions}

XMPの書き戻し機能でメタデータの変更が反映されるようにするには、これらのレンディションを、DAMメタデータの書き戻し]ワークフローのXMP書き戻しプロセスワークフローステップに指定します。 [!UICONTROL デフォルトでは、このステップには元のレンディションが設定されています。

XMP の書き戻し機能でメタデータをレンディションサムネール 140.100.png および 319.319.png に反映するには、次の手順を実行します。

1. Experience Managerインターフェイスで、**[!UICONTROL ツール]** / **[!UICONTROL ワークフロー]** / **[!UICONTROL モデル]**&#x200B;に移動します。
1. モデルページで、「**[!UICONTROL DAM メタデータの書き戻し]**」ワークフローモデルを開きます。
1. **[!UICONTROL DAM メタデータの書き戻し]**&#x200B;ページで、「**[!UICONTROL XMP の書き戻しプロセス]**」ステップを開きます。
1. [!UICONTROL ステップのプロパティ]ダイアログボックスで、「**[!UICONTROL プロセス]**」タブをクリックします。
1. 「**引数**」ボックスに`rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`を追加し、「**[!UICONTROL OK]**」をクリックします。

   ![step_properties](assets/step_properties.png)

1. 変更内容を保存します。
1. 新しい属性で[!DNL Dynamic Media]画像のピラミッドTIFFレンディションを再生成するには、**[!UICONTROL Dynamic Mediaプロセスの画像アセット]**&#x200B;ステップを[!UICONTROL DAMメタデータの書き戻し]ワークフローに追加します。

   PTIFF レンディションは、Dynamic Media Hybrid 実装でのみ、ローカルで作成および格納されます。

1. ワークフローを保存します。

メタデータの変更がアセットのレンディション thumbnail.140.100.png と thumbnail.319.319.png のみに反映され、他のレンディションには反映されなくなります。

>[!NOTE]
>
>64ビットLinuxでのXMPの書き戻しの問題については、[64ビットRedHat LinuxでXMPの書き戻しを有効にする方法](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html)を参照してください。
>
>サポートされるプラットフォームについては、[XMPメタデータの書き戻しの前提条件](/help/sites-deploying/technical-requirements.md#requirements-for-aem-assets-xmp-metadata-write-back)を参照してください。

## XMP メタデータのフィルタリング {#filtering-xmp-metadata}

[!DNL Experience Manager Assets] は、アセットの取り込み時にアセットバイナリから読み取られJCRに保存されるXMPメタデータのプロパティ/ノードのブロックリストと許可リストの両方のフィルタリングをサポートしています。

ブロックリストを使用したフィルターは、除外するよう指定されたプロパティを除く、すべての XMP メタデータプロパティを読み込みます。ただし、膨大な量の XMP メタデータ（例えば、10,000 個のプロパティを持つ 1,000 個のノード）を含む INDD ファイルなどのアセットタイプの場合、フィルタリングするノードの名前が必ずしも事前にわかるわけではありません。ブロックリストを使用したフィルタリングで、多数のXMPメタデータを含む多数のアセットを読み込める場合、監視キューの詰まりなど、安定性に関する問題が[!DNL Experience Manager]デプロイメントで発生する可能性があります。

この問題は、許可リストを介した XMP メタデータのフィルターで解決できます。このフィルターは、読み込む XMP プロパティを定義するので、許可リストに定義されていない XMP プロパティや不明な XMP プロパティは無視されます。下位互換性を確保するために、ブロックリストを使用するフィルターにこれらのプロパティの一部を追加できます。

>[!NOTE]
>
>フィルタリングは、アセットバイナリの XMP ソースから派生したプロパティに対してのみ機能します。EXIF 形式や IPTC 形式などの XMP 以外のソースから派生したプロパティについては、フィルタリングは機能しません。例えば、アセットの作成日は、`CreateDate` という名前のプロパティに EXIF TIFF 形式で格納されています。Experience Managerは、この値を`exif:DateTimeOriginal`という名前のメタデータフィールドに格納します。 この場合は XMP 以外のソースなので、このプロパティにはフィルタリングは機能しません。

1. Configuration Manager を開くには、`https://[aem_server]:[port]/system/console/configMgr` にアクセスします。
1. 「**[!UICONTROL Adobe CQ DAM XmpFilter]**」設定を開きます。
1. 許可リストを使用したフィルタリングを適用するには、「**[!UICONTROL Apply Allowlist to XMP Properties]**」を選択し、インポートするプロパティを「**[!UICONTROL Allowed XML Names for XMP filtering]**」ボックスで指定します。

   ![chlimage_1-136](assets/chlimage_1-347.png)

1. 許可リストを介してフィルタリングを適用した後、ブロックされたXMPプロパティを除外するには、「**[!UICONTROL Blocked XML Names for XMP filtering]**」ボックスにそれらを指定します。

   >[!NOTE]
   >
   >「**[!UICONTROL Apply Blocklist to XMP Properties]**」チェックボックスは、デフォルトでオンになっています。つまり、ブロックリストを使用したフィルタリングは、デフォルトで有効になっています。このようなフィルターを無効にするには、「**[!UICONTROL XMPのプロパティにを適用]**」オプションの選択をキャンセルしますブロックリスト。

1. 変更内容を保存します。
